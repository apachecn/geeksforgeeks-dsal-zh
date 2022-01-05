# 数组中最大和小于 K 的对

> 原文:[https://www . geeksforgeeks . org/与阵列中小于 k 的最大和配对/](https://www.geeksforgeeks.org/pair-with-largest-sum-which-is-less-than-k-in-the-array/)

给定一个大小为 **N** 的数组**和一个整数 **K** 。任务是找到整数对，使得它们的和最大，但小于 **K****

**示例:**

> **输入:** arr = {30，20，50}，K = 70
> **输出:** 30，20
> 30 + 20 = 50，这是小于 K
> 的最大可能和
> 
> **输入:** arr = {5，20，110，100，10}，K = 85
> **输出:** 20，10

**方法:**
一种有效的方法是[对给定数组进行](https://www.geeksforgeeks.org/sort-c-stl/)排序，找到大于或等于 **K** 的元素。如果在索引 **p** 处找到，我们必须只在**arr【0，…，p-1】**之间找到配对。运行嵌套循环。一个负责该对中的第一个元素，另一个负责该对中的第二个元素。维护一个变量 **maxsum** 和另外两个变量 **a** 和 **b** 来跟踪可能的解决方案。将 **maxsum** 初始化为 **0** 。求 **A[i] + A[j]** (假设我在外环跑，j 在内环跑)。如果大于 **maxsum** ，则用该和更新 **maxsum** ，并将 **a** 和 **b** 更改为此数组的第 I 个和第 j 个元素。
以下是上述方法的实施:

## C++

```
// CPP program to find pair with largest
// sum which is less than K in the array
#include <bits/stdc++.h>
using namespace std;

// Function to find pair with largest
// sum which is less than K in the array
void Max_Sum(int arr[], int n, int k)
{
    // To store the break point
    int  p = n;

    // Sort the given array
    sort(arr, arr + n);

    // Find the break point
    for (int i = 0; i < n; i++)
    {
         // No need to look beyond i'th index
        if (arr[i] >= k) {
            p = i;
            break;
        }
    }

    int maxsum = 0, a, b;

    // Find the required pair
    for (int i = 0; i < p; i++)
    {
        for (int j = i + 1; j < p; j++)
        {
            if (arr[i] + arr[j] < k and arr[i] + arr[j] >
                                                     maxsum)
            {
                maxsum = arr[i] + arr[j];

                a = arr[i];
                b = arr[j];
            }
        }
    }

    // Print the required answer
    cout << a << " " << b;
}

// Driver code
int main()
{
    int arr[] = {5, 20, 110, 100, 10}, k = 85;

    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    Max_Sum(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find pair with largest
// sum which is less than K in the array
import java.util.Arrays;

class GFG
{

// Function to find pair with largest
// sum which is less than K in the array
static void Max_Sum(int arr[], int n, int k)
{
    // To store the break point
    int p = n;

    // Sort the given array
    Arrays.sort(arr);

    // Find the break point
    for (int i = 0; i < n; i++)
    {
        // No need to look beyond i'th index
        if (arr[i] >= k)
        {
            p = i;
            break;
        }
    }

    int maxsum = 0, a = 0, b = 0;

    // Find the required pair
    for (int i = 0; i < p; i++)
    {
        for (int j = i + 1; j < p; j++)
        {
            if (arr[i] + arr[j] < k &&
                arr[i] + arr[j] > maxsum)
            {
                maxsum = arr[i] + arr[j];

                a = arr[i];
                b = arr[j];
            }
        }
    }

    // Print the required answer
    System.out.print( a + " " + b);
}

// Driver code
public static void main (String[] args)
{
    int []arr = {5, 20, 110, 100, 10};
    int k = 85;

    int n = arr.length;

    // Function call
    Max_Sum(arr, n, k);
}
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 program to find pair with largest
# sum which is less than K in the array

# Function to find pair with largest
# sum which is less than K in the array
def Max_Sum(arr, n, k):

    # To store the break point
    p = n

    # Sort the given array
    arr.sort()

    # Find the break point
    for i in range(0, n):

        # No need to look beyond i'th index
        if (arr[i] >= k):
            p = i
            break

    maxsum = 0
    a = 0
    b = 0

    # Find the required pair
    for i in range(0, p):    
        for j in range(i + 1, p):
            if(arr[i] + arr[j] < k and
               arr[i] + arr[j] > maxsum):
                maxsum = arr[i] + arr[j]
                a = arr[i]
                b = arr[j]

    # Print the required answer
    print(a, b)

# Driver code
arr = [5, 20, 110, 100, 10]
k = 85

n = len(arr)

# Function call
Max_Sum(arr, n, k)

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# program to find pair with largest
// sum which is less than K in the array
using System;

class GFG
{

// Function to find pair with largest
// sum which is less than K in the array
static void Max_Sum(int []arr, int n, int k)
{
    // To store the break point
    int p = n;

    // Sort the given array
    Array.Sort(arr);

    // Find the break point
    for (int i = 0; i < n; i++)
    {
        // No need to look beyond i'th index
        if (arr[i] >= k)
        {
            p = i;
            break;
        }
    }

    int maxsum = 0, a = 0, b = 0;

    // Find the required pair
    for (int i = 0; i < p; i++)
    {
        for (int j = i + 1; j < p; j++)
        {
            if (arr[i] + arr[j] < k &&
                arr[i] + arr[j] > maxsum)
            {
                maxsum = arr[i] + arr[j];

                a = arr[i];
                b = arr[j];
            }
        }
    }

    // Print the required answer
    Console.WriteLine( a + " " + b);
}

// Driver code
public static void Main ()
{
    int []arr = {5, 20, 110, 100, 10};
    int k = 85;

    int n = arr.Length;

    // Function call
    Max_Sum(arr, n, k);
}
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>
    // Javascript program to find pair with largest
    // sum which is less than K in the array

    // Function to find pair with largest
    // sum which is less than K in the array
    function Max_Sum(arr, n, k)
    {
        // To store the break point
        let p = n;

        // Sort the given array
        arr.sort(function(a, b){return a - b});

        // Find the break point
        for (let i = 0; i < n; i++)
        {
            // No need to look beyond i'th index
            if (arr[i] >= k)
            {
                p = i;
                break;
            }
        }

        let maxsum = 0, a = 0, b = 0;

        // Find the required pair
        for (let i = 0; i < p; i++)
        {
            for (let j = i + 1; j < p; j++)
            {
                if (arr[i] + arr[j] < k &&
                    arr[i] + arr[j] > maxsum)
                {
                    maxsum = arr[i] + arr[j];

                    a = arr[i];
                    b = arr[j];
                }
            }
        }

        // Print the required answer
        document.write( a + " " + b + "</br>");
    }

    let arr = [5, 20, 110, 100, 10];
    let k = 85;

    let n = arr.length;

    // Function call
    Max_Sum(arr, n, k);

</script>
```

**Output**

```
10 20
```

**时间复杂度:** O(N^2)

**高效方法:**双指针法
排序后，我们可以在数组的左右两端放置两个指针。通过以下步骤可以找到所需的配对:

1.  找出这两个指针值的当前总和。
2.  如果总和小于 k:
    1.  用先前答案和当前总和的最大值更新答案。
    2.  增加左指针。
3.  否则减小右指针。

## C++

```
// CPP program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find max sum less than k
int maxSum(vector<int> arr, int k)
{

    // Sort the array
    sort(arr.begin(), arr.end());
    int n = arr.size(), l = 0, r = n - 1, ans = 0;

    // While l is less than r
    while (l < r) {
        if (arr[l] + arr[r] < k) {
            ans = max(ans, arr[l] + arr[r]);
            l++;
        }
        else {
            r--;
        }
    }

    return ans;
}

// Driver Code
int main()
{
    vector<int> A = { 20, 10, 30, 100, 110 };
    int k = 85;

    // Function Call
    cout << maxSum(A, k) << endl;
}
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to find max sum less than k
static int maxSum(int[] arr, int k)
{

    // Sort the array
    Array.Sort(arr);
    int n = arr.Length, l = 0, r = n - 1, ans = 0;

    // While l is less than r
    while (l < r) {
        if (arr[l] + arr[r] < k) {
            ans = Math.Max(ans, arr[l] + arr[r]);
            l++;
        }
        else {
            r--;
        }
    }

    return ans;
}

// Driver code
public static void Main ()
{
    int[] A = { 20, 10, 30, 100, 110 };
    int k = 85;

    // Function Call
    Console.WriteLine(maxSum(A, k));
}
}

// This code is contributed by target_2.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find max sum less than k
function maxSum(arr, k)
{

    // Sort the array
    arr.sort((a,b)=>a-b);
    var n = arr.length, l = 0, r = n - 1, ans = 0;

    // While l is less than r
    while (l < r) {
        if (arr[l] + arr[r] < k) {
            ans = Math.max(ans, arr[l] + arr[r]);
            l++;
        }
        else {
            r--;
        }
    }

    return ans;
}

// Driver Code
var A = [20, 10, 30, 100, 110];
var k = 85;
// Function Call
document.write( maxSum(A, k));

</script>
```

**Output**

```
50
```

**时间复杂度** : O(NlogN)

**空间复杂度** : O(1)