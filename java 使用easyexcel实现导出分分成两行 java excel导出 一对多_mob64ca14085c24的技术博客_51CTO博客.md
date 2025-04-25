# java 使用easyexcel实现导出分分成两行 java excel导出 一对多_mob64ca14085c24的技术博客_51CTO博客
excel工具类对poi的封装,所以需要导入poi的依赖，我用的是4.1.0版本，如果是4以下，工具里面的poi的相关api需要改变；  
导入/导出支持：一对多合并（不限制层级数，但每个类只能有一个子集）、必填字段检测（读取的时候能用到）、排序（导出能用到）、动态隐藏字段（导入导出会忽略该字段）

hiddenField ：隐藏字段（默认为：false,当为true时，导入导出会忽略该字段，用法: IExcelUtils.hideColumn( clazz,columnName, target),参数依次为：需要修改的class对象、需要修改的字段名、修改的值,也就是true/false），  
注意 ：IExcelUtils.hideColumn()方法需要用在导入导出前才有效

sortNo ： 排序号（默认为0,不进行排序，如果需要排序，在字段上标注@IExcel(sortNo=正整数),从1开始排序）  
注意：如果有子集，子集也是从1开始排序

isNotBlank : 设置字段不为空（默认false;在导入时，如果希望某个字段必填不然该条数据就不要读取,就需要在该字段上标注：@IExcel(isNotBlank=true)；如需要获取没有读取的字段信息，用 IExcelUtils.getErrRowInfo()方法可以获取到）

booleanFormatter ：布尔类型字段转换（处理布尔值的转换，注意：请将表示true的标识写在分割符"|“的左边，表示false的标识写在分割符“|”的右边 ；默认"是|否”）