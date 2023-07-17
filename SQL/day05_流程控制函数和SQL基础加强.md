# 流程控制函数[对应命令操作6]

IF(expr1,expr2,expr3); 

 // 如果expr1为true,则返回 expr2,否则返回expr3



IFNULL(expr1,expr2);

//如果expr1不为NULL 则返回expr1,否则返回expr2



SELECT CASE WHEN expr1 THEN expr2 [WHEN expr3  THEN expr4.....]   END;

多重控制语句  如果 expr1则返回expr2[ 如果expr3则返回expr4......]



# 基础加强

where语句其实也可以用于比较日期(也就是说  日期可以直接进行比较)

eg

***SELECT ename,HIREDATE FROM  emp where HIREDATE>'1981-03-03';***

***大于也就是时间靠后的    小于就是时间点前的***

***判断是否为空 不能用 = NULL  要用 is NULL***



## 排序加强

ORDER BY 字段名  排序规则  ;  												//可以按照该字段的指定的排序规则进行排序

ORDER BY 字段名1  排序规则1 ,  字段名2  排序规则2; 			// 先按照字段一的排序规则一进行排序,然后在此基础上对字段二进行排序规则二排序



## 分页查询

select......[前面就是正常的查询语句]   limit start ,rows

**// 表示从 start+1行开始 取出  rows行   start一般从0开始的**



## 分组查询增强

eg  案例

-- 分单位编号查询,查询员工个数和没有获得奖金(comm is  null)的人
select DEPTNO,*COUNT*(*),*COUNT*(*IF*(COMM IS NULL ,1,NULL)) FROM emp GROUP BY DEPTNO;

eg  

查询所有的管理者

直接查询count(xxx)只会去除NULL 但是不会去重 导致数据偏多  此时 我们可以  count(distinct xxxx)



# 多子句查询

select语句如果同时包含group by ,  having ,order by,limit 那么他们的执行顺序是:

group by  ,  having  ,  order by ,limit
