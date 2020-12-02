# 在给定约束下交替移动权重比例

> 原文： [https://www.geeksforgeeks.org/move-weighting-scale-alternate-given-constraints/](https://www.geeksforgeeks.org/move-weighting-scale-alternate-given-constraints/)

给定一个权重标度和一系列不同的正权重，其中每个权重都有无限的供应量。 我们的任务是将砝码一个一个地放置在左右秤盘上，使秤盘移动到放置砝码的那一侧，即每次秤盘都移动到另一侧。

*   我们还获得了另一个整数“步数”，即执行此操作所需的时间。
*   另一个限制是我们不能连续放置相同的重量，即，如果使用重量 w，则在下一步将重量放到相对的锅上时，我们不能再次使用 w。

**示例：**

```
Let weight array is [7, 11]  and steps = 3 
then 7, 11, 7 is the sequence in which 
weights should be kept in order to move
scale alternatively.

Let another weight array is [2, 3, 5, 6] 
and steps = 10 then, 3, 2, 3, 5, 6, 5, 3, 
2, 3 is the sequence in which weights should
be kept in order to move scale alternatively.

```

通过在比例状态之间进行 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 可以解决此问题。

1.  我们遍历各种 DFS 状态以获得解决方案，其中每个 DFS 状态将对应于左右平移之间的实际差值和当前步数。
2.  我们不存储两个锅的重量，而是存储残差值，每次选择的重量值都应大于该差值，并且不应该等于先前选择的重量值。
3.  如果是这样，那么我们将使用新的差值和一个新的步骤递归调用 DFS 方法。

请参见下面的代码以更好地了解

## C ++

```

// C++ program to print weights for alternating 
// the weighting scale 
#include <bits/stdc++.h> 
using namespace std; 

// DFS method to traverse among states of weighting scales 
bool dfs(int residue, int curStep, int wt[], int arr[], 
         int N, int steps) 
{ 
    // If we reach to more than required steps, 
    // return true 
    if (curStep > steps) 
        return true; 

    // Try all possible weights and choose one which 
    // returns 1 afterwards 
    for (int i = 0; i < N; i++) 
    { 
        /* Try this weight only if it is greater than 
           current residueand not same as previous chosen 
           weight */
        if (arr[i] > residue && arr[i] != wt[curStep - 1]) 
        { 
            // assign this weight to array and recur for 
            // next state 
            wt[curStep] = arr[i]; 
            if (dfs(arr[i] - residue, curStep + 1, wt, 
                    arr, N, steps)) 
                return true; 
        } 
    } 

    //    if any weight is not possible, return false 
    return false; 
} 

// method prints weights for alternating scale and if 
// not possible prints 'not possible' 
void printWeightsOnScale(int arr[], int N, int steps) 
{ 
    int wt[steps]; 

    // call dfs with current residue as 0 and current 
    // steps as 0 
    if (dfs(0, 0, wt, arr, N, steps)) 
    { 
        for (int i = 0; i < steps; i++) 
            cout << wt[i] << " "; 
        cout << endl; 
    } 
    else
        cout << "Not possible\n"; 
} 

//    Driver code to test above methods 
int main() 
{ 
    int arr[] = {2, 3, 5, 6}; 
    int N = sizeof(arr) / sizeof(int); 

    int steps = 10; 
    printWeightsOnScale(arr, N, steps); 
    return 0; 
} 

```