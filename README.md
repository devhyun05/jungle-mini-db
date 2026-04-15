# 업데이트 내용
1. 테이블 포맷팅 
=> 출력 할때 테이블 보기 좋게 출력되게 
<img width="281" height="127" alt="image" src="https://github.com/user-attachments/assets/cb07b4f9-2b37-4d7b-92a7-c586bbd2619c" />

2. SQL 쿼리 case insensitive
<img width="289" height="258" alt="image" src="https://github.com/user-attachments/assets/92b356ad-4e46-4071-a4e7-986b3b8fe032" />

3. BETWEEN 절 작동하도록 구현 

<img width="1412" height="783" alt="image" src="https://github.com/user-attachments/assets/5f670ac2-de35-453a-8ccb-1c01f0f22267" />

### B+Tree BETWEEN 선택도별 성능 비교

테스트 조건:

- 데이터 수: 1,000,000 rows
- Row 크기: 64 bytes fixed row
- 반복 횟수: 각 케이스당 20회
- 측정 대상: 결과 출력 제외, range 탐색/count 비용만 비교
- 빌드 옵션: `clang -O2`

| 결과 row 수 | 선택도 | 조회 범위 | B+Tree 평균 | 선형 스캔 평균 | 차이 |
|---:|---:|---|---:|---:|---:|
| 1 | 0.0001% | 500000 ~ 500000 | 0.0016ms | 41.020ms | 24,934.5배 |
| 10 | 0.001% | 499995 ~ 500004 | 0.0018ms | 38.226ms | 20,688.1배 |
| 100 | 0.01% | 499950 ~ 500049 | 0.0021ms | 38.035ms | 18,549.9배 |
| 1,000 | 0.1% | 499500 ~ 500499 | 0.0069ms | 37.153ms | 5,420.1배 |
| 10,000 | 1% | 495000 ~ 504999 | 0.0533ms | 38.125ms | 714.7배 |
| 100,000 | 10% | 450000 ~ 549999 | 0.5490ms | 36.813ms | 67.0배 |
| 500,000 | 50% | 1 ~ 500000 | 2.9045ms | 40.109ms | 13.8배 |
| 1,000,000 | 100% | 1 ~ 1000000 | 6.2613ms | 41.681ms | 6.7배 |

인덱스 생성 시간은 약 3.13초였다.




