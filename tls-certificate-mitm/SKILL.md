---
name: tls-certificate-mitm
description: "TLS, Certificate Validation & MITM offensive playbook from 40 disclosed HackerOne reports (2 critical, 6 high, 19 medium, 13 low). Use when hunting or reviewing tls, certificate validation & mitm. Triggers: certificate, tls, verification, host, check."
license: "For authorized security testing and education only."
---

# TLS, Certificate Validation & MITM

> Distilled from **40** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

Weak transport security or certificate validation enables man-in-the-middle interception or downgrade.

## Where to hunt

- Check mobile/desktop/API clients for cert pinning and validation; test hostname/chain/revocation checks and TLS downgrade.

## Exploitation playbook

- Intercept traffic with a rogue cert where validation is missing/broken; strip TLS to capture credentials.

## Bypass techniques

- Self-signed or wrong-host certs accepted; missing revocation checks; cleartext fallback.

## Impact & escalation

- Credential/session capture, traffic tampering.

## Remediation

- Enforce full certificate validation and pinning, disable cleartext/downgrade, verify hostname and chain.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#2416725](https://hackerone.com/reports/2416725)  -  CVE-2024-2466: TLS certificate check bypass with mbedTLS
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

### 2. [#3752888](https://hackerone.com/reports/3752888)  -  CVE-2026-9545: exposing HTTP/3 early data
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

### 3. [#541502](https://hackerone.com/reports/541502)  -  [https-proxy-agent] Socket returned without TLS upgrade on non-200 …
*medium*

```http
GET / HTTP/1.1
Host: www.google.com
Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=
```

### 4. [#3150884](https://hackerone.com/reports/3150884)  -  CVE-2025-4947: QUIC certificate check skip with wolfSSL
*medium*

```bash
curl -V
WARNING: this libcurl is Debug-enabled, do not use in production

curl 8.13.0 (x86_64-pc-linux-gnu) libcurl/8.13.0 wolfSSL/5.8.0 zlib/1.3.1 libidn2/2.3.8 libpsl/0.21.2 ngtcp2/1.13.0-DEV nghttp3/1.1
Release-Date: 2025-04-02
Protocols: dict file ftp ftps gopher gophers http https imap imaps ipfs ipns mqtt pop3 pop3s rtsp smtp smtps telnet tftp ws wss
Features: alt-svc AsynchDNS Debug HSTS HTTP3 HTTPS-proxy IDN IPv6 Largefile libz PSL SSL threadsafe TrackMemory UnixSockets
```

### 5. [#3694390](https://hackerone.com/reports/3694390)  -  CVE-2026-7009: OCSP stapling bypass with Apple SecTrust
*medium*

```bash
curl --version
curl 8.20.0-DEV (Darwin) libcurl/8.20.0-DEV OpenSSL/3.6.1 zlib/1.2.12 brotli/1.2.0 zstd/1.5.7 libidn2/2.3.8 libpsl/0.21.5 nghttp2/1.68.0
Release-Date: [unreleased]
Protocols: dict file ftp ftps gopher gophers http https imap imaps ipfs ipns ldap ldaps mqtt mqtts pop3 pop3s rtsp smb smbs smtp smtps telnet tftp ws wss
Features: alt-svc AsynchDNS brotli HSTS HTTP2 HTTPS-proxy IDN IPv6 Largefile libz NTLM PSL SSL threadsafe TLS-SRP UnixSockets zstd
```

### 6. [#3694390](https://hackerone.com/reports/3694390)  -  CVE-2026-7009: OCSP stapling bypass with Apple SecTrust
*medium*

```bash
curl --version
curl 8.20.0-DEV (Darwin) libcurl/8.20.0-DEV OpenSSL/3.6.1 zlib/1.2.12 brotli/1.2.0 zstd/1.5.7 libidn2/2.3.8 libpsl/0.21.5 nghttp2/1.68.0
Release-Date: [unreleased]
Protocols: dict file ftp ftps gopher gophers http https imap imaps ipfs ipns mqtt mqtts pop3 pop3s rtsp smtp smtps telnet tftp ws wss
Features: alt-svc AppleSecTrust AsynchDNS brotli HSTS HTTP2 HTTPS-proxy IDN IPv6 Largefile libz PSL SSL threadsafe TLS-SRP UnixSockets zstd
```

More payloads: see [payloads.md](payloads.md) (54 curated).

## Recurring patterns in this dataset

Most frequent terms across the 40 reports (term (count)): `certificate` (32), `tls` (24), `verification` (18), `host` (12), `check` (12), `allowed` (11), `node.js` (11), `session` (10), `ocsp` (9), `server` (9), `proxy` (8), `curl` (8), `man-in-the-middle` (7), `caused` (7), `validation` (7), `certificates` (7), `undici` (6), `attacks` (6)

## Worked example  -  [report #746733](https://hackerone.com/reports/746733)

*Remotely trigger an assertion on a TLS server with a malformed certificate string* (critical,  - )

> Summary: Connecting to a NodeJS TLS server with a client certificate that has a type 19 string in its subjectAltName will crash the TLS server if it tries to read the peer certificate. Affected versions include v10.17.0 and v13.1.0. This is related to issue https://github.com/nodejs/node/issues/30521 but it works the other way around: in that issue, the client crashes; in this example, the server crashes. It is likely that the fix for that issue will also fix this. Description: Using e.g. node-forge it is possible to create certificates without common name and with any subjectAltName content. Hence anybody can create a malformed certificate and send it to a node server. The server will enco…

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#746733](https://hackerone.com/reports/746733) | critical |  -  | nodejs | Remotely trigger an assertion on a TLS server with a malformed certificate string |
| [#329645](https://hackerone.com/reports/329645) | critical |  -  | ibb | Silent omission of certificate hostname verification in LibreSSL and BoringSSL |
| [#1599063](https://hackerone.com/reports/1599063) | high | $1,000 | ibb | Undici ProxyAgent vulnerable to MITM |
| [#811502](https://hackerone.com/reports/811502) | high |  -  | nodejs | Node.js: TLS session reuse can lead to hostname verification bypass |
| [#608620](https://hackerone.com/reports/608620) | high |  -  | ibb | Industry-Wide MITM Vulnerability Impacting the JVM Ecosystem |
| [#982130](https://hackerone.com/reports/982130) | high |  -  | concretecms | Fetching the update json scheme from concrete5 over HTTP leads to remote code execution |
| [#1583680](https://hackerone.com/reports/1583680) | high |  -  | nodejs | Undici does not use CONNECT or otherwise validate upstream HTTPS certificates when usin… |
| [#879740](https://hackerone.com/reports/879740) | high |  -  | central-security-project | Repositories of datanucleus are fetched over insecure protocol (http insted of https) |

*See [reference.md](reference.md) for all 40 reports in this class.*
