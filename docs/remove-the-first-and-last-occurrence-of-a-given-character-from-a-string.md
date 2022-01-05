# 从字符串中删除给定字符的第一次和最后一次出现

> 原文:[https://www . geesforgeks . org/从字符串中删除给定字符的第一个和最后一个出现位置/](https://www.geeksforgeeks.org/remove-the-first-and-last-occurrence-of-a-given-character-from-a-string/)

给定一个字符 **C** 和一个字符串 **S** ，任务是从字符串 **S** 中移除字符 **C** 的第一个和最后一个出现。

**示例:**

> **输入:**s = " geekforgasks "，
> T3】输出:盖葛氏
> **解释:**
> eekforge
> 
> ****输入:** S = "helloWorld "，C = ' l '
> T3】输出: heloWord**

****方法:**
想法是从两端遍历给定的字符串，找到遇到的字符 **C** 的第一个出现，并删除相应的出现。最后，打印结果字符串。
以下是上述方法的实施:**

## **C++**

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to remove first and last
// occurrence of a given character
// from the given string
string removeOcc(string& s, char ch)
{
    // Traverse the given string from
    // the beginning
    for (int i = 0; s[i]; i++) {

        // If ch is found
        if (s[i] == ch) {
            s.erase(s.begin() + i);
            break;
        }
    }

    // Traverse the given string from
    // the end
    for (int i = s.length() - 1;
        i > -1; i--) {

        // If ch is found
        if (s[i] == ch) {
            s.erase(s.begin() + i);
            break;
        }
    }

    return s;
}

// Driver Code
int main()
{
    string s = "hello world";

    char ch = 'l';

    cout << removeOcc(s, ch);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java Program to implement
// the above approach
class GFG{

// Function to remove first and last
// occurrence of a given character
// from the given String
static String removeOcc(String s, char ch)
{
    // Traverse the given String from
    // the beginning
    for (int i = 0; i < s.length(); i++)
    {

        // If ch is found
        if (s.charAt(i) == ch)
        {
            s = s.substring(0, i) +
                s.substring(i + 1);
            break;
        }
    }

    // Traverse the given String from
    // the end
    for (int i = s.length() - 1; i > -1; i--)
    {

        // If ch is found
        if (s.charAt(i) == ch)
        {
            s = s.substring(0, i) +
                s.substring(i + 1);
            break;
        }
    }
    return s;
}

// Driver Code
public static void main(String[] args)
{
    String s = "hello world";

    char ch = 'l';

    System.out.print(removeOcc(s, ch));
}
}

// This code is contributed by sapnasingh4991
```

## **蟒蛇 3**

```
# Python3 program to implement
# the above approach

# Function to remove first and last
# occurrence of a given character
# from the given string
def removeOcc(s, ch):

    # Traverse the given string from
    # the beginning
    for i in range(len(s)):

        # If ch is found
        if (s[i] == ch):
            s = s[0 : i] + s[i + 1:]
            break

    # Traverse the given string from
    # the end
    for i in range(len(s) - 1, -1, -1):

        # If ch is found
        if (s[i] == ch):
            s = s[0 : i] + s[i + 1:]
            break

    return s

# Driver Code
s = "hello world"

ch = 'l'

print(removeOcc(s, ch))

# This code is contributed by sanjoy_62
```

## **C#**

```
// C# Program to implement
// the above approach
using System;
class GFG{

// Function to remove first and last
// occurrence of a given character
// from the given String
static String removeOcc(String s, char ch)
{
    // Traverse the given String from
    // the beginning
    for (int i = 0; i < s.Length; i++)
    {

        // If ch is found
        if (s[i] == ch)
        {
            s = s.Substring(0, i) +
                s.Substring(i + 1);
            break;
        }
    }

    // Traverse the given String from
    // the end
    for (int i = s.Length - 1; i > -1; i--)
    {

        // If ch is found
        if (s[i] == ch)
        {
            s = s.Substring(0, i) +
                s.Substring(i + 1);
            break;
        }
    }
    return s;
}

// Driver Code
public static void Main(String[] args)
{
    String s = "hello world";

    char ch = 'l';

    Console.Write(removeOcc(s, ch));
}
}

// This code is contributed by sapnasingh4991
```

## **java 描述语言**

```
<script>
      // JavaScript Program to implement
      // the above approach
      // Function to remove first and last
      // occurrence of a given character
      // from the given String
      function removeOcc(s, ch) {
        // Traverse the given String from
        // the beginning
        for (var i = 0; i < s.length; i++) {
          // If ch is found
          if (s[i] === ch) {
            s = s.substring(0, i) + s.substring(i + 1);
            break;
          }
        }

        // Traverse the given String from
        // the end
        for (var i = s.length - 1; i > -1; i--) {
          // If ch is found
          if (s[i] === ch) {
            s = s.substring(0, i) + s.substring(i + 1);
            break;
          }
        }
        return s;
      }

      // Driver Code
      var s = "hello world";
      var ch = "l";

      document.write(removeOcc(s, ch));
</script>
```

****Output:** 

```
helo word
```** 

*****时间复杂度:** O(N)*
***辅助空间:** O(1)*** 

#### **方法 2:使用索引方法**

*   **将字符串转换为列表。**
*   **遍历列表，如果我们找到一个给定的字符，那么使用 [**pop()**](https://www.geeksforgeeks.org/python-list-pop/) 移除该索引，并中断循环**
*   **从头到尾遍历列表，如果我们找到一个给定的字符，那么使用 pop()移除该索引并中断循环。**
*   **[**加入**](https://www.geeksforgeeks.org/join-function-python/) 列表并打印。**

**下面是实现:**

## **蟒蛇 3**

```
# Python3 program to implement
# the above approach

# Function to remove first and last
# occurrence of a given character
# from the given string

def removeOcc(str, ch):
    # Convert string to list
    s = list(str)
    # Traverse the string from starting position
    for i in range(len(s)):
        # if we find ch then remove it and break the loop
        if(s[i] == ch):
            s.pop(i)
            break
    # Traverse the string from the end
    for i in range(len(s)-1, -1, -1):
        # if we find ch then remove it and break the loop
        if(s[i] == ch):
            s.pop(i)
            break
    # Join the list
    return ''.join(s)

# Driver Code
s = "hello world"

ch = 'l'

print(removeOcc(s, ch))

# This code is contributed by vikkycirus
```

****时间复杂度:** O(N)**

****辅助空间:** O(N)**