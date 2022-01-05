# 将数组分割成最小数量的子集，使得所有对的元素在不同的子集中至少出现一次

> 原文:[https://www . geeksforgeeks . org/将数组拆分为最小数量的子集，以便所有对中的元素在不同的子集中至少出现一次/](https://www.geeksforgeeks.org/split-array-into-minimum-number-of-subsets-such-that-elements-of-all-pairs-are-present-in-different-subsets-at-least-once/)

给定一个由 **N** 个不同整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是找出需要将数组拆分为两个子集的最小次数，以便每对元素至少出现一次。

**示例:**

> **输入:** arr[] = { 3，4，2，1，5 }
> **输出:** 3
> **解释:**
> 可能的对是{ (1，2)，(1，3)，(1，4)，(1，5)，(2，3)，(2，4)，(2，5)，(3，4)，(3，5)，(4，5) }
> 将数组拆分为{ 1，2 }和{ 3，4，5 }
> 每对的元素{ }
> 将数组拆分为{ 1，3 }和{ 2，4，5 }
> 每对{ **(1，2)** 、(1，4)、(1，5)、(2，3)、 **(3，4)、(3，5)** }的元素存在于两个不同的子集。
> 将数组拆分为{ 1，3，4 }和{ 2，5 }
> 每对的元素{ (1，2)，(1，5)，(2，3)，(3，5)，(2，4)， **(4，5)** }存在于两个不同的子集。
> 由于每对数组的元素至少在两个不同的子集中出现一次，因此所需的输出为 3。
> 
> **输入:** arr[] = { 2，1，3 }
> T3】输出: 2

**方法:**想法是始终将数组拆分为两个大小的子集[楼层(N / 2)](https://www.geeksforgeeks.org/ceil-floor-functions-cpp/) 和[天花板(N / 2)](https://www.geeksforgeeks.org/ceil-floor-functions-cpp/) 。在每个分区之前，只需将 **arr[i]** 的值与 **arr[N / 2 + i]** 交换即可。按照下面给出的步骤解决问题:

*   [如果 N 为奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，则总的可能[交换(arr[i]，arr[N / 2 + i])](https://www.geeksforgeeks.org/c-program-swap-two-numbers/) 等于 **N / 2 + 1** 。因此，打印 **(N / 2 + 1)** 。
*   [如果 N 是偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，那么总的可能[互换(arr[i]，arr[N / 2 + i])](https://www.geeksforgeeks.org/c-program-swap-two-numbers/) 等于 **N / 2** 。因此，打印 **(N / 2)** 。

下面是上述方法的 C++实现:

## C++

```
// C++ program to to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum count of ways to split
// the array into two subset such that elements of
// each pair occurs in two different subset
int MinimumNoOfWays(int arr[], int n)
{

    // Stores minimum count of ways to split array
    // into two subset such that elements of
    // each pair occurs in two different subset
    int mini_no_of_ways;

    // If N is odd
    if (n % 2 == 0) {
        mini_no_of_ways = n / 2;
    }
    else {
        mini_no_of_ways = n / 2 + 1;
    }
    return mini_no_of_ways;
}

// Driver Code
int main()
{
    int arr[] = { 3, 4, 2, 1, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << MinimumNoOfWays(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find minimum count of ways to split
// the array into two subset such that elements of
// each pair occurs in two different subset
static int MinimumNoOfWays(int arr[], int n)
{

    // Stores minimum count of ways to split array
    // into two subset such that elements of
    // each pair occurs in two different subset
    int mini_no_of_ways;

    // If N is odd
    if (n % 2 == 0) {
        mini_no_of_ways = n / 2;
    }
    else {
        mini_no_of_ways = n / 2 + 1;
    }
    return mini_no_of_ways;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 3, 4, 2, 1, 5 };
    int N = arr.length;
    System.out.print(MinimumNoOfWays(arr, N));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python program to to implement
# the above approach

# Function to find minimum count of ways to split
# the array into two subset such that elements of
# each pair occurs in two different subset
def MinimumNoOfWays(arr, n):

    # Stores minimum count of ways to split array
    # into two subset such that elements of
    # each pair occurs in two different subset
    min_no_of_ways = 0

    # if n is even
    if (n % 2 == 0):
        mini_no_of_ways = n // 2

    # n is odd
    else:
        mini_no_of_ways = n // 2 + 1

    return mini_no_of_ways

# driver code
if __name__ == '__main__':
    arr = [3, 4, 1, 2, 5]
    n = len(arr)
    print(MinimumNoOfWays(arr, n))

# This code is contributed by MuskanKalra1
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

// Function to find minimum count of ways to split
// the array into two subset such that elements of
// each pair occurs in two different subset
static int MinimumNoOfWays(int []arr, int n)
{

    // Stores minimum count of ways to split array
    // into two subset such that elements of
    // each pair occurs in two different subset
    int mini_no_of_ways;

    // If N is odd
    if (n % 2 == 0)
    {
        mini_no_of_ways = n / 2;
    }
    else
    {
        mini_no_of_ways = n / 2 + 1;
    }
    return mini_no_of_ways;
}

  // Driver code
  public static void Main(string[] args)
  {
      int[] arr = { 3, 4, 2, 1, 5 };
      int N = arr.Length;
      Console.WriteLine(MinimumNoOfWays(arr, N));
  }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// javascript program to implement
// the above approach

    // Function to find minimum count of ways to split
    // the array into two subset such that elements of
    // each pair occurs in two different subset
    function MinimumNoOfWays(arr , n) {

        // Stores minimum count of ways to split array
        // into two subset such that elements of
        // each pair occurs in two different subset
        var mini_no_of_ways;

        // If N is odd
        if (n % 2 == 0) {
            mini_no_of_ways = n / 2;
        } else {
            mini_no_of_ways = n / 2 + 1;
        }
        return parseInt(mini_no_of_ways);
    }

    // Driver code

        var arr = [ 3, 4, 2, 1, 5 ];
        var N = arr.length;
        document.write(MinimumNoOfWays(arr, N));

// This code contributed by gauravrajput1
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(1)*
***空间复杂度:** O(1)*