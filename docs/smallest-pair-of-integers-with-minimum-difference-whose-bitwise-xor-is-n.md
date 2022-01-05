# 最小差整数对，按位异或为 N

> 原文:[https://www . geesforgeks . org/最小差整数对，其位异或为-n/](https://www.geeksforgeeks.org/smallest-pair-of-integers-with-minimum-difference-whose-bitwise-xor-is-n/)

给定一个正整数 **N** ，任务是找出两个最小的整数 **A** 和 **B** ，使得 **A** 和 **B** 的[按位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)为 **N** ， **A** 和 **B** 之差最小。

**示例:**

> **输入:** N = 26
> **输出:** 10 16
> **说明:**
> 10 和 16 的按位异或是 26，两者之差最小。
> 
> **输入:**N = 1
> T3】输出: 0 1

**天真方法:**解决给定问题最简单的方法是[生成范围内所有可能的数字对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)**【0，N】**并打印出那对数字，它们的[按位异或](https://www.geeksforgeeks.org/tag/xor/)是给定的数字 **N** ，两个数字都是最小的。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以基于以下观察进行优化:

*   考虑任何数字的[二进制表示](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)是**“1100011”**，那么该数字可以围绕它们的[最高有效位(MSB)](https://www.geeksforgeeks.org/find-significant-set-bit-number/) 拆分为**“1000000”**和**“100011”**，这些数字的按位异或就是给定的数字。
*   从上面的拆分可以看出，**“1000000”**(说 **A** )和**“100011”**(说 **B** )形成的数是最小的，它们之间的差是最小的，因为 **B** 形成的值总是越小越接近 **A** 。

根据以上观察，满足给定标准的 **A** 和 **B** 的最小值是围绕其**最高有效位(MSB)** 分割给定的数 **N** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the numbers A and
// B whose Bitwise XOR is N and the
// difference between them is minimum
void findAandB(int N)
{

    // Find the MSB of the N
    int K = log2(N);

    // Find the value of B
    int B = (1 << K);

    // Find the value of A
    int A = B ^ N;

    // Print the result
    cout << A << ' ' << B;
}

// Driver Code
int main()
{

    int N = 26;
    findAandB(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class MyClass
{

// Function to find the numbers A and
// B whose Bitwise XOR is N and the
// difference between them is minimum
static void findAandB(int N)
{

    // Find the MSB of the N
    int K = (int)(Math.log(N) / Math.log(2));

    // Find the value of B
    int B = (1 << K);

    // Find the value of A
    int A = B ^ N;

    // Print the result
    System.out.println(A + " " + B);
}

    public static void main(String args[]) {
      int N = 26;
      findAandB(N);

    }
}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import log2

# Function to find the numbers A and
# B whose Bitwise XOR is N and the
# difference between them is minimum
def findAandB(N):

    # Find the MSB of the N
    K = int(log2(N))

    # Find the value of B
    B = (1 << K)

    # Find the value of A
    A = B ^ N

    # Print the result
    print(A, B)

# Driver Code
if __name__ == '__main__':

    N = 26

    findAandB(N)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the numbers A and
// B whose Bitwise XOR is N and the
// difference between them is minimum
static void findAandB(int N)
{

    // Find the MSB of the N
    int K = (int)(Math.Log(N) /
                  Math.Log(2));

    // Find the value of B
    int B = (1 << K);

    // Find the value of A
    int A = B ^ N;

    // Print the result
    Console.Write(A + " " + B);
}

// Driver Code
public static void Main(String[] args)
{
    int N = 26;

    findAandB(N);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach

        // Function to find the numbers A and
        // B whose Bitwise XOR is N and the
        // difference between them is minimum
        function findAandB(N) {

            // Find the MSB of the N
            let K = Math.log2(N);

            // Find the value of B
            let B = (1 << K);

            // Find the value of A
            let A = B ^ N;

            // Print the result
            document.write(A + ' ' + B);
        }

        // Driver Code

        let N = 26;
        findAandB(N);

  // This code is contributed by Potta Lokesh

 </script>
```

**Output:** 

```
10 16
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)