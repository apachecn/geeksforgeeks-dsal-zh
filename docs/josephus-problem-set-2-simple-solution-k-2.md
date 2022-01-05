# 约瑟夫斯问题|集合 2(k = 2 时的简单解)

> 原文:[https://www . geesforgeks . org/josephus-problem-set-2-simple-solution-k-2/](https://www.geeksforgeeks.org/josephus-problem-set-2-simple-solution-k-2/)

有 n 个人站成一圈等着被处决。计数从圆圈中的某个点开始，并以固定的方向围绕圆圈进行。在每一步中，一定数量的人被跳过，下一个人被执行。消灭围绕着这个圆圈进行(随着被处决的人被除掉，这个圆圈越来越小)，直到最后一个人留下来，他被给予了自由。给定总人数 n 和数字 k，表示 k-1 人被跳过，第 k 人被杀。任务是在最初的圈子里选择一个位置，这样你就是最后一个剩下的人，所以生存下来。
我们在下面的集合 1 中讨论了一个广义解。
[约瑟夫斯问题|集合 1 (A O(n)解)](https://www.geeksforgeeks.org/josephus-problem-set-1-a-on-solution/)
本文讨论了 **k = 2** 时的一种特殊情况

**示例:**

```
Input  : n = 5
Output : The person at position 3 survives
Explanation : Firstly, the person at position 2 is killed, 
then at 4, then at 1 is killed. Finally, the person at 
position 5 is killed. So the person at position 3 survives.

Input  : n = 14
Output : The person at position 13 survives
```

以下是一些有趣的事实。

*   在第一回合中，所有被定位的人都被杀死。
*   第二轮出现了两种情况
    1.  **如果 n 为偶数:**例如 n = 8。第一轮，先杀 2 个，再杀 4 个，再杀 6 个，再杀 8 个。第二轮，我们在第一、二、三、四号位分别有 1、3、5、7 名。
    2.  **如果 n 是奇数:**例如 n = 7。第一轮，先杀 2 个，再杀 4 个，再杀 6 个。第二轮，我们在第 1、2、3 号位分别有 3、5、7 人。

如果 n 为**偶数**，并且一个人在本轮处于 x 位置，则该人在上一轮处于 2x–1 位置。
如果 n 为**奇数**且一个人在本轮处于 x 位置，则该人在前一轮处于 2x + 1 位置。
根据以上事实，我们可以递归定义求幸存者位置的公式。

```
Let f(n) be position of survivor for input n, 
the value of f(n) can be recursively written 
as below.

If n is even
   f(n) = 2f(n/2) - 1
Else
   f(n) = 2f((n-1)/2) + 1
```

上述递归的解是

```
f(n) = 2(n - 2floor(Log<sup>2n)</sup> + 1
     = 2n - 21 + floor(Log<sup>2n)</sup> + 1
```

下面是求上述公式值的实现。

## C++

```
// C/C++ program to find solution of Josephus
// problem when size of step is 2.
#include <stdio.h>

// Returns position of survivor among a circle
// of n persons and every second person being
// killed
int josephus(int n)
{
    // Find value of 2 ^ (1 + floor(Log n))
    // which is a power of 2 whose value
    // is just above n.
    int p = 1;
    while (p <= n)
        p *= 2;

    // Return 2n - 2^(1+floor(Logn)) + 1
    return (2 * n) - p + 1;
}

// Driver Program to test above function
int main()
{
    int n = 16;
    printf("The chosen place is %d", josephus(n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find solution of Josephus
// problem when size of step is 2.
import java.io.*;

class GFG {

    // Returns position of survivor among
    // a circle of n persons and every
    // second person being killed
    static int josephus(int n)
    {

        // Find value of 2 ^ (1 + floor(Log n))
        // which is a power of 2 whose value
        // is just above n.
        int p = 1;
        while (p <= n)
            p *= 2;

        // Return 2n - 2^(1+floor(Logn)) + 1
        return (2 * n) - p + 1;
    }

    // Driver Program to test above function
    public static void main(String[] args)
    {
        int n = 16;

        System.out.println("The chosen place is "
                           + josephus(n));
    }
}

// This Code is Contributed by Anuj_67
```

## 蟒蛇 3

```
# Python3 program to find solution of
# Josephus problem when size of step is 2.

# Returns position of survivor among a
# circle of n persons and every second
# person being killed
def josephus(n):

    # Find value of 2 ^ (1 + floor(Log n))
    # which is a power of 2 whose value
    # is just above n.
    p = 1
    while p <= n:
        p *= 2

    # Return 2n - 2^(1 + floor(Logn)) + 1
    return (2 * n) - p + 1

# Driver Code
n = 16
print ("The chosen place is", josephus(n))

# This code is contributed by Shreyanshi Arun.
```

## C#

```
// C# program to find solution of Josephus
// problem when size of step is 2.
using System;

class GFG {

    // Returns position of survivor among
    // a circle of n persons and every
    // second person being killed
    static int josephus(int n)
    {

        // Find value of 2 ^ (1 + floor(Log n))
        // which is a power of 2 whose value
        // is just above n.
        int p = 1;
        while (p <= n)
            p *= 2;

        // Return 2n - 2^(1+floor(Logn)) + 1
        return (2 * n) - p + 1;
    }

    // Driver Program to test above function
    static void Main()
    {
        int n = 16;

        Console.Write("The chosen place is "
                      + josephus(n));
    }
}

// This Code is Contributed by Anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find solution
// of Josephus problem when
// size of step is 2.

// Returns position of survivor
// among a circle of n persons
// and every second person being
// killed
function josephus($n)
{
    // Find value of 2 ^ (1 + floor(Log n))
    // which is a power of 2 whose value
    // is just above n.
    $p = 1;
    while ($p <= $n)
        $p *= 2;

    // Return 2n - 2^(1+floor(Logn)) + 1
    return (2 * $n) - $p + 1;
}

// Driver Code
$n = 16;
echo "The chosen place is ", josephus($n);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to find solution of Josephus
// problem when size of step is 2.

// Returns position of survivor among
// a circle of n persons and every
// second person being killed
function josephus(n)
{

    // Find value of 2 ^ (1 + floor(Log n))
    // which is a power of 2 whose value
    // is just above n.
    let p = 1;

    while (p <= n)
        p *= 2;

    // Return 2n - 2^(1+floor(Logn)) + 1
    return (2 * n) - p + 1;
}

// Driver code
let n = 16;

document.write("The chosen place is " +
               josephus(n));

// This code is contributed by susmitakundugoaldanga

</script>
```

**Output:** 

```
The chosen place is 1
```

上述解的时间复杂度为 0(对数 n)。
本文由**拉胡尔·贾恩**供稿。

这个问题的另一个有趣的解决方案，当 k=2 时，可以根据观察给出，我们只需要向左旋转 N 的二进制表示，就可以得到所需的答案。考虑到编号为 64 位编号，下面提供了
的工作代码。

下面是上述方法的实现:

## C++

```
// C++ program to find solution of Josephus
// problem when size of step is 2.
#include <bits/stdc++.h>

using namespace std;

// Returns position of survivor among a circle
// of n persons and every second person being
// killed
int josephus(int n)
{
    // An interesting observation is that
    // for every number of power of two
    // answer is 1 always.
    if (!(n & (n - 1)) && n) {
        return 1;
    }

    // The trick is just to right rotate the
    // binary representation of n once.
    // Find whether the number shed off
    // during left shift is set or not

    bitset<64> Arr(n);

    // shifting the bitset Arr
    // f will become true once leftmost
    // set bit is found
    bool f = false;
    for (int i = 63; i >= 0; --i) {
        if (Arr[i] == 1 && !f) {
            f = true;
            Arr[i] = Arr[i - 1];
        }
        if (f) {

            // shifting bits
            Arr[i] = Arr[i - 1];
        }
    }

    Arr[0] = 1;

    int res;

    // changing bitset to int
    res = (int)(Arr.to_ulong());
    return res;
}

// Driver Program to test above function
int main()
{
    int n = 16;
    printf("The chosen place is %d", josephus(n));
    return 0;
}
```

## 蟒蛇 3

```
# Python 3 program to find solution of Josephus
# problem when size of step is 2.

# Returns position of survivor among a circle
# of n persons and every second person being
# killed
def josephus(n):
    # An interesting observation is that
    # for every number of power of two
    # answer is 1 always.
    if (~(n & (n - 1)) and n) :
        return 1

    # The trick is just to right rotate the
    # binary representation of n once.
    # Find whether the number shed off
    # during left shift is set or not

    Arr=list(map(lambda x:int(x),list(bin(n)[2:])))
    Arr=[0]*(64-len(Arr))+Arr

    # shifting the bitset Arr
    # f will become true once leftmost
    # set bit is found
    f = False
    for i in range(63,-1,-1) :
        if (Arr[i] == 1 and not f) :
            f = True
            Arr[i] = Arr[i - 1]

        if (f) :

            # shifting bits
            Arr[i] = Arr[i - 1]

    Arr[0] = 1

    # changing bitset to int
    res = int(''.join(Arr),2)
    return res

# Driver Program to test above function
if __name__ == '__main__':
    n = 16
    print("The chosen place is", josephus(n))
```

**Output:** 

```
The chosen place is 1
```

**时间复杂度:** O(log(n))
**辅助空间:** O(log(n))
这个想法是由 [**Anukul Chand**](https://auth.geeksforgeeks.org/user/Cyberfreak/) 贡献的。
如果你喜欢 GeeksforGeeks，想投稿，也可以用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章，或者把文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。