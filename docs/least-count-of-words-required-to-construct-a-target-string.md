# 构建目标字符串所需的最少字数

> 原文:[https://www . geesforgeks . org/构造目标字符串所需的最少字数/](https://www.geeksforgeeks.org/least-count-of-words-required-to-construct-a-target-string/)

给定一组大小为 **M** 的[弦](https://www.geeksforgeeks.org/array-strings-c-3-different-ways-create/)、**字[]** 和大小为 **N** 的[弦](https://www.geeksforgeeks.org/string-data-structure/) **靶。任务是通过从单词集合中剪切出单个字母并重新排列，找到拼出字符串**目标**所需的最小数量的**单词**，前提是每个单词有无限的供应量。如果不可能，请打印-1。**

**示例:**

> **输入:**单词[]= {“with”、“example”、“science”}，target =“thehat”
> **输出:** 3
> **解释:**目标字符串中，“The hat”由{'h' = 2，' t' = 2，' e' = 1，' a' = 1}组成。
> 两个“with”字符串需要得到两个‘h’和两个‘t’，一个“example”字符串需要得到一个‘e’和一个‘a’组成目标字符串“thehat”。
> 所以，构建给定目标所需的总字数是 3。
> 
> **输入:**单词[] = {“注意”、“可能”}，target =“基本基础”
> **输出:** -1
> **说明:**不可能形成给定的目标字符串。

**进场:**思路是用[回溯](https://www.geeksforgeeks.org/backtracking-introduction/)。按照以下步骤解决问题:

*   声明一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-in-java/)，说 **countMap【】【】，**其中**count map【I】【j】**存储 **i <sup>th</sup>** 字符串中**j<sup>th</sup>T9】字符的个数。**
*   声明一个表示当前可用字符数的[数组](https://www.geeksforgeeks.org/array-data-structure/) **字符变量【26】**。
*   定义一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/)，该函数接受字符串的当前索引 **i** (初始为 0)**目标**作为输入。
    *   如果当前计数大于总计数，则[返回](https://www.geeksforgeeks.org/return-keyword-java/)。另外，如果当前指数 **i** 等于 **N** ，更新总计数[返回](https://www.geeksforgeeks.org/return-keyword-java/)。
    *   如果在**字符中出现**目标【I】****，
        *   减少字符**目标【I】**在**字符可用[]** 中的出现。
        *   [递归调用](https://www.geeksforgeeks.org/recursion/)获取索引 **i+1** ，同时将计数更新 1。
        *   在函数调用[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)后，将字符**目标【I】**的出现次数增加 1。
    *   否则，[迭代**count map【】【】**T3】找到**目标【I】**的出现。如果找到，则](https://www.geeksforgeeks.org/how-to-iterate-over-a-2d-list-or-list-of-lists-in-java/)[通过将计数更新 1 来递归调用](https://www.geeksforgeeks.org/recursion/)函数，并在函数调用后执行[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)步骤。
*   打印所需的最少字数。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// countMap[][] to store
// count of characters
vector<vector<int> > countMap;

int cnt = INT_MAX;

// Function to get minimum number of
// stickers for a particular state
void count(int curCnt, int pos, vector<int>charAvailable,
           string target, vector<string> stickers)
{

    // If an optimal solution is
    // already there, return
    if (curCnt >= cnt)
        return;

    int m = stickers.size();
    int n = target.size();

    // If Target has been constructed
    // update cnt and return
    if (pos == n)
    {
        cnt = min(cnt, curCnt);
        return;
    }

    char c = target[pos];

    if (charAvailable > 0)
    {

        // Update charAvailable[]
        charAvailable--;

        // Recursizevely function call
        // for (pos + 1)
        count(curCnt, pos + 1, charAvailable,
              target, stickers);

        // Update charAvailable[]
        charAvailable++;
    }
    else
    {
        for(int i = 0; i < m; i++)
        {
            if (countMap[i] == 0)
                continue;

            // Update charAvailable[]
            for(int j = 0; j < 26; j++)
            {
                charAvailable[j] += countMap[i][j];
            }

            // Recursizeve Call
            count(curCnt + 1, pos, charAvailable,
                  target, stickers);

            // Update charAvailable[]
            for(int j = 0; j < 26; j++)
            {
                charAvailable[j] -= countMap[i][j];
            }
        }
    }
}

// Function to find the minimum
// number of stickers
int minStickers(vector<string> stickers,
                string target)
{

    // Base Case
    if (target == "")
        return -1;

    if (target.size() == 0)
        return 0;

    if (stickers.size() == 0)
        return -1;

    int m = stickers.size();
    countMap.resize(m, vector<int>(26, 0));

    // Fill the countMap Array
    for(int i = 0; i < stickers.size(); i++)
    {
        string s = stickers[i];
        for(char c : s)
        {
            countMap[i]++;
        }
    }

    // Recusizeve function call to get
    // minimum number of stickers
    vector<int> temp(26);
    count(0, 0, temp, target, stickers);

    return cnt == INT_MAX ? -1 : cnt;
}

// Driver Code
int main()
{

    // Given Input
    vector<string> str = {"with", "example", "science"};
    string target = "thehat";

    // Function Call
    int Result = minStickers(str, target);

    // Print the result
    cout << Result;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.io.*;
import java.util.*;

class Sol {

    // countMap[][] to store
    // count of characters
    int[][] countMap;

    int cnt = Integer.MAX_VALUE;

    // Function to find the minimum
    // number of stickers
    public int minStickers(String[] stickers
                           , String target)
    {
        // Base Case
        if (target == null)
            return -1;

        if (target.length() == 0)
            return 0;

        if (stickers == null || stickers.length == 0)
            return -1;

        int m = stickers.length;
        countMap = new int[m][26];

        // Fill the countMap Array
        for (int i = 0; i < stickers.length; i++) {
            String s = stickers[i];
            for (char c : s.toCharArray()) {
                countMap[i]++;
            }
        }

        // Recursive function call to get
        // minimum number of stickers
        count(0, 0, new int[26], target, stickers);

        return cnt == Integer.MAX_VALUE ? -1 : cnt;
    }

    // Function to get minimum number of
    // stickers for a particular state
    private void count(int curCnt, int pos,
                       int[] charAvailable, String target,
                       String[] stickers)
    {
        // If an optimal solution is
        // already there, return
        if (curCnt >= cnt)
            return;

        int m = stickers.length;
        int n = target.length();

        // If Target has been constructed
        // update cnt and return
        if (pos == n) {
            cnt = Math.min(cnt, curCnt);
            return;
        }

        char c = target.charAt(pos);

        if (charAvailable > 0) {

            // Update charAvailable[]
            charAvailable--;

            // Recursively function call
            // for (pos + 1)
            count(curCnt, pos + 1, charAvailable, target,
                  stickers);

            // Update charAvailable[]
            charAvailable++;
        }
        else {
            for (int i = 0; i < m; i++) {

                if (countMap[i] == 0)
                    continue;

                // Update charAvailable[]
                for (int j = 0; j < 26; j++) {
                    charAvailable[j] += countMap[i][j];
                }

                // Recursive Call
                count(curCnt + 1, pos, charAvailable,
                      target, stickers);

                // Update charAvailable[]
                for (int j = 0; j < 26; j++) {
                    charAvailable[j] -= countMap[i][j];
                }
            }
        }
    }
}

class GFG {

    // Driver Code
    public static void main(String[] args)
    {
        Sol st = new Sol();

        // Given Input
        String[] str = { "with", "example", "science" };
        String target = "thehat";

        // Function Call
        int Result = st.minStickers(str, target);

        // Print the result
        System.out.println(Result);
    }
}
```

**Output:** 

```
3
```

***时间复杂度:**O(M * 26 * 2<sup>N</sup>)*
***辅助空间:** O(M*26)*