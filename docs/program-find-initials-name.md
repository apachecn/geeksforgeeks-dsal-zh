# 程序查找名字的首字母。

> 原文:[https://www.geeksforgeeks.org/program-find-initials-name/](https://www.geeksforgeeks.org/program-find-initials-name/)

给定一个字符串名称，我们必须找到名称的首字母

**示例:**

```
Input  : prabhat kumar singh
Output : P K S
We take the first letter of all
words and print in capital letter.

Input  : Jude Law
Output : J L

Input  : abhishek kumar singh
Output : A K S
```

1)用大写字母打印第一个字符。
2)遍历字符串的剩余部分，并打印大写字母空格后的每个字符。

## C++

```
// C++ program to print initials of a name
#include <bits/stdc++.h>
using namespace std;

void printInitials(const string& name)
{
    if (name.length() == 0)
        return;

    // Since toupper() returns int, we do typecasting
    cout << (char)toupper(name[0]);

    // Traverse rest of the string and print the
    // characters after spaces.
    for (int i = 1; i < name.length() - 1; i++)
        if (name[i] == ' ')
            cout << " " << (char)toupper(name[i + 1]);
}

// Driver code
int main()
{
    string name = "prabhat kumar singh";
    printInitials(name);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print initials of a name
class initials {

    static void printInitials(String name)
    {
        if (name.length() == 0)
            return;

        // Since toupper() returns int,
        // we do typecasting
        System.out.print(Character.toUpperCase(
            name.charAt(0)));

        // Traverse rest of the string and
        // print the characters after spaces.
        for (int i = 1; i < name.length() - 1; i++)
            if (name.charAt(i) == ' ')
                System.out.print(" " + Character.toUpperCase(
                                        name.charAt(i + 1)));
    }

    // Driver code
    public static void main(String args[])
    {
        String name = "prabhat kumar singh";
        printInitials(name);
    }
}

// This code is contributed by Danish Kaleem
```

## 计算机编程语言

```
# Python program to print
# initials of a name

# user define function
def printInitials(name):
    if(len(name) == 0):
        return
    print(name[0].upper()),
    for i in range(1, len(name) - 1):
        if (name[i] == ' '):
            print (name[i + 1].upper()),

def main():
    name = "Prabhat Kumar Singh"
    printInitials(name)

if __name__=="__main__":
    main()

# This code is contributed
# by prabhat kumar singh
```

## C#

```
// C# program to print initials of a name
using System;

class initials {

    static void printInitials(String name)
    {
        if (name.Length == 0)
            return;

        // Since toupper() returns int,
        // we do typecasting
        Console.Write(Char.ToUpper(name[0]));

        // Traverse rest of the string and
        // print the characters after spaces.
        for (int i = 1; i < name.Length - 1; i++)
            if (name[i] == ' ')
                Console.Write(" " + Char.ToUpper(name[i + 1]));
    }

    // Driver code
    public static void Main()
    {
        String name = "prabhat kumar singh";
        printInitials(name);
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php program to print initials of a name

function printInitials($name)
{
    if (strlen($name) == 0)
        return;

    // Since toupper() returns int, we do typecasting
    echo strtoupper($name[0]);

    // Traverse rest of the string and print the
    // characters after spaces.
    for ($i = 1; $i < strlen($name) - 1; $i++)
        if ($name[$i] == ' ')
            echo " " . strtoupper($name[$i + 1]);
}

// Driver code
$name = "prabhat kumar singh";
printInitials($name);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
    // Javascript program to print initials of a name

    function printInitials(name)
    {
        if (name.length == 0)
            return;

        // Since toupper() returns int,
        // we do typecasting
        document.write(name[0].toUpperCase());

        // Traverse rest of the string and
        // print the characters after spaces.
        for (let i = 1; i < name.length - 1; i++)
            if (name[i] == ' ')
                document.write(" " + name[i + 1].toUpperCase());
    }

    let name = "prabhat kumar singh";
      printInitials(name);

</script>
```

**输出:**

```
P K S
```

**另一种可能的解决方案如下:**

## C++

```
// C++ program to solve the above approach
#include <bits/stdc++.h>
using namespace std;

void printInitials(string name)
{
    if (name.length() == 0)
        return;

    // split the string using 'space'
    // and print the first character of every word
    stringstream X(name); // X is an object of stringstream
                          // that references the S string

    // use while loop to check the getline() function
    // condition
    while (getline(X, name, ' ')) {
        /* X represents to read the string from
         stringstream, T use for store the token string and,
         ' ' whitespace represents to split the string where
         whitespace is found. */

        cout << (char)toupper(name[0])<<" "; // print split string
    }
}

// Driver code
int main()
{
    string name = "prabhat kumar singh";
    printInitials(name);
    return 0;
}

// This code is contributed by gauravrajput1
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print initials of a name
class initials {

    static void printInitials(String name)
    {
        if (name.length() == 0)
            return;

        //split the string using 'space'
        //and print the first character of every word
        String words[] = name.split(" ");
        for(String word : words) {
            System.out.print(Character.toUpperCase(word.charAt(0)) + " ");
        }
    }

    // Driver code
    public static void main(String args[])
    {
        String name = "prabhat kumar singh";
        printInitials(name);
    }
}
```

## 蟒蛇 3

```
# Python3 program to print initials of a name
def printInitials(name):

    if (len(name) == 0):
        return

    # Split the string using 'space'
    # and print the first character of
    # every word
    words = name.split(" ")
    for word in words:
        print(word[0].upper(), end = " ")

# Driver code
if __name__ == '__main__':

    name = "prabhat kumar singh"
    printInitials(name)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to print initials of a name
using System;

public class initials {

    static void printInitials(String name)
    {
        if (name.Length == 0)
            return;

        //split the string using 'space'
        //and print the first character of every word
        String []words = name.Split(' ');
        foreach(String word in words) {
            Console.Write(char.ToUpper(word[0]) + " ");
        }
    }

    // Driver code
    public static void Main(String []args)
    {
        String name = "prabhat kumar singh";
        printInitials(name);
    }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// javascript program to print initials of a name
    function printInitials( name) {
        if (name.length == 0)
            return;

        // split the string using 'space'
        // and print the first character of every word
        var words = name.split(" ");

        words.forEach(myFunction);

    }
    function myFunction(item) {
 document.write((item[0].toUpperCase()) + " ");
}

    // Driver code
        var name = "prabhat kumar singh";
        printInitials(name);

// This code is contributed by gauravrajput1
</script>
```

**输出:**

```
P K S
```

该代码的复杂性将小于 O(w)，其中 w 是句子中的字数，这可能比 String 中的字符数好不了多少。
这段代码是 Anuj Khasgiwala
贡献的，我们也可以用 C/C++ 中的 [strtok()函数来实现。](https://www.geeksforgeeks.org/strtok-strtok_r-functions-c-examples/) 

本文由**普拉巴特库马尔辛格**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。