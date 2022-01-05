# 去掉元音后打印反串

> 原文:[https://www . geesforgeks . org/print-reverse-string-remove-元音/](https://www.geeksforgeeks.org/print-reverse-string-removing-vowels/)

给定一个字符串 **s** ，打印字符串的反串，并从反串中删除原字符串中有元音的字符。
**例:**

```
Input : geeksforgeeks
Output : segrfseg
Explanation :
Reversed string is skeegrofskeeg, removing characters 
from indexes 1, 2, 6, 9 & 10 (0 based indexing),
we get segrfseg .

Input :duck
Output :kud
```

一个**简单的解决方法**就是先倒串，然后遍历倒串，去掉元音。
一个**高效的解决方案**是在一次遍历中完成两个任务。
创建一个空字符串 r，遍历原始字符串 s，并将值赋给字符串 r。检查在该索引处，原始字符串是否包含辅音。如果是，则打印字符串 r 索引处的元素
上述方法的基本实现:

## C++

```
// CPP Program for removing characters
// from reversed string where vowels are
// present in original string
#include <bits/stdc++.h>
using namespace std;

// Function for replacing the string
void replaceOriginal(string s, int n)
{
    // initialize a string of length n
    string r(n, ' ');

    // Traverse through all characters of string
    for (int i = 0; i < n; i++) {

        // assign the value to string r
        // from last index of string s
        r[i] = s[n - 1 - i];

        // if s[i] is a consonant then
        // print r[i]
        if (s[i] != 'a' && s[i] != 'e' && s[i] != 'i'
            && s[i] != 'o' && s[i] != 'u') {
            cout << r[i];
        }
    }
    cout << endl;
}

// Driver function
int main()
{
    string s = "geeksforgeeks";
    int n = s.length();
    replaceOriginal(s, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for removing characters
// from reversed string where vowels are
// present in original string
class GFG {

// Function for replacing the string
    static void replaceOriginal(String s, int n) {
        // initialize a string of length n
        char r[] = new char[n];

        // Traverse through all characters of string
        for (int i = 0; i < n; i++) {

            // assign the value to string r
            // from last index of string s
            r[i] = s.charAt(n - 1 - i);

            // if s[i] is a consonant then
            // print r[i]
            if (s.charAt(i) != 'a' && s.charAt(i) != 'e' && s.charAt(i) != 'i'
                    && s.charAt(i) != 'o' && s.charAt(i) != 'u') {
                System.out.print(r[i]);
            }
        }
        System.out.println("");
    }

// Driver function
    public static void main(String[] args) {
        String s = "geeksforgeeks";
        int n = s.length();
        replaceOriginal(s, n);
    }
}

// This code is contributed by princiRaj1992
```

## 蟒蛇 3

```
# Python3 Program for removing characters
# from reversed string where vowels are
# present in original string

# Function for replacing the string
def replaceOriginal(s, n):

    # initialize a string of length n
    r = [' '] * n

    # Traverse through all characters of string
    for i in range(n):

        # assign the value to string r
        # from last index of string s
        r[i] = s[n - 1 - i]

        # if s[i] is a consonant then
        # print r[i]
        if (s[i] != 'a' and s[i] != 'e' and
            s[i] != 'i' and s[i] != 'o' and
            s[i] != 'u'):
            print(r[i], end = "")
    print()

# Driver Code
if __name__ == "__main__":
    s = "geeksforgeeks"
    n = len(s)
    replaceOriginal(s, n)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# Program for removing characters
// from reversed string where vowels are
// present in original string
using System;

class GFG
{

    // Function for replacing the string
    static void replaceOriginal(String s, int n)
    {
        // initialize a string of length n
        char []r = new char[n];

        // Traverse through all characters of string
        for (int i = 0; i < n; i++)
        {

            // assign the value to string r
            // from last index of string s
            r[i] = s[n - 1 - i];

            // if s[i] is a consonant then
            // print r[i]
            if (s[i] != 'a' && s[i] != 'e' && s[i] != 'i'
                    && s[i] != 'o' && s[i] != 'u')
            {
                Console.Write(r[i]);
            }
        }
        Console.WriteLine("");
    }

    // Driver code
    public static void Main(String[] args)
    {
        String s = "geeksforgeeks";
        int n = s.Length;
        replaceOriginal(s, n);
    }
}

// This code is contributed by Rajput-JI
```

## java 描述语言

```
<script>

// JavaScript Program for removing characters
// from reversed string where vowels are
// present in original string
// Function for replacing the string
function replaceOriginal(s, n)
{

        // initialize a string of length n
        var r = new Array(n);

        // Traverse through all characters of string
        for (var i = 0; i < n; i++) {

            // assign the value to string r
            // from last index of string s
            r[i] = s.charAt(n - 1 - i);

            // if s[i] is a consonant then
            // print r[i]
            if (s.charAt(i) != 'a' && s.charAt(i) != 'e' && s.charAt(i) != 'i'
                    && s.charAt(i) != 'o' && s.charAt(i) != 'u') {
                document.write(r[i]);
            }
        }
        document.write("");
    }

// Driver function
var s = "geeksforgeeks";
var n = s.length;
replaceOriginal(s, n);

// This code is contributed by shivanisinghss2110

</script>
```

**输出:**

```
segrfseg
```