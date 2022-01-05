# 最小字符串，使得给定字符串的每个相邻字符仍然相邻

> 原文:[https://www . geeksforgeeks . org/最小字符串，这样给定字符串的每个相邻字符仍然相邻/](https://www.geeksforgeeks.org/minimum-string-such-that-every-adjacent-character-of-given-string-is-still-adjacent/)

给定一个字符串 **S** ，任务是找到最小长度的字符串，使得该字符串的每个相邻字符在最小长度的字符串中保持相邻。

**示例:**

> **输入:** S = "acabpba"
> **输出:** pbac
> **解释:**
> 给定字符串可以转换为“pbac”，其中，
> 每个相邻字符保持相邻。
> 
> **输入:**S = " abcdea "
> T3】输出:不可能
> T6】说明:T8】不可能找到这样的字符串。

**方法:**想法是准备一个[图](https://www.geeksforgeeks.org/graph-and-its-representations/)一样的结构，其中图的每个相邻节点表示字符串的相邻字符。在两种情况下，这种类型的字符串是不可能的–

*   如果一个字符包含三个或更多相邻字符。
*   如果两个字符不只有一个相邻字符，长度为 1 的字符串除外。

如果字符串的上述条件成立，那么只需[用](https://www.geeksforgeeks.org/algorithms-gq/graph-traversals-gq/)[深度优先搜索遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)遍历图形，该遍历的路径将是最小长度的字符串。DFS 的源顶点将是任何一个只有一个相邻字符的字符。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// minimum length string such that
// adjacent characters of the string
// remains adjacent in the string

#include <bits/stdc++.h>
using namespace std;

class graph {
    int arr[26][2];
    vector<int> alpha;
    vector<int> answer;

public:
    // Constructor for the graph
    graph()
    {
        // Initialize the matrix by -1
        for (int i = 0; i < 26; i++) {
            for (int j = 0; j < 2; j++)
                arr[i][j] = -1;
        }

        // Initialize the alphabet array
        alpha = vector<int>(26);
    }

    // Function to do Depth first
    // search Traversal
    void dfs(int v)
    {
        // Pushing current character
        answer.push_back(v);

        alpha[v] = 1;

        for (int i = 0; i < 2; i++) {
            if (alpha[arr[v][i]] == 1
                || arr[v][i] == -1)
                continue;

            dfs(arr[v][i]);
        }
    }

    // Function to find the minimum
    // length string
    void minString(string str)
    {
        // Condition if given string
        // length is 1
        if (str.length() == 1) {
            cout << str << "\n";
            return;
        }

        bool flag = true;

        // Loop to find the adjacency
        // list of the given string
        for (int i = 0; i < str.length() - 1;
             i++) {
            int j = str[i] - 'a';
            int k = str[i + 1] - 'a';

            // Condition if character
            // already present
            if (arr[j][0] == k
                || arr[j][1] == k) {
            }
            else if (arr[j][0] == -1)
                arr[j][0] = k;
            else if (arr[j][1] == -1)
                arr[j][1] = k;

            // Condition if a character
            // have more than two different
            // adjacent characters
            else {
                flag = false;
                break;
            }

            if (arr[k][0] == j
                || arr[k][1] == j) {
            }
            else if (arr[k][0] == -1)
                arr[k][0] = j;
            else if (arr[k][1] == -1)
                arr[k][1] = j;

            // Condition if a character
            // have more than two different
            // adjacent characters
            else {
                flag = false;
                break;
            }
        }

        // Variable to check string contain
        // two end characters or not
        bool contain_ends = false;

        int count = 0;
        int index;

        for (int i = 0; i < 26; i++) {

            // Condition if a character has
            // only one type of adjacent
            // character
            if ((arr[i][0] == -1
                 && arr[i][1] != -1)
                || (arr[i][1] == -1
                    && arr[i][0] != -1)) {
                count++;
                index = i;
            }

            // Condition if the given string
            // has exactly two characters
            // having only one type of adjacent
            // character
            if (count == 2)
                contain_ends = true;

            if (count == 3)
                contain_ends = false;
        }

        if (contain_ends == false
            || flag == false) {
            cout << "Impossible"
                 << "\n";
            return;
        }

        // Depth first Search Traversal
        // on one of the possible end
        // character of the string
        dfs(index);

        // Loop to print the answer
        for (int i = 0; i < answer.size();
             i++) {
            char ch = answer[i] + 'a';
            cout << ch;
        }
    }
};

// Driver Code
int main()
{
    string s = "acabpba";

    graph g;
    g.minString(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// minimum length string such that
// adjacent characters of the string
// remains adjacent in the string
import java.util.ArrayList;

class Graph{

int[][] arr;
ArrayList<Integer> alpha;
ArrayList<Integer> answer;

// Constructor for the Graph
public Graph()
{
    arr = new int[26][2];

    // Initialize the matrix by -1
    for(int i = 0; i < 26; i++)
    {
        for(int j = 0; j < 2; j++)
            arr[i][j] = -1;
    }

    // Initialize the alphabet array
    alpha = new ArrayList<>();
    for(int i = 0; i < 26; i++)
    {
        alpha.add(0);
    }

    answer = new ArrayList<>();
}

// Function to do Depth first
// search Traversal
void dfs(int v)
{

    // Pushing current character
    answer.add(v);

    alpha.set(v, 1);

    for(int i = 0; i < 2; i++)
    {
        if (arr[v][i] == -1 ||
            alpha.get(arr[v][i]) == 1)
            continue;

        dfs(arr[v][i]);
    }
}

// Function to find the minimum
// length string
void minString(String str)
{

    // Condition if given string
    // length is 1
    if (str.length() == 1)
    {
        System.out.println(str);
        return;
    }

    boolean flag = true;

    // Loop to find the adjacency
    // list of the given string
    for(int i = 0; i < str.length() - 1; i++)
    {
        int j = str.charAt(i) - 'a';
        int k = str.charAt(i + 1) - 'a';

        // Condition if character
        // already present
        if (arr[j][0] == k || arr[j][1] == k)
        {}
        else if (arr[j][0] == -1)
            arr[j][0] = k;
        else if (arr[j][1] == -1)
            arr[j][1] = k;

        // Condition if a character
        // have more than two different
        // adjacent characters
        else
        {
            flag = false;
            break;
        }

        if (arr[k][0] == j || arr[k][1] == j)
        {}
        else if (arr[k][0] == -1)
            arr[k][0] = j;
        else if (arr[k][1] == -1)
            arr[k][1] = j;

        // Condition if a character
        // have more than two different
        // adjacent characters
        else
        {
            flag = false;
            break;
        }
    }

    // Variable to check string contain
    // two end characters or not
    boolean contain_ends = false;

    int count = 0;
    int index = 0;

    for(int i = 0; i < 26; i++)
    {

        // Condition if a character has
        // only one type of adjacent
        // character
        if ((arr[i][0] == -1 && arr[i][1] != -1) ||
            (arr[i][1] == -1 && arr[i][0] != -1))
        {
            count++;
            index = i;
        }

        // Condition if the given string
        // has exactly two characters
        // having only one type of adjacent
        // character
        if (count == 2)
            contain_ends = true;

        if (count == 3)
            contain_ends = false;
    }

    if (contain_ends == false || flag == false)
    {
        System.out.println("Impossible");
        return;
    }

    // Depth first Search Traversal
    // on one of the possible end
    // character of the string
    dfs(index);

    // Loop to print the answer
    for(int i = 0; i < answer.size(); i++)
    {
        char ch = (char)(answer.get(i) + 'a');
        System.out.print(ch);
    }
}
}

class GFG{

// Driver Code
public static void main(String[] args)
{
    String s = "acabpba";

    Graph graph = new Graph();
    graph.minString(s);
}
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python implementation to find the
# minimum length string such that
# adjacent characters of the string
# remains adjacent in the string

# Initialize the matrix by -1
arr = [[-1 for i in range(2)] for j in range(26)]

# Initialize the alphabet array
alpha = [0 for i in range(26)]
answer = []

# Function to do Depth first
# search Traversal
def dfs(v):
    global arr
    global alpha
    global answer

    # Pushing current character
    answer.append(v)
    alpha[v] = 1

    for i in range(2):
        if(alpha[arr[v][i]] == 1 or arr[v][i] == -1):
            continue
        dfs(arr[v][i])

# Function to find the minimum
# length string
def minString(Str):

    # Condition if given string
    # length is 1
    if(len(Str) == 1):
        print(Str)
        return

    flag = True
    temp = 0

    # Loop to find the adjacency
    # list of the given string
    for i in range(0,len(Str) - 1):
        j = ord(Str[i]) - ord('a')

        k = ord(Str[i + 1]) - ord('a')

        # Condition if character
        # already present we can do nothing
        if(arr[j][0] == k or arr[j][1] == k):
            temp = 1

        elif(arr[j][0] == -1):
            arr[j][0] = k
        elif(arr[j][1] == -1):
            arr[j][1] = k

        # Condition if a character
        # have more than two different
        # adjacent characters
        else:
            flag = alse
            break

        if(arr[k][0] == j or arr[k][1] == j):
            temp = 0
        elif(arr[k][0] == -1):
            arr[k][0] = j
        elif(arr[k][1] == -1):
            arr[k][1] = j

        # Condition if a character
        # have more than two different
        # adjacent characters
        else:
            flag = False
            break

    # Variable to check string contain
    # two end characters or not
    contain_ends = False

    count = 0
    index = 0

    for i in range(26):

        # Condition if a character has
        # only one type of adjacent
        # character
        if((arr[i][0] == -1 and arr[i][1] != -1) or (arr[i][1] == -1 and arr[i][0] != -1)):
            count += 1
            index = i

        # Condition if the given string
        # has exactly two characters
        # having only one type of adjacent
        # character
        if(count == 2):
            contain_ends = True
        if(count == 3):
            contain_ends = False

    if(contain_ends == False or flag == False):
        print("Impossible")
        return

    # Depth first Search Traversal
    # on one of the possible end
    # character of the string
    dfs(index)

    # Loop to print the answer
    for i in range(len(answer)):
        ch = chr(answer[i] + ord('a'))
        print(ch, end = "")

# Driver Code
s = "acabpba"
minString(s)

# This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>
// Javascript implementation to find the
// minimum length string such that
// adjacent characters of the string
// remains adjacent in the string
let arr;

let  alpha;
let answer;

// Constructor for the Graph
function Graph()
{
    arr = new Array(26);
    for(let i = 0; i < 26; i++)
    {
        arr[i] = new Array(2);
        for(let j = 0; j < 2; j++)
            arr[i][j] = -1;
    }

    alpha = [];
    for(let i = 0; i < 26; i++)
    {
        alpha.push(0);
    }

    answer = [];

}

// Function to do Depth first
// search Traversal
function dfs(v)
{
    // Pushing current character
    answer.push(v);

    alpha[v]= 1;

    for(let i = 0; i < 2; i++)
    {
        if (arr[v][i] == -1 ||
            alpha[arr[v][i]] == 1)
            continue;

        dfs(arr[v][i]);
    }
}

// Function to find the minimum
// length string
function minString(str)
{

    // Condition if given string
    // length is 1
    if (str.length == 1)
    {
        document.write(str+"<br>");
        return;
    }

    let flag = true;

    // Loop to find the adjacency
    // list of the given string
    for(let i = 0; i < str.length - 1; i++)
    {
        let j = str[i].charCodeAt(0) - 'a'.charCodeAt(0);
        let k = str[i + 1].charCodeAt(0) - 'a'.charCodeAt(0);

        // Condition if character
        // already present
        if (arr[j][0] == k || arr[j][1] == k)
        {}
        else if (arr[j][0] == -1)
            arr[j][0] = k;
        else if (arr[j][1] == -1)
            arr[j][1] = k;

        // Condition if a character
        // have more than two different
        // adjacent characters
        else
        {
            flag = false;
            break;
        }

        if (arr[k][0] == j || arr[k][1] == j)
        {}
        else if (arr[k][0] == -1)
            arr[k][0] = j;
        else if (arr[k][1] == -1)
            arr[k][1] = j;

        // Condition if a character
        // have more than two different
        // adjacent characters
        else
        {
            flag = false;
            break;
        }
    }

    // Variable to check string contain
    // two end characters or not
    let contain_ends = false;

    let count = 0;
    let index = 0;

    for(let i = 0; i < 26; i++)
    {

        // Condition if a character has
        // only one type of adjacent
        // character
        if ((arr[i][0] == -1 && arr[i][1] != -1) ||
            (arr[i][1] == -1 && arr[i][0] != -1))
        {
            count++;
            index = i;
        }

        // Condition if the given string
        // has exactly two characters
        // having only one type of adjacent
        // character
        if (count == 2)
            contain_ends = true;

        if (count == 3)
            contain_ends = false;
    }

    if (contain_ends == false || flag == false)
    {
        document.write("Impossible<br>");
        return;
    }

    // Depth first Search Traversal
    // on one of the possible end
    // character of the string
    dfs(index);

    // Loop to print the answer
    for(let i = 0; i < answer.length; i++)
    {
        let ch = String.fromCharCode(answer[i] + 'a'.charCodeAt(0));
        document.write(ch);
    }
}

// Driver Code
let s = "acabpba";

Graph();
minString(s);

// This code is contributed by ab2127
</script>
```

## C#

```
using System.Collections.Generic;
using System;

class Graph{

int[,] arr;
List<int> alpha;
List<int> answer;

// Constructor for the Graph
public Graph()
{
    arr = new int[26,2];

    // Initialize the matrix by -1
    for(int i = 0; i < 26; i++)
    {
        for(int j = 0; j < 2; j++)
            arr[i,j] = -1;
    }

    // Initialize the alphabet array
    alpha = new List<int>();
    for(int i = 0; i < 26; i++)
    {
        alpha.Add(0);
    }

    answer = new List<int>();
}

// Function to do Depth first
// search Traversal
void dfs(int v)
{

    // Pushing current character
    answer.Add(v);

    alpha[v] = 1;

    for(int i = 0; i < 2; i++)
    {
        if (arr[v,i] == -1 ||
            alpha[arr[v,i]] == 1)
            continue;

        dfs(arr[v,i]);
    }
}

// Function to find the minimum
// length string
public void minString(string str)
{

    // Condition if given string
    // length is 1
    if (str.Length == 1)
    {
        Console.WriteLine(str);
        return;
    }

    bool flag = true;

    // Loop to find the adjacency
    // list of the given string
    for(int i = 0; i < str.Length - 1; i++)
    {
        int j = str[i] - 'a';
        int k = str[i+1] - 'a';

        // Condition if character
        // already present
        if (arr[j,0] == k || arr[j,1] == k)
        {}
        else if (arr[j,0] == -1)
            arr[j,0] = k;
        else if (arr[j,1] == -1)
            arr[j,1] = k;

        // Condition if a character
        // have more than two different
        // adjacent characters
        else
        {
            flag = false;
            break;
        }

        if (arr[k,0] == j || arr[k,1] == j)
        {}
        else if (arr[k,0] == -1)
            arr[k,0] = j;
        else if (arr[k,1] == -1)
            arr[k,1] = j;

        // Condition if a character
        // have more than two different
        // adjacent characters
        else
        {
            flag = false;
            break;
        }
    }

    // Variable to check string contain
    // two end characters or not
    bool contain_ends = false;

    int count = 0;
    int index = 0;

    for(int i = 0; i < 26; i++)
    {

        // Condition if a character has
        // only one type of adjacent
        // character
        if ((arr[i,0] == -1 && arr[i,1] != -1) ||
            (arr[i,1] == -1 && arr[i,0] != -1))
        {
            count++;
            index = i;
        }

        // Condition if the given string
        // has exactly two characters
        // having only one type of adjacent
        // character
        if (count == 2)
            contain_ends = true;

        if (count == 3)
            contain_ends = false;
    }

    if (contain_ends == false || flag == false)
    {
        Console.WriteLine("Impossible");
        return;
    }

    // Depth first Search Traversal
    // on one of the possible end
    // character of the string
    dfs(index);

    // Loop to print the answer
    for(int i = 0; i < answer.Count; i++)
    {
        char ch = (char)(answer[i] + 'a');
        Console.Write(ch);
    }
}
}

// Driver Code
public class GFG{
    static public void Main (){

        string s = "acabpba";

    Graph graph = new Graph();
    graph.minString(s);

    }
}

// This code is contributed by patel2127.
```

**Output:** 

```
pbac
```