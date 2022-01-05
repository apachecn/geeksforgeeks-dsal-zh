# 最短超弦问题

> 原文:[https://www.geeksforgeeks.org/shortest-superstring-problem/](https://www.geeksforgeeks.org/shortest-superstring-problem/)

给定一组 n 个字符串 arr[]，找到包含给定集合中每个字符串的最小字符串作为子字符串。我们可以假设 arr[]中没有字符串是另一个字符串的子字符串。
示例:

```
Input:  arr[] = {"geeks", "quiz", "for"}
Output: geeksquizfor

Input:  arr[] = {"catg", "ctaagt", "gcta", "ttca", "atgcatc"}
Output: gctaagttcatgcatc
```

**最短超弦贪婪近似算法**
最短超弦问题是一个 [NP 难](https://www.geeksforgeeks.org/np-completeness-set-1/)问题。总能找到最短超弦的解需要指数时间。下面是一个近似贪婪算法。

```
Let arr[] be given set of strings.

1) Create an auxiliary array of strings, temp[].  Copy contents
   of arr[] to temp[]

2) While temp[] contains more than one strings
     a) Find the most overlapping string pair in temp[]. Let this
        pair be 'a' and 'b'. 
     b) Replace 'a' and 'b' with the string obtained after combining
        them.

3) The only string left in temp[] is the result, return it.
```

如果一个字符串的前缀与另一个字符串的后缀相同，则两个字符串重叠，反之亦然。匹配前缀和后缀的最大重叠平均长度最大。
**上述算法的工作:**

```
arr[] = {"catgc", "ctaagt", "gcta", "ttca", "atgcatc"}
Initialize:
temp[] = {"catgc", "ctaagt", "gcta", "ttca", "atgcatc"}

The most overlapping strings are "catgc" and "atgcatc"
(Suffix of length 4 of "catgc" is same as prefix of "atgcatc")
Replace two strings with "catgcatc", we get
temp[] = {"catgcatc", "ctaagt", "gcta", "ttca"}

The most overlapping strings are "ctaagt" and "gcta"
(Prefix of length 3 of "ctaagt" is same as suffix of "gcta")
Replace two strings with "gctaagt", we get
temp[] = {"catgcatc", "gctaagt", "ttca"}

The most overlapping strings are "catgcatc" and "ttca"
(Prefix of length 2 of "catgcatc" as suffix of "ttca")
Replace two strings with "ttcatgcatc", we get
temp[] = {"ttcatgcatc", "gctaagt"}

Now there are only two strings in temp[], after combing
the two in optimal way, we get tem[] = {"gctaagttcatgcatc"}

Since temp[] has only one string now, return it.
```

下面是上述算法的实现。

## C++

```
// C++ program to find shortest
// superstring using Greedy
// Approximate Algorithm
#include <bits/stdc++.h>
using namespace std;

// Utility function to calculate
// minimum of two numbers
int min(int a, int b)
{
    return (a < b) ? a : b;
}

// Function to calculate maximum
// overlap in two given strings
int findOverlappingPair(string str1,
                     string str2, string &str)
{

    // Max will store maximum
    // overlap i.e maximum
    // length of the matching
    // prefix and suffix
    int max = INT_MIN;
    int len1 = str1.length();
    int len2 = str2.length();

    // Check suffix of str1 matches
    // with prefix of str2
    for (int i = 1; i <=
                      min(len1, len2); i++)
    {

        // Compare last i characters
        // in str1 with first i
        // characters in str2
        if (str1.compare(len1-i, i, str2,
                                 0, i) == 0)
        {
            if (max < i)
            {
                // Update max and str
                max = i;
                str = str1 + str2.substr(i);
            }
        }
    }

    // Check prefix of str1 matches
    // with suffix of str2
    for (int i = 1; i <=
                        min(len1, len2); i++)
    {

        // compare first i characters
        // in str1 with last i
        // characters in str2
        if (str1.compare(0, i, str2,
                              len2-i, i) == 0)
        {
            if (max < i)
            {

                // Update max and str
                max = i;
                str = str2 + str1.substr(i);
            }
        }
    }

    return max;
}

// Function to calculate
// smallest string that contains
// each string in the given
// set as substring.
string findShortestSuperstring(string arr[],
                                    int len)
{

    // Run len-1 times to
    // consider every pair
    while(len != 1)
    {

        // To store  maximum overlap
        int max = INT_MIN;  

        // To store array index of strings
        int l, r;   

        // Involved in maximum overlap
        string resStr;   

        // Maximum overlap
        for (int i = 0; i < len; i++)
        {
            for (int j = i + 1; j < len; j++)
            {
                string str;

                // res will store maximum
                // length of the matching
                // prefix and suffix str is
                // passed by reference and
                // will store the resultant
                // string after maximum
                // overlap of arr[i] and arr[j],
                // if any.
                int res = findOverlappingPair(arr[i],
                                         arr[j], str);

                // check for maximum overlap
                if (max < res)
                {
                    max = res;
                    resStr.assign(str);
                    l = i, r = j;
                }
            }
        }

        // Ignore last element in next cycle
        len--;  

        // If no overlap, append arr[len] to arr[0]
        if (max == INT_MIN)
            arr[0] += arr[len];
        else
        {

            // Copy resultant string to index l
            arr[l] = resStr; 

            // Copy string at last index to index r
            arr[r] = arr[len]; 
        }
    }
    return arr[0];
}

// Driver program
int main()
{
    string arr[] = {"catgc", "ctaagt",
                    "gcta", "ttca", "atgcatc"};
    int len = sizeof(arr)/sizeof(arr[0]);

    // Function Call
    cout << "The Shortest Superstring is "
         << findShortestSuperstring(arr, len);

    return 0;
}
// This code is contributed by Aditya Goel
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find shortest
// superstring using Greedy
// Approximate Algorithm
import java.io.*;
import java.util.*;

class GFG
{

    static String str;

    // Utility function to calculate
    // minimum of two numbers
    static int min(int a, int b)
    {
        return (a < b) ? a : b;
    }

    // Function to calculate maximum
    // overlap in two given strings
    static int findOverlappingPair(String str1,
                                   String str2)
    {

        // max will store maximum
        // overlap i.e maximum
        // length of the matching
        // prefix and suffix
        int max = Integer.MIN_VALUE;
        int len1 = str1.length();
        int len2 = str2.length();

        // check suffix of str1 matches
        // with prefix of str2
        for (int i = 1; i <=
                            min(len1, len2); i++)
        {

            // compare last i characters
            // in str1 with first i
            // characters in str2
            if (str1.substring(len1 - i).compareTo(
                        str2.substring(0, i)) == 0)
            {
                if (max < i)
                {

                    // Update max and str
                    max = i;
                    str = str1 + str2.substring(i);
                }
            }
        }

        // check prefix of str1 matches
        // with suffix of str2
        for (int i = 1; i <=
                           min(len1, len2); i++)
        {

            // compare first i characters
            // in str1 with last i
            // characters in str2
            if (str1.substring(0, i).compareTo(
                      str2.substring(len2 - i)) == 0)
            {
                if (max < i)
                {

                    // pdate max and str
                    max = i;
                    str = str2 + str1.substring(i);
                }
            }
        }

        return max;
    }

    // Function to calculate smallest
    // string that contains
    // each string in the given set as substring.
    static String findShortestSuperstring(
                          String arr[], int len)
    {

        // run len-1 times to consider every pair
        while (len != 1)
        {

            // To store maximum overlap
            int max = Integer.MIN_VALUE;

            // To store array index of strings
            // involved in maximum overlap
            int l = 0, r = 0;

            // to store resultant string after
            // maximum overlap
            String resStr = "";

            for (int i = 0; i < len; i++)
            {
                for (int j = i + 1; j < len; j++)
                {

                    // res will store maximum
                    // length of the matching
                    // prefix and suffix str is
                    // passed by reference and
                    // will store the resultant
                    // string after maximum
                    // overlap of arr[i] and arr[j],
                    // if any.
                    int res = findOverlappingPair
                                  (arr[i], arr[j]);

                    // Check for maximum overlap
                    if (max < res)
                    {
                        max = res;
                        resStr = str;
                        l = i;
                        r = j;
                    }
                }
            }

            // Ignore last element in next cycle
            len--;

            // If no overlap,
            // append arr[len] to arr[0]
            if (max == Integer.MIN_VALUE)
                arr[0] += arr[len];
            else
            {

                // Copy resultant string
                // to index l
                arr[l] = resStr;

                // Copy string at last index
                // to index r
                arr[r] = arr[len];
            }
        }
        return arr[0];
    }

    // Driver Code
    public static void main(String[] args)
    {
        String[] arr = { "catgc", "ctaagt",
                      "gcta", "ttca", "atgcatc" };
        int len = arr.length;

        System.out.println("The Shortest Superstring is " +
                        findShortestSuperstring(arr, len));
    }
}

// This code is contributed by
// sanjeev2552
```

## C#

```
// C# program to find shortest
// superstring using Greedy
// Approximate Algorithm
using System;

class GFG
{

    static String str;

    // Utility function to calculate
    // minimum of two numbers
    static int min(int a, int b)
    {
        return (a < b) ? a : b;
    }

    // Function to calculate maximum
    // overlap in two given strings
    static int findOverlappingPair(String str1,
                                   String str2)
    {

        // max will store maximum
        // overlap i.e maximum
        // length of the matching
        // prefix and suffix
        int max = Int32.MinValue;
        int len1 = str1.Length;
        int len2 = str2.Length;

        // check suffix of str1 matches
        // with prefix of str2
        for (int i = 1; i <=
                            min(len1, len2); i++)
        {

            // compare last i characters
            // in str1 with first i
            // characters in str2
            if (str1.Substring(len1 - i).CompareTo(
                        str2.Substring(0, i)) == 0)
            {
                if (max < i)
                {

                    // Update max and str
                    max = i;
                    str = str1 + str2.Substring(i);
                }
            }
        }

        // check prefix of str1 matches
        // with suffix of str2
        for (int i = 1; i <=
                           min(len1, len2); i++)
        {

            // compare first i characters
            // in str1 with last i
            // characters in str2
            if (str1.Substring(0, i).CompareTo(
                      str2.Substring(len2 - i)) == 0)
            {
                if (max < i)
                {

                    // pdate max and str
                    max = i;
                    str = str2 + str1.Substring(i);
                }
            }
        }

        return max;
    }

    // Function to calculate smallest
    // string that contains
    // each string in the given set as substring.
    static String findShortestSuperstring(String []arr, int len)
    {

        // run len-1 times to consider every pair
        while (len != 1)
        {

            // To store maximum overlap
            int max = Int32.MinValue;

            // To store array index of strings
            // involved in maximum overlap
            int l = 0, r = 0;

            // to store resultant string after
            // maximum overlap
            String resStr = "";

            for (int i = 0; i < len; i++)
            {
                for (int j = i + 1; j < len; j++)
                {

                    // res will store maximum
                    // length of the matching
                    // prefix and suffix str is
                    // passed by reference and
                    // will store the resultant
                    // string after maximum
                    // overlap of arr[i] and arr[j],
                    // if any.
                    int res = findOverlappingPair
                                  (arr[i], arr[j]);

                    // Check for maximum overlap
                    if (max < res)
                    {
                        max = res;
                        resStr = str;
                        l = i;
                        r = j;
                    }
                }
            }

            // Ignore last element in next cycle
            len--;

            // If no overlap,
            // append arr[len] to arr[0]
            if (max == Int32.MinValue)
                arr[0] += arr[len];
            else
            {

                // Copy resultant string
                // to index l
                arr[l] = resStr;

                // Copy string at last index
                // to index r
                arr[r] = arr[len];
            }
        }
        return arr[0];
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String[] arr = { "catgc", "ctaagt",
                      "gcta", "ttca", "atgcatc" };
        int len = arr.Length;

        Console.Write("The Shortest Superstring is " +
                        findShortestSuperstring(arr, len));
    }
}

// This code is contributed by shivanisinghss2110
```

**Output**

```
The Shortest Superstring is gctaagttcatgcatc
```

**上述算法的性能:**
上述贪婪算法被证明是 4 个近似值(即该算法生成的超弦长度永远不会超过最短可能超弦的 4 倍)。这个算法被推测为 2 个近似值(没有人发现它产生两倍以上最差值的情况)。推测的最坏情况例子是{ab <sup>k</sup> ，b <sup>k</sup> c，b <sup>k+1</sup> }。例如{“abb”、“bbc”、“BBB”}，上述算法可能会生成“abbcbbb”(如果“abb”和“bbc”被选为第一对)，但实际最短的超弦是“abbbc”。这里比率是 7/5，但是对于大 k，比率接近 2。

**另一种方法:**

我所说的“贪婪方法”是指:每次我们合并最大长度重叠的两个字符串时，从字符串数组中移除它们，并将合并后的字符串放入字符串数组中。

那么问题就变成了:在这个图中找到访问每个节点一次的最短路径。这是一个旅行推销员问题。

应用旅行推销员问题的动态规划解决方案。记得记录路径。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.io.*;
import java.util.*;

class Solution
{

  // Function to calculate shortest
  // super string
  public static String shortestSuperstring(
                                   String[] A)
  {
    int n = A.length;
    int[][] graph = new int[n][n];

    // Build the graph
    for (int i = 0; i < n; i++)
    {
      for (int j = 0; j < n; j++)
      {
        graph[i][j] = calc(A[i], A[j]);
        graph[j][i] = calc(A[j], A[i]);
      }
    }

    // Creating dp array
    int[][] dp = new int[1 << n][n];

    // Creating path array
    int[][] path = new int[1 << n][n];
    int last = -1, min = Integer.MAX_VALUE;

    // start TSP DP
    for (int i = 1; i < (1 << n); i++)
    {
      Arrays.fill(dp[i], Integer.MAX_VALUE);

      // Iterate j from 0 to n - 1
      for (int j = 0; j < n; j++)
      {
        if ((i & (1 << j)) > 0)
        {
          int prev = i - (1 << j);

          // Check if prev is zero
          if (prev == 0)
          {
            dp[i][j] = A[j].length();
          }
          else
          {

            // Iterate k from 0 to n - 1
            for (int k = 0; k < n; k++)
            {
              if (dp[prev][k] < Integer.MAX_VALUE &&
                  dp[prev][k] + graph[k][j] < dp[i][j])
              {
                dp[i][j] = dp[prev][k] + graph[k][j];
                path[i][j] = k;
              }
            }
          }
        }
        if (i == (1 << n) - 1 && dp[i][j] < min)
        {
          min = dp[i][j];
          last = j;
        }
      }
    }

    // Build the path
    StringBuilder sb = new StringBuilder();
    int cur = (1 << n) - 1;

    // Creating a stack
    Stack<Integer> stack = new Stack<>();

    // Until cur is zero
    // push last
    while (cur > 0)
    {
      stack.push(last);
      int temp = cur;
      cur -= (1 << last);
      last = path[temp][last];
    }

    // Build the result
    int i = stack.pop();
    sb.append(A[i]);

    // Until stack is empty
    while (!stack.isEmpty())
    {
      int j = stack.pop();
      sb.append(A[j].substring(A[j].length() -
                                graph[i][j]));
      i = j;
    }
    return sb.toString();
  }

  // Function to check
  public static int calc(String a, String b)
  {
    for (int i = 1; i < a.length(); i++)
    {
      if (b.startsWith(a.substring(i)))
      {
        return b.length() - a.length() + i;
      }
    }

    // Return size of b
    return b.length();
  }

  // Driver Code
  public static void main(String[] args)
  {
    String[] arr = { "catgc", "ctaagt",
                    "gcta", "ttca", "atgcatc" };

    // Function Call
    System.out.println("The Shortest Superstring is " +
                    shortestSuperstring(arr));
   }
}
```

**Output**

```
The Shortest Superstring is gctaagttcatgcatc
```

**时间复杂度:** O(n^2 * 2^n)

对于这个问题有更好的近似算法。请参考以下链接。
[【最短超弦问题|集合 2(使用集合覆盖)](https://www.geeksforgeeks.org/shortest-superstring-problem-set-2-using-set-cover/)
**应用:**
在基因组计划中很有用，因为它将允许研究人员从片段的集合中确定整个编码区域。
**参考:**
[http://file admin . cs . lth . se/cs/Personal/Andrzej _ Lingas/super string . pdf](http://fileadmin.cs.lth.se/cs/Personal/Andrzej_Lingas/superstring.pdf)
[http://math.mit.edu/~goemans/18434S06/superstring-lele.pdf](http://math.mit.edu/~goemans/18434S06/superstring-lele.pdf)
本文由 **Piyush** 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。