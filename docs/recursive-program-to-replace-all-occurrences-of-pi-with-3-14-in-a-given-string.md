# 递归程序，在给定的字符串中用 3.14 替换圆周率的所有出现

> 原文:[https://www . geesforgeks . org/递归程序用给定字符串中的 3-14 替换所有出现的 pi/](https://www.geeksforgeeks.org/recursive-program-to-replace-all-occurrences-of-pi-with-3-14-in-a-given-string/)

给定大小为 **N** 的弦**弦**。任务是编写一个递归函数，用给定字符串中的 3.14 替换所有出现的 pi，并打印修改后的字符串。

**示例:**

> **输入:**str = " pippiiiipi "
> T3】输出:3 . 14 pp3 . 14 iiiii 3 . 14
> 
> **输入:**str = " pip "
> T3】输出: 3.14p
> 
> **输入:**str = " xpix "
> T3】输出: x3.14x

我们在这里讨论了迭代函数
**方法:**

*   如果字符串中只有一个字符或者字符串为空，则中断递归调用
*   否则，保留字符串的第一个字符，并将字符串的其余部分传递给递归。
    *   如果第一个字符不是“p ”,那么就把这个字符放在来自递归的答案前面
    *   否则，如果第一个字符是“p ”,传递给递归的部分的第一个字符是“I ”,则用“3.14”替换“pi”

下面是上述方法的实现:

## C++

```
// A recursive C++ program to replace
// all pi in a given string with 3.14
#include <bits/stdc++.h>
using namespace std;

// Recursive Function to replace all
// occurrences of pi in a given
// with 3.14
void replacePiHelper(char str[], int start)
{

    // Base condition
    // if the string is empty
    // or of length one
    if (str[start] == '\0' || str[start + 1] == '\0') {
        return;
    }

    // Getting the answer from
    // recursion for the smaller
    // problem
    replacePiHelper(str, start + 1);

    // Small calculation part
    // if the first character is 'p'
    // and the first character of the part
    // passed to recursion is 'i' then replace
    // "pi" with "3.14"
    if (str[start] == 'p' && str[start + 1] == 'i') {

        // Shifting the characters to
        // right side to put 3.14 in
        // the character array
        for (int i = strlen(str); i >= start + 2; i--) {
            str[i + 2] = str[i];
        }

        // Replacing with "3.14"
        str[start] = '3';
        str[start + 1] = '.';
        str[start + 2] = '1';
        str[start + 3] = '4';
    }
}

// Function to replace pi with 3.14
void replacePi(char str[])
{
    replacePiHelper(str, 0);
}

// Driver code
int main()
{
    char str[] = "pippppiiiipi";

    // Function call
    replacePi(str);

    cout << str;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A recursive Java program to replace
// all pi in a given string with 3.14

class GFG {

    // Recursive Function to replace all
    // occurrences of pi in a given
    // with 3.14
    public String replacePi(String str)
    {
        // base condition
        // if the string is empty
        // or of length one
        if (str.length() <= 1) {
            return str;
        }

        // if the first character is 'p'
        // and the first character of the part
        // passed to recursion is 'i' then replace
        //"pi" with "3.14"
        if (str.charAt(0) == 'p' && str.length() >= 2
            && str.charAt(1) == 'i') {
            return "3.14" + replacePi(str.substring(2, str.length()));
        }

        // if the first character is not 'p'
        // then just put that character in
        // front of the answer which came
        // from recursion
        return str.charAt(0) + replacePi(str.substring(1, str.length()));
    }

    // Driver Code
    public static void main(String args[])
    {
        GFG g = new GFG();
        String str = "pippppiiiipi";
        System.out.println(g.replacePi(str));
    }
}
```

## 蟒蛇 3

```
# A recursive Python3 program to replace
# all pi in a given string with 3.14

# Recursive Function to replace all
# occurrences of pi in a given
# with 3.14
def replacePieHelper(string, start):

    # Base condition
    # if the string is empty
    # or of length one
    if len(string) < 2 or start == len(string):
        return string

    # Getting the answer from
    # recursion for the smaller
    # problem
    replacePieHelper(string, start + 1)

    # Small calculation part
    # if the first character is 'p'
    # and the first character of the part
    # passed to recursion is 'i' then replace
    # "pi" with "3.14"
    if(string[start] == 'p' and
       string[start + 1] == 'i'):

        # Replacing with "3.14"
        string[start:start + 2] = ['3', '.', '1', '4']

# Function to replace pi with 3.14
def replacePi(string):
    replacePieHelper(string, 0)

# Driver Code
if __name__ == "__main__":
    string = "pippppiiiipi"

    string = list(string)

    # Function call
    replacePi(string)

    string = ''.join(string)
    print(string)

# This code is contributed by
# sanjeev2552
```

## C#

```
// A recursive C# program to replace
// all pi in a given string with 3.14

using System;
class gfg {
    // Recursive Function to replace all
    // occurrences of pi in a given
    // with 3.14
    public String replacePi(String str)
    {
        // base condition
        // if the string is empty
        // or of length one
        if (str.Length <= 1) {
            return str;
        }

        // if the first character is 'p'
        // and the first character of the part
        // passed to recursion is 'i' then replace
        //"pi" with "3.14"
        if (str[0] == 'p' && str.Length >= 2
            && str[1] == 'i') {
            return "3.14" + replacePi(str.Substring(2, str.Length - 2));
        }

        // if the first character is not 'p'
        // then just put that character in
        // front of the answer which came
        // from recursion
        return str[0] + replacePi(str.Substring(1, str.Length - 1));
    }
}

// Driver Code
class geek {
    public static int Main()
    {
        gfg g = new gfg();
        string input = "pippppiiiipi";
        Console.WriteLine(g.replacePi(input));
        return 0;
    }
}
```

## java 描述语言

```
<script>

      // A recursive JavaScript program to replace
      // all pi in a given string with 3.14

      // Recursive Function to replace all
      // occurrences of pi in a given
      // with 3.14
      function replacePi(str) {
        // base condition
        // if the string is empty
        // or of length one
        if (str.length <= 1) {
          return str;
        }

        // if the first character is 'p'
        // and the first character of the part
        // passed to recursion is 'i' then replace
        //"pi" with "3.14"
        if (str[0] === "p" && str.length >= 2 && str[1] === "i") {
          return "3.14" + replacePi(str.substring(2, str.length));
        }

        // if the first character is not 'p'
        // then just put that character in
        // front of the answer which came
        // from recursion
        return str[0] + replacePi(str.substring(1, str.length));
      }

      // Driver Code
      var input = "pippppiiiipi";
      document.write(replacePi(input));

</script>
```

**Output**

```
3.14ppp3.14iii3.14
```

**另一种方法:**

用“3.14”替换给定函数中所有圆周率的简单递归方法。首先声明函数，我们不需要任何辅助函数。

*   如果字符串为空或字符串长度为 1，则返回字符串。
*   如果字符串的第 0 个和第 1 个元素是 p，剩下的我们必须处理它们，我们必须称之为递归，它会给出结果。
*   如果不是，那么我们必须调用从第一个到所有元素的递归，然后将递归结果添加到第一个元素并返回它。

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// A simple recursive approach
// to replace all pi in a given
// function with "3.14". Firstly
// function is declared we don't
// need any helper function one
// function is enough
string replacePi(string s)
{

    // Base case if s is empty
    // or length of s is 1
    // return the s
    if (s.length() == 0 || s.length() == 1)
        return s;

    // If the 0th and 1st element
    // of s are p and i we have to
    // handle them for rest we have
    // to call recursion it will
    // give the result
    if (s[0] == 'p' && s[1] == 'i') {

        // Smalloutput is a variable
        // used to store recursion result
        string smallOutput = replacePi(s.substr(2));

        // And we have to add the recursion
        // result with the first part we
        // handled and return the answer
        return "3.14" + smallOutput;
    }
    else {
        // If 1st & 2nd element aren't "p" & "i", then keep
        // 1st index as it is & call recursion for rest of
        // the string.
        return s[0] + replacePi(s.substr(1));
    }
}

// Driver code
int main()
{
    string s = "pipppiiipi";

    // Function call
    string result = replacePi(s);

    cout << result << endl;

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
class GFG {

    // A simple recursive approach
    // to replace all pi in a given
    // function with "3.14". Firstly
    // function is declared we don't
    // need any helper function one
    // function is enough
    public static String replacePi(String s)
    {

        // Base case if s is empty
        // or length of s is 1
        // return the s
        if (s.length() == 0 || s.length() == 1)
            return s;

        // If the 0th and 1st element
        // of s are p and i we have to
        // handle them for rest we have
        // to call recursion it will
        // give the result
        if (s.charAt(0) == 'p' && s.charAt(1) == 'i') {

            // Smalloutput is a variable
            // used to store recursion result
            String smallOutput = replacePi(s.substring(2));

            // And we have to add the recursion
            // result with the first part we
            // handled and return the answer
            return "3.14" + smallOutput;
        }
        else {

            // If not then we have to call
            // recursion from 1st to all elements
            // then add recursion result to
            // 1st element and return it
            String smallOutput = replacePi(s.substring(1));
            return s.charAt(0) + smallOutput;
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "pipppiiipi";

        // Function call
        String result = replacePi(s);
        System.out.println(result);
    }
}

// This code is contributed by divyesh072019
```

## 计算机编程语言

```
# Python program for above approach

# A simple recursive approach
# to replace all
# pi in a given function with "3.14"
# Firstly function is declared we don't
# need any helper function one
# function is enough

def replacePi(string):

    # Base case if string is empty
    # or length of string is 1
    # return the string
    if len(string) == 0 or
                     len(string) == 1:
        return string

    # If the 0th and 1st element
    # of string are p
    # and i we have to handle them
    # for rest we have to call
    # recursion it will give the result
    if string[0] == 'p' and string[1] == 'i':

        # Smalloutput is a variable
        # used to store recursion result
        smallOutput = replacePi(string[2:])   

        # And we have to add the recursion
        # result with the first part we
          # handled and return the answer
        return "3.14" + smallOutput            
    else:

        # If not then we have to call
        # recursion from 1st to all elements
        # then add recursion result to
        # 1st element and return it
        smallOutput = replacePi(string[1:])
        return string[0] + smallOutput

# Driver code
if __name__ == "__main__":

  string = "pipppiiipi"

  # Function call
  result = replacePi(string)
  print result
```

## C#

```
// C# program for above approach
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;

class GFG {

    // A simple recursive approach
    // to replace all pi in a given
    // function with "3.14". Firstly
    // function is declared we don't
    // need any helper function one
    // function is enough
    static string replacePi(string s)
    {

        // Base case if s is empty
        // or length of s is 1
        // return the s
        if (s.Length == 0 || s.Length == 1)
            return s;

        // If the 0th and 1st element
        // of s are p and i we have to
        // handle them for rest we have
        // to call recursion it will
        // give the result
        if (s[0] == 'p' && s[1] == 'i') {

            // Smalloutput is a variable
            // used to store recursion result
            string smallOutput = replacePi(s.Substring(2));

            // And we have to add the recursion
            // result with the first part we
            // handled and return the answer
            return "3.14" + smallOutput;
        }
        else {

            // If not then we have to call
            // recursion from 1st to all elements
            // then add recursion result to
            // 1st element and return it
            string smallOutput = replacePi(s.Substring(1));
            return s[0] + smallOutput;
        }
    }

    // Driver Code
    public static void Main(string[] args)
    {
        string s = "pipppiiipi";

        // Function call
        string result = replacePi(s);
        Console.Write(result);
    }
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// JavaScript program for above approach

// A simple recursive approach
// to replace all pi in a given
// function with "3.14". Firstly
// function is declared we don't
// need any helper function one
// function is enough
function replacePi(s)
{

    // Base case if s is empty
    // or length of s is 1
    // return the s
    if (s.length == 0 || s.length == 1)
        return s;

    // If the 0th and 1st element
    // of s are p and i we have to
    // handle them for rest we have
    // to call recursion it will
    // give the result
    if (s[0] == 'p' && s[1] == 'i') {

        // Smalloutput is a variable
        // used to store recursion result
        let smallOutput = replacePi(s.substr(2));

        // And we have to add the recursion
        // result with the first part we
        // handled and return the answer
        return "3.14" + smallOutput;
    }
    else {
        // If 1st & 2nd element aren't "p" & "i", then keep
        // 1st index as it is & call recursion for rest of
        // the string.
        return s[0] + replacePi(s.substr(1));
    }
}

// Driver code

    let s = "pipppiiipi";

    // Function call
    let result = replacePi(s);

    document.write(result);

</script>
```

**输出:**

```
3.14pp3.14ii3.14
```