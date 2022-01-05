# 包含 2 的幂的数组，其异或和元素之和等于 X

> 原文:[https://www . geesforgeks . org/包含 2 的幂的数组，其元素的异或和等于-x/](https://www.geeksforgeeks.org/array-containing-power-of-2-whose-xor-and-sum-of-elements-equals-x/)

给定一个整数 **X** 。任务是找到并返回包含 **2 的**的幂的数组，数组的异或是 **X** 。
**举例:**

> **输入:** X = 20
> **输出:** 16 4
> **输入:** X = 15
> **输出:** 1 2 4 8

**方法:**答案在于数字 x 的二进制表示法。
因为在 2 的幂中，只有一个设定位。如果存在两个不同的 2 的幂，那么异或就是两个数的和。
同样，如果对整个数组进行异或运算，那么它应该等于 **X** ，这将是该数的二进制表示。
由于在 **2 的每一次幂**中有一个不同的设置位，所以异或和数组元素的和将是相同的。
以下是上述方法的实施:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the required array
vector<long> getArray(int n)
{
    vector<long> ans;

    // Store the power of 2
    long p2 = 1;

    // while n is greater than 0
    while (n > 0) {

        // if there is 1 in binary
        // representation
        if (n & 1)
            ans.push_back(p2);

        // Divide n by 2
        // Multiply p2 by 2
        n >>= 1;
        p2 *= 2;
    }

    return ans;
}

// Driver code
int main()
{
    long n = 15;

    // Get the answer
    vector<long> ans = getArray(n);

    // Printing the array
    for(int i : ans)
        cout << i << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation implementation
// of the above approach
import java.util.*;
class GFG
{

// Function to return the required array
static Vector<Long> getArray(int n)
{
    Vector<Long> ans = new Vector<Long>();

    // Store the power of 2
    long p2 = 1;

    // while n is greater than 0
    while (n > 0)
    {

        // if there is 1 in binary
        // representation
        if (n % 2 == 1)
            ans.add(p2);

        // Divide n by 2
        // Multiply p2 by 2
        n >>= 1;
        p2 *= 2;
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int n = 15;

    // Get the answer
    Vector<Long> ans = getArray(n);

    // Printing the array
    for(Long i : ans)
        System.out.print(i + " ");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to return the required array
def getArray(n) :

    ans = [];

    # Store the power of 2
    p2 = 1;

    # while n is greater than 0
    while (n > 0) :

        # if there is 1 in binary
        # representation
        if (n & 1) :
            ans.append(p2);

        # Divide n by 2
        # Multiply p2 by 2
        n >>= 1;
        p2 *= 2;

    return ans;

# Driver code
if __name__ == "__main__" :

    n = 15;

    # Get the answer
    ans = getArray(n);

    # Printing the array
    for i in ans :
        print(i, end = " ");

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to return the required array
static List<long> getArray(int n)
{
    List<long> ans = new List<long>();

    // Store the power of 2
    long p2 = 1;

    // while n is greater than 0
    while (n > 0)
    {

        // if there is 1 in binary
        // representation
        if (n % 2 == 1)
            ans.Add(p2);

        // Divide n by 2
        // Multiply p2 by 2
        n >>= 1;
        p2 *= 2;
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int n = 15;

    // Get the answer
    List<long> ans = getArray(n);

    // Printing the array
    foreach(long i in ans)
        Console.Write(i + " ");
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

// Function to return the required array
function getArray(n)
{
    let ans = [];

    // Store the power of 2
    let p2 = 1;

    // while n is greater than 0
    while (n > 0) {

        // if there is 1 in binary
        // representation
        if (n & 1)
            ans.push(p2);

        // Divide n by 2
        // Multiply p2 by 2
        n >>= 1;
        p2 *= 2;
    }

    return ans;
}

// Driver code
    let n = 15;

    // Get the answer
    let ans = getArray(n);

    // Printing the array
    for(let i = 0; i < ans.length; i++)
        document.write(ans[i] + " ");

</script>
```

**Output:** 

```
1 2 4 8 
```

时间复杂度:0(n)

辅助空间:O(n)