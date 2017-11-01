---
layout: post
title: "Fastjson 自定义 json 的 值输出格式"
date: 2017-11-01 22:00:00
categories: JAVA Fastjson
description: fastjson 序列化数值格式问题
keywords: java, fastjson
author: wxcsdb88
---

使用 fastjson 自定义数值类型（也可以进行其他类型的处理）格式的配置说明。

fastjson 版本
-------------

```
com.alibaba:fastjson:1.2.37
```

`json` 对象中数值的序列化处理在 `js` 与 `golang` 中结果是一致的， `java` 使用 `fastjson` 默认情况 下与前两种是有区别的。 针对 `json` 对象进行序列化 `{"name":"wxcsdb88","age":23.0, "salary": 15.00, "leftTime":0.00, "cost":99.0200}`,

js 处理:
--------

```
 JSON.stringify({"name":"wxcsdb88","age":23.0, "salary": 15.00, "leftTime":0.00, "cost":99.0200})

 output:
 "{"name":"wxcsdb88","age":23,"salary":15,"leftTime":0,"cost":99.02}"
```

## golang 处理
```
为了保持json序列化过程中的顺序我们需要先将其转换成 map(golang中有序), 再转换成 json， 最后转成 json 字符串, 即 struct->map->json->jsonString

output: "{"age":23,"cost":99.02,"leftTime":0,"name":"wxcsdb88","salary":15}"
```

java 处理
---------

为了使 `json` 对象中的 `value` 保持与 `js` 的 `JSON.stringify()` 及 `golang` 的`json` 序列化保持一致结果，我们需要添加一个值过滤器，对特定类型值进行类型转换。

### 配置

自定义 json 对象中 value 的值过滤器 `FastJsonValueFilter`
```
public class FastJsonValueFilter implements ValueFilter {

    public static String getPrettyNumberString(String number) {
        return BigDecimal.valueOf(Double.parseDouble(number))
                .stripTrailingZeros().toPlainString();
    }

    public static BigDecimal getPrettyNumber(String number) {
        return BigDecimal.valueOf(Double.parseDouble(number))
                .stripTrailingZeros();
    }

    @Override
    public Object process(Object object, String name, Object value) {
//        System.out.println(String.format("name: %s, value: %s, type is: %s", name, value, value.getClass().getSimpleName()));
        if (value != null && value instanceof BigDecimal) {
            return getPrettyNumber(value.toString());
        }
        return value;
    }
}
```

### 使用

```
FastJsonValueFilter fastJsonValueFilter = new FastJsonValueFilter();

public static String formatJsonContract(JSONObject jsonObject) {
     return JSONObject.toJSONString(jsonObject, fastJsonValueFilter, SerializerFeature.MapSortField,
             SerializerFeature.WriteNullStringAsEmpty, SerializerFeature.WriteMapNullValue,
             SerializerFeature.WriteNonStringKeyAsString,
             SerializerFeature.WriteNullNumberAsZero);
 }

```
