# 将一个数字转换为负基数表示

> 原文:[https://www . geesforgeks . org/convert-number-negative-base-presentation/](https://www.geeksforgeeks.org/convert-number-negative-base-representation/)

给我们一个数字 **n** 和一个负基数**负基数**，我们需要在那个负基数上表示 n。负基数的作用类似于正基数。例如，在基数为 2 的情况下，我们将比特乘以 1、2、4、8 等，得到十进制的实际数字。在基数为 2 的情况下，我们需要将位与 1、-2、4、-8 等相乘，以得到十进制数。
**例:**

```
Input  : n = 13, negBase = -2
Output : 11101
1*(16) + 1*(-8) + 1*(4) + 0*(-2) + 1*(1)  = 13
```

可以用同样的程序将一个数字表示成任意负基数(详见[维基](https://en.wikipedia.org/wiki/Negative_base))。为了简单起见(去掉输出中的 A、B 等字符)，我们只允许基数在-2 到-10 之间。

我们可以解决这个问题，类似于用正基数解决问题，但要记住的一点是，无论我们使用正基数还是负基数，余数总是正的，但是在大多数编译器中，负数除以负数的结果会四舍五入为 0，通常会留下负余数。
所以每当我们得到一个负余数，我们可以把它转换成正余数，如下所示，

```
Let 
n = (?negBase) * quotient + remainder 
  = (?negBase) * quotient + negBase ? negBase + negBase 
  = (?negBase) * (quotient + 1) + (remainder + negBase). 

So if after doing "remainder = n % negBase" and 
"n = n/negBase", we get negative remainder, we do 
following.
remainder = remainder + (-negBase)
n = n + 1

Example : n = -4, negBase = -3
In C++, we get
    remainder = n % negBase = -4/-3 = -1
    n = n/negBase [Next step for base conversion]
      = -4/-3 
      = 1
To avoid negative remainder, we do,
    remainder = -1 + (-negBase) = -1 - (-3) = 2
    n = n + 1 = 1  + 1 = 2.
```

所以当我们得到负余数时，我们将通过给它加上基数的绝对值并给我们的商加上 1 来使它为正。
上述方法在下面的代码
中实现

## C++

```
//  C/C++ program to convert n into negative base form
#include <bits/stdc++.h>
using namespace std;

//  Utility method to convert integer into string
string toString(int n)
{
    string str;
    stringstream ss;
    ss << n;
    ss >> str;
    return str;
}

// Method to convert n to base negBase
string toNegativeBase(int n, int negBase)
{
    //  If n is zero then in any base it will be 0 only
    if (n == 0)
        return "0";

    string converted = "";
    while (n != 0)
    {
        // Get remainder by negative base, it can be
        // negative also
        int remainder = n % negBase;
        n /= negBase;

        // if remainder is negative, add abs(base) to
        // it and add 1 to n
        if (remainder < 0)
        {
            remainder += (-negBase);
            n += 1;
        }

        // convert remainder to string add into the result
        converted = toString(remainder) + converted;
    }

    return converted;
}

//  Driver code to test above methods
int main()
{
    int n = 13;
    int negBase = -2;

    cout << toNegativeBase(n, negBase);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert n into
// negative base form
class GFG
{

// Method to convert n to base negBase
static String toNegativeBase(int n, int negBase)
{
    // If n is zero then in any base
    // it will be 0 only
    if (n == 0)
        return "0";

    String converted = "";
    while (n != 0)
    {
        // Get remainder by negative base,
        // it can be negative also
        int remainder = n % negBase;
        n /= negBase;

        // if remainder is negative,
        // add Math.abs(base) to it
        // and add 1 to n
        if (remainder < 0)
        {
            remainder += (-negBase);
            n += 1;
        }

        // convert remainder to String add into the result
        converted = String.valueOf(remainder) + converted;
    }
    return converted;
}

// Driver Code
public static void main(String[] args)
{
    int n = 13;
    int negBase = -2;

    System.out.print(toNegativeBase(n, negBase));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to convert n into
# negative base form

# Method to convert n to base negBase
def toNegativeBase(n, negBase):

    # If n is zero then in any base it
    # will be 0 only
    if (n == 0):
        return "0"

    converted = "01"
    while (n != 0):

        # Get remainder by negative base,
        # it can be negative also
        remainder = n % (negBase)
        n = int(n/negBase)

        # if remainder is negative, add
        # abs(base) to it and add 1 to n
        if (remainder < 0):
            remainder += ((-1) * negBase)
            n += 1

        # convert remainder to string add
        # into the result
        converted = str(remainder) + converted

    return converted

# Driver Code
if __name__ == '__main__':
    n = 13
    negBase = -2

    print(toNegativeBase(n, negBase))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to convert n into
// negative base form
using System;

class GFG
{

// Method to convert n to base negBase
static String toNegativeBase(int n, int negBase)
{
    // If n is zero then in any base
    // it will be 0 only
    if (n == 0)
        return "0";

    String converted = "";
    while (n != 0)
    {
        // Get remainder by negative base,
        // it can be negative also
        int remainder = n % negBase;
        n /= negBase;

        // if remainder is negative,
        // add Math.Abs(base) to it
        // and add 1 to n
        if (remainder < 0)
        {
            remainder += (-negBase);
            n += 1;
        }

        // convert remainder to String add into the result
        converted = String.Join("", remainder) + converted;
    }
    return converted;
}

// Driver Code
public static void Main(String[] args)
{
    int n = 13;
    int negBase = -2;

    Console.Write(toNegativeBase(n, negBase));
}
}

// This code is contributed by Rajput-Ji
```

**输出:**

```
11101
```

**时间复杂度:** O(N)
**辅助空间:** O(1)
**参考:**
[https://en.wikipedia.org/wiki/Negative_base](https://en.wikipedia.org/wiki/Negative_base)
本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。