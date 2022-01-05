# 使用对数的平方根

> 原文:[https://www.geeksforgeeks.org/square-root-number-using-log/](https://www.geeksforgeeks.org/square-root-number-using-log/)

对于给定的数字，用对数函数求平方根。数字可以是整型、浮点型或双精度型。

**示例:**

```
Input  : n = 9
Output : 3

Input  : n = 2.93
Output : 1.711724
```

我们可以用 sqrt()方法求一个数的平方根。

## C++

```
// C++ program to demonstrate finding
// square root of a number using sqrt()
#include<bits/stdc++.h>

int main(void)
{
    double n = 12;
    printf("%lf ", sqrt(n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to demonstrate finding
// square root of a number using sqrt()

import java.io.*;

class GFG {
    public static void main (String[] args) {
    double n = 12;
    System.out.println(Math.sqrt(n));

// This code is contributed by akt_mit
    }
}
```

## 蟒蛇 3

```
# Python3 program to demonstrate finding
# square root of a number using sqrt()
import math

if __name__=='__main__':
    n = 12
    print(math.sqrt(n))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to demonstrate finding
// square root of a number using sqrt()
using System;

class GFG
{
public static void Main()
{
    double n = 12;
    Console.Write(Math.Sqrt(n));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to demonstrate finding
// square root of a number using sqrt()
$n = 12;
echo sqrt($n);

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>

// Javascript program to demonstrate finding
// square root of a number using sqrt()
var n = 12;

document.write(Math.sqrt(n).toFixed(6));

// This code is contributed by aashish1995

</script>
```

**输出:**

```
3.464102 
```

**我们也可以使用 log2()库函数:**求平方根

## C++

```
// C++ program to demonstrate finding
// square root of a number using log2()
#include<bits/stdc++.h>

double squareRoot(double n)
{
    return pow(2, 0.5*log2(n));
}

int main(void)
{
    double n = 12;
    printf("%lf ", squareRoot(n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to demonstrate finding
// square root of a number using log2()
import java.io.*;

class GFG
{
static double squareRoot(double n)
{
    return Math.pow(2, 0.5 * (Math.log(n) /
                              Math.log(2)));
}

// Driver Code
public static void main (String[] args)
{
    double n = 12;
    System.out.println(squareRoot(n));
}
}

// This code is contributed by akt_mit
```

## 计算机编程语言

```
# Python program to demonstrate finding
# square root of a number using sqrt()
import math

# function to return squareroot
def squareRoot(n):

    return pow(2, 0.5 * math.log2(n))

# Driver program

n = 12
print(squareRoot(n))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to demonstrate finding
// square root of a number using log2()
using System;

public class GFG{

static double squareRoot(double n)
{
     return Math.Pow(2, 0.5 * (Math.Log(n) /Math.Log(2)));
}

    static public void Main (){
            double n = 12;
            Console.WriteLine(squareRoot(n));
    }
//This code is contributed by akt_mit   
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to demonstrate finding
// square root of a number using log2()
function squareRoot($n)
{
    return pow(2, 0.5 * log($n, 2));
}

// Driver Code
$n = 12;
echo squareRoot($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript program to demonstrate finding
    // square root of a number using log2()

    function squareRoot(n)
    {
         return Math.pow(2, 0.5 * (Math.log(n) /Math.log(2)));
    }

    let n = 12;
      document.write(squareRoot(n).toFixed(15));

</script>
```

**输出:**

```
3.464101615137755
```

**以上程序是如何工作的？**

```
 let d be our answer for input number n
 then n(1/2) = d 
     apply log2 on both sides
      log2(n(1/2)) = log2(d)
      log2(d) = 1/2 * log2(n)
      d = 2(1/2 * log2(n)) 
      d = pow(2, 0.5*log2(n))  
```

本文由 Jntuh 工程学院[**Tumma Umamaheswararao**](https://www.linkedin.com/in/umamaheswararao-tumma-3a0050130/)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。