# 如何设计一个微小的 URL 或 URL 缩写器？

> 原文:[https://www . geesforgeks . org/how-to-design-a-tiny-URL-or-URL-short ener/](https://www.geeksforgeeks.org/how-to-design-a-tiny-url-or-url-shortener/)

如何设计一个系统，把像“https://www . geeksforgeeks . org/count-numbers-sum-in-from-1-n/”这样的大网址转换成一个短的 6 个字符的网址。假设网址存储在数据库中，每个网址都有一个相关的整数 id。
需要注意的一点是，长 URL 也应该与短 URL 唯一可识别。所以我们需要一个[双射函数](https://en.wikipedia.org/wiki/Bijection)

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/design-a-tiny-url-or-url-shortener2031/1)

一个简单的解决方案是散列法。使用哈希函数将长字符串转换为短字符串。在哈希中，这可能是冲突(2 个长网址映射到同一个短网址)，我们需要为每个长网址分配一个唯一的短网址，以便我们可以访问长网址。
A **更好的解决方案**是使用存储在数据库中的整数 id，并将整数转换为最多 6 个字符长的字符串。这个问题基本上可以看作是一个基数转换问题，我们有一个 10 位数的输入数字，我们想把它转换成一个 6 个字符长的字符串。
以下是关于 URL 中可能出现的字符的一个重要观察。
网址字符可以是以下之一
1)小写字母['a '到' z']，共 26 个字符
2)大写字母['A '到' Z']，共 26 个字符
3)一个数字['0 '到' 9']，共 10 个字符
共 26 + 26 + 10 = 62 个可能的字符。
所以任务是把一个十进制数转换成以 62 为基数的数。
要获取原始的长 URL，我们需要在数据库中获取 URL id。id 可以通过 62 进制到十进制的转换获得。

## C++

```
// C++ program to generate short url from integer id and
// integer id back from short url.
#include<iostream>
#include<algorithm>
#include<string>
using namespace std;

// Function to generate a short url from integer ID
string idToShortURL(long int n)
{
    // Map to store 62 possible characters
    char map[] = "abcdefghijklmnopqrstuvwxyzABCDEF"
                 "GHIJKLMNOPQRSTUVWXYZ0123456789";

    string shorturl;

    // Convert given integer id to a base 62 number
    while (n)
    {
        // use above map to store actual character
        // in short url
        shorturl.push_back(map[n%62]);
        n = n/62;
    }

    // Reverse shortURL to complete base conversion
    reverse(shorturl.begin(), shorturl.end());

    return shorturl;
}

// Function to get integer ID back from a short url
long int shortURLtoID(string shortURL)
{
    long int id = 0; // initialize result

    // A simple base conversion logic
    for (int i=0; i < shortURL.length(); i++)
    {
        if ('a' <= shortURL[i] && shortURL[i] <= 'z')
          id = id*62 + shortURL[i] - 'a';
        if ('A' <= shortURL[i] && shortURL[i] <= 'Z')
          id = id*62 + shortURL[i] - 'A' + 26;
        if ('0' <= shortURL[i] && shortURL[i] <= '9')
          id = id*62 + shortURL[i] - '0' + 52;
    }
    return id;
}

// Driver program to test above function
int main()
{
    int n = 12345;
    string shorturl = idToShortURL(n);
    cout << "Generated short url is " << shorturl << endl;
    cout << "Id from url is " << shortURLtoID(shorturl);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to generate short url from integer id and
// integer id back from short url.
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{
    // Function to generate a short url from integer ID
    static String idToShortURL(int n)
    {
        // Map to store 62 possible characters
        char map[] = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789".toCharArray();

        StringBuffer shorturl = new StringBuffer();

        // Convert given integer id to a base 62 number
        while (n > 0)
        {
            // use above map to store actual character
            // in short url
            shorturl.append(map[n % 62]);
            n = n / 62;
        }

        // Reverse shortURL to complete base conversion
        return shorturl.reverse().toString();
    }

    // Function to get integer ID back from a short url
    static int shortURLtoID(String shortURL)
    {
        int id = 0; // initialize result

        // A simple base conversion logic
        for (int i = 0; i < shortURL.length(); i++)
        {
            if ('a' <= shortURL.charAt(i) &&
                       shortURL.charAt(i) <= 'z')
            id = id * 62 + shortURL.charAt(i) - 'a';
            if ('A' <= shortURL.charAt(i) &&
                       shortURL.charAt(i) <= 'Z')
            id = id * 62 + shortURL.charAt(i) - 'A' + 26;
            if ('0' <= shortURL.charAt(i) &&
                       shortURL.charAt(i) <= '9')
            id = id * 62 + shortURL.charAt(i) - '0' + 52;
        }
        return id;
    }

    // Driver Code
    public static void main (String[] args) throws IOException
    {
        int n = 12345;
        String shorturl = idToShortURL(n);
        System.out.println("Generated short url is " + shorturl);
        System.out.println("Id from url is " +
                            shortURLtoID(shorturl));
    }
}

// This code is contributed by shubham96301
```

## 蟒蛇 3

```
# Python3 code for above approach
def idToShortURL(id):
    map = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
    shortURL = ""

    # for each digit find the base 62
    while(id > 0):
        shortURL += map[id % 62]
        id //= 62

    # reversing the shortURL
    return shortURL[len(shortURL): : -1]

def shortURLToId(shortURL):
    id = 0
    for i in shortURL:
        val_i = ord(i)
        if(val_i >= ord('a') and val_i <= ord('z')):
            id = id*62 + val_i - ord('a')
        elif(val_i >= ord('A') and val_i <= ord('Z')):
            id = id*62 + val_i - ord('Z') + 26
        else:
            id = id*62 + val_i - ord('0') + 52
    return id

if (__name__ == "__main__"):
    id = 12345
    shortURL = idToShortURL(id)
    print("Short URL from 12345 is : ", shortURL)
    print("ID from", shortURL, "is : ", shortURLToId(shortURL))
```

## C#

```
// C# program to generate short url from integer id and
// integer id back from short url.
using System;

public class GFG
{
    // Function to generate a short url from integer ID
    static String idToShortURL(int n)
    {
        // Map to store 62 possible characters
        char []map = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789".ToCharArray();

        String shorturl = ""; 

        // Convert given integer id to a base 62 number
        while (n > 0)
        {
            // use above map to store actual character
            // in short url
            shorturl+=(map[n % 62]);
            n = n / 62;
        }

        // Reverse shortURL to complete base conversion
        return reverse(shorturl);
    }
    static String reverse(String input) {
        char[] a = input.ToCharArray();
        int l, r = a.Length - 1;
        for (l = 0; l < r; l++, r--) {
            char temp = a[l];
            a[l] = a[r];
            a[r] = temp;
        }
        return String.Join("",a);
    }
    // Function to get integer ID back from a short url
    static int shortURLtoID(String shortURL)
    {
        int id = 0; // initialize result

        // A simple base conversion logic
        for (int i = 0; i < shortURL.Length; i++)
        {
            if ('a' <= shortURL[i] &&
                       shortURL[i] <= 'z')
            id = id * 62 + shortURL[i] - 'a';
            if ('A' <= shortURL[i] &&
                       shortURL[i] <= 'Z')
            id = id * 62 + shortURL[i] - 'A' + 26;
            if ('0' <= shortURL[i] &&
                       shortURL[i] <= '9')
            id = id * 62 + shortURL[i] - '0' + 52;
        }
        return id;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int n = 12345;
        String shorturl = idToShortURL(n);
        Console.WriteLine("Generated short url is " + shorturl);
        Console.WriteLine("Id from url is " +
                            shortURLtoID(shorturl));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to generate short url from integer id and
// integer id back from short url.

// Function to generate a short url from integer ID
function idToShortURL(n)
{

    // Map to store 62 possible characters
    let map = "abcdefghijklmnopqrstuvwxyzABCDEF"
    "GHIJKLMNOPQRSTUVWXYZ0123456789";

    let shorturl = [];

    // Convert given integer id to a base 62 number
    while (n)
    {
        // use above map to store actual character
        // in short url
        shorturl.push(map[n % 62]);
        n = Math.floor(n / 62);
    }

    // Reverse shortURL to complete base conversion
    shorturl.reverse();

    return shorturl.join("");
}

// Function to get integer ID back from a short url
function shortURLtoID(shortURL) {
    let id = 0; // initialize result

    // A simple base conversion logic
    for (let i = 0; i < shortURL.length; i++) {
        if ('a' <= shortURL[i] && shortURL[i] <= 'z')
            id = id * 62 + shortURL[i].charCodeAt(0) - 'a'.charCodeAt(0);
        if ('A' <= shortURL[i] && shortURL[i] <= 'Z')
            id = id * 62 + shortURL[i].charCodeAt(0) - 'A'.charCodeAt(0) + 26;
        if ('0' <= shortURL[i] && shortURL[i] <= '9')
            id = id * 62 + shortURL[i].charCodeAt(0) - '0'.charCodeAt(0) + 52;
    }
    return id;
}

// Driver program to test above function

let n = 12345;
let shorturl = idToShortURL(n);
document.write("Generated short url is " + shorturl + "<br>");
document.write("Id from url is " + shortURLtoID(shorturl));

// This code is contributed by gfgking.
</script>
```

**输出:**

```
Generated short url is dnh
Id from url is 12345
```

优化:我们可以避免 idToShortURL()中的反向步骤。为了确保我们得到相同的 ID，我们还需要更改 shortURLtoID()来从末尾而不是开头处理字符。
本文由**希瓦姆**计算。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。