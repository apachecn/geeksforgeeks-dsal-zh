# 生成满足给定条件的大小为 K 的数组

> 原文:[https://www . geeksforgeeks . org/生成满足给定条件的大小为 k 的数组/](https://www.geeksforgeeks.org/generate-an-array-of-size-k-which-satisfies-the-given-conditions/)

给定两个整数 **N** 和 **K** ，任务是生成一个长度为 **K** 的数组**arr【】**:

1.  **arr[0]+arr[1]+…+arr[K–1]= N**。
2.  **arr【I】>0**为 **0 ≤ i < K** 。
3.  **疤痕[i] < 疤痕[i + 1] ≤ 2 * 疤痕[i]** 对于 **0 ≤在 < K – 1** 。

如果有多个答案，找到其中任意一个，否则打印 **-1** 。

**示例:**

> **输入:** N = 26，K = 6
> **输出:** 1 2 4 5 6 8
> 生成的数组满足所有给定的条件。
> **输入:** N = 8，K = 3
> **输出:** -1

**进场:**让**r = n–k *(k+1)/2**。如果 **r < 0** 那么答案是 **-1** 已经。否则，我们构造数组 **arr[]** ，其中所有 **arr[i]** 都是**楼层(r / k)** 除了最右边的 **r % k** 值外，都是**天花板(r / k)** 。
很容易看出这个数组的和是 **r** ，按非递减顺序排序，最大和最小元素之差不大于 1。
我们把 **1** 加到**arr【1】**、 **2** 加到**arr【2】**等等(这是我们一开始从 n 减去的)。
那么，如果 **r！= k–1**或 **k = 1** 那么 **arr[]** 就是我们需要的数组。否则，我们得到某种数组 **1，3，…..，arr[k]** 。对于 **k = 2** 或 **k = 3** ，这种情况没有答案。否则，我们可以从 **arr[2]** 中减去 **1** ，再加到 **arr[k]** 中，这个答案就是正确的。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to generate and print
// the required array
void generateArray(int n, int k)
{

    // Initializing the array
    vector<int> array(k, 0);

    // Finding r (from above approach)
    int remaining = n - int(k * (k + 1) / 2);

    // If r<0
    if (remaining < 0)
        cout << ("NO");

    int right_most = remaining % k;

    // Finding ceiling and floor values
    int high = ceil(remaining / (k * 1.0));
    int low = floor(remaining / (k * 1.0));

    // Fill the array with ceiling values
    for (int i = k - right_most; i < k; i++)
        array[i]= high;

    // Fill the array with floor values
    for (int i = 0; i < (k - right_most); i++)
        array[i]= low;

    // Add 1, 2, 3, ... with corresponding values
    for (int i = 0; i < k; i++)
        array[i] += i + 1;

    if (k - 1 != remaining or k == 1)
    {
        for(int u:array) cout << u << " ";
    }

    // There is no solution for below cases
    else if (k == 2 or k == 3)
        printf("-1\n");
    else
    {

        // Modify A[1] and A[k-1] to get
        // the required array
        array[1] -= 1;
        array[k - 1] += 1;
        for(int u:array) cout << u << " ";
    }
}

// Driver Code
int main()
{
    int n = 26, k = 6;
    generateArray(n, k);
    return 0;
}

// This code is contributed
// by Mohit Kumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to generate and print
// the required array
static void generateArray(int n, int k)
{

    // Initializing the array
    int []array = new int[k];

    // Finding r (from above approach)
    int remaining = n - (k * (k + 1) / 2);

    // If r < 0
    if (remaining < 0)
        System.out.print("NO");

    int right_most = remaining % k;

    // Finding ceiling and floor values
    int high = (int) Math.ceil(remaining / (k * 1.0));
    int low = (int) Math.floor(remaining / (k * 1.0));

    // Fill the array with ceiling values
    for (int i = k - right_most; i < k; i++)
        array[i] = high;

    // Fill the array with floor values
    for (int i = 0; i < (k - right_most); i++)
        array[i] = low;

    // Add 1, 2, 3, ... with corresponding values
    for (int i = 0; i < k; i++)
        array[i] += i + 1;

    if (k - 1 != remaining || k == 1)
    {
        for(int u:array)
            System.out.print(u + " ");
    }

    // There is no solution for below cases
    else if (k == 2 || k == 3)
        System.out.printf("-1\n");
    else
    {

        // Modify A[1] and A[k-1] to get
        // the required array
        array[1] -= 1;
        array[k - 1] += 1;
        for(int u:array)
            System.out.print(u + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int n = 26, k = 6;
    generateArray(n, k);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys
from math import floor, ceil

# Function to generate and print
# the required array
def generateArray(n, k):

    # Initializing the array
    array = [0] * k

    # Finding r (from above approach)
    remaining = n-int(k*(k + 1)/2)

    # If r<0
    if remaining<0:
        print("NO")
        sys.exit()

    right_most = remaining % k

    # Finding ceiling and floor values
    high = ceil(remaining / k)
    low = floor(remaining / k)

    # Fill the array with ceiling values
    for i in range(k-right_most, k):
        array[i]= high

    # Fill the array with floor values
    for i in range(k-right_most):
        array[i]= low

    # Add 1, 2, 3, ... with corresponding values
    for i in range(k):
        array[i]+= i + 1

    if k-1 != remaining or k == 1:
        print(*array)
        sys.exit()

    # There is no solution for below cases
    elif k == 2 or k == 3:
        print("-1")
        sys.exit()
    else:

        # Modify A[1] and A[k-1] to get
        # the required array
        array[1]-= 1
        array[k-1]+= 1
        print(*array)
        sys.exit()

# Driver Code
if __name__=="__main__":
    n, k = 26, 6
    generateArray(n, k)
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to generate and print
// the required array
static void generateArray(int n, int k)
{

    // Initializing the array
    int []array = new int[k];

    // Finding r (from above approach)
    int remaining = n - (k * (k + 1) / 2);

    // If r < 0
    if (remaining < 0)
        Console.Write("NO");

    int right_most = remaining % k;

    // Finding ceiling and floor values
    int high = (int) Math.Ceiling(remaining /
                                 (k * 1.0));
    int low = (int) Math.Floor(remaining /
                              (k * 1.0));

    // Fill the array with ceiling values
    for (int i = k - right_most; i < k; i++)
        array[i] = high;

    // Fill the array with floor values
    for (int i = 0;
             i < (k - right_most); i++)
        array[i] = low;

    // Add 1, 2, 3, ... with
    // corresponding values
    for (int i = 0; i < k; i++)
        array[i] += i + 1;

    if (k - 1 != remaining || k == 1)
    {
        foreach(int u in array)
            Console.Write(u + " ");
    }

    // There is no solution for below cases
    else if (k == 2 || k == 3)
        Console.Write("-1\n");
    else
    {

        // Modify A[1] and A[k-1] to get
        // the required array
        array[1] -= 1;
        array[k - 1] += 1;
        foreach(int u in array)
            Console.Write(u + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int n = 26, k = 6;
    generateArray(n, k);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// javascript implementation of the approach   
// Function to generate and print
    // the required array
    function generateArray(n , k) {

        // Initializing the array
        var array = Array(k).fill(0);

        // Finding r (from above approach)
        var remaining = n - parseInt(k * (k + 1) / 2);

        // If r < 0
        if (remaining < 0)
            document.write("NO");

        var right_most = remaining % k;

        // Finding ceiling and floor values
        var high = parseInt( Math.ceil(remaining / (k * 1.0)));
        var low = parseInt( Math.floor(remaining / (k * 1.0)));

        // Fill the array with ceiling values
        for (i = k - right_most; i < k; i++)
            array[i] = high;

        // Fill the array with floor values
        for (i = 0; i < (k - right_most); i++)
            array[i] = low;

        // Add 1, 2, 3, ... with corresponding values
        for (i = 0; i < k; i++)
            array[i] += i + 1;

        if (k - 1 != remaining || k == 1) {
            for (var u = 0;u< array.length;u++)
                document.write(array[u] + " ");
        }

        // There is no solution for below cases
        else if (k == 2 || k == 3)
            document.write("-1");
        else {

            // Modify A[1] and A[k-1] to get
            // the required array
            array[1] -= 1;
            array[k - 1] += 1;
            for (var f = 0;f< array.length;f++)
                document.write(array[f] + " ");
        }
    }

    // Driver Code

        var n = 26, k = 6;
        generateArray(n, k);

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
1 2 4 5 6 8
```