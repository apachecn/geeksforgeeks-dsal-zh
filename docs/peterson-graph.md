# 彼得森图形问题

> 原文:[https://www.geeksforgeeks.org/peterson-graph/](https://www.geeksforgeeks.org/peterson-graph/)

下面的图 G 被称为彼得森图，它的顶点被编号为 0 到 9。一些字母也被赋给了 G 的顶点，从下图可以看出:
我们来考虑图 G 中的一个游走 W，它由 L 个顶点 W1，W2，…，WL 组成。L 个字母的串 S ' A '–' E '如果沿着 W 写的字母序列等于 S，则通过走 W 来实现，顶点可以在沿着 W
走的同时多次访问，例如，S = ' ABBECCD '通过 W = (0，1，6，9，7，2，3)来实现。确定在图 G 中是否存在实现给定字符串 S 的遍历 W，如果存在，则找到字典序上最少的这样的遍历。输入的唯一一行包含一个字符串 S，如果没有实现 S 的 walk W，那么输出-1，否则应该输出实现 S 的最小字典序 walk W

![](img/93400bc3fb918f88886000766023dd97.png)

示例:

```
Input : s = 'ABB'
Output: 016
Explanation: As we can see in the graph
             the path from ABB is 016.
Input : s = 'AABE'
Output :-1
Explanation: As there is no path that
             exists, hence output is -1.
```

我们应用广度优先搜索来访问图的每个顶点。

## C++

```
// C++ program to find the
// path in Peterson graph
#include <bits/stdc++.h>
using namespace std;

// path to be checked
char S[100005];

// adjacency matrix.
bool adj[10][10];

// resulted path - way
char result[100005];

// we are applying breadth first search
// here
bool findthepath(char* S, int v)
{
    result[0] = v + '0';
    for (int i = 1; S[i]; i++) {

        // first traverse the outer graph
        if (adj[v][S[i] - 'A'] || adj[S[i] -
                              'A'][v]) {
            v = S[i] - 'A';
        }

        // then traverse the inner graph
        else if (adj[v][S[i] - 'A' + 5] ||
                 adj[S[i] - 'A' + 5][v]) {
            v = S[i] - 'A' + 5;
        }

        // if the condition failed to satisfy
        // return false
        else
            return false;

        result[i] = v + '0';
    }

    return true;
}

// driver code
int main()
{
    // here we have used adjacency matrix to make
    // connections between the connected nodes
    adj[0][1] = adj[1][2] = adj[2][3] = adj[3][4] =
    adj[4][0] = adj[0][5] = adj[1][6] = adj[2][7] =
    adj[3][8] = adj[4][9] = adj[5][7] = adj[7][9] =
    adj[9][6] = adj[6][8] = adj[8][5] = true;

    // path to be checked
    char S[] = "ABB";

    if (findthepath(S, S[0] - 'A') ||
        findthepath(S, S[0] - 'A' + 5)) {
        cout << result;
    } else {
        cout << "-1";
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// path in Peterson graph
class GFG
{

    // path to be checked
    static char []S = new char[100005];

    // adjacency matrix.
    static boolean [][]adj = new boolean[10][10];

    // resulted path - way
    static char[] result = new char[100005];

    // we are applying breadth first search
    // here
    static boolean findthepath(char[] S, int v)
    {
        result[0] = (char) (v + '0');
        for (int i = 1; i<(int)S.length; i++)
        {

            // first traverse the outer graph
            if (adj[v][S[i] - 'A'] ||
                adj[S[i] - 'A'][v])
            {
                v = S[i] - 'A';
            }

            // then traverse the inner graph
            else if (adj[v][S[i] - 'A' + 5] ||
                    adj[S[i] - 'A' + 5][v])
            {
                v = S[i] - 'A' + 5;
            }

            // if the condition failed to satisfy
            // return false
            else
                return false;

            result[i] = (char) (v + '0');
        }
        return true;
    }

    // Driver code
    public static void main(String[] args)
    {
        // here we have used adjacency matrix to make
        // connections between the connected nodes
        adj[0][1] = adj[1][2] = adj[2][3] = adj[3][4] =
        adj[4][0] = adj[0][5] = adj[1][6] = adj[2][7] =
        adj[3][8] = adj[4][9] = adj[5][7] = adj[7][9] =
        adj[9][6] = adj[6][8] = adj[8][5] = true;

        // path to be checked
        char S[] = "ABB".toCharArray();

        if (findthepath(S, S[0] - 'A') ||
            findthepath(S, S[0] - 'A' + 5))
        {
            System.out.print(result);
        }
        else
        {
            System.out.print("-1");
        }
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find the
# path in Peterson graph
# path to be checked

# adjacency matrix.
adj = [[False for i in range(10)] for j in range(10)]

# resulted path - way
result = [0]

# we are applying breadth first search
# here
def findthepath(S, v):
    result[0] = v
    for i in range(1, len(S)):

        # first traverse the outer graph
        if (adj[v][ord(S[i]) - ord('A')] or
            adj[ord(S[i]) - ord('A')][v]):
            v = ord(S[i]) - ord('A')

        # then traverse the inner graph
        elif (adj[v][ord(S[i]) - ord('A') + 5] or
               adj[ord(S[i]) - ord('A') + 5][v]):
            v = ord(S[i]) - ord('A') + 5

        # if the condition failed to satisfy
        # return false
        else:
            return False

        result.append(v)

    return True

# driver code
# here we have used adjacency matrix to make
# connections between the connected nodes
adj[0][1] = adj[1][2] = adj[2][3] = \
adj[3][4] = adj[4][0] = adj[0][5] = \
adj[1][6] = adj[2][7] = adj[3][8] = \
adj[4][9] = adj[5][7] = adj[7][9] = \
adj[9][6] = adj[6][8] = adj[8][5] = True

# path to be checked
S= "ABB"
S=list(S)
if (findthepath(S, ord(S[0]) - ord('A')) or
    findthepath(S, ord(S[0]) - ord('A') + 5)):
    print(*result, sep = "")
else:
    print("-1")

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program to find the
// path in Peterson graph
using System;
public class GFG
{

  // adjacency matrix.
  static bool [,]adj = new bool[10, 10];

  // resulted path - way
  static char[] result = new char[100005];

  // we are applying breadth first search
  // here
  static bool findthepath(String S, int v)
  {
    result[0] = (char) (v + '0');
    for (int i = 1; i < S.Length; i++)
    {

      // first traverse the outer graph
      if (adj[v,S[i] - 'A'] ||
          adj[S[i] - 'A',v])
      {
        v = S[i] - 'A';
      }

      // then traverse the inner graph
      else if (adj[v,S[i] - 'A' + 5] ||
               adj[S[i] - 'A' + 5,v])
      {
        v = S[i] - 'A' + 5;
      }

      // if the condition failed to satisfy
      // return false
      else
        return false;

      result[i] = (char) (v + '0');
    }
    return true;
  }

  // Driver code
  public static void Main(String[] args)
  {

    // here we have used adjacency matrix to make
    // connections between the connected nodes
    adj[0,1] = adj[1,2] = adj[2,3] = adj[3,4] =
      adj[4,0] = adj[0,5] = adj[1,6] = adj[2,7] =
      adj[3,8] = adj[4,9] = adj[5,7] = adj[7,9] =
      adj[9,6] = adj[6,8] = adj[8,5] = true;

    // path to be checked
    String S = "ABB";
    if (findthepath(S, S[0] - 'A') ||  findthepath(S, S[0] - 'A' + 5))
    {
      Console.WriteLine(result);
    }
    else
    {
      Console.Write("-1");
    }
  }
}

// This code is contributed by aashish1995
```

**输出:**

```
016
```

本文由**苏尼迪·乔德里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。