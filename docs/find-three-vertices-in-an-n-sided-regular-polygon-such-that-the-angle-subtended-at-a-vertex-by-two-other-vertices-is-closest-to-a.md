# 在一个 N 边正多边形中找到三个顶点，这样其他两个顶点对着一个顶点的角度最接近 A

> 原文:[https://www . geeksforgeeks . org/find-n 边正多边形中的三个顶点，以至于一个顶点对着另两个顶点的角度最接近 a/](https://www.geeksforgeeks.org/find-three-vertices-in-an-n-sided-regular-polygon-such-that-the-angle-subtended-at-a-vertex-by-two-other-vertices-is-closest-to-a/)

给定一个 [**N** 边正凸多边形](https://www.geeksforgeeks.org/check-if-it-is-possible-to-create-a-polygon-with-given-n-sides/)和一个以度为单位的角度 **A** ，任务是找到任意 **3** 顶点 **i** 、 **j** 和 **k** ，使得顶点 **i** 和 **k** 对着顶点 **j** 的角度最接近 **A**

***注意:**每个顶点从任意一个顶点开始逆时针方向编号，从 **1** 到 **N** 。*

**示例:**

> **输入:** N = 3，A = 15
> **输出:** 2 1 3
> **说明:**
> 给定的多边形是一个三角形，因此任意一个顶点所能对的最小角度等于 30°，最接近 A，包含多边形的所有顶点。
> 
> **输入:** N = 4，A = 90
> T3】输出: 2 1 4

**方法:**给定的问题可以基于以下观察来解决:

*   正多边形的顶点位于一个圆上。
*   [N 边正多边形](https://www.geeksforgeeks.org/central-angle-of-a-n-sided-regular-polygon/)的中心角为**360°/N**。
*   由 **X** 边分开的顶点对着圆心的[角等于 **(360*X)/N** 。](https://www.geeksforgeeks.org/angle-subtended-by-an-arc-at-the-centre-of-a-circle/)
*   根据定理，圆弧对着外接圆的角度是同一圆弧对着圆心的角度的一半。因此，由 **X** 边形成的弧对着顶点的角度将等于 **(180*X)/N** 。
*   由于多边形是规则的，因此可以通过取等于 **X** 的任何边缘差的 **2** 顶点来对着相同的角度。

按照以下步骤解决问题:

*   初始化两个变量，说 **ans** 为 **0** 和 **minElement** 为 [**INT_MAX**](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) 分别存储对着最接近 **A** 的角度的边数和存储最接近的角度。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N–2】**，并执行以下步骤:
    *   使用上述公式，找出由 **i** 条边形成的弧对着外接圆的角度，并将其存储在变量**角度中。**
    *   检查**(A–角度)**的绝对值是否小于**(minElement–A)**的[绝对值](https://www.geeksforgeeks.org/program-to-find-absolute-value-of-a-given-number/)，然后更新 **i** 至 **ans** 的值和**角度**至 **minElement** 的值。
*   完成以上步骤后，打印顶点 **{2，1，2 + ans}** 作为结果顶点。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

#define ll long long
#define MAXN 1000000

// Function to find three vertices that
// subtends an angle closest to A
void closestsAngle(int N, int A)
{
    // Stores the closest angle to A
    double mi = INT_MAX;

    // Stores the count of edge which
    // subtend an angle of A
    int ans = 0;

    // Iterate in the range [1, N-2]
    for (int i = 1; i < N - 1; i++) {

        // Stores the angle subtended
        double angle = 180.0 * i / N;

        // If absolute(angle-A) is less
        // than absolute(mi-A)
        if (fabs(angle - A) < fabs(mi - A)) {

            // Update angle to mi, and
            // also update i to ans
            mi = angle;
            ans = i;
        }
    }

    // Print the vertices
    cout << 2 << ' ' << 1 << ' '
         << 2 + ans;
}

// Driver Code
int main()
{
    int N = 3, A = 15;
    closestsAngle(N, A);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

    // Function to find three vertices that
    // subtends an angle closest to A
    static void closestsAngle(int N, int A)
    {
        // Stores the closest angle to A
        double mi = Integer.MAX_VALUE;

        // Stores the count of edge which
        // subtend an angle of A
        int ans = 0;

        // Iterate in the range [1, N-2]
        for (int i = 1; i < N - 1; i++) {

            // Stores the angle subtended
            double angle = 180.0 * i / N;

            // If absolute(angle-A) is less
            // than absolute(mi-A)
            if (Math.abs(angle - A) < Math.abs(mi - A)) {

                // Update angle to mi, and
                // also update i to ans
                mi = angle;
                ans = i;
            }
        }

        // Print the vertices
        System.out.print(2 + " " + 1 + " " + (2 + ans));
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 3, A = 15;
        closestsAngle(N, A);
    }
}

// This code is contributed by subhammahato348.
```

## 蟒蛇 3

```
# Python program for the above approach
# Function to find three vertices that
# subtends an angle closest to A
import math
import sys
def closestsAngle(N, A):

    # Stores the closest angle to A
    mi = sys.maxsize

    # Stores the count of edge which
    # subtend an angle of A
    ans = 0

    # Iterate in the range [1, N-2]
    for i in range(N ):

        # Stores the angle subtended
        angle = 180.0 * i / N

        # If absolute(angle-A) is less
        # than absolute(mi-A)
        if (math.fabs(angle - A) < math.fabs(mi - A)): 

            # Update angle to mi, and
            # also update i to ans
            mi = angle
            i+=1
            ans = i

    # Pr the vertices
    print(2 , 1 , 2 + ans)

# Driver Code
if __name__ == '__main__':

    N = 3
    A = 15
    closestsAngle(N, A)

# This code is contributed by Shivani
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find three vertices that
// subtends an angle closest to A
static void closestsAngle(int N, int A)
{

    // Stores the closest angle to A
    double mi = Int32.MaxValue;

    // Stores the count of edge which
    // subtend an angle of A
    int ans = 0;

    // Iterate in the range [1, N-2]
    for(int i = 1; i < N - 1; i++)
    {

        // Stores the angle subtended
        double angle = 180.0 * i / N;

        // If absolute(angle-A) is less
        // than absolute(mi-A)
        if (Math.Abs(angle - A) <
            Math.Abs(mi - A))
        {

            // Update angle to mi, and
            // also update i to ans
            mi = angle;
            ans = i;
        }
    }

    // Print the vertices
    Console.Write(2 + " " + 1 +
                      " " + (2 + ans));
}

// Driver Code
public static void Main()
{
    int N = 3, A = 15;
    closestsAngle(N, A);
}
}

// This code is contributed by subhammahato348
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach

        // Function to find three vertices that
        // subtends an angle closest to A
        function closestsAngle(N, A) {
            // Stores the closest angle to A
            let mi = Number.MAX_VALUE;

            // Stores the count of edge which
            // subtend an angle of A
            let ans = 0;

            // Iterate in the range [1, N-2]
            for (let i = 1; i < N - 1; i++) {

                // Stores the angle subtended
                let angle = 180.0 * i / N;

                // If absolute(angle-A) is less
                // than absolute(mi-A)
                if (Math.abs(angle - A) < Math.abs(mi - A)) {

                    // Update angle to mi, and
                    // also update i to ans
                    mi = angle;
                    ans = i;
                }
            }

            // Print the vertices
            document.write(2 + ' ' + 1 + ' '
                + parseInt(2 + ans));
        }

        // Driver Code

        let N = 3, A = 15;
        closestsAngle(N, A);

      // This code is contributed by Potta Lokesh

</script>
```

**Output:** 

```
2 1 3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)