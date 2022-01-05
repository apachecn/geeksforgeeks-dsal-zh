# 检查视塔问题是否发生

> 原文:[https://www . geeksforgeeks . org/check-如果发生或不发生视距塔问题/](https://www.geeksforgeeks.org/check-if-the-tower-of-sight-issue-occurs-or-not/)

给定需要建造塔的四个坐标 **A、B、C** 和 **D** ，任务是检查是否出现塔视线问题。

> 如果位于 **A** 或 **C** 的塔位于连接 **B** 和 **D** 的直线上，或者反之亦然，则会出现塔视线问题。

**例:**

> **输入:** A = (0，0)，B = (0，-2)，C = (2，0)，D = (0，2)
> T3】输出:是
> T6】说明:
> 塔 A 位于连接 B 和 D 的直线上
> **输入:** A = (0，0)，B = (0，-2)，C = (2，0)，D = (0，-5)
> **输出:**否

**进场:**

*   如果 A 和 C[平行于 X 轴](https://www.geeksforgeeks.org/program-check-points-parallel-x-axis-y-axis/)，检查 B 或 D 的 y 坐标是否等于 A 和 C 的 y 坐标，X 坐标是否在 A 和 C 之间。
*   如果 A 和 C[平行于 Y 轴](https://www.geeksforgeeks.org/program-check-points-parallel-x-axis-y-axis/)，检查 B 或 D 的 x 坐标是否等于 A 和 C 的 x 坐标，Y 坐标是否在 A 和 C 之间。
*   否则，检查 B 或 D 是否满足 A 和 c 的[线方程](https://www.geeksforgeeks.org/program-find-line-passing-2-points/)
*   同样，按照上述三个步骤检查 A 或 C 是否位于 B 或 d 之间

下面的代码是上述方法的实现:

## C++

```
// C++ program to check if tower
// of sight issue occurs or not

#include <bits/stdc++.h>
using namespace std;

// Function to check if point p lies in
// between the line joining p1 and p2
int checkIntersection(pair<int, int> p1,
                      pair<int, int> p2,
                      pair<int, int> p)
{
    int val;

    // If parallel to X-axis
    if (p1.second == p2.second
        && p1.second == p.second) {

        if (p.first <= max(p1.first, p2.first)
            && (p.first >= min(p1.first, p2.first)))

            // Point p lies between p1 and p2
            return 1;
    }

    // If parallel to Y-axis
    if (p1.first == p2.first
        && p1.first == p.first) {

        if (p.second <= max(p1.second, p2.second)
            && (p.second >= min(p1.second, p2.second)))

            // Point p lies between p1 and p2
            return 1;
    }

    // If point p satisfies the equation
    // of line joining p1 and p2
    else {
        val = (p.second - p1.second)
                  * (p2.first - p1.first)
              - (p.first - p1.first)
                    * (p2.second - p1.second);

        if (val == 0)
            if ((p.first <= max(p1.first, p2.first)
                 && (p.first >= min(p1.first, p2.first)))
                && (p.second <= max(p1.second, p2.second)
                    && (p.second >= min(p1.second, p2.second))))
                return 1;
    }

    return 0;
}

// Function to check if tower
// of sight issue occurred
void towerOfSight(pair<int, int> a,
                  pair<int, int> b,
                  pair<int, int> c,
                  pair<int, int> d)
{
    int flag = 0;

    if (checkIntersection(a, c, b))

        // B lies between AC
        flag = 1;

    else if (checkIntersection(a, c, d))

        // D lies between AC
        flag = 1;

    else if (checkIntersection(b, d, a))

        // A lies between BD
        flag = 1;

    else if (checkIntersection(b, d, c))

        // C lies between BD
        flag = 1;

    flag ? cout << "Yes\n"
         : cout << "No\n";
}

// Driver code
int main()
{
    // Point A
    pair<int, int> a = { 0, 0 };

    // Point B
    pair<int, int> b = { 0, -2 };

    // Point C
    pair<int, int> c = { 2, 0 };

    // Point D
    pair<int, int> d = { 0, 2 };

    towerOfSight(a, b, c, d);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if tower
// of sight issue occurs or not
class GFG{

static class pair
{
    int first, second;
    public pair(int first, int second) 
    {
        this.first = first;
        this.second = second;
    }   
}

// Function to check if point p lies in
// between the line joining p1 and p2
static int checkIntersection(pair p1,
                      pair p2,
                      pair p)
{
    int val;

    // If parallel to X-axis
    if (p1.second == p2.second
        && p1.second == p.second) {

        if (p.first <= Math.max(p1.first, p2.first)
            && (p.first >= Math.min(p1.first, p2.first)))

            // Point p lies between p1 and p2
            return 1;
    }

    // If parallel to Y-axis
    if (p1.first == p2.first
        && p1.first == p.first) {

        if (p.second <= Math.max(p1.second, p2.second)
            && (p.second >= Math.min(p1.second, p2.second)))

            // Point p lies between p1 and p2
            return 1;
    }

    // If point p satisfies the equation
    // of line joining p1 and p2
    else {
        val = (p.second - p1.second)
                  * (p2.first - p1.first)
              - (p.first - p1.first)
                    * (p2.second - p1.second);

        if (val == 0)
            if ((p.first <= Math.max(p1.first, p2.first)
                 && (p.first >= Math.min(p1.first, p2.first)))
                && (p.second <= Math.max(p1.second, p2.second)
                    && (p.second >= Math.min(p1.second, p2.second))))
                return 1;
    }

    return 0;
}

// Function to check if tower
// of sight issue occurred
static void towerOfSight(pair a,
                  pair b,
                  pair c,
                  pair d)
{
    int flag = 0;

    if (checkIntersection(a, c, b) == 1)

        // B lies between AC
        flag = 1;

    else if (checkIntersection(a, c, d) == 1)

        // D lies between AC
        flag = 1;

    else if (checkIntersection(b, d, a) == 1)

        // A lies between BD
        flag = 1;

    else if (checkIntersection(b, d, c) == 1)

        // C lies between BD
        flag = 1;

    System.out.print(flag==1?"Yes\n":"No\n");
}

// Driver code
public static void main(String[] args)
{
    // Point A
    pair a = new pair( 0, 0 );

    // Point B
    pair b = new pair( 0, -2 );

    // Point C
    pair c = new pair( 2, 0 );

    // Point D
    pair d = new pair( 0, 2 );

    towerOfSight(a, b, c, d);

}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 program to check if tower
# of sight issue occurs or not

# Function to check if point p lies in
# between the line joining p1 and p2
def checkIntersection(p1,p2,p):

    # If parallel to X-axis
    if (p1[1] == p2[1]
        and p1[1] == p[1]):

        if (p[0] <= max(p1[0], p2[0])
            and (p[0] >= min(p1[0], p2[0]))):

            # Point p lies between p1 and p2
            return 1

    # If parallel to Y-axis
    if (p1[0] == p2[0]
        and p1[0] == p[0]):

        if (p[1] <= max(p1[1], p2[1])
            and (p[1] >= min(p1[1], p2[1]))):

            # Point p lies between p1 and p2
            return 1

    # If point p satisfies the equation
    # of line joining p1 and p2
    else :
        val = ((p[1] - p1[1])*(p2[0] - p1[0])
              - (p[0] - p1[0])
                    * (p2[1] - p1[1]))

        if (val == 0):
            if ((p[0] <= max(p1[0], p2[0])
                 and (p[0] >= min(p1[0], p2[0])))
                and (p[1] <= max(p1[1], p2[1])
                    and (p[1] >= min(p1[1], p2[1])))):
                return 1

    return 0

# Function to check if tower
# of sight issue occurred
def towerOfSight(a, b, c, d):
    flag = 0

    if (checkIntersection(a, c, b)):

        # B lies between AC
        flag = 1

    elif (checkIntersection(a, c, d)):
        # D lies between AC
        flag = 1

    elif (checkIntersection(b, d, a)):

        # A lies between BD
        flag = 1

    elif (checkIntersection(b, d, c)):

        # C lies between BD
        flag = 1

    if(flag):
        print("Yes")
    else:
        print("No")

# Driver code
if __name__ == "__main__":

    # Point A
    a = [ 0, 0 ]

    # Point B
    b = [ 0, -2 ]

    # Point C
    c = [ 2, 0 ]

    # Point D
    d = [ 0, 2 ]

    towerOfSight(a, b, c, d)

# This code is contributed by chitranayal
```

## C#

```
// C# program to check if tower
// of sight issue occurs or not
using System;

class GFG{

class pair
{
    public int first, second;
    public pair(int first, int second) 
    {
        this.first = first;
        this.second = second;
    }   
}

// Function to check if point p lies in
// between the line joining p1 and p2
static int checkIntersection(pair p1,
                      pair p2,
                      pair p)
{
    int val;

    // If parallel to X-axis
    if (p1.second == p2.second
        && p1.second == p.second) {

        if (p.first <= Math.Max(p1.first, p2.first)
            && (p.first >= Math.Min(p1.first, p2.first)))

            // Point p lies between p1 and p2
            return 1;
    }

    // If parallel to Y-axis
    if (p1.first == p2.first
        && p1.first == p.first) {

        if (p.second <= Math.Max(p1.second, p2.second)
            && (p.second >= Math.Min(p1.second, p2.second)))

            // Point p lies between p1 and p2
            return 1;
    }

    // If point p satisfies the equation
    // of line joining p1 and p2
    else {
        val = (p.second - p1.second)
                  * (p2.first - p1.first)
              - (p.first - p1.first)
                    * (p2.second - p1.second);

        if (val == 0)
            if ((p.first <= Math.Max(p1.first, p2.first)
                 && (p.first >= Math.Min(p1.first, p2.first)))
                && (p.second <= Math.Max(p1.second, p2.second)
                    && (p.second >= Math.Min(p1.second, p2.second))))
                return 1;
    }

    return 0;
}

// Function to check if tower
// of sight issue occurred
static void towerOfSight(pair a,
                  pair b,
                  pair c,
                  pair d)
{
    int flag = 0;

    if (checkIntersection(a, c, b) == 1)

        // B lies between AC
        flag = 1;

    else if (checkIntersection(a, c, d) == 1)

        // D lies between AC
        flag = 1;

    else if (checkIntersection(b, d, a) == 1)

        // A lies between BD
        flag = 1;

    else if (checkIntersection(b, d, c) == 1)

        // C lies between BD
        flag = 1;

    Console.Write(flag==1?"Yes\n":"No\n");
}

// Driver code
public static void Main(String[] args)
{
    // Point A
    pair a = new pair( 0, 0 );

    // Point B
    pair b = new pair( 0, -2 );

    // Point C
    pair c = new pair( 2, 0 );

    // Point D
    pair d = new pair( 0, 2 );

    towerOfSight(a, b, c, d);

}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript program to check if tower
// of sight issue occurs or not

// Function to check if point p lies in
// between the line joining p1 and p2
function checkIntersection(p1,p2,p)
{
    let val;

    // If parallel to X-axis
    if (p1[1] == p2[1]
        && p1[1] == p[1]) {

        if (p[0] <= Math.max(p1[0], p2[0])
            && (p[0] >= Math.min(p1[0], p2[0])))

            // Point p lies between p1 and p2
            return 1;
    }

    // If parallel to Y-axis
    if (p1[0] == p2[0]
        && p1[0] == p[0]) {

        if (p[1] <= Math.max(p1[1], p2[1])
            && (p[1] >= Math.min(p1[1], p2[1])))

            // Point p lies between p1 and p2
            return 1;
    }

    // If point p satisfies the equation
    // of line joining p1 and p2
    else {
        val = (p[1] - p1[1])
                  * (p2[0] - p1[0])
              - (p[0] - p1[0])
                    * (p2[1] - p1[1]);

        if (val == 0)
            if ((p[0] <= Math.max(p1[0], p2[0])
                 && (p[0] >= Math.min(p1[0], p2[0])))
                && (p[1] <= Math.max(p1[1], p2[1])
                    && (p[1] >= Math.min(p1[1], p2[1]))))
                return 1;
    }

    return 0;
}

// Function to check if tower
// of sight issue occurred
function towerOfSight(a,b,c,d)
{
    let flag = 0;

    if (checkIntersection(a, c, b) == 1)

        // B lies between AC
        flag = 1;

    else if (checkIntersection(a, c, d) == 1)

        // D lies between AC
        flag = 1;

    else if (checkIntersection(b, d, a) == 1)

        // A lies between BD
        flag = 1;

    else if (checkIntersection(b, d, c) == 1)

        // C lies between BD
        flag = 1;

    document.write(flag==1?"Yes\n":"No\n");
}

// Driver code

// Point A
let a=[0,0];

// Point B
let b=[0, -2 ];

// Point C
let c=[2, 0 ];

// Point D
let d=[0, 2];
towerOfSight(a, b, c, d);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
Yes
```

时间复杂度:0(1)

辅助空间:0(1)