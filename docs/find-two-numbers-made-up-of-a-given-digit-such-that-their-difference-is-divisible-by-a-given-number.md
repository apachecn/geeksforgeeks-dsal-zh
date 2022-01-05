# 找出由给定数字组成的两个数字，这样它们的差可以被 N 整除

> 原文:[https://www . geesforgeks . org/find-两个数字-由给定的数字组成-这样它们的差可以被给定的数字除尽/](https://www.geeksforgeeks.org/find-two-numbers-made-up-of-a-given-digit-such-that-their-difference-is-divisible-by-a-given-number/)

给定两个数字， **N** 和 **M** ，任务是找到两个由 M 组成的数字作为它的所有数字，这样它们的差可以被 **N** 整除。
**示例:**

> **输入:** N = 8，M = 2
> **输出:** 22 222
> **说明:**222 与 22 (200)之差可被 8 整除
> **输入:** N = 17，M = 6
> **输出:** 6 666666666666666

**方法:**
在这个问题中，我们必须找到仅由一个唯一数字组成的数字。假设 **M** 等于 2，那么我们必须从 2，22，222，2222…这样的数字中找出 A 和 B，以此类推。A 和 B 的差应该可以被 **N** 整除。为了满足这个条件，我们必须选择 A 和 B，这样当 A 和 B 除以 **N** 时，剩下的部分是相同的。
对于长度为 **N+1** 长度的一个数字，仅由一个唯一的数字 **M** 组成，我们将有 **N+1** 个数字。如果我们将这些 **N+1** 数除以 **N** ，我们将得到 **N+1** 余数，其范围为**【0，N】**。由于数字可能超过整数值的范围，我们将数字的余数长度存储为映射中的键值对。一旦余数与映射中已配对的值出现，当前长度和映射长度就是所需数字的长度。
以下代码是上述方法的实现:

## C++

```
// C++ implementation
// of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to implement
// the above approach
void findNumbers(int N, int M)
{
    int m = M;

    // Hashmap to store
    // remainder-length of the
    // number as key-value pairs
    map<int, int> remLen;

    int len, remainder;
    // Iterate till N + 1 length
    for (len = 1; len <= N + 1; ++len) {
        remainder = M % N;
        // Search remainder in the map
        if (remLen.find(remainder)
            == remLen.end())
            // If remainder is not
            // already present insert
            // the length for the
            // corresponding remainder
            remLen[remainder] = len;
        else
            break;

        // Keep increasing M
        M = M * 10 + m;
        // To keep M in range of integer
        M = M % N;
    }
    // Length of one number
    // is the current Length
    int LenA = len;
    // Length of the other number
    // is the length paired with
    // current remainder in map
    int LenB = remLen[remainder];

    for (int i = 0; i < LenB; ++i)
        cout << m;
    cout << " ";
    for (int i = 0; i < LenA; ++i)
        cout << m;

    return;
}

// Driver code
int main()
{
    int N = 8, M = 2;

    findNumbers(N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG{

// Function to implement
// the above approach
static void findNumbers(int N, int M)
{
    int m = M;

    // Hashmap to store
    // remainder-length of the
    // number as key-value pairs
    Map<Integer, Integer> remLen = new HashMap<>();

    int len, remainder = 0;

    // Iterate till N + 1 length
    for(len = 1; len <= N + 1; ++len)
    {
       remainder = M % N;

       // Search remainder in the map
       if (!remLen.containsKey(remainder))
       {

           // If remainder is not
           // already present insert
           // the length for the
           // corresponding remainder
           remLen.put(remainder, len);
       }
       else
       {
           break;
       }

       // Keep increasing M
       M = M * 10 + m;

       // To keep M in range of integer
       M = M % N;
    }

    // Length of one number
    // is the current Length
    int LenA = len;

    // Length of the other number
    // is the length paired with
    // current remainder in map
    int LenB = remLen.getOrDefault(remainder, 0);

    for(int i = 0; i < LenB; ++i)
       System.out.print(m);
    System.out.print(" ");

    for(int i = 0; i < LenA; ++i)
       System.out.print(m);
}

// Driver code
public static void main(String[] args)
{
    int N = 8, M = 2;

    findNumbers(N, M);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation
# of the above approach

# Function to implement
# the above approach
def findNumbers(N, M):

    m = M

    # Hashmap to store
    # remainder-length of the
    # number as key-value pairs
    remLen = {}

    # Iterate till N + 1 length
    for len1 in range(1, N + 1, 1):
        remainder = M % N

        # Search remainder in the map
        if (remLen.get(remainder) == None):

            # If remainder is not
            # already present insert
            # the length for the
            # corresponding remainder
            remLen[remainder] = len1
        else:
            break

        # Keep increasing M
        M = M * 10 + m

        # To keep M in range of integer
        M = M % N

    # Length of one number
    # is the current Length
    LenA = len1

    # Length of the other number
    # is the length paired with
    # current remainder in map
    LenB = remLen[remainder]

    for i in range(LenB):
        print(m, end = "")
    print(" ", end = "")

    for i in range(LenA):
        print(m, end = "")

    return

# Driver code
if __name__ == '__main__':

    N = 8
    M = 2

    findNumbers(N, M)

# This code is contributed by Bhupendra_Singh
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to implement
// the above approach
static void findNumbers(int N, int M)
{
    int m = M;

    // To store remainder-length of
    // the number as key-value pairs
    Dictionary<int,
               int> remLen = new Dictionary<int,
                                            int>();

    int len, remainder = 0;

    // Iterate till N + 1 length
    for(len = 1; len <= N + 1; ++len)
    {
        remainder = M % N;

        // Search remainder in the map
        if (!remLen.ContainsKey(remainder))
        {

            // If remainder is not
            // already present insert
            // the length for the
            // corresponding remainder
            remLen.Add(remainder, len);
        }
        else
        {
            break;
        }

        // Keep increasing M
        M = M * 10 + m;

        // To keep M in range of integer
        M = M % N;
    }

    // Length of one number
    // is the current Length
    int LenA = len;

    // Length of the other number
    // is the length paired with
    // current remainder in map
    int LenB = remLen[remainder];

    for(int i = 0; i < LenB; ++i)
        Console.Write(m);

    Console.Write(" ");

    for(int i = 0; i < LenA; ++i)
        Console.Write(m);
}

// Driver code
public static void Main(String[] args)
{
    int N = 8, M = 2;

    findNumbers(N, M);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
    // Javascript implementation of the above approach

    // Function to implement
    // the above approach
    function findNumbers(N, M)
    {
        let m = M;

        // To store remainder-length of
        // the number as key-value pairs
        let remLen = new Map();

        let len, remainder = 0;

        // Iterate till N + 1 length
        for(len = 1; len <= N + 1; ++len)
        {
            remainder = M % N;

            // Search remainder in the map
            if (!remLen.has(remainder))
            {

                // If remainder is not
                // already present insert
                // the length for the
                // corresponding remainder
                remLen.set(remainder, len);
            }
            else
            {
                break;
            }

            // Keep increasing M
            M = M * 10 + m;

            // To keep M in range of integer
            M = M % N;
        }

        // Length of one number
        // is the current Length
        let LenA = len;

        // Length of the other number
        // is the length paired with
        // current remainder in map
        let LenB = remLen.get(remainder);

        for(let i = 0; i < LenB; ++i)
            document.write(m);

        document.write(" ");

        for(let i = 0; i < LenA; ++i)
            document.write(m);
    }

    let N = 8, M = 2;

    findNumbers(N, M);

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
22 222
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(1)*