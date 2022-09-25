# json和JAVA对象转换

- **J**son（JavaScript Object Notation,JS对象简谱）：
    - 一种轻量级数据交换格式
    - 键值对形式，逗号分隔
    - 一个大括号{}表示一个对象
    - 一个中括号[]表示一个数组，里面可以有多个对象

**JSON解析（**通过maven，pom中导入**fastJson**包，可以实现**json字符串和JAVA对象转换**，FastJson工具类都是静态方法，直接用类名.调用**）**

**要求：**json中的每一个字段，在对象中必须要有对应的属性 且格式一致，对应的属性必须都是私有属性，必须有空参构造和getter setter

```java
//json字符串 ==> java对象,   Student.class是 反射 后面学
        Student ss = JSONObject.parseObject(jsonString,Student.class);
//json字符串 ==> JAVA对象map
        Map<String,Object> map = JSONObject.parseObject(jsonString,Map.class);
//json数组字符串 ==> java对象list
        String json4 = "[{\"name\":\"张三\",\"age\":17,\"score\":77},{\"name\":\"李四\",\"age\":17,\"score\":77}]";
        List<Student> list = JSONObject.parseArray(json4, Student.class);
 //studentList.for输出studentList
        for (Student student : studentList) {
            System.out.println(student);
        }
//对象 ==> Json字符串
        Student s2 = new Student("李四",20,98);
        String json2 = JSONObject.toJSONString(s2);
//map ==> Json字符串
        String json3 = JSONObject.toJSONString(map);
```