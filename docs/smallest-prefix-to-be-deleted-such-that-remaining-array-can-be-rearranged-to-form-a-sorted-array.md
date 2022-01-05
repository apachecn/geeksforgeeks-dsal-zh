# 要删除的最小前缀，以便剩余的数组可以重新排列形成排序数组

> 原文:[https://www . geeksforgeeks . org/最小-要删除的前缀-这样-剩余-数组-可以重新排列-形成-排序-数组/](https://www.geeksforgeeks.org/smallest-prefix-to-be-deleted-such-that-remaining-array-can-be-rearranged-to-form-a-sorted-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到需要删除的前缀的最小长度，以便通过逐个选择第一个或最后一个元素来重复重新排列剩余的数组元素，从而形成一个[排序数组](https://www.geeksforgeeks.org/check-whether-given-array-k-sorted-array-not/)。

**示例:**

> **输入:** arr[] = {6，5，4，3，4}
> **输出:** 3
> **解释:**
> 要根据给定条件进行数组排序，请移除前 3 个元素。
> 删除后，数组 arr[]修改为{3，4}。
> 从数组 arr[]，逐个选择第一个元素，即 arr[0] - > arr[1]，形成排序数组{3，4}。
> 
> **输入:** arr[] = {1，3，4，2 }
> T3】输出: 3

**天真方法:**最简单的方法是从给定的数组中删除前缀的所有可能长度，对于每个前缀，检查是否可以通过删除这些前缀从剩余的数组元素中形成排序数组。如果发现为真，则打印删除的前缀的最小长度。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**有效方法:**上述方法可以通过观察得到的后缀必须是**arr[1]≤arr[2]≤…≥arr[N–2]≥arr[N–1]**的形式来优化，其中 **N** 是剩余数组的长度，后缀是最大长度。请遵循以下步骤:

*   将变量**索引**初始化为**N–1**。
*   [从终点开始遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并在 **arr【索引–1】≤【索引】arr**处停止。
*   随着迭代的进行，我们不断减少**答案**。
*   完成以上所有步骤后，打印**索引**的值，这是必须删除的前缀的最小长度。

下面是上述方法的实现:

## C++

```
// C++ program for above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum length
// of prefix required to be deleted
int findMinLength(vector<int>& arr)
{
    // Stores index to be returned
    int index = (int)arr.size() - 1;

    // Iterate until previous element
    // is <= current index
    while (index > 0
           && arr[index] >= arr[index - 1]) {

        // Decrementing index
        index--;
    }

    // Return index
    return index;
}

// Driver Code
int main()
{

    // Given arr[]
    vector<int> arr = { 7, 8, 5, 0, -1,
                        -1, 0, 1, 2, 3, 4 };

    // Function Call
    cout << findMinLength(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;
import java.io.*;

class GFG{

// Function to find the minimum length
// of prefix required to be deleted
static int findMinLength(int[] arr)
{

    // Stores index to be returned
    int index = (int)arr.length - 1;

    // Iterate until previous element
    // is <= current index
    while (index > 0 && arr[index] >=
                        arr[index - 1])
    {

        // Decrementing index
        index--;
    }

    // Return index
    return index;
}

// Driver code
public static void main(String args[])
{

    // Given arr[]
    int arr[]=  { 7, 8, 5, 0, -1,
                 -1, 0, 1, 2, 3, 4 };
    int n = arr.length;

    // Function call
    System.out.println(findMinLength(arr));
}
}

// This code is contributed by bikram2001jha
```

## 蟒蛇 3

```
# Python3 program for above approach

# Function to find the minimum length
# of prefix required to be deleted
def findMinLength(arr):

    # Stores index to be returned
    index = len(arr) - 1;

    # Iterate until previous element
    # is <= current index
    while (index > 0 and arr[index] >= arr[index - 1]):

        # Decrementing index
        index -= 1;

    # Return index
    return index;

# Driver code
if __name__ == '__main__':

    # Given arr
    arr = [7, 8, 5, 0, -1,
           -1, 0, 1, 2, 3, 4];
    n = len(arr);

    # Function call
    print(findMinLength(arr));

# This code is contributed by Princi Singh
```

## C#

```
// C# program for above approach
using System;

class GFG{

// Function to find the minimum length
// of prefix required to be deleted
static int findMinLength(int[] arr)
{

    // Stores index to be returned
    int index = (int)arr.Length - 1;

    // Iterate until previous element
    // is <= current index
    while (index > 0 && arr[index] >=
                        arr[index - 1])
    {

        // Decrementing index
        index--;
    }

    // Return index
    return index;
}

// Driver code
public static void Main(String []args)
{

    // Given []arr
    int []arr =  { 7, 8, 5, 0, -1,
                  -1, 0, 1, 2, 3, 4 };

    int n = arr.Length;

    // Function call
    Console.WriteLine(findMinLength(arr));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Java Script program for above approach

// Function to find the minimum length
// of prefix required to be deleted
function findMinLength( arr)
{

    // Stores index to be returned
    let index = parseInt(arr.length) - 1;

    // Iterate until previous element
    // is <= current index
    while (index > 0 && arr[index] >=
                        arr[index - 1])
    {

        // Decrementing index
        index--;
    }

    // Return index
    return index;
}

// Driver code

    // Given arr[]
    let arr=  [ 7, 8, 5, 0, -1,
                 -1, 0, 1, 2, 3, 4 ];
    let n = arr.length;

    // Function call
    document.write(findMinLength(arr));
//contributed by sravan kumar
</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)