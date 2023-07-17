# 一：SQL的通用语法

（1）SQL语句可以写在单行或者多行，以分号作为结束符

（2）SQL语句可使用空格和缩进

（3）MySQL不区分大小写，关键字建议大写

（4）注释：单行注释  ：--或者#（MySQL特有）    多行注释：/*     */

# 二：SQL的分类

## （1）DDL语句   数据定义语言    用来定义数据库对象（数据库，表，字段。。。）

### SQL中的数据类型

![image-20230504205734752](C:\Users\John\AppData\Roaming\Typora\typora-user-images\image-20230504205734752.png)



### DDL基础语句

SHOW DATABASES ;  //查询所有数据库

SELECT DATABASE();   //查询当前数据库



/*

 [ ]里面的内容  可有可无   和日常英语笔记（）差不多滴意思

[IF NOT EXISTS]判断语句			如果不存在创建 否则不操作

 [DEFAULT CHARSET字符集] [COLLATE排序规则]			指定存储字符集和对应的排序规则

*/



CREATE DATABASE [IF NOT EXISTS] 数据库名 [DEFAULT  CHARACTER SET（ CHARACTER SET可以简写为CHARSET）字符集] [COLLATE排序规则];  												 //创建数据库

DROP DATABASE[IF EXISTS]数据库名          			// 删除数据库

SHOW CREATE DATABASE 数据库名						// 查看指定数据库

USE  数据库名           													//  使用数据库

SHOW TABLES;    														//查看当前数据库的所有表  前提是先使用该数据库

DESC 表名字;          													 // 查询表结构

SHOW  CREATE TABLE  表名字 ；     						//查询指定表的建表语句  能查看比上面那句更详细点的表数据

ALTER TABLE 表名字 ADD 字段名 数据类型（长度）[COMMENT '注释'] [约束];  			//给表添加字段

ALTER TABLE 表名字 MODIFY 字段名 新数据类型（长度）;											// 修改表内字段的数据类型

ALTER TABLE 表名字 CHANGE 旧字段名字 新字段名字 数据类型（长度)[COMMENT 注释] [约束];	//修改表内字段的名字和数据类型

ALTER TABLE 表名字 DROP 字段名; 			 				// 删除字段

ALTER TABLE 表名字 RENAME TO 新表名字; 				 // 修改表名字

DROP TABLE [IF EXITS]表名字;										//删除表   完全删除

TRUNCATE TABLE 表名字;												//删除表后创建一个同名的空表



## （2）DML语句  数据操作语言     对数据库表中的数据进行增删操作

CREATE TABLE 表名字（           //     创建/添加表

​			字段一  字段一的类型[COMMENT '字段一注释']**,**

​			字段二  字段二的类型[COMMENT '字段二注释']**,**

​			字段三  字段三的类型[COMMENT '字段三注释']**,**

​			。。。			*//  **除最后一句每一行最后都有一个  逗号***   

）[COMMENT 表注释] ;          

还可以在后面跟CHARACTER SET 字符集    COLLATE  校对规则

engine  储存引擎       field   指定列名      datatype    指定数据类型        







**添加数据  INSERT             修改数据  UPDATA			删除数据  DELETE**



### 添加数据

***特别注意   如果添加的数据属于字符串或者日期 应该包含在单引号内  并且允许插入空值***

INSERT INTO 表名字（字段名一，字段名二,.......） VAULES(值1，值2......); //给指定字段添加数据，值一对应字段一，值二对应字段二，依次类推

INSERT INTO 表名字 VALUES（值一，值二，值三）;									//给所有的字段赋值 同上  值一对应字段一.....

INSERT INTO 表名字（字段名一，字段名二.....）VALUE(值1，值2.....) , (值1，值2.....) , (值1，值2.....)// 批量添加数据  每一个(值1，值2.....)对应给字段名一，字段名2，。。。。  添加数据

INSERT INTO 表名字 VALUE(值1，值2.....) ，(值1，值2.....) ，(值1，值2.....).....		//同上 给全部字段批量对应添加



### 修改数据

UPDATE 表名字 SET 字段名1=值1，字段名2=值2.....[WHERE 条件];***// where 条件是针对于满足特殊条件的数据进行修改  如果没有  则会默认对所有的数据的字段名1的数据进行修改了   并且where后面的条件语句可以加and（和）   or（或）    not/！（非）	xor（异或）来进行多条件的判断***







## （3）DQL语句   数据查询语言     对数据库表中的数据进行查询操作

DELETE  FROM 表明 [WHERE 条件]；//无条件默认删除整张表的所有数据**注意：delete不能删除某一个字段的数值  如果要删除那个数值可以使用update设为null**



## 查询语句：

SELECT [DISTINCT]

​		字段列表

FROM

​		表名列表		//只有这两行的为简单的查询 不带条件

WHERE

​		条件列表  	//带条件的查询

GROUP BY		

​		分组字段列表

HAVING

​		分组后条件列表			//分组查询  结合聚合函数使用  用于分组后的过滤

ORDER BY   						//排序查询

​		排序字段列表

LIMIT									//分夜查询

​	分页参数



### 普通查询

SELECT  字段名1，字段名2.。。 FROM 表名字;//查询一个或多个字段

***普通查询的字段名可以用算术组合来协助计算   例如目前有一个表table记录班上所有人的单科成绩***

***select   name  ， （数学+语文+英语）   from  table***    

***这样子打印出来的就是名字 以及 三课成绩总共和***



SELECT *FROM 表名字  //  查询返回表中所有的数据

SELECT 字段1[AS 别名],字段2[AS 别名2].....FROM 表名字;//设置别名  提高返回数据的可读性

SELECT DISTINCT 字段列表 FROM 表名字;// 对查询的数据进行去重





### 条件查询

where 后面的条件可通过逻辑词来连接

除了其他语言中共有的逻辑词&  |这些之外  还有一些特殊的

&&可以用and  				||可以用  or						！可以用not

is  null  判断是否为空			in（......）括号内的数据都可以	 != 可以用  <>   

between a and b 范围在a到b之间  包含边界并且要注意a为最小值不要和b换位置了

like 占位符         模糊匹配（_匹配单个字符，%匹配任意字符）  

%x 表示   满足最后为x   的字符/内容

 ***用于查找名字为两个字，id为两位数等类似需求时可以使用***



### 分组查询

#### 聚合函数        

将一列数据作为一个整体  进行纵向计算

**常见的聚合函数**

count				统计数量，可以count(字段)    也可以count (*)		max				最大值		min				最小值

avg				 平均值			sum				求和

**语法**			SELECT 聚合函数名（字段列表） FROM 表名字



***count()的括号里面可以使用条件语句 详情看 加强和命令操作6***



聚合函数可以同时对多个字段使用

select sum(A),sum(B) FROM 表名字 ；      //  分别查询A,B的各个的综合

select  sum(A+B)  FROM 表名字 ;   			// 查询A,B两者的总和



***count(\**) 返回满足条件的记录的所有行数  哪怕这一行中某个字段的属性为NULL也会计算在内*** 

***count(字段)  返回满足该条件的某字段有多少个  如果该字段在某一项中为NULL  将不会计入***

***注意  所有的null不参与聚合函数***

#### 分组查询

语法：SELECT  字段列表 FROM 表名字  [WHERE 条件]  GROUP BY 分组字段名 [HAVING 分组后过滤的条件]

where的条件是对分组前的数据进行判断作用   having是对分组后的数据进行判断作用

where不能对聚合函数进行判断   但是  having可以

***eg:***

***select  gender,avg(age) from table group by gender;从table表中按照性别分组，查询性别和年龄的平均值***

***select  *from table where age<45 group by workplace; 从table中按照工作地点分组，查询年龄小于45的员工的所有数据***

***select  *from table where age<45 group by workplace  having  count( * )>10;从table中按照工作地点分组并且每组人数大于10人，查询年龄小于45的员工的所有数据***



***注意：如果在有group by操作中，select后面接的结果集字段只有两种：要么就只有group by后出现的字段，要么就是group by后出现的字段＋聚合函数的组合***

***HAVING 后面的条件语句必须是相关数据的聚合函数形式或者该数据在order by 中被提及***



### 排列查询

SELECT 字段一，字段二，字段三。。。。FROM 表名字  ORDER BY  字段名x    asc/desc  ；//按照字段名x的  asc规则（升序，也是默认的规则）/desc规则（降序）  进行查找 

## （4）DCL语句   数据控制语言     创建用户和操作用户权限

## （5）数据库和表备份和恢复

### 数据库和表的备份

数据库备份指令其实存在mysql安装路径的bin文件中

mysqldump -u 用户名 -p -B 数据库1 数据库2  数据库n >文件名.sql（文件名前面要加磁盘位置  说白了就是备份保存的文件地址）



表的备份

mysqldump -u 用户名 -p 密码 数据库 表1 表2 表n >  备份保存的文件地址

### 数据库的恢复

Source 文件名.sql（这个文件名就是保存备份的文件）