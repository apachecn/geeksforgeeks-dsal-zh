# 从给定路径

停止的最少站数

二维空间中有许多需要按特定顺序访问的点。 始终选择从一个点到另一个点的路径，因为路径的最短部分始终与网格线对齐。 现在我们获得了用于访问点的选择路径，我们需要告知生成给定路径所需的最小点数。

示例：

```

In above diagram, we can see that there 
must be at least 3 points to get above 
path, which are denoted by A, B and C

```c

我们可以通过观察停靠点的运动方式来解决此问题。 如果我们想从一个点到另一个点采用最短的路径，那么我们将在一个或最大两个方向上移动，即始终可以沿着最大两个方向到达另一个点，如果使用了两个以上的方向，则该路径 不会是最短的，例如，路径 LLURD 只能用 LLL 代替，因此要找到路径中的最小停靠点，我们将遍历路径的字符并维护到目前为止的方向图。 如果在任何索引处我们同时找到了“ L”和“ R”，或者同时找到了“ U”和“ D”，那么当前索引必须有一个止损，因此我们将止损计数增加一个，然后我们 会清除下一段的地图。

解决方案的总时间复杂度为 O（N）

```
// C++ program to find minimum number of points
// in a given path
#include <bits/stdc++.h>
using namespace std;
[
// method returns minimum number of points in given path
int numberOfPointInPath(string path)
{
int N = path.length();
[
// Map to store last occurrence of direction
map< char , int > dirMap;
// variable to store count of points till now,
// initializing from 1 to count first point
int points = 1;
]
// looping over all characters of path string
for ( int i = 0; i < N; i++) {
// storing current direction in curDir
// variable
char curDir = path[i];
// marking current direction as visited
dirMap[curDir] = 1;
// if at current index, we found both 'L'
// and 'R' or 'U' and 'D' then current
// index must be a point
if ((dirMap[ 'L' ] && dirMap[ 'R' ]) ||
(dirMap[ 'U' ] && dirMap[ 'D' ])) {
// clearing the map for next segment
dirMap.clear();
// increasing point count
points++;
// revisitng current direction for next segment
dirMap[curDir] = 1; ]
}
}
// +1 to count the last point also
return (points + 1);
}
// Driver code to test above methods
int main()
[HTG21 4] {
string path = "LLUUULLDD" ;
cout << numberOfPointInPath(path) << endl;
return 0;
}
```

输出：

```
3

```

本文由 **[Utkarsh Trivedi](https://in.linkedin.com/in/utkarsh-trivedi-253069a7)** 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

