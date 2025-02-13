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
