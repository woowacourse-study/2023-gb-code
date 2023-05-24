## 11강 결과 행 제한하기 - LIMIT

> LIMIT 구로 조회할 행의 수를 제한할 수 있다.

### 1. 행수 제한

LIMIT 구: 표준 SQL이 아니다. (MySQL, PostgreSQL 에서만 사용 가능)

`SELECT 열 FROM 테이블 WHERE 조건식 ORDER BY 열 LIMIT 행 수`

- LIMIT구는 SELECT 명령의 맨 마지막에 지정하는 것

LIMIT구에 지정한 만큼의 최대 행이 반환된다.

- ex) `SELECT * FROM sample33 LIMIT 10`
    - 최대 10개의 행 반환

**정렬한 후 반환하기**

> LIMIT는 WHERE구로 검색한 후, ORDER BY로 정렬한 뒤 **최종적으로** 처리된다.
- ex) `SELECT * FROM sample33 ORDER BY id DESC LIMIT 3`
    - id가 큰 순서대로 정렬된 후, 최대 3개의 데이터가 반환된다.

**LIMIT를 사용할 수 없는 데이터베이스에서의 행 제한**

MySQL, PostgreSQL 외의 데이터베이스에서 행 제한하기

- SQL Server
    - `TOP` 사용
    - `SELECT TOP 행수 조회할열 FROM 테이블명`
        - ex) `SELECT TOP 3 * FROM sample33`
- Oracle
    - `RONUM` 사용
    - `SELECT 열 FROM 테이블 WHERE ROWNUM <= 행수`
        - ex) `SELECT * FROM sample33 WHERE ROWNUM <= 3`
    - ROWNUM: 클라이언트에게 결과가 반환될 때, 각 행에 할당되는 행 번호
    - ROWNUM은 WHERE구로 지정하기 때문에 **정렬되기 전에 처리**된다.
        - 따라서, 정렬 후 처리되는 LIMIT와 조회 결과 다름

### 2. 오프셋 지정

웹 시스템에서는 페이지 단위로 조회 결과를 보여준다. → **pagination**

`SELECT 열 FROM 테이블 LIMIT 행수 OFFSET 시작위치`

> OFFSET은 생략 가능하며, 기본값은 0이다.
**시작행 - 1** 로 OFFSET을 지정한다. 
OFFSET에 의한 시작 지정은 LIMIT 뒤에 작성한다.

ex) 한 페이지에 5개의 데이터를 보여주는 페이지가 있을 때

- 첫 페이지는1번 ~ 5번 데이터를 보여준다. → LIMIT 사용
    - `LIMIT 5` OR `LIMIT 5 OFFSET 0`
    - 1번 행부터 시작이므로 1 - 1 인 0을 지정
- 그 다음 페이지는 6번 ~ 10번 데이터를 보여준다. → LIMIT구에 OFFSET 지정
    - `SELECT * FROM sample33 LIMIT 5 OFFSET 5`
    - 6번 행부터 시작이므로 6 - 1 인 5를 지정
