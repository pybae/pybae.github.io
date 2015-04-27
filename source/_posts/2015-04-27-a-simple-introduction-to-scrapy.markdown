---
layout: post
title: "A simple introduction to Scrapy"
date: 2015-04-27 12:36:39 -0500
comments: true
categories:
---

### Introduction

[Scrapy](http://scrapy.org/) is a popular web scraper in Python 2.7.8. Python 3 is not officially supported, although there have been movements for this to port the language. In this article, I'll be going through some of the main features of Scrapy and sharing how I used it in [our project](http://freespirits.me). But first, let's define some common terminology used.

A spider (or crawler) refers to the component that navigates thorough a website. For example, one such Spider could be clicking on all possible links from the starting positions of the spider. In Scrapy, we can define Spiders from the lib `scrapy.contrib.spiders`

A parser is used to refer to software that parses some form of data into another. Common examples include a JSON parser, XML parser, and so forth. In this case, we're concerned with HTML parsers. I'll be using [Beautiful Soup 4](http://www.crummy.com/software/BeautifulSoup/bs4/doc/) for this tutorial, but it's possible to use whatever parser.

A scraper is a more ambiguous term. Scrapy uses the term to refer to the complete package of scraping tools, including the spider, parser, and a pipelined system. In a more colloquial sense, the word is used to refer to the act of retrieving data from websites. In general, it's best to use tools such as Scrapy for websites that have duplicated pages with similar structure, but different content. For example, Wikipedia would be a good example of a website to scrape. On the other hand, Apple's website would be inefficient to scrape, as each page is largely, if not entirely, different from the other. As an example for this tutorial, I'll be scraping Wikipedia.

### Scrapy

Let's first initialize a new Scrapy project. This is done as follows:
```bash
scrapy startproject wikipedia
```

This generates a directory of the following structure:
```bash
.
├── scrapy.cfg
└── wikipedia
    ├── __init__.py
    ├── items.py
    ├── pipelines.py
    ├── settings.py
    └── spiders
        └── __init__.py

2 directories, 6 files
```

The first file we'll take a look at it `items.py`, which specifies Scrapy classes that represent the items to be scraped.
A sample class could look like this:

```python
# items.py #
# -*- coding: utf-8 -*-

import scrapy


class WikipediaItem(scrapy.Item):
    url = scrapy.Field()
    name = scrapy.Field()
    description = scrapy.Field()
```

A Scrapy Item is similar to a C struct. The type of the Scrapy Field is a Python type and we can access the item using the common Python dictionary syntax.

```python
item = WikipediaItem()
item['url'] = http://en.wikipedia.org/wiki/Cat
item['name'] = "Cats"
item['description'] = "Lots of cats"
```

Now, let's take a look at the more interesting spiders directory.
Note that there is no file created for you by default. Scrapy expects you to create these spiders as separate files, and then they can be invoked by `scrapy crawl SPIDER_NAME_HERE`. Let's write up a sample spider now.

```python
from scrapy.contrib.spiders import CrawlSpider, Rule
from scrapy.contrib.linkextractors import LinkExtractor

from bs4 import BeautifulSoup
from wikipedia.items import WikipediaItem


class PagesSpider(CrawlSpider):
    """
    the Page Spider for wikipedia
    """

    name = "wikipedia_pages"
    allowed_domains = ["wikipedia.org"]

    start_urls = [
        "https://en.wikipedia.org/wiki/Main_Page"
    ]

    rules = (
        Rule(LinkExtractor(allow=".+"),
             callback='parse_wikipedia_page'),
    )

    def parse_wikipedia_page(self, response):
        print "Found a page"
        print response.url

        return
```

Note that the class takes in a CrawlSpider as the class parameter. A CrawlSpider simply clicks on all the links on a page, as a web crawler usually does, and verifies each of the link with the rules tuple. The tuple is ordered in terms of significance, meaning that the earlier elements in the tuple are rated higher than the later ones. Each Rule relies on the LinkExtractor class, which is essentially a regex verifying the links.

So, running the spider leads to the following log:


```bash
Found a page
https://en.wikipedia.org/wiki/Main_Page
Found a page
https://en.wikipedia.org/wiki/Praetorian_prefect
Found a page
https://en.wikipedia.org/wiki/Rufinus_(consul)
Found a page
https://en.wikipedia.org/wiki/Arcadius
Found a page
https://en.wikipedia.org/wiki/List_of_Byzantine_emperors
Found a page
https://en.wikipedia.org/wiki/F%C3%BCr_Elise
Found a page
https://en.wikipedia.org/wiki/1810
Found a page
https://en.wikipedia.org/wiki/Sultana_(steamboat)
Found a page
https://en.wikipedia.org/wiki/1865
Found a page
https://en.wikipedia.org/wiki/Ludwig_van_Beethoven
Found a page
https://en.wikipedia.org/wiki/Steamboat
Found a page
https://en.wikipedia.org/wiki/Mississippi_River
Found a page
https://en.wikipedia.org/wiki/Aelia_Eudoxia
Found a page
https://en.wikipedia.org/wiki/395
Found a page
https://en.wikipedia.org/wiki/Koningsdag
Found a page
https://en.wikipedia.org/wiki/Wikipedia:General_disclaimer
Found a page
https://en.wikipedia.org/wiki/Wikipedia:Text_of_Creative_Commons_Attribution-ShareAlike_3.0_Unported_License
Found a page
https://en.wikipedia.org/wiki/April_27
Found a page
https://en.wikipedia.org/wiki/Wikipedia:File_Upload_Wizard
Found a page
https://en.wikipedia.org/w/index.php?action=history&title=Main_Page
```

There's a couple errors with this log output, however.
The first, and more prominent errors, are the links looking like: `https:/en.wikipedia.org/w/*`. These links are related to the history (and views) of the page source. So, we can safely ignore these page sources. We can modify our LinkExtractor to only include those with /wiki/ links now.

We can do this as follows:

```python
rules = (
    Rule(LinkExtractor(allow="https://en\.wikipedia\.org/wiki/.+"),
            callback='parse_wikipedia_page'),
)
```

Finally, we want to also include not just /wiki/, but pages that seem to have some content. For example, we'd like to avoid the link `https://en.wikipedia.org/wiki/Wikipedia:File_Upload_Wizard`. Therefore, we can do this by writing a regex as follows:


```python
rules = (
    Rule(LinkExtractor(allow="https://en\.wikipedia\.org/wiki/.+_.+",
                        deny=[
                            "https://en\.wikipedia\.org/wiki/Wikipedia.*",
                            "https://en\.wikipedia\.org/wiki/Main_Page",
                            "https://en\.wikipedia\.org/wiki/Free_Content",
                            "https://en\.wikipedia\.org/wiki/Talk.*",
                            "https://en\.wikipedia\.org/wiki/Portal.*",
                            "https://en\.wikipedia\.org/wiki/Special.*"
                        ]),
            callback='parse_wikipedia_page'),
)
```

Which leads to some the following output:

```bash
Found a page
https://en.wikipedia.org/wiki/Free_content
Found a page
https://en.wikipedia.org/wiki/List_of_largest_volcanic_eruptions
Found a page
https://en.wikipedia.org/wiki/List_of_official_County_Championship_winners
Found a page
https://en.wikipedia.org/wiki/Manchester_Square
Found a page
https://en.wikipedia.org/wiki/Wikimedia_Foundation
Found a page
https://en.wikipedia.org/wiki/Deportation_of_Armenian_intellectuals_on_24_April_1915
Found a page
https://en.wikipedia.org/wiki/George_Cruikshank
Found a page
https://en.wikipedia.org/wiki/Morning_Herald
Found a page
https://en.wikipedia.org/wiki/Ferdinand_VII_of_Spain
Found a page
https://en.wikipedia.org/wiki/Morning_Chronicle
```

Finally, we can begin parsing the page with response and response.body.
We do this primarily with Beautiful Soup, and by simply finding tags on the page.
It's easiest to scrape website which uses ids.

Here's my scraping code:

```python
def parse_wikipedia_page(self, response):
    item = WikipediaItem()
    soup = BeautifulSoup(response.body)

    item['url'] = response.url
    item['name'] = soup.find("h1", {"id": "firstHeading"}).string

    description = soup.find("div", {"id": "mw-content-text"})
    # get the first tag
    description = string_from_listing(description.find('p'))

    item['description'] = description

    return item
```

Note that the function `string_from_listing` is a function I wrote that enumerates through the Beautiful Soup 4 strings and condenses strings in the listing. This is needed in the case where the body of the description contains links, which are parsed as tags in Beautiful Soup.

We can get the output in JSON format with the following call:
```bash
scrapy crawl wikipedia_pages -o out.json
```

And the JSON looks a little like this:
```json
[{
    "url": "https://en.wikipedia.org/wiki/Free_content",
    "name": "Free content",
    "description": "Free content, libre content, or free information, is any kind of functional work, artwork, or other creative content that meets the definition of a free cultural work. A free cultural work is one which has no significant legal restriction on people's freedom:"
},
{
    "url": "https://en.wikipedia.org/wiki/List_of_largest_volcanic_eruptions",
    "name": "List of largest volcanic eruptions",
    "description": "In a volcanic eruption, lava, tephra (volcanic bombs, lapilli, and ash), and various gases are expelled from a volcanic vent or fissure. While many eruptions only pose dangers to the immediately surrounding area, Earth's largest eruptions can have a major regional or even global impact, with some affecting the climate and contributing to mass extinctions.[1][2] Volcanic eruptions can generally be characterized as either explosive eruptions, sudden ejections of rock and ash, or effusive eruptions, relatively gentle outpourings of lava.[3] A separate list is given below for each type."
},
{
    "url": "https://en.wikipedia.org/wiki/List_of_official_County_Championship_winners",
    "name": "List of official County Championship winners",
    "description": "The County Championship is an annual first-class cricket league competition for county cricket clubs in England and Wales. The league is contested on a round-robin basis and the championship awarded to the team that is top of the league at the end of the season. Yorkshire County Cricket Club are the current champions, claiming their thirty first title in the 2014 season."
}]
```

Note the inclusion of unicode, as escaped sequences as well. As for more features of Scrapy, you could pipeline the process, filter out duplicate links for example, and multithread Scrapy as well, although I won't be covering that for this tutorial.

Hope you enjoyed!
- pybae
