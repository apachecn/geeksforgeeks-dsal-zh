# 将字符串 X 转换为 Y 的最小点击次数

> 原文： [https://www.geeksforgeeks.org/minimum-clicks-to-convert-string-x-to-y/](https://www.geeksforgeeks.org/minimum-clicks-to-convert-string-x-to-y/)

给定 3 个字符的开始字符串`X`，3 个字符的结束字符串`Y`和一组禁止的字符串。 任务是找到从 X 达到 Y 的最小点击次数。

**规则**：

*   这 3 个字符中的每个字符都以循环方式变化，即，每次单击时，您可以从 **a 到 b** 或 **a 到 z** ，并且从未显示禁止字。
*   如果无法达到 Y **，则**打印-1 **。** 每次单击只能更改一个字母。
*   每个禁止的字符串具有以下形式：{**“ S1”“ S2”“ S3”}** 其中每个字符串 S <sub>i</sub> 包含该字符的禁止字母。
*   禁止的字符串= **{“ ac”“ bx”“ lw”}** 表示单词**“ abl”，“ cxw”，“ cbl”，“ abw”，“ cbw”，“ axl”，“ axw”和“ cxl”** 被禁止，并且永远不会显示。

**注意**：如果起始字符串 X 也是可能的禁止字符组合，则结果也应该为-1。

> **输入**：X =“ znw”，Y =“ lof”，N = 4（禁止的字符串数）
> 禁止=
> {” qlb”，“ jcm”，“ mhoq”} ，
> {” azn”，“ piy”，“ vj”}，
> {”，“”，“ oy”，“ ubo”}，
> {” jqm”，“ f”，“ ej” }
> **输出**：所需的最低点击次数为 22
> **说明**：由于给定的禁止字符串中没有任何组合形成最终字符串 Y，因此字符串 Y 变为 有效。
> 
> 因此，所需的最小点击数计算如下：
> z – l 向前 12 次点击
> z – l 反向 14 次
> n – o 向前 1 点击
> n – o 向后 25 次点击
> w – f 向前 9 次点击
> w – f 向后 17 次点击
> 
> 最低总点击次数= 12 + 1 + 9 = 22。
> 
> **输入**：X =“ bdb”，Y =“ xxx”，N = 1（禁止字符串的数量）
> forbidden = {” ax”，“ acx”，“ bxy”}
> **输出**：所需的最低点击次数为-1
> **说明**：由于“ xxx”是可能的禁止字符组合，因此不可能从 X 到达 Y。

**方法**：

使用 [BFS（宽度优先搜索）](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/)进行某些修改，以获取最小的点击次数，绕过禁止的字符串。

1.  由于 3 个位置中的每个位置都可以包含字母，因此创建 3D 访问数组，尺寸为 26 * 26 * 26，以便遍历单词状态。
2.  要可视化每个受限制的单词，请创建另一个尺寸为 26 * 26 * 26 的 3D 数组，以跟踪在遍历中绝不能访问的单词。
3.  由于 3 个字符中的每个字符都以循环方式变化，即，每次单击时字母将以循环方式变化，因此，每次到达下一个字母时，都需要注意对 26 取模。
4.  令单词的当前状态为 **[X Y Z]** 。 然后单击一次即可移动到以下 6 个状态：

    > **[X + 1 YZ]，[X-1 YZ]，[XY + 1 Z]，[X Y -1 Z]，[XYZ + 1]，[XY Z-1]。**

5.  因此，创建 3 个实用程序数组 **dx，dy，dz** ，以使遍历过程简化。 将每个单词状态存储在一个结构中，该结构具有 4 个字段，即 a，b，c（3 个字符中的每一个）和距起始单词的距离。

下面是上述方法的实现：

## C ++

```

// C++ code for above program. 
#include <bits/stdc++.h> 
using namespace std; 
#define int long long int 

// each node represents a word state 
struct node { 
    int a, b, c; 
    // dist from starting word X 
    int dist; 
}; 

// 3D visited array 
bool visited[26][26][26]; 

// 3D restricted array 
bool restricted[26][26][26]; 

// utility arrays for single step 
// traversal in left and right 
int dx[6] = { 1, -1, 0, 0, 0, 0 }; 
int dy[6] = { 0, 0, 1, -1, 0, 0 }; 
int dz[6] = { 0, 0, 0, 0, 1, -1 }; 

// function to find the 
// minimum clicks. 
void solve(string start, 
           string end, int qx, 
           const vector<vector<string> >& forbidden) 
{ 

    memset(visited, 0, 
           sizeof(visited)); 
    memset(restricted, 0, 
           sizeof(restricted)); 

    for (auto vec : forbidden) { 

        string a = vec[0]; 
        string b = vec[1]; 
        string c = vec[2]; 

        for (auto x : a) 
            for (auto y : b) 
                for (auto z : c) { 

                    // each invalid word is 
                    // decoded and marked as 
                    // restricted = true. 
                    restricted[x - 'a'] 
                              [y - 'a'] 
                              [z - 'a'] 
                        = true; 
                } 
    } 

    // starting and ending letter a 
    int sa = start[0] - 'a'; 
    int ea = end[0] - 'a'; 

    // starting and ending letter b 
    int sb = start[1] - 'a'; 
    int eb = end[1] - 'a'; 

    // starting and ending letter c 
    int sc = start[2] - 'a'; 
    int ec = end[2] - 'a'; 

    if (restricted[sa][sb][sc] 
        or restricted[ea][eb][ec]) { 

        // check if starting word 
        // or finishing word is 
        // restricted or not 
        cout << -1 << endl; 

        return; 
    } 

    // queue of nodes for BFS 
    queue<node> q; 

    // initial starting word pushed in 
    // queue. dist = 0 for starting word 
    q.push({ sa, sb, sc, 0 }); 

    // mark as visited 
    visited[sa][sb][sc] = true; 

    while (!q.empty()) { 
        node x = q.front(); 
        q.pop(); 

        // final destination reached condition 
        if (x.a == (end[0] - 'a') 
            and x.b == (end[1] - 'a') 
            and x.c == (end[2] - 'a')) { 

            cout << x.dist 
                 << endl; 
            return; 
        } 

        int DIST = x.dist; 
        for (int i = 0; i < 6; i++) { 

            // mod 26 for circular letter sequence 

            // next letter for a 
            int A = (x.a + dx[i] + 26) % 26; 

            // next letter for b 
            int B = (x.b + dy[i] + 26) % 26; 

            // next letter for c 
            int C = (x.c + dz[i] + 26) % 26; 

            if (!restricted[A][B][C] 
                and !visited[A][B][C]) { 

                // if a valid word state, 
                // push into queue 
                q.push({ A, B, C, DIST + 1 }); 
                visited[A][B][C] = true; 
            } 
        } 
    } 

    // reach here if not possible 
    // to reach final word Y 
    cout << -1 << endl; 
} 

// Driver Code 
signed main() 
{ 
    // starting string 
    string X = "znw"; 

    // final string 
    string Y = "lof"; 

    // no of restricting word vectors 
    int N = 4; 

    vector<vector<string> > forbidden 
        = { { "qlb", "jcm", "mhoq" }, 
            { "azn", "piy", "vj" }, 
            { "by", "oy", "ubo" }, 
            { "jqm", "f", "ej" } }; 

    solve(X, Y, N, forbidden); 
    return 0; 
} 

```