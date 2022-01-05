# 给定数组中所有无序对的逐位异或

> 原文:[https://www . geeksforgeeks . org/给定数组中所有无序对的按位异或/](https://www.geeksforgeeks.org/bitwise-xor-of-all-unordered-pairs-from-a-given-array/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到给定数组中所有可能的无序对的[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。

**示例:**

> **输入** : arr[] = {1，5，3，7}
> **输出:** 0
> **解释:**
> 所有可能的无序对为(1，5)，(1，3)，(1，7)，(5，3)，(5，7)，(3，7)
> 所有可能对的按位异或为= 1 ^ 5 ^ 1 ^3 ^ 1 ^ 7 ^ 5 ^ 3 ^ 5^ 7 ^ 3 7 = 0
> 因此，需要的输出为 0。
> 
> **输入:** arr[] = {1，2，3，4}
> **输出:** 4

**天真的方法:**想法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[生成给定数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)的所有可能的对。最后，打印给定数组的这些对中存在的每个元素的[位异或](https://www.geeksforgeeks.org/tag/xor/)。按照以下步骤解决问题:

*   初始化一个变量，比如说 **totalXOR** ，来存储这些对中每个元素的[位 XOR](https://www.geeksforgeeks.org/tag/xor/) 。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[从给定数组生成所有可能的对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/) **(arr[i]，arr[j])** 。
*   对于每对 **(arr[i]，arr[j])** ，更新**total xor =(total xor ^ arr[I]^ arr[j])**的值。
*   最后，打印 **totalXOR** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to get bitwise XOR
// of all possible pairs of
// the given array
int TotalXorPair(int arr[], int N)
{
    // Stores bitwise XOR
    // of all possible pairs
    int totalXOR = 0;

    // Generate all possible pairs
    // and calculate bitwise XOR
    // of all possible pairs
    for (int i = 0; i < N; i++) {
        for (int j = i + 1; j < N;
             j++) {

            // Calculate bitwise XOR
            // of each pair
            totalXOR ^= arr[i]
                        ^ arr[j];
        }
    }
    return totalXOR;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << TotalXorPair(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to get bitwise XOR
// of all possible pairs of
// the given array
public static int TotalXorPair(int arr[],
                               int N)
{
  // Stores bitwise XOR
  // of all possible pairs
  int totalXOR = 0;

  // Generate all possible pairs
  // and calculate bitwise XOR
  // of all possible pairs
  for (int i = 0; i < N; i++)
  {
    for (int j = i + 1; j < N; j++)
    {
      // Calculate bitwise XOR
      // of each pair
      totalXOR ^= arr[i] ^ arr[j];
    }
  }

  return totalXOR;
}

// Driver code   
public static void main(String[] args)
{
  int arr[] = {1, 2, 3, 4};
  int N = arr.length;
  System.out.print(TotalXorPair(arr, N));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to get bitwise XOR
# of all possible pairs of
# the given array
def TotalXorPair(arr, N):

    # Stores bitwise XOR
    # of all possible pairs
    totalXOR = 0;

    # Generate all possible pairs
    # and calculate bitwise XOR
    # of all possible pairs
    for i in range(0, N):
        for j in range(i + 1, N):

            # Calculate bitwise XOR
            # of each pair
            totalXOR ^= arr[i] ^ arr[j];

    return totalXOR;

# Driver code
if __name__ == '__main__':

    arr = [1, 2, 3, 4];
    N = len(arr);
    print(TotalXorPair(arr, N));

# This code is contributed by shikhasingrajput
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to get bitwise XOR
// of all possible pairs of
// the given array
public static int TotalXorPair(int []arr,
                               int N)
{

  // Stores bitwise XOR
  // of all possible pairs
  int totalXOR = 0;

  // Generate all possible pairs
  // and calculate bitwise XOR
  // of all possible pairs
  for(int i = 0; i < N; i++)
  {
    for(int j = i + 1; j < N; j++)
    {

      // Calculate bitwise XOR
      // of each pair
      totalXOR ^= arr[i] ^ arr[j];
    }
  }
  return totalXOR;
}

// Driver code   
public static void Main(String[] args)
{
  int []arr = {1, 2, 3, 4};
  int N = arr.Length;

  Console.Write(TotalXorPair(arr, N));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to get bitwise XOR
// of all possible pairs of
// the given array
function TotalXorPair(arr, N)
{

    // Stores bitwise XOR
    // of all possible pairs
    let totalXOR = 0;

    // Generate all possible pairs
    // and calculate bitwise XOR
    // of all possible pairs
    for(let i = 0; i < N; i++)
    {
        for(let j = i + 1; j < N; j++)
        {

            // Calculate bitwise XOR
            // of each pair
            totalXOR ^= arr[i] ^ arr[j];
        }
    }
    return totalXOR;
}

// Driver Code
let arr = [ 1, 2, 3, 4 ];
let N = arr.length;

document.write(TotalXorPair(arr, N));

// This code is contributed by target_2

</script>
```

**Output**

```
4
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**要优化上述方法，请遵循以下观察结果:

> 按位异或的性质:
> a ^ a ^ a ……(偶数次)= 0
> a ^ a ^ a ……(奇数次)= a
> 
> 给定数组的每个元素在所有可能的对中都精确出现**(N–1)**次。
> 因此，如果 **N** 为偶数，那么所有可能对的按位异或等于所有数组元素的按位异或。
> 否则，所有可能对的按位异或等于 0。

按照以下步骤解决问题:

*   如果 **N** 为奇数，则打印 **0** 。
*   如果 **N** 为偶数，则打印给定数组所有元素的按位异或值。

下面是上述方法的实现

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to get bitwise XOR
// of all possible pairs of
// the given array
int TotalXorPair(int arr[], int N)
{
    // Stores bitwise XOR
    // of all possible pairs
    int totalXOR = 0;

    // Check if N is odd
    if (N % 2 != 0) {
        return 0;
    }

    // If N is even then calculate
    // bitwise XOR of all elements
    // of the given array.
    for (int i = 0; i < N; i++) {
        totalXOR ^= arr[i];
    }
    return totalXOR;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << TotalXorPair(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to get bitwise XOR
// of all possible pairs of
// the given array
public static int TotalXorPair(int arr[],
                               int N)
{
  // Stores bitwise XOR
  // of all possible pairs
  int totalXOR = 0;

  // Check if N is odd
  if( N % 2 != 0 )
  {
    return 0;
  }

  // If N is even then calculate
  // bitwise XOR of all elements
  // of the array
  for(int i = 0; i < N; i++)
  {
    totalXOR ^= arr[i];
  }

  return totalXOR;
}

// Driver code   
public static void main(String[] args)
{
  int arr[] = {1, 2, 3, 4};
  int N = arr.length;
  System.out.print(TotalXorPair(arr, N));
}
}

// This code is contributed by math_lover
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to get bitwise XOR
# of all possible pairs of
# the given array
def TotalXorPair(arr, N):

    # Stores bitwise XOR
    # of all possible pairs
    totalXOR = 0

    # Check if N is odd
    if (N % 2 != 0):
        return 0

    # If N is even then calculate
    # bitwise XOR of all elements
    # of the given array.
    for i in range(N):
        totalXOR ^= arr[i]

    return totalXOR

# Driver code
if __name__ == '__main__':

    arr = [ 1, 2, 3, 4 ]
    N = len(arr)

    print(TotalXorPair(arr, N))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to get bitwise XOR
// of all possible pairs of
// the given array
static int TotalXorPair(int []arr,
                        int N)
{

    // Stores bitwise XOR
    // of all possible pairs
    int totalXOR = 0;

    // Check if N is odd
    if (N % 2 != 0)
    {
        return 0;
    }

    // If N is even then calculate
    // bitwise XOR of all elements
    // of the array
    for(int i = 0; i < N; i++)
    {
        totalXOR ^= arr[i];
    }
    return totalXOR;
}

// Driver code   
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3, 4 };
    int N = arr.Length;

    Console.Write(TotalXorPair(arr, N));
}
}

// This code is contributed by doreamon_
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to get bitwise XOR
// of all possible pairs of
// the given array
function TotalXorPair(arr, N)
{
    // Stores bitwise XOR
    // of all possible pairs
    let totalXOR = 0;

    // Check if N is odd
    if (N % 2 != 0) {
        return 0;
    }

    // If N is even then calculate
    // bitwise XOR of all elements
    // of the given array.
    for (let i = 0; i < N; i++) {
        totalXOR ^= arr[i];
    }
    return totalXOR;
}

// Driver Code
    let arr = [ 1, 2, 3, 4 ];
    let N = arr.length;
    document.write(TotalXorPair(arr, N));

</script>
```

**Output**

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)