# 打印给定数字所有数字的 ASCII 值的程序

> 原文:[https://www . geesforgeks . org/program-to-print-ascii-给定数字的所有数字的值/](https://www.geeksforgeeks.org/program-to-print-ascii-value-of-all-digits-of-a-given-number/)

给定一个整数 **N** ，任务是打印 **N** 所有数字的 ASCII 值。

**示例:**

> **输入:** N = 8
> **输出:** 8 (56)
> **解释:**
> ASCII 值 8 为 56
> 
> **输入:** N = 240
> **输出:**
> 2 (50)
> 4 (52)
> 0 (48)

**方式:**使用如下所示的 ASCII 表，可以打印 **N** 所有数字的 ASCII 值:

<figure class="table">

| 手指 | ASCII 值 |
| Zero | Forty-eight |
| one | forty-nine |
| Two | Fifty |
| three | Fifty-one |
| four | fifty-two |
| five | Fifty-three |
| six | Fifty-four |
| seven | Fifty-five |
| eight | Fifty-six |
| nine | Fifty-seven |

可以观察到数字**【0–9】**的 ASCII 值范围为**【48–57】**。因此，为了打印任何数字的 ASCII 值，需要在数字上加上 48。

下面是上述方法的实现:

## C++

```
// C++ program to convert the digits
// of a number to its ASCII values
#include <iostream>
using namespace std;

// Function to convert digits of
// N to respective ASCII values
int convertToASCII(int N)
{
    while (N > 0) {
        int d = N % 10;
        cout << d << " ("
             << d + 48 << ")\n";

        N = N / 10;
    }
}

// Driver Code
int main()
{
    int N = 36;
    convertToASCII(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program convert the digits
// of a number to its ASCII values
import java.io.*;
class GFG {

    // Function to convert digits of
    // N to respective ASCII values
    static void convertToASCII(int N)
    {
        while (N > 0) {
            int d = N % 10;
            System.out.println(d + " ("
                               + (d + 48) + ")");

            N = N / 10;
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 36;
        convertToASCII(N);
    }
}
```

## 蟒蛇 3

```
# Python3 program to convert the digits
# of a number to its ASCII values

# Function to convert digits of
# N to respective ASCII values
def convertToASCII(N):
    while (N > 0):
        d = N % 10
        print(d, "(" + str(d + 48) + ")")
        N = N // 10

# Driver Code
if __name__ == '__main__':
    N = 36
    convertToASCII(N)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program convert the digits
// of a number to its ASCII values
using System;
public class GFG {

  // Function to convert digits of
  // N to respective ASCII values
  static void convertToASCII(int N)
  {
    while (N > 0) {
      int d = N % 10;
      Console.WriteLine(d + " ("
                        + (d + 48) + ")");

      N = N / 10;
    }
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int N = 36;
    convertToASCII(N);
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program to convert the digits
// of a number to its ASCII values

// Function to convert digits of
// N to respective ASCII values
function convertToASCII(N)
{
    while (N > 0) {
        var d = N % 10;
        document.write( d + " ("
             + (d + 48) + ")<br>");

        N = parseInt(N / 10);
    }
}

// Driver Code
var N = 36;
convertToASCII(N);

</script>
```

**Output:** 

```
6 (54)
3 (51)
```

***时间复杂度:**O(log<sub>10</sub>N)*
***辅助空间:** O(1)*

**交替进场:**思路是使用[式转换](https://www.geeksforgeeks.org/type-conversion-in-c/)。[将整数转换为等效字符串](https://www.geeksforgeeks.org/converting-string-to-number-and-vice-versa-in-c/)并打印字符串每个字符的 ASCII 值。

下面是上述方法的实现:

## C++

```
// C++ program to convert the digits
// of a number to its ASCII values
#include <bits/stdc++.h>
using namespace std;

// Function to convert digits of
// N to respective ASCII values
int convertToASCII(int N)
{
    string num = to_string(N);
    for (char ch : num) {
        cout << ch << " ("
             << (int)ch << ")\n";
    }
}

// Driver Code
int main()
{
    int N = 36;
    convertToASCII(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert the digits
// of a number to its ASCII values
import java.util.*;
class GFG{

// Function to convert digits of
// N to respective ASCII values
static void convertToASCII(int N)
{
    String num = Integer.toString(N);
    for (char ch : num.toCharArray()) {
        System.out.print(ch + " ("
            + (int)ch + ")\n");
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 36;
    convertToASCII(N);
}
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python3 program to convert the digits
# of a number to its ASCII values

# Function to convert digits of
# N to respective ASCII values
def convertToASCII(N):

    num = str(N)
    i = 0

    for ch in num:
        print(ch, "(", ord(ch), ")")

# Driver Code
N = 36

convertToASCII(N)

# This code is contributed by Dharanendra L V.
```

## C#

```
// C# program to convert the digits
// of a number to its ASCII values
using System;

public class GFG{

// Function to convert digits of
// N to respective ASCII values
static void convertToASCII(int N)
{
    String num = N.ToString();
    foreach (char ch in num.ToCharArray()) {
        Console.Write(ch + " ("
            + (int)ch + ")\n");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int N = 36;
    convertToASCII(N);
}
}

// This code contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript program to convert the digits
// of a number to its ASCII values

// Function to convert digits of
// N to respective ASCII values
function convertToASCII(N)
{
     let num = N.toString();
    for (let ch = 0; ch < num.length; ch++)
    {
        document.write(num[ch] + " ("
            + num[ch].charCodeAt(0) + ")<br>");
    }
}

// Driver Code
let N = 36;
convertToASCII(N);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
3 (51)
6 (54)
```

***时间复杂度:**O(log<sub>10</sub>N)*
***辅助空间:**O(log<sub>10</sub>N)*

</figure>