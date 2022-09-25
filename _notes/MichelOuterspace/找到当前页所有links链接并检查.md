# 找到当前页所有links链接并检查

```java
public class FindLinksAndCheck {
    private WebDriver driver;
    private String baseUrl;
    private HotelSearchPage hotelSearchPage;
    @Before
    public void setUp() throws Exception{
        driver = new ChromeDriver();
        baseUrl = "https://www.ctrip.com/";
        hotelSearchPage = new HotelSearchPage(driver);
        driver.manage().window().maximize();
        driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);
    }
    @Test
    public void testFindLinks(){
        driver.get(baseUrl);
        List<WebElement> links = findClickableLinks(driver);
        for (WebElement l:links){
            String href = l.getAttribute("href");
            try {
                //new一个URL对象，用构造方法，参数是一个URL的字符串
                System.out.println("URL:"+href+" returned"+linkStatus(new URL(href)));
            } catch (MalformedURLException e) {
                System.out.println(e.getMessage());
            }
        }
    }

    //封装获取全部links的方法, 设置成静态 无需依赖对象可以直接调用
    public static List<WebElement> findClickableLinks(WebDriver driver){
        List<WebElement> clickableLinks = new ArrayList<WebElement>();
        //通过tag名找到页面中所有的links，tag名是“a”和“img”，并且属性href还要有值才是能点击的
        List<WebElement> links = driver.findElements(By.tagName("a"));
        links.addAll(driver.findElements(By.tagName("img")));
        //判断是否可点击
        for(WebElement l:links){
            if (l.getAttribute("href")!=null){
                clickableLinks.add(l);
            }
        }
        return clickableLinks;
    }
    //封装方法 获取links中返回的状态码
    public static String linkStatus(URL url){
        try {
            //通过java里的URL类 的openConnection()方法 返回一个URLConnection
            //且URLConnection是HttpURLConnection的父类，所以需要强制转换一下
            HttpURLConnection http = (HttpURLConnection) url.openConnection();
            //connect()方法建立链接
            http.connect();
            String responseMessage = http.getResponseMessage();
            http.disconnect();
            return responseMessage;
        } catch (IOException e) {
            return e.getMessage();
        }
    }
}
```