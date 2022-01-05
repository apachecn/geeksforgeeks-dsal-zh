# 求队列重建后两个人的距离

> 原文:[https://www . geeksforgeeks . org/find-重建队列后两人之间的距离/](https://www.geeksforgeeks.org/find-the-distance-between-two-person-after-reconstruction-of-queue/)

给定一个 N 大小的 **2D** 数组，其中包含排队的人的不同身高，以及对应于每个人(P)的一个数字，该数字给出了比 P 矮并站在 P 前面的人的数量。任务是按照人的身高的实际顺序确定两个人之间的距离 **A** 和 **B** 。
**例:**

> **输入:** A = 6，B = 5，arr[][] = {{5，0}，{3，0}，{2，0}，
> {6，4}，{1，0}，{4，3 } }
> T4】输出: 4
> 人的身高的实际排列
> {5，0}，{3，0}，{2，0}，{1，0}，{6，4}，{4，3 }
> 6 之间的距离
> **输出:** 1

**天真法:**蛮力法是对凤凰社成员的给定高度尝试所有可能的排列，并验证前面的数字是否与给定序列匹配，然后找出两个人之间的距离。
**时间复杂度:** O(N！)
**高效方法:**另一种方法是存储人的身高及其正面值，存储在任意向量中，按身高升序排序。现在，遍历向量，在位置向量中插入第 k 个位置的人，其中 k 是站在当前人前面的人数。
以下是上述方法的实施:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the correct order and then
// return the distance between the two persons
int getDistance(int arr[][2], int n, int a, int b)
{
    vector<pair<int, int> > vp;

    // Make pair of both height & infront
    // and insert to vector
    for (int i = 0; i < n; i++) {
        vp.push_back({ arr[i][0], arr[i][1] });
    }

    // Sort the vector in ascending order
    sort(vp.begin(), vp.end());

    // Find the correct place for every person
    vector<int> pos;

    // Insert into position vector
    // according to infront value
    for (int i = 0; i < vp.size(); i++) {
        int height = vp[i].first;
        int k = vp[i].second;
        pos.insert(pos.begin() + k, height);
    }

    int first = -1, second = -1;

    for (int i = 0; i < pos.size(); i++) {
        if (pos[i] == a)
            first = i;
        if (pos[i] == b)
            second = i;
    }

    return abs(first - second);
}

// Driver code
int main()
{
    int arr[][2] = {
        { 5, 0 },
        { 3, 0 },
        { 2, 0 },
        { 6, 4 },
        { 1, 0 },
        { 4, 3 }
    };
    int n = sizeof(arr) / sizeof(arr[0]);
    int a = 6, b = 5;

    cout << getDistance(arr, n, a, b);

    return 0;
}
```

## 计算机编程语言

```
# Python implementation of the approach

# Function to find the correct order and then
# return the distance between the two persons
def getDistance(arr, n, a, b):
    vp = []

    # Make pair of both height & infront
    # and insert to vector
    for i in range(n):
        vp.append([arr[i][0], arr[i][1]])

    # Sort the vector in ascending order
    vp = sorted(vp)

    # Find the correct place for every person
    pos = [0 for i in range(n)]

    # Insert into position vector
    # according to infront value
    for i in range(len(vp)):
        height = vp[i][0]
        k = vp[i][1]
        pos[k] = height

    first = -1
    second = -1

    for i in range(n):
        if (pos[i] == a):
            first = i
        if (pos[i] == b):
            second = i

    return abs(first - second)

# Driver code
arr = [[5, 0],
        [3, 0],
        [2, 0],
        [6, 4],
        [1, 0],
        [4, 3]]
n = len(arr)
a = 6
b = 5

print(getDistance(arr, n, a, b))

# This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to find the correct order and then
// return the distance between the two persons   
function getDistance(arr,n,a,b)
{
    let vp=[];
    // Make pair of both height & infront
    // and insert to vector
    for (let i = 0; i < n; i++) {
        vp.push([ arr[i][0], arr[i][1] ]);
    }

    // Sort the vector in ascending order
    vp.sort(function(c,d){return c[0]-d[0];});

    // Find the correct place for every person
    let pos=new Array(n);
    for(let i=0;i<n;i++)
    {
        pos[i]=0;
    }

    // Insert into position vector
    // according to infront value
    for (let i = 0; i < vp.length; i++) {
        let height = vp[i][0];
        let k = vp[i][1];
        pos[k] = height
    }

    let first = -1, second = -1;

    for (let i = 0; i < pos.length; i++) {
        if (pos[i] == a)
            first = i;
        if (pos[i] == b)
            second = i;
    }

    return Math.abs(first - second);
}

// Driver code
let arr = [
        [ 5, 0 ],
        [ 3, 0 ],
        [ 2, 0 ],
        [ 6, 4 ],
        [ 1, 0 ],
        [ 4, 3 ]
    ];
    let n = arr.length;
    let a = 6, b = 5;

    document.write(getDistance(arr, n, a, b));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(n <sup>2</sup> )