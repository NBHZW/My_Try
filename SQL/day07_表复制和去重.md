# 表的复制和去重   --- 7

表的复制也称之 自我复制/ 蠕虫复制

## 复制步骤

### (1)获取要复制的表的结构  创建同结构的 空表

desc dept;  -- 获取要复制的表的相关信息

create table dept2(  -- 创建空表
    deptno int,
    DNAME varchar(14),
    LOC varchar(13)
);

除上述方法外 还可以直接用  CREATE TABLE  新表名字  like  要复制的表的名字  

以达到快速创建结构相同的表



### (2)通过查询要复制的表而产生的临时表 赋值给新表 从而达到拷贝作用

INSERT INTO dept2
(deptno, DNAME, LOC)
SELECT DEPTNO,DNAME,LOC FROM dept; 

## 去重步骤

(1)获取一张和要去重的表A的结构相同的空表B

(2)利用distinct关键字返回的临时表 赋值到B上

(3)直接删除A表 把B表改名为A  或者  清除A表上的数据后 再把B表的值复制到A表上

## 合并查询

将查询语句A的结果 和 查询语句B的结果合并在一起 

方法一:  将查询条件 用逻辑词语 连接起来

方法二:  使用 union all语句(合并两个查询后的表 但是不会自动去重)

A

union all

B;

方法三: 使用 union 语句 (同上 但是会自动去重)

## 外连接

需求来源: 在正常进行多表查询,多表合并的时候,如果表一与表二某些数据对不上,就会导致数据丢失

例如:

![image-20230527094846400](C:\Users\John\AppData\Roaming\Typora\typora-user-images\image-20230527094846400.png)

案例中,因为emp2表中没有部门编号为40的数据,导致最终表中也不存在部门编号为40的,但是如果我需要把部门40显示出来,数据用0或者null,此时就需要用到外连接(即有个表的内容我们需要完全显示)

外连接分为  左外连接(左边表的内容需要完全显示) 和 右外连接(右边表的内容需要完全显示)

语句   

左外连接 

SELECT ....  FROM  表A  LEFT JOIN 表B   ON   同where条件

[表A为左表  它会被完整显示]

右外连接

SELECT.... FROM 表A RIGHT JONIN 表B ON 条件

[表B为右表   它会被完整显示]

![image-20230527095842947](C:\Users\John\AppData\Roaming\Typora\typora-user-images\image-20230527095842947.png) 

这样子就可以看出来  没有员工的部门40 就显示出来了