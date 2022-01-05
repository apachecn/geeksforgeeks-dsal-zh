# 对放置在两个给定数组的相同索引处的相同值的元素进行计数

> 原文:[https://www . geeksforgeeks . org/count-同值元素-放在两个给定数组的相同索引处/](https://www.geeksforgeeks.org/count-elements-of-same-value-placed-at-same-indices-of-two-given-arrays/)

给定 **N** *唯一元素*的两个数组 **A[]** 和 **B[]** ，任务是从两个给定数组中找到最大数量的匹配元素。

> 如果两个数组的元素具有相同的值，并且可以放在相同的索引处(基于 *0 的索引*)，则它们是匹配的。(通过两个阵列的右移或左移)。

**示例:**

> **输入:** A[] = { 5，3，7，9，8 }，B[] = { 8，7，3，5，9 }
> **输出:** 3
> **解释:**向左移动 B[]，1 个索引将 B[]修改为{ 7，3，5，9，8 }。
> 因此，索引 1、3 和 4 中的元素匹配。因此，所需的计数是 3。
> 
> **输入:** A[] = { 9，5，6，2 }，B[] = { 6，2，9，5 }
> **输出:** 4

**幼稚的做法:**解决这个问题最简单的做法就是观察**一个右挡**和 **(N-1)左挡**是一样的，所以只执行一种类型的换挡，比如右挡。另外，在 **A** 上执行右移与执行左移 **B、**相同，所以只在一个阵列上执行右移，比如在 **A[]** 上。在保持 **B** 不变的情况下，对 **A** 进行右移操作，比较 **A** 和 **B** 的所有值，找出匹配的总数，并跟踪所有值的最大值。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述方法可以通过使用[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)来跟踪数组中存在的相等元素的索引之间的差异来优化 **A[]** 和 **B[]** 。如果差出来是负的，那么通过做 **k( = N +差)**左移来改变 **A[]** ，相当于**N–K**右移。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count maximum matched
// elements from the arrays A[] and B[]
int maxMatch(int A[], int B[], int M, int N)
{

    // Stores position of elements of
    // array A[] in the array B[]
    map<int,int> Aindex;

    // Keep track of difference
    // between the indices
    map<int,int> diff;

    // Traverse the array A[]
    for(int i = 0; i < M; i++)
    {
        Aindex[A[i]] = i ;
    }

    // Traverse the array B[]
    for(int i = 0; i < N; i++)
    {

        // If difference is negative, add N to it
        if (i - Aindex[B[i]] < 0)
        {     
            diff[M + i - Aindex[B[i]]] += 1;
        }

        // Keep track of the number of shifts
        // required to place elements at same indices
        else
        {
            diff[i - Aindex[B[i]]] += 1;
        }
    }

    // Return the max matches
    int max = 0;
    for(auto ele = diff.begin(); ele != diff.end(); ele++)
    {
        if(ele->second > max)
        {
            max = ele->second;
        }
    }
    return max;
}

// Driver code
int main()
{
    int A[] = { 5, 3, 7, 9, 8 };
    int B[] = { 8, 7, 3, 5, 9 };  
    int M = sizeof(A) / sizeof(A[0]);
    int N = sizeof(B) / sizeof(B[0]);

    // Returns the count 
    // of matched elements
    cout << maxMatch(A, B, M, N);
    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.Console;
import java.util.HashMap;
import java.util.Map;
class GFG
{

  // Function to count maximum matched
  // elements from the arrays A[] and B[]
  static int maxMatch(int[] A, int[] B)
  {

    // Stores position of elements of
    // array A[] in the array B[]
    HashMap<Integer, Integer> Aindex = new HashMap<Integer, Integer>();

    // Keep track of difference
    // between the indices
    HashMap<Integer, Integer> diff = new HashMap<Integer, Integer>();

    // Traverse the array A[]
    for (int i = 0; i < A.length; i++)
    {
      Aindex.put(A[i], i);
    }

    // Traverse the array B[]
    for (int i = 0; i < B.length; i++)
    {

      // If difference is negative, add N to it
      if (i - Aindex.get(B[i]) < 0)
      {
        if (!diff.containsKey(A.length + i - Aindex.get(B[i])))
        {
          diff.put(A.length + i - Aindex.get(B[i]), 1);
        } else {
          diff.put(A.length + i - Aindex.get(B[i]), diff.get(A.length + i - Aindex.get(B[i])) + 1);
        }
      }

      // Keep track of the number of shifts
      // required to place elements at same indices
      else {
        if (!diff.containsKey(i - Aindex.get(B[i]))) {
          diff.put(i - Aindex.get(B[i]), 1);
        }
        else
        {
          diff.put(i - Aindex.get(B[i]),
                   diff.get(i - Aindex.get(B[i])) + 1);
        }
      }
    }

    // Return the max matches
    int max = 0;
    for (Map.Entry<Integer, Integer> ele : diff.entrySet())
    {
      if (ele.getValue() > max)
      {
        max = ele.getValue();
      }
    }
    return max;
  }

  // Driver Code
  public static void main(String[] args)
  {

    int[] A = { 5, 3, 7, 9, 8 };
    int[] B = { 8, 7, 3, 5, 9 };

    // Returns the count
    // of matched elements
    System.out.println(maxMatch(A, B));
  }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to count maximum matched
# elements from the arrays A[] and B[]
def maxMatch(A, B):

    # Stores position of elements of
    # array A[] in the array B[]
    Aindex = {}

    # Keep track of difference
    # between the indices
    diff = {}

    # Traverse the array A[]
    for i in range(len(A)):
        Aindex[A[i]] = i

    # Traverse the array B[]
    for i in range(len(B)):

        # If difference is negative, add N to it
        if i-Aindex[B[i]] < 0:

            if len(A)+i-Aindex[B[i]] not in diff:
                diff[len(A)+i-Aindex[B[i]]] = 1

            else:
                diff[len(A)+i-Aindex[B[i]]] += 1

        # Keep track of the number of shifts
        # required to place elements at same indices
        else:
            if i-Aindex[B[i]] not in diff:
                diff[i-Aindex[B[i]]] = 1
            else:
                diff[i-Aindex[B[i]]] += 1

    # Return the max matches
    return max(diff.values())

# Driver Code
A = [5, 3, 7, 9, 8]
B = [8, 7, 3, 5, 9]

# Returns the count
# of matched elements
print(maxMatch(A, B))
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to count maximum matched
// elements from the arrays A[] and B[]
static int maxMatch(int[] A, int[] B)
{

    // Stores position of elements of
    // array A[] in the array B[]
    Dictionary<int,
               int> Aindex = new Dictionary<int,
                                            int>(); 

    // Keep track of difference
    // between the indices
    Dictionary<int,
               int> diff = new Dictionary<int,
                                          int>(); 

    // Traverse the array A[]
    for(int i = 0; i < A.Length; i++)
    {
        Aindex[A[i]] = i ;
    }

    // Traverse the array B[]
    for(int i = 0; i < B.Length; i++)
    {

        // If difference is negative, add N to it
        if (i - Aindex[B[i]] < 0)
        {     
            if (!diff.ContainsKey(A.Length + i -
                                  Aindex[B[i]]))
            {
                diff[A.Length + i - Aindex[B[i]]] = 1;
            }     
            else
            {
                diff[A.Length + i - Aindex[B[i]]] += 1;
            }
        }

        // Keep track of the number of shifts
        // required to place elements at same indices
        else
        {
            if (!diff.ContainsKey(i - Aindex[B[i]]))
            {
                diff[i - Aindex[B[i]]] = 1;
            }
            else
            {
                diff[i - Aindex[B[i]]] += 1;
            }
        }
    }

    // Return the max matches
    int max = 0;
    foreach(KeyValuePair<int, int> ele in diff)
    {
        if (ele.Value > max)
        {
            max = ele.Value;
        }
    }
    return max;
}

// Driver Code   
static void Main()
{
    int[] A = { 5, 3, 7, 9, 8 };
    int[] B = { 8, 7, 3, 5, 9 };

    // Returns the count 
    // of matched elements
    Console.WriteLine(maxMatch(A, B));
}
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Function to count maximum matched
      // elements from the arrays A[] and B[]
      function maxMatch(A, B) {
        // Stores position of elements of
        // array A[] in the array B[]
        var Aindex = {};

        // Keep track of difference
        // between the indices
        var diff = {};

        // Traverse the array A[]
        for (var i = 0; i < A.length; i++) {
          Aindex[A[i]] = i;
        }

        // Traverse the array B[]
        for (var i = 0; i < B.length; i++) {
          // If difference is negative, add N to it
          if (i - Aindex[B[i]] < 0) {
            if (!diff.hasOwnProperty(A.length + i - Aindex[B[i]])) {
              diff[A.length + i - Aindex[B[i]]] = 1;
            }
            else {
              diff[A.length + i - Aindex[B[i]]] += 1;
            }
          }

          // Keep track of the number of shifts
          // required to place elements at same indices
          else {
            if (!diff.hasOwnProperty(i - Aindex[B[i]])) {
              diff[i - Aindex[B[i]]] = 1;
            }
            else {
              diff[i - Aindex[B[i]]] += 1;
            }
          }
        }

        // Return the max matches
        var max = 0;
        for (const [key, value] of Object.entries(diff)) {
          if (value > max) {
            max = value;
          }
        }
        return max;
      }

      // Driver Code
      var A = [5, 3, 7, 9, 8];
      var B = [8, 7, 3, 5, 9];

      // Returns the count
      // of matched elements
      document.write(maxMatch(A, B));
</script>
```

**输出:**

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)