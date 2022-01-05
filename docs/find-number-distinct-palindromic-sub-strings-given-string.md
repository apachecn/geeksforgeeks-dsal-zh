# 查找给定字符串的所有不同回文子字符串

> 原文:[https://www . geesforgeks . org/find-number-distinct-回文-子字符串-给定-string/](https://www.geeksforgeeks.org/find-number-distinct-palindromic-sub-strings-given-string/)

给定一串小写 ASCII 字符，找到它的所有不同的连续回文子串。

**示例:**

```
Input: str = "abaaa"
Output:  Below are 5 palindrome sub-strings
a
aa
aaa
aba
b

Input: str = "geek"
Output:  Below are 4 palindrome sub-strings
e
ee
g
k
```

**第一步:使用改进的 Manacher 算法查找所有回文:**
将每个字符视为一个轴心，在两侧展开，以所考虑的轴心字符为中心查找偶数和奇数长度回文的长度，并将长度存储在 2 个数组中(奇数&偶数)。
这一步的时间复杂度是 O(n^2)

**第二步:将所有找到的回文插入 HashMap:**
将上一步找到的回文全部插入 HashMap。还将字符串中的所有单个字符插入到 HashMap 中(以生成不同的单字母回文子字符串)。
这个步骤的时间复杂度是 O(n^3)假设散列插入搜索花费 O(1)个时间。请注意，一个字符串最多只能有 O(n^2)回文子字符串。在下面的 C++代码中，有序 hashmap 用于插入和搜索时间复杂度为 O(Logn)的地方。在 C++中，使用[红黑树](https://www.geeksforgeeks.org/red-black-tree-set-1-introduction-2/)实现有序 hashmap。

**第三步:打印不同的回文以及这种不同回文的数量:**
最后一步是打印 HashMap 中存储的所有值(由于 HashMap 的属性，只有不同的元素会被散列)。地图的大小给出了不同回文连续子串的数量。

以下是上述想法的实现。

## C++

```
// C++ program to find all distinct palindrome sub-strings
// of a given string
#include <iostream>
#include <map>
using namespace std;

// Function to print all distinct palindrome sub-strings of s
void palindromeSubStrs(string s)
{
    map<string, int> m;
    int n = s.size();

    // table for storing results (2 rows for odd-
    // and even-length palindromes
    int R[2][n+1];

    // Find all sub-string palindromes from the given input
    // string insert 'guards' to iterate easily over s
    s = "@" + s + "#";

    for (int j = 0; j <= 1; j++)
    {
        int rp = 0;   // length of 'palindrome radius'
        R[j][0] = 0;

        int i = 1;
        while (i <= n)
        {
            //  Attempt to expand palindrome centered at i
            while (s[i - rp - 1] == s[i + j + rp])
                rp++;  // Incrementing the length of palindromic
                       // radius as and when we find vaid palindrome

            // Assigning the found palindromic length to odd/even
            // length array
            R[j][i] = rp;
            int k = 1;
            while ((R[j][i - k] != rp - k) && (k < rp))
            {
                R[j][i + k] = min(R[j][i - k],rp - k);
                k++;
            }
            rp = max(rp - k,0);
            i += k;
        }
    }

    // remove 'guards'
    s = s.substr(1, n);

    // Put all obtained palindromes in a hash map to
    // find only distinct palindromess
    m[string(1, s[0])]=1;
    for (int i = 1; i <= n; i++)
    {
        for (int j = 0; j <= 1; j++)
            for (int rp = R[j][i]; rp > 0; rp--)
               m[s.substr(i - rp - 1, 2 * rp + j)]=1;
        m[string(1, s[i])]=1;
    }

    //printing all distinct palindromes from hash map
   cout << "Below are " << m.size()-1
        << " palindrome sub-strings";
   map<string, int>::iterator ii;
   for (ii = m.begin(); ii!=m.end(); ++ii)
      cout << (*ii).first << endl;
}

// Driver program
int main()
{
    palindromeSubStrs("abaaa");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find all distinct palindrome
// sub-strings of a given string
import java.util.Map;
import java.util.TreeMap;

public class GFG
{    
    // Function to print all distinct palindrome
    // sub-strings of s
    static void palindromeSubStrs(String s)
    {
        //map<string, int> m;
        TreeMap<String , Integer> m = new TreeMap<>();
        int n = s.length();

        // table for storing results (2 rows for odd-
        // and even-length palindromes
        int[][] R = new int[2][n+1];

        // Find all sub-string palindromes from the
        // given input string insert 'guards' to
        // iterate easily over s
        s = "@" + s + "#";

        for (int j = 0; j <= 1; j++)
        {
            int rp = 0;   // length of 'palindrome radius'
            R[j][0] = 0;

            int i = 1;
            while (i <= n)
            {
                //  Attempt to expand palindrome centered
                // at i
                while (s.charAt(i - rp - 1) == s.charAt(i +
                                                j + rp))
                    rp++;  // Incrementing the length of
                           // palindromic radius as and
                           // when we find valid palindrome

                // Assigning the found palindromic length
                // to odd/even length array
                R[j][i] = rp;
                int k = 1;
                while ((R[j][i - k] != rp - k) && (k < rp))
                {
                    R[j][i + k] = Math.min(R[j][i - k],
                                              rp - k);
                    k++;
                }
                rp = Math.max(rp - k,0);
                i += k;
            }
        }

        // remove 'guards'
        s = s.substring(1, s.length()-1);

        // Put all obtained palindromes in a hash map to
        // find only distinct palindromess
        m.put(s.substring(0,1), 1);
        for (int i = 1; i < n; i++)
        {
            for (int j = 0; j <= 1; j++)
                for (int rp = R[j][i]; rp > 0; rp--)
                   m.put(s.substring(i - rp - 1,  i - rp - 1
                                       + 2 * rp + j), 1);
            m.put(s.substring(i, i + 1), 1);
        }

        // printing all distinct palindromes from
        // hash map
       System.out.println("Below are " + (m.size())
                           + " palindrome sub-strings");

       for (Map.Entry<String, Integer> ii:m.entrySet())
          System.out.println(ii.getKey());
    }

    // Driver program
    public static void main(String args[])
    {
        palindromeSubStrs("abaaa");
    }
}
// This code is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# Python program Find all distinct palindromic sub-strings
# of a given string

# Function to print all distinct palindrome sub-strings of s
def palindromeSubStrs(s):
    m = dict()
    n = len(s)

    # table for storing results (2 rows for odd-
    # and even-length palindromes
    R = [[0 for x in xrange(n+1)] for x in xrange(2)]

    # Find all sub-string palindromes from the given input
    # string insert 'guards' to iterate easily over s
    s = "@" + s + "#"

    for j in xrange(2):
        rp = 0    # length of 'palindrome radius'
        R[j][0] = 0

        i = 1
        while i <= n:

            # Attempt to expand palindrome centered at i
            while s[i - rp - 1] == s[i + j + rp]:
                rp += 1 # Incrementing the length of palindromic
                        # radius as and when we find valid palindrome

            # Assigning the found palindromic length to odd/even
            # length array
            R[j][i] = rp
            k = 1
            while (R[j][i - k] != rp - k) and (k < rp):
                R[j][i+k] = min(R[j][i-k], rp - k)
                k += 1
            rp = max(rp - k, 0)
            i += k

    # remove guards
    s = s[1:len(s)-1]

    # Put all obtained palindromes in a hash map to
    # find only distinct palindrome
    m[s[0]] = 1
    for i in xrange(1,n):
        for j in xrange(2):
            for rp in xrange(R[j][i],0,-1):
                m[s[i - rp - 1 : i - rp - 1 + 2 * rp + j]] = 1
        m[s[i]] = 1

    # printing all distinct palindromes from hash map
    print "Below are " + str(len(m)) + " pali sub-strings"
    for i in m:
        print i

# Driver program
palindromeSubStrs("abaaa")
# This code is contributed by BHAVYA JAIN and ROHIT SIKKA
```

## C#

```
// C# program to find all distinct palindrome
// sub-strings of a given string
using System;
using System.Collections.Generic;

class GFG
{

    // Function to print all distinct palindrome
    // sub-strings of s
    public static void palindromeSubStrs(string s)
    {
        //map<string, int> m;
        Dictionary < string,
        int > m = new Dictionary < string,
        int > ();
        int n = s.Length;

        // table for storing results (2 rows for odd-
        // and even-length palindromes
        int[, ] R = new int[2, n + 1];

        // Find all sub-string palindromes from the
        // given input string insert 'guards' to
        // iterate easily over s
        s = "@" + s + "#";
        for (int j = 0; j <= 1; j++)
        {
            int rp = 0; // length of 'palindrome radius'
            R[j, 0] = 0;
            int i = 1;
            while (i <= n)
            {

                // Attempt to expand palindrome centered
                // at i
                while (s[i - rp - 1] == s[i + j + rp])

                // Incrementing the length of
                // palindromic radius as and
                // when we find valid palindrome
                rp++;

                // Assigning the found palindromic length
                // to odd/even length array
                R[j, i] = rp;
                int k = 1;
                while ((R[j, i - k] != rp - k) && k < rp)
                {
                    R[j, i + k] = Math.Min(R[j, i - k], rp - k);
                    k++;
                }
                rp = Math.Max(rp - k, 0);
                i += k;
            }
        }

        // remove 'guards'
        s = s.Substring(1);

        // Put all obtained palindromes in a hash map to
        // find only distinct palindromess
        if (!m.ContainsKey(s.Substring(0, 1)))
            m.Add(s.Substring(0, 1), 1);
        else
            m[s.Substring(0, 1)]++;

        for (int i = 1; i < n; i++)
        {
            for (int j = 0; j <= 1; j++)
            for (int rp = R[j, i]; rp > 0; rp--)
            {
                if (!m.ContainsKey(s.Substring(i - rp - 1, 2 * rp + j)))
                    m.Add(s.Substring(i - rp - 1, 2 * rp + j), 1);
                else
                    m[s.Substring(i - rp - 1, 2 * rp + j)]++;
            }

            if (!m.ContainsKey(s.Substring(i, 1)))
                m.Add(s.Substring(i, 1), 1);
            else
                m[s.Substring(i, 1)]++;
        }

        // printing all distinct palindromes from
        // hash map
        Console.WriteLine("Below are " + (m.Count));

        foreach(KeyValuePair < string, int > ii in m)
        Console.WriteLine(ii.Key);
    }

    // Driver Code
    public static void Main(string[] args)
    {
        palindromeSubStrs("abaaa");
    }
}

// This code is contributed by
// sanjeev2552
```

**输出:**

```
 Below are 5 palindrome sub-strings
a
aa
aaa
aba
b 
```

**类似问题:**
[统计一串中所有回文子串](https://www.geeksforgeeks.org/count-palindrome-sub-strings-string/)
本文由 [Vignesh Narayanan](https://sites.google.com/a/asu.edu/vignesh-narayanan/) 和 [Sowmya Sampath](https://sites.google.com/a/usc.edu/sowmya/) 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。