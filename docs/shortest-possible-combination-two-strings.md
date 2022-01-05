# 两个字符串的最短可能组合

> 原文:[https://www . geesforgeks . org/最短可能组合-两个字符串/](https://www.geeksforgeeks.org/shortest-possible-combination-two-strings/)

计算两个给定字符串组合的最短字符串，使新字符串由两个字符串组成其[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)。
**例:**

```
Input : a = "pear"
        b = "peach"
Output : pearch
pearch is the shorted string such that both
pear and peach are its subsequences.

Input  : a = "geek"
         b = "code"
Output : gecodek
```

我们在下面的文章中讨论了一个寻找最短超序列长度的解决方案。
[【最短公共超序列】](https://www.geeksforgeeks.org/shortest-common-supersequence/)
本文讨论超序列的打印。该解决方案基于以下递归方法，作为替代方法，该方法在上文[文章](https://www.geeksforgeeks.org/shortest-common-supersequence/)中讨论。

```
Let a[0..m-1] and b[0..n-1] be two strings and m and
be respective lengths.

  if (m == 0) return n;
  if (n == 0) return m;

  // If last characters are same, then add 1 to
  // result and recur for a[]
  if (a[m-1] == b[n-1]) 
     return 1 + SCS(a, b, m-1, n-1);

  // Else find shortest of following two
  //  a) Remove last character from X and recur
  //  b) Remove last character from Y and recur
  else return 1 + min( SCS(a, b, m-1, n), 
                       SCS(a, b, m, n-1) );
```

我们构建一个 DP 数组来存储长度。建立 DP 数组后，我们从最右下方的位置遍历。打印的方式类似于[打印 LCS](https://www.geeksforgeeks.org/printing-longest-common-subsequence/) 。

## C++

```
/* C++ program to print supersequence of two
   strings */
#include<bits/stdc++.h>
using namespace std;

/* Prints super sequence of a[0..m-1] and b[0..n-1] */
void printSuperSeq(string &a, string &b)
{
    int m = a.length(), n = b.length();
    int dp[m+1][n+1];

    // Fill table in bottom up manner
    for (int i = 0; i <= m; i++)
    {
        for (int j = 0; j <= n; j++)
        {
           // Below steps follow above recurrence
           if (!i)
               dp[i][j] = j;
           else if (!j)
               dp[i][j] = i;
           else if (a[i-1] == b[j-1])
                dp[i][j] = 1 + dp[i-1][j-1];
           else
                dp[i][j] = 1 + min(dp[i-1][j], dp[i][j-1]);
        }
    }

   // Following code is used to print supersequence
   int index = dp[m][n];

   // Create a string of size index+1 to store the result
   string res(index+1, '\0');

   // Start from the right-most-bottom-most corner and
   // one by one store characters in res[]
   int i = m, j = n;
   while (i > 0 && j > 0)
   {
      // If current character in a[] and b are same,
      // then current character is part of LCS
      if (a[i-1] == b[j-1])
      {
          // Put current character in result
          res[index-1] = a[i-1];

          // reduce values of i, j and indexs
          i--; j--; index--;
      }

      // If not same, then find the smaller of two and
      // go in the direction of smaller value
      else if (dp[i-1][j] < dp[i][j-1])
      { res[index-1] = a[i-1];   i--;  index--; }
      else
      { res[index-1] = b[j-1];  j--; index--; }
   }

   // Copy remaining characters of string 'a'
   while (i > 0)
   {
       res[index-1] = a[i-1];   i--;  index--;
   }

   // Copy remaining characters of string 'b'
   while (j > 0)
   {
       res[index-1] = b[j-1];  j--; index--;
   }

   // Print the result
   cout << res;
}

/* Driver program to test above function */
int main()
{
  string a = "algorithm", b = "rhythm";
  printSuperSeq(a, b);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print supersequence of two
// strings
public class GFG_1 {

    String a , b;

    // Prints super sequence of a[0..m-1] and b[0..n-1]
    static void printSuperSeq(String a, String b)
    {
        int m = a.length(), n = b.length();
        int[][] dp = new int[m+1][n+1];

        // Fill table in bottom up manner
        for (int i = 0; i <= m; i++)
        {
            for (int j = 0; j <= n; j++)
            {
               // Below steps follow above recurrence
               if (i == 0)
                   dp[i][j] = j;
               else if (j == 0 )
                   dp[i][j] = i;
               else if (a.charAt(i-1) == b.charAt(j-1))
                    dp[i][j] = 1 + dp[i-1][j-1];
               else
                    dp[i][j] = 1 + Math.min(dp[i-1][j], dp[i][j-1]);
            }
        }

       // Create a string of size index+1 to store the result
       String res = "";

       // Start from the right-most-bottom-most corner and
       // one by one store characters in res[]
       int i = m, j = n;
       while (i > 0 && j > 0)
       {
          // If current character in a[] and b are same,
          // then current character is part of LCS
          if (a.charAt(i-1) == b.charAt(j-1))
          {
              // Put current character in result
              res = a.charAt(i-1) + res;

              // reduce values of i, j and indexs
              i--;
              j--;
          }

          // If not same, then find the larger of two and
          // go in the direction of larger value
          else if (dp[i-1][j] < dp[i][j-1])
          {
              res = a.charAt(i-1) + res;
              i--; 
          }
          else
          {
              res = b.charAt(j-1) + res;
              j--;
          }
       }

       // Copy remaining characters of string 'a'
       while (i > 0)
       {
           res = a.charAt(i-1) + res;
           i--;
       }

       // Copy remaining characters of string 'b'
       while (j > 0)
       {
           res = b.charAt(j-1) + res;  
           j--;
       }

       // Print the result
       System.out.println(res);
    }

    /* Driver program to test above function */
    public static void main(String args[])
    {
      String a = "algorithm";
      String b = "rhythm";
      printSuperSeq(a, b);

    }
}
// This article is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 program to print supersequence of two strings

# Prints super sequence of a[0..m-1] and b[0..n-1]
def printSuperSeq(a, b):
    m = len(a)
    n = len(b)
    dp = [[0] * (n + 1) for i in range(m + 1)]

    # Fill table in bottom up manner
    for i in range(0, m + 1):
        for j in range(0, n + 1):

            # Below steps follow above recurrence
            if not i:
                dp[i][j] = j;
            elif not j:
                dp[i][j] = i;
            elif (a[i - 1] == b[j - 1]):
                dp[i][j] = 1 + dp[i - 1][j - 1];
            else:
                dp[i][j] = 1 + min(dp[i - 1][j],
                                   dp[i][j - 1]);

    # Following code is used to print supersequence
    index = dp[m][n];

    # Create a string of size index+1
    # to store the result
    res = [""] * (index)

    # Start from the right-most-bottom-most corner
    # and one by one store characters in res[]
    i = m
    j = n;
    while (i > 0 and j > 0):

        # If current character in a[] and b are same,
        # then current character is part of LCS
        if (a[i - 1] == b[j - 1]):

            # Put current character in result
            res[index - 1] = a[i - 1];

            # reduce values of i, j and indexs
            i -= 1
            j -= 1
            index -= 1

        # If not same, then find the larger of two and
        # go in the direction of larger value
        elif (dp[i - 1][j] < dp[i][j - 1]):
            res[index - 1] = a[i - 1]
            i -= 1
            index -= 1

        else:
            res[index - 1] = b[j - 1]
            j -= 1
            index -= 1

    # Copy remaining characters of string 'a'
    while (i > 0):
        res[index - 1] = a[i - 1]
        i -= 1
        index -= 1

    # Copy remaining characters of string 'b'
    while (j > 0):
        res[index - 1] = b[j - 1]
        j -= 1
        index -= 1

    # Print the result
    print("".join(res))

# Driver Code
if __name__ == '__main__':
    a = "algorithm"
    b = "rhythm"
    printSuperSeq(a, b)

# This code is contributed by ashutosh450
```

## C#

```
// C# program to print supersequence of two
// strings
using System;
public class GFG_1 {

    // Prints super sequence of a[0..m-1] and b[0..n-1]
    static void printSuperSeq(string a, string b)
    {
        int m = a.Length, n = b.Length;
        int[,] dp = new int[m+1,n+1];

        // Fill table in bottom up manner
        for (int i = 0; i <= m; i++)
        {
            for (int j = 0; j <= n; j++)
            {
               // Below steps follow above recurrence
               if (i == 0)
                   dp[i,j] = j;
               else if (j == 0 )
                   dp[i,j] = i;
               else if (a[i-1] == b[j-1])
                    dp[i,j] = 1 + dp[i-1,j-1];
               else
                    dp[i,j] = 1 + Math.Min(dp[i-1,j], dp[i,j-1]);
            }
        }

       // Create a string of size index+1 to store the result
       string res = "";

       // Start from the right-most-bottom-most corner and
       // one by one store characters in res[]
       int k = m, l = n;
       while (k > 0 && l > 0)
       {
          // If current character in a[] and b are same,
          // then current character is part of LCS
          if (a[k-1] == b[l-1])
          {
              // Put current character in result
              res = a[k-1] + res;

              // reduce values of i, j and indexs
              k--;
              l--;
          }

          // If not same, then find the larger of two and
          // go in the direction of larger value
          else if (dp[k-1,l] < dp[k,l-1])
          {
              res = a[k-1] + res;
              k--; 
          }
          else
          {
              res = b[l-1] + res;
              l--;
          }
       }

       // Copy remaining characters of string 'a'
       while (k > 0)
       {
           res = a[k-1] + res;
           k--;
       }

       // Copy remaining characters of string 'b'
       while (l > 0)
       {
           res = b[l-1] + res;  
           l--;
       }

       // Print the result
       Console.WriteLine(res);
    }

    /* Driver program to test above function */
    public static void Main()
    {
      string a = "algorithm";
      string b = "rhythm";
      printSuperSeq(a, b);

    }
}
// This article is contributed by Ita_c.
```

## java 描述语言

```
<script>
// Javascript program to print supersequence of two
// strings

 // Prints super sequence of a[0..m-1] and b[0..n-1]
function printSuperSeq(a,b)
{
    let m = a.length, n = b.length;
        let dp = new Array(m+1);
        for(let i=0;i<m+1;i++)
            dp[i]=new Array(n+1);

        // Fill table in bottom up manner
        for (let i = 0; i <= m; i++)
        {
            for (let j = 0; j <= n; j++)
            {
               // Below steps follow above recurrence
               if (i == 0)
                   dp[i][j] = j;
               else if (j == 0 )
                   dp[i][j] = i;
               else if (a[i-1] == b[j-1])
                    dp[i][j] = 1 + dp[i-1][j-1];
               else
                    dp[i][j] = 1 + Math.min(dp[i-1][j], dp[i][j-1]);
            }
        }

       // Create a string of size index+1 to store the result
       let res = "";

       // Start from the right-most-bottom-most corner and
       // one by one store characters in res[]
       let i = m, j = n;
       while (i > 0 && j > 0)
       {
          // If current character in a[] and b are same,
          // then current character is part of LCS
          if (a[i-1] == b[j-1])
          {
              // Put current character in result
              res = a[i-1] + res;

              // reduce values of i, j and indexs
              i--;
              j--;
          }

          // If not same, then find the larger of two and
          // go in the direction of larger value
          else if (dp[i-1][j] < dp[i][j-1])
          {
              res = a[i-1] + res;
              i--;
          }
          else
          {
              res = b[j-1] + res;
              j--;
          }
       }

       // Copy remaining characters of string 'a'
       while (i > 0)
       {
           res = a[i-1] + res;
           i--;
       }

       // Copy remaining characters of string 'b'
       while (j > 0)
       {
           res = b[j-1] + res; 
           j--;
       }

       // Print the result
       document.write(res);
}

/* Driver program to test above function */
let a = "algorithm";
let b = "rhythm";
printSuperSeq(a, b);

// This code is contributed by ab2127
</script>
```

**输出:**

```
algorihythm
```

**基于 LCS 的解决方案:**
我们使用 LCS 解决方案构建 2D 阵列。如果两个指针位置的字符相等，我们将长度增加 1，否则我们存储相邻位置的最大值。最后，我们回溯矩阵以找到索引向量遍历，这将产生最短的可能组合。

## C++

```
// C++ implementation to find shortest string for
// a combination of two strings
#include <bits/stdc++.h>
using namespace std;

// Vector that store the index of string a and b
vector<int> index_a;
vector<int> index_b;

// Subroutine to Backtrack the dp matrix to
// find the index vector traversing which would
// yield the shortest possible combination
void index(int dp[][100], string a, string b,
           int size_a, int size_b)
{
    // Clear the index vectors
    index_a.clear();
    index_b.clear();

    // Return if either of a or b is reduced
    // to 0
    if (size_a == 0 || size_b == 0)
        return;

    // Push both to index_a and index_b with
    // the respective a and b index
    if (a[size_a - 1] == b[size_b - 1]) {
        index(dp, a, b, size_a - 1, size_b - 1);
        index_a.push_back(size_a - 1);
        index_b.push_back(size_b - 1);
    } else {
        if (dp[size_a - 1][size_b] > dp[size_a]
                                    [size_b - 1]) {
            index(dp, a, b, size_a - 1, size_b);
        } else {
            index(dp, a, b, size_a, size_b - 1);
        }
    }
}

// function to combine the strings to form
// the shortest string
void combine(string a, string b, int size_a,
             int size_b)
{

    int dp[100][100];
    string ans = "";
    int k = 0;

    // Initialize the matrix to 0
    memset(dp, 0, sizeof(dp));

    // Store the increment of diagonally
    // previous value if a[i-1] and b[j-1] are
    // equal, else store the max of dp[i][j-1]
    // and dp[i-1][j]
    for (int i = 1; i <= size_a; i++) {
        for (int j = 1; j <= size_b; j++) {
            if (a[i - 1] == b[j - 1]) {
                dp[i][j] = dp[i - 1][j - 1] + 1;
            } else {
                dp[i][j] = max(dp[i][j - 1],
                               dp[i - 1][j]);
            }
        }
    }

    // Get the Lowest Common Subsequence
    int lcs = dp[size_a][size_b];

    // Backtrack the dp array to get the index
    // vectors of two strings, used to find
    // the shortest possible combination.
    index(dp, a, b, size_a, size_b);

    int i, j = i = k;

    // Build the string combination using the
    // index found by backtracking
    while (k < lcs) {
        while (i < size_a && i < index_a[k]) {
            ans += a[i++];
        }

        while (j < size_b && j < index_b[k]) {
            ans += b[j++];
        }

        ans = ans + a[index_a[k]];
        k++;
        i++;
        j++;
    }

    // Append the remaining characters in a
    // to answer
    while (i < size_a) {
        ans += a[i++];
    }

    // Append the remaining characters in b
    // to answer
    while (j < size_b) {
        ans += b[j++];
    }

    cout << ans;
}

// Driver code
int main()
{
    string a = "algorithm";
    string b = "rhythm";

    // Store the length of string
    int size_a = a.size();
    int size_b = b.size();

    combine(a, b, size_a, size_b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find shortest string for
// a combination of two strings
import java.util.ArrayList;
public class GFG_2 {

    // Vector that store the index of string a and b
    static ArrayList<Integer> index_a = new ArrayList<>();
    static ArrayList<Integer> index_b = new ArrayList<>();

    // Subroutine to Backtrack the dp matrix to
    // find the index vector traversing which would
    // yield the shortest possible combination
    static void index(int dp[][], String a, String b,
               int size_a, int size_b)
    {
        // Clear the index vectors
        index_a.clear();
        index_b.clear();

        // Return if either of a or b is reduced
        // to 0
        if (size_a == 0 || size_b == 0)
            return;

        // Push both to index_a and index_b with
        // the respective a and b index
        if (a.charAt(size_a - 1) == b.charAt(size_b - 1)) {
            index(dp, a, b, size_a - 1, size_b - 1);
            index_a.add(size_a - 1);
            index_b.add(size_b - 1);
        } else {
            if (dp[size_a - 1][size_b] > dp[size_a]
                                        [size_b - 1]) {
                index(dp, a, b, size_a - 1, size_b);
            } else {
                index(dp, a, b, size_a, size_b - 1);
            }
        }
    }

    // function to combine the strings to form
    // the shortest string
    static void combine(String a, String b, int size_a,
                 int size_b)
    {

        int[][] dp = new int[100][100];
        String ans = "";
        int k = 0;

        // Store the increment of diagonally
        // previous value if a[i-1] and b[j-1] are
        // equal, else store the max of dp[i][j-1]
        // and dp[i-1][j]
        for (int i = 1; i <= size_a; i++) {
            for (int j = 1; j <= size_b; j++) {
                if (a.charAt(i - 1) == b.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                } else {
                    dp[i][j] = Math.max(dp[i][j - 1],
                                   dp[i - 1][j]);
                }
            }
        }

        // Get the Lowest Common Subsequence
        int lcs = dp[size_a][size_b];

        // Backtrack the dp array to get the index
        // vectors of two strings, used to find
        // the shortest possible combination.
        index(dp, a, b, size_a, size_b);

        int i, j = i = k;

        // Build the string combination using the
        // index found by backtracking
        while (k < lcs) {
            while (i < size_a && i < index_a.get(k)) {
                ans += a.charAt(i++);
            }

            while (j < size_b && j < index_b.get(k)) {
                ans += b.charAt(j++);
            }

            ans = ans + a.charAt(index_a.get(k));
            k++;
            i++;
            j++;
        }

        // Append the remaining characters in a
        // to answer
        while (i < size_a) {
            ans += a.charAt(i++);
        }

        // Append the remaining characters in b
        // to answer
        while (j < size_b) {
            ans +=  b.charAt(j++);
        }

        System.out.println(ans);
    }

    /* Driver program to test above function */
    public static void main(String args[])
    {
      String a = "algorithm";
      String b = "rhythm";
      combine(a, b, a.length(),b.length());

    }
}
// This article is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python implementation to find shortest string for
# a combination of two strings
index_a = []
index_b = []

def index(dp, a, b, size_a, size_b):
    if (size_a == 0 or size_b == 0):
        return
    if (a[size_a - 1] == b[size_b - 1]):
        index(dp, a, b, size_a - 1, size_b - 1)
        index_a.append(size_a - 1)
        index_b.append(size_b - 1)
    else:
        if(dp[size_a - 1][size_b] > dp[size_a][size_b - 1]):
            index(dp, a, b, size_a - 1, size_b)
        else:
            index(dp, a, b, size_a, size_b - 1)

def combine(a, b, size_a, size_b):
    dp = [[0 for i in range(100)] for j in range(100)]
    ans = ""
    k = 0

    for i in range(1, size_a + 1):
        for j in range(1, size_b + 1):
            if(a[i - 1] == b[j - 1]):
                dp[i][j] = dp[i - 1][j - 1] + 1
            else:
                dp[i][j] = max(dp[i][j - 1], dp[i - 1][j])

    lcs = dp[size_a][size_b]
    index(dp, a, b, size_a, size_b)
    j = i = k
    while (k < lcs):
        while (i < size_a and i < index_a[k]):
            ans += a[i];
            i += 1
        while (j < size_b and j < index_b[k]):
            ans += b[j]
            j += 1
        ans = ans + a[index_a[k]]
        k += 1
        i += 1
        j += 1

    while (i < size_a):
        ans += a[i]
        i += 1
    while (j < size_b):
        ans += b[j]
        j += 1
    print(ans)

# Driver code
a = "algorithm"
b = "rhythm"
size_a = len(a)
size_b = len(b)
combine(a, b, size_a, size_b)

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# implementation to find shortest string for
// a combination of two strings
using System;
using System.Collections.Generic;

class GFG
{

    // Vector that store the index of string a and b
    static List<int> index_a = new List<int>();
    static List<int> index_b = new List<int>();

    // Subroutine to Backtrack the dp matrix to
    // find the index vector traversing which would
    // yield the shortest possible combination
    static void index(int [,]dp, String a, String b,
                      int size_a, int size_b)
    {
        // Clear the index vectors
        index_a.Clear();
        index_b.Clear();

        // Return if either of a or b is reduced
        // to 0
        if (size_a == 0 || size_b == 0)
            return;

        // Push both to index_a and index_b with
        // the respective a and b index
        if (a[size_a - 1] == b[size_b - 1])
        {
            index(dp, a, b, size_a - 1, size_b - 1);
            index_a.Add(size_a - 1);
            index_b.Add(size_b - 1);
        }

        else
        {
            if (dp[size_a - 1,size_b] > dp[size_a,
                                           size_b - 1])
            {
                index(dp, a, b, size_a - 1, size_b);
            }
            else
            {
                index(dp, a, b, size_a, size_b - 1);
            }
        }
    }

    // function to combine the strings to form
    // the shortest string
    static void combine(String a, String b,
                        int size_a,int size_b)
    {
        int[,] dp = new int[100, 100];
        String ans = "";
        int k = 0, i, j;

        // Store the increment of diagonally
        // previous value if a[i-1] and b[j-1] are
        // equal, else store the max of dp[i,j-1]
        // and dp[i-1,j]
        for (i = 1; i <= size_a; i++)
        {
            for (j = 1; j <= size_b; j++)
            {
                if (a[i-1] == b[j - 1])
                {
                    dp[i, j] = dp[i - 1, j - 1] + 1;
                }
                else
                {
                    dp[i, j] = Math.Max(dp[i, j - 1],
                                        dp[i - 1, j]);
                }
            }
        }

        // Get the Lowest Common Subsequence
        int lcs = dp[size_a, size_b];

        // Backtrack the dp array to get the index
        // vectors of two strings, used to find
        // the shortest possible combination.
        index(dp, a, b, size_a, size_b);

        i = j = k;

        // Build the string combination using the
        // index found by backtracking
        while (k < lcs)
        {
            while (i < size_a && i < index_a[k])
            {
                ans += a[i++];
            }

            while (j < size_b && j < index_b[k])
            {
                ans += b[j++];
            }

            ans = ans + a[index_a[k]];
            k++;
            i++;
            j++;
        }

        // Append the remaining characters in a
        // to answer
        while (i < size_a)
        {
            ans += a[i++];
        }

        // Append the remaining characters in b
        // to answer
        while (j < size_b)
        {
            ans += b[j++];
        }

        Console.WriteLine(ans);
    }

    // Driver Code
    public static void Main(String []args)
    {
        String a = "algorithm";
        String b = "rhythm";
        combine(a, b, a.Length,b.Length);
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript implementation to find shortest string for
// a combination of two strings

// Vector that store the index of string a and b
let index_a =[];
let index_b = [];

// Subroutine to Backtrack the dp matrix to
// find the index vector traversing which would
// yield the shortest possible combination
function index(dp,a,b,size_a,size_b)
{
     // Clear the index vectors
        index_a=[];
        index_b=[];

        // Return if either of a or b is reduced
        // to 0
        if (size_a == 0 || size_b == 0)
            return;

        // Push both to index_a and index_b with
        // the respective a and b index
        if (a[size_a - 1] == b[size_b - 1]) {
            index(dp, a, b, size_a - 1, size_b - 1);
            index_a.push(size_a - 1);
            index_b.push(size_b - 1);
        } else {
            if (dp[size_a - 1][size_b] > dp[size_a]
                                        [size_b - 1]) {
                index(dp, a, b, size_a - 1, size_b);
            } else {
                index(dp, a, b, size_a, size_b - 1);
            }
        }
}

// function to combine the strings to form
// the shortest string
function combine(a,b,size_a,size_b)
{
    let dp = new Array(100);
    for(let i=0;i<100;i++)
    {
        dp[i]=new Array(100);
        for(let j=0;j<100;j++)
        {
            dp[i][j]=0;
        }

    }
        let ans = "";
        let k = 0;

        // Store the increment of diagonally
        // previous value if a[i-1] and b[j-1] are
        // equal, else store the max of dp[i][j-1]
        // and dp[i-1][j]
        for (let i = 1; i <= size_a; i++) {
            for (let j = 1; j <= size_b; j++) {
                if (a[i - 1] == b[j - 1]) {
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                } else {
                    dp[i][j] = Math.max(dp[i][j - 1],
                                   dp[i - 1][j]);
                }
            }
        }

        // Get the Lowest Common Subsequence
        let lcs = dp[size_a][size_b];

        // Backtrack the dp array to get the index
        // vectors of two strings, used to find
        // the shortest possible combination.
        index(dp, a, b, size_a, size_b);

        let i, j = i = k;

        // Build the string combination using the
        // index found by backtracking
        while (k < lcs) {
            while (i < size_a && i < index_a[k]) {
                ans += a[i++];
            }

            while (j < size_b && j < index_b[k]) {
                ans += b[j++];
            }

            ans = ans + a[index_a[k]];
            k++;
            i++;
            j++;
        }

        // Append the remaining characters in a
        // to answer
        while (i < size_a) {
            ans += a[i++];
        }

        // Append the remaining characters in b
        // to answer
        while (j < size_b) {
            ans +=  b[j++];
        }

        document.write(ans+"<br>");
}

/* Driver program to test above function */
let a = "algorithm";
let b = "rhythm";

combine(a, b, a.length,b.length);

// This code is contributed by patel2127

</script>
```

**输出:**

```
algorihythm
```

本文由 [**Raghav Jajodia**](https://github.com/jajodiaraghav) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。