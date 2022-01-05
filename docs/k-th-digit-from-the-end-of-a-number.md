# 从一个数字结束的第 K 个数字

> 原文:[https://www . geeksforgeeks . org/k-th-从数字末尾算起/](https://www.geeksforgeeks.org/k-th-digit-from-the-end-of-a-number/)

给定一个整数 **N** ，任务是从一个整数 **N** 的末尾找到 **K** <sup>第</sup>位。如果 **K** <sup>第</sup>位不存在，则打印 **-1** 。

**示例:**

> **输入** : N = 2354，K = 2
> 输出 : 5
> 
> **输入** : N = 1234，K = 1
> 输出 : 4

**天真法:**解决这个问题最简单的方法就是[将整数 N 转换为字符串。](https://www.geeksforgeeks.org/converting-string-to-number-and-vice-versa-in-c/)按照以下步骤解决此问题:

*   如果 **K** 小于等于 **0，**则打印 **-1** 返回。
*   将 **N** 转换成字符串，储存在**温度**中。
*   如果 **K** 大于**温度**的大小，则打印 **-1** ，否则从最后打印 **K** 字符。

下面是上述方法的实现:

## C++

```
// c++ program for the above approach
#include <bits/stdc++.h>

using namespace std;

// Function to find the kth digit
// from last in an integer n
void kthDigitFromLast(int n, int k)
{

    // If k is less than equal to 0
    if (k <= 0) {
        cout << -1 << endl;
        return;
    }

    // Convert integer into string
    string temp = to_string(n);

    // If k is greater than length of the
    // string temp
    if (k > temp.length()) {
        cout << -1 << endl;
    }
    // Print the k digit from last
    else {
        cout << temp[temp.length() - k] - '0';
    }
}

// Driver code
int main()
{
    // Given Input
    int n = 2354;
    int k = 2;

    // Function call
    kthDigitFromLast(n, k);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find the kth digit
// from last in an integer n   
public static void kthDigitFromLast(int n, int k)
{

    // If k is less than equal to 0
    if (k <= 0)
    {
        System.out.println(-1);
        return;
    }

    // Convert integer into string
    String temp = Integer.toString(n);

    // If k is greater than length of the
    // string temp
    if (k > temp.length())
    {
        System.out.println(-1);
    }

    // Print the k digit from last
    else
    {
        int index = temp.length() - k;
        int res = temp.charAt(index) - '0';
        System.out.println(res);
    }
}

// Driver code
public static void main(String[] args)
{

    // Given Input
    int n = 2354;
    int k = 2;

    // Function call
    kthDigitFromLast(n, k);
}
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the kth digit
# from last in an integer n
def kthDigitFromLast(n, k):

    # If k is less than equal to 0
    if (k <= 0):
        print(-1)
        return

    # Convert integer into string
    temp = str(n)

    # If k is greater than length of the
    # temp
    if (k > len(temp)):
        print(-1)

    # Print the k digit from last
    else:
        print(ord(temp[len(temp) - k]) - ord('0'))

# Driver code
if __name__ == '__main__':

    # Given Input
    n = 2354
    k = 2

    # Function call
    kthDigitFromLast(n, k)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the kth digit
// from last in an integer n
static void kthDigitFromLast(int n, int k)
{

    // If k is less than equal to 0
    if (k <= 0)
    {
        Console.Write(-1);
        return;
    }

    // Convert integer into string
    string temp = n.ToString();

    // If k is greater than length of the
    // string temp
    if (k > temp.Length)
    {
        Console.WriteLine(-1);
    }

    // Print the k digit from last
    else
    {
        Console.Write(temp[temp.Length - k] - 48);
    }
}

// Driver code
public static void Main()
{

    // Given Input
    int n = 2354;
    int k = 2;

    // Function call
    kthDigitFromLast(n, k);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the kth digit
// from last in an integer n
function kthDigitFromLast(n, k)
{

    // If k is less than equal to 0
    if (k <= 0)
    {
        document.write(-1);
        return;
    }

    // Convert integer into string
    var temp = String(n);

    // If k is greater than length of the
    // string temp
    if (k > temp.length)
    {
        document.write(-1);
    }

    // Print the k digit from last
    else
    {
        var req = temp.charAt(temp.length - k)

        // Convert to number again
        document.write(Number(req));
    }
}

// Driver code

// Given Input
var n = 2354;
var k = 2;

// Function call
kthDigitFromLast(n, k);

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
5
```

***时间复杂度:** O(d)，其中 d 为数字 **N** 中的位数。*
***辅助空间:** O(d)*

**高效方法**:这个问题可以通过[迭代数字 N](https://www.geeksforgeeks.org/program-count-digits-integer-3-different-methods/) 的位数来解决。按照以下步骤解决此问题:

*   如果 **K** 小于等于 **0，**则打印 **-1** 返回。
*   [迭代，同时](https://www.geeksforgeeks.org/java-while-loop-with-examples/) **N** 和 **K-1** 大于 **0** :
    *   将 **N** 更新为 **N/10** ，将 **K** 递减 **1** 。
*   如果 **N** 为 **0** ，则打印 **-1** ，否则打印 **N%10** 。

下面是上述方法的实现:

## C++

```
// c++ program for the above approach
#include <bits/stdc++.h>

using namespace std;

// Function to find the kth digit
// from last in an integer n
void kthDigitFromLast(int n, int k)
{
    // If k is less than equal to 0
    if (k <= 0) {
        cout << -1 << endl;
        return;
    }

    // Divide the number n by 10
    // upto k-1 times
    while ((k - 1) > 0 && n > 0) {
        n = n / 10;
        k--;
    }

    // If the number n is equal 0
    if (n == 0) {
        cout << -1 << endl;
    }
    // Print the right most digit
    else {
        cout << n % 10 << endl;
    }
}

// Driver code
int main()
{
    // Given Input
    int n = 2354;
    int k = 2;

    // Function call
    kthDigitFromLast(n, k);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find the kth digit
// from last in an integer n
public static void kthDigitFromLast(int n, int k)
{

    // If k is less than equal to 0
    if (k <= 0)
    {
        System.out.println(-1);
        return;
    }

    // Divide the number n by 10
    // upto k-1 times
    while ((k - 1) > 0 && n > 0)
    {
        n = n / 10;
        k--;
    }

    // If the number n is equal 0
    if (n == 0)
    {
        System.out.println(-1);
    }

    // Print the right most digit
    else
    {
        System.out.println(n % 10);
    }
}

// Driver code
public static void main(String[] args)
{
    int n = 2354;
    int k = 2;

    // Function call
    kthDigitFromLast(n, k);
}
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python program for the above approach
# Function to find the kth digit
# from last in an eger n
def kthDigitFromLast( n,  k):

    # If k is less than equal to 0
    if (k <= 0):
        print("-1")
        return

    # Divide the number n by 10
    # upto k-1 times
    while ((k - 1) > 0 and n > 0):
        n = n / 10
        k -= 1

    # If the number n is equal 0
    if (n == 0):
        print("-1")

    # Pr the right most digit
    else:
        print(int(n % 10 ))

# Driver code
if __name__ == '__main__':

    # Given Input
    n = 2354
    k = 2

    # Function call
    kthDigitFromLast(n, k)

# this code is contributed by shivanisinghss2110
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

// Function to find the kth digit
// from last in an integer n
public static void kthDigitFromLast(int n, int k)
{

    // If k is less than equal to 0
    if (k <= 0)
    {
        Console.Write(-1);
        return;
    }

    // Divide the number n by 10
    // upto k-1 times
    while ((k - 1) > 0 && n > 0)
    {
        n = n / 10;
        k--;
    }

    // If the number n is equal 0
    if (n == 0)
    {
        Console.Write(-1);
    }

    // Print the right most digit
    else
    {
        Console.Write(n % 10);
    }
}

// Driver code
public static void Main(String[] args)
{
    int n = 2354;
    int k = 2;

    // Function call
    kthDigitFromLast(n, k);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the kth digit
// from last in an integer n
function kthDigitFromLast(n, k)
{

    // If k is less than equal to 0
    if (k <= 0)
    {
        document.write(-1);
        return;
    }

    // Divide the number n by 10
    // upto k-1 times
    while ((k - 1) > 0 && n > 0)
    {
        n = n / 10;
        k--;
    }

    // If the number n is equal 0
    if (n == 0)
    {
        document.write(-1);
    }

    // Print the right most digit
    else
    {
        document.write(parseInt(n % 10));
    }
}

// Driver code

// Given Input
var n = 2354;
var k = 2;

// Function call
kthDigitFromLast(n, k);

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
5
```

***时间复杂度:** O(d)，其中 d 为数字 **N** 中的位数。*
***辅助空间:** O(1)*

**高效途径:**这个问题可以使用[幂函数](https://www.geeksforgeeks.org/power-function-cc/)解决。按照以下步骤解决此问题:

*   如果 **K** 小于等于 **0，**则打印 **-1** 返回。
*   初始化一个变量，比如说**除数**为[幂](https://www.geeksforgeeks.org/power-function-cc/) (10，K-1)。
*   如果**除数**大于 **N，**则打印 **-1，**否则打印**(N/除数)%10。**

下面是上述方法的实现:

## C++

```
// c++ program for the above approach
#include <bits/stdc++.h>

using namespace std;

// Function to find the kth digit
// from last in an integer n
void kthDigitFromLast(int n, int k)
{
    // If k is less than equal to 0
    if (k <= 0) {
        cout << -1 << endl;
        return;
    }

    // Calculate kth digit using power function
    int diviser = (int)pow(10, k - 1);

    // If diviser is greater than n
    if (diviser > n) {
        cout << -1 << endl;
    }
    // Otherwise print kth digit from last
    else {
        cout << (n / diviser) % 10 << endl;
    }
}

// Driver code
int main()
{
    // Given Input
    int n = 2354;
    int k = 2;

    // Function call
    kthDigitFromLast(n, k);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find the kth digit
// from last in an integer n
public static void kthDigitFromLast(int n, int k)
{

    // If k is less than equal to 0
    if (k <= 0)
    {
        System.out.println(-1);
        return;
    }

    // Calculate kth digit using power function
    int diviser = (int)Math.pow(10, k - 1);

    // If diviser is greater than n
    if (diviser > n)
    {
        System.out.println(-1);
    }

    // Otherwise print kth digit from last
    else
    {
        System.out.println((n / diviser) % 10);
    }
}

// Driver code
public static void main(String[] args)
{
    int n = 2354;
    int k = 2;

    // Function call
    kthDigitFromLast(n, k);
}
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the kth digit
# from last in an integer n
def kthDigitFromLast(n, k):

    # If k is less than equal to 0
    if (k <= 0):
        print("-1")
        return

    # Calculate kth digit using power function
    diviser = int(pow(10, k - 1))

    # If diviser is greater than n
    if (diviser > n):
        print("-1")

    # Otherwise print kth digit from last
    else:
        print(int((n / diviser) % 10))

# Given Input
n = 2354;
k = 2;

# Function call
kthDigitFromLast(n, k);

# This code is contributed by SoumikMondal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the kth digit
// from last in an integer n
public static void kthDigitFromLast(int n, int k)
{

    // If k is less than equal to 0
    if (k <= 0)
    {
        Console.Write(-1);
        return;
    }

    // Calculate kth digit using power function
    int diviser = (int)Math.Pow(10, k - 1);

    // If diviser is greater than n
    if (diviser > n)
    {
        Console.Write(-1);
    }

    // Otherwise print kth digit from last
    else
    {
        Console.Write((n / diviser) % 10);
    }
}

// Driver code
public static void Main(String[] args)
{
    int n = 2354;
    int k = 2;

    // Function call
    kthDigitFromLast(n, k);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// JavaScript program for the above approach
function kthDigitFromLast(n, k)
{

    // If k is less than equal to 0
    if (k <= 0)
    {
        document.write(-1);
        return;
    }

    // Calculate kth digit using power function
    var diviser = parseInt(Math.pow(10, k - 1));

    // If diviser is greater than n
    if (diviser > n)
    {
        document.write(-1);
    }

    // Otherwise print kth digit from last
    else
    {
        document.write(parseInt((n / diviser) % 10));
    }
}

// Driver code

// Given Input
var n = 2354;
var k = 2;

// Function call
kthDigitFromLast(n, k);

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
5
```

***时间复杂度:** O(log(K))，其中 d 为数字 **N** 中的位数。这个时间复杂度是由于**使用幂函数计算 10 的幂。*
***辅助空间:** O(1)*