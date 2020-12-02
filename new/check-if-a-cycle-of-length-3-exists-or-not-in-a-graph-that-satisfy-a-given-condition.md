# 检查在满足给定条件的图中是否存在长度为 3 的循环。

> 原文： [https://www.geeksforgeeks.org/check-if-a-cycle-of-length-3-exists-or-not-in-a-graph-that-satisfy-a-given-condition/](https://www.geeksforgeeks.org/check-if-a-cycle-of-length-3-exists-or-not-in-a-graph-that-satisfy-a-given-condition/)

给定**的数组 **Arr** N 个**整数，它们代表图形的节点。 在[按位与](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)不等于**零**的那些对之间定义边缘。 任务是查找图中是否存在长度为 3 的循环。

**示例**：

> **输入**：Arr [] = {26，33，35，40，50}
> **输出**：是
> 
> 在 26、33 和 50 之间存在一个循环。
> 
> **输入**：Arrr [] = {17，142，243，300}
> **输出**：否

**天真的方法**：
运行嵌套循环并检查每对之间是否存在边（如果它们的按位 AND 值不为零）。 因此，我们形成整个图，并通过使用[循环检测](https://www.geeksforgeeks.org/detect-cycle-undirected-graph/)方法中的任何一种来检查该图中是否存在循环。

**有效方法**：

*   通过连接至少`3`个边形成一个循环。
*   想法是制作一个二维数组，其中第 i 行存储 Arr [i]的二进制值。
*   接下来，以列方式循环并检查是否存在一列，其中 1 的数目至少为 3。
    *   如果是这样，则表明图中存在一个循环。
    *   如果不存在这样的列，则表示图中没有循环。

> Arr [] = {26，33，35，40，50}
> 
> 2D 数组如下
> bi = [
> [0 1 0 1 1 0 0 0]，
> [1 0 0 0 0 1 0 0]，
> [1 1 0 0 0 1 0 0]，
> [0 0 0 1 0 1 0 0]，
> [0 1 0 0 1 1 0 0]，
> ]
> bi [0] [1]，bi [2 ] [1]和 bi [4] [1]等于 1。这意味着以下对（Arr [0]，Arr [2]），（Arr [2]，Arr [4]的按位与值 ，（Arr [0]，Arr [4]）不为零。 这三个边形成一个循环。

下面是上述方法的实现：

## C ++

```

// C++ implementation of 
// the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Maximum numner of bits in Arr[i] 
#define MAX 64 

// Function to check if a cycle 
// exists in the given graph 
void checkCycle(int ar[], int n) 
{ 
    int bi[n][MAX] = { 0 }, size; 
    bool flag = false; 

    // storing the given ar[i] in 
    // binary in the array 
    // where bi[i] is the 
    // binary value of ar[i] 
    for (int i = 0; i < n; i++) { 
        size = 0; 
        while (ar[i] != 0) { 
            bi[i][size++] = ar[i] % 2; 
            ar[i] = ar[i] / 2; 
        } 
    } 

    // Checking if any column 
    // contains at least 3 1's 
    for (int i = 0; i < MAX; i++) { 
        int ctr = 0; 
        for (int j = 0; j < n; j++) { 
            if (bi[j][i] == 1) 
                ctr = ctr + 1; 
        } 
        if (ctr >= 3) { 

            // If number of 1's is more than 
            // 3, set flag to true and break 
            flag = true; 
            break; 
        } 
    } 

    // if flag is true, it implies 
    // that graph contains a cycle 
    if (flag) 
        cout << "Yes"; 
    // if flag is false, no cycle 
    // is there in the graph 
    else
        cout << "No"; 
} 

// Driver code 
int main() 
{ 
    int ar[] = { 26, 33, 35, 40, 50 }; 
    int n = sizeof(ar) / sizeof(ar[0]); 
    checkCycle(ar, n); 
} 

```