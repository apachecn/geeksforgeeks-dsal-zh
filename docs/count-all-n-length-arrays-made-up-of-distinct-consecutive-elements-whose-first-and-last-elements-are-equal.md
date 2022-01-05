# 计算所有由不同的连续元素组成的 N 长度数组，这些元素的第一个和最后一个元素相等

> 原文:[https://www . geeksforgeeks . org/count-all-n-length-arrays-由不同的连续元素组成-其第一个和最后一个元素相等/](https://www.geeksforgeeks.org/count-all-n-length-arrays-made-up-of-distinct-consecutive-elements-whose-first-and-last-elements-are-equal/)

给定两个整数 **M** 和 **N** ，任务是找出**N**-长度[数组](https://www.geeksforgeeks.org/array-data-structure/)的数量，这些数组可能具有位于范围**【1，M】**中的不相等的相邻元素，这些元素的第一个和最后一个索引相等。

**例:**

> ***输入:** N = 3，M = 3*
> ***输出:** 6*
> ***解释:***
> *可能的数组有{1，2，1}、{1，3，1}、{2，1，2}、{2，3，2}、{3，1，3}、{3，2，3}。*
> 
> ***输入:** N = 5，M = 4*
> T5**输出:** 84

**方法:**按照以下步骤解决问题:

*   首先将 **arr[0]** 和 **arr[N-1]** 设为 1。
*   现在找到大小为 **i** 的可能数组的数量，以 **1** 结束(即 *arr[i] = 1* )。将该结果存储到**end _ wit _ one[I]**中。
*   现在，找到大小为 **i** 的可能数组的数量，该数量不以**1**(*arr【I】≠1*)结束。将该结果存储到 **end_not_with_one[i]** 中。
*   因为，用 **arr[i] = 1** 构成数组直到第 **i <sup>个</sup>T3】索引的方式数，与用**arr[I–1]≠1**构成数组直到第**(I–1)<sup>个</sup>**索引的方式数相同，设置**end _ wit _ one[I]= end _ not _ wit _ one[I–1]**。**
*   现在，用**arr【I】≠1**组成阵列直到第 **i <sup>第</sup>T3】索引的方法如下:**
    *   **如果 arr[I–1]= 1，**有**(M–1)**号要放在 **i <sup>第</sup>** 号索引处。
    *   **如果 arr[I–1]≠1，**那么**(M–2)**号可以放在索引 **i** 处，因为 **arr[i]** 不能为 1， **arr[i]** 不能等于**arr[I–1]**。
    *   因此，设置**end _ not _ with _ one[I]= end _ with _ one[I-1]*(M–1)+end _ not _ with _ one[I-1]*(M–2)**。
*   因此，用**arr【0】**和**arr【N–1】**等于 **1** 形成大小为 **N** 的数组的方式数为**end _ wit _ one【N–1】**。
*   类似地， **arr[0]** 和**arr[N–1]**可以设置为从 **1** 到 **M** 的任意元素。
*   因此，可能的数组总数是 **M * end_with_one[N-1]** 。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print the count of
// arrays satisfying given condition
int totalArrays(int N, int M)
{

    int end_with_one[N + 1];
    int end_not_with_one[N + 1];

    // First element of
    // array is set as 1
    end_with_one[0] = 1;
    end_not_with_one[0] = 0;

    // Since the first element
    // of arr[] is 1, the
    // second element can't be 1
    end_with_one[1] = 0;
    end_not_with_one[1] = M - 1;

    // Traverse the remaining indices
    for (int i = 2; i < N; i++) {

        // If arr[i] = 1
        end_with_one[i]
            = end_not_with_one[i - 1];

        // If arr[i] ≠ 1
        end_not_with_one[i]
            = end_with_one[i - 1] * (M - 1)
              + end_not_with_one[i - 1] * (M - 2);
    }

    // Since last element needs to be 1
    return end_with_one[N - 1];
}

// Driver Code
int main()
{

    int N = 3, M = 3;

    // Stores the count of arrays
    // where arr[0] = arr[N - 1] = 1
    int temp = totalArrays(N, M);

    // Since arr[0] and arr[N - 1]
    // can be any number from 1 to M
    int ans = M * temp;

    // Print answer
    cout << ans << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to print the count of
// arrays satisfying given condition
static int totalArrays(int N, int M)
{
    int []end_with_one = new int[N + 1];
    int []end_not_with_one = new int[N + 1];

    // First element of
    // array is set as 1
    end_with_one[0] = 1;
    end_not_with_one[0] = 0;

    // Since the first element
    // of arr[] is 1, the
    // second element can't be 1
    end_with_one[1] = 0;
    end_not_with_one[1] = M - 1;

    // Traverse the remaining indices
    for (int i = 2; i < N; i++)
    {

        // If arr[i] = 1
        end_with_one[i]
            = end_not_with_one[i - 1];

        // If arr[i] ≠ 1
        end_not_with_one[i]
            = end_with_one[i - 1] * (M - 1)
              + end_not_with_one[i - 1] * (M - 2);
    }

    // Since last element needs to be 1
    return end_with_one[N - 1];
}

// Driver Code
public static void main(String[] args)
{
    int N = 3, M = 3;

    // Stores the count of arrays
    // where arr[0] = arr[N - 1] = 1
    int temp = totalArrays(N, M);

    // Since arr[0] and arr[N - 1]
    // can be any number from 1 to M
    int ans = M * temp;

    // Print answer
    System.out.print(ans+ "\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to print the count of
# arrays satisfying given condition
def totalArrays(N, M):
    end_with_one = [0] * (N + 1);
    end_not_with_one = [0] * (N + 1);

    # First element of
    # array is set as 1
    end_with_one[0] = 1;
    end_not_with_one[0] = 0;

    # Since the first element
    # of arr is 1, the
    # second element can't be 1
    end_with_one[1] = 0;
    end_not_with_one[1] = M - 1;

    # Traverse the remaining indices
    for i in range(2, N):

        # If arr[i] = 1
        end_with_one[i] = end_not_with_one[i - 1];

        # If arr[i] ≠ 1
        end_not_with_one[i] = end_with_one[i - 1] * (M - 1) + end_not_with_one[i - 1] * (M - 2);

    # Since last element needs to be 1
    return end_with_one[N - 1];

# Driver Code
if __name__ == '__main__':
    N = 3;
    M = 3;

    # Stores the count of arrays
    # where arr[0] = arr[N - 1] = 1
    temp = totalArrays(N, M);

    # Since arr[0] and arr[N - 1]
    # can be any number from 1 to M
    ans = M * temp;

    # Print answer
    print(ans);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to print the count of
    // arrays satisfying given condition
    static int totalArrays(int N, int M)
    {

        int[] end_with_one = new int[N + 1];
        int[] end_not_with_one = new int[N + 1];

        // First element of
        // array is set as 1
        end_with_one[0] = 1;
        end_not_with_one[0] = 0;

        // Since the first element
        // of arr[] is 1, the
        // second element can't be 1
        end_with_one[1] = 0;
        end_not_with_one[1] = M - 1;

        // Traverse the remaining indices
        for (int i = 2; i < N; i++) {

            // If arr[i] = 1
            end_with_one[i]
                = end_not_with_one[i - 1];

            // If arr[i] ≠ 1
            end_not_with_one[i]
                = end_with_one[i - 1] * (M - 1)
                  + end_not_with_one[i - 1] * (M - 2);
        }

        // Since last element needs to be 1
        return end_with_one[N - 1];
    } 

  // Driver code
  static void Main()
  {

    int N = 3, M = 3;

    // Stores the count of arrays
    // where arr[0] = arr[N - 1] = 1
    int temp = totalArrays(N, M);

    // Since arr[0] and arr[N - 1]
    // can be any number from 1 to M
    int ans = M * temp;

    // Print answer
    Console.WriteLine(ans);
  }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to print the count of
// arrays satisfying given condition
function totalArrays(N, M)
{

    var end_with_one = Array(N+1);
    var end_not_with_one = Array(N+1);

    // First element of
    // array is set as 1
    end_with_one[0] = 1;
    end_not_with_one[0] = 0;

    // Since the first element
    // of arr[] is 1, the
    // second element can't be 1
    end_with_one[1] = 0;
    end_not_with_one[1] = M - 1;

    // Traverse the remaining indices
    for (var i = 2; i < N; i++) {

        // If arr[i] = 1
        end_with_one[i]
            = end_not_with_one[i - 1];

        // If arr[i] ≠ 1
        end_not_with_one[i]
            = end_with_one[i - 1] * (M - 1)
            + end_not_with_one[i - 1] * (M - 2);
    }

    // Since last element needs to be 1
    return end_with_one[N - 1];
}

// Driver Code

var N = 3, M = 3;

// Stores the count of arrays
// where arr[0] = arr[N - 1] = 1
var temp = totalArrays(N, M);

// Since arr[0] and arr[N - 1]
// can be any number from 1 to M
var ans = M * temp;

// Print answer
document.write( ans + "<br>");

</script>
```

**Output:** 

```
6
```

***时间复杂度:*** O(N)
***辅助空间:*** O(N)