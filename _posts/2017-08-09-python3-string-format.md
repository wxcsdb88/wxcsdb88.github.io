---
layout: post
title:  "python3 字符串格式化用法"
date:   2017-08-09 00:00:00
categories: Python3
description: python3 格式话字符串用法
keywords: python,format,string
author: wxcsdb88
---

python3 使用 format 对字符串进行格式化

# 数字格式化

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;border-color:#bbb;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:#bbb;color:#594F4F;background-color:#E0FFEB;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:#bbb;color:#493F3F;background-color:#9DE0AD;}
.tg .tg-yw4l{vertical-align:top}
</style>
<table class="tg">
  <tr>
    <th class="tg-yw4l">数字</th>
    <th class="tg-yw4l">格式</th>
    <th class="tg-yw4l">输出</th>
    <th class="tg-yw4l">描述</th>
  </tr>
  <tr>
    <td class="tg-yw4l">3.1415926</td>
    <td class="tg-yw4l">{:.2f}</td>
    <td class="tg-yw4l">3.14</td>
    <td class="tg-yw4l">保留小数点后两位</td>
  </tr>
  <tr>
    <td class="tg-yw4l">3.1415926</td>
    <td class="tg-yw4l">{:+.2f}</td>
    <td class="tg-yw4l">+3.14</td>
    <td class="tg-yw4l">带符号保留小数点后两位</td>
  </tr>
  <tr>
    <td class="tg-yw4l">-1</td>
    <td class="tg-yw4l">{:+.2f}</td>
    <td class="tg-yw4l">-1.00</td>
    <td class="tg-yw4l">带符号保留小数点后两位</td>
  </tr>
  <tr>
    <td class="tg-yw4l">2.71828</td>
    <td class="tg-yw4l">{:.0f}</td>
    <td class="tg-yw4l">3</td>
    <td class="tg-yw4l">不带小数</td>
  </tr>
  <tr>
    <td class="tg-yw4l">5</td>
    <td class="tg-yw4l">{:0&gt;2d}</td>
    <td class="tg-yw4l">05</td>
    <td class="tg-yw4l">数字补零 (填充左边, 宽度为2)</td>
  </tr>
  <tr>
    <td class="tg-yw4l">5</td>
    <td class="tg-yw4l">{:x&lt;4d}</td>
    <td class="tg-yw4l">5xxx</td>
    <td class="tg-yw4l">数字补x (填充右边, 宽度为4)</td>
  </tr>
  <tr>
    <td class="tg-yw4l">10</td>
    <td class="tg-yw4l">{:x&lt;4d}</td>
    <td class="tg-yw4l">10xx</td>
    <td class="tg-yw4l">数字补x (填充右边, 宽度为4)</td>
  </tr>
  <tr>
    <td class="tg-yw4l">1000000</td>
    <td class="tg-yw4l">{:,}</td>
    <td class="tg-yw4l">1,000,000</td>
    <td class="tg-yw4l">以逗号分隔的数字格式</td>
  </tr>
  <tr>
    <td class="tg-yw4l">0.25</td>
    <td class="tg-yw4l">{:.2%}</td>
    <td class="tg-yw4l">25.00%</td>
    <td class="tg-yw4l">百分比格式</td>
  </tr>
  <tr>
    <td class="tg-yw4l">1000000000</td>
    <td class="tg-yw4l">{:.2e}</td>
    <td class="tg-yw4l">1.00e+09</td>
    <td class="tg-yw4l">指数记法</td>
  </tr>
  <tr>
    <td class="tg-yw4l">13</td>
    <td class="tg-yw4l">{:10d}</td>
    <td class="tg-yw4l">        13</td>
    <td class="tg-yw4l">右对齐 (默认, 宽度为10)</td>
  </tr>
  <tr>
    <td class="tg-yw4l">13</td>
    <td class="tg-yw4l">{:&lt;10d}</td>
    <td class="tg-yw4l">13</td>
    <td class="tg-yw4l">左对齐 (宽度为10)</td>
  </tr>
  <tr>
    <td class="tg-yw4l">13</td>
    <td class="tg-yw4l">{:^10d}</td>
    <td class="tg-yw4l">    13</td>
    <td class="tg-yw4l">中间对齐 (宽度为10)</td>
  </tr>
</table>

## 基本字符串替换

若没有指定格式，则直接将变量值作为字符串插入。

```python
s1 = "so much depends upon {}".format("a red wheel barrow")
s2 = "glazed with {} water beside the {} chickens".format("rain", "white")
```

也可以使用变量的位置数值，在字符串中改变它们，进行格式化时，会更加灵活。如果搞错了顺序，你可以轻易地修正而不需要打乱所有的变量。

```python
s1 = " {0} is better than {1} ".format("emacs", "vim")
s2 = " {1} is better than {0} ".format("emacs", "vim")
```

## 命名参

```python
madlib = " I {verb} the {object} off the {place} ".format(verb="took", object="cheese", place="table")
```

## 多次复用同一个变量

```python
str = "Oh {0}, {0}! wherefore art thou {0}?".format("Romeo")
```

## 将数值转换为不同的进制

```python
print("{0:d} - {0:x} - {0:o} - {0:b} ".format(21))
```

## 将格式作为函数来使用

可以将.format()用作函数，这就允许在代码中将普通文本和格式区分开来。例如，你可以在程序的开头包含所有需要使用的格式，然后在后面使用。这也是一种处理国际化的好方法，国际化不仅要求不同的文本，且常常要求不同的数字格式。

```python
## 定义格式
email_f = "Your email address was {email}".format

### 在另一个地方使用
print(email_f(email="bob@example.com"))
```

## 转义大括号

使用str.format()时，若你需要使用大括号，只要写两次就可以了：

```python
print(" The {} set is often represented as { {0} } ".format("empty"))
```
