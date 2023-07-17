# 数学函数



ABS(num);    										//  绝对值

BIN(decimal_number); 						 // 十进制转二进制

CEILING(number2);  							//向上取整 





CONV(number2,from_base,to_base); // 进制转化

***number2是原本的数字  ,  from_base是number2的进制数,to_base是转化后的进制   十六进制的字母要用单引号包起来***





FLOOR(number2); 								 // 向下取整





FORMAT(number,decimal_places);  	 // 保留小数位数

***decimal_places表示保留的小数位数(会四舍五入,也会自动补0)***



HEX( DecimalNumber );  						//转十六进制

LEAST(number,number2,[.......]);   		//求最小值

GREATEST(number,number2,[....]);      //求最大值

MOD(number,denominator); 				//  求余

RAND([seed]);  									//  产生一个范围在0~1的浮点数类型的随机数  如果seed种子值确定,那么产生一个重复序列