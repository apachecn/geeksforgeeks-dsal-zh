# 最小正整数 K，通过增加或减少最多 K 个

可以使所有数组元素相等

> 原文:[https://www . geesforgeks . org/minist-正整数-k-so-所有数组元素都可以通过最多 k 个元素的递增或递减来使其相等/](https://www.geeksforgeeks.org/smallest-positive-integer-k-such-that-all-array-elements-can-be-made-equal-by-incrementing-or-decrementing-by-at-most-k/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是找到最小正整数 **K** ，使得将每个数组元素递增或递减 **K** 至多一次使所有元素相等。如果无法使所有数组元素相等，则打印 **-1** 。

**示例:**

> **输入:** arr[] = { 5，7，9 }
> **输出:** 2
> **解释:**
> 将 arr[0]的值增加 K(= 2)会将 arr[]修改为{ 7，7，9 }。
> 将 arr[2]的值减 K(= 2)会将 arr[]修改为{ 7，7，7 }
> 
> **输入:** arr[] = {1，3，9}，N = 3
> **输出:** -1

**方法:**按照以下步骤解决问题:

*   初始化一个[设置](https://www.geeksforgeeks.org/set-in-cpp-stl/)来存储数组中存在的所有[不同元素。](https://www.geeksforgeeks.org/print-distinct-elements-given-integer-array/)
*   [计算数组](https://www.geeksforgeeks.org/setsize-c-stl/)中不同的元素，等于集合的[大小，比如 **M** 。](https://www.geeksforgeeks.org/setsize-c-stl/)
*   如果 **M > 3** ，则打印 **-1** 。
*   如果 **M = 3** ，则检查集合的最大和第二大元素之间的差是否等于集合的第二大和第三大元素之间的差。如果发现是真的，那么打印差异。否则，打印 **-1** 。
*   如果 **M = 2** ，则检查集合中最大元素和第二大元素的差是否为偶数。如果发现是真的，那就打印出他们差额的一半。否则，打印差异。
*   如果 **M < = 1** ，则打印 **0** 。

下面是上述解决方案的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
#include <set>
using namespace std;

// Function to find smallest integer K such that
// incrementing or decrementing each element by
// K at most once makes all elements equal
void findMinKToMakeAllEqual(int N, int A[])
{

    // Store distinct
    // array elements
    set<int> B;

    // Traverse the array, A[]
    for (int i = 0; i < N; i++)
        B.insert(A[i]);

    // Count elements into the set
    int M = B.size();

    // Iterator to store first
    // element of B
    set<int>::iterator itr = B.begin();

    // If M is greater than 3
    if (M > 3)
        printf("-1");

    // If M is equal to 3
    else if (M == 3) {

        // Stores the first
        // smallest element
        int B_1 = *itr;

        // Stores the second
        // smallest element
        int B_2 = *(++itr);

        // Stores the largest element
        int B_3 = *(++itr);

        // IF difference between B_2 and B_1
        // is equal to B_3 and B_2
        if (B_2 - B_1 == B_3 - B_2)
            printf("%d", B_2 - B_1);
        else
            printf("-1");
    }

    // If M is equal to 2
    else if (M == 2) {

        // Stores the smallest element
        int B_1 = *itr;

        // Stores the largest element
        int B_2 = *(++itr);

        // If difference is an even
        if ((B_2 - B_1) % 2 == 0)
            printf("%d", (B_2 - B_1) / 2);
        else
            printf("%d", B_2 - B_1);
    }

    // If M is equal to 1
    else
        printf("%d", 0);
}

// Driver Code
int main()
{

    // Given array
    int A[] = { 1, 3, 5, 1 };

    // Given size
    int N = sizeof(A) / sizeof(A[0]);

    // Print the required smallest integer
    findMinKToMakeAllEqual(N, A);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;
class GFG {

    // Function to find smallest integer K such that
    // incrementing or decrementing each element by
    // K at most once makes all elements equal
    static void findMinKToMakeAllEqual(int N, int A[])
    {

        // Store distinct
        // array elements
        Set<Integer> B = new HashSet<Integer>();

        // Traverse the array, A[]
        for (int i = 0; i < N; i++)
        {
            B.add(A[i]);
        }

        ArrayList<Integer> b = new ArrayList<Integer>(B);

        // Count elements into the set
        int M = b.size();
        int i = 0;

        // If M is greater than 3
        if (M > 3)
        {    System.out.print("-1");}

        // If M is equal to 3
        else if (M == 3)
        {

            // Stores the first
            // smallest element
            int B_1 = b.get(i++);

            // Stores the second
            // smallest element
            int B_2 =  b.get(i++);

            // Stores the largest element
            int B_3 = b.get(i++);

            // IF difference between B_2 and B_1
            // is equal to B_3 and B_2
            if (B_2 - B_1 == B_3 - B_2)
            {
                System.out.print(B_2 - B_1);
            }
            else
            {
                System.out.print("-1");
            }

        }

        // If M is equal to 2
        else if (M == 2)
        {

            // Stores the smallest element
            int B_1 = b.get(i++);

            // Stores the largest element
            int B_2 = b.get(i++);

            // If difference is an even
            if ((B_2 - B_1) % 2 == 0)
            {
                System.out.print((B_2 - B_1) / 2);
            }

            else
            {
                System.out.print(B_2 - B_1);
            }
        }
        // If M is equal to 1
        else
        {
            System.out.print(0);
        }
    }

  // Driver code
    public static void main (String[] args)
    {

        // Given array
        int A[] = { 1, 3, 5, 1 };

        // Given size
        int N = A.length;

        // Print the required smallest integer
        findMinKToMakeAllEqual(N, A);
    }
}

// This code is contributed by rag2127
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find smallest integer K such
# that incrementing or decrementing each
# element by K at most once makes all
# elements equal
def findMinKToMakeAllEqual(N, A):

    # Store distinct
    # array elements
    B = {}

    # Traverse the array, A[]
    for i in range(N):
        B[A[i]] = 1

    # Count elements into the set
    M = len(B)

    # Iterator to store first
    # element of B
    itr, i = list(B.keys()), 0

    # If M is greater than 3
    if (M > 3):
        print("-1")

    # If M is equal to 3
    elif (M == 3):

        # Stores the first
        # smallest element
        B_1, i = itr[i], i + 1

        # Stores the second
        # smallest element
        B_2, i = itr[i], i + 1

        # Stores the largest element
        B_3, i = itr[i], i + 1

        # IF difference between B_2 and B_1
        # is equal to B_3 and B_2
        if (B_2 - B_1 == B_3 - B_2):
            print(B_2 - B_1)
        else:
            print("-1")

    # If M is equal to 2
    elif (M == 2):

        # Stores the smallest element
        B_1, i = itr[i], i + 1

        # Stores the largest element
        B_2, i = itr[i], i + 1

        # If difference is an even
        if ((B_2 - B_1) % 2 == 0):
            print((B_2 - B_1) // 2)
        else:
            print(B_2 - B_1)

    # If M is equal to 1
    else:
        print(0)

# Driver Code
if __name__ == '__main__':

    # Given array
    A = [ 1, 3, 5, 1 ]

    # Given size
    N = len(A)

    # Print the required smallest integer
    findMinKToMakeAllEqual(N, A)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

  // Function to find smallest integer K such that
  // incrementing or decrementing each element by
  // K at most once makes all elements equal
  static void findMinKToMakeAllEqual(int N, int[] A)
  {

    // Store distinct
    // array elements
    var B = new HashSet<int>();

    // Traverse the array, A[]
    for (int i = 0; i < N; i++) {
      B.Add(A[i]);
    }

    List<int> b = new List<int>(B);

    // Count elements into the set
    int M = b.Count;
    int j = 0;

    // If M is greater than 3
    if (M > 3) {
      Console.Write("-1");
    }

    // If M is equal to 3
    else if (M == 3) {

      // Stores the first
      // smallest element
      int B_1 = b[j++];

      // Stores the second
      // smallest element
      int B_2 = b[j++];

      // Stores the largest element
      int B_3 = b[j++];

      // IF difference between B_2 and B_1
      // is equal to B_3 and B_2
      if (B_2 - B_1 == B_3 - B_2) {
        Console.Write(B_2 - B_1);
      }
      else {
        Console.Write("-1");
      }
    }

    // If M is equal to 2
    else if (M == 2) {

      // Stores the smallest element
      int B_1 = b[j++];

      // Stores the largest element
      int B_2 = b[j++];

      // If difference is an even
      if ((B_2 - B_1) % 2 == 0) {
        Console.Write((B_2 - B_1) / 2);
      }

      else {
        Console.Write(B_2 - B_1);
      }
    }
    // If M is equal to 1
    else {
      Console.Write(0);
    }
  }

  // Driver code
  public static void Main(string[] args)
  {

    // Given array
    int[] A = { 1, 3, 5, 1 };

    // Given size
    int N = A.Length;

    // Print the required smallest integer
    findMinKToMakeAllEqual(N, A);
  }
}

// This code is contributed by chitranayal.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find smallest integer K such that
// incrementing or decrementing each element by
// K at most once makes all elements equal
function findMinKToMakeAllEqual(N, A)
{

    // Store distinct
    // array elements
    var B = new Set();

    // Traverse the array, A[]
    for(var i = 0; i < N; i++)
        B.add(A[i]);

    // Count elements into the set
    var M = B.size;

    // Iterator to store first
    // element of B
    var itr = [...B].sort((a, b) => a - b);

    // If M is greater than 3
    if (M > 3)
        document.write("-1");

    // If M is equal to 3
    else if (M == 3)
    {

        // Stores the first
        // smallest element
        var B_1 = itr[0];

        // Stores the second
        // smallest element
        var B_2 = itr[1];

        // Stores the largest element
        var B_3 = itr[2];

        // IF difference between B_2 and B_1
        // is equal to B_3 and B_2
        if (B_2 - B_1 == B_3 - B_2)
            document.write(B_2 - B_1);
        else
            document.write("-1");
    }

    // If M is equal to 2
    else if (M == 2)
    {

        // Stores the smallest element
        var B_1 = itr[0];

        // Stores the largest element
        var B_2 =itr[1];

        // If difference is an even
        if ((B_2 - B_1) % 2 == 0)
            document.write(parseInt((B_2 - B_1) / 2));
        else
            document.write(B_2 - B_1);
    }

    // If M is equal to 1
    else
        document.write(0);
}

// Driver Code

// Given array
var A = [ 1, 3, 5, 1 ];

// Given size
var N = A.length;

// Print the required smallest integer
findMinKToMakeAllEqual(N, A);

// This code is contributed by noob2000

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(N)*