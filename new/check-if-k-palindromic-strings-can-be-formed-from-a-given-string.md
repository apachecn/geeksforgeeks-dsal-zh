# 检查是否可以从给定的字符串中生成`K`个回文字符串

> 原文：[https://www.geeksforgeeks.org/check-if-k-palindromic-strings-can-be-formed-from-a-given-string/](https://www.geeksforgeeks.org/check-if-k-palindromic-strings-can-be-formed-from-a-given-string/)

给定大小为`N`的字符串`S`和整数`K`，任务是确定是否可以安排字符串的字符以同时显示`K`个[回文字符串](https://www.geeksforgeeks.org/string-palindrome/)。

**示例**：

> **输入**：`S = "annabelle", K = 2`
>
> **输出**：`Yes`
>
> **说明**：
>
> 字符串`S`的所有字符都可以是回文，分别为`"elble"`和`"anna"`。
>
> **输入**：`S = "abcd", K = 4`
>
> **输出**：`Yes`
>
> **说明**：
>
> 将以下字符串的所有字符分割为单个字符。

**方法**

*   如果每个字符的[频率是偶数](https://www.geeksforgeeks.org/python-frequency-of-each-character-in-string/)，并且`K`在 1 和`N`之间，则总是有可能生成`K`个回文字符串。

*   但是，如果有一些字符（例如**奇数计数**）具有奇数频率，则`K`必须位于奇数计数和`N`之间，以使`K`个回文字符串成为可能。

因此，请按照以下步骤解决问题：

如果`K`超过字符串的长度，请直接打印`No`。

1.  将所有字符的频率存储在[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。

2.  计算具有奇数频率的字符数。

3.  如果计数小于给定的`K`，则打印`No`。 否则，打印`Yes`。

下面是上述方法的实现：

## C++

```cpp

// C++ program to check 
// whether the string is 
// K palindrome or not 
#include <iostream> 
#include <map> 
using namespace std; 

// function to check 
// whether the string is 
// K palindrome or not 
bool can_Construct(string S, int K) 
{ 
    // map to frequency of character 
    map<int, int> m; 

    int i = 0, j = 0, p = 0; 

    // Check when k is given 
    // as same as length of string 
    if (S.length() == K) { 
        return true; 
    } 

    // iterator for map 
    map<int, int>::iterator h; 

    // stroing the frequency of every 
    // character in map 
    for (i = 0; i < S.length(); i++) { 
        m[S[i]] = m[S[i]] + 1; 
    } 

    // if K is greater than size 
    // of string then return false 
    if (K > S.length()) { 
        return false; 
    } 

    else { 

        // check that number of character 
        // having the odd frequency 
        for (h = m.begin(); h != m.end(); h++) { 

            if (m[h->first] % 2 != 0) { 
                p = p + 1; 
            } 
        } 
    } 

    // if k is less than number of odd 
    // frequecny character then it is 
    // again false other wise true 
    if (K < p) { 
        return false; 
    } 

    return true; 
} 

// Driver code 
int main() 
{ 
    string S = "annabelle"; 
    int K = 4; 

    if (can_Construct(S, K)) { 
        cout << "Yes"; 
    } 
    else { 
        cout << "No"; 
    } 
} 

```

## Java

```java

// Java program to check 
// whether the string is 
// K palindrome or not 
import java.util.*;

class GFG{

// Function to check whether 
// the string is K palindrome or not 
static boolean can_Construct(String S, int K)
{ 

    // Map to frequency of character 
    Map<Character, Integer> m = new HashMap<>(); 

    int p = 0;

    // Check when k is given 
    // as same as length of string 
    if (S.length() == K) 
        return true;

    // Stroing the frequency of every 
    // character in map 
    for(int i = 0; i < S.length(); i++)
        m.put(S.charAt(i),
              m.getOrDefault(S.charAt(i), 0) + 1);

    // If K is greater than size 
    // of then return false 
    if (K > S.length()) 
        return false;

    else
    { 

        // Check that number of character 
        // having the odd frequency 
        for(Integer h : m.values())
        {
            if (h % 2 != 0) 
                p = p + 1;
        }
    }

    // If k is less than number of odd 
    // frequecny character then it is 
    // again false otherwise true 
    if (K < p) 
        return false;

    return true;
}

// Driver Code
public static void main (String[] args)
{
    String S = "annabelle";
    int K = 4;

    if (can_Construct(S, K))
        System.out.println("Yes"); 
    else
        System.out.println("No");
}
}

// This code is contributed by offbeat

```

## Python3

```py

# Python3 program to check whether 
# the is K palindrome or not 

# Function to check whether 
# the is K palindrome or not 
def can_Construct(S, K): 

    # map to frequency of character 
    m = dict() 
    p = 0

    # Check when k is given 
    # as same as length of string 
    if (len(S) == K): 
        return True

    # Stroing the frequency of every 
    # character in map 
    for i in S: 
        m[i] = m.get(i, 0) + 1

    # If K is greater than size 
    # of then return false 
    if (K > len(S)): 
        return False

    else: 

        # Check that number of character 
        # having the odd frequency 
        for h in m: 
            if (m[h] % 2 != 0): 
                p = p + 1

    # If k is less than number of odd 
    # frequecny character then it is 
    # again false otherwise true 
    if (K < p): 
        return False

    return True

# Driver code 
if __name__ == '__main__': 

    S = "annabelle"
    K = 4

    if (can_Construct(S, K)): 
        print("Yes") 
    else: 
        print("No") 

# This code is contributed by mohit kumar 29 

```

## C#

```cs

// C# program to check 
// whether the string is 
// K palindrome or not 
using System;
using System.Collections.Generic;
class GFG{

// Function to check whether 
// the string is K palindrome or not 
static bool can_Construct(String S, 
                          int K)
{     
  // Map to frequency of character 
  Dictionary<char, 
             int> m = new Dictionary<char, 
                                     int>(); 
  int p = 0;

  // Check when k is given 
  // as same as length of string 
  if (S.Length == K) 
    return true;

  // Stroing the frequency of every 
  // character in map 
  for(int i = 0; i < S.Length; i++)
    if(!m.ContainsKey(S[i]))
      m.Add(S[i], 1);
  else
    m[S[i]] = m[S[i]] + 1;

  // If K is greater than size 
  // of then return false 
  if (K > S.Length) 
    return false;

  else
  { 
    // Check that number of character 
    // having the odd frequency 
    foreach(int h in m.Values)
    {
      if (h % 2 != 0) 
        p = p + 1;
    }
  }

  // If k is less than number of odd 
  // frequecny character then it is 
  // again false otherwise true 
  if (K < p) 
    return false;

  return true;
}

// Driver Code
public static void Main(String[] args)
{
  String S = "annabelle";
  int K = 4;
  if (can_Construct(S, K))
    Console.WriteLine("Yes"); 
  else
    Console.WriteLine("No");
}
}

// This code is contributed by shikhasingrajput

```

**输出**： 

```
Yes

```

**时间复杂度**：`O(n)`。

**辅助空间**：`O(n)`。



* * *

* * *



