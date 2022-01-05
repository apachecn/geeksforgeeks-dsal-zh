# 检查一个数组是否可以通过移除不同的元素而减少到最多 K 个长度

> 原文:[https://www . geeksforgeeks . org/check-if-a-array-can-通过移除不同的元素将长度缩减到最大 k/](https://www.geeksforgeeks.org/check-if-an-array-can-be-reduced-to-at-most-length-k-by-removal-of-distinct-elements/)

给定一个由 **N** 个正整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是检查是否有可能通过移除不同数组元素的子集来将数组的[大小减少到最多 K 个。如果可能，则打印**“是”**。否则，打印**“否”**。](https://www.geeksforgeeks.org/how-to-find-size-of-array-in-cc-without-using-sizeof-operator/)

**示例:**

> **输入:** arr[] = {2，2，2，3}，K = 3
> **输出:**是
> **解释:**
> 通过移除子集{2，3}，数组修改为{2，2}(大小= 2)。
> 
> **输入:** arr[] = {1，1，1，3}，K = 1
> T3】输出:否

**方法:**给定的问题可以通过求[给定数组](https://www.geeksforgeeks.org/count-distinct-elements-in-an-array/)中不同元素的个数来解决，比如说**数**。如果**(N-count)**的值最多为**K**，则打印**是**。否则，打印**否**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible
// to reduce the size of the array to K
// by removing the set of the distinct
// array elements
void maxCount(int arr[], int N, int K)
{
    // Stores all distinct elements
    // present in the array arr[]
    set<int> st;

    // Traverse the given array
    for (int i = 0; i < N; i++) {

        // Insert array elements
        // into the set
        st.insert(arr[i]);
    }

    // Condition for reducing size
    // of the array to at most K
    if (N - st.size() <= K) {
        cout << "Yes";
    }
    else
        cout << "No";
}

// Driver Code
int main()
{
    int arr[] = { 2, 2, 2, 3 };
    int K = 3;
    int N = sizeof(arr) / sizeof(arr[0]);
    maxCount(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.HashSet;

public class GFG
{

    // Function to check if it is possible
    // to reduce the size of the array to K
    // by removing the set of the distinct
    // array elements
    static void maxCount(int arr[], int N, int K)
    {

        // Stores all distinct elements
        // present in the array arr[]
        HashSet<Integer> st = new HashSet<>();

        // Traverse the given array
        for (int i = 0; i < N; i++) {

            // Insert array elements
            // into the set
            st.add(arr[i]);
        }

        // Condition for reducing size
        // of the array to at most K
        if (N - st.size() <= K) {
            System.out.println("Yes");
        }
        else
            System.out.println("No");
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 2, 2, 2, 3 };
        int K = 3;
        int N = arr.length;
        maxCount(arr, N, K);
    }
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to check if it is possible
# to reduce the size of the array to K
# by removing the set of the distinct
# array elements
def maxCount(arr, N, K):

    # Stores all distinct elements
    # present in the array arr[]
    st = set()

    # Traverse the given array
    for i in range(N):

        # Insert array elements
        # into the set
        st.add(arr[i])

    # Condition for reducing size
    # of the array to at most K
    if (N - len(st) <= K):
        print("Yes")
    else:
        print("No")

# Driver Code
if __name__ == '__main__':
    arr = [2, 2, 2, 3]
    K = 3
    N = len(arr)
    maxCount(arr, N, K)

    # This code is contributed by bgangwar59.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check if it is possible
// to reduce the size of the array to K
// by removing the set of the distinct
// array elements
static void maxCount(int[] arr, int N, int K)
{

    // Stores all distinct elements
    // present in the array arr[]
    HashSet<int> st = new HashSet<int>();

    // Traverse the given array
    for(int i = 0; i < N; i++)
    {

        // Insert array elements
        // into the set
        st.Add(arr[i]);
    }

    // Condition for reducing size
    // of the array to at most K
    if (N - st.Count <= K)
    {
        Console.Write("Yes");
    }
    else
        Console.Write("No");
}

// Driver code
static public void Main()
{
    int[] arr = { 2, 2, 2, 3 };
    int K = 3;
    int N = arr.Length;

    maxCount(arr, N, K);
}
}

// This code is contributed by offbeat
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check if it is possible
// to reduce the size of the array to K
// by removing the set of the distinct
// array elements
function maxCount(arr, N, K) {
    // Stores all distinct elements
    // present in the array arr[]
    let st = new Set();

    // Traverse the given array
    for (let i = 0; i < N; i++) {

        // Insert array elements
        // into the set
        st.add(arr[i]);
    }

    // Condition for reducing size
    // of the array to at most K
    if (N - st.size <= K) {
        document.write("Yes");
    }
    else
        document.write("No");
}

// Driver Code

let arr = [2, 2, 2, 3];
let K = 3;
let N = arr.length
maxCount(arr, N, K);

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(N)*