# 使用 Python 中匿名函数的打印能力

> 原文:[https://www . geesforgeks . org/print-power-use-anonymous-in-function-python/](https://www.geeksforgeeks.org/print-powers-using-anonymous-function-in-python/)

**先决条件:** [匿名功能](https://www.geeksforgeeks.org/python-lambda-anonymous-functions-filter-map-reduce/)

在下面的程序中，我们已经在 map()内置函数中使用了匿名(lambda)函数来求 2 的幂。在 Python 中，匿名函数是在没有名称的情况下定义的。
虽然普通函数是使用 def 关键字定义的，但是在 Python 中匿名函数是使用 lambda 关键字定义的。因此，匿名函数也被称为 lambda 函数。
**语法:**

```
lambda arguments: expression
```

Lambda 函数可以有任意数量的参数，但只能有一个表达式。表达式被求值并返回
**示例:**

```
Input : ('The total terms is:', 10)

Output :
('2 raised to power', 0, 'is', 1)
('2 raised to power', 1, 'is', 2)
('2 raised to power', 2, 'is', 4)
('2 raised to power', 3, 'is', 8)
('2 raised to power', 4, 'is', 16)
('2 raised to power', 5, 'is', 32)
('2 raised to power', 6, 'is', 64)
('2 raised to power', 7, 'is', 128)
('2 raised to power', 8, 'is', 256)
('2 raised to power', 9, 'is', 512)

```

```
# Python Program to display the powers 
# of 2 using anonymous function

# Change this value for a different result
terms = 10

# Uncomment to take number of terms from user
# terms = int(input("How many terms? "))

# use anonymous function
result = list(map(lambda x: 2 ** x, range(terms)))

# display the result
print("The total terms is:", terms)
for i in range(terms):
   print("2 raised to power", i, "is", result[i])
```

输出:

```
('The total terms is:', 10)
('2 raised to power', 0, 'is', 1)
('2 raised to power', 1, 'is', 2)
('2 raised to power', 2, 'is', 4)
('2 raised to power', 3, 'is', 8)
('2 raised to power', 4, 'is', 16)
('2 raised to power', 5, 'is', 32)
('2 raised to power', 6, 'is', 64)
('2 raised to power', 7, 'is', 128)
('2 raised to power', 8, 'is', 256)
('2 raised to power', 9, 'is', 512)

```