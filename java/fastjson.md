# FastJson

> springboot中配置[请查看](../springboot/fastjson-config.md)

> maven依赖

```xml
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>1.2.51</version>
</dependency>
```

#### SerializerFeature 含义

|SerializerFeature             |        含义       |     备注     |
|------------------------------|------------------|--------------|
|QuoteFieldNames               | 输出key时是否使用双引号，默认为true | |
|UseSingleQuotes               | 使用单引号而不是双引号，默认为false | |
|WriteMapNullValue             | 是否输出值为null的字段，默认为false | 常用 |
|WriteEnumUsingToString        | Enum输出toString()，默认为false | |
|WriteEnumUsingName            | Enum输出name()，默认为false | |
|UseISO8601DateFormat          | Date使用ISO8601格式输出，默认为false | |
|WriteNullListAsEmpty          | 将Collection类型字段的字段空值输出为[] | 常用 |
|WriteNullStringAsEmpty        | 将字符串类型字段的空值输出为空字符串 "" | 常用 |
|WriteNullNumberAsZero         | 将数值类型字段的空值输出为0 | |
|WriteNullBooleanAsFalse       | 将Boolean类型字段的空值输出为false | |
|SkipTransientField            | 如果是true，类中的Get方法对应的Field是transient，序列化时将会被忽略。默认为true | |
|SortField                     | 按字段名称排序后输出。默认为false | |
|WriteTabAsSpecial             | 把\t做转义输出，默认为false | |
|PrettyFormat                  | 结果是否格式化，默认为false | |
|WriteClassName                | 序列化时写入类型信息，默认为false。反序列化是需用到 | |
|DisableCircularReferenceDetect| 消除对同一对象循环引用的问题，默认为false | |
|WriteSlashAsSpecial           | 对斜杠 "/" 进行转义 | |
|BrowserCompatible             | 将中文都会序列化为\uXXXX格式，字节数会多一些，但是能兼容IE 6，默认为false | |
|WriteDateUseDateFormat        | 全局修改日期格式，默认为false。JSON.DEFFAULT_DATE_FORMAT = "yyyy-MM-dd";JSON.toJSONString(obj, SerializerFeature.WriteDateUseDateFormat); | |
|NotWriteRootClassName         |  | |
|DisableCheckSpecialChar       | 一个对象的字符串属性中如果有特殊字符如双引号，将会在转成json时带有反斜杠转移符。如果不需要转义，可以使用这个属性。默认为false | |
|BeanToArray                   | 将对象转为array输出 | |
|WriteNonStringKeyAsString     | | |
|NotWriteDefaultValue          | | |
|BrowserSecure                 | | |
|IgnoreNonFieldGetter          | | |
|WriteNonStringValueAsString   | | |
|IgnoreErrorGetter             | | |
|WriteBigDecimalAsPlain        | | |
|MapSortField                  | | |


#### json -> 指定泛型类型 反序列化

```java
// new TypeReference<此处为指定的泛型类型>() { }
HashMap<String, List<ObjectBean>> map = JSON.parseObject(json, new TypeReference<HashMap<String, List<ObjectBean>>>() { });
```