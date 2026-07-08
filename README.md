# website-brochure-maker-
Website Brochure Maker

A small Python tool that scrapes a company's website and uses OpenAI's models to automatically generate a short marketing brochure about the company — covering things like culture, customers, and careers — in Markdown format.

How It Works


You give it a company's homepage URL.
scraper.py fetches the page and pulls out all the links (fetch_website_links) and the page's text content (fetch_website_contents).
The links are sent to an OpenAI model (gpt-5-nano), which picks out the ones most relevant to a brochure — About, Careers, Company pages, etc. — and returns them as JSON.
The scraped content plus those relevant links are sent to a second model (gpt-4.1-mini), which writes a brochure in Markdown, streamed live into the notebook.


Project Structure

.
├── mainn.ipynb     # Main notebook — run this to generate a brochure
├── scraper.py      # Helper functions for scraping links & page content
└── .env            # Your API key (not committed to git)

Setup

1. Clone the repo

bashgit clone <your-repo-url>
cd <your-repo-name>

2. Install dependencies

bashpip install openai python-dotenv beautifulsoup4 requests jupyter
3. Add your OpenAI API key

Create a .env file in the project root:

OPENAI_API_KEY=sk-proj-your-key-here
4. Run it

Open mainn.ipynb in Jupyter and run the cell. You'll be prompted to enter a website URL, and the brochure will stream into the notebook output as Markdown.

Example

Input: https://wikimediafoundation.org/

Output: A brochure covering the Wikimedia Foundation's mission, key projects (Wikipedia, Wikimedia Commons, etc.), community, careers, and donation info — generated automatically from the site's own content.

Notes / Limitations


Only fetches the first 2,000 characters of each page's text (kept simple on purpose).
Parses each page twice (once for links, once for content) — fine for a small project, but worth optimizing if scaling up.
Some websites block scraping via robots.txt or bot detection — this tool doesn't check robots.txt, so use responsibly and only on sites you have permission to scrape.
Requires an OpenAI API key with access to gpt-5-nano and gpt-4.1-mini (or swap in whichever models you have access to).

