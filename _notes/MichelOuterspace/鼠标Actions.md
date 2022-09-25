# 鼠标Actions

- 鼠标悬停
    
    ```java
    @Test
      public void mouseHoverAction() throws Exception {
          //先滑动到能见，并定位到需要鼠标悬停的元素
          JavascriptExecutor js;
          js = (JavascriptExecutor) driver;
          js.executeScript("window.scrollBy(0,600);");
          WebElement webElement = driver.findElement(By.id("mouseHover"));
          //Actions类实例化，driver作为参数
          **Actions actions = new Actions(driver);**
          //actions的操作，最后都要加perform()才是真的执行了。之后就可以查找到鼠标悬停才会出现的元素
    			//actions还可以实现点击，moveTo之后click之后perform
          **actions.moveToElement(webElement).perform();**
      }
    ```
    
- 拖拽页面上的元素
    
    ```java
    public class DragAndDropActions {
    	private WebDriver driver;
    	private String baseUrl;
    
    	@Before
    	public void setUp() throws Exception {
    		driver = new ChromeDriver();
    		baseUrl = "https://jqueryui.com/droppable/";
    
    		// Maximize the browser's window
    		driver.manage().window().maximize();
    		driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);
    	}
    	
    	@Test
    	public void testDragAndDrop() throws Exception {
    		driver.get(baseUrl);
    		Thread.sleep(2000);
    		driver.switchTo().frame(0);
    
    		WebElement fromElement = driver.findElement(By.id("draggable"));
    		WebElement toElement = driver.findElement(By.id("droppable"));
    		
    		Actions action = new Actions(driver);
    		// 方法一：Drag and drop，最后都要.build().perform()
    		action.dragAndDrop(fromElement, toElement).build().perform();
    		// 方法二：Click and hold点住鼠标, move to element移动到, release松开鼠标, build and perform
    		action.clickAndHold(fromElement).moveToElement(toElement).release().build().perform();
    	}
    
    	@After
    	public void tearDown() throws Exception {
    		// driver.quit();
    	}
    }
    ```
    
- 拖动滚动条
    
    ```java
    @Before
    	public void setUp() throws Exception {
    		driver = new ChromeDriver();
    		baseUrl = "https://jqueryui.com/slider/";
    
    		// Maximize the browser's window
    		driver.manage().window().maximize();
    		driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);
    	}
    	
    	@Test
    	public void testSliderActions() throws Exception {
    		driver.get(baseUrl);
    		driver.switchTo().frame(0);
    		Thread.sleep(3000);
    		WebElement element = driver.findElement(By.xpath("//div[@id='slider']/span"));
    
    		// 用Actions类dragAndDropBy(拖动条元素,横坐标,纵坐标)方法
    		**Actions action = new Actions(driver);
    		action.dragAndDropBy(element, 100, 0).perform();**		
    	}
    ```