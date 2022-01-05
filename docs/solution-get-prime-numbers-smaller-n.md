# 得到所有小于 n 的质数的有趣解法

> 原文:[https://www . geesforgeks . org/solution-get-prime-numbers-small-n/](https://www.geeksforgeeks.org/solution-get-prime-numbers-smaller-n/)

这种方法是基于[威尔逊定理](https://www.geeksforgeeks.org/wilsons-theorem/)并利用阶乘计算可以很容易地用 DP
完成的事实，威尔逊定理说如果一个数 k 是素数，那么((k-1)！+ 1) % k 必须为 0。
下面是该方法的 Python 实现。请注意，该解决方案在 Python 中有效，因为 [Python 默认支持大整数](https://www.geeksforgeeks.org/what-is-maximum-possible-value-of-an-integer-in-python/)，因此可以计算大数的阶乘。

## C++

```
// C++ program to Prints prime numbers smaller than n
#include<bits/stdc++.h>
using namespace std;
void primesInRange(int n)
{
    // Compute factorials and apply Wilson's
    // theorem.
    int fact = 1;
    for(int k=2;k<n;k++){
        fact = fact * (k - 1);
        if ((fact + 1) % k == 0)
            cout<<k<<endl;
            }
}

// Driver code
int main()
{
    int n = 15;
    primesInRange(n);

}
// This code is contributed by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program prints prime numbers smaller than n
class GFG{
static void primesInRange(int n)
{
    // Compute factorials and apply Wilson's
    // theorem.
    int fact = 1;
    for(int k=2;k<n;k++){
        fact = fact * (k - 1);
        if ((fact + 1) % k == 0)
            System.out.println(k);
            }
}

// Driver code
public static void main(String[] args){
int n = 15;
primesInRange(n);
}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to prints prime numbers smaller than n
def primesInRange(n) :

    # Compute factorials and apply Wilson's
    # theorem.
    fact = 1
    for k in range(2, n):
        fact = fact * (k - 1)
        if ((fact + 1) % k == 0):
            print k

# Driver code
n = 15
primesInRange(n)
```

## C#

```
// C# program prints prime numbers smaller than n
class GFG{
static void primesInRange(int n)
{
    // Compute factorials and apply Wilson's
    // theorem.
    int fact = 1;
    for(int k=2;k<n;k++){
        fact = fact * (k - 1);
        if ((fact + 1) % k == 0)
            System.Console.WriteLine(k);
            }
}

// Driver code
static void Main(){
int n = 15;
primesInRange(n);
}
}
// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to prints prime numbers smaller than n
function primesInRange($n)
{
    // Compute factorials and apply Wilson's
    // theorem.
    $fact = 1;
    for($k=2;$k<$n;$k++){
        $fact = $fact * ($k - 1);
        if (($fact + 1) % $k == 0)
            print($k."\n");
            }
}

// Driver code
$n = 15;
primesInRange($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to prints prime numbers smaller than n
function primesInRange(n)
{
    // Compute factorials and apply Wilson's
    // theorem.
    let fact = 1;
    for(let k = 2; k < n; k++){
        fact = fact * (k - 1);
        if ((fact + 1) % k == 0)
            document.write((k + "<br>"));
            }
}

// Driver code
let n = 15;
primesInRange(n);

// This code is contributed by _saurabh_jaiswal
</script>
```

**输出:**

```
2
3
5
7
11
13
```

本文由**巴黎圣慕克吉**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。