# 11강 결과 행 제한하기 - LIMIT

## 행수 제한

- 주의) LIMIT은 표준 SQL이 아닌 MySQL과 PostgreSQL에서 사용할 수 있는 문법임
- LIMIT 구는 SELECT 명령의 마지막에 지정 (WHERE / ORDER BY 구 뒤에 지정)
- LIMIT 구를 통해 반환될 최대 행수를 제한할 수 있음

    ```sql
    SELECT 열명 FROM 테이블명 WHERE 조건식 ORDER BY 열명 LIMIT 행수
    ```


### 정렬한 후 제한하기

- WHERE 구를 통해 LIMIT 구와 동일한 결과를 얻을 수 있음
    - `LIMIT 3` → `WHERE no ≤ 3`
- 다만 LIMIT과 WHERE의 기능과 내부처리 순서가 다름
    - LIMIT : 반환할 행수를 제한
    - WHERE : ORDER BY로 정렬한 뒤 최종적으로 처리 (상위 n개라는 조건을 거는 것임)

### LIMIT를 사용할 수 없는 데이터베이스에서의 행 제한

- MySQL, PostgreSQL : LIMIT 구 사용 가능
- SQL Server : LIMIT 대신 TOP 사용

    ```sql
    SELECT TOP 3 * FROM sampleTable;
    ```

- Oracle : ROWNUM 열을 사용해 WHERE 구로 조건을 지정해 행 제한
    - ROWNUM : 결과가 반환될 때 각 행에 할당되는 행 번호
    - 이 경우 WHERE 구로 지정하기에 정렬하기 전에 처리되어 LIMIT과 결과가 다를 수 있음

    ```sql
    SELECT * FROM sampleTable WHERE ROWNUM <= 3;
    ```


## 오프셋 지정

- LIMIT을 통해 페이지 나누기 기능을 구현할 수 있음
    - 페이지 나누기 기능(pagination) : 대량 데이터를 하나의 페이지에 표시하는 것은 기능 및 속도 측면에서 효율적이지 못하기에, 페이지 단위로 화면에 표시할 내용을 처리함
- LIMIT 구 뒤에 OFFSET을 지정하여 데이터 시작 위치를 지정할 수 있음
- OFFSET은 생략 가능하며, 기본값은 0
- 위치 지정은 0부터 시작으로 `시작할 행 - 1`으로 설정

    ```sql
    SELECT 열명 FROM 테이블 LIMIT 행수 OFFSET 위치
    ```

- 예시

    ```sql
    // 첫 번째 페이지로 1행부터 3건의 데이터를 반환
    SELECT * FROM sampleTable LIMIT 3 OFFSET 0;
    
    // 두 번째 페이지로 4행부터 3건의 데이터를 반환
    SELECT * FROM sampleTable LIMIT 3 OFFSET 3
    ```
