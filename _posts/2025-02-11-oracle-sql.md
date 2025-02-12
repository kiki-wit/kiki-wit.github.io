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
