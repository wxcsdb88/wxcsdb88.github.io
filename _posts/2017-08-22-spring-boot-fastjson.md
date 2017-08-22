---
layout: post
title:  "Spring Boot 配置使用 fastjson"
date:   2017-08-23 00:00:00
categories: JAVA Spring SpringBoot
description: spring boot 使用 fastjson
keywords: spring， spring-boot, spring boot
author: wxcsdb88
---

SpringBoot 项目(2.0.0.M3) 使用 fastjson 替换默认的jackson序列化的配置说明。

## SpringBoot 及 fastjson 版本
`springBootVersion = '2.0.0.M3'`

```
org.springframework.boot:spring-boot-starter-web
com.alibaba:fastjson:1.2.37
```

## 配置
有两种实现方式，一是注解 `Bean`，如下所示:
```
// SpringBootApplication
@Bean
 public HttpMessageConverters fastJsonHttpMessageConverters() {
     FastJsonHttpMessageConverter fastConverter = new FastJsonHttpMessageConverter();
     FastJsonConfig fastJsonConfig = new FastJsonConfig();
     fastJsonConfig.setFeatures(Feature.AllowArbitraryCommas, Feature.AllowUnQuotedFieldNames, Feature.DisableCircularReferenceDetect);
     fastJsonConfig.setSerializerFeatures(SerializerFeature.PrettyFormat);
     fastJsonConfig.setSerializerFeatures(SerializerFeature.WriteNullStringAsEmpty);
     fastJsonConfig.setDateFormat("yyyy-MM-dd HH:mm:ss");
     fastConverter.setFastJsonConfig(fastJsonConfig);
     HttpMessageConverter<?> converter = fastConverter;
     System.out.println(fastJsonConfig.getParserConfig().toString());
     return new HttpMessageConverters(converter);
 }
```
另一种是重写 `configureMessageConverters` (本人采用这种实现，减少 `Main` 函数文件中配置项)
```
@Configuration
@ComponentScan(basePackageClasses = AppApplication.class, useDefaultFilters = true)
public class MvcConfiguration extends WebMvcConfigurationSupport {

----------------------

@Override
    public void configureMessageConverters(
            List<HttpMessageConverter<?>> converters) {
        super.configureMessageConverters(converters);
        FastJsonHttpMessageConverter fastConverter = new FastJsonHttpMessageConverter();
        List<MediaType> mediaTypeList = new ArrayList<MediaType>();
        mediaTypeList.add(new MediaType("application", "json", Charset.forName("UTF-8")));
        mediaTypeList.add(new MediaType("application", "json", Charset.forName("UTF-8")));
        mediaTypeList.add(new MediaType("text", "html", Charset.forName("UTF-8")));
        fastConverter.setSupportedMediaTypes(mediaTypeList);

        FastJsonConfig fastJsonConfig = new FastJsonConfig();
        fastJsonConfig.setFeatures(Feature.AllowArbitraryCommas, Feature.AllowUnQuotedFieldNames, Feature.DisableCircularReferenceDetect);
        fastJsonConfig.setSerializerFeatures(SerializerFeature.PrettyFormat);
        fastJsonConfig.setSerializerFeatures(SerializerFeature.WriteNullStringAsEmpty);
        fastJsonConfig.setSerializerFeatures(SerializerFeature.WriteDateUseDateFormat);
        fastJsonConfig.setDateFormat("yyyy-MM-dd HH:mm:ss");
        fastConverter.setFastJsonConfig(fastJsonConfig);
        converters.add(fastConverter);
    }
```
