# 设置和未设置位计数的绝对差值，单位为 N

> 原文:[https://www . geesforgeks . org/set 和 unset 之间的绝对差异-n 位计数/](https://www.geeksforgeeks.org/absolute-difference-between-set-and-unset-bit-count-in-n/)

**先决条件:**[STL 库中的 Bitset 函数](https://www.geeksforgeeks.org/c-bitset-and-its-application/)
给定一个数 **N** ，任务是找出这个给定数的 set 和 unset 位数的绝对差。

**示例:**

> **输入:** N = 14
> **输出:** 2
> **解释:**
> 14 的二进制表示为“1110”。
> 这里设置的位数是 3，未设置的位数是 1。
> 因此，绝对差为 2。
> 
> **输入:** N = 56
> **输出:** 0
> **解释:**
> 56 的二进制表示为“110100”。
> 这里设置的位数是 3，未设置的位数是 3。
> 因此，绝对差 0。

**进场:**

1.  计算给定数字的二进制表示中的总位数。
2.  使用 [STL 库](https://www.geeksforgeeks.org/the-c-standard-template-library-stl/)中定义的[位设置功能](https://www.geeksforgeeks.org/c-bitset-and-its-application/)，有效统计设置的位数。
3.  然后，我们将从总位数中减去设置的位数，得到未设置的位数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Max size of bitset
const int sz = 64;

// Function to return the total bits
// in the binary representation
// of a number
int totalbits(int N)
{
    return (int)(1 + log2(N));
}

// Function to calculate the
// absolute difference
int absoluteDifference(int N)
{
    bitset<sz> arr(N);

    int total_bits = totalbits(N);

    // Calculate the number of
    // set bits
    int set_bits = arr.count();

    // Calculate the number of
    // unset bits
    int unset_bits = total_bits
                     - set_bits;

    int ans = abs(set_bits
                  - unset_bits);

    // Return the absolute difference
    return ans;
}

// Driver Code
int main()
{
    // Given Number
    int N = 14;

    // Function Call
    cout << absoluteDifference(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Max size of bitset
static final int sz = 64;

// Function to return the total bits
// in the binary representation
// of a number
static int totalbits(int N)
{
    return (1 + (int)(Math.log(N) /
                      Math.log(2)));
}

// Function to calculate the
// absolute difference
static int absoluteDifference(int N)
{
    int arr = N;

    int total_bits = totalbits(N);

    // Calculate the number of
    // set bits
    int set_bits = countSetBits(arr);

    // Calculate the number of
    // unset bits
    int unset_bits = total_bits - set_bits;

    int ans = Math.abs(set_bits - unset_bits);

    // Return the absolute difference
    return ans;
}

static int countSetBits(int n)
{
    int count = 0;
    while (n > 0)
    {
        n &= (n - 1);
        count++;
    }
    return count;
}

// Driver code
public static void main(String[] args)
{

    // Given Number
    int N = 14;

    // Function Call
    System.out.println(absoluteDifference(N));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Max size of bitset
sz = 64

# Function to return the total bits
# in the binary representation
# of a number
def totalbits(N) :

    return (1 + (int)(math.log(N) / math.log(2)))

# Function to calculate the
# absolute difference
def absoluteDifference(N) :

    arr = N

    total_bits = totalbits(N)

    # Calculate the number of
    # set bits
    set_bits = countSetBits(arr)

    # Calculate the number of
    # unset bits
    unset_bits = total_bits - set_bits

    ans = abs(set_bits - unset_bits)

    # Return the absolute difference
    return ans

def countSetBits(n) :

    count = 0
    while (n > 0) :

        n = n & (n - 1)
        count += 1

    return count

# Given Number
N = 14

# Function Call
print(absoluteDifference(N))

# This code is contributed by divyesh072019
```

## C#

```
// C# program for the above approach
using System;
class GFG{

    // Function to return the total bits
    // in the binary representation
    // of a number
    static int totalbits(int N)
    {
        return (1 + (int)(Math.Log(N) /
                          Math.Log(2)));
    }

    // Function to calculate the
    // absolute difference
    static int absoluteDifference(int N)
    {
        int arr = N;

        int total_bits = totalbits(N);

        // Calculate the number of
        // set bits
        int set_bits = countSetBits(arr);

        // Calculate the number of
        // unset bits
        int unset_bits = total_bits - set_bits;

        int ans = Math.Abs(set_bits - unset_bits);

        // Return the absolute difference
        return ans;
    }

    static int countSetBits(int n)
    {
        int count = 0;
        while (n > 0)
        {
            n &= (n - 1);
            count++;
        }
        return count;
    }

  // Driver code
  static void Main() {

        // Given Number
        int N = 14;

        // Function Call
        Console.WriteLine(absoluteDifference(N));
  }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

    // Javascript program for the above approach

    // Function to return the total bits
    // in the binary representation
    // of a number
    function totalbits(N)
    {
        return (1 + parseInt(Math.log(N) / Math.log(2), 10));
    }

    // Function to calculate the
    // absolute difference
    function absoluteDifference(N)
    {
        let arr = N;

        let total_bits = totalbits(N);

        // Calculate the number of
        // set bits
        let set_bits = countSetBits(arr);

        // Calculate the number of
        // unset bits
        let unset_bits = total_bits - set_bits;

        let ans = Math.abs(set_bits - unset_bits);

        // Return the absolute difference
        return ans;
    }

    function countSetBits(n)
    {
        let count = 0;
        while (n > 0)
        {
            n &= (n - 1);
            count++;
        }
        return count;
    }

    // Given Number
    let N = 14;

    // Function Call
    document.write(absoluteDifference(N));

</script>
```

**Output:** 

```
2
```

**时间复杂度:** *O(log N)*