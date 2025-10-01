---
layout: post
title: "Compare Sybase Date"
date: 2023-03-07 15:00:00
category: sql
tags: [sybase]
---

** SLOG_TABLES

| TABLES_SN | NAME              | CDATE               |
|-----------|-------------------|---------------------|
| 1         | SLOG_201901300835 | 2019-01-30 08:35:59 |
| 2         | SLOG_202201300935 | 2022-01-30 09:35:59 |
| 3         | SLOG_202212151513 | 2022-12-15 15:13:00 |
| 4         | SLOG_202212150907 | 2022-12-19 14:23:00 |


只會查出最後一筆:  

```sql
SELECT * FROM SLOG_TABLES WHERE(UPCODE IS NULL OR UPCODE<>'D') AND 
CDATE>(SELECT CONVERT(DATE,CDATE) FROM SLOG_TABLES WHERE(UPCODE IS NULL OR UPCODE<>'D') AND TABLES_SN=3);
```

要加等號才會查出最後 2 筆:   

```sql
SELECT * FROM SLOG_TABLES WHERE(UPCODE IS NULL OR UPCODE<>'D') AND 
CDATE>=(SELECT CONVERT(DATE,CDATE) FROM SLOG_TABLES WHERE(UPCODE IS NULL OR UPCODE<>'D') AND TABLES_SN=3);
```

如果用字串, 也會是 2筆:
```sql
SELECT * FROM SLOG_TABLES WHERE(UPCODE IS NULL OR UPCODE<>'D') AND 
CDATE>'2022-12-15';
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


