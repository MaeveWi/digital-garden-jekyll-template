# Selenium
[[Selenium基础、准备]]

## 面试问题：

- 什么是WebDriver?
    
    WebDriver是一个interface接口，selenium2.0之后就叫WebDriver了
    
- 如何用在不同的浏览器上进行测试？
    
    **每一个浏览器都有对应的一个Driver类来进行测试，他们都实现了WebDriver接口，都实现了其中的方法。有FirefoxDriver、ChromeDriver、InternetExplorerDriver、SafariDriver、EventFiringWebDriver、HTMLUnitDriver、RemoteWebDriver.**
    

[[Hello World 设置平台和开启浏览器]]

[[框架]]

[[元素定位方法]]

[[页面元素的操作]]

[[页面的操作]]

[[封装的类和方法]]

[[鼠标Actions]]

[[自动化框架]]

[[TestNG]]

[[封装截图方法]]

[[测试日志和报告生成]]

[[找到当前页所有links链接并检查]]

[[json和JAVA对象转换]]

[[Excel解析]]

[[sikuli操控浏览器之外的控件]]

[[事件监听器（自动记录log）]]

[[性能 ]]

[[cucumber进行行为驱动开发]]

- 构建的生命周期：
    
    包含一系列构建**阶段**，一定是从头按顺序构建，可以通过maven命令只运行到某个阶段
    
    有三个类型的生命周期：default，clean，site（不常用）
    
    - default生命周期的阶段（不完全）：
        1. validate-验证项目是否正确，所有的必要信息可用
        2. initialize-初始化构建状态，例如设置属性
        3. compile-编译
        4. test-compile-编译测试源代码到测试的目的目录中
        5. test-使用合适的单元测试框架测试编译好的源代码
        6. package-将编译后的代码 采用指定的格式进行打包（jar/war/zip）
        7. verify-执行检查，以确保满足质量标准
        8. install-将软件包安装到本地库中，可以用作本地其他项目的依赖
        9. depoly-将最终包复制到远程仓库，以便与其他开发人员和项目共享
    
    在项目文件夹下运行 mvn test ——执行test及之前的全部生命周期
    
- Maeven
    - test文件夹下放单元测试和集成测试，可以直接访问main中的所有方法
    - selenium不需要访问源代码，测试类可以放在test文件夹下的包内
    - 在maven中创建测试类必须要遵守命名规则，否则构建成功但测试类不会运行：要以Test开头或者结尾 或者TestCase结尾
    - 用sureFile插件，集成testNG到maven
        
        pom文件中加profile：
        
        ```xml
        <profiles>
            <profile><!--创建多个profile来选择想要执行的Test xml，用maven命令 例如：mvn test -PSmokeTest-->
                <id>SmokeTest</id>
                <build>
                    <plugins>
                        <plugin>
                            <groupId>org.apache.maven.plugins</groupId>
                            <artifactId>maven-surefire-plugin</artifactId>
                            <version>3.0.0-M5</version>
                            <configuration>
                                <suiteXmlFiles>
                                    <suiteXmlFile>testng1.xml</suiteXmlFile>
                                    <!--<suiteXmlFile>testng2.xml</suiteXmlFile> 最好不要在这里面放多个test的xml,这样他们还是会一起执行-->
                                </suiteXmlFiles>
                            </configuration>
                        </plugin>
                    </plugins>
                </build>
            </profile>
            <profile>
                <id>Regression</id>
                <build>
                    <plugins>
                        <plugin>
                            <groupId>org.apache.maven.plugins</groupId>
                            <artifactId>maven-surefire-plugin</artifactId>
                            <version>3.0.0-M5</version>
                            <configuration>
                                <suiteXmlFiles>
                                    <suiteXmlFile>testng2.xml</suiteXmlFile>
                                </suiteXmlFiles>
                            </configuration>
                        </plugin>
                    </plugins>
                </build>
            </profile>
        </profiles>
        ```
        
    - 然后，用jenkins在每次构建时持续的进行测试。可以跑所有的自动化测试
        
        在设置里面的buildTriggers可以设置定时构建任务
        
        ```xml
        共五个位置，分别代表：第几分钟，第几小时，日，月，周几
        举例：
        	每分钟运行，所有时间:
        * * * *
        	每小时的 0 分运行 (每小时间隔):
        0 * * * *
        	这也是每小时运行一次，但在 15 分钟运行 (00:15,01:15,02:15):
        15 * * * *
        	每天 2:30 跑一次:
        30 2 * * *
        	每月运行一次，在每月的第二天午夜(1 月 2 日 12:00am, 2 月 2 日
        12:00am):
        0 0 2 * *
        	星期一将每小时运行一次:
        0 * * * 1
        	可以使用逗号分隔的多个数字。每小时运行三次，分别在 0 分钟、
        10 分钟和 20 分钟:
        0,10,20 * * * *
        	也使用除法算子。每 10 分钟运行一次:
        */10 * * * *
        	‘-’可用于指定范围。在早上 5 点到 10 点之间每小时运行一次:
        0 5-10 * * *
        ```
        
        - 自动发送测试报告邮件：
            
            装插件：EmailExtension，
            
            在job的config中Add post-build action的Editable Email Notification做好配置，填入收件人、邮件模板、邮件主题、触发条件等。
            
        
- 数据库测试，添加mysqlDriver依赖
    
    可以用Properties对象来传用户名和密码，也可以直接用String来传用户名密码
    
    ```java
    import org.testng.annotations.AfterClass;
    import org.testng.annotations.BeforeClass;
    import org.testng.annotations.Test;
    import java.sql.*;
    import java.util.Properties;
    public class mysqlTesting {
            // Connection 对象
            static Connection conn = null;
            // Statement 对象
            private static Statement stmt;
            // 结果集
            private static ResultSet results = null;
            // 数据库URL，最后面的是数据库名称，可以另设一个数据库名称常量
            public static String DB_URL = "jdbc:mysql://10.200.79.70:92/hashme_account";
    				//Oracle："jdbc:oracle:thin:@localhost:1521/sid"
            // 数据库用户名
            public static String DB_USER = "root";
            // 数据库密码
            public static String DB_PASSWORD ="@wx123456";
            // Driver
            public static String driver = "com.mysql.cj.jdbc.Driver";//oracle.jdbc.driver.OracleDriver
    
            // WebDriver
    				public static WebDriver dv;
    
            @BeforeClass
            public void beforeClass() {
                // 初始化 WebDriver
         	  	 dv = new FirefoxDriver();
    
                // 也可以用Properties来传数据库用户名密码
                /*
    						Properties props = new Properties();
                props.setProperty("user", "root");
                props.setProperty("password","@wx123456");
    						*/
                try {
                    // STEP 1: 注册 JDBC driver
                    Class.forName(driver).newInstance();
    
                    // STEP 2: 连接数据库
                    System.out.println("Connecting to a selected database...");
                    conn = DriverManager.getConnection(DB_URL, DB_USER, DB_PASSWORD);
    						 		// 用properties传数据库密码
    								// conn = DriverManager.getConnection(DB_URL, props);
                    System.out.println("Connected database successfully...");
    
                    // STEP 3: Statement object to send the SQL statement to the Database
                    System.out.println("Creating statement...");
                    stmt = conn.createStatement();
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }
    
            @Test
            public void test() throws SQLException {
                String query = "select * from hashme_account.account";
                try {
                    // STEP 4: 从结果集里提取数据
                    results = stmt.executeQuery(query);
                    while (results.next()) { 
    									 //根据列名，取出每一个数据
                        int id = results.getInt("id");
                        String email = results.getString("email");
                        String uuid = results.getString("uuid");
                       
                        //显示值
                        System.out.println("ID"+id);
                        System.out.println("email"+email);
                        System.out.println("uuid"+uuid);
                        
                        //获取到web页面的数据，用于和数据库的数据比对
    			          		WebElement element = dv.findElement(By.id("uid"));
    			          		String actrualUserName = element.getText();
    			          		Assert.assertEquals(actrualUserName, first);
    
                    }
                    results.close();
                } catch (SQLException se) {
                    // 处理 JDBC errors
                    se.printStackTrace();
                } catch (Exception e) {
                    // 处理 Class.forName errors
                    e.printStackTrace();
                }
            }
    
            @AfterClass
            public void afterClass() {
                try {
                    if (results != null)
                        results.close();
                    if (stmt != null)
                        stmt.close();
                    if (conn != null)
                        conn.close();
                } catch (SQLException se) {
                    se.printStackTrace();
                }
            }
        }
    ```
    
    - MongoDB数据库测试
        
        下载MongoDB Driver，然后加入library
        
        ```java
        // Download Driver - http://mongodb.github.io/mongo-java-driver/
        public class DatabaseTestingMongoDB {
        	
        	MongoClient mongoClient = null;
        	MongoDatabase db = null;
        
        	@BeforeClass
        	public void beforeClass() {
        		try {
        			// STEP 1: 连接到数据库
        			mongoClient = new MongoClient("localhost",27017);
        			db = mongoClient.getDatabase("users");
        			
        			System.out.println("Connect to database successfully");
        		} catch (Exception e) {
        			System.err.println(e.getClass().getName() + ": " + e.getMessage());
        		}
        	}
        
        	@Test
        	public void test() throws Exception {
        		try {
        			// STEP 2: 获取Collection集合
        			MongoCollection<Document> table = db.getCollection("user_info");
        
        			// STEP 3: 提取数据
        			BasicDBObject searchQuery = new BasicDBObject();
        			searchQuery.put("first_name", "Lily");
        			FindIterable<Document> cursor = table.find(searchQuery);
        			// STEP 4: 遍历数据
        			for (Document obj :cursor) {
        				String firstName = obj.getString("first_name");
        				System.out.println(firstName);
        				System.out.println("************************************");
        				System.out.println(obj.toString());
        				
        //				Assert.assertEquals("", "");
        			}
        		} catch (Exception e) {
        			// 异常处理
        			e.printStackTrace();
        		}
        	}
        }
        ```