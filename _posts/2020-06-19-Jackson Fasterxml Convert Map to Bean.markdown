---
layout: post
title: "Jackson Fasterxml Convert Map to Bean"
date: 2020-06-18 09:14:00
category: program
tags: [json, jackson, fastxml]
---

The bean: AllowTime.java
```java
@JsonSerialize(using = CustomLocalTimeSerializer.class)
@JsonDeserialize(using = TimeToLocalTimeDeserializer.class)
LocalTime rmt_start;

@JsonSerialize(using = LocalDateToMiguoSerializer.class)
@JsonDeserialize(using = TimestampToLocalDateDeserializer.class)
LocalDate start_date;
```

Serializer1 : LocalDateToMiguoSerializer
```java
public class LocalDateToMiguoSerializer extends LocalDateSerializer {

	private static final long serialVersionUID = 1L;

	@Override
	public void serialize(LocalDate value, JsonGenerator g, SerializerProvider provider) throws IOException {
		DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyMMdd");

		MinguoChronology minguo = MinguoChronology.INSTANCE;
		String result = formatter.format(minguo.dateEpochDay(value.toEpochDay()));

		g.writeString(result);
	}

}
```

Serializer2 : CustomLocalTimeSerializer
```java
public class CustomLocalTimeSerializer extends LocalTimeSerializer {

	private static final long serialVersionUID = 1L;

	@Override
	public void serialize(LocalTime value, JsonGenerator g, SerializerProvider provider) throws IOException {
		DateTimeFormatter formatter = DateTimeFormatter.ofPattern("HHmm");

		String result = formatter.format(value);

		g.writeString(result);
	}

}
```

Deserializer1 : TimeToLocalTimeDeserializer
```java
public class TimeToLocalTimeDeserializer extends JsonDeserializer<LocalTime> {

	@Override
	public LocalTime deserialize(JsonParser jp, DeserializationContext dc) throws IOException, JsonProcessingException {
		return jp.readValueAs(Time.class).toLocalTime();
	}
}
```

由於都會用 Lombok 來簡化 setter/getter 就設定了: 
```java
@Setter(onMethod_={@JsonProperty(value="RMT_START")})
LocalTime rmt_start;
```
結果 ObjectManage 如果沒有 register 指定的 Deserializer, 則在 deserialize map 成 bean 時, 就會一直拋出：  
no constructor long integer...  
然後測了很久, 才知道是這個 `@Setter` 的問題。

另外也才知道, 其實可以不用在 bean 裡用 annotation 指定 serializer、deserializer,  
也可以在 Object Manager 指定。

好像兩邊都有道理, 尤其如果 serializer 是在 Object Manager 要執行時才指定,  
那就可以依據 view 的需求, serialize 成需要的格式。

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

