# 用给定的 LCM 构建唯一元素的最长可能序列

> 原文:[https://www . geeksforgeeks . org/construct-具有给定 lcm 的最长可能唯一元素序列/](https://www.geeksforgeeks.org/construct-longest-possible-sequence-of-unique-elements-with-given-lcm/)

给定一个正整数 **N** ，任务是构造唯一元素的最长排序序列，其的 [LCM](https://www.geeksforgeeks.org/lcm-of-given-array-elements/) 等于 **N** 。

**示例:**

> **输入:** N = 12
> **输出:** 1 2 3 4 6 12
> **说明:**
> 的{1，2，3，4，6，12 }的 LCM 为 N( = 12)。
> 因此，最长的可能序列是{1，2，3，4，6，12 }。
> 
> **输入:** N = 9
> **输出:** 1 3 9
> **说明:**
> 的{ 1，2，9 } LCM 为 N( = 9)。
> 因此，最长的可能序列是{1，3，9 }。

**方法:**根据以下观察可以解决问题:

> 如果一个数组元素不是 N 的因子，那么数组元素的 LCM 永远不是 N。因此，数组元素必须是 N 的因子

请按照以下步骤解决此问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如说**new RR[]**，来存储所有唯一的数组元素，这些元素的 LCM 等于 **N** 。
*   [找到 N](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/) 的所有因子，储存在**纽瓦尔[]** 中。
*   [排序数组](https://www.geeksforgeeks.org/sort-c-stl/) **纽瓦尔[]** 。
*   [打印所有**新**的数组元素](https://www.geeksforgeeks.org/print-distinct-elements-given-integer-array/)。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to construct an array of
// unique elements whose LCM is N
void constructArrayWithGivenLCM(int N)
{
    // Stores array elements
    // whose LCM is N
    vector<int> newArr;

    // Iterate over the range
    // [1, sqrt(N)]
    for (int i = 1; i * i <= N;
         i++) {

        // If N is divisible
        // by i
        if (N % i == 0) {

            // Insert i into newArr[]
            newArr.push_back(i);

            // If N is not perfect square
            if (N / i != i) {
                newArr.push_back(N / i);
            }
        }
    }

    // Sort the array newArr[]
    sort(newArr.begin(), newArr.end());

    // Print array elements
    for (auto i : newArr) {

        cout << i << " ";
    }
}

// Driver Code
int main()
{
    // Given N
    int N = 12;

    // Function Call
    constructArrayWithGivenLCM(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.Arrays;

class GFG{

// Function to construct an array of
// unique elements whose LCM is N
static void constructArrayWithGivenLCM(int N)
{

    // Stores array elements
    // whose LCM is N
    int newArr[] = new int[N];

    int j = 0;

    // Iterate over the range
    // [1, sqrt(N)]
    for(int i = 1; i * i <= N; i++)
    {

        // If N is divisible
        // by i
        if (N % i == 0)
        {

            // Insert i into newArr[]
            newArr[j] = i;
            j++;

            // If N is not perfect square
            if (N / i != i)
            {
                newArr[j] = N / i;
                j++;
            }
        }
    }

    // Sort the array newArr[]
    Arrays.sort(newArr);

    // Print array elements
    for(int i = j; i < N; i++) 
    {
        System.out.print(newArr[i] + " ");
    }
}

// Driver Code
public static void main (String[] args)
{

    // Given N
    int N = 12;

    // Function Call
    constructArrayWithGivenLCM(N);
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
from math import sqrt,ceil,floor

# Function to construct an array of
# unique elements whose LCM is N
def constructArrayWithGivenLCM(N):

    # Stores array elements
    # whose LCM is N
    newArr = []

    # Iterate over the range
    # [1, sqrt(N)]
    for i in range(1, ceil(sqrt(N + 1))):

        # If N is divisible
        # by i
        if (N % i == 0):

            # Insert i into newArr[]
            newArr.append(i)

            # If N is not perfect square
            if (N // i != i):
                newArr.append(N // i)

    # Sort the array newArr[]
    newArr = sorted(newArr)

    # Print array elements
    for i in newArr:
        print(i, end = " ")

# Driver Code
if __name__ == '__main__':

  # Given N
    N = 12

    # Function Call
    constructArrayWithGivenLCM(N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

  // Function to construct an array of
  // unique elements whose LCM is N
  static void constructArrayWithGivenLCM(int N)
  {

    // Stores array elements
    // whose LCM is N
    int []newArr = new int[N];

    int j = 0;

    // Iterate over the range
    // [1, sqrt(N)]
    for(int i = 1; i * i <= N; i++)
    {

      // If N is divisible
      // by i
      if (N % i == 0)
      {

        // Insert i into newArr[]
        newArr[j] = i;
        j++;

        // If N is not perfect square
        if (N / i != i)
        {
          newArr[j] = N / i;
          j++;
        }
      }
    }

    // Sort the array newArr[]
    Array.Sort(newArr);

    // Print array elements
    for(int i = j; i < N; i++) 
    {
      Console.Write(newArr[i] + " ");
    }
  }

  // Driver Code
  public static void Main(String[] args)
  {

    // Given N
    int N = 12;

    // Function Call
    constructArrayWithGivenLCM(N);
  }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

    // JavaScript program to implement the above approach

    // Function to construct an array of
    // unique elements whose LCM is N
    function constructArrayWithGivenLCM(N)
    {

      // Stores array elements
      // whose LCM is N
      let newArr = new Array(N);
      newArr.fill(0);

      let j = 0;

      // Iterate over the range
      // [1, sqrt(N)]
      for(let i = 1; i * i <= N; i++)
      {

        // If N is divisible
        // by i
        if (N % i == 0)
        {

          // Insert i into newArr[]
          newArr[j] = i;
          j++;

          // If N is not perfect square
          if (parseInt(N / i, 10) != i)
          {
            newArr[j] = parseInt(N / i, 10);
            j++;
          }
        }
      }

      // Sort the array newArr[]
      newArr.sort(function(a, b){return a - b});

      // Print array elements
      for(let i = j; i < N; i++)
      {
        document.write(newArr[i] + " ");
      }
    }

    // Given N
    let N = 12;

    // Function Call
    constructArrayWithGivenLCM(N);

</script>
```

**Output:** 

```
1 2 3 4 6 12
```

***时间复杂度:** O(√ N)*
***辅助空间:** O(1)*