## What
就是Client客户端的url工具的意思，**command line tool and library**  for transferring data with URLs.  
它的功能非常强大，命令行参数多达几十种。如果熟练的话，完全可以取代 Postman 这一类的图形界面工具。
[官网](https://curl.se/)      [Curl_Cookbook](https://catonmat.net/cookbooks/curl)

使用：
网页开发者工具，选择某个接口，可以右键复制curl命令，然后在命令行进行请求。
For example：
```curl
curl 'http://152.32.185.103:9003/api/login' \
  -H 'Accept: application/json' \
  -H 'Accept-Language: zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7,zh-TW;q=0.6' \
  -H 'Content-Type: application/json;charset=UTF-8' \
  -H 'Origin: http://152.32.185.103:9003' \
  -H 'Proxy-Connection: keep-alive' \
  -H 'Referer: http://152.32.185.103:9003/user/login?redirect=http://152.32.185.103:9003/dashboard' \
  -H 'TOKEN: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJVc2VySWQiOjU4OSwiZXhwIjoxODc4MzQ3NTE1fQ.JK4Ja6f8o-NEgkpuZOhv-d7sVpqmKFuvQdFBqXC_RX4' \
  -H 'User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36' \
  --data-raw $'{"Name":"wya9003","LoginPassword":"123456asD\u0021@1","TwoFactorCode":null,"type":"account"}' \
  --compressed \
  --insecure
```


