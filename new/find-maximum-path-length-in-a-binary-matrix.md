# 在二进制矩阵

中查找最大路径长度

> 原文： [https://www.geeksforgeeks.org/find-maximum-path-length-in-a-binary-matrix/](https://www.geeksforgeeks.org/find-maximum-path-length-in-a-binary-matrix/)

给定方阵*垫*，其每个元素为 *0* 或 *1* 。 值 1 表示已连接，值 0 表示未连接。 任务是在将至少一个 *0* 更改为 *1* 之后，找到矩阵中路径的最大长度。 路径是 1 个 4 方向连接的组。

**示例**：

> **输入**：mat [] [] = {{1，1}，{1，0}}
> **输出**：4
> 仅将 0 更改为 1，然后将 最大路径的长度为 4。
> 
> **输入**：mat [] [] = {{1，1}，{1，1}}
> **输出**：4

**天真的方法**：的想法是将每个“ 0”一一更改为“ 1”，然后执行[深度优先搜索](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)以找到最大路径的大小。

**有效方法**：在幼稚的方法中，我们检查了每个“ 0”。 但是，我们也可以通过存储每个组的大小来提高效率，从而不必使用深度优先搜索来重复计算相同的大小。

**注意**：当 0 碰到同一组时，我们需要注意。 例如，考虑 grid = [[0，1]，[1，1]]。 将 *0* 更改为 *1* 之后， *0* 的右邻居和下邻居将属于同一组。

我们可以通过跟踪组 *Id* （或*索引*）来解决此问题，这对于每个组都是唯一的。

*   对于每个组，用值*索引*填充它，并记住其大小作为数组*区域[Index]* 中的一个元素，可以通过深度优先搜索找到它。
*   然后，对于每个 *0* ，查看相邻的组 ID 并添加这些组的区域，然后为 *0* 添加 *1* 。 这将为我们提供答案，而我们会从先前的答案中获取最大的收益。

下面是上述方法的实现：

## Python

```py

# Python3 implementation of above approach 

# check if index is within range 
def neighbors(r, c, N): 
    for nr, nc in ((r - 1, c), (r + 1, c), (r, c - 1), (r, c + 1)): 
        if 0 <= nr < N and 0 <= nc < N: 
            yield nr, nc 

# dfs to calculate length of path 
def dfs(R, C, index, grid, N): 
    ans = 1
    grid[R][C] = index 
    for nr, nc in neighbors(R, C, N): 
        if grid[nr][nc] == 1: 
            ans += dfs(nr, nc, index) 

    return ans 

# function to return largest possible length of Path 
def largestPath(grid): 

    N = len(grid) 

    area = {} 
    index = 2

    for i in range(N): 
        for j in range(N): 
            if grid[i][j] == 1: 
                area[index] = dfs(i, j, index, grid, N) 
                index += 1

    ans = max(area.values() or [0]) 

    for i in range(N): 
        for j in range(N): 
            if grid[i][j] == 0: 
                seen = {grid[nr][nc] for nr, nc in neighbors(i, j, N) if grid[nr][nc] > 1} 
                ans = max(ans, 1 + sum(area[i] for i in seen)) 

    # return maximum possible length 
    return ans 

# Driver code 
I = [[1, 0], [0, 1]] 

# Function call to print answer 
print(largestPath(I)) 

# This code is written by 
# Sanjit_Prasad 

```

**Output:**

```
3

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。