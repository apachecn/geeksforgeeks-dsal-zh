# 反转给定字符串中的元音

> 原文:[https://www.geeksforgeeks.org/reverse-vowels-given-string/](https://www.geeksforgeeks.org/reverse-vowels-given-string/)

给定一个字符串，你的任务是只反转字符串的元音。
**例:**

```
Input : hello
Output : holle

Input : hello world
Output : hollo werld
```

一个简单的解决方案是在扫描字符串时存储所有元音，并在字符串的另一次迭代中以相反的顺序放置元音。

## C++

```
// C++ program to reverse order of vowels
#include<bits/stdc++.h>
using namespace std;

// utility function to check for vowel
bool isVowel(char c)
{
    return (c=='a' || c=='A' || c=='e' ||
            c=='E' || c=='i' || c=='I' ||
            c=='o' || c=='O' || c=='u' ||
            c=='U');
}

// Function to reverse order of vowels
string reverseVowel(string str)
{
    int j=0;
    // Storing the vowels separately
    string vowel;
    for (int i=0; str[i]!='\0'; i++)
        if (isVowel(str[i]))
            vowel[j++] = str[i];

    // Placing the vowels in the reverse
    // order in the string
    for (int i=0; str[i]!='\0'; i++)
        if (isVowel(str[i]))
            str[i] = vowel[--j] ;

    return str;
}

// Driver function
int main()
{
    string str = "hello world";
    cout << reverseVowel(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reverse order of vowels

class GFG {

// utility function to check for vowel
    static boolean isVowel(char c) {
        return (c == 'a' || c == 'A' || c == 'e'
                || c == 'E' || c == 'i' || c == 'I'
                || c == 'o' || c == 'O' || c == 'u'
                || c == 'U');
    }

// Function to reverse order of vowels
    static String reverseVowel(String str1) {
        int j = 0;
        // Storing the vowels separately
        char[] str = str1.toCharArray();
        String vowel = "";
        for (int i = 0; i < str.length; i++) {
            if (isVowel(str[i])) {
                j++;
                vowel += str[i];
            }
        }

        // Placing the vowels in the reverse
        // order in the string
        for (int i = 0; i < str.length; i++) {
            if (isVowel(str[i])) {
                str[i] = vowel.charAt(--j);
            }
        }

        return String.valueOf(str);
    }

// Driver function
    public static void main(String[] args) {
        String str = "hello world";
        System.out.println(reverseVowel(str));
    }
}

// This code is contributed by princiRaj1992
```

## 蟒蛇 3

```
# Python3 program to reverse order of vowels

# utility function to check for vowel
def isVowel(c):
    if (c == 'a' or c == 'A' or c == 'e' or
        c == 'E' or c == 'i' or c == 'I' or
        c == 'o' or c == 'O' or c == 'u' or c == 'U'):
        return True
    return False

# Function to reverse order of vowels
def reverserVowel(string):
    j = 0
    vowel = [0] * len(string)
    string = list(string)

    # Storing the vowels separately
    for i in range(len(string)):
        if isVowel(string[i]):
            vowel[j] = string[i]
            j += 1

    # Placing the vowels in the reverse
    # order in the string
    for i in range(len(string)):
        if isVowel(string[i]):
            j -= 1
            string[i] = vowel[j]

    return ''.join(string)

# Driver Code
if __name__ == "__main__":
    string = "hello world"
    print(reverserVowel(string))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to reverse order of vowels
using System;

class GFG
{

    // utility function to check for vowel
    static bool isVowel(char c)
    {
        return (c == 'a' || c == 'A' || c == 'e'
                || c == 'E' || c == 'i' || c == 'I'
                || c == 'o' || c == 'O' || c == 'u'
                || c == 'U');
    }

    // Function to reverse order of vowels
    static String reverseVowel(String str1)
    {
        int j = 0;

        // Storing the vowels separately
        char[] str = str1.ToCharArray();
        String vowel = "";
        for (int i = 0; i < str.Length; i++)
        {
            if (isVowel(str[i]))
            {
                j++;
                vowel += str[i];
            }
        }

        // Placing the vowels in the reverse
        // order in the string
        for (int i = 0; i < str.Length; i++)
        {
            if (isVowel(str[i]))
            {
                str[i] = vowel[--j];
            }
        }

        return String.Join("",str);
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "hello world";
        Console.WriteLine(reverseVowel(str));
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript program to reverse order of vowels

    // utility function to check for vowel
    function isVowel(c) {
        return (c == 'a' || c == 'A' || c == 'e'
                || c == 'E' || c == 'i' || c == 'I'
                || c == 'o' || c == 'O' || c == 'u'
                || c == 'U');
    }

    // Function to reverse order of vowels
    function reverseVowel(str1) {
        let j = 0;
        // Storing the vowels separately
        let str = str1.split('');
        let vowel = "";
        for (let i = 0; i < str.length; i++) {
            if (isVowel(str[i])) {
                j++;
                vowel += str[i];
            }
        }

        // Placing the vowels in the reverse
        // order in the string
        for (let i = 0; i < str.length; i++) {
            if (isVowel(str[i])) {
                str[i] = vowel[--j];
            }
        }

        return str.join("");
    }

    let str = "hello world";
      document.write(reverseVowel(str));

</script>
```

**输出:**

```
hollo werld
```

**时间复杂度:** O(n)其中 n =字符串长度
**辅助空间:** O(v)其中 v =字符串中元音个数
**更好的解决方案**是使用两个指针分别从数组的开始和结束进行扫描，并对这些指针指向的元音进行操作。

## C++

```
// C++ program to reverse order of vowels
#include<bits/stdc++.h>
using namespace std;

// utility function to check for vowel
bool isVowel(char c)
{
    return (c=='a' || c=='A' || c=='e' ||
            c=='E' || c=='i' || c=='I' ||
            c=='o' || c=='O' || c=='u' ||
            c=='U');
}

// Function to reverse order of vowels
string reverseVowel(string str)
{
    // Start two indexes from two corners
    // and move toward each other
    int i = 0;
    int j = str.length()-1;
    while (i < j)
    {
        if (!isVowel(str[i]))
        {
            i++;
            continue;
        }
        if (!isVowel(str[j]))
        {
            j--;
            continue;
        }

        // swapping
        swap(str[i], str[j]);

        i++;
        j--;
    }

    return str;
}

// Driver function
int main()
{
    string str = "hello world";
    cout << reverseVowel(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reverse order of vowels

class GFG {

// utility function to check for vowel
    static boolean isVowel(char c) {
        return (c == 'a' || c == 'A' || c == 'e'
                || c == 'E' || c == 'i' || c == 'I'
                || c == 'o' || c == 'O' || c == 'u'
                || c == 'U');
    }

// Function to reverse order of vowels
static String reverseVowel(String str) {
    // Start two indexes from two corners
    // and move toward each other
    int i = 0;
    int j = str.length()-1;
    char[] str1 = str.toCharArray();
    while (i < j)
    {
        if (!isVowel(str1[i]))
        {
            i++;
            continue;
        }
        if (!isVowel(str1[j]))
        {
            j--;
            continue;
        }

        // swapping
        char t = str1[i];
        str1[i]= str1[j];
        str1[j]= t;

        i++;
        j--;
    }
    String str2 = String.copyValueOf(str1);
    return str2;
}

// Driver function
    public static void main(String[] args) {
        String str = "hello world";
        System.out.println(reverseVowel(str));
    }
}
```

## 蟒蛇 3

```
# Python3 program to reverse order of vowels

# utility function to check for vowel
def isVowel(c):
    return (c=='a' or c=='A' or c=='e' or
            c=='E' or c=='i' or c=='I' or
            c=='o' or c=='O' or c=='u' or
            c=='U')

# Function to reverse order of vowels
def reverseVowel(str):

    # Start two indexes from two corners
    # and move toward each other
    i = 0
    j = len(str) - 1
    while (i < j):
        if not isVowel(str[i]):
            i += 1
            continue
        if (not isVowel(str[j])):
            j -= 1
            continue

        # swapping
        str[i], str[j] = str[j], str[i]
        i += 1
        j -= 1
    return str

# Driver function
if __name__ == "__main__":
    str = "hello world"
    print(*reverseVowel(list(str)), sep = "")

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program to reverse order of vowels
using System;

class GFG
{

    // utility function to check for vowel
    static Boolean isVowel(char c)
    {
        return (c == 'a' || c == 'A' || c == 'e'
                || c == 'E' || c == 'i' || c == 'I'
                || c == 'o' || c == 'O' || c == 'u'
                || c == 'U');
    }

// Function to reverse order of vowels
static String reverseVowel(String str)
{
    // Start two indexes from two corners
    // and move toward each other
    int i = 0;
    int j = str.Length-1;
    char[] str1 = str.ToCharArray();
    while (i < j)
    {
        if (!isVowel(str1[i]))
        {
            i++;
            continue;
        }
        if (!isVowel(str1[j]))
        {
            j--;
            continue;
        }

        // swapping
        char t = str1[i];
        str1[i]= str1[j];
        str1[j]= t;

        i++;
        j--;
    }
    String str2 = String.Join("",str1);
    return str2;
}

// Driver code
public static void Main(String[] args)
{
    String str = "hello world";
    Console.WriteLine(reverseVowel(str));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to reverse order of vowels

// utility function to check for vowel
function isVowel(c)
{
    return (c == 'a' || c == 'A' || c == 'e'
                || c == 'E' || c == 'i' || c == 'I'
                || c == 'o' || c == 'O' || c == 'u'
                || c == 'U');
}

// Function to reverse order of vowels
function reverseVowel(str)
{
    // Start two indexes from two corners
    // and move toward each other
    let i = 0;
    let j = str.length-1;
    let str1 = str.split("");
    while (i < j)
    {
        if (!isVowel(str1[i]))
        {
            i++;
            continue;
        }
        if (!isVowel(str1[j]))
        {
            j--;
            continue;
        }

        // swapping
        let t = str1[i];
        str1[i]= str1[j];
        str1[j]= t;

        i++;
        j--;
    }
    let str2 = (str1).join("");
    return str2;
}

// Driver function
let str = "hello world";
document.write(reverseVowel(str));

// This code is contributed by rag2127

</script>
```

**输出:**

```
hollo werld
```

**时间复杂度:** O(n)其中 n =弦的长度
**辅助空间:** O(1)
本文由**高拉夫·阿赫瓦尔**和**高拉夫·米格拉尼**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。