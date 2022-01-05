# 打印最长回文子序列

> 原文:[https://www . geesforgeks . org/print-最长-回文-子序列/](https://www.geeksforgeeks.org/print-longest-palindromic-subsequence/)

给定一个序列，打印它最长的回文子序列。
**例:**

```
Input : BBABCBCAB
Output : BABCBAB
The above output is the longest
palindromic subsequence of given
sequence. "BBBBB" and "BBCBB" are 
also palindromic subsequences of
the given sequence, but not the 
longest ones.

Input : GEEKSFORGEEKS
Output : Output can be either EEKEE
         or EESEE or EEGEE, ..
```

我们在下面的帖子中讨论了一个解决方案，以找到最长回文子序列的长度。
[动态规划|集合 12(最长回文子序列)](https://www.geeksforgeeks.org/dynamic-programming-set-12-longest-palindromic-subsequence/)
本文讨论了打印最长回文子序列的解决方案。
这个问题接近[最长公共子序列(LCS)问题](https://www.geeksforgeeks.org/longest-common-subsequence-dp-4/)。事实上，我们可以用 LCS 作为子程序来解决这个问题。以下是使用 LCS 的两步解决方案。
1)反转给定的序列，并将反转存储在另一个数组中，比如 rev[0..n-1]
2)给定序列的 LCS 和 rev[]将是最长的回文序列。
3)一旦找到 LCS，就可以[打印 LCS](https://www.geeksforgeeks.org/printing-longest-common-subsequence/) 。
以下是上述方法的实施:

## C++

```
/* CPP program to print longest palindromic
   subsequence */
#include<bits/stdc++.h>
using namespace std;

/* Returns LCS X and Y */
string lcs(string &X, string &Y)
{
    int m = X.length();
    int n = Y.length();

    int L[m+1][n+1];

    /* Following steps build L[m+1][n+1] in bottom
       up fashion. Note that L[i][j] contains
       length of LCS of X[0..i-1] and Y[0..j-1] */
    for (int i=0; i<=m; i++)
    {
        for (int j=0; j<=n; j++)
        {
            if (i == 0 || j == 0)
                L[i][j] = 0;
            else if (X[i-1] == Y[j-1])
                L[i][j] = L[i-1][j-1] + 1;
            else
                L[i][j] = max(L[i-1][j], L[i][j-1]);
        }
    }

    // Following code is used to print LCS
    int index = L[m][n];

    // Create a string length index+1 and
    // fill it with \0
    string lcs(index+1, '\0');

    // Start from the right-most-bottom-most
    // corner and one by one store characters
    // in lcs[]
    int i = m, j = n;
    while (i > 0 && j > 0)
    {
        // If current character in X[] and Y
        // are same, then current character
        // is part of LCS
        if (X[i-1] == Y[j-1])
        {
            // Put current character in result
            lcs[index-1] = X[i-1];
            i--;
            j--;

            // reduce values of i, j and index
            index--;
        }

        // If not same, then find the larger of
        // two and go in the direction of larger
        // value
        else if (L[i-1][j] > L[i][j-1])
            i--;
        else
            j--;
    }

    return lcs;
}

// Returns longest palindromic subsequence
// of str
string longestPalSubseq(string &str)
{
    // Find reverse of str
    string rev = str;
    reverse(rev.begin(), rev.end());

    // Return LCS of str and its reverse
    return lcs(str, rev);
}

/* Driver program to test above function */
int main()
{
    string str = "GEEKSFORGEEKS";
    cout << longestPalSubseq(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print longest palindromic
//subsequence
class GFG {

    /* Returns LCS X and Y */
    static String lcs(String a, String b) {
        int m = a.length();
        int n = b.length();
        char X[] = a.toCharArray();
        char Y[] = b.toCharArray();

        int L[][] = new int[m + 1][n + 1];

        /* Following steps build L[m+1][n+1] in bottom
    up fashion. Note that L[i][j] contains
    length of LCS of X[0..i-1] and Y[0..j-1] */
        for (int i = 0; i <= m; i++) {
            for (int j = 0; j <= n; j++) {
                if (i == 0 || j == 0) {
                    L[i][j] = 0;
                } else if (X[i - 1] == Y[j - 1]) {
                    L[i][j] = L[i - 1][j - 1] + 1;
                } else {
                    L[i][j] = Math.max(L[i - 1][j], L[i][j - 1]);
                }
            }
        }

        // Following code is used to print LCS
        int index = L[m][n];

        // Create a String length index+1 and
        // fill it with \0
        char[] lcs = new char[index + 1];

        // Start from the right-most-bottom-most
        // corner and one by one store characters
        // in lcs[]
        int i = m, j = n;
        while (i > 0 && j > 0) {
            // If current character in X[] and Y
            // are same, then current character
            // is part of LCS
            if (X[i - 1] == Y[j - 1]) {
                // Put current character in result
                lcs[index - 1] = X[i - 1];
                i--;
                j--;

                // reduce values of i, j and index
                index--;
            } // If not same, then find the larger of
            // two and go in the direction of larger
            // value
            else if (L[i - 1][j] > L[i][j - 1]) {
                i--;
            } else {
                j--;
            }
        }
        String ans = "";
        for (int x = 0; x < lcs.length; x++) {
            ans += lcs[x];
        }
        return ans;
    }

// Returns longest palindromic subsequence
// of str
    static String longestPalSubseq(String str) {
        // Find reverse of str
        String rev = str;
        rev = reverse(rev);

        // Return LCS of str and its reverse
        return lcs(str, rev);
    }

    static String reverse(String str) {
        String ans = "";
        // convert String to character array
        // by using toCharArray
        char[] try1 = str.toCharArray();

        for (int i = try1.length - 1; i >= 0; i--) {
            ans += try1[i];
        }
        return ans;
    }

    /* Driver program to test above function */
    public static void main(String[] args) {
        String str = "GEEKSFORGEEKS";
        System.out.println(longestPalSubseq(str));

    }
}
```

## 蟒蛇 3

```
# Python3 program to print longest
# palindromic subsequence

# Returns LCS X and Y
def lcs_(X, Y) :

    m = len(X)
    n = len(Y)

    L = [[0] * (n + 1)] * (m + 1)

    # Following steps build L[m+1][n+1]
    # in bottom up fashion. Note that
    # L[i][j] contains length of LCS of
    # X[0..i-1] and Y[0..j-1]
    for i in range(n + 1) :

        for j in range(n + 1) :

            if (i == 0 or j == 0) :
                L[i][j] = 0;
            elif (X[i - 1] == Y[j - 1]) :
                L[i][j] = L[i - 1][j - 1] + 1;
            else :
                L[i][j] = max(L[i - 1][j],
                              L[i][j - 1]);

    # Following code is used to print LCS
    index = L[m][n];

    # Create a string length index+1 and
    # fill it with \0
    lcs = ["\n "] * (index + 1)

    # Start from the right-most-bottom-most
    # corner and one by one store characters
    # in lcs[]
    i, j= m, n

    while (i > 0 and j > 0) :

        # If current character in X[] and Y
        # are same, then current character
        # is part of LCS
        if (X[i - 1] == Y[j - 1]) :

            # Put current character in result
            lcs[index - 1] = X[i - 1]
            i -= 1
            j -= 1

            # reduce values of i, j and index
            index -= 1

        # If not same, then find the larger of
        # two and go in the direction of larger
        # value
        elif(L[i - 1][j] > L[i][j - 1]) :
            i -= 1

        else :
            j -= 1

    ans = ""

    for x in range(len(lcs)) :
        ans += lcs[x]

    return ans

# Returns longest palindromic
# subsequence of str
def longestPalSubseq(string) :

    # Find reverse of str
    rev = string[: : -1]

    # Return LCS of str and its reverse
    return lcs_(string, rev)

# Driver Code
if __name__ == "__main__" :

    string = "GEEKSFORGEEKS";
    print(longestPalSubseq(string))

# This code is contributed by Ryuga
```

## C#

```
// C# program to print longest palindromic
//subsequence
using System;

public class GFG {

    /* Returns LCS X and Y */
    static String lcs(String a, String b) {
        int m = a.Length;
        int n = b.Length;
        char []X = a.ToCharArray();
        char []Y = b.ToCharArray();

        int [,]L = new int[m + 1,n + 1];
         int i, j;
        /* Following steps build L[m+1,n+1] in bottom
    up fashion. Note that L[i,j] contains
    length of LCS of X[0..i-1] and Y[0..j-1] */
        for (i = 0; i <= m; i++) {
            for (j = 0; j <= n; j++) {
                if (i == 0 || j == 0) {
                    L[i,j] = 0;
                } else if (X[i - 1] == Y[j - 1]) {
                    L[i,j] = L[i - 1,j - 1] + 1;
                } else {
                    L[i,j] = Math.Max(L[i - 1,j], L[i,j - 1]);
                }
            }
        }

        // Following code is used to print LCS
        int index = L[m,n];

        // Create a String length index+1 and
        // fill it with \0
        char[] lcs = new char[index + 1];

        // Start from the right-most-bottom-most
        // corner and one by one store characters
        // in lcs[]
        i = m; j = n;
        while (i > 0 && j > 0) {
            // If current character in X[] and Y
            // are same, then current character
            // is part of LCS
            if (X[i - 1] == Y[j - 1]) {
                // Put current character in result
                lcs[index - 1] = X[i - 1];
                i--;
                j--;

                // reduce values of i, j and index
                index--;
            } // If not same, then find the larger of
            // two and go in the direction of larger
            // value
            else if (L[i - 1,j] > L[i,j - 1]) {
                i--;
            } else {
                j--;
            }
        }
        String ans = "";
        for (int x = 0; x < lcs.Length; x++) {
            ans += lcs[x];
        }
        return ans;
    }

// Returns longest palindromic subsequence
// of str
    static String longestPalSubseq(String str) {
        // Find reverse of str
        String rev = str;
        rev = reverse(rev);

        // Return LCS of str and its reverse
        return lcs(str, rev);
    }

    static String reverse(String str) {
        String ans = "";
        // convert String to character array
        // by using toCharArray
        char[] try1 = str.ToCharArray();

        for (int i = try1.Length - 1; i >= 0; i--) {
            ans += try1[i];
        }
        return ans;
    }

    /* Driver program to test above function */
    public static void Main() {
        String str = "GEEKSFORGEEKS";
        Console.Write(longestPalSubseq(str));

    }
}
// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript program to print longest palindromic subsequence

    /* Returns LCS X and Y */
    function lcs(a, b) {
        let m = a.length;
        let n = b.length;
        let X = a.split('');
        let Y = b.split('');

        let L = new Array(m + 1);
        for (let i = 0; i <= m; i++) {
            L[i] = new Array(n + 1);
            for (let j = 0; j <= n; j++) {
                L[i][j] = 0;
            }
        }

        /* Following steps build L[m+1][n+1] in bottom
    up fashion. Note that L[i][j] contains
    length of LCS of X[0..i-1] and Y[0..j-1] */
        for (let i = 0; i <= m; i++) {
            for (let j = 0; j <= n; j++) {
                if (i == 0 || j == 0) {
                    L[i][j] = 0;
                } else if (X[i - 1] == Y[j - 1]) {
                    L[i][j] = L[i - 1][j - 1] + 1;
                } else {
                    L[i][j] = Math.max(L[i - 1][j], L[i][j - 1]);
                }
            }
        }

        // Following code is used to print LCS
        let index = L[m][n];

        // Create a String length index+1 and
        // fill it with \0
        let lcs = new Array(index + 1);
        lcs.fill('');

        // Start from the right-most-bottom-most
        // corner and one by one store characters
        // in lcs[]
        let i = m, j = n;
        while (i > 0 && j > 0) {
            // If current character in X[] and Y
            // are same, then current character
            // is part of LCS
            if (X[i - 1] == Y[j - 1]) {
                // Put current character in result
                lcs[index - 1] = X[i - 1];
                i--;
                j--;

                // reduce values of i, j and index
                index--;
            } // If not same, then find the larger of
            // two and go in the direction of larger
            // value
            else if (L[i - 1][j] > L[i][j - 1]) {
                i--;
            } else {
                j--;
            }
        }
        let ans = "";
        for (let x = 0; x < lcs.length; x++) {
            ans += lcs[x];
        }
        return ans;
    }

// Returns longest palindromic subsequence
// of str
    function longestPalSubseq(str) {
        // Find reverse of str
        let rev = str;
        rev = reverse(rev);

        // Return LCS of str and its reverse
        return lcs(str, rev);
    }

    function reverse(str) {
        let ans = "";
        // convert String to character array
        // by using toCharArray
        let try1 = str.split('');

        for (let i = try1.length - 1; i >= 0; i--) {
            ans += try1[i];
        }
        return ans;
    }

    let str = "GEEKSFORGEEKS";
      document.write(longestPalSubseq(str));

    // This code is contributed by suresh07.
</script>
```

**输出:**

```
EEGEE
```