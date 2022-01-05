# 重复数字

> 原文:[https://www.geeksforgeeks.org/repdigit-numbers/](https://www.geeksforgeeks.org/repdigit-numbers/)

**代表数字**是一个数字 **N** ，其在基数 **B** 中表示的所有数字都相等。
一些回复数字是:

> 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 11, 22, 33, 44, 55….

### 检查 N 是否是一个重复数字

给定一个数字 **N** ，任务是检查 **N** 是否是基 **B** 中的**重复数字**。如果 **N** 是基数 **B** 中的重复数字，则打印**“是”**否则打印**“否”**。
**举例:**

> **输入:** N = 2000，B = 7
> **输出:**是
> **说明:**
> 7 中的 2000 为 5555，所有数字相等。
> **输入:** N = 112，B = 10
> **输出:**否

**进场:**

*   一个接一个地找出基数 b 中 N 的所有数字。
*   将每个数字与其前一个数字进行比较。
*   如果任何数字不等于前一个数字，则返回 false。
*   否则返回真。

以下是上述方法的实现:

## C++

```
// C++ implementation to check
// if a number is Repdigit

#include <iostream>
using namespace std;

// Function to check if a number
// is a Repdigit number
bool isRepdigit(int num, int b)
{
    // To store previous digit (Assigning
    // initial value which is less than any
    // digit)
    int prev = -1;

    // Traverse all digits from right to
    // left and check if any digit is
    // smaller than previous.
    while (num) {
        int digit = num % b;
        num /= b;
        if (prev != -1 && digit != prev)
            return false;
        prev = digit;
    }

    return true;
}

// Driver code
int main()
{
    int num = 2000, base = 7;
    isRepdigit(num, base) ? cout << "Yes"
                          : cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check
// if a number is Repdigit
class GFG{

// Function to check if a number
// is a Repdigit number
static boolean isRepdigit(int num, int b)
{
    // To store previous digit (Assigning
    // initial value which is less than any
    // digit)
    int prev = -1;

    // Traverse all digits from right to
    // left and check if any digit is
    // smaller than previous.
    while (num != 0)
    {
        int digit = num % b;
        num /= b;
        if (prev != -1 && digit != prev)
            return false;
        prev = digit;
    }
    return true;
}

// Driver code
public static void main(String args[])
{
    int num = 2000, base1 = 7;
    if(isRepdigit(num, base1))
    {
        System.out.print("Yes");
    }
    else
    {
        System.out.print("No");
    }
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 implementation to check
# if a number is Repdigit

# Function to check if a number
# is a Repdigit number
def isRepdigit(num, b) :

    # To store previous digit (Assigning
    # initial value which is less than any
    # digit)
    prev = -1

    # Traverse all digits from right to
    # left and check if any digit is
    # smaller than previous.
    while (num) :
        digit = num % b
        num //= b
        if (prev != -1 and digit != prev) :
            return False
        prev = digit
    return True

# Driver code
num = 2000
base = 7
if(isRepdigit(num, base)):
    print("Yes")
else:
    print("No")

# This code is contributed by Vishal Maurya.
```

## C#

```
// C# implementation to check
// if a number is Repdigit
using System;
class GFG{

// Function to check if a number
// is a Repdigit number
static bool isRepdigit(int num, int b)
{
    // To store previous digit (Assigning
    // initial value which is less than any
    // digit)
    int prev = -1;

    // Traverse all digits from right to
    // left and check if any digit is
    // smaller than previous.
    while (num != 0)
    {
        int digit = num % b;
        num /= b;
        if (prev != -1 && digit != prev)
            return false;
        prev = digit;
    }
    return true;
}

// Driver code
public static void Main()
{
    int num = 2000, base1 = 7;
    if(isRepdigit(num, base1))
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("No");
    }
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript implementation to check
// if a number is Repdigit

    // Function to check if a number
    // is a Repdigit number
    function isRepdigit( num ,b) {
        // To store previous digit (Assigning
        // initial value which is less than any
        // digit)
        let prev = -1;

        // Traverse all digits from right to
        // left and check if any digit is
        // smaller than previous.
        while (num != 0) {
            let digit = num % b;
            num = parseInt(num/b);
            if (prev != -1 && digit != prev)
                return false;
            prev = digit;
        }
        return true;
    }

    // Driver code

        let num = 2000, base1 = 7;
        if (isRepdigit(num, base1)) {
            document.write("Yes");
        } else {
            document.write("No");
        }

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:***O(n)*
T5】参考:[http://www.numbersaplenty.com/set/repdigit/](http://www.numbersaplenty.com/set/repdigit/)