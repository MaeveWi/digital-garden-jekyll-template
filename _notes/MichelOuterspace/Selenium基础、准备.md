## 基础，准备

### JAVA基础
- JAVA的四大特性
    抽象：
    封装：对方法封装 是隐藏方法内部实现细节；对类封装是隐藏类的。。
    继承：
    多态：（继承父类 extends，实现接口 implements）
- Java文件，编译生成class，jvm识别class，运行
- 命名规则：驼峰，不能数字开头，特殊符号可以用_$
- 环境变量：能够让该目录下所有文件，在任何路径下都能运行

## Maven
主要是为了方便地导入第三方jar包（和管理项目 我们测试不需要），通过pom.xml文件，直接写上需要jar包的坐标，maven就可以自动 从本地仓库 或者公司内部maven私服 或者中央仓库（在国内用阿里云的镜像，就是一开始配置文件里加的那个）下载导入。

    1. 下载安装Apache-Maven之后，在根目录下创建一个 本地仓库文件夹repository，用于存放各种jar包.

    2. 然后修改conf文件夹中的config文件，增加一个阿里云镜像，并修改本地仓库地址为刚才新建的文件夹地址。

    3. 然后在Ideal中集成一下Maven，创建新项目设置setting for new projects中，maven配置地址改成自己的maven地址
    
    4. 其中最重要的是有一个pom文件，pom是一个主文件，不能轻易删改。需要在pom.xml中修改一下maven编译的jdk版本 和编码格式，因为默认运行的版本是1.5：


```xml
    <properties>
            <maven.compiler.target>1.8</maven.compiler.target>
            <maven.compiler.source>1.8</maven.compiler.source>
            <!--文件拷贝时的编码-->
            <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
            <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
            <!--编译时的编码-->
            <maven.compiler.encoding>UTF-8</maven.compiler.encoding>
            <aspectj.version>1.9.2</aspectj.version>
    </properties>
```
    
    pom.xml文件中怎么写jar包坐标呢？---直接搜maven仓库mvnrepository，搜索jar包名称，找到复制进去就行了。导入成功后，在左边的Library和右边的Maven中都可以看到。右边右键还可以下载源码和文档
    
### Selenium浏览器驱动配置
- 当代码写的没问题，但是浏览器启动不起的时候 很有可能就是兼容性问题，以下是较新的互相兼容的版本：
        
        selenium WebDriver 3.6.0
        geckodriver 0.19
        FF 55.0.3
- 需要下载浏览器驱动，并且在代码中，new driver之前，设置系统属性：
        或者把存放drivers的目录放到**path**中，这样就不用每次都要写：
```java
        System.setProperty("webdriver.gecko.driver", "E:\\maeve\\JAVA\\javaTestNG\\geckodriver.exe");
```

- 浏览器驱动下载地址：
	- 火狐浏览器：webdriver.gecko.driver [https://github.com/mozilla/geckodriver/releases](https://github.com/mozilla/geckodriver/releases)
	- chrome浏览器：webdriver.chrome.driver [http://chromedriver.storage.googleapis.com/index.html](http://chromedriver.storage.googleapis.com/index.html)
	- IE浏览器：webdriver.ie.driver [http://selenium-release.storage.googleapis.com/index.html](http://selenium-release.storage.googleapis.com/index.html)
- IE浏览器会有一些问题导致无法正常运行，需要设置：
	1. 64位电脑 也下载32位的IEDriverServer
	2. Internet选项-安全-所有 保护模式关掉
	3. 窗口要最大化driver.manager().window().maximize();
	4. 需要用到DesiredCapabilities类来设置IE属性如下
```java
caps.setCapability(InternetExplorerDriver.IGNORE_ZOOM_SETTING,true);  //发现只有这个有效
//caps.setCapability(InternetExplorerDriver.NATIVE_EVENTS,false);
//caps.setCapability(InternetExplorerDriver.REQUIRE_WINDOW_FOCUS,false);
//caps.setCapability(InternetExplorerDriver.ENABLE_PERSISTENT_HOVERING,false);
//caps.setCapability(InternetExplorerDriver.IE_ENSURE_CLEAN_SESSION,true);
//caps.setCapability(InternetExplorerDriver.INTRODUCE_FLAKINESS_BY_IGNORING_SECURITY_DOMAINS,true);
```

