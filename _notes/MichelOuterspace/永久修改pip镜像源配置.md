cd /c/ProgramData/
mkdir pip
vim pip.ini
```linux
[global]
trusted-host = brokerage-qa.hashkey.com
index-url = http://brokerage-qa.hashkey.com/devpi/root/dev/+simple/
```

保存完成配置后，再次pip install就通过配置的镜像源获取

### [官方文档permanent index configuration for pip](https://devpi.net/docs/devpi/devpi/stable/+d/quickstart-pypimirror.html)
