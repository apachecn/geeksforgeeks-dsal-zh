# 找到给定数组中唯一的非重复元素

> 原文:[https://www . geeksforgeeks . org/find-给定数组中唯一的非重复元素/](https://www.geeksforgeeks.org/find-the-only-non-repeating-element-in-a-given-array/)

给定一个由**N**(*1≤**N**≤10<sup>5</sup>*)正整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **A[]** ，任务是找到唯一一个出现一次的数组元素。

***注:**保证数组中只存在一个这样的元素。*

**示例:**

> **输入:** A[] = {1，1，2，3，3}
> **输出:** 2
> **解释:**
> 不同的数组元素是{1，2，3}。
> 这些元素的频率分别为{2，1，2}。
> 
> **输入** : A[] = {1，1，1，2，2，3，5，3，4，4}
> 输出 : 5

**方法:**按照以下步骤解决问题

1.  遍历数组
2.  使用[无序映射](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)存储数组元素的[频率。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
3.  [遍历地图](https://www.geeksforgeeks.org/iterate-map-java/)和[找到频率为 1 的元素](https://www.geeksforgeeks.org/non-repeating-element/)并打印该元素。

下面是上述方法的实现:

## C++

```
// C++ implementation of the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Function call to find
// element in A[] with frequency = 1
void CalcUnique(int A[], int N)
{
    // Stores frequency of
    // array elements
    unordered_map<int, int> freq;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update frequency of A[i]
        freq[A[i]]++;
    }

    // Traverse the Map
    for (int i = 0; i < N; i++) {

        // If non-repeating element
        // is found
        if (freq[A[i]] == 1) {

            cout << A[i];
            return;
        }
    }
}

// Driver Code
int main()
{
    int A[] = { 1, 1, 2, 3, 3 };
    int N = sizeof(A) / sizeof(A[0]);

    CalcUnique(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
import java.util.*;
class GFG
{

  // Function call to find
  // element in A[] with frequency = 1
  static void CalcUnique(int A[], int N)
  {
    // Stores frequency of
    // array elements
    HashMap<Integer,Integer> freq = new HashMap<Integer,Integer>();

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

      // Update frequency of A[i]
      if(freq.containsKey(A[i]))
      {
        freq.put(A[i], freq.get(A[i]) + 1);
      }
      else
      {
        freq.put(A[i], 1);
      }
    }

    // Traverse the Map
    for (int i = 0; i < N; i++)
    {

      // If non-repeating element
      // is found
      if (freq.containsKey(A[i])&&freq.get(A[i]) == 1)
      {
        System.out.print(A[i]);
        return;
      }
    }
  }

  // Driver Code
  public static void main(String[] args)
  {
    int A[] = { 1, 1, 2, 3, 3 };
    int N = A.length;
    CalcUnique(A, N);
  }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of the
# above approach
from collections import defaultdict

# Function call to find
# element in A[] with frequency = 1
def CalcUnique(A, N):

    # Stores frequency of
    # array elements
    freq = defaultdict(int)

    # Traverse the array
    for i in range(N):

        # Update frequency of A[i]
        freq[A[i]] += 1

    # Traverse the Map
    for i in range(N):

        # If non-repeating element
        # is found
        if (freq[A[i]] == 1):
            print(A[i])
            return

# Driver Code
if __name__ == "__main__":
    A = [1, 1, 2, 3, 3]
    N = len(A)
    CalcUnique(A, N)

    # This code is contributed by chitranayal.
```

## C#

```
// C# implementation of the
// above approach
using System;
using System.Collections.Generic;

public class GFG
{

  // Function call to find
  // element in []A with frequency = 1
  static void CalcUnique(int []A, int N)
  {

    // Stores frequency of
    // array elements
    Dictionary<int,int> freq = new Dictionary<int,int>();

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

      // Update frequency of A[i]
      if(freq.ContainsKey(A[i]))
      {
        freq[A[i]] = freq[A[i]] + 1;
      }
      else
      {
        freq.Add(A[i], 1);
      }
    }

    // Traverse the Map
    for (int i = 0; i < N; i++)
    {

      // If non-repeating element
      // is found
      if (freq.ContainsKey(A[i]) && freq[A[i]] == 1)
      {
        Console.Write(A[i]);
        return;
      }
    }
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int []A = { 1, 1, 2, 3, 3 };
    int N = A.Length;
    CalcUnique(A, N);
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the
// above approach

// Function call to find
// element in A[] with frequency = 1
function CalcUnique(A, N)
{
    // Stores frequency of
    // array elements
    var freq = new Map();

    // Traverse the array
    for (var i = 0; i < N; i++) {

        // Update frequency of A[i]
        if(freq.has(A[i]))
        {
            freq.set(A[i], freq.get(A[i])+1);
        }
        else
        {
            freq.set(A[i],1);
        }
    }

    // Traverse the Map
    for (var i = 0; i < N; i++) {

        // If non-repeating element
        // is found
        if (freq.get(A[i]) == 1) {

            document.write( A[i]);
            return;
        }
    }
}

// Driver Code
var A = [1, 1, 2, 3, 3 ];
var N = A.length;
CalcUnique(A, N);

</script>
```

**Output:** 

```
2
```

***时间复杂度** : O(N)*
***辅助空间** : O(N)*

#### **另一种方法:使用**内置的 **Python 函数:**

*   使用 [**计数器()**](https://www.geeksforgeeks.org/python-counter-objects-elements/) 功能计算频率。
*   遍历数组，找到频率为 1 的元素并打印出来。

下面是实现:

## 蟒蛇 3

```
# Python 3 implementation of the
# above approach
from collections import Counter

# Function call to find
# element in A[] with frequency = 1
def CalcUnique(A, N):

    # Calculate frequency of
    # all array elements
    freq = Counter(A)

    # Traverse the Array
    for i in A:

        # If non-repeating element
        # is found
        if (freq[i] == 1):
            print(i)
            return

# Driver Code
if __name__ == "__main__":
    A = [1, 1, 2, 3, 3]
    N = len(A)
    CalcUnique(A, N)

# This code is contributed by vikkycirus
```

**输出:**

```
2
```

**时间复杂度:** O(N)

**辅助空间:** O(N)