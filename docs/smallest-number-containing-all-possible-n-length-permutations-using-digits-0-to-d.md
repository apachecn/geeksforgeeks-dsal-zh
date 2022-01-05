# 包含所有可能的 N 长度排列的最小数字，使用数字 0 到 D

> 原文:[https://www . geesforgeks . org/最小-包含数字-所有可能的-n-长度-排列-使用数字-0 到-d/](https://www.geeksforgeeks.org/smallest-number-containing-all-possible-n-length-permutations-using-digits-0-to-d/)

给定两个整数 **N** 和 **D** ，任务是找到包含所有长度排列的最小字符串的大小 **N** ，该长度排列可以使用第一个 **D** 数字 **(0，1，…，D-1)** 形成。
**举例:**

> **输入:** N = 2，D = 2
> **输出:** 01100
> **解释:**
> 长度 2 从数字(0，1)开始的可能排列是{00，01，10，11}。
> “01100”就是这样一个包含所有排列的子串。
> 其他可能的答案是“00110”、“10011”、“11001”
> **输入:** N = 2，D = 4
> **输出:** 03322312113020100
> **解释:**
> 这里从数字{0，1，2，3}开始的长度 2 的所有可能排列都是
> 00 10 20 30

**方法:**
追加‘0’N-1 次，在当前状态下调用字符串上的 [DFS](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 。逐个追加所有的 D 字符。每次追加后，检查新字符串是否被访问。如果是，将其插入 [HashSet](https://www.geeksforgeeks.org/hashset-in-java/) 标记为已访问，并在答案中添加该字符。递归调用最后 D 个字符上的 DFS 函数。重复这个过程，直到从 D 位开始的所有可能的 N 长度子串都被附加到字符串中。打印生成的最终字符串。
以下是上述方法的实施:

## C++

```
// C++ Program to find the
// minimum length string
// consisting of all
// permutations of length N
// of D digits
#include <bits/stdc++.h>
using namespace std;

// Initialize set to see
// if all the possible
// permutations are present
// in the min length string
set<string> visited;

// To keep min length string
string ans;

// Generate the required string
void dfs(string curr, int D)
{
    // Iterate over all the possible
    // character
    for (int x = 0; x < D; ++x) {
        char chr = x + '0';

        // Append to make a new string
        string neighbour = curr + chr;
        // If the new string is not
        // visited

        if (visited.find(neighbour) == visited.end()) {

            // Add in set
            visited.insert(neighbour);
            // Call the dfs function on
            // the last d characters
            dfs(neighbour.substr(1), D);

            ans.push_back(chr);
        }
    }
}
string reqString(int N, int D)
{
    // Base case
    if (N == 1 && D == 1)
        return "0";

    visited.clear();
    ans.clear();
    string start;

    // Append '0' n-1 times
    for (int i = 0; i < N - 1; i++)
        start.append("0");

    // Call the DFS Function
    dfs(start, D);

    ans.append(start);
    return ans;
}

// Driver Code
int main()
{
    int N = 2;
    int D = 2;
    cout << reqString(N, D) << '\n';
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
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

## 蟒蛇 3

```
# Python3 Program to find the
# minimum length string
# consisting of all
# permutations of length N
# of D digits

#  Initialize set to see
#  if all the possible
#  permutations are present
#  in the min length string
visited=set()

# To keep min length string
ans=[]

# Generate the required string
def dfs(curr, D):

    # Iterate over all possible character
    for c in range(D):
        c = str(c)

        # Append to make a new string
        neighbour = curr + c

        # If the new string is not visited
        if neighbour not in visited:

            # Add in set
            visited.add(neighbour)

            # Call the dfs function on the last d characters
            dfs(neighbour[1:], D)

            ans.append(c)

def reqString(N, D):
    # Base case
    if (N == 1 and D == 1):
        return "0"

    # Append '0' n-1 times
    start=''.join(['0']*(N - 1))

    # Call the DFS Function
    dfs(start, D)

    ans.extend(['0']*(N - 1))
    return ''.join(ans)

if __name__ == '__main__':
    N, D = 2, 2
    print(reqString(N,D))

    # This code is contributed by amartyaghoshgfg.
```

**Output:** 

```
01100
```

***时间复杂度:**O(N * D<sup>N</sup>)*
***辅助空间:** O(N * D <sup>N</sup> )*