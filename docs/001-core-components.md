# SQL 처리기 핵심 구성

## 1. CLI SQL 입력 처리

텍스트 파일에 작성된 SQL문을 Command Line 명령으로 SQL 처리기에 전달할 수 있어야 한다.

## 2. SQL Parser + Executor

`INSERT`, `SELECT` 문을 파싱하고, 파싱 결과에 따라 실제 동작을 실행해야 한다.

## 3. 파일 기반 저장소

테이블별 파일을 두고, `INSERT`는 파일에 데이터를 추가하며 `SELECT`는 파일에서 데이터를 읽어 출력해야 한다.

## 전체 흐름

```text
SQL 파일 입력
-> SQL 파싱
-> INSERT / SELECT 실행
-> 테이블 파일 저장 또는 조회
```

이 3가지가 과제의 핵심인 SQL 처리기를 구성하는 최소 단위다.
