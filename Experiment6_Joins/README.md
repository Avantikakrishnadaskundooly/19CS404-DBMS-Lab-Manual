# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
--
<img width="1189" height="774" alt="image" src="https://github.com/user-attachments/assets/5d317d0b-94ea-4d3b-8d48-5640311723c2" />

```sql
select p.first_name from patients p
join surgeries s on p.patient_id=s.patient_id
where surgery_date='2024-01-15';
```

**Output:**

<img width="509" height="468" alt="image" src="https://github.com/user-attachments/assets/48e41e0c-430b-4390-8fa0-e348b149476e" />

**Question 2**
---
<img width="1245" height="765" alt="image" src="https://github.com/user-attachments/assets/eaa18794-73cb-4486-9fea-b0c67fefe359" />
<img width="1263" height="724" alt="image" src="https://github.com/user-attachments/assets/6a9944ee-f476-46d8-9fe9-dbf51aa9017d" />

```sql
select o.ord_no,o.purch_amt,o.ord_date,c.cust_name,c.city as 'customer_city',c.grade,s.name as 'salesman_name',s.city as 'salesman_city',s.commission
from salesman s
join customer c on s.salesman_id=c.salesman_id
join orders o on c.customer_id=o.customer_id;
```

**Output:**

<img width="1257" height="785" alt="image" src="https://github.com/user-attachments/assets/980448b8-c6f3-4975-a595-ad0e048165dd" />

**Question 3**
---
<img width="1179" height="679" alt="image" src="https://github.com/user-attachments/assets/883e5bb5-28fe-4f49-b1d6-476486fdd70d" />

```sql
select p.* from patients p
join test_results t on p.patient_id=t.patient_id
where t.test_name='X-Ray' and t.result='Normal';
```

**Output:**

<img width="1260" height="485" alt="image" src="https://github.com/user-attachments/assets/0f0d0f4a-5161-4ee3-bece-40c3097765a8" />

**Question 4**
---
<img width="1230" height="633" alt="image" src="https://github.com/user-attachments/assets/4e61e9a5-2816-401e-b8f6-983589beec4b" />
<img width="748" height="317" alt="image" src="https://github.com/user-attachments/assets/05e4c83b-134d-47fc-bcc4-3abb6fcdfc7a" />

```sql
select c.cust_name,c.city,c.grade,s.name as 'Salesman',s.city
from salesman s
join customer c on s.salesman_id=c.salesman_id
where c.grade<300 
order by c.customer_id asc;
```

**Output:**

<img width="1262" height="855" alt="image" src="https://github.com/user-attachments/assets/ad9a16f0-8680-400c-b91e-c8191996491b" />

**Question 5**
---
<img width="1221" height="620" alt="image" src="https://github.com/user-attachments/assets/14624597-6a63-4d12-8efe-97481e2b09b8" />
<img width="654" height="375" alt="image" src="https://github.com/user-attachments/assets/b69be2ed-3591-4e2f-85cf-f87bee22b696" />

```sql
select c.cust_name as 'Customer Name',c.city,s.name as 'Salesman',s.commission
from salesman s
join customer c on s.salesman_id=c.salesman_id;
```

**Output:**

<img width="1264" height="860" alt="image" src="https://github.com/user-attachments/assets/ad8cefa2-32b5-4646-8c03-7418535af846" />

**Question 6**
---
<img width="1187" height="386" alt="image" src="https://github.com/user-attachments/assets/6bf67f85-675d-4d8f-a68c-038c9973475c" />

```sql
select c.* from customer c
left join orders o on c.customer_id=o.customer_id
where ord_date between '2012-07-01' and '2012-07-30';
```

**Output:**

<img width="1262" height="486" alt="image" src="https://github.com/user-attachments/assets/14303bba-f0ce-4c94-b708-17a6b986627a" />

**Question 7**
---
<img width="1213" height="614" alt="image" src="https://github.com/user-attachments/assets/65d17f3f-eadb-4556-a8c9-00a7f7120cb8" />
<img width="648" height="328" alt="image" src="https://github.com/user-attachments/assets/5e7c6f7e-1cbe-485f-86e1-ff8ffce2603d" />

```sql
select c.cust_name as 'Customer Name',c.city,s.name as 'Salesman',s.commission
from salesman s
join customer c on s.salesman_id=c.salesman_id
where s.commission>0.12;
```

**Output:**

<img width="1265" height="850" alt="image" src="https://github.com/user-attachments/assets/13bf92c1-c6b3-4c7d-af73-c6507ab53671" />

**Question 8**
---
<img width="1242" height="771" alt="image" src="https://github.com/user-attachments/assets/76a6b50d-8acc-49d4-bda7-14e221f3fc55" />
<img width="999" height="723" alt="image" src="https://github.com/user-attachments/assets/028b8bc1-38d8-45ca-b12b-884665a7890c" />

```sql
select o.ord_no,o.ord_date,o.purch_amt,c.cust_name as 'Customer Name',c.grade,s.name as 'Salesman',s.commission
from salesman s
join customer c on s.salesman_id=c.salesman_id
join orders o on c.customer_id=o.customer_id;
```

**Output:**

<img width="1265" height="788" alt="image" src="https://github.com/user-attachments/assets/e719861b-bdd5-4446-816d-ac451d5e9a25" />

**Question 9**
---
<img width="1255" height="780" alt="image" src="https://github.com/user-attachments/assets/32589fbd-f9d9-43ec-a433-4753625d39ba" />

```sql
select p.first_name,s.surgery_id,p.patient_id,s.surgeon_id,s.surgery_date 
from surgeries s
join patients p on p.patient_id=s.patient_id
where p.first_name='Alice';
```

**Output:**

<img width="1256" height="490" alt="image" src="https://github.com/user-attachments/assets/2cb8325c-8ed4-4d35-8690-5812fbc192c6" />

**Question 10**
---
<img width="1253" height="409" alt="image" src="https://github.com/user-attachments/assets/4bafe975-e61b-4a03-91f4-cb0806fe6a00" />

```sql
select c.* from customer c
left join orders o on c.customer_id=o.customer_id
where o.ord_date between '2012-08-01' and '2012-08-30';
```

**Output:**

<img width="1261" height="558" alt="image" src="https://github.com/user-attachments/assets/bcd8e47c-f833-47dc-8482-50fa4dcd64c1" />

## Module Examination (SEB)
<img width="1141" height="78" alt="image" src="https://github.com/user-attachments/assets/56f2e016-2d37-4d7a-9161-20fc710d4097" />


## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
