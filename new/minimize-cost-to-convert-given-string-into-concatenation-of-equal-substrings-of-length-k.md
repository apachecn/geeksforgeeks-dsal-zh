# 最小化将给定字符串转换为长度为 K 的相等子字符串的串联的成本

> 原文：[https://www.geeksforgeeks.org/minimize-cost-to-convert-given-string-into-concatenation-of-equal-substrings-of-length-k/](https://www.geeksforgeeks.org/minimize-cost-to-convert-given-string-into-concatenation-of-equal-substrings-of-length-k/)

给定[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，长度为 **N** ，由小写字母和整数 **K** 组成，其中 **N％K = 0 [** ，任务是通过执行以下操作来找到将给定字符串转换为相同 **K** 个长度子字符串的串联字符串的最低成本：

*   一个字符可以替换为另一个字符。

*   每次操作的成本是被替换字符与替换字符之间的绝对差额。 例如，如果将**'a'**替换为**'z'**，则操作成本为 **|“ a”-“ z” | = 25** 。

**示例**：

> **输入**：S =“ abcdef”，K = 2
> **输出**：8
> **说明**：
> 一个可能的答案是“ cdcdcd” 而 repeatingK length 子字符串为“ cd”。 转换字符串所需的最低成本通过以下步骤计算：
> 步骤 1：将 S [0]替换为“ c”。 因此，成本= |“ a”-“ c” | =2。
> 步骤 2：将 S [1]替换为“ d”。 因此，成本= |“ b”-“ d” | =2。
> 步骤 3：将 S [2]替换为“ c”。 因此，成本= |“ c”-“ c” | =0。
> 步骤 4：将 S [3]替换为“ d”。 因此，成本= |“ d”-“ d” | =0。
> 步骤 5：将 S [4]替换为“ c”。 因此，成本= |“ e”-“ c” | =2。
> 步骤 6：将 S [5]替换为“ d”。 因此，成本= |“ f”-“ d” | =2。
> 因此，所需的最低成本= 2 + 2 + 0 + 0 + 2 + 2 = 8。
> 
> **输入**：S =“ abcabc”，K = 3
> **输出**：0
> **说明**：
> 给定的字符串已经包含重复 长度为 K 的子字符串“ abc”

**天真的方法**：最简单的方法是[生成所有长度为 **K** 的可能排列](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)并找出转换给定字符串以使其具有重复模式的成本 长度 **K** 。 然后，打印其中的最低成本。

**时间复杂度**：O（N * K <sup>26</sup> ），其中 N 是给定字符串的长度，K 是给定整数。

**辅助空间**：`O(n)`

**有效方法**：的想法是使用[贪婪技术](https://www.geeksforgeeks.org/greedy-algorithms/)，并观察到从 **0** 到 **K 的任何位置 **i** 1** ，位置 **i + j * K** 处的字符必须相同，其中 **0≤j < N / K** 。 例如，如果 **S =“ abcbbc”** 和 **K = 3** ，则位置 **0** 和 **3** 处的字符必须相等，字符 **1** 和 **4** 位置上的字符必须相同，并且 **2** 和 **5** 位置上的字符必须相等。 因此，可以分别计算位置 **i + j * K** 处字符的最低成本。 请按照以下步骤解决问题：

*   初始化变量**和**以存储所需的最低成本。

*   [在 **[0，K – 1]** 范围内遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)。

*   对于每个位置 **i** ，对于将每个字符 **0≤j < N / K [** 。 计算其中的最小成本并更新**和**。

*   完成上述步骤后，将**和**的值打印为所需的最低成本。

下面是上述方法的实现：

## Java

```java

// Java program for the above approach

import java.util.*;
import java.lang.*;

class GFG {

    // Function to find minimum cost
    // to convert given string into
    // string of K length same substring
    static void minCost(String s, int k)
    {
        // Stores length of string
        int n = s.length();

        // Stores the minimum cost
        int ans = 0;

        // Traverse left substring
        // of k length
        for (int i = 0; i < k; i++) {

            // Stores the frequency
            int[] a = new int[26];

            for (int j = i; j < n; j += k) {
                a[s.charAt(j) - 'a']++;
            }

            // Stores minimum cost for
            // sequence of S[i]%k indices
            int min_cost
                = Integer.MAX_VALUE;

            // Check for optimal charcter
            for (int ch = 0; ch < 26; ch++) {

                int cost = 0;

                // Find sum of distance 'a'+ ch
                // from charcter S[i]%k indices
                for (int tr = 0; tr < 26; tr++)
                    cost += Math.abs(ch - tr)
                            * a[tr];

                // Choose minimum cost for
                // each index i
                min_cost = Math.min(min_cost,
                                    cost);
            }

            // Increment ans
            ans += min_cost;
        }

        // Print minimum cost to
        // convert string
        System.out.println(ans);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given string S
        String S = "abcdefabc";

        int K = 3;

        // Function Call
        minCost(S, K);
    }
}

```

## C#

```cs

// C# program for the 
// above approach
using System;

class GFG{

// Function to find minimum cost
// to convert given string into
// string of K length same substring
static void minCost(string s, int k)
{

    // Stores length of string
    int n = s.Length;

    // Stores the minimum cost
    int ans = 0;

    // Traverse left substring
    // of k length
    for(int i = 0; i < k; i++)
    {

        // Stores the frequency
        int[] a = new int[26];

        for(int j = i; j < n; j += k)
        {
            a[s[j] - 'a']++;
        }

        // Stores minimum cost for
        // sequence of S[i]%k indices
        int min_cost = Int32.MaxValue;

        // Check for optimal charcter
        for(int ch = 0; ch < 26; ch++)
        {
            int cost = 0;

            // Find sum of distance 'a'+ ch
            // from charcter S[i]%k indices
            for(int tr = 0; tr < 26; tr++)
                cost += Math.Abs(ch - tr) * a[tr];

            // Choose minimum cost for
            // each index i
            min_cost = Math.Min(min_cost,
                                cost);
        }

        // Increment ans
        ans += min_cost;
    }

    // Print minimum cost to
    // convert string
    Console.WriteLine(ans);
}

// Driver Code
public static void Main()
{

    // Given string S
    string S = "abcdefabc";

    int K = 3;

    // Function call
    minCost(S, K);
}
}

// This code is contributed by sanjoy_62

```

**Output:** 

```
9

```

**时间复杂度**：O（N + K）

**辅助空间**：`O(n)`



* * *

* * *



