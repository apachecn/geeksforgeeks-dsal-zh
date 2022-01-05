# 给定长度 L 的连续唯一子串

> 原文:[https://www . geeksforgeeks . org/continuous-unique-substrings-with-给定长度-l/](https://www.geeksforgeeks.org/contiguous-unique-substrings-with-the-given-length-l/)

给定一个字符串**字符串**和一个整数 **L** 。任务是从字符串**到字符串**打印所有长度为 **L** 的唯一子字符串。

**示例:**

> **输入:** str = "abca "，L=3
> **输出:**【ABC】【BCA】
> 
> **输入:** str = "aaaa "，L=3
> **输出:**【AAA】

**方法:**
首先生成长度为 **L** 的所有子串，然后使用 set 插入唯一的子串，直到长度为 L，然后打印结果。

以下是上述方法的实现:

## C++

```
// C++ implementation
#include <bits/stdc++.h>
using namespace std;

// Function to print the
// unique sub-string of length n
void result(string s, int n)
{
    // set to store the strings
    unordered_set<string> st;

    for (int i = 0; i < (int)s.size(); i++) {

        string ans = "";
        for (int j = i; j < (int)s.size(); j++) {

            ans += s[j];

            // if the size of the string
            // is equal to 1 then insert
            if (ans.size() == n) {

                // inserting unique
                // sub-string of length L
                st.insert(ans);
                break;
            }
        }
    }

    // Printing the set of strings
    for (auto it : st)
        cout << it << " ";
}

// Driver Code
int main()
{
    string s = "abca";
    int n = 3;

    // Function calling
    result(s, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;
class GFG 
{

// Function to print the
// unique sub-String of length n
static void result(String s, int n)
{
    // set to store the Strings
    HashSet<String> st = new HashSet<String>();

    for (int i = 0; i < (int)s.length(); i++) 
    {
        String ans = "";
        for (int j = i; j < (int)s.length(); j++)
        {
            ans += s.charAt(j);

            // if the size of the String
            // is equal to 1 then insert
            if (ans.length()== n)
            {

                // inserting unique
                // sub-String of length L
                st.add(ans);
                break;
            }
        }
    }

    // Printing the set of Strings
    for (String it : st)
        System.out.print(it + " ");
}

// Driver Code
public static void main(String[] args)
{
    String s = "abca";
    int n = 3;

    // Function calling
    result(s, n);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the above approach 

# Function to print the 
# unique sub-string of length n 
def result(s, n) : 

    # set to store the strings 
    st = set(); 

    for i in range(len(s)) : 

        ans = ""; 
        for j in range(i, len(s)) :

            ans += s[j]; 

            # if the size of the string 
            # is equal to 1 then insert 
            if (len(ans) == n) :

                # inserting unique 
                # sub-string of length L 
                st.add(ans); 
                break; 

    # Printing the set of strings 
    for it in st :
        print(it, end = " "); 

# Driver Code 
if __name__ == "__main__" : 

    s = "abca"; 
    n = 3; 

    # Function calling 
    result(s, n); 

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation for above approach
using System;
using System.Collections.Generic; 

class GFG 
{

// Function to print the
// unique sub-String of length n
static void result(String s, int n)
{
    // set to store the Strings
    HashSet<String> st = new HashSet<String>();

    for (int i = 0; i < s.Length; i++) 
    {
        String ans = "";
        for (int j = i; j < s.Length; j++)
        {
            ans += s[j];

            // if the size of the String
            // is equal to 1 then insert
            if (ans.Length == n)
            {

                // inserting unique
                // sub-String of length L
                st.Add(ans);
                break;
            }
        }
    }

    // Printing the set of Strings
    foreach (String it in st)
        Console.Write(it + " ");
}

// Driver Code
public static void Main(String[] args)
{
    String s = "abca";
    int n = 3;

    // Function calling
    result(s, n);
}
}

// This code is contributed by 29AjayKumar
```

**Output:**

```
bca abc

```