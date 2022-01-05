# 检查数字 N 是否可以表示为 3、5、7 的倍数之和

> 原文:[https://www . geesforgeks . org/check-if-a-number-n-可表示为 3-5 和-7 的倍数之和/](https://www.geeksforgeeks.org/check-if-a-number-n-can-be-represented-as-a-sum-of-multiples-of-3-5-and-7/)

给定一个[非负整数](https://www.geeksforgeeks.org/smallest-missing-non-negative-integer-upto-every-array-index/) **N** ，任务是检查该整数是否可以表示为 3、5 和 7 的倍数之和，并打印它们各自的值。如果任务无法完成，则打印-1。

**示例:**

> **输入:** 10
> **输出:** 1 0 1
> **说明:** 10 可以表示为:(3 * 1) + (5 * 0) + (7 * 1) = 10。其他有效表示为(3 * 0) + (5 * 2) + (7 * 0)
> 
> **输入:** 4
> **输出:** -1
> **解释** : 4 不能表示为 3、5、7 的倍数之和。

**天真方法:**给定的问题可以通过使用三个嵌套 for 循环来解决，迭代 3、5 和 7 的倍数，并跟踪是否存在和为 n 的组合。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <iostream>
using namespace std;

// Function to check if a number can
// be represented as summation of the
// multiples of 3, 5 and 7
void check357(int N)
{
    // flag indicates if combination
    // is possible or not
    int flag = 0;

    // Loop for multiples of 3
    for (int i = 0; i <= N / 3; i++) {

        if (flag == 1)
            break;

        // Loop for multiples of 5
        for (int j = 0; j <= N / 5; j++) {

            if (flag == 1)
                break;

            // Loop for multiples of 7
            for (int k = 0; k <= N / 7; k++) {

                // If sum is N
                if (3 * i + 5 * j + 7 * k == N) {

                    // Combination found
                    flag = 1;

                    // Print Answer
                    cout << i << " "
                         << j << " " << k;
                    break;
                }
            }
        }
    }

    // No valid combination found
    if (flag == 0)
        cout << -1;
}

// Driver code
int main()
{
    int N = 10;
    check357(N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.io.*;

class GFG
{

  // Function to check if a number can
  // be represented as summation of the
  // multiples of 3, 5 and 7
  static void check357(int N)
  {

    // flag indicates if combination
    // is possible or not
    int flag = 0;

    // Loop for multiples of 3
    for (int i = 0; i <= N / 3; i++) {

      if (flag == 1)
        break;

      // Loop for multiples of 5
      for (int j = 0; j <= N / 5; j++) {

        if (flag == 1)
          break;

        // Loop for multiples of 7
        for (int k = 0; k <= N / 7; k++) {

          // If sum is N
          if (3 * i + 5 * j + 7 * k == N) {

            // Combination found
            flag = 1;

            // Print Answer
            System.out.print(i + " " + j + " "
                             + k);
            break;
          }
        }
      }
    }

    // No valid combination found
    if (flag == 0)
      System.out.println(-1);
  }

  // Driver code
  public static void main(String[] args)
  {
    int N = 10;
    check357(N);
  }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python implementation of the above approach

# Function to check if a number can
# be represented as summation of the
# multiples of 3, 5 and 7
def check357(N):

  # flag indicates if combination
  # is possible or not
  flag = 0;

  # Loop for multiples of 3
  for i in range((N // 3) + 1): 

    if (flag == 1):
      break;

    # Loop for multiples of 5
    for j in range((N // 5) + 1):

      if (flag == 1):
        break;

      # Loop for multiples of 7
      for k in range((N // 7) + 1):

        # If sum is N
        if (3 * i + 5 * j + 7 * k == N):

          # Combination found
          flag = 1;

          # Print Answer
          print(f"{i} {j} {k}");
          break;

  # No valid combination found
  if (flag == 0):
    print(-1);

# Driver code
N = 10;
check357(N);

# This code is contributed by saurabh_jaiswal.
```

## C#

```
// C# code for the above approach
using System;

public class GFG
{

  // Function to check if a number can
  // be represented as summation of the
  // multiples of 3, 5 and 7
  static void check357(int N)
  {

    // flag indicates if combination
    // is possible or not
    int flag = 0;

    // Loop for multiples of 3
    for (int i = 0; i <= N / 3; i++) {

      if (flag == 1)
        break;

      // Loop for multiples of 5
      for (int j = 0; j <= N / 5; j++) {

        if (flag == 1)
          break;

        // Loop for multiples of 7
        for (int k = 0; k <= N / 7; k++) {

          // If sum is N
          if (3 * i + 5 * j + 7 * k == N) {

            // Combination found
            flag = 1;

            // Print Answer
            Console.Write(i + " " + j + " " + k);
            break;
          }
        }
      }
    }

    // No valid combination found
    if (flag == 0)
      Console.WriteLine(-1);
  }

  // Driver code
  public static void Main(string[] args)
  {
    int N = 10;
    check357(N);
  }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

// Function to check if a number can
// be represented as summation of the
// multiples of 3, 5 and 7
function check357(N)
{

  // flag indicates if combination
  // is possible or not
  let flag = 0;

  // Loop for multiples of 3
  for (let i = 0; i <= Math.floor(N / 3); i++) {

    if (flag == 1)
      break;

    // Loop for multiples of 5
    for (let j = 0; j <= Math.floor(N / 5); j++) {

      if (flag == 1)
        break;

      // Loop for multiples of 7
      for (let k = 0; k <= Math.floor(N / 7); k++) {

        // If sum is N
        if (3 * i + 5 * j + 7 * k == N) {

          // Combination found
          flag = 1;

          // Print Answer
          document.write(i + " " + j + " " + k);
          break;
        }
      }
    }
  }

  // No valid combination found
  if (flag == 0)
    document.write(-1);
}

// Driver code
let N = 10;
check357(N);

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output**

```
0 2 0
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**有效方法:**给定的问题可以用[数学](https://www.geeksforgeeks.org/what-is-the-importance-of-mathematics-in-computer-science/)来解决。
因为每个数字都可以用 3 的倍数来表示，比如 3x、3x+1 或 3x+2。利用这个事实，我们可以说 5 可以用 3x+2 的形式表示，7 可以用 3x+1 的形式表示。
借助这个观察， **N** 可以用 **3** 以下方式表示:

*   如果 **N** 是 **3x** 的形式，可以表示为 **3x** 。
*   如果 **N** 是 **3x + 1** 的形式，
    *   如果 **N > 7** ，那么 N 可以表示为**3 *(x–2)+7**作为 **7** 类似于到 **3*2 + 1** 。
    *   否则如果 **N < = 7** ，则不能以给定的形式表示。
*   如果 **N** 是 **3n + 2** 的形式，
    *   如果 **N > 5** ，那么 N 可以表示为 **3x + 5** 作为 **5** 类似于到 **3*1 + 2** 。
    *   否则如果 **N < = 5** ，则不能以给定的形式表示。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if a number can be
// represented as summation of multiples
// of 3, 5 and 7
int check357(int N)
{
    // Stores if a valid
    // combination exists
    int f = 0;

    // if N is of the form 3n
    if (N % 3 == 0)
        return (N / 3) * 100 + 0 * 10 + 0;

    else if (N % 3 == 1) {

        // if N is of the form 3n + 1
        if (N - 7 >= 0)
            return ((N - 7) / 3) * 100 + 0 * 10 + 1;
    }
    else

        // if N is of the form 3n + 2
        if (N - 5 >= 0)
        return ((N - 5) / 3) * 100 + 1 * 10 + 0;

    // If no valid combinations exists
    return -1;
}

// Driver code
int main()
{
    int N = 10;
    cout << check357(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;
public class GFG
{

// Function to check if a number can be
// represented as summation of multiples
// of 3, 5 and 7
static int check357(int N)
{

    // Stores if a valid
    // combination exists
    int f = 0;

    // if N is of the form 3n
    if (N % 3 == 0)
        return (N / 3) * 100 + 0 * 10 + 0;

    else if (N % 3 == 1) {

        // if N is of the form 3n + 1
        if (N - 7 >= 0)
            return ((N - 7) / 3) * 100 + 0 * 10 + 1;
    }
    else

        // if N is of the form 3n + 2
        if (N - 5 >= 0)
        return ((N - 5) / 3) * 100 + 1 * 10 + 0;

    // If no valid combinations exists
    return -1;
}

// Driver code
public static void main(String args[])
{
    int N = 10;
    System.out.print(check357(N));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python implementation of the above approach

# Function to check if a number can be
# represented as summation of multiples
# of 3, 5 and 7
def check357(N):

    # Stores if a valid
    # combination exists
    f = 0;

    # if N is of the form 3n
    if (N % 3 == 0):
        return (N // 3) * 100 + 0 * 10 + 0;

    elif (N % 3 == 1):

        # if N is of the form 3n + 1
        if (N - 7 >= 0):
            return ((N - 7) // 3) * 100 + 0 * 10 + 1;
    else:
        if(N - 5 >= 0):
            # if N is of the form 3n + 2
            return ((N - 5) // 3) * 100 + 1 * 10 + 0;
    # If no valid combinations exists
    return -1;

# Driver code
if __name__ == '__main__':
    N = 10;
    print(check357(N));

# This code is contributed by shikhasingrajput
```

## C#

```
// C# implementation of the above approach
using System;
class GFG
{
// Function to check if a number can be
// represented as summation of multiples
// of 3, 5 and 7
static int check357(int N)
{
    // Stores if a valid
    // combination exists
    int f = 0;

    // if N is of the form 3n
    if (N % 3 == 0)
        return (N / 3) * 100 + 0 * 10 + 0;

    else if (N % 3 == 1) {

        // if N is of the form 3n + 1
        if (N - 7 >= 0)
            return ((N - 7) / 3) * 100 + 0 * 10 + 1;
    }
    else

        // if N is of the form 3n + 2
        if (N - 5 >= 0)
        return ((N - 5) / 3) * 100 + 1 * 10 + 0;

    // If no valid combinations exists
    return -1;
}

// Driver code
public static void Main()
{
    int N = 10;
    Console.Write(check357(N));
}
}
// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

// Function to check if a number can be
// represented as summation of multiples
// of 3, 5 and 7
function check357(N)
{

    // Stores if a valid
    // combination exists
    let f = 0;

    // if N is of the form 3n
    if (N % 3 == 0)
        return (N / 3) * 100 + 0 * 10 + 0;

    else if (N % 3 == 1) {

        // if N is of the form 3n + 1
        if (N - 7 >= 0)
            return ((N - 7) / 3) * 100 + 0 * 10 + 1;
    }
    else

        // if N is of the form 3n + 2
        if (N - 5 >= 0)
            return ((N - 5) / 3) * 100 + 1 * 10 + 0;

    // If no valid combinations exists
    return -1;
}

// Driver code
let N = 10;
document.write(check357(N));

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
101
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)