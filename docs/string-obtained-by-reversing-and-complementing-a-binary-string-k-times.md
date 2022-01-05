# 对二进制字符串进行 K 次反转和补码得到的字符串

> 原文:[https://www . geesforgeks . org/string-通过反转和补充二进制字符串获得-k-times/](https://www.geeksforgeeks.org/string-obtained-by-reversing-and-complementing-a-binary-string-k-times/)

给定一个大小为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)和一个整数 **K** ，任务是对字符串执行 **K** 操作并打印最终字符串:

*   如果操作数是奇数，则反转字符串，
*   如果操作数为偶数，则补字符串。

**示例:**

> **输入:** str = "1011 "，K = 2
> **输出:** 0010
> 第一步后，字符串会反转，变成“1101”。
> 第二步后，字符串会被补全，变成“0010”。
> 
> **输入:** str = "1001 "，K = 4
> **输出:** 1001
> 所有操作后，字符串保持不变。

**天真方法:**
遍历所有 K 步，如果当前步是奇数，则执行反向操作，否则补全字符串。

**有效方法:**观察给定的操作模式后:

*   如果字符串被反转偶数次，则获得原始字符串。
*   同样，如果一个字符串被补偶数次，则得到原始字符串。
*   因此，这些操作只取决于 K 的 [**奇偶**](https://www.geeksforgeeks.org/program-to-find-parity/) **。**
*   因此，我们将计算要执行的反向操作的数量。如果**奇偶性是奇数**，那么我们就反过来。否则字符串将保持不变。
*   同样，我们将计算要执行的补码操作的数量。如果**奇偶性是奇数**，那么我们就补足它。否则字符串将保持不变。

下面是上述方法的实现:

## C++

```
// C++ program to perform K operations upon
// the string and find the modified string
#include <bits/stdc++.h>
using namespace std;

// Function to perform K operations upon
// the string and find modified string
string ReverseComplement(
    string s, int n, int k)
{

    // Number of reverse operations
    int rev = (k + 1) / 2;

    // Number of complement operations
    int complement = k - rev;

    // If rev is odd parity
    if (rev % 2)
        reverse(s.begin(), s.end());

    // If complement is odd parity
    if (complement % 2) {
        for (int i = 0; i < n; i++) {
            // Complementing each position
            if (s[i] == '0')
                s[i] = '1';
            else
                s[i] = '0';
        }
    }

    // Return the modified string
    return s;
}

// Driver Code
int main()
{
    string str = "10011";
    int k = 5;
    int n = str.size();

    // Function call
    cout << ReverseComplement(str, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to perform K operations upon
// the String and find the modified String
class GFG{

// Function to perform K operations upon
// the String and find modified String
static String ReverseComplement(
    char []s, int n, int k)
{

    // Number of reverse operations
    int rev = (k + 1) / 2;

    // Number of complement operations
    int complement = k - rev;

    // If rev is odd parity
    if (rev % 2 == 1)
        s = reverse(s);

    // If complement is odd parity
    if (complement % 2 == 1) {
        for (int i = 0; i < n; i++) {
            // Complementing each position
            if (s[i] == '0')
                s[i] = '1';
            else
                s[i] = '0';
        }
    }

    // Return the modified String
    return String.valueOf(s);
}

static char[] reverse(char a[]) {
    int i, n = a.length;
    char t;
    for (i = 0; i < n / 2; i++) {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
    return a;
}

// Driver Code
public static void main(String[] args)
{
    String str = "10011";
    int k = 5;
    int n = str.length();

    // Function call
    System.out.print(ReverseComplement(str.toCharArray(), n, k));

}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to perform K operations upon
# the string and find the modified string

# Function to perform K operations upon
# the string and find modified string
def ReverseComplement(s,n,k):
    # Number of reverse operations
    rev = (k + 1) // 2

    # Number of complement operations
    complement = k - rev

    # If rev is odd parity
    if (rev % 2):
        s = s[::-1]

    # If complement is odd parity
    if (complement % 2):
        for i in range(n):
            # Complementing each position
            if (s[i] == '0'):
                s[i] = '1'
            else:
                s[i] = '0'

    # Return the modified string
    return s

# Driver Code
if __name__ == '__main__':
    str1 = "10011"
    k = 5
    n = len(str1)

    # Function call
    print(ReverseComplement(str1, n, k))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# program to perform K operations upon
// the String and find the modified String
using System;
class GFG{

// Function to perform K operations upon
// the String and find modified String
static string ReverseComplement(char []s,
                                int n, int k)
{

    // Number of reverse operations
    int rev = (k + 1) / 2;

    // Number of complement operations
    int complement = k - rev;

    // If rev is odd parity
    if (rev % 2 == 1)
        s = reverse(s);

    // If complement is odd parity
    if (complement % 2 == 1)
    {
        for (int i = 0; i < n; i++)
        {
            // Complementing each position
            if (s[i] == '0')
                s[i] = '1';
            else
                s[i] = '0';
        }
    }

    // Return the modified String
    return (new string(s));
}

static char[] reverse(char[] a)
{
    int i, n = a.Length;
    char t;
    for (i = 0; i < n / 2; i++)
    {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
    return a;
}

// Driver Code
public static void Main()
{
    string str = "10011";
    int k = 5;
    int n = str.Length;

    // Function call
    Console.Write(ReverseComplement(str.ToCharArray(), n, k));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program to perform K operations upon
// the string and find the modified string

// Function to perform K operations upon
// the string and find modified string
function ReverseComplement( s, n, k)
{

    // Number of reverse operations
    var rev = parseInt((k + 1) / 2);

    // Number of complement operations
    var complement = k - rev;

    // If rev is odd parity
    if (rev % 2)
    {
       s = s.split('').reverse().join('');
    }

    // If complement is odd parity
    if (complement % 2) {
        for (var i = 0; i < n; i++)
        {

            // Complementing each position
            if (s[i] == '0')
                s[i] = '1';
            else
                s[i] = '0';
        }
    }

    // Return the modified string
    return s;
}

// Driver Code
var str = "10011";
var k = 5;
var n = str.length;

// Function call
document.write( ReverseComplement(str, n, k));

// This code is contributed by famously.
</script>
```

**Output:** 

```
11001
```

***时间复杂度:**O(N)*T4】