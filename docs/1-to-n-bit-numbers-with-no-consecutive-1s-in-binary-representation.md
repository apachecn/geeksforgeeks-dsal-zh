# 二进制表示中没有连续 1 的 1 到 n 位数字。

> 原文:[https://www . geeksforgeeks . org/1 至 n 位二进制无连续 1 的数字/](https://www.geeksforgeeks.org/1-to-n-bit-numbers-with-no-consecutive-1s-in-binary-representation/)

给定一个数字 n，我们的任务是找到所有 1 到 n 个二进制表示中没有连续 1 的比特数。

示例:

```
Input : n = 4
Output : 1 2 4 5 8 9 10
These are numbers with 1 to 4
bits and no consecutive ones in
binary representation.

Input : n = 3
Output : 1 2 4 5

```

我们一个接一个地添加位，并递归打印数字。对于最后一点，我们有两个选择。

```
   if last digit in sol is 0 then
      we can insert 0 or 1 and recur. 
   else if last digit is 1 then
      we can insert 0 only and recur.

```

我们将使用递归-

1.  我们制作一个解向量 sol，并在其中插入第一位 1，这将是第一个数字。
2.  现在我们检查解向量的长度是否小于或等于 n。
3.  如果是这样，那么我们计算十进制数，并将其存储到地图中，因为它以排序顺序存储数字。
4.  现在我们有两个条件-
    *   如果 sol 中的最后一个数字是 0，我们可以插入 0 或 1 并重复。
    *   否则，如果最后一个数字是 1，那么我们只能插入 0 并重复。

```
numberWithNoConsecutiveOnes(n, sol)
{
if sol.size() <= n

  //  calculate decimal and store it
  if last element of sol is 1
     insert 0 in sol 
     numberWithNoConsecutiveOnes(n, sol)
 else
     insert 1 in sol
     numberWithNoConsecutiveOnes(n, sol)

     // because we have to insert zero 
     // also in place of 1
     sol.pop_back();
     insert 0 in sol
     numberWithNoConsecutiveOnes(n, sol)
 }

```

```
// CPP program to find all numbers with no
// consecutive 1s in binary representation.
#include <bits/stdc++.h>

using namespace std;
map<int, int> h;

void numberWithNoConsecutiveOnes(int n, vector<int> 
                                              sol)
{
    // If it is in limit i.e. of n lengths in 
    // binary
    if (sol.size() <= n) {
        int ans = 0;
        for (int i = 0; i < sol.size(); i++)
            ans += pow((double)2, i) * 
                   sol[sol.size() - 1 - i];
        h[ans] = 1;

        // Last element in binary
        int last_element = sol[sol.size() - 1];

        // if element is 1 add 0 after it else 
        // If 0 you can add either 0 or 1 after that
        if (last_element == 1) {
            sol.push_back(0);
            numberWithNoConsecutiveOnes(n, sol);
        } else {
            sol.push_back(1);
            numberWithNoConsecutiveOnes(n, sol);
            sol.pop_back();
            sol.push_back(0);
            numberWithNoConsecutiveOnes(n, sol);
        }
    }
}

// Driver program
int main()
{
    int n = 4;
    vector<int> sol;

    // Push first number
    sol.push_back(1);

    // Generate all other numbers
    numberWithNoConsecutiveOnes(n, sol);

    for (map<int, int>::iterator i = h.begin();
                            i != h.end(); i++)
        cout << i->first << " ";
    return 0;
}
```

输出:

```
1 2 4 5 8 9 10

```

**相关帖子:**
[统计没有连续 1 的二进制字符串数量](https://www.geeksforgeeks.org/count-number-binary-strings-without-consecutive-1s/)

本文由**尼泰什·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。