# 渐近分析指南

> 原文:[https://www . geesforgeks . org/渐近分析指南/](https://www.geeksforgeeks.org/guidelines-for-asymptotic-analysis/)

在本文中，重点是学习一些有助于确定算法运行时间的规则。

[**渐近分析**](https://www.geeksforgeeks.org/analysis-of-algorithms-set-1-asymptotic-analysis/) 是指用数学计算单位计算任何运算的运行时间。在渐近分析中，根据输入大小(我们不测量实际运行时间)评估算法的性能。还计算了算法占用的时间(或空间)如何随着输入大小而增加。

> (g(n)) = {f(n ),使得 g(n)是在较高的输入大小值 n 下近似 f(n)的曲线}
> 
> 这条曲线叫做 ***渐近曲线*** ，对于这样一条曲线的算法分析叫做**渐近分析**。

[**Loops**](https://www.geeksforgeeks.org/python-for-loops/) **:** 一个循环的运行时间最多是循环内部语句(包括测试)的运行时间乘以迭代次数。

下面是演示上述概念的 python 程序:

## 蟒蛇 3

```
# Python program to implement
# the above concept
# execute n times for in
# range(0.00);

for i in range(0, n):
print ('Current Number:', i, sep = "")
```

```
#constant time 
Total time a constant cx n = cn = O(n).
```

[**嵌套循环**](https://www.geeksforgeeks.org/loops-in-python/) **:** 由内而外分析。总运行时间是所有循环大小的乘积。

下面是一个演示上述概念的 python 程序:

## 蟒蛇 3

```
# Python program to implement
# the above concept
# outer loop executed n times
for i in range(0, n):

    # inner loop executes n times
    for j in range(0, n):
      print("i value % d  and j value % d" % (i, j))
```

```
# constant time 
Total time = C x n x n = cn^2 =0(n²).
```

[**连续语句**](https://www.geeksforgeeks.org/statement-indentation-and-comment-in-python/) **:** 添加每个语句的时间复杂度。

下面是一个演示上述概念的 python 程序:

## 蟒蛇 3

```
# Python program that implements
# the above concept
n = 100

# executes n times
for i in range (0, n):
    print (Current Number: i, sep = "")

    # outer loop executed n times
    for i in range (0, n):

      # inner loop executes n times
      for j in range(0, n):
        print(" i value % d and j value % d"%(i, j))

X
```

```
Total time = co + c1n + c2n^2 = 0(n^2).
```

[**【If-then-else 语句】**](https://www.geeksforgeeks.org/decision-making-c-c-else-nested-else/) **:** 最坏情况运行时间:测试，加上 else 部分的 then 部分中最大的一个。

下面是一个演示上述概念的 python 程序:

## 蟒蛇 3

```
# Python program that implements
# the above concept
if n == I:
  print ("Incorrect Value")
  print (n)

else:
  for i in range(0, n):

    # constant time
    print (CurrNumber:, i, sep = "")
```

```
Total time = co + c1*n = 0(n).
```