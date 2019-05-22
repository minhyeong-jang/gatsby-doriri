---
title: Mysql Query 정리
date: 2019-05-22 17:05:10
category: database
---

> 개발을 진행하며 학습한 라이브러리를 계속 추가하는 문서입니다.

### 문자열 붙이기

```sql
concat(문자열 or 컬럼명, 문자열 or 컬럼명, …)

SELECT concat("hello","world")
-> helloworld
```

### SELECT 결과 DELETE 하기

```sql
delete from products where number in (
	select * from (
		select number from products where number > 20
	) as a
)
-- 동일 테이블 조작이 불가능하여 임시 테이블인 select * from () as a 생성
```

### SELECT 결과 INSERT 하기

```sql
insert info aaa
( title, name, wdate )
select title, name, wdate
from bbb
where name = "test"
```

### SELECT 결과 UPDATE 하기

```sql
update ord as a,
(select uniq from ord where sol_no = 1583 limit 380, 400) as b
set wdate = '2018-08-05 10:00:00'
where a.uniq = b.uniq and sol_no = 1583;
```
