# 9강 정렬 - ORDER BY

## ORDER BY로 검색 결과 정렬하기

- SELECT 명령 시 정렬하고 싶은 열에 대 ORDER BY로 지정
  → 열의 값에 따라 행 순서가 변경됨
- ORDER BY는 WHERE 구 뒤에 지정함

    ```sql
    SELECT 열명 FROM 테이블명 WHERE 조건식 ORDER BY 열명
    ```

- 검색 조건이 필요 없는 경우 WHERE 구 생략 후 FROM 뒤에 ORDER BY 구 지정

    ```sql
    SELECT 열명 FROM 테이블명 ORDER BY 열명
    ```


## ORDER BY DESC로 내림차순 정렬하기

- 내림차순 지정 : 정렬할 열명 뒤에 DESC(Descendant) 붙이기
- 오름차순 지정 : 생략 or 정렬할 열명 뒤에 ASC(Ascendant) 붙이기

    ```sql
    // 내림차순으로 정렬
    SELECT 열명 FROM 테이블명 ORDER BY 열명 DESC
    
    // 오른차순으로 정렬
    SELECT 열명 FROM 테이블명 ORDER BY 열명 ASC
    SELECT 열명 FROM 테이블명 ORDER BY 열명
    ```


## 대소관계

- 수치형 데이터(숫자, 날짜시간형 데이터) : 숫자 크기로 판별
- 문자열형 데이터 : 사전식 순서로 판별

### 사전식 순서에서 주의할 점

- 문자열형 열에 숫자를 문자로 저장한 경우를 주의해야 함
    - 1, 2, 10, 11을 정렬했을 때 1, 10, 11, 2로 정렬이 됨
- 위와 같은 경우 대소관계를 계산하는 방법을 달리 해주어야 함

## ORDER BY는 테이블에 영향을 주지 않는다

- ORDER BY를 이용해 행 순서를 바꿀 수는 있지만, 저장장치의 행 순서를 변경하는 것은 아님
- 서버에서 클라이언트로 행 순서를 바꾸어 결과를 반환하는 것 뿐임
