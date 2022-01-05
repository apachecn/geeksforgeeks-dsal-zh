# 检查物体是否处于平衡状态的程序

> 原文:[https://www . geesforgeks . org/program-to-check-如果一个身体处于平衡或不平衡状态/](https://www.geeksforgeeks.org/program-to-check-if-a-body-is-in-equilibrium-or-not/)

给定一个 **2D** [阵](https://www.geeksforgeeks.org/array-data-structure/)**a【】【】**其中每一行由一个应用体的形式 **(x <sub>i</sub> ，y <sub>i</sub> ，z <sub>i</sub> )** 的矢量坐标组成。如果身体处于**平衡状态**，打印“**是**”。否则，打印“**否**”。

**示例:**

> **输入:** a[][] = {{4，1，7}，{-2，4，-1}，{1，-5，-3 } }
> T3】输出:否
> 
> **输入:** a[][] = {{3，-1，7}，{-5，2，-4}，{2，-1，-3 } }
> T3】输出:是

**方法:**按照以下步骤解决问题:

*   在所有矢量坐标上应用矢量加法。
*   如果向量相加的结果是 **(0，0，0)** ，则身体处于**平衡**。因此，打印“**是**”。
*   否则，打印“**否**”。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <iostream>
using namespace std;

// Function to calculate vector addition
void vectorAddition(int a[][3], int N)
{

    // Sum1 to store sum of xi
    // Sum2 to store sum of yi
    // Sum3 to store sum of zi
    int sum1 = 0, sum2 = 0, sum3 = 0;

    for (int i = 0; i < N; i++) {
        sum1 += a[i][0];
        sum2 += a[i][1];
        sum3 += a[i][2];
    }

    // If the sum1, sum2 and sum3
    // are all equal to zero
    if (sum1 == 0 && sum2 == 0
        && sum3 == 0) {

        // Body is in
        // equilibrium
        cout << "YES";
    }
    else {

        // Body is not in
        // equilibrium
        cout << "NO";
    }
}

// Driver Code
int main()
{
    int N = 3;

    int a[N][3]
        = { { 3, -1, 7 },
            { -5, 2, -4 },
            { 2, -1, -3 } };

    vectorAddition(a, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG{

// Function to calculate
// vector addition
static void vectorAddition(int a[][],
                           int N)
{
  // Sum1 to store sum of xi
  // Sum2 to store sum of yi
  // Sum3 to store sum of zi
  int sum1 = 0, sum2 = 0, sum3 = 0;

  for (int i = 0; i < N; i++)
  {
    sum1 += a[i][0];
    sum2 += a[i][1];
    sum3 += a[i][2];
  }

  // If the sum1, sum2 and sum3
  // are all equal to zero
  if (sum1 == 0 && sum2 == 0 &&
      sum3 == 0)
  {
    // Body is in
    // equilibrium
    System.out.print("YES");
  }
  else
  {
    // Body is not in
    // equilibrium
    System.out.print("NO");
  }
}

// Driver Code
public static void main(String[] args)
{
  int N = 3;
  int a[][] = {{3, -1, 7},
               {-5, 2, -4},
               {2, -1, -3}};
  vectorAddition(a, N);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to calculate vector addition
def vectorAddition(a, N):

    # Sum1 to store sum of xi
    # Sum2 to store sum of yi
    # Sum3 to store sum of zi
    sum1 = 0
    sum2 = 0
    sum3 = 0

    for i in range(N):
        sum1 += a[i][0]
        sum2 += a[i][1]
        sum3 += a[i][2]

    # If the sum1, sum2 and sum3
    # are all equal to zero
    if (sum1 == 0 and sum2 == 0 and
        sum3 == 0):

        # Body is in
        # equilibrium
        print("YES")

    else:

        # Body is not in
        # equilibrium
        print("NO")

# Driver Code
if __name__ == '__main__':

    N = 3
    a = [ [ 3, -1, 7 ],
          [ -5, 2, -4 ],
          [ 2, -1, -3 ] ]

    vectorAddition(a, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG{

// Function to calculate
// vector addition
static void vectorAddition(int[,]a,
                           int N)
{
  // Sum1 to store sum of xi
  // Sum2 to store sum of yi
  // Sum3 to store sum of zi
  int sum1 = 0, sum2 = 0, sum3 = 0;

  for (int i = 0; i < N; i++)
  {
    sum1 += a[i, 0];
    sum2 += a[i, 1];
    sum3 += a[i, 2];
  }

  // If the sum1, sum2 and sum3
  // are all equal to zero
  if (sum1 == 0 && sum2 == 0 &&
      sum3 == 0)
  {
    // Body is in
    // equilibrium
    Console.Write("YES");
  }
  else
  {
    // Body is not in
    // equilibrium
    Console.Write("NO");
  }
}

// Driver Code
public static void Main(String[] args)
{
  int N = 3;
  int[,]a = {{3, -1, 7},
             {-5, 2, -4},
             {2, -1, -3}};
  vectorAddition(a, N);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to calculate
// vector addition
function vectorAddition(a, N)
{
  // Sum1 to store sum of xi
  // Sum2 to store sum of yi
  // Sum3 to store sum of zi
  let sum1 = 0, sum2 = 0, sum3 = 0;

  for (let i = 0; i < N; i++)
  {
    sum1 += a[i][0];
    sum2 += a[i][1];
    sum3 += a[i][2];
  }

  // If the sum1, sum2 and sum3
  // are all equal to zero
  if (sum1 == 0 && sum2 == 0 &&
      sum3 == 0)
  {
    // Body is in
    // equilibrium
    document.write("YES");
  }
  else
  {
    // Body is not in
    // equilibrium
    document.write("NO");
  }
}

// Driver Code

  let N = 3;
  let a = [[3, -1, 7],
               [-5, 2, -4],
               [2, -1, -3]];
  vectorAddition(a, N);

</script>

</script>
```

**Output**

```
YES
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)