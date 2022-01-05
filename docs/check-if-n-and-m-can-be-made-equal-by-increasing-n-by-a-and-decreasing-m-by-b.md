# 检查 N 和 M 是否可以通过增加 A 的 N 和减少 B 的 M 而相等

> 原文:[https://www . geeksforgeeks . org/check-if-n-and-m-can-make-equal-by-n-a-递增-n-a-递减-m-b/](https://www.geeksforgeeks.org/check-if-n-and-m-can-be-made-equal-by-increasing-n-by-a-and-decreasing-m-by-b/)

给定四个数字 **M** 、 **N** 、 **A** 和 **B** ，任务是通过执行以下任一操作检查 **M** 和 **N** 是否可以相等:

*   **M** 可增加 **A** 和 **N** 可减少 **B**
*   让他们两个保持原样。

**示例:**

> **输入:** M = 2，N = 8，A = 3，B = 3
> **输出:**是
> **说明:**
> 第一次操作后:
> M 可以增加 A，所以 M = 2 + 3 = 5
> N 可以减少 B，所以 N = 8–3 = 5
> 最后 M = N = 5。
> 
> **输入:** M = 6，N = 4，A = 2，B = 1
> T3】输出:否

**逼近:**仔细观察可以发现，由于我们在增加 M，减少 N，所以只有 M 小于 N 时，才能使它们相等，因此当 M 小于 N 时，每一步都有两种情况:

1.  m 可以增加 A，N 可以减少 b。
2.  让他们两个保持原样。

可以做的另一个观察是当 **M** 增大而 **N** 减小时， **M** 和 **N** 之间的绝对距离减小了 **A + B** 的因子。例如:

> 设 M = 2，N = 14，A = 3，B = 3。
> 
> *   在步骤 1 中，M = 5，N = 11。M 和 N 之间的绝对距离减少了 6。也就是说，最初的绝对距离是 12(14–2)。执行给定步骤后，绝对距离变为 6(11–5)。
> *   第二步，M = 8，N = 8。M 和 N 之间的绝对距离再次减少了 6，从而使 M 和 N 相等。

从上面的例子中，我们可以得出这样的结论:只有检查 **M** 和 **N** 之间的绝对距离是否为 **(A + B)** 的倍数，才能在恒定时间内解决这个问题。

*   如果是倍数，那么 M 和 N 可以相等。
*   否则，他们就不能平等。

以下是上述方法的实现:

## C++

```
// C++ program to check if two numbers
// can be made equal by increasing
// the first by a and decreasing
// the second by b

#include <bits/stdc++.h>
using namespace std;

// Function to whether the numbers
// can be made equal or not
bool checkEqualNo(int m, int n, int a, int b)
{
    if (m <= n) {

        // Check whether the numbers can reach
        // an equal point or not
        if ((n - m) % (a + b) == 0) {
            return true;
        }
        else {
            return false;
        }
    }
    else {

        // M and N cannot be made equal by
        // increasing M and decreasing N when
        // M is already greater than N
        return false;
    }
}

// Driver code
int main()
{
    int M = 2, N = 8;
    int A = 3, B = 3;

    if (checkEqualNo(M, N, A, B)) 
        cout << "Yes" << endl;
    else
        cout << "No" << endl;

return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if two numbers
// can be made equal by increasing
// the first by a and decreasing
// the second by b
class GFG 
{

    // Function to whether the numbers
    // can be made equal or not
    static boolean checkEqualNo(int m, int n, int a, int b)
    {
        if (m <= n) {

            // Check whether the numbers can reach
            // an equal point or not
            if ((n - m) % (a + b) == 0) {
                return true;
            }
            else {
                return false;
            }
        }
        else {

            // M and N cannot be made equal by
            // increasing M and decreasing N when
            // M is already greater than N
            return false;
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int M = 2, N = 8;
        int A = 3, B = 3;

        if (checkEqualNo(M, N, A, B) == true) 
            System.out.println("Yes");
        else
            System.out.println("No");

    }
}

// This code is contributed by Yash_R
```

## 蟒蛇 3

```
# Python3 program to check if two numbers
# can be made equal by increasing
# the first by a and decreasing
# the second by b

# Function to whether the numbers
# can be made equal or not
def checkEqualNo(m, n, a, b) :
    if (m <= n) :

        # Check whether the numbers can reach
        # an equal point or not
        if ((n - m) % (a + b) == 0) :
            return True;

        else :
            return False;

    else :

        # M and N cannot be made equal by
        # increasing M and decreasing N when
        # M is already greater than N
        return False;

# Driver code
if __name__ == "__main__" :

    M = 2; N = 8;
    A = 3; B = 3;

    if (checkEqualNo(M, N, A, B)) :
        print("Yes");
    else :
        print("No");

# This code is contributed by Yash_R
```

## C#

```
// C# program to check if two numbers
// can be made equal by increasing
// the first by a and decreasing
// the second by b
using System;

class GFG 
{

    // Function to whether the numbers
    // can be made equal or not
    static bool checkEqualNo(int m, int n, int a, int b)
    {
        if (m <= n) {

            // Check whether the numbers can reach
            // an equal point or not
            if ((n - m) % (a + b) == 0) {
                return true;
            }
            else {
                return false;
            }
        }
        else {

            // M and N cannot be made equal by
            // increasing M and decreasing N when
            // M is already greater than N
            return false;
        }
    }

    // Driver code
    public static void Main (String[] args)
    {
        int M = 2;
        int N = 8;
        int A = 3;
        int B = 3;

        if (checkEqualNo(M, N, A, B) == true) 
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by Yash_R
```

**Output:**

```
Yes

```