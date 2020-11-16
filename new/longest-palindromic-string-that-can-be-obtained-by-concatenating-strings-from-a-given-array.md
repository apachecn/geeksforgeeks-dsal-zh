# 通过连接给定数组中的字符串，可以得到的最长回文字符串

> 原文：[https://www.geeksforgeeks.org/longest-palindromic-string-that-can-be-obtained-by-concatenating-strings-from-a-given-array/](https://www.geeksforgeeks.org/longest-palindromic-string-that-can-be-obtained-by-concatenating-strings-from-a-given-array/)

给定[字符串](https://www.geeksforgeeks.org/string-data-structure/)`S[]`的[数组](https://www.geeksforgeeks.org/array-data-structure/)，该数组由`N`个长度为`M`的不同字符串组成。 任务是通过连接给定数组中的某些字符串来生成最长的[回文字符串](https://www.geeksforgeeks.org/string-palindrome/)。

**示例**：

> **输入**：`N = 4, M = 3, S[] = {"omg", "bbb", "ffd", "gmo"}`
>
> **输出**：`omgbbbgmo`
>
> **说明**：字符串`"omg"`和`"gmo"`彼此相反，而`"bbb"`本身就是回文。 因此，连接`"omg" + "bbb" + "gmo"`会生成最长回文字符串`"omgbbbgmo"`。
> 
> **输入**：`N = 4, M = 3, S[] = {"poy", "fgh", "hgf", "yop"}`
>
> **输出**：`poyfghhgfyop`

**方法**：请按照以下步骤解决问题：

*   初始化[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)，并将给定数组中的每个字符串插入**集合**中。

*   初始化两个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)`left_ans`和`right_ans`，以跟踪获得的[回文串](https://www.geeksforgeeks.org/string-palindrome/)。

*   现在，[遍历字符串数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，并检查在集合中是否存在相反的内容。

*   如果发现是正确的，则将其中一个字符串插入`left_ans`，将另一个字符串插入`right_ans`，[从集合中删除两个字符串](https://www.geeksforgeeks.org/unordered_set-erase-function-in-c-stl/)。 避免重复。

*   [如果字符串是回文](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)，并且在[集合](https://www.geeksforgeeks.org/set-in-java/)中不存在该字符串对，则需要将该字符串附加到结果字符串的中间。

*   打印结果字符串。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach 
#include <bits/stdc++.h> 
using namespace std; 

void max_len(string s[], int N, int M) 
{ 
    // Stores the distinct strings 
    // from the given array 
    unordered_set<string> set_str; 

    // Insert the strings into set 
    for (int i = 0; i < N; i++) { 

        set_str.insert(s[i]); 
    } 

    // Stores the left and right 
    // substrings of the given string 
    vector<string> left_ans, right_ans; 

    // Stores the middle substring 
    string mid; 

    // Traverse the array of strings 
    for (int i = 0; i < N; i++) { 

        string t = s[i]; 

        // Reverse the current string 
        reverse(t.begin(), t.end()); 

        // Checking if the string is 
        // itself a palindrome or not 
        if (t == s[i]) { 

            mid = t; 
        } 

        // Check if the reverse of the 
        // string is present or not 
        else if (set_str.find(t) 
                != set_str.end()) { 

            // Append to the left substring 
            left_ans.push_back(s[i]); 

            // Append to the right substring 
            right_ans.push_back(t); 

            // Erase both the strings 
            // from the set 
            set_str.erase(s[i]); 
            set_str.erase(t); 
        } 
    } 

    // Print the left substring 
    for (auto x : left_ans) { 

        cout << x; 
    } 

    // Print the middle substring 
    cout << mid; 

    reverse(right_ans.begin(), 
            right_ans.end()); 

    // Print the right substring 
    for (auto x : right_ans) { 

        cout << x; 
    } 
} 

// Driver Code 
int main() 
{ 
    int N = 4, M = 3; 
    string s[] = { "omg", "bbb", 
                "ffd", "gmo" }; 

    // Function Call 
    max_len(s, N, M); 

    return 0; 
} 

```

## Java

```java

// Java program for the 
// above approach 
import java.util.*;
class GFG{ 

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

static void max_len(String s[], 
                    int N, int M) 
{ 
  // Stores the distinct Strings 
  // from the given array 
  HashSet<String> set_str = 
          new HashSet<>(); 

  // Insert the Strings 
  // into set 
  for (int i = 0; i < N; i++) 
  { 
    set_str.add(s[i]); 
  } 

  // Stores the left and right 
  // subStrings of the given String 
  Vector<String> left_ans =
                 new Vector<>();
  Vector<String> right_ans = 
                 new Vector<>(); 

  // Stores the middle 
  // subString 
  String mid = ""; 

  // Traverse the array 
  // of Strings 
  for (int i = 0; i < N; i++) 
  {
    String t = s[i]; 

    // Reverse the current 
    // String 
    t = reverse(t);

    // Checking if the String is 
    // itself a palindrome or not 
    if (t == s[i]) 
    {
      mid = t; 
    } 

    // Check if the reverse of the 
    // String is present or not 
    else if (set_str.contains(t)) 
    {
      // Append to the left 
      // subString 
      left_ans.add(s[i]); 

      // Append to the right 
      // subString 
      right_ans.add(t); 

      // Erase both the Strings 
      // from the set 
      set_str.remove(s[i]); 
      set_str.remove(t); 
    } 
  } 

  // Print the left subString 
  for (String x : left_ans) 
  {
    System.out.print(x); 
  } 

  // Print the middle 
  // subString 
  System.out.print(mid); 

  Collections.reverse(right_ans);
  // Print the right subString 

  for (String x : right_ans) 
  {
    System.out.print(x); 
  } 
} 

// Driver Code 
public static void main(String[] args) 
{ 
  int N = 4, M = 3; 
  String s[] = {"omg", "bbb", 
                "ffd", "gmo"}; 

  // Function Call 
  max_len(s, N, M); 
} 
} 

// This code is contributed by Rajput-Ji

```

## Python3

```py

# Python3 program for the above approach
def max_len(s, N, M):

    # Stores the distinct strings
    # from the given array
    set_str = {}

    # Insert the strings into set
    for i in s:
        set_str[i] = 1

    # Stores the left and right
    # substrings of the given string
    left_ans, right_ans = [], []

    # Stores the middle substring
    mid = ""

    # Traverse the array of strings
    for i in range(N):
        t = s[i]

        # Reverse the current string
        t = t[::-1]

        # Checking if the is
        # itself a palindrome or not
        if (t == s[i]):
            mid = t

        # Check if the reverse of the
        # is present or not
        elif (t in set_str):

            # Append to the left substring
            left_ans.append(s[i])

            # Append to the right substring
            right_ans.append(t)

            # Erase both the strings
            # from the set
            del set_str[s[i]]
            del set_str[t]

    # Print the left substring
    for x in left_ans:
        print(x, end = "")

    # Print the middle substring
    print(mid, end = "")

    right_ans = right_ans[::-1]

    # Print the right substring
    for x in right_ans:
        print(x, end = "")

# Driver Code
if __name__ == '__main__':

    N = 4
    M = 3

    s = [ "omg", "bbb", "ffd", "gmo"]

    # Function call
    max_len(s, N, M)

# This code is contributed by mohit kumar 29

```

## C#

```cs

// C# program for the 
// above approach 
using System;
using System.Collections.Generic;
class GFG{ 

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

static void max_len(String []s, 
                    int N, int M) 
{ 
  // Stores the distinct Strings 
  // from the given array 
  HashSet<String> set_str = 
          new HashSet<String>(); 

  // Insert the Strings 
  // into set 
  for (int i = 0; i < N; i++) 
  { 
    set_str.Add(s[i]); 
  } 

  // Stores the left and right 
  // subStrings of the given String 
  List<String> left_ans =
       new List<String>();
  List<String> right_ans = 
       new List<String>(); 

  // Stores the middle 
  // subString 
  String mid = ""; 

  // Traverse the array 
  // of Strings 
  for (int i = 0; i < N; i++) 
  {
    String t = s[i]; 

    // Reverse the current 
    // String 
    t = reverse(t);

    // Checking if the String is 
    // itself a palindrome or not 
    if (t == s[i]) 
    {
      mid = t; 
    } 

    // Check if the reverse of the 
    // String is present or not 
    else if (set_str.Contains(t)) 
    {
      // Append to the left 
      // subString 
      left_ans.Add(s[i]); 

      // Append to the right 
      // subString 
      right_ans.Add(t); 

      // Erase both the Strings 
      // from the set 
      set_str.Remove(s[i]); 
      set_str.Remove(t); 
    } 
  } 

  // Print the left subString 
  foreach (String x in left_ans) 
  {
    Console.Write(x); 
  } 

  // Print the middle 
  // subString 
  Console.Write(mid); 

  right_ans.Reverse();
  // Print the right subString 

  foreach (String x in right_ans) 
  {
    Console.Write(x); 
  } 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
  int N = 4, M = 3; 
  String []s = {"omg", "bbb", 
                "ffd", "gmo"}; 

  // Function Call 
  max_len(s, N, M); 
} 
} 

// This code is contributed by 29AjayKumar

```

**输出**：

```
omgbbbgmo

```

**时间复杂度**：`O(N * M)`。

**辅助空间**：`O(N * M)`。



* * *

* * *



