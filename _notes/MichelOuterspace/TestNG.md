# TestNG

- 介绍和资料
    
    testNG是一个单元测试框架，提供了丰富的注解，来帮助我们管理 被测项目的测试类和测试方法。
    
    [http://lemfix.com/topics/969](http://lemfix.com/topics/969)
    
- 配置准备
    
    pom.xml加一下坐标
    
    ```xml
    <dependency>
    	<groupId>org.testng</groupId>
    	<artifactId>testng</artifactId>
    	<version>7.1.0</version>
    	<scope>test</scope> //加上scope这个标签，打包的时候代码不会被打进去，不影响运行
    </dependency>
    ```
    
- 断言和软断言
    
    创建被测类的对象，就能调用里面的方法，用断言来做判断，方法返回的结果是否和预期结果一致.
    
    ```java
    @Test
        public void testAddNum(){
            ClassToBeTested obj = new ClassToBeTested();
            int result = obj.addNum(1,2);
    				//断言（第一个参数是实际结果，第二个参数是期望结果）
            **Assert.assertEquals(result,3);**
    				//常用的还有
    				**Assert.assertTrue(result);
    				Assert.assertFalse(result);**
        }
    ```
    
    一旦第一个断言错误，执行失败，后面断言的都不再执行了。如果想要前面的断言失败后，后面的继续执行，要用软断言。
    
    ```java
    public void softTestAddNum(){
            SoftAssert sa = new SoftAssert();
            ClassToBeTested obj = new ClassToBeTested();
            int result = obj.addNum(1,2);
            //Assert.assertEquals(result,3);
            **sa.assertEquals(result,3)**;
            //这个语句会让前面断言错误的执行失败，否则虽然softAssert能够让后面的语句继续执行，但是看不出哪个测试执行失败
            **sa.assertAll();**
        }
    ```
    
- 注解
    
    注意使用注解时看清楚导入的包是TestNG
    
    **@Test**：测试方法前面加入批注@Test，testng就会帮你调用这个方法 不需要main方法中调用。一个Test也就是一个测试用例。
    
    **@BeforeMethod/@AfterMethod**：将在每个@Test之前/后运行，可以做每个方法参数的替换
    
    **@BeforeTest/@AfterTest**：写在哪个test里面，就在哪个test前后执行
    
    **@BeforeClass/@AfterClass** ：写在哪个类里面 就在哪个类的前后执行；或者写在通用类里就在每一个类前后都执行，可以setUp(),clearUp()。
    
    **@BeforeSuite/@AfterSuite**：很多@Test会放到不同的class里，几个class就可以组成一个TestSuite，比如：几个class可以组成一个回归测试的TestSuite，几个class可以组成一个冒烟测试的TestSuite。
    
    beforeSuite可以做 项目配置、驱动预加载，afterSuite可以做资源释放回写。这样的通用的代码可以放在一个单独的包里，创建一个单独的类，其他的类直接继承该类，就不再需要每一个类里面都要写一遍
    
    ```java
    public class **BaseTestSuite** {
        @BeforeSuite
        public void beforeSuite(){
            System.out.println("base-beforeSuite");
        }
        @AfterSuite
        public void afterSuite(){
            System.out.println("base-afterSuite");
        }
    		@BeforeTest
        public void beforeTest(){
            System.out.println("base-beforeTest");
        }
        @AfterTest
        public void afterTest(){
            System.out.println("base-afterTest");
        }
        @BeforeClass
        public void beforeClass(){
            System.out.println("base-beforeClass");
        }
        @AfterClass
        public void afterClass(){
            System.out.println("base-afterClass");
        }
    }
    
    public class TestNGDemo2 **extends BaseTestSuite** {
    	**@Test
    	...
    	@BeforeMethod
    	...
    	@AfterMethod
    	...**
    }
    ```
    
    **@BeforeGroups/@AfterGroups**：在调用属于任何一个组的第一个测试方法之前/之后运行
    
- testng.xml
    
    如果有多个测试类，想要都运行，在项目的根目录下创建一个testng.xml，直接执行这个xml文件，testng**执行顺序**是 按照class的排序从上到下，但class里面的方法是按照英文的自然排序执行：
    
    ```xml
    <!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd">
    <suite name="**项目">		//suite元素 对应一个项目，其中可以有多个测试模块
    	<test name="**接口">    //test元素 对应测试模块或者接口，其中可以有多个测试类
    		<classes>   		//classes元素 测试类的集合
    			<class name="com.wang.TestNGDemo"></class>
    		</classes>
    	</test>
    </suite>
    ```
    
    - 保持xml文件中的顺序来执行
        
        xml文件中的<test>和<class>是按写的先后顺序执行，也就是preserve-order=true，也可以设为false，让他们按照name的排序来执行
        
        ```xml
        <test name="Test 1" **preserve-order="false"**>
        	<classes>
        		<class name="testclasses.TestNG_Preserve2"/>
        		<class name="testclasses.TestNG_Preserve1"/>
        	</classes>
        </test>
        ```
        
- Test属性：**groups**：想要只执行和某个功能相关的一套用例，但他们又和其他的用例在同一个class里面，可以把@test分组 (可以加入多个分组)，并在xml中<classes>同级加入<groups>标签写入想要执行的组：
    
    ```xml
    <suite name="Regression TestSuite">
    	<test name="GroupsDemo">
    			<groups>
    					<define name="all">  //任意定义不同组的组合
    							<include name="suv"/>
    							<include name="bike"/>
    							<include name="sedan"/>
    					</define>
    					<define name="nobike">
    							<include name="suv"/>
    							<include name="sedan"/>
    					</define>
    					<run>
    							<include name="nobike"/> //执行自己定义的组的组合
    					</run>  //也可以给每一个组合创建一个xml，这样想跑哪个组直接去跑对应的xml，便于管理
    			</groups>
    			<classes>
    					<class name="testclasses.TestNG_Grouping"/>
    			</classes>
    	</test>
    </suite>
    ```
    
    ```java
    public class TestNG_Grouping {
    	@BeforeClass(alwaysRun=true)  //没有加入分组的after和before方法，需要加alwaysRun
    	public void beforeClass() {
    		System.out.println("Before Class");
    	}
    	
    	@Test(groups = {"cars","suv"})
    	public void testBMWX6() {
    		System.out.println("Running Test - BMW X6");
    	}
    	
    	@Test(groups = {"cars","sedan"})
    	public void testAudiA6() {
    		System.out.println("Running Test - Audi A6 ");
    	}
    	
    	@Test(groups = {"bike"})
    	public void testNinja() {
    		System.out.println("Running Test - Kawasaki Ninja");
    	}
    	
    	@Test(groups = {"bike"})
    	public void testHondaCBR() {
    		System.out.println("Running Test - Honda CBR");
    	}
    
    	@AfterClass(alwaysRun=true)
    	public void afterClass() {
    		System.out.println("After Class");
    	}
    }
    ```
    
- Test属性：**priority**：让@test按某先后顺序执行，可以把测试方法分优先级。但我们要尽量设计成测试case之间没有依赖关系，可以独立执行。特殊情况才用此方法
    
    ```java
    @test(priority = 0)
    	public void test(){}
    @test(priority = 1)
    	public void testA(){}
    @test(priority = 2)
    	public void testB(){}
    ```
    
- Test属性：**dependsOnMethods：**让有依赖关系的@test 按依赖的顺序来执行，**alwaysRun（**防止testCase被skip掉**）**
    
    没有依赖关系的用例可以在任何时候执行，有依赖的用例在所依赖的方法之后执行。
    
    有依赖关系的测试用例，一旦依赖的测试用例执行失败，之后的case都会skip掉，但是可以通过设置alwaysRun=true，让后面的用例依然执行
    
    ```java
    	ClassToBeTested obj;
    	@BeforeClass
    	public void setUp() {
    		System.out.println("before class");
    		obj = new ClassToBeTested();
    	}
    	
    	@Test(dependsOnMethods = {"testMethod2"},alwaysRun=true) //在testMethod2之后执行
    	public void testMethod1() {        //testMethod2如果执行失败仍然继续执行，不会skip
    		System.out.println("testMethod1");
    	}
    	
    	@Test
    	public void testMethod2() {
    		System.out.println("testMethod2");
    		int result = obj.addNum(1, 2);
    		Assert.assertEquals(result, 2);
    	}
    	
    	@Test(dependsOnMethods = {"testMethod1"}) //在testMethod1之后执行，如果testMethod1失败会跳过执行
    	public void testMethod3() {
    		System.out.println("testMethod3");
    	}
    	
    	@Test
    	public void testMethod4() {    //自由执行
    		System.out.println("testMethod4");
    	}
    ```
    
- **parameter：**从xml文件中读取参数
    
    xml文件添加<parameter>标签，加在哪一级就是哪一级共用，是键值对形式。传的参数值只能是String类型，如果想要其他类型只能用java来转换。且只能用xml来执行（否则会自动生成一个默认的xml文件，找不到参数）
    
    ```xml
    <suite name="**项目Regression TestSuite">
        <test name="测试1"> //参数value只能传基础数据类型，引用类不能传如Student
            **<parameter name="platform" value="windows"></parameter>
            <parameter name="browser" value="chrome"></parameter>
            <parameter name="response" value="201,200"></parameter>**
            <classes>
                <class name="com.wang.TestParameters"></class>
            </classes>
        </test>
    </suite>  **** 
    ```
    
    @Test后加@Parameters({" "," "})，参数名称和<parameter>中name一致，用大括号括起来，与方法的参数按顺序对应（参数个数 类型必须匹配！）
    
    ```java
    public class TestParameters {
        @BeforeTest
        **@Parameters({"browser","platform"})**
        public void setUp**(String browser,String platform)**{
            System.out.println("browser:"+browser+"; platform:"+platform);;
        }
        @Test
        **@Parameters({"response"})**
        public void f1(**String response**){
            String[] responseArray = response.split(",");
            System.out.println("response[0] = " + responseArray[0] + ", response[1] = " + responseArray[1]);
        }
    ```
    
    例如：beforeTest里读取用哪个浏览器，test里面读取期望的结果。
    
- Test属性： **enabled** 当已知用例存在bug或者还没做好之类 需要**忽略**掉某case或者某<test>的方法：
    
    ```java
    @test(enabled = flase)
    public void testMethod(){   }
    ```
    
    ```xml
    <test name="Test 2" enabled="false"> </test>
    ```
    
- Test属性： **timeOut** 希望用例执行时间不超过多少毫秒，一旦超过就算执行失败（对性能有要求）：
    
    ```java
    @test(timeOut=300)
    ```
    
- Test属性： **threadPoolSize**线程数量，**invocationCount**总调用次数，两个一起用可以实现并发
    
    一个类里面的多个方法，是按照方法名字英文顺序执行的
    
    ```java
    @Test(threadPoolSize=50, invocationCount = 200) //50个线程，每个线程调用4次
    ```
    
- 并行执行：对没有依赖关系的测试用例，并行执行可以效率更高：<suite>的parallel、thread-count属性可以选择对class，test，method还是其他做并行，线程数默认是5
    
    并行执行要小心可能会丢失log，或者不好判断因为test有依赖关系而不能并行执行
    
    ```java
    <suite name="Parallel TestSuite" **parallel="methods" thread-count="2"**>
    		<test name="Test 1">
    				<classes>
    						<class name="testclasses.TestNG_Parallel1"/>
    				</classes>
    		</test>
    		<test name="Test 2">
    				<classes>
    						<class name="testclasses.TestNG_Parallel2"/>
    				</classes>
    		</test>
    </suite>
    ```
    
- dataProviders
    
    对同一个参数使用不同的参数值，将参数集存放到二位数组中，参数统一放在一个类，使用在其他类。存放类：返回一个二维数组，每一行是一组参数，会执行一次调用处的代码。
    
    ```java
    public class DataProviders {
        @DataProvider(name = "nameAndPassword")  //这里定义一个name
        public Object[][] getData(){
            return new Object[][]{
                    {"wangyamei","123456"}, //每一行是一组参数，每一行会执行一次
                    {"wang","123456"},
                    {"root","111111"}
            };
        }
    }
    ```
    
    ```java
    
    public class TestDataProvider {
        @Test(dataProvider = "nameAndPassword",  //要使用哪个provider就填写哪个的名字
    					dataProviderClass = dataProviderPackage.DataProviders.class) //因为provider在不同的类，要写清楚provider所在的类.class
        public void test(String name,String password){  //这里的参数和provider的一行对应
            System.out.println(name+" "+password);
        }
    }
    ```
    
- ITestResult 获得测试结果
    
    testNG包中的ITestResult类 就像一个监听器，你能够获得上一个执行过的方法的执行结果，可以根据测试的结果 进行相应的操作，所以适合放在@AfterMethod里面
    
    ```java
    public class TestDataProvider {
        @Test
        public void test(){
            //让断言失败
            Assert.assertTrue(false);
        }
        @Test
        public void test2(){
            //让断言成功
            Assert.assertTrue(true);
        }
        @AfterMethod
        //这里要传一个ITestResult对象作为参数，上一个方法跑完之后的结果会自动传进来
        public void afterTest(**ITestResult testResult**){
            //获取到所有断言的结果，根据执行成功或者失败做相应操作，比如截图，存数据到数据库，输出什么报告
            if ( **testResult.getStatus() == ITestResult.FAILURE**){
                //获取刚跑完的测试方法的名字（方法1）
                System.out.println("Failed:"+testResult.getMethod().getMethodName());
            }
            if (**testResult.getStatus() == ITestResult.SUCCESS**){
                //获取刚跑完的测试方法的名字（方法2）
                System.out.println("Success:"+testResult.getName());
            }
        }
    }
    ```
    
- ITestListener 监听器**：**注册监听器，然后通过实现各个接口写监听类，监听xml或者某个类发生的事件，然后写对应的动作。
    - 代码重构 让一个监听类实现所有监听接口，就不需要注册那么多监听器了，只需要在xml文件中注册监听器**：**
        
        ```java
        public class ListenerAll implements ITestListener,IInvokedMethodListener,ISuiteListener{
        ```
        
        监听器在<suite>标签内，在listener标签中，class-name不需要加.class
        
        ```xml
        <suite name="TestSuiteAAA">
            **<listeners>
                <listener class-name="listenersPackage.Listener2Suite"></listener>
            </listeners>**
            <test name="runWithChrome">
                <classes>
                    <class name="com.wang.Listener1Demo"></class>
                </classes>
            </test>
        </suite>
        ```
        
    - **IInvokedMethodListener接口：监听一个类中的每一个执行的方法**
        
        ```java
        //创建监听器，实现接口 重写接口中的方法
        public class Listener1Invoked implements IInvokedMethodListener {
            @Override
            public void beforeInvocation(**IInvokedMethod iInvokedMethod, ITestResult iTestResult**) {
                //**在测试类里的每一个方法运行之前之后跑**（不只是@test方法 所有方法）
                //参数是刚跑完的测试的结果 和测试方法，可以获取到类名，方法名，参数，时间等信息
                System.out.println("before invocation:"+**iTestResult.getName()**+
                        "-->"+**iInvokedMethod.getTestMethod().getMethodName()**);
            }
            @Override
            public void afterInvocation(IInvokedMethod iInvokedMethod, ITestResult iTestResult) {
                System.out.println("after invocation:"+**iTestResult.getTestClass().getName()**+
                        "-->"+iInvokedMethod.getTestMethod().getMethodName());
            }
        }
        ```
        
        ```java
        //在要监听的类之前，添加@Listener注解，参数填包名.类名 别忘了加**.class**
        **@Listeners(listenersPackage.Listener1Invoked.class)**
        public class Listener1Demo {
            @BeforeClass
            public void setUp() {
                System.out.println("Code in before class");
            }
            @AfterClass
            public void cleanUp() {
                System.out.println("Code in after class");
            }
            @Test
            public void testMethod1() {
                System.out.println("Code in testMethod1");
                Assert.assertTrue(true);
            }
            @Test
            public void testMethod2() {
                System.out.println("Code in testMethod2");
                Assert.assertTrue(false);
            }
        }
        ```
        
    - **ITestListener接口：**监听@Test方法的执行状态，开始、成功、失败、跳过之后做对应操作。
        
         监听器：实现ITestListener接口
        
        ```java
        public class Listener1ITest implements ITestListener {
            @Override
            public void onTestStart(ITestResult iTestResult) {
                //在@Test执行之前执行。可以代替@beforeMethod,并且可以获得更多信息，做更多操作
                System.out.println("On test start:"+iTestResult.getName());
            }
            @Override
            public void onTestSuccess(ITestResult iTestResult) {
                //在@Test执行之后执行
                System.out.println("on test success:"+iTestResult.getName());
            }
            @Override
            public void onTestFailure(ITestResult iTestResult) {
                //当@Test失败之后执行
                System.out.println("on test failure:"+iTestResult.getName());
            }
            @Override
            public void onTestSkipped(ITestResult iTestResult) {
                //当@Test失败之后执行
            }
            @Override
            public void onStart(ITestContext iTestContext) {
                //在xml的<test>之前执行，注意这个参数是ITestContext，获取到的是整个<test>
                System.out.println("on start->test tag name:"+iTestContext.getName());
                //可以获取到<test>标签里的所有测试方法。
                ITestNGMethod methods[] = iTestContext.getAllTestMethods();
                for (ITestNGMethod method : methods) {
                    System.out.println(method.getMethodName());
                }
        
            }
            @Override
            public void onFinish(ITestContext iTestContext) {
                //在xml的<test>之后执行
                System.out.println("on finish->test tag name:"+iTestContext.getName());
            }
            @Override
            public void onTestFailedButWithinSuccessPercentage(ITestResult iTestResult) {
                //忽略
            }
        }
        ```
        
        给要监听的类注册监听器，别忘了.class
        
        ```java
        @Listeners(listenersPackage.Listener1ITest.class)
        public class Listener1Demo {
            @BeforeClass
        		@Test
        		...
        ```
        
    - **ISuiteListener接口：**监听xml中<suite>标签的执行，注册监听器也要注册在<suite>之内
        
        监听器：实现ISuiteListener接口
        
        ```java
        public class Listener2Suite implements ISuiteListener {
            @Override
            public void onStart(ISuite iSuite) {
                //在<suite>标签之前执行
            }
            @Override
            public void onFinish(ISuite iSuite) {
                //在<suite>标签之前执行
            }
        }
        ```