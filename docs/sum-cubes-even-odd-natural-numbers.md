# 偶数和奇数自然数的立方之和

> 原文:[https://www . geesforgeks . org/sum-cubes-偶数-奇数-自然数/](https://www.geeksforgeeks.org/sum-cubes-even-odd-natural-numbers/)

我们知道[前 n 个自然数](https://www.geeksforgeeks.org/program-cube-sum-first-n-natural-numbers/)的立方之和为= (n(n+1)/2) <sup>2</sup> 。

**前 n 个偶数自然数的立方之和**
2<sup>3</sup>+4<sup>3</sup>+6<sup>3</sup>+……+(2n)<sup>3</sup>

```
Even Sum = 23 + 43 + 63 + .... + (2n)3
        if we multiply by 23 then 
        = 23 x (13 + 23 + 32 + .... + (n)3)
        = 23 + 43 + 63 + ......... + (2n)3
        =  23 (n(n+1)/2)2
        =  8(n(n+1))2/4
        =  2(n(n+1))2

```

**示例:**

```
Sum of cube of first 4 even numbers = 23 + 43 + 63 + 83 
 put n = 4     = 2(n(n+1))2
               = 2*(4*(4+1))2
               = 2(4*5)2
               = 2(20)2
               = 800
 8 + 64 + 256 + 512 = 800

```

[前 n 个偶数立方之和程序](https://www.geeksforgeeks.org/sum-of-cubes-of-first-n-even-numbers/)

**前 n 个奇数自然数的立方之和**
我们需要计算 1<sup>3</sup>+3<sup>3</sup>+5<sup>3</sup>+…。+ (2n-1) <sup>3</sup>

```
OddSum   = (Sum of cubes of all 2n numbers) - (Sum of cubes of first n even numbers)
         =  (2n(2n+1)/2)2 - 2(n(n+1))2 
         =  n2(2n+1)2 - 2* n2(n+1)2
         =  n2[(2n+1)2 - 2*(n+1)2]
         =  n2[4n2 + 1 + 4n - 2n2 - 2 - 4n]
         =  n2(2n2 - 1)

```

**示例:**

```
Sum of cube of first 4 odd numbers = 13 + 33 + 53 + 73 
 put n = 4     = n2(2n2 - 1)
               = 42(2*(4)2 - 1)
               = 16(32-1)
               =  496
 1 + 27 + 125 + 343 = 496

```

[前 n 个奇数立方之和程序](https://www.geeksforgeeks.org/sum-of-cubes-of-first-n-odd-natural-numbers/)