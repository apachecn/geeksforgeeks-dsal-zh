# 从字符串中删除多余的空格

> 原文:[https://www.geeksforgeeks.org/remove-extra-spaces-string/](https://www.geeksforgeeks.org/remove-extra-spaces-string/)

给定一个包含许多连续空格的字符串，修剪所有空格，使所有单词之间只包含一个空格**。转换应该就地完成，解决方案应该处理尾随和前导空格，并删除常见标点符号(如句号、逗号和问号)前的空格。**

**示例:**

```
Input: 
str = "   Hello Geeks . Welcome   to  GeeksforGeeks   .    ";
Output: 
"Hello Geeks. Welcome to GeeksforGeeks."

Input: 
str = "GeeksforGeeks";
Output: 
"GeeksforGeeks"
*(No change is needed)*
```

这个问题是[的扩展，从给定的字符串](https://www.geeksforgeeks.org/remove-spaces-from-a-given-string/)中删除空格

**方法 1:**

*   想法是保持 2 分。最初两者都指向数组的开头。
*   第一个指针跟踪输出字符串中要填充的下一个位置。
*   第二个指针前进，以逐个读取字符串的所有字符。
*   在找到任何非空格字符时，该字符被复制到第一个指针的位置，然后第一个和第二个指针都前进。
*   如果非空格字符是句号、逗号或问号，我们还会删除它前面的任何空格。
*   在查找连续的空格字符时，只有一个空格被复制到第一个指针的位置，其余的被忽略。在解决方案中，前导空格和尾随空格是分开处理的。

下面是上述思想的 C++实现。

## C++

```
// C++ program to implement custom trim() function
#include <iostream>
using namespace std;

// Function to in-place trim all spaces in the
// string such that all words should contain only
// a single space between them.
void removeSpaces(string &str)
{
    // n is length of the original string
    int n = str.length();

    // i points to next position to be filled in
    // output string/ j points to next character
    // in the original string
    int i = 0, j = -1;

    // flag that sets to true is space is found
    bool spaceFound = false;

    // Handles leading spaces
    while (++j < n && str[j] == ' ');

    // read all characters of original string
    while (j < n)
    {
        // if current characters is non-space
        if (str[j] != ' ')
        {
            // remove preceding spaces before dot,
            // comma & question mark
            if ((str[j] == '.' || str[j] == ',' ||
                 str[j] == '?') && i - 1 >= 0 &&
                 str[i - 1] == ' ')
                str[i - 1] = str[j++];

            else
                // copy current character at index i
                // and increment both i and j
                str[i++] = str[j++];

            // set space flag to false when any
            // non-space character is found
            spaceFound = false;
        }
        // if current character is a space
        else if (str[j++] == ' ')
        {
            // If space is encountered for the first
            // time after a word, put one space in the
            // output and set space flag to true
            if (!spaceFound)
            {
                str[i++] = ' ';
                spaceFound = true;
            }
        }
    }

    // Remove trailing spaces
    if (i <= 1)
        str.erase(str.begin() + i, str.end());
    else
        str.erase(str.begin() + i - 1, str.end());
}

// Driver Code
int main()
{
    string str = "   Hello Geeks . Welcome   to"
                 "  GeeksforGeeks   .    ";

    removeSpaces(str);

    cout << str;

    return 0;
}
```

**输出:**

```
Hello Geeks. Welcome to GeeksforGeeks.
```

**上述解的时间复杂度**为 O(n)。
**辅助空间**为 0(1)，因为转换是就地完成的。

**方法 2:**
使用 Python 3 中预定义函数的另一种解决方案:

## 蟒蛇 3

```
# Python program to Remove
# extra spaces from a string
input_string = \
    '   Hello Geeks  .  Welcome ,    Do you love Geeks , Geeks  ? '
output_string = []
space_flag = False # Flag to check if spaces have occured

for index in range(len(input_string)):

    if input_string[index] != ' ':
        if space_flag == True:
            if (input_string[index] == '.'
                    or input_string[index] == '?'
                    or input_string[index] == ','):
                pass
            else:
                output_string.append(' ')
            space_flag = False
        output_string.append(input_string[index])
    elif input_string[index - 1] != ' ':
        space_flag = True

print (''.join(output_string))
```

**输出:**

```
Hello Geeks. Welcome to GeeksforGeeks. Do you love Geeks, Geeks?
```

**上述解的时间复杂度**为 O(n)。
**辅助空间**为 0(n)，因为必须创建另一个列表。

**方法 3:** (使用内置功能)

## Java 语言(一种计算机语言，尤用于创建网站)

```
/**
Java Program to remove extra spaces from a string
**/

public class GFG {
  public static void main(String args[]) {
    String str = "   Hello Geeks  .  Welcome ,    Do you love Geeks , Geeks  ? ";
    System.out.println(str.replaceAll("\\s+"," ").trim());
  }
}
```

## java 描述语言

```
<script>

// JavaScript Program to remove
// extra spaces from a string
var str = "   Hello Geeks  .  Welcome ,    Do you love Geeks , Geeks  ? ";
document.write(str.replace("\\s+", " ").trim());

// This code is contributed by rdtank

</script>
```

**输出:**

```
Hello Geeks . Welcome , Do you love Geeks , Geeks ?
```

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。