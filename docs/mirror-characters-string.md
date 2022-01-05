# 字符串的镜像字符

> 原文:[https://www.geeksforgeeks.org/mirror-characters-string/](https://www.geeksforgeeks.org/mirror-characters-string/)

给定一个字符串和一个数字 N，我们需要按照字母顺序将字符从第 N 个位置镜像到字符串的长度。在镜像操作中，我们将“a”改为“z”，“b”改为“y”等等。
示例:

```
Input : N = 3
        paradox
Output : paizwlc
We mirror characters from position 3 to end.

Input : N = 6
        pneumonia
Output : pnefnlmrz
```

下面是不同的角色和他们的镜子。
![a b c d e f g h i j k l m || n o p q r s t u v w x y z ](img/5d2ef2a82a92da9e88e434036dc2ac42.png "Rendered by QuickLaTeX.com")
按照字母顺序镜像表示 *a* 对应 *z* ， *b* 对应 *y* 。也就是说第一个字符变成最后一个，以此类推。现在，为了实现这一点，我们维护一个包含小写英文字母的字符串(或字符数组)。现在从轴点到长度，我们可以通过使用字符的 ASCII 值作为索引来查找字符的*反向字母顺序*。使用上述技术，我们将给定的字符串转换为所需的字符串。

## C++

```
// C++ code to find the reverse alphabetical
// order from a given position
#include <iostream>
#include <string>
using namespace std;

// Function which take the given string
// and the position from which the reversing shall
// be done and returns the modified string
string compute(string str, int n)
{
    // Creating a string having reversed alphabetical order
    string reverseAlphabet = "zyxwvutsrqponmlkjihgfedcba";
    int l = str.length();

    // The string up to the point specified in the question,
    // the string remains unchanged and from the point up to
    // the length of the string, we reverse the alphabetical
    // order
    for (int i = n; i < l; i++)
        str[i] = reverseAlphabet[str[i] - 'a'];

    return str;
}

// Driver function
int main()
{
    string str = "pneumonia";
    int n = 4;
    string answer = compute(str, n - 1);
    cout << answer;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find the reverse alphabetical
// order from a given position
import java.io.*;

class GeeksforGeeks {

    // Function which take the given string
    // and the position from which the reversing shall
    // be done and returns the modified string
    static String compute(String str, int n)
    {

        // Creating a string having reversed alphabetical order
        String reverseAlphabet = "zyxwvutsrqponmlkjihgfedcba";
        int l = str.length();

        // The string up to the point specified in the question,
        // the string remains unchanged and from the point up to
        // the length of the string, we reverse the alphabetical order
        String answer = "";
        for (int i = 0; i < n; i++)
            answer = answer + str.charAt(i);
        for (int i = n; i < l; i++)
            answer = answer + reverseAlphabet.charAt(str.charAt(i) - 'a');
        return answer;
    }

    // Driver function
    public static void main(String args[])
    {
        String str = "pneumonia";
        int n = 4;
        System.out.print(compute(str, n - 1));
    }
}
```

## 蟒蛇 3

```
# python code to find the reverse
# alphabetical order from a given
# position

# Function which take the given string and the
# position from which the reversing shall be
# done and returns the modified string
def compute(st, n):

    # Creating a string having reversed
    # alphabetical order
    reverseAlphabet = "zyxwvutsrqponmlkjihgfedcba"
    l = len(st)

    # The string up to the point specified in the
    # question, the string remains unchanged and
    # from the point up to the length of the
    # string, we reverse the alphabetical order
    answer = ""
    for i in range(0, n):
        answer = answer + st[i];

    for i in range(n, l):
        answer = (answer +
        reverseAlphabet[ord(st[i]) - ord('a')]);

    return answer;

# Driver function
st = "pneumonia"
n = 4
answer = compute(st, n - 1)
print(answer)

# This code is contributed by Sam007.
```

## C#

```
// C# code to find the reverse alphabetical
// order from a given position
using System;

class GFG {

    // Function which take the given string
    // and the position from which the
    // reversing shall be done and returns
    // the modified string
    static String compute(string str, int n)
    {

        // Creating a string having reversed
        // alphabetical order
        string reverseAlphabet =
               "zyxwvutsrqponmlkjihgfedcba";
        int l = str.Length;

        // The string up to the point
        // specified in the question,
        // the string remains unchanged
        // and from the point up to
        // the length of the string, we
        // reverse the alphabetical order
        String answer = "";

        for (int i = 0; i < n; i++)
            answer = answer + str[i];

        for (int i = n; i < l; i++)
            answer = answer +
               reverseAlphabet[str[i]- 'a'];
        return answer;
    }

    // Driver function
    public static void Main()
    {
        string str = "pneumonia";
        int n = 4;
        Console.Write(compute(str, n - 1));
    }

}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php code to find the reverse alphabetical
// order from a given position

// Function which take the given string
// and the position from which the reversing
// shall be done and returns the modified
// string
function compute($str, $n)
{
    // Creating a string having reversed
    // alphabetical order
    $reverseAlphabet =
            "zyxwvutsrqponmlkjihgfedcba";
    $l = strlen($str);

    // The string up to the point
    // specified in the question,
    // the string remains unchanged
    // and from the point up to
    // the length of the string, we
    // reverse the alphabetical order
    $answer = "";

    for ($i = 0; $i < $n; $i++)
        $answer = $answer.$str[$i];

    for ($i = $n; $i < $l; $i++){
        $answer = $answer.$reverseAlphabet[
                   ord($str[$i])- ord('a')];
    }

    return $answer;
}

// Driver function
    $str = "pneumonia";
    $n = 4;
    $answer = compute($str, $n - 1);
    echo $answer;

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
    // Javascript code to find the reverse alphabetical
    // order from a given position

    // Function which take the given string
    // and the position from which the
    // reversing shall be done and returns
    // the modified string
    function compute(str, n)
    {

        // Creating a string having reversed
        // alphabetical order
        let reverseAlphabet =
               "zyxwvutsrqponmlkjihgfedcba";
        let l = str.length;

        // The string up to the point
        // specified in the question,
        // the string remains unchanged
        // and from the point up to
        // the length of the string, we
        // reverse the alphabetical order
        let answer = "";

        for (let i = 0; i < n; i++)
            answer = answer + str[i];

        for (let i = n; i < l; i++)
            answer = answer + reverseAlphabet[str[i].charCodeAt()- 'a'.charCodeAt()];
        return answer;
    }

    let str = "pneumonia";
    let n = 4;
    document.write(compute(str, n - 1));

</script>
```

输出:

```
pnefnlmrz
```

复杂度= ![O(length) ](img/5a6031c7ebfc112f35a426970f30856b.png "Rendered by QuickLaTeX.com")