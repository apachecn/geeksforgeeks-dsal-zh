# 给定数字的二进制表示

> 原文:[https://www . geesforgeks . org/给定数字的二进制表示/](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)

编写一个程序来打印给定数字的二进制表示。

来源:[微软面试集-3](https://www.geeksforgeeks.org/microsoft-interview-set-3/)

**方法 1:迭代**
对于任意一个数，我们可以通过与“2^i”(2 提升到 I)按位 and 运算来检查它的第 I 位是 0(OFF)还是 1(ON)。

```
1) Let us take number 'NUM' and we want to check whether it's 0th bit is ON or OFF    
    bit = 2 ^ 0 (0th bit)
    if  NUM & bit >= 1 means 0th bit is ON else 0th bit is OFF

2) Similarly if we want to check whether 5th bit is ON or OFF    
    bit = 2 ^ 5 (5th bit)
    if NUM & bit >= 1 means its 5th bit is ON else 5th bit is OFF.
```

让我们取无符号整数(32 位)，它由 0-31 位组成。要打印无符号整数的二进制表示，从第 31 位开始，检查第 31 位是开还是关，如果是开，打印“1”，否则打印“0”。现在检查第 30 位是开还是关，如果是开打印“1”，否则打印“0”，对从 31 到 0 的所有位都这样做，最后我们将得到数字的二进制表示。

## C++

```
// C++ Program for the binary
// representation of a given number
#include <bits/stdc++.h>
using namespace std;

  void bin(long n)
  {
    long i;
    cout << "0";
    for (i = 1 << 30; i > 0; i = i / 2)
    {
      if((n & i) != 0)
      {
        cout << "1";
      }
      else
      {
        cout << "0";
      }
    }
  }

// Driver Code
int main(void)
{
    bin(7);
    cout << endl;
    bin(4);
}

// This code is contributed by souravghosh0416
```

## C

```
#include<stdio.h>
void bin(unsigned n)
{
    unsigned i;
    for (i = 1 << 31; i > 0; i = i / 2)
        (n & i) ? printf("1") : printf("0");
}

int main(void)
{
    bin(7);
    printf("\n");
    bin(4);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
public class GFG
{
  static void bin(long n)
  {
    long i;
    System.out.print("0");
    for (i = 1 << 30; i > 0; i = i / 2)
    {
      if((n & i) != 0)
      {
        System.out.print("1");
      }
      else
      {
        System.out.print("0");
      }
    }
  }

  // Driver code
  public static void main(String[] args)
  {
    bin(7);
    System.out.println();
    bin(4);
  }
}

// This code is contributed by divyesh072019.
```

## 蟒蛇 3

```
def bin(n) :

    i = 1 << 31
    while(i > 0) :

        if((n & i) != 0) :

            print("1", end = "")

        else :
            print("0", end = "")

        i = i // 2

bin(7)
print()
bin(4)

# This code is contributed by divyeshrabadiya07.
```

## C#

```
using System;

public class GFG{
    static void bin(long n)
    {
        long i;
        Console.Write("0");
        for (i = 1 << 30; i > 0; i = i / 2)
        {
            if((n & i) != 0)
            {
                Console.Write("1");
            }
            else
            {
                Console.Write("0");
            }
        }
    }
    // Driver code
    static public void Main (){
        bin(7);
        Console.WriteLine();
        bin(4);
    }
}
// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>
// JavaScript Program for the binary
// representation of a given number
    function bin(n)
    {
        let i;
        document.write("0");
        for (i = 1 << 30; i > 0; i = Math.floor(i/2))
        {
            if((n & i) != 0)
            {
                document.write("1");
            }
            else
            {
                document.write("0");
            }
        }
    }

    bin(7);
    document.write("<br>");
    bin(4);

    // This code is contributed by rag2127

</script>
```

**Output**

```
00000000000000000000000000000111
00000000000000000000000000000100
```

**方法二:递归**
下面是递归方法打印‘NUM’的二进制表示。

```
step 1) if NUM > 1
    a) push NUM on stack
    b) recursively call function with 'NUM / 2'
step 2)
    a) pop NUM from stack, divide it by 2 and print it's remainder.
```

## C++

```
// C++ Program for the binary
// representation of a given number
#include <bits/stdc++.h>
using namespace std;

void bin(unsigned n)
{
    /* step 1 */
    if (n > 1)
        bin(n / 2);

    /* step 2 */
    cout << n % 2;
}

// Driver Code
int main(void)
{
    bin(7);
    cout << endl;
    bin(4);
}

// This code is contributed
// by Akanksha Rai
```

## C

```
// C Program for the binary
// representation of a given number
void bin(unsigned n)
{
    /* step 1 */
    if (n > 1)
        bin(n / 2);

    /* step 2 */
    printf("%d", n % 2);
}

// Driver Code
int main(void)
{
    bin(7);
    printf("\n");
    bin(4);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the binary
// representation of a given number
class GFG {
    static void bin(int n)
    {
        /* step 1 */
        if (n > 1)
            bin(n / 2);

        /* step 2 */
        System.out.print(n % 2);
    }

    // Driver code
    public static void main(String[] args)
    {
        bin(7);
        System.out.println();
        bin(4);
    }
}

// This code is contributed
// by ChitraNayal
```

## 蟒蛇 3

```
# Python3 Program for the binary
# representation of a given number

def bin(n):

    if n > 1:
        bin(n//2)

    print(n % 2, end="")

# Driver Code
if __name__ == "__main__":

    bin(7)
    print()
    bin(4)

# This code is contributed by ANKITRAI1
```

## C#

```
// C# Program for the binary
// representation of a given number
using System;

class GFG {

    static void bin(int n)
    {

        // step 1
        if (n > 1)
            bin(n / 2);

        // step 2
        Console.Write(n % 2);
    }

    // Driver code
    static public void Main()
    {
        bin(7);
        Console.WriteLine();
        bin(4);
    }
}

// This code is contributed ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program for the binary
// representation of a given number
function bin($n)
{
    /* step 1 */
    if ($n > 1)
        bin($n/2);

    /* step 2 */
    echo ($n % 2);
}

// Driver code
bin(7);
echo ("\n");
bin(4);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript program for the binary
// representation of a given number
function bin(n)
{

    // Step 1
    if (n > 1)
        bin(parseInt(n / 2, 10));

    // Step 2
    document.write(n % 2);
}

// Driver code
bin(7);
document.write("</br>");
bin(4);

// This code is contributed by divyeshrabadiya07

</script>
```

**Output**

```
111
100
```

**方法 3:递归使用按位运算符**
将十进制数转换为其二进制表示的步骤如下:

```
step 1: Check n > 0
step 2: Right shift the number by 1 bit and recursive function call
step 3: Print the bits of number
```

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to convert decimal
// to binary number
void bin(unsigned n)
{
    if (n > 1)
        bin(n >> 1);

    printf("%d", n & 1);
}

// Driver code
int main(void)
{
    bin(131);
    printf("\n");
    bin(3);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG {

    // Function to convert decimal
    // to binary number
    static void bin(Integer n)
    {
        if (n > 1)
            bin(n >> 1);

        System.out.printf("%d", n & 1);
    }

    // Driver code
    public static void main(String[] args)
    {
        bin(131);
        System.out.printf("\n");
        bin(3);
    }
}
/*This code is contributed by PrinciRaj1992*/
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# Function to convert decimal to
# binary number

def bin(n):

    if (n > 1):
        bin(n >> 1)
    print(n & 1, end="")

# Driver code
bin(131)
print()
bin(3)

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# implementation of above approach
using System;

public class GFG {

    // Function to convert decimal
    // to binary number
    static void bin(int n)
    {
        if (n > 1)
            bin(n >> 1);

        Console.Write(n & 1);
    }

    // Driver code
    public static void Main()
    {
        bin(131);
        Console.WriteLine();
        bin(3);
    }
}
/*This code is contributed by PrinciRaj1992*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to convert decimal
// to binary number
function bin($n)
{
    if ($n > 1)
    bin($n>>1);

    echo ($n & 1);
}

// Driver code
bin(131);
echo "\n";
bin(3);

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>
// JavaScript implementation of the approach

// Function to convert decimal
// to binary number
function bin(n)
{
    if (n > 1)
        bin(n >> 1);

    document.write(n & 1);
}

// Driver code

    bin(131);
    document.write("<br>");
    bin(3);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output**

```
10000011
11
```

**方法 4:** **使用 C++的位集**

我们可以使用 C++的*<u>位集类</u>* 来存储任意数字(正数和负数)的二进制表示。它为我们提供了灵活性，可以拥有我们想要的位数，比如我们是否想要一个 32 位的二进制表示，而不是一个 8 位的数字表示。

在这篇 gfg 文章 [**LINK**](https://www.geeksforgeeks.org/c-bitset-and-its-application/) 中可以找到完整的使用 bitset 的指南。

## C++

```
#include <bits/stdc++.h>
using namespace std;

int main()
{

    int n = 5, m = -5;
    bitset<8> b(n);
    bitset<8> b1(m);
    cout << "Binary of 5:" << b << endl;
    cout << "Binary of -5:" << b1 << endl;
    return 0;
}
```

```
Output:
Binary of 5:00000101
Binary of -5:11111011
```

**方法五:Python 内置库**

## 蟒蛇 3

```
def binary(num):
    return int(bin(num).split('0b')[1])

if __name__ == "__main__" :
    x = 10
    binary_x = binary(x)
    print(binary_x)

# This code is contributed by Rishika Gupta.
```

**Output**

```
1010
```

**视频教程**

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
本文由**纳伦德拉·康拉尔卡尔**整理。