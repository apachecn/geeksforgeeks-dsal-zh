# 通过最小步长加 1 或乘 2 将 0 转换为 N

> 原文:[https://www . geesforgeks . org/convert-0-n-by-add-1-or-乘-2-in-mini-steps/](https://www.geeksforgeeks.org/convert-0-to-n-by-adding-1-or-multiplying-by-2-in-minimum-steps/)

给定一个正整数 **N** ，任务是找到将数字 **0** 转换为 **N** 所需的最小加法运算数，这样在每个运算中，任何数字都可以**乘以 2** 或**将值 1 加到其上**。

**示例:**

> **输入:** N = 6
> **输出:** 1
> **解释:**
> 以下是将 0 转换为 6 的操作:
> 加 1–>0+1 = 1。
> 乘以 2–>1 * 2 = 2。
> 加 1–>2+1 = 3。
> 乘以 2–>3 * 2 = 6。
> 因此加法运算次数= 2。
> 
> **输入:**N = 3
> T3】输出: 2

**方法:**这个问题可以通过[位操作](https://www.geeksforgeeks.org/bits-manipulation-important-tactics/)技术来解决。在 **N** 的二进制数表示中，每当 **N** 变得奇数时(即 **N** 的[最低有效位被置位](https://www.geeksforgeeks.org/unset-least-significant-k-bits-of-a-given-number/)，则执行**加法运算**。否则，**乘以 2** 。给定问题的最终逻辑是[找到 N](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/) 中的设定位数。

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count number of
// set bits in N
int minimumAdditionOperation(
    unsigned long long int N)
{

    // Stores the count of set bits
    int count = 0;

    while (N) {

        // If N is odd, then it
        // a set bit
        if (N & 1 == 1) {
            count++;
        }
        N = N >> 1;
    }

    // Return the result
    return count;
}

// Driver Code
int main()
{
    int N = 6;
    cout << minimumAdditionOperation(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG {

    // Function to count number of
    // set bits in N
    static int minimumAdditionOperation(int N)
    {

        // Stores the count of set bits
        int count = 0;

        while (N > 0) {

            // If N is odd, then it
            // a set bit
            if (N % 2 == 1) {
                count++;
            }
            N = N >> 1;
        }

        // Return the result
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 6;
        System.out.println(minimumAdditionOperation(N));
    }
}

// This code is contributed by dwivediyash
```

## 蟒蛇 3

```
# python program for above approach

# Function to count number of
# set bits in N
def minimumAdditionOperation(N):

    # Stores the count of set bits
    count = 0

    while (N):

        # If N is odd, then it
        # a set bit
        if (N & 1 == 1):
            count += 1

        N = N >> 1

    # Return the result
    return count

# Driver Code
if __name__ == "__main__":

    N = 6
    print(minimumAdditionOperation(N))

    # This code is contributed by rakeshsahni.
```

## C#

```
// C# program for above approach
using System;
public class GFG{

    // Function to count number of
    // set bits in N
    static int minimumAdditionOperation(int N)
    {

        // Stores the count of set bits
        int count = 0;

        while (N != 0) {

            // If N is odd, then it
            // a set bit
            if ((N & 1) == 1) {
                count++;
            }
            N = N >> 1;
        }

        // Return the result
        return count;
    }

    // Driver Code
    static public void Main (){
        int N = 6;
        Console.Write(minimumAdditionOperation(N));

    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// Javascript program for above approach

// Function to count number of
// set bits in N
function minimumAdditionOperation(N)
{

  // Stores the count of set bits
  let count = 0;

  while (N)
  {

    // If N is odd, then it
    // a set bit
    if (N & (1 == 1)) {
      count++;
    }
    N = N >> 1;
  }

  // Return the result
  return count;
}

// Driver Code
let N = 6;
document.write(minimumAdditionOperation(N));

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*