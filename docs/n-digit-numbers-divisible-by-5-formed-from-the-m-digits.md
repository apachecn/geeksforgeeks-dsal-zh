# 由 M 位数字组成的可被 5 整除的 N 位数字

> 原文:[https://www . geesforgeks . org/n 位数字-可被 5 整除的 m 位数字/](https://www.geeksforgeeks.org/n-digit-numbers-divisible-by-5-formed-from-the-m-digits/)

给定 M 个唯一的数字和一个数字 N。任务是找出由给定的 M 个数字组成的 N 位数，这些数字可以被 5 整除，并且没有一个数字是重复的。
**注**:如果无法由给定的数字组成 N 位数，打印-1。
**示例:**

> **输入** : N = 3，M = 6，数字[] = {2，3，5，6，7，9}
> **输出** : 20
> **输入** : N = 5，M = 6，数字[] = {0，3，5，6，7，9}
> **输出** : 240

一个数字要被 5 整除，唯一的条件是数字中单位位置的数字必须是 T2 0 或 5 T3。
所以，要找出可被 5 整除且可由给定数字组成的数字的个数，请执行以下操作:

*   检查给定的数字是否同时包含 0 和 5。
*   如果给定的数字同时包含 0 和 5，则单位位置可以用 2 种方式填写，否则单位位置可以用 1 种方式填写。
*   现在，十位数现在可以用剩余的 **M-1** 位中的任何一位来填充。所以，有(M-1)种填充十位数的方法。
*   类似地，现在可以用剩余的(M-2)个数字中的任何一个来填充百的位置，以此类推。

因此，如果给定的数字既有 0 又有 5:

```
Required number of numbers = 2 * (M-1)* (M-2)...N-times. 
```

否则，如果给定的数字有 0 和 5 中的一个而不是两个:

```
Required number of numbers = 1 * (M-1)* (M-2)...N-times. 
```

下面是上述方法的实现。

## C++

```
// CPP program to find the count of all
// possible N digit numbers which are
// divisible by 5 formed from M digits
#include <bits/stdc++.h>
using namespace std;

// Function to find the count of all
// possible N digit numbers which are
// divisible by 5 formed from M digits
int numbers(int n, int arr[], int m)
{
    int isZero = 0, isFive = 0;
    int result = 0;

    // If it is not possible to form
    // n digit number from the given
    // m digits without repetition
    if (m < n) {
        return -1;
    }

    for (int i = 0; i < m; i++) {
        if (arr[i] == 0)
            isZero = 1;

        if (arr[i] == 5)
            isFive = 1;
    }

    // If both zero and five exists
    if (isZero && isFive) {
        result = 2;

        // Remaining N-1 iterations
        for (int i = 0; i < n - 1; i++) {
            result = result * (--m);
        }
    }
    else if (isZero || isFive) {
        result = 1;

        // Remaining N-1 iterations
        for (int i = 0; i < n - 1; i++) {
            result = result * (--m);
        }
    }
    else
        result = -1;

    return result;
}

// Driver code
int main()
{
    int n = 3, m = 6;

    int arr[] = { 2, 3, 5, 6, 7, 9 };

    cout << numbers(n, arr, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the count of all
// possible N digit numbers which are
// divisible by 5 formed from M digits

class GFG {

// Function to find the count of all
// possible N digit numbers which are
// divisible by 5 formed from M digits
    static int numbers(int n, int arr[], int m) {
        int isZero = 0, isFive = 0;
        int result = 0;

        // If it is not possible to form
        // n digit number from the given
        // m digits without repetition
        if (m < n) {
            return -1;
        }

        for (int i = 0; i < m; i++) {
            if (arr[i] == 0) {
                isZero = 1;
            }

            if (arr[i] == 5) {
                isFive = 1;
            }
        }

        // If both zero and five exists
        if (isZero == 1 && isFive == 1) {
            result = 2;

            // Remaining N-1 iterations
            for (int i = 0; i < n - 1; i++) {
                result = result * (--m);
            }
        } else if (isZero == 1 || isFive == 1) {
            result = 1;

            // Remaining N-1 iterations
            for (int i = 0; i < n - 1; i++) {
                result = result * (--m);
            }
        } else {
            result = -1;
        }

        return result;
    }

// Driver code
    public static void main(String[] args) {
        int n = 3, m = 6;

        int arr[] = {2, 3, 5, 6, 7, 9};
        System.out.println(numbers(n, arr, m));

    }
}
// This code is contributed by RAJPUT-JI
```

## 蟒蛇 3

```
# Python 3 program to find the count
# of all possible N digit numbers which
# are divisible by 5 formed from M digits

# Function to find the count of all
# possible N digit numbers which are
# divisible by 5 formed from M digits
def numbers(n, arr, m):

    isZero = 0
    isFive = 0
    result = 0

    # If it is not possible to form
    # n digit number from the given
    # m digits without repetition
    if (m < n) :
        return -1

    for i in range(m) :
        if (arr[i] == 0):
            isZero = 1

        if (arr[i] == 5):
            isFive = 1

    # If both zero and five exists
    if (isZero and isFive) :
        result = 2

        # Remaining N-1 iterations
        for i in range( n - 1):
            m -= 1
            result = result * (m)

    elif (isZero or isFive) :
        result = 1

        # Remaining N-1 iterations
        for i in range(n - 1) :
            m -= 1
            result = result * (m)
    else:
        result = -1

    return result

# Driver code
if __name__ == "__main__":
    n = 3
    m = 6

    arr = [ 2, 3, 5, 6, 7, 9]

    print(numbers(n, arr, m))

# This code is contributed by ChitraNayal
```

## C#

```
// C# program to find the count of all
// possible N digit numbers which are
// divisible by 5 formed from M digits
using System;
public class GFG {

// Function to find the count of all
// possible N digit numbers which are
// divisible by 5 formed from M digits
    static int numbers(int n, int []arr, int m) {
        int isZero = 0, isFive = 0;
        int result = 0;

        // If it is not possible to form
        // n digit number from the given
        // m digits without repetition
        if (m < n) {
            return -1;
        }

        for (int i = 0; i < m; i++) {
            if (arr[i] == 0) {
                isZero = 1;
            }

            if (arr[i] == 5) {
                isFive = 1;
            }
        }

        // If both zero and five exists
        if (isZero == 1 && isFive == 1) {
            result = 2;

            // Remaining N-1 iterations
            for (int i = 0; i < n - 1; i++) {
                result = result * (--m);
            }
        } else if (isZero == 1 || isFive == 1) {
            result = 1;

            // Remaining N-1 iterations
            for (int i = 0; i < n - 1; i++) {
                result = result * (--m);
            }
        } else {
            result = -1;
        }

        return result;
    }

// Driver code
    public static void Main() {
        int n = 3, m = 6;

        int []arr = {2, 3, 5, 6, 7, 9};
        Console.WriteLine(numbers(n, arr, m));

    }
}
// This code is contributed by RAJPUT-JI
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the count of all
// possible N digit numbers which are
// divisible by 5 formed from M digits

// Function to find the count of all
// possible N digit numbers which are
// divisible by 5 formed from M digits
function numbers($n, $arr, $m)
{
    $isZero = 0;
    $isFive = 0;
    $result = 0;

    // If it is not possible to form
    // n digit number from the given
    // m digits without repetition
    if ($m < $n)
    {
        return -1;
    }

    for ($i = 0; $i < $m; $i++)
    {
        if ($arr[$i] == 0)
            $isZero = 1;

        if ($arr[$i] == 5)
            $isFive = 1;
    }

    // If both zero and five exists
    if ($isZero && $isFive)
    {
        $result = 2;

        // Remaining N-1 iterations
        for ($i = 0; $i < $n - 1; $i++)
        {
            $result = $result * (--$m);
        }
    }
    else if ($isZero || $isFive)
    {
        $result = 1;

        // Remaining N-1 iterations
        for ($i = 0; $i < $n - 1; $i++)
        {
            $result = $result * (--$m);
        }
    }
    else
        $result = -1;

    return $result;
}

// Driver code
$n = 3;
$m = 6;

$arr = array( 2, 3, 5, 6, 7, 9 );

echo numbers($n, $arr, $m);

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>
    // Javascript program to find the count of all
    // possible N digit numbers which are
    // divisible by 5 formed from M digits

    // Function to find the count of all
    // possible N digit numbers which are
    // divisible by 5 formed from M digits
    function numbers(n, arr, m) {
        let isZero = 0, isFive = 0;
        let result = 0;

        // If it is not possible to form
        // n digit number from the given
        // m digits without repetition
        if (m < n) {
            return -1;
        }

        for (let i = 0; i < m; i++) {
            if (arr[i] == 0) {
                isZero = 1;
            }

            if (arr[i] == 5) {
                isFive = 1;
            }
        }

        // If both zero and five exists
        if (isZero == 1 && isFive == 1) {
            result = 2;

            // Remaining N-1 iterations
            for (let i = 0; i < n - 1; i++) {
                result = result * (--m);
            }
        } else if (isZero == 1 || isFive == 1) {
            result = 1;

            // Remaining N-1 iterations
            for (let i = 0; i < n - 1; i++) {
                result = result * (--m);
            }
        } else {
            result = -1;
        }

        return result;
    }

    let n = 3, m = 6;

    let arr = [2, 3, 5, 6, 7, 9];
    document.write(numbers(n, arr, m));

</script>
```

**Output:** 

```
20
```