# 增加和减少数组以达到 0 或 N 的最小步长

> 原文:[https://www . geesforgeks . org/递增和递减数组到达非 0 即 n 的最小步数/](https://www.geeksforgeeks.org/minimum-steps-for-increasing-and-decreasing-array-to-reach-either-0-or-n/)

给定一个整数 **N** 和两个数组**递增[]** 和**递减[]** ，这样它们只有从 **1 到 N** 的元素。任务是为两个阵列的每个元素找到最小步数，以达到 **0** 或 **N.** 一步定义如下:

*   在一个步骤中，**递增【】**数组的所有元素增加 1，**递减【】**数组的所有元素减少 1。
*   当一个元素变为 **0** 或 **N 时，**不再对其执行增加或减少操作。

**示例:**

> **输入:** N = 5，递增[] = {1，2}，递减[] = {3，4}
> **输出:** 4
> **说明:**
> 第一步:递增[]数组变成{2，3}，递减[] = {2，3}
> 第二步:递增[]数组变成{3，4}，递减[] = {1，2}
> 第三步:递增[]数组变成{4，5}，递减[] = {0，1 }
> 
> **输入:** N = 7，增加[] = {3，5}，减少[]= { 6 }
> T3】输出: 6

**方法:**思路是找到**递增【】**阵**T5】和**递减【】T7】阵所有元素所需步数的最大值，分别达到 **N** 和 **0** 。以下是步骤:****

1.  找到[数组的最小元素](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/) **递增[]** 。
2.  **递增[]** 阵的所有元素到达 **N** 的最大步数由*T5】N–T7】min(递增[])T9】给出。*
3.  找到[阵的最大元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) **递减[]** 。
4.  **递减[]** 阵所有元素到达 **0** 的最大步数由 ***max(递减[])*** 给出。
5.  因此，当所有元素变为 **0** 或 **N** 时的最小步数由*T5】max(N–**min(递增[])、max(递减[])*****给出。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that finds the minimum
// steps to reach either 0 or N for
// given increasing and decreasing
// arrays
void minSteps(int N, int increasing[],
              int decreasing[], int m1, int m2)
{

    // Initialize variable to
    // find the minimum element
    int mini = INT_MAX;

    // Find minimum element in
    // increasing[] array
    for(int i = 0; i < m1; i++)
    {
        if (mini > increasing[i])
            mini = increasing[i];
    }

    // Initialize variable to
    // find the maximum element
    int maxi = INT_MIN;

    // Find maximum element in
    // decreasing[] array
    for(int i = 0; i < m2; i++)
    {
        if (maxi < decreasing[i])
            maxi = decreasing[i];
    }

    // Find the minimum steps
    int minSteps = max(maxi,
                       N - mini);

    // Print the minimum steps
    cout << minSteps << endl;
}

// Driver code
int main()
{

    // Given N
    int N = 7;

    // Given increasing
    // and decreasing array
    int increasing[] = { 3, 5 };
    int decreasing[] = { 6 };

    // Find length of arrays
    // increasing and decreasing
    int m1 = sizeof(increasing) /sizeof(increasing[0]);
    int m2 = sizeof(decreasing) / sizeof(decreasing[0]);

    // Function call
    minSteps(N, increasing, decreasing, m1, m2);
}

// This code is contributed by Manne Sree Charan
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

public class GFG {

    // Function that finds the minimum
    // steps to reach either 0 or N for
    // given increasing and decreasing
    // arrays
    public static void
    minSteps(int N, int[] increasing,
            int[] decreasing)
    {

        // Initialize variable to
        // find the minimum element
        int min = Integer.MAX_VALUE;

        // Find minimum element in
        // increasing[] array
        for (int i : increasing) {
            if (min > i)
                min = i;
        }

        // Initialize variable to
        // find the maximum element
        int max = Integer.MIN_VALUE;

        // Find maximum element in
        // decreasing[] array
        for (int i : decreasing) {
            if (max < i)
                max = i;
        }

        // Find the minimum steps
        int minSteps = Math.max(max,
                                N - min);

        // Print the minimum steps
        System.out.println(minSteps);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given N
        int N = 7;

        // Given increasing
        // and decreasing array
        int increasing[] = { 3, 5 };
        int decreasing[] = { 6 };

        // Function call
        minSteps(N, increasing, decreasing);
    }
}
```

## 蟒蛇 3

```
# Python3 program for
# the above approach
import sys

# Function that finds the minimum
# steps to reach either 0 or N for
# given increasing and decreasing
# arrays
def minSteps(N, increasing, decreasing):
    # Initialize variable to
    # find the minimum element
    Min = sys.maxsize;

    # Find minimum element in
    # increasing array
    for i in increasing:
        if (Min > i):
            Min = i;

    # Initialize variable to
    # find the maximum element
    Max = -sys.maxsize;

    # Find maximum element in
    # decreasing array
    for i in decreasing:
        if (Max < i):
            Max = i;

    # Find the minimum steps
    minSteps = max(Max, N - Min);

    # Prthe minimum steps
    print(minSteps);

# Driver Code
if __name__ == '__main__':

    # Given N
    N = 7;

    # Given increasing
    # and decreasing array
    increasing = [3, 5];
    decreasing = [6];

    # Function call
    minSteps(N, increasing, decreasing);

# This code contributed by Rajput-Ji
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function that finds the minimum
// steps to reach either 0 or N for
// given increasing and decreasing
// arrays
public static void minSteps(int N, int[] increasing,
                                   int[] decreasing)
{

    // Initialize variable to
    // find the minimum element
    int min = int.MaxValue;

    // Find minimum element in
    // increasing[] array
    foreach(int i in increasing)
    {
        if (min > i)
            min = i;
    }

    // Initialize variable to
    // find the maximum element
    int max = int.MinValue;

    // Find maximum element in
    // decreasing[] array
    foreach(int i in decreasing)
    {
        if (max < i)
            max = i;
    }

    // Find the minimum steps
    int minSteps = Math.Max(max,
                            N - min);

    // Print the minimum steps
    Console.WriteLine(minSteps);
}

// Driver Code
public static void Main(String[] args)
{

    // Given N
    int N = 7;

    // Given increasing
    // and decreasing array
    int []increasing = { 3, 5 };
    int []decreasing = { 6 };

    // Function call
    minSteps(N, increasing, decreasing);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function that finds the minimum
// steps to reach either 0 or N for
// given increasing and decreasing
// arrays
function minSteps(N, increasing, decreasing, m1, m2)
{

    // Initialize variable to
    // find the minimum element
    var mini = 2147483647;

    var i;
    // Find minimum element in
    // increasing[] array
    for(i = 0; i < m1; i++)
    {
        if (mini > increasing[i])
            mini = increasing[i];
    }

    // Initialize variable to
    // find the maximum element
    var maxi = -2147483648;

    // Find maximum element in
    // decreasing[] array
    for(i = 0; i < m2; i++)
    {
        if (maxi < decreasing[i])
            maxi = decreasing[i];
    }

    // Find the minimum steps
    var minSteps = Math.max(maxi,N - mini);

    // Print the minimum steps
    document.write(minSteps);
}

// Driver code

    // Given N
    var N = 7;

    // Given increasing
    // and decreasing array
    var increasing = [3, 5];
    var decreasing = [6];

    // Find length of arrays
    // increasing and decreasing
    var m1 = increasing.length;
    var m2 = decreasing.length;

    // Function call
    minSteps(N, increasing, decreasing, m1, m2);

// This code is contributed by bgangwar59.
</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)