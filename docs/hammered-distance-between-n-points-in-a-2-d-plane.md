# 二维平面内 N 个点之间的锤击距离

> 原文:[https://www . geesforgeks . org/hammed-二维平面中 n 个点之间的距离/](https://www.geeksforgeeks.org/hammered-distance-between-n-points-in-a-2-d-plane/)

给定二维平面中的第 n 个点，然后是，易描述第 n 个点。任务是计算 n 个点的锤击距离。
**注:**锤击距离是每对点之间最短距离的平方之和。

**示例:**

```
Input: n = 3
0 1
0 0
1 0
Output: 4

Input: n = 4
1 0
2 0
3 0
4 0
Output: 20
```

**基本方法:**因为我们必须找出所有对中最短距离的平方和。所以，我们可以取每一个可能的对，计算距离的平方和。

```
// Pseudo code to find hammered-distance using above approach.
//this will store hammered distance
Distance=0
for(int i=0;i<n;i++)
{
    for(int j=i+1;j<n;j++)
    {
         //shortest distance between point i and j.
         Distance+=(x[i]-x[j])^2+(y[i]-y[j])^2
     }
}
```

它的时间复杂度将是 O(n^2).
**高效途径:**这个问题可以用 O(N)的时间复杂度来解决。

![\begin{document} $Sum=\sum_{i=1}^{n} \sum_{j=1}^{i-1} \left(X_j-X_i \right)^2+\left(Y_j-Y_i \right)^2$ We can solve separtely for x and y coordinates. For X: $Sum_x=\sum_{i=1}^{n} \sum_{j=1}^{i-1} \left(X_j-X_i \right)^2$ $Sum_x= \sum_{i=1}^{n} \sum_{j=1}^{i-1} \left(X_j^2+X_i^2 -2 \cdot X_i \cdot X_j \right)$ Now expand the summation part, We can write this equation as- $Sum_x=\sum_{i=1}^{n} \left( (i-1)*X_i^2+\sum_{j=1}^{i-1}X_j^2-2 \cdot X_i\cdot \sum_{j=1}^{i-1} X_j \right)$ $\sum_{j=1}^{i-1}X_j$ This is commulative sum of square of points upto i-1.So, this can be calculated in linear time. Similarly, This can also be calculated in linear time. $2 \cdot X_i\cdot \sum_{j=1}^{i-1} X_j$ \end{document}        ](img/1017c13bfa37bf7a4a5e55bd1209996f.png "Rendered by QuickLaTeX.com")

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Function calculate cumulative sum
// of x, y, x^2, y^2 coordinates.
void cumm(vector<ll>& x, vector<ll>& y,
        vector<ll>& cummx, vector<ll>& cummy,
        vector<ll>& cummx2, vector<ll>& cummy2, ll n)
{
    for (int i = 1; i <= n; i++) {
        cummx[i] = cummx[i - 1] + x[i];
        cummy[i] = cummy[i - 1] + y[i];
        cummx2[i] = cummx2[i - 1] + x[i] * x[i];
        cummy2[i] = cummy2[i - 1] + y[i] * y[i];
    }
}

// Function ot calculate the hammered distance
int calHammeredDistance(int n, vector<ll>& x, vector<ll>& y)
{
    // cummx contains cumulative sum of x
    // cummy contains cumulative sum of y
    vector<ll> cummx(n + 1, 0), cummy(n + 1, 0);

    // cummx2 contains cumulative sum of x^2
    // cummy2 contains cumulative sum of y^2
    vector<ll> cummx2(n + 1, 0), cummy2(n + 1, 0);

    // calculate cumulative of x
    //, y, x^2, y^2, because these terms
    // required in formula to reduce complexity.

    // this function calculate all required terms.
    cumm(x, y, cummx, cummy, cummx2, cummy2, n);

    // hdx calculate hammer distance for x coordinate
    // hdy calculate hammer distance for y coordinate
    ll hdx = 0, hdy = 0;

    for (int i = 1; i <= n; i++) {

        // came from formula describe in explanation
        hdx += (i - 1) * x[i] * x[i] + cummx2[i - 1]
            - 2 * x[i] * cummx[i - 1];

        // came from formula describe in explanation
        hdy += (i - 1) * y[i] * y[i] + cummy2[i - 1]
            - 2 * y[i] * cummy[i - 1];
    }

    // total is the sum of both x and y.
    ll total = hdx + hdy;
    return total;
}

// Driver code
int main()
{
    // number of points
    int n = 3;

    // x contains the x coordinates
    // y contains the y coordinates
    //and converting the size to n+1
    vector<ll> x = {0, 0, 1, 0};
    vector<ll> y = {1, 0, 0, 0};

    cout << calHammeredDistance(n, x, y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

class GFG{

// Function calculate cumulative sum
// of x, y, x^2, y^2 coordinates.
static void cumm(int [] x, int [] y,
        int [] cummx, int [] cummy,
        int [] cummx2, int [] cummy2, int n)
{
    for (int i = 1; i <= n; i++) {
        cummx[i] = cummx[i - 1] + x[i];
        cummy[i] = cummy[i - 1] + y[i];
        cummx2[i] = cummx2[i - 1] + x[i] * x[i];
        cummy2[i] = cummy2[i - 1] + y[i] * y[i];
    }
}

// Function ot calculate the hammered distance
static int calHammeredDistance(int n, int [] x, int [] y)
{
    // cummx contains cumulative sum of x
    // cummy contains cumulative sum of y
    int []cummx = new int[n + 1];
    int []cummy = new int[n + 1];

    // cummx2 contains cumulative sum of x^2
    // cummy2 contains cumulative sum of y^2
    int []cummx2 = new int[n + 1];
    int []cummy2 = new int[n + 1];

    // calculate cumulative of x
    //, y, x^2, y^2, because these terms
    // required in formula to reduce complexity.

    // this function calculate all required terms.
    cumm(x, y, cummx, cummy, cummx2, cummy2, n);

    // hdx calculate hammer distance for x coordinate
    // hdy calculate hammer distance for y coordinate
    int hdx = 0, hdy = 0;

    for (int i = 1; i <= n; i++) {

        // came from formula describe in explanation
        hdx += (i - 1) * x[i] * x[i] + cummx2[i - 1]
               - 2 * x[i] * cummx[i - 1];

        // came from formula describe in explanation
        hdy += (i - 1) * y[i] * y[i] + cummy2[i - 1]
               - 2 * y[i] * cummy[i - 1];
    }

    // total is the sum of both x and y.
    int total = hdx + hdy;
    return total;
}

// Driver code
public static void main(String[] args)
{
    // number of points
    int n = 3;

    // x contains the x coordinates
    // y contains the y coordinates
    int []x = new int[n + 1];
    int []y = new int[n + 1];
    x[2] = 1;
    y[0] = 1;

    System.out.print(calHammeredDistance(n, x, y));

}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function calculate cumulative sum
# of x, y, x^2, y^2 coordinates.
def cumm(x, y, cummx, cummy,
               cummx2, cummy2, n):

    for i in range(1, n+1):
        cummx[i] = cummx[i - 1] + x[i]
        cummy[i] = cummy[i - 1] + y[i]
        cummx2[i] = cummx2[i - 1] + x[i] * x[i]
        cummy2[i] = cummy2[i - 1] + y[i] * y[i]

# Function ot calculate the
# hammered distance
def calHammeredDistance(n, x, y):

    # cummx contains cumulative sum of x
    # cummy contains cumulative sum of y
    cummx = [0] * (n + 1)
    cummy = [0] * (n + 1)

    # cummx2 contains cumulative sum of x^2
    # cummy2 contains cumulative sum of y^2
    cummx2 = [0] * (n + 1)
    cummy2 = [0] * (n + 1)

    # calculate cumulative of x , y, x^2, y^2,
    # because these terms are required in the
    # formula to reduce complexity.

    # This function calculate all required terms.
    cumm(x, y, cummx, cummy, cummx2, cummy2, n)

    # hdx calculate hammer distance for x coordinate
    # hdy calculate hammer distance for y coordinate
    hdx, hdy = 0, 0

    for i in range(1, n + 1):

        # came from formula describe in explanation
        hdx += ((i - 1) * x[i] * x[i] + cummx2[i - 1] -
                             2 * x[i] * cummx[i - 1])

        # came from formula describe in explanation
        hdy += ((i - 1) * y[i] * y[i] + cummy2[i - 1] -
                             2 * y[i] * cummy[i - 1])

    # total is the sum of both x and y.
    total = hdx + hdy
    return total

# Driver Code
if __name__ == "__main__":

    # number of points
    n = 3

    # x contains the x coordinates
    # y contains the y coordinates
    x = [0, 0, 1, 0]
    y = [1, 0, 0, 0]

    print(calHammeredDistance(n, x, y))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of above approach
using System;

class GFG{

// Function calculate cumulative sum
// of x, y, x^2, y^2 coordinates.
static void cumm(int [] x, int [] y,
        int [] cummx, int [] cummy,
        int [] cummx2, int [] cummy2, int n)
{
    for (int i = 1; i <= n; i++) {
        cummx[i] = cummx[i - 1] + x[i];
        cummy[i] = cummy[i - 1] + y[i];
        cummx2[i] = cummx2[i - 1] + x[i] * x[i];
        cummy2[i] = cummy2[i - 1] + y[i] * y[i];
    }
}

// Function ot calculate the hammered distance
static int calHammeredDistance(int n, int [] x, int [] y)
{
    // cummx contains cumulative sum of x
    // cummy contains cumulative sum of y
    int []cummx = new int[n + 1];
    int []cummy = new int[n + 1];

    // cummx2 contains cumulative sum of x^2
    // cummy2 contains cumulative sum of y^2
    int []cummx2 = new int[n + 1];
    int []cummy2 = new int[n + 1];

    // calculate cumulative of x
    //, y, x^2, y^2, because these terms
    // required in formula to reduce complexity.

    // this function calculate all required terms.
    cumm(x, y, cummx, cummy, cummx2, cummy2, n);

    // hdx calculate hammer distance for x coordinate
    // hdy calculate hammer distance for y coordinate
    int hdx = 0, hdy = 0;

    for (int i = 1; i <= n; i++) {

        // came from formula describe in explanation
        hdx += (i - 1) * x[i] * x[i] + cummx2[i - 1]
               - 2 * x[i] * cummx[i - 1];

        // came from formula describe in explanation
        hdy += (i - 1) * y[i] * y[i] + cummy2[i - 1]
               - 2 * y[i] * cummy[i - 1];
    }

    // total is the sum of both x and y.
    int total = hdx + hdy;
    return total;
}

// Driver code
public static void Main(String[] args)
{
    // number of points
    int n = 3;

    // x contains the x coordinates
    // y contains the y coordinates
    int []x = new int[n + 1];
    int []y = new int[n + 1];
    x[2] = 1;
    y[0] = 1;

    Console.Write(calHammeredDistance(n, x, y)); 
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
      // JavaScript implementation of above approach
      // Function calculate cumulative sum
      // of x, y, x^2, y^2 coordinates.
      function cumm(x, y, cummx, cummy, cummx2, cummy2, n) {
        for (var i = 1; i <= n; i++) {
          cummx[i] = cummx[i - 1] + x[i];
          cummy[i] = cummy[i - 1] + y[i];
          cummx2[i] = cummx2[i - 1] + x[i] * x[i];
          cummy2[i] = cummy2[i - 1] + y[i] * y[i];
        }
      }

      // Function ot calculate the hammered distance
      function calHammeredDistance(n, x, y) {
        // cummx contains cumulative sum of x
        // cummy contains cumulative sum of y
        var cummy = new Array(n + 1).fill(0);
        var cummx = new Array(n + 1).fill(0);

        // cummx2 contains cumulative sum of x^2
        // cummy2 contains cumulative sum of y^2
        var cummx2 = new Array(n + 1).fill(0);
        var cummy2 = new Array(n + 1).fill(0);

        // calculate cumulative of x
        //, y, x^2, y^2, because these terms
        // required in formula to reduce complexity.

        // this function calculate all required terms.
        cumm(x, y, cummx, cummy, cummx2, cummy2, n);

        // hdx calculate hammer distance for x coordinate
        // hdy calculate hammer distance for y coordinate
        var hdx = 0,
          hdy = 0;

        for (var i = 1; i <= n; i++) {
          // came from formula describe in explanation
          hdx +=
            (i - 1) * x[i] * x[i] + cummx2[i - 1] - 2 * x[i] * cummx[i - 1];

          // came from formula describe in explanation
          hdy +=
            (i - 1) * y[i] * y[i] + cummy2[i - 1] - 2 * y[i] * cummy[i - 1];
        }

        // total is the sum of both x and y.
        var total = hdx + hdy;
        return total;
      }

      // Driver code
      // number of points
      var n = 3;

      // x contains the x coordinates
      // y contains the y coordinates
      var x = new Array(n + 1).fill(0);
      var y = new Array(n + 1).fill(0);
      x[2] = 1;
      y[0] = 1;

      document.write(calHammeredDistance(n, x, y));
    </script>
```

**Output**

```
2
```