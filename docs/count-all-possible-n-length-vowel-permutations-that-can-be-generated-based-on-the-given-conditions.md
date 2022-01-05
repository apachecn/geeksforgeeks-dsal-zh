# 根据给定条件

统计所有可能产生的 N 长元音排列

> 原文:[https://www . geeksforgeeks . org/count-all-可能性-n-length-元音-置换-可以基于给定的条件生成/](https://www.geeksforgeeks.org/count-all-possible-n-length-vowel-permutations-that-can-be-generated-based-on-the-given-conditions/)

给定一个整数 **N** ，任务是统计由小写元音组成的 N 长度字符串的数量，这些字符串可以基于以下条件生成:

*   每个**‘a’**后面只能跟一个**‘e’**。
*   每个**‘e’**后面只能跟一个**‘a’**或者一个**‘I’。**
*   每个**‘I’**后面不可以跟另一个**‘I’**。
*   每个**后面只能跟一个**【I】**或一个**。****
*   ****每个**后面只能跟一个**【a】**。******

******示例:******

> ******输入:** N = 1
> **输出:** 5
> **说明:**所有可以构成的字符串都是:“a”、“e”、“I”、“o”和“u”。****
> 
> ******输入:** N = 2
> **输出:** 10
> **说明:**所有可以构成的字符串为:“AE”“ea”“ei”“ia”“ie”“io”“iu”“oi”“ou”“ua”。****

******方法:**解决这个问题的思路是将其可视化为[图形问题](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)。根据给定的规则，可以构造一个[有向图](https://www.geeksforgeeks.org/detect-cycle-in-a-graph/)，其中从 **u** 到 **v** 的边意味着 **v** 可以紧接在结果字符串中的 **u** 之后。该问题简化为在构造的有向图中寻找 N 长度路径的数目。按照以下步骤解决问题:****

*   ****让元音 **a、e、I、o、u** 分别编号为 **0、1、2、3、4** ，并使用给定图中所示的依赖关系，将该图转换为邻接表**关系**，其中索引表示元音，该索引处的列表表示从该索引到列表中给定字符的边。****

****![](img/b86eaaabb0cc5e37d6064f5ac6bc9f7c.png)****

*   ****初始化一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-in-java/)**DP【N+1】【5】**，其中**DP【N】【字符】**表示长度为 **N** 的有向路径的数量，其在特定顶点**字符**处结束。****
*   ****将所有字符的 **dp[i][char]** 初始化为 **1** ，因为长度为 1 的**字符串将只包含字符串中的一个元音。******
*   ****对于所有可能的长度，假设 **i** ，使用变量 **u** 遍历有向边，并执行以下步骤:

    *   将 **dp[i + 1][u]** 的值更新为 **0** 。
    *   遍历**节点 u** 的邻接表，将 **dp[i][u]** 的值增加 **dp[i][v]** ，该值存储所有值的和，使得存在从**节点 u** 到**节点 v** 的有向边。**** 
*   ****完成上述步骤后，所有值 **dp[N][i]** 的和，其中 I 属于范围**【0，5】**，将给出元音排列的总数。****

****下面是上述方法的实现:****

## ****C++****

```
**// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number of
// vowel permutations possible
int countVowelPermutation(int n)
{

    // To avoid the large output value
    int MOD = (int)(1e9 + 7);

    // Initialize 2D dp array
    long dp[n + 1][5];

    // Initialize dp[1][i] as 1 since
    // string of length 1 will consist
    // of only one vowel in the string
    for(int i = 0; i < 5; i++)
    {
        dp[1][i] = 1;
    }

    // Directed graph using the
    // adjacency matrix
    vector<vector<int>> relation = {
        { 1 }, { 0, 2 },
        { 0, 1, 3, 4 },
        { 2, 4 }, { 0 }
    };

    // Iterate over the range [1, N]
    for(int i = 1; i < n; i++)
    {

        // Traverse the directed graph
        for(int u = 0; u < 5; u++)
        {
            dp[i + 1][u] = 0;

            // Traversing the list
            for(int v : relation[u])
            {

                // Update dp[i + 1][u]
                dp[i + 1][u] += dp[i][v] % MOD;
            }
        }
    }

    // Stores total count of permutations
    long ans = 0;

    for(int i = 0; i < 5; i++)
    {
        ans = (ans + dp[n][i]) % MOD;
    }

    // Return count of permutations
    return (int)ans;
}

// Driver code
int main()
{
    int N = 2;

    cout << countVowelPermutation(N);
}

// This code is contributed by Mohit kumar 29**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program for the above approach

import java.io.*;
import java.util.*;
class GFG {

    // Function to find the number of
    // vowel permutations possible
    public static int
    countVowelPermutation(int n)
    {
        // To avoid the large output value
        int MOD = (int)(1e9 + 7);

        // Initialize 2D dp array
        long[][] dp = new long[n + 1][5];

        // Initialize dp[1][i] as 1 since
        // string of length 1 will consist
        // of only one vowel in the string
        for (int i = 0; i < 5; i++) {
            dp[1][i] = 1;
        }

        // Directed graph using the
        // adjacency matrix
        int[][] relation = new int[][] {
            { 1 }, { 0, 2 },
            { 0, 1, 3, 4 },
            { 2, 4 }, { 0 }
        };

        // Iterate over the range [1, N]
        for (int i = 1; i < n; i++) {

            // Traverse the directed graph
            for (int u = 0; u < 5; u++) {
                dp[i + 1][u] = 0;

                // Traversing the list
                for (int v : relation[u]) {

                    // Update dp[i + 1][u]
                    dp[i + 1][u] += dp[i][v] % MOD;
                }
            }
        }

        // Stores total count of permutations
        long ans = 0;

        for (int i = 0; i < 5; i++) {
            ans = (ans + dp[n][i]) % MOD;
        }

        // Return count of permutations
        return (int)ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 2;
        System.out.println(
            countVowelPermutation(N));
    }
}**
```

## ****蟒蛇 3****

```
**# Python 3 program for the above approach

# Function to find the number of
# vowel permutations possible
def countVowelPermutation(n):

    # To avoid the large output value
    MOD =  1e9 + 7

    # Initialize 2D dp array
    dp = [[0 for i in range(5)] for j in range(n + 1)]

    # Initialize dp[1][i] as 1 since
    # string of length 1 will consist
    # of only one vowel in the string
    for i in range(5):
        dp[1][i] = 1

    # Directed graph using the
    # adjacency matrix
    relation = [[1],[0, 2], [0, 1, 3, 4], [2, 4],[0]]

    # Iterate over the range [1, N]
    for i in range(1, n, 1):

        # Traverse the directed graph
        for u in range(5):
            dp[i + 1][u] = 0

            # Traversing the list
            for v in relation[u]:

                # Update dp[i + 1][u]
                dp[i + 1][u] += dp[i][v] % MOD

    # Stores total count of permutations
    ans = 0
    for i in range(5):
        ans = (ans + dp[n][i]) % MOD

    # Return count of permutations
    return int(ans)

# Driver code
if __name__ == '__main__':
    N = 2
    print(countVowelPermutation(N))

    # This code is contributed by bgangwar59.**
```

## ****C#****

```
**// C# program to find absolute difference
// between the sum of all odd frequenct and
// even frequent elements in an array
using System;
using System.Collections.Generic;
class GFG {

    // Function to find the number of
    // vowel permutations possible
    static int countVowelPermutation(int n)
    {

        // To avoid the large output value
        int MOD = (int)(1e9 + 7);

        // Initialize 2D dp array
        long[,] dp = new long[n + 1, 5];

        // Initialize dp[1][i] as 1 since
        // string of length 1 will consist
        // of only one vowel in the string
        for (int i = 0; i < 5; i++) {
            dp[1, i] = 1;
        }

        // Directed graph using the
        // adjacency matrix
        List<List<int>> relation = new List<List<int>>();
        relation.Add(new List<int> { 1 });
        relation.Add(new List<int> { 0, 2 });
        relation.Add(new List<int> { 0, 1, 3, 4 });
        relation.Add(new List<int> { 2, 4 });
        relation.Add(new List<int> { 0 });

        // Iterate over the range [1, N]
        for (int i = 1; i < n; i++)
        {

            // Traverse the directed graph
            for (int u = 0; u < 5; u++)
            {
                dp[i + 1, u] = 0;

                // Traversing the list
                foreach(int v in relation[u])
                {

                    // Update dp[i + 1][u]
                    dp[i + 1, u] += dp[i, v] % MOD;
                }
            }
        }

        // Stores total count of permutations
        long ans = 0;

        for (int i = 0; i < 5; i++)
        {
            ans = (ans + dp[n, i]) % MOD;
        }

        // Return count of permutations
        return (int)ans;
    }

  // Driver code
  static void Main() {
    int N = 2;
    Console.WriteLine(countVowelPermutation(N));
  }
}

// This code is contributed by divyesh072019.**
```

## ****java 描述语言****

```
**<script>

// JavaScript program to implement
// the above approach

    // Function to find the number of
    // vowel permutations possible
    function
    countVowelPermutation(n)
    {
        // To avoid the large output value
        let MOD = (1e9 + 7);

        // Initialize 2D dp array
        let dp = new Array(n + 1);

        // Loop to create 2D array using 1D array
        for (var i = 0; i < dp.length; i++) {
            dp[i] = new Array(2);
        }

        // Initialize dp[1][i] as 1 since
        // string of length 1 will consist
        // of only one vowel in the string
        for (let i = 0; i < 5; i++) {
            dp[1][i] = 1;
        }

        // Directed graph using the
        // adjacency matrix
        let relation = [
            [ 1 ], [ 0, 2 ],
            [ 0, 1, 3, 4 ],
            [ 2, 4 ], [ 0 ]
        ];

        // Iterate over the range [1, N]
        for (let i = 1; i < n; i++) {

            // Traverse the directed graph
            for (let u = 0; u < 5; u++) {
                dp[i + 1][u] = 0;

                // Traversing the list
                for (let v in relation[u]) {

                    // Update dp[i + 1][u]
                    dp[i + 1][u] += dp[i][v] % MOD;
                }
            }
        }

        // Stores total count of permutations
        let ans = 0;

        for (let i = 0; i < 5; i++) {
            ans = (ans + dp[n][i]) % MOD;
        }

        // Return count of permutations
        return ans;
    }

// Driver code

    let N = 2;
    document.write(
            countVowelPermutation(N));

</script>**
```

******Output:** 

```
10
```**** 

*******时间复杂度:**O(N)*
T5**辅助空间:** O(N)****