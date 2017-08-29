---
layout: post
title:  "Spring Boot 配置使用 HTTPS"
date:   2017-08-29 00:00:00
categories: JAVA SpringBoot HTTPS
description: spring boot 使用 https
keywords: https spring-boot, spring boot, spring-boot https, spring-boot-https
author: wxcsdb88
---

`SpringBoot` 项目(2.0.0.M3) 配置 `https` 访问， 支持 `https/http` 或 `https` 的配置说名。

在 `Java` 环境中，常用的证书形式有 `p12`、`jks` 格式等。`HTTPS` 证书我们一般会选择配置在 `nginx` 上。
本文使用编程方式进行 `HTTPS` 配置。

## SpringBoot 版本
`springBootVersion = '2.0.0.M3'`

## keytool 生成证书

```
keytool -genkey -alias tomcat  -storetype PKCS12 -keyalg RSA -keysize 2048 \
-keystore keystore.p12 -validity 3650
```
具体用法可以参考: `keytool -genkey -help`

## 配置 HTTPS
### 仅 HTTPS 生效的配置
`application.yml` 配置修改
```
server:
  port: 8443
  ssl:
    key-store: classpath:keystore/keystore.p12
    key-store-password: yourpassword
    key-store-type: PKCS12
    key-alias: tomcat
```
------
> 下面是两种同时支持 HTTP 和 HTTPS 配置的方法

### 配置 HTTP 转发 到 HTTPS <推荐>
由于不能在配置文件中同时配置两个`connector`, 所以要以编程的方式配置 `HTTP connector`，
然后重定向到 `HTTPS connector`
```
@Bean
public ServletWebServerFactory servletContainer() {
    TomcatServletWebServerFactory tomcat = new TomcatServletWebServerFactory();
    tomcat.addAdditionalTomcatConnectors(createHTTPConnector());
    return tomcat;
}

    private Connector createHTTPConnector() {
    Connector connector = new Connector("org.apache.coyote.http11.Http11NioProtocol");
    connector.setScheme("http");
    connector.setSecure(false);
    connector.setPort(8081);
    connector.setRedirectPort(8443);
    return connector;
}
```
------
### 配置文件配置 HTTP, 编码方式配置 HTTPS

这种方式不能禁止 `HTTP` 访问， 出于安全考虑同时需要支持 `HTTP`， 建议使用编码配置 `HTTP`
转发 `HTTPS` 的方式或者编码配置 `HTTP`。

`application.yml` 配置修改
```
server:
  port: 8081
```

编码方式配置 `HTTPS connector`
```
@Bean
   public ServletWebServerFactory servletContainer() {
       TomcatServletWebServerFactory tomcat = new TomcatServletWebServerFactory();
       tomcat.addAdditionalTomcatConnectors(createSslConnector());
       return tomcat;
   }

   private Connector createSslConnector() {
       Connector connector = new Connector("org.apache.coyote.http11.Http11NioProtocol");
       Http11NioProtocol protocol = (Http11NioProtocol) connector.getProtocolHandler();
       try {
           File keystore = new ClassPathResource("keystore/keystore.p12").getFile();
           connector.setScheme("https");
           connector.setSecure(true);
           connector.setPort(8443);
           protocol.setSSLEnabled(true);
           protocol.setKeystoreFile(keystore.getAbsolutePath());
           protocol.setKeystorePass("uniapp");
           protocol.setKeyAlias("tomcat");
           return connector;
       } catch (IOException ex) {
           throw new IllegalStateException("can't access keystore: [" + "keystore"
                   + "] or truststore: [" + "keystore" + "]", ex);
       }
   }
```
