# 打印所有小于或等于给定值的跳跃数

> 原文:[https://www . geesforgeks . org/print-all-jump-numbers-小于或等于给定值/](https://www.geeksforgeeks.org/print-all-jumping-numbers-smaller-than-or-equal-to-a-given-value/)

如果一个数字中所有相邻的数字相差 1，这个数字被称为跳跃数。“9”和“0”之间的差异不被视为 1。
所有的个位数都被认为是跳跃数。例如，7、8987 和 4343456 是跳跃数字，而 796 和 89098 不是。
给定一个正数 x，打印所有小于或等于 x 的跳转数字，数字可以任意顺序打印。

示例:

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

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/preview-problems/705076)

一个**简单的解决方法**是遍历从 0 到 x 的所有数字，对于每个遍历的数字，检查它是否是一个跳跃的数字。如果是，那就打印出来。否则忽略它。该解决方案的时间复杂度为 0(x)。

一个**高效解**可以在 O(k)时间内解决这个问题，其中 k 是小于或等于 x 的跳数个数，思路是使用 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 或 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 。
假设我们有一个图，其中起始节点为 0，我们需要从起始节点遍历到所有可到达的节点。

根据图中给出的关于跳跃数的限制，你认为定义图中下一个过渡的限制应该是什么。

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

以下是上述想法在 BFS 的实现。

## C++

```
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

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Finds and prints all jumping numbers smaller than or
// equal to x.
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG {

    // Prints all jumping numbers smaller than or equal to x starting
    // with 'num'. It mainly does BFS starting from 'num'.
    public void bfs(int x, int num)
    {
        // Create a queue and enqueue 'i' to it
        Queue<Integer> q = new LinkedList<Integer>();
        q.add(num);

        // Do BFS starting from i
        while (!q.isEmpty()) {
            num = q.peek();
            q.poll();
            if (num <= x) {
                System.out.print(num + " ");
                int last_digit = num % 10;

                // If last digit is 0, append next digit only
                if (last_digit == 0) {
                    q.add((num * 10) + (last_digit + 1));
                }

                // If last digit is 9, append previous digit only
                else if (last_digit == 9) {
                    q.add((num * 10) + (last_digit - 1));
                }

                // If last digit is neighter 0 nor 9, append both
                // previous and next digits
                else {
                    q.add((num * 10) + (last_digit - 1));
                    q.add((num * 10) + (last_digit + 1));
                }
            }
        }
    }

    // Prints all jumping numbers smaller than or equal to
    // a positive number x
    public void printJumping(int x)
    {
        System.out.print("0 ");

        for (int i = 1; i <= 9 && i <= x; i++) {
            this.bfs(x, i);
        }
    }

    // Driver program
    public static void main(String[] args) throws IOException
    {
        int x = 40;
        GFG obj = new GFG();
        obj.printJumping(x);
    }
}
```

## 蟒蛇 3

```
# Class queue for use later
class Queue:
    def __init__(self):
        self.lst = []

    def is_empty(self):
        return self.lst == []

    def enqueue(self, elem):
        self.lst.append(elem)

    def dequeue(self):
        return self.lst.pop(0)

# Prints all jumping numbers smaller than or equal to
# x starting with 'num'. It mainly does BFS starting
# from 'num'.
def bfs(x, num):

    # Create a queue and enqueue i to it
    q = Queue()
    q.enqueue(num)

    # Do BFS starting from 1
    while (not q.is_empty()):
        num = q.dequeue()

        if num<= x:
            print(str(num), end =' ')
            last_dig = num % 10

            # If last digit is 0, append next digit only
            if last_dig == 0:
                q.enqueue((num * 10) + (last_dig + 1))

            # If last digit is 9, append previous digit
            # only
            elif last_dig == 9:
                q.enqueue((num * 10) + (last_dig - 1))

            # If last digit is neighter 0 nor 9, append
            # both previous digit and next digit
            else:
                q.enqueue((num * 10) + (last_dig - 1))
                q.enqueue((num * 10) + (last_dig + 1))

# Prints all jumping numbers smaller than or equal to
# a positive number x
def printJumping(x):
    print (str(0), end =' ')
    for i in range(1, 10):
        bfs(x, i)

# Driver Program ( Change value of x as desired )
x = 40
printJumping(x)

# This code is contributed by Saket Modi
```

## C#

```
// C# program to finds and prints all jumping 
// numbers smaller than or equal to x.
using System;
using System.Collections.Generic;

class GFG 
{

    // Prints all jumping numbers smaller than or 
    // equal to x starting with 'num'. It mainly
    // does BFS starting from 'num'.
    public void bfs(int x, int num)
    {
        // Create a queue and enqueue 'i' to it
        Queue<int> q = new Queue<int>();
        q.Enqueue(num);

        // Do BFS starting from i
        while (q.Count!=0) 
        {
            num = q.Peek();
            q.Dequeue();
            if (num <= x) 
            {
                Console.Write(num + " ");
                int last_digit = num % 10;

                // If last digit is 0, append next digit only
                if (last_digit == 0) 
                {
                    q.Enqueue((num * 10) + (last_digit + 1));
                }

                // If last digit is 9, append previous digit only
                else if (last_digit == 9) 
                {
                    q.Enqueue((num * 10) + (last_digit - 1));
                }

                // If last digit is neighter 0 nor 9, append both
                // previous and next digits
                else 
                {
                    q.Enqueue((num * 10) + (last_digit - 1));
                    q.Enqueue((num * 10) + (last_digit + 1));
                }
            }
        }
    }

    // Prints all jumping numbers smaller than or equal to
    // a positive number x
    public void printJumping(int x)
    {
        Console.Write("0 ");

        for (int i = 1; i <= 9 && i <= x; i++) 
        {
            this.bfs(x, i);
        }
    }

    // Driver code
    public static void Main(String[] args) 
    {
        int x = 40;
        GFG obj = new GFG();
        obj.printJumping(x);
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Finds and prints all jumping numbers 
// smaller than or equal to x.

// Prints all jumping numbers smaller than
// or equal to x starting with 'num'. It 
// mainly does BFS starting from 'num'.
function bfs(x, num)
{

    // Create a queue and enqueue 'i' to it
    let q = [];
    q.push(num);

    // Do BFS starting from i
    while (q.length != 0) 
    {
        num = q.shift();

        if (num <= x) 
        {
            document.write(num + " ");
            let last_digit = num % 10;

            // If last digit is 0, append next digit only
            if (last_digit == 0) 
            {
                q.push((num * 10) + (last_digit + 1));
            }

            // If last digit is 9, append previous 
            // digit only
            else if (last_digit == 9)
            {
                q.push((num * 10) + (last_digit - 1));
            }

            // If last digit is neighter 0 nor 9, 
            // append both previous and next digits
            else 
            {
                q.push((num * 10) + (last_digit - 1));
                q.push((num * 10) + (last_digit + 1));
            }
        }
    }
}

// Prints all jumping numbers smaller 
// than or equal to a positive number x
function printJumping(x)
{
    document.write("0 ");

    for(let i = 1; i <= 9 && i <= x; i++)
    {
        bfs(x, i);
    }
}

// Driver code
let x = 40;
printJumping(x);

// This code is contributed by rag2127

</script>
```

**输出:**

```
0 1 10 12 2 21 23 3 32 34 4 5 6 7 8 9 
```

感谢 Gaurav Ahirwar 的上述解决方案。

**运动:**

1.  将上述解决方案改为使用 DFS 而不是 BFS。
2.  扩展您的解决方案，以排序顺序打印所有数字，而不是任何顺序。
3.  进一步扩展解决方案，打印给定范围内的所有数字。

如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。