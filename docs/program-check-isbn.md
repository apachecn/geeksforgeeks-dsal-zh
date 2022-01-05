# 检查书号的程序

> 原文:[https://www.geeksforgeeks.org/program-check-isbn/](https://www.geeksforgeeks.org/program-check-isbn/)

国际标准书号是用来识别一本书的 10 位数。
国际标准书号的前九位用来表示图书的书名、出版者和组别，最后一位用来检查国际标准书号是否正确。

它的前 9 位，可以取 0 到 9 之间的任何值，但最后一位，有时可能取等于 10 的值；这是通过将它写成“X”来完成的。

要验证一个 ISBN，计算第一个数字的 10 倍，加上第二个数字的 9 倍，加上第三个数字的 8 倍，以此类推，直到我们加上最后一个数字的 1 倍。如果最后的数字除以 11 后没有余数，则该代码是有效的 ISBN。

**例:**

```
Input : 007462542X
Output : Valid
007462542X = 10*0 + 9*0 + 8*7 + 7*4 + 6*6 + 
        5*2 + 4*5 + 3*4 + 2*2 + 1*10 = 176
Since 55 leaves no remainder when divided 
by 11, hence it is a valid ISBN.

Input : 0112112425
Output : Invalid
0112112425 = 10*0 + 9*1 + 8*1 + 7*2 + 6*1 +
           5*1 + 4*1 + 3*4 + 2*2 + 1*5 = 71
Since 71 is not divisible by 11, given number
is not a valid ISBN.
```

现在，我们设计一个程序来接受用户的十位数代码，然后我们将检查一个数字是否是国际标准书号。显示适当的消息。

## C++

```
// CPP program to check if a
// given ISBN is valid or not
#include <bits/stdc++.h>
using namespace std;

bool isValidISBN(string& isbn)
{
    // length must be 10
    int n = isbn.length();
    if (n != 10)
        return false;

    // Computing weighted sum
    // of first 9 digits
    int sum = 0;
    for (int i = 0; i < 9; i++)
    {
        int digit = isbn[i] - '0';
        if (0 > digit || 9 < digit)
            return false;
        sum += (digit * (10 - i));
    }

    // Checking last digit.
    char last = isbn[9];
    if (last != 'X' && (last < '0' ||
                        last > '9'))
        return false;

    // If last digit is 'X', add 10
    // to sum, else add its value.
    sum += ((last == 'X') ? 10 :
                  (last - '0'));

    // Return true if weighted sum
    // of digits is divisible by 11.
    return (sum % 11 == 0);
}

// Driver code
int main()
{
    string isbn = "007462542X";
    if (isValidISBN(isbn))
        cout << "Valid";
    else
        cout << "Invalid";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if
// a given ISBN isvalid or not

class GFG
{
    static boolean isValidISBN(String isbn)
    {
        // length must be 10
        int n = isbn.length();
        if (n != 10)
            return false;

        // Computing weighted sum
        // of first 9 digits
        int sum = 0;
        for (int i = 0; i < 9; i++)
        {
            int digit = isbn.charAt(i) - '0';
            if (0 > digit || 9 < digit)
                return false;
            sum += (digit * (10 - i));
        }

        // Checking last digit.
        char last = isbn.charAt(9);
        if (last != 'X' && (last < '0' ||
                            last > '9'))
            return false;

        // If last digit is 'X', add 10
        // to sum, else add its value
        sum += ((last == 'X') ? 10 : (last - '0'));

        // Return true if weighted sum
        // of digits is divisible by 11.
        return (sum % 11 == 0);
    }

    // Driver code
    public static void main(String[] args)
    {
        String isbn = "007462542X";
        if (isValidISBN(isbn))
            System.out.print("Valid");
        else
            System.out.print("Invalid");
    }
}

// This code is contributed
// by Anant Agarwal.
```

## 蟒蛇 3

```
# Python code to check if a
# given ISBN is valid or not.

def isValidISBN(isbn):

    # check for length
    if len(isbn) != 10:
        return False

    # Computing weighted sum
    # of first 9 digits
    _sum = 0
    for i in range(9):
        if 0 <= int(isbn[i]) <= 9:
            _sum += int(isbn[i]) * (10 - i)
        else:
            return False

    # Checking last digit
    if(isbn[9] != 'X' and
       0 <= int(isbn[9]) <= 9):
        return False

    # If last digit is 'X', add
    # 10 to sum, else add its value.
    _sum += 10 if isbn[9] == 'X' else int(isbn[9])

    # Return true if weighted sum of
    # digits is divisible by 11
    return (_sum % 11 == 0)

# Driver Code
isbn = "007462542X"
if isValidISBN(isbn):
    print('Valid')
else:
    print("Invalid")

# This code is contributed
# by "Abhishek Sharma 44"
```

## C#

```
// C# program to check if a given
// ISBN isvalid or not.
using System;

class GFG {

    static bool isValidISBN(string isbn)
    {

        // length must be 10
        int n = isbn.Length;
        if (n != 10)
            return false;

        // Computing weighted sum of
        // first 9 digits
        int sum = 0;
        for (int i = 0; i < 9; i++)
        {
            int digit = isbn[i] - '0';

            if (0 > digit || 9 < digit)
                return false;

            sum += (digit * (10 - i));
        }

        // Checking last digit.
        char last = isbn[9];
        if (last != 'X' && (last < '0'
                         || last > '9'))
            return false;

        // If last digit is 'X', add 10
        // to sum, else add its value.
        sum += ((last == 'X') ? 10 :
                          (last - '0'));

        // Return true if weighted sum
        // of digits is divisible by 11.
        return (sum % 11 == 0);
    }

    // Driver code
    public static void Main()
    {

        string isbn = "007462542X";

        if (isValidISBN(isbn))
            Console.WriteLine("Valid");
        else
            Console.WriteLine("Invalid");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a
// given ISBN is valid or not.

function isValidISBN($isbn)
{
    // length must be 10
    $n = strlen($isbn);
    if ($n != 10)
        return -1;

    // Computing weighted sum
    // of first 9 digits
    $sum = 0;
    for ($i = 0; $i < 9; $i++)
    {
        $digit = $isbn[$i] - '0';
        if (0 > $digit || 9 < $digit)
            return -1;
        $sum += ($digit * (10 - $i));
    }

    // Checking last digit.
    $last = $isbn[9];
    if ($last != 'X' && ($last < '0' ||
                         $last > '9'))
        return -1;

    // If last digit is 'X', add 10
    // to sum, else add its value.
    $sum += (($last == 'X')
      ? 10 : ($last - '0'));

    // Return true if weighted sum of
    // digits is divisible by 11.
    return ($sum % 11 == 0);
}

// Driver code
$isbn = "007462542X";
if (isValidISBN($isbn))
    echo "Valid";
else
    echo "Invalid";

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
    // Javascript program to check if a given
    // ISBN isvalid or not.

    function isValidISBN(isbn)
    {

        // length must be 10
        let n = isbn.length;
        if (n != 10)
            return false;

        // Computing weighted sum of
        // first 9 digits
        let sum = 0;
        for (let i = 0; i < 9; i++)
        {
            let digit = isbn[i] - '0';

            if (0 > digit || 9 < digit)
                return false;

            sum += (digit * (10 - i));
        }

        // Checking last digit.
        let last = isbn[9];
        if (last != 'X' && (last < '0' || last > '9'))
            return false;

        // If last digit is 'X', add 10
        // to sum, else add its value.
        sum += ((last == 'X') ? 10 : (last - '0'));

        // Return true if weighted sum
        // of digits is divisible by 11.
        return (sum % 11 == 0);
    }

    let isbn = "007462542X";

    if (isValidISBN(isbn))
      document.write("Valid");
    else
      document.write("Invalid");

</script>
```

**输出:**

```
Valid
```

以上代码检查 [ISBN 10](https://en.wikipedia.org/wiki/International_Standard_Book_Number#ISBN-10_check_digit_calculation) 。国际标准书号的最新版本是[国际标准书号 13](https://en.wikipedia.org/wiki/International_Standard_Book_Number#ISBN-13_check_digit_calculation)(2005 年)。