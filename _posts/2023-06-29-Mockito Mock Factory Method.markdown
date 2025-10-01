---
layout: post
title: "Mockito Mock Factory Method"
date: 2023-06-29 11:44:00
category: mockito
tags: [unit test, mockito]
---

#### junit test mock variable inside method
	https://stackoverflow.com/questions/23236338/using-mockito-to-mock-a-local-variable-of-a-method
	雖然最底下的回答沒有被接受, 但是他不是把 local variable 變成 instance variable, 而是把 factory 變成 instance variable
	才想到可能可以把 builder 也變成 instance variable!
	所以 https://www.baeldung.com/mockito-fluent-apis 去模擬 Builder 是對的!
www.baeldung.com Mockito "anyString"
找到 Mockito 應該還能用 2 的版本
mockito any(HttpServletRequest.class) not work
	unreported exception NoPrivilegeException; must be caught or declared to be thrown
mockito anyHttpServletRequest
mockito mock custom method

突然覺得這個 service 層很沒有測試的意義...
	還覺得真的把查詢全部放 service 層是對的嗎?
java which to unit test

```java
incompatible types: List<CAP#1> cannot be converted to List<NpPtt07010R612Bean>
  where CAP#1 is a fresh type-variable:
    CAP#1 extends Object from capture of ?
```

mockito mock constructor

```java
PtTch07010R63_66Rpt ptTch07010R63_66Rpt = mock(PtTch07010R63_66Rpt.class,
			withSettings()
				.useConstructor(anyString(), anyInt())
				.defaultAnswer(CALLS_REAL_METHODS)
		);
	You cannot use argument matchers outside of verification or stubbing.
	Examples of correct usage of argument matchers:
	    when(mock.get(anyInt())).thenReturn(null);
	    doThrow(new RuntimeException()).when(mock).someVoidMethod(anyObject());
	    verify(mock).someMethod(contains("foo"))
```

Still not work:  
```java
PtTch07010R63_66Rpt ptTch07010R63_66Rpt = mock(PtTch07010R63_66Rpt.class,
			withSettings()
				.useConstructor(anyString(), anyInt())
				.defaultAnswer(Mockito.RETURNS_DEEP_STUBS)
		);
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


