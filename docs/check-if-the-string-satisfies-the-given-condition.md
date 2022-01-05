# 检查字符串是否满足给定条件

> 原文:[https://www . geesforgeks . org/check-如果字符串满足给定条件/](https://www.geeksforgeeks.org/check-if-the-string-satisfies-the-given-condition/)

给定一个字符串 **str** ，任务是检查给定字符串中元音的个数是否为素数。如果它的主要然后打印**是**否则打印**否**。

**示例:**

> **输入:** str = "geeksforgeeks"
> **输出:** YES
> 元音的个数是 5 (e，e，o，e 和 e)，是素数。
> 
> **输入:**输出:否

**方法:**初始化一个变量**计数= 0** 并逐个字符遍历字符串，如果当前字符是元音，则更新**计数=计数+ 1** 。最后，如果**计数**为质数，则打印**是**否则打印**否**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Function that returns true if n is prime
bool prime(int n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function that returns true if c is a vowel
bool isVowel(char c)
{
    c = tolower(c);
    if (c == 'a'
        || c == 'e'
        || c == 'i'
        || c == 'o'
        || c == 'u')
        return true;
    return false;
}

// Function that returns true if the count
// of vowels in word is prime
bool isValidString(string word)
{
    int cnt = 0;

    for (int i = 0; i < word.length(); i++) {
        if (isVowel(word[i]))
            cnt++;
    }

    // If count of vowels is prime
    if (prime(cnt))
        return true;
    else
        return false;
}

// Driver code
int main()
{
    string s = "geeksforgeeks";
    if (isValidString(s))
        cout << "YES";
    else
        cout << "NO";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function that returns true if n is prime
    static boolean prime(int n)
    {
        // Corner cases
        if (n <= 1)
        {
            return false;
        }
        if (n <= 3)
        {
            return true;
        }

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (n % 2 == 0 || n % 3 == 0)
        {
            return false;
        }

        for (int i = 5; i * i <= n; i = i + 6)
        {
            if (n % i == 0 || n % (i + 2) == 0)
            {
                return false;
            }
        }

        return true;
    }

    // Function that returns true if c is a vowel
    static boolean isVowel(char c)
    {
        c = Character.toLowerCase(c);
        if (c == 'a' || c == 'e' ||
            c == 'i' || c == 'o' || c == 'u')
        {
            return true;
        }
        return false;
    }

    // Function that returns true if the count
    // of vowels in word is prime
    static boolean isValidString(String word)
    {
        int cnt = 0;

        for (int i = 0; i < word.length(); i++)
        {
            if (isVowel(word.charAt(i)))
            {
                cnt++;
            }
        }

        // If count of vowels is prime
        if (prime(cnt))
        {
            return true;
        } else
        {
            return false;
        }
    }

    // Driver code
    public static void main(String args[])
    {
        String s = "geeksforgeeks";
        if (isValidString(s))
            System.out.println("YES");
        else
            System.out.println("NO");
    }
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if n is prime
def prime(n):

    # Corner cases
    if (n <= 1):
        return False
    if (n <= 3):
        return True

    # This is checked so that we can skip
    # middle five numbers in below loop
    if (n % 2 == 0 or n % 3 == 0):
        return False

    i = 5
    while i * i <= n:
        if (n % i == 0 or n % (i + 2) == 0):
            return False

        i += 6

    return True

# Function that returns true
# if c is a vowel
def isVowel(c):

    c = c.lower()
    if (c == 'a' or c == 'e' or
        c == 'i' or c == 'o' or
        c == 'u'):
        return True

    return False

# Function that returns true if the
# count of vowels in word is prime
def isValidString(word):

    cnt = 0;

    for i in range(len(word)):
        if (isVowel(word[i])):
            cnt += 1

    # If count of vowels is prime
    if (prime(cnt)):
        return True
    else:
        return False

# Driver code
if __name__=="__main__":

    s = "geeksforgeeks"

    if (isValidString(s)):
        print("YES")
    else:
        print("NO")

# This code is contributed by rutvik_56
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that returns true if n is prime
    static Boolean prime(int n)
    {
        // Corner cases
        if (n <= 1)
        {
            return false;
        }
        if (n <= 3)
        {
            return true;
        }

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (n % 2 == 0 || n % 3 == 0)
        {
            return false;
        }

        for (int i = 5; i * i <= n; i = i + 6)
        {
            if (n % i == 0 || n % (i + 2) == 0)
            {
                return false;
            }
        }

        return true;
    }

    // Function that returns true if c is a vowel
    static Boolean isVowel(char c)
    {
        c = char.ToLower(c);
        if (c == 'a' || c == 'e' ||
            c == 'i' || c == 'o' || c == 'u')
        {
            return true;
        }
        return false;
    }

    // Function that returns true if the count
    // of vowels in word is prime
    static Boolean isValidString(String word)
    {
        int cnt = 0;

        for (int i = 0; i < word.Length; i++)
        {
            if (isVowel(word[i]))
            {
                cnt++;
            }
        }

        // If count of vowels is prime
        if (prime(cnt))
        {
            return true;
        } else
        {
            return false;
        }
    }

    // Driver code
    public static void Main(String []args)
    {
        String s = "geeksforgeeks";
        if (isValidString(s))
            Console.WriteLine("YES");
        else
            Console.WriteLine("NO");
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function that returns true if n is prime
function prime(n)
{
    // Corner cases
        if (n <= 1)
        {
            return false;
        }
        if (n <= 3)
        {
            return true;
        }

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (n % 2 == 0 || n % 3 == 0)
        {
            return false;
        }

        for (let i = 5; i * i <= n; i = i + 6)
        {
            if (n % i == 0 || n % (i + 2) == 0)
            {
                return false;
            }
        }

        return true;
}

// Function that returns true if c is a vowel
function isVowel(c)
{
    c = c.toLowerCase();
        if (c == 'a' || c == 'e' ||
            c == 'i' || c == 'o' || c == 'u')
        {
            return true;
        }
        return false;
}

 // Function that returns true if the count
    // of vowels in word is prime
function isValidString(word)
{
    let cnt = 0;

        for (let i = 0; i < word.length; i++)
        {
            if (isVowel(word[i]))
            {
                cnt++;
            }
        }

        // If count of vowels is prime
        if (prime(cnt))
        {
            return true;
        } else
        {
            return false;
        }
}

// Driver code
let s = "geeksforgeeks";
if (isValidString(s))
    document.write("YES<br>");
else
    document.write("NO<br>");

// This code is contributed by rag2127

</script>
```

**Output:** 

```
YES
```