# Enabling AmazonAdBot for Contextual Advertising

Amazon requires technical adjustments on your website to continue delivering Amazon demand on your ad placements.

Starting **April 1, 2026**, websites that do not allow AmazonAdBot will no longer be eligible for demand from Amazon Ads.

This document explains:

* Why this change is important
* What AmazonAdBot does
* What you need to change
* How to implement the changes step by step
* How to verify proper configuration

**Important:** These are general implementation guidelines. Since each infrastructure setup is different (CMS, hosting, CDN, firewall, WAF), adjustments may vary slightly.

<br>

#### Table of Contents

* [1. Background & Why This Is Important](#1-background--why-this-is-important)
* [2. What is AmazonAdBot?](#2-what-is-amazonadbot)
  * [2.1 Bot Behavior & Safety](#21-bot-behavior--safety)
* [3. Required Changes Overview](#3-required-changes-overview)
* [4. Step 1 – Update robots.txt](#4-step-1--update-robotstxt)
  * [4.1 What to check](#41-what-to-check)
  * [4.2 Example robots.txt configuration](#42-example-robotstxt-configuration)
* [5. Step 2 – Allowlist in Bot Protection / Firewall Systems](#5-step-2--allowlist-in-bot-protection--firewall-systems)
  * [5.1 User-Agent](#51-user-agent)
  * [5.2 Reverse DNS Validation](#52-reverse-dns-validation)
  * [5.3 Typical Providers](#53-typical-providers)
* [6. Verifying Genuine AmazonAdBot Traffic](#6-verifying-genuine-amazonadbot-traffic)
* [7. How to Test the Implementation](#7-how-to-test-the-implementation)
* [8. Important Notes](#8-important-notes)
* [9. Help](#9-help)

<br>

---

<br>

# 1. Background & Why This Is Important

Amazon Ads uses AmazonAdBot to:

* Classify your content (IAB categories)
* Ensure brand safety for advertisers
* Analyze contextual signals
* Improve ad relevance
* Increase fill rate

This directly impacts monetization:

If AmazonAdBot can crawl your pages:

* Better contextual matching
* Higher fill rate
* More relevant ads
* Higher revenue potential

If AmazonAdBot is blocked:

* No contextual classification
* Reduced or stopped Amazon demand
* Lower fill rate
* Revenue loss

Blocking AmazonAdBot does not only risk losing Amazon demand completely — it can also reduce performance and bidding competitiveness.

Deadline: **April 1, 2026**

After this date, sites blocking AmazonAdBot will no longer be eligible for Amazon Ads demand.

<br>

---

# 2. What is AmazonAdBot?

AmazonAdBot is a crawler operated by Amazon Ads.

It scans pages that request ads from Amazon’s advertising systems. The collected content is processed through Amazon’s classification systems to:

* Detect potentially inappropriate content
* Improve contextual targeting
* Maintain brand safety
* Improve ad performance

Official information:
[https://adbot.amazon.com](https://adbot.amazon.com)

AmazonAdBot identifies itself with the following User-Agent:

```
Mozilla/5.0 (compatible; AmazonAdBot/1.0; +https://adbot.amazon.com)
```

<br>

## 2.1 Bot Behavior & Safety

AmazonAdBot is designed to be resource-friendly and transparent:

* It honors robots.txt directives
* It respects Allow and Disallow rules
* It supports Crawl-Delay directives
* It limits scan speed
* It clearly identifies itself via User-Agent
* It originates from IP addresses whose reverse DNS resolves to `amazonadbot.com` subdomains

This crawler does not impact SEO rankings and is not used for indexing search results.

<br>

---

# 3. Required Changes Overview

Two potential blocking mechanisms must be checked:

1. robots.txt configuration
2. Bot protection / firewall / security systems

   * Cloudflare
   * Akamai
   * AWS WAF
   * Custom firewalls
   * Captcha systems
   * Rate limiting systems

Both must allow AmazonAdBot to access pages where Amazon ads are displayed.

<br>

---

# 4. Step 1 – Update robots.txt

The `robots.txt` file controls which crawlers are allowed or disallowed to access your website.

It is usually accessible at:

```
https://yourdomain.com/robots.txt
```

<br>

## 4.1 What to check

Search your robots.txt for:

```
User-agent: AmazonAdBot
```

If you find any of the following directives blocking access, they must be adjusted for ad-relevant pages:

Remove any:

```
Disallow: /
```

or other Disallow rules blocking content pages.

Regarding Crawl-Delay:

AmazonAdBot honors Crawl-Delay directives.
However, removing restrictive Crawl-Delay settings allows optimal ad performance and faster content classification.

<br>

## 4.2 Example robots.txt configuration

Correct example:

```
User-agent: AmazonAdBot
Allow: /
```

If you already use general restrictions:

```
User-agent: *
Disallow: /admin/

User-agent: AmazonAdBot
Allow: /
```

This ensures:

* Sensitive backend areas remain protected
* Editorial and ad pages are crawlable

Important: AmazonAdBot must be allowed on all pages where Amazon demand is expected.

<br>

---

# 5. Step 2 – Allowlist in Bot Protection / Firewall Systems

Even with a correct robots.txt configuration, AmazonAdBot may still be blocked by:

* CDN security layers
* Web Application Firewalls (WAF)
* Bot management systems
* Rate limiting rules
* Captcha protection

If you use such systems, you must explicitly allow AmazonAdBot.

<br>

## 5.1 User-Agent

Allow requests containing the following User-Agent:

```
Mozilla/5.0 (compatible; AmazonAdBot/1.0; +https://adbot.amazon.com)
```

<br>

## 5.2 Reverse DNS Validation

Requests should only be allowed if:

* The IP address reverse DNS resolves to a subdomain of:

```
amazonadbot.com
```

Example:

```
crawler-52-70-xx-52.amazonadbot.com
```

To prevent spoofing:

1. Perform reverse DNS lookup on the IP
2. Verify it resolves to `*.amazonadbot.com`
3. Perform forward DNS lookup
4. Confirm it resolves back to the original IP

Amazon does not publish static IP ranges because they may change.

Allowlisting must rely on:

* User-Agent validation
* Reverse DNS verification

<br>

## 5.3 Typical Providers

Cloudflare
Create a custom rule to allow traffic when:

* User-Agent contains "AmazonAdBot"
* Reverse DNS matches amazonadbot.com

Akamai
Add an exception rule in Bot Manager for verified AmazonAdBot traffic.

AWS WAF
Create an allow rule based on:

* Header match (User-Agent)
* Reverse DNS validation logic (if implemented)

If unsure, please forward this documentation to your DevOps team or hosting provider.

<br>

---

# 6. Verifying Genuine AmazonAdBot Traffic

If you want to verify that traffic is genuinely coming from AmazonAdBot:

Step 1 – Reverse DNS Lookup

Run:

```
host <IP_ADDRESS>
```

Example:

```
host 52.70.xx.52
```

Expected result:

```
crawler-52-70-xx-52.amazonadbot.com
```

The domain must end with:

```
amazonadbot.com
```

Step 2 – Forward DNS Lookup

Run:

```
host crawler-52-70-xx-52.amazonadbot.com
```

The returned IP address must match the original IP.

This confirms the request is genuine.

On Windows systems:

Use:

```
nslookup <IP_ADDRESS>
```

The same forward and reverse validation principle applies.

<br>

---

# 7. How to Test the Implementation

1. Check robots.txt manually
   Open:

```
https://yourdomain.com/robots.txt
```

Verify AmazonAdBot is not disallowed.

2. Check server logs
   Look for:

* User-Agent containing "AmazonAdBot"
* HTTP status code 200 (not 403, 429, or 503)

3. Monitor Amazon APS Portal
   Amazon will notify you if crawling is still blocked.

<br>

---

# 8. Important Notes

* These changes only affect Amazon’s advertising crawler.
* This does not impact SEO.
* This does not expose protected backend areas when properly configured.
* Only ad-relevant content pages must be accessible.
* Amazon does not provide static IP allowlists.
* Deadline: **April 1, 2026**
* Without implementation, Amazon demand will stop.

<br>

---

# 9. Help

If you have technical questions regarding implementation, please contact:

**Ad Technology Team**<br>
adtechnology@axelspringer.com
