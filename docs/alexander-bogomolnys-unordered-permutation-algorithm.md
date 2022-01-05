# 亚历山大·博戈莫利的无序排列算法

> 原文:[https://www . geeksforgeeks . org/Alexander-bogomolnys-无序-排列-算法/](https://www.geeksforgeeks.org/alexander-bogomolnys-unordered-permutation-algorithm/)

亚历山大·博戈莫林的算法用于置换前 N 个自然数。
给定 N 的值，我们必须输出从 1 到 N 的所有数字排列。
**示例:**

```
Input : 2
Output : 1 2
         2 1

Input : 3
Output : 1 2 3
         1 3 2
         2 1 3
         3 1 2
         2 3 1
         3 2 1
```

其思想是维护一个数组来存储当前的排列。静态整数级变量用于定义这些排列。

1.  它初始化当前级别的值，并将剩余的值置换到更高的级别。
2.  当值的赋值动作达到最高级别时，它打印得到的置换。
3.  这种方法被递归地实现以获得所有可能的排列。

## C++

```
#include<bits/stdc++.h>
using namespace std;

void solve(vector<int> &v,int n,string &s,vector<vector<int>> &vv)
{
    if(v.size()==n)
    {
        vv.push_back(v);
        return;
    }
    for(int i=0;i<n;i++)
    {
        if(s[i]!='1')
        {
            s[i]='1';
            v.push_back(i+1);
            solve(v,n,s,vv);
            s[i]='0';
            v.pop_back();
        }
    }

}

int main()
{
    int n=3
    vector<int> v;
    vector<vector<int>> vv;
    string s;
    for(int i=0;i<n;i++) s+='0';
    solve(v,n,s,vv);
    for(int i=0;i<vv.size();i++)
    {
        for(int j=0;j<vv[i].size();j++)
        {
            cout<<vv[i][j]<<" ";
        }
        cout<<endl;
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// Alexander Bogomolny UnOrdered
// Permutation Algorithm
import java.io.*;

class GFG
{
static int level = -1;

// A function to print
// the permutation.
static void print(int perm[], int N)
{
    for (int i = 0; i < N; i++)
        System.out.print(" " + perm[i]);
    System.out.println();
}

// A function implementing
// Alexander Bogomolyn algorithm.
static void AlexanderBogomolyn(int perm[],
                               int N, int k)
{

    // Assign level to
    // zero at start.
    level = level + 1;
    perm[k] = level;

    if (level == N)
        print(perm, N);
    else
        for (int i = 0; i < N; i++)

            // Assign values
            // to the array
            // if it is zero.
            if (perm[i] == 0)
                AlexanderBogomolyn(perm, N, i);

    // Decrement the level
    // after all possible
    // permutation after
    // that level.
    level = level - 1;

    perm[k] = 0;
}

// Driver Code
public static void main (String[] args)
{
    int i, N = 3;
    int perm[] = new int[N];
    AlexanderBogomolyn(perm, N, 0);
}
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python3 program to implement Alexander
# Bogomolny’s UnOrdered Permutation Algorithm

# A function to print permutation.
def printn(perm, N):
    for i in range(N):
        print(" ",perm[i], sep = "", end = "")
    print()

# A function implementing Alexander Bogomolyn
# algorithm.
level = [-1]
def AlexanderBogomolyn(perm, N, k):

    # Assign level to zero at start.
    level[0] = level[0] + 1
    perm[k] = level[0]
    if (level[0] == N):
        printn(perm, N)
    else:
        for i in range(N):

            # Assign values to the array
            # if it is zero.
            if (perm[i] == 0):
                AlexanderBogomolyn(perm, N, i)

    # Decrement the level after all possible
    # permutation after that level.
    level[0] = level[0] - 1

    perm[k] = 0
    return

# Driver code
N = 3
perm = [0]*N
AlexanderBogomolyn(perm, N, 0)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program to implement
// Alexander Bogomolny UnOrdered
// Permutation Algorithm
using System;

class GFG
{
static int level = -1;

// A function to print
// the permutation.
static void print(int []perm,
                  int N)
{
    for (int i = 0; i < N; i++)
        Console.Write(" " + perm[i]);
    Console.WriteLine();
}

// A function implementing
// Alexander Bogomolyn algorithm.
static void AlexanderBogomolyn(int []perm,
                               int N, int k)
{

    // Assign level to
    // zero at start.
    level = level + 1;
    perm[k] = level;

    if (level == N)
        print(perm, N);
    else
        for (int i = 0; i < N; i++)

            // Assign values
            // to the array
            // if it is zero.
            if (perm[i] == 0)
                AlexanderBogomolyn(perm, N, i);

    // Decrement the level
    // after all possible
    // permutation after
    // that level.
    level = level - 1;

    perm[k] = 0;
}

// Driver Code
public static void Main ()
{
    int N = 3;
    int []perm = new int[N];
    AlexanderBogomolyn(perm, N, 0);
}
}

// This code is contributed
// by anuj_67.
```

## java 描述语言

```
<script>

// Javascript program to implement
// Alexander Bogomolny UnOrdered
// Permutation Algorithm

let level = -1;

// A function to print
// the permutation.
function prlet(perm, N)
{
    for (let i = 0; i < N; i++)
        document.write(" " + perm[i]);
    document.write("<br/>");
}

// A function implementing
// Alexander Bogomolyn algorithm.
function AlexanderBogomolyn(perm, N, k)
{

    // Assign level to
    // zero at start.
    level = level + 1;
    perm[k] = level;

    if (level == N)
        prlet(perm, N);
    else
        for (let i = 0; i < N; i++)

            // Assign values
            // to the array
            // if it is zero.
            if (perm[i] == 0)
                AlexanderBogomolyn(perm, N, i);

    // Decrement the level
    // after all possible
    // permutation after
    // that level.
    level = level - 1;

    perm[k] = 0;
}
// driver program

    let i, N = 3;
    let perm = Array.from({length: N}, (_, i) => 0);
    AlexanderBogomolyn(perm, N, 0);

</script>
```

**输出:**

```
1 2 3
1 3 2
2 1 3
3 1 2
2 3 1
3 2 1
```

本文由 [**维奈乔希**](https://auth.geeksforgeeks.org/profile.php?user=Vineet Joshi) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。