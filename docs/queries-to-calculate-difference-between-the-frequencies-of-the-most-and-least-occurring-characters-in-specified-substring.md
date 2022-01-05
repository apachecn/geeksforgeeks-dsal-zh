# 查询计算指定子串中出现最多和最少字符的频率差

> 原文:[https://www . geeksforgeeks . org/查询-计算指定子串中出现最多和最少字符的频率差/](https://www.geeksforgeeks.org/queries-to-calculate-difference-between-the-frequencies-of-the-most-and-least-occurring-characters-in-specified-substring/)

给定一个由 **N** 个小写字符和一个数组 **Q[][]** 组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，表格的每一行 **{l，r}** 代表一个查询。对于每个查询，任务是找到子串 **{str[l]，…)中字符的最大频率和最小频率之间的差异。str[r]}** 。

***注:**考虑**1**——基于索引。*

**示例:**

> **输入:** N = 7，S =“abaac”，Q[][] = {{ 2，6 }，{ 1，7 }}
> **输出:**1 3
> T6】解释:
> 查询 1:‘a’在给定范围内出现次数最多即 3，‘b’在给定范围内出现次数最少即 2。因此，输出= 3–2 = 1。
> 查询 2:“a”在给定范围内出现的次数最多，即 4 次，“c”在给定范围内出现的次数最少，即 1 次。因此，输出= 4–1 = 3。
> 
> **输入:** N = 6，S =“aabbcc”，Q[][] = {{1，4}，{1，6}}
> **输出:**0 0
> T6】解释:
> 查询 1:“a”和“b”在给定范围内出现的次数相同。因此，输出为 0。
> 查询 2:所有“a”、“b”和“c”在给定范围内出现的次数相同。因此，输出为 0。

**天真法:**对于每个查询，找出给定范围内所有字符的[频率，取最大和最小频率之差。](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)

***时间复杂度:**O((N+26)* | Q |)*
T5**辅助空间:** O(26)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find difference between maximum and
// minimum frequency of a character in given range
void maxDiffFreq(vector<pair<int, int> > queries,
                 string S)
{

    // Stores length of string
    int N = S.size();

    // Stores count of queries
    int Q = queries.size();

    // Iterate over the characters
    // of the string
    for (int i = 0; i < Q; ++i) {

        // Stores l-value of a query
        int l = queries[i].first - 1;

        // Stores r-value of a query
        int r = queries[i].second - 1;
        int freq[26] = { 0 };

        // Store count of every character
        // laying in range [l, r]
        for (int j = l; j <= r; j++) {

            // Update frequency of
            // current character
            freq[S[j] - 'a']++;
        }

        // Stores maximum frequency
        // of characters in given range
        int mx = 0;

        // Stores minimum frequency
        // of characters in given range
        int mn = 99999999;

        // Iterate over all possible characters
        // of the given string
        for (int j = 0; j < 26; j++) {

            // Update mx
            mx = max(mx, freq[j]);

            // If (j + 'a') is present
            if (freq[j])
                mn = min(mn, freq[j]);
        }

        // difference between max and min
        cout << mx - mn << endl;
    }
}

// Driver Code
int main()
{

    // Given string
    string S = "abaabac";

    // Given queries
    vector<pair<int, int> > queries{ { 2, 6 }, { 1, 7 } };

    // Function Call
    maxDiffFreq(queries, S);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

  // Function to find difference between maximum and
  // minimum frequency of a character in given range
  static void maxDiffFreq(int [][]queries,
                          String S)
  {

    // Stores length of String
    int N = S.length();

    // Stores count of queries
    int Q = queries.length;

    // Iterate over the characters
    // of the String
    for (int i = 0; i < Q; ++i)    
    {

      // Stores l-value of a query
      int l = queries[i][0] - 1;

      // Stores r-value of a query
      int r = queries[i][1] - 1;
      int freq[] = new int[26];

      // Store count of every character
      // laying in range [l, r]
      for (int j = l; j <= r; j++) {

        // Update frequency of
        // current character
        freq[S.charAt(j) - 'a']++;
      }

      // Stores maximum frequency
      // of characters in given range
      int mx = 0;

      // Stores minimum frequency
      // of characters in given range
      int mn = 99999999;

      // Iterate over all possible characters
      // of the given String
      for (int j = 0; j < 26; j++) {

        // Update mx
        mx = Math.max(mx, freq[j]);

        // If (j + 'a') is present
        if (freq[j]>0)
          mn = Math.min(mn, freq[j]);
      }

      // difference between max and min
      System.out.print(mx - mn +"\n");
    }
  }

  // Driver Code
  public static void main(String[] args)
  {

    // Given String
    String S = "abaabac";

    // Given queries
    int [][]queries = { { 2, 6 }, { 1, 7 } };

    // Function Call
    maxDiffFreq(queries, S);
  }
}
// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find difference between maximum
# and minimum frequency of a character in
# given range
def maxDiffFreq(queries, S):

    # Stores length of string
    N = len(S)

    # Stores count of queries
    Q = len(queries)

    # Iterate over the characters
    # of the string
    for i in range(Q):

        # Stores l-value of a query
        l = queries[i][0] - 1

        # Stores r-value of a query
        r = queries[i][1] - 1
        freq = [0] * 26

        # Store count of every character
        # laying in range [l, r]
        for j in range(l, r + 1):

            # Update frequency of
            # current character
            freq[ord(S[j]) - ord('a')] += 1

        # Stores maximum frequency
        # of characters in given range
        mx = 0

        # Stores minimum frequency
        # of characters in given range
        mn = 99999999

        # Iterate over all possible characters
        # of the given string
        for j in range(26):

            # Update mx
            mx = max(mx, freq[j])

            # If (j + 'a') is present
            if (freq[j]):
                mn = min(mn, freq[j])

        # Difference between max and min
        print(mx - mn)

# Driver Code
if __name__ == "__main__":

    # Given string
    S = "abaabac"

    # Given queries
    queries = [ [ 2, 6 ], [ 1, 7 ] ]

    # Function Call
    maxDiffFreq(queries, S)

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to find difference between maximum and
    // minimum frequency of a character in given range
    static void maxDiffFreq(List<Tuple<int, int>> queries, string S)
    {

        // Stores length of string
        int N = S.Length;

        // Stores count of queries
        int Q = queries.Count;

        // Iterate over the characters
        // of the string
        for (int i = 0; i < Q; ++i)
        {

            // Stores l-value of a query
            int l = queries[i].Item1 - 1;

            // Stores r-value of a query
            int r = queries[i].Item2 - 1;
            int[] freq = new int[26];

            // Store count of every character
            // laying in range [l, r]
            for (int j = l; j <= r; j++)
            {

                // Update frequency of
                // current character
                freq[S[j] - 'a']++;
            }

            // Stores maximum frequency
            // of characters in given range
            int mx = 0;

            // Stores minimum frequency
            // of characters in given range
            int mn = 99999999;

            // Iterate over all possible characters
            // of the given string
            for (int j = 0; j < 26; j++)
            {

                // Update mx
                mx = Math.Max(mx, freq[j]);

                // If (j + 'a') is present
                if (freq[j] != 0)
                    mn = Math.Min(mn, freq[j]);
            }

            // difference between max and min
            Console.WriteLine(mx - mn);
        }
    }   

  // Driver code
  static void Main()
  {

    // Given string
    string S = "abaabac";

    // Given queries
    List<Tuple<int, int>> queries = new List<Tuple<int, int>>();
    queries.Add(new Tuple<int, int>(2, 6));
    queries.Add(new Tuple<int, int>(1, 7));

    // Function Call
    maxDiffFreq(queries, S);
  }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find difference between maximum and
// minimum frequency of a character in given range
function maxDiffFreq(queries, S)
{

    // Stores length of string
    let N = S.length;

    // Stores count of queries
    let Q = queries.length;

    // Iterate over the characters
    // of the string
    for(let i = 0; i < Q; ++i)
    {

        // Stores l-value of a query
        let l = queries[i][0] - 1;

        // Stores r-value of a query
        let r = queries[i][1] - 1;
        let freq = new Array(26).fill(0);

        // Store count of every character
        // laying in range [l, r]
        for(let j = l; j <= r; j++)
        {

            // Update frequency of
            // current character
            freq[S[j].charCodeAt(0) -
                  'a'.charCodeAt(0)]++;
        }

        // Stores maximum frequency
        // of characters in given range
        let mx = 0;

        // Stores minimum frequency
        // of characters in given range
        let mn = 99999999;

        // Iterate over all possible characters
        // of the given string
        for(let j = 0; j < 26; j++)
        {

            // Update mx
            mx = Math.max(mx, freq[j]);

            // If (j + 'a') is present
            if (freq[j])
                mn = Math.min(mn, freq[j]);
        }

        // Difference between max and min
        document.write(mx - mn + "<br>");
    }
}

// Driver Code

// Given string
let S = "abaabac";

// Given queries
let queries = [ [ 2, 6 ], [ 1, 7 ] ];

// Function Call
maxDiffFreq(queries, S);

// This code contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
1
3
```

**高效方法:**想法是使用[2D-芬威克树来存储每个角色的频率](https://www.geeksforgeeks.org/range-queries-for-frequencies-of-array-elements/)。按照以下步骤解决问题:

1.  创建一个二维的[分威克树](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)，存储从**‘a’**到**‘z’**的每个角色的信息。
2.  然后对于每个查询，使用[分威克树](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)计算给定范围内每个字符的频率。
3.  从上面找到的频率，得到最大和最小频率。
4.  打印最大和最小频率之间的差值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to update frequency of
// a character in Fenwick tree
void update(int BIT[26][10005], int idx,
            int i, int val)
{
    while (i < 10005) {

        // Update frequency of (idx + 'a')
        BIT[idx][i] += val;

        // Update i
        i = i + (i & (-i));
    }
}

// Function to find the frequency of
// a character (idx + 'a') in range [1, i]
int query(int BIT[26][10005], int idx, int i)
{

    // Stores frequency of character, (idx + 'a')
    // in range [1, i]
    int ans = 0;

    while (i > 0) {

        // Update ans
        ans += BIT[idx][i];

        // Update i
        i = i - (i & (-i));
    }
    return ans;
}

// Function to find difference between maximum and
// minimum frequency of a character in given range
void maxDiffFreq(string s, vector<pair<int, int> > queries)
{

    // BIT[i][j]: Stores frequency of (i + 'a')
    // If j is a power of 2, then it stores
    // the frequency (i + 'a') of  from [1, j]
    int BIT[26][10005];

    // Stores length of string
    int n = s.size();

    // Iterate over the characters
    // of the string
    for (int i = 0; i < n; i++) {

        // Update the frequency of
        // s[i] in fenwick tree
        update(BIT, s[i] - 'a', i + 1, 1);
    }

    // Stores count of queries
    int Q = queries.size();

    // Iterate over all the queries
    for (int i = 0; i < Q; ++i) {

        // Stores maximum frequency of
        // a character in range [l, r]
        int mx = 0;

        // Stores minimum frequency of
        // a character in range [l, r]

        int mn = INT_MAX;
        int l = queries[i].first;
        int r = queries[i].second;

        // Iterate over all possible characters
        for (int j = 0; j < 26; j++) {

            // Stores frequency of (j + 'a')
            // in range [1, r]
            int p = query(BIT, j, r);

            // Stores frequency of (j + 'a')
            // in range [1, l - 1]
            int q = query(BIT, j, l - 1);

            // Update mx
            mx = max(mx, p - q);

            // If a character (i + 'a') present
            // in range [l, r]
            if (p > 0) {

                // Update mn
                mn = min(mn, p - q);
            }
        }

        // Print the difference between
        // max and min freq
        cout << mx - mn << endl;
    }
}

// Driver Code
int main()
{

    // Given string
    string S = "abaabac";

    // Given queries
    vector<pair<int, int> > queries
        = { { 2, 6 }, { 1, 7 } };

    // Function Call
    maxDiffFreq(S, queries);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

// Function to update frequency of
// a character in Fenwick tree
static void update(int BIT[][], int idx,
            int i, int val)
{
    while (i < 10005)
    {

        // Update frequency of (idx + 'a')
        BIT[idx][i] += val;

        // Update i
        i = i + (i & (-i));
    }
}

// Function to find the frequency of
// a character (idx + 'a') in range [1, i]
static int query(int BIT[][], int idx, int i)
{

    // Stores frequency of character, (idx + 'a')
    // in range [1, i]
    int ans = 0;

    while (i > 0) {

        // Update ans
        ans += BIT[idx][i];

        // Update i
        i = i - (i & (-i));
    }
    return ans;
}

// Function to find difference between maximum and
// minimum frequency of a character in given range
static void maxDiffFreq(String s, int [][]queries)
{

    // BIT[i][j]: Stores frequency of (i + 'a')
    // If j is a power of 2, then it stores
    // the frequency (i + 'a') of  from [1, j]
    int[][] BIT = new int[26][10005];

    // Stores length of String
    int n = s.length();

    // Iterate over the characters
    // of the String
    for (int i = 0; i < n; i++) {

        // Update the frequency of
        // s[i] in fenwick tree
        update(BIT, s.charAt(i) - 'a', i + 1, 1);
    }

    // Stores count of queries
    int Q = queries.length;

    // Iterate over all the queries
    for (int i = 0; i < Q; ++i) {

        // Stores maximum frequency of
        // a character in range [l, r]
        int mx = 0;

        // Stores minimum frequency of
        // a character in range [l, r]

        int mn = Integer.MAX_VALUE;
        int l = queries[i][0];
        int r = queries[i][1];

        // Iterate over all possible characters
        for (int j = 0; j < 26; j++) {

            // Stores frequency of (j + 'a')
            // in range [1, r]
            int p = query(BIT, j, r);

            // Stores frequency of (j + 'a')
            // in range [1, l - 1]
            int q = query(BIT, j, l - 1);

            // Update mx
            mx = Math.max(mx, p - q);

            // If a character (i + 'a') present
            // in range [l, r]
            if (p > 0) {

                // Update mn
                mn = Math.min(mn, p - q);
            }
        }

        // Print the difference between
        // max and min freq
        System.out.print(mx - mn +"\n");
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given String
    String S = "abaabac";

    // Given queries
    int [][]queries
        = { { 2, 6 }, { 1, 7 } };

    // Function Call
    maxDiffFreq(S, queries);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to update frequency of
# a character in Fenwick tree
def update(BIT, idx, i, val) :
    while (i < 10005) :

      # Update frequency of (idx + 'a')
      BIT[idx][i] += val

      # Update i
      i = i + (i & (-i))

# Function to find the frequency of
# a character (idx + 'a') in range [1, i]
def query(BIT, idx, i) :

    # Stores frequency of character, (idx + 'a')
    # in range [1, i]
    ans = 0
    while (i > 0) :

      # Update ans
      ans += BIT[idx][i]

      # Update i
      i = i - (i & (-i))

    return ans

# Function to find difference between maximum and
# minimum frequency of a character in given range
def maxDiffFreq(s, queries) :

    # BIT[i][j]: Stores frequency of (i + 'a')
    # If j is a power of 2, then it stores
    # the frequency (i + 'a') of  from [1][j]
    BIT = [[0 for i in range(10005)] for j in range(26)]

    # Stores length of String
    n = len(s)

    # Iterate over the characters
    # of the String
    for i in range(n) :

      # Update the frequency of
      # s[i] in fenwick tree
      update(BIT, ord(s[i]) - ord('a'), i + 1, 1)

    # Stores count of queries
    Q = len(queries)

    # Iterate over all the queries
    for i in range(Q) :

      # Stores maximum frequency of
      # a character in range [l, r]
      mx = 0

      # Stores minimum frequency of
      # a character in range [l, r]
      mn = sys.maxsize
      l = queries[i][0]
      r = queries[i][1]

      # Iterate over all possible characters
      for j in range(26) :

        # Stores frequency of (j + 'a')
        # in range [1, r]
        p = query(BIT, j, r)

        # Stores frequency of (j + 'a')
        # in range [1, l - 1]
        q = query(BIT, j, l - 1)

        # Update mx
        mx = max(mx, p - q)

        # If a character (i + 'a') present
        # in range [l, r]
        if (p > 0) :

          # Update mn
          mn = min(mn, p - q)

      # Print the difference between
      # max and min freq
      print(mx - mn)

# Given String
S = "abaabac"

# Given queries
queries = [ [ 2, 6 ], [ 1, 7 ] ]

# Function Call
maxDiffFreq(S, queries)

# This code is contributed by divyesh072019.
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

  // Function to update frequency of
  // a character in Fenwick tree
  static void update(int [,]BIT, int idx,
                     int i, int val)
  {
    while (i < 10005)
    {

      // Update frequency of (idx + 'a')
      BIT[idx,i] += val;

      // Update i
      i = i + (i & (-i));
    }
  }

  // Function to find the frequency of
  // a character (idx + 'a') in range [1, i]
  static int query(int [,]BIT, int idx, int i)
  {

    // Stores frequency of character, (idx + 'a')
    // in range [1, i]
    int ans = 0;
    while (i > 0)
    {

      // Update ans
      ans += BIT[idx,i];

      // Update i
      i = i - (i & (-i));
    }
    return ans;
  }

  // Function to find difference between maximum and
  // minimum frequency of a character in given range
  static void maxDiffFreq(String s, int [,]queries)
  {

    // BIT[i,j]: Stores frequency of (i + 'a')
    // If j is a power of 2, then it stores
    // the frequency (i + 'a') of  from [1, j]
    int[,] BIT = new int[26, 10005];

    // Stores length of String
    int n = s.Length;

    // Iterate over the characters
    // of the String
    for (int i = 0; i < n; i++)
    {

      // Update the frequency of
      // s[i] in fenwick tree
      update(BIT, s[i] - 'a', i + 1, 1);
    }

    // Stores count of queries
    int Q = queries.GetLength(0);

    // Iterate over all the queries
    for (int i = 0; i < Q; ++i)
    {

      // Stores maximum frequency of
      // a character in range [l, r]
      int mx = 0;

      // Stores minimum frequency of
      // a character in range [l, r]
      int mn = int.MaxValue;
      int l = queries[i, 0];
      int r = queries[i, 1];

      // Iterate over all possible characters
      for (int j = 0; j < 26; j++)
      {

        // Stores frequency of (j + 'a')
        // in range [1, r]
        int p = query(BIT, j, r);

        // Stores frequency of (j + 'a')
        // in range [1, l - 1]
        int q = query(BIT, j, l - 1);

        // Update mx
        mx = Math.Max(mx, p - q);

        // If a character (i + 'a') present
        // in range [l, r]
        if (p > 0)
        {

          // Update mn
          mn = Math.Min(mn, p - q);
        }
      }

      // Print the difference between
      // max and min freq
      Console.Write(mx - mn +"\n");
    }
  }

  // Driver Code
  public static void Main(String[] args)
  {

    // Given String
    String S = "abaabac";

    // Given queries
    int [,]queries
      = { { 2, 6 }, { 1, 7 } };

    // Function Call
    maxDiffFreq(S, queries);
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to update frequency of
// a character in Fenwick tree
function update(BIT, idx, i, val)
{
    while (i < 10005)
    {

        // Update frequency of (idx + 'a')
        BIT[idx][i] += val;

        // Update i
        i = i + (i & (-i));
    }
}

// Function to find the frequency of
// a character (idx + 'a') in range [1, i]
function query(BIT, idx, i)
{

    // Stores frequency of character, (idx + 'a')
    // in range [1, i]
    let ans = 0;

    while (i > 0)
    {

        // Update ans
        ans += BIT[idx][i];

        // Update i
        i = i - (i & (-i));
    }
    return ans;
}

// Function to find difference between maximum and
// minimum frequency of a character in given range
function maxDiffFreq(s, queries)
{

    // BIT[i][j]: Stores frequency of (i + 'a')
    // If j is a power of 2, then it stores
    // the frequency (i + 'a') of  from [1, j]
    let BIT = new Array(26);
    for(let i = 0; i < 26; i++)
    {
        BIT[i] = new Array(10005);
        for(let j = 0; j < 10005; j++)
        {
            BIT[i][j] = 0;
        }
    }

    // Stores length of String
    let n = s.length;

    // Iterate over the characters
    // of the String
    for(let i = 0; i < n; i++)
    {

        // Update the frequency of
        // s[i] in fenwick tree
        update(BIT, s[i].charCodeAt(0) -
                     'a'.charCodeAt(0),
                     i + 1, 1);
    }

    // Stores count of queries
    let Q = queries.length;

    // Iterate over all the queries
    for(let i = 0; i < Q; ++i)
    {

        // Stores maximum frequency of
        // a character in range [l, r]
        let mx = 0;

        // Stores minimum frequency of
        // a character in range [l, r]
        let mn = Number.MAX_VALUE;
        let l = queries[i][0];
        let r = queries[i][1];

        // Iterate over all possible characters
        for(let j = 0; j < 26; j++)
        {

            // Stores frequency of (j + 'a')
            // in range [1, r]
            let p = query(BIT, j, r);

            // Stores frequency of (j + 'a')
            // in range [1, l - 1]
            let q = query(BIT, j, l - 1);

            // Update mx
            mx = Math.max(mx, p - q);

            // If a character (i + 'a') present
            // in range [l, r]
            if (p > 0)
            {

                // Update mn
                mn = Math.min(mn, p - q);
            }
        }

        // Print the difference between
        // max and min freq
        document.write(mx - mn + "<br>");
    }
}

// Driver Code
let S = "abaabac";

// Given queries
let queries = [ [ 2, 6 ], [ 1, 7 ] ];

// Function Call
maxDiffFreq(S, queries);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
1
3
```

***时间复杂度:**O(| Q | * log(N)* 26)*
***辅助空间:** O(N * 26)*