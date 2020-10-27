# 在给定的 N 个三角形中查找唯一三角形的数量

给定 N 个元素的三个数组 a []，b []和 c []，它们代表 **N** 个三角形的三个边。 任务是找到给定三角形中唯一的三角形数量。 如果三角形的所有边与其他三角形的所有边都匹配，则该三角形是非唯一的。

**示例：**

> **输入：** a [] = {1，2}，b [] = {2，3}，c [] = {3，5}
> **输出：** 2 [ [三角形]的三角形分别具有边 1、2、3 和 2、3、5。
> 他们都没有相同的一面。 因此，两者都是独特的。
> 
> **输入：** a [] = {7，5，8，2，2}，b [] = {6，7，2，3，4}，c [] = {5，6，9 、、 4、3}
> **输出：** 1
> 只有带有边 8、2 和 9 的三角形才是唯一的。

**方法：**的想法是，对于每个三角形，将其所有边排序，然后将其存储在地图中，如果地图中已经存在这三个边，则将频率增加 1，否则将其频率 将会是 1。地图中最后出现频率为 1 的元素的数量就是答案。

下面是上述方法的实现：

## C ++

```

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to return the number of unique triangles 
int UniqueTriangles(int a[], int b[], int c[], int n) 
{ 
    vector<int> sides[n]; 

    // Map to store the frequency of triangles 
    // with same sides 
    map<vector<int>, int> m; 

    for (int i = 0; i < n; i++) { 

        // Push all the sides of the current triangle 
        sides[i].push_back(a[i]); 
        sides[i].push_back(b[i]); 
        sides[i].push_back(c[i]); 

        // Sort the three sides 
        sort(sides[i].begin(), sides[i].end()); 

        // Store the frequency of the sides 
        // of the triangle 
        m[sides[i]] = m[sides[i]] + 1; 
    } 

    map<vector<int>, int>::iterator i; 

    // To store the count of unique triangles 
    int count = 0; 
    for (i = m.begin(); i != m.end(); i++) { 

        // If current triangle has unique sides 
        if (i->second == 1) 
            count++; 
    } 

    return count; 
} 

// Driver code 
int main() 
{ 
    int a[] = { 7, 5, 8, 2, 2 }; 
    int b[] = { 6, 7, 2, 3, 4 }; 
    int c[] = { 5, 6, 9, 4, 3 }; 

    int n = sizeof(a) / sizeof(int); 

    cout << UniqueTriangles(a, b, c, n); 

    return 0; 
} 

```

## Python3

```

# Python3 implementation of the approach 
from collections import defaultdict 

# Function to return the number 
# of unique triangles 
def UniqueTriangles(a, b, c, n): 

    sides = [None for i in range(n)] 

    # Map to store the frequency of  
    # triangles with same sides 
    m = defaultdict(lambda:0) 

    for i in range(0, n): 

        # Push all the sides of the current triangle 
        sides[i] = (a[i], b[i], c[i])  

        # Sort the three sides 
        sides[i] = tuple(sorted(sides[i])) 

        # Store the frequency of the sides 
        # of the triangle 
        m[sides[i]] += 1

    # To store the count of unique triangles 
    count = 0
    for i in m:  

        # If current triangle has unique sides 
        if m[i] == 1: 
            count += 1

    return count 

# Driver code 
if __name__ == "__main__": 

    a = [7, 5, 8, 2, 2]  
    b = [6, 7, 2, 3, 4]  
    c = [5, 6, 9, 4, 3]  

    n = len(a) 

    print(UniqueTriangles(a, b, c, n)) 

# This code is contributed by Rituraj Jain 

```

**Output:**

```
1

```

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。