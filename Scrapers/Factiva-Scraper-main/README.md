# Factiva Scraper

Scrapes articles and saves data in an SQLite database.

![](ss.jpg)

### Instructions

-   Install Python if not installed already (<https://python.org/>).
-   Install requirements `pip install -r requirements.txt`.
-   Edit `conf.ini` with all your juicy details.
-   Start browser `/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --remote-debugging-port=9222 --user-data-dir="~/ChromeProfile"`
-   Disable images `chrome://settings/content/images` and select  `Don't allow sites to show images`.
-   Log into the website <https://global-factiva-com.ezproxy.cul.columbia.edu>.
-   Search for the articles you need <https://global-factiva-com.ezproxy.cul.columbia.edu/sb/default.aspx?NAPC=S>
-   Run it `python run.py` (see arguments to run sections).

### Arguments

    usage: run.py [-h] [-a] [-b]

    optional arguments:
      -h, --help  show this help message and exit
      -a, --one   Scraper A - Get urls from search page
      -b, --two   Scraper A - Get article text from urls


