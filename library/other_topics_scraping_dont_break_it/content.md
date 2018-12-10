---
title: Don't break it!
author: Thinkful
team: grading
time: 60
uuid: 245a512e-c1c0-42c5-a277-a5ea9d5732c9
---

## Breaking the website

As of this writing, the first sponsored search option when you type 'web scraping' into Google is 'Guide to Blocking Web Scraping.'  Websites are designed to be navigated by human beings, who have a fairly low bandwidth for new information.  From the viewpoint of the web server, even the fastest reader will go through a website's pages fairly slowly.  

A web scraping program, on the other hand, consumes information incredibly quickly-- after all, that's why we wrote the program.  From the point of view of the server hosting the website the rapid-fire requests from a scraper can flood the server bandwidth and cause it to crash, and [then there's no website for anybody](https://xkcd.com/958/).

In fact, crashing a website by flooding it with automated traffic a common hacking technique called a Denial of Service (DoS) attack.  The goal in scraping is to retrieve information while a DoS attack seeks to hide information by making a website unavailable, but the mechanism (repeated automated calls to a server) is pretty much the same.  Visualize all Three Stooges trying to go through a doorway at once and getting stuck, and you've got the general idea.  

There are two sides to being a good netizen-scraper.  The first is writing a scraper that gets the information you want at a reasonable rate without overwhelming the server.  The second is how to work within the methods that websites have developed to protect themselves from DoS attacks and signal that you are a 'good' scraper who shouldn't be blocked.  

Scrapy provides some very convenient options for both of these aspects.  They are set in the 'settings.py' file if you are using the scrapy API interface, and in the ´CrawlerProcess()´ command if you are working in the script.  Scrapy is very flexible and there are [a lot of settings](https://doc.scrapy.org/en/latest/topics/settings.html)- we're going to focus on the following:

´process = CrawlerProcess({
    'AUTOTHROTTLE_ENABLED': True,
    'HTTPCACHE_ENABLED': True,
    'ROBOTSTXT_OBEY': True,
    'USER_AGENT': 'ThinkfulDataScienceBootcampCrawler (thinkful.com)'
})´


## Not overwhelming the server

### Autothrottle and download delay

To avoid a DoS-style scraping attack, you can use the DOWNLOAD_DELAY setting to introduce a variable amount of delay between calls to the server.  Alternatively, you can use the autothrottle option (AUTOTHROTTLE_ENABLED) which will try to dynamically set the delay based on how quickly the server responds to scrapy's requests.  By default, DOWNLOAD_DELAY is set to 0 and autothrottle is turned off, so make sure to look into these before setting your scraper loose in the wild.

### Caching

As you're setting up a scraper, you're probably going to run the same code over and over, catching new bugs each time.  To avoid constantly hammering the server to download the exact same pages, you can enable the 'HTTP cache' option.  Then, when you try to download a page that is already cached on your machine, scrapy will use the cached copy instead.  Remember, turn this off (or at least clear your cache) before you start your scraper in earnest to make sure you are getting the most recent data!

## Following the Rules

### Robots.txt
Websites sometimes provide rules to scrapers about what sorts of activities they can engage in and whether certain parts of the site are off-limits.  They do this by creating a *robots.txt* file, usually in the root directory.  Here is Amazon's:  [https://amazon.com/robots.txt](https://amazon.com/robots.txt).

If you click on it, you can see that they place a lot of different aspects of the website off-limits to scrapers.  Below, we've pulled some pieces to focus on:

```
User-agent: *
Disallow: /exec/obidos/account-access-login
Disallow: /exec/obidos/change-style
Disallow: /exec/obidos/flex-sign-in
Disallow: /exec/obidos/handle-buy-box
Disallow: /exec/obidos/tg/cm/member/
Disallow: /gp/aw/help/id=sss
Disallow: /gp/cart
Disallow: /gp/flex
Disallow: /gp/product/e-mail-friend
Allow: /wishlist/universal*
Allow: /wishlist/vendor-button*
Allow: /wishlist/get-button*
Disallow: /gp/wishlist/


User-agent: Googlebot
Disallow: /rss/people/*/reviews
Disallow: /gp/pdp/rss/*/reviews
Disallow: /gp/cdp/member-reviews/
Disallow: /gp/aw/cr/
Disallow: /exec/obidos/account-access-login
Disallow: /exec/obidos/change-style
Disallow: /exec/obidos/flex-sign-in
Disallow: /exec/obidos/handle-buy-box
Disallow: /exec/obidos/tg/cm/member/
Disallow: /gp/aw/help/id=sss


User-agent: EtaoSpider
Disallow: /
```

The User-agent identifies the specific robot or scraper that the permissions refer to.  A * indicates that these permissions apply to all robots otherwise not named.  Notice that amazon's file both disallows some places, and explicitly allows others.

It also has special permissions for the Google robot, which indexes the website for search.  And finally, it apparently doesn't like EtaoSpider, because they block it from crawling any of the website at all.

Scrapy is set to automatically obey robots.txt files when it finds them.  Attempts to crawl a disallowed section will generate the following message: 

´2016-08-19 16:12:56 [scrapy] DEBUG: Forbidden by robots.txt: <GET http://website.com/login>´

### USER_AGENT

The user agent setting allows you to identify yourself to the administrators of the website.  Ideally you would include both a name and an email address so they can contact you if your scraping is causing issues.


## Be a good scraper

[If you scrape too much, too fast, too carelessly, you'll eventually end up with no website to scrape from](http://www.qwantz.com/index.php?comic=1731).  But if you keep the needs of the website in mind, you'll be able to keep scraping data as long as you need.

