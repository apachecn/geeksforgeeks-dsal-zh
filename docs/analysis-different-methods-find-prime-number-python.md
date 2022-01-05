# Python 中不同求素数方法的分析

> 原文:[https://www . geesforgeks . org/analysis-differential-methods-find-质数-python/](https://www.geeksforgeeks.org/analysis-different-methods-find-prime-number-python/)

如果你参加竞争性编程，你可能会熟悉这样一个事实，即与素数相关的问题是问题设置者的选择之一。在这里，我们将讨论如何优化您的函数，该函数在给定的一组范围内检查素数，并且还将计算执行它们的时间。

根据定义，素数是一个只能被自身和 1 整除的正整数。例如:2，3，5，7。但是如果一个数可以分解成更小的数，它就叫做复合数。例如:4=2*2，6=2*3

整数 1 既不是素数，也不是复合数。检查一个数字是质数很容易，但是有效地检查需要一些努力。

**方法 1:**

现在让我们从第一个函数开始，检查一个数，比如 n，是否是质数。在这个方法中，我们将测试从 2 到 n-1 的所有除数。我们将跳过 1 和 n。如果 n 可以被任何除数整除，函数将返回 False，否则返回 True。
以下是该方法中使用的步骤:

1.  如果整数小于或等于 1，则返回 False。
2.  如果给定的数可以被 2 到 n 之间的任何一个数整除，函数将返回 False
3.  否则它将返回真

## 蟒蛇 3

```
# Python Program to find prime numbers in a range
import time
def is_prime(n):
    if n <= 1:
        return False
    for i in range(2,n):
        if n % i == 0:
            return False
    return True

# Driver function
t0 = time.time()
c = 0 #for counting

for n in range(1,100000):
    x = is_prime(n)
    c += x
print("Total prime numbers in range :", c)

t1 = time.time()
print("Time required :", t1 - t0)
```

**输出:**

```
Total prime numbers in range: 9592
Time required: 60.702312707901
```

在上面的代码中，我们检查了从 1 到 100000 的所有数字，不管这些数字是否是质数。它有一个巨大的运行时间，如图所示。跑步大约需要 1 分钟。这是一种简单的方法，但需要花费大量时间来运行。所以，它在竞争性编程中不是首选。

**方法二:**

在这个方法中，我们使用一个简单的技巧，减少我们检查的除数。我们发现有一条细线作为镜子，以相反的顺序显示线下的因式分解和线上的因式分解。将因子分成两半的线是数的平方根线。如果这个数是一个完美的正方形，我们可以把这条线移动 1，如果我们可以得到这条线的整数值。

```
36=1*36          
  =2*18
  =3*12
  =4*9
------------
  =6*6
------------
  =9*4
  =12*3
  =18*2
  =36*1
```

在这个函数中，我们计算一个整数，比如 max_div，它是数字的平方根，并使用 Python 的数学库获得它的 floor 值。在最后一个例子中，我们从 2 迭代到 n-1。但是在这里，我们把除数减少了一半，如图所示。您需要导入数学模块来获得 floor 和 sqrt 函数。
以下是该方法中使用的步骤:

1.  如果整数小于或等于 1，则返回 False。
2.  现在，我们把需要检查的数字减少到给定数字的平方根。
3.  如果给定的数可以被 2 到该数的平方根之间的任何一个数整除，则该函数将返回 False
4.  否则它将返回真

## 蟒蛇 3

```
# Python Program to find prime numbers in a range
import math
import time
def is_prime(n):
    if n <= 1:
        return False

    max_div = math.floor(math.sqrt(n))
    for i in range(2, 1 + max_div):
        if n % i == 0:
            return False
    return True

# Driver function
t0 = time.time()
c = 0 #for counting

for n in range(1,100000):
    x = is_prime(n)
    c += x
print("Total prime numbers in range :", c)

t1 = time.time()
print("Time required :", t1 - t0)
```

**输出:**

```
Total prime numbers in range: 9592
Time required: 0.4116342067718506
```

在上面的代码中，我们检查了从 1 到 100000 的所有数字，不管这些数字是否是质数。与以前的方法相比，它花费的时间相对较少。这是一个有点棘手的方法，但是在代码的运行时有很大的不同。所以，它在竞技编程中更受青睐。

**方法 3:**

现在，我们将优化我们的代码到下一个级别，比以前的方法花费更少的时间。您可能已经注意到，在最后一个示例中，我们迭代了每个偶数，直到达到极限，这是一种浪费。需要注意的是，除了两个以外，所有的偶数都不能是质数。在这个方法中，我们踢出所有的偶数来优化我们的代码，并且只检查奇数除数。
以下是该方法中使用的步骤:

1.  如果整数小于或等于 1，则返回 False。
2.  如果数字等于 2，它将返回真。
3.  如果这个数大于 2 并且能被 2 整除，那么它将返回 False。
4.  现在，我们已经检查了所有的偶数。现在，寻找奇数。
5.  如果给定的数可以被从 3 到平方根的任何一个数整除，跳过所有偶数，函数将返回 False
6.  否则它将返回真

## 蟒蛇 3

```
# Python Program to find prime numbers in a range
import math
import time
def is_prime(n):
    if n <= 1:
        return False
    if n == 2:
        return True
    if n > 2 and n % 2 == 0:
        return False

    max_div = math.floor(math.sqrt(n))
    for i in range(3, 1 + max_div, 2):
        if n % i == 0:
            return False
    return True

# Driver function
t0 = time.time()
c = 0 #for counting

for n in range(1,100000):
    x = is_prime(n)
    c += x
print("Total prime numbers in range :", c)

t1 = time.time()
print("Time required :", t1 - t0)
```

**输出:**

```
Total prime numbers in range: 9592
Time required: 0.23305177688598633
```

在上面的代码中，我们检查了从 1 到 100000 的所有数字，不管这些数字是否是质数。运行该程序所花费的时间比以前的所有方法都要少。这是检查质数最有效、最快的方法。因此，它在竞争性编程中是最受欢迎的。下次在竞争性编程中尝试任何问题时，使用此方法以获得最佳结果。

### **筛选方法:**

此方法打印所有小于或等于给定数字 n 的素数。例如，如果 n 是 10，则输出应为“2，3，5，7”。如果 n 是 20，输出应该是“2，3，5，7，11，13，17，19”。
这种方法被认为是生成所有小于给定数 n 的素数的最有效方法，被认为是生成素数列表的最快方法。这种方法不适合检查特定的数字。这种方法是生成所有素数列表的首选方法。

## 蟒蛇 3

```
# Python Program to find prime numbers in a range
import time
def SieveOfEratosthenes(n):

    # Create a boolean array "prime[0..n]" and
    # initialize all entries it as true. A value
    # in prime[i] will finally be false if i is
    # Not a prime, else true.
    prime = [True for i in range(n+1)]

    p = 2
    while(p * p <= n):

        # If prime[p] is not changed, then it is
       # a prime
        if (prime[p] == True):

            # Update all multiples of p
            for i in range(p * p, n + 1, p):
                prime[i] = False
        p += 1
    c = 0

    # Print all prime numbers
    for p in range(2, n):
        if prime[p]:
            c += 1
    return c

# Driver function
t0 = time.time()
c = SieveOfEratosthenes(100000)
print("Total prime numbers in range:", c)

t1 = time.time()
print("Time required:", t1 - t0)
```

**输出:**

```
Total prime numbers in range: 9592
Time required: 0.0312497615814209
```

**注意:**所有过程所需的时间可能因编译器而异，但不同方法所需的时间顺序将保持不变。

**参考:**

[\ https://www . geeksforgeeks . org/筛埃拉托斯特尼/](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
[【http://en.wikipedia.org/wiki/Sieve_of_Eratosthenes】](http://en.wikipedia.org/wiki/Sieve_of_Eratosthenes)
本文由 [**Rishabh Bansal**](https://www.linkedin.com/in/rishabh-bansal-9b4b71108/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。