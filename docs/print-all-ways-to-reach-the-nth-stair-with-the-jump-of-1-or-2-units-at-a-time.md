# 打印一次跳 1 或 2 个单位到达第 n 级楼梯的所有方式

> 原文:[https://www . geeksforgeeks . org/print-所有到达第 n 个阶梯的方法，每次跳 1 或 2 个单位/](https://www.geeksforgeeks.org/print-all-ways-to-reach-the-nth-stair-with-the-jump-of-1-or-2-units-at-a-time/)

给定一个正整数 **N** 代表 **N** 楼梯和一个人它在第一个楼梯，任务是打印所有到达 **N <sup>第</sup>楼梯**的方式，一次跳转 **1 或 2 个单位**。

**示例:**

> ***输入:** N = 3*
> ***输出:***
> *11*
> *2*
> ***说明:***
> *第 N 级楼梯可通过以下方式到达，每级跳 1 或 2 个单位为:*
> 
> 1.  执行 1 个单位的两次跳跃，每次为 1 -> 1。
> 2.  执行两次跳跃，每次 1 个单位，作为 2。
> 
> **输入:***N = 5*
> T5】输出:
> 1111
> 112
> 121
> 211
> 22

**方法:**给定的问题可以使用[递归](https://www.geeksforgeeks.org/recursion/)来解决。这个想法是涵盖每次一两次跳跃的情况，并打印所有可能到达**N<sup>th</sup>stage**的方法。按照以下步骤解决给定的问题:

*   定义一个递归函数，比如**total 可能性跳跃(int N)** ，返回所有可能的跳跃方式到达 **N <sup>第</sup>级**。
    *   在递归的起点，检查基本情况如下:
        *   如果 **N < 0** ，那么就不是有效的方式。所以返回一个空数组
        *   如果 **N = 0** ，则是有效方式。所以返回一个包含一个空白空间的大小为 **1** 的数组。
    *   每次递归调用[递归函数](https://www.geeksforgeeks.org/recursive-functions/)两次，一次用于 **1 单元跳转**，另一次用于 **2 单元跳转**，并分别存储结果。
    *   初始化一个字符串的[数组，比如 **totalJumps** 来存储到达 **i <sup>th</sup> 索引**的方法，并存储所有可能的到达索引 **i** 的方法，结果存储在上述两个递归调用中。](https://www.geeksforgeeks.org/array-strings-c-3-different-ways-create/)
*   完成上述步骤后，将上述递归调用返回的所有可能的组合打印为**total 可能性跳转(N)** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find all the ways to reach
// Nth stair using one or two jumps
vector<string> TotalPossibleJumps(int N)
{
    // Base Cases
    if ((N - 1) == 0) {
        vector<string> newvec;
        newvec.push_back("");
        return newvec;
    }
    else {
        if (N < 0) {
            vector<string> newvec;
            return newvec;
        }
    }

    // Recur for jump1 and jump2
    vector<string> jump1
        = TotalPossibleJumps(N - 1);
    vector<string> jump2
        = TotalPossibleJumps(N - 2);

    // Stores the total possible jumps
    vector<string> totaljumps;

    // Add "1" with every element
    // present in jump1
    for (string s : jump1) {
        totaljumps.push_back("1" + s);
    }

    // Add "2" with every element
    // present in jump2
    for (string s : jump2) {
        totaljumps.push_back("2" + s);
    }

    return totaljumps;
}

// Driver Code
int main()
{
    int N = 3;
    vector<string> Ans = TotalPossibleJumps(N);
    for (auto& it : Ans)
        cout << it << '\n';

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to find all the ways to reach
    // Nth stair using one or two jumps
    static ArrayList<String> TotalPossibleJumps(int N)
    {
        // Base Cases
        if ((N - 1) == 0) {
            ArrayList<String> newvec
                = new ArrayList<String>();
            newvec.add("");
            return newvec;
        }
        else {
            if (N < 0) {
                ArrayList<String> newvec
                    = new ArrayList<String>();
                return newvec;
            }
        }

        // Recur for jump1 and jump2
        ArrayList<String> jump1 = TotalPossibleJumps(N - 1);
        ArrayList<String> jump2 = TotalPossibleJumps(N - 2);

        // Stores the total possible jumps
        ArrayList<String> totaljumps
            = new ArrayList<String>();

        // Add "1" with every element
        // present in jump1
        for (String s : jump1) {
            totaljumps.add("1" + s);
        }

        // Add "2" with every element
        // present in jump2
        for (String s : jump2) {
            totaljumps.add("2" + s);
        }

        return totaljumps;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 3;
        ArrayList<String> Ans = TotalPossibleJumps(N);
        for (String it : Ans)
            System.out.println(it);
    }
}

// This code is contributed by ukasp.
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find all the ways to reach
# Nth stair using one or two jumps

def TotalPossibleJumps(N):

    # Base Cases
    if ((N - 1) == 0):
        newvec = []
        newvec.append("")
        return newvec

    else:
        if (N < 0):
            newvec = []
            return newvec

    # Recur for jump1 and jump2
    jump1 = TotalPossibleJumps(N - 1)
    jump2 = TotalPossibleJumps(N - 2)

    # Stores the total possible jumps
    totaljumps = []

    # Add "1" with every element
    # present in jump1
    for s in jump1:
        totaljumps.append("1" + s)

    # Add "2" with every element
    # present in jump2
    for s in jump2:
        totaljumps.append("2" + s)

    return totaljumps

# Driver Code
if __name__ == "__main__":

    N = 3
    Ans = TotalPossibleJumps(N)
    for it in Ans:
        print(it)

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find all the ways to reach
// Nth stair using one or two jumps
static List<string> TotalPossibleJumps(int N)
{
    // Base Cases
    if ((N - 1) == 0) {
        List<string> newvec = new List<string>();
        newvec.Add("");
        return newvec;
    }
    else {
        if (N < 0) {
            List<string> newvec = new List<string>();
            return newvec;
        }
    }

    // Recur for jump1 and jump2
    List<string> jump1
        = TotalPossibleJumps(N - 1);
    List<string> jump2
        = TotalPossibleJumps(N - 2);

    // Stores the total possible jumps
    List<string> totaljumps = new List<string>();

    // Add "1" with every element
    // present in jump1
    foreach (string s in jump1) {
        totaljumps.Add("1" + s);
    }

    // Add "2" with every element
    // present in jump2
    foreach (string s in jump2) {
        totaljumps.Add("2" + s);
    }

    return totaljumps;
}

// Driver Code
public static void Main()
{
    int N = 3;
    List<string> Ans = TotalPossibleJumps(N);
    foreach(string it in Ans)
        Console.WriteLine(it);
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>
    // JavaScript program for the above approach

    // Function to find all the ways to reach
    // Nth stair using one or two jumps
    const TotalPossibleJumps = (N) => {
        // Base Cases
        if ((N - 1) == 0) {
            let newvec = [];
            newvec.push("");
            return newvec;
        }
        else {
            if (N < 0) {
                let newvec = [];
                return newvec;
            }
        }

        // Recur for jump1 and jump2
        let jump1 = TotalPossibleJumps(N - 1);
        let jump2 = TotalPossibleJumps(N - 2);

        // Stores the total possible jumps
        let totaljumps = [];

        // Add "1" with every element
        // present in jump1
        for (let s in jump1) {
            totaljumps.push("1" + jump1[s]);
        }

        // Add "2" with every element
        // present in jump2
        for (let s in jump2) {
            totaljumps.push("2" + jump2[s]);
        }

        return totaljumps;
    }

    // Driver Code

    let N = 3;
    let Ans = TotalPossibleJumps(N);
    for (let it in Ans)
        document.write(`${Ans[it]}<br/>`);

// This code is contributed by rakeshsahni
</script>
```

**Output:** 

```
11
2
```

**时间复杂度:**O(2<sup>N</sup>)
T5】辅助空间: O(N)