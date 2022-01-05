# 从其所有对的给定按位异或和按位与值中找到三元组

> 原文:[https://www . geeksforgeeks . org/find-the-three-from-given-bitwise-xor-and-bitwise-and-values-of-it-all-pairs/](https://www.geeksforgeeks.org/find-the-triplet-from-given-bitwise-xor-and-bitwise-and-values-of-all-its-pairs/)

给定六个正整数表示三重态 **(a，b，c)** 的所有可能对的[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)和[位与](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)，任务是找到三重态。

**示例:**

> **输入:** aXORb = 30，aANDb = 0，aXORc = 10，aANDc = 20，aXORb = 20，aANDb = 10
> **输出:** a = 10，b = 20，c = 30
> T6】解释:t8】如果 a = 10，b = 20，c= 30
> a ^ b = 30，a & b = 0
> a ^ c = 10
> 
> **输入:** aXORb = 3，aANDb = 0，aXORc = 2，aANDc = 1，aXORb = 1，aANDb = 2
> **输出:** a = 1，b = 2，c = 3

**方法:**想法是基于以下观察，使用它们的[逐位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)和[逐位与](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)值来找到每一个可能的三元组对的和:

> a + b = a ^ b + 2 * (a & b)

按照以下步骤解决问题:

*   用上面的公式求出每一对可能的三元组的和，即 **(a + b，b + c，c + a)** 。
*   **a** 的值可以计算为**((a+b)+(a+c)–(b+c))/2**。
*   **b** 的值可以计算为**((a+b)–a)**。
*   **c** 的值可以计算为**((b+ c)–b)**。
*   最后，打印三元组 **(a，b，c)** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the triplet with given
// Bitwise XOR and Bitwise AND values of all
// possible pairs of the triplet
void findNumbers(int aXORb, int aANDb, int aXORc, int aANDc,
                 int bXORc, int bANDc)
{
    // Stores values of
    // a triplet
    int a, b, c;

    // Stores a + b
    int aSUMb;

    // Stores a + c
    int aSUMc;

    // Stores b + c
    int bSUMc;

    // Calculate aSUMb
    aSUMb = aXORb + aANDb * 2;

    // Calculate aSUMc
    aSUMc = aXORc + aANDc * 2;

    // Calculate bSUMc
    bSUMc = bXORc + bANDc * 2;

    // Calculate a
    a = (aSUMb - bSUMc + aSUMc) / 2;

    // Calculate b
    b = aSUMb - a;

    // Calculate c
    c = aSUMc - a;

    // Print a
    cout << "a = " << a;

    // Print b
    cout << ", b = " << b;

    // Print c
    cout << ", c = " << c;
}

// Driver Code
int main()
{
    int aXORb = 30, aANDb = 0, aXORc = 20, aANDc = 10,
        bXORc = 10, bANDc = 20;

    findNumbers(aXORb, aANDb, aXORc, aANDc, bXORc, bANDc);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to find the triplet with given
// Bitwise XOR and Bitwise AND values of all
// possible pairs of the triplet
static void findNumbers(int aXORb, int aANDb,
                        int aXORc, int aANDc,
                        int bXORc, int bANDc)
{

    // Stores values of
    // a triplet
    int a, b, c;

    // Stores a + b
    int aSUMb;

    // Stores a + c
    int aSUMc;

    // Stores b + c
    int bSUMc;

    // Calculate aSUMb
    aSUMb = aXORb + aANDb * 2;

    // Calculate aSUMc
    aSUMc = aXORc + aANDc * 2;

    // Calculate bSUMc
    bSUMc = bXORc + bANDc * 2;

    // Calculate a
    a = (aSUMb - bSUMc + aSUMc) / 2;

    // Calculate b
    b = aSUMb - a;

    // Calculate c
    c = aSUMc - a;

    // Print a
    System.out.print("a = " + a);

    // Print b
    System.out.print(", b = " + b);

    // Print c
    System.out.print(", c = " + c);
}

// Driver Code
public static void main(String[] args)
{
    int aXORb = 30, aANDb = 0,
        aXORc = 20, aANDc = 10,
        bXORc = 10, bANDc = 20;

    findNumbers(aXORb, aANDb, aXORc,
                aANDc, bXORc, bANDc);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program to implement
# the above approach

# Function to find the triplet with given
# Bitwise XOR and Bitwise AND values of all
# possible pairs of the triplet
def findNumbers(aXORb, aANDb, aXORc, aANDc, bXORc, bANDc):

    # Stores values of
    # a triplet
    a, b, c = 0, 0, 0;

    # Stores a + b
    aSUMb = 0;

    # Stores a + c
    aSUMc = 0;

    # Stores b + c
    bSUMc = 0;

    # Calculate aSUMb
    aSUMb = aXORb + aANDb * 2;

    # Calculate aSUMc
    aSUMc = aXORc + aANDc * 2;

    # Calculate bSUMc
    bSUMc = bXORc + bANDc * 2;

    # Calculate a
    a = (aSUMb - bSUMc + aSUMc) // 2;

    # Calculate b
    b = aSUMb - a;

    # Calculate c
    c = aSUMc - a;

    # Pra
    print("a = " , a, end = "");

    # Prb
    print(", b = " , b, end = "");

    # Prc
    print(", c = " , c, end = "");

# Driver Code
if __name__ == '__main__':
    aXORb = 30; aANDb = 0; aXORc = 20; aANDc = 10; bXORc = 10; bANDc = 20;

    findNumbers(aXORb, aANDb, aXORc, aANDc, bXORc, bANDc);

# This code contributed by shikhasingrajput
```

## C#

```
// C# code for above approach
using System;
public class GFG
{

  // Function to find the triplet with given
  // Bitwise XOR and Bitwise AND values of all
  // possible pairs of the triplet
  static void findNumbers(int aXORb, int aANDb,
                          int aXORc, int aANDc,
                          int bXORc, int bANDc)
  {

    // Stores values of
    // a triplet
    int a, b, c;

    // Stores a + b
    int aSUMb;

    // Stores a + c
    int aSUMc;

    // Stores b + c
    int bSUMc;

    // Calculate aSUMb
    aSUMb = aXORb + aANDb * 2;

    // Calculate aSUMc
    aSUMc = aXORc + aANDc * 2;

    // Calculate bSUMc
    bSUMc = bXORc + bANDc * 2;

    // Calculate a
    a = (aSUMb - bSUMc + aSUMc) / 2;

    // Calculate b
    b = aSUMb - a;

    // Calculate c
    c = aSUMc - a;

    // Print a
    System.Console.Write("a = " + a);

    // Print b
    System.Console.Write(", b = " + b);

    // Print c
    System.Console.Write(", c = " + c);
  }

  // Driver code
  static public void Main ()
  {
    int aXORb = 30, aANDb = 0,
    aXORc = 20, aANDc = 10,
    bXORc = 10, bANDc = 20;

    findNumbers(aXORb, aANDb, aXORc,
                aANDc, bXORc, bANDc);
  }
}

// This code is contributed by offbeat.
```

## java 描述语言

```
<script>
// JavaScript program to implement
// the above approach

// Function to find the triplet with given
// Bitwise XOR and Bitwise AND values of all
// possible pairs of the triplet
function findNumbers(aXORb, aANDb, aXORc, aANDc, bXORc, bANDc)
{
    // Stores values of
    // a triplet
    let a, b, c;

    // Stores a + b
    let aSUMb;

    // Stores a + c
    let aSUMc;

    // Stores b + c
    let bSUMc;

    // Calculate aSUMb
    aSUMb = aXORb + aANDb * 2;

    // Calculate aSUMc
    aSUMc = aXORc + aANDc * 2;

    // Calculate bSUMc
    bSUMc = bXORc + bANDc * 2;

    // Calculate a
    a = Math.floor((aSUMb - bSUMc + aSUMc) / 2);

    // Calculate b
    b = aSUMb - a;

    // Calculate c
    c = aSUMc - a;

    // Print a
    document.write("a = " + a);

    // Print b
    document.write(", b = " + b);

    // Print c
    document.write(", c = " + c);
}

// Driver Code

    let aXORb = 30, aANDb = 0, aXORc = 20, aANDc = 10,
        bXORc = 10, bANDc = 20;

    findNumbers(aXORb, aANDb, aXORc, aANDc, bXORc, bANDc);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
a = 10, b = 20, c = 30
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)