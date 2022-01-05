# 数组中同时存在正负值的最大数字

> 原文:[https://www . geeksforgeeks . org/数组中同时存在正负值的最大数/](https://www.geeksforgeeks.org/largest-number-having-both-positive-and-negative-values-present-in-the-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到最大的数 **K** ( *> 0* )使得值 **K** 和 **-K** 都出现在给定数组 **arr[]** 。如果没有，则打印 **-1** 。

**示例:**

> **输入:** arr[] = {3，2，-2，5，-3 }
> T3】输出: 3
> 
> **输入:** arr[] = {1，2，3，-4}
> **输出:** -1

**天真方法:**解决给定问题的最简单方法是[迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，对于每个元素，遍历剩余的数组，检查其负值是否存在于数组中。完成数组遍历后，打印得到的最大值。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方式:**上述方式可以通过[排序](https://www.geeksforgeeks.org/sorting-algorithms/)和[两个指针](https://www.geeksforgeeks.org/two-pointers-technique/)进行优化。按照以下步骤解决此问题:

*   初始化一个变量，说 **res** 为 **-1** ，存储获得的最大元素。
*   [给定数组排序 **arr[]**](https://www.geeksforgeeks.org/quick-sort/) 。
*   初始化两个变量，将 **l** 和 **r** 设为 **0** 和**(N–1)**，并执行以下步骤:
    *   如果 **(arr[l] + arr[r])** 的值等于 **0** ，则返回 **arr[l]** 和 **arr[r]** 的[绝对值。](https://www.geeksforgeeks.org/abs-labs-llabs-functions-cc/)
    *   否则，如果 **(arr[l] + arr[r])** 的值小于 **0** ，则将 **l** 的值增加 **1** 。
    *   否则，将 **r** 的值递减 **1** 。
*   完成上述步骤后，打印 **res** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find the largest
// number k such that both k and
// -k are present in the array
int largestNum(vector<int>arr)
{

    // Stores the resultant value
    // of K
    int res = 0;

    // Sort the array arr[]
    sort(arr.begin(), arr.end());

    // Initialize two variables to
    // use two pointers technique
    int l = 0, r = arr.size() - 1;

    // Iterate until the value of
    // l is less than r
    while (l < r)
    {

        // Find the value of the sum
        int sum = arr[l] + arr[r];

        // If the sum is 0, then the
        // resultant element is found
        if (sum == 0)
        {
            res = max(res, max(arr[l], arr[r]));
            return res;
        }

        // If the sum is negative
        else if (sum < 0)
        {
            l++;
        }

        // Otherwise, decrement r
        else
        {
            r--;
        }
    }
    return res;
}

// Driver Code
int main()
{
    vector<int>arr = { 3, 2, -2, 5, -3 };
    cout << (largestNum(arr));
}

// This code is contributed by amreshkumar3
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

public class GFG {

    // Function to find the largest
    // number k such that both k and
    // -k are present in the array
    public static int largestNum(int[] arr)
    {
        // Stores the resultant value
        // of K
        int res = 0;

        // Sort the array arr[]
        Arrays.sort(arr);

        // Initialize two variables to
        // use two pointers technique
        int l = 0, r = arr.length - 1;

        // Iterate until the value of
        // l is less than r
        while (l < r) {

            // Find the value of the sum
            int sum = arr[l] + arr[r];

            // If the sum is 0, then the
            // resultant element is found
            if (sum == 0) {
                res = Math.max(
                    res, Math.max(
                             arr[l], arr[r]));

                return res;
            }

            // If the sum is negative
            else if (sum < 0) {
                l++;
            }

            // Otherwise, decrement r
            else {
                r--;
            }
        }

        return res;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 3, 2, -2, 5, -3 };
        System.out.println(
            largestNum(arr));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the largest
# number k such that both k and
# -k are present in the array
def largestNum(arr):

    # Stores the resultant value
    # of K
    res = 0

    # Sort the array arr[]
    arr = sorted(arr)

    # Initialize two variables to
    # use two pointers technique
    l = 0
    r = len(arr) - 1

    # Iterate until the value of
    # l is less than r
    while (l < r):

        # Find the value of the sum
        sum = arr[l] + arr[r]

        # If the sum is 0, then the
        # resultant element is found
        if (sum == 0):
            res = max(res, max(arr[l], arr[r]))

            return res

        # If the sum is negative
        elif (sum < 0):
            l += 1

        # Otherwise, decrement r
        else:
            r-=1

    return res

# Driver Code
if __name__ == '__main__':
    arr =[3, 2, -2, 5, -3]
    print(largestNum(arr))

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the largest
// number k such that both k and
// -k are present in the array
static int largestNum(List<int>arr)
{

    // Stores the resultant value
    // of K
    int res = 0;

    // Sort the array arr[]
    arr.Sort();

    // Initialize two variables to
    // use two pointers technique
    int l = 0, r = arr.Count - 1;

    // Iterate until the value of
    // l is less than r
    while (l < r)
    {

        // Find the value of the sum
        int sum = arr[l] + arr[r];

        // If the sum is 0, then the
        // resultant element is found
        if (sum == 0)
        {
            res = Math.Max(res, Math.Max(arr[l],
                                         arr[r]));
            return res;
        }

        // If the sum is negative
        else if (sum < 0)
        {
            l++;
        }

        // Otherwise, decrement r
        else
        {
            r--;
        }
    }
    return res;
}

// Driver Code
public static void Main()
{
    List<int>arr = new List<int>(){ 3, 2, -2, 5, -3 };
    Console.Write(largestNum(arr));
}
}

// This code is contributed by bgangwar59
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the largest
// number k such that both k and
// -k are present in the array
function largestNum(arr) {

    // Stores the resultant value
    // of K
    let res = 0;

    // Sort the array arr[]
    arr.sort((a, b) => a - b);

    // Initialize two variables to
    // use two pointers technique
    let l = 0, r = arr.length - 1;

    // Iterate until the value of
    // l is less than r
    while (l < r) {

        // Find the value of the sum
        let sum = arr[l] + arr[r];

        // If the sum is 0, then the
        // resultant element is found
        if (sum == 0) {
            res = Math.max(res, Math.max(arr[l], arr[r]));
            return res;
        }

        // If the sum is negative
        else if (sum < 0) {
            l++;
        }

        // Otherwise, decrement r
        else {
            r--;
        }
    }
    return res;
}

// Driver Code

let arr = [3, 2, -2, 5, -3];
document.write((largestNum(arr)));

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*

**优化方法:**通过将元素存储到[集合](https://www.geeksforgeeks.org/hashset-in-java/)中，可以进一步优化上述方法。按照以下步骤解决此问题:

*   初始化一个存储数组元素的[集合](https://www.geeksforgeeks.org/hashset-in-java/) **S** 。
*   初始化一个变量，说 **res** 为 **-1** 来存储[最大元素，同时遍历数组](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–1】**，并执行以下步骤:
    *   将当前元素添加到设置 **S** 中。
    *   如果元素存在，则将 **res** 的值更新为当前元素。
*   完成上述步骤后，打印 **res** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find the largest
// number k such that both k and
// -k are present in the array
int largestNum(int arr[] ,int n)
{

    // Stores the array elements
    set<int> st;

    // Initialize a variable res as
    // 0 to store maximum element
    // while traversing the array
    int res = 0;

    // Iterate through array arr
    for(int i = 0; i < n; i++)
    {

        // Add the current element
        // into the st
        st.insert(arr[i]);

        // Check if the negative of
        // this element is also
        // present in the st or not
        if (st.find(-1 * arr[i]) != st.end())
        {
            res = max(res, abs(arr[i]));
        }
    }

    // Return the resultant element
    return res;
}

// Drive Code
int main()
{
    int arr[] = { 3, 2, -2, 5, -3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << largestNum(arr, n);
}

// This code is contributed by SURENDRA_GANGWAR
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to find the largest
    // number k such that both k and
    // -k are present in the array
    public static int largestNum(int[] arr)
    {
        // Stores the array elements
        Set<Integer> set = new HashSet<>();

        // Initialize a variable res as
        // 0 to store maximum element
        // while traversing the array
        int res = 0;

        // Iterate through array arr
        for (int i = 0;
             i < arr.length; i++) {

            // Add the current element
            // into the set
            set.add(arr[i]);

            // Check if the negative of
            // this element is also
            // present in the set or not
            if (set.contains(-1 * arr[i])) {

                res = Math.max(
                    res, Math.abs(arr[i]));
            }
        }

        // Return the resultant element
        return res;
    }

    // Drive Code
    public static void
        main(String[] args)
    {

        int[] arr = { 3, 2, -2, 5, -3 };
        System.out.println(
            largestNum(arr));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the largest
# number k such that both k and
# -k are present in the array
def largestNum(arr, n) :

    # Stores the array elements
    st = set([])

    # Initialize a variable res as
    # 0 to store maximum element
    # while traversing the array
    res = 0

    # Iterate through array arr
    for i in range(n):

        # Add the current element
        # into the st
        st.add(arr[i])

        # Check if the negative of
        # this element is also
        # present in the st or not
        if (-1 * arr[i]) in st:

            res = max(res, abs(arr[i]))

    # Return the resultant element
    return res

arr = [ 3, 2, -2, 5, -3 ]
n = len(arr)

print(largestNum(arr, n))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG{

    // Function to find the largest
    // number k such that both k and
    // -k are present in the array
    public static int largestNum(int[] arr)
    {
        // Stores the array elements
        HashSet<int> set = new HashSet<int>();

        // Initialize a variable res as
        // 0 to store maximum element
        // while traversing the array
        int res = 0;

        // Iterate through array arr
        for (int i = 0;
             i < arr.Length; i++) {

            // Add the current element
            // into the set
            set.Add(arr[i]);

            // Check if the negative of
            // this element is also
            // present in the set or not
            if (set.Contains(-1 * arr[i])) {

                res = Math.Max(
                    res, Math.Abs(arr[i]));
            }
        }

        // Return the resultant element
        return res;
    }

    // Drive Code

    static public void Main (){

        int[] arr = { 3, 2, -2, 5, -3 };
        Console.WriteLine(
            largestNum(arr));

    }
}

// This code is contributed by unknown2108
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

 // Function to find the largest
    // number k such that both k and
    // -k are present in the array
function largestNum(arr)
{
    // Stores the array elements
        let set = new Set();

        // Initialize a variable res as
        // 0 to store maximum element
        // while traversing the array
        let res = 0;

        // Iterate through array arr
        for (let i = 0;
             i < arr.length; i++) {

            // Add the current element
            // into the set
            set.add(arr[i]);

            // Check if the negative of
            // this element is also
            // present in the set or not
            if (set.has(-1 * arr[i])) {

                res = Math.max(
                    res, Math.abs(arr[i]));
            }
        }

        // Return the resultant element
        return res;
}

// Drive Code
let arr=[3, 2, -2, 5, -3 ];
document.write(largestNum(arr));

// This code is contributed by patel2127

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)