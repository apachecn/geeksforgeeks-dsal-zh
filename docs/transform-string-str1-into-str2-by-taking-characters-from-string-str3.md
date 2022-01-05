# 从字符串 str3

中提取字符，将字符串 str1 转换为 str2

> 原文:[https://www . geesforgeks . org/transform-string-str 1-to-str 2-从字符串中提取字符-str3/](https://www.geeksforgeeks.org/transform-string-str1-into-str2-by-taking-characters-from-string-str3/)

给定三个字符串 **str1，str2 & str3** 。任务是从 **str3** 中取字符，找出字符串 **str1** 是否可以转化为字符串 **str2** 。如果是，则打印“**是”**，否则打印“**否”**。
**示例:**

> **输入:**str 1 =“abyzf”，str 2 =“abgdeyzf”，str 3 =“poqgode”。
> **输出:** YES
> **说明:**
> 从 str3 中删除‘g’并将其插入到 str1 中的‘b’之后，A = "abgyzf "，C="poqode"
> 从 str3 中删除‘d’并将其插入到 str1 中的‘g’之后，A = "abgdyzf "，C="poqoe"
> 从 str3 中删除‘e’并将其插入到 str1 中的‘d’之后，A = "abgdeyzf "，C
> **输入:**A =“abyzf”，B =“abcdyezf”，C =“Popo de”。
> **输出:**否
> **说明:**
> 不可能把 A 变换成 C.

**进场:**这个问题可以用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)解决。

1.  计算字符串 s **tr3** 每个字符的频率。
2.  使用两个指针(例如 str1 的 **i** 和 str2 的 **j** )同时遍历字符串 **str1 & str2** ，并执行以下操作:
    *   如果 **str1** 的**和 **str2** 的 **jth** 索引处的字符相同，则检查下一个字符。**
    *   如果第**个第**索引和第**个第**索引的字符不相同，则检查第**个第【j】个第**个字符的频率，如果第**个字符的频率大于 0 个第**个字符，则递增第**个第**个指针并检查下一对字符。
    *   否则我们无法将弦 **str1** 转换为弦 **str2** 。
3.  经过以上所有的迭代，如果两个指针都分别到达了字符串的末尾，那么 **str1** 可以转换成 **str2。**
4.  否则 str1 不能转换为 str2。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check whether str1 can
// be transformed to str2
void convertString(string str1, string str2,
                   string str3)
{
    // To store the frequency of
    // characters of string str3
    map<char, int> freq;
    for (int i = 0; str3[i]; i++) {
        freq[str3[i]]++;
    }

    // Declare two pointers & flag
    int ptr1 = 0;
    int ptr2 = 0;
    bool flag = true;

    // Traverse both the string and
    // check whether it can be transformed
    while (ptr1 < str1.length()
           && ptr2 < str2.length()) {
        // If both pointers point to same
        // characters increment them
        if (str1[ptr1] == str2[ptr2]) {
            ptr1++;
            ptr2++;
        }

        // If the letters don't match check
        // if we can find it in string C
        else {

            // If the letter is available in
            // string str3, decrement it's
            // frequency & increment the ptr2
            if (freq[str3[ptr2]] > 0) {

                freq[str3[ptr2]]--;
                ptr2++;
            }

            // If letter isn't present in str3[]
            // set the flag to false and break
            else {
                flag = false;
                break;
            }
        }
    }

    // If the flag is true and both pointers
    // points to their end of respective strings
    // then it is possible to transformed str1
    // into str2, otherwise not.
    if (flag && ptr1 == str1.length()
        && ptr2 == str2.length()) {
        cout << "YES" << endl;
    }
    else {
        cout << "NO" << endl;
    }
}

// Driver Code
int main()
{
    string str1 = "abyzfe";
    string str2 = "abcdeyzf";
    string str3 = "popode";

    // Function Call
    convertString(str1, str2, str3);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of
// the above approach 
import java.util.*;
class GFG{

// Function to check whether str1 can
// be transformed to str2
static void convertString(String str1,
                          String str2,
                          String str3)
{
  // To store the frequency of
  // characters of String str3
  HashMap<Character,
          Integer> freq = new HashMap<>();

  for (int i = 0; i<str3.length(); i++)
  {
    if(freq.containsKey(str3.charAt(i)))
      freq.put(str3.charAt(i),
               freq.get(str3.charAt(i)) + 1);
    else
      freq.put(str3.charAt(i), 1);

  }

  // Declare two pointers & flag
  int ptr1 = 0;
  int ptr2 = 0;
  boolean flag = true;

  // Traverse both the String and
  // check whether it can be transformed
  while (ptr1 < str1.length() &&
         ptr2 < str2.length())
  {

    // If both pointers point to same
    // characters increment them
    if (str1.charAt(ptr1) == str2.charAt(ptr2))
    {
      ptr1++;
      ptr2++;
    }

    // If the letters don't match check
    // if we can find it in String C
    else
    {

      // If the letter is available in
      // String str3, decrement it's
      // frequency & increment the ptr2
      if(freq.containsKey(str3.charAt(ptr2)))
        if (freq.get(str3.charAt(ptr2)) > 0)
        {
          freq.put(str3.charAt(ptr2),
                   freq.get(str3.charAt(ptr2)) - 1);
          ptr2++;
        }

      // If letter isn't present in str3[]
      // set the flag to false and break
      else
      {
        flag = false;
        break;
      }
    }
  }

  // If the flag is true and both pointers
  // points to their end of respective Strings
  // then it is possible to transformed str1
  // into str2, otherwise not.
  if (flag && ptr1 == str1.length() &&
      ptr2 == str2.length())
  {
    System.out.print("YES" + "\n");
  }
  else
  {
    System.out.print("NO" + "\n");
  }
}

// Driver Code
public static void main(String[] args)
{
  String str1 = "abyzfe";
  String str2 = "abcdeyzf";
  String str3 = "popode";

  // Function Call
  convertString(str1, str2, str3);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program of the above approach

# Function to check whether str1 can
# be transformed to str2
def convertString(str1, str2, str3):

    # To store the frequency of
    # characters of string str3
    freq = {}

    for i in range(len(str3)):
        if(freq.get(str3[i]) == None):
            freq[str3[i]] = 1
        else:
            freq.get(str3[i], 1)

    # Declare two pointers & flag
    ptr1 = 0
    ptr2 = 0;
    flag = True

    # Traverse both the string and
    # check whether it can be transformed
    while (ptr1 < len(str1) and
           ptr2 < len(str2)):

        # If both pointers point to same
        # characters increment them
        if (str1[ptr1] == str2[ptr2]):
            ptr1 += 1
            ptr2 += 1

        # If the letters don't match check
        # if we can find it in string C
        else:

            # If the letter is available in
            # string str3, decrement it's
            # frequency & increment the ptr2
            if (freq[str3[ptr2]] > 0):
                freq[str3[ptr2]] -= 1
                ptr2 += 1

            # If letter isn't present in str3[]
            # set the flag to false and break
            else:
                flag = False
                break

    # If the flag is true and both pointers
    # points to their end of respective strings
    # then it is possible to transformed str1
    # into str2, otherwise not.
    if (flag and ptr1 == len(str1) and
                 ptr2 == len(str2)):
        print("YES")
    else:
        print("NO")

# Driver Code
if __name__ == '__main__':

    str1 = "abyzfe"
    str2 = "abcdeyzf"
    str3 = "popode"

    # Function Call
    convertString(str1, str2, str3)

# This code is contributed by Bhupendra_Singh
```

## C#

```
// C# program of
// the above approach 
using System;
using System.Collections.Generic;
class GFG{

// Function to check whether str1 can
// be transformed to str2
static void convertString(String str1,
                          String str2,
                          String str3)
{
  // To store the frequency of
  // characters of String str3
  Dictionary<char,
             int> freq = new Dictionary<char,
                                        int>();

  for (int i = 0; i < str3.Length; i++)
  {
    if(freq.ContainsKey(str3[i]))
      freq[str3[i]] =  freq[str3[i]] + 1;
    else
      freq.Add(str3[i], 1);
  }

  // Declare two pointers & flag
  int ptr1 = 0;
  int ptr2 = 0;
  bool flag = true;

  // Traverse both the String and
  // check whether it can be transformed
  while (ptr1 < str1.Length &&
         ptr2 < str2.Length)
  {    
    // If both pointers point to same
    // characters increment them
    if (str1[ptr1] == str2[ptr2])
    {
      ptr1++;
      ptr2++;
    }

    // If the letters don't match check
    // if we can find it in String C
    else
    {      
      // If the letter is available in
      // String str3, decrement it's
      // frequency & increment the ptr2
      if(freq.ContainsKey(str3[ptr2]))
        if (freq[str3[ptr2]] > 0)
        {
          freq[str3[ptr2]] = freq[str3[ptr2]] - 1;
          ptr2++;
        }

      // If letter isn't present in str3[]
      // set the flag to false and break
      else
      {
        flag = false;
        break;
      }
    }
  }

  // If the flag is true and both pointers
  // points to their end of respective Strings
  // then it is possible to transformed str1
  // into str2, otherwise not.
  if (flag && ptr1 == str1.Length &&
      ptr2 == str2.Length)
  {
    Console.Write("YES" + "\n");
  }
  else
  {
    Console.Write("NO" + "\n");
  }
}

// Driver Code
public static void Main(String[] args)
{
  String str1 = "abyzfe";
  String str2 = "abcdeyzf";
  String str3 = "popode";

  // Function Call
  convertString(str1, str2, str3);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// JavaScript program of
// the above approach

// Function to check whether str1 can
// be transformed to str2
function convertString(str1,str2,str3)
{
    // To store the frequency of
  // characters of String str3
  let freq = new Map();

  for (let i = 0; i<str3.length; i++)
  {
    if(freq.has(str3[i]))
      freq.set(str3[i],
               freq.get(str3[i]) + 1);
    else
      freq.set(str3[i], 1);

  }

  // Declare two pointers & flag
  let ptr1 = 0;
  let ptr2 = 0;
  let flag = true;

  // Traverse both the String and
  // check whether it can be transformed
  while (ptr1 < str1.length &&
         ptr2 < str2.length)
  {

    // If both pointers point to same
    // characters increment them
    if (str1[ptr1] == str2[ptr2])
    {
      ptr1++;
      ptr2++;
    }

    // If the letters don't match check
    // if we can find it in String C
    else
    {

      // If the letter is available in
      // String str3, decrement it's
      // frequency & increment the ptr2
      if(freq.has(str3[ptr2]))
        if (freq.get(str3[ptr2]) > 0)
        {
          freq.set(str3[ptr2],
                   freq.get(str3[ptr2]) - 1);
          ptr2++;
        }

      // If letter isn't present in str3[]
      // set the flag to false and break
      else
      {
        flag = false;
        break;
      }
    }
  }

  // If the flag is true and both pointers
  // points to their end of respective Strings
  // then it is possible to transformed str1
  // into str2, otherwise not.
  if (flag && ptr1 == str1.length &&
      ptr2 == str2.length)
  {
    document.write("YES" + "<br>");
  }
  else
  {
    document.write("NO" + "<br>");
  }
}

// Driver Code
let str1 = "abyzfe";
let str2 = "abcdeyzf";
let str3 = "popode";

// Function Call
convertString(str1, str2, str3);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
NO
```

**时间复杂度:** O(N)，N =最大长度(str1，str2，str3)

**辅助空间:** O(N)