# 根据字数倒串

> 原文:[https://www . geeksforgeeks . org/reverse-string-resident-number-word/](https://www.geeksforgeeks.org/reverse-string-according-number-words/)

给定包含多个单词的字符串。如果字符串中的单词数为偶数，则反转其偶数位置的单词，否则反转其奇数位置，在新字符串的开头推送反转的单词，并按顺序追加剩余的单词。

**示例:**

```
Input:  Ashish Yadav Abhishek Rajput Sunil Pundir
Output: ridnuP tupjaR vadaY Ashish Abhishek Sunil

Input:  Ashish Yadav Abhishek Rajput Sunil Pundir Prem
Output: merP linuS kehsihbA hsihsA Yadav Rajput Pundir 
```

**方法:**如果单词数是偶数，那么偶数位置的单词首先出现，并且也反转该特定单词，如果单词数是奇数，那么奇数位置的单词首先出现，并且也反转该特定单词，然后剩余的单词按顺序追加。例如

> ashish Yadav Abhishek Rajput Sunil Pundir。
> 在上面的字符串中，字数是偶数，然后“Yadav Rajput Pundir”出现在偶数位置，然后最终输出将是:
> ridnuP tup jar vadaY Ashish Abhishek Sunil

## C++

```
// C++ program to reverse string
// according to the number of words
#include <bits/stdc++.h>
using namespace std;

// Reverse the letters of the word
void reverse(char str[], int start, int end)
{

    // Temporary variable to store character
    char temp;
    while (start <= end)
    {
        // Swapping the first and last character
        temp = str[start];
        str[start] = str[end];
        str[end] = temp;
        start++;
        end--;
    }
}

// This function forms the required string
void reverseletter(char str[], int start, int end)
{
    int wstart, wend;
    for (wstart = wend = start; wend < end; wend++)
    {
        if (str[wend] == ' ')
            continue;

        // Checking the number of words
        // present in string to reverse
        while (str[wend] != ' ' && wend <= end)
            wend++;
        wend--;

        // Reverse the letter
        // of the words
        reverse(str, wstart, wend);
    }
}

// Driver Code
int main()
{
    char str[1000] = "Ashish Yadav Abhishek Rajput Sunil Pundir";
    reverseletter(str, 0, strlen(str) - 1);
    cout << str;
    return 0;
}

// This code is contributed by SHUBHAMSINGH10
```

## C

```
// C program to reverse string
// according to the number of words
#include<stdio.h>
#include<string.h>

// Reverse the letters of the word
void reverse(char str[], int start, int end) {

    // Temporary variable to store character
    char temp;
    while (start <= end)
    {
        // Swapping the first and last character
        temp = str[start];
        str[start] = str[end];
        str[end] = temp;
        start++;
        end--;
    }
}

// This function forms the required string
void reverseletter(char str[], int start, int end) {

    int wstart, wend;
    for (wstart = wend = start; wend < end; wend++) {

        if (str[wend] == ' ')
            continue;

        // Checking the number of words
        // present in string to reverse
        while (str[wend] != ' ' && wend <= end)
            wend++;
        wend--;

        //Reverse the letter
        //of the words
        reverse(str, wstart, wend);
    }
}

// Driver Code
int main()
{
    char str[1000] = "Ashish Yadav Abhishek Rajput Sunil Pundir";
    reverseletter(str, 0, strlen(str)-1);
    printf("%s", str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reverse string
// according to the number of words
class GFG
{

    // Reverse the letters of the word
    static void reverse(char str[],
                       int start, int end)
    {

        // Temporary variable to store character
        char temp;
        while (start <= end)
        {
            // Swapping the first and last character
            temp = str[start];
            str[start] = str[end];
            str[end] = temp;
            start++;
            end--;
        }
    }

    // This function forms the required string
    static void reverseletter(char str[],
                            int start, int end)
    {

        int wstart, wend;
        for (wstart = wend = start; wend < end; wend++)
        {

            if (str[wend] == ' ')
            {
                continue;
            }

            // Checking the number of words
            // present in string to reverse
            while (wend <= end && str[wend] != ' ')
            {
                wend++;
            }
            wend--;

            // Reverse the letter
            // of the words
            reverse(str, wstart, wend);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        char str[] = "Ashish Yadav Abhishek Rajput Sunil Pundir".toCharArray();
        reverseletter(str, 0, str.length - 1);
        System.out.printf("%s", String.valueOf(str));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to reverse string
# according to the number of words

# Reverse the letters of the word
def reverse(string, start, end):

    # Temporary variable to store character
    temp = ''
    while start <= end:

        # Swapping the first and last character
        temp = string[start]
        string[start] = string[end]
        string[end] = temp
        start += 1
        end -= 1

# This function forms the required string
def reverseletter(string, start, end):
    wstart, wend = start, start

    while wend < end:
        if string[wend] == " ":
            wend += 1
            continue

        # Checking the number of words
        # present in string to reverse
        while wend <= end and string[wend] != " ":
            wend += 1
        wend -= 1

        # Reverse the letter
        # of the words
        reverse(string, wstart, wend)
        wend += 1

# Driver Code
if __name__ == "__main__":
    string = "Ashish Yadav Abhishek Rajput Sunil Pundir"
    string = list(string)
    reverseletter(string, 0, len(string) - 1)
    print(''.join(string))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to reverse string
// according to the number of words
using System;

class GFG
{

    // Reverse the letters of the word
    static void reverse(char []str,
                       int start, int end)
    {

        // Temporary variable to store character
        char temp;
        while (start <= end)
        {
            // Swapping the first and last character
            temp = str[start];
            str[start] = str[end];
            str[end] = temp;
            start++;
            end--;
        }
    }

    // This function forms the required string
    static void reverseletter(char []str,
                            int start, int end)
    {

        int wstart, wend;
        for (wstart = wend = start; wend < end; wend++)
        {

            if (str[wend] == ' ')
            {
                continue;
            }

            // Checking the number of words
            // present in string to reverse
            while (wend <= end && str[wend] != ' ')
            {
                wend++;
            }
            wend--;

            // Reverse the letter
            // of the words
            reverse(str, wstart, wend);
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        char []str = "Ashish Yadav Abhishek Rajput Sunil Pundir".ToCharArray();
        reverseletter(str, 0, str.Length - 1);
        Console.Write("{0}", String.Join("",str));
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to reverse string
// according to the number of words

// Reverse the letters of the word
function reverse(str,start,end)
{
    // Temporary variable to store character
        let temp;
        while (start <= end)
        {
            // Swapping the first and last character
            temp = str[start];
            str[start] = str[end];
            str[end] = temp;
            start++;
            end--;
        }
}

// This function forms the required string
function reverseletter(str,start,end)
{
    let wstart, wend;
        for (wstart = wend = start; wend < end; wend++)
        {

            if (str[wend] == ' ')
            {
                continue;
            }

            // Checking the number of words
            // present in string to reverse
            while (wend <= end && str[wend] != ' ')
            {
                wend++;
            }
            wend--;

            // Reverse the letter
            // of the words
            reverse(str, wstart, wend);
        }
}

 // Driver Code
let str= "Ashish Yadav Abhishek Rajput Sunil Pundir".split("");
reverseletter(str, 0, str.length - 1);
document.write((str).join(""));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
ridnuP tupjaR vadaY Ashish Abhishek Sunil
```