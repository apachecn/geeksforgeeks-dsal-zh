# 在第一个 HEAD 右侧交替位置有 HEAD 的序列数

> 原文:[https://www . geeksforgeeks . org/sequence-number-of-head-在第一个头部的右侧有交替位置的头部/](https://www.geeksforgeeks.org/number-of-sequences-which-has-head-at-alternate-positions-to-the-right-of-the-first-head/)

假设一枚硬币被投掷 N 次。任务是找到投掷序列的总数，这样在从左数第一个头之后，它右边的所有交替位置都只被头占据。除了交替位置之外的位置可以被头部或尾部中的任何一个占据。
比如你抛硬币 10 次(N = 10)，第一个头出现在第 3 个位置，那么右边所有进一步交替的位置都是 5，7，9…

**示例:**

> **输入:** N = 2
> **输出:** 4
> 所有可能的组合都是 TT、TH、HT、HH。
> 
> **输入:** N = 3
> **输出:** 6
> 所有可能的组合将是 TTT、TTH、THT、THH、HTH、HHH。
> 在这种情况下，HHT & HTT 是不可能的，因为在这种组合中
> 交替头的条件不满足。因此，答案将是 6。

**方法:**
如果序列以尾部开始，那么长度为 N-1 的所有可能序列都是有效的。现在，如果序列以头开始，那么序列中的每个奇数索引(假设序列是从 1 开始的)都将是头，剩下的 N/2 个位置可以是头也可以是尾。因此，上述问题的递归公式为:

```
f(N) = f(N-1) + 2floor(N/2)
```

**数学计算:**

```
Let f<sub>o(N)</sub> and f<sub>e(N)</sub> be the functions 
that are defined for the odd and even values of N respectively.

 fo(N) =  fe(N-1) + 2(N-1)/2
 fe(N) =  fo(N-1) + 2N/2

From above equation compute
 fo(N) = fo(N-2) + 2(N-1)/2 + 2(N-1)/2
 fe(N) = fe(N-2) + 2N/2 + 2(N-2)/2

Base Case: 
 fo(1) = 2
 fe(0) = 1

By using the above equation, compute the following results :
 fo(N) - fo(N-2) =  2(N-1)/2 + 2(N-1)/2
 fo(N) - fo(N-2) =  2(N+1)/2 

By taking the sum of above equation for all odd values of N, 
below thing is computed.  
 fo(N) - fo(N-2) + fo(N-1) - fo(N-3) + ...... + fo(3) - fo(1) = 
 22 + 23 + 24 + ..... + 2(N+1)/2

Hence on summation,
fo(N) - fo(1) = SUM[ n = 0 to (N+1)/2 ] 2n - 21 - 20

By using sum of geometric progression
f<sub>o(N) = 2<sup>( N + 1 ) / 2 + 2( N + 1 ) / 2 - 2</sup></sub>

Similarly, find fe(N) :
 fe(N) = fe(N-2) + 2N/2 + 2(N-2)/2
 fe(N) - fe(0) = SUM[ n = 0 to N/2 ] 2n - 20 - SUM[ n = 0 to (N-1)/2 ] 2n

By using sum of geometric progression
f<sub>e(N) = 2 <sup>(N / 2) + 1 + 2 N / 2 - 2</sup></sub>
```

最终公式如下:

> **f(N)= 2<sup>(N+1)/2</sup>+2<sup>(N+1)/2</sup>–2**，如果 N 为奇数
> **f(N)= 2<sup>(N/2)+1</sup>+2<sup>N/2</sup>–2**，如果 N 为偶数

下面是上述方法的实现:

## C++

```
// C++ program to find number of sequences
#include <bits/stdc++.h>
using namespace std;

// function to calculate total sequences possible
int findAllSequence(int N)
{

    // Value of N is even
    if (N % 2 == 0) {
        return pow(2, N / 2 + 1) + pow(2, N / 2) - 2;
    }
    // Value of N is odd
    else {
        return pow(2, (N + 1) / 2) + pow(2, (N + 1) / 2) - 2;
    }
}

// Driver code
int main()
{
    int N = 2;
    cout << findAllSequence(N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// number of sequences
import java.io.*;

class GFG
{

// function to calculate
// total sequences possible
static int findAllSequence(int N)
{

    // Value of N is even
    if (N % 2 == 0)
    {
        return (int)(Math.pow(2, N / 2 + 1) +
                     Math.pow(2, N / 2) - 2);
    }

    // Value of N is odd
    else
    {
        return (int)(Math.pow(2, (N + 1) / 2) +
                     Math.pow(2, (N + 1) / 2) - 2);
    }
}

// Driver code
public static void main (String[] args)
{
    int N = 2;
    System.out.print( findAllSequence(N));
}
}

// This code is contributed
// by anuj_67.
```

## 蟒蛇 3

```
# Python3 program to find number
# of sequences

# function to calculate total
# sequences possible
def findAllSequence(N):

    # Value of N is even
    if (N % 2 == 0):
        return (pow(2, N / 2 + 1) +
                pow(2, N / 2) - 2);
    # Value of N is odd
    else:
        return (pow(2, (N + 1) / 2) +
                pow(2, (N + 1) / 2) - 2);

# Driver code
N = 2;
print(int(findAllSequence(N)));

# This code is contributed by mits
```

## C#

```
// C# program to find
// number of sequences
using System;
public class GFG{

    // function to calculate
    // total sequences possible
    static int findAllSequence(int N)
    {

        // Value of N is even
        if (N % 2 == 0)
        {
            return (int)(Math.Pow(2, N / 2 + 1) +
                         Math.Pow(2, N / 2) - 2);
        }

        // Value of N is odd
        else
        {
            return (int)(Math.Pow(2, (N + 1) / 2) +
                         Math.Pow(2, (N + 1) / 2) - 2);
        }
    }

    // Driver code
    public static void Main ()
    {
        int N = 2;
        Console.WriteLine( findAllSequence(N));
    }
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number of sequences

// function to calculate total
// sequences possible
function findAllSequence($N)
{

    // Value of N is even
    if ($N % 2 == 0)
    {
        return pow(2, $N / 2 + 1) +
               pow(2, $N / 2) - 2;
    }

    // Value of N is odd
    else
    {
        return pow(2, ($N + 1) / 2) +
               pow(2, ($N + 1) / 2) - 2;
    }
}

// Driver code
$N = 2;
echo findAllSequence($N);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
    // Javascript program to find number of sequences

    // function to calculate
    // total sequences possible
    function findAllSequence(N)
    {

        // Value of N is even
        if (N % 2 == 0)
        {
            return (Math.pow(2, N / 2 + 1) +
                         Math.pow(2, N / 2) - 2);
        }

        // Value of N is odd
        else
        {
            return (Math.pow(2, (N + 1) / 2) +
                         Math.pow(2, (N + 1) / 2) - 2);
        }
    }

    let N = 2;
      document.write(findAllSequence(N));

</script>
```

**Output:** 

```
4
```

**时间复杂度** : O(LogN)