# 检查数组是否可以拆分为子数组，使得这些子数组的最长递减子序列的长度的异或为 0

> 原文:[https://www . geeksforgeeks . org/check-if-array-can-split-in-subarray-so-xor-of-length-最长递减子序列-这些子阵列-是-0/](https://www.geeksforgeeks.org/check-if-array-can-be-split-into-subarrays-such-that-xor-of-length-of-longest-decreasing-subsequences-of-those-subarrays-is-0/)

给定大小为 **N、**的整数**arr【】**的[数组](https://www.geeksforgeeks.org/array-data-structure/)，任务是检查**arr【】**是否可以分割成不同的[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，使得在对所有子阵列的 [LDS(最长递减子序列)](https://www.geeksforgeeks.org/longest-decreasing-subsequence/)的长度进行[异或](http://www.geeksforgeeks.org/calculate-xor-1-n/)时等于 **0** 。打印'**是**'如果可以拆分其他打印'**否**。

**示例:**

> ***输入:*** arr[] = {1，0，3，4，5}
> ***输出:*** YES
> ***解释:*** {1}、{0}、{3}、{4，5}子阵列的 LDS 长度:1，1，1，1，长度的 XOR = 0。所以答案是肯定的。
> 
> ***输入:*** arr[] = {5，4，3}
> ***输出:*** 否

**逼近:**偶数 **1 的**的异或运算为 **0。**所以如果数组长度是偶数，那么每个元素可以被认为是大小为 **1** 的 LDS，这使得偶数 **1 的**的异或等于 **0** 的异或，对于奇数长度的数组具有偶数 LDS 的 **1 的**任何大小为 **2** 的子数组都可以被认为是 LDS，即子数组应该严格增加，所以 LDS 将是 **1** 。按照以下步骤解决问题:

*   初始化一个变量**发现**为**假。**
*   如果 **N** 为偶数则打印**‘是’**并返回。
*   否则，[使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/) **(0，N–1)**，并执行以下任务:
    *   通过 **arr[i] > arr[i-1]** 检查是否有连续增加的元素
    *   如果 **arr[i] > arr[i-1]** 使**发现**为**真**并脱离循环
*   如果**发现**是**真**打印**“是”**否则打印**“否”**

下面是上述方法的实现。

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find XOR of LDS's
// of subarrays
void xor_of_lds(int arr[], int n)
{

    // If length is even each element
    // can be considered as lds of length
    // 1 which makes even 1's and xor is 0
    if (n % 2 == 0) {
        cout << "YES" << endl;
        return;
    }
    else {

        // For odd length we need to find
        // even subarray of length 2 which
        // is strictly increasing so that it
        // makes a subarray with lds=1

        bool found = 0;
        for (int i = 1; i < n; i++) {

            // Check if there are 2
            // consecutive increasing elements
            if (arr[i] > arr[i - 1]) {
                found = 1;
                break;
            }
        }
        if (found == 1)
            cout << "YES" << endl;
        else
            cout << "NO" << endl;
    }
}

// Driver Code
int main()
{

    // Initializing array of arr
    int arr[] = { 1, 0, 3, 4, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Call the function
    xor_of_lds(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.*;
class GFG{

// Function to find XOR of LDS's
// of subarrays
static void xor_of_lds(int arr[], int n)
{

    // If length is even each element
    // can be considered as lds of length
    // 1 which makes even 1's and xor is 0
    if (n % 2 == 0) {
        System.out.print("YES" +"\n");
        return;
    }
    else {

        // For odd length we need to find
        // even subarray of length 2 which
        // is strictly increasing so that it
        // makes a subarray with lds=1

        boolean found = false;
        for (int i = 1; i < n; i++) {

            // Check if there are 2
            // consecutive increasing elements
            if (arr[i] > arr[i - 1]) {
                found = true;
                break;
            }
        }
        if (found == true)
            System.out.print("YES" +"\n");
        else
            System.out.print("NO" +"\n");
    }
}

// Driver Code
public static void main(String[] args)
{

    // Initializing array of arr
    int arr[] = { 1, 0, 3, 4, 5 };
    int N = arr.length;

    // Call the function
    xor_of_lds(arr, N);

}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to find XOR of LDS's
# of subarrays
def xor_of_lds  (arr, n) :

    # If length is even each element
    # can be considered as lds of length
    # 1 which makes even 1's and xor is 0
    if (n % 2 == 0):
        print("YES")
        return
    else:

        # For odd length we need to find
        # even subarray of length 2 which
        # is strictly increasing so that it
        # makes a subarray with lds=1

        found = 0
        for i in range(1, n):
            # Check if there are 2
            # consecutive increasing elements
            if (arr[i] > arr[i - 1]):
                found = 1
                break
        if (found == 1):
            print("YES")
        else:
            print("NO")

# Driver Code
# Initializing array of arr
arr = [1, 0, 3, 4, 5]
N = len(arr)

# Call the function
xor_of_lds(arr, N)

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# code for the above approach
using System;

class GFG
{

// Function to find XOR of LDS's
// of subarrays
static void xor_of_lds(int []arr, int n)
{

    // If length is even each element
    // can be considered as lds of length
    // 1 which makes even 1's and xor is 0
    if (n % 2 == 0) {
        Console.Write("YES" + "\n");
        return;
    }
    else {

        // For odd length we need to find
        // even subarray of length 2 which
        // is strictly increasing so that it
        // makes a subarray with lds=1

        bool found = false;
        for (int i = 1; i < n; i++) {

            // Check if there are 2
            // consecutive increasing elements
            if (arr[i] > arr[i - 1]) {
                found = true;
                break;
            }
        }
        if (found == true)
            Console.Write("YES" +"\n");
        else
            Console.Write("NO" +"\n");
    }
}

// Driver Code
public static void Main()
{

    // Initializing array of arr
    int []arr = { 1, 0, 3, 4, 5 };
    int N = arr.Length;

    // Call the function
    xor_of_lds(arr, N);
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
    // JavaScript code for the above approach

    // Function to find XOR of LDS's
    // of subarrays
    const xor_of_lds = (arr, n) => {

        // If length is even each element
        // can be considered as lds of length
        // 1 which makes even 1's and xor is 0
        if (n % 2 == 0) {
            document.write("YES<br/>");
            return;
        }
        else {

            // For odd length we need to find
            // even subarray of length 2 which
            // is strictly increasing so that it
            // makes a subarray with lds=1

            let found = 0;
            for (let i = 1; i < n; i++) {

                // Check if there are 2
                // consecutive increasing elements
                if (arr[i] > arr[i - 1]) {
                    found = 1;
                    break;
                }
            }
            if (found == 1)
                document.write("YES<br/>");
            else
                document.write("NO<br/>");
        }
    }

    // Driver Code
    // Initializing array of arr
    let arr = [1, 0, 3, 4, 5];
    let N = arr.length;

    // Call the function
    xor_of_lds(arr, N);

    // This code is contributed by rakeshsahni
</script>
```

**Output**

```
YES
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)