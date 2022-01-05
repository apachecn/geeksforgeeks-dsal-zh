# 由自然数串联而成的字符串中的第 N 个字符

> 原文:[https://www . geeksforgeeks . org/n-th-由串联自然数构成的字符串字符/](https://www.geeksforgeeks.org/n-th-character-in-the-string-made-by-concatenating-natural-numbers/)

给定一个整数 N，任务是通过连接自然数(从 1 开始的整数)找到字符串中的第 N 个字符。起始字符串将是“12345678910111213 ..”。

**示例**:

```
Input: N = 3 
Output: 3
3rd character in the string "12345678910111213.." is 3.

Input: N = 11
Output: 0
11th character in the string "12345678910111213..." is 0 
```

想法是生成所需的字符串，直到字符串长度不超过 n。

*   初始化一个空字符串，c=1
*   通过将 c 类型转换为字符，将 c 添加到字符串中
*   如果 c 是一位数字，将其附加到字符串中
*   如果 c 大于 9，则将其存储在临时字符串中，并将其反转并追加到原始字符串中
*   如果在任何时刻字符串长度超过 N，则返回 s[n-1]。

下面是上述方法的实现:

## C++

```
// C++ program to find the N-th character
// in the string "1234567891011.."
#include <bits/stdc++.h>
using namespace std;

// Function that returns the N-th character
char NthCharacter(int n)
{
    // initially null string
    string s = "";

    // starting integer
    int c = 1;

    // add integers in string
    for (int i = 1;; i++) {

        // one digit numbers added
        if (c < 10)
            s += char(48 + c);

        // more than 1 digit number, generate
        // equivalent number in a string s1
        // and concatenate s1 into s.
        else
        {
            string s1 = "";
            int dup = c;

            // add the number in string
            while (dup) {
                s1 += char((dup % 10) + 48);
                dup /= 10;
            }

            // reverse the string
            reverse(s1.begin(), s1.end());

            // attach the number
            s += s1;
        }
        c++;

        // if the length exceeds N
        if (s.length() >= n) {
            return s[n - 1];
        }
    }
}

// Driver Code
int main()
{
    int n = 11;

    cout << NthCharacter(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the N-th character
// in the string "1234567891011.."

class GFG
{
    // Function that returns the N-th character
    static char NthCharacter(int n)
    {
        // initially null string
        String s = "";

        // starting integer
        int c = 1;

        // add integers in string
        for (int i = 1;; i++) {

            // one digit numbers added
            if (c < 10)
                s += Integer.toString(c);

            // more than 1 digit number, generate
            // equivalent number in a string s1
            // and concatenate s1 into s.
            else
            {
                String s1 = "";
                int dup = c;

                // add the number in string
                while (dup >0) {
                    s1 += Integer.toString(dup % 10);
                    dup /= 10;
                }

                // reverse the string
                StringBuilder temp = new StringBuilder();
                temp.append(s1);
                temp = temp.reverse();

                // attach the number
                s += temp;
            }
            c++;

            // if the length exceeds N
            if (s.length() >= n) {
                return s.charAt(n - 1);
            }
        }
    }

    // Driver Code
    public static void main(String []args)
    {
        int n = 11;

        System.out.println( NthCharacter(n));

    }

}

// This article is contributed by ihritik
```

## 蟒蛇 3

```
# Python 3 program to find the N-th character
# in the string "1234567891011.."

# Function that returns the N-th character
def NthCharacter(n):

    # initially null string
    s = ""

    # starting integer
    c = 1

    # add integers in string
    while(True) :

        # one digit numbers added
        if (c < 10):
            s += chr(48 + c)

        # more than 1 digit number, generate
        # equivalent number in a string s1
        # and concatenate s1 into s.
        else:
            s1 = ""
            dup = c

            # add the number in string
            while (dup > 0):
                s1 += chr((dup % 10) + 48)
                dup //= 10

            # reverse the string
            s1 = "".join(reversed(s1))

            # attach the number
            s += s1
        c += 1

        # if the length exceeds N
        if (len(s) >= n):
            return s[n - 1]

# Driver Code
if __name__ == "__main__":

    n = 11
    print(NthCharacter(n))

# This code is contributed by ita_c
```

## C#

```
// C# program to find the N-th character
// in the string "1234567891011.."
using System;

class GFG
{
    // Function that returns the N-th character
    static char NthCharacter(int n)
    {
        // initially null string
        String s = "";

        // starting integer
        int c = 1;

        // add integers in string
        for (int i = 1;; i++)
        {

            // one digit numbers added
            if (c < 10)
                s += c.ToString();

            // more than 1 digit number, generate
            // equivalent number in a string s1
            // and concatenate s1 into s.
            else
            {
                String s1 = "";
                int dup = c;

                // add the number in string
                while (dup > 0)
                {
                    s1 += (dup % 10).ToString();
                    dup /= 10;
                }

                // reverse the string
                String temp = reverse(s1);

                // attach the number
                s += temp;
            }
            c++;

            // if the length exceeds N
            if (s.Length >= n)
            {
                return s[n - 1];
            }
        }
    }

    static String reverse(String input)
    {
        char[] a = input.ToCharArray();
        int l, r = 0;
        r = a.Length - 1;

        for (l = 0; l < r; l++, r--)
        {

            // Swap values of l and r
            char temp = a[l];
            a[l] = a[r];
            a[r] = temp;
        }
        return String.Join("", a);
    }

    // Driver Code
    public static void Main(String []args)
    {
        int n = 11;

        Console.WriteLine( NthCharacter(n));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to find the N-th character
// in the string "1234567891011.."

// Function that returns the N-th character
function NthCharacter(n)
{
    // initially null string
        let s = "";

        // starting integer
        let c = 1;

        // add integers in string
        for (let i = 1;; i++) {

            // one digit numbers added
            if (c < 10)
                s += c.toString();

            // more than 1 digit number, generate
            // equivalent number in a string s1
            // and concatenate s1 into s.
            else
            {
                let s1 = "";
                let dup = c;

                // add the number in string
                while (dup >0) {
                    s1 += (dup % 10).toString();
                    dup = Math.floor(dup/10);
                }

                // reverse the string
                s1=s1.split("").reverse().join("");

                // attach the number
                s += s1;
            }
            c++;

            // if the length exceeds N
            if (s.length >= n) {
                return s[n-1];
            }
        }
}

// Driver Code

let n = 11;
document.write( NthCharacter(n));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
0
```