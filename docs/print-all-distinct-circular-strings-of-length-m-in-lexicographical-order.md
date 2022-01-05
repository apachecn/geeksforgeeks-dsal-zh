# 按照字典顺序打印所有长度为 M 的不同圆形字符串

> 原文:[https://www . geeksforgeeks . org/print-all-distinct-circular-长度为 m 的字符串按词典顺序/](https://www.geeksforgeeks.org/print-all-distinct-circular-strings-of-length-m-in-lexicographical-order/)

给定一个字符串和一个整数 M，按照字典顺序打印长度为 M 的所有不同的循环字符串。

**示例:**

> **输入:**str = " baaa "，M = 3
> **输出:** aaa aab aba baa
> 长度为 3 的所有可能的圆形子串都是“baa”“AAA”“AAA”“aab”“ABA”
> 在 6 个中，4 个是不同的，字典顺序是 aaa aab aba baa
> 
> **输入:** str = "saurav "，M = 3
> **输出:** aura avsa ravs saur urav vsau
> 所有可能的长度为 4 的圆形子串都是 saur aura urav ravs avsa vsau。
> 所有的子串都是截然不同的，字典顺序是 aura avsa ravs saur urav vsau。

**方法:**使用[子串](https://www.geeksforgeeks.org/substring-in-cpp/)函数来解决问题。首先将字符串附加到自身。迭代字符串的长度以生成长度为 m 的所有可能的子字符串。在 C++中使用[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)来存储长度为 4 的所有不同子字符串，默认情况下，集合按照字典顺序存储其所有元素。生成所有字符串后，从头开始打印集合中的元素。

下面是上述方法的实现:

## C++

```
// C++ program to print all
// distinct circular strings
// of length M in lexicographical order
#include <bits/stdc++.h>
using namespace std;

// Function to print all the distinct substrings
// in lexicographical order
void printStrings(string s, int l, int m)
{
    // stores all the distinct substrings
    set<string> c;

    // Append the string to self
    s = s + s;

    // Iterate over the length to generate
    // all substrings of length m
    for (int i = 0; i < l; i++) {

        // insert the substring of length m
        // in the set
        c.insert(s.substr(i, m));
    }

    // prints all the distinct circular
    // substrings  of length m
    while (!c.empty()) {

        // Prints the substring
        cout << *c.begin() << " ";

        // erases the beginning element after
        // printing
        c.erase(c.begin());
    }
}

// Driver code
int main()
{
    string str = "saurav";
    int N = str.length();
    int M = 4;

    printStrings(str, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all
// distinct circular strings
// of length M in lexicographical order
import java.util.*;

class GFG
{

// Function to print all the distinct substrings
// in lexicographical order
static void printStrings(String s, int l, int m)
{
    // stores all the distinct substrings
    Set<String> c = new LinkedHashSet<>();

    // Append the string to self
    s = s + s;

    // Iterate over the length to generate
    // all substrings of length m
    for (int i = 0; i < l; i++)
    {

        // insert the substring of length m
        // in the set
            c.add(s.substring(i, i+m));
    }

    // prints all the distinct circular
    // substrings of length m
    Iterator itr = c.iterator();
    while (itr.hasNext())
    {

        // Prints the substring
        String a =(String) itr.next();
        System.out.print(a+" ");

    }
    c.clear();
}

// Driver code
public static void main(String[] args)
{
    String str = "saurav";
    int N = str.length();
    int M = 4;

    printStrings(str, N, M);
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python program to print all
# distinct circular strings
# of length M in lexicographical order

# Function to print all the distinct substrings
# in lexicographical order
def printStrings(s, l, m):

    # stores all the distinct substrings
    c = set()

    # Append the string to self
    s = s+s

    # Iterate over the length to generate
    # all substrings of length m
    for i in range(l):

        # insert the substring of length m
        # in the set
        c.add(s[i:i+m])

    # prints all the distinct circular
    # substrings of length m
    for i in c:

        # Prints the substring
        print(i, end=" ")

# Driver code
if __name__ == "__main__":

    string = "saurav"
    N = len(string)
    M = 4

    printStrings(string, N, M)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to print all
// distinct circular strings
// of length M in lexicographical order
using System;
using System.Collections.Generic;

class GFG
{
    // Function to print all the distinct substrings
    // in lexicographical order
    static void printStrings(String s, int l, int m)
    {
        // stores all the distinct substrings
        HashSet<string> c = new HashSet<string>();

        // Append the string to self
        s = s + s;

        // Iterate over the length to generate
        // all substrings of length m
        for (int i = 0; i < l; i++)
        {
            // insert the substring of length m
            // in the set
            c.Add(s.Substring(i, m));
        }

        // prints all the distinct circular
        // substrings of length m
        foreach (string i in c)
        {
            string a = (string)i;
            Console.Write(a + " ");
        }
        c.Clear();
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "saurav";
        int N = str.Length;
        int M = 4;

        printStrings(str, N, M);
    }
}

// This code contributed by
// sanjeev2552
```

## java 描述语言

```
<script>

// Javascript program to print all
// distinct circular strings
// of length M in lexicographical order

// Function to print all the distinct substrings
// in lexicographical order
function printStrings(s, l, m)
{

    // Stores all the distinct substrings
    var c = new Set();

    // Append the string to self
    s = s + s;

    // Iterate over the length to generate
    // all substrings of length m
    for(var i = 0; i < l; i++)
    {

        // Insert the substring of length m
        // in the set
        c.add(s.substring(i, i + m));
    }

    // Prints all the distinct circular
    // substrings  of length m
    while (c.size != 0)
    {

        var tmp = [...c].sort()[0];

        // Prints the substring
        document.write( tmp + " ");

        // Erases the beginning element after
        // printing
        c.delete(tmp);
    }
}

// Driver code
var str = "saurav";
var N = str.length;
var M = 4;

printStrings(str, N, M);

// This code is contributed by itsok

</script>
```

**Output:** 

```
aura avsa ravs saur urav vsau
```

**时间复杂度** : O(N*M)，其中 N 为字符串的长度。