# 找到给定序列的第 k 个位置元素

> 原文:[https://www . geeksforgeeks . org/find-the-kth-position-element-of-the-给定序列/](https://www.geeksforgeeks.org/find-the-kth-position-element-of-the-given-sequence/)

给定两个整数 **N** 和 **K** ，如果从 **1** 到 **N** 的所有奇数按递增顺序写下，然后从 **1** 到 **N** 的所有偶数按递增顺序写下，那么任务是在 **K <sup>第</sup>个**位置找到元素。
**举例:**

> **输入:** N = 10，K = 3
> **输出:** 5
> 所需顺序为 1、3、5、7、9、2、4、6、8、10。
> **输入:** N = 7，K = 7
> **输出:** 6

**进场:**已知 **N <sup>第</sup>T5】偶数由 **2 * K** 给出， **N <sup>第</sup>T11】奇数由**2 * K–1**给出。但是由于这里偶数写在 **(N + 1) / 2** 奇数之后。因此， **K <sup>th</sup>** 偶数由**2 *(K–(N+1)/2)**给出，奇数将保持与**2 * K–1**
相同，以下是上述方法的实现:**** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the kth number
// from the required sequence
int kthNum(int n, int k)
{

    // Count of odd integers
    // in the sequence
    int a = (n + 1) / 2;

    // kth number is even
    if (k > a)
        return (2 * (k - a));

    // It is odd
    return (2 * k - 1);
}

// Driver code
int main()
{
    int n = 7, k = 7;

    cout << kthNum(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the kth number
// from the required sequence
static int kthNum(int n, int k)
{

    // Count of odd integers
    // in the sequence
    int a = (n + 1) / 2;

    // kth number is even
    if (k > a)
        return (2 * (k - a));

    // It is odd
    return (2 * k - 1);
}

// Driver code
public static void main(String []args)
{
    int n = 7, k = 7;

    System.out.println(kthNum(n, k));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the kth number
# from the required sequence
def kthNum(n, k) :

    # Count of odd integers
    # in the sequence
    a = (n + 1) // 2;

    # kth number is even
    if (k > a) :
        return (2 * (k - a));

    # It is odd
    return (2 * k - 1);

# Driver code
if __name__ == "__main__" :

    n = 7; k = 7;

    print(kthNum(n, k));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the kth number
// from the required sequence
static int kthNum(int n, int k)
{

    // Count of odd integers
    // in the sequence
    int a = (n + 1) / 2;

    // kth number is even
    if (k > a)
        return (2 * (k - a));

    // It is odd
    return (2 * k - 1);
}

// Driver code
public static void Main(String []args)
{
    int n = 7, k = 7;

    Console.WriteLine(kthNum(n, k));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the kth number
// from the required sequence
function kthNum(n, k)
{
    // Count of odd integers
    // in the sequence
    var a = (n + 1) / 2;

    // kth number is even
    if (k > a)
        return (2 * (k - a));

    // It is odd
    return (2 * k - 1);
}

// Driver code
var n = 7, k = 7;
document.write(kthNum(n, k));

</script>
```

**Output:** 

```
6
```

**时间复杂度:** O(1)