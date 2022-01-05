# 相邻对异或替换 M 个数组元素后的第 k 个数组元素

> 原文:[https://www . geeksforgeeks . org/kth-数组-m 后元素-相邻对异或替换数组元素/](https://www.geeksforgeeks.org/kth-array-element-after-m-replacements-of-array-elements-by-xor-of-adjacent-pairs/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和两个整数 **M** 和 **K** ，任务是在给定数组上执行以下 **M** 运算后，在 **K <sup>第</sup>** 索引处找到数组元素。

> 在一次操作中，形成一个新的数组，其元素具有当前数组相邻元素的[位异或](https://www.geeksforgeeks.org/bitwise-algorithms/)值。

如果操作次数 **M** 或 **M** 操作后 **K** 的值无效，则打印 **-1** 。

**示例:**

> **输入:** arr[] = {1，4，5，6，7}，M = 1，K = 2
> **输出:** 3
> **解释:**
> 由于 M = 1，因此，操作只需在数组上执行一次。
> 数组修改为{1^4、4^5、5^6、6^7} = {5、1、3、1}。
> 更新数组中索引 K = 2 处的元素值为 3。
> 
> **输入:** arr[] = {3，2，6}，M = 2，K = 1
> **输出:** -1
> **说明:**
> 从 M = 2 开始，操作已经执行了两次。
> 在阵列{3，2，6}上执行第一次操作时，它被修改为 2^6} {3^2 = { 1，4}。
> 在阵列{1，4}上执行第二次操作时，它被修改为{1^4} = {5}。
> 执行 2 次操作后，数组大小缩减为 1。这意味着索引 K = 1 在 2 次操作后不存在。
> 因此，给定的输入无效。所以输出是-1。

**方法 1:**

> 观察:
> 
> 设数组为[1，2，3，4 5，6，7，8，9，10]
> 
> 一次手术后:[1^2、2^3、3^4、4^5、5^6、6^7、7^8、8^9、9 10]
> 
> 两次手术后:[1^2^2^3、2^3^3^4、3^4^4^5、4^5^5^6、,5^6^6^7、6^7^7^8、7^8^8^9、8^9 ^9^10]= = = >[1 3、2 4、3 5、4 6、5 7、6 8、7 9、8 10]
> 
> 三次手术后:[ 1^3^2^4、2^4^3^5、3^5^4^6、4^6^5^7、5^7^6^8、6^8^7^9、7^9^8^10 ]
> 
> 四次手术后:[1^3^2^4^2^4^3^5、2^4^3^5^3^5^4^6、3^5^4^6^4^6^5^7、4^6^5^7 ^5^7^6^8、5^7^6^8^6^8^7^9、6^8^7^9^7^9^8^10]= = = >[1^5、2^6、3 7、4 8、5 9、6 10]
> 
> 五次手术后:[1^5^2^6、2^6^3^7、3^7^4^8、4^8^5^9、5^9^6^10 ]
> 
> 六次手术后:[1^5^3^7、2^6^4^8、3^7^5^9、4^8^6^10]
> 
> 七次手术后:[1^5^3^7^2^6^4^8、2^6^4^8^3^7^5^9、3^7^5^9^4^8^6^10]
> 
> 八次手术后:[2^10 1^9]
> 
> 因此，从观察中我们可以看出，在 2^k 的第 16 次 a[i]=a[i]^a[i+(2^k 行动中]对于:i

1.  检查给定数量的操作是否可以在阵列上执行。
2.  每次迭代后，数组的长度减少 1，这意味着 M 次运算后数组的大小将为 N-M，如果我们需要返回的索引大于或等于 M 次运算后数组的大小(即 **K > =N-M** ，因此我们无法执行运算并返回 **-1** 。
3.  如果它有效，那么我们需要在 M 操作后返回更新数组中的第 Kth 个索引。
4.  现在我们需要执行 M 次操作
    *   正如我们所知的关系 a[i]=a[i]^a[i+(2^k】。所以，我们只需要把 m 作为 2^k 形式的数的和，然后跳到这个数。
    *   为此，我们可以迭代 m 中以二进制形式设置的位，并根据上述与所有索引(索引< n-2^k)的关系执行更新。
5.  现在我们必须返回更新后数组的第 k 个 lemon。

## C++

```
#include <iostream>
#include <vector>
using namespace std;

int m_step_xor(vector<int> a, int m, int k)
{
    int n = a.size();

    // the total number of element remain afte m operation
    // is n-m so the index that are greater than or equal to
    // n-m in zero-based indexing will be not present
    if (k >= n - m)
        return -1;

    // consedering m<2^18

    for (int i = 0; i < 18; i++) {
        // check whether ith bit is on or not in m
        if (m & (1 << i)) {
            m -= (1 << i);

            // as the bit is on
            // Updating index that exist with the relation
            // a[i]=a[i]^a[i+2^j]
            for (int j = 0; j < n - (1 << i); j++) {
                a[j] = a[j] ^ a[j + (1 << i)];
            }
        }
    }

    // returning the Kth index in updated array after M
    // operation
    return a[k];
}

int main()
{

    vector<int> a = { 1, 4, 5, 6, 7 };

    int m = 1, k = 2;

    // Function call
    int ans = m_step_xor(a, m, k);

    cout << ans << "\n";

    return 0;
}

// This code is contributed by swaraj jain
```

**Output**

```
3

```

**时间复杂度** : O(N*log(M))
**辅助空间** : O(1)

**方法 2:** 思路是在每次操作后生成数组，并在每次迭代后检入是否有可能进一步做操作。如果不可能，则返回**-1”**。以下是步骤:

1.  检查给定数量的操作是否可以在阵列上执行。
2.  每次迭代后，数组长度减少 1，这意味着如果 **M** 大于或等于 **N** ，则无法执行操作。于是，印**“-1”**。
3.  如果 **M** 的值有效，那么检查给定的指数 **K** 是否有效。
4.  **M** 运算后，**(N–M)**元素留在数组中。因此，如果指数值大于或等于**(N–M)**的值，则打印**-1”**。
5.  如果 **M** 和 **K** 值都有效，则循环 **M** 次，并执行以下操作:
    *   在每次迭代中，创建一个临时数组 **temp[]** ，该数组存储通过对原始数组的相邻值执行操作而获得的值。
    *   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，计算相邻元素的按位异或值，并将这些计算值保存在临时数组 **temp[]** 中。
    *   用**温度[]** 更新当前数组 **arr[]** 。
6.  在 **M** 迭代后，返回**arr【K】**的值，这是所需的输出。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Method that returns the
// corresponding output by
// taking the given inputs.
int xor_operations(int N, int arr[], 
                   int M, int K)
{

    // If this condition is satisfied,
    // value of M is invalid
    if (M < 0 or M >= N)
        return -1;

    // Check if index K is valid
    if (K < 0 or K >= N - M)
        return -1;

    // Loop to perform M operations
    for(int p = 0; p < M; p++)
    {

        // Creating a temporary list
        vector<int>temp;

        // Traversing the array
        for(int i = 0; i < N; i++)
        {

            // Calculate XOR values
            // of adjacent elements
            int value = arr[i] ^ arr[i + 1];

            // Adding this value to
            // the temporary list
            temp.push_back(value);

            // Update the original array
            arr[i] = temp[i];
        }
    }

    // Getting value at index K
    int ans = arr[K];

    return ans;
}

// Driver Code
int main()
{
    // Number of elements
    int N = 5;

    // Given array arr[]
    int arr[] = {1, 4, 5, 6, 7};
    int M = 1, K = 2;

    // Function call
    cout << xor_operations(N, arr, M, K);
    return 0;
}

// This code is contributed by gauravrajput1
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Method that returns the
// corresponding output by
// taking the given inputs.
static int xor_operations(int N, int arr[],
                          int M, int K)
{

    // If this condition is satisfied,
    // value of M is invalid
    if (M < 0 || M >= N)
        return -1;

    // Check if index K is valid
    if (K < 0 || K >= N - M)
        return -1;

    // Loop to perform M operations
    for(int p = 0; p < M; p++)
    {

        // Creating a temporary list
        Vector<Integer>temp = new Vector<Integer>();

        // Traversing the array
        for(int i = 0; i < N - 1; i++)
        {

            // Calculate XOR values
            // of adjacent elements
            int value = arr[i] ^ arr[i + 1];

            // Adding this value to
            // the temporary list
            temp.add(value);

            // Update the original array
            arr[i] = temp.get(i);
        }
    }

    // Getting value at index K
    int ans = arr[K];

    return ans;
}

// Driver Code
public static void main(String[] args)
{

    // Number of elements
    int N = 5;

    // Given array arr[]
    int arr[] = { 1, 4, 5, 6, 7 };
    int M = 1, K = 2;

    // Function call
    System.out.print(xor_operations(N, arr, M, K));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Method that returns the
# corresponding output by
# taking the given inputs.
def xor_operations(N, arr, M, K):

    # If this condition is satisfied,
    # value of M is invalid
    if M < 0 or M >= N:
        return -1

    # Check if index K is valid
    if K < 0 or K >= N-M:
        return -1

    # Loop to perform M operations
    for _ in range(M):

        # Creating a temporary list
        temp = []

        # Traversing the array
        for i in range(len(arr)-1):

            # Calculate XOR values
            # of adjacent elements
            value = arr[i]^arr[i + 1]

            # Adding this value to
            # the temporary list
            temp.append(value)

        # Update the original array
        arr = temp[:]

    # Getting value at index K
    ans = arr[K]
    return ans

# Driver Code

# Number of elements
N = 5

# Given array arr[]
arr = [1, 4, 5, 6, 7]
M = 1
K = 2

# Function Call
print(xor_operations(N, arr, M, K))
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG{

// Method that returns the
// corresponding output by
// taking the given inputs.
static int xor_operations(int N, int []arr,
                          int M, int K)
{
  // If this condition is satisfied,
  // value of M is invalid
  if (M < 0 || M >= N)
    return -1;

  // Check if index K is valid
  if (K < 0 || K >= N - M)
    return -1;

  // Loop to perform M operations
  for(int p = 0; p < M; p++)
  {
    // Creating a temporary list
    List<int>temp = new List<int>();

    // Traversing the array
    for(int i = 0; i < N - 1; i++)
    {
      // Calculate XOR values
      // of adjacent elements
      int value = arr[i] ^ arr[i + 1];

      // Adding this value to
      // the temporary list
      temp.Add(value);

      // Update the original array
      arr[i] = temp[i];
    }
  }

  // Getting value at index K
  int ans = arr[K];

  return ans;
}

// Driver Code
public static void Main(String[] args)
{
  // Number of elements
  int N = 5;

  // Given array []arr
  int []arr = {1, 4, 5, 6, 7};
  int M = 1, K = 2;

  // Function call
  Console.Write(xor_operations(N, arr,
                               M, K));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // Javascript program for the above approach

    // Method that returns the
    // corresponding output by
    // taking the given inputs.
    function xor_operations(N, arr, M, K)
    {

        // If this condition is satisfied,
        // value of M is invalid
        if (M < 0 || M >= N)
            return -1;

        // Check if index K is valid
        if (K < 0 || K >= N - M)
            return -1;

        // Loop to perform M operations
        for(let p = 0; p < M; p++)
        {

            // Creating a temporary list
            let temp = [];

            // Traversing the array
            for(let i = 0; i < N; i++)
            {

                // Calculate XOR values
                // of adjacent elements
                let value = arr[i] ^ arr[i + 1];

                // Adding this value to
                // the temporary list
                temp.push(value);

                // Update the original array
                arr[i] = temp[i];
            }
        }

        // Getting value at index K
        let ans = arr[K];

        return ans;
    }

    // Number of elements
    let N = 5;

    // Given array arr[]
    let arr = [1, 4, 5, 6, 7];
    let M = 1, K = 2;

    // Function call
    document.write(xor_operations(N, arr, M, K));

</script>
```

**Output**

```
3
```

***时间复杂度:** O(M * N)*
***辅助空间:** O(N)*