# day_08-----8

## 自增长  auto_increment

让表中某个字段在添加数据的时候让该列从1开始,自动增加

***格式***

(一般与主键搭配使用,当然,如果不是主键,则需要给该字段加上union约束使其只有唯一索引)  

(auto_increment的顺序和约束的顺序可以交换)

***字段名 整形(也可以是小数 但是很少很少)  primary key auto_increment***

***字段名 整形  Unique auto_increment***



在创建表的时候  加上  auto_incremen =  x  则可以是该表的自增长从 x 开始

![image-20230528093952173](C:\Users\John\AppData\Roaming\Typora\typora-user-images\image-20230528093952173.png)



自增长字段的添加方法(默认字段一为自增长)

(1)  INSERT INTO 表名字(字段1,字段2....) values(null,值2,值3....)

null值对应字段1  ,  使其从1开始

(2) INSERT INTO 表名字(字段2....) values(值1,值2....)

值1对应给字段2  字段一不需要管 系统被你赋值

(3) INSERT INTO 表名字 values( null , 值1.....)

![image-20230528093554989](C:\Users\John\AppData\Roaming\Typora\typora-user-images\image-20230528093554989.png)

![image-20230528093629459](C:\Users\John\AppData\Roaming\Typora\typora-user-images\image-20230528093629459.png)



如果你在添加数据的时候 , 给自增长的字段进行指定赋值,那么之后的自增长就会以指定值为标准

![image-20230528094528170](C:\Users\John\AppData\Roaming\Typora\typora-user-images\image-20230528094528170.png)

# 索引

面对海量数据,直接查询就会很慢,为了优化查询速度,我们有了索引,

而且索引优化机制很是明显

## 创建索引(注意 同一个字段可以是有多个索引的)

CREATE TNDEX 索引名字  ON 表名字(字段名字)

意思代表:在某表的某个字段上添加索引

注意:索引本身是需要占用内存的,所以创建完索引后表的内存是会变大,典型的空间换时间

## 索引优化机制的原理

不存在索引的时候,数据库的查询方式是全表扫描,即一个一个查找操作,

创建索引后,我们会把要查找的字段,按照中间值为根节点,创建二叉搜索树,所以就加大了查询效率

## 索引优化机制的代价

(1)占用内存

(2)提高了查询操作速度,但是减慢了增删操作的速度

因为创建完索引后,对表中数据进行增删的话,同时也需要对索引创建的二叉查找树进行修改,所以会增加  增删操作的工作量

## 索引类型

1:主键索引   主键约束自动创建为一种索引

可以在创建表的时候就带上主键约束,就算是一种索引了

也可以创建表的时候不带上主键索引,在后边自己加上

CREATE PRIMARY KEY 索引名字 ON 表名字(表中字段名字)

ALTER TABLE 表名字 ADD PRIMARY INDEX 索引名字 (表中字段名字)

2:唯一索引(UNIQUE)   unique约束自动创建成为一种索引

![image-20230528150249815](C:\Users\John\AppData\Roaming\Typora\typora-user-images\image-20230528150249815.png)

3:普通索引(INDEX)     

CREATE INDEX 索引名字  ON  表名字(表中字段名字)

![image-20230528150402624](C:\Users\John\AppData\Roaming\Typora\typora-user-images\image-20230528150402624.png)

ALTER TABLE 表名字 ADD INDEX 索引名字 (表中字段名字)

![image-20230528150642378](C:\Users\John\AppData\Roaming\Typora\typora-user-images\image-20230528150642378.png)

4:全文索引(FULLTEXT)     适用于 MyISAM存储引擎   MySQL中用的较少因为不好   MySQL中我们使用全文索引一般用 全文搜索 Solr 和 ElasticSearch(ES)

## 删除索引

(1) 删除普通索引

DROP INDEX 索引名字 ON 表名字

(2)删除主键索引

ALTER TABLE 表名字 DROP PRIMARY KEY

## 修改索引

并没有直接的修改索引的语句

修改索引的实现靠的是 先删除 再创建

## 查询索引

完整版可以再后面加上  IN  数据库名字

方法一二三都是可以查询到所有索引

方式一:

SHOW INDEX  FROM 表名字

方式二:(一般用于检测索引)

SHOW INDEXES FROM 表名字

方式三:

SHOW KEYS FROM 表名字

方式四:(信息比较少)

DESC 表名字

## 创建索引的一些规则

(1) 较为频繁的作为查找标准的元素建议创建索引

(2)唯一性太差的字段不建议创建索引

(3)更新数据频繁的字段不建议创建索引

(4)不会出现在where语句中的字段不建议创建索引