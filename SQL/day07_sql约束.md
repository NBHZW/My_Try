# MySQL约束---8

约束,确保数据库的数据满足某种规矩(给数据加限制)

##### **一般有五种:**

##### **not null(非空)	;	unique(唯一)	;	check(检查)**

##### **primary kry(主键)	;	foreign key(外键)**

五种主键可以同时加在一个字段上

#### (1) primary key    主键   

#### 加有该约束字段,数据不能重复并且不能为 null 

![image-20230527111813164](C:\Users\John\AppData\Roaming\Typora\typora-user-images\image-20230527111813164.png)

![image-20230527111850395](C:\Users\John\AppData\Roaming\Typora\typora-user-images\image-20230527111850395.png)



要注意的是,一个表中不能有多个主键,但是可以有复合主键

不能有多个主键的意思是:

![image-20230527111922572](C:\Users\John\AppData\Roaming\Typora\typora-user-images\image-20230527111922572.png)

这种形式是不允许的

复合主键是:

![image-20230527112017738](C:\Users\John\AppData\Roaming\Typora\typora-user-images\image-20230527112017738.png)

这种形式是允许的,但是这样子的话就是id和name这一对组成了一个主键,所以要当id和name同时相等的时候才算重复

***用desc可以查看字段是否为主键***

#### (2) not null

不能为null值  

#### (3)unique

唯一 , 即不能重复 ,但是可以为 null

#### (4)foreign key(外键)

用于定义主表和从表之间的关系,外键约束要定义在从表上,主表则必须要有主键约束或者unique约束,定义外键约束后,要求外键列数据必须在主表的主键列存在或者是为null

![image-20230527164420683](C:\Users\John\AppData\Roaming\Typora\typora-user-images\image-20230527164420683.png)

![image-20230527164434455](C:\Users\John\AppData\Roaming\Typora\typora-user-images\image-20230527164434455.png)

员工表和部门表中,部门id是联系的(即 每个员工的部门id对应一个部门表中的部门id)

但是,我们也可以存在就是说乱写部门id(或者说部门id不存在的情况),例如 员工表中我加一个  员工信息并且让他的部门id为 50

但实际上 我的部门一共才4个10,20,30,40  那么说明这个50是不存在的.

那么为了防止这种操作出现,即为了确保这个部门id确实存在而非乱写的,就可以给员工表的部门id字段后面加上外键约束

因为外键约束的存在,我们增删的操作就需要有顺序要求了.

就拿上面员工表和部门表来说,如果我们有新加的员工,我们则首先要去判断其部门编号是否存在,如果不存在,我们要先在部门表中添加对应的编号,然后再到员工表中加入这位员工;同理,如果要删除部门表中的A id,那么我们也需要先把员工表中部门id为A的信息删除,然后再去删部门表中的数据.

语句格式

FOREGN KEY(本表字段名) REFERENCES 主表名字

![image-20230527171536147](C:\Users\John\AppData\Roaming\Typora\typora-user-images\image-20230527171536147.png)

外键的一些细节:

1:外键指向的主表的字段,必须是主键约束或者是 unique约束

2:表的储引擎必须是innodb ,其他的引擎不支持外键

3:外键字段的数据类型和主键字段数据类型必须保持一致,长度可以不同

4:一旦建立了主外键的关系,数据就不能随意删除了

5:外键中对应的值必须在主键中出现(但是如果主键中没有 no null  即允许存在null的时候  可以直接加一个对应的null的数据)

![image-20230527171559846](C:\Users\John\AppData\Roaming\Typora\typora-user-images\image-20230527171559846.png)



#### (5)check约束

check约束是在sql 现在版本才能实现的,他实在5.7版本的时候就出现了 但是不支持语法功能,只具备语法校验功能

而且该约束在其他数据库里面也支持

![image-20230528091004848](C:\Users\John\AppData\Roaming\Typora\typora-user-images\image-20230528091004848.png)

以前不支持的时候,如果条件范围小,我们也可以使用枚举类型来代替(性别只能是男女)

![image-20230528091302291](C:\Users\John\AppData\Roaming\Typora\typora-user-images\image-20230528091302291.png)
