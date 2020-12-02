# 打印所有小于或等于给定值的跳转号

> 原文： [https://www.geeksforgeeks.org/print-all-jumping-numbers-smaller-than-or-equal-to-a-given-value/](https://www.geeksforgeeks.org/print-all-jumping-numbers-smaller-than-or-equal-to-a-given-value/)

如果数字中的所有相邻数字相差 1，则该数字称为跳号。“ 9”和“ 0”之间的差异不视为 1。
所有单个数字都被视为跳号。 例如，7，8987 和 4343456 是跳跃数，而 796 和 89098 不是。

给定正数 x，请打印所有小于或等于 x 的跳数。 数字可以按任何顺序打印。

例：

```
Input: x = 20
Output:  0 1 2 3 4 5 6 7 8 9 10 12

Input: x = 105
Output:  0 1 2 3 4 5 6 7 8 9 10 12
         21 23 32 34 43 45 54 56 65
         67 76 78 87 89 98 101

Note: Order of output doesn't matter, 
i.e. numbers can be printed in any order

```

## 强烈建议您在继续解决方案之前，单击此处进行练习。

一种**简单解决方案**是遍历从 0 到 x 的所有数字。 对于每个遍历的数字，请检查它是否为跳跃数。 如果是，则打印它。 否则忽略它。 该解决方案的时间复杂度为 O（x）。

有效的**解决方案**可以在 O（k）时间内解决此问题，其中 k 是小于或等于 x 的跳跃数的数量。 这个想法是使用 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 或 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 。

假设我们有一个图，其中起始节点为 0，我们需要将其从起始节点遍历到所有可达节点。

鉴于图中给出了关于跳跃数的限制，您认为应该是定义图中下一个过渡的限制。

```
Lets take a example for input x = 90

Start node = 0
From 0, we can move to 1 2 3 4 5 6 7 8 9 
[these are not in our range so we don't add it]

Now from 1, we can move to 12 and 10 
From 2, 23 and 21
From 3, 34 and 32
.
.
.
.
.
.
and so on.

```

以下是上述想法基于 BFS 的实现。

## C++

```cpp

// Finds and prints all jumping numbers smaller than or 
// equal to x. 
#include <bits/stdc++.h> 
using namespace std; 

// Prints all jumping numbers smaller than or equal to x starting 
// with 'num'. It mainly does BFS starting from 'num'. 
void bfs(int x, int num) 
{ 
    // Create a queue and enqueue 'i' to it 
    queue<int> q; 
    q.push(num); 

    // Do BFS starting from i 
    while (!q.empty()) { 
        num = q.front(); 
        q.pop(); 

        if (num <= x) { 
            cout << num << " "; 
            int last_dig = num % 10; 

            // If last digit is 0, append next digit only 
            if (last_dig == 0) 
                q.push((num * 10) + (last_dig + 1)); 

            // If last digit is 9, append previous digit only 
            else if (last_dig == 9) 
                q.push((num * 10) + (last_dig - 1)); 

            // If last digit is neighter 0 nor 9, append both 
            // previous and next digits 
            else { 
                q.push((num * 10) + (last_dig - 1)); 
                q.push((num * 10) + (last_dig + 1)); 
            } 
        } 
    } 
} 

// Prints all jumping numbers smaller than or equal to 
// a positive number x 
void printJumping(int x) 
{ 
    cout << 0 << " "; 
    for (int i = 1; i <= 9 && i <= x; i++) 
        bfs(x, i); 
} 

// Driver program 
int main() 
{ 
    int x = 40; 
    printJumping(x); 
    return 0; 
} 

```