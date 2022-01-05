# 第 Kth 位被置位的超过 N 的最小数

> 原文:[https://www . geeksforgeeks . org/最小超出数-n-其-kth-bit-被设置/](https://www.geeksforgeeks.org/smallest-number-exceeding-n-whose-kth-bit-is-set/)

给定两个整数 **N** 和 **K** ，任务是找到大于 **N** 的最小数，其二进制表示中的**K**位被设置。

**示例:**

> **输入:** N = 15，K = 2
> **输出:** 20
> **解释:**
> (20)<sub>10</sub>的二进制表示为(10100) <sub>2</sub> 。从左数的 2 <sup>nd</sup> 位( *0 基分度*)设置在(20) <sub>10</sub> 中。因此，20 是设置了 2 <sup>和</sup>位的大于 15 的最小数字。
> 
> **输入:** N = 16，K = 3
> T3】输出: 24

**简单方法:**最简单的方法是遍历从 **N + 1** 开始的所有数字，并检查每个数字的 **K <sup>第</sup>** 位是否置位。如果找到这样的号码，那么打印该号码。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include "bits/stdc++.h"
using namespace std;

// Function to find the number greater
// than n whose Kth bit is set
int find_next(int n, int k)
{
    // Iterate from N + 1
    int M = n + 1;

    while (1) {

        // Check if Kth bit is
        // set or not
        if (M & (1ll << k))
            break;

        // Increment M for next number
        M++;
    }

    // Return the minimum value
    return M;
}

// Driver Code
int main()
{
    // Given N and K
    int N = 15, K = 2;

    // Function Call
    cout << find_next(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{

// Function to find the number greater
// than n whose Kth bit is set
static int find_next(int n, int k)
{
  // Iterate from N + 1
  int M = n + 1;

  while (true)
  {
    // Check if Kth bit is
    // set or not
    if ((M & (1L << k)) > 0)
      break;

    // Increment M for
    // next number
    M++;
  }

  // Return the minimum value
  return M;
}

// Driver Code
public static void main(String[] args)
{
  // Given N and K
  int N = 15, K = 2;

  // Function Call
  System.out.print(find_next(N, K));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to find the number
# greater than n whose Kth
# bit is set
def find_next(n, k):

    # Iterate from N + 1
    M = n + 1;

    while (True):

        # Check if Kth bit is
        # set or not
        if ((M & (1 << k)) > 0):
            break;

        # Increment M for
        # next number
        M += 1;

    # Return the
    # minimum value
    return M;

# Driver Code
if __name__ == '__main__':

    # Given N and K
    N = 15; K = 2;

    # Function Call
    print(find_next(N, K));

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function to find the
// number greater than n
// whose Kth bit is set
static int find_next(int n, int k)
{
  // Iterate from N + 1
  int M = n + 1;

  while (true)
  {
    // Check if Kth bit is
    // set or not
    if ((M & (1L << k)) > 0)
      break;

    // Increment M for
    // next number
    M++;
  }

  // Return the minimum value
  return M;
}

// Driver Code
public static void Main(String[] args)
{
  // Given N and K
  int N = 15, K = 2;

  // Function Call
  Console.Write(find_next(N, K));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

 // Function to find the number greater
// than n whose Kth bit is set
function find_next(n, k)
{
  // Iterate from N + 1
  let M = n + 1;

  while (true)
  {
    // Check if Kth bit is
    // set or not
    if ((M & (1 << k)) > 0)
      break;

    // Increment M for
    // next number
    M++;
  }

  // Return the minimum value
  return M;
}

// Driver Code

     // Given N and K
  let N =  15, K = 2;

  // Function Call
  document.write(find_next(N, K));

 // This code is contributed by avijitmondal1998.
</script>
```

**Output**

```
20
```

***时间复杂度:**O(2<sup>K</sup>)*
***辅助空间:** O(1)*

**高效方法:**要优化上述方法，存在两种可能性:

1.  **K <sup>第</sup>位未置位:**观察位置大于 **K** 的位不受影响。因此，使 **K <sup>第</sup>** 位置位，并使其左侧的所有位 **0** 。
2.  **K <sup>第</sup>位被置位:**找到[第一个最低有效未置位位](https://www.geeksforgeeks.org/unset-least-significant-k-bits-of-a-given-number/)并置位。之后，取消设置它右边的所有位。

按照以下步骤解决问题:

1.  检查是否设置了 **N** 的 **K <sup>第</sup>T3】位。如果发现为真，则找到最低的未置位位并置位，将其右侧的所有位更改为 **0** 。**
2.  否则，设置 **K <sup>第</sup>** 位，并将所有低于 **K** 的位更新为 **0** 。
3.  完成以上步骤后打印答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include "bits/stdc++.h"
using namespace std;

// Function to find the number greater
// than n whose Kth bit is set
int find_next(int n, int k)
{
    // Stores the resultant number
    int ans = 0;

    // If Kth bit is not set
    if ((n & (1ll << k)) == 0) {
        int cur = 0;

        // cur will be the sum of all
        // powers of 2 < k
        for (int i = 0; i < k; i++) {

            // If the current bit is set
            if (n & (1ll << i))
                cur += 1ll << i;
        }

        // Add Kth power of 2 to n and
        // subtract the all powers of 2
        // less than K that are set
        ans = n - cur + (1ll << k);
    }

    // If the kth bit is set
    else {
        int first_unset_bit = -1, cur = 0;

        for (int i = 0; i < 64; i++) {

            // First unset bit position
            if ((n & (1ll << i)) == 0) {
                first_unset_bit = i;
                break;
            }

            // sum of bits that are set
            else
                cur += (1ll << i);
        }

        // Add Kth power of 2 to n and
        // subtract the all powers of 2
        // less than K that are set
        ans = n - cur
              + (1ll << first_unset_bit);

        // If Kth bit became unset
        // then set it again
        if ((ans & (1ll << k)) == 0)
            ans += (1ll << k);
    }

    // Return the resultant number
    return ans;
}

// Driver Code
int main()
{
    int N = 15, K = 2;

    // Print ans
    cout << find_next(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{

// Function to find the number
// greater than n whose Kth
// bit is set
static int find_next(int n,
                     int k)
{
  // Stores the resultant
  // number
  int ans = 0;

  // If Kth bit is not set
  if ((n & (1L << k)) == 0)
  {
    int cur = 0;

    // cur will be the sum of all
    // powers of 2 < k
    for (int i = 0; i < k; i++)
    {
      // If the current bit is set
      if ((n & (1L << i)) > 0)
        cur += 1L << i;
    }

    // Add Kth power of 2 to n and
    // subtract the all powers of 2
    // less than K that are set
    ans = (int)(n - cur + (1L << k));
  }

  // If the kth bit is set
  else
  {
    int first_unset_bit = -1, cur = 0;

    for (int i = 0; i < 64; i++)
    {
      // First unset bit position
      if ((n & (1L << i)) == 0)
      {
        first_unset_bit = i;
        break;
      }

      // sum of bits that are set
      else
        cur += (1L << i);
    }

    // Add Kth power of 2 to n and
    // subtract the all powers of 2
    // less than K that are set
    ans = (int)(n - cur +
          (1L << first_unset_bit));

    // If Kth bit became unset
    // then set it again
    if ((ans & (1L << k)) == 0)
      ans += (1L << k);
  }

  // Return the resultant number
  return ans;
}

// Driver Code
public static void main(String[] args)
{
  int N = 15, K = 2;

  // Print ans
  System.out.print(find_next(N, K));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the number greater
# than n whose Kth bit is set
def find_next(n, k):

    # Stores the resultant number
    ans = 0

    # If Kth bit is not set
    if ((n & (1 << k)) == 0):
        cur = 0

        # cur will be the sum of all
        # powers of 2 < k
        for i in range(k):

            # If the current bit is set
            if (n & (1 << i)):
                cur += 1 << i

        # Add Kth power of 2 to n and
        # subtract the all powers of 2
        # less than K that are set
        ans = n - cur + (1 << k)

    # If the kth bit is set
    else:
        first_unset_bit, cur = -1, 0

        for i in range(64):

            # First unset bit position
            if ((n & (1 << i)) == 0):
                first_unset_bit = i
                break

            # Sum of bits that are set
            else:
                cur += (1 << i)

        # Add Kth power of 2 to n and
        # subtract the all powers of 2
        # less than K that are set
        ans = n - cur + (1 << first_unset_bit)

        # If Kth bit became unset
        # then set it again
        if ((ans & (1 << k)) == 0):
            ans += (1 << k)

    # Return the resultant number
    return ans

# Driver code
N, K = 15, 2

# Print ans
print(find_next(N, K))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function to find the number
// greater than n whose Kth
// bit is set
static int find_next(int n,
                     int k)
{
  // Stores the resultant
  // number
  int ans = 0;

  // If Kth bit is not set
  if ((n & (1L << k)) == 0)
  {
    int cur = 0;

    // cur will be the sum of all
    // powers of 2 < k
    for (int i = 0; i < k; i++)
    {
      // If the current bit is set
      if ((n & (1L << i)) > 0)
        cur += (int)1L << i;
    }

    // Add Kth power of 2 to n and
    // subtract the all powers of 2
    // less than K that are set
    ans = (int)(n - cur + (1L << k));
  }

  // If the kth bit is set
  else
  {
    int first_unset_bit = -1, cur = 0;

    for (int i = 0; i < 64; i++)
    {
      // First unset bit position
      if ((n & (1L << i)) == 0)
      {
        first_unset_bit = i;
        break;
      }

      // Sum of bits that are set
      else
        cur +=(int)(1L << i);
    }

    // Add Kth power of 2 to n and
    // subtract the all powers of 2
    // less than K that are set
    ans = (int)(n - cur +
          (1L << first_unset_bit));

    // If Kth bit became unset
    // then set it again
    if ((ans & (1L << k)) == 0)
      ans += (int)(1L << k);
  }

  // Return the resultant number
  return ans;
}

// Driver Code
public static void Main(String[] args)
{
  int N = 15, K = 2;

  // Print ans
  Console.Write(find_next(N, K));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript program for
// the above approach

    // Function to find the number
    // greater than n whose Kth
    // bit is set
    function find_next(n , k) {
        // Stores the resultant
        // number
        var ans = 0;

        // If Kth bit is not set
        if ((n & (1 << k)) == 0) {
            var cur = 0;

            // cur will be the sum of all
            // powers of 2 < k
            for (i = 0; i < k; i++) {
                // If the current bit is set
                if ((n & (1 << i)) > 0)
                    cur += 1 << i;
            }

            // Add Kth power of 2 to n and
            // subtract the all powers of 2
            // less than K that are set
            ans = parseInt( (n - cur + (1 << k)));
        }

        // If the kth bit is set
        else {
            var first_unset_bit = -1, cur = 0;

            for (i = 0; i < 64; i++) {
                // First unset bit position
                if ((n & (1 << i)) == 0) {
                    first_unset_bit = i;
                    break;
                }

                // sum of bits that are set
                else
                    cur += (1 << i);
            }

            // Add Kth power of 2 to n and
            // subtract the all powers of 2
            // less than K that are set
            ans = parseInt( (n - cur + (1 << first_unset_bit)));

            // If Kth bit became unset
            // then set it again
            if ((ans & (1 << k)) == 0)
                ans += (1 << k);
        }

        // Return the resultant number
        return ans;
    }

    // Driver Code

        var N = 15, K = 2;

        // Prvar ans
        document.write(find_next(N, K));

// This code is contributed by umadevi9616
</script>
```

**Output**

```
20
```

***时间复杂度:** O(K)*
***辅助空间:** O(1)*