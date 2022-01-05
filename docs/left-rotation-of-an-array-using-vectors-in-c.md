# 使用 C++中的向量向左旋转数组

> 原文:[https://www . geeksforgeeks . org/左-使用 c 中向量旋转数组/](https://www.geeksforgeeks.org/left-rotation-of-an-array-using-vectors-in-c/)

给定一个整数数组 **arr[]** 和另一个整数 **D** ，任务是在数组上执行 **D** 左旋转并打印修改后的数组。

**示例:**

```
Input: arr[] = {1, 2, 3, 4, 5, 6}, D = 2
Output: 3 4 5 6 1 2

Input: arr[] = {1, 2, 3, 4, 5, 6}, D = 12
Output: 1 2 3 4 5 6

```

**方法:**在 C++中使用[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，可以通过从向量中移除第一个元素，然后将其插入同一向量的末尾来执行旋转。同样，可以执行所有需要的旋转，然后打印修改后的向量的内容，以获得所需的旋转数组。

下面是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to left rotate the array by d elements
// here we are passing vector by reference to avoid copying
// that just make our program slow
void rotate(vector<int>& vec, int d)
{
    // Base case
    if (d == 0)
        return;

    // Push first d elements from the beginning
    // to the end and remove those elements
    // from the beginning
    for (int i = 0; i < d; i++)
    {
        // adding first element at
        // the end of vector
        vec.push_back(vec[0]);

        // removing first element
        vec.erase(vec.begin());
    }

    // Print the rotated array
    for (int i = 0; i < vec.size(); i++)
    {
        cout << vec[i] << " ";
    }
}

// Driver code
int main()
{
    vector<int> vec = { 1, 2, 3, 4, 5, 6 };
    int n = vec.size();
    int d = 2;

    // Function call
    rotate(vec, d % n);

    return 0;
}
```

**Output**

```
3 4 5 6 1 2 
```