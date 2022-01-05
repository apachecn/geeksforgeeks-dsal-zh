# 可逆数字

> 原文:[https://www.geeksforgeeks.org/reversible-numbers/](https://www.geeksforgeeks.org/reversible-numbers/)

如果一个数和它的倒数只有奇数，那么这个数就是可逆的。问题是找出一个数是否可逆。

示例:

```
Input: 36 
Output: Reversible number
as 36 + 63 = 99 has only odd digits.

Input: 409 
Output: Reversible number
as 409 + 904 = 1313 has only odd digits.

Input: 35 
Output: Not Reversible number
as 35 + 53 = 88 has only odd digits
```

**天真法**

计算每个数字的倒数，并将其加到数字上。如果结果是可逆的，增加计数值。为从 1 到 n 的每个数字计算这个。

**时间复杂度:** O(10^n)，因为它应该计算每个数字的倒数。

**进阶法**

*   **1 位数:**任何一个数字加起来都是偶数，所以没有解。
*   **2 位数:**两位数必须为奇数。
    *   如果 a+b > 10，则我们有一个结转，因此结果的第一个数字将与第二个数字具有不同的奇偶校验。
    *   所以，只有当 a+b < 10，a+b 为奇数时，才能形成解。总共有 20 个这样的数字是可能的。
*   **3 位数:**
    *   中间的数字需要添加到自身。这意味着第三个数字必须有一个结转并且是奇数。
    *   由于第三个数字是奇数，如果第二个数字没有结转，第一个数字也是奇数，当第二个数字小于 5 时会发生这种情况，这为我们提供了第一/第三个数字集的 20 个选项和中间的 5 个选项。总共 100 对。
*   **4 位数:**有两对，说是内外对。
    *   如果内部对有遗留物，那么外部对也必须有遗留物。
    *   否则，两个内部对将具有不同的奇偶性。
    *   如果内部对有进位，那么外部对将有不同的奇偶校验，因为第一个数字将以进位结束，而最后一个数字不会得到进位。
    *   因此，只有当没有一对有结转时，我们才有解决办法。
    *   总的来说:对于外部对，这给了我们在两位数情况下看到的 20 个选择。它给了我们 30 个内对的例子，因为它们也可以包含一个零。
        或者我们总共得到 20*30 = 600 个解。
*   **5、9、13..位数:**无解为 1 位数。
*   **6、8、10..位数:**与 2 位数相同，即如果 n = 2*k，则总解= 20*30^(k-1).
*   **7、11、15..位数:**与 3 位数相同，即如果 n = 4k + 3，则总解= 100*500^(k).

**概括解决方案:**

*   所有偶数数字(2、4、6、8..)具有相同的公式，因此我们可以推广
    ,对于某个整数 k，n = 2k，我们有 20*30^(k-1)解
    ,它代表外部对以及所有内部对。
*   对于 n (3，7，11..)的形式 4k + 3 (k 是整数)，我们有中间的数字和
    外对给我们 5 和 20 个选项，就像 3 位数的情况一样。
    然后我们有一组内部对，给我们 20 和 25 个解。
    所以这意味着我们可以把它推广到 20*5*(20*25)^(k) = 100*500^(k).
*   对于形式为 4k+ 1 的 n，这意味着 1，5，9..这些都没有任何解决办法。

**检查数字是否可逆的程序**

## C++

```
// C++ program to check if a given
// number is reversible or not
#include <iostream>
#include <cmath>
using namespace std;

// Function to check reversible number
void checkReversible (int n)
{
    int rev = 0, rem;

    // Calculate reverse of n
    int flag = n;
    while (flag)
    {
        rem = flag % 10;
        rev *= 10;
        rev += rem;
        flag /= 10;
    }

    // Calculate sum of number
    // and its reverse
    int sum = rev + n;

    // Check for reverse number
    // reach digit must be odd
    while (sum && (rem % 2 != 0))
    {
        rem = sum % 10;
        sum /= 10;
    }

    if (sum == 0)
        cout << "Reversible Number";
    else
        cout << "Non-Reversible Number";
}

// Driver function
int main()
{
    int n = 36;
    checkReversible(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a given
// number is reversible or not
import java.io.*;

class GFG {

    // Function to check reversible number
    static void checkReversible (int n)
    {
        int rev = 0, rem = 0;

        // Calculate reverse of n
        int flag = n;
        while (flag>0)
        {
            rem = flag % 10;
            rev *= 10;
            rev += rem;
            flag /= 10;
        }

        // Calculate sum of number
        // and its reverse
        int sum = rev + n;

        // Check for reverse number
        // reach digit must be odd
        while (sum > 0 && (rem % 2 != 0))
        {
            rem = sum % 10;
            sum /= 10;
        }

        if (sum == 0)
            System.out.println("Reversible Number");
        else
            System.out.println("Non-Reversible Number");
    }

    // Driver function
    public static void main (String[] args)
    {
        int n = 36;
        checkReversible(n);

    }
}
// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program to check if a given
# number is reversible or not

# Function to check reversible number
def checkReversible (n):

    rev = 0

    # Calculate reverse of n
    flag = n

    while (flag != 0):
        rem = flag % 10
        rev *= 10
        rev += rem
        flag //= 10

    # Calculate sum of number
    # and its reverse
    sum = rev + n

    # Check for reverse number
    # reach digit must be odd
    while (sum and ((rem % 2) != 0)):
        rem = sum % 10
        sum //= 10

    if (sum == 0):
        print("Reversible Number")
    else:
        print("Non-Reversible Number")

# Driver Code
n = 36

checkReversible(n)

# This code is contributed by sanjoy_62
```

## C#

```
// C# program to check if a given
// number is reversible or not
using System;

class GFG {

    // Function to check reversible number
    static void checkReversible (int n)
    {
        int rev = 0, rem = 0;

        // Calculate reverse of n
        int flag = n;
        while (flag > 0)
        {
            rem = flag % 10;
            rev *= 10;
            rev += rem;
            flag /= 10;
        }

        // Calculate sum of number
        // and its reverse
        int sum = rev + n;

        // Check for reverse number
        // reach digit must be odd
        while (sum > 0 && (rem % 2 != 0))
        {
            rem = sum % 10;
            sum /= 10;
        }

        if (sum == 0)
        Console.WriteLine("Reversible Number");
        else
        Console.WriteLine("Non-Reversible Number");
    }

    // Driver function
    public static void Main ()
    {
        int n = 36;
          checkReversible(n);

    }
}

// This code is contributed by vt_m.
```

**输出:**

```
Reversible Number
```

**将可逆总数计数到最高的程序**

## C++

```
// C++ program to find the count of
// reversible numbers upto a given number n
#include <iostream>
#include <cmath>
using namespace std;

// Function to calculate the count of reversible number
void countReversible (int n)
{
    int count = 0;

    // Calculate counts of
    // reversible number of 1 to n-digits
    for ( int i = 1; i <= n; i++)
    {
        // All four possible cases and their formula
        switch (i % 4)
        {

        // for i of form 2k
        case 0:
        case 2:
            count += 20 * pow( 30, ( i / 2 - 1));
            break;

        // for i of form 4k + 3
        case 3:
            count += 100 * pow ( 500, i / 4 );
            break;

        // for i of form 4k + 1 no solution
        case 1:
            break;
        }
    }
    cout << count;
}

// Driver function
int main()
{
    // count up-to 9 digit numbers (1 billion)
    int n = 9;
    countReversible(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the count of
// reversible numbers upto a given number n
import java.io.*;

class GFG {

    // Function to calculate the count
    // of reversible number
    static void countReversible (int n)
    {
        int count = 0;

        // Calculate counts of
        // reversible number of 1 to n-digits
        for ( int i = 1; i <= n; i++)
        {
            // All four possible cases
            // and their formula
            switch (i % 4)
            {

            // for i of form 2k
            case 0:
            case 2:
                count += 20 * Math.pow( 30, ( i / 2 - 1));
                break;

            // for i of form 4k + 3
            case 3:
                count += 100 * Math.pow ( 500, i / 4 );
                break;

            // for i of form 4k + 1 no solution
            case 1:
                break;
            }
        }
        System.out.println(count);
    }

    // Driver function
    public static void main (String[] args)
    {
        // count up-to 9 digit numbers (1 billion)
        int n = 9;
        countReversible(n);

    }
}
// This code is contributed by vt_m.
```

## C#

```
// C# program to find the count of
// reversible numbers upto a given number n
using System;

class GFG {

    // Function to calculate the
    // count of reversible number
    static void countReversible (int n)
    {
        int count = 0;

        // Calculate counts of
        // reversible number of 1 to n-digits
        for ( int i = 1; i <= n; i++)
        {
            // All four possible cases
            // and their formula
            switch (i % 4)
            {

            // for i of form 2k
            case 0:
            case 2:
                count += 20 * (int)Math.Pow( 30, ( i / 2 - 1));
                break;

            // for i of form 4k + 3
            case 3:
                count += 100 * (int)Math.Pow ( 500, i / 4 );
                break;

            // for i of form 4k + 1 no solution
            case 1:
                break;
            }
        }
        Console.WriteLine(count);
    }

    // Driver function
    public static void Main ()
    {
        // count up-to 9 digit numbers (1 billion)
        int n = 9;
        countReversible(n);

    }
}

// This code is contributed by vt_m.
```

**输出:**

```
608720
```

时间复杂度 O(n)
**参考:** [欧拉 145 计划:十亿以下可逆数有多少？](http://www.mathblog.dk/project-euler-145-how-many-reversible-numbers-are-there-below-one-billion/)

本文由[**Shivam Pradhan(anuj _ charm)**](https://www.facebook.com/anuj.charm)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。