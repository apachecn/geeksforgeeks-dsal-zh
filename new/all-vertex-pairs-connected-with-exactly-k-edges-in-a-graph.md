# 所有顶点对均与图形

中的 k 个边连接

> 原文： [https://www.geeksforgeeks.org/all-vertex-pairs-connected-with-exactly-k-edges-in-a-graph/](https://www.geeksforgeeks.org/all-vertex-pairs-connected-with-exactly-k-edges-in-a-graph/)

给定一个表示为邻接矩阵和整数“ k”的有向图，任务是找到与确切的“ k”边连接的所有顶点对。
另外，找到可以在完全 k 个边缘中链接两个顶点的方式。

**示例**：

```
Input : k = 3 and graph :
0 1 0 0 0 
0 0 1 0 0 
0 0 0 1 1 
1 0 0 0 0 
0 0 1 0 0 
Output :
1 -> 4 in 1 way(s)
1 -> 5 in 1 way(s)
2 -> 1 in 1 way(s)
2 -> 3 in 1 way(s)
3 -> 2 in 1 way(s)
3 -> 4 in 1 way(s)
3 -> 5 in 1 way(s)
4 -> 3 in 1 way(s)
5 -> 1 in 1 way(s)
5 -> 3 in 1 way(s)

Input : k = 2 and graph :
0 0 0 
1 0 1 
0 1 0 
Output :
2 -> 2 in 1 way(s)
3 -> 1 in 1 way(s)
3 -> 3 in 1 way(s)

```

**方法**：

*   我们将邻接矩阵本身乘以“ k”次。
*   在结果矩阵中，`res[i][j]`是可以从覆盖精确到'k'边的顶点'i'到达顶点'j'的方式数量。

下面是上述方法的实现：

## 爪哇

```

// Java implementation of the approach 
public class KPaths { 

    // Function to multiply two square matrices 
    static int[][] multiplyMatrices(int[][] arr1, int[][] arr2) 
    { 
        int order = arr1.length; 
        int[][] ans = new int[order][order]; 
        for (int i = 0; i < order; i++) { 
            for (int j = 0; j < order; j++) { 
                for (int k = 0; k < order; k++) { 
                    ans[i][j] += arr1[i][k] * arr2[k][j]; 
                } 
            } 
        } 
        return ans; 
    } 

    // Function to find all the pairs that 
    // can be connected with exactly 'k' edges 
    static void solve(int[][] arr, int k) 
    { 
        int[][] res = new int[arr.length][arr[0].length]; 

        // copying arr to res, 
        // which is the result for k=1 
        for (int i = 0; i < res.length; i++) 
            for (int j = 0; j < res.length; j++) 
                res[i][j] = arr[i][j]; 

        // multiplying arr with itself 
        // the required number of times 
        for (int i = 2; i <= k; i++) 
            res = multiplyMatrices(res, arr); 

        for (int i = 0; i < res.length; i++) 
            for (int j = 0; j < res.length; j++) 

                // if there is a path between 'i' 
                // and 'j' in exactly 'k' edges 
                if (res[i][j] > 0) 
                    System.out.println(i + " -> " + j + " in " + res[i][j] + " way(s)"); 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        int[][] arr = new int[5][5]; 
        arr[0][1] = 1; 
        arr[1][2] = 1; 
        arr[2][3] = 1; 
        arr[2][4] = 1; 
        arr[3][0] = 1; 
        arr[4][2] = 1; 
        int k = 3; 
        solve(arr, k); 
    } 
} 

```