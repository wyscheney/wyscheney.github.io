---
layout: wiki
title: XML Schema 简单编写及应用
categories: Schema
description: 最近在看webservice的部分,正好顺便看了一下关于XML Schema的部分,做了一个小的总结,详细的标签属性建议参考官方文档
keywords: Schema,Schema约束,XML
---

## 什么是XML Schema
菜鸟教程上这样描述:
>XML Schema 是基于 XML 的 DTD 替代者。
>XML Schema 可描述 XML 文档的结构。
>XML Schema 语言也可作为 XSD（XML Schema Definition）来引用。

其实简单的来说，XML Schema 就是XML的一中构造，用来约束XML文档中可以有哪些元素，元素应该具有哪些属性。所以XML Schem也常常被叫着*<font color="red">Schema约束</font>*。

## 简单的Schema 实例
下面这是一段Schema文件的代码,后缀名为<code>.xsd</code>
@代码段一(xsd)
```XML
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"  
targetNamespace="http://www.cheneyc.cn" 
xmlns="http://www.cheneyc.cn"
elementFormDefault="qualified">

<xs:element name="cc" >
	<xs:complexType>
		<xs:sequence maxOccurs="unbounded">
			<xs:element name="name" type="xs:string"/>
			<xs:element name="age" type="xs:integer"/>
			<xs:element name="sex" type="xs:byte"/>
		</xs:sequence>
	</xs:complexType>	
</xs:element>  
```
@代码段二(xml引用)
```XML
<?xml version="1.0" encoding="UTF-8"?>
<cc xmlns="http://www.cheneyc.cn" 
	xmlns:xsi="http://www.http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.cheneyc.cn cc.xsd"
	>
	<name>陈晨</name>
	<age>123</age>
	<sex>m</sex>
</cc>
```

## 关于上面代码的说明
#### 代码段1.1
```<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"  ```
这段也是XML 引用Schema约束的写法,因为Schema约束本质上也是XML,由w3c组织定义了他的约束写法,所以在自定义Schema约束时,也必须引用相关约束。
文字段分为三个部分：
1. <xs:schema></xs:schema>w3c中定义的根标签.
1. xmlns:xs :xmlns 是XML NamespacesXML Namespaces的缩写,命名空间. xs 代码此命名空间的标签使用的前缀.
1. http://www.w3.org/2001/XMLSchema 引用的命名空间.(xsd 固定)

#### 代码段1.2
```targetNamespace="http://www.cheneyc.cn" ```
声明这个文件的唯一的namespace ,在XML文件中，通过namespac，来引入Schema约束。

#### 代码段1.3
```xmlns="http://www.cheneyc.cn" ```
指出默认的命名空间是 "http://www.w3school.com.cn"。
作用是,当使用默认命名空间的标签时,可以省略代码的前缀.例如:若果xmlns="http://www.w3.org/2001/XMLSchema",那么在代码块一时,标签可以省略XS


#### 代码段1.4
```elementFormDefault="qualified" ```
有效值是 qualified 和unqualified，如果该值是 qualified，实例xml根元素及其下所有子元素都必须通过命名空间前缀限定目标命名空间。这个命名空间必须是schema中定义的targetNameSpace。

#### 代码段 1.5
```<element> ```标签:表示定义元素.
```<complexType> ```复杂元素,可以包括序列,多个属性.
```<sequence> ``` 序列,其中maxOccurs代表可以子元素最大出现的次数

element 包含2个关键属性,name 和type,name 表示xml文件可以使用的标签.,type表示类型限定.


#### 代码段2.1
```cc xmlns="http://www.cheneyc.cn```
同代码块1,引用自定Schema约束.

#### 代码段2.2
```XML
xmlns:xsi="http://www.http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="{namespace} {location}
```
这两个放在一起来说,对于自定义的Schema引用,我们必须声明自定义应用的位置，语法如上。
如果引用多个文件，可以用空格隔开,参考Spring配置文件的标签引用。
