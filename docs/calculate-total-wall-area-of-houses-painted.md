# 计算粉刷房屋的总墙面积

> 原文:[https://www . geeksforgeeks . org/calculate-total-wall-area-houses-paired/](https://www.geeksforgeeks.org/calculate-total-wall-area-of-houses-painted/)

给定整数 **N，L** 和 **W** 表示每行房屋的行数和长宽，数组**Heights【】**表示每栋房屋的高度，任务是找出相邻房屋共用一面墙时需要粉刷的外墙总面积。

**示例:**

> **输入:** N = 4，W = 1，L = 1，Heights[] = {1，2，3， 4}
> **输出:** 28
> **说明:**
> 房屋-1 粉刷面积= 2 * 1 + 1 * 1 = 3
> 房屋-2 粉刷面积= 2 * 2 + 1 * 1 = 5
> 房屋-3 粉刷面积= 2 * 3 + 1 * 1 = 7
> 房屋-4 粉刷面积= 2 * 4 + 1 * 1 + 1 * 4 = 13
> 因此，总粉刷面积= 28【T11
> 
> **输入:** N = 7，W = 1，L = 1，Heights[] = {4，3，1，2，3，4，2 }
> T3】输出: 52

**方法:**使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。按照以下步骤解决问题:

*   第一栋粉刷房屋的墙体总面积等于 2 * w * h<sub>1</sub>+l *(h<sub>1</sub>+max(0，h<sub>2</sub>–h<sub>1</sub>)。
*   最后粉刷的房屋墙体总面积等于 2 * w * h<sub>n</sub>+l *(h<sub>n</sub>+max(0，h<sub>n</sub>–h<sub>n-1</sub>)。
*   除第一栋和最后一栋房屋外，粉刷房屋的墙壁总面积等于 2 * w * h <sub>i</sub> + l * (max(0，h<sub>I</sub>–h<sub>I+1</sub>)+max(0，h<sub>I</sub>–h<sub>I-1</sub>)。
*   因此，所有粉刷房屋的总面积将使用以下公式计算:

> 总印刷面积= 2 * w(h+【h】+T2【n】)+l(h<sub>【1】</sub>+h<sub>)+l *σABS(h<sub>【I】</sub>)</sub>

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the total area
// of walls painted in N row-houses
void areaToPaint(int N, int W, int L,
                 int Heights[])
{

    // Stores total area of N row-houses
    // that needs to be painted
    int total = 0;

    // Traverse the array of wall heights
    for (int i = 0; i < N; i++) {

        // Update total area painted
        total += 2 * Heights[i] * W;
    }

    // Update total
    total += L * (Heights[0]
                  + Heights[N - 1]);

    // Traverse all the houses and
    // print the shared walls
    for (int i = 1; i < N; i++) {

        // Update total
        total += L * abs(Heights[i]
                         - Heights[i - 1]);
    }

    // Print total area needs to paint
    cout << total;
}

// Driver Code
int main()
{

    // Given N, W & L
    int N = 7, W = 1, L = 1;

    // Given heights of houses
    int Heights[N]
        = { 4, 3, 1, 2, 3, 4, 2 };

    // Function Call
    areaToPaint(N, W, L, Heights);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code of above approach
import java.util.*;
class GFG {

  // Function to find the total area
  // of walls painted in N row-houses
  static void areaToPaint(int N, int W, int L,
                          int Heights[])
  {

    // Stores total area of N row-houses
    // that needs to be painted
    int total = 0;

    // Traverse the array of wall heights
    for (int i = 0; i < N; i++) {

      // Update total area painted
      total += 2 * Heights[i] * W;
    }

    // Update total
    total += L * (Heights[0]
                  + Heights[N - 1]);

    // Traverse all the houses and
    // print the shared walls
    for (int i = 1; i < N; i++) {

      // Update total
      total += L * Math.abs(Heights[i]
                            - Heights[i - 1]);
    }

    // Print total area needs to paint
    System.out.print(total);
  }

  // Driver code
  public static void main(String[] args)
  {
    // Given N, W & L
    int N = 7, W = 1, L = 1;

    // Given heights of houses
    int Heights[]
      = { 4, 3, 1, 2, 3, 4, 2 };

    // Function Call
    areaToPaint(N, W, L, Heights);
  }
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the total area
# of walls painted in N row-houses
def areaToPaint(N, W, L, Heights):

    # Stores total area of N row-houses
    # that needs to be painted
    total = 0

    # Traverse the array of wall heights
    for i in range(N):

        # Update total area painted
        total += 2 * Heights[i] * W

    # Update total
    total += L * (Heights[0]
                  + Heights[N - 1])

    # Traverse all the houses and
    # print the shared walls
    for i in range(1, N):

        # Update total
        total += L * abs(Heights[i]
                         - Heights[i - 1])

    # Print total area needs to paint
    print(total)

# Driver Code
if __name__ == "__main__":

    # Given N, W & L
    N = 7
    W = 1
    L = 1

    # Given heights of houses
    Heights = [4, 3, 1, 2, 3, 4, 2]

    # Function Call
    areaToPaint(N, W, L, Heights)

    # This code is contributed by chitranayal.
```

## java 描述语言

```
<script>

// JavaScript code of above approach

// Function to find the total area
  // of walls painted in N row-houses
function areaToPaint(N,W,L,Heights)
{
    // Stores total area of N row-houses
    // that needs to be painted
    let total = 0;

    // Traverse the array of wall heights
    for (let i = 0; i < N; i++) {

      // Update total area painted
      total += 2 * Heights[i] * W;
    }

    // Update total
    total += L * (Heights[0]
                  + Heights[N - 1]);

    // Traverse all the houses and
    // print the shared walls
    for (let i = 1; i < N; i++) {

      // Update total
      total += L * Math.abs(Heights[i]
                            - Heights[i - 1]);
    }

    // Print total area needs to paint
    document.write(total);
}

// Driver code
// Given N, W & L
let N = 7, W = 1, L = 1;

// Given heights of houses
let Heights
= [ 4, 3, 1, 2, 3, 4, 2 ];

// Function Call
areaToPaint(N, W, L, Heights);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
52
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)