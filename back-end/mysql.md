# mySQL 셋팅\(버전 8.0.17 기준\)

## 로그인

```bash
mysql -uroot -p
```

## 데이터베이스 생성

```text
create database 데이터베이스명;
```

## 유저 생성 & 권한 설정

```text
CREATE USER '유저명';
GRANT all on 데이터베이스명.테이블명 TO '유저명'@'<host>';
FLUSH PRIVILEGES;
```

## 예제

```text
mysql -uroot -p;
create database connectdb;
create user 'connectuser'@'localhost' identified by 'connect123!@#';
grant all on connectdb.* to 'connectuser'@'localhost';
flush privileges;
```

[원문 link](https://www.rosehosting.com/blog/create-a-new-mysql-user-and-grant-permissions-to-mysql-database/) [추가 link](https://link2me.tistory.com/431)

{% tabs %}
{% tab title="Basic" %}
```text
show databases;
use [DB Name];
show tables;
desc [table Name];
\c //취소
```
{% endtab %}

{% tab title="More" %}
```text
select user,host from mysql.user; //등록된 모든 유저 확인
select user(); //현재 접속 유저
select version(); //mysql 버전
select current_date;
select now();

```
{% endtab %}
{% endtabs %}

