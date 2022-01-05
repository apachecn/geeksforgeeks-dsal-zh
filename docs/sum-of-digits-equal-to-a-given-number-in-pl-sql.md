# PL/SQL 中等于给定数字的位数之和

> 原文:[https://www . geesforgeks . org/数字总和等于给定的 pl-sql 中的数字/](https://www.geeksforgeeks.org/sum-of-digits-equal-to-a-given-number-in-pl-sql/)

**先决条件**–[PL/SQL 简介](https://www.geeksforgeeks.org/plsql-introduction/)
在 PL/SQL 中，命令的代码组排列在一个块内。一组相关的声明或语句。在声明部分，我们声明变量，在开始和结束部分之间，我们执行操作。

给定一个数字和范围，任务是显示所有数字总和等于给定数字的数字。
**例:**

> 输入:x = 23
> 输出:599 689 698 779 788 797 869 878 887 896 959 968 977 986 995
> (注:范围- > 1 至 999)
> 
> 输入:x=12
> 输出:39 48 57 66 75 84 93
> (注:范围- > 1 至 100)

**逼近**是取一个数，找出给定范围内所有可能的数，并对该数的所有位数求和，如果位数和等于该数，则打印该数。

下面是它的实现:

```
--Take a number 
--sum all digit of the number 
--if sum digit is 25  
--then display all 
--Declaration block 
DECLARE 
    --declare N variable 
    n NUMBER; 
    --declare B variable 
    m NUMBER; 
    --declare S variable 
    --S initialize with 0 
    s NUMBER := 0; 
BEGIN 
    --Code block  
    --loop run until max 999 to min 1 
    FOR i IN 1..999 LOOP 
        n := i; 

        WHILE n > 0 LOOP 
            --logic of digit sum 
            m := MOD(n, 10); 

            s := s + m; 

            n := Trunc(n / 10); 
        END LOOP; 

        IF s = 25 THEN 
          --digit sum to be same with 25 
          --Display in result 
          dbms_output.Put_line(i 
                               ||' '); 
        END IF; 

        s := 0; 
    END LOOP; 
--end loop 
END; 
--end program 
```

**输出:**

```
799 
889 
898 
979 
988 
997 

```