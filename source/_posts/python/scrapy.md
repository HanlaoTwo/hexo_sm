---
title: scrapy
date: 2018-07-10 21:09:19
tags: python
---
```
import scrapy

import re

class mySpider(scrapy.Spider):
    name = "OSC-NEWS-SPIDER"
    start_urls = [
        'http://blog.csdn.net/',
    ]

    def parse(self, response):
        for quote in response.css("div.blog_list_wrap"):
            print('hello bitch')
            yield {
                'title': quote.css("dl.blog_list clearfix::text").extract_first(),
                #'content': quote.css("div.sc sc-text text-gradient wrap summary::text").extract_first(),
                #'tags': quote.css("div.tags > a.tag::text").extract()
            }

        next_page_url = response.css("li.next > a::attr(href)").extract_first()
        if next_page_url is not None:
            yield scrapy.Request(response.urljoin(next_page_url))




from twisted.internet import reactor
from scrapy.crawler import Crawler
from scrapy import log, signals
from scrapy.utils.project import get_project_settings
from spiders.MoiveSpider import MoiveSpider

spider = MoiveSpider()  #这里改为你的爬虫类名
settings = get_project_settings()
crawler = Crawler(settings)
crawler.signals.connect(reactor.stop, signal=signals.spider_closed)
crawler.configure()
crawler.crawl(spider)
crawler.start()
log.start()
reactor.run()


from scrapy import cmdline
....