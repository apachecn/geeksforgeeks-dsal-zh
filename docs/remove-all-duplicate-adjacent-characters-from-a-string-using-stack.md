# 使用堆栈

删除字符串中所有重复的相邻字符

> 原文:[https://www . geesforgeks . org/从字符串中删除所有重复的相邻字符-使用堆栈/](https://www.geeksforgeeks.org/remove-all-duplicate-adjacent-characters-from-a-string-using-stack/)

给定一个字符串 **str** ，任务是从给定的字符串中移除所有重复的相邻字符。

**示例:**

> ***输入:**str = " azxzy "*
> ***输出:** ay*
> 移除“xx”将字符串修改为“azzy”。
> 现在，删除“zz”会将字符串修改为“ay”。
> 由于字符串“ay”不包含重复项，输出为 **ay** 。
> 
> ***输入**:【aaccdd】*
> ***输出:**空串*

**递归方法:**参考文章[递归去除所有相邻重复](https://www.geeksforgeeks.org/recursively-remove-adjacent-duplicates-given-string/)递归解决这个问题。
***时间复杂度:** O(N)*
***辅助空间:** O(N)*

[**字符串函数**](https://www.geeksforgeeks.org/string-data-structure/) **基于方法:**参考本文[删除第一对相邻的相似字符，直到可能](https://www.geeksforgeeks.org/remove-first-adjacent-pairs-of-similar-characters-until-possible/)使用[字符串](https://www.geeksforgeeks.org/string-data-structure/)的内置函数 [pop_back()](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/) 和 [back()](https://www.geeksforgeeks.org/stdstringback-in-c-with-examples/) 方法来解决这个问题。

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)

[**堆叠**](https://www.geeksforgeeks.org/stack-data-structure/) **基于方法:**使用[堆叠](https://www.geeksforgeeks.org/stack-data-structure/)使用**后进先出**的属性可以解决问题。思路是[从左到右遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)，[检查栈是空的](https://www.geeksforgeeks.org/stack-empty-and-stack-size-in-c-stl/)还是栈顶元素不等于**字符串**的当前字符，然后将当前字符推入栈中。否则，从堆栈的[顶部弹出元素](https://www.geeksforgeeks.org/stack-top-c-stl/)。按照以下步骤解决问题:

1.  创建一个[栈](https://www.geeksforgeeks.org/stack-data-structure/)、 **st** 来移除**字符串**中相邻的重复字符。
2.  遍历字符串**字符串**，检查堆栈是否为空，或者堆栈的顶部元素是否不等于当前字符。如果发现是真的，将当前角色推入**圣**。
3.  否则，从堆栈顶部弹出元素。
4.  最后，打印堆栈的所有剩余元素。

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to remove adjacent
// duplicate elements
string ShortenString(string str1)
{

    // Store the string without
    // duplicate elements
    stack<char> st;

    // Store the index of str
    int i = 0;

    // Traverse the string str
    while (i < str1.length())
    {

        // Checks if stack is empty or top of the
        // stack is not equal to current character
        if (st.empty() || str1[i] != st.top())
        {
            st.push(str1[i]);
            i++;
        }

        // If top element of the stack is
        // equal to the current character
        else
        {
            st.pop();
            i++;
        }
    }

    // If stack is empty
    if (st.empty())
    {
        return ("Empty String");
    }

    // If stack is not Empty
    else
    {
        string short_string = "";
        while (!st.empty())
        {
            short_string = st.top() +
                           short_string;
            st.pop();
        }
        return (short_string);
    }
}

// Driver Code
int main()
{
    string str1 ="azzxzy";

    cout << ShortenString(str1);

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Function to remove adjacent
// duplicate elements
static String ShortenString(String str1)
{
  // Store the String without
  // duplicate elements
  Stack<Character> st =
        new Stack<Character>();

  // Store the index of str
  int i = 0;

  // Traverse the String str
  while (i < str1.length())
  {
    // Checks if stack is empty
    // or top of the stack is not
    // equal to current character
    if (st.isEmpty() ||
        str1.charAt(i) != st.peek())
    {
      st.add(str1.charAt(i));
      i++;
    }

    // If top element of the stack is
    // equal to the current character
    else
    {
      st.pop();
      i++;
    }
  }

  // If stack is empty
  if (st.isEmpty())
  {
    return ("Empty String");
  }

  // If stack is not Empty
  else
  {
    String short_String = "";
    while (!st.isEmpty())
    {
      short_String = st.peek() +
                     short_String;
      st.pop();
    }
    return (short_String);
  }
}

// Driver Code
public static void main(String[] args)
{
  String str1 ="azzxzy";
  System.out.print(ShortenString(str1));

}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to remove adjacent
# duplicate elements
def ShortenString(str1):

    # Store the string without
    # duplicate elements
    st = []

    # Store the index of str
    i = 0

    # Traverse the string str
    while i < len(str1):

        # Checks if stack is empty or top of the
        # stack is not equal to current character
        if len(st)== 0 or str1[i] != st[-1]:
            st.append(str1[i])
            i += 1

        # If top element of the stack is
        # equal to the current character
        else:
            st.pop()
            i += 1

    # If stack is empty
    if len(st)== 0:
        return("Empty String")

    # If stack is not Empty
    else:
        short_string = ""
        for i in st:
            short_string += str(i)
        return(short_string)

# Driver Code
if __name__ == "__main__":
    str1 ="azzxzy"
    print(ShortenString(str1))
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to remove adjacent
// duplicate elements
static String ShortenString(String str1)
{

    // Store the String without
    // duplicate elements
    Stack<char> st = new Stack<char>();

    // Store the index of str
    int i = 0;

    // Traverse the String str
    while (i < str1.Length)
    {

        // Checks if stack is empty
        // or top of the stack is not
        // equal to current character
        if (st.Count == 0 || (st.Count != 0 &&
             str1[i] != st.Peek()))
        {
            st.Push(str1[i]);
            i++;
        }

        // If top element of the stack is
        // equal to the current character
        else
        {
            if (st.Count != 0)
                st.Pop();

            i++;
        }
    }

    // If stack is empty
    if (st.Count == 0)
    {
        return ("Empty String");
    }

    // If stack is not Empty
    else
    {
        String short_String = "";

        while (st.Count != 0)
        {
            short_String = st.Peek() +
                           short_String;
            st.Pop();
        }
        return (short_String);
    }
}

// Driver Code
public static void Main(String[] args)
{
    String str1 ="azzxzy";

    Console.Write(ShortenString(str1));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to remove adjacent
// duplicate elements
function ShortenString(str1)
{

    // Store the string without
    // duplicate elements
    var st = [];

    // Store the index of str
    var i = 0;

    // Traverse the string str
    while (i < str1.length)
    {

        // Checks if stack is empty or top of the
        // stack is not equal to current character
        if (st.length==0 || str1[i] != st[st.length-1])
        {
            st.push(str1[i]);
            i++;
        }

        // If top element of the stack is
        // equal to the current character
        else
        {
            st.pop();
            i++;
        }
    }

    // If stack is empty
    if (st.length==0)
    {
        return ("Empty String");
    }

    // If stack is not Empty
    else
    {
        var short_string = "";
        while(st.length!=0)
        {
            short_string = st[st.length-1] +
                           short_string;
            st.pop();
        }
        return (short_string);
    }
}

// Driver Code
var str1 ="azzxzy";
document.write( ShortenString(str1));

</script>
```

**Output:** 

```
axzy
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)