# 小于 X 的最大数字，最多有 K 个设置位

> 原文:[https://www . geeksforgeeks . org/最大数量小于 x 最多有 k 个设置位/](https://www.geeksforgeeks.org/largest-number-less-than-x-having-at-most-k-set-bits/)

给定一个整数 **X > 1** 和一个整数 **K > 0** ，任务是找到最大的奇数 **< X** ，使得其二进制表示中 **1 的**的数量最多为 **K** 。
**举例:**

> **输入:** X = 10，K = 2
> **输出:** 10
> **输入:** X = 29，K = 2
> **输出:** 24

**天真法:**从**X–1**开始，检查 **X** 下面最多有 **K** 个设置位的所有数字，第一个满足条件的数字就是需要的答案。
**有效方法:**是对设置位进行计数。如果计数小于或等于 K，则返回 x。否则，在计数–K 不变为 0 时，继续移除最右边的设置位。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the greatest number <= X
// having at most K set bits.
int greatestKBits(int X, int K)
{
    int set_bit_count = __builtin_popcount(X);
    if (set_bit_count <= K)
        return X;

    // Remove rightmost set bits one
    // by one until we count becomes k
    int diff = set_bit_count - K;
    for (int i = 0; i < diff; i++)
        X &= (X - 1);

    // Return the required number
    return X;
}

// Driver code
int main()
{
    int X = 21, K = 2;
    cout << greatestKBits(X, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG {

    // Function to return the greatest number <= X
    // having at most K set bits.
     int greatestKBits(int X, int K)
     {
       int set_bit_count = Integer.bitCount(X);
       if (set_bit_count <= K)
            return X;

        // Remove rightmost set bits one
        // by one until we count becomes k
        int diff = set_bit_count - K;
        for (int i = 0; i < diff; i++)
            X &= (X - 1);

        // Return the required number
        return X;
    }

// Driver code
public static void main (String[] args)
{
    int X = 21, K = 2;
    GFG g=new GFG();
      System.out.print(g.greatestKBits(X, K));
}

//This code is contributed by Shivi_Aggarwal
}
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the greatest
# number <= X having at most K set bits.
def greatestKBits(X, K):
    set_bit_count = bin(X).count('1')
    if (set_bit_count <= K):
        return X

    # Remove rightmost set bits one
    # by one until we count becomes k
    diff = set_bit_count - K
    for i in range(0, diff, 1):
        X &= (X - 1)

    # Return the required number
    return X

# Driver code
if __name__ == '__main__':
    X = 21
    K = 2
    print(greatestKBits(X, K))

# This code is contributed by
# Shashank_Sharma
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
    // Function to get no of set
    // bits in binary representation
    // of positive integer n
    static int countSetBits(int n)
    {
        int count = 0;
        while (n > 0)
        {
            count += n & 1;
            n >>= 1;
        }
        return count;
    }

    // Function to return the greatest number <= X
    // having at most K set bits.
    static int greatestKBits(int X, int K)
    {
        int set_bit_count = countSetBits(X);
        if (set_bit_count <= K)
        return X;

        // Remove rightmost set bits one
        // by one until we count becomes k
        int diff = set_bit_count - K;
        for (int i = 0; i < diff; i++)
            X &= (X - 1);

        // Return the required number
        return X;
    }

    // Driver code
    public static void Main()
    {
        int X = 21, K = 2;
        Console.WriteLine(greatestKBits(X, K));

    }
}

// This code is contributed by Ryuga
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to get no of set
// bits in binary representation
// of positive integer n
function countSetBits( n)
{
    let count = 0;
    while (n > 0)
    {
        count += n & 1;
        n >>= 1;
    }
    return count;
}

// Function to return the greatest number <= X
// having at most K set bits.
function greatestKBits( X, K)
{
    let set_bit_count = countSetBits(X);
    if (set_bit_count <= K)
    return X;

    // Remove rightmost set bits one
    // by one until we count becomes k
    let diff = set_bit_count - K;
    for (let i = 0; i < diff; i++)
        X &= (X - 1);

    // Return the required number
    return X;
}

// Driver Code

let X = 21, K = 2;
document.write(greatestKBits(X, K));

</script>
```

**Output:** 

```
20
```