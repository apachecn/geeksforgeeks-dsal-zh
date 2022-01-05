# 计算给定范围内可能出现的不同对的总和

> 原文:[https://www . geesforgeks . org/count-distinct-对之和-给定范围内的可能值/](https://www.geeksforgeeks.org/count-distinct-sum-of-pairs-possible-from-a-given-range/)

给定两个正整数 **L** 和 **R** ( *其中 **L ≤ R*** )，任务是计算从**【L，R】**范围内任意一对整数相加可以得到的不同整数的个数。

**示例:**

> **输入:** L = 3，R = 5
> **输出:** 11
> **解释:**所有可能的不同对和如下:
> 
> 1.  (3, 3).总和= 6。
> 2.  (3, 4).总和= 7。
> 3.  (3, 5).总和= 8。
> 4.  (4, 5).总和= 9。
> 5.  (5, 5).总和= 10。
> 
> 因此，不同和的计数是 5。
> 
> **输入:** L = 12，R = 14
> T3】输出: 5

**天真法:**解决给定问题最简单的方法是从范围**【L，R】**中找出[所有可能的数对之和，并打印得到的所有不同和的计数。](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)

***时间复杂度:**O((L–R)<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以基于以下观察进行优化:

*   既然给定的范围**【L，R】**是连续的，那么相加得到的数的范围也将是连续的。
*   该范围内的最小和最大对数分别由 **2 * L** 和 **2 * R** 给出。
*   因此，对的计数相异和由**(2 * R–2 * L+1)**给出。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count distinct sum of
// pairs possible from the range [L, R]
int distIntegers(int L, int R)
{
    // Return the count of
    // distinct sum of pairs
    return 2 * R - 2 * L + 1;
}

// Driver Code
int main()
{
    int L = 3, R = 8;
    cout << distIntegers(L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to count distinct sum of
// pairs possible from the range [L, R]
static int distIntegers(int L, int R)
{

    // Return the count of
    // distinct sum of pairs
    return 2 * R - 2 * L + 1;
}

// Driver Code
public static void main (String[] args)
{
    int L = 3, R = 8;

    System.out.println(distIntegers(L, R));
}
}

// This code is contributed by rag2127
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count distinct sum of
# pairs possible from the range [L, R]
def distIntegers(L, R):

    # Return the count of
    # distinct sum of pairs
    return 2 * R - 2 * L + 1

# Driver Code
if __name__ == '__main__':
    L, R = 3, 8
    print (distIntegers(L, R))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to count distinct sum of
// pairs possible from the range [L, R]
static int distIntegers(int L, int R)
{

    // Return the count of
    // distinct sum of pairs
    return 2 * R - 2 * L + 1;
}

// Driver Code
static public void Main()
{
    int L = 3, R = 8;

    Console.Write(distIntegers(L, R));
}
}

// This code is contributed by avijitmondal1998
```

## java 描述语言

```
<script>

    // Function to count distinct sum of
    // pairs possible from the range [L, R]
    function distIntegers(L,R)
    {
        // Return the count of
        // distinct sum of pairs
        return 2 * R - 2 * L + 1;
    }

    // Driver Code
    let L = 3, R = 8;
    document.write(distIntegers(L, R));

    // This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
11
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)