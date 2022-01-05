# 检查是否可以将数组拆分成大小至少为 K 的严格递增的子集

> 原文:[https://www . geeksforgeeks . org/check-如果可能，将数组拆分为严格递增的大小至少为-k 的子集/](https://www.geeksforgeeks.org/check-if-its-possible-to-split-the-array-into-strictly-increasing-subsets-of-size-at-least-k/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个整数 **K** ，任务是检查是否有可能将数组拆分为大小至少为 **K** 的[严格递增子集](https://www.geeksforgeeks.org/length-of-longest-strictly-increasing-subset-with-each-pair-of-adjacent-elements-satisfying-the-condition-2-ai-ai-1/)。如果可能，则打印“**是**”。否则，打印“**否**”。

**示例:**

> **输入:** arr[] = {5，6，4，9，12}，K = 2
> **输出:**是
> **解释:**
> 将数组拆分为至少大小为 2 的子集的一种可能方式是，{arr[2](=4)，arr[0](=5)和{arr[1](=6)，arr[3](=9)，arr[4](=12)}
> 
> **输入:** arr[] = {5，7，7，7}，K = 2
> T3】输出:否

**方法:**利用 Map 存储每个元素的频率，将数组划分为 X 个子集，其中 X 为数组中出现次数最大的元素的[频率](https://www.geeksforgeeks.org/frequent-element-array/)即可解决问题。按照以下步骤解决问题:

*   初始化一个[映射](https://www.geeksforgeeks.org/java-util-hashmap-in-java/)表示 **m** 来存储元素的频率，也初始化一个变量 **mx** 为 **0** 来存储数组中最大出现元素的[频率](https://www.geeksforgeeks.org/frequent-element-array/) **arr[]** 。
*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr[]** ，并将**m【arr[I]】**增加 **1** ，并将 **mx** 的值更新为 **max(mx，m【arr[I]】)**。
*   现在，如果 **N/mx > = K** 则打印“**是**，因为它是子集可以拥有的最大元素数量。
*   否则，打印**“否**”。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible
// to split the array into strictly
// increasing subsets of size atleast K
string ifPossible(int arr[], int N, int K)
{

    // Map to store frequency of elements
    map<int, int> m;

    // Stores the frequency of the maximum
    // occurring element in the array
    int mx = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {
        m[arr[i]] += 1;
        mx = max(mx, m[arr[i]]);
    }
    // Stores the minimum count of elements
    // in a subset
    int sz = N / mx;

    // If sz is greater than k-1
    if (sz >= K) {
        return "Yes";
    }
    // Otherwise
    else {

        return "No";
    }
}

// Driver Code
int main()
{
    // Given Input
    int arr[] = { 5, 6, 4, 9, 12 };
    int K = 2;
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << ifPossible(arr, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java approach for the above program
import java.util.HashMap;

public class GFG
{

    // Function to check if it is possible
    // to split the array into strictly
    // increasing subsets of size atleast K
    static String ifPossible(int arr[], int N, int K)
    {

        // Map to store frequency of elements
        HashMap<Integer, Integer> m
            = new HashMap<Integer, Integer>();

        // Stores the frequency of the maximum
        // occurring element in the array
        int mx = 0;

        // Traverse the array
        for (int i = 0; i < N; i++) {
            m.put(arr[i], m.getOrDefault(arr[i], 0) + 1);
            mx = Math.max(mx, m.get(arr[i]));
        }
        // Stores the minimum count of elements
        // in a subset
        int sz = N / mx;

        // If sz is greater than k-1
        if (sz >= K) {
            return "Yes";
        }
        // Otherwise
        else {

            return "No";
        }
    }
    // Driver code
    public static void main(String[] args)
    {
        // Given Input
        int arr[] = { 5, 6, 4, 9, 12 };
        int K = 2;
        int N = arr.length;

        // Function Call
        System.out.println(ifPossible(arr, N, K));
    }
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if it is possible
# to split the array into strictly
# increasing subsets of size atleast K
def ifPossible(arr, N, K):

    # Map to store frequency of elements
    m = {}

    # Stores the frequency of the maximum
    # occurring element in the array
    mx = 0

    # Traverse the array
    for i in range(N):
        if arr[i] in m:
            m[arr[i]] += 1
        else:
            m[arr[i]] = 1

        mx = max(mx, m[arr[i]])

    # Stores the minimum count of elements
    # in a subset
    sz = N // mx

    # If sz is greater than k-1
    if (sz >= K):
        return "Yes"

    # Otherwise
    else:
        return "No"

# Driver Code
if __name__ == '__main__':

    # Given Input
    arr = [ 5, 6, 4, 9, 12 ]
    K = 2
    N = len(arr)

    # Function Call
    print(ifPossible(arr, N, K))

# This code is contributed by bgangwar59
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to check if it is possible
// to split the array into strictly
// increasing subsets of size atleast K
static string ifPossible(int []arr, int N, int K)
{

    // Map to store frequency of elements
    Dictionary<int,int> m = new Dictionary<int,int>();

    // Stores the frequency of the maximum
    // occurring element in the array
    int mx = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {
        if(m.ContainsKey(arr[i]))
          m[arr[i]] += 1;
        else
          m.Add(arr[i],1);
        mx = Math.Max(mx, m[arr[i]]);
    }

    // Stores the minimum count of elements
    // in a subset
    int sz = N / mx;

    // If sz is greater than k-1
    if (sz >= K) {
        return "Yes";
    }

    // Otherwise
    else {

        return "No";
    }
}

// Driver Code
public static void Main()
{
    // Given Input
    int []arr = { 5, 6, 4, 9, 12 };
    int K = 2;
    int N = arr.Length;

    // Function Call
    Console.Write(ifPossible(arr, N, K));
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check if it is possible
// to split the array into strictly
// increasing subsets of size atleast K
function ifPossible(arr, N, K)
{

    // Map to store frequency of elements
    let m = new Map();

    // Stores the frequency of the maximum
    // occurring element in the array
    let mx = 0;

    // Traverse the array
    for (let i = 0; i < N; i++) {
        m[arr[i]] += 1;
        if(m.has(arr[i])){
            m.set(arr[i], m.get([arr[i]]) + 1)
        }else{
            m.set(arr[i], 1)
        }
        mx = Math.max(mx, m.get(arr[i]));
    }
    // Stores the minimum count of elements
    // in a subset
    let sz = Math.floor(N / mx);

    // If sz is greater than k-1
    if (sz >= K) {
        return "Yes";
    }
    // Otherwise
    else {

        return "No";
    }
}

// Driver Code

    // Given Input
    let arr = [ 5, 6, 4, 9, 12 ];
    let K = 2;
    let N = arr.length;

    // Function Call
    document.write(ifPossible(arr, N, K));

</script>
```

**Output**

```
Yes
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(N)*