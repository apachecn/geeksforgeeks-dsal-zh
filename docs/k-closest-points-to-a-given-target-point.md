# K 个最接近给定目标点的点

> 原文:[https://www . geesforgeks . org/k-最接近给定目标点/](https://www.geeksforgeeks.org/k-closest-points-to-a-given-target-point/)

给定二维平面上的点列表 **arr[][]** 、给定点 **target** 和整数 **K** 。任务是从给定的点列表中找到最接近**目标**的 **K** 点。

**注:**平面上两点之间的距离为 [**欧氏距离**](https://en.wikipedia.org/wiki/Euclidean_distance#:~:text=In%20mathematics%2C%20the%20Euclidean%20distance,being%20called%20the%20Pythagorean%20distance.) 。

**示例:**

> **输入:**点= [[3，3]，[5，-1]，[-2，4]]，目标= [0，0]，K = 2
> **输出:** [[3，3]，[-2，4]]
> **说明:**目标的距离平方(=原点)距此点为
> (3，3) = 18
> (5，-1) = 26
> (-2，4) = 20
> 
> **输入:**点= [[1，3]，[-2，2]]，目标= [0，1]，K = 1
> **输出:** [[1，3]]

**进场:**解决方案基于[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)。这个想法是计算每个给定点到目标的欧几里得距离，并将它们存储在一个数组中。然后根据找到的欧氏距离对数组进行排序，打印列表中前 k 个最近的点。

下面是上述方法的实现。

## C++

```
// C++ program to implement of above approach
#include <bits/stdc++.h>
using namespace std;

// Calculate the Euclidean distance
// between two points
float distance(int x1, int y1, int x2, int y2)
{
    return sqrt(pow((x1 - x2), 2) +
                pow((y1 - y2), 2));
}

// Function to calculate K closest points
vector<vector<int> > kClosest(
    vector<vector<int> >& points,
    vector<int> target, int K)
{

    vector<vector<int> > pts;
    int n = points.size();
    vector<pair<float, int> > d;

    for (int i = 0; i < n; i++) {
        d.push_back(
            make_pair(distance(points[i][0], points[i][1],
                               target[0], target[1]),
                      i));
    }

    sort(d.begin(), d.end());

    for (int i = 0; i < K; i++) {
        vector<int> pt;
        pt.push_back(points[d[i].second][0]);
        pt.push_back(points[d[i].second][1]);
        pts.push_back(pt);
    }

    return pts;
}

// Driver code
int main()
{
    vector<vector<int> > points
        = { { 1, 3 }, { -2, 2 } };
    vector<int> target = { 0, 1 };
    int K = 1;

    for (auto pt : kClosest(points, target, K)) {
        cout << pt[0] << " " << pt[1] << endl;
    }
    return 0;
}
```

## java 描述语言

```
<script>
        // JavaScript code for the above approach

        // Calculate the Euclidean distance
        // between two points
        function distance(x1, y1, x2, y2)
        {
            return Math.sqrt(Math.pow((x1 - x2), 2) +
                Math.pow((y1 - y2), 2));
        }

        // Function to calculate K closest points
        function kClosest(points,
            target, K)
        {

            let pts = [];
            let n = points.length;
            let d = [];

            for (let i = 0; i < n; i++) {
                d.push({
                        first: distance(points[i][0], points[i][1],
                            target[0], target[1]), second: i
                    });
            }

            d.sort(function (a, b) { return a.first < b.first })

            for (let i = 0; i < K; i++) {
                let pt = [];
                pt.push(points[d[i].second][0]);
                pt.push(points[d[i].second][1]);
                pts.push(pt);
            }

            return pts;
        }

        // Driver code
        let points
            = [[1, 3], [-2, 2]];
        let target = [0, 1];
        let K = 1;

        for (let pt of kClosest(points, target, K)) {
            document.write(pt[0] + " " + pt[1] + '<br>');
        }

  // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
1 3
```

***时间复杂度:**T3】O(N * logN)
T5】T6】辅助空间:T8】O(N)*