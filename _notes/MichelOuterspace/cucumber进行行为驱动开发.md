# cucumber进行行为驱动开发

是从feature文件作为测试的入口：首先要创建一个文件，后缀名为.feature。一个feature文件里面可以写多个Scenario。

将原来的测试类中的一个测试方法，分成多个方法，分别加@Given, @When等标签

```java
public class TestingSteps {
WebDriver driver;
		@Given("^User is on Login Page$")
		public void user_is_on_Login_Page() {
			System.setProperty("webdriver.chrome.driver", "/Users/gaoyan/eclipse-workspace/driver/chromedriver");
			driver = new ChromeDriver();
			String baseUrl = "<https://mail.qq.com/cgi-bin/loginpage>";
			
		
			// Maximize the browser's window
			driver.manage().window().maximize();
			driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);
			driver.get(baseUrl);
		}
		
		@When("^User enters UserName and Password$")
		public void user_enters_UserName_and_Password() {
			driver.switchTo().frame("login_frame");
			WebElement emailField = driver.findElement(By.id("u"));
			emailField.sendKeys("5159045");
			
			WebElement passwordField = driver.findElement(By.id("p"));
			passwordField.sendKeys(Constants.password);
		}
		
		@When("^Click Login button$")
		public void click_Login_button() throws InterruptedException {
			WebElement goButton = driver.findElement(By.id("login_button"));
			goButton.click();
			Thread.sleep(3000);
		}
		
		@Then("^He can visit mail home page$")
		public void he_can_visit_mail_home_page() {
			WebElement welcomeText = driver.findElement(By.xpath("//b[text()='Diana']"));
		}
		
		@Then("^Account name is displayed$")
		public void account_name_is_displayed(){
			System.out.println("登录成功");
		}
}	
```

### 例：注意 只有Feature和Scenario后面要加“：”

**Feature:** Login
**Scenario:** Successful Login with valid credentials
**Given** User is on Login Page
**When** User enters UserName and Password
**Then** He can visit mail home page

- **Gherkin 支持的关键字列表:**
    
    • Feature
    • Background
    • Scenario
    • Given
    • When
    • Then
    • And
    • But
    
- Feature: 关键字
    
    每个文件都是从feature这个关键字开始，他定义了你要在feature file里测试的功能.
    
    Feature: Login Test
    Or
    Feature: Login Test
    Description: This feature will test Login functionality
    
- Background: 关键字
    
    Background关键字用于定义步骤，这些步骤对于feature file中所有测试都是通用的。例如，要到达邮箱主页，需要执行以下步骤:
    
    • Navigate to Login Page
    • Click on the Login button
    
    Feature: Login Action
    Background: Open Login Page
    Description: This feature will test Login functionality 
    Scenario: Successful Login with Valid Credentials
    Given User is on Login Page
    When User enters Username and Password
    Then He can visit mailbox home page
    
- Scenario: 关键字
    
    每个测试都称为一个Scenario，并使用Scenario:关键字进行描述
    
    Feature: Login Action
    Description: This feature will test Login functionality
    Scenario: Successful Login with Valid Credentials
    
- Given 关键字
    
    Given 定义了一个测试的先决条件。
    
    Feature: Login Action
    Description: This feature will test Login functionality
    Scenario: Successful Login with Valid Credentials
    Given User is on Login Page
    
- When 关键字
    
    When 关键字定义将要执行的测试操作. 
    
    Scenario: Successful Login with Valid Credentials
    Given User is on Login Page
    When User enters Username and Password
    
- Then 关键字
    
    Then 关键字定义测试的结果/结果。
    
    Feature: Login Action
    Description: This feature will test Login functionality
    Scenario: Successful Login with Valid Credentials
    Given User is on Login Page
    When User enters Username and Password
    Then He can visit mailbox home page
    
- And 关键字
    
    And 关键字用于向步骤添加条件。
    
    Feature: Login Action
    Description: This feature will test Login functionality
    Scenario: Successful Login with Valid Credentials
    Given User is on Login Page
    When User enters Username and Password
    And Clicks the Sing In button
    Then He can visit mailbox home page
    And It displays the logout link
    
- But 关键字
    
    But 关键字用于添加否定类型的注释。
    
    Feature: Login Test
    Description: This feature will test Login functionality
    Scenario: Successful Login with Valid Credentials
    Given User is on Login Page
    When User enters Username and Password
    And Clicks the Sing In button
    But The user credentials are wrong
    Then Message displayed Wrong Username & Password