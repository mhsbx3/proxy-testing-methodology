# reliable proxies: how to test a provider in one afternoon and spot the ones that waste your budget

Anyone searching for reliable proxies has usually already lost a week to the unreliable kind. A session dies halfway through a checkout flow. A batch job returns block pages that still count as HTTP 200. The dashboard says 500 IPs; the target site says you've seen twelve of them before.

So the useful version of this topic isn't a definition. Residential HTTP proxies are a known quantity. What's hard is separating a provider that holds up under a real workload from one that only looks good on a pricing page — and doing that without spending hundreds of dollars on an experiment.

Below is what actually decides reliability, the four numbers worth measuring before you commit, and how a provider like 9Proxy fits into those criteria — including the parts of it that won't suit everyone.

## The claims that mean the least

Pool size is the first one to ignore. Every vendor quotes tens of millions of IPs, nobody audits the number, and it usually counts addresses seen at any point over months. You will never touch most of them. Pull 1,000 IPs from one country during your working hours and count the unique ones — that tells you more than a headline figure.

Advertised success rates have the same problem. Vendors publish 95–99%. When AImultiple runs continuous requests against sites that actively block bots, residential and datacenter providers both land between 55% and 75% on a given day. The gap isn't fraud, it's measurement: a CAPTCHA served with a 200 status counts as a success on a vendor page and a failure in your pipeline. Their data also shows a provider's daily score can swing by 20 points, and the top performer changes constantly. Reliability, in practice, means consistency and a backup, not a ranking.

Uptime percentages are close to noise too. 99.95% sounds precise; across a month it still permits hours of degraded performance that no one will refund.

## The four numbers worth measuring yourself

Pick the smallest paid plan on your shortlist and run the same job on each. Five hundred requests against your real targets, not a demo page.

1. **Success rate** — count a block page, login wall, or CAPTCHA as a failure even when the status code is 200. This is the single number that drives everything else.
2. **Unique IPs and ASN diversity** — pull 1,000 IPs in your target country and count uniques. Too many coming from one ASN looks unnatural and burns reputation faster.
3. **Median latency, plus spread** — residential medians generally sit around 2.0–2.5 seconds. Stability matters as much as the median; a tight timeout turns a slow provider's real successes into your failures.
4. **Cost per successful request** — list price divided by pages you actually got. A $0.20/GB provider at 40% success costs more than a $2/GB provider at 90%.

Then hold one sticky session for an hour and see whether it survives. If logging in is part of your workflow, that single test eliminates more providers than any benchmark table.

## Per-IP, per-GB, bundles: the billing model decides your real cost

Most "cheap proxies" problems are billing-model problems. The same workload can cost three times as much under the wrong structure.

| Model | How it charges | Fits | Watch out for |
| --- | --- | --- | --- |
| Per-IP | Fixed fee per IP, bandwidth usually unlimited | Stable sessions, account work, long jobs with unpredictable traffic | No rotation; useless if you need thousands of rotating exits |
| Per-GB | Pay for traffic transferred | High-rotation scraping, ad verification, geo checks | Images, JS, and retries inflate the bill |
| Bundles | IPs plus a traffic allowance | Mixed workloads inside one project or client | Only economical if you'll genuinely use both halves |
| Monthly subscription | Fixed quota per month | Predictable, large, steady volume | Unused quota is money you don't get back |
| Pay-as-you-go | No commitment | Testing, spiky usage | Higher unit cost |

A concrete example of why per-GB pricing needs care: 10,000 product pages at ~500 KB each is roughly 5 GB before retries, scripts, fonts, and tracking pixels. Browser-based scraping realistically multiplies that by three to five. Budget the estimate you calculated and you'll blow through it by the second week.

## Where unreliable providers actually fail

Three patterns cover most of it.

**Recycled IPs.** Small pools mean every address gets reused constantly. Reputation accumulates, block rates climb, and the provider's dashboard shows nothing unusual because the request did technically succeed.

**Rotating sessions where you needed identity.** Rotating residential is the right tool for anonymous collection and the wrong tool for a logged-in profile. A sticky session typically lasts 10–30 minutes before the IP changes, which is the classic trigger for re-verification.

**Unclear sourcing.** If a provider can't explain where the residential IPs come from and whether the people behind them consented and got paid, that's a legal and uptime risk you inherit. Some low-cost networks historically built their pools with software that turned users' devices into exit nodes without clear consent. Free proxy lists are worse on every axis: slow, pre-blocked, and a straightforward security risk.

## Where 9Proxy sits in this picture

9Proxy sells residential IPs through a balance-based account, with three purchasing models rather than a subscription. The network is advertised as 20M+ residential IPs across 90+ countries with targeting down to country, state, city, ZIP, and ISP level, and it supports HTTP/HTTPS and SOCKS5 — the last one matters if you're routing Scrapy, Puppeteer, Playwright, or anti-detect browsers without protocol conversion hacks.

For a provider at this price point, the operational details are the interesting part:

- **60-second replacement.** A proxy that fails within the first minute of activation is credited back. Most providers count a dead connection as a consumed resource.
- **Today List.** IPs you've used in the last 24 hours can be reused at no extra cost while they're still online. On flaky residential pools this removes a lot of waste.
- **Unused IPs don't expire.** Buying 5,000 IPs doesn't start a countdown; the balance sits until you forward them.
- **Access without the desktop app.** Proxy2Web issues IP-based proxies from a browser, and ProxyHub handles mobile devices. The Windows client still exists for OS-level routing where an app has no proxy setting of its own.

👉 [Create a 9Proxy account and pick the package that matches your workload](https://bit.ly/9-Proxy)

The honest limitations, since this is an article about reliability and not a brochure: dynamic residential IPs live from a few hours up to roughly 24 hours, depending on whether the underlying household stays online. Trustpilot's page for the service carries complaints from users whose IPs dropped about an hour in and triggered security locks on their accounts — and 9Proxy's own public reply doesn't dispute it. Their answer is that dynamic residential addressing behaves that way by nature, and that anyone needing a fixed address for weeks belongs on static ISP proxies instead. That's a correct technical answer, and it's worth reading before you buy if your plan is "keep this account logged in."

Third-party reviews are mixed in the usual way. Geekflare's 2026 review treats it as a budget residential option with a working pricing ladder; Caproxy's directory entry scores it around 4.33 from users while noting it isn't aimed at beginners; iTWire flagged the mandatory app and promotion-dependent trials as drawbacks. Most positive user comments in aggregator listings mention stable IPs with Dolphin Anty and AdsPower, which is consistent with what the product is built for.

## IP-based or GB-based? This is the decision that matters

|  | Residential by IP | Residential by GB |
| --- | --- | --- |
| Billing | Per IP, unlimited bandwidth during active time | Per GB consumed |
| IP lifetime | A few hours up to ~24h | Rotates per request or per sticky window you set |
| Endpoint generation | 1 IP = 1 activation when forwarded | Unlimited endpoints |
| Validity | Unused IPs don't expire | 180 days (unlimited on Enterprise) |
| Auth | Desktop app or Proxy2Web, optional proxy auth | Username/password or IP whitelist, straight from the dashboard |
| Targeting | Country, city | Country, state, city, ZIP, ISP |

If your work is account management, checkout QA, or anything with a long session, the IP model is the closer fit — with the caveat above about how long residential addresses last. If your work is high-rotation collection where each request moves little data, per-GB is cheaper and simpler, because you stop counting IPs and start counting gigabytes.

## Full package list and current pricing

IP-based and bundle pricing changed on June 1, 2026, per the provider's own announcement; GB prices were left untouched. That's why you'll still find older, lower IP figures on reseller pages and review sites written before the change.

| Package | What you get | Price | Billing / validity | Buy |
| --- | --- | --- | --- | --- |
| IP-Based — 100 IPs | Unlimited bandwidth per IP | $24 ($0.24/IP) | One-off, IPs never expire unactivated | [Get the 100 IP package](https://bit.ly/9-Proxy) |
| IP-Based — 500 IPs | Unlimited bandwidth per IP | $72 ($0.144/IP) | One-off | [Get the 500 IP package](https://bit.ly/9-Proxy) |
| IP-Based — 1,000 IPs + 500 bonus | 1,500 IPs total, unlimited bandwidth | $126 ($0.084/IP) | One-off | [Get the 1,000 + 500 IP package](https://bit.ly/9-Proxy) |
| IP-Based — 2,500 IPs | Unlimited bandwidth per IP | $210 | One-off | [Get the 2,500 IP package](https://bit.ly/9-Proxy) |
| IP-Based — 5,000 IPs | Unlimited bandwidth per IP | $360 | One-off | [Get the 5,000 IP package](https://bit.ly/9-Proxy) |
| IP-Based — 15,000 IPs | Unlimited bandwidth per IP | $720 | One-off | [Get the 15,000 IP package](https://bit.ly/9-Proxy) |
| IP-Based — 25,000 IPs | Unlimited bandwidth per IP | $863 | One-off | [Get the 25,000 IP package](https://bit.ly/9-Proxy) |
| IP-Based — 50,000 IPs | Unlimited bandwidth per IP | $1,438 | One-off | [Get the 50,000 IP package](https://bit.ly/9-Proxy) |
| Business IP — 100,000 IPs | High-volume IP pool | $2,300 ($0.023/IP) | One-off | [Get the 100,000 IP business package](https://bit.ly/9-Proxy) |
| Business IP — 200,000 IPs | High-volume IP pool | $4,140 ($0.021/IP) | One-off | [Get the 200,000 IP business package](https://bit.ly/9-Proxy) |
| Business IP — 500,000 IPs | High-volume IP pool | $8,625 ($0.018/IP) | One-off | [Get the 500,000 IP business package](https://bit.ly/9-Proxy) |
| GB-Based — 5 GB | Unlimited endpoints | $15 ($3.00/GB) | 180 days | [Get the 5 GB package](https://bit.ly/9-Proxy) |
| GB-Based — 50 GB + 5 GB bonus | Unlimited endpoints | $105 ($2.10/GB) | 180 days | [Get the 50 + 5 GB package](https://bit.ly/9-Proxy) |
| GB-Based — 100 GB | Unlimited endpoints | $150 ($1.50/GB) | 180 days | [Get the 100 GB package](https://bit.ly/9-Proxy) |
| GB-Based — 200 GB | Unlimited endpoints | $200 ($1.00/GB) | 180 days | [Get the 200 GB package](https://bit.ly/9-Proxy) |
| GB-Based — 1,000 GB | Unlimited endpoints | $800 ($0.80/GB) | 180 days | [Get the 1,000 GB package](https://bit.ly/9-Proxy) |
| GB-Based — 2,000 GB | Unlimited endpoints | $1,500 ($0.75/GB) | 180 days | [Get the 2,000 GB package](https://bit.ly/9-Proxy) |
| GB-Based — 10,000 GB | Unlimited endpoints | $0.68/GB | 180 days | [Get a high-volume GB package](https://bit.ly/9-Proxy) |
| Enterprise GB | Unlimited validity, team mode (1 owner + 5 members), per-member traffic controls, activity logs | Custom pricing | No expiry on shared traffic | [Ask about Enterprise pricing](https://bit.ly/9-Proxy) |
| Bundle — Starter | 100 IPs + 5 GB | $30 | 180-day traffic validity | [Get the Starter bundle](https://bit.ly/9-Proxy) |
| Bundle — Popular | 1,500 IPs + 50 GB | $180 | 180-day traffic validity | [Get the Popular bundle](https://bit.ly/9-Proxy) |
| Bundle — Pro | 5,000 IPs + 500 GB | $720 | 180-day traffic validity | [Get the Pro bundle](https://bit.ly/9-Proxy) |

A few notes that affect what you actually pay. Bundles show a list price and a discounted price at checkout; the Pro bundle appears in the provider's own payment documentation at $720 against a $860 list. Selected payment methods add either a 5% discount or a 5% product bonus, which is worth checking before you top up, and payments run through cards, bank cards, crypto including USDT, BTC, ETH, LTC and DOGE, Alipay, Apple Pay, and Google Pay. Sign-up works on an invite code rather than open registration, which is also how the referral discount gets attached.

Free trials exist but aren't guaranteed — they're limited, availability-dependent, and generally have to be requested from support. Treat "try before you buy" as a possibility rather than a plan.

## Getting set up without overbuying

The sensible sequence, and it takes about ten minutes:

1. Sign up with an invite code and confirm which model you need. If you can't describe your workload as "stable sessions" or "high rotation," spend five minutes deciding that first — it changes the whole cost structure.
2. Buy the smallest package in that model. The 100-IP or 5-GB tier is a test, not a waste.
3. Pick an access method. Windows client for OS-level routing, Proxy2Web for browser-based work, ProxyHub for mobile devices, or the API when you're wiring proxies into a pipeline rather than a browser.
4. Run your 500-request test on your own targets and log success rate, unique IPs, latency, and cost per successful page.
5. Only then scale, and keep the balance-based model in mind: nothing expires while it sits, so a larger top-up at a lower rate only makes sense once the small one passed.

👉 [Run your first test on the smallest 9Proxy package](https://bit.ly/9-Proxy)

## Quick answers

**Do unused IPs or traffic expire?** Unactivated IPs don't expire. GB traffic is valid for 180 days on standard packages and has no expiry on Enterprise.

**Is SOCKS5 supported?** Yes, alongside HTTP and HTTPS, which is what lets anti-detect browsers and scraping frameworks connect without an adapter layer.

**What happens if an IP is dead on arrival?** If it fails within the first 60 seconds of activation, the provider credits it back.

**Can I hold the same IP for weeks?** Not on revolving residential pools — and this applies to every provider selling them, not just this one. Long-lived identities need static ISP proxies, which is what 9Proxy's own support tells users who ask.

**Is 20M IPs enough?** For scraping, monitoring, ad verification, and multi-account work at typical volumes, yes. It isn't a 100M+ pool, and anyone running hundreds of thousands of concurrent exits in unusual geographies should measure coverage in their target country before committing.

Measure first, buy small, scale only what survived the test. That's the whole method, and it works on any provider you're considering.
