# 堆栈排列(检查一个数组是否是其他数组的堆栈排列)

> 原文:[https://www . geeksforgeeks . org/stack-排列-检查数组是否是堆栈-排列-其他/](https://www.geeksforgeeks.org/stack-permutations-check-if-an-array-is-stack-permutation-of-other/)

**堆栈排列**是给定输入队列中对象的排列，这是通过借助堆栈和内置的推送和弹出功能将元素从输入队列转移到输出队列来完成的。
定义明确的规则是:

1.  仅从输入队列出列。
2.  在单个堆栈中使用内置的推送、弹出功能。
3.  堆栈和输入队列的末尾必须为空。
4.  仅排队到输出队列。

对于单个输入队列，使用堆栈有大量可能的排列。
给定两个数组，都是唯一元素。一个代表输入队列，另一个代表输出队列。我们的任务是通过堆栈排列检查给定的输出是否可能。
**例:**

```
Input : First array: 1, 2, 3  
        Second array: 2, 1, 3
Output : Yes
Procedure:
push 1 from input to stack
push 2 from input to stack
pop 2 from stack to output
pop 1 from stack to output
push 3 from input to stack
pop 3 from stack to output

Input : First array: 1, 2, 3  
        Second array: 3, 1, 2
Output : Not Possible  
```

这样做的想法是，我们将尝试使用堆栈将输入队列转换为输出队列，如果我们能够这样做，那么队列是可置换的，否则就不能。
**下面是做这个的分步算法** :

1.  不断地从输入队列中弹出元素，并检查它是否等于输出队列的顶部，如果它不等于输出队列的顶部，那么我们将把元素推到堆栈中。

2.  一旦我们在输入队列中找到一个元素，使得输入队列的顶部等于输出队列的顶部，我们将从输入和输出队列中弹出一个元素，现在比较堆栈的顶部和输出队列的顶部。如果堆栈和输出队列的顶部相等，则从堆栈和输出队列中弹出元素。如果不相等，请转到步骤 1。

3.  重复以上两个步骤，直到输入队列变空。最后，如果输入队列和堆栈都是空的，那么输入队列是可置换的，否则不是。

以下是上述想法的实现:

## C++

```
// Given two arrays, check if one array is
// stack permutation of other.
#include<bits/stdc++.h>
using namespace std;

// function to check if input queue is
// permutable to output queue
bool checkStackPermutation(int ip[], int op[], int n)
{
    // Input queue
    queue<int> input;
    for (int i=0;i<n;i++)
        input.push(ip[i]);

    // output queue
    queue<int> output;
    for (int i=0;i<n;i++)
        output.push(op[i]);

    // stack to be used for permutation
    stack <int> tempStack;
    while (!input.empty())
    {
        int ele = input.front();
        input.pop();
        if (ele == output.front())
        {
            output.pop();
            while (!tempStack.empty())
            {
                if (tempStack.top() == output.front())
                {
                    tempStack.pop();
                    output.pop();
                }
                else
                    break;
            }
        }
        else
            tempStack.push(ele);
    }

    // If after processing, both input queue and
    // stack are empty then the input queue is
    // permutable otherwise not.
    return (input.empty()&&tempStack.empty());
}

// Driver program to test above function
int main()
{
    // Input Queue
    int input[] = {1, 2, 3};

    // Output Queue
    int output[] = {2, 1, 3};

    int n = 3;

    if (checkStackPermutation(input, output, n))
        cout << "Yes";
    else
        cout << "Not Possible";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Given two arrays, check if one array is
// stack permutation of other.
import java.util.LinkedList;
import java.util.Queue;
import java.util.Stack;

class Gfg
{
    // function to check if input queue is
    // permutable to output queue
    static boolean checkStackPermutation(int ip[],
                                    int op[], int n)
    {
        Queue<Integer> input = new LinkedList<>();

        // Input queue
        for (int i = 0; i < n; i++)
        {
            input.add(ip[i]);
        }

        // Output queue
        Queue<Integer> output = new LinkedList<>();
        for (int i = 0; i < n; i++)
        {
            output.add(op[i]);
        }

        // stack to be used for permutation
        Stack<Integer> tempStack = new Stack<>();
        while (!input.isEmpty())
        {
            int ele = input.poll();

            if (ele == output.peek())
            {
                output.poll();
                while (!tempStack.isEmpty())
                {
                    if (tempStack.peek() == output.peek())
                    {
                        tempStack.pop();
                        output.poll();
                    }
                    else
                        break;
                }
            }
            else
            {
                tempStack.push(ele);
            }
        }

        // If after processing, both input queue and
        // stack are empty then the input queue is
        // permutable otherwise not.
        return (input.isEmpty() && tempStack.isEmpty());
    }

    // Driver code
    public static void main(String[] args)
    {
        // Input Queue
        int input[] = { 1, 2, 3 };

        // Output Queue
        int output[] = { 2, 1, 3 };
        int n = 3;
        if (checkStackPermutation(input, output, n))
            System.out.println("Yes");
        else
            System.out.println("Not Possible");
    }
}

// This code is contributed by Vivekkumar Singh
```

## 蟒蛇 3

```
# Given two arrays, check if one array is
# stack permutation of other.
from queue import Queue

# function to check if Input queue
# is permutable to output queue
def checkStackPermutation(ip, op, n):

    # Input queue
    Input = Queue()
    for i in range(n):
        Input.put(ip[i])

    # output queue
    output = Queue()
    for i in range(n):
        output.put(op[i])

    # stack to be used for permutation
    tempStack = []
    while (not Input.empty()):
        ele = Input.queue[0]
        Input.get()
        if (ele == output.queue[0]):
            output.get()
            while (len(tempStack) != 0):
                if (tempStack[-1] == output.queue[0]):
                    tempStack.pop()
                    output.get()
                else:
                    break
        else:
            tempStack.append(ele)

    # If after processing, both Input
    # queue and stack are empty then 
    # the Input queue is permutable
    # otherwise not.
    return (Input.empty() and
        len(tempStack) == 0)

# Driver Code
if __name__ == '__main__':

    # Input Queue
    Input = [1, 2, 3]

    # Output Queue
    output = [2, 1, 3]

    n = 3

    if (checkStackPermutation(Input,
                              output, n)):
        print("Yes")
    else:
        print("Not Possible")

# This code is contributed by PranchalK
```

## C#

```
// Given two arrays, check if one array is
// stack permutation of other.
using System;
using System.Collections.Generic;

class GFG
{
    // function to check if input queue is
    // permutable to output queue
    static bool checkStackPermutation(int []ip,
                                      int []op, int n)
    {
        Queue<int> input = new Queue<int>();

        // Input queue
        for (int i = 0; i < n; i++)
        {
            input.Enqueue(ip[i]);
        }

        // Output queue
        Queue<int> output = new Queue<int>();
        for (int i = 0; i < n; i++)
        {
            output.Enqueue(op[i]);
        }

        // stack to be used for permutation
        Stack<int> tempStack = new Stack<int>();
        while (input.Count != 0)
        {
            int ele = input.Dequeue();

            if (ele == output.Peek())
            {
                output.Dequeue();
                while (tempStack.Count != 0)
                {
                    if (tempStack.Peek() == output.Peek())
                    {
                        tempStack.Pop();
                        output.Dequeue();
                    }
                    else
                        break;
                }
            }
            else
            {
                tempStack.Push(ele);
            }
        }

        // If after processing, both input queue and
        // stack are empty then the input queue is
        // permutable otherwise not.
        return (input.Count == 0 && tempStack.Count == 0);
    }

    // Driver code
    public static void Main(String[] args)
    {
        // Input Queue
        int []input = { 1, 2, 3 };

        // Output Queue
        int []output = { 2, 1, 3 };
        int n = 3;
        if (checkStackPermutation(input, output, n))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("Not Possible");
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
    // Given two arrays, check if one array is
    // stack permutation of other.

    // function to check if input queue is
    // permutable to output queue
    function checkStackPermutation(ip, op, n)
    {
        let input = [];

        // Input queue
        for (let i = 0; i < n; i++)
        {
            input.push(ip[i]);
        }

        // Output queue
        let output = [];
        for (let i = 0; i < n; i++)
        {
            output.push(op[i]);
        }

        // stack to be used for permutation
        let tempStack = [];
        while (input.length != 0)
        {
            let ele = input.shift();

            if (ele == output[0])
            {
                output.shift();
                while (tempStack.length != 0)
                {
                    if (tempStack[tempStack.length - 1] == output[0])
                    {
                        tempStack.pop();
                        output.shift();
                    }
                    else
                        break;
                }
            }
            else
            {
                tempStack.push(ele);
            }
        }

        // If after processing, both input queue and
        // stack are empty then the input queue is
        // permutable otherwise not.
        return (input.length == 0 && tempStack.length == 0);
    }

    // Input Queue
    let input = [ 1, 2, 3 ];

    // Output Queue
    let output = [ 2, 1, 3 ];
    let n = 3;
    if (checkStackPermutation(input, output, n))
      document.write("Yes");
    else
      document.write("Not Possible");

    // This code is contributed by rameshtravel07.
</script>
```

**输出:**

```
Yes
```

本文由**掌门人 Dey** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。