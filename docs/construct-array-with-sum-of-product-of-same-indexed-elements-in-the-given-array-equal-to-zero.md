# 构造给定数组中相同索引元素乘积之和等于零的数组

> 原文:[https://www . geeksforgeeks . org/construct-array-带有相同索引元素的乘积之和-给定数组中的元素等于零/](https://www.geeksforgeeks.org/construct-array-with-sum-of-product-of-same-indexed-elements-in-the-given-array-equal-to-zero/)

给定一个大小为 **N** (总是*甚至*)的[数组](https://www.geeksforgeeks.org/array-data-structure/)、 **arr[]** ，任务是构造一个由 **N** 个非零整数组成的新数组，使得 **arr[]** 的相同索引元素与新数组的乘积之和等于 **0** 。如果存在多个解决方案，请打印其中任何一个。

**示例:**

> **输入:** arr[] = {1，2，3，4}
> **输出:** -4 -3 2 1
> **解释:**
> arr[]的相同索引数组元素与新数组的乘积之和= { 1 *(4)+2 *(3)+3 *(2)+4 *(1)} = 0。
> 因此，所需输出为-4 -3 2 1。
> 
> **输入:** arr[] = {-1，2，-3，6，4}
> 输出: 1 1 1 1 -1

**方法:**使用[贪婪技术](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。这一想法基于以下观察:

> arr[I]*(-arr[I+1])+arr[I+1]* arr[I]= 0

按照以下步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)，比如说**new warr【】**来存储新的数组元素，使得**σ(arr[I]* new warr[I])= 0**
*   [使用变量 **i** 和](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)[遍历给定数组](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，检查我是否为偶数。如果发现为真，则**新的[i] = arr[i + 1]** 。
*   否则，**新的[I]=-arr[I–1]**
*   最后，打印**new RR【】**的值。

下面是上述方法的实现

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to generate a new array with product
// of same indexed elements with arr[] equal to 0
void constructNewArraySumZero(int arr[], int N)
{
    // Stores sum of same indexed array
    // elements of arr and new array
    int newArr[N];

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If i is an even number
        if (i % 2 == 0) {

            // Insert arr[i + 1] into
            // the new array newArr[]
            newArr[i] = arr[i + 1];
        }

        else {

            // Insert -arr[i - 1] into
            // the new array newArr[]
            newArr[i] = -arr[i - 1];
        }
    }

    // Print new array elements
    for (int i = 0; i < N; i++) {
        cout << newArr[i] << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, -5, -6, 8 };
    int N = sizeof(arr) / sizeof(arr[0]);

    constructNewArraySumZero(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to generate a new array with
// product of same indexed elements with
// arr[] equal to 0
static void constructNewArraySumZero(int arr[],
                                     int N)
{

    // Stores sum of same indexed array
    // elements of arr and new array
    int newArr[] = new int[N];

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // If i is an even number
        if (i % 2 == 0)
        {

            // Insert arr[i + 1] into
            // the new array newArr[]
            newArr[i] = arr[i + 1];
        }
        else
        {

            // Insert -arr[i - 1] into
            // the new array newArr[]
            newArr[i] = -arr[i - 1];
        }
    }

    // Print new array elements
    for(int i = 0; i < N; i++)
    {
        System.out.print(newArr[i] + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, -5, -6, 8 };
    int N = arr.length;

    constructNewArraySumZero(arr, N);
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to generate a new array
# with product of same indexed elements
# with arr[] equal to 0
def constructNewArraySumZero(arr, N):

    # Stores sum of same indexed array
    # elements of arr and new array
    newArr = [0] * N

    # Traverse the array
    for i in range(N):

        # If i is an even number
        if (i % 2 == 0):

            # Insert arr[i + 1] into
            # the new array newArr[]
            newArr[i] = arr[i + 1]

        else:

            # Insert -arr[i - 1] into
            # the new array newArr[]
            newArr[i] = -arr[i - 1]

    # Print new array elements
    for i in range(N):
        print(newArr[i] ,
              end = " ")

# Driver code
arr = [1, 2, 3, -5, -6, 8]
N = len(arr)
constructNewArraySumZero(arr, N)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Function to generate a new array with
// product of same indexed elements with
// arr[] equal to 0
static void constructNewArraySumZero(int[] arr,
                                     int N)
{

    // Stores sum of same indexed array
    // elements of arr and new array
    int[] newArr = new int[N];

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // If i is an even number
        if (i % 2 == 0)
        {

            // Insert arr[i + 1] into
            // the new array newArr[]
            newArr[i] = arr[i + 1];
        }
        else
        {

            // Insert -arr[i - 1] into
            // the new array newArr[]
            newArr[i] = -arr[i - 1];
        }
    }

    // Print new array elements
    for(int i = 0; i < N; i++)
    {
        Console.Write(newArr[i] + " ");
    }
}

// Driver Code
public static void Main()
{
    int[] arr = { 1, 2, 3, -5, -6, 8 };
    int N = arr.Length;

    constructNewArraySumZero(arr, N);
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to generate a new array with
// product of same indexed elements with
// arr[] equal to 0
function constructNewArraySumZero(arr, N)
{

    // Stores sum of same indexed array
    // elements of arr and new array
    let newArr = [];

    // Traverse the array
    for(let i = 0; i < N; i++)
    {

        // If i is an even number
        if (i % 2 == 0)
        {

            // Insert arr[i + 1] into
            // the new array newArr[]
            newArr[i] = arr[i + 1];
        }
        else
        {

            // Insert -arr[i - 1] into
            // the new array newArr[]
            newArr[i] = -arr[i - 1];
        }
    }

    // Prlet new array elements
    for(let i = 0; i < N; i++)
    {
        document.write(newArr[i] + " ");
    }
}

    // Driver Code
    let arr = [ 1, 2, 3, -5, -6, 8 ];
    let N = arr.length;

    constructNewArraySumZero(arr, N);

// This code is contributed by souravghosh0416.
</script>
```

**Output**

```
2 -1 -5 -3 8 6 
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)