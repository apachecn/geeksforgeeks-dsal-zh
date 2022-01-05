# 检查给定的数字 N 是否为裸数字

> 原文:[https://www . geesforgeks . org/check-给定号码-n-是-裸号码-还是-否/](https://www.geeksforgeeks.org/check-whether-a-given-number-n-is-a-nude-number-or-not/)

给定一个整数 **N** ，任务是检查 **N** 是否为裸号。

> 裸数是可被其所有数字整除的[数(应该是非零的)。](https://www.geeksforgeeks.org/check-digits-number-divide/)

**例:**

> **输入:** N = 672
> **输出:**是
> **说明:**
> 既然，672 可以被它的三个数字 6、7、2 整除。因此，输出是“是”。
> **输入:** N = 450
> **输出:**否
> **说明:**
> 既然，450 不能被 0 整除(也给出例外)。因此输出号为

**方法:**从数字中逐个提取数字，检查这两个条件:

1.  为了避免异常，数字必须是非零的
2.  数字必须除以数字 N

当 N 的所有数字都满足这两个条件时，这个数就叫做裸数。
以下是上述方法的实现:

## C++

```
// C++ program to check if the
// number if Nude number or not

#include <iostream>
using namespace std;

// Check if all digits
// of num divide num
bool checkDivisbility(int num)
{
    // array to store all digits
    // of the given number
    int digit;
    int N = num;
    while (num != 0) {
        digit = num % 10;
        num = num / 10;

        // If any of the condition
        // is true for any digit
        // Then N is not a nude number
        if (digit == 0 || N % digit != 0)
            return false;
    }

    return true;
}

// Driver code
int main()
{
    int N = 128;

    bool result = checkDivisbility(N);
    if (result)
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if the
// number if Nude number or not
import java.util.*;
class GFG{

// Check if all digits
// of num divide num
static boolean checkDivisbility(int num)
{
    // array to store all digits
    // of the given number
    int digit;
    int N = num;
    while (num != 0)
    {
        digit = num % 10;
        num = num / 10;

        // If any of the condition
        // is true for any digit
        // Then N is not a nude number
        if (digit == 0 || N % digit != 0)
            return false;
    }
    return true;
}

// Driver code
public static void main(String[] args)
{
    int N = 128;

    boolean result = checkDivisbility(N);
    if (result)
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to check if the
# number if nude number or not

# Check if all digits
# of num divide num
def checkDivisbility(num):

    # Array to store all digits
    # of the given number
    digit = 0
    N = num

    while (num != 0):
        digit = num % 10
        num = num // 10

        # If any of the condition
        # is true for any digit
        # then N is not a nude number
        if (digit == 0 or N % digit != 0):
            return False

    return True

# Driver code
if __name__ == '__main__':

    N = 128

    result = checkDivisbility(N)
    if (result):
        print("Yes")
    else:
        print("No")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to check if the
// number if Nude number or not
using System;
class GFG{

// Check if all digits
// of num divide num
static bool checkDivisbility(int num)
{
    // array to store all digits
    // of the given number
    int digit;
    int N = num;
    while (num != 0)
    {
        digit = num % 10;
        num = num / 10;

        // If any of the condition
        // is true for any digit
        // Then N is not a nude number
        if (digit == 0 || N % digit != 0)
            return false;
    }
    return true;
}

// Driver code
public static void Main()
{
    int N = 128;

    bool result = checkDivisbility(N);
    if (result)
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Nidhi_biet
```

## java 描述语言

```
<script>

// Javascript program to check if the
// number if Nude number or not

// Check if all digits
// of num divide num
function checkDivisbility(num)
{
    // array to store all digits
    // of the given number
    let digit;
    let N = num;
    while (num != 0) {
        digit = num % 10;
        num = Math.floor(num / 10);

        // If any of the condition
        // is true for any digit
        // Then N is not a nude number
        if (digit == 0 || N % digit != 0)
            return false;
    }

    return true;
}

// Driver code

    let N = 128;

    let result = checkDivisbility(N);
    if (result)
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** *O(长度为 N )*