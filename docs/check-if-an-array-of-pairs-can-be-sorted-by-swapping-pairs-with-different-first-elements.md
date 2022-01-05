# 检查是否可以通过交换具有不同第一元素的对来对一组对进行排序

> 原文:[https://www . geeksforgeeks . org/check-if-a-array-of-pair-of-material-first-elements-可通过交换对来排序/](https://www.geeksforgeeks.org/check-if-an-array-of-pairs-can-be-sorted-by-swapping-pairs-with-different-first-elements/)

给定一个由**N**T6】对组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，其中每对分别代表**值**和 **ID** ，任务是检查是否有可能通过仅交换具有不同**ID**的对来按照第一个元素对数组进行排序。如果可以排序，则打印**“是”**。否则，打印**“否”**。

**示例:**

> ***输入:** arr[] = {{340000，2}、{45000，1}、{30000，2}、{50000，4}}*
> ***输出:**是*
> ***解释:***
> *对数组进行排序的一种可能方式是按照以下顺序交换数组元素:*
> 
> 1.  *交换， **arr[0]** 和 **arr[3]** ，将数组修改为 arr[] = {{50000，4}、{45000，1}、{30000，2}、{340000，2}}。*
> 2.  *交换， **arr[0]** 和 **arr[2]** ，将数组修改为 arr[] = {{30000，2}、{45000，1}、{50000，4}、{340000，2}}。*
> 
> *因此，在上述步骤之后，给定的数组按第一个元素排序..*
> 
> ***输入:** arr[] = {{15000，2}，{34000，2}，{10000，2}}*
> ***输出:**否*

**方法:**如果存在任意两个不同**id**的数组元素，[数组可以排序](https://www.geeksforgeeks.org/check-if-array-can-be-sorted-with-one-swap/)的观察可以解决给定的问题。按照以下步骤解决问题:

*   初始化一个变量，比如说 **X** ，它在索引 **0** 处存储该对的 **ID** 。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**如果有任何一对 **ID** 与 **X** 不同，则打印**“是”**[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   完成上述步骤后，如果所有元素的**标识**和[相同，如果数组已经排序](https://www.geeksforgeeks.org/program-check-array-sorted-not-iterative-recursive/)，则打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if an
// array is sorted or not
bool isSorted(pair<int, int>* arr,
              int N)
{
    // Traverse the array arr[]
    for (int i = 1; i < N; i++) {

        if (arr[i].first
            > arr[i - 1].first) {
            return false;
        }
    }

    // Return true
    return true;
}

// Function to check if it is possible
// to sort the array w.r.t. first element
string isPossibleToSort(
    pair<int, int>* arr, int N)
{
    // Stores the ID of the first element
    int group = arr[0].second;

    // Traverse the array arr[]
    for (int i = 1; i < N; i++) {

        // If arr[i].second is not
        // equal to that of the group
        if (arr[i].second != group) {
            return "Yes";
        }
    }

    // If array is sorted
    if (isSorted(arr, N)) {
        return "Yes";
    }
    else {
        return "No";
    }
}

// Driver Code
int main()
{
    pair<int, int> arr[]
        = { { 340000, 2 }, { 45000, 1 },
            { 30000, 2 }, { 50000, 4 } };

    int N = sizeof(arr) / sizeof(arr[0]);

    cout << isPossibleToSort(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG {

    // Function to check if an
    // array is sorted or not
    static boolean isSorted(int[][] arr, int N)
    {
        // Traverse the array arr[]
        for (int i = 1; i < N; i++) {

            if (arr[i][0] > arr[i - 1][0]) {
                return false;
            }
        }

        // Return true
        return true;
    }

    // Function to check if it is possible
    // to sort the array w.r.t. first element
    static String isPossibleToSort(int[][] arr, int N)
    {
        // Stores the ID of the first element
        int group = arr[0][1];

        // Traverse the array arr[]
        for (int i = 1; i < N; i++) {

            // If arr[i].second is not
            // equal to that of the group
            if (arr[i][1] != group) {
                return "Yes";
            }
        }

        // If array is sorted
        if (isSorted(arr, N)) {
            return "Yes";
        }
        else {
            return "No";
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        int arr[][] = { { 340000, 2 },
                        { 45000, 1 },
                        { 30000, 2 },
                        { 50000, 4 } };

        int N = arr.length;
        System.out.print(isPossibleToSort(arr, N));
    }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if an
# array is sorted or not
def isSorted(arr, N):

    # Traverse the array arr[]
    for i in range(1, N):
        if (arr[i][0] > arr[i - 1][0]):
            return False

    # Return true
    return True

# Function to check if it is possible
# to sort the array w.r.t. first element
def isPossibleToSort(arr, N):

    # Stores the ID of the first element
    group = arr[0][1]

    # Traverse the array arr[]
    for i in range(1, N):

        # If arr[i][1] is not
        # equal to that of the group
        if (arr[i][1] != group):
            return "Yes"

    # If array is sorted
    if (isSorted(arr, N)):
        return "Yes"
    else:
        return "No"

# Driver Code
if __name__ == '__main__':
    arr = [ [ 340000, 2 ], [ 45000, 1 ],[ 30000, 2 ], [ 50000, 4 ] ]

    N = len(arr)

    print (isPossibleToSort(arr, N))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
class GFG {
    // Function to check if an
    // array is sorted or not
    static bool isSorted(int[, ] arr, int N)
    {
        // Traverse the array arr[]
        for (int i = 1; i < N; i++) {

            if (arr[i, 0] > arr[i - 1, 0]) {
                return false;
            }
        }

        // Return true
        return true;
    }

    // Function to check if it is possible
    // to sort the array w.r.t. first element
    static string isPossibleToSort(int[, ] arr, int N)
    {
        // Stores the ID of the first element
        int group = arr[0, 1];

        // Traverse the array arr[]
        for (int i = 1; i < N; i++) {

            // If arr[i].second is not
            // equal to that of the group
            if (arr[i, 1] != group) {
                return "Yes";
            }
        }

        // If array is sorted
        if (isSorted(arr, N)) {
            return "Yes";
        }
        else {
            return "No";
        }
    }

    // Driver Code
    public static void Main()
    {
        int[, ] arr = { { 340000, 2 },
                        { 45000, 1 },
                        { 30000, 2 },
                        { 50000, 4 } };

        int N = arr.GetLength(0);

        Console.WriteLine(isPossibleToSort(arr, N));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // Javascript program for the above approach

        // Function to check if an
        // array is sorted or not
        function isSorted(arr, N) {
            // Traverse the array arr[]
            for (let i = 1; i < N; i++) {

                if (arr[i][0] > arr[i - 1][0]) {
                    return false;
                }
            }

            // Return true
            return true;
        }

        // Function to check if it is possible
        // to sort the array w.r.t. first element
        function isPossibleToSort(arr, N) {
            // Stores the ID of the first element
            let group = arr[0][1];

            // Traverse the array arr[]
            for (let i = 1; i < N; i++) {

                // If arr[i].second is not
                // equal to that of the group
                if (arr[i][1] != group) {
                    return "Yes";
                }
            }

            // If array is sorted
            if (isSorted(arr, N)) {
                return "Yes";
            }
            else {
                return "No";
            }
        }

        // Driver Code

        let arr = [[340000, 2],
        [15000, 2],
        [34000, 2],
        [10000, 2]];

        let N = arr.length;
        document.write(isPossibleToSort(arr, N));

        // This code is contributed by Hritik
    </script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)