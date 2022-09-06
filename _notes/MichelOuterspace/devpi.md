## What
[[pypi]]私有服务系统，一个pypi server 和 packaging、testing、release工具  

文档：[doc](https://docs.pytest.org/en/latest/)

## Why
python有非常多的第三方包，这些包可以通过pip install安装。  而对于一个多pythoner团队，内部私有pypi库是非常重要的：
1. 在企业内部，多人团队协同开发,特别是近几年[微服务](https://so.csdn.net/so/search?q=%E5%BE%AE%E6%9C%8D%E5%8A%A1&spm=1001.2101.3001.7020)模式的流行，为了减少公有功能的重复开发，建议大家封装好内部python包然后供其他成员使用。
2. 如今容器化已经比较普遍，使用容器部署python应用时，必不可少的一步就是安装依赖包，一般企业都会在生产环境禁止服务器直接访问外部网络，这就导致无法通过官方源来安装python包。即使没有禁止访问，也会因为某些原因导致使用官方源安装包时速度非常慢。这就需要pypi私有仓库
### advantages
1. devpi支持使用豆瓣、清华等镜像源作为下载源，当安装的包在devpi-server不存在时，devpi会先从指定的下载源下载并缓存以此保证后续的下载速度。
2. devpi支持缓存,只要安装一次，这个包就会缓存在devpi服务端，以后安装python包时将直接从devpi服务端下载，这点在企业生产环境将非常高效。只需要允许devpi服务器访问豆瓣或者清华源地址即可为生产环境服务器提供稳定高速的pypi包下载服务。


## How
从devpi  pip install python包时，devpi会自动从其他（默认官方）服务器下载python包，并缓存下来，当它处于离线状态时，会直接将缓存中的包反馈给你。

#### 设置镜像仓库的镜像源，如豆瓣源、清华源：

使用客户端连接到devpi-server后，执行命令
```
devpi index root/pypi mirror_url="https://pypi.doubanio.com/simple/"
devpi index root/pypi mirror_url="https://pypi.tuna.tsinghua.edu.cn/simple/"
```

#### 修改web搜索页面
devpi的默认web页面比较简陋,可以通过修改site-packages/devpi_web/templates/root.pt来做适当的定制，如企业名称、企业logo等


### devpi分为三个部分:
1. devpi-server: 用于索引以及基于用户或团队的索引，这些索引可以从pypi.org站点或者豆瓣、清华源继承
2. devpi-web: devpi-server的插件，提供web和搜索界面
3. devpi-client: 命令行工具，用于创建用户，使用索引，上传包等功能




