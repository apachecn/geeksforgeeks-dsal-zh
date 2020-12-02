# 水连接问题

> 原文： [https://www.geeksforgeeks.org/water-connection-problem/](https://www.geeksforgeeks.org/water-connection-problem/)

殖民地中的每个房屋最多只能有一个管道进入，最多只能有一个管道离开。
给定 两个整数`n`，并且 p 表示房屋数量和管道数量。 房屋之间的管道连接包含三个输入值： **a_i** ， **b_i** ， **d_i** 表示从房屋 **a_i** 容纳 **b_i** ，找出网络的有效解决方案。
输出将包含安装在第一行中的储罐和水龙头对的数量`t`，下一个`t`行包含三个整数：储罐的房屋数量，水龙头的房屋数量 以及它们之间的最小管道直径。

例子：

```
Input : 4 2
        1 2 60
        3 4 50
Output :2
        1 2 60
        3 4 50
Explanation:
Connected components are: 
*1->2 and 3->4*
Therefore, our answer is 2 followed by
1 2 60 and 3 4 50.

Input :9 6
       7 4 98
       5 9 72
       4 6 10
       2 8 22
       9 7 17
       3 1 66
Output :3
        2 8 22
        3 1 66
        5 6 10
Explanation:
Connected components are *3->1, 
5->9->7->4->6 and 2->8*. 
Therefore, our answer is 3 followed by
2 8 22, 3 1 66, 5 6 10

```

**方法**：
从适当的房屋执行 DFS，以找到所有不同的连接组件。 不同的连接组件数是我们的答案 t。
输出的下 t 条线是连接的组件的起点，连接的组件的终点以及每行中从连接的组件的起点到终点的最小直径。
由于只能将罐子安装在有出水管而没有进水管的房屋上，因此，这些房屋是从 DFS 开始进行 DFS 的合适房屋，即从未经访问的房屋执行 DFS。

下面是上述方法的实现：

## C++

```cpp

// C++ program to find efficient 
// solution for the network 
#include <bits/stdc++.h> 
using namespace std; 

// number of houses and number 
// of pipes 
int n, p; 

// Array rd stores the  
// ending vertex of pipe 
int rd[1100]; 

// Array wd stores the value  
// of diameters between two pipes 
int wt[1100]; 

// Array cd stores the  
// starting end of pipe 
int cd[1100]; 

// Vector a, b, c are used 
// to store the final output 
vector<int> a; 
vector<int> b; 
vector<int> c; 

int ans; 

int dfs(int w) 
{ 
    if (cd[w] == 0) 
        return w; 
    if (wt[w] < ans) 
        ans = wt[w]; 
    return dfs(cd[w]); 
} 

// Function performing calculations. 
void solve(int arr[][3]) 
{ 
    int i = 0; 

    while (i < p) { 

        int q = arr[i][0], h = arr[i][1], 
            t = arr[i][2]; 

        cd[q] = h; 
        wt[q] = t; 
        rd[h] = q; 
        i++; 
    } 

    a.clear(); 
    b.clear(); 
    c.clear(); 

    for (int j = 1; j <= n; ++j) 

        /*If a pipe has no ending vertex  
        but has starting vertex i.e is  
        an outgoing pipe then we need  
        to start DFS with this vertex.*/
        if (rd[j] == 0 && cd[j]) { 
            ans = 1000000000; 
            int w = dfs(j); 

            // We put the details of component 
            // in final output array 
            a.push_back(j); 
            b.push_back(w); 
            c.push_back(ans); 
        } 

    cout << a.size() << endl; 
    for (int j = 0; j < a.size(); ++j) 
        cout << a[j] << " " << b[j]  
             << " " << c[j] << endl; 
} 

// driver function 
int main() 
{ 
    n = 9, p = 6; 

    memset(rd, 0, sizeof(rd)); 
    memset(cd, 0, sizeof(cd)); 
    memset(wt, 0, sizeof(wt)); 

    int arr[][3] = { { 7, 4, 98 }, 
                    { 5, 9, 72 }, 
                    { 4, 6, 10 }, 
                    { 2, 8, 22 }, 
                    { 9, 7, 17 }, 
                    { 3, 1, 66 } }; 

    solve(arr); 
    return 0; 
} 

```

## Java

```java

// Java program to find efficient 
// solution for the network 
import java.util.*; 

class GFG { 

    // number of houses and number 
    // of pipes 
    static int n, p; 

    // Array rd stores the  
    // ending vertex of pipe 
    static int rd[] = new int[1100]; 

    // Array wd stores the value  
    // of diameters between two pipes 
    static int wt[] = new int[1100]; 

    // Array cd stores the  
    // starting end of pipe 
    static int cd[] = new int[1100]; 

    // arraylist a, b, c are used 
    // to store the final output 
    static List <Integer> a =  
              new ArrayList<Integer>(); 

    static List <Integer> b =  
              new ArrayList<Integer>(); 

    static List <Integer> c =  
              new ArrayList<Integer>(); 

    static int ans; 

    static int dfs(int w) 
    { 
        if (cd[w] == 0) 
            return w; 
        if (wt[w] < ans) 
            ans = wt[w]; 

        return dfs(cd[w]); 
    } 

    // Function to perform calculations. 
    static void solve(int arr[][]) 
    { 
        int i = 0; 

        while (i < p) 
        { 

            int q = arr[i][0]; 
            int h = arr[i][1]; 
            int t = arr[i][2]; 

            cd[q] = h; 
            wt[q] = t; 
            rd[h] = q; 
            i++; 
        } 

        a=new ArrayList<Integer>(); 
        b=new ArrayList<Integer>(); 
        c=new ArrayList<Integer>(); 

        for (int j = 1; j <= n; ++j) 

            /*If a pipe has no ending vertex  
            but has starting vertex i.e is  
            an outgoing pipe then we need  
            to start DFS with this vertex.*/
            if (rd[j] == 0 && cd[j]>0) { 
                ans = 1000000000; 
                int w = dfs(j); 

                // We put the details of 
                // component in final output 
                // array 
                a.add(j); 
                b.add(w); 
                c.add(ans); 
            } 

        System.out.println(a.size()); 

        for (int j = 0; j < a.size(); ++j) 
            System.out.println(a.get(j) + " " 
                + b.get(j) + " " + c.get(j)); 
    } 

    // main function 
    public static void main(String args[]) 
    { 
        n = 9; 
        p = 6; 

        // set the value of the araray  
        // to zero 
        for(int i = 0; i < 1100; i++) 
            rd[i] = cd[i] = wt[i] = 0; 

        int arr[][] = { { 7, 4, 98 }, 
                        { 5, 9, 72 }, 
                        { 4, 6, 10 }, 
                        { 2, 8, 22 }, 
                        { 9, 7, 17 }, 
                        { 3, 1, 66 } }; 
        solve(arr); 
    } 
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```

# Python3 program to find efficient 
# solution for the network 

# number of houses and number 
# of pipes 
n = 0
p = 0

# Array rd stores the  
# ending vertex of pipe 
rd = [0]*1100

# Array wd stores the value  
# of diameters between two pipes 
wt = [0]*1100

# Array cd stores the  
# starting end of pipe 
cd = [0]*1100

# List a, b, c are used 
# to store the final output 
a = [] 
b = [] 
c = [] 

ans = 0

def dfs(w): 
    global ans 
    if (cd[w] == 0): 
        return w 
    if (wt[w] < ans): 
        ans = wt[w] 
    return dfs(cd[w]) 

# Function performing calculations. 
def solve(arr): 
    global ans 
    i = 0
    while (i < p): 
        q = arr[i][0] 
        h = arr[i][1] 
        t = arr[i][2] 

        cd[q] = h 
        wt[q] = t 
        rd[h] = q 
        i += 1
    a = [] 
    b = [] 
    c = [] 

    '''If a pipe has no ending vertex  
    but has starting vertex i.e is  
    an outgoing pipe then we need  
    to start DFS with this vertex.'''
    for j in range(1, n + 1): 
        if (rd[j] == 0 and cd[j]): 

            ans = 1000000000
            w = dfs(j) 

            # We put the details of component 
            # in final output array 
            a.append(j) 
            b.append(w)  
            c.append(ans) 
    print(len(a)) 
    for j in range(len(a)): 
        print(a[j], b[j], c[j]) 

# Driver function 
n = 9
p = 6

arr = [[7, 4, 98], [5, 9, 72], [4, 6, 10 ],  
        [2, 8, 22 ], [9, 7, 17], [3, 1, 66]] 

solve(arr) 

# This code is contributed by shubhamsingh10 

```

## C#

```cs

// C# program to find efficient  
// solution for the network  
using System; 
using System.Linq; 
using System.Collections.Generic;  

class GFG  
{  

    // number of houses and number  
    // of pipes  
    static int n, p;  

    // Array rd stores the  
    // ending vertex of pipe  
    static int []rd = new int[1100];  

    // Array wd stores the value  
    // of diameters between two pipes  
    static int []wt = new int[1100];  

    // Array cd stores the  
    // starting end of pipe  
    static int []cd = new int[1100];  

    // arraylist a, b, c are used  
    // to store the final output  
    static List <int> a =  
            new List <int>();  

    static List <int> b =  
            new List <int>();  

    static List <int> c =  
            new List <int>();  

    static int ans;  

    static int dfs(int w)  
    {  
        if (cd[w] == 0)  
            return w;  
        if (wt[w] < ans)  
            ans = wt[w];  

        return dfs(cd[w]);  
    }  

    // Function to perform calculations.  
    static void solve(int [,]arr)  
    {  
        int i = 0;  

        while (i < p)  
        {  

            int q = arr[i,0];  
            int h = arr[i,1];  
            int t = arr[i,2];  

            cd[q] = h;  
            wt[q] = t;  
            rd[h] = q;  
            i++;  
        }  

        a = new List <int>();  
        b = new List <int>();  
        c = new List <int>();  

        for (int j = 1; j <= n; ++j)  

            /*If a pipe has no ending vertex  
            but has starting vertex i.e is  
            an outgoing pipe then we need  
            to start DFS with this vertex.*/
            if (rd[j] == 0 && cd[j] > 0)  
            {  
                ans = 1000000000;  
                int w = dfs(j);  

                // We put the details of  
                // component in final output  
                // array  
                a.Add(j);  
                b.Add(w);  
                c.Add(ans);  
            }  

        Console.WriteLine(a.Count);  

        for (int j = 0; j < a.Count; ++j)  
            Console.WriteLine(a[j] + " "
                + b[j] + " " + c[j]);  
    }  

    // Driver code  
    public static void Main(String []args)  
    {  
        n = 9;  
        p = 6;  

        // set the value of the araray  
        // to zero  
        for(int i = 0; i < 1100; i++)  
            rd[i] = cd[i] = wt[i] = 0;  

        int [,]arr = { { 7, 4, 98 },  
                        { 5, 9, 72 },  
                        { 4, 6, 10 },  
                        { 2, 8, 22 },  
                        { 9, 7, 17 },  
                        { 3, 1, 66 } };  
        solve(arr);  
    }  
}  

// This code has been contributed by 29AjayKumar 

```

**输出**：

```
3
2 8 22
3 1 66
5 6 10

```

[![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)](https://practice.geeksforgeeks.org/courses/competitive-programming-live?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_cp)

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。