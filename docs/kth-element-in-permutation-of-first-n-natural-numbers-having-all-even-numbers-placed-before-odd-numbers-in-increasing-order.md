# 前 N 个自然数排列中的第 k 个元素，所有偶数以递增顺序放在奇数之前

> 原文:[https://www . geesforgeks . org/kth-第一个 n 个自然数排列中的元素-将所有偶数放在奇数之前-递增顺序/](https://www.geeksforgeeks.org/kth-element-in-permutation-of-first-n-natural-numbers-having-all-even-numbers-placed-before-odd-numbers-in-increasing-order/)

给定两个整数 **N** 和 **K** ，任务是在排列的第一个**N**T10】自然数的排列中找到第 **K <sup>第</sup>T7】元素，使得所有偶数以递增的顺序出现在奇数之前。**

**示例:**

> **输入:** N = 10，K = 3
> **输出:** 6
> **说明:**
> 需要的排列是{2，4，6，8，10，1，3，5，7，9}。
> 排列中的 3 <sup>rd</sup> 数为 6。
> 
> **输入:** N = 5，K = 4
> **输出:** 3
> **说明:**
> 需要的排列是{2，4，1，3，5}。
> 排列中的第 4 个<sup>数是 3。</sup>

**天真方法:**解决问题最简单的方法是首先生成所需的[排列的 **N** 自然数](https://www.geeksforgeeks.org/check-if-an-array-is-a-permutation-of-numbers-from-1-to-n/)，然后遍历排列找到其中存在的 **K <sup>th</sup>** 元素。
按照以下步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/array-data-structure/)，说 **V[]** 大小 **N** 。，以存储所需的序列。
*   将所有小于或等于 **N** 的偶数插入 **V[]** 。
*   然后，将所有小于或等于 **N** 的奇数插入 **V[]** 。
*   形成数组后，打印**V【K–1】**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the K-th element
// in the required permutation
void findKthElement(int N, int K)
{
    // Stores the required permutation
    vector<int> v;

    // Insert all the even numbers
    // less than or equal to N
    for (int i = 1; i <= N; i++) {
        if (i % 2 == 0) {
            v.push_back(i);
        }
    }

    // Now, insert all odd numbers
    // less than or equal to N
    for (int i = 1; i <= N; i++) {
        if (i % 2 != 0) {
            v.push_back(i);
        }
    }

    // Print the Kth element
    cout << v[K - 1];
}

// Driver Code
int main()
{
    int N = 10, K = 3;
    findKthElement(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;
class GFG
{

  // Function to find the K-th element
  // in the required permutation
  static void findKthElement(int N, int K)
  {

    // Stores the required permutation
    ArrayList<Integer> v = new ArrayList<>();

    // Insert all the even numbers
    // less than or equal to N
    for (int i = 1; i <= N; i++) {
      if (i % 2 == 0) {
        v.add(i);
      }
    }

    // Now, insert all odd numbers
    // less than or equal to N
    for (int i = 1; i <= N; i++) {
      if (i % 2 != 0) {
        v.add(i);
      }
    }

    // Print the Kth element
    System.out.println(v.get(K - 1));
  }

  // Driver code
  public static void main(String[] args)
  {

    int N = 10, K = 3;

    // functions call
    findKthElement(N, K);
  }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# python 3 program for the above approach

# Function to find the K-th element
# in the required permutation
def findKthElement(N, K):

    # Stores the required permutation
    v = []

    # Insert all the even numbers
    # less than or equal to N
    for i in range(1, N + 1):
        if (i % 2 == 0):
            v.append(i)

    # Now, insert all odd numbers
    # less than or equal to N
    for i in range(1, N + 1):
        if (i % 2 != 0):
            v.append(i)

    # Print the Kth element
    print(v[K - 1])

# Driver Code
if __name__ == "__main__":
    N = 10
    K = 3
    findKthElement(N, K)

    # This code is contributed by ukasp.
```

## C#

```
// C# program for above approach
using System;
using System.Collections.Generic;

public class GFG
{

  // Function to find the K-th element
  // in the required permutation
  static void findKthElement(int N, int K)
  {

    // Stores the required permutation
    List<int> v = new List<int>();

    // Insert all the even numbers
    // less than or equal to N
    for (int i = 1; i <= N; i++) {
      if (i % 2 == 0) {
        v.Add(i);
      }
    }

    // Now, insert all odd numbers
    // less than or equal to N
    for (int i = 1; i <= N; i++) {
      if (i % 2 != 0) {
        v.Add(i);
      }
    }

    // Print the Kth element
    Console.WriteLine(v[K - 1]);
  }

  // Driver code
  public static void Main(String[] args)
  {
    int N = 10, K = 3;

    // functions call
    findKthElement(N, K);
  }
}

// This code is contributed by susmitakundugoaldanga.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Function to find the K-th element
    // in the required permutation
    function findKthElement(N , K) {

        // Stores the required permutation
        var v = [];

        // Insert all the even numbers
        // less than or equal to N
        for (i = 1; i <= N; i++) {
            if (i % 2 == 0) {
                v.push(i);
            }
        }

        // Now, insert all odd numbers
        // less than or equal to N
        for (i = 1; i <= N; i++) {
            if (i % 2 != 0) {
                v.push(i);
            }
        }

        // Print the Kth element
        document.write(v[K - 1]);
    }

    // Driver code

        var N = 10, K = 3;

        // functions call
        findKthElement(N, K);

// This code contributed by Rajput-Ji

</script>
```

**Output**

```
6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)

**高效进场:**对上述进场进行优化，思路是基于前半段第一 **N / 2** 元素为偶数，**K<sup>th</sup>T7】元素的值等于 **K * 2** 。如果 **K > N/2** ， **K <sup>th</sup>** 元素的值取决于 [**N** 是奇数还是偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)。
按照以下步骤解决问题:**

*   初始化一个变量，说 **ans，**来存储**K<sup>th</sup>T5】元素。**
*   检查 **K 值是否≤ N/2** 。如果发现属实，将 **ans** 更新为 **K*2** 。
*   否则 **K** 位于后半段。在这种情况下， **ans** 取决于 **N** 的值。
    *   [如果 **N** 的值为偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，则将 **ans** 更新为 **(K*2)-N-1** 。
    *   否则，将 **ans** 更新为 **(K*2)-N** 。
*   打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the Kth element
// in the required permutation
void findKthElement(int N, int K)
{
    // Store the required result
    int ans = 0;

    // If K is in the first
    // N / 2 elements, print K * 2
    if (K <= N / 2) {
        ans = K * 2;
    }

    // Otherwise, K is greater than N/2
    else {

        // If N is even
        if (N % 2 == 0) {
            ans = (K * 2) - N - 1;
        }

        // If N is odd
        else {
            ans = (K * 2) - N;
        }
    }

    // Print the required result
    cout << ans;
}

// Driver Code
int main()
{
    int N = 10, K = 3;
    findKthElement(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;
class GFG {

  // Function to find the Kth element
  // in the required permutation
  static void findKthElement(int N, int K)
  {
    // Store the required result
    int ans = 0;

    // If K is in the first
    // N / 2 elements, print K * 2
    if (K <= N / 2) {
      ans = K * 2;
    }

    // Otherwise, K is greater than N/2
    else {

      // If N is even
      if (N % 2 == 0) {
        ans = (K * 2) - N - 1;
      }

      // If N is odd
      else {
        ans = (K * 2) - N;
      }
    }

    // Print the required result
    System.out.println(ans);
  }

  // Driver code
  public static void main(String[] args)
  {

    int N = 10, K = 3;

    // functions call
    findKthElement(N, K);
  }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the Kth element
# in the required permutation
def findKthElement(N, K):

    # Store the required result
    ans = 0

    # If K is in the first
    # N / 2 elements, print K * 2
    if (K <= N / 2):
        ans = K * 2

    # Otherwise, K is greater than N/2
    else:

        # If N is even
        if (N % 2 == 0):
            ans = (K * 2) - N - 1

        # If N is odd
        else:
            ans = (K * 2) - N

    # Print the required result
    print(ans)

# Driver Code
if __name__ == '__main__':
    N = 10
    K = 3
    findKthElement(N, K)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

  // Function to find the Kth element
  // in the required permutation
  static void findKthElement(int N, int K)
  {

    // Store the required result
    int ans = 0;

    // If K is in the first
    // N / 2 elements, print K * 2
    if (K <= N / 2) {
      ans = K * 2;
    }

    // Otherwise, K is greater than N/2
    else {

      // If N is even
      if (N % 2 == 0) {
        ans = (K * 2) - N - 1;
      }

      // If N is odd
      else {
        ans = (K * 2) - N;
      }
    }

    // Print the required result
    Console.Write(ans);
  }

  // Driver code
  static void Main()
  {
    int N = 10, K = 3;

    // functions call
    findKthElement(N, K);
  }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>
// javascript program for the above approach

// Function to find the Kth element
// in the required permutation
function findKthElement( N,  K)
{

    // Store the required result
    let ans = 0;

    // If K is in the first
    // N / 2 elements, print K * 2
    if (K <= N / 2)
    {
        ans = K * 2;
    }

    // Otherwise, K is greater than N/2
    else
    {

        // If N is even
        if (N % 2 == 0)
        {
            ans = (K * 2) - N - 1;
        }

        // If N is odd
        else
        {
            ans = (K * 2) - N;
        }
    }

    // Print the required result
    document.write(ans);
}

// Driver Code
    let N = 10, K = 3;
    findKthElement(N, K);

// This code is contributed by todaysgaurav
</script>
```

**Output**

```
6
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)