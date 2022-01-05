# 关于比特操作

> 原文:[https://www.geeksforgeeks.org/all-about-bit-manipulation/](https://www.geeksforgeeks.org/all-about-bit-manipulation/)

[位操作](https://www.geeksforgeeks.org/bits-manipulation-important-tactics/)是一种在各种问题中使用的技术，以优化的方式获得解决方案。从[竞技编程](https://www.geeksforgeeks.org/how-to-prepare-for-competitive-programming/)的角度来看，这种技术非常有效。这都是关于[逐位运算符](https://www.geeksforgeeks.org/interesting-facts-bitwise-operators-c/)，它直接作用于[二进制数](https://www.geeksforgeeks.org/interesting-method-generate-binary-numbers-1-n/)或有助于快速实现的位数。下面是使用的**位运算符**:

*   按位“与”(&)
*   按位或(|)
*   按位异或(^)
*   按位 NOT(！)

在本文中了解更多关于按位运算符的信息。

以下是编程中经常使用的一些常见位操作:

### **<u>逐位运算</u> :**

下表说明了使用按位运算符执行操作时的结果。这里 **0s** 或 **1s** 分别表示一系列的 **0** 或 **1** 。

<figure class="table">

| 经营者 | 操作 | 结果 |
| --- | --- | --- |
| 异或 | X ^ 0s | X |
| 异或 | X ^ 1s | ~X |
| 异或 | X ^ X | Zero |
| 和 | X & 0s | Zero |
| 和 | X & 1s | X |
| 和 | X & X | X |
| 运筹学 | X &#124; 0s | X |
| 运筹学 | X &#124; 1s | 1s |
| 运筹学 | X &#124; X | X |

</figure>

### **<u>获得比特</u> :**

该方法用于查找给定编号 **N** 的特定位置(比如 **i** )的位。其思想是找到给定数的[位“与”](https://www.geeksforgeeks.org/bitwise-and-or-of-a-range/)和 **2 <sup>i</sup>** 可以表示为 **(1 < < i)** 。如果返回值为 **1** ，则设置 **i <sup>th</sup> 位置**的位。否则，它是未设置的。

下面是相同的伪代码:

## C++

```
// Function to get the bit at the
// ith position
boolean getBit(int num, int i)
{
    // Return true if the bit is
    // set. Otherwise return false
    return ((num & (1 << i)) != 0);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Function to get the bit at the
// ith position
static boolean getBit(int num, int i)
{
    // Return true if the bit is
    // set. Otherwise return false
    return ((num & (1 << i)) != 0);
}

// This code is contributed by rishavmahato348.
```

## 蟒蛇 3

```
# Function to get the bit at the
# ith position
def getBit(num, i):

    # Return true if the bit is
    # set. Otherwise return false
    return ((num & (1 << i)) != 0)

# This code is contributed by shivani
```

## C#

```
// Function to get the bit at the
// ith position
static bool getBit(int num, int i)
{
    // Return true if the bit is
    // set. Otherwise return false
    return ((num & (1 << i)) != 0);
}

// This code is contributed by subhammahato348.
```

## java 描述语言

```
<script>

// Function to get the bit at the
// ith position
function getBit(num, i)
{

    // Return true if the bit is
    // set. Otherwise return false
    return ((num & (1 << i)) != 0);
}

// This code is contributed by Ankita saini

</script>
```

### **<u>设置位</u> :**

该方法用于在给定编号 **N** 的特定位置(比如 **i** )设置位。其思想是将给定数 **N** 的值更新为给定数 **N** 和 **2 <sup>i</sup>** 的**位 OR** ，可以表示为 **(1 < < i)** 。如果返回值为 **1** ，则设置 **i <sup>th</sup> 位置**的位。否则，它是未设置的。

下面是相同的伪代码:

## C++

```
// Function to set the ith bit of the
// given number num
int setBit(int num, int i)
{
    // Sets the ith bit and return
    // the updated value
    return num | (1 << i);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Function to set the ith bit of the
// given number num
static int setBit(int num, int i)
{
    // Sets the ith bit and return
    // the updated value
    return num | (1 << i);
}

// This code is contributed by subhammahato348
```

## 蟒蛇 3

```
# Function to set the ith bit of the
# given number num
def setBit(num, i):

    # Sets the ith bit and return
    # the updated value
    return num | (1 << i)

# This code is contributed by kirti
```

## C#

```
// Function to set the ith bit of the
// given number num
static int setBit(int num, int i)
{
    // Sets the ith bit and return
    // the updated value
    return num | (1 << i);
}
```

## java 描述语言

```
// Function to set the ith bit of the
// given number num
function setBit(num, i)
{
    // Sets the ith bit and return
    // the updated value
    return num | (1 << i);
}
```

### **<u>清零位</u> :**

该方法用于清除给定编号 **N** 的特定位置(比如 **i** )的位。其思想是将给定数 **N** 的值更新为给定数 **N** 的**位 AND** 以及 **2 <sup>i</sup>** 的[补语，可以表示为 **~(1 < < i)** 。如果返回值为 **1** ，则设置 **i <sup>th</sup> 位置**的位。否则，它是未设置的。](https://www.geeksforgeeks.org/find-ones-complement-integer/)

下面是相同的伪代码:

## C++

```
// Function to clear the ith bit of
// the given number N
int clearBit(int num, int i)
{

    // Create the mask for the ith
    // bit unset
    int mask = ~(1 << i);

    // Return the update value
    return num & mask;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Function to clear the ith bit of
// the given number N
static int clearBit(int num, int i)
{

    // Create the mask for the ith
    // bit unset
    int mask = ~(1 << i);

    // Return the update value
    return num & mask;
}

// This code is contributed by subham348
```

## 蟒蛇 3

```
# Function to clear the ith bit of
# the given number N

def clearBit(num, i):

    # Create the mask for the ith
    # bit unset
    mask = ~(1 << i)

    # Return the update value
    return num & mask

# This code is contributed by subhammahato348
```

## C#

```
// Function to clear the ith bit of
// the given number N
static int clearBit(int num, int i)
{

    // Create the mask for the ith
    // bit unset
    int mask = ~(1 << i);

    // Return the update value
    return num & mask;
}

// This code is contributed by Ankita Saini
```

## java 描述语言

```
// Function to clear the ith bit of
// the given number N
function clearBit(num, i)
{

    // Create the mask for the ith
    // bit unset
    let mask = ~(1 << i);

    // Return the update value
    return num & mask;
}

// This code is contributed by souravmahato348.
```

下面是实现上述功能的程序:

## C++

```
// C++ program to implement all the
// above functionalities

#include "bits/stdc++.h"
using namespace std;

// Function to get the bit at the
// ith position
bool getBit(int num, int i)
{
    // Return true if the ith bit is
    // set. Otherwise return false
    return ((num & (1 << i)) != 0);
}

// Function to set the ith bit of the
// given number num
int setBit(int num, int i)
{
    // Sets the ith bit and return
    // the updated value
    return num | (1 << i);
}

// Function to clear the ith bit of
// the given number N
int clearBit(int num, int i)
{

    // Create the mask for the ith
    // bit unset
    int mask = ~(1 << i);

    // Return the update value
    return num & mask;
}

// Driver Code
int main()
{
    // Given number N
    int N = 70;

    cout << "The bit at the 3rd position is: "
         << (getBit(N, 3) ? '1' : '0')
         << endl;

    cout << "The value of the given number "
         << " after setting the bit at "
         << " MSB is: "
         << setBit(N, 0) << endl;

    cout << "The value of the given number "
         << " after clearing the bit at "
         << " MSB is: "
         << clearBit(N, 0) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement all the
// above functionalities
import java.io.*;

class GFG{

// Function to get the bit at the
// ith position
static boolean getBit(int num, int i)
{

    // Return true if the ith bit is
    // set. Otherwise return false
    return ((num & (1 << i)) != 0);
}

// Function to set the ith bit of the
// given number num
static int setBit(int num, int i)
{

    // Sets the ith bit and return
    // the updated value
    return num | (1 << i);
}

// Function to clear the ith bit of
// the given number N
static int clearBit(int num, int i)
{

    // Create the mask for the ith
    // bit unset
    int mask = ~(1 << i);

    // Return the update value
    return num & mask;
}

// Driver Code
public static void main(String[] args)
{

    // Given number N
    int N = 70;

    System.out.println("The bit at the 3rd position is: " +
                       (getBit(N, 3) ? '1' : '0'));

    System.out.println("The value of the given number " +
                       " after setting the bit at " +
                       " MSB is: " + setBit(N, 0));

    System.out.println("The value of the given number " +
                       " after clearing the bit at " +
                       " MSB is: " + clearBit(N, 0));
}
}

// This code is contributed by souravmahato348
```

## 计算机编程语言

```
# Python program to implement all the
# above functionalities
# Function to get the bit at the
# ith position
def getBit( num,  i):

    # Return true if the ith bit is
    # set. Otherwise return false
    return ((num & (1 << i)) != 0)

# Function to set the ith bit of the
# given number num
def setBit( num,  i):

    # Sets the ith bit and return
    # the updated value
    return num | (1 << i)

# Function to clear the ith bit of
# the given number N
def clearBit( num,  i):

    # Create the mask for the ith
    # bit unset
    mask = ~(1 << i)

    # Return the update value
    return num & mask

# Driver Code
# Given number N
N = 70
print"The bit at the 3rd position is: " , 1 if (getBit(N, 3)) else '0'

print"The value of the given number" , "after setting the bit at ","MSB is: " , setBit(N, 0)

print"The value of the given number" , "after clearing the bit at ","MSB is: " , clearBit(N, 0)

# This code is contributed by shivanisinghss2110
```

## C#

```
// C# program to implement all the
// above functionalities
using System;

class GFG {

    // Function to get the bit at the
    // ith position
    static bool getBit(int num, int i)
    {

        // Return true if the ith bit is
        // set. Otherwise return false
        return ((num & (1 << i)) != 0);
    }

    // Function to set the ith bit of the
    // given number num
    static int setBit(int num, int i)
    {

        // Sets the ith bit and return
        // the updated value
        return num | (1 << i);
    }

    // Function to clear the ith bit of
    // the given number N
    static int clearBit(int num, int i)
    {

        // Create the mask for the ith
        // bit unset
        int mask = ~(1 << i);

        // Return the update value
        return num & mask;
    }

    // Driver Code
    public static void Main()
    {

        // Given number N
        int N = 70;

        Console.WriteLine("The bit at the 3rd position is: "
                          + (getBit(N, 3) ? '1' : '0'));

        Console.WriteLine("The value of the given number "
                          + " after setting the bit at "
                          + " MSB is: " + setBit(N, 0));

        Console.WriteLine("The value of the given number "
                          + " after clearing the bit at "
                          + " MSB is: " + clearBit(N, 0));
    }
}

// This code is contributed by rishavmahato348.
```

## java 描述语言

```
<script>

// Javascript program to implement all
// the above functionalities

// Function to get the bit at the
// ith position
function getBit(num, i)
{

    // Return true if the ith bit is
    // set. Otherwise return false
    return ((num & (1 << i)) != 0);
}

// Function to set the ith bit of the
// given number num
function setBit(num, i)
{

    // Sets the ith bit and return
    // the updated value
    return num | (1 << i);
}

// Function to clear the ith bit of
// the given number N
function clearBit(num, i)
{

    // Create the mask for the ith
    // bit unset
    let mask = ~(1 << i);

    // Return the update value
    return num & mask;
}

// Driver code

// Given number N
let N = 70;

document.write("The bit at the 3rd position is: " +
              (getBit(N, 3) ? '1' : '0') + "</br>");

document.write("The value of the given number " +
               " after setting the bit at " +
               " MSB is: " + setBit(N, 0) + "</br>");

document.write("The value of the given number " +
               " after clearing the bit at " +
               " MSB is: " + clearBit(N, 0) + "</br>");

// This code is contributed by divyeshrabadiya07

</script>
```

**Output:** 

```
The bit at the 3rd position is: 0
The value of the given number  after setting the bit at  MSB is: 71
The value of the given number  after clearing the bit at  MSB is: 70
```