# Hello World 设置平台和开启浏览器：

```java
public static void main(String[] args) { 
**//加载Firefox驱动：geckodriver**
System.setProperty("webdriver.gecko.driver","E:\\maeve\\JAVA\\javaTestNG\\geckodriver.exe");
**//DesiredCapabilities类：用来设置运行的平台、浏览器
//可以基于selenium grid实现分布式自动化测试
//new的时候直接后面跟.explorer()，是设置平台和浏览器的一种方式**
DesiredCapabilities caps = new DesiredCapabilities().firefox();
**//设置想要运行的浏览器，这里设置火狐**
caps.setBrowserName("firefox");
**//设置想要运行的平台，这里设置Windows**
caps.setPlatform(Platform.WINDOWS);
**//创建的DesiredCapabilities对象作为参数，传递给WebDriver构造方法**
driver= new FirefoxDriver(caps);
**//将浏览器最大化**
driver.manage().window().maximize();
**//启动浏览器（网址以后可以作为参数传入，要字符串形式）**
String url = "http://cn.bing.com/";
driver.get(url);
**//之后可以开始 驱动页面元素实现自动化**

```