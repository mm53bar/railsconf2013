# Cache = Cash

### Stefan Wintermeyer
### @wintermeyer
### Slides: https://speakerdeck.com/wintermeyer/cache-equals-cash-1

* impact of slow pages
  * web search delay experiment by @igrigorik of google
* definitions
  * 0-100 ms = instant
  * 100-300 ms = sluggish
  * 300 - 1000 ms = machine is working
* in U.S., 25% of users are using only mobile web
* 1000ms budget
  * 200ms dns lookup
  * 200ms tcp connection
  * 200ms http request
  * only leaves 400ms of budget!

* builds simple rails 3.2 app using 1.9.3, nginx, unicorn, mysql
* main index page has a user-specific shopping cart piece
  * intentionally hard to cache
* builds a watir script to automate using the site
* https://github.com/wintermeyer/snappy_webshop

how fast to get this workflow running on raspberry pi?

116 seconds

* views are taking more than 3 seconds to render
* db is 76ms - not the problem

### Fragment caching

* easy first step

    cache [current_user, product] do
    ...
    end

Add dalli to your gemfile

* How much diff can a few lines of code make?
* page load down to 60s
* if first 25 products are displayed in index page, group them into clusters of 10
  * might create problems if you do zebra-striping in index page
* adding more fragment caching (headers, footers, shows, etc) saved another 15s on pageload

### HTTP caching

* last-modified header
  * 304 Not Modified
* e-tag
  * use fresh_when method to set etag
* beauty of http caching is that view isn't even rendered
* saves another 10 seconds and takes total load time down to 35s

### Preheating the cache

* Waste a lot of time writing initial cache
* Could preheat the cache in off business hours
* Don't be afraid to use brute force!
* Saved another 9s and takes time down to 26s

### nginx

* page caching
* brute force is your friend
* saves another 7s to 19s
* but what about user-specific content?
  * hard drive space is cheap
  * cache the files and use nginx to gzip the files on the fly
  * nginx will happily read a cookie and find the pre-rendered page in a given directory structure

### emberjs

* down to 8seconds

### recommendation

* go for low-hanging fruit
* use fragment caching and http caching
* new applications - learn ember and combine it with rails
  * don't forget http caching!

