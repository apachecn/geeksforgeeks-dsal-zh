# 将给定的 BCD 转换为其等效的二进制形式

> 原文:[https://www . geesforgeks . org/convert-the-given-BCD-to-其等效二进制形式/](https://www.geeksforgeeks.org/convert-the-given-bcd-to-its-equivalent-binary-form/)

给定一个 **BCD(二进制编码十进制)**，任务是将其转换为其等价的**二进制数**。
**例:**

> **输入:** 1001000
> **输出:** 110000
> **说明:**
> 给定 BCD 的整数值为 48(0100 - > 4，1000 - > 8)。
> (48)<sub>10</sub>=(110000)<sub>2</sub>
> **输入:** 1001001
> **输出:** 110001

**方法:**为了解决这个问题，我们需要将给定的 BCD 编号拆分为长度为 4 的二进制组块，并逐一将其转换为整数，以生成给定 BCD 的最终整数表示。生成后，将整数转换为二进制形式。
以下是上述办法的实施情况。

## C++

```
// C++ code to convert BCD to its
// equivalent Binary

#include <bits/stdc++.h>
using namespace std;

// Function to convert BCD to Decimal
string bcdToBinary(string s)
{
    int l = s.length();
    int num = 0;
    int mul = 1;
    int sum = 0;

     // If the length of given BCD is not
    // divisible by 4
    for (int i = l % 4 - 1; i >= 0; i--)
    {
        sum += (s[i] - '0') * mul;
        mul *= 2;
    }
    num = sum;
    sum = 0;
    mul = pow(2, 3);
    int ctr = 0;
    for (int i = l % 4; i < l; i++)
    {
        ctr++;
        sum += (s[i] - '0') * mul;
        mul /= 2;
        if (ctr == 4) {
            num = num * 10 + sum;
            sum = 0;
            mul = pow(2, 3);
            ctr = 0;
        }
    }

    // Convert decimal to binary
    string ans = "";
    while (num > 0) {
        ans += (char)(num % 2 + '0');
        num /= 2;
    }
    reverse(ans.begin(), ans.end());
    return ans;
}

// Driver Code
int main()
{
    string s = "1001000";

    // Function Call
    cout << bcdToBinary(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to convert BCD to its
// equivalent Binary
import java.io.*;
import java.util.*;

class GFG{

// Function to convert BCD to Decimal
static String bcdToBinary(String s)
{
    int l = s.length();
    int num = 0;
    int mul = 1;
    int sum = 0;

    // If the length of given BCD is not
    // divisible by 4
    for(int i = l % 4 - 1; i >= 0; i--)
    {
        sum += (s.charAt(i) - '0') * mul;
        mul *= 2;
    }

    num = sum;
    sum = 0;
    mul = (int)Math.pow(2, 3);
    int ctr = 0;

    for(int i = l % 4; i < l; i++)
    {
        ctr++;
        sum += (s.charAt(i) - '0') * mul;
        mul /= 2;

        if (ctr == 4)
        {
            num = num * 10 + sum;
            sum = 0;
            mul = (int)Math.pow(2, 3);
            ctr = 0;
        }
    }

    // Convert decimal to binary
    String ans = "";
    while (num > 0)
    {
        ans += (char)(num % 2 + '0');
        num /= 2;
    }

    StringBuilder ans1 = new StringBuilder();

    // Append a string into StringBuilder input1
    ans1.append(ans);

    // Reverse StringBuilder input1
    ans = ans1.reverse().toString();

    return ans;
}

// Driver code
public static void main(String[] args)
{
    String s = "1001000";

    // Function call
    System.out.println(bcdToBinary(s));
}
}

// This code is contributed by coder001
```

## 蟒蛇 3

```
# Python3 code to convert
# BCD to its equivalent Binary

# Function to convert
# BCD to Decimal
def bcdToBinary(s):

    l = len(s)
    num = 0;
    mul = 1;
    sum = 0;

    # If the length of given
    # BCD is not divisible by 4   
    for i in range(l % 4 - 1,
                   -1, -1):   
        sum += (ord(s[i]) -
                ord('0')) * mul;
        mul *= 2;

    num = sum;
    sum = 0;
    mul = pow(2, 3);
    ctr = 0;

    for i in range(l % 4, l):   
        ctr += 1;
        sum += (ord(s[i]) -
                ord('0')) * mul;
        mul //= 2;
        if (ctr == 4):
            num = num * 10 + sum;
            sum = 0;
            mul = pow(2, 3);
            ctr = 0;       

    # Convert decimal to binary
    ans = "";
    while (num > 0):
        ans += (chr((num % 2) +
                ord('0')));
        num //= 2;
    ans = ans[:: -1]

    return ans;

# Driver code
if __name__ == "__main__":

    s = "1001000";

    # Function Call
    print(bcdToBinary(s));

# This code is contributed by rutvik_56
```

## C#

```
// C# code to convert BCD to its
// equivalent Binary
using System;
using System.Text;
public class GFG{

// Function to convert BCD to Decimal
static String bcdToBinary(String s)
{
    int l = s.Length;
    int num = 0;
    int mul = 1;
    int sum = 0;

    // If the length of given BCD is not
    // divisible by 4
    for(int i = l % 4 - 1; i >= 0; i--)
    {
        sum += (s[i] - '0') * mul;
        mul *= 2;
    }
    num = sum;
    sum = 0;
    mul = (int)Math.Pow(2, 3);
    int ctr = 0;
    for(int i = l % 4; i < l; i++)
    {
        ctr++;
        sum += (s[i] - '0') * mul;
        mul /= 2;
        if (ctr == 4)
        {
            num = num * 10 + sum;
            sum = 0;
            mul = (int)Math.Pow(2, 3);
            ctr = 0;
        }
    }

    // Convert decimal to binary
    String ans = "";
    while (num > 0)
    {
        ans += (char)(num % 2 + '0');
        num /= 2;
    }
    StringBuilder ans1 = new StringBuilder();

    // Append a string into StringBuilder input1
    ans1.Append(ans);

    // Reverse StringBuilder input1
    ans = reverse(ans1.ToString());
    return ans;
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

// Driver code
public static void Main(String[] args)
{
    String s = "1001000";

    // Function call
    Console.WriteLine(bcdToBinary(s));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript code to convert BCD to its
// equivalent Binary

// Function to convert BCD to Decimal
function bcdToBinary(s)
{
    let l = s.length;
    let num = 0;
    let mul = 1;
    let sum = 0;

    // If the length of given BCD is not
    // divisible by 4
    for (let i = l % 4 - 1; i >= 0; i--)
    {
        sum += (s[i].charCodeAt(0) - '0'.charCodeAt(0)) * mul;
        mul *= 2;
    }
    num = sum;
    sum = 0;
    mul = Math.pow(2, 3);
    let ctr = 0;
    for (let i = l % 4; i < l; i++) {
        ctr++;
        sum += (s[i].charCodeAt(0) - '0'.charCodeAt(0)) * mul;
        mul = Math.floor(mul / 2);
        if (ctr == 4) {
            num = num * 10 + sum;
            sum = 0;
            mul = Math.pow(2, 3);
            ctr = 0;
        }
    }

    // Convert decimal to binary
    let ans = "";
    while (num > 0) {
        ans += String.fromCharCode(num % 2 + '0'.charCodeAt(0));
        num = Math.floor(num / 2);
    }
    ans = ans.split("").reverse().join("")
    console.log(ans)
    return ans;
}

// Driver Code
let s = "1001000";

// Function Call
document.write(bcdToBinary(s));

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
110000
```

**时间复杂度:** *O(N)* 其中 N 表示提供的 BCD 字符串的长度
**辅助空间:** *O(1)*