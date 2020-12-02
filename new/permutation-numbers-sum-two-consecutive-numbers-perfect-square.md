# 数字的排列，使得两个连续数字的和为一个完美的平方

> 原文： [https://www.geeksforgeeks.org/permutation-numbers-sum-two-consecutive-numbers-perfect-square/](https://www.geeksforgeeks.org/permutation-numbers-sum-two-consecutive-numbers-perfect-square/)

**先决条件**：[哈密顿循环](https://www.geeksforgeeks.org/backtracking-set-7-hamiltonian-cycle/)

给定一个整数 n（> = 2），找到一个从 1 到 n 的数字置换，使得该置换的两个连续数字之和是一个完美的平方。 如果无法进行这种排列，则打印“无解决方案”。

**示例**：

```
Input : 17
Output : [16, 9, 7, 2, 14, 11, 5, 4, 12, 13, 3, 6, 10, 15, 1, 8, 17]
Explanation : 16+9 = 25 = 5*5, 9+7 = 16 = 4*4, 7+2 = 9 = 3*3 and so on.

Input: 20
Output: No Solution

Input : 25
Output : [2, 23, 13, 12, 24, 25, 11, 14, 22, 3, 1, 8,  
          17, 19, 6, 10, 15, 21, 4, 5, 20, 16, 9, 7, 18]

```

**方法**：
我们可以表示一个图，其中从 1 到 n 的数字是图的节点，并且如果（i + j）是理想正方形，则 ith 节点与第 j 个节点之间会有一条边。 然后我们可以搜索图中是否存在任何[哈密顿路径](https://www.geeksforgeeks.org/mathematics-euler-hamiltonian-paths/)。 如果存在至少一条路径，则我们打印一条路径，否则我们将打印“无解决方案”。

![square-sum](img/f650909de318656c59ff8a4c2324492e.png)

**方法**：

```
1\. First list up all the perfect square numbers 
   which we can get by adding two numbers.
   We can get at max (2*n-1). so we will take 
   only the squares up to (2*n-1).
2\. Take an adjacency matrix to represent the graph.
3\. For each number from 1 to n find out numbers with 
   which it can add upto a perfect square number.
   Fill respective cells of the adjacency matrix by 1.
4\. Now find if there is any Hamiltonian path in the 
   graph using backtracking as discussed earlier.  

```

## Python3

```

# Python3 program for Sum-square series using 
# hamiltonian path concept and backtracking 

# Function to check wheter we can add number 
# v with the path in the position pos. 
def issafe(v, graph, path, pos): 

    # if there is no edge between v and the 
    # last element of the path formed so far 
    # return false. 
    if (graph[path[pos - 1]][v] == 0): 
        return False

    # Otherwise if there is an edge between  
    # v and last element of the path formed so 
    # far, then check all the elements of the 
    # path. If v is already in the path return 
    # false. 
    for i in range(pos): 

        if (path[i] == v): 
            return False

    # If none of the previous cases satisfies 
    # then we can add v to the path in the 
    # position pos. Hence return true. 
    return True

# Function to form a path based on the graph. 
def formpath(graph, path, pos): 

    # If all the elements are included in the 
    # path i.e. length of the path is n then 
    # return true i.e. path formed. 
    n = len(graph) - 1
    if (pos == n + 1): 
        return True

    # This loop checks for each element if it 
    # can be fitted as the next element of the 
    # path and recursively finds the next  
    # element of the path. 
    for v in range(1, n + 1): 

        if issafe(v, graph, path, pos): 
            path[pos] = v 

            # Recurs for next element of the path. 
            if (formpath(graph, path, pos + 1) == True): 
                return True

            # If adding v does not give a solution 
            # then remove it from path 
            path[pos] = -1

    # if any vertex cannot be added with the  
    # formed path then return false and  
    # backtracks. 
    return False

# Function to find out sum-square series. 
def hampath(n): 

    # base case: if n = 1 there is no solution 
    if n == 1: 
        return 'No Solution'

    # Make an array of perfect squares from 1  
    # to (2 * n-1) 
    l = list() 

    for i in range(1, int((2 * n-1) ** 0.5) + 1): 
        l.append(i**2) 

    # Form the graph where sum of two adjacent 
    # vertices is a perfect square 
    graph = [[0 for i in range(n + 1)] for j in range(n + 1)] 

    for i in range(1, n + 1): 
        for ele in l: 

            if ((ele-i) > 0 and (ele-i) <= n 
                and (2 * i != ele)): 
                graph[i][ele - i] = 1
                graph[ele - i][i] = 1

    # strating from 1 upto n check for each  
    # element i if any path can be formed  
    # after taking i as the first element. 
    for j in range(1, n + 1): 
        path = [-1 for k in range(n + 1)] 
        path[1] = j 

        # If starting from j we can form any path 
        # then we will return the path 
        if formpath(graph, path, 2) == True: 
            return path[1:] 

    # If no path can be formed at all return 
    # no solution. 
    return 'No Solution'

# Driver Function 
print(17, '->', hampath(17)) 
print(20, '->', hampath(20)) 
print(25, '->', hampath(25)) 

```

**输出**：

```
17 -> [16, 9, 7, 2, 14, 11, 5, 4, 12, 13, 3, 6, 10, 15, 1, 8, 17]
20 -> No Solution
25 -> [2, 23, 13, 12, 24, 25, 11, 14, 22, 3, 1, 8, 17, 19, 6, 10, 
       15, 21, 4, 5, 20, 16, 9, 7, 18]

```

**讨论**：
这种回溯算法花费指数时间来找到哈密顿路径。 因此，该算法的时间复杂度是指数级的。
在 hampath（n）函数的最后一部分中，如果我们只是打印路径而不是返回路径，则它将打印所有可能的汉密尔顿路径，即所有可能的表示形式。
实际上，对于 n = 15，我们首先会得到这样的表示。对于 n < 15，没有表示。 对于 n = 18、19、20、21、22、24，也没有哈密顿路径。 对于其余的数字，效果很好。

参考：[亲爱的人](http://www.numberphile.com/)



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。