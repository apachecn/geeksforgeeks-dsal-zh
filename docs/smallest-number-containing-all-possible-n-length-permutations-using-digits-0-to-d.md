# 最小的数字，包含使用数字 0 到 D 的所有可能的 N 个长度排列。

> 原文： [https://www.geeksforgeeks.org/smallest-number-containing-all-possible-n-length-permutations-using-digits-0-to-d/](https://www.geeksforgeeks.org/smallest-number-containing-all-possible-n-length-permutations-using-digits-0-to-d/)

给定两个整数`N`和`K`，任务是找到最小字符串的大小，该字符串包含所有长度为`N`的排列，可以使用第一个[`D`位**（0，1，…，D-1）**。

**示例**：

> **输入**：N = 2，D = 2
> **输出**：01100
> **说明**：
> 长度 2 可能由数字（0 ，1）为{00，01，10，11}。
> “ 01100”是一个这样的字符串，其中包含所有排列作为子字符串。
> 其他可能的答案是“ 00110”，“ 10011”，“ 11001”
> 
> **输入**：N = 2，D = 4
> **输出**：03322312113020100
> **解释**：
> 这里所有可能的数字长度排列 2 {0，1，2，3}是
> 00 10 20 30
> 01 11 21 31
> 02 12 22 32
> 03 13 23 33
> “ 03322312113020100”是最小长度的字符串 包含上述所有排列。

**方法**：

附加“ 0” N-1 次，并以当前状态在字符串上调用 [DFS](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 。 所有 D 字符一一附加。 每次附加后，请检查是否访问了新字符串。 如果是这样，请将其插入 [HashSet](http://www.geeksforgeeks.org/hashset-in-java/) ，以将其标记为已访问，然后在答案中添加此字符。 在最后的 D 个字符上递归调用 DFS 函数。 重复此过程，直到从 D 位开始的所有可能的 N 长度的子字符串都附加到该字符串为止。 打印生成的最终字符串。

下面是上述方法的实现：

## Java

```java

// Java Program to find the 
// minimum length string 
// consisting of all 
// permutations of length N 
// of D digits 
import java.io.*; 
import java.util.*; 
import java.lang.*; 

class GeeksforGeeks { 

    // Initialize hashset to see 
    // if all the possible 
    // permutations are present 
    // in the min length string 
    static Set<String> visited; 
    // To keep min length string 
    static StringBuilder ans; 

    public static String reqString(int N, 
                                   int D) 
    { 
        // Base case 
        if (N == 1 && D == 1) 
            return "0"; 
        visited = new HashSet<>(); 
        ans = new StringBuilder(); 

        StringBuilder sb = new StringBuilder(); 
        // Append '0' n-1 times 
        for (int i = 0; i < N - 1; ++i) { 
            sb.append("0"); 
        } 
        String start = sb.toString(); 
        // Call the DFS Function 
        dfs(start, D); 
        ans.append(start); 

        return new String(ans); 
    } 
    // Generate the required string 
    public static void dfs(String curr, int D) 
    { 
        // Iterate over all the possible 
        // character 
        for (int x = 0; x < D; ++x) { 
            // Append to make a new string 
            String neighbour = curr + x; 
            // If the new string is not 
            // visited 
            if (!visited.contains(neighbour)) { 
                // Add in hashset 
                visited.add(neighbour); 
                // Call the dfs function on 
                // the last d characters 
                dfs(neighbour.substring(1), D); 

                ans.append(x); 
            } 
        } 
    } 
    // Driver Code 
    public static void main(String args[]) 
    { 

        int N = 2; 
        int D = 2; 
        System.out.println(reqString(N, D)); 
    } 
} 

```