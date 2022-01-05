# 安全警报开始的最短剩余时间

> 原文:[https://www . geeksforgeeks . org/安全警报启动剩余时间最小值/](https://www.geeksforgeeks.org/minimum-time-remaining-for-safety-alarm-to-start/)

极客正在组织一场与 **N** 车手的自行车比赛。 **i <sup>th</sup> 机车**的初始速度用 **H <sub>i</sub> Km/hr** 表示，而 **i <sup>th</sup> 机车**的加速度为**A<sub>I</sub>Km/Hr<sup>2</sup>T19】。速度为**‘L’**或更高的摩托车手被认为是速度快的摩托车手。每一小时赛道上的总速度是通过将每一个骑快车的人在那个小时的速度相加计算出来的。当赛道上的总速度为**‘M’**公里每小时或以上时，安全警报开启。任务是找到安全警报开始的最小小时数。**

**示例:**

> **输入:** N = 3，M = 400，L = 120，H = {20，50，20}，A = {20，70，90}
> **输出:** 3
> **解释:**
> 第一小时所有骑行者的速度:
> 自行车 R1 =【20 40 60 80 100】
> 自行车 R2 =【50 120 190 260 330】
> 
> 赛道上的初始速度= 0，因为骑车人的速度都不够快。
> 第 1 小时后赛道上的速度= 120。
> 第 2 小时后赛道上的速度= 190 + 200 = 390。
> 第 3 小时后赛道上的速度= 260 + 290。
> 第 3 小时开始报警。
> 
> **输入:** N = 2，M = 60，L = 120，H = {50，30}，A = {20，40 }
> T3】输出: 3

**方法:**给定的问题可以通过使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)来解决，通过使用以下事实:如果自行车具有初始速度 **U** 并且具有均匀加速度 **A** ，则可以使用等式: **(V = U + A*t)** 来找到任意时间点的速度，并且如果在时间 **t** 条件满足，则一直大于 **t** 的条件将满足，因此丢弃该问题按照以下步骤解决问题:

*   定义一个[功能](https://www.geeksforgeeks.org/functions-in-c/) **检查(长 H[]，长 A[]，长中，长 N，长 M，长 L)** 并执行以下步骤:
    *   初始化变量，将**总和**设为存储速度总和的 **0** 。
    *   [使用变量 **i** 迭代一个范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，如果**(中间*A[i] + H[i])** 的值至少为****L**，则将该值加到**和**上。**
    *   **执行上述步骤后，返回**和**的值作为结果。**
*   **初始化变量，说**低**为 **0** 、**高**为 **10 <sup>10</sup>** 为答案的[二分搜索法](https://www.geeksforgeeks.org/binary-search/)的范围， **ans** 为存储最小小时数的 **0** 。**
*   **重复直到**低< =高**并执行以下步骤:

    *   求**中间**的值为**(低+高)/2** 。
    *   调用[函数](https://www.geeksforgeeks.org/functions-in-c/) **检查(H、A、mid、N、M、L)** ，如果该函数返回的值至少为**M**，则将 **ans** 的值更新为 **mid** 。否则，将**高值**更新为**(中-1)**。
    *   否则，将**低**的值更新为**(中+ 1)** 。** 
*   **执行上述步骤后，打印**和**的值作为小时数。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if the value of
// mid as the minimum number of hours
// satisfies the condition
long check(long H[], long A[], long mid,
           long N, long M, long L)
{
    // Stores the sum of speed
    long sum = 0;

    // Iterate over the range [0, N]
    for (long i = 0; i < N; i++) {

        // Find the value of speed
        long speed = mid * A[i] + H[i];

        // If the bike is considered
        // to be fast add it in sum
        if (speed >= L) {
            sum += speed;
        }
    }

    // Return the resultant sum
    return sum;
}

// Function to find the minimum number
// of time required
long buzzTime(long N, long M, long L,
              long H[], long A[])
{
    // Stores the range of Binary Search
    long low = 0, high = 1e10;

    // Stores the minimum number of
    // time required
    long ans = 0;

    while (high >= low) {

        // Find the value of mid
        long mid = low + (high - low) / 2;

        // If the mid is the resultant
        // speed required
        if (check(H, A, mid,
                  N, M, L)
            >= M) {

            // Update the ans and high
            ans = mid;
            high = mid - 1;
        }

        // Otherwise
        else
            low = mid + 1;
    }

    // Return the minimum number of hours
    return ans;
}

// Driver Code
int main()
{
    long M = 400, L = 120;
    long H[] = { 20, 50, 20 };
    long A[] = { 20, 70, 90 };
    long N = sizeof(A) / sizeof(A[0]);

    cout << buzzTime(N, M, L, H, A);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.io.*;

class GFG
{

  // Function to check if the value of
  // mid as the minimum number of hours
  // satisfies the condition
  static long check(long H[], long A[], long mid,
                    long N, long M, long L)
  {

    // Stores the sum of speed
    long sum = 0;

    // Iterate over the range [0, N]
    for (long i = 0; i < N; i++) {

      // Find the value of speed
      long speed = mid * A[(int) i] + H[(int) i];

      // If the bike is considered
      // to be fast add it in sum
      if (speed >= L) {
        sum += speed;
      }
    }

    // Return the resultant sum
    return sum;
  }

  // Function to find the minimum number
  // of time required
  static long buzzTime(long N, long M, long L,
                       long H[], long A[])
  {
    // Stores the range of Binary Search
    long low = 0, high = 100000000;

    // Stores the minimum number of
    // time required
    long ans = 0;

    while (high >= low) {

      // Find the value of mid
      long mid = low + (high - low) / 2;

      // If the mid is the resultant
      // speed required
      if (check(H, A, mid,
                N, M, L)
          >= M) {

        // Update the ans and high
        ans = mid;
        high = mid - 1;
      }

      // Otherwise
      else
        low = mid + 1;
    }

    // Return the minimum number of hours
    return ans;
  }

  // Driver Code
  public static void main (String[] args) {
    long M = 400, L = 120;
    long H[] = { 20, 50, 20 };
    long A[] = { 20, 70, 90 };
    long N = A.length;

    System.out.println(buzzTime(N, M, L, H, A));
  }
}

// This code is contributed by Potta Lokesh
```

## **蟒蛇 3**

```
# Python 3 program for the above approach

# Function to check if the value of
# mid as the minimum number of hours
# satisfies the condition
def check(H, A, mid, N, M, L):
    # Stores the sum of speed
    sum = 0

    # Iterate over the range [0, N]
    for i in range(N):
        # Find the value of speed
        speed = mid * A[i] + H[i]

        # If the bike is considered
        # to be fast add it in sum
        if (speed >= L):
            sum += speed

    # Return the resultant sum
    return sum

# Function to find the minimum number
# of time required
def buzzTime(N, M, L, H, A):
    # Stores the range of Binary Search
    low = 0
    high = 1e10

    # Stores the minimum number of
    # time required
    ans = 0

    while (high >= low):

        # Find the value of mid
        mid = low + (high - low) // 2

        # If the mid is the resultant
        # speed required
        if (check(H, A, mid, N, M, L) >= M):
            # Update the ans and high
            ans = mid
            high = mid - 1

        # Otherwise
        else:
            low = mid + 1

    # Return the minimum number of hours
    return int(ans)

# Driver Code
if __name__ == '__main__':
    M = 400
    L = 120
    H = [20, 50, 20]
    A = [20, 70, 90]
    N = len(A)

    print(buzzTime(N, M, L, H, A))

    # This code is contributed by ipg2016107.
```

## **C#**

```
// C# program for the above approach
using System;

class GFG{

// Function to check if the value of
// mid as the minimum number of hours
// satisfies the condition
static long check(long []H, long []A, long mid,
                  long N, long M, long L)
{

    // Stores the sum of speed
    long sum = 0;

    // Iterate over the range [0, N]
    for(long i = 0; i < N; i++)
    {

        // Find the value of speed
        long speed = mid * A[(int) i] + H[(int) i];

        // If the bike is considered
        // to be fast add it in sum
        if (speed >= L)
        {
            sum += speed;
        }
    }

    // Return the resultant sum
    return sum;
}

// Function to find the minimum number
// of time required
static long buzzTime(long N, long M, long L,
                     long []H, long []A)
{

    // Stores the range of Binary Search
    long low = 0, high = 100000000;

    // Stores the minimum number of
    // time required
    long ans = 0;

    while (high >= low)
    {

        // Find the value of mid
        long mid = low + (high - low) / 2;

        // If the mid is the resultant
        // speed required
        if (check(H, A, mid, N, M, L) >= M)
        {

            // Update the ans and high
            ans = mid;
            high = mid - 1;
        }

        // Otherwise
        else
            low = mid + 1;
    }

    // Return the minimum number of hours
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    long M = 400, L = 120;
    long []H = { 20, 50, 20 };
    long []A = { 20, 70, 90 };
    long N = A.Length;

    Console.Write(buzzTime(N, M, L, H, A));
}
}

// This code is contributed by shivanisinghss2110
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

// Function to check if the value of
// mid as the minimum number of hours
// satisfies the condition
function check(H, A, mid, N, M, L)
{

    // Stores the sum of speed
    let sum = 0;

    // Iterate over the range [0, N]
    for (let i = 0; i < N; i++) {

        // Find the value of speed
        let speed = mid * A[i] + H[i];

        // If the bike is considered
        // to be fast add it in sum
        if (speed >= L) {
            sum += speed;
        }
    }

    // Return the resultant sum
    return sum;
}

// Function to find the minimum number
// of time required
function buzzTime(N, M, L, H, A)
{

    // Stores the range of Binary Search
    let low = 0, high = 1e10;

    // Stores the minimum number of
    // time required
    let ans = 0;

    while (high >= low) {

        // Find the value of mid
        let mid = Math.floor(low + (high - low) / 2);

        // If the mid is the resultant
        // speed required
        if (check(H, A, mid, N, M, L)
            >= M) {

            // Update the ans and high
            ans = mid;
            high = mid - 1;
        }

        // Otherwise
        else
            low = mid + 1;
    }

    // Return the minimum number of hours
    return ans;
}

// Driver Code
    let M = 400, L = 120;
    let H = [ 20, 50, 20 ];
    let A = [ 20, 70, 90 ];
    let N = A.length;

    document.write(buzzTime(N, M, L, H, A));

    // This code is contributed by _saurabh_jaiswal.
</script>
```

****Output:** 

```
3
```** 

*****时间复杂度:** O(N*log(max(L，M)))*
***辅助空间:** O(1)***