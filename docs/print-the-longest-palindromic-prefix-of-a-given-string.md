# 打印给定字符串的最长回文前缀

> 原文:[https://www . geesforgeks . org/print-给定字符串的最长回文前缀/](https://www.geeksforgeeks.org/print-the-longest-palindromic-prefix-of-a-given-string/)

给定一个字符串 **str** ，任务是找到给定字符串的最长回文前缀。

**示例:**

> **输入:** str = "abaac"
> **输出:** aba
> **解释:**
> 给定回文字符串的最长前缀是“aba”。
> 
> **输入:** str = "abacabaxyz"
> **输出:** abacaba
> **解释:**
> 给定回文字符串的前缀是“aba”和“abacabaxyz”。
> 但其中最长的是“abacabaxyz”。

**天真方法:**思路是[从起始索引生成给定字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)的所有子串，检查子串是否回文。最大长度的回文字符串就是结果字符串。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the longest prefix
// which is palindromic
void LongestPalindromicPrefix(string s)
{

    // Find the length of the given string
    int n = s.length();

    // For storing the length of longest
    // prefix palindrome
    int max_len = 0;

    // Loop to check the substring of all
    // length from 1 to N which is palindrome
    for (int len = 1; len <= n; len++) {

        // String of length i
        string temp = s.substr(0, len);

        // To store the reversed of temp
        string temp2 = temp;

        // Reversing string temp2
        reverse(temp2.begin(), temp2.end());

        // If string temp is palindromic
        // then update the length
        if (temp == temp2) {
            max_len = len;
        }
    }

    // Print the palindromic string of
    // max_len
    cout << s.substr(0, max_len);
}

// Driver Code
int main()
{

    // Given string
    string str = "abaab";

    // Function Call
    LongestPalindromicPrefix(str);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to find the longest prefix
// which is palindromic
static void LongestPalindromicPrefix(String s)
{

    // Find the length of the given String
    int n = s.length();

    // For storing the length of longest
    // prefix palindrome
    int max_len = 0;

    // Loop to check the subString of all
    // length from 1 to N which is palindrome
    for (int len = 1; len <= n; len++)
    {

        // String of length i
        String temp = s.substring(0, len);

        // To store the reversed of temp
        String temp2 = temp;

        // Reversing String temp2
        temp2 = reverse(temp2);

        // If String temp is palindromic
        // then update the length
        if (temp.equals(temp2))
        {
            max_len = len;
        }
    }

    // Print the palindromic String of
    // max_len
    System.out.print(s.substring(0, max_len));
}

static String reverse(String input)
{
    char[] a = input.toCharArray();
    int l, r = a.length - 1;
    for (l = 0; l < r; l++, r--)
    {
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return String.valueOf(a);
}

// Driver Code
public static void main(String[] args)
{

    // Given String
    String str = "abaab";

    // Function Call
    LongestPalindromicPrefix(str);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the longest prefix
# which is palindrome
def LongestPalindromicPrefix(string):

    # Find the length of the given string
    n = len(string)

    # For storing the length of longest
    # Prefix Palindrome
    max_len = 0

    # Loop to check the substring of all
    # length from 1 to n which is palindrome
    for length in range(0, n + 1):

        # String of length i
        temp = string[0:length]

        # To store the value of temp
        temp2 = temp

        # Reversing the value of temp
        temp3 = temp2[::-1]

        # If string temp is palindromic
        # then update the length
        if temp == temp3:
            max_len = length

    # Print the palindromic string
    # of max_len
    print(string[0:max_len])

# Driver code
if __name__ == '__main__' :

    string = "abaac";

    # Function call
    LongestPalindromicPrefix(string)

# This code is contributed by virusbuddah_
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the longest prefix
// which is palindromic
static void longestPalindromicPrefix(String s)
{

    // Find the length of the given String
    int n = s.Length;

    // For storing the length of longest
    // prefix palindrome
    int max_len = 0;

    // Loop to check the subString of all
    // length from 1 to N which is palindrome
    for (int len = 1; len <= n; len++)
    {

        // String of length i
        String temp = s.Substring(0, len);

        // To store the reversed of temp
        String temp2 = temp;

        // Reversing String temp2
        temp2 = reverse(temp2);

        // If String temp is palindromic
        // then update the length
        if (temp.Equals(temp2))
        {
            max_len = len;
        }
    }

    // Print the palindromic String of
    // max_len
    Console.Write(s.Substring(0, max_len));
}

static String reverse(String input)
{
    char[] a = input.ToCharArray();
    int l, r = a.Length - 1;
    for (l = 0; l < r; l++, r--)
    {
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return String.Join("",a);
}

// Driver Code
public static void Main(String[] args)
{

    // Given String
    String str = "abaab";

    // Function Call
    longestPalindromicPrefix(str);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach

    // Function to find the longest prefix
    // which is palindromic
    function LongestPalindromicPrefix(s)
    {

        // Find the length of the given String
        let n = s.length;

        // For storing the length of longest
        // prefix palindrome
        let max_len = 0;

        // Loop to check the subString of all
        // length from 1 to N which is palindrome
        for (let len = 1; len <= n; len++)
        {

            // String of length i
            let temp = s.substring(0, len);

            // To store the reversed of temp
            let temp2 = temp;

            // Reversing String temp2
            temp2 = reverse(temp2);

            // If String temp is palindromic
            // then update the length
            if (temp == temp2)
            {
                max_len = len;
            }
        }

        // Print the palindromic String of
        // max_len
        document.write(s.substring(0, max_len));
    }

    function reverse(input)
    {
        let a = input.split('');
        let l, r = a.length - 1;
        for (l = 0; l < r; l++, r--)
        {
            let temp = a[l];
            a[l] = a[r];
            a[r] = temp;
        }
        return a.join("");
    }

    // Given String
    let str = "abaab";

    // Function Call
    LongestPalindromicPrefix(str);

</script>
```

**Output:** 

```
aba
```

**时间复杂度:** *O(N <sup>2</sup> )* ，其中 N 为给定字符串的长度。

**高效途径:**思路是使用预处理算法 [KMP 算法](https://www.geeksforgeeks.org/searching-for-patterns-set-2-kmp-algorithm/)。以下是步骤:

*   创建一个临时字符串(比如 **str2** )，它是:

```
str2 = str + '?' reverse(str);
```

*   创建一个字符串长度大小的数组(比如 **lps[]** )，该数组将存储最长的回文前缀，该前缀也是字符串的后缀 **str2** 。
*   使用 [KMP 搜索算法](https://www.geeksforgeeks.org/kmp-algorithm-for-pattern-searching/)的预处理算法更新 lps[]。
*   **LPS[length(str 2)–1**]将给出给定字符串**字符串**的最长回文前缀字符串的长度。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the longest prefix
// which is palindromic
void LongestPalindromicPrefix(string str)
{

    // Create temporary string
    string temp = str + '?';

    // Reverse the string str
    reverse(str.begin(), str.end());

    // Append string str to temp
    temp += str;

    // Find the length of string temp
    int n = temp.length();

    // lps[] array for string temp
    int lps[n];

    // Initialise every value with zero
    fill(lps, lps + n, 0);

    // Iterate the string temp
    for (int i = 1; i < n; i++) {

        // Length of longest prefix
        // till less than i
        int len = lps[i - 1];

        // Calculate length for i+1
        while (len > 0
               && temp[len] != temp[i]) {
            len = lps[len - 1];
        }

        // If character at current index
        // len are same then increment
        // length by 1
        if (temp[i] == temp[len]) {
            len++;
        }

        // Update the length at current
        // index to len
        lps[i] = len;
    }

    // Print the palindromic string of
    // max_len
    cout << temp.substr(0, lps[n - 1]);
}

// Driver's Code
int main()
{

    // Given string
    string str = "abaab";

    // Function Call
    LongestPalindromicPrefix(str);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the longest
// prefix which is palindromic
static void LongestPalindromicPrefix(String str)
{

    // Create temporary String
    String temp = str + '?';

    // Reverse the String str
    str = reverse(str);

    // Append String str to temp
    temp += str;

    // Find the length of String temp
    int n = temp.length();

    // lps[] array for String temp
    int []lps = new int[n];

    // Initialise every value with zero
    Arrays.fill(lps, 0);

    // Iterate the String temp
    for(int i = 1; i < n; i++)
    {

       // Length of longest prefix
       // till less than i
       int len = lps[i - 1];

       // Calculate length for i+1
       while (len > 0 && temp.charAt(len) !=
                         temp.charAt(i))
       {
           len = lps[len - 1];
       }

       // If character at current index
       // len are same then increment
       // length by 1
       if (temp.charAt(i) == temp.charAt(len))
       {
           len++;
       }

       // Update the length at current
       // index to len
       lps[i] = len;
    }

    // Print the palindromic String
    // of max_len
    System.out.print(temp.substring(0, lps[n - 1]));
}

static String reverse(String input)
{
    char[] a = input.toCharArray();
    int l, r = a.length - 1;

    for(l = 0; l < r; l++, r--)
    {
       char temp = a[l];
       a[l] = a[r];
       a[r] = temp;
    }
    return String.valueOf(a);
}

// Driver Code
public static void main(String[] args)
{

    // Given String
    String str = "abaab";

    // Function Call
    LongestPalindromicPrefix(str);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the longest prefix
# which is palindromic
def LongestPalindromicPrefix(Str):

    # Create temporary string
    temp = Str + "?"

    # Reverse the string Str
    Str = Str[::-1]

    # Append string Str to temp
    temp = temp + Str

    # Find the length of string temp
    n = len(temp)

    # lps[] array for string temp
    lps = [0] * n

    # Iterate the string temp
    for i in range(1, n):

        # Length of longest prefix
        # till less than i
        Len = lps[i - 1]

        # Calculate length for i+1
        while (Len > 0 and temp[Len] != temp[i]):
            Len = lps[Len - 1]

        # If character at current index
        # Len are same then increment
        # length by 1
        if (temp[i] == temp[Len]):
            Len += 1

        # Update the length at current
        # index to Len
        lps[i] = Len

    # Print the palindromic string
    # of max_len
    print(temp[0 : lps[n - 1]])

# Driver Code
if __name__ == '__main__':

    # Given string
    Str = "abaab"

    # Function call
    LongestPalindromicPrefix(Str)

# This code is contributed by himanshu77
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the longest
// prefix which is palindromic
static void longestPalindromicPrefix(String str)
{

    // Create temporary String
    String temp = str + '?';

    // Reverse the String str
    str = reverse(str);

    // Append String str to temp
    temp += str;

    // Find the length of String temp
    int n = temp.Length;

    // lps[] array for String temp
    int []lps = new int[n];

    // Iterate the String temp
    for(int i = 1; i < n; i++)
    {

       // Length of longest prefix
       // till less than i
       int len = lps[i - 1];

       // Calculate length for i+1
       while (len > 0 && temp[len] != temp[i])
       {
           len = lps[len - 1];
       }

       // If character at current index
       // len are same then increment
       // length by 1
       if (temp[i] == temp[len])
       {
           len++;
       }

       // Update the length at current
       // index to len
       lps[i] = len;
    }

    // Print the palindromic String
    // of max_len
    Console.Write(temp.Substring(0, lps[n - 1]));
}

static String reverse(String input)
{
    char[] a = input.ToCharArray();
    int l, r = a.Length - 1;

    for(l = 0; l < r; l++, r--)
    {
       char temp = a[l];
       a[l] = a[r];
       a[r] = temp;
    }
    return String.Join("", a);
}

// Driver Code
public static void Main(String[] args)
{

    // Given String
    String str = "abaab";

    // Function Call
    longestPalindromicPrefix(str);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the longest
// prefix which is palindromic
function longestPalindromicPrefix(str)
{

    // Create temporary String
    let temp = str + '?';

    // Reverse the String str
    str = reverse(str);

    // Append String str to temp
    temp += str;

    // Find the length of String temp
    let n = temp.length;

    // lps[] array for String temp
    let lps = new Array(n);
    lps.fill(0);

    // Iterate the String temp
    for(let i = 1; i < n; i++)
    {

        // Length of longest prefix
        // till less than i
        let len = lps[i - 1];

        // Calculate length for i+1
        while (len > 0 && temp[len] != temp[i])
        {
            len = lps[len - 1];
        }

        // If character at current index
        // len are same then increment
        // length by 1
        if (temp[i] == temp[len])
        {
            len++;
        }

        // Update the length at current
        // index to len
        lps[i] = len;
    }

    // Print the palindromic String
    // of max_len
    document.write(temp.substring(0, lps[n - 1]));
}

function reverse(input)
{
    let a = input.split('');
    let l, r = a.length - 1;

    for(l = 0; l < r; l++, r--)
    {
        let temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return a.join("");
}

// Driver code

// Given String
let str = "abaab";

// Function Call
longestPalindromicPrefix(str);

// This code is contributed by mukesh07

</script>
```

**Output:** 

```
aba
```

**时间复杂度:** *O(N)* ，其中 N 为给定字符串的长度。
**辅助空间:** *O(N)* ，其中 N 为给定字符串的长度。