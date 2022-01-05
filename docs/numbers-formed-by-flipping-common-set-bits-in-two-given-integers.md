# 通过翻转两个给定整数中的公共集合位形成的数字

> 原文:[https://www . geeksforgeeks . org/numbers-通过翻转普通二进制整数位形成/](https://www.geeksforgeeks.org/numbers-formed-by-flipping-common-set-bits-in-two-given-integers/)

给定两个正整数 **A** 和 **B** ，任务是翻转 **A** 和 **B** 中常用的[设定位](https://www.geeksforgeeks.org/find-position-of-the-only-set-bit/)。

**示例:**

> **输入:** A = 7，B = 4
> **输出:** 3 0
> **解释:**
> 7 的二进制表示为 111
> 4 的二进制表示为 100
> 因为 A 和 B 的第三位都是设定位。因此，翻转 A 和 B 的第三位会修改 A = 3 和 B = 0
> 因此，所需的输出为 3 0
> 
> **输入:** A = 10，B = 20
> T3】输出: 10 20

**天真方法:**解决这个问题最简单的方法是[检查 **A** 和 **B** 的**I<sup>th</sup>T6】位是否都是一组**](https://www.geeksforgeeks.org/check-whether-k-th-bit-set-not/)。如果发现为真，则翻转 **A** 和 **B** 的 **i <sup>th</sup>** 位。最后，打印 **A** 和 **B** 的更新值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to flip bits of A and B
// which are set bits in A and B
void flipBitsOfAandB(int A, int B)
{
    // Iterator all possible bits
    // of A and B
    for (int i = 0; i < 32; i++) {

        // If ith bit is set in
        // both A and B
        if ((A & (1 << i)) && (B & (1 << i))) {

            // Clear i-th bit of A
            A = A ^ (1 << i);

            // Clear i-th bit of B
            B = B ^ (1 << i);
        }
    }

    // Print A and B
    cout << A << " " << B;
}

// Driver Code
int main()
{
    int A = 7, B = 4;

    flipBitsOfAandB(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to flip bits of A and B
// which are set bits in A and B
static void flipBitsOfAandB(int A, int B)
{

    // Iterator all possible bits
    // of A and B
    for(int i = 0; i < 32; i++)
    {

        // If ith bit is set in
        // both A and B
        if (((A & (1 << i)) &
             (B & (1 << i))) != 0)
        {

            // Clear i-th bit of A
            A = A ^ (1 << i);

            // Clear i-th bit of B
            B = B ^ (1 << i);
        }
    }

    // Print A and B
    System.out.print(A + " " + B);
}

// Driver Code
public static void main(String[] args)
{
    int A = 7, B = 4;

    flipBitsOfAandB(A, B);
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to flip bits of A and B
# which are set in both of them
def flipBitsOfAandB(A, B):

    # Iterate all possible bits of
    # A and B
    for i in range(0, 32):

        # If ith bit is set in
        # both A and B
        if ((A & (1 << i)) and
            (B & (1 << i))):

            # Clear i-th bit of A
            A = A ^ (1 << i)

            # Clear i-th bit of B
            B = B ^ (1 << i)

    print(A, B)

# Driver Code 
if __name__ == "__main__" :

    A = 7
    B = 4

    flipBitsOfAandB(A, B)

# This code is contributed by Virusbuddah_
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to flip bits of A and B
// which are set bits in A and B
static void flipBitsOfAandB(int A, int B)
{

    // Iterator all possible bits
    // of A and B
    for(int i = 0; i < 32; i++)
    {

        // If ith bit is set in
        // both A and B
        if (((A & (1 << i)) &
             (B & (1 << i))) != 0)
        {

            // Clear i-th bit of A
            A = A ^ (1 << i);

            // Clear i-th bit of B
            B = B ^ (1 << i);
        }
    }

    // Print A and B
    Console.Write(A + " " + B);
}

// Driver Code
public static void Main(string[] args)
{
    int A = 7, B = 4;

    flipBitsOfAandB(A, B);
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>
// javascript program to implement
// the above approach

// Function to flip bits of A and B
// which are set bits in A and B
function flipBitsOfAandB(A , B)
{

    // Iterator all possible bits
    // of A and B
    for(i = 0; i < 32; i++)
    {

        // If ith bit is set in
        // both A and B
        if (((A & (1 << i)) &
             (B & (1 << i))) != 0)
        {

            // Clear i-th bit of A
            A = A ^ (1 << i);

            // Clear i-th bit of B
            B = B ^ (1 << i);
        }
    }

    // Print A and B
    document.write(A + " " + B);
}

// Driver Code
var A = 7, B = 4;

flipBitsOfAandB(A, B);

// This code is contributed by Princi Singh

</script>
```

**Output:** 

```
3 0
```

***时间复杂度:** O(32)*
***辅助空间:*** O(1)

**高效方法:**为了优化上述方法，该想法基于以下观察:

> 使用(A & B)找出 A 和 B 中的设定位。
> 使用 A = (A ^ (A & B))
> 清除在 a 和 b 中均为设定位的 a 位，使用 B = (B ^ (A & B))
> 清除在 a 和 b 中均为设定位的 b 位

按照以下步骤解决问题:

*   更新 **A = (A ^ (A & B))** 。
*   更新 **B = (B ^ (A & B))** 。
*   最后打印 **A** 和 **B** 的更新值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to flip bits of A and B
// which are set in both of them
void flipBitsOfAandB(int A, int B)
{

    // Clear the bits of A which
    // are set in both A and B
    A = A ^ (A & B);

    // Clear the bits of B which
    // are set in both A and B
    B = B ^ (A & B);

    // Print updated A and B
    cout << A << " " << B;
}

// Driver Code
int main()
{
    int A = 10, B = 20;

    flipBitsOfAandB(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to flip bits of A and B
// which are set in both of them
static void flipBitsOfAandB(int A, int B)
{

    // Clear the bits of A which
    // are set in both A and B
    A = A ^ (A & B);

    // Clear the bits of B which
    // are set in both A and B
    B = B ^ (A & B);

    // Print updated A and B
    System.out.print(A + " " + B);
}

// Driver Code
public static void main(String[] args)
{
    int A = 10, B = 20;

    flipBitsOfAandB(A, B);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to flip bits of A and B
# which are set in both of them
def flipBitsOfAandB(A, B):

    # Clear the bits of A which
    # are set in both A and B
    A = A ^ (A & B)

    # Clear the bits of B which
    # are set in both A and B
    B = B ^ (A & B)

    # Print updated A and B
    print(A, B)

# Driver Code 
if __name__ == "__main__" :

    A = 10
    B = 20

    flipBitsOfAandB(A, B)

# This code is contributed by Virusbuddah_
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to flip bits of A and B
// which are set in both of them
static void flipBitsOfAandB(int A, int B)
{

    // Clear the bits of A which
    // are set in both A and B
    A = A ^ (A & B);

    // Clear the bits of B which
    // are set in both A and B
    B = B ^ (A & B);

    // Print updated A and B
    Console.Write(A + " " + B);
}

// Driver Code
public static void Main(String[] args)
{
    int A = 10, B = 20;

    flipBitsOfAandB(A, B);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// javascript program to implement
// the above approach

// Function to flip bits of A and B
// which are set in both of them
function flipBitsOfAandB(A , B)
{

    // Clear the bits of A which
    // are set in both A and B
    A = A ^ (A & B);

    // Clear the bits of B which
    // are set in both A and B
    B = B ^ (A & B);

    // Print updated A and B
    document.write(A + " " + B);
}

// Driver Code
var A = 10, B = 20;

flipBitsOfAandB(A, B);

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
10 20
```

***时间复杂度:*** O(1)
***辅助空间:*** O(1)