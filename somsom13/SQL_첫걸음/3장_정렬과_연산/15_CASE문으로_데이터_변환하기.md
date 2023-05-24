## 15강 CASE 문으로 데이터 변환하기

> CASE문을 사용해서 독자적으로 데이터를 변환할 수 있다.

### 1. CASE 문

RDBMS에서 제공하는 연산자, 함수만으로는 처리할 수 없는 케이스가 있다.

ex) NULL을 0으로 간주하여 연산하는 것 (실제로는 NULL이 포함된 연산 결과는 모두 NULL이 된다.

RDBMS에서는 사용자가 함수를 정의할 수 있지만, **간단한 상황에서는 CASE문으로 처리**할 수 있다.

```sql
CASE 
	WHEN 조건식1 THEN 식1
	[WHEN 조건식2 THEN 식2 ...]
	[ELSE 식3]
END
```

- WHEN절: 참, 거짓을 반환하는 조건식 기술
    - WHEN절이 참이라면, THEN에 기술한 식이 처리된다.
    - **가장 먼저 처리된 WHEN절과 대응되는 THEN의 처리 결과가 CASE문의 반환값**
    - 무엇도 만족하지 못하면 ELSE에 기술한 결과가 반환값
    - **ELSE를 생략하면, ‘ELSE NULL’로 간주**

```sql
SELECT CASE WHEN a IS NULL THEN 0 ELSE a END "a(null=0)" FROM 테이블명;
```

- a컬럼을 선택할 때, a가 NULL이라면 0으로 선택 / NULL이 아니라면 그 값을 그대로 선택
- 선택한 필드명: “a(null=0)”

**COALESCE**

NULL반환을 처리하는 경우에는 **COALESCE 함수**를 사용하는 것이 편하다.

- `SELECT COALESCE(a, 0) FROM 테이블명`
- 여러 개의 인수를 지정할 수 있다.
    - NULL이 아닌 인수는 지정된 인수의 값을 반환
    - NULL이 아니라면 지정한 값 (여기서는 0)을 출력

### 2. 또 하나의 CASE 문

> 숫자로 이루어진 코드를 알아보기 쉽게 문자열로 변환하는 경우 CASE문을 사용한다.

ex) 1 → 남자, 2 → 여자 라면 문자열로 변환하여 표기(디코드)

```sql
WHEN a = 1 THEN '남자'
WHEN a = 2 THEN '여자'
```

**검색 CASE 문 VS 단순 CASE 문**

- 검색 CASE문
    - `CASE WHEN 조건식 THEN 식` 의 형식
    - 위의 NULL처리, 디코드 예시가 여기에 해당
- 단순 CASE문

```sql
CASE 식1
	WHEN 식2 THEN 식3
	[WHEN 식3 THEN 식4]
	[ELSE 식6]
END
```

- 식1의 값이 WHEN뒤의 식(식2)와 동일한지 비교 → 동일하다면 식3이 결과로 반환
- 가장 먼저 식1과 일치하는 CASE의 THEN이 결과가 된다.
- 모두 일치하지 않는다면 ELSE절이 적용

**검색 CASE 예시**

```sql
SELECT a AS '코드'
CASE 
	WHEN a = 1 THEN '남자'
	WHEN a = 2 THEN '여자'
	ELSE '미지정'
END AS '성별' FROM 테이블명;
```

- CASE뒤에 식이 오지 않고, WHEN 뒤에 조건식이 온다.

**단순 CASE 예시**

```sql
SELECT a AS '코드'
CASE a
	WHEN 1 THEN '남자'
	WHEN 2 THEN '여자'
	ELSE '미지정'
END AS '성별' FROM 테이블명;
```

- CASE뒤에 비교대상이 될 식이 오고, WHEN 뒤에 비교대상과 비교할 **조건식이 아닌 값**이 온다.

### 3. CASE를 사용할 경우 주의사항

> CASE는 SELECT 뿐만 아니라 어디에나 사용할 수 있다.
- SELECT, WHERE, ORDER BY 등등..

**ELSE 생략**

- ELSE를 생략하면 `ELSE NULL` 로 처리된다.
- **ELSE를 생략하지 않고 지정하는 것이 좋다.**

**WHEN에 NULL 지정하기**

- **단순 CASE문**에서 `CASE a WHEN NULL THEN '값'` 은 문법적 오류는 아니지만, **정상 처리되지 않는다.**
- **조건식이 처리될 때, `a = NULL` 로 처리가 되지만 NULL은 `=` 으로 비교할 수 없다.**
- 따라서, CASE문에서 NULL을 처리하기 위해서는 **검색 CASE문**을 사용해야 한다.
    - `CASE WHEN a IS NULL THEN '값'`

**DECODE NVL**

- 디코드: 특정 값을 문자열로 표현하는 것

Oracle에서는 DECODE 함수를 제공하지만, 다른 데이터베이스 제품에서는 사용할 수 없다.
