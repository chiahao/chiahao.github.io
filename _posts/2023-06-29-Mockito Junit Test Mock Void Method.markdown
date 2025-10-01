---
layout: post
title: "Mockito Junit Test Mock Void Method"
date: 2023-06-29 14:09:00
category: mockito
tags: [unit test, mockito]
---

#### mockito mock void method

mockito mock member setter
```java
java.lang.IllegalStateException: This was not supposed to happend
	at org.mockito.internal.util.reflection.GenericMetadataSupport$GenericArrayReturnType.rawType(GenericMetadataSupport.java:527)
	at org.mockito.internal.stubbing.answers.InvocationInfo.isVoid(InvocationInfo.java:55)
	at org.mockito.internal.stubbing.answers.Returns.validateFor(Returns.java:32)
	at org.mockito.internal.stubbing.InvocationContainerImpl.addAnswer(InvocationContainerImpl.java:70)
	at org.mockito.internal.stubbing.InvocationContainerImpl.addAnswer(InvocationContainerImpl.java:56)
	at org.mockito.internal.stubbing.OngoingStubbingImpl.thenAnswer(OngoingStubbingImpl.java:32)
	at org.mockito.internal.stubbing.BaseStubbing.thenReturn(BaseStubbing.java:35)
	at PtTchMgr.report.ReportServiceTest.testCreateReport07010_1_check_logging(ReportServiceTest.java:350)
```
結果居然是 constructor
結果是因為雖然有 mock class instance variable, 但是最後呼叫 instance.create() 時, 都有再重新建立 instance variable, 所以根本不對!!

Still not work:  
```java
FreemarkerUtil mock = mock(FreemarkerUtil.class, Mockito.RETURNS_MOCKS);
when(mock.genQueriesDocx(any(InputStream.class), any(ByteArrayOutputStream.class), any(List.class)))
		.thenReturn(new byte[]{});
super.setFreemarkerUtil(mock);
```

Try following search:  
mockito "thenreturn" primitive type  
mockito why donothing wtill execute ?  
"mockito" "request.getSession().getAttribute"

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


