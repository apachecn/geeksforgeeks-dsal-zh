# 字符串

> 原文：[https://www.geeksforgeeks.org/maximum-length-substring-with-highest-frequency-in-a-string/](https://www.geeksforgeeks.org/maximum-length-substring-with-highest-frequency-in-a-string/)

中频率最高的最大子字符串

给定一个字符串。 任务是找到最大长度的最大出现子字符串。 这些情况可能会重叠。

**示例**：

```
Input: str = "abab"
Output: ab
"a", "b", "ab" are occur 2 times. But, "ab" has maximum length

Input: str = "abcd"
Output: a

```

**方法**：这个想法是使用[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)存储每个子串的频率，并打印出最大频率和最大长度的子串。

以下是上述方法的实现：

## C++

```cpp

// C++ program to find maximum 
// occurred substring of a string 
#include <bits/stdc++.h> 
using namespace std; 

// function to return maximum 
// occurred substring of a string 
string MaxFreq(string str) 
{ 
    // size of the string 
    int n = str.size(); 

    unordered_map<string, int> m; 

    for (int i = 0; i < n; i++) { 
        string s = ""; 
        for (int j = i; j < n; j++) { 
            s += str[j]; 
            m[s]++; 
        } 
    } 

    // to store maximum frequency 
    int maxi = 0; 

    // to store string which has maximum frequency 
    string s; 
    for (auto i = m.begin(); i != m.end(); i++) { 
        if (i->second > maxi) { 
            maxi = i->second; 
            s = i->first; 
        } 
        else if (i->second == maxi) { 
            string ss = i->first; 
            if (ss.size() > s.size()) 
                s = ss; 
        } 
    } 

    // return substring which has maximum frequency 
    return s; 
} 

// Driver program 
int main() 
{ 
    string str = "ababecdecd"; 

    // function call 
    cout << MaxFreq(str); 

    return 0; 
} 

```

## Java

```java

// Java program to find maximum 
// occurred subString of a String 
import java.util.*;
class GFG{ 

// Function to return maximum 
// occurred subString of a String 
static String MaxFreq(String str) 
{ 
  // Size of the String 
  int n = str.length(); 

  Map<String, 
      Integer> mp = new HashMap<String, 
                                Integer>(); 

  for (int i = 0; i < n; i++) 
  { 
    String s = ""; 
    for (int j = i; j < n; j++) 
    { 
      s += str.charAt(j); 
      if(mp.containsKey(s))
      {
        mp.put(s, mp.get(s) + 1);
      }
      else
      {
        mp.put(s, 1);
      }
    } 
  } 

  // To store maximum frequency 
  int maxi = 0; 

  // To store String which 
  // has maximum frequency 
  String s = ""; 
  for (Map.Entry<String, 
                 Integer> i : mp.entrySet())
  { 
    if (i.getValue() > maxi) 
    { 
      maxi = i.getValue(); 
      s = i.getKey(); 
    } 
    else if (i.getValue() == maxi) 
    { 
      String ss = i.getKey(); 
      if (ss.length() > s.length()) 
        s = ss; 
    } 
  } 

  // Return subString which 
  // has maximum frequency 
  return s; 
} 

// Driver code
public static void main(String[] args) 
{ 
  String str = "ababecdecd"; 

  // Function call 
  System.out.print(MaxFreq(str)); 
} 
} 

// This code is contributed by shikhasingrajput

```

## Python3

```py

# Python3 program to find maximum 
# occured of a string 

# function to return maximum occurred 
# substring of a string 
def MaxFreq(s): 

    # size of string 
    n = len(s) 

    m = dict() 

    for i in range(n): 
        strng = '' 
        for j in range(i, n): 
            strng += s[j] 
            if strng in m.keys(): 
                m[strng] += 1
            else: 
                m[strng] = 1

    # to store maximum freqency 
    maxi = 0

    # To store string which has 
    # maximum frequency 
    maxi_str = '' 

    for i in m: 
        if m[i] > maxi: 
            maxi = m[i] 
            maxi_str = i 
        elif m[i] == maxi: 
            ss = i 
            if len(ss) > len(maxi_str): 
                maxi_str = ss 

    # return substring which has maximum freq 
    return maxi_str 

# Driver code 
strng = "ababecdecd"

print(MaxFreq(strng)) 

# This code is contributed by Mohit kumar 29     

```

## C#

```cs

// C# program to find maximum 
// occurred substring of a string 
using System; 
using System.Collections.Generic;

class GFG{ 

// Function to return maximum
// occurred substring of a string
static string MaxFreq(string str)
{

    // Size of the string
    int n = str.Length;

    Dictionary<string, 
               int> m = new Dictionary<string,
                                       int>();

    for(int i = 0; i < n; i++)
    {
        string sp = "";
        for(int j = i; j < n; j++)
        {
            sp += str[j];
            if(m.ContainsKey(sp))
            {
                m[sp]++;
            }
            else
            {
                m[sp] = 1; 
            }
        }
    }

    // To store maximum frequency
    int maxi = 0;

    // To store string which has maximum frequency
    string s = "";

    foreach(KeyValuePair<string, int> i in m) 
    { 
        if (i.Value > maxi)
        {
            maxi = i.Value;
            s = i.Key;
        }
        else if (i.Value == maxi)
        {
            string ss = i.Key;
            if (ss.Length > s.Length)
                s = ss;
        }
    } 

    // Return substring which has
    // maximum frequency
    return s;
}

// Driver Code 
public static void Main(string[] args) 
{ 
    string str = "ababecdecd";

    // Function call
    Console.Write(MaxFreq(str));
}
} 

// This code is contributed by rutvik_56

```

**输出**： 

```
ecd

```



* * *

* * *



