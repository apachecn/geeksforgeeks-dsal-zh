# 开门数量| TCS 编码问题

> 原文:[https://www . geesforgeks . org/open-doors-TCS-coding-question/](https://www.geeksforgeeks.org/number-of-open-doors-tcs-coding-question/)

考虑一侧有 **N** 门的长巷子。所有的门最初都是关着的。你在小巷里来回移动，改变门的状态如下:

*   你打开一扇已经关闭的门，你关闭一扇已经打开的门。
*   你从一端开始，继续改变门的状态，直到你到达另一端，然后你回来，再次开始改变门的状态。
*   第一步，你改变编号为 **1，2，3，…，N** 的门的状态。
*   第二次，你改变编号为 **2、4、6、…** 的门的状态。
*   第三次，你改变编号为 **3，6，9 …** 的门的状态。
*   等等…

上述程序将持续到第 **N <sup>次</sup>转弯**时，您将改变编号为 **N** 的门的状态。任务是在程序结束时找到打开的门的数量。

**示例:**

> **输入:**N = 3
> T3】输出: 1
> 
> **输入:**N = 100
> T3】输出: 10

**方法:**给定的问题可以基于以下观察来解决:

*   只有当且仅当某个门具有奇数个因子时，该门才能最终打开，因为每个门都会被其每个[因子](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)访问一次。
*   最初，所有的门都是关闭的，所以如果它有偶数个因子[它将保持关闭，如果它有奇数个因子它将保持打开。](https://www.geeksforgeeks.org/check-if-total-number-of-divisors-are-even-or-odd/)
*   因此，从 **1** 到 **N** 保持打开的门的总数将是具有奇数因子的门的数量。

从以上观察，只有[完美平方](https://www.geeksforgeeks.org/find-number-perfect-squares-two-given-numbers/)的数具有奇数个因子。因此，从 **1** 到 **N** 保持打开的总门数将是 **1** 到 **N** 之间的[完美方块数，而 **1** 到 **N** 之间的完美方块数是 **sqrt(N)** 。](https://www.geeksforgeeks.org/find-number-perfect-squares-two-given-numbers/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function that counts the number of
// doors opens after the Nth turn
int countOpenDoors(int N)
{

    // Find the number of open doors
    int doorsOpen = sqrt(N);

    // Return the resultant count of
    // open doors
    return doorsOpen;
}

// Driver Code
int main()
{

    int N = 100;
    cout << countOpenDoors(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
import java.io.*;

class GFG
{

  // Function that counts the number of
// doors opens after the Nth turn
static int countOpenDoors(int N)
{

    // Find the number of open doors
    int doorsOpen = (int) Math.sqrt(N);

    // Return the resultant count of
    // open doors
    return doorsOpen;
}

// Driver Code
    public static void main (String[] args) {
        int N = 100;
        System.out.println(countOpenDoors(N));

    }
}

 // This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 code for the above approach
import math

# Function that counts the number of
# doors opens after the Nth turn
def countOpenDoors(N):

    # Find the number of open doors
    doorsOpen = int(math.sqrt(N))

    # Return the resultant count of
    # open doors
    return doorsOpen

# Driver Code
if __name__ == '__main__':
    N = 100
    print(countOpenDoors(N))

# This code is contributed by MuskanKalra1
```

## C#

```
using System;

class GFG {

    // Function that counts the number of
    // doors opens after the Nth turn
    static int countOpenDoors(int N)
    {

        // Find the number of open doors
        int doorsOpen = (int)Math.Sqrt(N);

        // Return the resultant count of
        // open doors
        return doorsOpen;
    }

    // Driver Code
    public static void Main()
    {
        int N = 100;
        Console.Write(countOpenDoors(N));
    }
}

// This code is contributed by subhammahato348.
```

## java 描述语言

```
<script>
        // JavaScript program for the above approach

        // Function that counts the number of
        // doors opens after the Nth turn
        function countOpenDoors(N) {

            // Find the number of open doors
            let doorsOpen = parseInt(Math.sqrt(N));

            // Return the resultant count of
            // open doors
            return doorsOpen;
        }

        // Driver Code

        let N = 100;
        document.write(countOpenDoors(N));

    // This code is contributed by Potta Lokesh

    </script>
```

**Output**

```
10
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*