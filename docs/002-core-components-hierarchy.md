# SQL 처리기 핵심 구성 계층화

## 1. CLI SQL 입력 처리

텍스트 파일에 작성된 SQL문을 Command Line 명령으로 SQL 처리기에 전달하는 영역이다.

### 1.1 실행 인자 처리

사용자가 입력한 SQL 파일 경로를 Command Line 인자로 받는다.

예시:

```text
./mini_db queries/input.sql
```

### 1.2 SQL 파일 읽기

전달받은 파일을 열고, 파일 안의 SQL 문자열을 메모리로 읽어온다.

### 1.3 입력 검증

파일 경로가 없거나, 파일을 열 수 없거나, SQL 내용이 비어 있는 경우를 처리한다.

## 2. SQL Parser + Executor

입력된 SQL을 구조화하고, 그 결과에 따라 `INSERT` 또는 `SELECT` 동작을 실행하는 영역이다.

### 2.1 SQL 타입 판별

SQL 문장이 `INSERT`인지 `SELECT`인지 구분한다.

### 2.2 SQL 파싱

SQL 문자열에서 테이블명, 컬럼, 값, 조회 대상 같은 실행에 필요한 정보를 뽑아낸다.

예시:

```sql
INSERT INTO users VALUES (1, 'kim');
SELECT * FROM users;
```

### 2.3 실행 분기

파싱 결과를 기준으로 `INSERT` 실행 함수 또는 `SELECT` 실행 함수를 호출한다.

## 3. 파일 기반 저장소

테이블별 파일을 두고, 데이터를 저장하거나 조회하는 영역이다.

### 3.1 테이블 파일 매핑

테이블 이름을 실제 파일 경로로 변환한다.

예시:

```text
users -> data/users.tbl
```

### 3.2 INSERT 저장

파싱된 값을 테이블 파일 끝에 추가한다.

### 3.3 SELECT 조회

테이블 파일을 읽고, 조건에 맞는 데이터를 출력한다.

## 전체 계층 구조

```text
SQL 처리기
├── 1. CLI SQL 입력 처리
│   ├── 1.1 실행 인자 처리
│   ├── 1.2 SQL 파일 읽기
│   └── 1.3 입력 검증
├── 2. SQL Parser + Executor
│   ├── 2.1 SQL 타입 판별
│   ├── 2.2 SQL 파싱
│   └── 2.3 실행 분기
└── 3. 파일 기반 저장소
    ├── 3.1 테이블 파일 매핑
    ├── 3.2 INSERT 저장
    └── 3.3 SELECT 조회
```

## 실행 흐름

```text
SQL 파일 입력
-> 실행 인자 처리
-> SQL 파일 읽기
-> SQL 타입 판별
-> SQL 파싱
-> INSERT / SELECT 실행
-> 테이블 파일 저장 또는 조회
```
