# 以 2

的完美幂跳跃到达第 n 级楼梯的最小步数

> 原文:[https://www . geeksforgeeks . org/到达第 n 级阶梯跳跃的最小步数-2 的完美幂/](https://www.geeksforgeeks.org/minimum-steps-to-reach-the-nth-stair-in-jumps-of-perfect-power-of-2/)

给定 **N** 级楼梯，任务是找到 **2** 到达**第 N**级楼梯所需的完美力量的最小跳跃次数。

**示例:**

> **输入:** N = 5
> **输出:**
> **解释:**
> 我们可以从 **0- > 4- > 5 进行跳跃。**
> 所以最小跳跃要求是 2。
> 
> **输入:** N = 23
> **输出:** 4
> **解释:**
> 我们可以从**0->1->3->7->23**进行跳转。
> 所以需要的最小跳跃是 4。

**第一次进场:**因为跳跃需要 2 的完美幂。因此，给定数量 **N** 中设定位的[计数是达到**N**级所需的最小跳跃次数，作为所有设定位**索引 i** 的**2<sup>I</sup>T11】的总和等于 **N** 。**](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include "bits/stdc++.h"
using namespace std;

// Function to count the number of jumps
// required to reach Nth stairs.
int stepRequired(int N)
{

    int cnt = 0;

    // Till N becomes 0
    while (N) {

        // Removes the set bits from
        // the right to left
        N = N & (N - 1);
        cnt++;
    }

    return cnt;
}

// Driver Code
int main()
{

    // Number of stairs
    int N = 23;

    // Function Call
    cout << stepRequired(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG{

// Function to count the number of jumps
// required to reach Nth stairs.
static int stepRequired(int N)
{

    int cnt = 0;

    // Till N becomes 0
    while (N > 0) {

        // Removes the set bits from
        // the right to left
        N = N & (N - 1);
        cnt++;
    }

    return cnt;
}

// Driver Code
public static void main(String[] args)
{

    // Number of stairs
    int N = 23;

    // Function Call
    System.out.print(stepRequired(N));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of jumps
# required to reach Nth stairs.
def stepRequired(N):

    cnt = 0;

    # Till N becomes 0
    while (N > 0):

        # Removes the set bits from
        # the right to left
        N = N & (N - 1);
        cnt += 1;
    return cnt;

# Driver Code
if __name__ == '__main__':

    # Number of stairs
    N = 23;

    # Function Call
    print(stepRequired(N));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count the number of
// jumps required to reach Nth stairs.
static int stepRequired(int N)
{
    int cnt = 0;

    // Till N becomes 0
    while (N > 0)
    {

        // Removes the set bits from
        // the right to left
        N = N & (N - 1);
        cnt++;
    }

    return cnt;
}

// Driver Code
public static void Main(String[] args)
{

    // Number of stairs
    int N = 23;

    // Function Call
    Console.Write(stepRequired(N));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count the number of jumps
// required to reach Nth stairs.
function stepRequired(N)
{
    let cnt = 0;

    // Till N becomes 0
    while (N)
    {

        // Removes the set bits from
        // the right to left
        N = N & (N - 1);
        cnt++;
    }

    return cnt;
}

// Driver Code

// Number of stairs
let N = 23;

// Function Call
document.write(stepRequired(N));

// This code is contributed by Surbhi Tyagi

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(log N)*
T5】辅助空间: O(1)

**第二次进场:**因为跳跃需要在 **2** 的完全功率下。我们可以观察到 **log2** 函数给出了 **2** 的最高完美幂，如果把它打造成一个整数，可以达到不到 N。所以我们可以从 **N** 中每次减去**幂(2，(int)log2(N))** ，直到其值大于 **0** ，同时递增 **cnt** 。

## C++14

```
#include <bits/stdc++.h>

using namespace std;

int stepRequired(int& N)
{

    int cnt = 0;

    //until N is reached
    while(N>0)
    {
        //subtract highest perfect power of 2 we can reach from previous level
        N-=pow(2,(int)log2(N));

        //increment cnt for total number of steps taken
        cnt++;
    }
    return cnt;
}

int main()
{

    // Number of stairs
    int N = 23;

    // Function Call
    cout << stepRequired(N);
    return 0;
}
```

**时间复杂度:** O(对数 N)

**辅助空间:** O(1)