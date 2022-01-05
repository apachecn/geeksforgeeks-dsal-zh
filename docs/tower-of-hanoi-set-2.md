# 河内塔|第二集

> 原文:[https://www.geeksforgeeks.org/tower-of-hanoi-set-2/](https://www.geeksforgeeks.org/tower-of-hanoi-set-2/)

给定一个正整数 **N** 代表河内[塔](https://www.geeksforgeeks.org/c-program-for-tower-of-hanoi/)中的磁盘数量，任务是使用[二进制表示法](https://www.geeksforgeeks.org/binary-representations-in-digital-logic/)解决**河内塔难题**。

**示例:**

> **输入:** N = 3
> **输出:**
> 将 1 盘移到下一个圆形右杆
> 将 2 盘移到下一个圆形右杆
> 将 1 盘移到下一个圆形右杆
> 将 3 盘移到下一个圆形右杆
> 将 1 盘移到下一个圆形右杆
> 将 2 盘移到下一个圆形右杆
> 将 1 盘移到下一个圆形右杆
> 
> **输入:** N = 4
> **输出:**
> 将 1 盘移到下一个圆形右杆
> 将 2 盘移到下一个圆形右杆
> 将 1 盘移到下一个圆形右杆
> 将 3 盘移到下一个圆形右杆
> 将 1 盘移到下一个圆形右杆
> 将 2 盘移到下一个圆形右杆
> 将 1 盘移到下一个圆形右杆
> 将 4 盘移到下一个圆形右杆
> 将 1 盘移到下一个圆形右杆
> 将 2 盘移到下一个圆形右杆
> 将 1 盘移到下一个圆形右杆
> 将 3 盘移到下一个圆形右杆
> 将 1 盘移到下一个圆形右杆
> 将 2 盘移到下一个圆形右杆
> 将 1 盘移到下一个圆形右杆

**方法:**给定的问题可以基于以下观察来解决:

*   可以观察到，要移动 **N <sup>第</sup>T3】盘，**(N–1)<sup>第</sup>** 盘需要移动。因此，要移动**(N–1)<sup>第</sup>** 个磁盘，**(N–2)<sup>第</sup>** 个磁盘需要移动。这个过程递归地进行。**
*   上述过程类似于设置[最右边的未设置位](https://www.geeksforgeeks.org/get-position-rightmost-unset-bit/)，因为它需要首先设置其右边的所有位。
*   因此，想法是打印所有中间步骤，每次通过将当前编号增加 **1** 来设置[最右边的位](https://www.geeksforgeeks.org/position-of-rightmost-set-bit/)。

按照以下步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/majority-element/)，比如**计数器[]** ，大小为 **N** ，来存储问题的当前状态。
*   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，2<sup>N</sup>–1】**，[设置最右侧的未设置位](https://www.geeksforgeeks.org/set-rightmost-unset-bit-2/)，并将其右侧的所有位取消设置。
*   在上述步骤的每次迭代中，将[最右边未置位位](https://www.geeksforgeeks.org/get-position-rightmost-unset-bit/)的位置打印为要移动的盘的编号。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to increment binary counter
int increment(int* counter, int n)
{
    int i = 0;

    while (true) {

        // Stores the Bitwise XOR of
        // the i-th bit of N and 1
        int a = counter[i] ^ 1;

        // Stores the Bitwise AND of
        // the i-th bit of N and 1
        int b = counter[i] & 1;

        // Swaps the i-th bit of N
        counter[i] = a;

        // If b is equal to zero
        if (b == 0)
            break;

        // Increment i by 1
        i = i + 1;
    }

    // Return i
    return i;
}

// Function to print order of movement
// of disks across three rods to place
// all disks on the third rod from the
// first rod
void TowerOfHanoi(int N)
{
    // Stores the binary representation
    // of a state
    int counter[N] = { 0 };

    // Traverse the range [0, 2^N - 1]
    for (int step = 1;
         step <= pow(2, N) - 1; step++) {

        // Stores the position of the
        // rightmost unset bit
        int x = increment(counter, N) + 1;

        // Print the Xth bit
        cout << "Move disk " << x
             << " to next circular"
             << " right rod \n";
    }
}

// Driver Code
int main()
{
    int N = 3;
    TowerOfHanoi(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to increment binary counter
static int increment(int[] counter, int n)
{
    int i = 0;

    while (true)
    {

        // Stores the Bitwise XOR of
        // the i-th bit of N and 1
        int a = counter[i] ^ 1;

        // Stores the Bitwise AND of
        // the i-th bit of N and 1
        int b = counter[i] & 1;

        // Swaps the i-th bit of N
        counter[i] = a;

        // If b is equal to zero
        if (b == 0)
            break;

        // Increment i by 1
        i = i + 1;
    }

    // Return i
    return i;
}

// Function to print order of movement
// of disks across three rods to place
// all disks on the third rod from the
// first rod
static void TowerOfHanoi(int N)
{

    // Stores the binary representation
    // of a state
    int[] counter=new int[N];

    // Traverse the range [0, 2^N - 1]
    for(int step = 1;
            step <= Math.pow(2, N) - 1;
            step++)
    {

        // Stores the position of the
        // rightmost unset bit
        int x = increment(counter, N) + 1;

        // Print the Xth bit
        System.out.println("Move disk " + x +
                           " to next circular" +
                           " right rod");
    }
}

// Driver code
public static void main(String[] args)
{

    // Given inputs
    int N = 3;

    TowerOfHanoi(N);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python program for the above approach
import math

# Function to increment binary counter
def increment(counter, n):
    i = 0

    while (True):

        # Stores the Bitwise XOR of
        # the i-th bit of N and 1
        a = counter[i] ^ 1

        # Stores the Bitwise AND of
        # the i-th bit of N and 1
        b = counter[i] & 1

        # Swaps the i-th bit of N
        counter[i] = a

        # If b is equal to zero
        if (b == 0):
            break

        # Increment i by 1 
        i = i + 1
    return i

# Function to print order of movement
# of disks across three rods to place
# all disks on the third rod from the
# first rod   
def TowerOfHanoi(N):

    # Stores the binary representation
    # of a state
    counter=[0 for i in range(N)]

    # Traverse the range [0, 2^N - 1]
    for step in range(1,int(math.pow(2,N))):

        # Stores the position of the
        # rightmost unset bit
        x = increment(counter, N) + 1

        #Print the Xth bit
        print("Move disk ",x," to next circular"," right rod")

# Driver code
N = 3
TowerOfHanoi(N)

# This code is contributed by rag2127
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to increment binary counter
    static int increment(int[] counter, int n)
    {
        int i = 0;
        while (true)
        {

            // Stores the Bitwise XOR of
            // the i-th bit of N and 1
            int a = counter[i] ^ 1;

            // Stores the Bitwise AND of
            // the i-th bit of N and 1
            int b = counter[i] & 1;

            // Swaps the i-th bit of N
            counter[i] = a;

            // If b is equal to zero
            if (b == 0)
                break;

            // Increment i by 1
            i = i + 1;
        }

        // Return i
        return i;
    }

    // Function to print order of movement
    // of disks across three rods to place
    // all disks on the third rod from the
    // first rod
    static void TowerOfHanoi(int N)
    {

        // Stores the binary representation
        // of a state
        int[] counter = new int[N];

        // Traverse the range [0, 2^N - 1]
        for (int step = 1;
             step <= (int)(Math.Pow(2, N) - 1); step++)
        {

            // Stores the position of the
            // rightmost unset bit
            int x = increment(counter, N) + 1;

            // Print the Xth bit
            Console.WriteLine("Move disk " + x
                              + " to next circular"
                              + " right rod ");
        }
    }

    // Driver Code
    public static void Main()
    {
        int N = 3;
        TowerOfHanoi(N);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// Javascript implementation for the above approach

// Function to increment binary counter
function increment(counter, n)
{
    let i = 0;

    while (true)
    {

        // Stores the Bitwise XOR of
        // the i-th bit of N and 1
        let a = counter[i] ^ 1;

        // Stores the Bitwise AND of
        // the i-th bit of N and 1
        let b = counter[i] & 1;

        // Swaps the i-th bit of N
        counter[i] = a;

        // If b is equal to zero
        if (b == 0)
            break;

        // Increment i by 1
        i = i + 1;
    }

    // Return i
    return i;
}

// Function to prlet order of movement
// of disks across three rods to place
// all disks on the third rod from the
// first rod
function TowerOfHanoi(N)
{

    // Stores the binary representation
    // of a state
    let counter= Array.from({length: N}, (_, i) => 0);

    // Traverse the range [0, 2^N - 1]
    for(let step = 1;
            step <= Math.pow(2, N) - 1;
            step++)
    {

        // Stores the position of the
        // rightmost unset bit
        let x = increment(counter, N) + 1;

        // Print the Xth bit
        document.write("Move disk " + x +
                           " to next circular" +
                           " right rod" + "<br/>");
    }
}

    // Driver Code

    // Given inputs
    let N = 3;

    TowerOfHanoi(N);

// This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
Move disk 1 to next circular right rod 
Move disk 2 to next circular right rod 
Move disk 1 to next circular right rod 
Move disk 3 to next circular right rod 
Move disk 1 to next circular right rod 
Move disk 2 to next circular right rod 
Move disk 1 to next circular right rod
```

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(N)*

**高效进场:**上述进场可基于以下观察进行优化: **M** 在范围**【1，2<sup>N</sup>–1】**内，源棒等于**(M&(M–1))% 3**，目的棒等于**(M |(M–1)+1)% 3**。所以思路是[迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)****【1，2<sup>N</sup>–1】**打印**的值(I&(I–1))% 3**为源棒，**(I |(I–1)+1)% 3**为目的棒。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print order of movement
// of N disks across three rods to place
// all disks on the third rod from the
// first-rod using binary representation
void TowerOfHanoi(int N)
{
    // Iterate over the range [0, 2^N - 1]
    for (int x = 1;
         x <= pow(2, N) - 1; x++) {

        // Print the movement
        // of the current rod
        cout << "Move from Rod "
             << ((x & x - 1) % 3 + 1)
             << " to Rod "
             << (((x | x - 1) + 1) % 3 + 1)
             << endl;
    }
}

// Driver Code
int main()
{
    int N = 3;
    TowerOfHanoi(N);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
class GFG{

// Function to print order of movement
// of N disks across three rods to place
// all disks on the third rod from the
// first-rod using binary representation
static void TowerOfHanoi(int N)
{

    // Iterate over the range [0, 2^N - 1]
    for(int x = 1;
            x <= Math.pow(2, N) - 1; x++)
    {

        // Print the movement
        // of the current rod
        System.out.print("Move from Rod " +
                         ((x & x - 1) % 3 + 1) + " to Rod " +
                         (((x | x - 1) + 1) % 3 + 1) + "\n");
    }
}

// Driver Code
public static void main (String[] args)
{
    int N = 3;

    TowerOfHanoi(N);
}
}

// This code is contributed by jana_sayantan
```

## **蟒蛇 3**

```
# Python program for the above approach
import math

# Function to print order of movement
# of N disks across three rods to place
# all disks on the third rod from the
# first-rod using binary representation
def TowerOfHanoi(N):

    # Iterate over the range [0, 2^N - 1]
    for x in range(1,int(math.pow(2, N)) ):

        # Print the movement
        # of the current rod
        print("Move from Rod " ,
                         ((x & x - 1) % 3 + 1) , " to Rod " ,
                         (((x | x - 1) + 1) % 3 + 1) )

# Driver Code
N=3
TowerOfHanoi(N)

# This code is contributed by avanitrachhadiya2155
```

## **C#**

```
// C# program for the above approach
using System;

class GFG{

// Function to print order of movement
// of N disks across three rods to place
// all disks on the third rod from the
// first-rod using binary representation
static void TowerOfHanoi(int N)
{

    // Iterate over the range [0, 2^N - 1]
    for(int x = 1;
            x <= Math.Pow(2, N) - 1; x++)
    {

        // Print the movement
        // of the current rod
        Console.Write("Move from Rod " +
                         ((x & x - 1) % 3 + 1) + " to Rod " +
                         (((x | x - 1) + 1) % 3 + 1) + "\n");
    }
}

// Driver Code
static void Main()
{
    int N = 3;

    TowerOfHanoi(N);
}
}

// This code is contributed by SoumikMondal
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

// Function to print order of movement
// of N disks across three rods to place
// all disks on the third rod from the
// first-rod using binary representation
function TowerOfHanoi(N)
{
    // Iterate over the range [0, 2^N - 1]
    for (let x = 1;
         x <= Math.pow(2, N) - 1; x++) {

        // Print the movement
        // of the current rod
        document.write("Move from Rod "
             + ((x & x - 1) % 3 + 1)
             + " to Rod "
             + (((x | x - 1) + 1) % 3 + 1)
             + "<br>");
    }
}

// Driver Code
    let N = 3;
    TowerOfHanoi(N);

</script>
```

****Output:** 

```
Move from Rod 1 to Rod 3
Move from Rod 1 to Rod 2
Move from Rod 3 to Rod 2
Move from Rod 1 to Rod 3
Move from Rod 2 to Rod 1
Move from Rod 2 to Rod 3
Move from Rod 1 to Rod 3
```** 

*****时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)***