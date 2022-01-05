# 将数组拆分成子数组，每个元素只属于一个子数组

> 原文:[https://www . geesforgeks . org/sort-array-by-split-in-subarray-其中每个元素只属于一个子阵列/](https://www.geeksforgeeks.org/sort-array-by-splitting-into-subarrays-where-each-element-belongs-to-only-subarray/)

给定一个由不同的整数组成的[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)**arr[]****N****，任务是检查是否有可能通过在**顺序**中精确地执行以下操作**一次**以递增的顺序对数组进行排序:**

*   **将阵列**arr【】**拆分为**恰好**T6】Y(1<= Y<= N)**非空[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，使得每个元素恰好属于一个子阵列。
*   **以任意顺序重新排列**子阵列。
*   **合并**重新排序的子阵列。

**示例:**

> **输入:** arr[ ] = {6，3，4，2，1}，Y = 4
> **输出:**是
> **说明:**
> 操作可按如下方式进行:
> 
> *   将阵列精确分割为 4 个非空子阵列:{6，3，4，2，1 }--> { 6 }、{3，4}、{2}、{1}
> *   重新排列子阵列:{6}、{3，4}、{2}、{ 1 }--> { 1 }、{2}、{3，4}、{6}
> *   合并子阵列:{1}、{2}、{3，4}、{6} -> {1，2，3，4，6} ( **排序后的**)
> 
> **输入:** arr[ ] = {1，-4，0，-2}，Y = 2
> T3】输出:否

**方法:**主要思想是如果排序给定数组**arr【】**所需的**最小**拆分数小于或等于 **Y，**则总是可以排序数组。此外，所需的分割数必须等于将阵列分割成最小数量的非递减子阵列所需的最小分割数的[计数](https://www.geeksforgeeks.org/split-an-array-into-minimum-number-of-non-increasing-or-non-decreasing-subarrays/)。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Initialization of pair
pair<int, int> a[100001];

// Function to check if it is possible
// to sort the array by performing the
// operations exactly once in order
void checkForSortedSubarray(int n, int y, int arr[])
{

    // Traversing the array
    for (int i = 1; i <= n; i++) {
        // Storing the array element
        // in the first part of pair
        a[i].first = arr[i];

        // Storing the index as second
        // element in the pair
        a[i].second = i;
    }

    // Initialize Count
    int cnt = 1;

    // Sorting the array
    sort(a + 1, a + n + 1);

    for (int i = 1; i <= n - 1; i++) {

        // Checking if the index lies
        // in order
        if (a[i].second != a[i + 1].second - 1)
            cnt++;
    }

    // If minimum splits required is
    // greater than y
    if (cnt > y)
        cout << "No";
    else
        cout << "Yes";
}

// Driver Code
int main()

{
    int Y = 4;
    int arr[] = { 6, 3, 4, 2, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);

    checkForSortedSubarray(N, Y, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Initialization of pair
static pair []a = new pair[100001];
static class pair
{
    int first, second;
    public pair(int first, int second) 
    {
        this.first = first;
        this.second = second;
    }   
}
// Function to check if it is possible
// to sort the array by performing the
// operations exactly once in order
static void checkForSortedSubarray(int n, int y, int arr[])
{

    // Traversing the array
    for (int i = 1; i <= n; i++) {
        // Storing the array element
        // in the first part of pair
        a[i].first = arr[i];

        // Storing the index as second
        // element in the pair
        a[i].second = i;
    }

    // Initialize Count
    int cnt = 1;

    // Sorting the array
    Arrays.sort(a,(a, b) -> a.first - b.first);

    for (int i = 1; i <= n - 1; i++) {

        // Checking if the index lies
        // in order
        if (a[i].second != a[i + 1].second - 1)
            cnt++;
    }

    // If minimum splits required is
    // greater than y
    if (cnt > y)
        System.out.print("No");
    else
        System.out.print("Yes");
}

// Driver Code
public static void main(String[] args)

{
    int Y = 4;
    int arr[] = { 6, 3, 4, 2, 1 };
    int N = arr.length;
    for(int i = 0;i<a.length;i++) {
        a[i] = new pair(0, 0);
    }
    checkForSortedSubarray(N-1, Y, arr);

}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Initialization of pair

# Function to check if it is possible
# to sort the array by performing the
# operations exactly once in order
def checkForSortedSubarray(n, y, arr, a):

    # Traversing the array
    for i in range(0, n, 1):

        # Storing the array element
        # in the first part of pair
        a[i][0] = arr[i]

        # Storing the index as second
        # element in the pair
        a[i][1] = i

    # Initialize Count
    cnt = 1

    # Sorting the array
    a.sort()

    for i in range(0,n,1):
        # Checking if the index lies
        # in order
        if (a[i][1] != a[i + 1][1] - 1):
            cnt += 1

    # If minimum splits required is
    # greater than y
    if (cnt > y):
        print("Yes")
    else:
        print("No")

# Driver Code
if __name__ == '__main__':
    Y = 4
    a = [[0,0] for i in range(100001)]
    arr = [6, 3, 4, 2, 1]
    N = len(arr)
    checkForSortedSubarray(N, Y, arr,a)

    # This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to check if it is possible
        // to sort the array by performing the
        // operations exactly once in order

        // Initialization of pair
        var a = [];
        function checkForSortedSubarray(n, y, arr)
        {

            // Traversing the array
            for (let i = 0; i < n; i++)
            {

                // Storing the array element
                // in the first part of pair

                // Storing the index as second
                // element in the pair
                a.push({
                    first: arr[i],
                    second: i
                })
            }

            // Initialize Count
            let cnt = 1;

            // Sorting the array
            a.sort(function (a, b) { return a.first - b.first; })

            for (let i = 0; i < n - 1; i++) {

                // Checking if the index lies
                // in order
                if (a[i].second != a[i + 1].second - 1)
                    cnt++;
            }

            // If minimum splits required is
            // greater than y
            if (cnt > y)
                document.write("No");
            else
                document.write("Yes");
        }

        // Driver Code
        let Y = 4;
        let arr = [6, 3, 4, 2, 1];
        let N = arr.length;

        checkForSortedSubarray(N, Y, arr);

// This code is contributed by Potta Lokesh

    </script>
```

**Output**

```
Yes
```

***时间复杂度:** O(N Log N)*
***辅助空间:** O(N)*