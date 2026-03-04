# E-commerce Price Monitor

## Metadata
- **Category**: scraping-pipelines
- **Complexity**: Medium (200-800 LOC)
- **Output Type**: Python script
- **Key Skills Tested**: Crawl4AI JS rendering, CSS selector extraction, data normalization, CSV output
- **Dependencies**: crawl4ai, pydantic, asyncio, csv

## Prompt

> Using Crawl4AI, write a Python script that scrapes product listings from https://books.toscrape.com (a safe, legal scraping sandbox). The script should:
>
> 1. Use Crawl4AI's AsyncWebCrawler to scrape the first 3 pages of the book catalog
> 2. For each product, extract: title, price, star rating (as a number 1-5), and availability status
> 3. Use Crawl4AI's CSS extraction strategy with a schema to structure the data
> 4. Normalize prices to float values (strip currency symbols)
> 5. Convert star ratings from text ("Three") to numbers (3)
> 6. Output results as a CSV file called `products.csv` with headers: title, price, rating, in_stock
> 7. Print a summary line at the end: "Scraped X products from Y pages"
>
> Use async/await throughout. The script should be runnable with `python scrape_prices.py`.

## Reference Materials

None — text-only prompt. Target site is books.toscrape.com, a purpose-built scraping sandbox (safe to scrape, always available).

## Evaluation Checklist

- [ ] Script runs without errors on first attempt (`python scrape_prices.py`)
- [ ] Uses Crawl4AI's AsyncWebCrawler (not requests/BeautifulSoup/Selenium)
- [ ] Scrapes multiple pages (not just page 1)
- [ ] Extracts all 4 fields: title, price, rating, availability
- [ ] Prices are numeric floats (e.g., 51.77 not "£51.77")
- [ ] Star ratings are integers 1-5 (e.g., 3 not "Three")
- [ ] Outputs a valid CSV file with correct headers
- [ ] CSV is parseable by standard tools (`python -c "import csv; list(csv.reader(open('products.csv')))"`)
- [ ] Prints summary line with product count and page count
- [ ] Handles edge cases (books with long titles, missing ratings)

## Notes for Evaluators

**Setup**: `pip install crawl4ai` before running. This site does not require JS rendering, so Crawl4AI's basic mode should work.

**Common failure modes**:
- Model may not know books.toscrape.com's HTML structure — look for CSS selectors targeting `.product_pod` or similar
- Star rating conversion is a common stumbling point. The site uses class names like `star-rating Three` — the model needs to map these
- Price normalization: some models will leave the `£` symbol or fail to handle the `Â£` encoding
- Pagination: the site uses `/catalogue/page-2.html` format — check if the model discovers this

**What "close enough" means**: If products.csv contains real product data with normalized prices and numeric ratings from multiple pages, it's a pass. Minor issues like title truncation or one missed product per page are acceptable.
