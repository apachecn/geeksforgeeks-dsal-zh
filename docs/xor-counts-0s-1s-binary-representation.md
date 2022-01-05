# 二进制表示中 0 和 1 的异或计数

> 原文:[https://www . geesforgeks . org/xor-counts-0s-1s-二进制表示/](https://www.geeksforgeeks.org/xor-counts-0s-1s-binary-representation/)

给定一个数，任务是在给定数的二进制表示中求 0 计数和 1 计数的异或。
**例:**

```
Input  : 5
Output : 3
Binary representation : 101
Count of 0s = 1, 
Count of 1s = 2
1 XOR 2 = 3.

Input  : 7
Output : 3
Binary representation : 111
Count of 0s = 0
Count of 1s = 3
0 XOR 3 = 3.
```

想法很简单，我们遍历一个数的所有位，计数 0 和 1，最后返回两个计数的异或。

## C++

```
// C++ program to find XOR of counts 0s and 1s in
// binary representation of n.
#include<iostream>
using namespace std;

// Returns XOR of counts 0s and 1s in
// binary representation of n.
int countXOR(int n)
{
    int count0 = 0, count1 = 0;
    while (n)
    {
        //calculating count of zeros and ones
        (n % 2 == 0) ? count0++ :count1++;
        n /= 2;
    }
    return (count0 ^ count1);
}

// Driver Program
int main()
{
    int n = 31;
    cout << countXOR (n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find XOR of counts 0s
// and 1s in binary representation of n.

class GFG {

    // Returns XOR of counts 0s and 1s
    // in binary representation of n.
    static int countXOR(int n)
    {
        int count0 = 0, count1 = 0;
        while (n != 0)
        {
            //calculating count of zeros and ones
            if(n % 2 == 0)
            count0++ ;
            else
            count1++;
            n /= 2;
        }
        return (count0 ^ count1);
    }

    // Driver Program
    public static void main(String[] args)
    {
        int n = 31;
        System.out.println(countXOR (n));
    }
}

// This code is contributed by prerna saini
```

## 蟒蛇 3

```
# Python3 program to find XOR of counts 0s
# and 1s in binary representation of n.

# Returns XOR of counts 0s and 1s
# in binary representation of n.
def countXOR(n):

    count0, count1 = 0, 0
    while (n != 0):

        # calculating count of zeros and ones
        if(n % 2 == 0):
            count0 += 1
        else:
            count1 += 1
        n //= 2

    return (count0 ^ count1)

# Driver Code
n = 31
print(countXOR(n))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to find XOR of counts 0s
// and 1s in binary representation of n.
using System;

class GFG {

    // Returns XOR of counts 0s and 1s
    // in binary representation of n.
    static int countXOR(int n)
    {
        int count0 = 0, count1 = 0;
        while (n != 0)
        {

            // calculating count of zeros
            // and ones
            if(n % 2 == 0)
                count0++ ;
            else
                count1++;

            n /= 2;
        }

        return (count0 ^ count1);
    }

    // Driver Program
    public static void Main()
    {

        int n = 31;

        Console.WriteLine(countXOR (n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?PHP
// PHP program to find XOR of
// counts 0s and 1s in binary
// representation of n.

// Returns XOR of counts 0s and 1s
// in binary representation of n.
function countXOR($n)
{
    $count0 = 0;
    $count1 = 0;
    while ($n)
    {
        // calculating count of
        // zeros and ones
        ($n % 2 == 0) ? $count0++ :$count1++;
        $n = intval($n / 2);
    }
    return ($count0 ^ $count1);
}

// Driver Code
$n = 31;
echo countXOR ($n);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript program to find XOR of counts 0s
// and 1s in binary representation of n.

    // Returns XOR of counts 0s and 1s
    // in binary representation of n.
    function  countXOR(n)
    {
        let count0 = 0, count1 = 0;
        while (n != 0)
        {
            //calculating count of zeros and ones
            if(n % 2 == 0)
            count0++ ;
            else
            count1++;
            n = Math.floor(n/2);
        }
        return (count0 ^ count1);
    }

    // Driver Program
    let n = 31;
    document.write(countXOR (n));

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
5
```

**时间复杂度** : O(log(N))
**辅助空间** : O(1)

一个观察是，对于形式为**2^x-1**的数，输出总是 x。我们可以通过首先检查 n+1 是否为 2 的[次方](https://www.geeksforgeeks.org/write-one-line-c-function-to-find-whether-a-no-is-power-of-two/)来直接产生这种情况的答案。

本文由[**Shivam Pradhan(anuj _ charm)**](https://www.facebook.com/anuj.charm)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。