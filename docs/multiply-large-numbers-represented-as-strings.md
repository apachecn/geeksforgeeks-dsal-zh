# 用字符串表示的大数相乘

> 原文:[https://www . geesforgeks . org/multiply-大数-表示为字符串/](https://www.geeksforgeeks.org/multiply-large-numbers-represented-as-strings/)

给定两个正数作为字符串。这些数字可能非常大(可能不适合 long long int)，任务是找到这两个数字的乘积。
**例:**

```
Input : num1 = 4154  
        num2 = 51454
Output : 213739916 

Input :  num1 = 654154154151454545415415454  
         num2 = 63516561563156316545145146514654 
Output : 41549622603955309777243716069997997007620439937711509062916
```

这个想法是基于学校数学。

![multiplication](img/1fbfdb42cc43d4df8d692dc55c0d25ab.png)

我们从第二个数字的最后一个数字开始，乘以第一个数字。然后我们把第二个数字的第二个数字乘以第一个数字，以此类推。我们把所有这些乘法相加。加法时，我们把第 I 次乘法移位。
下面解决方案中使用的方法是只保留一个结果数组。我们遍历循环中的所有数字第一个和第二个数字，并在适当的位置添加结果。

## C++

```
// C++ program to multiply two numbers represented
// as strings.
#include<bits/stdc++.h>
using namespace std;

// Multiplies str1 and str2, and prints result.
string multiply(string num1, string num2)
{
    int len1 = num1.size();
    int len2 = num2.size();
    if (len1 == 0 || len2 == 0)
    return "0";

    // will keep the result number in vector
    // in reverse order
    vector<int> result(len1 + len2, 0);

    // Below two indexes are used to find positions
    // in result.
    int i_n1 = 0;
    int i_n2 = 0;

    // Go from right to left in num1
    for (int i=len1-1; i>=0; i--)
    {
        int carry = 0;
        int n1 = num1[i] - '0';

        // To shift position to left after every
        // multiplication of a digit in num2
        i_n2 = 0;

        // Go from right to left in num2            
        for (int j=len2-1; j>=0; j--)
        {
            // Take current digit of second number
            int n2 = num2[j] - '0';

            // Multiply with current digit of first number
            // and add result to previously stored result
            // at current position.
            int sum = n1*n2 + result[i_n1 + i_n2] + carry;

            // Carry for next iteration
            carry = sum/10;

            // Store result
            result[i_n1 + i_n2] = sum % 10;

            i_n2++;
        }

        // store carry in next cell
        if (carry > 0)
            result[i_n1 + i_n2] += carry;

        // To shift position to left after every
        // multiplication of a digit in num1.
        i_n1++;
    }

    // ignore '0's from the right
    int i = result.size() - 1;
    while (i>=0 && result[i] == 0)
    i--;

    // If all were '0's - means either both or
    // one of num1 or num2 were '0'
    if (i == -1)
    return "0";

    // generate the result string
    string s = "";

    while (i >= 0)
        s += std::to_string(result[i--]);

    return s;
}

// Driver code
int main()
{
    string str1 = "1235421415454545454545454544";
    string str2 = "1714546546546545454544548544544545";

    if((str1.at(0) == '-' || str2.at(0) == '-') &&
        (str1.at(0) != '-' || str2.at(0) != '-' ))
        cout<<"-";

    if(str1.at(0) == '-')
        str1 = str1.substr(1);

    if(str2.at(0) == '-')
        str2 = str2.substr(1);

    cout << multiply(str1, str2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to multiply two numbers
// represented as Strings.
class GFG
{

// Multiplies str1 and str2, and prints result.
static String multiply(String num1, String num2)
{
    int len1 = num1.length();
    int len2 = num2.length();
    if (len1 == 0 || len2 == 0)
        return "0";

    // will keep the result number in vector
    // in reverse order
    int result[] = new int[len1 + len2];

    // Below two indexes are used to
    // find positions in result.
    int i_n1 = 0;
    int i_n2 = 0;

    // Go from right to left in num1
    for (int i = len1 - 1; i >= 0; i--)
    {
        int carry = 0;
        int n1 = num1.charAt(i) - '0';

        // To shift position to left after every
        // multipliccharAtion of a digit in num2
        i_n2 = 0;

        // Go from right to left in num2            
        for (int j = len2 - 1; j >= 0; j--)
        {
            // Take current digit of second number
            int n2 = num2.charAt(j) - '0';

            // Multiply with current digit of first number
            // and add result to previously stored result
            // charAt current position.
            int sum = n1 * n2 + result[i_n1 + i_n2] + carry;

            // Carry for next itercharAtion
            carry = sum / 10;

            // Store result
            result[i_n1 + i_n2] = sum % 10;

            i_n2++;
        }

        // store carry in next cell
        if (carry > 0)
            result[i_n1 + i_n2] += carry;

        // To shift position to left after every
        // multipliccharAtion of a digit in num1.
        i_n1++;
    }

    // ignore '0's from the right
    int i = result.length - 1;
    while (i >= 0 && result[i] == 0)
    i--;

    // If all were '0's - means either both
    // or one of num1 or num2 were '0'
    if (i == -1)
    return "0";

    // genercharAte the result String
    String s = "";

    while (i >= 0)
        s += (result[i--]);

    return s;
}

// Driver code
public static void main(String[] args)
{
    String str1 = "1235421415454545454545454544";
    String str2 = "1714546546546545454544548544544545";

    if ((str1.charAt(0) == '-' || str2.charAt(0) == '-') &&
        (str1.charAt(0) != '-' || str2.charAt(0) != '-'))
        System.out.print("-");

    if (str1.charAt(0) == '-')
        str1 = str1.substring(1);

    if (str2.charAt(0) == '-')
        str2 = str2.substring(1);

    System.out.println(multiply(str1, str2));
}
}

// This code is contributed by ankush_953
```

## 蟒蛇 3

```
# Python3 program to multiply two numbers
# represented as strings.

# Multiplies str1 and str2, and prints result.
def multiply(num1, num2):
    len1 = len(num1)
    len2 = len(num2)
    if len1 == 0 or len2 == 0:
        return "0"

    # will keep the result number in vector
    # in reverse order
    result = [0] * (len1 + len2)

    # Below two indexes are used to
    # find positions in result.
    i_n1 = 0
    i_n2 = 0

    # Go from right to left in num1
    for i in range(len1 - 1, -1, -1):
        carry = 0
        n1 = ord(num1[i]) - 48

        # To shift position to left after every
        # multiplication of a digit in num2
        i_n2 = 0

        # Go from right to left in num2
        for j in range(len2 - 1, -1, -1):

            # Take current digit of second number
            n2 = ord(num2[j]) - 48

            # Multiply with current digit of first number
            # and add result to previously stored result
            # at current position.
            summ = n1 * n2 + result[i_n1 + i_n2] + carry

            # Carry for next iteration
            carry = summ // 10

            # Store result
            result[i_n1 + i_n2] = summ % 10

            i_n2 += 1

            # store carry in next cell
        if (carry > 0):
            result[i_n1 + i_n2] += carry

            # To shift position to left after every
            # multiplication of a digit in num1.
        i_n1 += 1

        # print(result)

    # ignore '0's from the right
    i = len(result) - 1
    while (i >= 0 and result[i] == 0):
        i -= 1

    # If all were '0's - means either both or
    # one of num1 or num2 were '0'
    if (i == -1):
        return "0"

    # generate the result string
    s = ""
    while (i >= 0):
        s += chr(result[i] + 48)
        i -= 1

    return s

# Driver code
str1 = "1235421415454545454545454544"
str2 = "1714546546546545454544548544544545"

if((str1[0] == '-' or str2[0] == '-') and
   (str1[0] != '-' or str2[0] != '-')):
    print("-", end = '')

if(str1[0] == '-' and str2[0] != '-'):
    str1 = str1[1:]
elif(str1[0] != '-' and str2[0] == '-'):
    str2 = str2[1:]
elif(str1[0] == '-' and str2[0] == '-'):
    str1 = str1[1:]
    str2 = str2[1:]
print(multiply(str1, str2))

# This code is contributed by ankush_953
```

## C#

```
// C# program to multiply two numbers
// represented as Strings.
using System;

class GFG
{

// Multiplies str1 and str2, and prints result.
static String multiply(String num1, String num2)
{
    int len1 = num1.Length;
    int len2 = num2.Length;
    if (len1 == 0 || len2 == 0)
        return "0";

    // will keep the result number in vector
    // in reverse order
    int []result = new int[len1 + len2];

    // Below two indexes are used to
    // find positions in result.
    int i_n1 = 0;
    int i_n2 = 0;
    int i;

    // Go from right to left in num1
    for (i = len1 - 1; i >= 0; i--)
    {
        int carry = 0;
        int n1 = num1[i] - '0';

        // To shift position to left after every
        // multipliccharAtion of a digit in num2
        i_n2 = 0;

        // Go from right to left in num2            
        for (int j = len2 - 1; j >= 0; j--)
        {
            // Take current digit of second number
            int n2 = num2[j] - '0';

            // Multiply with current digit of first number
            // and add result to previously stored result
            // charAt current position.
            int sum = n1 * n2 + result[i_n1 + i_n2] + carry;

            // Carry for next itercharAtion
            carry = sum / 10;

            // Store result
            result[i_n1 + i_n2] = sum % 10;

            i_n2++;
        }

        // store carry in next cell
        if (carry > 0)
            result[i_n1 + i_n2] += carry;

        // To shift position to left after every
        // multipliccharAtion of a digit in num1.
        i_n1++;
    }

    // ignore '0's from the right
    i = result.Length - 1;
    while (i >= 0 && result[i] == 0)
    i--;

    // If all were '0's - means either both
    // or one of num1 or num2 were '0'
    if (i == -1)
    return "0";

    // genercharAte the result String
    String s = "";

    while (i >= 0)
        s += (result[i--]);

    return s;
}

// Driver code
public static void Main(String[] args)
{
    String str1 = "1235421415454545454545454544";
    String str2 = "1714546546546545454544548544544545";

    if ((str1[0] == '-' || str2[0] == '-') &&
        (str1[0] != '-' || str2[0] != '-'))
        Console.Write("-");

    if (str1[0] == '-' && str2[0] != '-')
    {
        str1 = str1.Substring(1);
    }
    else if (str1[0] != '-' && str2[0] == '-')
    {
        str2 = str2.Substring(1);
    }
    else if (str1[0] == '-' && str2[0] == '-')
    {
        str1 = str1.Substring(1);
        str2 = str2.Substring(1);
    }
    Console.WriteLine(multiply(str1, str2));
}
}

// This code is contributed by Rajput-Ji
```

**输出:**

```
2118187521397235888154583183918321221520083884298838480662480
```

以上代码改编自 Gaurav 提供的代码。
**时间复杂度:** O(m*n)，其中 m 和 n 是需要相乘的两个数的长度。
T4【另一种方法:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to multiply two numbers represented
// as strings.
import java.util.Scanner;

public class StringMultiplication {
    // Driver code
    public static void main(String[] args)
    {
        String num1 = "1235421415454545454545454544";
        String tempnum1 = num1;
        String num2 = "1714546546546545454544548544544545";
        String tempnum2 = num2;

        // Check condition if one string is negative
        if (num1.charAt(0) == '-'
            && num2.charAt(0) != '-') {
            num1 = num1.substring(1);
        }
        else if (num1.charAt(0) != '-'
                 && num2.charAt(0) == '-') {
            num2 = num2.substring(1);
        }
        else if (num1.charAt(0) == '-'
                 && num2.charAt(0) == '-') {
            num1 = num1.substring(1);
            num2 = num2.substring(1);
        }
        String s1
            = new StringBuffer(num1).reverse().toString();
        String s2
            = new StringBuffer(num2).reverse().toString();

        int[] m = new int[s1.length() + s2.length()];

        // Go from right to left in num1
        for (int i = 0; i < s1.length(); i++) {
            // Go from right to left in num2
            for (int j = 0; j < s2.length(); j++) {
                m[i + j] = m[i + j]
                           + (s1.charAt(i) - '0')
                                 * (s2.charAt(j) - '0');
            }
        }

        String product = new String();
        // Multiply with current digit of first number
        // and add result to previously stored product
        // at current position.
        for (int i = 0; i < m.length; i++) {
            int digit = m[i] % 10;
            int carry = m[i] / 10;
            if (i + 1 < m.length) {
                m[i + 1] = m[i + 1] + carry;
            }
            product = digit + product;
        }

        // ignore '0's from the right
        while (product.length() > 1
               && product.charAt(0) == '0') {
            product = product.substring(1);
        }

        // Check condition if one string is negative
        if (tempnum1.charAt(0) == '-'
            && tempnum2.charAt(0) != '-') {
            product = new StringBuffer(product)
                          .insert(0, '-')
                          .toString();
        }
        else if (tempnum1.charAt(0) != '-'
                 && tempnum2.charAt(0) == '-') {
            product = new StringBuffer(product)
                          .insert(0, '-')
                          .toString();
        }
        else if (tempnum1.charAt(0) == '-'
                 && tempnum2.charAt(0) == '-') {
            product = product;
        }
        System.out.println("Product of the two numbers is :"
                           + "\n" + product);
    }
}
```

**输出:**

```
2118187521397235888154583183918321221520083884298838480662480
```

**相关文章:**
[Karatsuba 快速乘法算法](https://www.geeksforgeeks.org/divide-and-conquer-set-2-karatsuba-algorithm-for-fast-multiplication/)
本文由 **Aditya Kumar** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。