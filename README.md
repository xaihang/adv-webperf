# Advanced Web Performance 

## Problem with performance
- Mostly frontend responbnsiblity when it comes to performance; if the web is slow it's usually bad frontend decisions
- time to interactive ~ 12.5 seconds median mobile/ 6.1 sec on desktop; ready for interaction
- you can start using the website before it completely loads
- underestimating the mobile webt
- North America/ bandwidth/ cellular networks 
- not every country is 'advanced' 4/5G and 28% of user are lower than 3G
**Latency: time delay between when a data packet is sent and when it is recieved, expressed in milliseconds.**
- first contentful paint; more than 50% 

## How can we measure the performance? 
**Browser-centric metrics**
* TTFB = time to first byte
* First Paint 
* Page Load; time to measure performance (define: Page load time is the time it takes to download and display the entire content of a web page in the browser window (measured in seconds).)
- *browser-centric metrics are not so important for web performance optimization*

**User-centric metrics**
* First Interactive
* Speed Index - under use
* Time To Interactive 
* Largest Contentful Paint (LCP); mostly focused on; time depending on your website content
* Custom Metric; can personalize/define 
* Measure the data/real data user (RAM), test, and apply 
* Interaction to next paint = responsiveness

## Core Web Vitals 
1. LCP = largest contentful paint (Loading) 
    * initial load
1. FID = First Input Delay (Interactivity)
1. CLS = Cumulative Layout Shift (visual)

**optimizing the frontend has high impact, it is relatively cheap to optimize and results are immediate!**

## Understand the browser
- HTTPS 
- HTTP:
    * response = downlink
        * HEADER - BODY
    * request = uplink
        * HEADER - BODY

## HTTP/1.1
- one req per tccp connection
- limited number of parallel req to the server
- GZIP encoding accepted

## HTTP/2
- performance from scratch
- header compression
- tcp connection reuse

## Caches
**browser will check the cache** 
### cache headers per file:
    * absolute expire date 1.0
    * relative expire date 1.1
    * more specs / values

### browser needs a resource
1. it checks the cache
    a. cache MISS: we go the network
    b. cache HIT:
        i. it's expired 
            * conditional request
        ii. it's not expired - we use the file from the cache 

## Basic Performance
- release the single thread ASAP
- embrace SVG
- compress img define placeholder size
- webfont can be possible blocking so be careful with usage 

## Hacking performance 
1. FIRST LOAD - avoid more than 1 round trip; tcp slow start
1. ATF = above the fold
1. BTF = below the fold 
1. HEADER - HTTP Strict Transport Security

## Hacking LCP 
1. PRELOADING 
```html
 <link rel="preload" href="gallery/ancient-greece.png" as="image">

```
The "rel=preload" attribute is used in HTML to instruct the browser to preload a resource, such as an image, script, or stylesheet, before it is actually needed by the page. By preloading resources, the browser can start fetching them in advance, which can help to reduce page load times and improve performance.

*It's important to note that "rel=preload" should be used judiciously, as preloading too many resources can actually slow down page load times by consuming more bandwidth and server resources.*
1. fetchpriority = high
1. HTTP Early Hints - code 103, we sent it before processing server-side; then the service will send back 200 OK 

## Hacking Data Transfer
1. HTTP/3 
- transport protocol over udp
- optimized request can be of 75%
- use zopfli = save 3-8% data transfer to gzip
- brotli = save 25% data transfer compared to gzip; encoding header; consuming more cpu and caching 

## Hacking Resource Loading
- modern img formats: svg, webp, avif, guetzli jpeg, zopfli pgn
**muted video instead of GIFs** (gif slows down web performances)
- mordern cache control: immutable
    1. serve from the caches 
    2. update it in the background ~ stale-while-revalidate=99
- warming up the engines 
```html
<link rel="preconnect" href="https://example.com">
<link rel="dns-prefetch" href="https://example.com">
```
Both `rel="preconnect"` and `rel="dns-prefetch"` are link relation attributes in HTML that are used to improve website performance by reducing the time it takes to establish connections to external resources such as third-party domains, CDNs (content delivery networks), and APIs.

`rel="preconnect"` instructs the browser to establish a connection to a specified resource in advance, so that when the resource is actually needed, the connection is already established and the data can be transferred more quickly. This can help to reduce latency and improve page load times, especially for resources that are hosted on external domains or services.

`rel="dns-prefetch"` is similar to rel="preconnect", but it specifically instructs the browser to perform a DNS (Domain Name System) lookup for a specified domain in advance, so that the IP address of the domain is already cached and available when the resource is requested. This can help to further reduce latency and improve page load times, especially for resources that are hosted on domains that are not yet in the browser's DNS cache.

In summary, both `rel="preconnect"` and `rel="dns-prefetch"` are link relation attributes that can be used to optimize website performance by reducing the time it takes to establish connections to external resources. While `rel="preconnect"` is used to establish a connection in advance, `rel="dns-prefetch"` is used to perform a DNS lookup in advance, both of which can help to reduce latency and improve page load times.

## RUM 
- we can make analytics on every user to improve their experiences 

## console -> performance option 
- root of performances apis
- `performance.now()` (expression of miliseconds of time since started navigation; high precision time)
- `performance.originTime`

**PERFORMANCE IS TOP PRIORITY**

## RESOURCES
- Luke W ideation/design: mobile design details: avoid the spinner!
- Chrome UX; page speed insight = use it to test performance for mobile/desktop
- google chrome/dev tool -> inspect -> lighthouse (a cloud base analysis) 
- Filmstrip view (array of screenshots of your app)
- webpagetest.org (tests your website's performance)
- letsencrypt.org 
- archive.org; saving all the headers on performance and measure how it's doing overtime
- hstspreload.org 
- squoosh.app ~ PWA 100% client side or CLI 



