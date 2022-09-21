## What?
本地hosts文件是：匹配IP地址和域名的文件。

系统在通过域名服务器解析一个域名的IP地址之前，会先查看这个文件。 

比如公司局域网中一般没有架设DNS服务器，所以，为了不用每次都输入IP地址进行登录，可以通过修改hosts文件，来达到通过域名访问相关资源了。

其他用处：屏蔽某些网站；解决某些网站打不开、加快网页打开速度并减少带宽消耗。

## How?
1. 它在C:\WINDOWS\system32\drivers\etc目录下
2. 右击win键，打开 Windows PowerShell(管理员)权限，cd进入目录：C:\WINDOWS\system32\drivers\etc
3. notepad hosts 回车
4. 就可以打开该文件并保存修改了
5. 另外有可能需要：查看该文件属性-常规，去掉“只读”选项