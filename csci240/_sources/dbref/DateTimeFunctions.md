

# Date and Time Functions



These are examples of date functions.  Note that they can be used in both the **select** and the **where** clauses of the select statement. There are corresponding time functions as well -  [Click Here](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_date-format)



```mysql
drop database if exists zdbTestDates;
create  or replace database zdbTestDates;

drop table if exists tbl_testdates;

create table tbl_testdates(
date1 DATE,
date2 DATE,
misc Varchar(255),
testdates_id int(9) not null auto_increment primary key);


insert into tbl_testdates(date1, date2, Misc)
	values
		('2020-01-31','2020-12-31', "some year"),
		('2021-01-31','2021-12-31', "some year"),
		('2022-01-31','2022-12-31', "some year"),
		('2023-01-31','2023-12-31', "some year"),
		('2024-01-31','2024-12-31', "some year"),
		('2025-01-31','2025-12-31', "some year");
		
		
-- There is a year(), month(), day(), week(), 
-- weekday(), dayname(), datedif(), date_format(), date_add()

-- There are corresponding functions for time.

-- These can be used in the select and/or the the where statement.

Select 	year(date1) as year, 
		month(date1) as month, 
		day(date1) as day, 
		week(date1) as week_number, 
		weekday(date1) as day_number, 
		dayname(date1) as dayname, 
		date_format(date1,'%M %d%, %Y') as dateformat1,  
		date_format(date1,'%m%/%e%/%y') as dateformat2   
    from tbl_testdates
    Where year(date1) > 2023;
	
/*
+------+-------+------+-------------+------------+-----------+------------------+-------------+
| year | month | day  | week_number | day_number | dayname   | dateformat1      | dateformat2 |
+------+-------+------+-------------+------------+-----------+------------------+-------------+
| 2024 |     1 |   31 |           4 |          2 | Wednesday | January 31, 2024 | 01/31/24    |
| 2025 |     1 |   31 |           4 |          4 | Friday    | January 31, 2025 | 01/31/25    |
+------+-------+------+-------------+------------+-----------+------------------+-------------+
2 rows in set (0.003 sec)
*/
```





## Date / Time Format 

| Specifier | Description                                                  |
| --------- | ------------------------------------------------------------ |
| `%a`      | Abbreviated weekday name                (`Sun`..`Sat`)       |
| `%b`      | Abbreviated month name (`Jan`..`Dec`)                        |
| `%c`      | Month, numeric (`0`..`12`)                                   |
| `%D`      | Day of the month with English suffix (`0th`,                `1st`, `2nd`,                `3rd`, …) |
| `%d`      | Day of the month, numeric (`00`..`31`)                       |
| `%e`      | Day of the month, numeric (`0`..`31`)                        |
| `%f`      | Microseconds (`000000`..`999999`)                            |
| `%H`      | Hour (`00`..`23`)                                            |
| `%h`      | Hour (`01`..`12`)                                            |
| `%I`      | Hour (`01`..`12`)                                            |
| `%i`      | Minutes, numeric (`00`..`59`)                                |
| `%j`      | Day of year (`001`..`366`)                                   |
| `%k`      | Hour (`0`..`23`)                                             |
| `%l`      | Hour (`1`..`12`)                                             |
| `%M`      | Month name (`January`..`December`)                           |
| `%m`      | Month, numeric (`00`..`12`)                                  |
| `%p`      | `AM` or `PM`                                                 |
| `%r`      | Time, 12-hour (*`hh:mm:ss`* followed by                `AM` or `PM`) |
| `%S`      | Seconds (`00`..`59`)                                         |
| `%s`      | Seconds (`00`..`59`)                                         |
| `%T`      | Time, 24-hour (*`hh:mm:ss`*)                                 |
| `%U`      | Week (`00`..`53`), where Sunday is the                first day of the week;                [`WEEK()`](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_week) mode 0 |
| `%u`      | Week (`00`..`53`), where Monday is the                first day of the week;                [`WEEK()`](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_week) mode 1 |
| `%V`      | Week (`01`..`53`), where Sunday is the                first day of the week;                [`WEEK()`](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_week) mode 2; used with                `%X` |
| `%v`      | Week (`01`..`53`), where Monday is the                first day of the week;                [`WEEK()`](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_week) mode 3; used with                `%x` |
| `%W`      | Weekday name (`Sunday`..`Saturday`)                          |
| `%w`      | Day of the week                (`0`=Sunday..`6`=Saturday)    |
| `%X`      | Year for the week where Sunday is the first day of the week, numeric,                four digits; used with `%V` |
| `%x`      | Year for the week, where Monday is the first day of the week, numeric,                four digits; used with `%v` |
| `%Y`      | Year, numeric, four digits                                   |
| `%y`      | Year, numeric (two digits)                                   |
| `%%`      | A literal `%` character                                      |
| `%*`x`*`  | *`x`*, for any                “*`x`*” not listed                above |

[https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_date-format](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_date-format)