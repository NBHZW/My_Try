# 常见的字符串函数

CHARSE(str);  						//返回字串字符集（字符编码格式 eg  UTF-8）

eg: SELECT *CHARSET*(ENAME) FROM emp;





CONCAT(string2[，.......]);    		// 连接字串

eg: select *CONCAT*( ENAME ,' 工作是 ',JOB)FROM emp;   

输出结果就是        ENAME列元素 工作是 对应的JOB 元素   

一般用于  列的拼接    SQL中该句拼接括号内为（str1，str2，str3....）







INSTR(string , substring); 					//返回substring在string中首次出现的位置,没找到则返回0

第一个string可以用表的字段来代替 查询该字段中出现substring的位置

eg： SELECT *INSERT*(JOB,'L')FROM EMP;

***需要注意的是   SQL中数组的索引是从1开始的***





UCASE(string2);   			// 转化为大写

LCASE(string2);  			 // 转化为小写



LEFT(string2,length);		//从string2的左边起取出length个字符

RIGHT(string2,length);		//从string2的右边起取出length个字符





LENGTH(string); 				//返回string的长度     

***注意：按照字节长度来返回 而不是字符个数***





REPLACE(str,search_str,replace_str); // 在str中用replace_str替换search_str





STRCMP(string1,string2); 			//逐字符比较字串大小





SUBSTRING(str,position[,length]);  	 //从str的position位置开始取（length）个字符，默认到字符串最后





LTRIM（string2）			// 去除前端空格

RTRIM(string2)；			 //去除后端空格

TRIM（string2）;			// 去除两端空格

