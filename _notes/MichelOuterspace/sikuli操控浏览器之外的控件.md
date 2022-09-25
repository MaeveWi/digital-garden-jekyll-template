# sikuli操控浏览器之外的控件

selenium不能操控基于浏览器之外的控件，可以用sikuli实现，它是一种图形脚本语言

```java
import java.awt.AWTException;
import java.awt.Robot;
import java.awt.event.KeyEvent;
import java.io.IOException;
import org.sikuli.script.FindFailed;
import org.sikuli.script.Key;
import org.sikuli.script.Screen;

public class SikuliDemo {
	public static void main(String[] args) throws AWTException, FindFailed {
		Screen s = new Screen();
		// 定义图片存放路径
		String imgpath = "/Users/gaoyan/Desktop/";
	
		Robot robot = new Robot();
	
		// Cmd+Space
		robot.keyPress(KeyEvent.VK_META);
		robot.keyPress(KeyEvent.VK_SPACE);
		robot.keyRelease(KeyEvent.VK_META);
		robot.keyRelease(KeyEvent.VK_SPACE);
		robot.delay(2000);
	
		// Hit Delete and type text
		s.type(Key.DELETE);
		s.type(imgpath + "searchbox","text");
	
		robot.delay(2000);
		// Hit enter key
		s.type(Key.ENTER);
		// Paste & double click & delete
		s.paste(imgpath + "editor","testing");
		s.doubleClick(imgpath + "testing");
	
		robot.delay(2000);
		s.type(Key.DELETE);
	
		// close &delete
		s.click(imgpath + "close");
		robot.delay(2000);
		s.click(imgpath + "delete");
	
		System.out.println("end");
	}
}
```