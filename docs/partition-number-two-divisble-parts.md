# 将一个数分成两个可分割的部分

> 原文:[https://www . geesforgeks . org/partition-number-two-division-parts/](https://www.geeksforgeeks.org/partition-number-two-divisble-parts/)

给定一个数字(如字符串)和两个整数 a 和 b，将字符串分成两个非空部分，这样第一部分可以被 a 整除，第二部分可以被 b 整除。如果字符串不能被分成两个非空部分，输出“否”，否则用这两个部分打印“是”。
**例:**

```
Input  : str = "123", a = 12, b = 3
Output : YES
         12, 3
"12" is divisible by a and "3" is 
divisible by b. 

Input  : str = "1200", a = 4, b = 3
Output : YES
         12, 00

Input  : str = "125", a = 12, b = 3
Output : NO
```

一个**简单的解决方法**就是在所有点的周围逐个划分数组。对于每个分区，检查它的左边和右边是否可以分别被 a 和 b 整除。如果是，打印左右部分并返回。
一个**高效的解决方案**是做一些预处理，通过从左到右扫描字符串并从右到左以“b”为模进行除法运算来保存以“a”为模的除法运算。
如果我们知道前缀从 0 到 I 的余数，当除以 a 时，那么我们用下面的公式计算前缀从 0 到 i+1 的余数。
lr[I+1]=(lr[I]* 10+str[I]-(0))% a .
同样，从右向左扫描可以找到以 b 为模。我们创建另一个 rl[]来存储从右到左为 b 的余数。
一旦我们预先计算了两个余数，我们就可以很容易地找到将字符串分成两部分的点。

## C++

```
// C++ program to check if a string can be splitted
// into two strings such that one is divisible by 'a'
// and other is divisible by 'b'.
#include <bits/stdc++.h>
using namespace std;

// Finds if it is possible to partition str
// into two parts such that first part is
// divisible by a and second part is divisible
// by b.
void findDivision(string &str, int a, int b)
{
    int len = str.length();

    // Create an array of size len+1 and initialize
    // it with 0.
    // Store remainders from left to right when
    // divided by 'a'
    vector<int> lr(len+1, 0);
    lr[0] = (str[0] - '0')%a;
    for (int i=1; i<len; i++)
        lr[i] = ((lr[i-1]*10)%a + (str[i]-'0'))%a;

    // Compute remainders from right to left when
    // divided by 'b'
    vector<int> rl(len+1, 0);
    rl[len-1] = (str[len-1] - '0')%b;
    int power10 = 10;
    for (int i= len-2; i>=0; i--)
    {
        rl[i] = (rl[i+1] + (str[i]-'0')*power10)%b;
        power10 = (power10 * 10) % b;
    }

    // Find a point that can partition a number
    for (int i=0; i<len-1; i++)
    {
        // If split is not possible at this point
        if (lr[i] != 0)
            continue;

        // We can split at i if one of the following
        // two is true.
        // a) All characters after str[i] are 0
        // b) String after str[i] is divisible by b, i.e.,
        //    str[i+1..n-1] is divisible by b.
        if (rl[i+1] == 0)
        {
            cout << "YES\n";
            for (int k=0; k<=i; k++)
                cout << str[k];

            cout << ", ";

            for (int k=i+1; k<len; k++)
                cout << str[k];
            return;
        }
    }

    cout << "NO\n";
}

// Driver code
int main()
{
    string str = "123";
    int a = 12, b = 3;
    findDivision(str, a, b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a string can be splitted
// into two strings such that one is divisible by 'a'
// and other is divisible by 'b'.
class GFG
{

// Finds if it is possible to partition str
// into two parts such that first part is
// divisible by a and second part is divisible
// by b.
static void findDivision(String str, int a, int b)
{
    int len = str.length();

    // Create an array of size len+1 and initialize
    // it with 0.
    // Store remainders from left to right when
    // divided by 'a'
    int[] lr = new int[len + 1];

    lr[0] = ((int)str.charAt(0) - (int)'0')%a;
    for (int i = 1; i < len; i++)
        lr[i] = ((lr[i - 1] * 10) % a +
                ((int)str.charAt(i)-(int)'0')) % a;

    // Compute remainders from right to left when
    // divided by 'b'
    int[] rl = new int[len + 1];
    rl[len - 1] = ((int)str.charAt(len - 1) -
                            (int)'0') % b;
    int power10 = 10;
    for (int i= len - 2; i >= 0; i--)
    {
        rl[i] = (rl[i + 1] + ((int)str.charAt(i) -
                        (int)'0') * power10) % b;
        power10 = (power10 * 10) % b;
    }

    // Find a point that can partition a number
    for (int i = 0; i < len - 1; i++)
    {
        // If split is not possible at this point
        if (lr[i] != 0)
            continue;

        // We can split at i if one of the following
        // two is true.
        // a) All characters after str.charAt(i] are 0
        // b) String after str.charAt(i] is divisible by b, i.e.,
        // str.charAt(i+1..n-1] is divisible by b.
        if (rl[i + 1] == 0)
        {
            System.out.println("YES");
            for (int k = 0; k <= i; k++)
                System.out.print(str.charAt(k));

            System.out.print(", ");

            for (int k = i + 1; k < len; k++)
                System.out.print(str.charAt(k));
            return;
        }
    }
    System.out.println("NO");
}

// Driver code
public static void main (String[] args)
{
    String str = "123";
    int a = 12, b = 3;
    findDivision(str, a, b);
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to check if a can be splitted
# into two strings such that one is divisible by 'a'
# and other is divisible by 'b'.

# Finds if it is possible to partition str
# into two parts such that first part is
# divisible by a and second part is divisible
# by b.
def findDivision(str, a, b):
    lenn = len(str)

    # Create an array of size lenn+1 and
    # initialize it with 0.
    # Store remainders from left to right
    # when divided by 'a'
    lr = [0] * (lenn + 1)
    lr[0] = (int(str[0]))%a
    for i in range(1, lenn):
        lr[i] = ((lr[i - 1] * 10) % a + \
                     int(str[i])) % a

    # Compute remainders from right to left
    # when divided by 'b'
    rl = [0] * (lenn + 1)
    rl[lenn - 1] = int(str[lenn - 1]) % b
    power10 = 10
    for i in range(lenn - 2, -1, -1):
        rl[i] = (rl[i + 1] + int(str[i]) * power10) % b
        power10 = (power10 * 10) % b

    # Find a pothat can partition a number
    for i in range(0, lenn - 1):

        # If split is not possible at this point
        if (lr[i] != 0):
            continue

        # We can split at i if one of the following
        # two is true.
        # a) All characters after str[i] are 0
        # b) after str[i] is divisible by b, i.e.,
        # str[i+1..n-1] is divisible by b.
        if (rl[i + 1] == 0):
            print("YES")
            for k in range(0, i + 1):
                print(str[k], end = "")

            print(",", end = " ")

            for i in range(i + 1, lenn):
                print(str[k], end = "")
                return

    print("NO")

# Driver code
str = "123"
a, b = 12, 3
findDivision(str, a, b)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program to check if a string can be splitted
// into two strings such that one is divisible by 'a'
// and other is divisible by 'b'.
using System;

class GFG
{

// Finds if it is possible to partition str
// into two parts such that first part is
// divisible by a and second part is divisible
// by b.
static void findDivision(string str, int a, int b)
{
    int len = str.Length;

    // Create an array of size len+1 and initialize
    // it with 0.
    // Store remainders from left to right when
    // divided by 'a'
    int[] lr = new int[len + 1];
    lr[0] = ((int)str[0] - (int)'0')%a;

    for (int i = 1; i < len; i++)
        lr[i] = ((lr[i - 1] * 10) % a +
                ((int)str[i] - (int)'0')) % a;

    // Compute remainders from right to left when
    // divided by 'b'
    int[] rl = new int[len + 1];
    rl[len - 1] = ((int)str[len - 1] - (int)'0') % b;

    int power10 = 10;
    for (int i= len - 2; i >= 0; i--)
    {
        rl[i] = (rl[i + 1] + ((int)str[i] -
                (int)'0') * power10) % b;
        power10 = (power10 * 10) % b;
    }

    // Find a point that can partition a number
    for (int i = 0; i < len - 1; i++)
    {
        // If split is not possible at this point
        if (lr[i] != 0)
            continue;

        // We can split at i if one of the following
        // two is true.
        // a) All characters after str[i] are 0
        // b) String after str[i] is divisible by b, i.e.,
        // str[i+1..n-1] is divisible by b.
        if (rl[i + 1] == 0)
        {
            Console.WriteLine("YES");
            for (int k = 0; k <= i; k++)
                Console.Write(str[k]);

            Console.Write(", ");

            for (int k = i + 1; k < len; k++)
                Console.Write(str[k]);
            return;
        }
    }
    Console.WriteLine("NO");
}

// Driver code
static void Main()
{
    string str = "123";
    int a = 12, b = 3;
    findDivision(str, a, b);
}
}

// This code is contributed by mits
```

## java 描述语言

```
<script>

// js program to check if a string can be splitted
// into two strings such that one is divisible by 'a'
// and other is divisible by 'b'.

// Finds if it is possible to partition str
// into two parts such that first part is
// divisible by a and second part is divisible
// by b.
function findDivision(str, a, b)
{
    let len = str.length;

    // Create an array of size len+1 and initialize
    // it with 0.
    // Store remainders from left to right when
    // divided by 'a'
    let lr= [];
    for(let i = 0;i<len+1;i++)
        lr.push(0);
    lr[0] = (str[0] - '0')%a;
    for (let i=1; i<len; i++)
        lr[i] = ((lr[i-1]*10)%a + (str.charCodeAt(i)))%a;

    // Compute remainders from right to left when
    // divided by 'b'
    let rl= [];
    for(let i = 0;i<len+1;i++)
        rl.push(0);
    rl[len-1] = (str.charCodeAt(len-1))%b;
    let power10 = 10;
    for (let i= len-2; i>=0; i--)
    {
        rl[i] = (rl[i+1] + (str.charCodeAt(i))*power10)%b;
        power10 = (power10 * 10) % b;
    }

    // Find a point that can partition a number
    for (let i=0; i<len-1; i++)
    {
        // If split is not possible at this point
        if (lr[i] != 0)
            continue;

        // We can split at i if one of the following
        // two is true.
        // a) All characters after str[i] are 0
        // b) String after str[i] is divisible by b, i.e.,
        //    str[i+1..n-1] is divisible by b.
        if (rl[i+1] == 0)
        {
            document.write("YES<br>");
            for (let k=0; k<=i; k++)
                document.write(str[k]);

            document.write(", ");

            for (let k=i+1; k<len; k++)
                document.write(str[k]);
            return;
        }
    }

    document.write( "NO<br>");
}

// Driver code
    let str = "123";
    let a = 12, b = 3;
    findDivision(str, a, b);

</script>
```

**输出:**

```
YES
12, 3
```

**时间复杂度:** O(len)，其中 len 为输入数字串的长度。
本文由**埃克塔·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息。关于上面讨论的话题