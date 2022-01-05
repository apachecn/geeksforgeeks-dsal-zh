# 前 K 个偶数长度回文数之和

> 原文:[https://www . geesforgeks . org/sum-first-k-偶数长度-回文-numbers/](https://www.geeksforgeeks.org/sum-first-k-even-length-palindrome-numbers/)

给定一个整数 k，求前 k 个偶数长度[回文](https://www.geeksforgeeks.org/check-if-a-number-is-palindrome/)数的和。
这里的偶数长度是指一个数字的位数是偶数。
**示例:**

```
Input : k = 3
Output : 66
Explanation: 11 + 22 + 33  = 66 (Sum 
of first three even-length palindrome 
numbers)

Input : 10
Output : 1496
Explanation: 11+22+33+44+55+66+77+88+
99+1001 = 1496
```

一个**天真的方法**将是检查每一个偶数长度的数字，如果它是一个回文数字，那么我们总结它。我们对前 K 个偶数长度的回文数字重复同样的过程，并将它们相加得到总和。
在这种情况下，复杂度会变高，因为偶数长度的数字从 10-99 开始，然后是 1000-9999，以此类推……
10-99，1000-9999，100000-99999..里面分别有 9，90，900 个回文数字，所以要检查 k 个数字，我们必须检查很多效率不够的数字。
一种有效的方法**是观察偶数长度质数的模式。** 

> 11、22、33、44、55、66、77、88、99、1001、1111、1221、1331、1441、1551、1661……

第一个数字是 11，第二个是 22，第三个是 33，第十六个是 **16-rev(16)，即 1661** 。
**所以第 n 个数字会是 int(字符串(n)+rev(字符串(n))。**
整数到字符串、字符串到整数的转换见此处。
以下是上述方法的实施:

## C++

```
#include <bits/stdc++.h>
#include <boost/lexical_cast.hpp>
using namespace std;

// function to return the sum of
// first K even length palindrome numbers
int sum(int k)
{
    // loop to get sum of first K even
    // palindrome numbers
    int sum = 0;
    for (int i = 1; i <= k; i++) {

        // convert integer to string
        string num = to_string(i);

        // Find reverse of num.
        string revNum = num;
        reverse(revNum.begin(), revNum.end());

        // string(n)+rev(string(n)
        string strnum = (num + revNum);

        // convert string to integer
        int number = boost::lexical_cast<int>(strnum);

        sum += number; // summation
    }
    return sum;
}
// driver program to check the above function
int main()
{
    int k = 3;
    cout << sum(k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find sum of
// first K even-length Palindrome numbers
import java.util.*;
import java.lang.*;

public class GfG{

public static String reverseString(String str)
{
    StringBuilder sb = new StringBuilder(str);   
    sb.reverse();  
    return sb.toString();
}

// function to return the sum of
// first K even length palindrome numbers
static int sum(int k)
{
    // loop to get sum of first K even
    // palindrome numbers
    int sum = 0;
    for (int i = 1; i <= k; i++) {

    // convert integer to string
    String num = Integer.toString(i);

    // Find reverse of num.
    String revNum = num;
    revNum = reverseString(num);

    // string(n)+rev(string(n)
    String strnum = (num + revNum);

    // convert string to integer
    int number = Integer.parseInt(strnum);

    sum += number; // summation
    }

    return sum;
}

// driver function
public static void main(String argc[])
{
    int n = 3;
    System.out.println(sum(n));
}
}

// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# function to return the sum of
# first K even length palindrome numbers
def summ(k):

    # loop to get sum of first K even
    # palindrome numbers
    sum = 0
    for i in range(1, k + 1):

        # convert integer to string
        num = str(i)

        # Find reverse of num.
        revNum = num
        revNum = ''.join(reversed(revNum))

        # string(n)+rev(string(n)
        strnum = num + revNum

        # convert string to integer
        number = int(strnum)

        sum += number # summation

    return sum

# Driver Code
if __name__ == "__main__":
    k = 3
    print(summ(k))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation to find sum of
// first K even-length Palindrome numbers
using System;

class GfG
{

    // function to return the sum of
    // first K even length palindrome numbers
    static int sum(int k)
    {

        // loop to get sum of first K even
        // palindrome numbers
        int sum = 0;
        for (int i = 1; i <= k; i++)
        {

            // convert integer to string
            String num = Convert.ToString(i);

            // Find reverse of num.
            String revNum = num;
            revNum = reverse(num);

            // string(n)+rev(string(n)
            String strnum = (num + revNum);

            // convert string to integer
            int number = Convert.ToInt32(strnum);

            sum += number; // summation
        }

        return sum;
    }

    static String reverse(String input)
    {
        char[] temparray = input.ToCharArray();
        int left, right = 0;
        right = temparray.Length - 1;

        for (left = 0; left < right; left++, right--)
        {

            // Swap values of left and right
            char temp = temparray[left];
            temparray[left] = temparray[right];
            temparray[right] = temp;
        }
        return String.Join("",temparray);
    }

    // Driver code
    public static void Main(String []argc)
    {
        int n = 3;
        Console.WriteLine(sum(n));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// function to return the sum of
// first K even length palindrome numbers
function sum(k)
{
    // loop to get sum of first K even
    // palindrome numbers
    var sum = 0;
    for (var i = 1; i <= k; i++) {

        // convert integer to string
        var num = (i.toString());

        // Find reverse of num.
        var revNum = num;
        revNum = revNum.split('').reverse().join('');

        // string(n)+rev(string(n)
        var strnum = (num + revNum);

        // convert string to integer
        var number = parseInt(strnum);

        sum += number; // summation
    }
    return sum;
}

// driver program to check the above function
var k = 3;
document.write(sum(k));

</script>
```

**输出:**

```
66
```