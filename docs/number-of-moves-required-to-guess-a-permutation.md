# 猜测排列所需的移动次数。

> 原文:[https://www . geeksforgeeks . org/需要猜测排列的移动次数/](https://www.geeksforgeeks.org/number-of-moves-required-to-guess-a-permutation/)

给定一个整数 **N** ，你需要猜测一个隐藏的排列(从 **1** 到 **N** 的数字，每个数字恰好出现一次)。您可以执行以下操作:

在第一个位置选择一个数字:

*   如果是正确的，你猜下一个位置。
*   如果它是错误的，整个排列重置，你回到猜测第一个位置。

你可以试错得出正确的排列，你也可以用你以前的知识进行下一次猜测。也就是说，如果你正确地知道第一个位置的数字，但第二个位置错了，那么在下一步中，你可以正确地输入第一个位置，然后进入第二个位置。

找出最坏情况下的最小移动次数，以使整个排列正确。

**示例:**

> **输入:** N = 2
> **输出:** 3
> 您选择 2 作为第一个位置，排列重置。
> 第一个位置你选 1，猜对了，现在你要猜第二个位置。
> 你选择 2 作为第二个位置，因为这是你唯一剩下的选择。
> 
> **输入:**N = 3
> T3】输出: 7

**进场:**要想猜对**和**的位置，需要 **(n-i)** 的猜测。对于每一个猜测，你需要合计 **i** 个移动((i-1)个移动来输入你已经知道的正确前缀，而 **1** 个移动来猜测当前的前缀)。在最后一步，你需要更多的移动来进入正确的排列。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns the required moves
int countMoves(int n)
{
    int ct = 0;
    for (int i = 1; i <= n; i++)
        ct += i * (n - i);

    // Final move
    ct += n;
    return ct;
}

// Driver Program to test above function
int main()
{
    int n = 3;
    cout << countMoves(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

import java.io.*;

class GFG {

// Function that returns the required moves
static int countMoves(int n)
{
    int ct = 0;
    for (int i = 1; i <= n; i++)
        ct += i * (n - i);

    // Final move
    ct += n;
    return ct;
}

// Driver Program to test above function

    public static void main (String[] args) {
        int n = 3;
    System.out.println( countMoves(n));
    }
}
// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns the
# required moves
def countMoves(n):

    ct = 0
    for i in range(1, n + 1):
        ct += i * (n - i)

    # Final move
    ct += n
    return ct

# Driver Code
if __name__ == "__main__":
    n = 3
    print(countMoves(n))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# implementation of the approach
using System;
class GFG {

    // Function that returns the required moves
    static int countMoves(int n)
    {
        int ct = 0;
        for (int i = 1; i <= n; i++)
            ct += i * (n - i);

        // Final move
        ct += n;
        return ct;
    }

    // Driver Program to test above function
    static void Main()
    {
        int n = 3;
        Console.WriteLine(countMoves(n));
    }

    // This code is contributed by Ryuga.

}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns the
// required moves
function countMoves($n)
{
    $ct = 0;
    for ($i = 1; $i <= $n; $i++)
        $ct += $i * ($n - $i);

    // Final move
    $ct += $n;
    return $ct;
}

// Driver Code
$n = 3;
echo countMoves($n);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns the required moves
function countMoves(n)
{
    let ct = 0;
    for(let i = 1; i <= n; i++)
        ct += i * (n - i);

    // Final move
    ct += n;
    return ct;
}

// Driver code
let n = 3;

document.write(countMoves(n));

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
7
```