# 将阵列分成 K 个子阵列，使得所有子阵列的最大值之和最大

> 原文:[https://www . geesforgeks . org/split-array-in-k-subarray-这样所有子阵列的最大值之和被最大化/](https://www.geeksforgeeks.org/split-array-into-k-subarrays-such-that-sum-of-maximum-of-all-subarrays-is-maximized/)

给定一个大小为 **N** 的[阵列](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个数量为 **K** 的阵列，任务是将给定的阵列划分为 **K** [个相邻子阵列](https://www.geeksforgeeks.org/tag/subarray/)，使得每个子阵列的最大值之和为最大可能值。如果有可能以这种方式拆分数组，则打印最大可能的总和。否则，打印“ **-1** ”。

**示例:**

> **输入:** arr[] = {5，3，2，7，6，4}，N = 6，K = 3
> **输出:** 18
> 5
> 3 2 7
> 6 4
> **解释:**
> 一种方法是在索引 0，3 和 4 处拆分数组。
> 因此，形成的子阵列为{5}、{3，2，7}和{6，4}。
> 因此，每个子阵列的最大值之和= 5 + 7 + 6 =18(这是最大可能值)。
> 
> **输入:** arr[] = {1，4，5，6，1，2}，N = 6，K = 2
> **输出:** 11

**方法:**给定的问题可以使用[地图数据结构](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)和[排序技术](https://www.geeksforgeeks.org/sorting-algorithms/)来解决，基于以下观察:

> *   The maximum sum that can be obtained will be the sum of **k maximum** elements of the array, because it is always possible to divide the array into **k** segments, so that the maximum value of each segment is one of **k maximum** elements.
> *   One method is to break a line segment once one of the elements with the largest **k is encountered.**

按照以下步骤解决问题:

*   首先如果 **N** 小于 **K** 则打印“ **-1** ”然后返回。
*   [将数组复制到另一个数组中](https://www.geeksforgeeks.org/array-copy-in-java/)说**temp【】**和[按降序排列数组 temp【】](https://www.geeksforgeeks.org/sort-c-stl/)。
*   将变量**和**初始化为 **0** ，以存储最大可能总和。
*   另外，初始化一个[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)比如 **mp** ，来存储**K-最大**元素的频率。
*   使用变量 **i、**在范围**【0，K-1】**中迭代，并且在每次迭代中将 **ans** 增加**temp【I】**，并且增加地图 **mp 中**temp【I】**的计数。**
*   初始化向量的[向量](https://www.geeksforgeeks.org/vector-of-vectors-in-c-stl-with-examples/)表示 **P** 来存储可能的分区，初始化向量的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)表示 **V** 来存储分区的元素。
*   [在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**内迭代，使用变量表示 **i** ，执行以下步骤:
    *   在矢量 **V** 中推动当前元素**arr【I】**。
    *   如果 **mp[arr[i]]** 大于 **0** ，则执行以下操作:
        *   将地图 **mp** 中**arr【I】**的 **K** 和计数减 **1** 。
        *   如果 **K** 等于 **0** ，即它是最后一个片段，则在 **V.** 中推送数组的所有剩余元素**arr【】**
        *   现在按下 **P** 中的当前段 **V** 。
*   最后，完成上述步骤后，打印变量**和**中存储的最大和，然后分区存储在 **P** 中。

下面是上述方法的实现:

## C++

```
// C++ program for tha above approach
#include <bits/stdc++.h>
using namespace std;

// Function to split the array into K
// subarrays such that the sum of
// maximum of each subarray is maximized
void partitionIntoKSegments(int arr[],
                            int N, int K)
{
    // If N is less than K
    if (N < K) {
        cout << -1 << endl;
        return;
    }
    // Map to store the K
    // largest elements
    map<int, int> mp;

    // Auxiliary array to
    // store and sort arr[]
    int temp[N];

    // Stores the maximum sum
    int ans = 0;

    // Copy arr[] to temp[]
    for (int i = 0; i < N; i++) {
        temp[i] = arr[i];
    }

    // Sort array temp[] in
    // descending order
    sort(temp, temp + N,
         greater<int>());

    // Iterate in the range [0, K - 1]
    for (int i = 0; i < K; i++) {

        // Increment sum by temp[i]
        ans += temp[i];

        // Increment count of
        // temp[i] in the map mp
        mp[temp[i]]++;
    }

    // Stores the partitions
    vector<vector<int> > P;

    // Stores temporary subarrays
    vector<int> V;

    // Iterate over the range [0, N - 1]
    for (int i = 0; i < N; i++) {
        V.push_back(arr[i]);

        // If current element is
        // one of the K largest
        if (mp[arr[i]] > 0) {

            mp[arr[i]]--;
            K--;

            if (K == 0) {
                i++;
                while (i < N) {
                    V.push_back(arr[i]);
                    i++;
                }
            }

            if (V.size()) {
                P.push_back(V);
                V.clear();
            }
        }
    }

    // Print the ans
    cout << ans << endl;

    // Print the partition
    for (auto u : P) {
        for (auto x : u)
            cout << x << " ";
        cout << endl;
    }
}
// Driver code
int main()
{
    // Input
    int A[] = { 5, 3, 2, 7, 6, 4 };
    int N = sizeof(A) / sizeof(A[0]);
    int K = 3;

    // Function call
    partitionIntoKSegments(A, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG
{

// Function to split the array into K
// subarrays such that the sum of
// maximum of each subarray is maximized
static void partitionIntoKSegments(int arr[], int N, int K)
{

    // If N is less than K
    if (N < K)
    {
         System.out.println(-1);
        return;
    }

    // Map to store the K
    // largest elements
    HashMap<Integer,Integer> mp = new HashMap<Integer,Integer>();

    // Auxiliary array to
    // store and sort arr[]
    Integer []temp = new Integer[N];

    // Stores the maximum sum
    int ans = 0;

    // Copy arr[] to temp[]
    for(int i = 0; i < N; i++)
    {
        temp[i] = arr[i];
    }

    // Sort array temp[] in
    // descending order
    Arrays.sort(temp,Collections.reverseOrder());
    //Array.Reverse(temp);

    // Iterate in the range [0, K - 1]
    for(int i = 0; i < K; i++)
    {

        // Increment sum by temp[i]
        ans += temp[i];

        // Increment count of
        // temp[i] in the map mp
        if (mp.containsKey(temp[i]))
            mp.get(temp[i]++);
        else
            mp.put(temp[i], 1);
    }

    // Stores the partitions
    ArrayList<ArrayList<Integer>> P = new ArrayList<ArrayList<Integer>>();

    // Stores temporary subarrays
    ArrayList<Integer> V = new ArrayList<Integer>();

    // Iterate over the range [0, N - 1]
    for(int i = 0; i < N; i++)
    {
        V.add(arr[i]);

        // If current element is
        // one of the K largest
        if (mp.containsKey(arr[i]) && mp.get(arr[i]) > 0)
        {
            mp.get(arr[i]--);
            K--;

            if (K == 0)
            {
                i++;

                while (i < N)
                {
                    V.add(arr[i]);
                    i++;
                }
            }

            if (V.size() > 0)
            {
                P.add(new ArrayList<Integer>(V));
                V.clear();
            }
        }
    }

    // Print the ans
     System.out.println(ans);

    // Print the partition
    for (ArrayList<Integer > subList : P)
    {
        for(Integer  item : subList)
        {
              System.out.print(item+" ");
        }
         System.out.println();
    }
}

// Driver code
public static void main(String args[])
{

    // Input
    int []A = { 5, 3, 2, 7, 6, 4 };
    int N = A.length;
    int K = 3;

    // Function call
    partitionIntoKSegments(A, N, K);
}
}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python program for tha above approach

# Function to split the array into K
# subarrays such that the sum of
# maximum of each subarray is maximized
def partitionIntoKSegments(arr, N, K):
    # If N is less than K
    if (N < K):
        print(-1)
        return
    # Map to store the K
    # largest elements
    mp = {}

    # Auxiliary array to
    # store and sort arr[]
    temp = [0]*N

    # Stores the maximum sum
    ans = 0

    # Copy arr[] to temp[]
    for i in range(N):
        temp[i] = arr[i]

    # Sort array temp[] in
    # descending order
    temp = sorted(temp)[::-1]

    # Iterate in the range [0, K - 1]
    for i in range(K):
        # Increment sum by temp[i]
        ans += temp[i]

        # Increment count of
        # temp[i] in the map mp
        mp[temp[i]] = mp.get(temp[i], 0) + 1

    # Stores the partitions
    P = []

    # Stores temporary subarrays
    V = []

    # Iterate over the range [0, N - 1]
    for i in range(N):
        V.append(arr[i])

        # If current element is
        # one of the K largest
        if (arr[i] in mp):

            mp[arr[i]] -= 1
            K -= 1

            if (K == 0):
                i += 1
                while (i < N):
                    V.append(arr[i])
                    i += 1
            # print(V)

            if (len(V) > 0):
                P.append(list(V))
                V.clear()

    # Print ans
    print(ans)

    # Print partition
    for u in P:
        for x in u:
            print(x,end=" ")
        print()
# Driver code
if __name__ == '__main__':
    # Input
    A = [5, 3, 2, 7, 6, 4]
    N = len(A)
    K = 3

    # Function call
    partitionIntoKSegments(A, N, K)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for tha above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to split the array into K
// subarrays such that the sum of
// maximum of each subarray is maximized
static void partitionIntoKSegments(int []arr,
                                   int N, int K)
{

    // If N is less than K
    if (N < K)
    {
        Console.WriteLine(-1);
        return;
    }

    // Map to store the K
    // largest elements
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();

    // Auxiliary array to
    // store and sort arr[]
    int []temp = new int[N];

    // Stores the maximum sum
    int ans = 0;

    // Copy arr[] to temp[]
    for(int i = 0; i < N; i++)
    {
        temp[i] = arr[i];
    }

    // Sort array temp[] in
    // descending order
    Array.Sort(temp);
    Array.Reverse(temp);

    // Iterate in the range [0, K - 1]
    for(int i = 0; i < K; i++)
    {

        // Increment sum by temp[i]
        ans += temp[i];

        // Increment count of
        // temp[i] in the map mp
        if (mp.ContainsKey(temp[i]))
            mp[temp[i]]++;
        else
            mp.Add(temp[i],1);
    }

    // Stores the partitions
    List<List<int>> P = new List<List<int>>();

    // Stores temporary subarrays
    List<int> V = new List<int>();

    // Iterate over the range [0, N - 1]
    for(int i = 0; i < N; i++)
    {
        V.Add(arr[i]);

        // If current element is
        // one of the K largest
        if (mp.ContainsKey(arr[i]) && mp[arr[i]] > 0)
        {
            mp[arr[i]]--;
            K--;

            if (K == 0)
            {
                i++;

                while (i < N)
                {
                    V.Add(arr[i]);
                    i++;
                }
            }

            if (V.Count > 0)
            {
                P.Add(new List<int>(V));
                V.Clear();
            }
        }
    }

    // Print the ans
    Console.WriteLine(ans);

    // Print the partition
    foreach (List<int> subList in P)
    {
        foreach (int item in subList)
        {
            Console.Write(item+" ");
        }
        Console.WriteLine();
    }
}

// Driver code
public static void Main()
{

    // Input
    int []A = { 5, 3, 2, 7, 6, 4 };
    int N = A.Length;
    int K = 3;

    // Function call
    partitionIntoKSegments(A, N, K);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>
// Javascript program for tha above approach

// Function to split the array into K
// subarrays such that the sum of
// maximum of each subarray is maximized
function partitionIntoKSegments(arr, N, K)
{

    // If N is less than K
    if (N < K) {
        document.write(-1 + "<br>");
        return;
    }

    // Map to store the K
    // largest elements
    let mp = new Map();

    // Auxiliary array to
    // store and sort arr[]
    let temp = new Array(N);

    // Stores the maximum sum
    let ans = 0;

    // Copy arr[] to temp[]
    for (let i = 0; i < N; i++) {
        temp[i] = arr[i];
    }

    // Sort array temp[] in
    // descending order
    temp.sort((a, b) => a - b).reverse();

    // Iterate in the range [0, K - 1]
    for (let i = 0; i < K; i++) {

        // Increment sum by temp[i]
        ans += temp[i];

        // Increment count of
        // temp[i] in the map mp
        if (mp.has(temp[i])) {
            mp.set(temp[i], mp.get(temp[i]) + 1)
        } else {
            mp.set(temp[i], 1)
        }
    }

    // Stores the partitions
    let P = [];

    // Stores temporary subarrays
    let V = [];

    // Iterate over the range [0, N - 1]
    for (let i = 0; i < N; i++) {
        V.push(arr[i]);

        // If current element is
        // one of the K largest
        if (mp.get(arr[i]) > 0)
        {

            mp.set(arr[i], mp.get(arr[i]) - 1)
            K--;

            if (K == 0) {
                i++;
                while (i < N) {
                    V.push(arr[i]);
                    i++;
                }
            }

            if (V.length) {
                P.push(V);
                V = [];
            }
        }
    }

    // Print the ans
    document.write(ans + "<br>");

    // Print the partition
    for (let u of P) {
        for (let x of u)
            document.write(x + " ");
        document.write("<br>");
    }
}

// Driver code
// Input
let A = [5, 3, 2, 7, 6, 4];
let N = A.length
let K = 3;

// Function call
partitionIntoKSegments(A, N, K);

// This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
18
5 
3 2 7 
6 4
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(N)*