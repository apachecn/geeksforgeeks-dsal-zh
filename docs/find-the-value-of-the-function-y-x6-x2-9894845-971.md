# 求函数 Y = (X^6 + X^2 + 9894845) % 971

的值

> 原文:[https://www . geesforgeks . org/find-函数的值-y-x6-x2-9894845-971/](https://www.geeksforgeeks.org/find-the-value-of-the-function-y-x6-x2-9894845-971/)

给定一个函数，对于给定值， **Y = (X^6 + X^2 + 9894845) % 971** 。任务是找到函数的值。
**例:**

```
Input: x = 5
Output: 469

Input: x = 654654
Output: 450
```

**说明:**

> **Y = (X^6 + X^2 + 9894845) % 971。**
> 如果我们分解方程，我们得到**y =(x^6)%971+(x^2)%971+(9894845)% 971**
> ，我们可以将方程简化为**y=(x^6)%971+(x^2)%971+355**。

下面是需要的实现:

## C++

```
// CPP implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// computing (a^b)%c
long long int modpow(long long int base, long long int exp, long long int modulus) {
base %= modulus;
long long int result = 1;
while (exp > 0) {
    if (exp & 1) result = (result * base) % modulus;
    base = (base * base) % modulus;
    exp >>= 1;
}
return result;
}

// Driver code
int main(){
    long long int n = 654654, mod = 971;
    cout<<(((modpow(n, 6, mod)+modpow(n, 2, mod))% mod + 355)% mod);

    return 0;
}
// This code is contributed by Sanjit_Prasad
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

class GFG
{

// computing (a^b)%c
static long modpow(long base, long exp, long modulus)
{
    base %= modulus;
    long result = 1;
    while (exp > 0) {
        if ((exp & 1)>0) result = (result * base) % modulus;
            base = (base * base) % modulus;
            exp >>= 1;
    }
    return result;
}

    public static void main(String[] args)
    {
        long n = 654654;
        long mod = 971;
        System.out.println(((modpow(n, 6, mod)+modpow(n, 2, mod))% mod + 355)% mod);
    }
}
// This code is contributed by mits;
```

## 蟒蛇 3

```
# Python implementation of above approach

n = 654654
mod = 971
print(((pow(n, 6, mod)+pow(n, 2, mod))% mod + 355)% mod)
```

## C#

```
// C# implementation of above approach
using System;
class GFG
{

// computing (a^b)%c
static long modpow(long base1, long exp, long modulus)
{
    base1 %= modulus;
    long result = 1;
    while (exp > 0) {
        if ((exp & 1)>0) result = (result * base1) % modulus;
            base1 = (base1 * base1) % modulus;
            exp >>= 1;
    }
    return result;
}

    public static void Main()
    {
        long n = 654654;
        long mod = 971;
        Console.WriteLine(((modpow(n, 6, mod)+modpow(n, 2, mod))% mod + 355)% mod);
    }
}
// This code is contributed by mits;
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// computing (a^b)%c
function modpow($base, $exp, $modulus)
{
    $base %= $modulus;
    $result = 1;
    while ($exp > 0)
    {
        if ($exp & 1) $result = ($result * $base) %
                                        $modulus;
        $base = ($base * $base) % $modulus;
        $exp >>= 1;
    }
    return $result;
}

// Driver code
$n = 654654;
$mod = 971;
echo (((modpow($n, 6, $mod) +
        modpow($n, 2, $mod)) %
        $mod + 355) % $mod);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of above approach

// computing (a^b)%c
function modpow(base, exp, modulus)
{
    base %= modulus;
    let result = 1;
    while (exp > 0) {
        if ((exp & 1)>0) result = (result * base) % modulus;
            base = (base * base) % modulus;
            exp >>= 1;
    }
    return result;
}

// driver code

     let n = 654654;
        let mod = 971;
        document.write(((modpow(n, 6, mod)+
        modpow(n, 2, mod))% mod + 355)% mod);

</script>
```

**Output:** 

```
450
```