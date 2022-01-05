# 如何使用高斯算法

计算给定年份的复活节日期

> 原文:[https://www . geesforgeks . org/如何使用高斯算法计算特定年份的复活节日期/](https://www.geeksforgeeks.org/how-to-calculate-the-easter-date-for-a-given-year-using-gauss-algorithm/)

给定一个整数 **Y** ，表示一年，作为输入，任务是找到该年的复活节日期。

**示例:**

> **输入:** Y = 2020
> **输出:** 2020-04-12
> **说明:**
> 2020 年复活节是 4 月 12 日
> 因此，复活节日期将是 2020-04-12
> 
> **输入:** Y = 1991
> **输出:** 1991-03-30
> **解释:**
> 1991 年，复活节是 3 月 30 日
> 因此，复活节日期将是 1991-03-30

**方法:** **高斯复活节算法**用于轻松计算一年的复活节日期。卡尔·弗里德里希·高斯首先想到了这个算法。关于高斯是如何得出这个算法的，没有适当的解释，但是这个算法的实现被证明是非常精确的。
高斯复活节算法的详细解释如下:

*   首先，计算年 **Y** 在美托周期中的位置。

> A = Y mod 19

*   现在，根据儒略历找出闰日的数字。

> B = Y mod 4

*   然后，让我们考虑一下，非闰年比 52 周长一天。

> C = Y mod 7

*   **M** 取决于一年中的世纪 **Y** 。对于 19 世纪，M = 23。对于 21 世纪，M = 24 等等。
    使用以下关系计算:

> P =楼板(y/100)
> q =((13+8 * p)/25)
> m =(15–q+p-(p/4))mod 30

*   儒略历和公历的闰日数之差由下式给出:

> N = （4 + P – （P / 4）） mod 7

*   为了找到逾越节满月的日期，3 月 21 日的天数由下式给出:

> D = (19*A + M) mod 30

*   并且，从逾越节满月到下一个星期日的天数由下式给出:

> E = (N + 2*B + 4*C + 6*D) mod 7

*   因此，使用 **D** 和 **E** ，复活节周日的日期将是**3 月(22 + D + E)** 。如果这个数字大于 31，那么我们就移到 4 月。
*   现在农历月份不是正好 30 天而是少了一点 30 天。因此，为了消除这种不一致，遵循以下情况:

> if (D == 29)和(E == 6)
> 返回“4 月 19 日”
> 否则 if (D == 28)和(E == 6)
> 返回“4 月 18 日”

下面是上述方法的实现:

## C++

```
// C++ program for the
// above approach

#include <iostream>
#include <math.h>

using namespace std;

// Function calculates and prints
// easter date for given year Y
void gaussEaster(int Y)
{
    float A, B, C, P, Q,
        M, N, D, E;

    // All calculations done
    // on the basis of
    // Gauss Easter Algorithm
    A = Y % 19;
    B = Y % 4;
    C = Y % 7;
    P = (float)floor(Y / 100);
    Q = (float)floor((13 + 8 * P) / 25);
    M = (int)(15 - Q + P - P / 4) % 30;
    N = (int)(4 + P - P / 4) % 7;
    D = (int)(19 * A + M) % 30;
    E = (int)(2 * B + 4 * C + 6 * D + N) % 7;
    int days = (int)(22 + D + E);

    // A corner case,
    // when D is 29
    if ((D == 29) && (E == 6)) {
        cout << Y << "-04-19";
        return;
    }
    // Another corner case,
    // when D is 28
    else if ((D == 28) && (E == 6)) {
        cout << Y << "-04-18";
        return;
    }
    else {
        // If days > 31, move to April
        // April = 4th Month
        if (days > 31) {
            cout << Y << "-04-"
                 << (days - 31);
            return;
        }
        else {
            // Otherwise, stay on March
            // March = 3rd Month
            cout << Y << "-03-"
                 << days;
            return;
        }
    }
}

// Driver Code
int main()
{
    int Y = 2020;
    gaussEaster(Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach

import java.util.Date;
import java.util.Scanner;

// Function calculates and prints
// easter date for given year Y
public class GaussEaster {

    static void gaussEaster(int Y)
    {
        float A, B, C, P, Q,
            M, N, D, E;

        // All calculations done
        // on the basis of
        // Gauss Easter Algorithm
        A = Y % 19;
        B = Y % 4;
        C = Y % 7;
        P = (float)Math.floor(Y / 100);
        Q = (float)Math.floor(
            (13 + 8 * P) / 25);
        M = (15 - Q + P - P / 4) % 30;
        N = (4 + P - P / 4) % 7;
        D = (19 * A + M) % 30;
        E = (2 * B + 4 * C + 6 * D + N) % 7;
        int days = (int)(22 + D + E);

        // A corner case,
        // when D is 29
        if ((D == 29) && (E == 6)) {
            System.out.println(Y + "-04"
                               + "-19");
            return;
        }
        // Another corner case,
        // when D is 28
        else if ((D == 28) && (E == 6)) {
            System.out.println(Y + "-04"
                               + "-18");
            return;
        }
        else {

            // If days > 31, move to April
            // April = 4th Month
            if (days > 31) {
                System.out.println(Y + "-04-"
                                   + (days - 31));
                return;
            }
            // Otherwise, stay on March
            // March = 3rd Month
            else {
                System.out.println(Y + "-03-"
                                   + days);
                return;
            }
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int Y = 2020;
        gaussEaster(Y);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the
# above approach
import math

# Function calculates and prints
# easter date for given year Y
def gaussEaster(Y):

    # All calculations done
    # on the basis of
    # Gauss Easter Algorithm
    A = Y % 19
    B = Y % 4
    C = Y % 7

    P = math.floor(Y / 100)
    Q = math.floor((13 + 8 * P) / 25)
    M = (15 - Q + P - P // 4) % 30
    N = (4 + P - P // 4) % 7
    D = (19 * A + M) % 30
    E = (2 * B + 4 * C + 6 * D + N) % 7
    days = (22 + D + E)

    # A corner case,
    # when D is 29
    if ((D == 29) and (E == 6)):
        print(Y, "-04-19")
        return

    # Another corner case,
    # when D is 28
    elif ((D == 28) and (E == 6)):
        print(Y, "-04-18")
        return

    else:

        # If days > 31, move to April
        # April = 4th Month
        if (days > 31):
            print(Y, "-04-", (days - 31))
            return

        else:

            # Otherwise, stay on March
            # March = 3rd Month
            print(Y, "-03-", days)
            return

# Driver Code
Y = 2020

gaussEaster(Y)

# This code is contributed by code_hunt
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

// Function calculates and prints
// easter date for given year Y
static void gaussEaster(int Y)
{
    float A, B, C, P, Q,
            M, N, D, E;

    // All calculations done
    // on the basis of
    // Gauss Easter Algorithm
    A = Y % 19;
    B = Y % 4;
    C = Y % 7;
    P = (float)(Y / 100);
    Q = (float)(
        (13 + 8 * P) / 25);
    M = (15 - Q + P - P / 4) % 30;
    N = (4 + P - P / 4) % 7;
    D = (19 * A + M) % 30;
    E = (2 * B + 4 * C + 6 * D + N) % 7;
    int days = (int)(22 + D + E);

    // A corner case,
    // when D is 29
    if ((D == 29) && (E == 6))
    {
        Console.Write(Y + "-04" + "-19");
        return;
    }

    // Another corner case,
    // when D is 28
    else if ((D == 28) && (E == 6))
    {
          Console.Write(Y + "-04" + "-18");
          return;
    }
    else
    {

        // If days > 31, move to April
        // April = 4th Month
        if (days > 31)
        {
            Console.Write(Y + "-04-" +
                         (days - 31));
            return;
        }
        // Otherwise, stay on March
        // March = 3rd Month
        else
        {
            Console.Write(Y + "-03-" + days);
            return;
        }
    }
}

// Driver code
public static void Main(string[] args)
{
    int Y = 2020;
    gaussEaster(Y);
}
}

// This code is contributed by Ritik Bansal
```

## java 描述语言

```
<script>
// Javascript implementation for the above approach

// Function calculates and prlets
// easter date for given year Y

    function gaussEaster(Y)
    {
        let A, B, C, P, Q,
            M, N, D, E;

        // All calculations done
        // on the basis of
        // Gauss Easter Algorithm
        A = Y % 19;
        B = Y % 4;
        C = Y % 7;
        P = Math.floor(Y / 100);
        Q = Math.floor(
            (13 + 8 * P) / 25);
        M = (15 - Q + P - P / 4) % 30;
        N = (4 + P - P / 4) % 7;
        D = (19 * A + M) % 30;
        E = (2 * B + 4 * C + 6 * D + N) % 7;
        let days = (22 + D + E);

        // A corner case,
        // when D is 29
        if ((D == 29) && (E == 6)) {
            document.write(Y + "-04"
                               + "-19");
            return;
        }
        // Another corner case,
        // when D is 28
        else if ((D == 28) && (E == 6)) {
            document.write(Y + "-04"
                               + "-18");
            return;
        }
        else {

            // If days > 31, move to April
            // April = 4th Month
            if (days > 31) {
                document.write(Y + "-04-"
                                   + (days - 31));
                return;
            }
            // Otherwise, stay on March
            // March = 3rd Month
            else {
                document.write(Y + "-03-"
                                   + days);
                return;
            }
        }
    }

    // Driver Code

    let Y = 2020;
    gaussEaster(Y);

</script>
```

**Output:** 

```
2020-04-12
```

***时间复杂度:** O(1)*
***辅助空间:** O(1)*