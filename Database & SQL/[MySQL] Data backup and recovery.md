# Data backup and recovery
## backup
MySQL이 설치된 폴더의 'BIN' 로 이동, 파일의 형태로 백업이 됨
```
MySQLDump -u사용자 -p암호 DB이름 > DB백업.sql
```
```
ex) mysqldump -u root -p teambranch > 20211207_teambranch.sql
```
#### table backup
```
MySQLDump -u사용자 -p암호 DB이름 TB이름 > TB백업.sql
```
#### data backup
```
MySQLDump -u사용자 -p암호 DB이름 TB이름 -w "조건" > 데이터백업.sql
```
## recovery
```
MySQL -u사용자 -p암호 DB이름 < DB백업.sql -- DB가 존재 하지 않는 경우 미리 생성 후 진행 하여야 함.
```
```
ex) mysql -u root -p teambranch < 20211207_teambranch.sql
```
#### table recovery
```
MySQL -u사용자 -p암호 DB이름 TB이름 < TB백업.sql
```
#### data recovery
```
MySQL -u사용자 -p암호 DB이름 TB이름 < 데이터백업.sql
```
주의) 복원 명령 시 기존의 테이블은 제거 된 후 재생성 하여 복원 됨 (기존 데이터는 삭제됨) 
#### TIP) 파일명 자동 생성 명령을 위한 명령문 
```
ex) mysqldump -uroot -p1234 test_db > test_db_%date%.sql -- ('test_db_2013-04-02.sql' 형태로 생성됨) 
```
