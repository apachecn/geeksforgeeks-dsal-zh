# 执行 n 个步骤，将数字的每个数字转换为[计数][数字]

格式

> 原文:[https://www . geesforgeks . org/perform-n-steps-to-convert-format-count digit 中的每一位数字/](https://www.geeksforgeeks.org/perform-n-steps-to-convert-every-digit-of-a-number-in-the-format-countdigit/)

给定一个数字 *num* 作为一个字符串和一个数字 N。任务是编写一个程序，在执行 N 个步骤后，将给定的数字 *num* 转换为另一个数字。在每一步中，num 的每一位数字都会以[计数][数字]的格式写入新的数字中，其中*计数*是一位数字在 num 中连续出现的次数。

**示例:**

> **输入:**num = " 123 "；n = 3
> **输出:** 1321123113
> 对于，n = 1: 123 变成 1 次 1，1 次 2，1 次 3，因此编号为 111213
> 对于，n = 2: 3 乘以 1，1 乘以 2，1 乘以 1，1 乘以 1，1 乘以 3，因此编号为 3112113
> 对于，n = 3: 1 乘以 3，2 乘以 1，1 乘以 2，3 乘以 1，1 乘以 3，因此编号为 13213
> 
> **输入:**num = " 1213 "；n = 1
> T3【输出: 11121113

**方法:**将字符串的字符解析为一个数字，并保持该数字的计数，直到找到不同的数字。一旦找到一个不同的数字，将该数字的计数添加到新字符串中，并对其进行编号。一旦字符串被完全解析，用这个新字符串再次重复这个函数，直到 n 个步骤完成。

下面是上述方法的实现:

## C++

```
// C++ program to convert number
// to the format [count][digit] at every step
#include <bits/stdc++.h>
using namespace std;

// Function to perform every step
void countDigits(string st, int n)
{

    // perform N steps
    if (n > 0) {
        int cnt = 1, i;
        string st2 = "";

        // Traverse in the string
        for (i = 1; i < st.length(); i++) {
            if (st[i] == st[i - 1])
                cnt++;
            else {
                st2 += ('0' + cnt);
                st2 += st[i - 1];
                cnt = 1;
            }
        }

        // for last digit
        st2 += ('0' + cnt);
        st2 += st[i - 1];

        // recur for current string
        countDigits(st2, --n);
    }

    else
        cout << st;
}

// Driver Code
int main()
{

    string num = "123";
    int n = 3;

    countDigits(num, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert number
// to the format [count][digit] at every step
class GFG
{

    // Function to perform every step
    public static void countDigits(String st, int n)
    {

        // perform N steps
        if (n > 0)
        {
            int cnt = 1, i;
            String st2 = "";

            // Traverse in the string
            for (i = 1; i < st.length(); i++)
            {
                if (st.charAt(i) == st.charAt(i - 1))
                    cnt++;
                else
                {
                    st2 += ((char) 0 + (char) cnt);
                    st2 += st.charAt(i - 1);
                    cnt = 1;
                }
            }

            // for last digit
            st2 += ((char) 0 + (char) cnt);
            st2 += st.charAt(i - 1);

            // recur for current string
            countDigits(st2, --n);
        }
        else
            System.out.print(st);
    }

    // Driver Code
    public static void main(String[] args)
    {
        String num = "123";
        int n = 3;
        countDigits(num, n);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python program to convert number
# to the format [count][digit] at every step

# Function to perform every step
def countDigits(st, n):

    # perform N steps
    if (n > 0) :
        cnt = 1
        i = 0
        st2 = ""
        i = 1

        # Traverse in the string
        while (i < len(st) ) :
            if (st[i] == st[i - 1]):
                cnt = cnt + 1
            else :
                st2 += chr(48 + cnt)
                st2 += st[i - 1]
                cnt = 1
            i = i + 1

        # for last digit
        st2 += chr(48 + cnt)
        st2 += st[i - 1]

        # recur for current string
        countDigits(st2, n - 1)
        n = n - 1;

    else:
        print(st)

# Driver Code

num = "123"
n = 3

countDigits(num, n)

# This code is contributed by Arnab Kundu
```

## C#

```
// C# program to convert number
// to the format [count][digit] at every step
using System;
class GFG
{

// Function to perform every step
public static void countDigits(string st, int n)
{

    // perform N steps
    if (n > 0)
    {
        int cnt = 1, i;
        string st2 = "";

        // Traverse in the string
        for (i = 1; i < st.Length; i++)
        {
            if (st[(i)] == st[(i - 1)])
                cnt++;
            else
            {
                st2 += ((char) 0 + (char) cnt);
                st2 += st[(i - 1)];
                cnt = 1;
            }
        }

        // for last digit
        st2 += ((char) 0 + (char) cnt);
        st2 += st[(i - 1)];

        // recur for current string
        countDigits(st2, --n);
    }
    else
        Console.Write(st);
}

// Driver Code
public static void Main()
{
    string num = "123";
    int n = 3;
    countDigits(num, n);
}
}

// This code is contributed by
// Code_Mech.
```

## java 描述语言

```
<script>

// Javascript program to convert number
// to the format [count][digit] at every step

// Function to perform every step
function countDigits(st, n)
{

    // Perform N steps
    if (n > 0)
    {
        let cnt = 1, i;
        let st2 = "";

        // Traverse in the string
        for(i = 1; i < st.length; i++)
        {
            if (st[i] == st[i - 1])
                cnt++;
            else
            {
                st2 += String.fromCharCode(
                    '0'.charCodeAt() + cnt);
                st2 += st[i - 1];
                cnt = 1;
            }
        }

        // For last digit
        st2 += String.fromCharCode(
            '0'.charCodeAt() + cnt);
        st2 += st[i - 1];

        // Recur for current string
        countDigits(st2, --n);
    }
    else
        document.write(st);
}

// Driver code
let num = "123";
let n = 3;

countDigits(num, n);

// This code is contributed by decode2207

</script>
```

**Output:** 

```
1321123113
```