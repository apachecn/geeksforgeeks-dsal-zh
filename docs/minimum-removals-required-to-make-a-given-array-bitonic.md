# 使给定阵列双离子化所需的最小移除量

> 原文:[https://www . geeksforgeeks . org/minimum-removes-需要制作给定阵列-bitonic/](https://www.geeksforgeeks.org/minimum-removals-required-to-make-a-given-array-bitonic/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是找到需要从数组中移除的最小数组元素数，从而将给定的数组转换为[双音素数组](https://www.geeksforgeeks.org/program-to-check-if-an-array-is-bitonic-or-not/)。

**示例:**

> **输入:** arr[] = { 2，1，1，5，6，2，3，1 }
> **输出:** 3
> **解释:**
> 移除 arr[0]，arr[1]和 arr[5]将 arr[]修改为{ 1，5，6，3，1 }
> 由于数组元素遵循先增后减的顺序，因此所需的输出为 3。
> 
> **输入:** arr[] = { 1，3，1 }
> **输出:** 0
> **解释:**
> 给定的数组已经是双离子数组了。因此，所需的输出为 3。

**方法:**问题可以基于[最长递增子序列问题](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/)的概念来解决。按照以下步骤解决问题:

*   初始化一个变量，比如说**left【】**，这样**left【I】**存储**最长递增子序列** ce 到 **i <sup>th</sup>** 索引的长度。
*   初始化一个变量，比如说 **right[]** ，这样 **right[i]** 存储**最长递减子序列**在**【I，N】**范围内的长度。
*   使用变量 **i** 遍历**左[]** 和**右[]** 数组，找到**(左[i] +右[I]–1)**的最大值，并将其存储在一个变量中，比如 **maxLen** 。
*   最后，打印**N–maxLen**的值。

下面是上述方法的实现:

## C++14

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to coutnt minimum array elements
// required to be removed to make an array bitonic
void min_element_removal(int arr[], int N)
{
    // left[i]: Stores the length
    // of LIS up to i-th index
    vector<int> left(N, 1);

    // right[i]: Stores the length
    // of decreasing subsequence
    // over the range [i, N]
    vector<int> right(N, 1);

    // Calculate the length of LIS
    // up to i-th index
    for (int i = 1; i < N; i++) {

        // Traverse the array
        // upto i-th index
        for (int j = 0; j < i; j++) {

            // If arr[j] is less than arr[i]
            if (arr[j] < arr[i]) {

                // Update left[i]
                left[i] = max(left[i],
                              left[j] + 1);
            }
        }
    }

    // Calculate the length of decreasing
    // subsequence over the range [i, N]
    for (int i = N - 2; i >= 0;
         i--) {

        // Traverse right[] array
        for (int j = N - 1; j > i;
             j--) {

            // If arr[i] is greater
            // than arr[j]
            if (arr[i] > arr[j]) {

                // Update right[i]
                right[i] = max(right[i],
                               right[j] + 1);
            }
        }
    }

    // Stores length of the
    // longest bitonic array
    int maxLen = 0;

    // Traverse left[] and right[] array
    for (int i = 1; i < N - 1; i++) {

        // Update maxLen
        maxLen = max(maxLen, left[i] + right[i] - 1);
    }

    cout << (N - maxLen) << "\n";
}

// Function to print minimum removals
// required to make given array bitonic
void makeBitonic(int arr[], int N)
{
    if (N == 1) {
        cout << "0" << endl;
        return;
    }

    if (N == 2) {
        if (arr[0] != arr[1])
            cout << "0" << endl;
        else
            cout << "1" << endl;

        return;
    }

    min_element_removal(arr, N);
}

// Driver Code
int main()
{
    int arr[] = { 2, 1, 1, 5, 6, 2, 3, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);

    makeBitonic(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG {

    // Function to coutnt minimum array elements
    // required to be removed to make an array bitonic
    static void min_element_removal(int arr[], int N)
    {
        // left[i]: Stores the length
        // of LIS up to i-th index
        int left[] = new int[N];

        for(int i = 0; i < N; i++)
            left[i] = 1;

        // right[i]: Stores the length
        // of decreasing subsequence
        // over the range [i, N]
        int right[] = new int[N];

        for(int i = 0; i < N; i++)
            right[i] = 1;

        // Calculate the length of LIS
        // up to i-th index
        for (int i = 1; i < N; i++) {

            // Traverse the array
            // upto i-th index
            for (int j = 0; j < i; j++) {

                // If arr[j] is less than arr[i]
                if (arr[j] < arr[i]) {

                    // Update left[i]
                    left[i] = Math.max(left[i],
                                  left[j] + 1);
                }
            }
        }

        // Calculate the length of decreasing
        // subsequence over the range [i, N]
        for (int i = N - 2; i >= 0;
             i--) {

            // Traverse right[] array
            for (int j = N - 1; j > i;
                 j--) {

                // If arr[i] is greater
                // than arr[j]
                if (arr[i] > arr[j]) {

                    // Update right[i]
                    right[i] = Math.max(right[i],
                                   right[j] + 1);
                }
            }
        }

        // Stores length of the
        // longest bitonic array
        int maxLen = 0;

        // Traverse left[] and right[] array
        for (int i = 1; i < N - 1; i++) {

            // Update maxLen
            maxLen = Math.max(maxLen, left[i] + right[i] - 1);
        }

        System.out.println(N - maxLen);
    }

    // Function to print minimum removals
    // required to make given array bitonic
    static void makeBitonic(int arr[], int N)
    {
        if (N == 1) {
            System.out.println("0");
            return;
        }

        if (N == 2) {
            if (arr[0] != arr[1])
                System.out.println("0");
            else
                System.out.println("1");

            return;
        }

        min_element_removal(arr, N);
    }

    // Driver Code
    public static void main (String[] args) {

        int arr[] = { 2, 1, 1, 5, 6, 2, 3, 1 };

        int N = arr.length;

        makeBitonic(arr, N);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to coutnt minimum array elements
# required to be removed to make an array bitonic
def min_element_removal(arr, N):

    # left[i]: Stores the length
    # of LIS up to i-th index
    left = [1] * N

    # right[i]: Stores the length
    # of decreasing subsequence
    # over the range [i, N]
    right = [1] * (N)

    #Calculate the length of LIS
    #up to i-th index
    for i in range(1, N):

        #Traverse the array
        #upto i-th index
        for j in range(i):

            #If arr[j] is less than arr[i]
            if (arr[j] < arr[i]):

                #Update left[i]
                left[i] = max(left[i], left[j] + 1)

    # Calculate the length of decreasing
    # subsequence over the range [i, N]
    for i in range(N - 2, -1, -1):

        # Traverse right[] array
        for j in range(N - 1, i, -1):

            # If arr[i] is greater
            # than arr[j]
            if (arr[i] > arr[j]):

                # Update right[i]
                right[i] = max(right[i], right[j] + 1)

    # Stores length of the
    # longest bitonic array
    maxLen = 0

    # Traverse left[] and right[] array
    for i in range(1, N - 1):

        # Update maxLen
        maxLen = max(maxLen, left[i] + right[i] - 1)

    print((N - maxLen))

# Function to prminimum removals
# required to make given array bitonic
def makeBitonic(arr, N):
    if (N == 1):
        print("0")
        return

    if (N == 2):
        if (arr[0] != arr[1]):
            print("0")
        else:
            print("1")

        return

    min_element_removal(arr, N)

# Driver Code
if __name__ == '__main__':
    arr=[2, 1, 1, 5, 6, 2, 3, 1]
    N = len(arr)

    makeBitonic(arr, N)

    # This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to coutnt minimum array elements
// required to be removed to make an array bitonic
static void min_element_removal(int []arr, int N)
{

    // left[i]: Stores the length
    // of LIS up to i-th index
    int []left = new int[N];

    for(int i = 0; i < N; i++)
        left[i] = 1;

    // right[i]: Stores the length
    // of decreasing subsequence
    // over the range [i, N]
    int []right = new int[N];

    for(int i = 0; i < N; i++)
        right[i] = 1;

    // Calculate the length of LIS
    // up to i-th index
    for(int i = 1; i < N; i++)
    {

        // Traverse the array
        // upto i-th index
        for(int j = 0; j < i; j++)
        {

            // If arr[j] is less than arr[i]
            if (arr[j] < arr[i])
            {

                // Update left[i]
                left[i] = Math.Max(left[i],
                                   left[j] + 1);
            }
        }
    }

    // Calculate the length of decreasing
    // subsequence over the range [i, N]
    for(int i = N - 2; i >= 0; i--)
    {

        // Traverse right[] array
        for(int j = N - 1; j > i; j--)
        {

            // If arr[i] is greater
            // than arr[j]
            if (arr[i] > arr[j])
            {

                // Update right[i]
                right[i] = Math.Max(right[i],
                                    right[j] + 1);
            }
        }
    }

    // Stores length of the
    // longest bitonic array
    int maxLen = 0;

    // Traverse left[] and right[] array
    for(int i = 1; i < N - 1; i++)
    {

        // Update maxLen
        maxLen = Math.Max(maxLen, left[i] +
                                 right[i] - 1);
    }
    Console.WriteLine(N - maxLen);
}

// Function to print minimum removals
// required to make given array bitonic
static void makeBitonic(int []arr, int N)
{
    if (N == 1)
    {
        Console.WriteLine("0");
        return;
    }

    if (N == 2)
    {
        if (arr[0] != arr[1])
            Console.WriteLine("0");
        else
            Console.WriteLine("1");

        return;
    }
    min_element_removal(arr, N);
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 2, 1, 1, 5, 6, 2, 3, 1 };
    int N = arr.Length;

    makeBitonic(arr, N);
}
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to coutnt minimum array elements
// required to be removed to make an array bitonic
function min_element_removal(arr, N)
{
    // left[i]: Stores the length
    // of LIS up to i-th index
    var left = Array(N).fill(1);

    // right[i]: Stores the length
    // of decreasing subsequence
    // over the range [i, N]
    var right = Array(N).fill(1);

    // Calculate the length of LIS
    // up to i-th index
    for (var i = 1; i < N; i++) {

        // Traverse the array
        // upto i-th index
        for (var j = 0; j < i; j++) {

            // If arr[j] is less than arr[i]
            if (arr[j] < arr[i]) {

                // Update left[i]
                left[i] = Math.max(left[i],
                              left[j] + 1);
            }
        }
    }

    // Calculate the length of decreasing
    // subsequence over the range [i, N]
    for (var i = N - 2; i >= 0;
         i--) {

        // Traverse right[] array
        for (var j = N - 1; j > i;
             j--) {

            // If arr[i] is greater
            // than arr[j]
            if (arr[i] > arr[j]) {

                // Update right[i]
                right[i] = Math.max(right[i],
                               right[j] + 1);
            }
        }
    }

    // Stores length of the
    // longest bitonic array
    var maxLen = 0;

    // Traverse left[] and right[] array
    for (var i = 1; i < N - 1; i++) {

        // Update maxLen
        maxLen = Math.max(maxLen, left[i] + right[i] - 1);
    }

    document.write((N - maxLen) + "<br>");
}

// Function to print minimum removals
// required to make given array bitonic
function makeBitonic(arr, N)
{
    if (N == 1) {
        document.write( "0" + "<br>");
        return;
    }

    if (N == 2) {
        if (arr[0] != arr[1])
            document.write( "0" + "<br>");
        else
            document.write( "1" + "<br>");

        return;
    }

    min_element_removal(arr, N);
}

// Driver Code
var arr = [2, 1, 1, 5, 6, 2, 3, 1];
var N = arr.length;
makeBitonic(arr, N);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*