# 卡塔洛马号码

> 原文:[https://www.geeksforgeeks.org/katadrome-number/](https://www.geeksforgeeks.org/katadrome-number/)

卡塔德罗姆数是一个数字按降序排列的数。
少数武士道编号为:

> 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 20, 21….

### 检查 N 是否是一个武士道

给定一个数字 **N** ，任务是检查是否是武士道。
**例:**

> **输入:**4321
> T3】输出:是
> T6】输入:1243
> T9】输出:否

**方法:**思路是遍历数字的位数，检查当前位数是否小于最后一位。如果所有的数字都满足条件，那么这个数字就是一个武士道数字。
以下是上述办法的实施情况:

## C++

```
// C++ implementation to check if
// a number is Katadrome or not.

#include <iostream>
using namespace std;

// Function to check if a number
// is a Katadrome number or not
bool isKatadrome(int num)
{
    // To store previous digit (Assigning
    // initial value which is less than any
    // digit)
    int prev = -1;

    // Traverse all digits from right to
    // left and check if any digit is
    // smaller than previous.
    while (num) {
        int digit = num % 10;
        num /= 10;
        if (digit < prev)
            return false;
        prev = digit;
    }

    return true;
}

// Driver code
int main()
{
    int num = 4321;
    isKatadrome(num) ? cout << "Yes"
                     : cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check if
// a number is Katadrome or not.
class GFG{

// Function to check if a number
// is a Katadrome number or not
static boolean isKatadrome(int num)
{

    // To store previous digit
    // (Assigning initial value
    // which is less than any digit)
    int prev = -1;

    // Traverse all digits from right
    // to left and check if any digit
    // is smaller than previous.
    while (num > 0)
    {
        int digit = num % 10;
        num /= 10;
        if (digit < prev)
            return false;
        prev = digit;
    }
    return true;
}

// Driver Code
public static void main(String[] args)
{
    int N = 4321;

    // Function Call
    if (isKatadrome(N))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by Pratima Pandey
```

## 蟒蛇 3

```
# Python3 program to print count of values such
# that n+i = n^i

def isKatadrome(num):

    # To store previous digit (Assigning
    # initial value which is less than any
    # digit)
    prev = -1

    # Traverse all digits from right to
    # left and check if any digit is
    # smaller than previous.
    while num:
        digit = num % 10
        num //= 10
        if digit < prev:
            return False
        prev = digit

    return True

# Driver code
if __name__=='__main__':

    num = 4321

    if isKatadrome(num):
        print('Yes')
    else:
        print('No')

# This code is contributed by rutvik
```

## C#

```
// C# implementation to check if
// a number is Katadrome or not.
using System;
class GFG{

// Function to check if a number
// is a Katadrome number or not
static bool isKatadrome(int num)
{

    // To store previous digit
    // (Assigning initial value
    // which is less than any digit)
    int prev = -1;

    // Traverse all digits from right
    // to left and check if any digit
    // is smaller than previous.
    while (num > 0)
    {
        int digit = num % 10;
        num /= 10;
        if (digit < prev)
            return false;
        prev = digit;
    }
    return true;
}

// Driver Code
public static void Main()
{
    int N = 4321;

    // Function Call
    if (isKatadrome(N))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript implementation to check if
// a number is Katadrome or not.

    // Function to check if a number
    // is a Katadrome number or not
    function isKatadrome( num) {

        // To store previous digit
        // (Assigning initial value
        // which is less than any digit)
        let prev = -1;

        // Traverse all digits from right
        // to left and check if any digit
        // is smaller than previous.
        while (num > 0) {
            let digit = num % 10;
            num = parseInt(num/10);
            if (digit < prev)
                return false;
            prev = digit;
        }
        return true;
    }

    // Driver Code

        let N = 4321;

        // Function Call
        if (isKatadrome(N))
            document.write("Yes");
        else
            document.write("No");

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(d)* 其中 d 为给定数字的位数。
**参考:**[http://www.numbersaplenty.com/set/katadrome/](http://www.numbersaplenty.com/set/katadrome/)T9】