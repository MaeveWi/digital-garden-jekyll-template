Jenkins项目页面，拉到最下面 点击“REST API” 

进入API页面  

Perform a build --- 提供可以自动化执行该job的URL:
	http://18.166.28.146:8888/jenkins/job/fas_api_test/buildWithParameters

需要生成自己的jenkins_token：
	jenkins - Manage Jenkins - Manage Users - Admin - configure - API Token
将此Token配置到服务器全局变量中

在[[gitlab-ci.yml内容]]请求：
```yml
script:
    - curl -X POST http://10.10.11.215:8888/jenkins/job/fas_api_test/buildWithParameters --user ${JENKINS_USER}:${JENKINS_TOKEN}
``` 

