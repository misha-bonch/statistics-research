# statistics-research

`statistics-research` is a small research tool that reads public product prices from online shops in Taiwan and
Hong Kong for official consumer price statistics: an international comparison of the prices of a fixed list of
everyday goods. This page explains what it does and how to reach the people who run it.

Its plain HTTP requests identify themselves with this User-Agent:

```
statistics-research/1.0 (consumer price statistics; +https://github.com/misha-bonch/statistics-research)
```

Pages that only work in a browser are opened in a standard Chrome browser, which sends Chrome's own User-Agent.

Until November 2026 the tool was called `price-collector`, and its requests were signed
`price-collector/1.0 (price statistics research)`. Some shops may still see the old name while the change is checked
shop by shop.

## What it is not

- Not a price-comparison site, a reseller or a data broker. It works for no retailer.
- The prices are used only for statistics. They are not sold and not passed to any retailer or other company.

## What it collects

- Public prices of a fixed list of everyday products (food, drinks, personal care and similar), as any visitor
  sees them on category and product pages: the current price, a struck "before" price, promotion text and
  availability.
- No personal data. It never signs in, creates an account, places an order or fills a cart.
- It does not use site search.

## How it behaves

- Few requests: at most one request every 5 seconds over plain HTTP, and one page every 15 seconds when a browser
  is needed. A collection run is capped at 300 page loads; a development check is at most 100.
- It stops at once on any block, captcha, HTTP 401/403/429 or unexpected redirect. After a stop it waits at least
  an hour before one small check of at most 3 pages, and makes at most four such checks per shop a day. After a
  captcha or challenge page it waits at least three hours, and a second one ends work on that shop until the next
  day.
- It does not hide what it is: no rotating IP addresses, no proxy services, no captcha solving, no copied browser
  cookies.
- It prefers the way that needs the fewest requests and puts the least load on a site. Where a shop's own catalogue
  API needs the keys its page gives every anonymous visitor, the tool opens that page once per session, then
  asks the API directly with those keys and its own User-Agent, instead of loading every category page. It never
  signs in and does not reuse the keys after the session.
- A person reads each site's robots.txt once a month. Its Crawl-delay is kept. Its Disallow lines are recorded for
  review but are not applied automatically; if you want us to keep off part of your site, tell us (see Contact).
- Where a shop offers a public data feed or an API its own pages use, that is preferred over loading pages.

## Contact

If you run one of these sites and want us to slow down, change what we read, keep off some pages, use a data feed
instead, or stop, please open an issue at **https://github.com/misha-bonch/statistics-research/issues**. We answer
and act on such requests.

## 中文說明

`statistics-research`（原名 `price-collector`）是一個用於官方消費者物價統計的小型研究工具，讀取台灣及香港網上商店公開顯示的固定商品清單價格，用於國際物價比較。
價格只用於統計，不出售，也不提供給任何零售商或其他公司。
它不收集個人資料，不登入、不下單；請求頻率低（純 HTTP 每 5 秒最多一次，瀏覽器每 15 秒一頁），遇到封鎖或驗證碼即停止，至少一小時後才作少量檢查。
它盡量以最少的請求讀取資料：如商店自身的商品 API 需要網頁發給匿名訪客的金鑰，工具每次只開啟該網頁一次，之後以這些金鑰及自身的 User-Agent 直接查詢 API，不登入，會話結束後不再使用。
我們每月由人工閱讀各網站的 robots.txt：遵守 Crawl-delay；Disallow 規則會記錄以供檢討，但不會自動執行。
如網站經營者希望我們降低頻率、避開部分頁面、改用數據源或停止讀取，請在此提交 issue： https://github.com/misha-bonch/statistics-research/issues
