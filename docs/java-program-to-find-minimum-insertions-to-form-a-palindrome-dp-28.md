# 寻找最少插入形成回文的 Java 程序| DP-28

> 原文:[https://www . geesforgeks . org/Java-program-to-find-minimum-insertions-to-form-a-回文-dp-28/](https://www.geeksforgeeks.org/java-program-to-find-minimum-insertions-to-form-a-palindrome-dp-28/)

给定字符串 **str** ，任务是找到要插入的最小字符数，将其转换为回文。

在我们进一步讨论之前，让我们通过几个例子来理解:

*   **ab:** 所需插入次数为 1，即 **b** ab
*   **aa:** 所需的插入次数为 0，即 aa
*   **abcd:** 所需插入次数为 3，即 **dcb** abcd
*   **abcda:** 需要的插入数为 2，即 a **dc** bcda，与子串 bcd 中的插入数相同(为什么？).
*   **abcde:** 所需插入次数为 4，即 **edcb** abcde

让输入字符串为*字符串【l……h】*。这个问题可以分为三个部分:

1.  在子串字符串[l+1，…]中找到插入的最小数量。h]。
2.  找到子字符串[l …]中插入的最小数量。h-1]。
3.  找到子串字符串[l+1……h-1]中插入的最小数量。

**递归方法**:字符串中的最小插入次数**字符串【l…..h]** 可以给出为:

*   mininsertings(str[l+1…..h-1])如果字符串[l]等于字符串[h]
*   最小插入(字符串[l…..h-1])，最小插入(str[l+1…..h])) + 1，否则

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Naive recursive Java program to find 
// minimum number insertions needed to make 
// a string palindrome
class GFG 
{
    // Recursive function to find minimum 
    // number of insertions
    static int findMinInsertions(char str[], 
                                 int l, int h)
    {
        // Base Cases
        if (l > h) 
            return Integer.MAX_VALUE;

        if (l == h) 
            return 0;

        if (l == h - 1) 
            return (str[l] == str[h]) ? 0 : 1;

        // Check if the first and last characters
        // are same. On the basis of the  comparison
        // result, decide which subrpoblem(s) to call
        return (str[l] == str[h])?
                findMinInsertions(str, l + 1, h - 1):
               (Integer.min(findMinInsertions(str, l, h - 1),
                findMinInsertions(str, l + 1, h)) + 1);
    }

    // Driver code
    public static void main(String args[])
    {
        String str= "geeks";
        System.out.println(
        findMinInsertions(str.toCharArray(),
                          0, str.length()-1));
    }
}
// This code is contributed by Sumit Ghosh
```

**输出:**

```
3
```

**基于动态规划的解决方案**
如果我们仔细观察上述方法，我们可以发现它展示了[重叠子问题](https://www.geeksforgeeks.org/dynamic-programming-set-1/)。
假设我们想要找到字符串“abcde”中插入的最小数量:

```
                      abcde
            /       |      
           /        |        
           bcde         abcd       bcd  cd   bcd abc bc
   / |   / |  /| / | 
de cd d cd bc c………………….->
```

粗体的子字符串表示递归将被终止，递归树不能从那里开始。相同颜色的子串表示[重叠子问题](https://www.geeksforgeeks.org/dynamic-programming-set-1/)。

*如何重用子问题的解？*记忆技术用于避免类似的子问题回忆。我们可以创建一个表来存储子问题的结果，以便在再次遇到相同的子问题时可以直接使用它们。
下表表示字符串 abcde 的存储值。

```
a b c d e
----------
0 1 2 3 4
0 0 1 2 3 
0 0 0 1 2 
0 0 0 0 1 
0 0 0 0 0
```

***如何填表？***
表格应该以对角线的方式填写。对于字符串 abcde，0…4，应按照填充表格的顺序排列如下:

```
Gap = 1: (0, 1) (1, 2) (2, 3) (3, 4)

Gap = 2: (0, 2) (1, 3) (2, 4)

Gap = 3: (0, 3) (1, 4)

Gap = 4: (0, 4)
```

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java solution for Dynamic Programming
// based program to find minimum number
// insertions needed to make a string
// palindrome
import java.util.Arrays;

class GFG
{
    // A DP function to find minimum number
    // of insertions
    static int findMinInsertionsDP(char str[], 
                                   int n)
    {
        // Create a table of size n*n. table[i][j]
        // will store minimum number of insertions
        // needed to convert str[i..j] to a palindrome.
        int table[][] = new int[n][n];
        int l, h, gap;

        // Fill the table
        for (gap = 1; gap < n; ++gap)
        for (l = 0, h = gap; h < n; ++l, ++h)
            table[l][h] = (str[l] == str[h])?
                           table[l+1][h-1] :
                          (Integer.min(table[l][h-1],
                                 table[l+1][h]) + 1);

        // Return minimum number of insertions
        // for str[0..n-1]
        return table[0][n-1];
    }

    // Driver code
    public static void main(String args[])
    {
        String str = "geeks";
        System.out.println(
        findMinInsertionsDP(str.toCharArray(), 
                            str.length()));
    }
}
// This code is contributed by Sumit Ghosh
```

**输出:**

```
3
```

**时间复杂度:**o(n^2)
T3】辅助空间: O(N^2)

**另一个动态规划解(变异的** [**【最长公共子序列问题】)**](https://www.geeksforgeeks.org/dynamic-programming-set-4-longest-common-subsequence/)
寻找最小插入的问题也可以用[最长公共子序列(LCS)问题](https://www.geeksforgeeks.org/longest-common-subsequence-dp-4/)来解决。如果我们找出字符串的 LCS 及其反义词，我们就知道一个回文最多可以有多少个字符。我们需要插入剩余的字符。以下是步骤。

1.  求输入字符串的 LCS 长度及其倒数。让长度为 l。
2.  所需的最小插入次数是输入字符串的长度减去“l”。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// An LCS based Java program to find minimum
// number insertions needed to make a string
// palindrome
class GFG
{
    /* Returns length of LCS for X[0..m-1],
       Y[0..n-1]. See http://goo.gl/bHQVP for
       details of this function */
    static int lcs(String X, String Y, 
                   int m, int n)
    {
        int L[][] = new int[m+1][n+1];
        int i, j;

        /* Following steps build L[m+1][n+1] in
           bottom up fashion. Note that L[i][j]
           contains length of LCS of X[0..i-1]
           and Y[0..j-1] */
        for (i = 0; i <= m; i++)
        {
            for (j = 0; j <= n; j++)
            {
                if (i == 0 || j == 0)
                    L[i][j] = 0;

                else if (X.charAt(i-1) == 
                         Y.charAt(j-1))
                    L[i][j] = L[i-1][j-1] + 1;

                else
                    L[i][j] = Integer.max(L[i-1][j], 
                                          L[i][j-1]);
            }
        }

        /* L[m][n] contains length of LCS for
           X[0..n-1] and Y[0..m-1] */
        return L[m][n];
    }

    // LCS based function to find minimum number
    // of insertions
    static int findMinInsertionsLCS(String str, 
                                    int n)
    {
        // Using StringBuffer to reverse a String
        StringBuffer sb = new StringBuffer(str);
        sb.reverse();
        String revString = sb.toString();

        // The output is length of string minus
        // length of lcs of str and it reverse
        return (n - lcs(str, revString , n, n));
    }

    // Driver program to test above functions
    public static void main(String args[])
    {
        String str = "geeks";
        System.out.println(
        findMinInsertionsLCS(str, str.length()));
    }
}
// This code is contributed by Sumit Ghosh
```

**输出:**

```
3
```

**时间复杂度:**o(n^2)
T3】辅助空间 o(n^2)

更多详情请参考完整文章[最小插入形成回文| DP-28](https://www.geeksforgeeks.org/minimum-insertions-to-form-a-palindrome-dp-28/) ！