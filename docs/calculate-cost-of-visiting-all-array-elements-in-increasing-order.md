# 按递增顺序计算访问所有数组元素的成本

> 原文:[https://www . geeksforgeeks . org/compute-访问所有数组元素的成本-递增顺序/](https://www.geeksforgeeks.org/calculate-cost-of-visiting-all-array-elements-in-increasing-order/)

如果从索引 **i** 到索引 **j** 的移动成本是 **i** 和 **j** 之间的绝对差值，那么给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】】**，任务是从 **0** 开始，以升序查找访问所有数组元素的总成本。

**示例:**

> **输入:** arr[ ] = { 4，3，2，5，1 }
> **输出:** 11
> **解释:**
> 从索引 0 跳转到索引 4。成本= ABS(4–0)= 4。
> 从指数 4 跳到指数 2。成本= ABS(4–2)= 2。
> 从索引 2 跳转到索引 1。成本= ABS(2–1)= 1。
> 从指数 1 跳到指数 0。成本= ABS(1–0)= 1。
> 从指数 0 跳到指数 3。成本= ABS(0–3)= 3。
> 因此，按升序访问所有数组元素的总开销= (4 + 2 + 1 + 1 + 3 = 11)。
> 
> **输入:** arr[ ] = { 1，2，3 }
> T3】输出: 2

**方法:**思路是利用[的概念对向量对](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)进行排序。按照以下步骤解决问题:

*   初始化一对**向量<对< int，int > >** ，比如 **v，**来存储元素对及其各自的位置。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**并在向量 **v.** 中推[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/) **{arr[i]，i}**
*   初始化两个变量，比如 **ans = 0** 和 **last = 0，**来存储所需的总成本和上次访问元素的索引。
*   [按升序对向量对进行排序。](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-2-sort-in-descending-order-by-first-and-second/)
*   [遍历向量](https://www.geeksforgeeks.org/how-to-iterate-through-a-vector-without-using-iterators-in-c/) **v** 并将 **ans** 增加 **abs(v[i]。倒数第二)**。将**最后一个**更新为**最后一个= arr[i].秒.**
*   完成上述步骤后，将获得的答案打印为 **ans。**

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate total
// cost of visiting array
// elements in increasing order
int calculateDistance(int arr[], int N)
{
    // Stores the pair of element
    // and their positions
    vector<pair<int, int> > v;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++)

        // Push the pair {arr[i], i} in v
        v.push_back({ arr[i], i });

    // Sort the vector in ascending order.
    sort(v.begin(), v.end());

    // Stores the total cost
    int ans = 0;

    // Stores the index of last element visited
    int last = 0;

    // Traverse the vector v
    for (auto j : v) {

        // Increment ans
        ans += abs(j.second - last);

        // Assign
        last = j.second;
    }

    // Return ans
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 4, 3, 2, 5, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << calculateDistance(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {

  // Pair class
  static class Pair {

    int first;
    int second;

    Pair(int first, int second)
    {
      this.first = first;
      this.second = second;
    }
  }

  // Function to calculate total
  // cost of visiting array
  // elements in increasing order
  static int calculateDistance(int arr[], int N)
  {
    // Stores the pair of element
    // and their positions
    Pair v[] = new Pair[N];

    // Traverse the array arr[]
    for (int i = 0; i < N; i++)

      // Push the pair {arr[i], i} in v
      v[i] = new Pair(arr[i], i);

    // Sort the vector in ascending order.
    Arrays.sort(v, (p1, p2) -> {
      if (p1.first != p2.first)
        return p1.first - p2.first;
      return p1.second - p2.second;
    });

    // Stores the total cost
    int ans = 0;

    // Stores the index of last element visited
    int last = 0;

    // Traverse the vector v
    for (Pair j : v) {

      // Increment ans
      ans += Math.abs(j.second - last);

      // Assign
      last = j.second;
    }

    // Return ans
    return ans;
  }

  // Driver Code
  public static void main(String[] args)
  {
    int arr[] = { 4, 3, 2, 5, 1 };
    int N = arr.length;

    // Function call
    System.out.println(calculateDistance(arr, N));
  }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to calculate total
# cost of visiting array
# elements in increasing order
def calculateDistance(arr, N):

    # Stores the pair of element
    # and their positions
    v = []

    # Traverse the array arr[]
    for i in range(N):

        # Push the pair {arr[i], i} in v
        v.append([arr[i], i])

    # Sort the vector in ascending order.
    v.sort()

    # Stores the total cost
    ans = 0

    # Stores the index of last element visited
    last = 0

    # Traverse the vector v
    for j in v:

        # Increment ans
        ans += abs(j[1] - last)

        # Assign
        last = j[1]

    # Return ans
    return ans

# Driver Code
if __name__ == "__main__" :

    arr = [ 4, 3, 2, 5, 1 ]
    N = len(arr)

    print(calculateDistance(arr, N))

# This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

// Function to calculate total
// cost of visiting array
// elements in increasing order
function calculateDistance(arr, N)
{
    // Stores the pair of element
    // and their positions
    var v = [];

    // Traverse the array arr[]
    for (var i = 0; i < N; i++)
    {
        // Push the pair {arr[i], i} in v
        v.push([ arr[i], i ]);
    }

    // Sort the vector in ascending order.
    v = v.sort();

    // Stores the total cost
    var ans = 0;

    // Stores the index of last element visited
    var last = 0;

    // Traverse the vector v
    for (var i = 0; i < N; i++)
    {
        // Increment ans
        ans += Math.abs(v[i][1] - last);

        // Assign
        last = v[i][1];
    }

    // Return ans
    return ans;
}

// Driver Code
var arr = [ 4, 3, 2, 5, 1 ];
var N = arr.length;
document.write(calculateDistance(arr, N));

// This code is contributed by Shubhamsingh10
</script>
```

**Output:** 

```
11
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)