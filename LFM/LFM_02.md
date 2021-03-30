# LFM_02_SQL_Developer_
## :muscle:실수에서 배우자 02 - SQL Developer
* 어느날 갑자기 SQL 디벨로퍼에서 DB 연결이 되지 않고 아래와 같은 에러 메세지가 나온다. 무언가 잘못 건드린게 분명하다.
![SQL_Developer_Error_Message](https://raw.githubusercontent.com/372dev/TIL/main/LFM/img/02_01.JPG)

### :star:원인
* ORA-12514, TNS 리스너 에러이다. 가끔 서비스 진입 방식에 따라 ORA-12505 에러가 뜨기도 했다.

* 가능한 원인
  1. 사용 가능한 DB가 없다. 혹은 해당 리스너에 등록된 서비스가 없다.
  2. tnsnames.ora의 서비스 이름이 리스너의 서비스 이름과 매치 되지 않는다.
  3. 서비스 이름이 사용자가 생각하고 있는 포트와 다른 포트에 등록되어 있다.

* 다양한 자료를 검색해 보니 문제는 SID에서 발생한 것 같다. 새로운 DB를 생성할 때 가이드라인을 따르지 않고 직관적으로 이것저것 설정한게 잘못된 것 같다.

### :star:OracleXETNListener 실행 확인
1. 윈도우 검색창에서 services.msc를 검색해서 실행한다.
2. OracleXETNListener가 실행중임을 확인한다.
![services.msc](https://raw.githubusercontent.com/372dev/TIL/main/LFM/img/02_02.JPG)

### :star:listener.ora 수정
* 나는 SQL 디벨로퍼에서 연습용 테스트 서버만 만들어 사용했고 SID를 모두 XE로 입력했다. 때문에 아래 방법으로 해결이 가능하다.

1. C:\oraclexe\app\oracle\product\11.2.0\server\network\ADMIN 경로의 listener.ora를 연다.

```sql
SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (SID_NAME = PLSExtProc)
      (ORACLE_HOME = C:\oraclexe\app\oracle\product\11.2.0\server)
      (PROGRAM = extproc)
    )
    (SID_DESC =
      (SID_NAME = CLRExtProc)
      (ORACLE_HOME = C:\oraclexe\app\oracle\product\11.2.0\server)
      (PROGRAM = extproc)
    )
  )

LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1))
      (ADDRESS = (PROTOCOL = TCP)(HOST = DESKTOP-DT78ROT)(PORT = 1521))
    )
  )

DEFAULT_SERVICE_LISTENER = (XE)
```

2. 이중에 SID_DESC 부분을 수정한다.

```sql
    (SID_DESC =
      (GLOBAL_DBNAME = XE)
      (SID_NAME = XE)
      (ORACLE_HOME = C:\oraclexe\app\oracle\product\11.2.0\server)
    )
```

수정 후

```sql
SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (SID_NAME = PLSExtProc)
      (ORACLE_HOME = C:\oraclexe\app\oracle\product\11.2.0\server)
      (PROGRAM = extproc)
    )
    (SID_DESC =
      (GLOBAL_DBNAME = XE)
      (SID_NAME = XE)
      (ORACLE_HOME = C:\oraclexe\app\oracle\product\11.2.0\server)
    )
  )

LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1))
      (ADDRESS = (PROTOCOL = TCP)(HOST = DESKTOP-DT78ROT)(PORT = 1521))
    )
  )

DEFAULT_SERVICE_LISTENER = (XE)
```

3. OracleXETNListener를 재실행한다.

### :star:문제가 발생한 DB 제거
* 문제를 발생시켰던 DB를 제외하고 다른 DB들은 이제 접근이 가능해졌다. 이전까지는 어느 DB에 접근하려 시도해도 같은 에러 메세지가 나왔다.

* 문제가 발생한 DB를 제거하고 가이드라인을 따라 새로 생성했다.

### :star:시행착오
* listener.ora에 손을 대기 전에 OracleXETNListener 부터 재실행 해보았으면 좋았을 것 같다. 그것만으로 문제가 해결될 수 있는지 궁금하다.

* DB를 생성할 땐 가이드라인을 보고 꼼꼼하게.

-References :  
https://mingggu.tistory.com/77  
https://logic.edchen.org/how-to-resolve-ora-12514-tns-listener-does-not-currently-know-of-service-requested-in-connect-descriptor/  
https://hulbo.tistory.com/28  
https://culinarydeveloper.tistory.com/42