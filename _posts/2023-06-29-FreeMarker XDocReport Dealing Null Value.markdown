---
layout: post
title: "XDocReport Dealing Null Value"
date: 2023-06-29 11:51:00
category: java
tags: [xdocreport]
---

> e = (fr.opensagres.xdocreport.core.XDocReportException) fr.opensagres.xdocreport.core.XDocReportException: freemarker.core.InvalidReferenceException: The following has evaluated to null or missing:
> ==> bean.name  [in template "fr.opensagres.xdocreport.document.docx.DocxReport@71811419!word/document.xml" at line 4, column 3960]
> 
> Tip: If the failing expression is known to be legally null/missing, either specify a default value with myOptionalVar!myDefault, or use [#if myOptionalVar??]when-present[#else]when-missing[/#if]. (These only cover the last step of the expression; to cover the whole expression, use parenthessis: (myOptionVar.foo)!myDefault, (myOptionVar.foo)??
> 
> The failing instruction:
> ==> ${bean.name} auto-escaped  [in template "fr.opensagres.xdocreport.document.docx.DocxReport@71811419!word/document.xml" at line 4, column 3958]

According to [How to check if a variable exists in a FreeMarker template?](https://stackoverflow.com/questions/306732/how-to-check-if-a-variable-exists-in-a-freemarker-template):  

> For versions previous to FreeMarker 2.3.7
> You can not use ?? to handle missing values, the old syntax is:

> <#if userName?exists>
>    Hi ${userName}, How are you?
> </#if>
> 	https://stackoverflow.com/questions/306732/how-to-check-if-a-variable-exists-in-a-freemarker-template
> 	freemarker.core.ParseException: Parsing error in template "fr.opensagres.xdocreport.document.docx.DocxReport@333903d0!word/document.xml" in line 4, column 4975:
> 	Encountered "<", but was expecting one of:
> 	    <STRING_LITERAL>
> 	    <RAW_STRING>
> 	    "false"
> 	    "true"
> 	    <INTEGER>
> 	    <DECIMAL>
> 	    "."
> 	    "+"
> 	    "-"
> 	    "!"
> 	    "["
> 	    "("
> 	    "{"
> 	    <ID>
> 	freemarker.core.ParseException: Parsing error in template "fr.opensagres.xdocreport.document.docx.DocxReport@333903d0!word/document.xml" in line 4, column 4975:
> 	Encountered "<", but was expecting one of:
> 	    <STRING_LITERAL>
> 	    <RAW_STRING>
> 	    "false"
> 	    "true"
> 	    <INTEGER>
> 	    <DECIMAL>
> 	    "."
> 	    "+"
> 	    "-"
> 	    "!"
> 	    "["
> 	    "("
> 	    "{"
> 	    <ID>

##### Not work:
```java
?if_exists
```

```java
{ MERGEFIELD  ${bean.name ?if_exists}  \* MERGEFORMAT }
```
or remove the space between bean.name ?

##### Finally this works!

Give default value:  
```java
!""
```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


