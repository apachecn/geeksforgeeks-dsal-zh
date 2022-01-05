# 通过在每第 I 步从一个数组元素中减去 K^i 使所有数组元素等于 0 来修改数组

> 原文:[https://www . geeksforgeeks . org/通过将所有数组元素从每 I 步数组元素中减去 ki 等于 0 来修改数组/](https://www.geeksforgeeks.org/modify-array-by-making-all-array-elements-equal-to-0-by-subtracting-ki-from-an-array-element-in-every-i-th-step/)

给定一个大小为 **N、**的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是在 **i <sup>th</sup>** 步骤中，通过从数组元素中减去 **K <sup>i</sup>** 来检查是否有可能将所有数组元素转换为 **0** s。如果可以，则打印“**是**”。否则，打印“**否**”。

**示例:**

> **输入:** N = 5，K = 2，arr[] = {8，0，3，4，80}
> **输出:**是
> **解释:**
> 一种可能的操作顺序如下:
> 
> 1.  从 arr[2]( = 3)中减去 2 <sup>0</sup> 。此后，数组修改为，arr[] = {8，0，2，4，32}。
> 2.  从 arr[2]( = 2)中减去 2 <sup>1</sup> 。此后，数组修改为，arr[] = {8，0，0，4，32}。
> 3.  从 arr[3]( = 4)中减去 2 <sup>2</sup> 。此后，数组修改为，arr[] = {8，0，0，0，32}。
> 4.  从 arr[1]( = 8)中减去 2 <sup>3</sup> 。此后，数组修改为，arr[] = {0，0，0，0，32}。
> 5.  不要从任何数组元素中减去 2 <sup>4</sup> 。
> 6.  从 arr[4]( = 32)中减去 2 <sup>5</sup> 。此后，数组修改为，arr[] = {0，0，0，0，0}。
> 
> **输入:** N = 3，K = 2，arr[] = {0，1，3 }
> T3】输出:否

**方法:**按照以下步骤解决问题:

*   [初始化一个向量](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/)，比如 **V、**来存储 **K** 所有可能的力量。
*   另外，初始化一个[映射< int，int >](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) ，比如 **MP** ，来存储是否使用了 **K** 的电源。
*   初始化一个变量，说 **X** 为 **1，**存储 **K.** 的幂的计数
*   [迭代](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)直到 **X** 小于**T5**INT _ MAX**并执行以下步骤:**
    *   将 **X** 的值推入[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)。
    *   将**乘以**乘以 **K.**
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–1】**，并执行以下步骤:
    *   使用变量 **j** 反向迭代向量 **V** ，并执行以下步骤:
        *   如果 **arr[i]** 大于 **V[j]** 且**MP【V[j]】**为 **0，**则从 **arr[i]** 中减去 **V[j]** 。
        *   将**MP【V[j]】**更新为 **1** 。
    *   如果**arr【I】**不等于 **0** ，则[从](https://www.geeksforgeeks.org/break-statement-cc/)[循环中断开](https://www.geeksforgeeks.org/c-c-for-loop-with-examples/)。
*   如果 **i** 小于 **N，**则打印**“否”，**作为[数组](https://www.geeksforgeeks.org/array-data-structure/)元素不能做成 **0** 。否则，打印**“是”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check whether all array
// elements can be made zero or not
string isMakeZero(int arr[], int N, int K)
{
    // Stores if a power of K has
    // already been subtracted or not
    map<int, int> MP;

    // Stores all the Kth power
    vector<int> V;

    int X = 1;
    int i;

    // Iterate until X is
    // less than INT_MAX
    while (X > 0 && X < INT_MAX) {
        V.push_back(X);
        X *= K;
    }

    // Traverse the array arr[]
    for (i = 0; i < N; i++) {

        // Iterate over the range [0, M]
        for (int j = V.size() - 1; j >= 0; j--) {

            // If MP[V[j]] is 0 and V[j]
            // is less than or equal to arr[i]
            if (MP[V[j]] == 0 && V[j] <= arr[i]) {
                arr[i] -= V[j];
                MP[V[j]] = 1;
            }
        }

        // If arr[i] is not 0
        if (arr[i] != 0)
            break;
    }

    // If i is less than N
    if (i < N)
        return "No";

    // Otherwise,
    else
        return "Yes";
}

// Driver code
int main()
{

    int arr[] = { 8, 0, 3, 4, 80 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 2;

    cout << isMakeZero(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.ArrayList;
import java.util.HashMap;

class GFG {

    // Function to check whether all array
    // elements can be made zero or not
    static String isMakeZero(int arr[], int N, int K)
    {

        // Stores if a power of K has
        // already been subtracted or not
        HashMap<Integer, Integer> MP = new HashMap<Integer, Integer>();

        // Stores all the Kth power
        ArrayList<Integer> V = new ArrayList<Integer>();

        int X = 1;
        int i;

        // Iterate until X is
        // less than INT_MAX
        while (X > 0 && X < Integer.MAX_VALUE) {
            V.add(X);
            X *= K;
        }

        // Traverse the array arr[]
        for (i = 0; i < N; i++) {

            // Iterate over the range [0, M]
            for (int j = V.size() - 1; j >= 0; j--) {

                // If MP[V[j]] is 0 and V[j]
                // is less than or equal to arr[i]
                if (MP.containsKey(V.get(j)) == false && V.get(j) <= arr[i]) {
                    arr[i] -= V.get(j);
                    MP.put(V.get(j), 1);
                }
            }

            // If arr[i] is not 0
            if (arr[i] != 0)
                break;
        }

        // If i is less than N
        if (i < N)
            return "No";

        // Otherwise,
        else
            return "Yes";
    }

    // Driver code
    public static void main(String[] args)
    {

        int arr[] = { 8, 0, 3, 4, 80 };
        int N = arr.length;
        int K = 2;

        System.out.println(isMakeZero(arr, N, K));
    }
}

// This code is contributed by _saurabh_jaiswal.
```

## 蟒蛇 3

```
# Python Program for the above approach

# Function to check whether all array
# elements can be made zero or not
def isMakeZero(arr, N, K):

    # Stores if a power of K has
    # already been subtracted or not
    MP = {}

    # Stores all the Kth power
    V = []

    X = 1

    # Iterate until X is
    # less than INT_MAX
    while (X > 0 and X < 10**20):
        V.append(X)
        X *= K

    # Traverse the array arr[]
    for i in range(0, N, 1):

        # Iterate over the range [0, M]
        for j in range(len(V) - 1, -1, -1):

            # If MP[V[j]] is 0 and V[j]
            # is less than or equal to arr[i]
            if (V[j] not in MP and V[j] <= arr[i]):
                arr[i] -= V[j]
                MP[V[j]] = 1

        # If arr[i] is not 0
        if (arr[i] != 0):
            break

    # If i is less than N - 1

    if (i < N - 1):
        return "No"

    # Otherwise,
    else:
        return "Yes"

# Driver code
arr = [8, 0, 3, 4, 80]
N = len(arr)
K = 2

print(isMakeZero(arr, N, K))

# This code is contributed by _saurabh_jaiswal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

   // Function to check whether all array
    // elements can be made zero or not
    static string isMakeZero(int[] arr, int N, int K)
    {

        // Stores if a power of K has
        // already been subtracted or not
        Dictionary<int,int> MP = new Dictionary<int,int>();

        // Stores all the Kth power
        List<int> V = new List<int>();

        int X = 1;
        int i;

        // Iterate until X is
        // less than INT_MAX
        while (X > 0 && X < Int32.MaxValue) {
            V.Add(X);
            X *= K;
        }

        // Traverse the array arr[]
        for (i = 0; i < N; i++) {

            // Iterate over the range [0, M]
            for (int j = V.Count - 1; j >= 0; j--) {

                // If MP[V[j]] is 0 and V[j]
                // is less than or equal to arr[i]
                if (MP.ContainsKey(V[j]) == false && V[j] <= arr[i]) {
                    arr[i] -= V[j];
                    MP[V[j]] = 1;
                }
            }

            // If arr[i] is not 0
            if (arr[i] != 0)
                break;
        }

        // If i is less than N
        if (i < N)
            return "No";

        // Otherwise,
        else
            return "Yes";
    }

// Driver Code
public static void Main(String[] args)
{
    int[] arr = { 8, 0, 3, 4, 80 };
        int N = arr.Length;
        int K = 2;

        Console.WriteLine(isMakeZero(arr, N, K));
}
}

// This code is contributed by splevel62.
```

## java 描述语言

```
<script>
        // JavaScript Program for the above approach

        // Function to check whether all array
        // elements can be made zero or not
        function isMakeZero(arr, N, K) {
            // Stores if a power of K has
            // already been subtracted or not
            let MP = new Map();

            // Stores all the Kth power
            let V = [];

            let X = 1;
            let i;

            // Iterate until X is
            // less than INT_MAX
            while (X > 0 && X < Number.MAX_VALUE) {
                V.push(X);
                X *= K;
            }

            // Traverse the array arr[]
            for (i = 0; i < N; i++) {

                // Iterate over the range [0, M]
                for (let j = V.length - 1; j >= 0; j--) {

                    // If MP[V[j]] is 0 and V[j]
                    // is less than or equal to arr[i]
                    if (MP.has(V[j]) == false && V[j] <= arr[i]) {
                        arr[i] -= V[j];
                        MP.set(V[j], 1);
                    }
                }

                // If arr[i] is not 0
                if (arr[i] != 0)
                    break;
            }

            // If i is less than N
            if (i < N)
                return "No";

            // Otherwise,
            else
                return "Yes";
        }

        // Driver code

        let arr = [8, 0, 3, 4, 80];
        let N = arr.length;
        let K = 2;

        document.write(isMakeZero(arr, N, K));

    // This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N * log<sub>K</sub>(INT _ MAX))*
***辅助空间:**O(log<sub>K</sub>(INT _ MAX))*