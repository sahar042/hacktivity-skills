---
name: file-upload
description: "Unrestricted File Upload offensive playbook from 9 disclosed HackerOne reports (2 critical, 1 high, 4 medium, 2 low). Use when hunting or reviewing unrestricted file upload. Triggers: upload, file, unrestricted, sqlite, rce."
license: "For authorized security testing and education only."
---

# Unrestricted File Upload

> Distilled from **9** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

The app accepts a dangerous file (executable, HTML/SVG, polyglot) and serves or processes it in a way that leads to XSS or RCE.

## Where to hunt

- Test every upload for extension/MIME/content checks; see how and where the file is later served.

## Exploitation playbook

- Upload a web shell where server-side execution is possible; SVG/HTML for stored XSS when served inline.
- Polyglot files that pass image validation but execute as script/code.

## Bypass techniques

- Double extensions, MIME spoofing, magic-byte prefixes, null bytes, case tricks, oversized scan-limit padding.

## Impact & escalation

- Web shell → RCE; stored XSS → account takeover.

## Remediation

- Allowlist extensions+content, re-encode images, store outside web root, serve with `Content-Disposition: attachment` and a benign content type, randomize names.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#1606957](https://hackerone.com/reports/1606957)  -  Unrestricted File Upload on reddit.secure.force.com
*low, $100*

```http
POST /adhelp/apexremote HTTP/1.1
Host: reddit.secure.force.com
```

## Recurring patterns in this dataset

Most frequent terms across the 9 reports (term (count)): `upload` (10), `file` (9), `unrestricted` (6), `sqlite` (5), `rce` (3), `jdbc` (3), `database` (3)

## Worked example  -  [report #1547877](https://hackerone.com/reports/1547877)

*[Kafka Connect] [JdbcSinkConnector][HttpSinkConnector] RCE by leveraging file upload via SQLite JDBC driver and SSRF to internal Jolokia* (critical, $5,000)

> Summary: The Aiven JDBC sink includes the SQLite JDBC Driver. This JDBC driver can be used to upload SQLite database files onto the server. The HTTP sink connector allows sending HTTP requests to localhost. There is unprotected Jolokia listening on localhost:6725. JMX exports the com.sun.management:type=DiagnosticCommand MBean, which contains the jvmtiAgentLoad operation. This operation can be used to execute the SQLite database as JVM Agent by embedding the JVM Agent JAR file inside the SQLite database as an BLOB field in a table. Steps To Reproduce: {F1703051} 1. Login into my VPS: ssh ████, password: █████████@ 1. Execute nc -nlvp 4446 1. cd to jdbc-sqlite-jolokia-rce and run python3 poc…

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#1547877](https://hackerone.com/reports/1547877) | critical | $5,000 | aiven_ltd | [Kafka Connect] [JdbcSinkConnector][HttpSinkConnector] RCE by leveraging file upload vi… |
| [#2357778](https://hackerone.com/reports/2357778) | critical |  -  | mars | Unrestricted File Upload at ██████████ |
| [#833080](https://hackerone.com/reports/833080) | high | $1,500 | slack | Tricking the "Create snippet" feature into displaying the wrong filetype can lead to RC… |
| [#1890284](https://hackerone.com/reports/1890284) | medium |  -  | tiktok | Unrestricted File Upload on https://partner.tiktokshop.com/wsos_v2/oec_partner/upload |
| [#1644062](https://hackerone.com/reports/1644062) | medium |  -  | linktree | No validation to Image upload user can upload ( php APK zip files and can be used as st… |
| [#722919](https://hackerone.com/reports/722919) | medium |  -  | lemlist | Unrestricted File Upload on https://app.lemlist.com |
| [#823588](https://hackerone.com/reports/823588) | medium |  -  | stripo | Unrestricted File Upload on https://my.stripo.email and https://stripo.email |
| [#1606957](https://hackerone.com/reports/1606957) | low | $100 | reddit | Unrestricted File Upload on reddit.secure.force.com |

*See [reference.md](reference.md) for all 9 reports in this class.*
