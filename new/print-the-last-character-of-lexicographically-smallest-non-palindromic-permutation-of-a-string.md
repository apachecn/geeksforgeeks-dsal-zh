# 打印字符串的按字典顺序最小的非回文排列的最后一个字符

> 原文：[https://www.geeksforgeeks.org/print-the-last-character-of-lexicographically-smallest-non-palindromic-permutation-of-a-string/](https://www.geeksforgeeks.org/print-the-last-character-of-lexicographically-smallest-non-palindromic-permutation-of-a-string/)

给定[字符串](https://www.geeksforgeeks.org/string-data-structure/) **str** ，任务是打印给定字符串的字典最小的[非回文排列的最后一个字符。 如果不存在这样的排列，请打印**“ -1”** 。](https://www.geeksforgeeks.org/make-the-string-lexicographically-smallest-non-palindromic-by-replacing-exactly-one-character/)

**示例**：

> **输入**：str =“ deepqvu”
> **输出**：v
> **说明**：字符串“ deepquv”是字典上最小的排列，并非 回文。
> 因此，最后一个字符是 **v** 。
> 
> **输入**：str =“ zyxaaabb”
> **输出**：z
> **说明**：字符串“ aaabbxyz”是按字典顺序排列的最小排列，并非 回文。
> 因此，最后一个字符是 **z** 。

**天真的方法**：解决该问题的最简单方法是[生成给定字符串](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)的所有可能排列，并针对每个排列检查它是否是回文集。 在所有获得的非回文排列中，按字典顺序打印最小的排列的最后一个字符。 请按照以下步骤操作：

1.  [对给定的字符串](https://www.geeksforgeeks.org/sort-string-characters/) **str** 进行排序。

2.  使用函数 [next_permutation（）](https://www.geeksforgeeks.org/stdnext_permutation-prev_permutation-c/)检查回文的字符串的所有后续排列。

3.  如果存在**非回文**的任何排列，则打印其最后一个字符。

4.  否则，打印**“ -1”。**

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check whether a string
// s is a palindrome or not
bool isPalin(string s, int N)
{
    // Traverse the string
    for (int i = 0; i < N; i++) {

        // If unequal character
        if (s[i] != s[N - i - 1]) {
            return false;
        }
    }

    return true;
}

// Function to find the smallest
// non-palindromic lexicographic
// permutation of string s
void lexicographicSmallestString(
    string s, int N)
{
    // Base Case
    if (N == 1) {
        cout << "-1";
    }

    // Sort the given string
    sort(s.begin(), s.end());

    int flag = 0;

    // If the formed string is
    // non palindromic
    if (isPalin(s, N) == false)
        flag = 1;

    if (!flag) {

        // Check for all permutations
        while (next_permutation(s.begin(),
                                s.end())) {

            // Check palindromic
            if (isPalin(s, N) == false) {
                flag = 1;
                break;
            }
        }
    }

    // If non palindromic string found
    // print its last character
    if (flag == 1) {
        int lastChar = s.size() - 1;
        cout << s[lastChar] << ' ';
    }

    // Otherwise, print "-1"
    else {
        cout << "-1";
    }
}

// Driver Code
int main()
{
    // Given string str
    string str = "deepqvu";

    // Length of the string
    int N = str.length();

    // Function Call
    lexicographicSmallestString(str, N);

    return 0;
}

```

## Java

```java

// Java program for the 
// above approach
import java.util.*;
class GFG{

// Function to check whether 
// a String s is a palindrome 
// or not
static boolean isPalin(String s, 
                       int N)
{
  // Traverse the String
  for (int i = 0; i < N; i++) 
  {
    // If unequal character
    if (s.charAt(i) != 
        s.charAt(N - i - 1)) 
    {
      return false;
    }
  }

  return true;
}

static boolean next_permutation(char[] p) 
{
  for (int a = p.length - 2; 
           a >= 0; --a)
    if (p[a] < p[a + 1])
      for (int b = p.length - 1;; --b)
        if (p[b] > p[a]) 
        {
          char t = p[a];
          p[a] = p[b];
          p[b] = t;
          for (++a, b = p.length - 1; 
                 a < b; ++a, --b) 
          {
            t = p[a];
            p[a] = p[b];
            p[b] = t;
          }

          return true;
        }

  return false;
}

//Method to sort a string alphabetically 
static String sortString(String inputString) 
{ 
  // convert input string 
  // to char array 
  char tempArray[] = 
       inputString.toCharArray(); 

  // Sort tempArray 
  Arrays.sort(tempArray); 

  // Return new sorted string 
  return new String(tempArray); 
}  

// Function to find the smallest
// non-palindromic lexicographic
// permutation of String s
static void lexicographicSmallestString(String s, 
                                        int N)
{
  // Base Case
  if (N == 1) 
  {
    System.out.print("-1");
  }

  // Sort the given String
  s =  sortString(s);

  int flag = 0;

  // If the formed String is
  // non palindromic
  if (isPalin(s, N) == false)
    flag = 1;

  if (flag != 0) 
  {
    // Check for all permutations
    while (next_permutation(s.toCharArray())) 
    {
      // Check palindromic
      if (isPalin(s, N) == false) 
      {
        flag = 1;
        break;
      }
    }
  }

  // If non palindromic String found
  // print its last character
  if (flag == 1) 
  {
    int lastChar = s.length() - 1;
    System.out.print(s.charAt(lastChar) + " ");
  }

  // Otherwise, print "-1"
  else
  {
    System.out.print("-1");
  }
}

// Driver Code
public static void main(String[] args)
{
  // Given String str
  String str = "deepqvu";

  // Length of the String
  int N = str.length();

  // Function Call
  lexicographicSmallestString(str, N);
}
}

// This code is contributed by Rajput-Ji

```

## C#

```cs

// C# program for the 
// above approach
using System;
class GFG{

// Function to check whether 
// a String s is a palindrome 
// or not
static bool isPalin(String s, 
                    int N)
{
  // Traverse the String
  for (int i = 0; i < N; i++) 
  {
    // If unequal character
    if (s[i] != 
        s[N - i - 1]) 
    {
      return false;
    }
  }

  return true;
}

static bool next_permutation(char[] p) 
{
  for (int a = p.Length - 2; 
           a >= 0; --a)
    if (p[a] < p[a + 1])
      for (int b = p.Length - 1;; --b)
        if (p[b] > p[a]) 
        {
          char t = p[a];
          p[a] = p[b];
          p[b] = t;
          for (++a, b = p.Length - 1; 
                 a < b; ++a, --b) 
          {
            t = p[a];
            p[a] = p[b];
            p[b] = t;
          }

          return true;
        }

  return false;
}

//Method to sort a string alphabetically 
static String sortString(String inputString) 
{ 
  // convert input string 
  // to char array 
  char []tempArray = 
       inputString.ToCharArray(); 

  // Sort tempArray 
  Array.Sort(tempArray); 

  // Return new sorted string 
  return new String(tempArray); 
}  

// Function to find the smallest
// non-palindromic lexicographic
// permutation of String s
static void lexicographicSmallestString(String s, 
                                        int N)
{
  // Base Case
  if (N == 1) 
  {
    Console.Write("-1");
  }

  // Sort the given String
  s =  sortString(s);

  int flag = 0;

  // If the formed String is
  // non palindromic
  if (isPalin(s, N) == false)
    flag = 1;

  if (flag != 0) 
  {
    // Check for all permutations
    while (next_permutation(s.ToCharArray())) 
    {
      // Check palindromic
      if (isPalin(s, N) == false) 
      {
        flag = 1;
        break;
      }
    }
  }

  // If non palindromic String found
  // print its last character
  if (flag == 1) 
  {
    int lastChar = s.Length - 1;
    Console.Write(s[lastChar] + " ");
  }

  // Otherwise, print "-1"
  else
  {
    Console.Write("-1");
  }
}

// Driver Code
public static void Main(String[] args)
{
  // Given String str
  String str = "deepqvu";

  // Length of the String
  int N = str.Length;

  // Function Call
  lexicographicSmallestString(str, N);
}
}

// This code is contributed by Amit Katiyar

```

**Output**

```
v 
```

***时间复杂度**：O（N * N！）*

***辅助空间**：O（1）*

**有效方法**：为了优化上述方法，其思想是存储给定字符串 **str** 的每个字符的[频率。 如果所有字符都相同，则打印**“ -1”** 。 否则，打印给定字符串 **str** 的最大字符。](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest non
// palindromic lexicographic string
void lexicographicSmallestString(
    string s, int N)
{
    // Stores the frequency of each
    // character of the string s
    map<char, int> M;

    // Traverse the string
    for (char ch : s) {
        M[ch]++;
    }

    // If there is only one element
    if (M.size() == 1) {
        cout << "-1";
    }

    // Otherwise
    else {
        auto it = M.rbegin();
        cout << it->first;
    }
}

// Driver Code
int main()
{
    // Given string str
    string str = "deepqvu";

    // Length of the string
    int N = str.length();

    // Function Call
    lexicographicSmallestString(str, N);

    return 0;
}

```

## Python3

```py

# Python3 program for the above approach

# Function to find the smallest non
# palindromic lexicographic string
def lexicographicSmallestString(s, N):

    # Stores the frequency of each
    # character of the s
    M = {}

    # Traverse the string
    for ch in s:
        M[ch] = M.get(ch, 0) + 1

    # If there is only one element
    if len(M) == 1:
        print("-1")

    # Otherwise
    else:
        x = list(M.keys())[-2]
        print(x)

# Driver Code
if __name__ == '__main__':

    # Given str
    str = "deepqvu"

    # Length of the string
    N = len(str)

    # Function call
    lexicographicSmallestString(str, N)

# This code is contributed by mohit kumar 29

```

**Output**

```
v
```

***时间复杂度**：O（N）*

***辅助空间**：O（26）*



* * *

* * *



