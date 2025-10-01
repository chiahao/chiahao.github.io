---
layout: post
title: "Jdk6 Mail With Attachment"
date: 2023-07-10 09:20:00
category: mail
tags: [mail]
---

Add following parameter to enable mail debug.  
```java
java -Dmail.debug=true
```

compile result:  
not found com.sun.xml.internal.ws.util.ByteArrayDataSource;  
```java
mimeBodyPart = new MimeBodyPart();
DataSource fileDataSource = new ByteArrayDataSource(attachment, "8bit");
mimeBodyPart.setDataHandler(new DataHandler(fileDataSource));
mimeBodyPart.setFileName(fileName);
multipart.addBodyPart(mimeBodyPart);
```



```java
InputStream is = new ByteArrayInputStream(attachment.toByteArray());
mimeBodyPart = new MimeBodyPart(is);
```

會出現  
```java
nested exception is:
		java.io.IOException: Error in encoded stream: needed at least 2 valid base64 characters, but only got 1 before padding character (=), the 10 most recent characters were: "\155)P\30\0y\171\174\242="
```

所以猜測可能是沒有 header 的問題


##### 結果信件的附件檔案破損
在猜會不會是需要指定大小？

```java
InternetHeaders headers = new InternetHeaders();
headers.setHeader("Content-Type", "application/vnd.ms-excel" + "; charset=UTF-8");
headers.setHeader("Content-Transfer-Encoding", "quoted-printable");
mimeBodyPart = new MimeBodyPart(headers, attachment.toByteArray());
```



```java
// for HTML Content
MimeBodyPart mimeBodyPart = new MimeBodyPart();
message.setFrom(new InternetAddress(mailFrom, mailName, "utf-8"));
for(String address: addressList) {
	message.addRecipients(Message.RecipientType.TO, address);
}
message.setSentDate(new Date());
message.setSubject(mailSubject, "utf-8");

// for HTML Content
mimeBodyPart.setContent(mailContent, "text/html;charset=utf-8");
Multipart multipart = new MimeMultipart();
multipart.addBodyPart(mimeBodyPart);

// for HTML Content
MimeBodyPart mimeBodyPart = new MimeBodyPart();

mimeBodyPart = new MimeBodyPart();
File file = null;
try {
	file = new File("tempFile");
	file.createNewFile();
	FileOutputStream fos = new FileOutputStream(file);
	attachment.writeTo(fos);
	fos.close();
} catch (IOException ex) {
}

DataSource fileDataSource = new FileDataSource(file);
mimeBodyPart.setDataHandler(new DataHandler(fileDataSource));
// webmail filename would be garbled, and the downloaded one still be garbled.  
// mimeBodyPart.setFileName(fileName);
// webmail filename would be garbled, but the downloaded one would be correct.  
mimeBodyPart.setFileName(URLEncoder.encode(fileName, "UTF-8"));
multipart.addBodyPart(mimeBodyPart);

message.setContent(multipart);

Transport.send(message);

```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


