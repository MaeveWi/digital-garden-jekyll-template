cd /c/ProgramData/
mkdir pip
vim pip.ini
```linux
[global]
trusted-host = brokerage-qa.hashkey.com
index-url = http://brokerage-qa.hashkey.com/devpi/root/dev/+simple/
```

保存完成配置后，再次pip install就通过配置的镜像源获取
