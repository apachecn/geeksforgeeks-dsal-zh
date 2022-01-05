# 到所有给定点的欧几里德距离的最小和

> 原文:[https://www . geesforgeks . org/到所有给定点的最小欧几里得距离之和/](https://www.geeksforgeeks.org/minimum-sum-of-euclidean-distances-to-all-given-points/)

给定一个矩阵 **mat[][]** ，该矩阵由 **N** 对形式 **{x，y}** 组成，每对形式表示 **N** 点的坐标，任务是找到到所有点的欧几里得距离的最小和。

**示例:**

> **输入:** mat[][] = { { 0，1}、{ 1，0 }、{ 1，2 }、{ 2，1 }}
> **输出:** : 4
> **解释:**
> 点集的平均值，即质心= ((0+1+1+2)/4，(1+0+2+1)/4) = (1，1)。
> 各点距质心的欧氏距离为{1，1，1，1}
> 所有距离之和= 1 + 1 + 1 + 1 = 4
> **输入:** mat[][] = { { 1，1}，{ 3，3 }}
> **输出:** 2.82843

**方法:**
由于任务是最小化[到所有点的欧氏距离](https://en.wikipedia.org/wiki/Euclidean_distance#:~:text=In%20mathematics%2C%20the%20Euclidean%20distance, metric%20as%20the%20Pythagorean%20metric.)，所以想法是计算所有点的[中值](https://www.geeksforgeeks.org/program-for-mean-and-median-of-an-unsorted-array/)。[几何中值](https://www.geeksforgeeks.org/geometric-median/)将中值的概念推广到更高维度

按照以下步骤解决问题:

*   通过获取点的平均值，计算所有给定坐标的质心。
*   求所有点到质心的欧氏距离。
*   计算这些距离的总和并打印为答案。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate Euclidean distance
double find(double x, double y,
            vector<vector<int> >& p)
{

    double mind = 0;
    for (int i = 0; i < p.size(); i++) {

        double a = p[i][0], b = p[i][1];
        mind += sqrt((x - a) * (x - a)
                     + (y - b) * (y - b));
    }

    return mind;
}

// Function to calculate the minimum sum
// of the euclidean distances to all points
double getMinDistSum(vector<vector<int> >& p)
{

    // Calculate the centroid
    double x = 0, y = 0;
    for (int i = 0; i < p.size(); i++) {
        x += p[i][0];
        y += p[i][1];
    }
    x = x / p.size();
    y = y / p.size();

    // Calculate distance of all
    // points
    double mind = find(x, y, p);

    return mind;
}

// Driver Code
int main()
{

    // Initializing the points
    vector<vector<int> > vec
        = { { 0, 1 }, { 1, 0 }, { 1, 2 }, { 2, 1 } };

    double d = getMinDistSum(vec);
    cout << d << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to calculate Euclidean distance
static double find(double x, double y,
                   int [][] p)
{
    double mind = 0;

    for(int i = 0; i < p.length; i++)
    {
        double a = p[i][0], b = p[i][1];
        mind += Math.sqrt((x - a) * (x - a) +
                          (y - b) * (y - b));
    }
    return mind;
}

// Function to calculate the minimum sum
// of the euclidean distances to all points
static double getMinDistSum(int [][]p)
{

    // Calculate the centroid
    double x = 0, y = 0;
    for(int i = 0; i < p.length; i++)
    {
        x += p[i][0];
        y += p[i][1];
    }

    x = x / p.length;
    y = y / p.length;

    // Calculate distance of all
    // points
    double mind = find(x, y, p);

    return mind;
}

// Driver Code
public static void main(String[] args)
{

    // Initializing the points
    int [][]vec = { { 0, 1 }, { 1, 0 },
                    { 1, 2 }, { 2, 1 } };

    double d = getMinDistSum(vec);

    System.out.print(d + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
from math import sqrt

# Function to calculate Euclidean distance
def find(x, y, p):

    mind = 0
    for i in range(len(p)):
        a = p[i][0]
        b = p[i][1]
        mind += sqrt((x - a) * (x - a) +
                     (y - b) * (y - b))

    return mind

# Function to calculate the minimum sum
# of the euclidean distances to all points
def getMinDistSum(p):

    # Calculate the centroid
    x = 0
    y = 0

    for i in range(len(p)):
        x += p[i][0]
        y += p[i][1]

    x = x // len(p)
    y = y // len(p)

    # Calculate distance of all
    # points
    mind = find(x, y, p)

    return mind

# Driver Code
if __name__ == '__main__':

    # Initializing the points
    vec = [ [ 0, 1 ], [ 1, 0 ],
            [ 1, 2 ], [ 2, 1 ] ]

    d = getMinDistSum(vec)
    print(int(d))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to calculate Euclidean distance
static double find(double x, double y,
                   int [,] p)
{
    double mind = 0;

    for(int i = 0; i < p.GetLength(0); i++)
    {
        double a = p[i,0], b = p[i,1];
        mind += Math.Sqrt((x - a) * (x - a) +
                          (y - b) * (y - b));
    }
    return mind;
}

// Function to calculate the minimum sum
// of the euclidean distances to all points
static double getMinDistSum(int [,]p)
{

    // Calculate the centroid
    double x = 0, y = 0;
    for(int i = 0; i < p.GetLength(0); i++)
    {
        x += p[i,0];
        y += p[i,1];
    }

    x = x / p.Length;
    y = y / p.Length;

    // Calculate distance of all
    // points
    double mind = find(x, y, p);

    return mind;
}

// Driver Code
public static void Main(String[] args)
{

    // Initializing the points
    int [,]vec = { { 0, 1 }, { 1, 0 },
                    { 1, 2 }, { 2, 1 } };

    int d = (int)getMinDistSum(vec);

    Console.Write(d + "\n");
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to calculate Euclidean distance
function find(x, y, p)
{
    let mind = 0;

    for(let i = 0; i < p.length; i++)
    {
        let a = p[i][0], b = p[i][1];
        mind += Math.sqrt((x - a) * (x - a) +
                          (y - b) * (y - b));
    }
    return mind;
}

// Function to calculate the minimum sum
// of the euclidean distances to all polets
function getMinDistSum(p)
{

    // Calculate the centroid
    let x = 0, y = 0;
    for(let i = 0; i < p.length; i++)
    {
        x += p[i][0];
        y += p[i][1];
    }

    x = x / p.length;
    y = y / p.length;

    // Calculate distance of all
    // polets
    let mind = find(x, y, p);

    return mind;
}

// Driver Code

    // Initializing the points
    let vec = [[ 0, 1 ], [ 1, 0 ],
               [ 1, 2 ], [ 2, 1 ]];

    let d = getMinDistSum(vec);

    document.write(d);

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)