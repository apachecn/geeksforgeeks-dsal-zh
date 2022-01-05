# 给定字符串的第 K 个字典上最小的唯一子串

> 原文:[https://www . geesforgeks . org/k-th-按字典顺序排列-最小-唯一-给定字符串的子字符串/](https://www.geeksforgeeks.org/k-th-lexicographically-smallest-unique-substring-of-a-given-string/)

给定一个字符串 s，任务是打印 s 的不同子字符串中按字典顺序最小的第 K 个。
s 的子字符串是通过取出 s 中非空的连续部分而获得的字符串。
例如，如果 s = ababc，A、bab 和 ababc 是 s 的子字符串，而 ac、z 和空字符串不是。另外，我们说当子字符串作为字符串不同时，它们是不同的。

**示例:**

> **输入:** str = "aba "，k = 4
> **输出:** b
> 所有唯一的子串都是 a，ab，aba，b，ba。
> 因此，第 4 个字典序最小的子串是 b。
> 
> **输入:** str = "geeksforgeeks "，k = 5
> **输出:** eeksf

**方法:**对于任意的字符串 t，它的每个合适的后缀在字典上小于 t，t 的字典序秩至少为|t|。因此，答案的长度最多为 K。
生成长度最多为 K 的所有 S 的子串。对它们进行排序，使它们唯一，并打印第 K 个，其中 N = |S|。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include<bits/stdc++.h>
using namespace std;

void kThLexString(string st, int k, int n)
{

    // Set to store the unique substring
    set<string> z;

    for(int i = 0; i < n; i++)
    {

       // String to create each substring
       string pp;

       for(int j = i; j < i + k; j++)
       {
          if (j >= n)
              break;
          pp += st[j];

          // Adding to set
          z.insert(pp);
       }
    }

    // Converting set into a list
    vector<string> fin(z.begin(), z.end());

    // Sorting the strings int the list
    // into lexicographical order
    sort(fin.begin(), fin.end());

    // Printing kth substring
    cout << fin[k - 1];
}

// Driver code
int main()
{
    string s = "geeksforgeeks";
    int k = 5;
    int n = s.length();

    kThLexString(s, k, n);
}

// This code is contributed by yatinagg
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
import java.util.*;
class GFG{

public static void kThLexString(String st,
                                int k, int n)
{
    // Set to store the unique substring
    Set<String> z = new HashSet<String>();

    for(int i = 0; i < n; i++)
    {
        // String to create each substring
        String pp = "";

        for(int j = i; j < i + k; j++)
        {
        if (j >= n)
            break;
        pp += st.charAt(j);

        // Adding to set
        z.add(pp);
        }
    }

    // Converting set into a list
    Vector<String> fin = new Vector<String>();
    fin.addAll(z);

    // Sorting the strings int the list
    // into lexicographical order
    Collections.sort(fin);

    // Printing kth substring
    System.out.print(fin.get(k - 1));
}

// Driver Code
public static void main(String[] args)
{
    String s = "geeksforgeeks";
    int k = 5;
    int n = s.length();
    kThLexString(s, k, n);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
def kThLexString(st, k, n):
    # Set to store the unique substring
    z = set()

    for i in range(n):
        # String to create each substring
        pp = ""

        for j in range(i, i + k):

            if (j >= n):

                break

            pp += s[j]
            # adding to set
            z.add(pp)

    # converting set into a list
    fin = list(z)

    # sorting the strings int the list
    # into lexicographical order
    fin.sort()

    # printing kth substring
    print(fin[k - 1])

s = "geeksforgeeks"

k = 5

n = len(s)
kThLexString(s, k, n)
```

## C#

```
// C# implementation of
// the above approach
using System;
using System.Collections.Generic;
using System.Collections;

class GFG{

public static void kThLexString(string st,
                                int k, int n)
{

    // Set to store the unique substring
    HashSet<string> z = new HashSet<string>();

    for(int i = 0; i < n; i++)
    {

        // String to create each substring
        string pp = "";

        for(int j = i; j < i + k; j++)
        {
            if (j >= n)
                break;

            pp += st[j];

            // Adding to set
            z.Add(pp);
        }
    }

    // Converting set into a list
    ArrayList fin = new ArrayList();

    foreach(string s in z)
    {
        fin.Add(s);
    }

    // Sorting the strings int the list
    // into lexicographical order
    fin.Sort();

    // Printing kth substring
    Console.Write(fin[k - 1]);
}

// Driver Code
public static void Main(string[] args)
{
    string s = "geeksforgeeks";
    int k = 5;
    int n = s.Length;

    kThLexString(s, k, n);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

function kThLexString(st, k, n)
{

    // Set to store the unique substring
    var z = new Set();

    for(var i = 0; i < n; i++)
    {

       // String to create each substring
       var pp = "";

       for(var j = i; j < i + k; j++)
       {
          if (j >= n)
              break;
          pp += st[j];

          // Adding to set
          z.add(pp);
       }
    }

    var fin = [];

    z.forEach(element => {
        fin.push(element);
    });

    fin.sort();

    // Printing kth substring
    document.write( fin[k-1]);
}

// Driver code

var s = "geeksforgeeks";
var k = 5;
var n = s.length;
kThLexString(s, k, n);

</script>
```

**Output:** 

```
eeksf
```