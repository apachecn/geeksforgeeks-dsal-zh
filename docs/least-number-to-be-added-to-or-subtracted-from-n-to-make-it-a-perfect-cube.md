# 最少的要加或减的数，使其成为一个完美的立方体

> 原文:[https://www . geeksforgeeks . org/n 加或减最少数字使其成为完美立方体/](https://www.geeksforgeeks.org/least-number-to-be-added-to-or-subtracted-from-n-to-make-it-a-perfect-cube/)

给定一个数 **N** ，求 **N** 需要加减的最小数，使其成为[完美立方体](https://www.geeksforgeeks.org/tag/maths-perfect-cube/)。如果要加数字，用+号打印，否则如果要减数字，用–号打印。

**示例:**

> **输入:** N = 25
> **输出:**2
> 25 = 8
> 25 = 27
> 后最近的完美立方体因此需要将 2 加到 25 才能得到最近的完美立方体
> 
> **输入:** N = 40
> **输出:**-13
> 40 = 25 之前最近的完美立方体
> 40 = 64 之后最近的完美立方体
> 因此需要从 40 中减去 13 才能得到最近的完美立方体

**接近**:

1.  拿到号码。
2.  求数字的[立方根，将结果转换为整数。](https://www.geeksforgeeks.org/find-cubic-root-of-a-number/)
3.  将双精度值转换为整数后，这将包含 N 之前的完美立方体的根，即 **floor(立方根(N))** 。
4.  然后求这个数的立方，这将是 n 之前的完美立方。
5.  求 N 后的完美立方根，即**天花板(立方根(N))** 。
6.  然后求这个数的立方，这将是 n 之后的完美立方。
7.  检查楼层值的立方是最接近 N 还是天花板值。
8.  如果楼层值的立方最接近 N，用-号打印差值。否则打印天花板值的立方和带+号的 N 之间的差值。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the Least number
int nearest(int n)
{

    // Get the perfect cube
    // before and after N
    int prevCube = cbrt(n);
    int nextCube = prevCube + 1;
    prevCube = prevCube * prevCube * prevCube;
    nextCube = nextCube * nextCube * nextCube;

    // Check which is nearest to N
    int ans
        = (n - prevCube) < (nextCube - n)
              ? (prevCube - n)
              : (nextCube - n);

    // return the result
    return ans;
}

// Driver code
int main()
{
    int n = 25;
    cout << nearest(n) << endl;

    n = 27;
    cout << nearest(n) << endl;

    n = 40;
    cout << nearest(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach 
class GFG {

    // Function to return the Least number 
    static int nearest(int n) 
    { 

        // Get the perfect cube 
        // before and after N 
        int prevCube = (int)Math.cbrt(n); 
        int nextCube = prevCube + 1; 
        prevCube = prevCube * prevCube * prevCube; 
        nextCube = nextCube * nextCube * nextCube; 

        // Check which is nearest to N 
        int ans = (n - prevCube) < (nextCube - n) ? 
                    (prevCube - n) : (nextCube - n); 

        // return the result 
        return ans; 
    } 

    // Driver code 
    public static void main (String[] args)
    { 
        int n = 25; 
        System.out.println(nearest(n)); 

        n = 27; 
        System.out.println(nearest(n)) ; 

        n = 40; 
        System.out.println(nearest(n)) ; 
    } 
}

// This code is contributed by Yash_R
```

**Output:**

```
2
0
-13

```