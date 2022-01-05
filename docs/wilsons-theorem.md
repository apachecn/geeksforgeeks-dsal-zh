# 威尔逊定理

> 原文:[https://www.geeksforgeeks.org/wilsons-theorem/](https://www.geeksforgeeks.org/wilsons-theorem/)

威尔逊定理指出自然数 p > 1 是素数的当且仅当

```

    (p - 1) ! ≡  -1   mod p 
OR  (p - 1) ! ≡  (p-1) mod p

```

示例:

```
p  = 5
(p-1)! = 24
24 % 5  = 4

p  = 7
(p-1)! = 6! = 720
720 % 7  = 6

```

**它是如何工作的？**
1)我们可以快速检查 p = 2 或 p = 3 的结果。

2)对于 p > 3:如果 p 是复合的，那么它的正整数除数在整数 1，2，3，4，…，p-1 之间，很明显 gcd((p-1)！，p) > 1，所以我们不能有(p-1)！= -1 (mod p)。

3)现在让我们看看当 p 是素数时，它是如何精确地为-1 的。如果 p 是素数，那么[1，p-1]中的所有数相对于 p 都是素数，并且对于范围[2，p-2]中的每个数 x，必须存在一对 y，使得(x*y)%p = 1。因此

```
    [1 * 2 * 3 * ... (p-1)]%p 
 =  [1 * 1 * 1 ... (p-1)] // Group all x and y in [2..p-2] 
                          // such that (x*y)%p = 1
 = (p-1)
```

**怎么可能有用？**
考虑一个接近输入数的素数模下的阶乘计算问题，即我们要求“n！% p”使得 n < p，p 是素数，n 接近 p 例如(25！% 29).从威尔逊定理，我们知道 28！是-1。所以我们基本上需要求[ (-1) *逆(28，29) *逆(27，29) *逆(26) ] % 29。反函数逆(x，p)返回模 p 下 x 的逆(详见[本](https://www.geeksforgeeks.org/multiplicative-inverse-under-modulo-m/))。

威尔逊定理的更多应用见[本](https://en.wikipedia.org/wiki/Wilson's_theorem#Applications)。

**参考文献:**T2[https://en.wikipedia.org/wiki/Wilson's_theorem](https://en.wikipedia.org/wiki/Wilson's_theorem)T5[https://primes.utm.edu/notes/proofs/Wilsons.html](https://primes.utm.edu/notes/proofs/Wilsons.html)

如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论