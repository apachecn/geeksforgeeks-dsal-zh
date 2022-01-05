# 模乘

> 原文:[https://www.geeksforgeeks.org/modular-multiplication/](https://www.geeksforgeeks.org/modular-multiplication/)

下面是模乘的一些有趣的性质

> (a x b) mod m = ((a mod m) x (b mod m)) mod m
> 
> (a x b x c)mod m =((a mod m)x(b mod m)x(c mod m))mod m
> 
> 相同的属性适用于三个以上的数字。

上述公式是以下公式的扩展版本:

**例 1:**
求 15×17×19 除以 7 的余数。
**解:**
15 除以 7，我们得到 1 作为余数。
17 除以 7，我们得到 3 的余数。
19 除以 7，我们得到 5 的余数。
表达式的余数(15×17×19)/7 将等于(1×3×5)/7。
组合余数等于 15/7 的余数，即 1。

**例 2:**
求 1421×1423×1425 除以 12 的余数。
**解:**
将 1421 除以 12，我们得到 5 作为余数。
将 1423 除以 12，我们得到 7 作为余数。
将 1425 除以 12，我们得到 9 作为余数。
Rem[(1421 x 1423 x 1425)/12]= Rem[(5 x 7 x 9)/12]
Rem[(35 x 9)/12]= Rem[(11 x 9)/12]
Rem[99/12]= 3。

**怎么有用？**
如果需要求两个大数相乘的余数，可以避免做大数乘法，在大数乘法会导致溢出的编程中特别有帮助。

**证明:**如果我们对两个数进行证明，那么我们可以很容易地对其进行推广。让我们看看两个数字的证明。

```
Let a % m = r1
and b % m = r2

Then a and b can be written as (using quotient
theorem).  Here q1 is quotient when we divide 
a by m and r1 is remainder. Similar meanings 
are there for q2 and r2
a = m x q1 + r1
b = m x q2 + r2

LHS = (a x b) % m

    = ((m x q1 + r1 ) x (m x q2 + r2) ) % m

    = (m x m x q1 x q2 + 
        m x q1 x r2 + 
        m x q2 x r1 + r1 x r2 ) % m

    = (m x (m x q1 x q2 + q1 x r2 + 
        q2 x r1) + 
        r1 x r2 ) % m

We can eliminate the multiples of m when
we take the mod m.
LHS = (r1 x r2) % m

RHS = (a % m x b % m) % m
    = (r1 x r2) % m

Hence, LHS = RHS
```