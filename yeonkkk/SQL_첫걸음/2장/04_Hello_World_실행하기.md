# 04강. Hello World 실행하기

## 1. SELECT * FROM
> mysql 클라이언트에 SQL 명령을 입력하여 실행할 수 있다.  
> 명령 마지막엔 세미 콜론(;)을 붙인다.  

<br>

* SELECT 명령
```sql
-- SELECT 열 FROM 테이블명; 
SELECT * FROM 테이블명
```

<br><br>

## 2. SELECT 명령 구문

* SELECT 는 DML에 속한다.
* SELECT 명령은 '질의', '쿼리' 라고 불린다.
* 애스터리스크(*): 모든 열을 의미하는 메타문자
* SQL 명령은 키워드에 의해 '구'라는 단위로 나눌 수 있고, SELECT 명령은 여러개의 구로 구성된다.  

<br><br>

## 3. 예약어와 데이터베이스 객체명

* SELECT, FROM은 구를 결정하는 키워드이자 예약어 이다.
* 데이터베이스 객체: 다양한 데이터를 저장, 관리하는 것으로 뷰(view)가 해당된다.
* 데이터베이스 객체는 이름을 붙여 관리하며, 같은 이름으로 생성이 불가하다.
* 데이터베이스 객체와 예약어 이름은 중복하여 사용할 수 없다.
* 예약어와 데이터베이스 객체명은 대소문자를 구별하지 않는다(데이터베이스 제품에 따라 다를 수 있으니 주의).

<br><br>

## 4. 실행한 결과 = 테이블
> 테이블은 행과 열로 구성된 표 형식의 데이터다.

* 표 형식의 데이터는 행과 열로 구성된다.
  * 행: 레코드
  * 열: 컬럼, 필드/열마다 이름 지정
  * 셀: 행과 열이 만나는 부분. 하나의 데이터 값이 저장

<br><br>

### 자료형
> 데이터는 자료형으로 분류할 수 있다.  
> 열은 하나의 자료형만 가질 수 있다.  

* 수치형 데이터: 숫자로만 구성된 데이터 / 오른쪽 정렬
* 문자열형 데이터: 임의의 문자로 구성된 데이터 / 왼쪽으로 정렬
* 날짜형 데이터: 날짜와 시각을 나타내는 데이터 / 왼쪽으로 정렬

<br><br>

## 5. 값이 없는 데이터 (NULL)
> NULL은 데이터가 들어있지 않은 것을 의미하는 특별한 값이다.



