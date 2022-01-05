# 通过移除“10”

形式的所有子序列，检查字符串是否可以被清空

> 原文:[https://www . geesforgeks . org/check-if-a-string-可以通过移除表单的所有子序列来清空-10/](https://www.geeksforgeeks.org/check-if-a-string-can-be-emptied-by-removing-all-subsequences-of-the-form-10/)

给定一个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **字符串**，任务是通过移除表单**【10】**
的所有[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)来检查该字符串是否可以清空

**示例**:

> **输入:** str = "11011000"
> **输出:**是
> **说明:**需要执行以下步骤清空给定字符串**“11011000”→“111000”→“1100”→“10”→“**
> 
> **输入** : 101001
> **输出**:否

**方法:**按照以下步骤解决问题:

1.  [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)并将所有 **1** 存储在[堆栈](https://www.geeksforgeeks.org/stack-data-structure/)中。
2.  如果 **str[i] = 1** ，则将其存储在堆栈中。
3.  如果 **str[i] = 0** 和[堆栈不为空](https://www.geeksforgeeks.org/stack-empty-and-stack-size-in-c-stl/)，则[弹出](https://www.geeksforgeeks.org/stack-pop-method-in-java/)堆栈顶部的字符。
4.  否则，返回**假**。
5.  如果[栈](https://www.geeksforgeeks.org/stack-data-structure/)为空，返回**真**。
6.  否则，返回**假**

以下是上述方法的实现:

## C++

```
// C++ program for
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find if string
// is reducible to NULL
bool isReducible(string str)
{
    // Length of string
    int N = str.size();

    // Stack to store all 1s
    stack<char> s;

    // Iterate over the characters
    // of the string
    for (int i = 0; i < N; i++) {

        // If current character is 1
        if (str[i] == '1')

            // Push it into the stack
            s.push(str[i]);

        else if (!s.empty())

            // Pop from the stack
            s.pop();

        else
            // If the stack is empty
            return false;
    }

    return s.empty();
}

// Driver Code
int main()
{
    string str = "11011000";

    if (isReducible(str))
        cout << "Yes";

    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.io.*;
import java.util.*;

class GFG
{

  // Function to find if string
  // is reducible to NULL
  static boolean isReducible(String str)
  {

    // Length of string
    int N = str.length();

    // Stack to store all 1s
    ArrayList<Character> s = new ArrayList<Character>();

    // Iterate over the characters
    // of the string
    for (int i = 0; i < N; i++)
    {

      // If current character is 1
      if (str.charAt(i) == '1')

        // Push it into the stack
        s.add(str.charAt(i));
      else if (s.size() > 0)

        // Pop from the stack
        s.remove(s.size() - 1);

      else

        // If the stack is empty
        return false;
    }

    if(s.size() == 0)
    {
      return true;
    }
    else{
      return false;
    }

  }

  // Driver code
  public static void main (String[] args)
  {
    String str = "11011000";
    if (isReducible(str))
    {
      System.out.println("Yes");
    }
    else
    {
      System.out.println("No");
    }
  }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find if string
# is reducible to NULL
def isReducible(Str) :

    # Length of string
    N = len(Str)

    # Stack to store all 1s
    s = []

    # Iterate over the characters
    # of the string
    for i in range(N) :

      # If current character is 1
      if (Str[i] == '1') :

        # Push it into the stack
        s.append(Str[i])

      elif(len(s) > 0) :

        # Pop from the stack
        del s[len(s) - 1]

      else :
        # If the stack is empty
        return False

    if(len(s) == 0) :
      return True

    else :
      return False

      # Driver code
Str = "11011000"

if (isReducible(Str)) :
  print("Yes")

else :
  print("No")

  # This code is contributed by divyeshrabadiya07.
```

## C#

```
// C# program for
// the above approach
using System;
using System.Collections.Generic;
class GFG {

  // Function to find if string
  // is reducible to NULL
  static bool isReducible(string str)
  {
    // Length of string
    int N = str.Length;

    // Stack to store all 1s
    List<char> s = new List<char>();

    // Iterate over the characters
    // of the string
    for (int i = 0; i < N; i++) {

      // If current character is 1
      if (str[i] == '1')

        // Push it into the stack
        s.Add(str[i]);

      else if (s.Count > 0)

        // Pop from the stack
        s.RemoveAt(s.Count - 1);

      else
        // If the stack is empty
        return false;
    }

    if(s.Count == 0)
    {
      return true;
    }
    else{
      return false;
    }
  }

  // Driver code
  static void Main()
  {
    string str = "11011000";

    if (isReducible(str))
      Console.WriteLine("Yes");

    else
      Console.WriteLine("No");
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
    // Javascript program for
    // the above approach

    // Function to find if string
    // is reducible to NULL
    function isReducible(str)
    {
      // Length of string
      let N = str.length;

      // Stack to store all 1s
      let s = [];

      // Iterate over the characters
      // of the string
      for (let i = 0; i < N; i++) {

        // If current character is 1
        if (str[i] == '1')

          // Push it into the stack
          s.push(str[i]);

        else if (s.length > 0)

          // Pop from the stack
          s.pop();

        else
          // If the stack is empty
          return false;
      }

      if(s.length == 0)
      {
        return true;
      }
      else{
        return false;
      }
    }

    let str = "11011000";

    if (isReducible(str))
      document.write("Yes");

    else
      document.write("No");

      // This code is contributed by suresh07.
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)