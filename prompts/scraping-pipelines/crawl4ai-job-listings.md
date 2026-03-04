# Job Listings Scraper

## Metadata
- **Category**: scraping-pipelines
- **Complexity**: Medium (200-800 LOC)
- **Output Type**: Python script
- **Key Skills Tested**: Crawl4AI async crawling, structured data extraction with LLM, JSON output, pagination handling
- **Dependencies**: crawl4ai, pydantic, asyncio

## Prompt

> Using Crawl4AI, write a Python script that scrapes software engineering job listings from https://news.ycombinator.com/jobs. The script should:
>
> 1. Use Crawl4AI's AsyncWebCrawler to fetch the page
> 2. Extract structured data for each job listing: title, company name, location (if available), and posted date
> 3. Use Crawl4AI's LLM extraction strategy with a Pydantic model to structure the data
> 4. Handle pagination — scrape at least the first 3 pages of results
> 5. Output the results as a JSON array to stdout
> 6. Include error handling for network failures and missing fields
>
> The Pydantic model should be:
> ```python
> class JobListing(BaseModel):
>     title: str
>     company: str
>     location: str = "Not specified"
>     posted_date: str
> ```
>
> Use async/await throughout. The script should be runnable with `python scrape_jobs.py`.

## Reference Materials

None — text-only prompt. Target site is Hacker News jobs page (publicly accessible, no auth required).

## Evaluation Checklist

- [ ] Script runs without errors on first attempt (`python scrape_jobs.py`)
- [ ] Uses Crawl4AI's AsyncWebCrawler (not requests/BeautifulSoup/Selenium)
- [ ] Extracts job listings with all specified fields (title, company, location, posted_date)
- [ ] Uses a Pydantic model for data validation
- [ ] Handles pagination (fetches more than one page of results)
- [ ] Outputs valid JSON to stdout (parseable by `python -m json.tool`)
- [ ] Handles missing fields gracefully (defaults, not crashes)
- [ ] Includes error handling for network failures (try/except, retries, or timeout)
- [ ] Uses async/await pattern correctly
- [ ] Script is runnable as-is (no missing imports, no placeholder API keys without instructions)

## Notes for Evaluators

**Setup**: `pip install crawl4ai pydantic` before running. Crawl4AI may also need `playwright install` for browser setup.

**Common failure modes**:
- Model may use `requests` or `BeautifulSoup` instead of Crawl4AI — this is a fail on the Crawl4AI checklist item
- Model may hardcode URLs instead of implementing pagination logic
- LLM extraction strategy requires an API key (OpenAI/Anthropic) — check if the model mentions this or leaves it as a gap
- HN jobs page structure is simple HTML — if the model overcomplicates with JS rendering, that's not wrong but worth noting

**What "close enough" means**: If the script runs, uses Crawl4AI, and outputs structured JSON with job data, that's a pass even if the pagination approach is basic (e.g., just appending `?p=2` to the URL).
