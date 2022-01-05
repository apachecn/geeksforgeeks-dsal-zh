# 利用中国剩余定理组合模方程

> 原文:[https://www . geesforgeks . org/using-Chinese-余数-定理-组合-模-方程/](https://www.geeksforgeeks.org/using-chinese-remainder-theorem-combine-modular-equations/)

给定 n 个模方程:
**a≅x<sub>1</sub>mod(m<sub>1</sub>)**
。
。
**a≅x<sub>n</sub>mod(m<sub>n</sub>)**
在方程**a≅xmod(m<sub>1</sub>* m<sub>2</sub>* m<sub>3</sub>中找到 x..*m <sub>n</sub> )**
其中 m <sub>i</sub> 是素数，或者是素数的幂，I 取 1 到 n 的值。

输入以两个数组给出，第一个数组包含每个 x <sub>i</sub> 的值，第二个数组包含每个素数的值集。m <sub>i</sub>
输出一个整数作为最终方程中 x 的值。
**示例:**

```
Consider the two equations
A ≅ 2mod(3)
A ≅ 3mod(5)
Input : 
2 3
3 5
Output : 
8

Consider the four equations,
A ≅ 3mod(4)
A ≅ 4mod(7)
A ≅ 1mod(9) (32)
A ≅ 0mod(11)
Input :
3 4 1 0
4 7 9 11
Output :
1243

```

**说明:**

我们的目标是一次解两个方程。我们把前两个方程结合起来，然后用这个结果和第三个方程结合起来，以此类推。结合两个方程的过程通过参考例 2 解释如下:

1.  ≅ 3mod(4)和≅ 4mod(7)是我们最初得到的两个方程。让结果方程为 a<sub>0</sub>≅x<sub>0</sub>mod(m<sub>1</sub>* m<sub>2</sub>)。
    *   A <sub>0</sub> 由 m<sub>1</sub>' * m<sub>1</sub>* x<sub>0</sub>+m<sub>0</sub>' * m<sub>0</sub>* x<sub>1</sub>T14】给出，其中 m<sub>1</sub>' = m<sub>1</sub>模 m <sub>0</sub> 和 m <sub>0</sub> '的模逆=模逆
    *   我们可以使用扩展欧几里德算法计算模逆。
    *   我们发现 x <sub>0</sub> 为 A<sub>0</sub>mod(m<sub>1</sub>* m<sub>2</sub>
    *   我们得到新的方程是≅11 模(28)，其中 a 是 95
2.  我们现在试着把它和等式 3 结合起来，通过类似的方法，我们得到一个≅ 235mod(252)，其中 A = 2503
3.  最后，结合等式 4，我们得到≅ 1243mod(2772 ),其中 A = 59455，x = 1243

我们观察到 2772 正好等于 4 * 7 * 9 * 11。
我们由此找到了最终方程的 x 值。

你可以参考[扩展欧几里德算法](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/)和[模乘逆](https://www.geeksforgeeks.org/multiplicative-inverse-under-modulo-m/)来获得这些主题的额外信息。

```
# Python 2.x program to combine modular equations
# using Chinese Remainder Theorem

# function that implements Extended euclidean
# algorithm
def extended_euclidean(a, b):
    if a == 0:
        return (b, 0, 1)
    else:
        g, y, x = extended_euclidean(b % a, a)
        return (g, x - (b // a) * y, y)

# modular inverse driver function
def modinv(a, m):
    g, x, y = extended_euclidean(a, m)
    return x % m

# function implementing Chinese remainder theorem
# list m contains all the modulii
# list x contains the remainders of the equations
def crt(m, x):

    # We run this loop while the list of
    # remainders has length greater than 1
    while True:

        # temp1 will contain the new value 
        # of A. which is calculated according 
        # to the equation m1' * m1 * x0 + m0'
        # * m0 * x1
        temp1 = modinv(m[1],m[0]) * x[0] * m[1] + \
                modinv(m[0],m[1]) * x[1] * m[0]

        # temp2 contains the value of the modulus
        # in the new equation, which will be the 
        # product of the modulii of the two
        # equations that we are combining
        temp2 = m[0] * m[1]

        # we then remove the first two elements
        # from the list of remainders, and replace
        # it with the remainder value, which will
        # be temp1 % temp2
        x.remove(x[0])
        x.remove(x[0])
        x = [temp1 % temp2] + x 

        # we then remove the first two values from
        # the list of modulii as we no longer require
        # them and simply replace them with the new 
        # modulii that  we calculated
        m.remove(m[0])
        m.remove(m[0])
        m = [temp2] + m

        # once the list has only one element left,
        # we can break as it will only  contain 
        # the value of our final remainder
        if len(x) == 1:
            break

    # returns the remainder of the final equation
    return x[0]

# driver segment
m = [4, 7, 9, 11]
x = [3, 4, 1, 0]
print crt(m, x)
```

```
Output
1243

```

这个定理和算法有很好的应用。一个非常有用的应用是计算 <sup>n</sup> C <sub>r</sub> % m，其中 m 不是素数，[卢卡斯定理](https://www.geeksforgeeks.org/compute-ncr-p-set-2-lucas-theorem/)不能直接应用。在这种情况下，我们可以计算 m 的素因子，并在我们的 <sup>n</sup> C <sub>r</sub> % m 方程中使用这些素因子作为一个模数，我们可以使用卢卡斯定理来计算，然后使用上面显示的中国剩余定理将得到的方程组合在一起。

本文由 **Deepak Srivatsav** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。