# Excel解析

- **excel读取**
    1. IO流读入Excel文件
    2. WorkbookFactory获取Excel的Workbook（包含所有sheet）
    3. workbook获取指定sheet
    4. sheet获取指定row
    5. row获取指定cell单元格
    6. cell获取到里面的内容String
    
    ```java
    //1.IO流读入Excel文件
    FileInputStream fis = new FileInputStream("src/test/resources/测试资金消耗.xlsx");
    // 2.WorkbookFactory获取Excel的Workbook（包含所有sheet）
    Workbook workbook = WorkbookFactory.create(fis);
    //3.workbook获取指定sheet
    Sheet sheet = workbook.getSheetAt(0);
    // 4.sheet获取指定row
    Row row = sheet.getRow(1);
    //5.row获取指定cell单元格,后面加一个 枚举型参数 用来处理单元格无数据的情况 不会报错
    Cell cell = row.getCell(2, Row.MissingCellPolicy.CREATE_NULL_AS_BLANK);
    //6.cell获取到里面的内容，注意数据格式要对应，小数用double，字用String
    double excelValue = cell.getNumericCellValue();
    System.out.println(excelValue);
    //IO流要在WorkbookFactory.create之后关，否则关闭会报错
    fis.close();
    //4.1 sheet中，使用普通for循环获取所有row
    int lastRowNum= sheet.getLastRowNum();
    //获取row，要获取到最后一行必须多循环一次，判断用<=
    for (int i = 0; i <= lastRowNum; i++) {
         //获取每一行
         Row row= sheet.getRow(i);
         for (int j = 0; j < row.getLastCellNum(); j++) {
              //获取每一个单元格，记得要有为空策略
              Cell cell =  row.getCell(j,Row.MissingCellPolicy.CREATE_NULL_AS_BLANK);
              System.out.print(cell+",");
        }
        System.out.println();
    }
    // 4.2.sheet中 使用增强for循环获取所有row
    for (Row row : sheet) {
       for (Cell cell : row) {
           //可以直接输出cell
           System.out.print(cell+", ");
           //也可以用get获取输出,用get必须用对应的数据类型，如果数据类型不对要强制进行转换????怎么不对
           //System.out.println(new String(String.valueOf(cell.getRichStringCellValue())));
       }
       System.out.println();
    }
    ```
    

**excel写入修改**

前面获取指定单元格和读取的时候一样。写入用cell.setCellValue()方法。 但是 关键是set之后只是改变了JAVA内存中的值，要写出到文件还需要IO流进行一次回写。

```java
//写入
cell.setCellValue(123);
FileOutputStream fos = new FileOutputStream("src/test/resources/测试资金消耗.xlsx");
//回写的话：调用一次workbook的write方法，传入输出流作为参数，就可以了
workbook.write(fos);
```