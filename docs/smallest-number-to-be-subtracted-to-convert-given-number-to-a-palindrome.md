# 将给定数字转换为回文所需减去的最小数字

> 原文:[https://www . geesforgeks . org/最小待减数转给定数回文/](https://www.geeksforgeeks.org/smallest-number-to-be-subtracted-to-convert-given-number-to-a-palindrome/)

给定一个整数 **N** ，任务是找到要从 **N** 中减去的最小数，得到一个[回文](https://www.geeksforgeeks.org/tag/palindrome/)。

**示例:**

> **输入:** N = 1000
> **输出:** 1
> **说明:**由于 1000–1 = 999，是回文，所以要减去的最小数是 1。
> 
> **输入:** N = 3456
> **输出:** 13
> **说明:**由于 3456–13 = 3443，是回文，所以要减去的最小数是 13。

**方法:**按照以下步骤解决问题:

1.  从 **N** 迭代到 **0** 。
2.  初始化一个**计数器**。每次迭代时，反转 **N** 的减小值，并将其与 **N** 的当前值进行比较。如果两者相等，打印**计数器**的值。
3.  否则，增加计数器并继续循环直到 **N** 为 **0** 。
4.  打印**计数器**的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to evaluate minimum
// subtraction required to make
// a number palindrome
void minSub(int N)
{

    // Counts number of
    // subtractions required
    int count = 0;

    // Run a loop till N>=0
    while (N >= 0) {

        // Store the current number
        int num = N;

        // Store reverse of current number
        int rev = 0;

        // Reverse the number
        while (num != 0) {
            int digit = num % 10;
            rev = (rev * 10) + digit;
            num = num / 10;
        }

        // Check if N is palindrome
        if (N == rev) {

            break;
        }

        // Increment the counter
        count++;

        // Reduce the number by 1
        N--;
    }

    // Print the result
    cout << count;
}

// Driver Code
int main()
{
    int N = 3456;

    // Function call
    minSub(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

// Function to evaluate minimum
// subtraction required to make
// a number palindrome
static void minSub(int N)
{
  // Counts number of
  // subtractions required
  int count = 0;

  // Run a loop till N>=0
  while (N >= 0)
  {
    // Store the current
    // number
    int num = N;

    // Store reverse of
    // current number
    int rev = 0;

    // Reverse the number
    while (num != 0)
    {
      int digit = num % 10;
      rev = (rev * 10) + digit;
      num = num / 10;
    }

    // Check if N is
    // palindrome
    if (N == rev)
    {
      break;
    }

    // Increment the counter
    count++;

    // Reduce the number
    // by 1
    N--;
  }

  // Print the result
  System.out.print(count);
}

// Driver Code
public static void main(String[] args)
{
  int N = 3456;

  // Function call
  minSub(N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to evaluate minimum
# subtraction required to make
# a number palindrome
def minSub(N):

    # Counts number of
    # subtractions required
    count = 0

    # Run a loop till N>=0
    while (N >= 0):

        # Store the current number
        num = N

        # Store reverse of current number
        rev = 0

        # Reverse the number
        while (num != 0):
            digit = num % 10
            rev = (rev * 10) + digit
            num = num // 10

        # Check if N is palindrome
        if (N == rev):
            break

        # Increment the counter
        count += 1

        # Reduce the number by 1
        N -= 1

    # Print the result
    print(count)

# Driver Code
if __name__ == '__main__':

    N = 3456

    # Function call
    minSub(N)

# This code is contributed by bgangwar59
```

## C#

```
// C# program for the
// above approach
using System;

class GFG{

// Function to evaluate minimum
// subtraction required to make
// a number palindrome
static void minSub(int N)
{

  // Counts number of
  // subtractions required
  int count = 0;

  // Run a loop till N>=0
  while (N >= 0)
  {

    // Store the current
    // number
    int num = N;

    // Store reverse of
    // current number
    int rev = 0;

    // Reverse the number
    while (num != 0)
    {
      int digit = num % 10;
      rev = (rev * 10) + digit;
      num = num / 10;
    }

    // Check if N is
    // palindrome
    if (N == rev)
    {
      break;
    }

    // Increment the counter
    count++;

    // Reduce the number
    // by 1
    N--;
  }

  // Print the result
  Console.Write(count);
}

// Driver Code
public static void Main(String[] args)
{
  int N = 3456;

  // Function call
  minSub(N);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program for the
// above approach

// Function to evaluate minimum
// subtraction required to make
// a number palindrome
function minSub(N)
{

    // Counts number of
    // subtractions required
    let count = 0;

    // Run a loop till N>=0
    while (N >= 0)
    {

        // Store the current
        // number
        let num = N;

        // Store reverse of
        // current number
        let rev = 0;

        // Reverse the number
        while (num != 0)
        {
            let digit = num % 10;
            rev = (rev * 10) + digit;
            num = Math.floor(num / 10);
        }

        // Check if N is
        // palindrome
        if (N == rev)
        {
            break;
        }

        // Increment the counter
        count++;

        // Reduce the number
        // by 1
        N--;
    }

    // Print the result
    document.write(count);
}

// Driver Code
let N = 3456;

// Function call
minSub(N);

// This code is contributed by souravghosh0416

</script>
```

**Output:** 

```
13
```

***时间复杂度:** O(N * K)，其中 K 是整数的位数。*
***辅助空间:** O(1)*