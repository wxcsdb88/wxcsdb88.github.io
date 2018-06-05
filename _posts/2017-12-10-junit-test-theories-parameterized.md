---
layout: post  
title: "Junit 指定多组测试数据"  
date: 2017-12-10 22:00:00  
categories: JAVA Junit  
description: Junit 多组测试数据测试  
keywords: java, junit
author: wxcsdb88
---

使用 `Junit` 指定多组测试数据进行测试。

测试方法使用的 `SHA3Utils` 代码仓库地址: [java-core](https://github.com/futurever/java-core.git)

---
Parameterized 测试
------------------

> 批量指定多个待测参数, 按数据逐一测试

---

```
import org.junit.Test;
import org.junit.runner.RunWith;
import org.junit.runners.Parameterized;

import java.util.Arrays;
import java.util.List;

/**
 * Description: JunitTest 批量指定多个待测参数, 按数据逐一测试
 * <p>Blog: http://blog.wxcsdb88.com</p>
 *
 * @author wxcsdb88
 * @since 2017-12-10 00:21
 **/
@RunWith(Parameterized.class)
public class JunitTestParameterizeDemo {
    private String input;

    public JunitTestParameterizeDemo(String input) {
        this.input = input;
    }

    @Parameterized.Parameters
    public static List getParams() {
        return Arrays.asList("hello", "hi", "good morning", "how are you");
    }

    @Test
    public void sha224() throws Exception {
        String result = SHA3Utils.sha224(input);
        System.out.println(String.format("input is %s, SHA3-224 output: %s", input, result));
    }

    @Test
    public void sha256() throws Exception {
        String result = SHA3Utils.sha256(input);
        System.out.println(String.format("input is %s, SHA3-256 output: %s", input, result));
    }

    @Test
    public void sha384() throws Exception {
        String result = SHA3Utils.sha384(input);
        System.out.println(String.format("input is %s, SHA3-384 output: %s", input, result));
    }

    @Test
    public void sha512() throws Exception {
        String result = SHA3Utils.sha512(input);
        System.out.println(String.format("input is %s, SHA3-512 output: %s", input, result));
    }
}

```

Theories 测试
-------------

> 提供一组参数的排列组合值作为待测试方法的输入参数, 按照方法逐一测试

---

```
import org.junit.experimental.theories.DataPoints;
import org.junit.experimental.theories.Theories;
import org.junit.experimental.theories.Theory;
import org.junit.runner.RunWith;

/**
 * Description: theories 提供一组参数的排列组合值作为待测试方法的输入参数, 按照方法逐一测试
 * <p>Blog: http://blog.wxcsdb88.com</p>
 *
 * @author wxcsdb88
 * @since 2017-12-10 00:21
 **/
@RunWith(Theories.class)
public class JUnitTestDemoTheories {
    @DataPoints
    public static String[] inputs = {"hello", "hi", "good morning", "how are you"};

    @Theory
    public void sha224Theories(String input) throws Exception {
        String result = SHA3Utils.sha224(input);
        System.out.println(String.format("input is %s, SHA3-224 output: %s", input, result));
    }

    @Theory
    public void sha256(String input) throws Exception {
        String result = SHA3Utils.sha256(input);
        System.out.println(String.format("input is %s, SHA3-256 output: %s", input, result));
    }

    @Theory
    public void sha384(String input) throws Exception {
        String result = SHA3Utils.sha384(input);
        System.out.println(String.format("input is %s, SHA3-384 output: %s", input, result));
    }

    @Theory
    public void sha512(String input) throws Exception {
        String result = SHA3Utils.sha512(input);
        System.out.println(String.format("input is %s, SHA3-512 output: %s", input, result));
    }
}
```
