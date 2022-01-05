# 给定数组中所有无序对的按位“与”

> 原文:[https://www . geeksforgeeks . org/给定数组中所有无序对的位与运算/](https://www.geeksforgeeks.org/bitwise-and-of-all-unordered-pairs-from-a-given-array/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到给定数组中所有可能的无序对的[位“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。

**示例:**

> **输入:** arr[] = {1，5，3，7}
> **输出:** 1
> **解释:**
> 所有可能的无序对为(1，5)、(1，3)、(1，7)、(5，3)、(5，7)、(3，7)。
> 所有可能对的按位 AND =(1&5)&(1&3)&(1&7)&(5&3)&(5&7)&(3&7)
> = 1&1&1&1&5&3
> = 1
> 因此，所需输出为 1
> 
> **输入:** arr[] = {4，5，12，15 }
> T3】输出: 4

**天真的方法:**想法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[生成给定数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)的所有可能的对。最后，打印给定数组的这些对中存在的每个元素的[位“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。按照以下步骤解决问题:

*   初始化一个变量，比如 **totalAND** ，来存储这些对中每个元素的**位 AND** 。
*   [迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)并从给定数组生成所有可能的对( **arr[i]，arr[j]** )。
*   对于每对( **arr[i]，arr[j]【T1])，更新**total and =(total and&arr[I]&arr[j])**的值。**
*   最后，打印**total 和**的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate bitwise AND
// of all pairs from the given array
int TotalAndPair(int arr[], int N)
{
    // Stores bitwise AND
    // of all possible pairs
    int totalAND = (1 << 30) - 1;

    // Generate all possible pairs
    for (int i = 0; i < N; i++) {
        for (int j = i + 1; j < N;
             j++) {

            // Calculate bitwise AND
            // of each pair
            totalAND &= arr[i]
                        & arr[j];
        }
    }
    return totalAND;
}

// Driver Code
int main()
{
    int arr[] = { 4, 5, 12, 15 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << TotalAndPair(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to calculate bitwise AND
// of all pairs from the given array
static int TotalAndPair(int arr[], int N)
{
    // Stores bitwise AND
    // of all possible pairs
    int totalAND = (1 << 30) - 1;

    // Generate all possible pairs
    for (int i = 0; i < N; i++)
    {
        for (int j = i + 1; j < N;
             j++)
        {

            // Calculate bitwise AND
            // of each pair
            totalAND &= arr[i]
                        & arr[j];
        }
    }
    return totalAND;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 4, 5, 12, 15 };
    int N = arr.length;
    System.out.print(TotalAndPair(arr, N));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to calculate bitwise AND
# of all pairs from the given array
def TotalAndPair(arr, N):

  # Stores bitwise AND
  # of all possible pairs
    totalAND = (1 << 30) - 1

    # Generate all possible pairs
    for i in range(N):
        for j in range(i + 1, N):

            # Calculate bitwise AND
            # of each pair
            totalAND &= (arr[i] & arr[j])
    return totalAND

# Driver Code
if __name__ == '__main__':
    arr=[4, 5, 12, 15]
    N = len(arr)
    print(TotalAndPair(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Function to calculate bitwise AND
// of all pairs from the given array
static int TotalAndPair(int[] arr, int N)
{

    // Stores bitwise AND
    // of all possible pairs
    int totalAND = (1 << 30) - 1;

    // Generate all possible pairs
    for(int i = 0; i < N; i++)
    {
        for(int j = i + 1; j < N; j++)
        {

            // Calculate bitwise AND
            // of each pair
            totalAND &= arr[i] & arr[j];
        }
    }
    return totalAND;
}

// Driver Code
public static void Main()
{
    int[] arr = { 4, 5, 12, 15 };
    int N = arr.Length;

    Console.Write(TotalAndPair(arr, N));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to calculate bitwise AND
// of all pairs from the given array
function TotalAndPair(arr, N)
{
    // Stores bitwise AND
    // of all possible pairs
    let totalAND = (1 << 30) - 1;

    // Generate all possible pairs
    for (let i = 0; i < N; i++) {
        for (let j = i + 1; j < N;
            j++) {

            // Calculate bitwise AND
            // of each pair
            totalAND &= arr[i]
                        & arr[j];
        }
    }
    return totalAND;
}

// Driver Code
    let arr = [ 4, 5, 12, 15 ];
    let N = arr.length;
    document.write(TotalAndPair(arr, N));

// This code is contributed by Surbhi Tyagi

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以基于以下观察进行优化:

*   考虑一个由 4 个元素组成的数组，所需的按位“与”如下:

> (arr[0]& arr[1])&(arr[0]& arr[2])&(arr[0]& arr[3])&(arr[1]& arr[2])&(arr[1]& arr[3])&(arr[2]& arr[3])

*   由于按位“与”遵循 [**关联属性**](https://en.wikipedia.org/wiki/Associative_property) ，因此上述表达式可以重新排列为:

> (arr[0]& arr[0]& arr[0])&(arr[1]& arr[1]& arr[1])&(arr[2]& arr[2]& arr[2])&(arr[3]& arr[3]& arr[3])

*   可以观察到，每个数组元素在所有可能的对中都恰好出现**(N–1)**次。
*   基于**位与**运算符的 **X & X = X** 属性，上述表达式可以重新排列为**arr[0]&arr[1]&arr[2]&arr[3]**，等于原始数组所有元素的[位与。](https://www.geeksforgeeks.org/bitwise-and-of-all-the-elements-of-array/)

按照以下步骤解决问题:

*   初始化一个变量**和**来存储结果。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。
*   通过更新**total AND = total AND&arr[I]**，计算所有无序对的**位 AND** 。

下面是上述方法的实现

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate bitwise AND
// of all pairs from the given array
int TotalAndPair(int arr[], int N)
{
    // Stores bitwise AND
    // of all possible pairs
    int totalAND = (1 << 30) - 1;

    // Iterate over the array arr[]
    for (int i = 0; i < N; i++) {

        // Calculate bitwise AND
        // of each array element
        totalAND &= arr[i];
    }
    return totalAND;
}

// Driver Code
int main()
{
    int arr[] = { 4, 5, 12, 15 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << TotalAndPair(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

import java.util.*;

class GFG{

// Function to calculate bitwise AND
// of all pairs from the given array
static int TotalAndPair(int arr[], int N)
{
    // Stores bitwise AND
    // of all possible pairs
    int totalAND = (1 << 30) - 1;

    // Iterate over the array arr[]
    for (int i = 0; i < N; i++) {

        // Calculate bitwise AND
        // of each array element
        totalAND &= arr[i];
    }
    return totalAND;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 4, 5, 12, 15 };
    int N = arr.length;
    System.out.print(TotalAndPair(arr, N));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program to implement
# the above approach

# Function to calculate bitwise AND
# of all pairs from the given array
def TotalAndPair(arr, N):

    # Stores bitwise AND
    # of all possible pairs
    totalAND = (1 << 30) - 1;

    # Iterate over the array arr
    for i in range(N):

        # Calculate bitwise AND
        # of each array element
        totalAND &= arr[i];

    return totalAND;

# Driver Code
if __name__ == '__main__':
    arr = [4, 5, 12, 15];
    N = len(arr);
    print(TotalAndPair(arr, N));

    # This code is contributed by 29AjayKumar
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to calculate bitwise AND
// of all pairs from the given array
static int TotalAndPair(int []arr, int N)
{

    // Stores bitwise AND
    // of all possible pairs
    int totalAND = (1 << 30) - 1;

    // Iterate over the array arr[]
    for(int i = 0; i < N; i++)
    {

        // Calculate bitwise AND
        // of each array element
        totalAND &= arr[i];
    }
    return totalAND;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 4, 5, 12, 15 };
    int N = arr.Length;

    Console.Write(TotalAndPair(arr, N));
}
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// JavaScript program to implement
// the above approach

// Function to calculate bitwise AND
// of all pairs from the given array
function TotalAndPair(arr, N)
{
    // Stores bitwise AND
    // of all possible pairs
    let totalAND = (1 << 30) - 1;

    // Iterate over the array arr[]
    for (let i = 0; i < N; i++) {

        // Calculate bitwise AND
        // of each array element
        totalAND &= arr[i];
    }
    return totalAND;
}

// Driver Code

    let arr = [ 4, 5, 12, 15 ];
    let N = arr.length;
    document.write(TotalAndPair(arr, N));

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
4
```

***时间复杂度** : O(N)*
***辅助空间:** O(1)*