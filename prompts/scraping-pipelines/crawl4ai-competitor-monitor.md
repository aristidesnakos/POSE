# Competitor Content Monitor

## Metadata
- **Category**: scraping-pipelines
- **Complexity**: Complex (800+ LOC)
- **Output Type**: Python script
- **Key Skills Tested**: Crawl4AI multi-URL crawling, content extraction, date parsing, diff/comparison logic, report generation
- **Dependencies**: crawl4ai, pydantic, asyncio, datetime

## Prompt

> Using Crawl4AI, write a Python script that monitors competitor blogs for new content. The script should:
>
> 1. Accept a list of blog URLs and a "since" date as configuration at the top of the script:
>    ```python
>    COMPETITOR_BLOGS = [
>        "https://blog.anthropic.com",
>        "https://openai.com/blog",
>        "https://blog.google/technology/ai/"
>    ]
>    SINCE_DATE = "2025-01-01"  # Only show posts after this date
>    ```
> 2. Use Crawl4AI's AsyncWebCrawler to scrape each blog concurrently
> 3. Extract from each blog post: title, URL, published date, and a one-line summary (first ~150 chars of content)
> 4. Filter to only show posts published after SINCE_DATE
> 5. Use this Pydantic model:
>    ```python
>    class BlogPost(BaseModel):
>        title: str
>        url: str
>        source: str
>        published_date: str  # ISO 8601
>        summary: str
>    ```
> 6. Generate a markdown-formatted report to stdout organized by source:
>    ```
>    # Competitor Content Report
>    ## Since: 2025-01-01
>
>    ### Anthropic Blog (X new posts)
>    - **[Post Title](url)** — 2025-02-15
>      Summary text here...
>
>    ### OpenAI Blog (Y new posts)
>    ...
>
>    ## Summary
>    Total: X new posts across Y sources
>    ```
> 7. Also save the raw data as `competitor_report.json`
> 8. Handle cases where a blog is unreachable (log a warning, continue with others)
>
> Use async/await with concurrent crawling. The script should be runnable with `python monitor_competitors.py`.

## Reference Materials

None — text-only prompt. Target sites are public tech company blogs.

## Evaluation Checklist

- [ ] Script runs without errors on first attempt
- [ ] Uses Crawl4AI's AsyncWebCrawler
- [ ] Fetches all 3 blog sources concurrently
- [ ] Extracts post titles and URLs from each blog
- [ ] Extracts or approximates publish dates
- [ ] Filters posts by the SINCE_DATE threshold
- [ ] Generates a markdown-formatted report to stdout
- [ ] Report is organized by source with post counts
- [ ] Saves raw data as `competitor_report.json` with valid JSON
- [ ] Handles unreachable blogs gracefully (warning, not crash)
- [ ] Handles blogs with no new posts since the date (shows "0 new posts", not crash)

## Notes for Evaluators

**Setup**: `pip install crawl4ai pydantic` before running.

**Important context**: These are real company blogs with different structures. This is intentionally harder than scraping a sandbox site. The evaluation tests whether the AI can handle real-world HTML diversity.

**Common failure modes**:
- Each blog has a completely different HTML structure. The model must either use LLM-based extraction or write site-specific parsing
- Date parsing is notoriously unreliable across blogs. Some use "February 15, 2025", others use "2025-02-15", others use relative dates ("3 days ago")
- Blog.google may require JS rendering — Crawl4AI handles this but the model needs to enable it
- OpenAI's blog may have pagination or infinite scroll — the model should at least attempt the front page
- Models often forget the "handle unreachable blog" requirement — test by temporarily adding a fake URL to the config

**What "close enough" means**: If the script successfully scrapes at least 2 of 3 blogs, extracts real post titles/URLs, makes an attempt at date filtering, and generates a readable report, it's a pass. Perfect date extraction from all 3 blogs on the first shot would be impressive.
