### 인덱스 사용 이유

* 데이터를 신속하게 찾기 위해서 사용한다.
* 인덱스가 없는 수백만 개의 행을 가진 테이블의 경우, 데이터 검색의 결과를 반환하는 데 많은 시간이 걸린다.
* <https://www.mysqltutorial.org/mysql-index/mysql-create-index/>

<br>

### 인덱스 소개

* 인덱스는 B-Tree 구조로 검색 속도를 유지 보수하기 위한 쓰기 및 저장에 소요되는 비용을 절감한다.
* primary key 또는 unique key와 함께 테이블을 생성하면 MySQL은 자동으로 PRIMARY index를 생성하고 이를 clustered index라고 부른다.
* PRIMARY index가 아닌 인덱스를 secondary index 또는 non-clustered index라고 부른다.

<br>

### 인덱스 생성

* column 또는 column 집합에 대해서 인덱스를 추가하려면 CREATE INDEX를 사용한다.
* CREATE INDEX 인덱스명 ON 테이블명 (column_list);

<br>

### 인덱스 종류

* 기본적으로 MySQL은 인덱스 유형을 지정하지 않으면 B-Tree 인덱스를 생성한다.

|저장 엔진|허용된 인덱스 유형|
|--------|-----------------|
|InnoDB|BTREE|
|MyISAM|BTREE|
|MEMORY/HEAP|HASH, BTREE|

<br>

### 인덱스 확인

* 'EXPLAIN + 쿼리'를 이용해서 인덱스를 참조했는지 확인해보자.
* EXPLAIN SELECT employeeNumber, lastName, firstName FROM employees WHERE jobTitle = 'Sales Rep';
* 인덱스 없이 전체를 스캔 한 경우
<img src = "https://user-images.githubusercontent.com/53414240/131798910-aaf2bf0a-c2aa-4ceb-9281-dcc14723eafa.png" width="70%" height="70%">

* 인덱스를 참조한 경우
<img src = "https://user-images.githubusercontent.com/53414240/131799010-d4511478-1ebf-4be4-ac0e-644c0bf3130d.png" width="70%" height="70%">

<br>

### 인덱스 조회

* 테이블의 인덱스를 확인하려면 SHOW INDEXES를 사용하자.
* SHOW INDEXES FROM 테이블명;
* <https://www.mysqltutorial.org/mysql-index/mysql-show-indexes/>

<br>

### 다른 DB 인덱스 조회

* SHOW INDEXES FROM 테이블명 IN DB명;
* SHOW INDEXES FROM DB명.테이블명;
* 위의 쿼리는 서로 유사하다.
* SHOW INDEXES IN 테이블명 FROM DB명;
* SHOW KEYS FROM 테이블명 IN DB명;
* 위의 쿼리는 서로 같다.
* 참고로 INDEXES 쿼리에서 INDEX와 KEYS는 동의어고 IN과 FROM도 동의어다.

<br>

### clustered index on InnoDB tables

* MySQL은 clustered index의 행 검색에 primary key 값을 사용한다.
* 따라서 primary key가 짧은 것이 유리하다.
* 일반적으로 primary key는 auto-increment integer를 사용한다.
* <https://www.mysqltutorial.org/mysql-index/mysql-clustered-index/>

<br>

### 인덱스와 Cardinality

* Cardinality 낮은 경우 인덱스를 사용하지 않고 행 전체를 스캔하는 것이 효과적일 수 있다.
* <https://www.mysqltutorial.org/mysql-index/mysql-index-cardinality/>

<br>

### USE INDEX hint

* query optimizer 최상의 계획을 위해 많은 매개 변수를 사용한다.
* 사용할 인덱스를 선택하는 가장 중요한 매개변수 중 하나는 cardinality이다.
* 그러나 많은 삽입 또는 삭제하여 테이블 많이 수정된 경우 cardinality가 정확하지 않다.
* 이 문제를 해결하려면 ANALYZE TABLE 문을 주기적으로 실행하여 cardinality를 업데이트해야 한다.
* 또는 USE INDEX라는 인덱스 힌트를 사용하여 query optimizer가 수행하는 인덱스를 추천할 수 있는 대체 방법이 있다.
* SELECT 컬럼명 FROM 테이블명 USE INDEX(인덱스리스트) WHERE 조건;
* 위의 구문에서 USE INDEX(인덱스리스트)는 query optimizer에게 명명된 인덱스리스트 중 하나를 사용하여 테이블에서 행을 찾도록 지시한다.
* <https://www.mysqltutorial.org/mysql-index/mysql-use-index/>
