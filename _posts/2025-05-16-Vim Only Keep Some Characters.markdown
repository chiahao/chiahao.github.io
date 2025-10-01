---
layout: post
title: "Vim Only Keep Some Characters"
date: 2025-05-16 09:45:00
category: program
tags: [vim]
---

```bash
%s/\([^,()]*\)/?/g
```

Will convert  

```sql
(FORM_SN,ATTEND_DATE,DATE_PROPERTY,START_TIME,END_TIME,REST_TIME,REST_PRICE,LEGAL_PAY_BASE,EXT_HOUR_BEFORE,EXT_HOUR_AFTER,REGULAR_HOUR_MAX_EIGHT,TOTAL_HOUR,COMMENT,APPLICANT_TYPE,APPLICANT_PERSON_SN,UPPERSON_TYPE,UPPERSON_SN,UPCODE,UPDAT)
```

to  

```sql
(?,?,?,?,?,?,?,?,?,?,?,?,?,?,?,?,?,?,?)
```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

