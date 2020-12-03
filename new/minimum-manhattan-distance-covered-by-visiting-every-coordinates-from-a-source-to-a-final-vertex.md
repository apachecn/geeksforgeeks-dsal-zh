# 通过访问从源到最终顶点的每个坐标所覆盖的最小曼哈顿距离

> 原文： [https://www.geeksforgeeks.org/minimum-manhattan-distance-covered-by-visiting-every-coordinates-from-a-source-to-a-final-vertex/](https://www.geeksforgeeks.org/minimum-manhattan-distance-covered-by-visiting-every-coordinates-from-a-source-to-a-final-vertex/)

给定坐标点的数组 **arr []** 以及源坐标和最终坐标点，任务是找到从源到最终顶点的最小曼哈顿距离，以使坐标的每个点 数组仅被访问一次。

> 曼哈顿距离= ![\left | x2 - x1 \right | + \left | y2 - y1 \right |](img/38a56f6e5856fcc14f950b22b7fb1fad.png "Rendered by QuickLaTeX.com")

**示例**：

> **输入**：源=（0，0），最终=（100，100）
> arr [] = {（70，40），（30，10），（10，5），（ 90，70），（50，20）}
> **输出**：200
> 
> **输入**：源=（0，0），最终=（5，5）
> arr [] = {（1，1）}
> **输出**：10

**方法**：的想法是使用[置换和组合](https://www.geeksforgeeks.org/permutation-and-combination/)生成每个可能的置换运动到坐标，然后计算从的第一个坐标移动到的曼哈顿总距离 数组到最终坐标，如果最终覆盖的距离小于到目前为止的最小距离。 然后更新覆盖的最小距离。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to find the  
// minimum manhattan distance  
// covered by visiting N co-ordinates 

#include <bits/stdc++.h> 
using namespace std; 

// Class of co-ordinates 
class pairs { 
public: 
    int x; 
    int y; 
}; 

// Function to calculate the  
// manhattan distance between  
// pair of points 
int calculate_distance(pairs a,  
                       pairs b) 
{ 
    return abs(a.x - b.x) +  
           abs(a.y - b.y); 
} 

// Function to find the minimum  
// distance covered for visiting  
// every co-ordinate point 
int findMinDistanceUtil(vector<int> nodes,  
           int noOfcustomer, int** matrix) 
{ 
    int mindistance = INT_MAX; 

    // Loop to compute the distance 
    // for every possible permutation 
    do { 
        int distance = 0; 
        int prev = 1; 

        // Computing every total manhattan 
        // distance covered for the every  
        // co-ordinate points 
        for (int i = 0; i < noOfcustomer; i++) { 
            distance = distance +  
                       matrix[prev][nodes[i]]; 
            prev = nodes[i]; 
        } 

        // Adding the final distance 
        distance = distance + matrix[prev][0]; 

        // if distance is less than  
        // minimum value than update it 
        if (distance < mindistance) 
            mindistance = distance; 
    }while ( 
        next_permutation( 
            nodes.begin(), nodes.end() 
        )); 
    return mindistance; 
} 

// Function to intialize the input 
// and find the minimum distance  
// by visiting every cordinate 
void findMinDistance() 
{ 
    int noOfcustomer = 1; 
    vector<pairs> cordinate; 
    vector<int> nodes; 
    // filling the coordinates into vector 
    pairs office, home, customer; 
    office.x = 0; 
    office.y = 0; 
    cordinate.push_back(office); 
    home.x = 5; 
    home.y = 5; 
    cordinate.push_back(home); 
    customer.x = 1; 
    customer.y = 1; 
    cordinate.push_back(customer); 

    // make a 2d matrix which stores 
    // distance between two point 
    int** matrix = new int*[noOfcustomer + 2]; 

    // Loop to compute the distance between 
    // every pair of points in the co-ordinate 
    for (int i = 0; i < noOfcustomer + 2; i++) { 
        matrix[i] = new int[noOfcustomer + 2]; 

        for (int j = 0; j < noOfcustomer + 2; j++) { 
            matrix[i][j] = calculate_distance( 
                    cordinate[i], cordinate[j]); 
        } 

        // Condition to not move the  
        // index of the source or  
        // the final vertex 
        if (i != 0 && i != 1) 
            nodes.push_back(i); 
    } 
    cout << findMinDistanceUtil( 
        nodes, noOfcustomer, matrix); 
} 

// Driver Code 
int main() 
{ 
    // Function Call 
    findMinDistance(); 
    return 0; 
} 

```

**Output:**

```
10

```

**效果分析**：

*   **时间复杂度**：*O（N！* N）*

*   **辅助空间**：*`O(N^2)`*



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。