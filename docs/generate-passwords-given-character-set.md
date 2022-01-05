# 从给定的字符集生成所有密码

> 原文:[https://www . geesforgeks . org/generate-passwords-给定-字符集/](https://www.geeksforgeeks.org/generate-passwords-given-character-set/)

给定一组字符，从中生成所有可能的密码。这意味着我们应该使用给定的字符生成所有可能的单词排列，有重复，也达到给定的长度。
**例:**

```
Input : arr[] = {a, b}, 
          len = 2.
Output :
a b aa ab ba bb
```

解决方法是对给定的字符数组使用递归。其思想是将所有可能的长度和一个空字符串最初传递给一个助手函数。在 helper 函数中，我们将所有字符一个接一个地追加到当前字符串中，并重复填充剩余的字符串，直到达到所需的长度。
使用下面的递归树可以更好的可视化:

```
        (a, b)
         /   \
        a     b
       / \   / \
      aa  ab ba bb
```

下面是上述方法的实现。

## C++

```
// C++ program to generate all passwords for given characters
#include <bits/stdc++.h>
using namespace std;

// int cnt;

// Recursive helper function, adds/removes characters
// until len is reached
void generate(char* arr, int i, string s, int len)
{
    // base case
    if (i == 0) // when len has been reached
    {
        // print it out
        cout << s << "\n";
        // cnt++;
        return;
    }

    // iterate through the array
    for (int j = 0; j < len; j++) {

        // Create new string with next character
        // Call generate again until string has
        // reached its len
        string appended = s + arr[j];
        generate(arr, i - 1, appended, len);
    }

    return;
}

// function to generate all possible passwords
void crack(char* arr, int len)
{
    // call for all required lengths
    for (int i = 1; i <= len; i++) {
        generate(arr, i, "", len);
    }
}

// driver function
int main()
{
    char arr[] = { 'a', 'b', 'c' };
    int len = sizeof(arr) / sizeof(arr[0]);
    crack(arr, len);

    //cout << cnt << endl;
    return 0;
}
// This code is contributed by Satish Srinivas.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to generate all passwords for given characters
import java.util.*;

class GFG
{

    // int cnt;
    // Recursive helper function, adds/removes characters
    // until len is reached
    static void generate(char[] arr, int i, String s, int len)
    {
        // base case
        if (i == 0) // when len has been reached
        {
            // print it out
            System.out.println(s);

            // cnt++;
            return;
        }

        // iterate through the array
        for (int j = 0; j < len; j++)
        {

            // Create new string with next character
            // Call generate again until string has
            // reached its len
            String appended = s + arr[j];
            generate(arr, i - 1, appended, len);
        }

        return;
    }

    // function to generate all possible passwords
    static void crack(char[] arr, int len)
    {
        // call for all required lengths
        for (int i = 1; i <= len; i++)
        {
            generate(arr, i, "", len);
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        char arr[] = {'a', 'b', 'c'};
        int len = arr.length;
        crack(arr, len);
    }

}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to
# generate all passwords
# for given characters

# Recursive helper function,
# adds/removes characters
# until len is reached
def generate(arr, i, s, len):

    # base case
    if (i == 0): # when len has
                 # been reached

        # print it out
        print(s)
        return

    # iterate through the array
    for j in range(0, len):

        # Create new string with
        # next character Call
        # generate again until
        # string has reached its len
        appended = s + arr[j]
        generate(arr, i - 1, appended, len)

    return

# function to generate
# all possible passwords
def crack(arr, len):

    # call for all required lengths
    for i in range(1 , len + 1):
        generate(arr, i, "", len)

# Driver Code
arr = ['a', 'b', 'c' ]
len = len(arr)
crack(arr, len)

# This code is contributed by Smita.
```

## C#

```
// C# program to generate all passwords for given characters
using System;

class GFG
{

    // int cnt;
    // Recursive helper function, adds/removes characters
    // until len is reached
    static void generate(char[] arr, int i, String s, int len)
    {
        // base case
        if (i == 0) // when len has been reached
        {
            // print it out
            Console.WriteLine(s);

            // cnt++;
            return;
        }

        // iterate through the array
        for (int j = 0; j < len; j++)
        {

            // Create new string with next character
            // Call generate again until string has
            // reached its len
            String appended = s + arr[j];
            generate(arr, i - 1, appended, len);
        }

        return;
    }

    // function to generate all possible passwords
    static void crack(char[] arr, int len)
    {
        // call for all required lengths
        for (int i = 1; i <= len; i++)
        {
            generate(arr, i, "", len);
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        char []arr = {'a', 'b', 'c'};
        int len = arr.Length;
        crack(arr, len);
    }

}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>
// JavaScript program to generate all passwords for given characters

    // let cnt;
    // Recursive helper function, adds/removes characters
    // until len is reached
    function generate(arr, i, s, len)
    {
        // base case
        if (i == 0) // when len has been reached
        {
            // prlet it out
            document.write(s + "<br/>");

            // cnt++;
            return;
        }

        // iterate through the array
        for (let j = 0; j < len; j++)
        {

            // Create new string with next character
            // Call generate again until string has
            // reached its len
            let appended = s + arr[j];
            generate(arr, i - 1, appended, len);
        }

        return;
    }

    // function to generate all possible passwords
    function crack(arr, len)
    {
        // call for all required lengths
        for (let i = 1; i <= len; i++)
        {
            generate(arr, i, "", len);
        }
    }

// Driver Code

        let arr = ['a', 'b', 'c'];
        let len = arr.length;
        crack(arr, len);

</script>
```

**输出:**

```
a
b
c
aa
ab
ac
ba
bb
bc
ca
cb
cc
aaa
aab
aac
aba
abb
abc
aca
acb
acc
baa
bab
bac
bba
bbb
bbc
bca
bcb
bcc
caa
cab
cac
cba
cbb
cbc
cca
ccb
ccc
```

如果我们想查看字数，我们可以取消代码中有 cnt 变量的行的注释。我们可以观察到它出来是![n^1 + n^2 +..+ n^n  ](img/4202026ab33013f55e4b4dfdaadbd9b5.png "Rendered by QuickLaTeX.com")，其中 n = len。因此程序的时间复杂度也是

```
*** QuickLaTeX cannot compile formula:

*** Error message:
Error: Nothing to show, formula is empty

```

，因此是指数型的。我们也可以在生成时检查特定的密码
，如果找到就中断循环返回。我们还可以包含其他要生成的符号，如果需要，通过使用哈希表预处理输入来移除重复的符号。
本文由 [**萨蒂什·斯里尼瓦斯**](https://disqus.com/by/satish_srinivas/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。