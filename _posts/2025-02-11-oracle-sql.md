---
date: 2025-02-11 22:03
layout: post
title: 오라클 SQL 개론
subtitle: 오라클 SQL 작성 방법
description: >-
  DDL, DML, DCL, TCL, FUNCTION, INDEX, SP 등에 대해 정리
image: 
optimized_image: https://res.cloudinary.com/dm7h7e8xj/image/upload/c_scale,w_380/v1559822138/theme9_v273a9.jpg
category: sql
tags:
  - 오라클
  - SQL
author: kiki
---
### 집계함수

`GROUPING SETS`
>GROUPING SETS는 여러 개의 GROUP BY 조건을 한 번에 정의한다. department 와 job 을 각각 집계하고 집계되지 않는 컬럼은 NULL 처리하여
집계되지 않을경우 1로 리턴시키고 집계된 데이터는 0으로 리턴한다.

```sql
SELECT department, job, sum(salary), GROUPING(department), GROUPING(job)
FROM employees
GROUP BY GROUPING SETS(department, job);
```

`원본`
<table border="1">
  <thead>
    <tr>
      <th>DEPARTMENT</th>
      <th>JOB</th>
      <th>SALARY</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Accounting</td>
      <td>Accountant</td>
      <td>50000</td>
    </tr>
    <tr>
      <td>Accounting</td>
      <td>Accountant</td>
      <td>50000</td>
    </tr>
    <tr>
      <td>Accounting</td>
      <td>Manager</td>
      <td>70000</td>
    </tr>
    <tr>
      <td>HR</td>
      <td>Recruiter</td>
      <td>60000</td>
    </tr>
    <tr>
      <td>HR</td>
      <td>Manager</td>
      <td>80000</td>
    </tr>
    <tr>
      <td>IT</td>
      <td>Developer</td>
      <td>90000</td>
    </tr>
  </tbody>
</table>

`결과`
<table border="1">
  <thead>
    <tr>
      <th>DEPARTMENT</th>
      <th>JOB</th>
      <th>SUM(SALARY)</th>
      <th>GROUPING(DEPARTMENT)</th>
      <th>GROUPING(JOB)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>HR</td>
      <td>-</td>
      <td>140000</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <td>IT</td>
      <td>-</td>
      <td>90000</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <td>Accounting</td>
      <td>-</td>
      <td>170000</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <td>-</td>
      <td>Developer</td>
      <td>90000</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <td>-</td>
      <td>Accountant</td>
      <td>100000</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <td>-</td>
      <td>Recruiter</td>
      <td>60000</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <td>-</td>
      <td>Manager</td>
      <td>150000</td>
      <td>1</td>
      <td>0</td>
    </tr>
  </tbody>
</table>

### 랭킹함수

`RANK` `DENSE_RANK` `ROW_NUMBER`
>순위를 매길 때 사용하는 윈도우 함수이다. 

`원본`
<table>
    <tr>
        <th>ID</th>
        <th>NAME</th>
        <th>SCORE</th>
    </tr>
    <tr>
        <td>1</td>
        <td>Alice</td>
        <td>90</td>
    </tr>
    <tr>
        <td>2</td>
        <td>Bob</td>
        <td>85</td>
    </tr>
    <tr>
        <td>3</td>
        <td>Charlie</td>
        <td>85</td>
    </tr>
    <tr>
        <td>4</td>
        <td>David</td>
        <td>80</td>
    </tr>
    <tr>
        <td>5</td>
        <td>Eve</td>
        <td>75</td>
    </tr>
</table>

```sql
SELECT ID, NAME, SCORE,
       RANK() OVER (ORDER BY SCORE DESC) AS RANKING,
       DENSE_RANK() OVER (ORDER BY SCORE DESC) AS DENSE_RANKING,
       ROW_NUMBER() OVER (ORDER BY SCORE DESC) AS ROW_NUM
FROM STUDENTS;
```
`결과`
<table>
    <tr>
        <th>ID</th>
        <th>NAME</th>
        <th>SCORE</th>
        <th>RANK()</th>
        <th>DENSE_RANK()</th>
        <th>ROW_NUMBER()</th>
    </tr>
    <tr>
        <td>1</td>
        <td>Alice</td>
        <td>90</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
    </tr>
    <tr>
        <td>2</td>
        <td>Bob</td>
        <td>85</td>
        <td>2</td>
        <td>2</td>
        <td>2</td>
    </tr>
    <tr>
        <td>3</td>
        <td>Charlie</td>
        <td>85</td>
        <td>2</td>
        <td>2</td>
        <td>3</td>
    </tr>
    <tr>
        <td>4</td>
        <td>David</td>
        <td>80</td>
        <td>4</td>
        <td>3</td>
        <td>4</td>
    </tr>
    <tr>
        <td>5</td>
        <td>Eve</td>
        <td>75</td>
        <td>5</td>
        <td>4</td>
        <td>5</td>
    </tr>
</table>

✅ **각 함수의 차이점**

1️⃣ RANK() 
- 동일한 점수(85)일 경우 같은 순위(2) 부여
- 다음 순위는 건너뛰어서 4가 됨

2️⃣ DENSE_RANK()
- 동일한 점수(85)일 경우 같은 순위(2) 부여
- 다음 순위는 연속적으로 3이 됨

3️⃣ ROW_NUMBER()
- 무조건 각 행마다 고유한 번호 부여
- 동점이라도 순서대로 번호가 매겨짐


### 계층형

- START WITH : 계층 구조 전개의 시작 위치를 지정한다.
- CONNECT BY : 다음에 전개될 자식 데이터를 지정한다.
- PRIOR : CONNECT BY절에 사용되며 PRIOR 자식 = 부모 (순방향 전개) 자식 = PRIOR 부모 (역방향 전개)
- NOCYCLE : 
- ORDER SIBLINGS BY : 형제 노드(동일 LEVEL) 사이에서 정렬을 수행한다.
- WHERE : 모든 전개를 수행한 후에 지정된 조건을 만족하는 데이터만 추출한다.

<br/>

### 가상컬럼(Pseudo Column)

<table>
  <tr>
      <th>LAVEL</th>
      <td>루트 데이터면 1, 그 하위 데이터면 2이다.</td>
  </tr>
  <tr>
      <th>CONNECT_BY_ISLEAF</th>
      <td>전개 과정에서 해당 데이터가 리프 데이터면 1, 그렇지 않으면 2이다.</td>
  </tr>
  <tr>
      <th>CONNECT_BY_ISCYCLE</th>
      <td>전개 과정에서 자식을 갖는데, 해당 데이터가 조상으로서 존재하면 1, 그렇지 않으면 0이다.</td>
  </tr>
</table>

### 계층형 질의에서 사용되는 함수

<table>
  <tr>
      <th>SYS_CONNECT_BY_PATH(컬럼, 경로분리자)</th>
      <td>루트 데이터부터 현재 전개할 데이터까지의 경로를 표시한다.</td>
  </tr>
  <tr>
      <th>CONNECT_BY_ROOT(컬럼)</th>
      <td>현재 전개할 데이터의 루트 데이터를 표시한다. 단항 연산자이다.</td>
  </tr>
</table>




