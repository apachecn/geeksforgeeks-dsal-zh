# 最右边设定位的位置

> 原文:[https://www . geeksforgeeks . org/最右置位位置/](https://www.geeksforgeeks.org/position-of-rightmost-set-bit/)

编写一个单行函数，以整数的二进制表示形式，从右向左返回第一个 1 的位置。

```
I/P    18,   Binary Representation 010010
O/P   2
I/P    19,   Binary Representation 010011
O/P   1
```

**算法:**(例 12(1100))
设 I/P 为 12 (1100)
1。取给定否的二进制补码，因为所有位都被还原
除了从右到左的第一个“1”【0100】
2 用原来的否做一点点&，这将返回否，而
只需要一个(0100)
3 取否的对数 2，你将得到(位置–1)(2)
4 加 1 (3)

**解释–**

**(n & ~(n-1))** 始终返回包含最右边设置位的二进制数为 1。

**如果 N = 12 (1100)，那么它将返回 4 (100)**

在这里，log2 将返回，我们可以用 2 的幂表示的次数。

对于所有包含**的二进制数，只有**最右边的位设置为 1，如 2，4，8，16，32……。

我们会发现最右边设置位的位置总是等于 log2(数字)+1

**程序:**

## C++

```
// C++ program for Position
// of rightmost set bit
#include <iostream>
#include <math.h>
using namespace std;

class gfg
{

public:
unsigned int getFirstSetBitPos(int n)
{
    return log2(n & -n) + 1;
}
};

// Driver code
int main()
{
    gfg g;
    int n = 12;
    cout << g.getFirstSetBitPos(n);
    return 0;
}

// This code is contributed by SoM15242
```

## C

```
// C program for Position
// of rightmost set bit
#include <math.h>
#include <stdio.h>

unsigned int getFirstSetBitPos(int n)
{
    return log2(n & -n) + 1;
}

// Driver code
int main()
{
    int n = 12;
    printf("%u", getFirstSetBitPos(n));
    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Code for Position of rightmost set bit
class GFG {

    public static int getFirstSetBitPos(int n)
    {
        return (int)((Math.log10(n & -n)) / Math.log10(2)) + 1;
    }

    // Drive code
    public static void main(String[] args)
    {
        int n = 12;
        System.out.println(getFirstSetBitPos(n));
    }
}
// This code is contributed by Arnav Kr. Mandal
```

## 蟒蛇 3

```
# Python Code for Position
# of rightmost set bit

import math

def getFirstSetBitPos(n):

     return math.log2(n&-n)+1

# driver code

n = 12
print(int(getFirstSetBitPos(n)))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# Code for Position of rightmost set bit
using System;

class GFG {
    public static int getFirstSetBitPos(int n)
    {
        return (int)((Math.Log10(n & -n))
                / Math.Log10(2)) + 1;
    }

    // Driver method
    public static void Main()
    {
        int n = 12;
        Console.WriteLine(getFirstSetBitPos(n));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Code for Position of
// rightmost set bit

function getFirstSetBitPos($n)
{
    return ceil(log(($n& -
                     $n) + 1, 2));
}

// Driver Code
$n = 12;
echo getFirstSetBitPos($n);

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>
// JavaScript program for Position
// of rightmost set bit

function getFirstSetBitPos(n)
{
    return Math.log2(n & -n) + 1;
}

// Driver code
    let g;
    let n = 12;
    document.write(getFirstSetBitPos(n));

// This code is contributed by Manoj.
</script>
```

**Output**

```
3
```

***时间复杂度:** O(log <sub>2</sub> n)*

**使用 ffs()函数:** ffs()函数返回第一个最低有效集位的索引。索引从 1 开始于 ffs()函数。
例如:
n = 12 = 1100

在上面的例子中，ffs(n)返回最右边的设置位索引，即 3。

## C++

```
// C++ program to find the
// position of first rightmost
// set bit in a given number.
#include <bits/stdc++.h>
using namespace std;

// Function to find rightmost
// set bit in given number.
int getFirstSetBitPos(int n)
{
    return ffs(n);
}

// Driver function
int main()
{
    int n = 12;
    cout << getFirstSetBitPos(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program program to find the
// position of first rightmost
// set bit in a given number
import java.util.*;

class GFG{

// Function to find rightmost
// set bit in given number.
static int getFirstSetBitPos(int n)
{
    return (int)((Math.log10(n & -n)) / Math.log10(2)) + 1;
}

// Driver code
public static void main(String[] args)
{
    int n = 12;
    System.out.print( getFirstSetBitPos(n));

}
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python3 program to find the
# position of first rightmost
# set bit in a given number
import math

# Function to find rightmost
# set bit in given number.
def getFirstSetBitPos(n):

    return int(math.log2 (n & -n) + 1)

# Driver Code
if __name__ == '__main__':

    n = 12
    print(getFirstSetBitPos(n))

# This code is contributed by nirajgusain5.
```

## C#

```
// C# program program to find the
// position of first rightmost
// set bit in a given number
using System;
public class GFG{

// Function to find rightmost
// set bit in given number.
static int getFirstSetBitPos(int n)
{
    return (int)((Math.Log10(n & -n)) / Math.Log10(2)) + 1;
}

// Driver code
public static void Main(String[] args)
{
    int n = 12;
    Console.Write( getFirstSetBitPos(n));

}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find the
// position of first rightmost
// set bit in a given number

// Function to find rightmost
// set bit in given number.
function getFirstSetBitPos(n)
{
    return Math.log2(n & -n) + 1;
}

// Driver Code

    let n = 12;
    document.write( getFirstSetBitPos(n));

</script>
```

**Output**

```
3
```

**使用异或和&运算符:**
将 m 初始化为 1，并从最右边的位开始检查其异或。将 m 左移 1，直到我们找到第一个设置位，因为当我们用 m 执行&运算时，第一个设置位给出一个数字。

## C++

```
// C++ program to find the first
// rightmost set bit using XOR operator
#include <bits/stdc++.h>
using namespace std;

// function to find the rightmost set bit
int PositionRightmostSetbit(int n)
{
    // Position variable initialize with 1
    // m variable is used to check the set bit
    int position = 1;
    int m = 1;

    while (!(n & m)) {

        // left shift
        m = m << 1;
        position++;
    }
    return position;
}
// Driver Code
int main()
{
    int n = 16;
    // function call
    cout << PositionRightmostSetbit(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// first rightmost set bit
// using XOR operator

class GFG {

    // function to find
    // the rightmost set bit
    static int PositionRightmostSetbit(int n)
    {
        // Position variable initialize
        // with 1 m variable is used to
        // check the set bit
        int position = 1;
        int m = 1;

        while ((n & m) == 0) {

            // left shift
            m = m << 1;
            position++;
        }
        return position;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 16;

        // function call
        System.out.println(PositionRightmostSetbit(n));
    }
}

// This code is contributed
// by Smitha
```

## 蟒蛇 3

```
# Python3 program to find
# the first rightmost set
# bit using XOR operator

# function to find the
# rightmost set bit
def PositionRightmostSetbit(n):

    # Position variable initialize
    # with 1 m variable is used
    # to check the set bit
    position = 1
    m = 1

    while (not(n & m)) :

        # left shift
        m = m << 1
        position += 1

    return position

# Driver Code
n = 16

# function call
print(PositionRightmostSetbit(n))

# This code is contributed
# by Smitha
```

## C#

```
// C# program to find the
// first rightmost set bit
// using XOR operator
using System;

class GFG {

    // function to find
    // the rightmost set bit
    static int PositionRightmostSetbit(int n)
    {
        // Position variable initialize
        // with 1 m variable is used to
        // check the set bit
        int position = 1;
        int m = 1;

        while ((n & m) == 0) {

            // left shift
            m = m << 1;
            position++;
        }
        return position;
    }

    // Driver Code
    static public void Main()
    {
        int n = 16;

        // function call
        Console.WriteLine(
            PositionRightmostSetbit(n));
    }
}

// This code is contributed
// by @ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// first rightmost set bit
// using XOR operator

// function to find the
// rightmost set bit
function PositionRightmostSetbit($n)
{
    // Position variable initialize
    // with 1 m variable is used to
    // check the set bit
    $position = 1;
    $m = 1;

    while (!($n & $m))
    {

        // left shift
        $m = $m << 1;
        $position++;
    }
    return $position;
}

// Driver Code
$n = 16;

// function call
echo PositionRightmostSetbit($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

    // Javascript program to find the first
    // rightmost set bit using XOR operator

    // function to find the rightmost set bit
    function PositionRightmostSetbit(n)
    {

        // Position variable initialize with 1
        // m variable is used to check the set bit
        let position = 1;
        let m = 1;

        while ((n & m) == 0) {

            // left shift
            m = m << 1;
            position++;
        }
        return position;
    }

    let n = 16;

    // function call
    document.write(PositionRightmostSetbit(n));

    // This code is contributed by divyesh072019.
</script>
```

**Output**

```
5
```

穆巴拉克·艾哈迈德促成了这一做法

**使用左移位(< < ) :** 用 1 初始化 pos，向上迭代到 INT_SIZE(此处为 32)并检查是否设置了位，如果设置了位则中断循环，否则递增 pos。

## C++

```
// C++ implementation of above approach
#include <iostream>
using namespace std;
#define INT_SIZE 32

int Right_most_setbit(int num)
{
  if(num==0)// for num==0 there is zero set bit
  {  return 0;
  }
  else
  {
    int pos = 1;
    // counting the position of first set bit
    for (int i = 0; i < INT_SIZE; i++) {
        if (!(num & (1 << i)))
            pos++;
        else
            break;
    }
    return pos;
}
}
int main()
{
    int num = 0;
    int pos = Right_most_setbit(num);
    cout << pos << endl;
    return 0;
}
// This approach has been contributed by @yashasvi7
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation of above approach
public class GFG {

    static int INT_SIZE = 32;

    static int Right_most_setbit(int num)
    {
        int pos = 1;
        // counting the position of first set bit
        for (int i = 0; i < INT_SIZE; i++) {
            if ((num & (1 << i))== 0)
                pos++;

            else
                break;
        }
        return pos;
    }

    //Driver code
    public static void main(String[] args) {

         int num = 18;
            int pos = Right_most_setbit(num);
            System.out.println(pos);
    }
}  
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

INT_SIZE = 32

def Right_most_setbit(num) :

    pos = 1

    # counting the position of first set bit
    for i in range(INT_SIZE) :
        if not(num & (1 << i)) :
            pos += 1
        else :
            break

    return pos

if __name__ == "__main__" :

    num = 18
    pos = Right_most_setbit(num)
    print(pos)

# This code is contributed by ANKITRAI1
```

## C#

```
// C# implementation of above approach
using System;

class GFG {

    static int INT_SIZE = 32;

    static int Right_most_setbit(int num)
    {
        int pos = 1;

        // counting the position
        // of first set bit
        for (int i = 0; i < INT_SIZE; i++)
        {
            if ((num & (1 << i))== 0)
                pos++;

            else
                break;
        }
        return pos;
    }

    // Driver code
    static public void Main ()
    {
        int num = 18;
        int pos = Right_most_setbit(num);
        Console.WriteLine(pos);
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

function Right_most_setbit($num)
{
    $pos = 1;
    $INT_SIZE = 32;

    // counting the position
    // of first set bit
    for ($i = 0; $i < $INT_SIZE; $i++)
    {
        if (!($num & (1 << $i)))
            $pos++;
        else
            break;
    }
    return $pos;
}

// Driver code
$num = 18;
$pos = Right_most_setbit($num);
echo $pos;
echo ("\n")

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach
let INT_SIZE = 32;

function Right_most_setbit(num)
{
    let pos = 1;

    // Counting the position of first set bit
    for(let i = 0; i < INT_SIZE; i++)
    {
        if ((num & (1 << i)) == 0)
            pos++;
        else
            break;
    }
    return pos;
}

// Driver code
let num = 18;
let pos = Right_most_setbit(num);

document.write(pos);

// This code is contributed by mukesh07

</script>
```

**输出:**

```
 2
```

**使用右移的另一种方法(> > )** :

初始化 pos=1。迭代直到数字> 0，在每一步检查最后一位是否被设置。如果最后一位被置位，返回当前位置，否则将 pos 增加 1，右移 n 增加 1。

## C++

```
// C++ program for above approach
#include<bits/stdc++.h>
using namespace std;

// Program to find position of
// rightmost set bit
int PositionRightmostSetbit(int n)
{
  int p=1;

  // Iterate till number>0
  while(n > 0)
  {

    // Checking if last bit is set
    if(n&1){
      return p;
    }

    // Increment position and right shift number
    p++;
    n=n>>1;
  }

  // set bit not found.
  return -1;
}

// Driver Code
int main()
{
  int n=18;

  // Function call
  int pos=Last_set_bit(n);

  if(pos!=-1)
    cout<<pos;
  else
    cout<<0;

  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.io.*;

class GFG{

// Function to find position of
// rightmost set bit
public static int Last_set_bit(int n)
{
    int p = 1;

    // Iterate till number>0
    while (n > 0)
    {

        // Checking if last bit is set
        if ((n & 1) > 0)
        {
            return p;
        }

        // Increment position and
        // right shift number
        p++;
        n = n >> 1;
    }

    // set bit not found.
    return -1;
}

// Driver Code
public static void main(String[] args)
{
    int n = 18;

    // Function call
    int pos = Last_set_bit(n);

    if (pos != -1)
        System.out.println(pos);
    else
        System.out.println("0");
}
}

// This code is contributed by RohitOberoi
```

## 蟒蛇 3

```
# Python program for above approach

# Program to find position of
# rightmost set bit
def PositionRightmostSetbit( n):
  p = 1

  # Iterate till number>0
  while(n > 0):

    # Checking if last bit is set
    if(n&1):
      return p

    # Increment position and right shift number
    p += 1
    n = n>>1

  # set bit not found.
  return -1;

# Driver Code
n = 18
# Function call
pos = PositionRightmostSetbit(n)
if(pos != -1):
  print(pos)
else:
  print(0)

# This code is contributed by rohitsingh07052.
```

## C#

```
// C# program for above approach
using System;

class GFG{

// Function to find position of
// rightmost set bit
public static int Last_set_bit(int n)
{
    int p = 1;

    // Iterate till number>0
    while (n > 0)
    {

        // Checking if last bit is set
        if ((n & 1) > 0)
        {
            return p;
        }

        // Increment position and
        // right shift number
        p++;
        n = n >> 1;
    }

    // Set bit not found.
    return -1;
}

// Driver Code
public static void Main(string[] args)
{
    int n = 18;

    // Function call
    int pos = Last_set_bit(n);

    if (pos != -1)
        Console.WriteLine(pos);
    else
        Console.WriteLine("0");
}
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// Javascript program for above approach

// Program to find position of
// rightmost set bit
function Last_set_bit(n)
{
    let p = 1;

    // Iterate till number>0
    while (n > 0)
    {

        // Checking if last bit is set
        if ((n & 1) > 0)
        {
            return p;
        }

        // Increment position and
        // right shift number
        p++;
        n = n >> 1;
    }

    // Set bit not found.
    return -1;
}

// Driver code
let n = 18;

// Function call
let pos = Last_set_bit(n);

if (pos != -1)
{
    document.write(pos);
}
else
{
    document.write(0);
}

// This code is contributed by divyeshrabadiya07

</script>
```

**Output**

```
2
```