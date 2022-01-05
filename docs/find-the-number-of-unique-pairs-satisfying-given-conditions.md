# 找出满足给定条件的唯一对的数量

> 原文:[https://www . geeksforgeeks . org/find-满足给定条件的唯一对的数量/](https://www.geeksforgeeks.org/find-the-number-of-unique-pairs-satisfying-given-conditions/)

给定不同正元素的数组 **arr[]** ，任务是找到唯一对 **(a，b)** 的数量，使得 **a** 是最大值， **b** 是给定数组的某个子数组的第二大元素。
**举例:**

> **输入:** arr[] = {1，2，3}
> **输出:** 2
> {1，2}、{2，3}、{1，2，3}为子阵，满足给定条件的对
> 仅为(2，1)和(3，2)。
> **输入:** arr[] = {4，1，2}
> **输出:** 3

**天真的方法:**我们可以为每个子阵列找到配对，并将其存储在一个集合中，然后打印出来。这种方法需要 **O(n <sup>3</sup> )** 时间，因为需要 **O(n <sup>2</sup> )** 来寻找子阵列，需要 **O(n)** 来寻找子阵列的最大和第二大元素。
**高效的方法:**让我们考虑 **a1、a2、a3、a4** 作为数组的前四个元素，同时也假设 **a2** 和 **a3** 小于 **a1** 和 **a4** 大于 **a1** 。
显然， **(a4，a1)** 是必选对之一。现在可以证明 **a4** 之后的任何元素都不能与 **a1** 配对。
由于所有元素都是唯一的，要么会有大于 **a4** 的元素，要么 **a4** 之后的所有元素都会小于 **a4** 。假设 **aM** 大于 **a4** 。然后，从第一个元素到 **Mth** 元素的子阵列将有 **aM** 作为最大元素， **a4** 作为第二个最大元素，因此， **(aM，a4)** 将是所需的对。现在，如果直到 **M** 的所有元素都小于 **a4** ，那么 **a4** 将是最大元素。在任何情况下， **a1** 将仅与 **a4** 配对。
简单来说，如果存在比这更大的元素并且也具有更高的指数，则元素将对一对做出贡献。如果数组以相反的方向遍历，也可以使用相同的参数。
因此，**总对数=向前遍历中具有较大元素的元素数+向后遍历中具有较大元素的元素数**，这可以使用本文中讨论的方法轻松计算。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of the required pairs
int countPairs(int arr[], int n)
{

    // Calculating the valid pairs
    // in forward direction
    int forward[n] = { 0 };
    stack<int> sForward;
    for (int i = 0; i < n; i++) {
        while (!sForward.empty()
               && arr[i] > arr[sForward.top()]) {
            forward[sForward.top()] = 1;
            sForward.pop();
        }
        sForward.push(i);
    }

    // Calculating the valid pairs
    // in backward direction
    int backward[n] = { 0 };
    stack<int> sBackward;
    for (int i = n - 1; i >= 0; i--) {
        while (!sBackward.empty()
               && arr[i] > arr[sBackward.top()]) {
            backward[sBackward.top()] = 1;
            sBackward.pop();
        }
        sBackward.push(i);
    }

    // Calculating the total number of pairs
    int res = 0;
    for (int i = 0; i < n; i++) {
        res += forward[i] + backward[i];
    }
    return res;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << countPairs(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to return the count
    // of the required pairs
    static int countPairs(int arr[], int n)
    {

        // Calculating the valid pairs
        // in forward direction
        int forward[] = new int[n];
        Stack<Integer> sForward = new Stack<Integer>();
        for (int i = 0; i < n; i++)
        {
            while (!sForward.empty()
                && arr[i] > arr[(Integer)sForward.peek()])
            {
                forward[(Integer)sForward.peek()] = 1;
                sForward.pop();
            }
            sForward.push(i);
        }

        // Calculating the valid pairs
        // in backward direction
        int backward [] = new int[n] ;
        Stack<Integer> sBackward = new Stack<Integer>() ;
        for (int i = n - 1; i >= 0; i--)
        {
            while (!sBackward.empty()
                && arr[i] > arr[(Integer)sBackward.peek()])
            {
                backward[(Integer)sBackward.peek()] = 1;
                sBackward.pop();
            }
            sBackward.push(i);
        }

        // Calculating the total number of pairs
        int res = 0;
        for (int i = 0; i < n; i++)
        {
            res += forward[i] + backward[i];
        }
        return res;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 1, 2, 3, 4, 5 };
        int n = arr.length;

        System.out.println(countPairs(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of the required pairs
def countPairs(arr, n) :

    # Calculating the valid pairs
    # in forward direction
    forward = [0] * n;

    sForward = [];

    for i in range(n) :
        while (len(sForward) != 0 and arr[i] > arr[sForward[-1]]) :
            forward[sForward[-1]] = 1;
            sForward.pop();

        sForward.append(i);

    # Calculating the valid pairs
    # in backward direction
    backward = [0] * n;

    sBackward = [];

    for i in range(n - 1, -1, -1) :

        while (len(sBackward) != 0 and arr[i] > arr[sBackward[-1]]) :
            backward[sBackward[-1]] = 1;
            sBackward.pop();

        sBackward.append(i);

    # Calculating the total number of pairs
    res = 0;
    for i in range(n) :
        res += forward[i] + backward[i];

    return res;

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 2, 3, 4, 5 ];

    n = len(arr);

    print(countPairs(arr, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections;

class GFG
{

    // Function to return the count
    // of the required pairs
    static int countPairs(int []arr, int n)
    {

        // Calculating the valid pairs
        // in forward direction
        int []forward = new int[n];
        Stack sForward = new Stack();

        for (int i = 0; i < n; i++)
        {
            while (sForward.Count != 0
                && arr[i] > arr[(int)sForward.Peek()])
            {
                forward[(int)sForward.Peek()] = 1;
                sForward.Pop();
            }
            sForward.Push(i);
        }

        // Calculating the valid pairs
        // in backward direction
        int []backward = new int[n] ;
        Stack sBackward = new Stack() ;
        for (int i = n - 1; i >= 0; i--)
        {
            while (sBackward.Count != 0
                && arr[i] > arr[(int)sBackward.Peek()])
            {
                backward[(int)sBackward.Peek()] = 1;
                sBackward.Pop();
            }
            sBackward.Push(i);
        }

        // Calculating the total number of pairs
        int res = 0;
        for (int i = 0; i < n; i++)
        {
            res += forward[i] + backward[i];
        }
        return res;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 1, 2, 3, 4, 5 };
        int n = arr.Length;

        Console.WriteLine(countPairs(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count
// of the required pairs
function countPairs(arr, n)
{

    // Calculating the valid pairs
    // in forward direction
    var forward = Array(n).fill(0);
    var sForward = [];
    for (var i = 0; i < n; i++) {
        while (sForward.length!=0
               && arr[i] > arr[sForward[sForward.length-1]]) {
            forward[sForward[sForward.length-1]] = 1;
            sForward.pop();
        }
        sForward.push(i);
    }

    // Calculating the valid pairs
    // in backward direction
    var backward = Array(n).fill(0);
    var sBackward = [];
    for (var i = n - 1; i >= 0; i--) {
        while (sBackward.length != 0
               && arr[i] > arr[sBackward[sBackward.length-1]]) {
            backward[sBackward[sBackward.length-1]] = 1;
            sBackward.pop();
        }
        sBackward.push(i);
    }

    // Calculating the total number of pairs
    var res = 0;
    for (var i = 0; i < n; i++) {
        res += forward[i] + backward[i];
    }
    return res;
}

// Driver code
var arr = [1, 2, 3, 4, 5];
var n = arr.length;
document.write( countPairs(arr, n));

// This code is contributed by itsok.
</script>
```

**Output:** 

```
4
```

**时间复杂度:**O(N)
T3】辅助空间 : O(N)