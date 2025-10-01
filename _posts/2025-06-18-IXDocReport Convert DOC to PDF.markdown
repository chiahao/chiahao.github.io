---
layout: post
title: "IXDocReport Convert DOC to PDF"
date: 2025-06-18 11:47:00
category: program
tags: [java,]
---

### Option 1. More appropriate when not using `TemplateEngine`:  

```java
IConverter converter = ConverterRegistry.getRegistry().getConverter(options);
converter.convert(getDocStream(), result, options);
```

### Option 2.

```xml
fr.opensagres.xdocreport.core.registry.AbstractRegistry.initializeIfNeeded Error while registration of Discovery instance  fr.opensagres.xdocreport.converter.odt.odfdom.itext.discovery.ODF2PDFViaITextConverterDiscovery@31d421fd
	java.lang.NoClassDefFoundError: org/odftoolkit/odfdom/doc/OdfDocument
```


```java
import fr.opensagres.xdocreport.document.IXDocReport;
import fr.opensagres.xdocreport.document.docx.DocxReport;
import fr.opensagres.xdocreport.document.registry.XDocReportRegistry;
import fr.opensagres.xdocreport.template.IContext;
import fr.opensagres.xdocreport.template.ITemplateEngine;
import fr.opensagres.xdocreport.template.TemplateEngineKind;

IXDocReport report = XDocReportRegistry.getRegistry().loadReport(
	getDocStream(), TemplateEngineKind.Velocity  
);

// 2) Prepare PDF options
PdfOptions pdfOptions = PdfOptions.create().fontProvider((String familyName, String encoding, float size, int style, Color color) -> {
  Font result1 = null;
  try {
    BaseFont bfChinese = BaseFont.createFont(chnFontPath, BaseFont.IDENTITY_H, BaseFont.EMBEDDED);
    Font fontChinese = new Font(bfChinese, size, style, color);
    if (familyName != null) {
      fontChinese.setFamily(familyName);
    }
    result1 = fontChinese;
  } catch (DocumentException | IOException ex) {
    System.out.println("轉 pdf 失敗: " + ex.getMessage());
  }
  return result1;
});

Options options = Options.getFrom(DocumentKind.DOCX).to(ConverterTypeTo.PDF);
options.subOptions(pdfOptions);

// 3) Convert to Pdf
IContext context = report.createContext();
context.put("name", "prevent empty");
report.convert(context, options, result);
```  

Both would occured a lot of errors when not include `odfdom-java`:  

```java
fr.opensagres.xdocreport.core.registry.AbstractRegistry.initializeIfNeeded Error while registration of Discovery instance  fr.opensagres.xdocreport.converter.odt.odfdom.itext.discovery.ODF2PDFViaITextConverterDiscovery@31d421fd
	java.lang.NoClassDefFoundError: org/odftoolkit/odfdom/doc/OdfDocument
```  

Dependency:  

1. Silent the error  

```xml
<dependency>
  <groupId>org.odftoolkit</groupId>
  <artifactId>odfdom-java</artifactId>
  <version>0.12.0</version>
</dependency>
```

2. Still needs old `itext` for multibyte characters:  

```xml
<dependency>
  <groupId>com.lowagie</groupId>
  <artifactId>itext</artifactId>
  <version>2.1.7</version>
</dependency>
```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

