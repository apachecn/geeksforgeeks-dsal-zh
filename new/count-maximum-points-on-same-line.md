# 计算同一条线上的最大点数

给定二维平面上的 N 个点作为（x，y）坐标对，我们需要找到同一条线上的最大点数。

例子：

```
Input : points[] = {-1, 1}, {0, 0}, {1, 1}, 
                    {2, 2}, {3, 3}, {3, 4} 
Output : 4
Then maximum number of point which lie on same
line are 4, those point are {0, 0}, {1, 1}, {2, 2},
{3, 3}

```

我们可以通过以下方法解决上述问题–对于每个点 p，计算其与其他点的斜率，并使用地图记录有多少点具有相同的斜率，由此我们可以找出与 p 在同一线上的点数。 一点。 对于每个点，继续做同样的事情，并更新到目前为止找到的最大点数。

在实现中需要注意的一些事情是：
1）如果两个点分别是（x1，y1）和（x2，y2），则它们的斜率将是（y2 – y1）/（x2 – x1），可以是双精度值 并可能导致精度问题。 为了消除精度问题，我们将斜率视为对（（y2 – y1），（x2 – x1））而不是比率，并在插入地图之前将其对的 gcd 减小。 在下面的代码中，垂直或重复的代码点将单独处理。

2）如果我们使用 c ++ 中的 [unordered_map 或 Java](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/) 中的 [HashMap 来存储斜率对，则解的总时间复杂度将为 O（n ^ 2）](https://www.geeksforgeeks.org/hashmap-treemap-java/)

## C ++

```

/* C/C++ program to find maximum number of point 
which lie on same line */
#include <bits/stdc++.h> 
#include <boost/functional/hash.hpp> 

using namespace std; 

// method to find maximum colinear point 
int maxPointOnSameLine(vector< pair<int, int> > points) 
{ 
    int N = points.size(); 
    if (N < 2) 
        return N; 

    int maxPoint = 0; 
    int curMax, overlapPoints, verticalPoints; 

    // here since we are using unordered_map  
    // which is based on hash function  
    //But by default we don't have hash function for pairs 
    //so we'll use hash function defined in Boost library 
    unordered_map<pair<int, int>, int,boost:: 
              hash<pair<int, int> > > slopeMap; 

    // looping for each point 
    for (int i = 0; i < N; i++) 
    { 
        curMax = overlapPoints = verticalPoints = 0; 

        // looping from i + 1 to ignore same pair again 
        for (int j = i + 1; j < N; j++) 
        { 
            // If both point are equal then just 
            // increase overlapPoint count 
            if (points[i] == points[j]) 
                overlapPoints++; 

            // If x co-ordinate is same, then both 
            // point are vertical to each other 
            else if (points[i].first == points[j].first) 
                verticalPoints++; 

            else
            { 
                int yDif = points[j].second - points[i].second; 
                int xDif = points[j].first - points[i].first; 
                int g = __gcd(xDif, yDif); 

                // reducing the difference by their gcd 
                yDif /= g; 
                xDif /= g; 

                // increasing the frequency of current slope 
                // in map 
                slopeMap[make_pair(yDif, xDif)]++; 
                curMax = max(curMax, slopeMap[make_pair(yDif, xDif)]); 
            } 

            curMax = max(curMax, verticalPoints); 
        } 

        // updating global maximum by current point's maximum 
        maxPoint = max(maxPoint, curMax + overlapPoints + 1); 

        // printf("maximum colinear point  
        // which contains current point  
        // are : %d\n", curMax + overlapPoints + 1); 
        slopeMap.clear(); 
    } 

    return maxPoint; 
} 

// Driver code 
int main() 
{ 
    const int N = 6; 
    int arr[N][2] = {{-1, 1}, {0, 0}, {1, 1}, {2, 2}, 
                    {3, 3}, {3, 4}}; 

    vector< pair<int, int> > points; 
    for (int i = 0; i < N; i++) 
        points.push_back(make_pair(arr[i][0], arr[i][1])); 

    cout << maxPointOnSameLine(points) << endl; 

    return 0; 
} 

```

## Python3

```

def maxPoints(points): 
        n=len(points) 

        # upto two points all points will be part of the line 
        if n<3: 
            return n 

        max_val=0

        # looping for each point 
        for i in points: 

            # Creating a dictionary for every new 
            # point to save memory 
            d = {}  
            dups = 0
            cur_max = 0

            # pairing with all other points  
            for j in points: 
                if i!=j: 
                    if j[0]==i[0]: #vertical line 
                        slope='inf'
                    else: 
                        slope=float(j[1]-i[1])/float(j[0]-i[0]) 

                    # Increasing the frequency of slope and  
                    # updating cur_max for current point(i)  
                    d[slope] = d.get(slope,0)+1
                    cur_max=max(cur_max, d[slope]) 

                # if both points are equal same increase  
                # duplicates count. 
                # Please note that this will also increment 
                # when we map it with itself. 
                # we still do it because we will not have to 
                # add the extra one at the end. 
                else: 
                    dups+=1

            max_val=max(max_val, cur_max+dups) 

        return max_val 

# Driver code 
points = [(-1, 1), (0, 0), (1, 1), (2, 2), (3, 3), (3, 4)] 
print(maxPoints(points)) 

```

本文由 **[Utkarsh Trivedi](https://in.linkedin.com/in/utkarsh-trivedi-253069a7)** 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。