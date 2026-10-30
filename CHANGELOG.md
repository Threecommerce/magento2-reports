# Changelog

## 1.13.2

- Security: the `token_uri` of the pasted GA4 service-account key must be https on googleapis.com, otherwise the Google default is used (the signed JWT could be sent to an arbitrary host).

## 1.13.1

- Metadata: license in `composer.json` is now `proprietary` (commercial module), no functional change.

## 1.13.0

- Quote Request Analysis report (Reports > Sales > Quote Request Analysis, only with Threecommerce Catalog Mode
  installed): requests against the previous period, requested value, requests followed by an order of the same
  customer within N days (30) with orders and revenue, time to first reply, path from request to order, current
  statuses, requests waiting for a reply; grid per requested product (conversion, quantity and revenue ordered)
  or per request (first reply, order that followed); CSV / Excel XML export.
- Durations of one day read "1 day" instead of "1 days".

## 1.12.0

- Store Comparison report (Reports > Sales > Store Comparison): store views or websites side by side against the
  previous period or the same period last year, with net revenue, orders, average order value and their changes,
  share of revenue, customers, new customers, revenue from repeat orders, guest orders, items per order,
  discounts, shipping and refunds; amounts in the global currency; trend chart of revenue, orders or average
  order value per day, week or month; CSV / Excel XML export.

## 1.11.0

- Pickups by Store report (Reports > Sales > Pickups by Store, only with Threecommerce Store Pickup installed):
  pickup orders per pickup store with revenue, average order value, customers, picked up, waiting, overdue,
  canceled, median and average time to pickup and the comparison with the previous period; stores enabled for
  pickup without orders, orders without a store and deleted stores included; list of the orders waiting to be
  picked up with the customer's phone and e-mail; CSV / Excel XML export. Works with Store Pickup 2.x
  (`3com_storelocator`) and 1.x (`mageos_storelocator_store`).

## 1.10.0

- Bot Check: when Varnish is the full page cache, the pages it serves are counted from the varnishncsa log, read
  every 5 minutes (cron `tcreports_traffic_import_log`) from where the previous run stopped, log rotation
  included. Combined format supported; with the recommended format (cache status, X-Forwarded-For,
  Accept-Language) only cache hits are added, otherwise every request comes from the log and Magento stops
  counting the requests from Varnish. The report shows the state of the import (missing or unreadable log, no new
  lines).
- New settings "Import the Varnish Log" (on) and "Varnish Log File" (`/var/log/varnish/varnishncsa.log`), command
  `bin/magento tcreports:traffic:import-log [--file=PATH] [--force] [--reset]`.
- Varnish ESI blocks are no longer counted as requests.
- Requires Magento_PageCache.

## 1.9.0

- Bot Check report (Reports > Traffic > Bot Check): requests reaching Magento (built-in full page cache hits
  included) counted per hour, IP and user agent and classified as people, search engines, AI crawlers, SEO
  tools, previews & services, other bots, scripts & scrapers, suspicious browsers and fake bots (reverse DNS
  check of Googlebot, Bingbot & co.); pie charts by type and by bot, requests over time, list of IPs and agents
  with a recommendation (block, consider, allow) and its reasons, ready-made rules for robots.txt, nginx,
  Apache and Cloudflare; CSV / Excel XML export.
- New settings (Stores > Configuration > Threecommerce Plugins > Reports > Bot Check): recording on/off (on by
  default), days the IP details are kept (30), requests per hour above which a browser is suspicious, client IP
  header behind a proxy or CDN, excluded IPs.
- Cron jobs `tcreports_traffic_aggregate` (hourly) and `tcreports_traffic_verify_bots` (every 10 minutes),
  command `bin/magento tcreports:traffic:aggregate [--days=N] [--verify]`.
- Period presets Today, Yesterday and Last 7 days (bot check only).

## 1.8.0

- Hourly Heatmap report (Reports > Sales > Hourly Heatmap): orders, net revenue, average order value or carts
  created by day of the week and hour in the admin timezone (daylight saving time per date), busiest slots,
  weekend and night shares; CSV export.

## 1.7.0

- Sales Geography report (Reports > Sales > Sales Geography): orders, customers, new customers, net revenue,
  average order value and shipping by country, province, Italian region, city or postcode, compared with the
  previous period; top areas by revenue; CSV / Excel XML export.

## 1.6.0

- Fulfillment Times report (Reports > Sales > Fulfillment Times): per order hours to invoice, ship and add
  tracking, working days to ship against a target, late orders still to ship; classes that filter the grid;
  breakdowns by shipping method and day of the week; CSV / Excel XML export.

## 1.5.0

- Searches Without Results report (Reports > Marketing > Searches Without Results): search terms without (or
  with few) results, most searched first, with handling (redirect, synonym, to fix), products in the catalog
  whose name matches the term, links to the storefront search, to the term (redirect) and to a new synonym
  group; CSV / Excel XML export.
- Requires Magento_Search.

## 1.4.0

- Product Conversion report (Reports > Products > Product Conversion): views, add-to-cart events, carts,
  carts ordered, cart abandonment, orders, revenue and conversion rates per product; insights (stars, viewed a
  lot but sold little, hidden gems, abandoned in the cart) with suggested actions that filter the grid.
- Product views from the Magento statistics when enabled, otherwise from GA4 (Data API, service account) when
  the Threecommerce GA4 module is installed, otherwise none.
- New configuration Stores > Configuration > Threecommerce Plugins > Reports (GA4 property and key) and table
  `tcreports_ga4_item`.
- Report periods shared by the date-based reports.
- Requires Magento_Quote.

## 1.3.0

- Dead Stock & Coverage report (Reports > Products > Dead Stock & Coverage): stock on hand, reserved and
  available (MSI, or legacy stock), sales rate, coverage in days, last sale, stock value at cost; stock health
  classes (dead stock, overstock, to reorder, out of stock with demand, healthy, new) with suggested actions
  that filter the grid; excess quantity/value and suggested reorder quantity; CSV / Excel XML export.
- Product name renderer shared by the product reports.
- Requires Magento_CatalogInventory.

## 1.2.0

- Inactive Customers report (Reports > Customers > Inactive Customers): customers without orders for at least
  N days, most valuable first, with newsletter subscription, usual interval between orders, last login;
  inactivity bands with suggested actions that filter the grid; CSV / Excel XML export for win-back campaigns.
- Optional listing of registered accounts that never ordered.
- Minimum orders and minimum net spend filters.
- Requires Magento_Newsletter.

## 1.1.0

- Customer RFM Analysis report (Reports > Customers > RFM Analysis): recency, frequency and monetary scores
  per customer, ten segments (Champions … Lost) with suggested actions, segment cards that filter the grid,
  CSV / Excel XML export for newsletter or CRM campaigns.
- Customers identified by order email, so guest orders join the account of a customer who registered later.
- Configurable recency (days) and frequency (orders) thresholds; monetary score as spend quintile.
- Shared admin stylesheet and helpers for the reports.

## 1.0.0

- New admin menu group Reports > Profitability.
- Product Margin report: net revenue, cost, margin, margin %, markup % and cost coverage per product
  (variants together) or per sold SKU, computed live from the order items.
- Period presets or custom range, store view, order statuses, optional fallback to the current product
  cost, optional refund subtraction; KPI summary, totals row, CSV / Excel XML export.
