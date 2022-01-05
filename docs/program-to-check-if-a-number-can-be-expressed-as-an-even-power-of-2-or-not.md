# 检查一个数是否可以表示为 2 的偶次幂的程序

> 原文:[https://www . geeksforgeeks . org/program-to-check-如果一个数字可以表示为 2 的偶数幂或不/](https://www.geeksforgeeks.org/program-to-check-if-a-number-can-be-expressed-as-an-even-power-of-2-or-not/)

给定一个正整数 **N** ，任务是检查给定的整数是否为**2**T5 的偶数[次幂。](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)

**示例:**

> **输入:** N = 4
> **输出:**是
> **说明:** 4 可以表示为 2 <sup>2</sup> = 4，是 2 的偶数次方。
> 
> **输入:** N = 8
> **输出:** No
> **说明:** 8 可以表示为 2 <sup>3</sup> = 8，是 2 的奇次幂。

**天真法:**最简单的方法是迭代 **2** 的所有指数值，检查对应的值是否为 **N** ，[指数是否为偶数](https://www.geeksforgeeks.org/check-if-a-n-base-number-is-even-or-odd/)。如果两者都为真，则打印**“是”**。否则，如果 **2** 的当前指数超过 **N** ，则打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if N can be
// expressed as an even power of 2
bool checkEvenPower(int n)
{
    int x = 0;

    // Iterate till x is N
    while (x < n) {

        int value = pow(2, x);

        if (value == n) {

            // if x is even then
            // return true
            if (x % 2 == 0)
                return true;
            else
                return false;
        }

        // Increment x
        x++;
    }

    // If N is not a power of 2
    return false;
}

// Driver Code
int main()
{
    int N = 4;
    cout << (checkEvenPower(N) ? "Yes" : "No");
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to check if N can be
// expressed as an even power of 2
static boolean checkEvenPower(int n)
{
    int x = 0;

    // Iterate till x is N
    while (x < n)
    {
        int value = (int)Math.pow(2, x);

        if (value == n)
        {

            // if x is even then
            // return true
            if (x % 2 == 0)
                return true;
            else
                return false;
        }

        // Increment x
        x++;
    }

    // If N is not a power of 2
    return false;
}

// Driver Code
public static void main (String[] args)
{
    int N = 4;

    System.out.println((checkEvenPower(N) ? "Yes" : "No"));
}
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if N can be
# expressed as an even power of 2
def checkEvenPower(n):

    x = 0

    # Iterate till x is N
    while (x < n):
        value = pow(2, x)

        if (value == n):

            # If x is even then
            # return true
            if (x % 2 == 0):
                return True
            else:
                return False

        # Increment x
        x += 1

    # If N is not a power of 2
    return False

# Driver Code
if __name__ == '__main__':

    N = 4

    if checkEvenPower(N):
        print("Yes")
    else:
        print("No")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check if N can be
// expressed as an even power of 2
static bool checkEvenPower(int n)
{
    int x = 0;

    // Iterate till x is N
    while (x < n)
    {
        int value = (int)Math.Pow(2, x);

        if (value == n)
        {

            // if x is even then
            // return true
            if (x % 2 == 0)
                return true;
            else
                return false;
        }

        // Increment x
        x++;
    }

    // If N is not a power of 2
    return false;
}

// Driver Code
static public void Main()
{
    int N = 4;

    Console.Write((checkEvenPower(N) ? "Yes" : "No"));
}
}

// This code is contributed by avijitmondal1998
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if N can be
// expressed as an even power of 2
function checkEvenPower(n)
{
    var x = 0;

    // Iterate till x is N
    while (x < n)
    {
        var value = Math.pow(2, x);

        if (value == n)
        {

            // If x is even then
            // return true
            if (x % 2 == 0)
                return true;
            else
                return false;
        }

        // Increment x
        x++;
    }

    // If N is not a power of 2
    return false;
}

// Driver code
var N = 4;

document.write((checkEvenPower(N) ? "Yes" : "No"));

// This code is contributed by Ankita saini

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*

**另一种方法:**上述方法也可以使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)实现。按照以下步骤解决问题:

*   初始化两个变量，说**低**为 **0** 和**高**为 **N** 。
*   重复直到**低电平**超过**高电平**:
    *   求**中间**的值为**低+(高-低)/2** 。
    *   如果 **2 <sup>中</sup>T3】的值为 **N** ，而**中**的值为偶数，则打印**“是”**[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。**
    *   如果 **2 <sup>中间</sup> < N** 的值，更新**低**的值为**(中间+ 1)** 。
    *   否则，将**高值**更新为**(中-1)**。
*   完成上述步骤后，如果循环没有中断，则打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if N can be
// expressed as an even power of 2 or not
string checkEvenPower(int n)
{
    int low = 0, high = n;

    // Iterate until low > high
    while (low <= high) {

        // Calculate mid
        int mid = low + (high - low) / 2;

        int value = pow(2, mid);

        // If 2 ^ mid is equal to n
        if (value == n) {

            // If mid is odd
            if (mid % 2 == 1)
                return "No";
            else
                return "Yes";
        }

        // Update the value of low
        else if (value < n)
            low = mid + 1;

        // Update the value of high
        else
            high = mid - 1;
    }

    // Otherwise
    return "No";
}

// Driver Code
int main()
{
    int N = 4;
    cout << checkEvenPower(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if N can be
// expressed as an even power of 2 or not
static String checkEvenPower(int n)
{
    int low = 0, high = n;

    // Iterate until low > high
    while (low <= high)
    {

        // Calculate mid
        int mid = low + (high - low) / 2;

        int value = (int) Math.pow(2, mid);

        // If 2 ^ mid is equal to n
        if (value == n)
        {

            // If mid is odd
            if (mid % 2 == 1)
                return "No";
            else
                return "Yes";
        }

        // Update the value of low
        else if (value < n)
            low = mid + 1;

        // Update the value of high
        else
            high = mid - 1;
    }

    // Otherwise
    return "No";
}

// Driver code
public static void main(String[] args)
{
    int N = 4;

    System.out.println(checkEvenPower(N));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if N can be
# expressed as an even power of 2 or not
def checkEvenPower(n):

    low, high = 0, n

    # Iterate until low > high
    while (low <= high):

        # Calculate mid
        mid = low + (high - low) / 2
        value = pow(2, mid)

        # If 2 ^ mid is equal to n
        if (value == n):

            # If mid is odd
            if (mid % 2 == 1):
                return "No"
            else:
                return "Yes"

        # Update the value of low
        elif (value < n):
            low = mid + 1

        # Update the value of high
        else:
            high = mid - 1

    # Otherwise
    return "No"

# Driver code
N = 4

print(checkEvenPower(N))

# This code is contributed by SoumikMondal
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

// Function to check if N can be
// expressed as an even power of 2 or not
static String checkEvenPower(int n)
{
    int low = 0, high = n;

    // Iterate until low > high
    while (low <= high)
    {

        // Calculate mid
        int mid = low + (high - low) / 2;

        int value = (int) Math.Pow(2, mid);

        // If 2 ^ mid is equal to n
        if (value == n)
        {

            // If mid is odd
            if (mid % 2 == 1)
                return "No";
            else
                return "Yes";
        }

        // Update the value of low
        else if (value < n)
            low = mid + 1;

        // Update the value of high
        else
            high = mid - 1;
    }

    // Otherwise
    return "No";
}

// Driver code
public static void Main(String[] args)
{
    int N = 4;

    Console.WriteLine(checkEvenPower(N));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Function to check if N can be
    // expressed as an even power of 2 or not
    function checkEvenPower(n)
    {
        var low = 0, high = n;

        // Iterate until low > high
        while (low <= high) {

            // Calculate mid
            var mid = low + (high - low) / 2;
            var value = parseInt( Math.pow(2, mid));

            // If 2 ^ mid is equal to n
            if (value == n)
            {

                // If mid is odd
                if (mid % 2 == 1)
                    return "No";
                else
                    return "Yes";
            }

            // Update the value of low
            else if (value < n)
                low = mid + 1;

            // Update the value of high
            else
                high = mid - 1;
        }

        // Otherwise
        return "No";
    }

    // Driver code
        var N = 4;
        document.write(checkEvenPower(N));

// This code is contributed by gauravrajput1
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以基于以下观察进行优化:

*   **2** 的二进制幂表示形式如下:

> 2<sup>0</sup>= 00…0001
> 2<sup>1</sup>= 00…0010
> 2<sup>2</sup>= 00…0100
> 2<sup>3</sup>= 00…1000

*   从上面的二进制表示中观察到，一个数要成为 2 的[次幂](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)，它必须只有**1 个设定位**，要成为 2 的**偶次幂**，那么唯一的设定位应该在奇数位置。
*   因此，能够区分这些偶次方和奇次方的数是 **5 (0101)** 。假设该值适合 64 位长整数， **0x55555555** 与 **N** 的[位“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)是正数，当且仅当设置了奇数位时，即具有 2 的偶数幂。

因此，思路是检查 **0x55555555** 、 **N** 的[位“与”](https://www.geeksforgeeks.org/bitwise-and-or-of-a-range/)是否为正，然后打印**“是”。**否则**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if N can be
// expressed as an even power of 2 or not
bool checkEvenPower(long long int N)
{
    // If N is not a power of 2
    if ((N & (N - 1)) != 0)
        return false;

    // Bitwise AND operation
    N = N & 0x55555555;

    return (N > 0);
}

// Driver Code
int main()
{
    int N = 4;
    cout << checkEvenPower(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to check if N can be
// expressed as an even power of 2 or not
static boolean checkEvenPower(long N)
{

    // If N is not a power of 2
    if ((N & (N - 1)) != 0)
        return false;

    // Bitwise AND operation
    N = N & 0x55555555;

    return (N > 0);
}

// Driver Code
public static void main (String[] args)
{
    long N = 4;

    System.out.println(checkEvenPower(N)? 1 : 0);
}
}

// This code is contributed by rag2127
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if N can be
# expressed as an even power of 2 or not
def checkEvenPower(N):

    # If N is not a power of 2   
    if ((N & (N - 1)) != 0):
        return false

    # Bitwise AND operation
    N = N & 0x55555555
    return (N > 0)

# Driver Code
N = 4
print(1 if checkEvenPower(N) else 0)

# This code is contributed by shivanisinghss2110
```

## C#

```
// C# program for the above approach

using System;

public class GFG {

    // Function to check if N can be
    // expressed as an even power of 2 or not
    static bool checkEvenPower(long N) {

        // If N is not a power of 2
        if ((N & (N - 1)) != 0)
            return false;

        // Bitwise AND operation
        N = N & 0x55555555;

        return (N > 0);
    }

    // Driver Code
    public static void Main(String[] args) {
        long N = 4;

        Console.WriteLine(checkEvenPower(N) ? 1 : 0);
    }
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to check if N can be
// expressed as an even power of 2 or not
function checkEvenPower(N)
{

    // If N is not a power of 2
    if ((N & (N - 1)) != 0)
        return false;

    // Bitwise AND operation
    N = N & 0x55555555;

    return (N > 0);
}

// Driver code
    let N = 4;

    document.write(checkEvenPower(N)? 1 : 0);

// This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)