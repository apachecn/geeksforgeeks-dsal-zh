# 包含给定字符串中每个单词的第一个字母并带有空格的字符串

> 原文:[https://www . geesforgeks . org/字符串-包含第一个字母-每个单词-给定字符串-空格/](https://www.geeksforgeeks.org/string-containing-first-letter-every-word-given-string-spaces/)

给出了包含小写英文字母和空格的字符串**。它可能包含多个空格。获取每个单词的第一个字母，并将结果作为字符串返回。结果不应包含任何空格。** 

**示例:**

```
Input : str = "geeks for geeks"
Output : gfg

Input : str = "happy   coding"
Output : hc
```

来源:[https://www.geeksforgeeks.org/amazon-interview-set-8-2/](https://www.geeksforgeeks.org/amazon-interview-set-8-2/)

其思想是遍历字符串中的每个字符，并维护一个布尔变量，该变量最初被设置为 true。每当我们遇到空间，我们设置布尔变量为真。如果我们遇到除了空格之外的任何字符，我们将检查布尔变量，如果它被设置为真，就像将该宪章复制到输出字符串并将布尔变量设置为假一样。如果布尔变量设置为 false，则不执行任何操作。
算法:

```
1\. Traverse string str. And initialize a variable v as true.
2\. If str[i] == ' '. Set v as true.
3\. If str[i] != ' '. Check if v is true or not.
   a) If true, copy str[i] to output string and set v as false.
   b) If false, do nothing.
```

## C++

```
// C++ program to find the string which contain
// the first character of each word of another
// string.
#include<bits/stdc++.h>
using namespace std;

// Function to find string which has first
// character of each word.
string firstLetterWord(string str)
{
    string result = "";

    // Traverse the string.
    bool v = true;
    for (int i=0; i<str.length(); i++)
    {
        // If it is space, set v as true.
        if (str[i] == ' ')
            v = true;

        // Else check if v is true or not.
        // If true, copy character in output
        // string and set v as false.
        else if (str[i] != ' ' && v == true)
        {
            result.push_back(str[i]);
            v = false;
        }
    }

    return result;
}

// Driver code
int main()
{
    string str = "geeks for geeks";
    cout << firstLetterWord(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the string which
// contain the first character of each word 
// of another string.

class GFG
{

    // Function to find string which has first
    // character of each word.
    static String firstLetterWord(String str)
    {
        String result = "";

        // Traverse the string.
        boolean v = true;
        for (int i = 0; i < str.length(); i++)
        {
            // If it is space, set v as true.
            if (str.charAt(i) == ' ')
            {
                v = true;
            }

            // Else check if v is true or not.
            // If true, copy character in output
            // string and set v as false.
            else if (str.charAt(i) != ' ' && v == true)
            {
                result += (str.charAt(i));
                v = false;
            }
        }

        return result;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "geeks for geeks";
        System.out.println(firstLetterWord(str));
    }
}

// This code is contributed by
// 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to find the string which
# contain the first character of each word
# of another string.

# Function to find string which has first
# character of each word.
def firstLetterWord(str):

    result = ""

    # Traverse the string.
    v = True
    for i in range(len(str)):

        # If it is space, set v as true.
        if (str[i] == ' '):
            v = True

        # Else check if v is true or not.
        # If true, copy character in output
        # string and set v as false.
        elif (str[i] != ' ' and v == True):
            result += (str[i])
            v = False

    return result

# Driver Code
if __name__ == "__main__":

    str = "geeks for geeks"
    print(firstLetterWord(str))

# This code is contributed by ita_c
```

## C#

```
// C# program to find the string which
// contain the first character of each word
// of another string.
using System;

class GFG
{

    // Function to find string which has first
    // character of each word.
    static String firstLetterWord(String str)
    {
        String result = "";

        // Traverse the string.
        bool v = true;
        for (int i = 0; i < str.Length; i++)
        {
            // If it is space, set v as true.
            if (str[i] == ' ')
            {
                v = true;
            }

            // Else check if v is true or not.
            // If true, copy character in output
            // string and set v as false.
            else if (str[i] != ' ' && v == true)
            {
                result += (str[i]);
                v = false;
            }
        }
        return result;
    }

    // Driver code
    public static void Main()
    {
        String str = "geeks for geeks";
        Console.WriteLine(firstLetterWord(str));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

    // Javascript program to find the string which
    // contain the first character of each word
    // of another string.

    // Function to find string which has first
    // character of each word.
    function firstLetterWord(str)
    {
        let result = "";

        // Traverse the string.
        let v = true;
        for (let i = 0; i < str.length; i++)
        {
            // If it is space, set v as true.
            if (str[i] == ' ')
            {
                v = true;
            }

            // Else check if v is true or not.
            // If true, copy character in output
            // string and set v as false.
            else if (str[i] != ' ' && v == true)
            {
                result += (str[i]);
                v = false;
            }
        }
        return result;
    }

    let str = "geeks for geeks";
      document.write(firstLetterWord(str));

</script>
```

**输出:**

```
gfg
```

**时间复杂度:** O(n)

### **另一种方法 1** :

这种方法使用 Java 的 StringBuilder 类。在这种方法中，我们将首先根据空格分割输入字符串。字符串中的空格可以使用正则表达式进行匹配。拆分的字符串存储在字符串数组中。然后，我们可以简单地在字符串生成器对象中追加每个拆分字符串的第一个字符。

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

string processWords(char *input)
{
    /* we are splitting the input based on
    spaces (s)+ : this regular expression
    will handle scenarios where we have words
    separated by multiple spaces */
    char *p;
    vector<string> s;

    p = strtok(input, " ");
    while (p != NULL)
    {
        s.push_back(p);
        p = strtok(NULL, " ");
    }

    string charBuffer;

    for (string values : s)

        /* charAt(0) will pick only the first character
        from the string and append to buffer */
        charBuffer += values[0];

    return charBuffer;
}

// Driver code
int main()
{
    char input[] = "geeks for geeks";
    cout << processWords(input);
    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

class GFG
{
   private static StringBuilder charBuffer = new StringBuilder();

   public static String processWords(String input)
   {
        /* we are splitting the input based on
           spaces (s)+ : this regular expression
           will handle scenarios where we have words
           separated by multiple spaces */
        String s[] = input.split("(\\s)+");

        for(String values : s)
        {
           /* charAt(0) will pick only the first character
              from the string and append to buffer */
            charBuffer.append(values.charAt(0));
        }

      return charBuffer.toString();
   }

   // main function
   public static void main (String[] args)
   {
      String input = "geeks for       geeks geeks      for geeks";
      System.out.println(processWords(input));
   }
}

// This code is contributed by Goutam Das
```

## 蟒蛇 3

```
# An efficient Python3 implementation
# of above approach
charBuffer = []
def processWords(input):

    """ we are splitting the input based on
    spaces (s)+ : this regular expression
    will handle scenarios where we have words
    separated by multiple spaces """
    s = input.split(" ")

    for values in s:
        """ charAt(0) will pick only the first
        character from the string and append
        to buffer """
        charBuffer.append(values[0])
    return charBuffer

# Driver Code
if __name__ == '__main__':
    input = "geeks for geeks"
    print(*processWords(input), sep = "")

# This code is contributed
# by SHUBHAMSINGH10
```

## C#

```
// C# implementation of above approach
using System;
using System.Text;

class GFG
{

private static StringBuilder charBuffer = new StringBuilder();

public static String processWords(String input)
{
        /* we are splitting the input based on
        spaces (s)+ : this regular expression
        will handle scenarios where we have words
        separated by multiple spaces */
        String []s = input.Split(' ');

        foreach(String values in s)
        {

            /* charAt(0) will pick only the first character
            from the string and append to buffer */
            charBuffer.Append(values[0]);
        }

    return charBuffer.ToString();
}

// Driver code
public static void Main()
{
    String input = "geeks for geeks";
    Console.WriteLine(processWords(input));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach
var charBuffer = "";

function processWords(input)
{

        /* we are splitting the input based on
        spaces (s)+ : this regular expression
        will handle scenarios where we have words
        separated by multiple spaces */
        var s = input.split(' ');

        s.forEach(element => {

            /* charAt(0) will pick only the first character
            from the string and append to buffer */
            charBuffer+=element[0];
        });

    return charBuffer;
}

// Driver code
var input = "geeks for geeks";
document.write( processWords(input));

// This code is contributed by rutvik_56.
</script>
```

**输出:**

```
gfg
```

### **另一种方法 2** :

使用边界检查器，请参考[https://www . geeksforgeeks . org/get-first-letter-word-string-use-regex-Java/](http://Get the first letter of each word in a string using regex in Java)

本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。