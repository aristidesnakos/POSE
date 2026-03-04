# Real Estate Listings Scraper

## Metadata
- **Category**: scraping-pipelines
- **Complexity**: Medium (200-800 LOC)
- **Output Type**: Python script
- **Key Skills Tested**: Crawl4AI LLM extraction, messy data normalization, structured output, handling varied formats
- **Dependencies**: crawl4ai, pydantic, asyncio

## Prompt

> Using Crawl4AI, write a Python script that scrapes property listings from https://www.scrapethissite.com/pages/listings/ (a safe scraping sandbox). The script should:
>
> 1. Use Crawl4AI's AsyncWebCrawler to fetch the listings page
> 2. Extract for each property: name, city, state, and any numeric data available (population, area, etc.)
> 3. Define a Pydantic model:
>    ```python
>    class PropertyListing(BaseModel):
>        name: str
>        city: str = "Not specified"
>        state: str = "Not specified"
>        population: Optional[int] = None
>        area: Optional[float] = None
>    ```
> 4. Clean and normalize the data:
>    - Strip extra whitespace from all text fields
>    - Convert numeric strings to proper int/float types
>    - Handle entries with missing or malformed data without crashing
> 5. Output as both:
>    - A JSON file (`listings.json`)
>    - A formatted table printed to stdout (aligned columns)
> 6. Print summary: "Found X listings across Y states"
>
> Use async/await. The script should be runnable with `python scrape_listings.py`.

## Reference Materials

None — text-only prompt. Target site is scrapethissite.com, a purpose-built scraping sandbox.

## Evaluation Checklist

- [ ] Script runs without errors on first attempt
- [ ] Uses Crawl4AI's AsyncWebCrawler
- [ ] Extracts listing data with all specified fields
- [ ] Uses Pydantic model for validation
- [ ] Text fields are clean (no excess whitespace, no HTML artifacts)
- [ ] Numeric fields are actual numbers (int/float), not strings
- [ ] Handles missing/malformed data gracefully (None or default, not crash)
- [ ] Outputs a JSON file (`listings.json`) with valid JSON
- [ ] Prints a formatted table to stdout with aligned columns
- [ ] Prints summary with listing count and state count

## Notes for Evaluators

**Setup**: `pip install crawl4ai pydantic` before running.

**Note on target site**: scrapethissite.com may have different data than real estate (it uses country/city data as a sandbox). The evaluation tests the same skills regardless — structured extraction, normalization, dual output format. If the model adapts the Pydantic model to match the actual site data, that shows good judgment.

**Common failure modes**:
- The site's HTML may have inconsistent whitespace — watch for text fields with `\n` or `\t` in output
- Numeric conversion: some entries may have commas in numbers (e.g., "1,234,567") — check if the model handles this
- Formatted table printing: models sometimes produce ugly tables. Look for any attempt at alignment (f-strings, tabulate, etc.)
- Some models will try to scrape a real real estate site instead of the sandbox — this is a fail

**What "close enough" means**: If the script extracts structured data from the sandbox site, outputs clean JSON, and prints a readable table, it's a pass. The exact Pydantic model fields can adapt to what the site actually provides.
