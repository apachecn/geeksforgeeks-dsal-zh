# 两个整数的二进制表示中不匹配的位数

> 原文:[https://www . geesforgeks . org/两个整数的二进制表示中的不匹配位数/](https://www.geeksforgeeks.org/number-of-mismatching-bits-in-the-binary-representation-of-two-integers/)

给定两个整数(小于 2^31) A 和 b，任务是找出二进制表示中不同的位数。

**例:**

```
Input :  A = 12, B = 15
Output : Number of different bits : 2
Explanation: The binary representation of 
12 is 1100 and 15 is 1111.
So, the number of different bits are 2.

Input : A = 3, B = 16
Output : Number of different bits : 3
```

**方法:**

*   Loop from' 0' to' 31', shift the bits of A and B to the right by' I' bit, and then check whether the bits of' 0' bit are different.
*   If the bits are different, the count is increased.
*   Since the number is less than 2.31, we only need to cycle' 32' times, that is, from' 0' to' 31'.
*   If we "AND" 1 the number bit by bit, we can get the first digit.
*   Display the count at the end of the loop.

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// compute number of different bits
void solve(int A, int B)
{
    int count = 0;

    // since, the numbers are less than 2^31
    // run the loop from '0' to '31' only
    for (int i = 0; i < 32; i++) {

        // right shift both the numbers by 'i' and
        // check if the bit at the 0th position is different
        if (((A >> i) & 1) != ((B >> i) & 1)) {
            count++;
        }
    }

    cout << "Number of different bits : " << count << endl;
}

// Driver code
int main()
{
    int A = 12, B = 15;

    // find number of different bits
    solve(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

import java.io.*;

class GFG {

// compute number of different bits
static void solve(int A, int B)
{
    int count = 0;

    // since, the numbers are less than 2^31
    // run the loop from '0' to '31' only
    for (int i = 0; i < 32; i++) {

        // right shift both the numbers by 'i' and
        // check if the bit at the 0th position is different
        if (((A >> i) & 1) != ((B >> i) & 1)) {
            count++;
        }
    }

    System.out.println("Number of different bits : " + count);
}

// Driver code

    public static void main (String[] args) {
        int A = 12, B = 15;

    // find number of different bits
    solve(A, B);

    }
}
// this code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# compute number of different bits
def solve( A,  B):

    count = 0

    # since, the numbers are less than 2^31
    # run the loop from '0' to '31' only
    for i in range(0,32):

        # right shift both the numbers by 'i' and
        # check if the bit at the 0th position is different
        if ((( A >>  i) & 1) != (( B >>  i) & 1)):
             count=count+1

    print("Number of different bits :",count)

# Driver code
A = 12
B = 15

# find number of different bits
solve( A,  B)

# This code is contributed by ihritik
```

## C#

```
// C# implementation of the approach

using System;
class GFG
{
    // compute number of different bits
    static void solve(int A, int B)
    {
        int count = 0;

        // since, the numbers are less than 2^31
        // run the loop from '0' to '31' only
        for (int i = 0; i < 32; i++) {

            // right shift both the numbers by 'i' and
            // check if the bit at the 0th position is different
            if (((A >> i) & 1) != ((B >> i) & 1)) {
                count++;
            }
        }

        Console.WriteLine("Number of different bits : " + count);
    }

    // Driver code
    public static void  Main()
    {
        int A = 12, B = 15;

        // find number of different bits
        solve(A, B);

    }

}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// compute number of different bits
function solve($A, $B)
{
    $count = 0;

    // since, the numbers are less than 2^31
    // run the loop from '0' to '31' only
    for ($i = 0; $i < 32; $i++) {

        // right shift both the numbers by 'i' and
        // check if the bit at the 0th position is different
        if ((($A >> $i) & 1) != (($B >> $i) & 1)) {
            $count++;
        }
    }

    echo "Number of different bits : $count";
}

// Driver code
$A = 12;
$B = 15;

// find number of different bits
solve($A, $B);

// This code is contributed by ihritik
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Compute number of different bits
function solve(A, B)
{
    var count = 0;

    // Since, the numbers are less than 2^31
    // run the loop from '0' to '31' only
    for(i = 0; i < 32; i++)
    {

        // Right shift both the numbers by 'i'
        // and check if the bit at the 0th
        // position is different
        if (((A >> i) & 1) != ((B >> i) & 1))
        {
            count++;
        }
    }
    document.write("Number of different bits : " +
                   count);
}

// Driver code   
var A = 12, B = 15;

// Find number of different bits
solve(A, B);

// This code is contributed by Rajput-Ji

</script>
```

**Output**

```
Number of different bits : 2
```

**一种不同的方法使用 xor(^):**

*   Seek two numbers of difference or (), such as A and B. 。
*   And let A&B of their result xor () become c;
*   Calculate the set number of bits in the binary representation of C (1);
*   Return count;

例:

*   Let A = 10 (01010) and B = 20(10100)
*   XOR = 11110 is obtained after XOR of A and B .. (Check the XOR table if necessary).
*   Calculating the number of 1 in XOR operation gives the count of bit difference between A and B (using Brian Knigan's algorithm).

下面是上述方法的实现:

## c++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// compute number of different bits
int solve(int A, int B)
{
    int XOR = A ^ B;
    // Check for 1's in the binary form using
    // Brian Kerninghan's Algorithm
    int count = 0;
    while (XOR) {
        XOR = XOR & (XOR - 1);
        count++;
    }
    return count;
}

// Driver code
int main()
{
    int A = 12, B = 15;
    // 12 = 1100 & 15 = 1111
    int result = solve(A, B);
    cout << "Number of different bits : " << result;

    return 0;
}
// the code is by Samarpan Chakraborty
```

## Java

```
/*package whatever //do not write package name here */
// Java implementation of the approach
import java.io.*;

class GFG {

    // compute number of different bits
    static int solve(int A, int B)
    {
        int XOR = A ^ B;
        // Check for 1's in the binary form using
        // Brian Kerninghan's Algorithm
        int count = 0;
        while (XOR > 0) {
            XOR = XOR & (XOR - 1);
            count++;
        }
        // return the count of different bits
        return count;
    }

    public static void main(String[] args)
    {
        int A = 12, B = 15;

        // find number of different bits
        int result = solve(A, B);
        System.out.println("Number of different bits : "
                           + result);
    }
}
// the code is by Samarpan Chakraborty
```

## python 3

```
# code
def solve(A, B):
    XOR = A ^ B
    count = 0
    # Check for 1's in the binary form using
    # Brian Kernighan's Algorithm
    while (XOR):
        XOR = XOR & (XOR - 1)
        count += 1
    return count

result = solve(3, 16)
# 3 = 00011 & 16 = 10000
print("Number of different bits : ", result)

# the code is by Samarpan Chakraborty
```

## c#

```
// C# program for the above approach
using System;
class GFG {

   // compute number of different bits
    static int solve(int A, int B)
    {
        int XOR = A ^ B;

        // Check for 1's in the binary form using
        // Brian Kerninghan's Algorithm
        int count = 0;
        while (XOR > 0) {
            XOR = XOR & (XOR - 1);
            count++;
        }
        // return the count of different bits
        return count;
    }

// Driver code
public static void Main()
{
    int A = 12, B = 15;

        // find number of different bits
        int result = solve(A, B);
        Console.WriteLine("Number of different bits : "
                           + result);
}
}

// This code is contributed by target_2.
```

## Javascript

```
<script>

/*package whatever //do not write package name here */
// JavaScript implementation of the approach
// compute number of different bits
function solve(A, B)
{
        var XOR = A ^ B;

        // Check for 1's in the binary form using
        // Brian Kerninghan's Algorithm
        var count = 0;
        while (XOR > 0) {
            XOR = XOR & (XOR - 1);
            count++;
        }

        // return the count of different bits
        return count;
    }

        var A = 12, B = 15;

        // find number of different bits
        var result = solve(A, B);
        document.write("Number of different bits : "
                           + result);

// This code is contributed by shivanisinghss2110
</script>
```

**输出**

[布莱恩·克尼根的算法](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)