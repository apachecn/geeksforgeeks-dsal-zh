# 曼哈顿和欧几里得距离相同的对

> 原文：[https://www.geeksforgeeks.org/pairs-with-same-manhattan-and-euclidean-distance/](https://www.geeksforgeeks.org/pairs-with-same-manhattan-and-euclidean-distance/)

在给定的笛卡尔平面中，有 N 个点。 任务是找到点对数（A，B）使得

*   点 A 和点 B 不重合。

*   点之间的曼哈顿距离和欧几里得距离应相等。

**注意**：2 点对（A，B）被认为与 2 点对（B，A）相同。

> 曼哈顿距离= **| x2-x1 | + | y2-y1 |**
> 
> 欧氏距离= **（（x2-x1）^ 2 +（y2-y1）^ 2）^ 0.5** 其中点是（x1，y1）和（x2，y2）。

**示例**：

> **输入**：N = 3，点= {{{1，2}，{2，3}，{1，3}}
> **输出**：2
> 对是 ：
> 1）（1、2）和（1，3）
> （1，2）和（1，3）的欧几里德距离= &根；（（（1 – 1） <sup>2</sup> +（3 – 2） <sup>2</sup> ）= 1
> （1，2）和（1，3）的曼哈顿距离= |（1 – 1）| + |（2 – 3）| = 1
> 
> 2）（1，3）和（2，3）
> （1，3）和（2，3）的欧几里德距离= &根；（（（1 – 2） <sup>2</sup> + （3 – 3） <sup>2</sup> ）= 1
> （1，3）和（2，3）的曼哈顿距离= |（1 – 2）| + |（3 – 3）| = 1
> 
> **输入**：N = 3，点= {{{1，1}，{2，3}，{1，1}}
> **输出**：0
> 此处无 对中满足上述两个条件的对

**方法**：求解方程

> | x2-x1 | + | y2-y1 | = sqrt（（x2-x1）^ 2 +（y2-y1）^ 2）

我们得到 **x2 = x1 或 y2 = y1。**

考虑 3 个映射，

1.  映射 X，其中 X [x <sub>i</sub> ]存储其 x 坐标等于 x <sub>i</sub>

的点的数量 2）映射 Y，其中 Y [y <sub>i</sub> ]存储其 y 坐标等于 y <sub>i</sub>

的点数 3）映射 XY，其中 XY [（X <sub>i</sub> ，Y <sub>i</sub> ）]存储与点重合的点数（x <sub>i</sub> y <sub>i</sub> ）

现在，对于所有不同的 x <sub>i，

令 Xans 为具有相同 X 坐标的对数= <sup>X [x <sub>i</sub> ]</sup> <sub>2</sub></sub> =

设 Yans 为具有相同 Y 坐标的对数= <sup>Y [x <sub>i</sub> ]</sup> <sub>2</sub> 对于所有不同的 y <sub>i</sub>

令 XYans 为重合点数= <sup>XY [{x <sub>i</sub> ，y <sub>i</sub> }]</sup> <sub>2</sub> 用于所有不同点（x <sub>i</sub> ，y <sub>i</sub> ）

因此，所需答案= **Xans + Yans – XYans**

下面是上述方法的实现：

## C++

```cpp

// C++ implementtaion of the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to return the number of non coincident 
// pairs of points with manhattan distance 
// equal to euclidean distance 
int findManhattanEuclidPair(pair<int, int> arr[], int n) 
{ 
    // To store frequency of all distinct Xi 
    map<int, int> X; 

    // To store Frequency of all distinct Yi 
    map<int, int> Y; 

    // To store Frequency of all distinct  
    // points (Xi, Yi); 
    map<pair<int, int>, int> XY; 

    for (int i = 0; i < n; i++) { 
        int xi = arr[i].first; 
        int yi = arr[i].second; 

        // Hash xi coordinate 
        X[xi]++; 

        // Hash yi coordinate 
        Y[yi]++; 

        // Hash the point (xi, yi) 
        XY[arr[i]]++; 
    } 

    int xAns = 0, yAns = 0, xyAns = 0; 

    // find pairs with same Xi 
    for (auto xCoordinatePair : X) { 
        int xFrequency = xCoordinatePair.second; 

        // calculate ((xFrequency) C2) 
        int sameXPairs =  
             (xFrequency * (xFrequency - 1)) / 2; 
        xAns += sameXPairs; 
    } 

    // find pairs with same Yi 
    for (auto yCoordinatePair : Y) { 
        int yFrequency = yCoordinatePair.second; 

        // calculate ((yFrequency) C2) 
        int sameYPairs = 
                (yFrequency * (yFrequency - 1)) / 2; 
        yAns += sameYPairs; 
    } 

    // find pairs with same (Xi, Yi) 
    for (auto XYPair : XY) { 
        int xyFrequency = XYPair.second; 

        // calculate ((xyFrequency) C2) 
        int samePointPairs =  
             (xyFrequency * (xyFrequency - 1)) / 2; 
        xyAns += samePointPairs; 
    } 

    return (xAns + yAns - xyAns); 
} 

// Driver Code 
int main() 
{ 
    pair<int, int> arr[] = { 
        { 1, 2 }, 
        { 2, 3 }, 
        { 1, 3 } 
    }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    cout << findManhattanEuclidPair(arr, n) << endl; 
    return 0; 
} 

```

## Python3

```py

# Python3 implementtaion of the  
# above approach  
from collections import defaultdict 

# Function to return the number of  
# non coincident pairs of points with  
# manhattan distance equal to  
# euclidean distance  
def findManhattanEuclidPair(arr, n):  

    # To store frequency of all distinct Xi  
    X = defaultdict(lambda:0)  

    # To store Frequency of all distinct Yi  
    Y = defaultdict(lambda:0)  

    # To store Frequency of all distinct  
    # points (Xi, Yi)  
    XY = defaultdict(lambda:0)  

    for i in range(0, n):  
        xi = arr[i][0] 
        yi = arr[i][1]  

        # Hash xi coordinate  
        X[xi] += 1

        # Hash yi coordinate  
        Y[yi] += 1

        # Hash the point (xi, yi)  
        XY[tuple(arr[i])] += 1

    xAns, yAns, xyAns = 0, 0, 0

    # find pairs with same Xi  
    for xCoordinatePair in X:  
        xFrequency = X[xCoordinatePair] 

        # calculate ((xFrequency) C2)  
        sameXPairs = (xFrequency * 
                     (xFrequency - 1)) // 2
        xAns += sameXPairs  

    # find pairs with same Yi  
    for yCoordinatePair in Y:  
        yFrequency = Y[yCoordinatePair]  

        # calculate ((yFrequency) C2)  
        sameYPairs = (yFrequency * 
                     (yFrequency - 1)) // 2
        yAns += sameYPairs  

    # find pairs with same (Xi, Yi)  
    for XYPair in XY:  
        xyFrequency = XY[XYPair]  

        # calculate ((xyFrequency) C2)  
        samePointPairs = (xyFrequency * 
                         (xyFrequency - 1)) // 2
        xyAns += samePointPairs  

    return (xAns + yAns - xyAns)  

# Driver Code  
if __name__ == "__main__": 

    arr = [[1, 2], [2, 3], [1, 3]]  

    n = len(arr)  

    print(findManhattanEuclidPair(arr, n))  

# This code is contributed by Rituraj Jain 

```

**Output:**

```
2

```

**时间复杂度**：O（NlogN），其中 N 是点数

**空间复杂度**：O（N）

[![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)](https://practice.geeksforgeeks.org/courses/competitive-programming-live?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_cp)

* * *

* * *



