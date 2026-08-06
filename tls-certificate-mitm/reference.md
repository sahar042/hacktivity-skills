# TLS, Certificate Validation & MITM  -  all 40 disclosed reports

Ranked by severity, then bounty, then votes.

| Report | Severity | Bounty | Program | Disclosed | Title |
| :-- | :-- | :-- | :-- | :-- | :-- |
| [#746733](https://hackerone.com/reports/746733) | critical |  -  | nodejs | 2020-02-06 | Remotely trigger an assertion on a TLS server with a malformed certificate string |
| [#329645](https://hackerone.com/reports/329645) | critical |  -  | ibb | 2019-09-26 | Silent omission of certificate hostname verification in LibreSSL and BoringSSL |
| [#1599063](https://hackerone.com/reports/1599063) | high | $1,000 | ibb | 2022-07-13 | Undici ProxyAgent vulnerable to MITM |
| [#811502](https://hackerone.com/reports/811502) | high |  -  | nodejs | 2020-06-03 | Node.js: TLS session reuse can lead to hostname verification bypass |
| [#608620](https://hackerone.com/reports/608620) | high |  -  | ibb | 2019-09-10 | Industry-Wide MITM Vulnerability Impacting the JVM Ecosystem |
| [#982130](https://hackerone.com/reports/982130) | high |  -  | concretecms | 2021-09-22 | Fetching the update json scheme from concrete5 over HTTP leads to remote code execution |
| [#1583680](https://hackerone.com/reports/1583680) | high |  -  | nodejs | 2022-07-13 | Undici does not use CONNECT or otherwise validate upstream HTTPS certificates when using a proxy |
| [#879740](https://hackerone.com/reports/879740) | high |  -  | central-security-project | 2020-10-05 | Repositories of datanucleus are fetched over insecure protocol (http insted of https) |
| [#2435482](https://hackerone.com/reports/2435482) | medium | $2,580 | ibb | 2024-03-29 | CVE-2024-2466: TLS certificate check bypass with mbedTLS (reward request) |
| [#2208860](https://hackerone.com/reports/2208860) | medium | $1,270 | ibb | 2023-11-30 | Integrity checks according to policies can be circumvented in Node.js 20 and Node.js 18 |
| [#1455411](https://hackerone.com/reports/1455411) | medium | $1,200 | ibb | 2022-01-20 | Invalid handling of X509_verify_cert() internal errors in libssl (CVE-2021-4044) |
| [#3153497](https://hackerone.com/reports/3153497) | medium |  -  | curl | 2025-05-28 | CVE-2025-5025: No QUIC certificate pinning with wolfSSL |
| [#1048457](https://hackerone.com/reports/1048457) | medium |  -  | curl | 2020-12-09 | CVE-2020-8286: Inferior OCSP verification |
| [#3150884](https://hackerone.com/reports/3150884) | medium |  -  | curl | 2025-05-28 | CVE-2025-4947: QUIC certificate check skip with wolfSSL |
| [#2669852](https://hackerone.com/reports/2669852) | medium |  -  | curl | 2024-09-11 | CVE-2024-8096: OCSP stapling bypass with GnuTLS |
| [#3694390](https://hackerone.com/reports/3694390) | medium |  -  | curl | 2026-04-29 | CVE-2026-7009: OCSP stapling bypass with Apple SecTrust |
| [#3812439](https://hackerone.com/reports/3812439) | medium |  -  | nodejs | 2026-07-30 | HTTPS Agent TLS session reuse skips hostname verification across identity policies (incomplete fix of CVE-2026-48934) |
| [#2416725](https://hackerone.com/reports/2416725) | medium |  -  | curl | 2024-03-27 | CVE-2024-2466: TLS certificate check bypass with mbedTLS |
| [#3633146](https://hackerone.com/reports/3633146) | medium |  -  | aws_vdp | 2026-07-28 | Sandbox User Can Inject Rogue CA Certificate into OS Trust Store via Sudo-Allowed deploy-certificates.sh |
| [#819717](https://hackerone.com/reports/819717) | medium |  -  | kubernetes | 2021-11-07 | IPv4 only clusters susceptible to MitM attacks via IPv6 rogue router advertisements |
| [#2094235](https://hackerone.com/reports/2094235) | medium |  -  | nodejs | 2023-10-13 | Integrity checks according to policies can be circumvented |
| [#3649802](https://hackerone.com/reports/3649802) | medium |  -  | nodejs | 2026-06-25 | TLS host identity verification bypass via session reuse with different servername leads to unauthorized connections |
| [#509390](https://hackerone.com/reports/509390) | medium |  -  | nextcloud | 2019-08-29 | Missing DNSSEC |
| [#541502](https://hackerone.com/reports/541502) | medium |  -  | nodejs-ecosystem | 2019-09-25 | [https-proxy-agent] Socket returned without TLS upgrade on non-200 CONNECT response, allowing request data to be sent over unencrypted connection |
| [#1429694](https://hackerone.com/reports/1429694) | medium |  -  | nodejs | 2022-02-10 | Node.js Certificate Verification Bypass via String Injection |
| [#764986](https://hackerone.com/reports/764986) | medium |  -  | kubernetes | 2021-11-04 | Man in the middle using LoadBalancer or ExternalIPs services |
| [#813279](https://hackerone.com/reports/813279) | medium |  -  | endless_group | 2020-04-01 | Lets Encrypt Certificates affected by CAA Rechecking Incident |
| [#2437050](https://hackerone.com/reports/2437050) | low | $560 | ibb | 2024-03-29 | CVE-2024-2379: QUIC certificate check bypass with wolfSSL |
| [#1278254](https://hackerone.com/reports/1278254) | low | $150 | nodejs | 2021-09-10 | Built-in TLS module unexpectedly treats "rejectUnauthorized: undefined" as "rejectUnauthorized: false", disabling all certificate validation |
| [#437800](https://hackerone.com/reports/437800) | low | $100 | fanduel | 2018-12-21 | Passive mixed content issues on the site https://*.fanduel.com |
| [#3558277](https://hackerone.com/reports/3558277) | low |  -  | pyca | 2026-03-20 | Fail-Open in set_tlsext_servername_callback on pyopenssl via unhandled exceptions leads to security bypass |
| [#3355218](https://hackerone.com/reports/3355218) | low |  -  | curl | 2025-11-05 | CVE-2025-10966: missing SFTP host verification with wolfSSH |
| [#2298922](https://hackerone.com/reports/2298922) | low |  -  | curl | 2024-01-31 | CVE-2024-0853: OCSP verification bypass with TLS session reuse |
| [#3477116](https://hackerone.com/reports/3477116) | low |  -  | curl | 2026-01-07 | CVE-2025-15079: libssh global knownhost override |
| [#2410774](https://hackerone.com/reports/2410774) | low |  -  | curl | 2024-03-27 | CVE-2024-2379: QUIC certificate check bypass with wolfSSL |
| [#3797526](https://hackerone.com/reports/3797526) | low |  -  | curl | 2026-06-24 | CVE-2026-12064: proto-default skips SSH verification |
| [#1129529](https://hackerone.com/reports/1129529) | low |  -  | curl | 2021-04-30 | CVE-2021-22890: TLS 1.3 session ticket proxy host mixup |
| [#1991427](https://hackerone.com/reports/1991427) | low |  -  | ibb | 2023-06-25 | CVE-2023-28321: IDN wildcard match |
| [#3752888](https://hackerone.com/reports/3752888) | low |  -  | curl | 2026-06-24 | CVE-2026-9545: exposing HTTP/3 early data |
| [#1950627](https://hackerone.com/reports/1950627) | low |  -  | curl | 2023-05-18 | CVE-2023-28321: IDN wildcard match |
