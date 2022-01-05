# 使用给定的 Q 异或查询构建一个列表

> 原文:[https://www . geeksforgeeks . org/construct-a-list-use-given-q-xor-query/](https://www.geeksforgeeks.org/construct-a-list-using-the-given-q-xor-queries/)

给定一个最初包含单个值 **0** 的列表 **S** 。以下是以下类型的**问题**查询:

*   **0 X** :列表中插入 X
*   **1 X** :对于 S 中的每个元素 A，用 A XOR X 替换

任务是在执行给定的 **Q** 查询后，按升序打印列表中的所有元素。

**示例:**

> **输入:** Q[][] = { {0，6}、{0，3}、{0，2}、{1，4}、{1，5} }
> **输出:** 1 2 3 7
> **解释:**T8】【0】(初始值)
> 【0 6】(列表增加 6)
> 【0 6 3】(列表增加 3)
> 【0 6 3 2】(列表增加 2)
> 【4 2 7
> 
> **输入:** Q[][]= {{0，2}，{1，3}，{0，5} }
> **输出:** 1 3 5
> **解释:**
> 【0】(初始值)
> 【0 2】(列表加 2)
> 【3 1】(每个元素用 3 异或)
> 【3 1 5】(列表加 5)
> 这样执行查询后排序顺序为【1 3 5】

**天真的方法:**解决问题最简单的方法是:

1.  用 **0** 初始化一个列表，然后遍历每个查询，并执行以下操作:
    *   对于查询类型 0，在列表中添加给定值。
    *   对于查询类型 1，遍历列表并使用它们各自的[值**值**按位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)来更新每个元素。
2.  执行完所有查询后，按升序打印最终列表。

***时间复杂度:** O(N*Q)，其中 N 为列表长度，Q 为查询次数*
***辅助空间:** O(1)*

**高效方法:**通过跟踪从右到左工作的累积[逐位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)，以相反的顺序处理数字要容易得多。按照以下步骤解决问题:

1.  用 **0 初始化一个变量异或。**
2.  从右到左迭代查询数组，将 **xor^value** 添加到列表中，同时查询类型为 **0** ,否则使用 **xor^value** 更新 xor。
3.  遍历查询后，在列表中加入**异或**，对最终列表进行排序。
4.  完成上述操作后，打印最终列表。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
#define N 5
#define M 2

// Function to return required list
// after performing all the queries
list<int> ConstructList(int Q[N][M])
{

    // Store cumulative Bitwise XOR
    int xr = 0;

    // Initialize final list to return
    list<int> ans;

    // Perform each query
    for (int i = N - 1; i >= 0; i--)
    {
        if (Q[i][0] == 0)
            ans.push_back(Q[i][1] ^ xr);
        else
            xr ^= Q[i][1];
    }

    // The initial value of 0
    ans.push_back(xr);

    // Sort the list
    ans.sort();

    // Return final list
    return ans;
}

// Driver Code
int main()
{
    // Given Queries
    int Q[N][M] = {{ 0, 6 }, { 0, 3 },
                   { 0, 2 }, { 1, 4 },
                   { 1, 5 }};

    // Function Call
    list<int> ans = ConstructList(Q);
    for (auto it = ans.begin(); it != ans.end(); ++it)
        cout << ' ' << *it;
}

// This code is contributed by gauravrajput1
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to return required list
    // after performing all the queries
    static List<Integer> ConstructList(int[][] Q)
    {

        // Store cumulative Bitwise XOR
        int xor = 0;

        // Initialize final list to return
        List<Integer> ans = new ArrayList<>();

        // Perform each query
        for (int i = Q.length - 1; i >= 0; i--) {

            if (Q[i][0] == 0)
                ans.add(Q[i][1] ^ xor);

            else
                xor ^= Q[i][1];
        }

        // The initial value of 0
        ans.add(xor);

        // Sort the list
        Collections.sort(ans);

        // Return final list
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given Queries
        int[][] Q = {
            { 0, 6 }, { 0, 3 }, { 0, 2 },
            { 1, 4 }, { 1, 5 }
        };

        // Function Call
        System.out.println(ConstructList(Q));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to return required list
# after performing all the queries
def ConstructList(Q):

    # Store cumulative Bitwise XOR
    xor = 0

    # Initialize final list to return
    ans = []

    # Perform each query
    for i in range(len(Q) - 1, -1, -1):
        if(Q[i][0] == 0):
            ans.append(Q[i][1] ^ xor)

        else:
            xor ^= Q[i][1]

    # The initial value of 0
    ans.append(xor)

    # Sort the list
    ans.sort()

    # Return final list
    return ans

# Driver Code

# Given Queries
Q = [ [0, 6], [0, 3],
      [0, 2], [1, 4],
      [1, 5] ]

# Function call
print(ConstructList(Q))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

    // Function to return required list
    // after performing all the queries
    static List<int> ConstructList(int[,] Q)
    {

        // Store cumulative Bitwise XOR
        int xor = 0;

        // Initialize readonly list to return
        List<int> ans = new List<int>();

        // Perform each query
        for (int i = Q.GetLength(0) - 1; i >= 0; i--)
        {
            if (Q[i, 0] == 0)
                ans.Add(Q[i, 1] ^ xor);

            else
                xor ^= Q[i, 1];
        }

        // The initial value of 0
        ans.Add(xor);

        // Sort the list
        ans.Sort();

        // Return readonly list
        return ans;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        // Given Queries
        int[,] Q = {{ 0, 6 }, { 0, 3 }, { 0, 2 },
                    { 1, 4 }, { 1, 5 }};

        // Function Call
        foreach( int i in ConstructList(Q))
            Console.Write(i + ", ");
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript program for the above approach
var N = 5
var M = 2

// Function to return required list
// after performing all the queries
function ConstructList(Q)
{

    // Store cumulative Bitwise XOR
    var xr = 0;

    // Initialize final list to return
    var ans = [];

    // Perform each query
    for (var i = N - 1; i >= 0; i--)
    {
        if (Q[i][0] == 0)
            ans.push(Q[i][1] ^ xr);
        else
            xr ^= Q[i][1];
    }

    // The initial value of 0
    ans.push(xr);

    // Sort the list
    ans.sort((a,b)=>a-b);

    // Return final list
    return ans;
}

// Driver Code
// Given Queries
var Q = [[ 0, 6 ], [ 0, 3 ],
               [ 0, 2 ], [ 1, 4 ],
               [ 1, 5 ]];
// Function Call
var ans = ConstructList(Q);
ans.forEach(element => {
    document.write(" "+element);
});

// This code is contributed by famously.
</script>
```

**Output:** 

```
[1, 2, 3, 7]
```

***时间复杂度:** O(Q * log(Q))* ，其中 Q 为查询次数。
***辅助空间:** O(N)* ，其中 N 为结果列表中的元素个数。