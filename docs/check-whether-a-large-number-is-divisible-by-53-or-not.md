# 检查一个大数是否能被 53 整除

> 原文:[https://www . geesforgeks . org/check-一个大数是否能被 53 整除/](https://www.geeksforgeeks.org/check-whether-a-large-number-is-divisible-by-53-or-not/)

给定一个字符串形式的大数 **N** ，任务是检查这个数是否能被 53 整除。

**示例:**

> **输入:**N = 5299947
> T3】输出:是
> 
> **输入:**N = 54
> T3】输出:否

**进场:**

*   提取给定字符串 **N** 的最后一位数字并删除。
*   把那个数字乘以 37。
*   [用剩余数减去](https://www.geeksforgeeks.org/difference-of-two-large-numbers/)上一步计算的乘积。
*   继续，直到我们把给定的字符串减少到一个 3 或 4 位数。
*   将剩余的字符串转换为相应的整数形式，并检查它是否能被 53 整除。

下面是上述方法的实现:

## C++

```
// C++ program to check
// whether a number
// is divisible by 53 or not
#include <bits/stdc++.h>
using namespace std;

// Function to check if the
// number is divisible by 53 or not
bool isDivisible(string s)
{
    int flag = 0;
    while (s.size() > 4) {

        int l = s.size() - 1;
        int x = (s[l] - '0') * 37;

        reverse(s.begin(), s.end());
        s.erase(0, 1);

        int i = 0, carry = 0;
        while (x) {
            int d = (s[i] - '0')
                    - (x % 10)
                    - carry;
            if (d < 0) {
                d += 10;
                carry = 1;
            }
            else
                carry = 0;

            s[i] = (char)(d + '0');
            x /= 10;
            i++;
        }

        while (carry && i < l) {
            int d = (s[i] - '0') - carry;
            if (d < 0) {
                d += 10;
                carry = 1;
            }
            else
                carry = 0;

            s[i] = (char)(d + '0');

            i++;
        }

        reverse(s.begin(), s.end());
    }

    int num = 0;
    for (int i = 0; i < s.size(); i++) {
        num = num * 10 + (s[i] - '0');
    }

    if (num % 53 == 0)
        return true;
    else
        return false;
}

// Driver Code
int main()
{
    string N = "18432462191076";

    if (isDivisible(N))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether 
// a number is divisible by 53 or not
import java.util.*;

class GFG{

// Function to check if the
// number is divisible by 53 or not
static boolean isDivisible(char []s)
{
    while (s.length > 4)
    {
        int l = s.length - 1;
        int x = (s[l] - '0') * 37;

        s = reverse(s);
        s = Arrays.copyOfRange(s, 1, s.length);

        int i = 0, carry = 0;
        while (x > 0) 
        {
            int d = (s[i] - '0') - 
                        (x % 10) - 
                        carry;

            if (d < 0)
            {
                d += 10;
                carry = 1;
            }
            else
                carry = 0;

            s[i] = (char)(d + '0');
            x /= 10;
            i++;
        }

        while (carry > 0 && i < l)
        {
            int d = (s[i] - '0') - carry;
            if (d < 0)
            {
                d += 10;
                carry = 1;
            }
            else
                carry = 0;

            s[i] = (char)(d + '0');
            i++;
        }
        s = reverse(s);
    }

    int num = 0;
    for(int i = 0; i < s.length; i++) 
    {
       num = num * 10 + (s[i] - '0');
    }

    if (num % 53 == 0)
        return true;
    else
        return false;
}

static char[] reverse(char []a)
{
    int l, r = a.length - 1;

    for(l = 0; l < r; l++, r--)
    {
       char temp = a[l];
            a[l] = a[r];
            a[r] = temp;
    }
    return a;
}

// Driver Code
public static void main(String[] args)
{
    String N = "18432462191076";

    if (isDivisible(N.toCharArray()))
        System.out.print("Yes" + "\n");
    else
        System.out.print("No" + "\n");
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program to check whether a  
# number is divisible by 53 or not

# Function to check if the
# number is divisible by 53 or not
def isDivisible(s):

    flag = 0

    while (len(s) > 4):
        l = len(s) - 1
        x = (ord(s[l]) - ord('0')) * 37

        s = s[::-1]
        s = s.replace('0', '', 1)

        i = 0
        carry = 0

        while (x):
            d = ((ord(s[i]) - ord('0')) - 
                 (x % 10) - carry)
            if (d < 0):
                d += 10
                carry = 1
            else:
                carry = 0

            s = s.replace(s[i], chr(d + ord('0')), 1)
            x //= 10
            i += 1

        while (carry and i < l):
            d = (ord(s[i]) - ord('0')) - carry

            if (d < 0):
                d += 10
                carry = 1
            else:
                carry = 0

            s = s.replace(s[i], chr(d + ord('0')), 1)
            i += 1
        s = s[::-1]

    num = 0
    for i in range(len(s)):
        num = num * 10 + (ord(s[i]) - ord('0'))

    if (num % 53 == 0):
        return True
    else:
        return False

# Driver Code
if __name__ == '__main__':

    N = "1843246219106"

    if (isDivisible(N)):
        print("No")
    else:
        print("Yes")

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# program to check whether  
// a number is divisible by 53 or not 
using System; 
using System.Collections; 
using System.Collections.Generic; 

class GFG{

// Function to check if the
// number is divisible by 53 or not
static bool isDivisible(char []s)
{
    while (s.Length > 4)
    {
        int l = s.Length - 1;
        int x = (s[l] - '0') * 37;

        s = reverse(s);

        char []tmp = new char[s.Length - 1];

        Array.Copy(s, 1, tmp, 0, s.Length - 1);
        s = tmp;

        int i = 0, carry = 0;
        while (x > 0) 
        {
            int d = (s[i] - '0') - 
                       (x % 10) - carry;

            if (d < 0)
            {
                d += 10;
                carry = 1;
            }
            else
                carry = 0;

            s[i] = (char)(d + '0');
            x /= 10;
            i++;
        }

        while (carry > 0 && i < l)
        {
            int d = (s[i] - '0') - carry;
            if (d < 0)
            {
                d += 10;
                carry = 1;
            }
            else
                carry = 0;

            s[i] = (char)(d + '0');
            i++;
        }
        s = reverse(s);
    }

    int num = 0;
    for(int i = 0; i < s.Length; i++) 
    {
        num = num * 10 + (s[i] - '0');
    }

    if (num % 53 == 0)
        return true;
    else
        return false;
}

static char[] reverse(char []a)
{
    int l, r = a.Length - 1;

    for(l = 0; l < r; l++, r--)
    {
        char temp = a[l];
             a[l] = a[r];
             a[r] = temp;
    }
    return a;
}

// Driver Code
public static void Main(string[] args)
{
    string N = "18432462191076";

    if (isDivisible(N.ToCharArray()))
        Console.Write("Yes" + "\n");
    else
        Console.Write("No" + "\n");
}
}

// This code is contributed by rutvik_56
```

**Output:**

```
Yes

```