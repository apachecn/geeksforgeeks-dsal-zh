# 删除给定字符串中的空格

> 原文:[https://www . geesforgeks . org/remove-spaces-from-给定字符串/](https://www.geeksforgeeks.org/remove-spaces-from-a-given-string/)

给定一个字符串，移除字符串中的所有空格并返回它。

```
Input:  "g  eeks   for ge  eeks  "
Output: "geeksforgeeks"
```

预期时间复杂度为 O(n)，并且只有一次字符串遍历。

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/remove-spaces0128/1)

下面是一个**简单的解决方案**

```
1) Iterate through all characters of given string, do following
   a) If current character is a space, then move all subsequent
      characters one position back and decrease length of the 
      result string.
```

上述解的时间复杂度为 O(n <sup>2</sup> )。
A **更好的解决方案**可以在 O(n)时间内解决。这个想法是记录到目前为止看到的非空格字符的数量。

```
1) Initialize 'count' = 0 (Count of non-space character seen so far)
2) Iterate through all characters of given string, do following
     a) If current character is non-space, then put this character
        at index 'count' and increment 'count'
3) Finally, put '\0' at index 'count'
```

下面是上述算法的实现。

## C++

```
// An efficient C++ program to remove all spaces
// from a string
#include <iostream>
using namespace std;

// Function to remove all spaces from a given string
void removeSpaces(char *str)
{
    // To keep track of non-space character count
    int count = 0;

    // Traverse the given string. If current character
    // is not space, then place it at index 'count++'
    for (int i = 0; str[i]; i++)
        if (str[i] != ' ')
            str[count++] = str[i]; // here count is
                                   // incremented
    str[count] = '\0';
}

// Driver program to test above function
int main()
{
    char str[] = "g  eeks   for ge  eeks  ";
    removeSpaces(str);
    cout << str;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```

// An efficient Java program to remove all spaces
// from a string
class GFG
{

// Function to remove all spaces
// from a given string
static int removeSpaces(char []str)
{
    // To keep track of non-space character count
    int count = 0;

    // Traverse the given string.
    // If current character
    // is not space, then place
    // it at index 'count++'
    for (int i = 0; i<str.length; i++)
        if (str[i] != ' ')
            str[count++] = str[i]; // here count is
                                    // incremented

    return count;
}

// Driver code
public static void main(String[] args)
{
    char str[] = "g eeks for ge eeks ".toCharArray();
    int i = removeSpaces(str);
    System.out.println(String.valueOf(str).subSequence(0, i));
}
}

// This code is contributed by Rajput-Ji
```

## 计算机编程语言

```
# Python program to Remove spaces from a given string

# Function to remove all spaces from a given string
def removeSpaces(string):

    # To keep track of non-space character count
    count = 0

    list = []

    # Traverse the given string. If current character
    # is not space, then place it at index 'count++'
    for i in xrange(len(string)):
        if string[i] != ' ':
            list.append(string[i])

    return toString(list)

# Utility Function
def toString(List):
    return ''.join(List)

# Driver program
string = "g  eeks  for ge  eeks  "
print removeSpaces(string)

# This code is contributed by Bhavya Jain
```

## C#

```
// An efficient C# program to remove all
// spaces from a string
using System;

class GFG
{

// Function to remove all spaces
// from a given string
static int removeSpaces(char []str)
{
    // To keep track of non-space
    // character count
    int count = 0;

    // Traverse the given string. If current
    // character is not space, then place
    // it at index 'count++'
    for (int i = 0; i < str.Length; i++)
        if (str[i] != ' ')
            str[count++] = str[i]; // here count is
                                   // incremented

    return count;
}

// Driver code
public static void Main(String[] args)
{
    char []str = "g eeks for ge eeks ".ToCharArray();
    int i = removeSpaces(str);
    Console.WriteLine(String.Join("", str).Substring(0, i));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

      // An efficient JavaScript program to remove all
      // spaces from a string

      // Function to remove all spaces
      // from a given string
      function removeSpaces(str) {
        // To keep track of non-space
        // character count
        var count = 0;

        // Traverse the given string. If current
        // character is not space, then place
        // it at index 'count++'
        for (var i = 0; i < str.length; i++)
          if (str[i] !== " ") str[count++] = str[i];
         // here count is
        // incremented

        return count;
      }

      // Driver code
      var str = "g eeks for ge eeks ".split("");
      var i = removeSpaces(str);
      document.write(str.join("").substring(0, i));

</script>
```

**Output**

```
geeksforgeeeks
```

上述解的时间复杂度为 O(n)，并且只遍历一次字符串。
div yam Madaan 建议的另一种解决方案是使用预定义函数。下面是实现:

## C++

```
// CPP program to Remove spaces
// from a given string

#include <iostream>
#include <algorithm>
using namespace std;

// Function to remove all spaces from a given string
string removeSpaces(string str)
{
    str.erase(remove(str.begin(), str.end(), ' '), str.end());
    return str;
}

// Driver program to test above function
int main()
{
    string str = "g eeks for ge eeks ";
    str = removeSpaces(str);
    cout << str;
    return 0;
}

// This code is contributed by Divyam Madaan
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove
// all spaces from a string

class GFG {

    // Function to remove all
    // spaces from a given string
    static String removeSpace(String str)
    {
        str = str.replaceAll("\\s","");
        return str;
    }

    // Driver Code
    public static void main(String args[])
    {
        String str = "g eeks for ge eeks ";
        System.out.println(removeSpace(str));
    }
}

// This code is contributed by Kanhaiya.
```

## 计算机编程语言

```
# Python program to Remove spaces from a given string

# Function to remove all spaces from a given string
def removeSpaces(string):
    string = string.replace(' ','')
    return string

# Driver program
string = "g  eeks  for ge  eeks  "
print(removeSpaces(string))

# This code is contributed by Divyam Madaan
```

## C#

```
// C# program to remove
// all spaces from a string
using System;

class GFG
{

    // Function to remove all
    // spaces from a given string
    static String removeSpace(String str)
    {
        str = str.Replace(" ","");
        return str;
    }

    // Driver Code
    public static void Main()
    {
        String str = "g eeks for ge eeks ";
        Console.WriteLine(removeSpace(str));
    }
}

// This code is contributed by
// PrinciRaj1992
```

## java 描述语言

```
<script>
// javascript program to remove
// all spaces from a string
    // Function to remove all
    // spaces from a given string
     function removeSpace( str)
     {
        str = str.replace(/\s/g,'')
        return str;
    }

    // Driver Code   
        var str = "g eeks for ge eeks ";
        document.write(removeSpace(str));

// This code contributed by aashish1995
</script>
```

**Output**

```
geeksforgeeeks
```

使用预定义的 STL 函数解决这个问题的另一种方法，如***【count()***、***【remove()***、 ***getline()*** 和 ***resize()*** 也存在。下面是相同的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;
int main()
{
    string s = "g e e k s f o r g e e k s";

    cout << "string with spaces is " << s << endl;

    int l = s.length(); // storing the length of the string

    int c
        = count(s.begin(), s.end(),
                ' '); // counting the number of whitespaces

    remove(s.begin(), s.end(),
           ' '); // removing all the whitespaces

    s.resize(l - c); // resizing the string to l-c

    cout << "string without spaces is " << s << endl;

    return 0;
}
```

**Output**

```
string with spaces is g e e k s f o r g e e k s
string without spaces is geeksforgeeks
```

感谢 Souravi Sarkar 提出这个问题和初步解决方案。
[**Java |使用 Regex**](https://www.geeksforgeeks.org/java-removing-whitespaces-using-regex/)
移除空格如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息