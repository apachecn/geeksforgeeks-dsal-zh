# 不使用异或运算符求两个数的异或

> 原文:[https://www . geesforgeks . org/find-xor-of-two-number-of-not-xor-operator/](https://www.geeksforgeeks.org/find-xor-of-two-number-without-using-xor-operator/)

给定两个整数，在不使用 XOR 运算符的情况下，即在 C/C++中不使用^，求它们的 XOR。

**例:**

```
Input:  x = 1, y = 2
Output: 3

Input:  x = 3, y = 5
Output: 6
```

一个**简单的解决方案**是逐个遍历所有的位。对于每对位，检查两者是否相同，在输出中设置相应的位，如 0，否则设置为 1。

## c++

```
// C++ program to find XOR without using ^
#include <iostream>
using namespace std;

// Returns XOR of x and y
int myXOR(int x, int y)
{
    int res = 0; // Initialize result

    // Assuming 32-bit Integer
    for (int i = 31; i >= 0; i--)                    
    {
       // Find current bits in x and y
       bool b1 = x & (1 << i);
       bool b2 = y & (1 << i);

        // If both are 1 then 0 else xor is same as OR
        bool xoredBit = (b1 & b2) ? 0 : (b1 | b2);         

        // Update result
        res <<= 1;
        res |= xoredBit;
    }
    return res;
}

// Driver program to test above function
int main()
{
   int x = 3, y = 5;
   cout << "XOR is " << myXOR(x, y);
   return 0;
}
```

## Java

```
// Java program to find XOR without using ^
import java.io.*;

class GFG{

// Returns XOR of x and y
static int myXOR(int x, int y)
{

    // Initialize result
    int res = 0;

    // Assuming 32-bit Integer
    for(int i = 31; i >= 0; i--)                    
    {

        // Find current bits in x and y
        int b1 = ((x & (1 << i)) == 0 ) ? 0 : 1; 
        int b2 = ((y & (1 << i)) == 0 ) ? 0 : 1; 

        // If both are 1 then 0 else xor is same as OR
        int xoredBit = ((b1 & b2) != 0) ? 0 : (b1 | b2);         

        // Update result
        res <<= 1;
        res |= xoredBit;
    }
    return res;
}

// Driver Code
public static void main (String[] args)
{
    int x = 3, y = 5;

    System.out.println("XOR is " + myXOR(x, y));
}
}

// This code is contributed by math_lover
```

## python 3

```
# Python3 program to find XOR without using ^

# Returns XOR of x and y
def myXOR(x, y):
    res = 0 # Initialize result

    # Assuming 32-bit Integer
    for i in range(31, -1, -1):

        # Find current bits in x and y
        b1 = x & (1 << i)
        b2 = y & (1 << i)
        b1 = min(b1, 1)
        b2 = min(b2, 1)

        # If both are 1 then 0
        # else xor is same as OR
        xoredBit = 0
        if (b1 & b2):
            xoredBit = 0
        else:
            xoredBit = (b1 | b2)

        # Update result
        res <<= 1;
        res |= xoredBit
    return res

# Driver Code
x = 3
y = 5
print("XOR is", myXOR(x, y))

# This code is contributed by Mohit Kumar
```

## c#

```
// C# program to find XOR
// without using ^
using System;
class GFG{

// Returns XOR of x and y
static int myXOR(int x,
                 int y)
{   
  // Initialize result
  int res = 0;

  // Assuming 32-bit int
  for(int i = 31; i >= 0; i--)                    
  {
    // Find current bits in x and y
    int b1 = ((x & (1 << i)) == 0 ) ?
               0 : 1; 
    int b2 = ((y & (1 << i)) == 0 ) ?
               0 : 1; 

    // If both are 1 then 0 else
    // xor is same as OR
    int xoredBit = ((b1 & b2) != 0) ?
                     0 : (b1 | b2);         

    // Update result
    res <<= 1;
    res |= xoredBit;
  }
  return res;
}

// Driver Code
public static void Main(String[] args)
{
  int x = 3, y = 5;
  Console.WriteLine("XOR is " +
                     myXOR(x, y));
}
}

// This code is contributed by 29AjayKumar
```

## Javascript

```
<script>

// JavaScript program to find XOR without using ^

// Returns XOR of x and y
function myXOR(x, y)
{
    let res = 0; // Initialize result

    // Assuming 32-bit Integer
    for (let i = 31; i >= 0; i--)                    
    {
    // Find current bits in x and y
      let b1 = ((x & (1 << i)) == 0 ) ? 0 : 1; 
      let b2 = ((y & (1 << i)) == 0 ) ? 0 : 1; 

        // If both are 1 then 0 else xor is same as OR
        let xoredBit = (b1 & b2) ? 0 : (b1 | b2);        

        // Update result
        res <<= 1;
        res |= xoredBit;
    }
    return res;
}

// Driver program to test above function

let x = 3, y = 5;
document.write("XOR is " + myXOR(x, y));

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出**

```
XOR is 6
```