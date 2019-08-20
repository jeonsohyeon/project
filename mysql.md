# mySQL 셋팅\(버전 8.0.17 기준\)

## 로그인

```text
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

