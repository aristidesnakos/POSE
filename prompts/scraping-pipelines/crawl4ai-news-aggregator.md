# Multi-Source News Aggregator

## Metadata
- **Category**: scraping-pipelines
- **Complexity**: Complex (800+ LOC)
- **Output Type**: Python script
- **Key Skills Tested**: Crawl4AI multi-URL crawling, LLM extraction across different HTML structures, deduplication, date normalization
- **Dependencies**: crawl4ai, pydantic, asyncio

## Prompt

> Using Crawl4AI, write a Python script that aggregates tech news from 3 different sources into a unified feed. The script should:
>
> 1. Scrape the front page of these 3 sources:
>    - https://news.ycombinator.com (Hacker News)
>    - https://lobste.rs (Lobsters)
>    - https://www.techmeme.com (Techmeme)
> 2. Use Crawl4AI's AsyncWebCrawler to fetch all 3 pages concurrently
> 3. Extract from each story: title, source URL, source name, and a brief summary if available
> 4. Normalize the data into a unified Pydantic model:
>    ```python
>    class NewsItem(BaseModel):
>        title: str
>        url: str
>        source: str  # "hackernews", "lobsters", or "techmeme"
>        summary: str = ""
>        scraped_at: str  # ISO 8601 timestamp
>    ```
> 5. Deduplicate stories that appear on multiple sources (same URL or very similar titles)
> 6. Sort the combined feed by source, then alphabetically by title
> 7. Output as JSON to stdout
> 8. Print a summary: "Aggregated X unique stories from 3 sources (Y duplicates removed)"
>
> Use async/await with concurrent crawling. The script should be runnable with `python scrape_news.py`.

## Reference Materials

None — text-only prompt. All target sites are publicly accessible.

## Evaluation Checklist

- [ ] Script runs without errors on first attempt
- [ ] Uses Crawl4AI's AsyncWebCrawler (not requests/BeautifulSoup)
- [ ] Fetches all 3 sources (not just 1 or 2)
- [ ] Concurrent crawling (asyncio.gather or similar, not sequential)
- [ ] Extracts story titles and URLs from each source
- [ ] All output items match the Pydantic model schema
- [ ] Source field correctly identifies where each story came from
- [ ] Deduplication logic exists (removes stories with same URL or very similar title)
- [ ] Output is sorted as specified
- [ ] Outputs valid JSON with summary line
- [ ] Includes `scraped_at` timestamp in ISO 8601 format

## Notes for Evaluators

**Setup**: `pip install crawl4ai pydantic` before running.

**Common failure modes**:
- Each site has a completely different HTML structure. The model needs to handle this — either with site-specific extraction logic or LLM-based extraction
- Techmeme may require JS rendering (it loads content dynamically). If the model doesn't account for this, the Techmeme results may be empty
- Deduplication is the hardest part. URL-based dedup is straightforward; title-based dedup requires fuzzy matching, which models often skip
- Concurrent fetching: models may write sequential code despite the prompt asking for concurrency

**What "close enough" means**: If the script scrapes at least 2 of 3 sources successfully, extracts real stories, and makes an attempt at deduplication, it's a reasonable pass. Perfect deduplication across different headline phrasings is hard — any attempt counts.
