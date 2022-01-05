# 给定范围内的元素和，从无限连接给定数组形成的数组

> 原文:[https://www . geeksforgeeks . org/给定范围内的元素总和由无限连接给定数组形成的数组/](https://www.geeksforgeeks.org/sum-of-elements-in-given-range-from-array-formed-by-infinitely-concatenating-given-array/)

给定一个由 **N** 个正整数和两个正整数 **L** 和 **R** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**(基于 1 的索引)，如果给定的数组**arr【】**连接到自身无限次，那么任务就是找出该范围内的数组元素之和**【L，R】**。

**示例:**

> **输入:** arr[] = {1，2，3}，L = 2，R = 8
> **输出:** 14
> **解释:**
> 串联后的数组 arr[]，是{1，2，3，1，2，3，1，1，2，…}从索引 2 到 8 的元素之和是 2 + 3 + 1 + 2 + 3 + 1 + 2 = 14。
> 
> **输入:** arr[] = {5，2，6，9}，L = 10，R = 13
> **输出:** 22

**天真方法:**解决给定问题的最简单方法是使用变量 **i** 迭代范围**【L，R】**，并将**arr【I % N】**的值加到每个指标的**和**上。迭代完成后，打印**和**的值作为结果和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of elements
// in a given range of an infinite array
void rangeSum(int arr[], int N, int L, int R)
{
    // Stores the sum of array elements
    // from L to R
    int sum = 0;

    // Traverse from L to R
    for (int i = L - 1; i < R; i++) {
        sum += arr[i % N];
    }

    // Print the resultant sum
    cout << sum;
}

// Driver Code
int main()
{
    int arr[] = { 5, 2, 6, 9 };
    int L = 10, R = 13;
    int N = sizeof(arr) / sizeof(arr[0]);
    rangeSum(arr, N, L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

    // Function to find the sum of elements
    // in a given range of an infinite array
    static void rangeSum(int arr[], int N, int L, int R)
    {

        // Stores the sum of array elements
        // from L to R
        int sum = 0;

        // Traverse from L to R
        for (int i = L - 1; i < R; i++) {
            sum += arr[i % N];
        }

        // Print the resultant sum
        System.out.println(sum);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 5, 2, 6, 9 };
        int L = 10, R = 13;
        int N = arr.length;
        rangeSum(arr, N, L, R);
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the sum of elements
# in a given range of an infinite array
def rangeSum(arr, N, L, R):

    # Stores the sum of array elements
    # from L to R
    sum = 0

    # Traverse from L to R
    for i in range(L - 1,R,1):
        sum += arr[i % N]

    # Print the resultant sum
    print(sum)

# Driver Code
if __name__ == '__main__':
    arr = [5, 2, 6, 9 ]
    L = 10
    R = 13
    N = len(arr)
    rangeSum(arr, N, L, R)

    # This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to find the sum of elements
    // in a given range of an infinite array
    static void rangeSum(int[] arr, int N, int L, int R)
    {

        // Stores the sum of array elements
        // from L to R
        int sum = 0;

        // Traverse from L to R
        for (int i = L - 1; i < R; i++) {
            sum += arr[i % N];
        }

        // Print the resultant sum
        Console.Write(sum);
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int[] arr = { 5, 2, 6, 9 };
        int L = 10, R = 13;
        int N = arr.Length;
        rangeSum(arr, N, L, R);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the sum of elements
// in a given range of an infinite array
function rangeSum(arr, N, L, R)
{

    // Stores the sum of array elements
    // from L to R
    let sum = 0;

    // Traverse from L to R
    for(let i = L - 1; i < R; i++)
    {
        sum += arr[i % N];
    }

    // Print the resultant sum
    document.write(sum);
}

// Driver Code
let arr = [ 5, 2, 6, 9 ];
let L = 10, R = 13;
let N = arr.length

rangeSum(arr, N, L, R);

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
22
```

***时间复杂度:**O(R–L)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以通过使用[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)进行优化。按照以下步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/array-data-structure/)，说**前缀[]** 大小为 **(N + 1)** ，所有元素为 **0s** 。
*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)、 **arr[]** ，并将**前缀【I】**更新为**前缀【I–1】**和**arr【I–1】**之和。
*   现在，范围**【L，R】**内的元素之和由下式给出:

> 范围内的元素之和**【1，R】**–范围内的元素之和**【1，L–1】**。

*   初始化一个变量，说 **leftSum** 为**((L–1)/N)*前缀【N】****+****前缀[(L–1)% N]**存储范围**【1，L-1】**内的元素之和。
*   同样，将另一个变量 **rightSum** 初始化为**(R/N)*前缀【N】+前缀【R % N】**来存储范围**【1，R】**内的元素之和。
*   完成上述步骤后，打印**(右总和–左总和)**的值，作为给定范围内**【L，R】**元素的合成总和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of elements
// in a given range of an infinite array
void rangeSum(int arr[], int N, int L,
              int R)
{
    // Stores the prefix sum
    int prefix[N + 1];
    prefix[0] = 0;

    // Calculate the prefix sum
    for (int i = 1; i <= N; i++) {
        prefix[i] = prefix[i - 1]
                    + arr[i - 1];
    }

    // Stores the sum of elements
    // from 1 to L-1
    int leftsum
        = ((L - 1) / N) * prefix[N]
          + prefix[(L - 1) % N];

    // Stores the sum of elements
    // from 1 to R
    int rightsum = (R / N) * prefix[N]
                   + prefix[R % N];

    // Print the resultant sum
    cout << rightsum - leftsum;
}

// Driver Code
int main()
{
    int arr[] = { 5, 2, 6, 9 };
    int L = 10, R = 13;
    int N = sizeof(arr) / sizeof(arr[0]);
    rangeSum(arr, N, L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find the sum of elements
// in a given range of an infinite array
static void rangeSum(int arr[], int N, int L, int R)
{

    // Stores the prefix sum
    int prefix[] = new int[N+1];
    prefix[0] = 0;

    // Calculate the prefix sum
    for (int i = 1; i <= N; i++) {
        prefix[i] = prefix[i - 1]
                    + arr[i - 1];
    }

    // Stores the sum of elements
    // from 1 to L-1
    int leftsum
        = ((L - 1) / N) * prefix[N]
          + prefix[(L - 1) % N];

    // Stores the sum of elements
    // from 1 to R
    int rightsum = (R / N) * prefix[N]
                   + prefix[R % N];

    // Print the resultant sum
    System.out.print( rightsum - leftsum);
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = { 5, 2, 6, 9 };
    int L = 10, R = 13;
    int N = arr.length;
    rangeSum(arr, N, L, R);

}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the sum of elements
# in a given range of an infinite array
def rangeSum(arr, N, L, R):

    # Stores the prefix sum
    prefix = [0 for i in range(N + 1)]
    prefix[0] = 0

    # Calculate the prefix sum
    for i in range(1,N+1,1):
        prefix[i] = prefix[i - 1] + arr[i - 1]

    # Stores the sum of elements
    # from 1 to L-1
    leftsum = ((L - 1) // N) * prefix[N] + prefix[(L - 1) % N]

    # Stores the sum of elements
    # from 1 to R
    rightsum = (R // N) * prefix[N] + prefix[R % N]

    # Print the resultant sum
    print(rightsum - leftsum)

# Driver Code
if __name__ == '__main__':
    arr = [5, 2, 6, 9]
    L = 10
    R = 13
    N = len(arr)
    rangeSum(arr, N, L, R)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the sum of elements
// in a given range of an infinite array
static void rangeSum(int []arr, int N, int L, int R)
{

    // Stores the prefix sum
    int []prefix = new int[N+1];
    prefix[0] = 0;

    // Calculate the prefix sum
    for (int i = 1; i <= N; i++) {
        prefix[i] = prefix[i - 1]
                    + arr[i - 1];
    }

    // Stores the sum of elements
    // from 1 to L-1
    int leftsum
        = ((L - 1) / N) * prefix[N]
          + prefix[(L - 1) % N];

    // Stores the sum of elements
    // from 1 to R
    int rightsum = (R / N) * prefix[N]
                   + prefix[R % N];

    // Print the resultant sum
    Console.Write( rightsum - leftsum);
}

// Driver Code
public static void Main (String[] args)
{
    int []arr = { 5, 2, 6, 9 };
    int L = 10, R = 13;
    int N = arr.Length;
    rangeSum(arr, N, L, R);

}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the sum of elements
// in a given range of an infinite array
function rangeSum(arr, N, L, R) {
  // Stores the prefix sum
  let prefix = new Array(N + 1);
  prefix[0] = 0;

  // Calculate the prefix sum
  for (let i = 1; i <= N; i++) {
    prefix[i] = prefix[i - 1] + arr[i - 1];
  }

  // Stores the sum of elements
  // from 1 to L-1
  let leftsum = ((L - 1) / N) * prefix[N] + prefix[(L - 1) % N];

  // Stores the sum of elements
  // from 1 to R
  let rightsum = (R / N) * prefix[N] + prefix[R % N];

  // Print the resultant sum
  document.write(rightsum - leftsum);
}

// Driver Code

let arr = [5, 2, 6, 9];
let L = 10,
  R = 13;
let N = arr.length;
rangeSum(arr, N, L, R);

</script>
```

**Output:** 

```
22
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)