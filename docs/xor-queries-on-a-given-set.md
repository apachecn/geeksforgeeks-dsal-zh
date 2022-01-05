# 给定集合上的异或查询

> 原文:[https://www.geeksforgeeks.org/xor-queries-on-a-given-set/](https://www.geeksforgeeks.org/xor-queries-on-a-given-set/)

给定初始元素为 0 的集合 S，即 S = { 0 }。任务是在给出 Q 个查询时执行每个查询，并在每个类型为 3 的查询后打印答案。
我们可以进行三种查询操作:

*   **1 X:** 我们可以在集合 s 中加入 X。
*   **2 Y:** 对于每个元素 I，执行 i ⊕ Y。
*   **3:** 求集合的最小元素。

**例:**

> **输入:** Q = 10，
> 3
> 1 7
> 3
> 2 4
> 2 8
> 2 3
> 1 10
> 1 3
> 3
> 2 1
> **输出:** 0 0 3
> **解释:**
> 对于给定的 10 个查询，每个查询的集合变化如下:
> 
> 1.  最小值为 0。
> 2.  S–> { 0，7}中添加的数字 7。
> 3.  最小值仍为 0。
> 4.  S 中的所有数字都改为 4–> { 4，3}的异或。
> 5.  S 中的所有数字都改为与 8–> { 12，11}的异或。
> 6.  S 中的所有数字都被改为 3–> { 15，8}的异或。
> 7.  S–> { 15，8，10}中添加的数字 10。
> 8.  S–> { 15，8，10，3}中添加的数字 3。
> 9.  最低现在是 3。
> 10.  S 中的所有数字都改为 1–> { 14，9，11，2}的异或。
> 
> **输入:**Q = 6
> 3
> 1 7
> 3
> 1 4
> 2 8
> 3
> T9】输出: 0 0 8

**先决条件:**T2】特里尔。
**方法:**
我们将尝试使用[最小异或值对](https://www.geeksforgeeks.org/minimum-xor-value-pair/)问题的 trie 方法来解决这个问题。

*   所以，在这个问题中，我们有一个二进制 trie 和一个整数 x，我们必须找到 XOR(x，y)的最小值，其中 y 是 trie 中的某个整数。

*   现在，为了解决这个问题，我们将从最高有效位到最低有效位进行遍历。

*   假设我们在第一位:
    如果 x[i]是 1，我们将沿着有 1 的特里的路径前进。
    如果 x[i]为 0，我们将沿着有 0 的路径前进。
    如果在位置 I，我们没有分支可以向下 x[i]，我们将走另一条路。

现在，说到我们的问题。

*   假设我们在集合中插入了 a1、a2、a3，然后将所有的东西与 x1、x2、x3 进行异或运算，那么这就和用 X = XOR(x1、x2、x3)进行异或运算是一样的。

*   所以，求最小元素相当于和 x 异或后求(a1，a2，a3)中的最小值
    我们一开始就已经注意到怎么做了。

*   现在，如何回答每个问题。
    设 x = XOR(x1，x2，…..，xn)，其中 x1，x2，…，xn 都是要求与集合 s 的元素异或的数字。
    1.  对于**查询 2** ，与 xi 异或。
        我们不会将 trie 中的每个元素与 xi 进行异或运算。相反，我们将只更新 x = XOR(x，xi)

    2.  对于**查询 3** ，获取最小元素。
        到目前为止，我们应该用 X 对整个数组进行异或运算。
        所以，现在我们将使用上述方法计算集合中所有元素与 X 进行异或运算得到的最小值。

    3.  对于**查询 1** ，插入 ai。
        我们不会在 trie 中插入 ai，而是 XOR(ai，x)。原因:
        *   假设我们插入 a1，a2，然后与 x1 异或，然后插入 a3，然后与 x2 异或。

        *   当我们现在查询最小值时，我们会在:{XOR(a1，x1，x2)，XOR(a2，x1，x2)，XOR(a3，x1，x2)}
            中找到最小值，但是 a3 只和 x2 进行了 XOR 运算，没有和 x1 进行 XOR 运算。

        *   因此，在我们将元素 ai 插入 trie 的每个时刻，我们插入 XOR(ai，x)是至关重要的。这确保了当我们计算最小值时，它将抵消之前的 xor。
            所以，在我们的例子中，我们的 trie 将包含
            {a1，a2，XOR(a3，x1)}。

        *   当我们查询 XOR(x)的最小值时，我们将使用上述{XOR(a1，x1，x2)，XOR(a2，x1，x2)，XOR(a3，x2)}的方法找到最小值，这就是我们想要的。插入 XOR(ai，x)将确保无论我们做什么最小操作，我们都不会在任何 ai 上做任何不必要的 XOR。

下面是这种方法的 C++实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to operate
// queries in a given set
#include <bits/stdc++.h>
using namespace std;

const int Maxbits = 30;

// Function for Query 1
void Insert(int x, int curx,
            int* sz, int trie[100][2])
{
    // XOR each element before
    // storing it in the trie.
    x = x ^ curx;
    int p = 0;

    // Storing xored element in the trie.
    for (int i = Maxbits - 1; i >= 0; i--)
    {
        if (!trie[p][x >> i & 1])
            trie[p][x >> i & 1] = (*sz)++;

        p = trie[p][x >> i & 1];
    }
}

// Function for Query 2
void XorQuery(int x, int* curx)
{
    // Simply xor-ing all the number which
    // was asked to xor with the set elements.
    (*curx) = (*curx) ^ x;
}

// Function for Query 3
void MinXor(int x, int trie[100][2])
{
    int ans = 0, p = 0;

    // Finding the minimum element by checking
    // if x[i] bit is same with trie element.
    for (int i = Maxbits - 1; i >= 0; i--)
    {
        bool Currbit = (x >> i & 1);

        if (trie[p][Currbit])
            p = trie[p][Currbit];

        else {
            p = trie[p][!Currbit];
            ans |= 1 << i;
        }
    }

    cout << ans << endl;
}

// Driver code
int main()
{
    int sz = 1;
    int curx = 0;
    int trie[100][2] = { 0 };

    // Initialising the trie
    Insert(0, 0, &sz, trie);

    // Calling the Query
    MinXor(curx, trie);
    Insert(7, curx, &sz, trie);
    MinXor(curx, trie);
    XorQuery(4, &curx);
    XorQuery(8, &curx);
    XorQuery(3, &curx);
    Insert(10, curx, &sz, trie);
    Insert(3, curx, &sz, trie);
    MinXor(curx, trie);
    XorQuery(1, &curx);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to operate
# queries in a given set

Maxbits = 30

# Function for Query 1

def Insert(x, curx, trie):
    global sz
    # XOR each element before
    # storing it in the trie.
    x = x ^ curx
    p = 0

    # Storing xored element in the trie.
    for i in range(Maxbits - 1, -1, -1):
        if not(trie[p][x >> i & 1]):
            trie[p][x >> i & 1] = sz
            sz += 1

        p = trie[p][x >> i & 1]

# Function for Query 2
def XorQuery(x,):
    global curx
    # Simply xor-ing all the number which
    # was asked to xor with the set elements.
    curx ^= x

# Function for Query 3
def MinXor(x, trie):
    ans = 0
    p = 0

    # Finding the minimum element by checking
    # if x[i] bit is same with trie element.
    for i in range(Maxbits - 1, -1, -1):
        Currbit = (x >> i & 1)

        if (trie[p][Currbit]):
            p = trie[p][Currbit]

        else:
            p = trie[p][~Currbit]
            ans |= 1 << i

    print(ans)

# Driver code
if __name__ == '__main__':
    sz = 1
    curx = 0
    trie = [[0]*2 for _ in range(100)]

    # Initialising the trie
    Insert(0, 0, trie)

    # Calling the Query
    MinXor(curx, trie)
    Insert(7, curx, trie)
    MinXor(curx, trie)
    XorQuery(4, )
    XorQuery(8, )
    XorQuery(3, )
    Insert(10, curx, trie)
    Insert(3, curx,  trie)
    MinXor(curx, trie)
    XorQuery(1,)
```

**Output:** 

```
0
0
3
```

**时间复杂度:**每个查询 O(N)。其中 N 是查询元素中的位数。
**辅助空间:** O(N)