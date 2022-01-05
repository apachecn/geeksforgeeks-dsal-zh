# 给定字符串的 URLify(替换空格为%20)

> 原文:[https://www . geeksforgeeks . org/urlify-给定-字符串-替换-空格/](https://www.geeksforgeeks.org/urlify-given-string-replace-spaces/)

编写一个方法，用“%20”替换字符串中的所有空格。您可以假设字符串末尾有足够的空间来容纳额外的字符，并且您得到了字符串的“真实”长度。
**例:**

```
Input: "Mr John Smith", 13
Output: Mr%20John%20Smith

Input: "Mr John Smith   ", 13
Output: Mr%20John%20Smith
```

一个**简单的解决方案**就是创建一个辅助字符串，一个个复制字符。每当遇到空间时，用%20 代替它。

假设我们在输入字符串中有额外的空间，一个更好的解决方案是原地执行。我们首先计算输入字符串中的空格数。使用这个计数，我们可以找到修改后的(或结果)字符串的长度。在计算新的长度后，我们从末尾开始填充字符串。

下面是上述方法的实现:

## C++

```
// C++ program to replace spaces with %20
#include<stdio.h>

// Maximum length of string after modifications.
const int MAX = 1000;

// Replaces spaces with %20 in-place and returns
// new length of modified string. It returns -1
// if modified string cannot be stored in str[]
int replaceSpaces(char str[])
{
    // count spaces and find current length
    int space_count = 0, i;
    for (i = 0; str[i]; i++)
        if (str[i] == ' ')
            space_count++;

    // Remove trailing spaces
    while (str[i-1] == ' ')
    {
       space_count--;
       i--;
    }

    // Find new length.
    int new_length = i + space_count * 2 + 1;

    // New length must be smaller than length
    // of string provided.
    if (new_length > MAX)
        return -1;

    // Start filling character from end
    int index = new_length - 1;

    // Fill string termination.
    str[index--] = '\0';

    // Fill rest of the string from end
    for (int j=i-1; j>=0; j--)
    {
        // inserts %20 in place of space
        if (str[j] == ' ')
        {
            str[index] = '0';
            str[index - 1] = '2';
            str[index - 2] = '%';
            index = index - 3;
        }
        else
        {
            str[index] = str[j];
            index--;
        }
    }

    return new_length;
}

// Driver code
int main()
{
    char str[MAX] = "Mr John Smith   ";

    // Prints the replaced string
    int new_length = replaceSpaces(str);
    for (int i=0; i<new_length; i++)
        printf("%c", str[i]);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to replace spaces with %20
class GFG
{

    // Maximum length of string
    // after modifications.
    static int MAX = 1000;

    // Replaces spaces with %20 in-place
    // and returns new length of modified string.
    // It returns -1 if modified string
    // cannot be stored in str[]
    static char[] replaceSpaces(char[] str)
    {

        // count spaces and find current length
        int space_count = 0, i = 0;
        for (i = 0; i < str.length; i++)
            if (str[i] == ' ')
                space_count++;

        // count spaces and find current length
        while (str[i - 1] == ' ')
        {
            space_count--;
            i--;
        }

        // Find new length.
        int new_length = i + space_count * 2;

        // New length must be smaller than length
        // of string provided.
        if (new_length > MAX)
            return str;

        // Start filling character from end
        int index = new_length - 1;

        char[] old_str = str;
        str = new char[new_length];

        // Fill rest of the string from end
        for (int j = i - 1; j >= 0; j--)
        {

            // inserts %20 in place of space
            if (old_str[j] == ' ')
            {
                str[index] = '0';
                str[index - 1] = '2';
                str[index - 2] = '%';
                index = index - 3;
            }

            else
            {
                str[index] = old_str[j];
                index--;
            }
        }
        return str;
    }

    // Driver Code
    public static void main(String[] args)
    {
        char[] str = "Mr John Smith ".toCharArray();

        // Prints the replaced string
        str = replaceSpaces(str);

        for (int i = 0; i < str.length; i++)
            System.out.print(str[i]);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Maximum length of string after modifications.
MAX = 1000;

# Replaces spaces with %20 in-place and returns
# new length of modified string. It returns -1
# if modified string cannot be stored in str[]
def replaceSpaces(string):

    # Remove remove leading and trailing spaces
    string = string.strip()

    i = len(string)

    # count spaces and find current length
    space_count = string.count(' ')

    # Find new length.
    new_length = i + space_count * 2

    # New length must be smaller than length
    # of string provided.
    if new_length > MAX:
        return -1

    # Start filling character from end
    index = new_length - 1

    string = list(string)

    # Fill string array
    for f in range(i - 2, new_length - 2):
        string.append('0')

    # Fill rest of the string from end
    for j in range(i - 1, 0, -1):

        # inserts %20 in place of space
        if string[j] == ' ':
            string[index] = '0'
            string[index - 1] = '2'
            string[index - 2] = '%'
            index = index - 3
        else:
            string[index] = string[j]
            index -= 1

    return ''.join(string)

# Driver Code
if __name__ == '__main__':
    s = "Mr John Smith "
    s = replaceSpaces(s)
    print(s)

# This code is contributed by Vinayak
```

## C#

```
// C# program to replace spaces with %20
using System;

class GFG
{

    // Maximum length of string
    // after modifications.
    static int MAX = 1000;

    // Replaces spaces with %20 in-place
    // and returns new length of modified string.
    // It returns -1 if modified string
    // cannot be stored in []str
    static char[] replaceSpaces(char[] str)
    {

        // count spaces and find current length
        int space_count = 0, i = 0;
        for (i = 0; i < str.Length; i++)
            if (str[i] == ' ')
                space_count++;

        // count spaces and find current length
        while (str[i - 1] == ' ')
        {
            space_count--;
            i--;
        }

        // Find new length.
        int new_length = i + space_count * 2;

        // New length must be smaller than
        // length of string provided.
        if (new_length > MAX)
            return str;

        // Start filling character from end
        int index = new_length - 1;

        char[] new_str = str;
        str = new char[new_length];

        // Fill rest of the string from end
        for (int j = i - 1; j >= 0; j--)
        {

            // inserts %20 in place of space
            if (new_str[j] == ' ')
            {
                str[index] = '0';
                str[index - 1] = '2';
                str[index - 2] = '%';
                index = index - 3;
            }
            else
            {
                str[index] = new_str[j];
                index--;
            }
        }
        return str;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        char[] str = "Mr John Smith ".ToCharArray();

        // Prints the replaced string
        str = replaceSpaces(str);

        for (int i = 0; i < str.Length; i++)
            Console.Write(str[i]);
    }
}

// This code is contributed by 29AjayKumar
```

**输出:**

```
Mr%20John%20Smith
```

**时间复杂度:** O(n)，其中 n 为字符串的真实长度。
**辅助空间:** O(1)，因为上面的程序是一个[在位](https://en.wikipedia.org/wiki/In-place_algorithm)算法。

**方法 2:**
修剪字符串并调用 replaceAll()方法，将所有空格 Unicode 替换为%20。

以下是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG
{
    public static void main(String[] args)
    {
        // Instantiate the string
        String str = "Mr John Smith   ";

        // Trim the given string
        str = str.trim();

        // Replace All space (unicode is \\s) to %20
        str = str.replaceAll("\\s", "%20");

        // Display the result
        System.out.println(str);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Instantiate the string
s = "Mr John Smith "

# Trim the given string
s = s.strip()

# Replace All space (unicode is \\s) to %20
s = s.replace(' ', "%20")

# Display the result
print(s)

# This code is contributed by vinayak
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{
    public static void Main()
    {
        // Instantiate the string
        String str = "Mr John Smith   ";

        // Trim the given string
        str = str.Trim();

        // Replace All space (unicode is \\s) to %20
        str = str.Replace(" ", "%20");

        // Display the result
        Console.Write(str);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

      // JavaScript implementation of above approach

      // Instantiate the string
      var str = "Mr John Smith ";

      // Trim the given string
      str = str.trim();

      // Replace All space (unicode is \\s) to %20
      str = str.replaceAll(" ", "%20");

      // Display the result
      document.write(str);

</script>
```

**输出:**

```
Mr%20John%20Smith
```

**方法 3:使用 string.replace()函数:**

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

void replaceSpaces(string input)
{
    string rep = "%20";
    for(int i=0 ; i<input.length() ; i++)
    {
        if(input[i] == ' ')
            input.replace(i,1,rep);
    }
    cout<<input;
}

int main()
{
    string input = "Mr John Smith";
    replaceSpaces(input);

    return 0;
}
```

**输出:**

```
Mr%20John%20Smith
```

本文由**婆罗门赛**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。