# 插入一个字符增加一个 LCS 的方法数

> 原文:[https://www . geesforgeks . org/number-way-insert-character-address-LCS-one/](https://www.geeksforgeeks.org/number-ways-insert-character-increase-lcs-one/)

给定两根弦 **A** 和 **B** 。任务是计算在字符串 A 中插入一个字符的方法的数量，以将字符串 A 和字符串 B 之间的最长公共子序列的长度增加 1。
**例:**

> 输入:A =“aa”，B =“baaa”
> 输出:4
> 字符串 A 和字符串 B 共享的最长公共子序列为“aa”，长度为 2。
> 有两种方法可以通过在字符串 A 中添加单个字符来将最长的公共子序列的长度增加到 3:
> 
> 1.  字符串 A 中有 3 个不同的位置，我们可以在其中插入一个额外的“A”来创建最长的公共子序列“aaa”(即在字符串的开头、中间和结尾)。
> 2.  我们可以在字符串的开头插入一个“b”，作为新的最长的公共子序列“baaa”。因此，我们有 3 + 1 = 4 种方法将字母数字字符插入字符串 A，并将最长的公共子序列的长度增加 1。

假设对于给定的弦 A 和弦 B，它们的 [LCS](https://www.geeksforgeeks.org/longest-common-subsequence/) 的长度是 **k** 。让我们在字符串 A 中的第 ith 个字符后插入单个字符“c”，并将插入后形成的字符串表示为字符串 A <sub>new</sub> ，看起来像:
A <sub>new</sub> = A <sub>1，i</sub> 。c . A <sub>i + 1，n</sub>
其中 A <sub>i，j</sub> 表示从第 ith 到第 jth 个字符和“.”的字符串 A 的子字符串表示两个字符串的串联。
我们把 k <sub>new</sub> 定义为 A <sub>new</sub> 和 b 的 LCS 长度，现在我们想知道 k <sub>new</sub> 是否= k + 1。
关键的观察是，新插入的字符“c”必须是长度为> k 的 A <sub>new</sub> 和 B 的任何公共子序列的一部分。我们知道这一点，因为如果存在 A <sub>new</sub> 和 B 的任何公共子序列，这是一个矛盾，因为这意味着 A 和 B 的 LCS 长度为>k。
使用上述观察，我们可以尝试以下方法。对于每个可能的字符‘c’(有 52 个大小写英文字母和 10 个阿拉伯数字，因此有 62 个可能的字符要插入)以及对于字符串 A 中的每个可能的插入 I(有|a| + 1 个插入位置)，让我们尝试在字符串 A 中的 ith 字符之后插入‘c’，并将其与字符串 B 中的‘c’的每个出现相匹配，我们可以尝试匹配这些‘c’字符，例如:
A <sub>1，i</sub> 。c . A <sub>i+1，n</sub>T34】B<sub>1，j-1</sub> 。c . B <sub>j+1，m</sub>
现在，为了检查这样的插入是否产生长度为 k + 1 的 LCS，检查 A <sub>1，i</sub> 和 B <sub>1，j-1</sub> 的 LCS 长度加上 LCS A <sub>i+1，n</sub> 和 B <sub>j+1，m</sub> 的长度是否等于 k 就足够了。在这种情况下， A <sub>新</sub>和 B 的 lCS 是 k + 1，因为在字符‘c’的固定出现之间存在匹配，并且它们之间不再存在共同的子序列。
如果我们能快速得到 A 和 B 的每两个前缀之间以及它们的每两个后缀之间的 LCS 长度，我们就能计算出结果。在这种方法中，dp[i][j]存储 A <sub>，i</sub> 和 B <sub>i，j</sub> 的最长公共子序列的长度。类似地，它们的后缀之间的 LCS 长度可以从类似的 dp 表中读取，该 DP 表可以在计算 A <sub>反转</sub>和 B <sub>反转</sub>的 LCS 期间计算，其中 S <sub>反转</sub>表示反转的字符串 S

## C++

```
// CPP Program to Number of ways to insert a
// character to increase LCS by one
#include <bits/stdc++.h>
#define MAX 256
using namespace std;

// Return the Number of ways to insert a
// character to increase the Longest
// Common Subsequence by one
int numberofways(string A, string B, int N, int M)
{
    vector<int> pos[MAX];

    // Insert all positions of all characters
    // in string B.
    for (int i = 0; i < M; i++)
        pos[B[i]].push_back(i + 1);

    // Longest Common Subsequence
    int dpl[N + 2][M + 2];
    memset(dpl, 0, sizeof(dpl));
    for (int i = 1; i <= N; i++) {
        for (int j = 1; j <= M; j++) {
            if (A[i - 1] == B[j - 1])
                dpl[i][j] = dpl[i - 1][j - 1] + 1;
            else
                dpl[i][j] = max(dpl[i - 1][j],
                                dpl[i][j - 1]);
        }
    }
    int LCS = dpl[N][M];

    // Longest Common Subsequence from reverse
    int dpr[N + 2][M + 2];
    memset(dpr, 0, sizeof(dpr));
    for (int i = N; i >= 1; i--) {
        for (int j = M; j >= 1; j--) {
            if (A[i - 1] == B[j - 1])
                dpr[i][j] = dpr[i + 1][j + 1] + 1;
            else
                dpr[i][j] = max(dpr[i + 1][j],
                                dpr[i][j + 1]);
        }
    }

    // inserting character between position
    // i and i+1
    int ans = 0;
    for (int i = 0; i <= N; i++) {
        for (int j = 0; j < MAX; j++) {
            for (auto x : pos[j]) {
                if (dpl[i][x - 1] + dpr[i + 1][x + 1] == LCS) {
                    ans++;
                    break;
                }
            }
        }
    }

    return ans;
}

// Driver Program
int main()
{
    string A = "aa", B = "baaa";
    int N = A.length(), M = B.length();
    cout << numberofways(A, B, N, M) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for Number of ways to insert a
// character to increase LCS by one
import java.util.*;

class GFG
{
    static final int MAX = 256;

    // Return the Number of ways to insert a
    // character to increase the Longest
    // Common Subsequence by one
    static int numberofways(String A, String B, int N, int M)
    {
        Vector<Integer>[] pos = new Vector[MAX];

        // Insert all positions of all characters
        // in string B.
        for (int i = 0; i < MAX; i++)
            pos[i] = new Vector<>();

        for (int i = 0; i < M; i++)
            pos[B.charAt(i)].add(i + 1);

        // Longest Common Subsequence
        int[][] dpl = new int[N + 2][M + 2];
        for (int i = 1; i <= N; i++)
        {
            for (int j = 1; j <= M; j++)
            {
                if (A.charAt(i - 1) == B.charAt(j - 1))
                    dpl[i][j] = dpl[i - 1][j - 1] + 1;
                else
                    dpl[i][j] = Math.max(dpl[i - 1][j],
                                         dpl[i][j - 1]);
            }
        }
        int LCS = dpl[N][M];

        // Longest Common Subsequence from reverse
        int[][] dpr = new int[N + 2][M + 2];
        for (int i = N; i >= 1; i--)
        {
            for (int j = M; j >= 1; j--)
            {
                if (A.charAt(i - 1) == B.charAt(j - 1))
                    dpr[i][j] = dpr[i + 1][j + 1] + 1;
                else
                    dpr[i][j] = Math.max(dpr[i + 1][j],
                                         dpr[i][j + 1]);
            }
        }

        // inserting character between position
        // i and i+1
        int ans = 0;
        for (int i = 0; i <= N; i++)
        {
            for (int j = 0; j < MAX; j++)
            {
                for (int x : pos[j])
                {
                    if (dpl[i][x - 1] +
                        dpr[i + 1][x + 1] == LCS)
                    {
                        ans++;
                        break;
                    }
                }
            }
        }
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String A = "aa", B = "baaa";
        int N = A.length(), M = B.length();
        System.out.println(numberofways(A, B, N, M));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python Program to Number of ways to insert a
# character to increase LCS by one

MAX = 256

def numberofways(A, B, N, M):
    pos = [[] for _ in range(MAX)]

    # Insert all positions of all characters
    # in string B
    for i in range(M):
        pos[ord(B[i])].append(i+1)

    # Longest Common Subsequence
    dpl = [[0] * (M+2) for _ in range(N+2)]
    for i in range(1, N+1):
        for j in range(1, M+1):
            if A[i - 1] == B[j - 1]:
                dpl[i][j] = dpl[i - 1][j - 1] + 1
            else:
                dpl[i][j] = max(dpl[i - 1][j],
                                dpl[i][j - 1])

    LCS = dpl[N][M]

    # Longest Common Subsequence from reverse
    dpr = [[0] * (M+2) for _ in range(N+2)]
    for i in range(N, 0, -1):
        for j in range(M, 0, -1):
            if A[i - 1] == B[j - 1]:
                dpr[i][j] = dpr[i + 1][j + 1] + 1
            else:
                dpr[i][j] = max(dpr[i + 1][j],
                                dpr[i][j + 1])

    # inserting character between position
    # i and i+1
    ans = 0
    for i in range(N+1):
        for j in range(MAX):
            for x in pos[j]:
                if dpl[i][x - 1] + dpr[i + 1][x + 1] == LCS:
                    ans += 1
                    break

    return ans

# Driver Code
if __name__ == "__main__":
    A = "aa"
    B = "baaa"
    N = len(A)
    M = len(B)
    print(numberofways(A, B, N, M))

# This code is contributed by vibhu4agarwal
```

## C#

```
// C# Program for Number of ways to insert a
// character to increase LCS by one
using System;
using System.Collections.Generic;

class GFG
{
    static readonly int MAX = 256;

    // Return the Number of ways to insert a
    // character to increase the longest
    // Common Subsequence by one
    static int numberofways(String A, String B,
                                  int N, int M)
    {
        List<int>[] pos = new List<int>[MAX];

        // Insert all positions of all characters
        // in string B.
        for (int i = 0; i < MAX; i++)
            pos[i] = new List<int>();

        for (int i = 0; i < M; i++)
            pos[B[i]].Add(i + 1);

        // longest Common Subsequence
        int[,] dpl = new int[N + 2, M + 2];
        for (int i = 1; i <= N; i++)
        {
            for (int j = 1; j <= M; j++)
            {
                if (A[i - 1] == B[j - 1])
                    dpl[i, j] = dpl[i - 1, j - 1] + 1;
                else
                    dpl[i, j] = Math.Max(dpl[i - 1, j],
                                         dpl[i, j - 1]);
            }
        }
        int LCS = dpl[N, M];

        // longest Common Subsequence from reverse
        int[,] dpr = new int[N + 2, M + 2];
        for (int i = N; i >= 1; i--)
        {
            for (int j = M; j >= 1; j--)
            {
                if (A[i - 1] == B[j - 1])
                    dpr[i, j] = dpr[i + 1, j + 1] + 1;
                else
                    dpr[i, j] = Math.Max(dpr[i + 1, j],
                                         dpr[i, j + 1]);
            }
        }

        // inserting character between position
        // i and i+1
        int ans = 0;
        for (int i = 0; i <= N; i++)
        {
            for (int j = 0; j < MAX; j++)
            {
                foreach (int x in pos[j])
                {
                    if (dpl[i, x - 1] +
                        dpr[i + 1, x + 1] == LCS)
                    {
                        ans++;
                        break;
                    }
                }
            }
        }
        return ans;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String A = "aa", B = "baaa";
        int N = A.Length, M = B.Length;
        Console.WriteLine(numberofways(A, B, N, M));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript Program for Number of ways to insert a
// character to increase LCS by one

let MAX = 256;

// Return the Number of ways to insert a
    // character to increase the Longest
    // Common Subsequence by one
function numberofways(A,B,N,M)
{
    let pos = new Array(MAX);

        // Insert all positions of all characters
        // in string B.
        for (let i = 0; i < MAX; i++)
            pos[i] =[];

        for (let i = 0; i < M; i++)
            pos[B[i].charCodeAt(0)].push(i + 1);

        // Longest Common Subsequence
        let dpl = new Array(N + 2);
        for(let i=0;i<N+2;i++)
           {
            dpl[i]=new Array(M+2);
            for(let j=0;j<M+2;j++)
                dpl[i][j]=0;
        }

        for (let i = 1; i <= N; i++)
        {
            for (let j = 1; j <= M; j++)
            {
                if (A[i - 1] == B[j - 1])
                    dpl[i][j] = dpl[i - 1][j - 1] + 1;
                else
                    dpl[i][j] = Math.max(dpl[i - 1][j],
                                         dpl[i][j - 1]);
            }
        }
        let LCS = dpl[N][M];

        // Longest Common Subsequence from reverse
        let dpr = new Array(N + 2);
        for(let i=0;i<N+2;i++)
        {
            dpr[i]=new Array(M+2);
            for(let j=0;j<M+2;j++)
                dpr[i][j]=0;
        }

        for (let i = N; i >= 1; i--)
        {
            for (let j = M; j >= 1; j--)
            {
                if (A[i - 1] == B[j - 1])
                    dpr[i][j] = dpr[i + 1][j + 1] + 1;
                else
                    dpr[i][j] = Math.max(dpr[i + 1][j],
                                         dpr[i][j + 1]);
            }
        }

        // inserting character between position
        // i and i+1
        let ans = 0;
        for (let i = 0; i <= N; i++)
        {
            for (let j = 0; j < MAX; j++)
            {
                for (let x=0;x< pos[j].length;x++)
                {
                    if (dpl[i][pos[j][x] - 1] +
                        dpr[i + 1][pos[j][x] + 1] == LCS)
                    {
                        ans++;
                        break;
                    }
                }
            }
        }
        return ans;
}

// Driver Code
let A = "aa", B = "baaa";
let N = A.length, M = B.length;
document.write(numberofways(A, B, N, M));

// This code is contributed by rag2127

</script>
```

**输出:**

```
4
```

**时间复杂度:** O(N x M)