# Python | 使用字典

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)

实现动态编程

[动态编程](http://www.geeksforgeeks.org/dynamic-programming/)是可以用作对[递归](http://www.geeksforgeeks.org/recursion/)进行优化的一种方式。 只要我们看到递归解决方案重复调用相同的输入，就可以使用动态编程对其进行优化。 这个想法只是简单地存储子问题的结果，这样我们以后就不必在需要时重新计算它们。 这种简单的优化降低了从指数到多项式的时间复杂度。 在本文中，已经讨论了使用 python 的[字典](https://www.geeksforgeeks.org/python-dictionary/)来实现动态编程的方法。

为了理解 python 中动态编程的实现，让我们使用[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)问题对其进行可视化。

用数学术语来说，斐波纳契数的顺序由递归关系定义：

```
Fn = Fn-1 + Fn-2

```

具有种子值：

```
F0 = 0 and F1 = 1

```

**示例**：

> **输入**：N = 9
> **输出**：34
> **说明**：
> 9 <sup>在斐波那契数列中的第</sup>个数字 是 34。
> 
> **输入**：N = 2
> **输出**：1
> **说明**：
> 2 <sup>和</sup>编号在斐波那契数列中 是 1。

下面是朴素方法的实现：

```
# Function to find nth Fibonacci number

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)
def Fibonacci(n):
# Corner case

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)
if n< 0 :
print ( "Incorrect input" )
# Base case

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)
elif n = = 0 :
return 0
elif n = = 1 :
return 1
]
# Recursive case

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)
else :
return Fibonacci(n - 1 ) + Fibonacci(n - 2 )
print (Fibonacci( 9 ))
```

**Output:**

```
34

```

显然，以上方法具有指数时间复杂度。 为了存储先前计算的结果，让我们使用 python 的[字典](https://www.geeksforgeeks.org/python-dictionary/)类。

**方法**：的想法是自定义词典类的 *__missing__* 方法。 当用户尝试访问不在词典中的键时，将执行此方法。 我们将使用自己的函数定义来重写此方法。

下面是上述方法的实现：

```
# Python program to customize the

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)
# __missing__ method of the

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)
# dictionary class in python

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)
class Fibonacci( dict ):
[
# Function signature of the

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)
# __missing__ function in

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)
# python

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)
def __missing__( self , n):
# Base case

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)
if n< = 1 :
[
# Storing the value in the

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)
# dictionary before returning

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)
self [n] = n
return n
# Storing the value in the dictionary

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)
# before returning the value

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)
val = self [n] = self [n - 1 ] + self [n - 2 ]
return val
if __name__ = = "__main__" :
# Create an instance of the class

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)
Fib = Fibonacci()
N = Fib[ 9 ]
print (N)
```

**Output:**

```
34

```

上述方法也可以通过在 python 中使用[装饰器](https://www.geeksforgeeks.org/decorators-in-python/)来实现。

[Decorator](https://www.geeksforgeeks.org/function-decorators-in-python-set-1-introduction/) 是 Python 中非常强大且有用的工具，因为它允许程序员修改函数或类的行为。 装饰器允许我们包装另一个函数以扩展包装函数的行为，而无需对其进行永久性修改。 这里，[备注](https://www.geeksforgeeks.org/memoization-using-decorators-in-python/?ref=rp)用于实现装饰器。

下面是上述方法的实现：

```
# Python program to find the nth Fibonacci

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)
# number with memoization using decorators

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)
from inspect import signature
# Defining a decorator

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)
class memoise( dict ):
# Initializing function

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)
def __init__( self , func):
self .func = func
self .signature = signature(func)
# Missing method to store the

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)
# Fibonacci numbers in a

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)
# Dictionary

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)
def __missing__( self , key):
(arg, kwarg) = key
self [key] = val = self .func( * arg,
* * dict (kwarg))
return val
def __call__( self , * arg, * * kwarg):
key = self .signature.bind( * arg,
* * kwarg)
return self [key.args,
frozenset (key.kwargs.items())]
[
# Function to find the n-th Fibonacci

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)
# number using the above defined

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)
# decorator

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)
@memoise
def Fibonacci(n):
# Corner case

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)
if n< 0 :
print ( "Incorrect input" )
# Base cases

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)
elif n = ] [H TG122] 0 :
return 0
elif n = = 1 :
return 1
# Recursive case

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)
else :
return Fibonacci(n - 1 ) + Fibonacci(n - 2 )
HTG265]
if __name__ = = "__main__" :
print (Fibonacci( 9 ))
```

**Output:**

```
34

```



* * *

* * *



