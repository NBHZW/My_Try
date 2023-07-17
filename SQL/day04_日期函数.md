# 日期函数[对应命令操作5]

**简单的查询当前时间  前三句的()可以省略**

CURRENT_DATE(); // 当前日期

CURRENT_TIME();//当前时间

CURRENT_TIMESTAMP();//当前时间戳  包含了年月日时分秒



DATE(datetime);//返回datetime的日期部分    

data部分的日期部分格式应该为  XXXX - XX - XX  写年月日读取不出来





***DATE_ADD(date2,INTERVAL d_value d_type);//在date2中加上日期或者时间***

***DATE_SUB(date2,INTERVAL d_value d_type);//在date2中减去一个时间***

***时间加减中,后面为  INTERVAL +  x  +  时间名词***   

***例如   select DATE_ADD(NOW(),INTERVAL 6 day);  现在的时间加6天***   

***这个x可以是小数  但是整个语句后面只能由一个  INTERVAL***   

***不能   select DATE_ADD(NOW(),INTERVAL 6 day ,INTERVAL 8 hour);***

***也不能select DATE_ADD(NOW(),INTERVAL 6 day , 8 hour);***





DATEDIFF(date1,date2);//两个日期的差(返回天数)

***返回的天数是date1-date2的日期  所以可能出现负数***

***并且完全不会在意时间  所以不会出现小数 返回的就是准确的天数***



TIMEDIFF(date1,date2);//两个时间差(返回多少小时多少分钟多少秒)

***同理  date1减去date2的时间  一样可能出现负数***



NOW();//当前时间



YEAR[Month] (datetime) ;//只读取年份/月份/日

unix_timestamp();   // 返回从1970-1-1到现在的秒数



FROM_UNIXTIME(); // 可以把 一个秒数时间转化成指定格式的时间   可以让我们用一个整数来记录时间 然后通过这个函数进行转化

***eg***

***select FROM_UNIXTIME(unix_timestamp(),'%y-%m-%d %h:%i:%s') FROM dual;***

***,'%y-%m-%d %h:%i:%s'这一段要是不写 默认展示 ,也可以删除一些 输出你想要的部分  %y-%m-%d  这样子就只会输出年月日***