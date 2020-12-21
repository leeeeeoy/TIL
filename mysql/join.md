# Join

- RDB에서 두 개 이상의 테이블 or DB를 연결하여 데이터를 검색하는 방법
- 적어도 하나의 컬럼을 공유하고 있어야 함
- 보통 Primary Key or Foreign Key 로 두 테이블을 연결

### INNER JOIN

- 교집합, 기준 테이블과 join 테이블의 중복된 값

```sql
SELECT 테이블별칭.조회할칼럼, 테이블별칭.조회할칼럼 FROM 기준테이블 별칭 INNER JOIN 조인테이블 별칭 ON 기준테이블별칭.기준키 = 조인테이블별칭.기준키....

SELECT A.NAME, B.AGE FROM EX_TABLE A INNER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```

### LEFT OUTER JOIN

- 기준 테이블과 join테이블과 중복된 값을 보여줌
- 왼쪽 테이블을 기준으로 join을 함

```sql
SELECT 테이블별칭.조회할칼럼, 테이블별칭.조회할칼럼 FROM 기준테이블 별칭 LEFT OUTER JOIN 조인테이블 별칭 ON 기준테이블별칭.기준키 = 조인테이블별칭.기준키 .....

SELECT A.NAME, B.AGE FROM EX_TABLE A LEFT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```

### RIGHT OUTER JOIN

- 오른쪽 테이블을 기준으로 join

```sql
SELECT 테이블별칭.조회할칼럼, 테이블별칭.조회할칼럼 FROM 기준테이블 별칭 RIGHT OUTER JOIN 조인테이블 별칭 ON 기준테이블별칭.기준키 = 조인테이블별칭.기준키 .....

SELECT A.NAME, B.AGE FROM EX_TABLE A RIGHT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```

### FULL OUTER JOIN

- 합집합, A와 B의 모든 데이터를 검색

```sql
SELECT 테이블별칭.조회할칼럼, 테이블별칭.조회할칼럼 FROM 기준테이블 별칭 FULL OUTER JOIN 조인테이블 별칭 ON 기준테이블별칭.기준키 = 조인테이블별칭.기준키 .....

SELECT A.NAME, B.AGE FROM EX_TABLE A FULL OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```

### CROSS JOIN

- 모든 경우의 수를 검색함
- A가 3개, B가 4개의 데이터를 가진다면 3\*4 개의 데이터가 검색

```sql
--첫번째 방식
SELECT 테이블별칭.조회할칼럼, 테이블별칭.조회할칼럼 FROM 기준테이블 별칭 CROSS JOIN 조인테이블 별칭

--두번째 방식
SELECT 테이블별칭.조회할칼럼, 테이블별칭.조회할칼럼 FROM 기준테이블 별칭,조인테이블 별칭

SELECT A.NAME, B.AGE FROM EX_TABLE A CROSS JOIN JOIN_TABLE B

SELECT A.NAME, B.AGE FROM EX_TABLE A,JOIN_TABLE B
```

### SELF JOIN

- 자기 자신을 join 하는 것
- 하나의 테이블을 여러번 복사해서 join, 컬럼을 다양하게 변형시켜 활용할 때 자주 사용

```sql
SELECT 테이블별칭.조회할칼럼, 테이블별칭.조회할칼럼 FROM 테이블 별칭,테이블 별칭2

SELECT A.NAME, B.AGE FROM EX_TABLE A, EX_TABLE B
```
