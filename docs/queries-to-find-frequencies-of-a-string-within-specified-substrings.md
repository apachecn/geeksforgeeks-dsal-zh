# 在指定子串中查找字符串频率的查询

> 原文:[https://www . geesforgeks . org/query-to-find-frequency-of-a-string-in-specific-substrings/](https://www.geeksforgeeks.org/queries-to-find-frequencies-of-a-string-within-specified-substrings/)

给定查询的字符串 **S** 和矩阵 **Q** ，每个查询分别指定 S 的子串的开始和结束索引 **L( = Q[i][0])** 和 **R( = Q[i][0])** ，任务是在子串**【L，R】**中找到字符串 **K** 的频率。

**注意:**范围遵循基于 1 的索引。

**示例:**

> **输入:**S = " gfgfgffg "，K = "GFG "，Q = {{1，8}，{3，5}，{5，8}}
> **输出:**
> 2
> 0
> 1
> **说明:**对于查询 1，从索引 1 到索引 8 有 2 个(“GFG”)子串。一个是从索引 1 到 3，另一个是从索引 6 到 8。
> 对于查询 2，从索引 3 到 5 有 0 个(“GFG”)子字符串。
> 对于查询 3，从索引 5 到索引 8 有 1 个(“GFG”)子串。唯一的子串是从索引 6 到 8。
> 
> **输入:**S =“abcbababc”，K =“ABC”，Q = {{1，6}，{5，11 } }
> T3】输出:T5】2
> 1

**天真方法:**
对所有查询运行从 **L** 到 **R** 的循环。计数字符串 **K** 的出现次数并返回计数。

**时间复杂度:**O(Q * S |的长度)。

**有效方法:**
预先计算并存储每个指标的 K 频率。现在，要计算一个范围内的弦的频率**【L，R】**，我们只需要计算指数 **(R-1)** 和 **(L-1)** 处的 K 的频率之差。

下面是上述方法的实现:

## C++

```
// C++ Program to find
// frequency of a string K
// in a substring [L, R] in S

#include <bits/stdc++.h>
#define max_len 100005
using namespace std;

// Store the frequency of
// string for each index
int cnt[max_len];

// Compute and store frequencies
// for every index
void precompute(string s, string K)
{

    int n = s.size();
    for (int i = 0; i < n - 1; i++) {
        cnt[i + 1]
            = cnt[i]
              + (s.substr(i, K.size()) == K);
    }
}

// Driver Code
int main()
{
    string s = "ABCABCABABC";
    string K = "ABC";
    precompute(s, K);

    vector<pair<int, int> > Q
        = { { 1, 6 }, { 5, 11 } };

    for (auto it : Q) {
        cout << cnt[it.second - 1]
                    - cnt[it.first - 1]
             << endl;
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// frequency of a string K
// in a substring [L, R] in S
class GFG{

static int max_len = 100005;

// Store the frequency of
// string for each index
static int cnt[] = new int[max_len];

// Compute and store frequencies
// for every index
public static void precompute(String s,
                              String K)
{
    int n = s.length();

    for(int i = 0; i < n - 2; i++)
    {
        cnt[i + 1] = cnt[i];
        if (s.substring(
            i, i + K.length()).equals(K))
        {
            cnt[i + 1] += 1;
        }
    }
    cnt[n - 2 + 1] = cnt[n - 2];
}

// Driver code
public static void main(String[] args)
{
    String s = "ABCABCABABC";
    String K = "ABC";
    precompute(s, K);

    int Q[][] = { { 1, 6 }, { 5, 11 } };

    for(int it = 0; it < Q.length; it++)
    {
        System.out.println(cnt[Q[it][1] - 1] -
                           cnt[Q[it][0] - 1]);
    }
}
}

// This code is contributed by divyesh072019
```

## 蟒蛇 3

```
# Python3 Program to find
# frequency of a string K
# in a substring [L, R] in S
max_len = 100005

# Store the frequency of
# string for each index
cnt = [0] * max_len

# Compute and store frequencies
# for every index
def precompute(s, K):

    n = len(s)
    for i in range(n - 1):
        cnt[i + 1] = cnt[i]
        if s[i : len(K) + i] == K:
            cnt[i + 1] += 1

# Driver Code
if __name__ == "__main__":

    s = "ABCABCABABC"
    K = "ABC"
    precompute(s, K)
    Q = [[1, 6], [5, 11]]

    for it in Q:
        print(cnt[it[1] - 1] -
              cnt[it[0] - 1])

# This code is contributed by Chitranayal
```

## C#

```
// C# program to find frequency of
// a string K in a substring [L, R] in S
using System.IO;
using System;

class GFG{

static int max_len = 100005;

// Store the frequency of
// string for each index
static int[] cnt = new int[max_len];

// Compute and store frequencies
// for every index
static void precompute(string s,string K)
{
    int n = s.Length;

    for(int i = 0; i < n - 2; i++)
    {
        cnt[i + 1] = cnt[i];

        if (s.Substring(i, K.Length).Equals(K))
        {
            cnt[i + 1] += 1;
        }
    }
    cnt[n - 2 + 1] = cnt[n - 2];
}

// Driver code
static void Main()
{
    string s = "ABCABCABABC";
    string K = "ABC";
    precompute(s, K);
    int[,] Q = { { 1, 6 }, { 5, 11 } };

    for(int it = 0; it < Q.GetLength(0); it++)
    {  
        Console.WriteLine(cnt[Q[it, 1] - 1] -
                          cnt[Q[it, 0] - 1]);
    }
}
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>

// Javascript program to find
// frequency of a string K
// in a substring [L, R] in S
var max_len = 100005;

// Store the frequency of
// string for each index
var cnt = Array(max_len).fill(0);

// Compute and store frequencies
// for every index
function precompute(s, K)
{
    var n = s.length;
    for(var i = 0; i < n - 1; i++)
    {
        cnt[i + 1] = cnt[i] +
        (s.substring(i, i + K.length) == K);
    }
}

// Driver Code
var s = "ABCABCABABC";
var K = "ABC";
precompute(s, K);
var Q = [ [ 1, 6 ], [ 5, 11 ] ];

Q.forEach((it) => {

    document.write(cnt[it[1] - 1] -
                   cnt[it[0] - 1] + "<br>");
});

// This code is contributed by itsok

</script>
```

**Output:** 

```
2
1
```

**时间复杂度:***O(| S |+Q 的长度)*，因为每个查询都是在 O(1)中回答的。
**辅助空间:** *O( |S| )*