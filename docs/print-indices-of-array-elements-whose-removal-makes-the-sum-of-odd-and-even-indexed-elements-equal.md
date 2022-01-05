# 打印数组元素的索引，删除数组元素会使奇数和偶数索引元素的总和相等

> 原文:[https://www . geeksforgeeks . org/print-indexes-of-array-elements-其移除使奇数和偶数索引元素的总和相等/](https://www.geeksforgeeks.org/print-indices-of-array-elements-whose-removal-makes-the-sum-of-odd-and-even-indexed-elements-equal/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到数组元素的索引，移除这些索引会使奇数和偶数索引元素的总和相等。如果不存在这样的元素，则打印 **-1** 。

**示例:**

> **输入:** arr[] = {4，1，6，2}
> **输出:** 1
> **解释:**
> 移除 arr[1]将 arr[]修改为{4，6，2}
> 偶数索引数组元素之和= arr[0] + arr[2] = 4 + 2 = 6
> 奇数索引数组元素之和= arr[1] = 6
> 因此，所需输出为 1。
> 
> **输入:** arr = {3，2，1}
> **输出:** -1

**天真法:**解决这个问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并从数组中移除 **i <sup>th</sup>** 元素，检查奇数索引数组元素的和是否等于偶数索引数组元素的和。如果发现是真的，那么打印索引。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**有效方法:**上述方法可以使用[前缀求和技术](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)进行优化。其思想是利用这样一个事实:如果一个数组元素从索引中移除，那么在那个索引之后，偶数索引的数组元素变成奇数索引的，反之亦然。按照以下步骤解决问题:

*   初始化两个数组，比如**奇数[]** 和**偶数[]** ，分别存储奇数和偶数索引数组元素的前缀和和偶数索引数组元素的前缀和。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，计算奇数和偶数索引数组元素的前缀和。
*   初始化两个变量，比如 **P = 0** 和 **Q = 0** ，分别存储一个数组元素移除后的偶数和奇数索引数组元素的和。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，逐个删除数组元素，并相应更新前缀和。检查偶数索引数组元素的和 **P** 是否等于奇数索引数组元素的和 **Q** 。如果发现为真，则打印当前索引。
*   否则，打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find indices of array elements
// whose removal makes the sum of odd and
// even indexed array elements equal
void removeIndicesToMakeSumEqual(vector<int>& arr)
{
    // Stores size of array
    int N = arr.size();

    // Store prefix sum of odd
    // index array elements
    vector<int> odd(N, 0);

    // Store prefix sum of even
    // index array elements
    vector<int> even(N, 0);

    // Update even[0]
    even[0] = arr[0];

    // Traverse the given array
    for (int i = 1; i < N; i++) {

        // Update odd[i]
        odd[i] = odd[i - 1];

        // Update even[i]
        even[i] = even[i - 1];

        // If the current index
        // is an even number
        if (i % 2 == 0) {

            // Update even[i]
            even[i] += arr[i];
        }

        // If the current index
        // is an odd number
        else {

            // Update odd[i]
            odd[i] += arr[i];
        }
    }

    // Check if at least one
    // index found or not that
    // satisfies the condition
    bool find = 0;

    // Store odd indices sum by
    // removing 0-th index
    int p = odd[N - 1];

    // Store even indices sum by
    // removing 0-th index
    int q = even[N - 1] - arr[0];

    // If p and q are equal
    if (p == q) {
        cout << "0 ";
        find = 1;
    }

    // Traverse the array arr[]
    for (int i = 1; i < N; i++) {

        // If i is an even number
        if (i % 2 == 0) {

            // Update p by removing
            // the i-th element
            p = even[N - 1] - even[i - 1]
                - arr[i] + odd[i - 1];

            // Update q by removing
            // the i-th element
            q = odd[N - 1] - odd[i - 1]
                + even[i - 1];
        }
        else {

            // Update q by removing
            // the i-th element
            q = odd[N - 1] - odd[i - 1]
                - arr[i] + even[i - 1];

            // Update p by removing
            // the i-th element
            p = even[N - 1] - even[i - 1]
                + odd[i - 1];
        }

        // If odd index values sum is equal
        // to even index values sum
        if (p == q) {

            // Set the find variable
            find = 1;

            // Print the current index
            cout << i << " ";
        }
    }

    // If no index found
    if (!find) {

        // Print not possible
        cout << -1;
    }
}

// Driver Code
int main()
{
    vector<int> arr = { 4, 1, 6, 2 };
    removeIndicesToMakeSumEqual(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find indices of array elements
// whose removal makes the sum of odd and
// even indexed array elements equal
static void removeIndicesToMakeSumEqual(int []arr)
{

    // Stores size of array
    int N = arr.length;

    // Store prefix sum of odd
    // index array elements
    int []odd = new int[N];

    // Store prefix sum of even
    // index array elements
    int []even = new int[N];

    // Update even[0]
    even[0] = arr[0];

    // Traverse the given array
    for(int i = 1; i < N; i++)
    {

        // Update odd[i]
        odd[i] = odd[i - 1];

        // Update even[i]
        even[i] = even[i - 1];

        // If the current index
        // is an even number
        if (i % 2 == 0)
        {

            // Update even[i]
            even[i] += arr[i];
        }

        // If the current index
        // is an odd number
        else
        {

            // Update odd[i]
            odd[i] += arr[i];
        }
    }

    // Check if at least one
    // index found or not that
    // satisfies the condition
    boolean find = false;

    // Store odd indices sum by
    // removing 0-th index
    int p = odd[N - 1];

    // Store even indices sum by
    // removing 0-th index
    int q = even[N - 1] - arr[0];

    // If p and q are equal
    if (p == q)
    {
        System.out.print("0 ");
        find = true;
    }

    // Traverse the array arr[]
    for(int i = 1; i < N; i++)
    {

        // If i is an even number
        if (i % 2 == 0)
        {

            // Update p by removing
            // the i-th element
            p = even[N - 1] - even[i - 1] -
                     arr[i] + odd[i - 1];

            // Update q by removing
            // the i-th element
            q = odd[N - 1] - odd[i - 1] +
               even[i - 1];
        }
        else
        {

            // Update q by removing
            // the i-th element
            q = odd[N - 1] - odd[i - 1] -
                    arr[i] + even[i - 1];

            // Update p by removing
            // the i-th element
            p = even[N - 1] - even[i - 1] +
                 odd[i - 1];
        }

        // If odd index values sum is equal
        // to even index values sum
        if (p == q)
        {

            // Set the find variable
            find = true;

            // Print the current index
            System.out.print(i + " ");
        }
    }

    // If no index found
    if (!find)
    {

        // Print not possible
        System.out.print(-1);
    }
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 4, 1, 6, 2 };

    removeIndicesToMakeSumEqual(arr);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python program to implement
# the above approach

# Function to find indices of array elements
# whose removal makes the sum of odd and
# even indexed array elements equal
def removeIndicesToMakeSumEqual(arr):

    # Stores size of array
    N = len(arr);

    # Store prefix sum of odd
    # index array elements
    odd = [0] * N;

    # Store prefix sum of even
    # index array elements
    even = [0] * N;

    # Update even[0]
    even[0] = arr[0];

    # Traverse the given array
    for i in range(1, N):

        # Update odd[i]
        odd[i] = odd[i - 1];

        # Update even[i]
        even[i] = even[i - 1];

        # If the current index
        # is an even number
        if (i % 2 == 0):

            # Update even[i]
            even[i] += arr[i];

        # If the current index
        # is an odd number
        else:

            # Update odd[i]
            odd[i] += arr[i];

    # Check if at least one
    # index found or not that
    # satisfies the condition
    find = False;

    # Store odd indices sum by
    # removing 0-th index
    p = odd[N - 1];

    # Store even indices sum by
    # removing 0-th index
    q = even[N - 1] - arr[0];

    # If p and q are equal
    if (p == q):
        print("0 ");
        find = True;

    # Traverse the array arr
    for i in range(1, N):

        # If i is an even number
        if (i % 2 == 0):

            # Update p by removing
            # the i-th element
            p = even[N - 1] - even[i - 1] - arr[i] + odd[i - 1];

            # Update q by removing
            # the i-th element
            q = odd[N - 1] - odd[i - 1] + even[i - 1];
        else:

            # Update q by removing
            # the i-th element
            q = odd[N - 1] - odd[i - 1] - arr[i] + even[i - 1];

            # Update p by removing
            # the i-th element
            p = even[N - 1] - even[i - 1] + odd[i - 1];

        # If odd index values sum is equal
        # to even index values sum
        if (p == q):

            # Set the find variable
            find = True;

            # Print the current index
            print(i, end = "");

    # If no index found
    if (find == False):

        # Print not possible
        print(-1);

# Driver Code
if __name__ == '__main__':
    arr = [4, 1, 6, 2];

    removeIndicesToMakeSumEqual(arr);

    # This code is contributed by shikhasingrajput
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to find indices of array elements
// whose removal makes the sum of odd and
// even indexed array elements equal
static void removeIndicesToMakeSumEqual(int []arr)
{

    // Stores size of array
    int N = arr.Length;

    // Store prefix sum of odd
    // index array elements
    int []odd = new int[N];

    // Store prefix sum of even
    // index array elements
    int []even = new int[N];

    // Update even[0]
    even[0] = arr[0];

    // Traverse the given array
    for(int i = 1; i < N; i++)
    {

        // Update odd[i]
        odd[i] = odd[i - 1];

        // Update even[i]
        even[i] = even[i - 1];

        // If the current index
        // is an even number
        if (i % 2 == 0)
        {

            // Update even[i]
            even[i] += arr[i];
        }

        // If the current index
        // is an odd number
        else
        {

            // Update odd[i]
            odd[i] += arr[i];
        }
    }

    // Check if at least one
    // index found or not that
    // satisfies the condition
    bool find = false;

    // Store odd indices sum by
    // removing 0-th index
    int p = odd[N - 1];

    // Store even indices sum by
    // removing 0-th index
    int q = even[N - 1] - arr[0];

    // If p and q are equal
    if (p == q)
    {
        Console.Write("0 ");
        find = true;
    }

    // Traverse the array arr[]
    for(int i = 1; i < N; i++)
    {

        // If i is an even number
        if (i % 2 == 0)
        {

            // Update p by removing
            // the i-th element
            p = even[N - 1] - even[i - 1] -
                     arr[i] + odd[i - 1];

            // Update q by removing
            // the i-th element
            q = odd[N - 1] - odd[i - 1] +
               even[i - 1];
        }
        else
        {

            // Update q by removing
            // the i-th element
            q = odd[N - 1] - odd[i - 1] -
                    arr[i] + even[i - 1];

            // Update p by removing
            // the i-th element
            p = even[N - 1] - even[i - 1] +
                 odd[i - 1];
        }

        // If odd index values sum is equal
        // to even index values sum
        if (p == q)
        {

            // Set the find variable
            find = true;

            // Print the current index
            Console.Write(i + " ");
        }
    }

    // If no index found
    if (!find)
    {

        // Print not possible
        Console.Write(-1);
    }
}

// Driver Code
public static void Main(String[] args)
{
    int[] arr = { 4, 1, 6, 2 };

    removeIndicesToMakeSumEqual(arr);
}
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// javascript program to implement
// the above approach

    // Function to find indices of array elements
    // whose removal makes the sum of odd and
    // even indexed array elements equal
    function removeIndicesToMakeSumEqual(arr) {

        // Stores size of array
        var N = arr.length;

        // Store prefix sum of odd
        // index array elements
        var odd = Array(N).fill(0);

        // Store prefix sum of even
        // index array elements
        var even = Array(N).fill(0);

        // Update even[0]
        even[0] = arr[0];

        // Traverse the given array
        for (i = 1; i < N; i++) {

            // Update odd[i]
            odd[i] = odd[i - 1];

            // Update even[i]
            even[i] = even[i - 1];

            // If the current index
            // is an even number
            if (i % 2 == 0) {

                // Update even[i]
                even[i] += arr[i];
            }

            // If the current index
            // is an odd number
            else {

                // Update odd[i]
                odd[i] += arr[i];
            }
        }

        // Check if at least one
        // index found or not that
        // satisfies the condition
        var find = false;

        // Store odd indices sum by
        // removing 0-th index
        var p = odd[N - 1];

        // Store even indices sum by
        // removing 0-th index
        var q = even[N - 1] - arr[0];

        // If p and q are equal
        if (p == q) {
            document.write("0 ");
            find = true;
        }

        // Traverse the array arr
        for (i = 1; i < N; i++) {

            // If i is an even number
            if (i % 2 == 0) {

                // Update p by removing
                // the i-th element
                p = even[N - 1] - even[i - 1] - arr[i] + odd[i - 1];

                // Update q by removing
                // the i-th element
                q = odd[N - 1] - odd[i - 1] + even[i - 1];
            } else {

                // Update q by removing
                // the i-th element
                q = odd[N - 1] - odd[i - 1] - arr[i] + even[i - 1];

                // Update p by removing
                // the i-th element
                p = even[N - 1] - even[i - 1] + odd[i - 1];
            }

            // If odd index values sum is equal
            // to even index values sum
            if (p == q) {

                // Set the find variable
                find = true;

                // Print the current index
                document.write(i + " ");
            }
        }

        // If no index found
        if (!find) {

            // Print not possible
            document.write(-1);
        }
    }

    // Driver Code

        var arr = [ 4, 1, 6, 2 ];

        removeIndicesToMakeSumEqual(arr);

// This code is contributed by Rajput-Ji
</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)