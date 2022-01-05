# 找出范围[L，R]内具有 X 峰和 Y 谷的数字排列

> 原文:[https://www . geesforgeks . org/find-范围内数字排列-l-r-having-x-peaks-and-y-valley/](https://www.geeksforgeeks.org/find-permutation-of-numbers-in-range-l-r-having-x-peaks-and-y-valleys/)

给定整数 **L，R，X** 和 **Y** ，使得(R > L ≥ 1)、(X ≥ 0)和(Y ≥ 0)。找到范围**【L，R】**中数字的排列，这样排列中正好有 **X 峰**和 **Y 谷**。如果找到排列，打印“是”和排列。否则打印否。

**注:**在一个数组中**arr【】**如果**arr[I-1]<arr[I]>arr[I+1]**则在**有一个带有**索引的峰，如果**arr[I-1]>arr[I]<arr[I+1]，**其中 **0 < i < N**

***例:***

> ***输入:** L = 1，R = 3，X = 1，Y = 0*
> ***输出:**是，arr[] = { 1，3，2 }*
> ***说明:**需要 1 个峰，不需要谷。*
> *明确 arr[0] < arr[1] > arr[2]，arr[1]为峰值。*
> 
> ***输入:** L = 4，R = 8，X = 4，Y = 1*
> ***输出:**否*
> ***说明:**大小 5 没有 4 峰 1 谷这样的排列。*
> 
> ***输入:** L = 3，R = 5，X = 0，Y = 0*
> ***输出:**是，arr[] = { 3，4，5 }*
> ***说明:**要求 0 峰 0 谷。*
> *排序后的数组没有峰也没有谷。*

**方法:**可以有以下五种情况。遵循每个案例中提到的方法。

**情况-1(没有可能的排列):**排列的第一个和最后一个元素不影响峰和谷的数量。

*   所以如果**(X+Y)>(R–L–1)**没有满足峰谷数的排列。
*   同样如果**(X–Y)>的绝对值为 1** ，则不会有这样的排列，因为两个峰之间正好有 1 个谷，反之亦然。

**情况-2(X = 0，Y = 0):** 按照下面提到的步骤操作。

*   创建一个大小为**(R–L+1)**的数组 **arr[]** ，并将范围**【L，R】**中的数字按排序顺序存储在数组中。
*   打印数组。

**案例-3(X > Y):** 按照以下步骤操作:

*   创建一个大小为**(R–L+1)**的数组 **arr[]** ，由范围**【L，R】**中的数字按排序顺序组成。
*   考虑**最后(X+Y–1)**元素分配 **X** 峰和 **Y** 谷。
*   从**I =(N–2)**迭代到**I =(N –( X+Y–1))**。其中**N =(R–L+1)**
    *   在每次迭代中**用 arr[i+1]** 交换 arr[i]，并将 **i** 减 2。
*   打印数组

**案例-4(X < Y):** 按照以下步骤操作:

*   创建一个大小为**(R–L+1)**的数组 **arr[]** ，由范围**【L，R】**中的数字按排序顺序组成。
*   首先考虑 **(X + Y)** 元素分配 **X** 峰和 **Y** 谷。
*   从 **i = 1** 迭代到 **i = (X+Y)** 。
    *   每次迭代**用 arr[i-1]** 交换 arr[i]，并将 **i** 增加 2。
*   打印数组。

**案例-5(X = Y):** 遵循以下步骤:

*   创建一个长度为**(R–L+1)**的数组 **arr[]** ，该数组由范围**【L，R】**中的数字按排序顺序组成。
*   首先考虑 **(X+Y)** 元素分配 **(X-1)** 峰和 **Y** 谷。
*   从 **i = 1** 迭代到 **i = (X+Y)。**
    *   每次迭代**用 arr[i-1]** 交换 arr[i]，并将 **i** 增加 2。
*   迭代完成后**交换****数组的最后两个**元素，得到一个峰值。
*   打印数组。

下面给出了上述方法的实现:

## C++

```
// C++ code to implement the above approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to build the permutation
void BuildMountainArray(int L, int R, int X, int Y)
{
    int N = (R - L + 1);
    // Case-1: permutaion cannot be built
    if (((X + Y) > (N - 2)) || abs(X - Y) > 1) {
        cout << "No" << endl;
    }
    else {
        // Vector to store the permutation
        vector<int> res(N, 0);
        for (int index = 0; index < N;
             index++) {
            res[index] = L + index;
        }

        // Case-2: X = 0, Y = 0
        if (X == 0 && Y == 0) {
            cout << "Yes" << endl;
            for (int index = 0; index < N;
                 index++) {
                cout << res[index] << " ";
            }
            cout << endl;
            return;
        }

        // Case-3: X > Y
        // Consider last (X+Y+1) elements
        else if (X > Y) {
            for (int index = N - 2;
                 index >= (N - (X + Y + 1));
                 index -= 2) {
                swap(res[index],
                     res[index + 1]);
            }
        }

        // Case-4: X < Y
        // Consider first (X+Y) elements
        else if (Y > X) {
            for (int index = 1; index <=
                 (X + Y); index += 2) {
                swap(res[index],
                     res[index - 1]);
            }
        }
        else {
            // Case-5: X = Y
            // Consider first (X+Y) elements,
            // it will give (X-1) peaks
            // and Y valleys
            for (int index = 1; index <=
                 (X + Y); index += 2) {
                swap(res[index],
                     res[index - 1]);
            }
            // Swap last 2 elements,
            // to get 1 more peak
            swap(res[N - 2], res[N - 1]);
        }

        // Print the required array
        cout << "Yes" << endl;
        for (int index = 0; index < N;
             index++) {
            cout << res[index] << " ";
        }
        cout << endl;
    }
}

// Driver code
int main()
{
    // Input
    int L = 1, R = 3, X = 1, Y = 0;

    // Function call
    BuildMountainArray(L, R, X, Y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.io.*;

class GFG {

  // Utility function to build the permutation
  static void BuildMountainArray(int L, int R, int X,
                                 int Y)
  {
    int N = (R - L + 1);

    // Case-1: permutaion cannot be built
    if (((X + Y) > (N - 2)) || Math.abs(X - Y) > 1) {
      System.out.println("No");
    }
    else
    {
      // Vector to store the permutation
      int res[] = new int[N];
      for (int index = 0; index < N; index++) {
        res[index] = L + index;
      }

      // Case-2: X = 0, Y = 0
      if (X == 0 && Y == 0) {
        System.out.println("Yes");
        for (int index = 0; index < N; index++) {
          System.out.print(res[index] + " ");
        }
        System.out.println();
        return;
      }

      // Case-3: X > Y
      // Consider last (X+Y+1) elements
      else if (X > Y) {
        for (int index = N - 2;
             index >= (N - (X + Y + 1));
             index -= 2) {
          int temp = res[index];
          res[index] = res[index + 1];
          res[index + 1] = temp;
        }
      }

      // Case-4: X < Y
      // Consider first (X+Y) elements
      else if (Y > X) {
        for (int index = 1; index <= (X + Y);
             index += 2) {
          int temp = res[index];
          res[index] = res[index - 1];
          res[index - 1] = temp;
        }
      }
      else {
        // Case-5: X = Y
        // Consider first (X+Y) elements,
        // it will give (X-1) peaks
        // and Y valleys
        for (int index = 1; index <= (X + Y);
             index += 2) {
          int temp = res[index];
          res[index] = res[index - 1];
          res[index - 1] = temp;
        }

        // Swap last 2 elements,
        // to get 1 more peak
        int temp = res[N - 2];
        res[N - 2] = res[N - 1];
        res[N - 1] = temp;
      }

      // Print the required array
      System.out.println("Yes");
      for (int index = 0; index < N; index++) {
        System.out.print(res[index] + " ");
      }
      System.out.println();
    }
  }

  // Driver code
  public static void main(String[] args)
  {
    // Input
    int L = 1, R = 3, X = 1, Y = 0;

    // Function call
    BuildMountainArray(L, R, X, Y);
  }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python code to implement the above approach
import math as Math

# Utility function to build the permutation
def BuildMountainArray(L, R, X, Y):
    N = (R - L + 1)

    # Case-1: permutaion cannot be built
    if (((X + Y) > (N - 2)) or Math.fabs(X - Y) > 1):
        print("No")
    else:
        # Vector to store the permutation
        res = [0] * N
        for index in range(N):
            res[index] = L + index

        # Case-2: X = 0, Y = 0
        if (X == 0 and Y == 0):
            print("Yes")
            for index in range(N):
                print(res[index], end=" ")
            print("")
            return

        # Case-3: X > Y
        # Consider last (X+Y+1) elements
        elif (X > Y):
            for index in range(N - 2, N - (X + Y + 1) - 1, -2):
                temp = res[index]
                res[index] = res[index + 1]
                res[index + 1] = temp

        # Case-4: X < Y
        # Consider first (X+Y) elements
        elif (Y > X):
            for index in range(1, X + Y + 1, 2):
                temp = res[index]
                res[index] = res[index - 1]
                res[index - 1] = temp
        else:

            # Case-5: X = Y
            # Consider first (X+Y) elements,
            # it will give (X-1) peaks
            # and Y valleys
            for index in range(1, X + Y + 1, 2):
                temp = res[index]
                res[index] = res[index - 1]
                res[index - 1] = temp

            # Swap last 2 elements,
            # to get 1 more peak
            temp = res[N - 2]
            res[N - 2] = res[N - 1]
            res[N - 1] = temp

        # Print the required array
        print("Yes")
        for index in range(N):
            print(res[index], end=" ")
        print("")

# Driver code

# Input
L = 1
R = 3
X = 1
Y = 0

# Function call
BuildMountainArray(L, R, X, Y)

# This code is contributed by Saurabh jaiswal
```

## C#

```
// C# implementation of above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG {

  // Utility function to build the permutation
  static void BuildMountainArray(int L, int R, int X,
                                 int Y)
  {
    int N = (R - L + 1);

    // Case-1: permutaion cannot be built
    if (((X + Y) > (N - 2)) || Math.Abs(X - Y) > 1) {
      Console.WriteLine("No");
    }
    else
    {
      // Vector to store the permutation
      int[] res = new int[N];
      for (int index = 0; index < N; index++) {
        res[index] = L + index;
      }

      // Case-2: X = 0, Y = 0
      if (X == 0 && Y == 0) {
        Console.WriteLine("Yes");
        for (int index = 0; index < N; index++) {
          Console.Write(res[index] + " ");
        }
        Console.WriteLine();
        return;
      }

      // Case-3: X > Y
      // Consider last (X+Y+1) elements
      else if (X > Y) {
        for (int index = N - 2;
             index >= (N - (X + Y + 1));
             index -= 2) {
          int temp1 = res[index];
          res[index] = res[index + 1];
          res[index + 1] = temp1;
        }
      }

      // Case-4: X < Y
      // Consider first (X+Y) elements
      else if (Y > X) {
        for (int index = 1; index <= (X + Y);
             index += 2) {
          int temp2 = res[index];
          res[index] = res[index - 1];
          res[index - 1] = temp2;
        }
      }
      else
      {

        // Case-5: X = Y
        // Consider first (X+Y) elements,
        // it will give (X-1) peaks
        // and Y valleys
        for (int index = 1; index <= (X + Y);
             index += 2) {
          int temp3 = res[index];
          res[index] = res[index - 1];
          res[index - 1] = temp3;
        }

        // Swap last 2 elements,
        // to get 1 more peak
        int temp4 = res[N - 2];
        res[N - 2] = res[N - 1];
        res[N - 1] = temp4;
      }

      // Print the required array
      Console.WriteLine("Yes");
      for (int index = 0; index < N; index++) {
        Console.Write(res[index] + " ");
      }
      Console.WriteLine();
    }
  }

  // Driver Code
  public static void Main()
  {
    // Input
    int L = 1, R = 3, X = 1, Y = 0;

    // Function call
    BuildMountainArray(L, R, X, Y);

  }
}

// This code is contributed sanjoy_62.
```

## java 描述语言

```
<script>
    // JavaScript code to implement the above approach

    // Utility function to build the permutation
    const BuildMountainArray = (L, R, X, Y) => {
        let N = (R - L + 1);

        // Case-1: permutaion cannot be built
        if (((X + Y) > (N - 2)) || Math.abs(X - Y) > 1) {
            document.write("No<br/>");
        }
        else
        {

            // Vector to store the permutation
            let res = new Array(N).fill(0);
            for (let index = 0; index < N;
                index++) {
                res[index] = L + index;
            }

            // Case-2: X = 0, Y = 0
            if (X == 0 && Y == 0) {
                document.write("Yes<br/>");
                for (let index = 0; index < N;
                    index++) {
                    document.write(`${res[index]} `);
                }
                document.write("<br/>");
                return;
            }

            // Case-3: X > Y
            // Consider last (X+Y+1) elements
            else if (X > Y) {
                for (let index = N - 2;
                    index >= (N - (X + Y + 1));
                    index -= 2) {
                    let temp = res[index];
                    res[index] = res[index + 1];
                    res[index + 1] = temp;
                }
            }

            // Case-4: X < Y
            // Consider first (X+Y) elements
            else if (Y > X) {
                for (let index = 1; index <=
                    (X + Y); index += 2) {
                    let temp = res[index];
                    res[index] = res[index - 1];
                    res[index - 1] = temp;
                }
            }
            else {

                // Case-5: X = Y
                // Consider first (X+Y) elements,
                // it will give (X-1) peaks
                // and Y valleys
                for (let index = 1; index <=
                    (X + Y); index += 2) {
                    let temp = res[index];
                    res[index] = res[index - 1];
                    res[index - 1] = temp;
                }

                // Swap last 2 elements,
                // to get 1 more peak
                let temp = res[N - 2];
                res[N - 2] = res[N - 1];
                res[N - 1] = temp;
            }

            // Print the required array
            document.write("Yes<br/>");
            for (let index = 0; index < N;
                index++) {
                document.write(`${res[index]} `);
            }
            document.write("<br/>");
        }
    }

    // Driver code

    // Input
    let L = 1, R = 3, X = 1, Y = 0;

    // Function call
    BuildMountainArray(L, R, X, Y);

    // This code is contributed by rakeshsahni

</script>
```

**Output**

```
Yes
1 3 2 
```

**时间复杂度:** O(N)其中 N =(R–L+1)
T3】空间复杂度: O(1)