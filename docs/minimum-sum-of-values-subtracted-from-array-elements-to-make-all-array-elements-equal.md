# 从数组元素中减去的值的最小和，使所有数组元素相等

> 原文:[https://www . geeksforgeeks . org/最小值-从数组元素中减去-使所有数组元素相等/](https://www.geeksforgeeks.org/minimum-sum-of-values-subtracted-from-array-elements-to-make-all-array-elements-equal/)

给定一个由正整数 **N** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找出需要从每个数组元素中减去的所有数组元素的和，使得剩余的数组元素都相等。

**示例:**

> **输入:** arr[] = {1，2}
> **输出:** 1
> **解释:**从 arr[1]中减去 1 将 arr[]修改为{1，1}。因此，所需的总和为 1。
> 
> **输入:** arr[] = {1，2，3}
> **输出:** 3
> **解释:**从 arr[1]和 arr[2]中减去 1 和 2 将 arr[]修改为{1，1，1}。因此，所需的总和= 1 + 2 = 3。

**方法:**想法是将所有数组元素减少到数组中存在的[最小元素。按照以下步骤解决问题:](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/)

*   初始化一个变量，比如**和**，存储所有减去的值的和。
*   使用 [min_element()](https://www.geeksforgeeks.org/stdmin_element-in-cpp/) 找到数组中存在的[最小元素，说**最小**。](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/)
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个数组元素，说出 **arr[i]** ，将**(arr[I]–最小值)**加到所需的和上。
*   完成数组遍历后，打印得到的和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of values
// removed to make all array elements equal
int minValue(int arr[], int n)
{
    // Stores the minimum of the array
    int minimum = *min_element(
        arr, arr + n);

    // Stores required sum
    int sum = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // Add the value subtracted
        // from the current element
        sum = sum + (arr[i] - minimum);
    }

    // Return the total sum
    return sum;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << minValue(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;
class GFG
{

// Function to find the sum of values
// removed to make all array elements equal
static int minValue(int []arr, int n)
{
    Arrays.sort(arr);

    // Stores the minimum of the array
    int minimum = arr[0];

    // Stores required sum
    int sum = 0;

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // Add the value subtracted
        // from the current element
        sum = sum + (arr[i] - minimum);
    }

    // Return the total sum
    return sum;
}

// Driver Code
static public void main(String args[])
{
    int []arr = { 1, 2, 3 };
    int N = arr.length;

    // Function Call
    System.out.println(minValue(arr, N));
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the sum of values
# removed to make all array elements equal
def minValue(arr, n):

    # Stores the minimum of the array
    minimum = min(arr)

    # Stores required sum
    sum = 0

    # Traverse the array
    for i in range(n):

        # Add the value subtracted
        # from the current element
        sum = sum + (arr[i] - minimum)

    # Return the total sum
    return sum

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 3 ]
    N = len(arr)

    # Function Call
    print(minValue(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the sum of values
// removed to make all array elements equal
static int minValue(int []arr, int n)
{
    Array.Sort(arr);

    // Stores the minimum of the array
    int minimum = arr[0];

    // Stores required sum
    int sum = 0;

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // Add the value subtracted
        // from the current element
        sum = sum + (arr[i] - minimum);
    }

    // Return the total sum
    return sum;
}

// Driver Code
static public void Main ()
{
    int []arr = { 1, 2, 3 };
    int N = arr.Length;

    // Function Call
    Console.WriteLine(minValue(arr, N));
}
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the sum of values
// removed to make all array elements equal
function minValue(arr, n)
{
    // Stores the minimum of the array
    var minimum = Math.min.apply(Math,arr);

    // Stores required sum
    var sum = 0;

    var i;
    // Traverse the array
    for (i = 0; i < n; i++) {

        // Add the value subtracted
        // from the current element
        sum = sum + (arr[i] - minimum);
    }

    // Return the total sum
    return sum;
}

// Driver Code

 var arr = [1, 2, 3];
 var N = arr.length;

// Function Call
 document.write(minValue(arr, N));

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)