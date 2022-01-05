# 字符串排序

> 原文:[https://www.geeksforgeeks.org/sort-string-characters/](https://www.geeksforgeeks.org/sort-string-characters/)

给定一串来自“a”–“z”的小写字符。我们需要编写一个程序来按排序顺序打印这个字符串的字符。
**例:**

```
Input : bbccdefbbaa 
Output : aabbbbccdef

Input : geeksforgeeks
Output : eeeefggkkorss
```

一种**简单的方法**是使用排序算法，如[快速排序](https://www.geeksforgeeks.org/quick-sort/)或[合并排序](https://www.geeksforgeeks.org/merge-sort/)，对输入字符串进行排序并打印。

## C++

```
// C++ program to sort a string of characters
#include<bits/stdc++.h>
using namespace std;

// function to print string in sorted order
void sortString(string &str)
{
   sort(str.begin(), str.end());
   cout << str;
}

// Driver program to test above function
int main()
{
    string s = "geeksforgeeks";
    sortString(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort a string of characters

import java.util.Arrays;

class GFG {

// function to print string in sorted order
    static void sortString(String str) {
        char []arr = str.toCharArray();
        Arrays.sort(arr);
        System.out.print(String.valueOf(arr));
    }

// Driver program to test above function
    public static void main(String[] args) {
        String s = "geeksforgeeks";
        sortString(s);
    }
}
// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to sort a string
# of characters

# function to print string in
# sorted order
def sortString(str) :
    str = ''.join(sorted(str))
    print(str)

# Driver Code
s = "geeksforgeeks"
sortString(s)

# This code is contributed by Smitha
```

## C#

```
// C# program to sort a string of characters
using System;   
public class GFG {

// function to print string in sorted order
    static void sortString(String str) {
        char []arr = str.ToCharArray();
        Array.Sort(arr);
        Console.WriteLine(String.Join("",arr));
    }

// Driver program to test above function
    public static void Main() {
        String s = "geeksforgeeks";
        sortString(s);
    }
}
// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // javascript program to sort a string of characters

    let MAX_CHAR = 26;

    // function to print string in sorted order
    function sortString(str)
    {

        // Hash array to keep count of characters.
        // Initially count of all characters is
        // initialized to zero.
        let charCount = new Array(MAX_CHAR);
        charCount.fill(0);

        // Traverse string and increment
        // count of characters
        for (let i = 0; i < str.length; i++)

            // 'a'-'a' will be 0, 'b'-'a' will be 1,
            // so for location of character in count
            // array we wil do str[i]-'a'.
            charCount[str[i].charCodeAt()-'a'.charCodeAt()]++;   

        // Traverse the hash array and print
        // characters
        for (let i=0;i<MAX_CHAR;i++)
            for (let j=0;j<charCount[i];j++)
                 document.write(String.fromCharCode('a'.charCodeAt()+i) );
    }

    let s = "geeksforgeeks";   
    sortString(s);   

    // This code is contributed by vaibhavrabadiya117.
</script>
```

**输出:**

```
eeeefggkkorss
```

**时间复杂度:** O(n log n)，其中 n 为字符串长度。
一个**有效的方法**将是首先观察总共只能有 26 个独特的字符。因此，我们可以在散列数组中存储从“a”到“z”的所有字符的出现次数。散列数组的第一个索引将代表字符“a”，第二个将代表“b”等等。最后，我们将简单地遍历散列数组，并打印从“a”到“z”的字符在输入字符串中出现的次数。
以下是上述思路的实现:

## C++

```
// C++ program to sort a string of characters
#include<bits/stdc++.h>
using namespace std;

const int MAX_CHAR = 26;

// function to print string in sorted order
void sortString(string &str)
{
    // Hash array to keep count of characters.
    // Initially count of all characters is
    // initialized to zero.
    int charCount[MAX_CHAR] = {0};

    // Traverse string and increment
    // count of characters
    for (int i=0; i<str.length(); i++)

        // 'a'-'a' will be 0, 'b'-'a' will be 1,
        // so for location of character in count
        // array we will do str[i]-'a'.
        charCount[str[i]-'a']++;   

    // Traverse the hash array and print
    // characters
    for (int i=0;i<MAX_CHAR;i++)
        for (int j=0;j<charCount[i];j++)
            cout << (char)('a'+i);
}

// Driver program to test above function
int main()
{
    string s = "geeksforgeeks";   
    sortString(s);   
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort
// a string of characters
public class SortString{
    static final int MAX_CHAR = 26;

    // function to print string in sorted order
    static void sortString(String str) {

        // Hash array to keep count of characters.
        int letters[] = new int[MAX_CHAR];

        // Traverse string and increment
        // count of characters
        for (char x : str.toCharArray()) {

            // 'a'-'a' will be 0, 'b'-'a' will be 1,
            // so for location of character in count
            // array we will do str[i]-'a'.
            letters[x - 'a']++;
        }

        // Traverse the hash array and print
        // characters
        for (int i = 0; i < MAX_CHAR; i++) {
            for (int j = 0; j < letters[i]; j++) {
                System.out.print((char) (i + 'a'));
            }
        }
    }

    // Driver program to test above function
    public static void main(String[] args) {
        sortString("geeksforgeeks");
    }
}
// This code is contributed
// by Sinuhe
```

## 蟒蛇 3

```
# Python 3 program to sort a string
# of characters

MAX_CHAR = 26

# function to print string in sorted order
def sortString(str):

    # Hash array to keep count of characters.
    # Initially count of all characters is
    # initialized to zero.
    charCount = [0 for i in range(MAX_CHAR)]

    # Traverse string and increment
    # count of characters
    for i in range(0, len(str), 1):

        # 'a'-'a' will be 0, 'b'-'a' will be 1,
        # so for location of character in count
        # array we wil do str[i]-'a'.
        charCount[ord(str[i]) - ord('a')] += 1

    # Traverse the hash array and print
    # characters
    for i in range(0, MAX_CHAR, 1):
        for j in range(0, charCount[i], 1):
            print(chr(ord('a') + i), end = "")

# Driver Code
if __name__ == '__main__':
    s = "geeksforgeeks"
    sortString(s)

# This code is contributed by
# Sahil_Shelangia
```

## C#

```
// C# program to sort
// a string of characters
using System;

class GFG
{

    // Method to sort a
    // string alphabetically
    public static string sortString(string inputString)
    {

        // convert input
        // string to char array
        char[] tempArray = inputString.ToCharArray();

        // sort tempArray
        Array.Sort(tempArray);

        // return new sorted string
        return new string(tempArray);
    }

    // Driver Code
    public static void Main(string[] args)
    {
        string inputString = "geeksforgeeks";

        Console.WriteLine(sortString(inputString));
    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// JavaScript program to sort
// a string of characters

let MAX_CHAR = 26;

// function to print string in sorted order
function sortString(str)
{
// Hash array to keep count of characters.
    let letters=new Array(MAX_CHAR);
    for(let i=0;i<MAX_CHAR;i++)
    {
        letters[i]=0;
    }

     // Traverse string and increment
        // count of characters
    for(let x=0;x<str.length;x++)
    {
        // 'a'-'a' will be 0, 'b'-'a' will be 1,
            // so for location of character in count
            // array we will do str[i]-'a'.
            letters[str[x].charCodeAt(0) - 'a'.charCodeAt(0)]++;
    }
    // Traverse the hash array and print
        // characters
        for (let i = 0; i < MAX_CHAR; i++) {
            for (let j = 0; j < letters[i]; j++) {
                document.write(String.fromCharCode
                (i + 'a'.charCodeAt(0)));
            }
        }
}

// Driver program to test above function
sortString("geeksforgeeks");

// This code is contributed by rag2127

</script>
```

**输出:**

```
eeeefggkkorss
```

**时间复杂度:** O(Max_CHAR*n)，当 Max_CHAR 不变时变成 O(n)，所以总时间复杂度:- O(n)，其中 n 是字符串的长度。
**辅助空间:** O( 1)。
本文由 [**Harsh Agarwal**](https://www.facebook.com/harsh.agarwal.16752) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。