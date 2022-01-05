# 添加两个位串

> 原文:[https://www.geeksforgeeks.org/add-two-bit-strings/](https://www.geeksforgeeks.org/add-two-bit-strings/)

给定两个字符串形式的位序列，编写一个函数来返回这两个序列的相加。位串也可以有不同的长度。例如，如果字符串 1 是“1100011”，第二个字符串 2 是“10”，那么函数应该返回“1100101”。

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/add-binary-strings3805/1)

由于两个字符串的大小可能不同，我们首先通过添加前导 0 使较小字符串的大小等于较大字符串的大小。在使大小相同后，我们一个接一个地从最右边的位向最左边的位添加位。在每次迭代中，我们需要对 3 位进行求和:2 个给定字符串的 2 位进行进位。如果这 3 个位全部置位或其中一个置位，总和位将为 1。所以我们可以对所有的比特进行异或运算，找到和比特。如何找到进位–如果两个位中的任何一个被置位，进位将为 1。所以我们可以通过取所有对的或来找到进位。下面是分步算法。
**1。**在较小的字符串开头加上 0，使它们大小相等。
T4【2】。执行位添加
…..用于添加 3 位 a、b、c 的布尔表达式
…..求和=一异或二异或三
…..进位= (a 和 b)或(b 和 c)或(c 和 a )
下面是上述算法的实现。

## C++

```
#include <iostream>
using namespace std;

//adds the two-bit strings and return the result
string addBitStrings( string first, string second );

// Helper method: given two unequal sized bit strings, converts them to
// same length by adding leading 0s in the smaller string. Returns the
// the new length
int makeEqualLength(string &str1, string &str2)
{
    int len1 = str1.size();
    int len2 = str2.size();
    if (len1 < len2)
    {
        for (int i = 0 ; i < len2 - len1 ; i++)
            str1 = '0' + str1;
        return len2;
    }
    else if (len1 > len2)
    {
        for (int i = 0 ; i < len1 - len2 ; i++)
            str2 = '0' + str2;
    }
    return len1; // If len1 >= len2
}

// The main function that adds two-bit sequences and returns the addition
string addBitStrings( string first, string second )
{
    string result;  // To store the sum bits

    // make the lengths same before adding
    int length = makeEqualLength(first, second);

    int carry = 0;  // Initialize carry

    // Add all bits one by one
    for (int i = length-1 ; i >= 0 ; i--)
    {
        int firstBit = first.at(i) - '0';
        int secondBit = second.at(i) - '0';

        // boolean expression for sum of 3 bits
        int sum = (firstBit ^ secondBit ^ carry)+'0';

        result = (char)sum + result;

        // boolean expression for 3-bit addition
        carry = (firstBit & secondBit) | (secondBit & carry) | (firstBit & carry);
    }

    // if overflow, then add a leading 1
    if (carry)
        result = '1' + result;

    return result;
}

// Driver program to test above functions
int main()
{
    string str1 = "1100011";
    string str2 = "10";

    cout << "Sum is " << addBitStrings(str1, str2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above algorithm
class GFG
{

    // Helper method: given two unequal sized bit strings,
    // converts them to same length by adding leading 0s
    // in the smaller string. Returns the the new length
    // Using StringBuilder as Java only uses call by value
    static int makeEqualLength(StringBuilder str1,
                               StringBuilder str2)
    {
        int len1 = str1.length();
        int len2 = str2.length();
        if (len1 < len2)
        {
            for (int i = 0; i < len2 - len1; i++)
                str1.insert(0, '0');
            return len2;
        }
        else if (len1 > len2)
        {
            for (int i = 0; i < len1 - len2; i++)
                str2.insert(0, '0');
        }

        return len1; // If len1 >= len2
    }

    // The main function that adds two-bit sequences
    // and returns the addition
    static String addBitStrings(StringBuilder str1,
                                StringBuilder str2)
    {
        String result = ""; // To store the sum bits

        // make the lengths same before adding
        int length = makeEqualLength(str1, str2);

        // Convert StringBuilder to Strings
        String first = str1.toString();
        String second = str2.toString();

        int carry = 0; // Initialize carry

        // Add all bits one by one
        for (int i = length - 1; i >= 0; i--)
        {
            int firstBit = first.charAt(i) - '0';
            int secondBit = second.charAt(i) - '0';

            // boolean expression for sum of 3 bits
            int sum = (firstBit ^ secondBit ^ carry) + '0';

            result = String.valueOf((char) sum) + result;

            // boolean expression for 3-bit addition
            carry = (firstBit & secondBit) |
                    (secondBit & carry) |
                    (firstBit & carry);
        }

        // if overflow, then add a leading 1
        if (carry == 1)
            result = "1" + result;
        return result;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String str1 = "1100011";
        String str2 = "10";
        System.out.println("Sum is " +
        addBitStrings(new StringBuilder(str1),
                      new StringBuilder(str2)));
    }
}

// This code is contributed by Vivek Kumar Singh
```

## 蟒蛇 3

```
# Python3 program for above approach

# adds the two-bit strings and return the result

# Helper method: given two unequal sized bit strings,
# converts them to same length by adding leading 0s
# in the smaller string. Returns the the new length
def makeEqualLength(str1, str2):

    len1 = len(str1)     # Length of string 1
    len2 = len(str2)     # length of string 2
    if len1 < len2:
        str1 = (len2 - len1) * '0' + str1
        len1 = len2
    elif len2 < len1:
        str2 = (len1 - len2) * '0' + str2
        len2 = len1
    return len1, str1, str2

def addBitStrings( first, second ):
    result = '' # To store the sum bits

    # make the lengths same before adding
    length, first, second = makeEqualLength(first, second)

    carry = 0 # initialize carry as 0

    # Add all bits one by one
    for i in range(length - 1, -1, -1):
        firstBit = int(first[i])
        secondBit = int(second[i])

        # boolean expression for sum of 3 bits
        sum = (firstBit ^ secondBit ^ carry) + 48
        result = chr(sum) + result

        # boolean expression for 3 bits addition
        carry = (firstBit & secondBit) | \
                (secondBit & carry) | \
                (firstBit & carry)

        # if overflow, then add a leading 1
    if carry == 1:
        result = '1' + result
    return result

# Driver Code
if __name__ == '__main__':
    str1 = '1100011'
    str2 = '10'
    print('Sum is', addBitStrings(str1, str2))

# This code is contributed by
# chaudhary_19 (Mayank Chaudhary)
```

## C#

```
// C# implementation of above algorithm
using System;
using System.Text;

class GFG
{

    // Helper method: given two unequal sized
    // bit strings, converts them to same length
    // by adding leading 0s in the smaller string.
    // Returns the the new length Using StringBuilder
    // as Java only uses call by value
    static int makeEqualLength(StringBuilder str1,
                               StringBuilder str2)
    {
        int len1 = str1.Length;
        int len2 = str2.Length;
        if (len1 < len2)
        {
            for (int i = 0; i < len2 - len1; i++)
            {
                str1.Insert(0, '0');
            }
            return len2;
        }
        else if (len1 > len2)
        {
            for (int i = 0; i < len1 - len2; i++)
            {
                str2.Insert(0, '0');
            }
        }

        return len1; // If len1 >= len2
    }

    // The main function that adds two-bit sequences
    // and returns the addition
    static string addBitStrings(StringBuilder str1,
                                StringBuilder str2)
    {
        string result = ""; // To store the sum bits

        // make the lengths same before adding
        int length = makeEqualLength(str1, str2);

        // Convert StringBuilder to Strings
        string first = str1.ToString();
        string second = str2.ToString();

        int carry = 0; // Initialize carry

        // Add all bits one by one
        for (int i = length - 1; i >= 0; i--)
        {
            int firstBit = first[i] - '0';
            int secondBit = second[i] - '0';

            // boolean expression for sum of 3 bits
            int sum = (firstBit ^ secondBit ^ carry) + '0';

            result = ((char) sum).ToString() + result;

            // boolean expression for 3-bit addition
            carry = (firstBit & secondBit) |
                       (secondBit & carry) |
                        (firstBit & carry);
        }

        // if overflow, then add a leading 1
        if (carry == 1)
        {
            result = "1" + result;
        }
        return result;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        string str1 = "1100011";
        string str2 = "10";
        Console.WriteLine("Sum is " +
                addBitStrings(new StringBuilder(str1),
                              new StringBuilder(str2)));
    }
}

// This code is contributed by kumar65
```

**输出:**

```
 Sum is 1100101
```

***时间复杂度:** O(|str1|)*

***辅助空间:** O(1)*
本文由 **Ravi Chandra Enaganti** 整理。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。