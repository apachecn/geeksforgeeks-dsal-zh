# 合成号码

> 原文:[https://www.geeksforgeeks.org/composite-number/](https://www.geeksforgeeks.org/composite-number/)

一个复合数是一个非[素数](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)的正整数。换句话说，它有一个正除数，而不是一个或它本身。前几个合成数字是 4、6、8、9、10、12、14、15、16、18、20、……

*   每一个大于 1 的整数要么是质数，要么是合数。
*   第一个是一个单位，它既不是质数，也不是合成数。

如何检查一个给定的数是否是复合数？
**例:**

```
Input : n = 21
Output: Yes
The number is a composite number!

Input : n = 11
Output : No
```

想法很简单，我们可以使用以下任何一种方法进行质数检查。我们只需要更改返回语句。返回真改为返回假，反之亦然。

*   [素性测验|第一套(入门和学校方法)](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)
*   [素性检验|集合 2(费马方法)](https://www.geeksforgeeks.org/primality-test-set-2-fermet-method/)
*   [素性检验|集合 3(米勒-拉宾)](https://www.geeksforgeeks.org/primality-test-set-3-miller-rabin/)

下面代码中的优化学校方法讨论。

## C++

```
// A optimized school method based C++ program to check
// if a number is composite.
#include <bits/stdc++.h>
using namespace std;

bool isComposite(int n)
{
    // Corner cases
    if (n <= 1)  return false;
    if (n <= 3)  return false;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n%2 == 0 || n%3 == 0) return true;

    for (int i=5; i*i<=n; i=i+6)
        if (n%i == 0 || n%(i+2) == 0)
           return true;

    return false;
}

// Driver Program to test above function
int main()
{
    isComposite(11)?  cout << " true\n": cout << " false\n";
    isComposite(15)?  cout << " true\n": cout << " false\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/// An optimized method based Java
// program to check if a number
// is Composite or not.
import java.io.*;

class Composite
{
    static boolean isComposite(int n)
    {
        // Corner cases
        if (n <= 1)
        System.out.println("False");

        if (n <= 3)
        System.out.println("False");

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (n % 2 == 0 || n % 3 == 0) return true;

        for (int i = 5; i * i <= n; i = i + 6)
            if (n % i == 0 || n % (i + 2) == 0)
            return true;

        return false;
    }

    // Driver Program to test above function
    public static void main(String args[])
    {
        System.out.println(isComposite(11) ?
                       "true" : "false");

        System.out.println(isComposite(15) ?
                       "true" : "false");
    }
}

// This code is contributed by Anshika Goyal
```

## 蟒蛇 3

```
# A optimized school method based Python program to check
# if a number is composite.

def isComposite(n):

    # Corner cases
    if (n <= 1):
        return False
    if (n <= 3):
        return False

    # This is checked so that we can skip
    # middle five numbers in below loop
    if (n % 2 == 0 or n % 3 == 0):
        return True
    i = 5
    while(i * i <= n):

        if (n % i == 0 or n % (i + 2) == 0):
            return True
        i = i + 6

    return False

# Driver Program to test above function

print("true") if(isComposite(11)) else print("false")
print("true") if(isComposite(15)) else print("false")
# This code is contributed by Anant Agarwal.
```

## C#

```
// A optimized school method based C# program
// to check if a number is composite.
using System;

namespace Composite
{
public class GFG
{    

    public static bool isComposite(int n)
    {

    // Corner cases
    if (n <= 1) return false;
    if (n <= 3) return false;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0) return true;

    for (int i = 5; i * i <= n; i = i + 6)

        if (n % i == 0 || n % (i + 2) == 0)
        return true;

    return false;
    }

    // Driver Code
    public static void Main()
    {

    if(isComposite(11)) Console.WriteLine("true");
    else Console.WriteLine("false");

    if(isComposite(15)) Console.WriteLine("true");
    else Console.WriteLine("false");
    }

}
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A optimized school
// method based PHP
// program to check
// if a number is composite.

function isComposite($n)
{

    // Corner cases
    if ($n <= 1)
        return false;
    if ($n <= 3)
        return false;

    // This is checked so
    // that we can skip
    // middle five numbers
    // in below loop
    if ($n%2 == 0 || $n % 3 == 0)
        return true;

    for ($i = 5; $i * $i <= $n;
                   $i = $i + 6)
        if ($n % $i == 0 || $n % ($i + 2) == 0)
        return true;

    return false;
}

    // Driver Code
    if(isComposite(11))
        echo "true";
        else
        echo "false";
        echo"\n";
    if(isComposite(15))
        echo "true";
        else
        echo "false";
        echo"\n";

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// A optimized school method based Javascript program to check
// if a number is composite.

function isComposite(n)
{
    // Corner cases
    if (n <= 1) return false;
    if (n <= 3) return false;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n%2 == 0 || n%3 == 0) return true;

    for (let i=5; i*i<=n; i=i+6)
        if (n%i == 0 || n%(i+2) == 0)
        return true;

    return false;
}

// Driver Program to test above function

    isComposite(11)? document.write(" true" + "<br>"): document.write(" false" + "<br>");
    isComposite(15)? document.write(" true" + "<br>"): document.write(" false" + "<br>");

// This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
false
true
```

**复合数字编程**

*   [找到一个给定长度的合成数范围](https://www.geeksforgeeks.org/find-range-composite-numbers-given-length/)
*   [生成 n 个连续合成数字的列表(一个有趣的方法)](https://www.geeksforgeeks.org/generate-list-n-consecutive-composite-numbers-interesting-method/)
*   [数组中 k 个最小和 k 个最大合成数的和与积](https://www.geeksforgeeks.org/sum-and-product-of-k-smallest-and-k-largest-composite-numbers-in-the-array/)
*   [数组中所有复合数的乘积](https://www.geeksforgeeks.org/product-of-all-the-composite-numbers-in-an-array/)
*   [数组中复合元素的计数和总和](https://www.geeksforgeeks.org/count-and-sum-of-composite-elements-in-an-array/)
*   [将 n 分为最大合成数](https://www.geeksforgeeks.org/split-n-maximum-composite-numbers/)

**参考:**
https://en.wikipedia.org/wiki/Composite_number
本文由 **Ajay Puri** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。