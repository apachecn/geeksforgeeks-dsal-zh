# 每个子序列中出现的最小元素

> 原文:[https://www . geesforgeks . org/每个子序列中出现的最小元素/](https://www.geeksforgeeks.org/smallest-occurring-element-in-each-subsequence/)

给定一个由 **N** 个不同整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)。对于每个元素，任务是从最小元素是当前元素的所有可能的子序列中找到子序列的计数。
**例:**

> **输入:** arr[] = {1，2}
> **输出:** 2 1
> **解释:**
> 子序列为{1}、{2}、{1，2}。
> 每个子序列中最小元素的计数为:
> 1 = 2，2 = 1
> **输入:** arr[] = {1，2，3}
> **输出:** 4 2 1

**天真方法:**想法是[生成给定数组](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)的所有可能的子序列，并计算每个子序列中最小的元素，并为数组中的每个元素打印其计数。
***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(N)*

**高效方法:**思路是观察一个模式，即这样观察，最小元素出现 2<sup>n–1</sup>次，第二个最小元素出现 2<sup>n–2</sup>次，以此类推……**。例如:**

> 让数组为 arr[] = {1，2，3}
> 子序列为{1}、{2}、{3}、{1，2}、{1，3}、{2，3}、{1，2，3}
> 每个子序列的最小值为:{1}、{2}、{3}、{1}、{1}、{2}、{1}。
> 其中
> 1 出现 4 次，即 2<sup>n–1</sup>其中 n = 3。
> 2 发生 2 次，即 2<sup>n–2</sup>，其中 n = 3。
> 3 发生 1 次，即 2<sup>n–3</sup>，其中 n = 3。

以下是步骤:

1.  将每个元素的索引存储在[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中，这样我们就可以按照原始数组的顺序打印该元素。
2.  [给定数组排序](https://www.geeksforgeeks.org/sorting-algorithms/)。
3.  现在元素按递增顺序排列，从上面的观察[遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并保持子序列的计数，使得每个元素都是最小的元素，由**幂(2，N–1–I)**给出。
4.  现在遍历地图，并根据原始数组中的元素打印子序列的计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that count the subsequence
// such that each element as the
// minimum element in the subsequence
void solve(int arr[], int N)
{
    map<int, int> M;

    // Store index in a map
    for (int i = 0; i < N; i++) {
        M[i] = arr[i];
    }

    // Sort the array
    sort(arr, arr + N);

    // To store count of subsequence
    unordered_map<int, int> Count;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Store count of subsequence
        Count[arr[i]] = pow(2, N - i - 1);
    }

    // Print the count of subsequence
    for (auto& it : M) {
        cout << Count[M[it.second]] << ' ';
    }
}

// Driver code
int main()
{
    int arr[] = { 5, 2, 1 };
    int N = sizeof arr / sizeof arr[0];

    // Function call
    solve(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function that count the subsequence
// such that each element as the
// minimum element in the subsequence
static void solve(int arr[], int N)
{
    HashMap<Integer,
              Integer> M = new HashMap<>();

    // Store index in a map
    for (int i = 0; i < N; i++)
    {
        M.put(i, arr[i]);
    }

    // Sort the array
    Arrays.sort(arr);

    // To store count of subsequence
    HashMap<Integer,
              Integer> Count = new HashMap<>();

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

        // Store count of subsequence
        Count.put(arr[i],
                 (int)Math.pow(2, N - i - 1));
    }

    // Print the count of subsequence
    for (Map.Entry<Integer,
                    Integer> m : M.entrySet())
    {
        System.out.print(Count.get(m.getValue()) + " ");
    }
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 5, 2, 1 };
    int N = arr.length;

    // Function call
    solve(arr, N);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that count the subsequence
# such that each element as the
# minimum element in the subsequence
def solve(arr, N):

    M = {}

    # Store index in a map
    for i in range(N):
        M[i] = arr[i]

    # Sort the array
    arr.sort()

    # To store count of subsequence
    Count = {}

    # Traverse the array
    for i in range(N):

        # Store count of subsequence
        Count[arr[i]] = pow(2, N - i - 1)

    # Print the count of subsequence
    for it in Count.values():
        print(it, end = " ")

# Driver code
if __name__ == "__main__":

    arr = [ 5, 2, 1 ]
    N = len(arr)

    # Function call
    solve(arr, N)

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function that count the subsequence
// such that each element as the
// minimum element in the subsequence
static void solve(int []arr, int N)
{
    Dictionary<int,
               int> M = new Dictionary<int,
                                         int>();

    // Store index in a map
    for (int i = 0; i < N; i++)
    {
        M.Add(i, arr[i]);
    }

    // Sort the array
    Array.Sort(arr);

    // To store count of subsequence
    Dictionary<int,
               int> Count = new Dictionary<int,
                                             int>();

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

        // Store count of subsequence
        Count.Add(arr[i],
                 (int)Math.Pow(2, N - i - 1));
    }
  // Print the count of subsequence
   foreach(KeyValuePair<int, int> m in M)
{
    Console.Write(Count[m.Value]);  
} 
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 5, 2, 1 };
    int N = arr.Length;

    // Function call
    solve(arr, N);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function that count the subsequence
// such that each element as the
// minimum element in the subsequence
function solve(arr, N)
{
    var M = new Map();

    // Store index in a map
    for (var i = 0; i < N; i++) {
        M.set(i, arr[i]);
    }

    // Sort the array
    arr.sort((a,b)=>a-b);

    // To store count of subsequence
    var Count = new Map();

    // Traverse the array
    for (var i = 0; i < N; i++) {

        // Store count of subsequence
        Count.set(arr[i], parseInt(Math.pow(2, N - i - 1)));
    }

    // Print the count of subsequence
    M.forEach((value, key) => {
        document.write(Count.get(value) + ' ');
    });

}

// Driver code
var arr = [5, 2, 1];
var N = arr.length;
// Function call
solve(arr, N);

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
4 2 1
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*