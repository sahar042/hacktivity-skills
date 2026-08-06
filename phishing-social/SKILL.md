---
name: phishing-social
description: "Phishing & Social Engineering Vectors offensive playbook from 14 disclosed HackerOne reports (2 high, 1 medium, 11 low). Use when hunting or reviewing phishing & social engineering vectors. Triggers: link, allowed, attacker, brave, github."
license: "For authorized security testing and education only."
---

# Phishing & Social Engineering Vectors

> Distilled from **14** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

Features that help attackers spoof trusted brands or craft convincing phishing  -  open redirects, email spoofing, fake login flows, or unsafe URL previews.

## Where to hunt

- Look for email-from / display-name fields, invite templates, link unfurling, and any place the app renders attacker-controlled URLs as trusted.
- Test SPF/DKIM/DMARC gaps and From-header injection on outbound mail features.

## Exploitation playbook

- Craft messages that appear to come from the product; chain with open redirect or XSS for credential capture.
- Abuse invite/share flows to send attacker links under the brand domain.

## Bypass techniques

- Homoglyph domains, subdomain tricks on allowlists, HTML/email client quirks.

## Impact & escalation

- Credential theft, OAuth token theft, mass phishing of the user base.

## Remediation

- Authenticate outbound mail, lock display names, preview untrusted links safely, and warn on off-site destinations.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#481472](https://hackerone.com/reports/481472)  -  URL link spoofing
*low, $250*

```http
POST /api/chat.postMessage HTTP/1.1
 Host: example.slack.com

...
 -----------------------------87462859699239992111770463
 Content-Disposition: form-data; name="text"

-http://example.com
+<http://evil.com|http://example.com>
 -----------------------------87462859699239992111770463
 ...
```

### 2. [#500348](https://hackerone.com/reports/500348)  -  URL filter bypass in Enterprise Grid
*low, $100*

```http
POST /api/users.profile.set HTTP/1.1
 Host: example-corp.slack.com

-----------------------------7110134921404748136166706634
 Content-Disposition: form-data; name="profile"

-{"real_name":"Akaki Tsunoda","title":"","phone":"03-9999-0000","fields":{"XfABVBP467":{"value":"https://www.mcdonalds.com","alt":"McDonald's"}}}
+{"real_name":"Akaki Tsunoda","title":"","phone":"03-9999-0000","fields":{"XfABVBP467":{"value":"tel://03-9999-0000","alt":"McDonald's"}}}
 -----------------------------7110134921404748136166706634
 ...
```

### 3. [#1031321](https://hackerone.com/reports/1031321)  -  Github Account hijack through broken link in developer.twitter.com
*high*

```http
put this link https://github.com/HunterLarco

Please let me know if you have any questions. I am happy to help
```

### 4. [#1124540](https://hackerone.com/reports/1124540)  -  Login CSRF : Login Authentication Flaw on  https://liberapay.com/
*low*

```html
<script>history.pushState('', '', '/')</script>
```

## Recurring patterns in this dataset

Most frequent terms across the 14 reports (term (count)): `link` (6), `allowed` (5), `attacker` (5), `brave` (5), `github` (4), `broken` (4), `csrf` (4), `website` (4), `showing` (4), `ios` (4), `spoofing` (4), `hijack` (3), `another` (3), `potentially` (3), `login` (3), `information` (3), `victim` (3), `label` (3)

## Worked example  -  [report #1031321](https://hackerone.com/reports/1031321)

*Github Account hijack through broken link in developer.twitter.com* (high,  - )

> Description A link in https://developer.twitter.com/en/docs/twitter-api/tools-and-libraries was broken and anyone could create that account which leads to account impersonate Steps To Reproduce 1) Visit https://developer.twitter.com/en/docs/twitter-api/tools-and-libraries 2) Scroll down to Javascript/Node.js and click on by @HunterLarco (v2) 3) Create github username HunterLarcol 4) When someone visits and scroll down to javascript/Node.js and click on @HunterLarco (v2). They are redirected to my account similar report https://hackerone.com/reports/265696 To solve this issue put this link https://github.com/HunterLarco Please let me know if you have any questions. I am happy to help Impact I…

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#1031321](https://hackerone.com/reports/1031321) | high |  -  | x | Github Account hijack through broken link in developer.twitter.com |
| [#407355](https://hackerone.com/reports/407355) | high |  -  | greenhouse | Subdomain Takeover on demo.greenhouse.io pointing to unbouncepages |
| [#652447](https://hackerone.com/reports/652447) | medium |  -  | avito | Missing SPF Records |
| [#481472](https://hackerone.com/reports/481472) | low | $250 | slack | URL link spoofing |
| [#500348](https://hackerone.com/reports/500348) | low | $100 | slack | URL filter bypass in Enterprise Grid |
| [#1124540](https://hackerone.com/reports/1124540) | low |  -  | liberapay | Login CSRF : Login Authentication Flaw on  https://liberapay.com/ |
| [#1128701](https://hackerone.com/reports/1128701) | low |  -  | security | Lack warning label when receiving a letter |
| [#515574](https://hackerone.com/reports/515574) | low |  -  | gsa_bbp | Unclaimed Github Repository Takeover on https://www.data.gov/labs |

*See [reference.md](reference.md) for all 14 reports in this class.*
