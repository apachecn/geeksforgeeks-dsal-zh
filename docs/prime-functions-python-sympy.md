# Python 中的素数函数

> 原文:[https://www.geeksforgeeks.org/prime-functions-python-sympy/](https://www.geeksforgeeks.org/prime-functions-python-sympy/)

如何用库函数在 python 中快速获取质数？
库函数总是让我们的代码变得简单，所以在这里我们将讨论 python 中一些处理素数的库函数。 **SymPy** 是一个 python 模块，包含一些非常酷的质数相关库函数。下面列出了这些功能:

1.  **为素数(n):** 测试 n 是否为素数(真)或(假)。
2.  **素数范围(a，b):** 它生成范围[a，b]内所有素数的列表。
3.  **randprime(a，b):** 它返回一个范围[a，b]内的随机素数。
4.  **素数(n):** 返回小于等于 n 的素数个数。
5.  **素数(第 n 个):**它返回第 n 个素数，素数索引为素数(1) = 2。第 n 个素数约为 n*log(n)，永远不能大于 2**n。
6.  **prevprime(n):** 返回小于 n 的 prevprime。
7.  **下一个素数(n):** 它返回下一个大于 n 的素数。
8.  **screen . prime range(a，b):** 它生成范围[a，b]内的所有素数，实现为一个动态增长的厄拉多塞筛。

**例:**

## 蟒蛇 3

```
# Library functions for prime
import sympy

# Output : True
print(sympy.isprime(5))                       

# Output : [2, 3, 5, 7, 11, 13, 17, 19, 23,
# 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71,
# 73, 79, 83, 89, 97]
print(list(sympy.primerange(0, 100)))     

print(sympy.randprime(0, 100))  # Output : 83
print(sympy.randprime(0, 100)) # Output : 41
print(sympy.prime(3))          # Output : 5
print(sympy.prevprime(50))     # Output : 47
print(sympy.nextprime(50))      # Output : 53

# Output : [2, 3, 5, 7, 11, 13, 17, 19, 23, 29,
# 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73,
# 79, 83, 89, 97]
print list(sympy.sieve.primerange(0, 100))
```

**参考:**
[https://stackoverflow . com/questions/13326673/is-a-python-library-to-list-primes](https://stackoverflow.com/questions/13326673/is-there-a-python-library-to-list-primes)
本文由 [**Shashank Mishra(古卢)**](https://auth.geeksforgeeks.org/profile.php?user=Shashank Mishra) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。