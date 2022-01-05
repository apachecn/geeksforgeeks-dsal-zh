# 所需的最小字符删除量，以使给定字符串的排列成为回文

> 原文:[https://www . geeksforgeeks . org/最小字符移除要求给定字符串的这种排列是回文/](https://www.geeksforgeeks.org/minimum-removal-of-characters-required-such-that-permutation-of-given-string-is-a-palindrome/)

给定由小写字母组成的字符串**字符串**，任务是从给定字符串中找到要删除的最小字符数，以便剩余字符串的任何排列都是一个 [**回文**](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/) 。

**示例:**

> **输入:** str="aba"
> **输出:** 1
> **解释:**去掉‘b’生成回文串“aa”。
> 
> **输入:**“abab”
> **输出:** 0
> **解释:**给定字符串的排列“abba”、“baab”已经是回文了。因此，不需要删除任何字符。
> 
> **输入:**【abab】
> T3】输出: 0

**方法:**按照以下步骤解决问题:

1.  [检查给定的字符串是否已经是回文](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)。如果发现是真的，打印 **0** 。
2.  否则，使用[哈希表](https://www.geeksforgeeks.org/java-util-hashmap-in-java/)计算字符串中每个字符的[频率。](https://www.geeksforgeeks.org/python-frequency-of-each-character-in-string/)
3.  计算奇数频率的字符数并存储在一个变量中，比如 **k** 。
4.  现在需要删除的字符总数为 **k-1** 。因此，打印**k–1**作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if a string
// is palindrome or not
bool IsPalindrome(string& str)
{
    string s = str;

    // Reverse the string
    reverse(str.begin(), str.end());

    // Check if the string is
    // already a palindrome or not
    if (s == str) {

        return true;
    }

    return false;
}

// Function to calculate the minimum
// deletions to make a string palindrome
void CountDeletions(string& str, int len)
{
    if (IsPalindrome(str)) {

        cout << 0 << endl;
        return;
    }

    // Stores the frequencies
    // of each character
    map<char, int> mp;

    // Iterate over the string
    for (int i = 0; i < len; i++) {

        // Update frequency of
        // each character
        mp[str[i]]++;
    }

    int k = 0;

    // Iterate over the map
    for (auto it : mp) {

        // Count characters with
        // odd frequencies
        if (it.second & 1) {
            k++;
        }
    }

    // Print the result
    cout << k - 1 << endl;
}

int main()
{
    string str = "abca";
    int len = str.length();
    CountDeletions(str, len);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

static String str;

static String reverse(String input)
{
  char[] a = input.toCharArray();
  int l, r = a.length - 1;

  for (l = 0; l < r; l++, r--)
  {
    char temp = a[l];
    a[l] = a[r];
    a[r] = temp;
  }
  return String.valueOf(a);
}

// Function to check if a String
// is palindrome or not
static boolean IsPalindrome()
{
  String s = str;

  // Reverse the String
  s = reverse(str);

  // Check if the String is
  // already a palindrome or not
  if (s == str)
  {
    return true;
  }

  return false;
}

// Function to calculate the
// minimum deletions to make
// a String palindrome
static void CountDeletions(int len)
{
  if (IsPalindrome())
  {
    System.out.print(0 + "\n");
    return;
  }

  // Stores the frequencies
  // of each character
  HashMap<Character,
          Integer> mp =
          new HashMap<>();

  // Iterate over the String
  for (int i = 0; i < len; i++)
  {
    // Update frequency of
    // each character
    if(mp.containsKey(str.charAt(i)))
    {
      mp.put(str.charAt(i),
      mp.get(str.charAt(i)) + 1);
    }
    else
    {
      mp.put(str.charAt(i), 1);
    }
  }

  int k = 0;

  // Iterate over the map
  for (Map.Entry<Character,
                 Integer> it :
       mp.entrySet())
  {
    // Count characters with
    // odd frequencies
    if (it.getValue() % 2 == 1)
    {
      k++;
    }
  }

  // Print the result
  System.out.print(k - 1 + "\n");
}

// Driver code
public static void main(String[] args)
{
  str = "abca";
  int len = str.length();
  CountDeletions(len);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach
from collections import defaultdict

# Function to check if a string
# is palindrome or not
def IsPalindrome(str):

    s = str

    # Reverse the string
    s = s[::-1]

    # Check if the string is
    # already a palindrome or not
    if (s == str):
        return True

    return False

# Function to calculate the minimum
# deletions to make a string palindrome
def CountDeletions(str, ln):

    if (IsPalindrome(str)):
        print(0)
        return

    # Stores the frequencies
    # of each character
    mp = defaultdict(lambda : 0)

    # Iterate over the string
    for i in range(ln):

        # Update frequency of
        # each character
        mp[str[i]] += 1

    k = 0

    # Iterate over the map
    for it in mp.keys():

        # Count characters with
        # odd frequencies
        if (mp[it] & 1):
            k += 1

    # Print the result
    print(k - 1)

# Driver code
if __name__ == '__main__':

    str = "abca"

    ln = len(str)

    # Function Call
    CountDeletions(str, ln)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the
// above approach
using System;
using System.Collections.Generic;
class GFG{

static String str;

static String reverse(String input)
{
  char[] a = input.ToCharArray();
  int l, r = a.Length - 1;

  for (l = 0; l < r; l++, r--)
  {
    char temp = a[l];
    a[l] = a[r];
    a[r] = temp;
  }
  return String.Join("", a);
}

// Function to check if
// a String is palindrome 
// or not
static bool IsPalindrome()
{
  String s = str;

  // Reverse the String
  s = reverse(str);

  // Check if the String
  // is already a palindrome
  // or not
  if (s == str)
  {
    return true;
  }

  return false;
}

// Function to calculate the
// minimum deletions to make
// a String palindrome
static void CountDeletions(int len)
{
  if (IsPalindrome())
  {
    Console.Write(0 + "\n");
    return;
  }

  // Stores the frequencies
  // of each character
  Dictionary<char,
             int> mp =
             new Dictionary<char,
                            int>();

  // Iterate over the String
  for (int i = 0; i < len; i++)
  {
    // Update frequency of
    // each character
    if(mp.ContainsKey(str[i]))
    {
      mp[str[i]] = mp[str[i]] + 1;
    }
    else
    {
      mp.Add(str[i], 1);
    }
  }

  int k = 0;

  // Iterate over the map
  foreach (KeyValuePair<char,
                        int> it in mp)
  {
    // Count characters with
    // odd frequencies
    if (it.Value % 2 == 1)
    {
      k++;
    }
  }

  // Print the result
  Console.Write(k - 1 + "\n");
}

// Driver code
public static void Main(String[] args)
{
  str = "abca";
  int len = str.Length;
  CountDeletions(len);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    let str;

    function reverse(input)
    {
      let a = input.split('');
      let l, r = a.length - 1;

      for (l = 0; l < r; l++, r--)
      {
        let temp = a[l];
        a[l] = a[r];
        a[r] = temp;
      }
      return a.join("");
    }

    // Function to check if
    // a String is palindrome
    // or not
    function IsPalindrome()
    {
      let s = str;

      // Reverse the String
      s = reverse(str);

      // Check if the String
      // is already a palindrome
      // or not
      if (s == str)
      {
        return true;
      }

      return false;
    }

    // Function to calculate the
    // minimum deletions to make
    // a String palindrome
    function CountDeletions(len)
    {
      if (IsPalindrome())
      {
        document.write(0 + "</br>");
        return;
      }

      // Stores the frequencies
      // of each character
      let mp = new Map();

      // Iterate over the String
      for (let i = 0; i < len; i++)
      {
        // Update frequency of
        // each character
        if(mp.has(str[i]))
        {
          mp.set(str[i], mp.get(str[i]) + 1);
        }
        else
        {
          mp.set(str[i], 1);
        }
      }

      let k = 0;

      // Iterate over the map
      mp.forEach((values,it)=>{
        if(values % 2 == 1)
        {
            k++;
        }
      })

      // Print the result
      document.write((k - 1) + "</br>");
    }

    str = "abca";
    let len = str.length;
    CountDeletions(len);

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)