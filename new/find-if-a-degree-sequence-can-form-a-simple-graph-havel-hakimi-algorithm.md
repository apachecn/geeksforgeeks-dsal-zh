# 查找度数序列是否可以形成简单图形| Havel-Hakimi 算法

> 原文： [https://www.geeksforgeeks.org/find-if-a-degree-sequence-can-form-a-simple-graph-havel-hakimi-algorithm/](https://www.geeksforgeeks.org/find-if-a-degree-sequence-can-form-a-simple-graph-havel-hakimi-algorithm/)

给定非负整数 **arr []** 的序列，任务是检查是否存在与该度序列相对应的简单图。 **注意**简单图是没有自环和平行边的图。

**示例**：

> **输入**：arr [] = {3、3、3、3}
> **输出**：是
> 这实际上是一个完整的图形（K <sub>4</sub> ）
> 
> **输入**：arr [] = {3，2，1，0}
> **输出**：否
> 一个顶点的度为 n-1，因此它与所有其他顶点相连 n-1 个顶点。
> 但是另一个顶点的度为 0，即孤立。 这是一个矛盾。

**方法**：一种检查简单图是否存在的方法是 [Havel-Hakimi 算法](https://en.wikipedia.org/wiki/Havel%E2%80%93Hakimi_algorithm)，如下所示：

*   以非递增顺序对非负整数序列进行排序。
*   删除第一个元素（例如 V）。 从下一个 V 元素中减去 1。
*   重复 1 和 2，直到满足停止条件之一。

停止条件：

*   剩余的所有元素都等于 0（存在简单图）。
*   减后遇到负数（不存在简单图形）。
*   减去步骤剩余的元素不足（没有简单的图形）。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if
// a simple graph exists
bool graphExists(vector<int> &a, int n)
{
    // Keep performing the operations until one
    // of the stopping condition is met
    while (1)
    {
        // Sort the list in non-decreasing order
        sort(a.begin(), a.end(), greater<>());

        // Check if all the elements are equal to 0
        if (a[0] == 0)
            return true;

        // Store the first element in a variable
        // and delete it from the list
        int v = a[0];
        a.erase(a.begin() + 0);

        // Check if enough elements
        // are present in the list
        if (v > a.size())
            return false;

        // Subtract first element from next v elements
        for (int i = 0; i < v; i++)
        {
            a[i]--;

            // Check if negative element is
            // encountered after subtraction
            if (a[i] < 0)
                return false;
        }
    }
}

// Driver Code
int main()
{
    vector<int> a = {3, 3, 3, 3};
    int n = a.size();

    graphExists(a, n) ? cout << "Yes" : 
                        cout << "NO" << endl;

    return 0;
}

// This code is contributed by
// sanjeev2552

```

## Python

```py

# Python implementation of the approach 

# Function that returns true if 
# a simple graph exists
def graphExists(a):

    # Keep performing the operations until one 
    # of the stopping condition is met
    while True: 

        # Sort the list in non-decreasing order
        a = sorted(a, reverse = True)

        # Check if all the elements are equal to 0
        if a[0]== 0 and a[len(a)-1]== 0:
            return True

        # Store the first element in a variable
        # and delete it from the list
        v = a[0]
        a = a[1:]

        # Check if enough elements 
        # are present in the list
        if v>len(a): 
            return False

        # Subtract first element from next v elements
        for i in range(v):
            a[i]-= 1

            # Check if negative element is 
            # encountered after subtraction
            if a[i]<0:
                return False

# Driver code
a = [3, 3, 3, 3]
if(graphExists(a)):
    print("Yes")
else:
    print("No")

```

## C#

```cs

// C# implementation of the approach 
using System;
using System.Collections; 

class GFG{

// Function that returns true if 
// a simple graph exists 
static bool graphExists(ArrayList a, int n) 
{ 

    // Keep performing the operations until one 
    // of the stopping condition is met 
    while (true) 
    { 

        // Sort the list in non-decreasing order 
        a.Sort();
        a.Reverse();

        // Check if all the elements are equal to 0 
        if ((int)a[0] == 0) 
            return true; 

        // Store the first element in a variable 
        // and delete it from the list 
        int v = (int)a[0]; 
        a.Remove(a[0]); 

        // Check if enough elements 
        // are present in the list 
        if (v > a.Count) 
            return false; 

        // Subtract first element from 
        // next v elements 
        for(int i = 0; i < v; i++) 
        { 
            a[i] = (int)a[i] - 1; 

            // Check if negative element is 
            // encountered after subtraction 
            if ((int)a[i] < 0) 
                return false; 
        } 
    } 
} 

// Driver Code
public static void Main(string[] args) 
{
    ArrayList a = new ArrayList(){ 3, 3, 3, 3 }; 
    int n = a.Count; 

    if (graphExists(a, n))
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("NO");
    }
}
}

// This code is contributed by rutvik_56

```

**Output:** 

```
Yes

```

注意怪胎！ 通过 [**Python 编程基础**](https://practice.geeksforgeeks.org/courses/Python-Foundation?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=GFG_Article_Bottom_Python_Foundation) 课程加强基础，并学习基础知识。

首先，您的面试准备将通过 [**Python DS**](https://practice.geeksforgeeks.org/courses/Data-Structures-With-Python?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=GFG_Article_Bottom_Python_DS) 课程来增强您的数据结构概念。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。