# 创建数据库
create database 数据库名;
# 查看数据库
show database;
# 创建数据表
create table 表名(
    属性名1 数据类型 [column_constraint]  -- 注释 
    )

 
|数据类型|	描述|
|-------|-------|
integer(size),int(size),smallint(size),tinyint(size) |	仅容纳整数、在括号内规定数字的最大位数
decimal(size,d),numeric(size,d)	|容纳带有小数的数字、“size” 规定数字的最大位数、“d” 规定小数点右侧的最大位数
char(size)|	容纳固定长度的字符串（可容纳字母、数字以及特殊字符）、在括号中规定字符串的长度
varchar(size)	|容纳可变长度的字符串（可容纳字母、数字以及特殊的字符）、在括号中规定字符串的最大长度
date(yyyymmdd)	|容纳日期
## 列约束
### NOT NULL
该约束规定列中不允许存储 NULL 值，即该列必须有一个确定的值
```
-- 在 `users` 表中添加一个 `age` 列，数据类型为整数，且不允许为空
ALTER TABLE users
ADD age INT NOT NULL;
```
### DEFAULT
为列指定一个默认值，当插入数据时如果没有为该列提供值，那么将使用默认值。
```
-- 在 `users` 表中添加一个 `is_active` 列，数据类型为布尔型，默认值为 true
ALTER TABLE users
ADD is_active BOOLEAN DEFAULT true;
```
### UNIQUE
确保列中的所有值都是唯一的，即不允许出现重复值
```
-- 在 `users` 表中添加一个 `email` 列，数据类型为字符串，且该列的值必须唯一
ALTER TABLE users
ADD email VARCHAR(100) UNIQUE;
```
### CHECK
用于限制列中的值必须满足指定的条件。
```
-- 在 `users` 表中添加一个 `age` 列，数据类型为整数，且年龄必须大于 0
ALTER TABLE users
ADD age INT CHECK (age > 0);
```
### PRIMARY KEY
用于唯一标识表中的每一行记录，它结合了 NOT NULL 和 UNIQUE 的特性，一个表只能有一个主键。
```
-- 在 `users` 表中添加一个 `user_id` 列，数据类型为整数，并将其设置为主键
ALTER TABLE users
ADD user_id INT PRIMARY KEY;
```
### 复合主键
需要多个列的组合才能保证记录的唯一性时，就会使用复合主键        
```
-- 创建一个名为 student_course 的表，包含 Sno、Cno 和 Grade 列，使用 Sno 和 Cno 作为复合主键
CREATE TABLE student_course (
    Sno VARCHAR(20),
    Cno VARCHAR(20),
    Grade DECIMAL(5, 2),
    PRIMARY KEY (Sno, Cno)
);
```
# 修改表
## 添加列
```
alter table table_name add column_name data_type [column_constraint];
-- 示例：在 `users` 表中添加一个 `age` 列，数据类型为整数
ALTER TABLE users
ADD age INT;
```
## 修改列的数据类型
```
MsSql:
alter table table_name modify column_name new_data_type;
SQL Server:
alter table table_name alter column column_name new_data_type;
```
## 修改列名
```
alter table table_name change old_column_name new_column_name data_type;
```
## 删除列
```
alter table table_name drop column column_name;
```
## 添加主键
```
MySQL:
alter table table_name add primary key (clumn_name);
-- 示例：为 `users` 表的 `id` 列添加主键约束
ALTER TABLE users
ADD PRIMARY KEY (id);
SQL Serve:
alter table table_name add constraint constraint_name primary key (column_name);
--constraint_name 是用户为数据库中的约束所赋予的一个唯一标识符。当你在表上定义约束（如主键约束、外键约束、唯一约束、检查约束等）时，数据库系统会为该约束创建一个内部标识，但为了方便管理和引用这些约束，你可以自己为它们指定一个有意义的名称。
-- 示例：为 `customers` 表的 `customer_id` 列添加主键约束
ALTER TABLE customers
ADD CONSTRAINT PK_Customers PRIMARY KEY (customer_id);
```
## 删除主键
```
MySQL:
alter table table_name drop primary key;
SQL Serve:
alter table table_name drop constraint constraint_name;
```
# 删除表
```
drop table [if exists] users;
```
# 插入数据
## 指定列名插入
```
insert into table_name (column1,colunmn2,....)
values (value1,value2,....);
```
## 不指定列名
```
insert into table_name values (value1,value2,...);
-- 值的顺序与表中列的数据一致
```
## 插入多条记录
```
insert into table_name (column1, column2, ...)
values (value1_1, value1_2, ...),
       (value2_1, value2_2, ...),
       ...;
```
## 从其他表插入数据
```
INSERT INTO table_name (column1, column2, ...)
SELECT column1, column2, ...
FROM another_table
[WHERE condition];
```
# 查询数据
## 基本查询
### 查询所有列
```
select * from table_name;
```
### 查询指定列
```
select column1,column2,... from table_name;
```
### 条件查询
```
select column1,column2,... from table_name where condation;
-- condation是bool表达式
```
### 模糊查询
使用 LIKE 关键字进行模糊查询，通常结合通配符使用：      
- %：表示任意数量（包括零个）的任意字符。
- _：表示单个任意字符。
```
-- 例如，查询 employees 表中 first_name 以 J 开头的员工信息：
select * from employees where first_name like 'J%';
```
### 范围查询
- 使用 BETWEEN 关键字
查询某个范围内的数据
```sql
-- 例如，查询 employees 表中 salary 在 5000 到 10000 之间的员工信息：
select * from employees where salary between 5000 and 10000;
```
- 使用 IN 关键字
  查询值在指定列表中的数据
```sql
-- 例如，查询 employees 表中 department_id 为 10、20 或 30 的员工信息
select * from employees where department_id in (10,20,30);
```
### 排序查询
使用 ORDER BY 子句对查询结果进行排序，可以按升序（ASC，默认）或降序（DESC）排列。
```sql
select column1,column2,...
from table_name 
order by column1 [ASC|DESC], column2 [ASC|DESC],...;
```
### 分组查询
使用 GROUP BY 子句对数据进行分组，通常结合聚合函数（如 SUM、AVG、COUNT、MAX、MIN 等）使用。     
|   函数      |  功能     |
|----------|-------|
|SUM |用于计算指定列中所有数值的总和|
|AVG|计算指定列中所有数值的平均值|
|COUNT| 1. 计表中的行数，无论列中是否包含 NULL 值  2.  统计指定列中非 NULL 值的数量   3. 统计指定列中不同非 NULL 值的数量|
|MAX|返回指定列中的最大值。对于数值列，返回最大的数值；对于字符列，返回按字典序排序后的最后一个值；对于日期列，返回最晚的日期。|
|MIN|返回指定列中的最小值。其比较规则与 MAX 函数相反|
```sql
select column1, aggreate_function(column2)
from table_name
group by column1;
--GROUP BY 关键字用于将表中的数据按照 column1 列的值进行分组。具有相同 column1 值的行将被归为一组。在分组之后，聚合函数会分别对每个分组内的 column2 列的值进行计算。
```
### 过滤分组结果
使用 HAVING 子句对分组后的结果进行过滤，HAVING 子句与 WHERE 子句类似，但 HAVING 用于过滤分组后的结果，而 WHERE 用于过滤原始数据。
```sql
-- 例如，查询员工数量大于 5 的部门：
SELECT department_id, COUNT(*) 
FROM employees 
GROUP BY department_id 
HAVING COUNT(*) > 5;
```
### 连接查询
1. 内连接（INNER JOIN） 
返回两个表中匹配的行
   ```sql
--例如，查询 employees 表和 departments 表中匹配的员工信息和部门信息：
SELECT employees.employee_id, employees.first_name, departments.department_name 
FROM employees 
INNER JOIN departments 
ON employees.department_id = departments.department_id;
   ```
2. 左连接（LEFT JOIN）
返回左表中的所有行，以及右表中匹配的行。如果右表中没有匹配的行，则右表的列值为 NULL。
```sql
SELECT employees.employee_id, employees.first_name, departments.department_name 
FROM employees 
LEFT JOIN departments 
ON employees.department_id = departments.department_id;
```
3. 右连接（RIGHT JOIN）
与左连接相反，返回右表中的所有行，以及左表中匹配的行
```
SELECT employees.employee_id, employees.first_name, departments.department_name 
FROM employees 
RIGHT JOIN departments 
ON employees.department_id = departments.department_id;
```
3. 全连接（FULL JOIN）
返回两个表中的所有行，无论是否匹配。如果没有匹配的行，则相应表的列值为 NULL。不过，并非所有数据库都支持 FULL JOIN，例如 MySQL 需要使用 UNION 来模拟。
```sql
-- 在支持 FULL JOIN 的数据库中
SELECT employees.employee_id, employees.first_name, departments.department_name 
FROM employees 
FULL JOIN departments 
ON employees.department_id = departments.department_id;

--My SQL 使用 UNION 模拟全连接

-- 左连接查询
SELECT employees.employee_id, employees.employee_name, departments.department_id, departments.department_name
FROM employees
LEFT JOIN departments ON employees.department_id = departments.department_id

UNION

-- 右连接查询
SELECT employees.employee_id, employees.employee_name, departments.department_id, departments.department_name
FROM employees
RIGHT JOIN departments ON employees.department_id = departments.department_id;
```
### 子查询
在查询中嵌套另一个查询，子查询可以出现在 WHERE 子句、FROM 子句等位置
```sql
-- 例如，查询工资高于平均工资的员工信息
SELECT * 
FROM employees 
WHERE salary > (SELECT AVG(salary) FROM employees);
```

### DISTINCT 关键字
从查询结果中去除重复的行      
```
SELECT DISTINCT column1, column2, ...
FROM table_name;
```  
## UPDATE：更新数据
```
update table_name set column1 = value1, column2 = value2,....
[where condation];
```
## DELETE：删除数据
### 删除表中所有行
```
delete from table_name
```
### 根据条件删除部分行
```sql
delete from table_name
where condation;
```
## TRUNCATE TABLE：清除表数据
直接删除整个数据页，不逐行删除，不会记录详细的事务日志,速度更快     
```
truncate table table_name;
```