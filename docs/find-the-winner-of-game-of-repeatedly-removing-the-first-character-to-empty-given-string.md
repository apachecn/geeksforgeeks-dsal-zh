# 找到重复移除第一个字符清空给定字符串的游戏的赢家

> 原文:[https://www . geesforgeks . org/find-the-winner-of-game-reply-remove-first-character-to-empty-given-string/](https://www.geeksforgeeks.org/find-the-winner-of-game-of-repeatedly-removing-the-first-character-to-empty-given-string/)

给定一个正整数 **N** ，代表玩游戏的玩家数量，以及一个字符串[数组](https://www.geeksforgeeks.org/array-strings-c-3-different-ways-create/)**arr【】**，由范围**【1】【N】**的数字组成的数字字符串。考虑到 **i <sup>th</sup>** 玩家被分配了字符串**arr【I】**，任务是当所有 **N** 玩家按照以下规则进行最佳游戏时，寻找游戏的赢家:

*   **玩家 1** 开始游戏，移除字符串的第一个字符**arr【1】**(*T5【1】)基于索引*，说 **X** ，下一回合 **X <sup>th</sup>** 玩家将进行游戏，移除**arr【X】**的第一个字符，以此类推。
*   不能从指定字符串中移除任何字符的玩家将赢得游戏。

**示例:**

> **输入:** N = 3，arr[]= {“323”，“2”，“2”}
> **输出:**玩家 2
> **解释:**
> **回合 1:** 玩家 1 移除 arr[0][0]将 arr[0]修改为“23”。
> **回合 2:** 玩家 3 移除 arr[2][0]将 arr[2]修改为" "。
> **第三回合:**玩家 2 移除 arr[1][0]将 arr[1]修改为" "。
> **回合 4:** 玩家 2 无法移除 arr[1]中的任何角色。
> 因此，玩家 2 赢得游戏。
> 
> **输入:** N = 3，arr[]= {“121”、“21”、“23123”}
> **输出:**玩家 1

**方法:**使用[队列](https://www.geeksforgeeks.org/queue-cpp-stl/)可以高效去除每个字符串的第一个字符，从而解决问题。按照以下步骤解决问题:

*   初始化一个[队列](https://www.geeksforgeeks.org/queue-cpp-stl/)的[数组](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如说 **Q[]** ，这样 **Q[i]** 存储字符串 **arr[i]** 的字符。
*   [按照游戏规则使用变量 **i** 遍历阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)T2【Q】，检查**Q【I】**中的人物个数是否为 **0** 。如果发现是真的，那么打印**“玩家 I”**。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the winner of a game of
// repeatedly removing the first character
// to empty a string
void find_Winner(vector<string>& arr, int N)
{

    // Store characters of each
    // string of the array arr[]
    vector<queue<char> > Q(N);

    // Stores count of strings in arr[]
    int M = arr.size();

    // Traverse the array arr[]
    for (int i = 0; i < M; i++) {

        // Stores length of current string
        int len = arr[i].length();

        // Traverse the string
        for (int j = 0; j < len; j++) {

            // Insert arr[i][j]
            Q[i].push(arr[i][j] - 1);
        }
    }

    // 1st Player starts the game
    int player = 0;

    while (Q[player].size() > 0) {

        // Stores the player number
        // for the next turn
        int nextPlayer
            = Q[player].front() - '0';

        // Remove 1st character of
        // current string
        Q[player].pop();

        // Update player number for
        // the next turn
        player = nextPlayer;
    }

    cout << "Player " << (player + 1);
}

// Driver Code
int main()
{

    int N = 3;
    vector<string> arr
        = { "323", "2", "2" };

    find_Winner(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG
{

// Function to find the winner of a game of
// repeatedly removing the first character
// to empty a String
static void find_Winner(String[] arr, int N)
{

    // Store characters of each
    // String of the array arr[]
    @SuppressWarnings("unchecked")
    Vector<Character> [] Q = new Vector[N];
    for (int i = 0; i < Q.length; i++)
        Q[i] = new Vector<Character>();

    // Stores count of Strings in arr[]
    int M = arr.length;

    // Traverse the array arr[]
    for (int i = 0; i < M; i++)
    {

        // Stores length of current String
        int len = arr[i].length();

        // Traverse the String
        for (int j = 0; j < len; j++)
        {

            // Insert arr[i][j]
            Q[i].add(arr[i].charAt(j));
        }

    }

    // 1st Player starts the game
    int player = 0;

    while (Q[player].size() > 0 )
    {

        // Stores the player number
        // for the next turn
        int nextPlayer
            = Q[player].get(0) - '0'-1;

        // Remove 1st character of
        // current String
        Q[player].remove(0);

        // Update player number for
        // the next turn
        player = nextPlayer;
    }
    System.out.print("Player " +  (player + 1));
}

// Driver Code
public static void main(String[] args)
{
    int N = 3;
    String[] arr
        = { "323", "2", "2" };
    find_Winner(arr, N);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the winner of a game of
# repeatedly removing the first character
# to empty a string
def find_Winner(arr, N) :

    # Store characters of each
    # string of the array arr[]
    Q = [0]*N  
    for i in range(N) :       
        Q[i] = []

    # Stores count of strings in arr[]
    M = len(arr)

    # Traverse the array arr[]
    for i in range(M) :

        # Stores length of current string
        Len = len(arr[i])

        # Traverse the string
        for j in range(Len) :

            # Insert arr[i][j]
            Q[i].append(ord(arr[i][j]) - 1)

    # 1st Player starts the game
    player = 0

    while (len(Q[player]) > 0) :

        # Stores the player number
        # for the next turn
        nextPlayer = Q[player][0] - ord('0')

        # Remove 1st character of
        # current string
        del Q[player][0]

        # Update player number for
        # the next turn
        player = nextPlayer

    print("Player", (player + 1))

N = 3
arr = [ "323", "2", "2" ]

find_Winner(arr, N)

# This code is contributed by divyeshrabadiya07.
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the winner of a game of
// repeatedly removing the first character
// to empty a String
static void find_Winner(String[] arr, int N)
{

    // Store characters of each
    // String of the array []arr
    List<char> [] Q = new List<char>[N];
    for(int i = 0; i < Q.Length; i++)
        Q[i] = new List<char>();

    // Stores count of Strings in []arr
    int M = arr.Length;

    // Traverse the array []arr
    for(int i = 0; i < M; i++)
    {

        // Stores length of current String
        int len = arr[i].Length;

        // Traverse the String
        for(int j = 0; j < len; j++)
        {

            // Insert arr[i,j]
            Q[i].Add(arr[i][j]);
        }
    }

    // 1st Player starts the game
    int player = 0;

    while (Q[player].Count > 0 )
    {

        // Stores the player number
        // for the next turn
        int nextPlayer = Q[player][0] - '0'- 1;

        // Remove 1st character of
        // current String
        Q[player].RemoveAt(0);

        // Update player number for
        // the next turn
        player = nextPlayer;
    }
    Console.Write("Player " + (player + 1));
}

// Driver Code
public static void Main(String[] args)
{
    int N = 3;
    String[] arr = { "323", "2", "2" };

    find_Winner(arr, N);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find the winner of a game of
// repeatedly removing the first character
// to empty a string
function find_Winner( arr, N)
{

    // Store characters of each
    // string of the array arr[]
    var Q = Array.from(Array(N), ()=>Array())

    // Stores count of strings in arr[]
    var M = arr.length;

    // Traverse the array arr[]
    for (var i = 0; i < M; i++) {

        // Stores length of current string
        var len = arr[i].length;

        // Traverse the string
        for (var j = 0; j < len; j++) {

            // Insert arr[i][j]
            Q[i].push(arr[i][j] - 1);
        }
    }

    // 1st Player starts the game
    var player = 0;

    while (Q[player].length > 0) {

        // Stores the player number
        // for the next turn
        var nextPlayer
            = Q[player][0] - '0';

        // Remove 1st character of
        // current string
        Q[player].shift();

        // Update player number for
        // the next turn
        player = nextPlayer;
    }

    document.write( "Player " + (player + 1));
}

// Driver Code
var N = 3;
var arr
    = ["323", "2", "2"];
find_Winner(arr, N);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
Player 2
```

***时间复杂度:** O(N * M)，其中 **M** 是数组中存在的最长字符串的长度。*
***辅助空间:** O(N * M)*