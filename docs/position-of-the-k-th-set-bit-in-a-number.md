# 数字中第 K 个设定位的位置

> 原文:[https://www . geeksforgeeks . org/第 k 组位在数字中的位置/](https://www.geeksforgeeks.org/position-of-the-k-th-set-bit-in-a-number/)

给定两个数字 **N** 和 **K** 。任务是从右边找到数字中第 K 个集合位的索引。
**注**:二进制表示中的索引从右 0 开始。例如，在二进制数“000011”中，第一个设置位位于从右开始的索引 0 处，第二个设置位位于从右开始的索引 1 处。
**示例:**

```
Input: N = 15, K = 3
Output: 2
15 is "1111", hence the third bit is at index 2 from right. 

Input:  N = 19, K = 2
Output: 1
19 is "10011", hence the second set bit is at index 1 from right. 
```

**方法:**初始化一个计数器 0，如果最后一位设置在数字中，则增加该计数器。要访问下一位，请将数字右移 1。当计数器的值等于 K 时，我们返回在每次右移时递增的数字的索引。
以下是上述办法的实施情况:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns the Kth set bit
int FindIndexKthBit(int n, int k)
{
    int cnt = 0;
    int ind = 0;

    // Traverse in the binary
    while (n) {

        // Check if the last
        // bit is set or not
        if (n & 1)
            cnt++;

        // Check if count is equal to k
        // then return the index
        if (cnt == k)
            return ind;

        // Increase the index
        // as we move right
        ind++;

        // Right shift the number by 1
        n = n >> 1;
    }

    return -1;
}

// Driver Code
int main()
{
    int n = 15, k = 3;
    int ans = FindIndexKthBit(n, k);
    if (ans != -1)
        cout << ans;
    else
        cout << "No k-th set bit";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG
{

// Function that returns the Kth set bit
static int FindIndexKthBit(int n, int k)
{
    int cnt = 0;
    int ind = 0;

    // Traverse in the binary
    while (n > 0)
    {

        // Check if the last
        // bit is set or not
        if ((n & 1 ) != 0)
            cnt++;

        // Check if count is equal to k
        // then return the index
        if (cnt == k)
            return ind;

        // Increase the index
        // as we move right
        ind++;

        // Right shift the number by 1
        n = n >> 1;
    }

    return -1;
}

// Driver Code
public static void main(String args[])
{
    int n = 15, k = 3;
    int ans = FindIndexKthBit(n, k);
    if (ans != -1)
        System.out.println(ans);
    else
        System.out.println("No k-th set bit");
}
}

// This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns the Kth set bit
def FindIndexKthBit(n, k):

    cnt, ind = 0, 0

    # Traverse in the binary
    while n > 0:

        # Check if the last
        # bit is set or not
        if n & 1:
            cnt += 1

        # Check if count is equal to k
        # then return the index
        if cnt == k:
            return ind

        # Increase the index
        # as we move right
        ind += 1

        # Right shift the number by 1
        n = n >> 1

    return -1

# Driver Code
if __name__ == "__main__":

    n, k = 15, 3
    ans = FindIndexKthBit(n, k)

    if ans != -1:
        print(ans)
    else:
        print("No k-th set bit")

# This code is contributed by
# Rituraj Jain
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG
{

// Function that returns the Kth set bit
static int FindIndexKthBit(int n, int k)
{
    int cnt = 0;
    int ind = 0;

    // Traverse in the binary
    while (n > 0)
    {

        // Check if the last
        // bit is set or not
        if ((n & 1 ) != 0)
            cnt++;

        // Check if count is equal to k
        // then return the index
        if (cnt == k)
            return ind;

        // Increase the index
        // as we move right
        ind++;

        // Right shift the number by 1
        n = n >> 1;
    }

    return -1;
}

// Driver Code
public static void Main()
{
    int n = 15, k = 3;
    int ans = FindIndexKthBit(n, k);
    if (ans != -1)
        Console.WriteLine(ans);
    else
        Console.WriteLine("No k-th set bit");
}
}

// This code is contributed by
// Code_Mech.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement
// the above approach

// Function that returns the Kth set bit
function FindIndexKthBit($n, $k)
{
    $cnt = 0;
    $ind = 0;

    // Traverse in the binary
    while ($n)
    {

        // Check if the last
        // bit is set or not
        if ($n & 1)
            $cnt++;

        // Check if count is equal to k
        // then return the index
        if ($cnt == $k)
            return $ind;

        // Increase the index
        // as we move right
        $ind++;

        // Right shift the number by 1
        $n = $n >> 1;
    }

    return -1;
}

// Driver Code
$n = 15;
$k = 3;

$ans = FindIndexKthBit($n, $k);

if ($ans != -1)
    echo $ans;
else
    echo "No k-th set bit";

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
    // Javascript program to implement
    // the above approach

    // Function that returns the Kth set bit
    function FindIndexKthBit(n, k)
    {
        let cnt = 0;
        let ind = 0;

        // Traverse in the binary
        while (n > 0) {

            // Check if the last
            // bit is set or not
            if (n & 1 > 0)
                cnt++;

            // Check if count is equal to k
            // then return the index
            if (cnt == k)
                return ind;

            // Increase the index
            // as we move right
            ind++;

            // Right shift the number by 1
            n = n >> 1;
        }

        return -1;
    }

    let n = 15, k = 3;
    let ans = FindIndexKthBit(n, k);
    if (ans != -1)
        document.write(ans);
    else
        document.write("No k-th set bit");

</script>
```

**Output:** 

```
2
```