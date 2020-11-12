# Python | 使用字典实现动态规划

> 原文：[https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/](https://www.geeksforgeeks.org/python-implementing-dynamic-programming-using-dictionary/)

[动态规划](http://www.geeksforgeeks.org/dynamic-programming/)是可以用作对[递归](http://www.geeksforgeeks.org/recursion/)进行优化的一种方式。 只要我们看到递归解决方案重复调用相同的输入，就可以使用动态规划对其进行优化。 这个想法只是简单地存储子问题的结果，这样我们以后就不必在需要时重新计算它们。 这种简单的优化降低了从指数到多项式的时间复杂度。 在本文中，已经讨论了使用 python 的[字典](https://www.geeksforgeeks.org/python-dictionary/)来实现动态规划的方法。

为了理解 python 中动态规划的实现，让我们使用[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)问题对其进行可视化。

用数学术语来说，斐波纳契数的顺序由递归关系定义：

```
Fn = Fn-1 + Fn-2

```

具有种子值：

```
F0 = 0 and F1 = 1

```

**示例**：

> **输入**：`N = 9`
>
> **输出**：34
>
> **说明**：
>
> 在斐波那契数列中的第 9 个数字是 34。
> 
> **输入**：`N = 2`
>
> **输出**：1
>
> **说明**：
>
> 在斐波那契数列中的第 2 个数字是 1。

下面是朴素方法的实现：

```
# Function to find nth Fibonacci number
def Fibonacci(n):
# Corner case
if n< 0 :
print ( "Incorrect input" )
# Base case
elif n = = 0 :
return 0
elif n = = 1 :
return 1
]
# Recursive case
else :
return Fibonacci(n - 1 ) + Fibonacci(n - 2 )
print (Fibonacci( 9 ))
```

**输出**：

```
34

```

显然，以上方法具有指数时间复杂度。 为了存储先前计算的结果，让我们使用 python 的[字典](https://www.geeksforgeeks.org/python-dictionary/)类。

**方法**：想法是自定义词典类的`__missing__`方法。 当用户尝试访问不在词典中的键时，将执行此方法。 我们将使用自己的函数定义来重写此方法。

下面是上述方法的实现：

```
# Python program to customize the
# __missing__ method of the
# dictionary class in python
class Fibonacci( dict ):
[
# Function signature of the
# __missing__ function in
# python
def __missing__( self , n):
# Base case
if n< = 1 :
[
# Storing the value in the
# dictionary before returning
self [n] = n
return n
# Storing the value in the dictionary
# before returning the value
val = self [n] = self [n - 1 ] + self [n - 2 ]
return val
if __name__ = = "__main__" :
# Create an instance of the class
Fib = Fibonacci()
N = Fib[ 9 ]
print (N)
```

**输出**：

```
34

```

上述方法也可以通过在 python 中使用[装饰器](https://www.geeksforgeeks.org/decorators-in-python/)来实现。

[装饰器](https://www.geeksforgeeks.org/function-decorators-in-python-set-1-introduction/)是 Python 中非常强大且有用的工具，因为它允许程序员修改函数或类的行为。 装饰器允许我们包装另一个函数以扩展包装函数的行为，而无需对其进行永久性修改。 这里，[注解](https://www.geeksforgeeks.org/memoization-using-decorators-in-python/?ref=rp)用于实现装饰器。

下面是上述方法的实现：

```
# Python program to find the nth Fibonacci
# number with memoization using decorators
from inspect import signature
# Defining a decorator
class memoise( dict ):
# Initializing function
def __init__( self , func):
self .func = func
self .signature = signature(func)
# Missing method to store the
# Fibonacci numbers in a
# Dictionary
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
# number using the above defined
# decorator
@memoise
def Fibonacci(n):
# Corner case
if n< 0 :
print ( "Incorrect input" )
# Base cases
elif n = ] [H TG122] 0 :
return 0
elif n = = 1 :
return 1
# Recursive case
else :
return Fibonacci(n - 1 ) + Fibonacci(n - 2 )
HTG265]
if __name__ = = "__main__" :
print (Fibonacci( 9 ))
```

**输出**：

```
34

```



* * *

* * *



