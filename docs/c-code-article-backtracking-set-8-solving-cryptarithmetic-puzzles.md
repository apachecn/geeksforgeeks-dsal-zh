# 用于解决密码学难题的 C++程序

> 原文:[https://www . geeksforgeeks . org/c-code-article-回溯-set-8-求解-cryptarithmetic-拼图/](https://www.geeksforgeeks.org/c-code-article-backtracking-set-8-solving-cryptarithmetic-puzzles/)

报纸和杂志经常有以下形式的加密算术谜题:
例子:

```
Input : s1 = SEND, s2 = "MORE", s3 = "MONEY"
Output : One of the possible solution is:
         D=1 E=5 M=0 N=3 O=8 R=2 S=7 Y=6  
Explanation:
The above values satisfy below equation : 
  SEND
+ MORE
--------
 MONEY
-------- 

```

强烈建议参考[回溯|集合 8(解决密码谜题)](https://www.geeksforgeeks.org/backtracking-set-8-solving-cryptarithmetic-puzzles/)来处理这个问题。

这个想法是给每个字母分配一个从 0 到 9 的数字，以便算术运算正确。置换是一个递归函数，它为整数的每个可能的置换调用一个校验函数。
Check 函数检查前两个字符串对应的前两个数字之和是否等于第三个字符串对应的第三个数字。如果找到解决方案，则打印解决方案。

```
// CPP program for solving cryptographic puzzles
#include <bits/stdc++.h>
using namespace std;

// vector stores 1 corresponding to index
// number which is already assigned
// to any char, otherwise stores 0
vector<int> use(10);

// structure to store char and its corresponding integer
struct node
{
    char c;
    int v;
};

// function check for correct solution
int check(node* nodeArr, const int count, string s1,
                               string s2, string s3)
{
    int val1 = 0, val2 = 0, val3 = 0, m = 1, j, i;

    // calculate number corresponding to first string
    for (i = s1.length() - 1; i >= 0; i--)
    {
        char ch = s1[i];
        for (j = 0; j < count; j++)
            if (nodeArr[j].c == ch)
                break;

        val1 += m * nodeArr[j].v;
        m *= 10;
    }
    m = 1;

    // calculate number corresponding to second string
    for (i = s2.length() - 1; i >= 0; i--)
    {
        char ch = s2[i];
        for (j = 0; j < count; j++)
            if (nodeArr[j].c == ch)
                break;

        val2 += m * nodeArr[j].v;
        m *= 10;
    }
    m = 1;

    // calculate number corresponding to third string
    for (i = s3.length() - 1; i >= 0; i--)
    {
        char ch = s3[i];
        for (j = 0; j < count; j++)
            if (nodeArr[j].c == ch)
                break;

        val3 += m * nodeArr[j].v;
        m *= 10;
    }

    // sum of first two number equal to third return true
    if (val3 == (val1 + val2))
        return 1;

    // else return false
    return 0;
}

// Recursive function to check solution for all permutations
bool permutation(const int count, node* nodeArr, int n,
                 string s1, string s2, string s3)
{
    // Base case
    if (n == count - 1)
    {

        // check for all numbers not used yet
        for (int i = 0; i < 10; i++)
        {

            // if not used
            if (use[i] == 0)
            {

                // assign char at index n integer i
                nodeArr[n].v = i;

                // if solution found
                if (check(nodeArr, count, s1, s2, s3) == 1)
                {
                    cout << "\nSolution found: ";
                    for (int j = 0; j < count; j++)
                        cout << " " << nodeArr[j].c << " = "
                             << nodeArr[j].v;
                    return true;
                }
            }
        }
        return false;
    }

    for (int i = 0; i < 10; i++)
    {

        // if ith integer not used yet
        if (use[i] == 0)
        {

            // assign char at index n integer i
            nodeArr[n].v = i;

            // mark it as not available for other char
            use[i] = 1;

            // call recursive function
            if (permutation(count, nodeArr, n + 1, s1, s2, s3))
                return true;

            // backtrack for all other possible solutions
            use[i] = 0;
        }
    }
    return false;
}

bool solveCryptographic(string s1, string s2,
                                   string s3)
{
    // count to store number of unique char
    int count = 0;

    // Length of all three strings
    int l1 = s1.length();
    int l2 = s2.length();
    int l3 = s3.length();

    // vector to store frequency of each char
    vector<int> freq(26);

    for (int i = 0; i < l1; i++)
        ++freq[s1[i] - 'A'];

    for (int i = 0; i < l2; i++)
        ++freq[s2[i] - 'A'];

    for (int i = 0; i < l3; i++)
        ++freq[s3[i] - 'A'];

    // count number of unique char
    for (int i = 0; i < 26; i++)
        if (freq[i] > 0)
            count++;

    // solution not possible for count greater than 10
    if (count > 10)
    {
        cout << "Invalid strings";
        return 0;
    }

    // array of nodes
    node nodeArr[count];

    // store all unique char in nodeArr
    for (int i = 0, j = 0; i < 26; i++)
    {
        if (freq[i] > 0)
        {
            nodeArr[j].c = char(i + 'A');
            j++;
        }
    }
    return permutation(count, nodeArr, 0, s1, s2, s3);
}

// Driver function
int main()
{
    string s1 = "SEND";
    string s2 = "MORE";
    string s3 = "MONEY";

    if (solveCryptographic(s1, s2, s3) == false)
        cout << "No solution";
    return 0;
}
```

输出:

```
Solution found:  D=1 E=5 M=0 N=3 O=8 R=2 S=7 Y=6

```