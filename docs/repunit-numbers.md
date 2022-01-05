# 重复单元号

> 原文:[https://www.geeksforgeeks.org/repunit-numbers/](https://www.geeksforgeeks.org/repunit-numbers/)

如果一个数在一个基数> = 2 中可以表示为一串三个或三个以上的 1，则该数在基数 **B** 中是一个重复单位。

### 检查 N 是否为重复单元号

给定一个整数 N，任务是检查 **N** 是否为基数 **B** 中的重复单元号。
**例:**

> **输入:** N = 31，B = 5
> **输出:**是
> 31 可以写成 5
> **中的 111 基数输入:** N = 5，B = 2
> **输出:**否
> 5 是 2
> 中的 101 基数

**进场:**我们会统计给定号码 **N** 的基数 **B** 中的人数，也会统计给定号码 **N** 的基数 **B** 中的位数。如果相同，则打印“是”，否则打印“否”。
**例如:**

> N = 31，B = 5
> 31 可以写成 5 中的 111 基数，所以给定数**的基数**B**N**= 3 和给定数**的基数 **B** 中的位数 N** = 3
> 由于两者相等，因此 31 是基数 **5** 中的重复单位数。

以下是上述方法的实现:

## C++

```
// C++ implementation  to check
// if a number is Repunit Number

#include <iostream>
#include <math.h>
using namespace std;

// Function to check if a number
// contains all the digits 0, 1, .., (b-1)
// an equal number of times
bool isRepunitNum(int n, int b)
{
    // to store number of digits of n
    // in base B
    int length = 0;
    // to count frequency of digit 1
    int countOne = 0;
    while (n != 0) {
        int r = n % b;
        length++;
        if (r == 1)
            countOne++;
        n = n / b;
    }

    // condition to check three or more 1's
    // and number of ones is equal to number
    // of digits of n in base B
    return countOne >= 3 && countOne == length;
}

// Driver Code
int main()
{
    // taking inputs
    int n = 31;
    int base = 2;

    // function to check
    if (isRepunitNum(n, base))
        cout << "Yes";
    else
        cout << "NO";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check
// if a number is Repunit Number
class GFG{

// Function to check if a number
// contains all the digits 0, 1, .., (b-1)
// an equal number of times
static boolean isRepunitNum(int n, int b)
{
    // to store number of digits of n
    // in base B
    int length = 0;

    // to count frequency of digit 1
    int countOne = 0;
    while (n != 0)
    {
        int r = n % b;
        length++;
        if (r == 1)
            countOne++;
        n = n / b;
    }

    // condition to check three or more 1's
    // and number of ones is equal to number
    // of digits of n in base B
    return countOne >= 3 &&
           countOne == length;
}

// Driver Code
public static void main(String[] args)
{
    // taking inputs
    int n = 31;
    int base = 2;

    // function to check
    if (isRepunitNum(n, base))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by rock_cool
```

## 蟒蛇 3

```
# Python3 implementation to check
# if a number is Repunit Number

# Function to check if a number
# contains all the digits 0, 1, .., (b-1)
# an equal number of times
def isRepunitNum(n, b):

    # to store number of digits of n
    # in base B
    length = 0;

    # to count frequency of digit 1
    countOne = 0;
    while (n != 0):
        r = n % b;
        length += 1;
        if (r == 1):
            countOne += 1;
        n = n // b;

    # condition to check three or more 1's
    # and number of ones is equal to number
    # of digits of n in base B
    return countOne >= 3 and countOne == length;

# Driver Code
if __name__ == '__main__':

    # taking inputs
    n = 31;
    base = 2;

    # function to check
    if (isRepunitNum(n, base)):
        print("Yes");
    else:
        print("No");

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation to check
// if a number is Repunit Number
using System;
class GFG{

// Function to check if a number
// contains all the digits 0, 1, .., (b-1)
// an equal number of times
static bool isRepunitNum(int n, int b)
{
    // to store number of digits of n
    // in base B
    int length = 0;

    // to count frequency of digit 1
    int countOne = 0;
    while (n != 0)
    {
        int r = n % b;
        length++;
        if (r == 1)
            countOne++;
        n = n / b;
    }

    // condition to check three or more 1's
    // and number of ones is equal to number
    // of digits of n in base B
    return countOne >= 3 &&
           countOne == length;
}

// Driver Code
public static void Main()
{
    // taking inputs
    int n = 31;
    int base1 = 2;

    // function to check
    if (isRepunitNum(n, base1))
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

// Javascript implementation to check
// if a number is Repunit Number

    // Function to check if a number
    // contains all the digits 0, 1, .., (b-1)
    // an equal number of times
    function isRepunitNum( n ,b) {
        // to store number of digits of n
        // in base B
        let length = 0;

        // to count frequency of digit 1
        let countOne = 0;
        while (n != 0) {
            let r = n % b;
            length++;
            if (r == 1)
                countOne++;
            n = parseInt(n / b);
        }

        // condition to check three or more 1's
        // and number of ones is equal to number
        // of digits of n in base B
        return countOne >= 3 && countOne == length;
    }

    // Driver Code

        // taking inputs
        let n = 31;
        let base = 2;

        // function to check
        if (isRepunitNum(n, base))
            document.write("Yes");
        else
            document.write("No");

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(log <sub>b</sub> n)*

***辅助空间:** O(1)*

**参考**:[http://www.numbersaplenty.com/set/repunit/](http://www.numbersaplenty.com/set/repunit/)T4】