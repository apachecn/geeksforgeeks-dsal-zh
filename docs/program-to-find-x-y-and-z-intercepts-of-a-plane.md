# 求平面 X、Y、Z 截距的程序

> 原文:[https://www . geesforgeks . org/program-to-find-x-y-和-z-a-plane-intercepts/](https://www.geeksforgeeks.org/program-to-find-x-y-and-z-intercepts-of-a-plane/)

在这篇文章中，解释了如何找到一个平面的 X，Y，Z 截距。
有两种方法可以找到截获的内容:

*   **<u>例 1:</u>** <u>当给出平面的一般方程时。</u>

**示例:**

> 输入:A = -6，B = 5，C = -3，D = 9
> **输出:** 1.5
> -1.8
> 3.0
> 
> **输入:** A = 7，B = 4，C = 5，D =-7
> T3】输出: 1.0
> 1.75
> 1.4

**方法:**可以通过以下步骤计算结果:

*   将平面的一般方程 **Ax + By + Cz + D = 0** 转换为**Ax+By+Cz =–D**
*   除以等式两边的 **-D**
*   所以，方程变成**x/(-D/A)+y/(-D/B)+z(-D/C)= 1**
*   上述方程是平面截距形式。因此，
    X 截获将为=**-D/A**T3】Y 截获将为=**-D/B**T6】Z 截获将为= **-D/C**

下面是上述方法的实现:

## C++

```
// C++ program to find the
// X, Y and Z intercepts of a plane
#include<iostream>
using namespace std;

float * XandYandZintercept(float A, float B,
                            float C, float D)
{
        static float rslt[3];

        // For finding the x-intercept
        // put y = 0 and z = 0
        float x = -D / A ;

        // For finding the y-intercept
        // put x = 0 and z = 0
        float y = -D / B ;

        // For finding the z-intercept
        // put x = 0 and y = 0
        float z = -D / C ;

        rslt[0] = x;
        rslt[1] = y;
        rslt[2] = z;

        return rslt;
}

// Driver code
int main ()
{
    int A = 2 ;
    int B = 5 ;
    int C = 7;
    int D = 8 ;

    float *rslt = XandYandZintercept(A, B, C, D);

    for(int i = 0; i < 3 ; i++)
    {
        cout << rslt[i] << " ";
    }

}

// This code is contributed by ANKITKUMAR34
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// X, Y and Z intercepts of a plane
class GFG
{

    static float[] XandYandZintercept(float A,
                    float B, float C, float D)
    {
        float rslt[] = new float[3];

        // For finding the x-intercept
        // put y = 0 and z = 0
        float x = -D / A ;

        // For finding the y-intercept
        // put x = 0 and z = 0
        float y = -D / B ;

        // For finding the z-intercept
        // put x = 0 and y = 0
        float z = -D / C ;

        rslt[0] = x;
        rslt[1] = y;
        rslt[2] = z;

        return rslt;
    }

    // Driver code
    public static void main (String[] args)
    {
        int A = 2 ;
        int B = 5 ;
        int C = 7;
        int D = 8 ;

        float rslt[] = XandYandZintercept(A, B, C, D);

        for(int i = 0; i < 3 ; i++)
        {
            System.out.print(rslt[i] + " ");
        }
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python program to find the
# X, Y and Z intercepts of a plane

def XandYandZintercept(A, B, C, D):

    # For finding the x-intercept
    # put y = 0 and z = 0
    x = -D / A

    # For finding the y-intercept
    # put x = 0 and z = 0
    y = -D / B

    # For finding the z-intercept
    # put x = 0 and y = 0
    z = -D / C
    return [x, y, z]

# Driver code
A = 2
B = 5
C = 7
D = 8
print(XandYandZintercept(A, B, C, D))
```

## C#

```
// C# program to find the
// X, Y and Z intercepts of a plane
using System;

class GFG
{

    static float[] XandYandZintercept(float A,
                    float B, float C, float D)
    {
        float []rslt = new float[3];

        // For finding the x-intercept
        // put y = 0 and z = 0
        float x = -D / A ;

        // For finding the y-intercept
        // put x = 0 and z = 0
        float y = -D / B ;

        // For finding the z-intercept
        // put x = 0 and y = 0
        float z = -D / C ;

        rslt[0] = x;
        rslt[1] = y;
        rslt[2] = z;

        return rslt;
    }

    // Driver code
    public static void Main()
    {
        int A = 2 ;
        int B = 5 ;
        int C = 7;
        int D = 8 ;

        float []rslt = XandYandZintercept(A, B, C, D);

        for(int i = 0; i < 3 ; i++)
        {
            Console.Write(rslt[i] + " ");
        }
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
      // JavaScript program to find the
      // X, Y and Z intercepts of a plane

      function XandYandZintercept(A, B, C, D) {
        // For finding the x-intercept
        // put y = 0 and z = 0
        var x = -D / A;

        // For finding the y-intercept
        // put x = 0 and z = 0
        var y = -D / B;

        // For finding the z-intercept
        // put x = 0 and y = 0
        var z = -D / C;
        return [x, y, z];
      }
      function equation_plane(p, q, r) {
        var x1 = p[0];
        var y1 = p[1];
        var z1 = p[2];
        var x2 = q[0];
        var y2 = q[1];
        var z2 = q[2];
        var x3 = r[0];
        var y3 = r[1];
        var z3 = r[2];

        // For Finding value of A, B, C, D
        var a1 = x2 - x1;
        var b1 = y2 - y1;
        var c1 = z2 - z1;
        var a2 = x3 - x1;
        var b2 = y3 - y1;
        var c2 = z3 - z1;
        var A = b1 * c2 - b2 * c1;
        var B = a2 * c1 - a1 * c2;
        var C = a1 * b2 - b1 * a2;
        var D = -A * x1 - B * y1 - C * z1;

        // Calling the first created function

        var [x, y, z] = XandYandZintercept(A, B, C, D);
        document.write(x + " " + y + " " + z);
      }
      // Driver Code
      var x1 = -1;
      var y1 = 2;
      var z1 = 1;
      var x2 = 0;
      var y2 = -3;
      var z2 = 2;
      var x3 = 1;
      var y3 = 1;
      var z3 = -4;

      var p = [x1, y1, z1];
      var q = [x2, y2, z2];
      var r = [x3, y3, z3];

      equation_plane(p, q, r);
    </script>
```

**Output:** 

```
[-4.0, -1.6, -1.1428571428571428]
```

*   **<u>情况 2:</u>** <u>给出 3 个不共线点时。</u>

**示例:**

> **输入:** A = (3，17，2)，B = (4，8，5)，C = (1，8，3)
> T3】输出: 1.5
> -1.8
> 3.0
> 
> **输入:** A = (2，11，4)，B = (7，8，3)，C = (9，18，23)
> T3】输出: 1.0
> 1.75
> 1.4

**方法:**思路是利用三个点找到方程的笛卡尔形式。

*   当给出三个点(x1，y1，z1)，(x2，y2，z2)，(x3，y3，z3)时，下面矩阵的行列式值给出笛卡尔形式。
*   |(x–x1)(y–y1)(z–Z1)|
    |(x2–x1)(y2–y1)(z2–Z1)| = 0
    |(x3–x1)(y3–y1)(z3–Z1)|
*   一旦找到了上面的行列式，就可以使用前面提到的方法找到截距。

下面是上述方法的实现:

## C++

```
// C++ program to find the
// X, Y and Z intercepts of a plane
#include<bits/stdc++.h>
using namespace std;

float * XandYandZintercept( float A, float B,
                            float C, float D)
{
    static float rslt[3];

    // For finding the x-intercept
    // put y = 0 and z = 0
    float x = -D / A;

    // For finding the y-intercept
    // put x = 0 and z = 0
    float y = -D / B ;

    // For finding the z-intercept
    // put x = 0 and y = 0
    float z = -D / C;
    rslt[0] = x;
    rslt[1] = y;
    rslt[2] = z;

    return rslt;
}

void equation_plane(int p[], int q[], int r[])
{
    int x1 = p[0];
    int y1 = p[1];
    int z1 = p[2];
    int x2 = q[0];
    int y2 = q[1];
    int z2 = q[2];
    int x3 = r[0];
    int y3 = r[1];
    int z3 = r[2];

    // For Finding value of A, B, C, D
    int a1 = x2 - x1;
    int b1 = y2 - y1;
    int c1 = z2 - z1;
    int a2 = x3 - x1;
    int b2 = y3 - y1;
    int c2 = z3 - z1;
    int A = b1 * c2 - b2 * c1;
    int B = a2 * c1 - a1 * c2;
    int C = a1 * b2 - b1 * a2;
    int D = (- A * x1 - B * y1 - C * z1);

    // Calling the first created function
    float * rslt=XandYandZintercept(A, B, C, D);
    for(int i = 0; i < 3; i++)
    {
        cout << rslt[i] << " ";
    }
}

// Driver Code
int main()
{
    int x1 =-1;
    int y1 = 2;
    int z1 = 1;
    int x2 = 0;
    int y2 =-3;
    int z2 = 2;
    int x3 = 1;
    int y3 = 1;
    int z3 =-4;

    int p[3] = {x1, y1, z1};
    int q[3] = {x2, y2, z2};
    int r[3] = {x3, y3, z3};
    equation_plane(p, q, r);

}

// This code is contributed by chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// X, Y and Z intercepts of a plane
import java.util.*;

class solution{

static double[] XandYandZintercept( double A, double B,
                            double C, double D)
{
    double []rslt = new double[3];

    // For finding the x-intercept
    // put y = 0 and z = 0
    double x = -D / A;

    // For finding the y-intercept
    // put x = 0 and z = 0
    double y = -D / B ;

    // For finding the z-intercept
    // put x = 0 and y = 0
    double z = -D / C;
    rslt[0] = x;
    rslt[1] = y;
    rslt[2] = z;

    return rslt;
}

static void equation_plane(int []p, int []q, int []r)
{
    int x1 = p[0];
    int y1 = p[1];
    int z1 = p[2];
    int x2 = q[0];
    int y2 = q[1];
    int z2 = q[2];
    int x3 = r[0];
    int y3 = r[1];
    int z3 = r[2];

    // For Finding value of A, B, C, D
    int a1 = x2 - x1;
    int b1 = y2 - y1;
    int c1 = z2 - z1;
    int a2 = x3 - x1;
    int b2 = y3 - y1;
    int c2 = z3 - z1;
    int A = b1 * c2 - b2 * c1;
    int B = a2 * c1 - a1 * c2;
    int C = a1 * b2 - b1 * a2;
    int D = (- A * x1 - B * y1 - C * z1);

    // Calling the first created function
    double []rslt = XandYandZintercept(A, B, C, D);
    for(int i = 0; i < 3; i++)
    {
        System.out.printf(rslt[i]+" ");
    }
}

// Driver Code
public static void main(String args[])
{
    int x1 =-1;
    int y1 = 2;
    int z1 = 1;
    int x2 = 0;
    int y2 =-3;
    int z2 = 2;
    int x3 = 1;
    int y3 = 1;
    int z3 =-4;

    int []p = {x1, y1, z1};
    int []q = {x2, y2, z2};
    int []r = {x3, y3, z3};
    equation_plane(p, q, r);

}
}

// This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python program to find the
# X, Y and Z intercepts of a plane

def XandYandZintercept(A, B, C, D):

    # For finding the x-intercept
    # put y = 0 and z = 0
    x = -D / A

    # For finding the y-intercept
    # put x = 0 and z = 0
    y = -D / B

    # For finding the z-intercept
    # put x = 0 and y = 0
    z = -D / C
    return [x, y, z]

def equation_plane(p, q, r):
    x1 = p[0]
    y1 = p[1]
    z1 = p[2]
    x2 = q[0]
    y2 = q[1]
    z2 = q[2]
    x3 = r[0]
    y3 = r[1]
    z3 = r[2]

    # For Finding value of A, B, C, D
    a1 = x2 - x1
    b1 = y2 - y1
    c1 = z2 - z1
    a2 = x3 - x1
    b2 = y3 - y1
    c2 = z3 - z1
    A = b1 * c2 - b2 * c1
    B = a2 * c1 - a1 * c2
    C = a1 * b2 - b1 * a2
    D = (- A * x1 - B * y1 - C * z1)

    # Calling the first created function
    print(XandYandZintercept(A, B, C, D))

# Driver Code
x1 =-1
y1 = 2
z1 = 1
x2 = 0
y2 =-3
z2 = 2
x3 = 1
y3 = 1
z3 =-4

equation_plane((x1, y1, z1), (x2, y2, z2), (x3, y3, z3))
```

## C#

```
// C# program to find the 
// X, Y and Z intercepts of a plane
using System;
class GFG{

static double[] XandYandZintercept(double A,
                                   double B, 
                                   double C,
                                   double D)
{
  double[] rslt = new double[3];

  // For finding the x-intercept 
  // put y = 0 and z = 0
  double x = -D / A;

  // For finding the y-intercept 
  // put x = 0 and z = 0 
  double y = -D / B ;

  // For finding the z-intercept 
  // put x = 0 and y = 0
  double z = -D / C;
  rslt[0] = x;
  rslt[1] = y;
  rslt[2] = z; 

  return rslt;
}

static void equation_plane(int[] p,
                           int[] q,
                           int[] r)
{
  int x1 = p[0];
  int y1 = p[1];
  int z1 = p[2];
  int x2 = q[0];
  int y2 = q[1];
  int z2 = q[2];
  int x3 = r[0];
  int y3 = r[1];
  int z3 = r[2];

  // For Finding value
  // of A, B, C, D
  int a1 = x2 - x1;
  int b1 = y2 - y1;
  int c1 = z2 - z1;
  int a2 = x3 - x1;
  int b2 = y3 - y1;
  int c2 = z3 - z1;
  int A = (b1 * c2 -
           b2 * c1);
  int B = (a2 * c1 -
           a1 * c2);
  int C = (a1 * b2 -
           b1 * a2);
  int D = (- A * x1 -
           B * y1 -
           C * z1);

  // Calling the first
  // created function 
  double[] rslt = XandYandZintercept(A, B,
                                     C, D);
  for(int i = 0; i < 3; i++)
  {
    Console.Write(rslt[i] + " ");
  }
}

// Driver code
static void Main()
{
  int x1 =-1;
  int y1 = 2;
  int z1 = 1;
  int x2 = 0;
  int y2 =-3;
  int z2 = 2;
  int x3 = 1;
  int y3 = 1;
  int z3 =-4;

  int[] p = {x1, y1, z1};
  int[] q = {x2, y2, z2};
  int[] r = {x3, y3, z3};
  equation_plane(p, q, r);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript program to find the
// X, Y and Z intercepts of a plane
function XandYandZintercept(A, B, C, D)
{
    let rslt = new Array(3);

    // For finding the x-intercept
    // put y = 0 and z = 0
    let x = -D / A;

    // For finding the y-intercept
    // put x = 0 and z = 0
    let y = -D / B ;

    // For finding the z-intercept
    // put x = 0 and y = 0
    let z = -D / C;
    rslt[0] = x;
    rslt[1] = y;
    rslt[2] = z;

    return rslt;
}

function equation_plane(p, q, r)
{
    let x1 = p[0];
    let y1 = p[1];
    let z1 = p[2];
    let x2 = q[0];
    let y2 = q[1];
    let z2 = q[2];
    let x3 = r[0];
    let y3 = r[1];
    let z3 = r[2];

    // For Finding value of A, B, C, D
    let a1 = x2 - x1;
    let b1 = y2 - y1;
    let c1 = z2 - z1;
    let a2 = x3 - x1;
    let b2 = y3 - y1;
    let c2 = z3 - z1;
    let A = b1 * c2 - b2 * c1;
    let B = a2 * c1 - a1 * c2;
    let C = a1 * b2 - b1 * a2;
    let D = (- A * x1 - B * y1 - C * z1);

    // Calling the first created function
    let rslt = XandYandZintercept(A, B, C, D);
    for(let i = 0; i < 3; i++)
    {
        document.write(rslt[i] + " ");
    }
}

// Driver Code
let x1 = -1;
let y1 = 2;
let z1 = 1;
let x2 = 0;
let y2 = -3;
let z2 = 2;
let x3 = 1;
let y3 = 1;
let z3 = -4;

let p = [ x1, y1, z1 ];
let q = [ x2, y2, z2 ];
let r = [ x3, y3, z3 ];

equation_plane(p, q, r);

// This code is contributed by rag2127

</script>
```

**Output:** 

```
[-0.11538461538461539, -0.42857142857142855, -0.3333333333333333]
```