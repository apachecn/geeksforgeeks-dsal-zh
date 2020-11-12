# 下一个更高的频率元素

> 原文：[https://www.geeksforgeeks.org/next-greater-frequency-element/](https://www.geeksforgeeks.org/next-greater-frequency-element/)

给定一个数组，对于每个元素，找到最右边的元素的值，该元素的频率大于当前元素的频率。 如果不存在职位的答案，则将值设为`-1`。

**示例**：

```
Input : a[] = [1, 1, 2, 3, 4, 2, 1] 
Output : [-1, -1, 1, 2, 2, 1, -1]
Explanation:
Given array a[] = [1, 1, 2, 3, 4, 2, 1] 
Frequency of each element is: 3, 3, 2, 1, 1, 2, 3
Lets calls Next Greater Frequency element as NGF
1\. For element a[0] = 1 which has a frequency = 3,
   As it has frequency of 3 and no other next element 
   has frequency more than 3 so  '-1'
2\. For element a[1] = 1 it will be -1 same logic 
   like a[0]
3\. For element a[2] = 2 which has frequency = 2,
   NGF element is 1 at position = 6  with frequency 
   of 3 > 2
4\. For element a[3] = 3 which has frequency = 1,
   NGF element is 2 at position = 5 with frequency 
   of 2 > 1
5\. For element a[4] = 4 which has frequency = 1,
   NGF element is 2 at position = 5 with frequency 
   of 2 > 1
6\. For element a[5] = 2 which has frequency = 2,
   NGF element is 1 at position = 6 with frequency
   of 3 > 2
7\. For element a[6] = 1 there is no element to its 
   right, hence -1 

Input : a[] = [1, 1, 1, 2, 2, 2, 2, 11, 3, 3]
Output : [2, 2, 2, -1, -1, -1, -1, 3, -1, -1]

```

**朴素的方法**：

一种简单的哈希技术是使用值，因为使用索引来存储每个元素的频率。 假设创建一个列表，以存储数组中每个数字的频率。 （需要单遍历）。 现在使用两个循环。

外循环一个接一个地拾取所有元素。

内循环查找其频率大于当前元素频率的第一个元素。

如果找到频率更高的元素，则将打印该元素，否则将打印 -1。

**时间复杂度**：`O(n * n)`

**高效方法**：

我们可以使用哈希和栈数据结构来有效解决许多情况。 一种简单的哈希技术是将值用作索引，将每个元素的频率用作值。 我们使用栈数据结构来存储元素在数组中的位置。

1.  创建一个列表，使用值作为索引来存储每个元素的频率。
1.  将第一个元素的位置压入栈。
1.  逐个拾取其余元素的位置，然后循环执行以下步骤。
    1.  将当前元素的位置标记为`i`。
    1.  如果栈顶部指向的元素的频率比当前元素的频率高，则将当前位置`i`推入栈
    1.  如果栈顶部指向的元素的频率比当前元素的频率小，并且栈不为空，则请执行以下步骤：
        1.  继续弹出栈
        1.  如果步骤`c`中的条件失败，则将当前位置`i`推入栈。
1.  步骤 3 中的循环结束后，从栈中弹出所有元素 并将 -1 打印，因为不存在下一个更高频率元素。

下面是上述问题的实现。

## C++

```cpp

// C++ program of Next Greater Frequency Element
#include <iostream>
#include <stack>
#include <stdio.h>

using namespace std;

/*NFG function to find the next greater frequency
element for each element in the array*/
void NFG(int a[], int n, int freq[])
{

    // stack data structure to store the position
    // of array element
    stack<int> s;
    s.push(0);

    // res to store the value of next greater
    // frequency element for each element
    int res[n] = { 0 };
    for (int i = 1; i < n; i++) {
        /* If the frequency of the element which is
            pointed by the top of stack is greater
            than frequency of the current element
            then push the current position i in stack*/

        if (freq[a[s.top()]] > freq[a[i]])
            s.push(i);
        else {
            /*If the frequency of the element which
            is pointed by the top of stack is less
            than frequency of the current element, then
            pop the stack and continuing popping until
            the above condition is true while the stack
            is not empty*/

            while (freq[a[s.top()]] < freq[a[i]]
                   && !s.empty()) {

                res[s.top()] = a[i];
                s.pop();
            }
            //  now push the current element
            s.push(i);
        }
    }

    while (!s.empty()) {
        res[s.top()] = -1;
        s.pop();
    }
    for (int i = 0; i < n; i++) {
        // Print the res list containing next
        // greater frequency element
        cout << res[i] << " ";
    }
}

// Driver code
int main()
{

    int a[] = { 1, 1, 2, 3, 4, 2, 1 };
    int len = 7;
    int max = INT16_MIN;
    for (int i = 0; i < len; i++) {
        // Getting the max element of the array
        if (a[i] > max) {
            max = a[i];
        }
    }
    int freq[max + 1] = { 0 };

    // Calculating frequency of each element
    for (int i = 0; i < len; i++) {
        freq[a[i]]++;
    }

    // Function call
    NFG(a, len, freq);
    return 0;
}

```

## Java

```java

// Java program of Next Greater Frequency Element
import java.util.*;

class GFG {

    /*NFG function to find the next greater frequency
    element for each element in the array*/
    static void NFG(int a[], int n, int freq[])
    {

        // stack data structure to store the position
        // of array element
        Stack<Integer> s = new Stack<Integer>();
        s.push(0);

        // res to store the value of next greater
        // frequency element for each element
        int res[] = new int[n];
        for (int i = 0; i < n; i++)
            res[i] = 0;

        for (int i = 1; i < n; i++) {
            /* If the frequency of the element which is
                pointed by the top of stack is greater
                than frequency of the current element
                then push the current position i in stack*/

            if (freq[a[s.peek()]] > freq[a[i]])
                s.push(i);
            else {
                /*If the frequency of the element which
                is pointed by the top of stack is less
                than frequency of the current element, then
                pop the stack and continuing popping until
                the above condition is true while the stack
                is not empty*/

                while (freq[a[s.peek()]] < freq[a[i]]
                       && s.size() > 0) {
                    res[s.peek()] = a[i];
                    s.pop();
                }

                // now push the current element
                s.push(i);
            }
        }

        while (s.size() > 0) {
            res[s.peek()] = -1;
            s.pop();
        }

        for (int i = 0; i < n; i++) {
            // Print the res list containing next
            // greater frequency element
            System.out.print(res[i] + " ");
        }
    }

    // Driver code
    public static void main(String args[])
    {

        int a[] = { 1, 1, 2, 3, 4, 2, 1 };
        int len = 7;
        int max = Integer.MIN_VALUE;
        for (int i = 0; i < len; i++) {
            // Getting the max element of the array
            if (a[i] > max) {
                max = a[i];
            }
        }
        int freq[] = new int[max + 1];

        for (int i = 0; i < max + 1; i++)
            freq[i] = 0;

        // Calculating frequency of each element
        for (int i = 0; i < len; i++) {
            freq[a[i]]++;
        }
        // Function call
        NFG(a, len, freq);
    }
}

// This code is contributed by Arnab Kundu

```

## Python3

```py

'''NFG function to find the next greater frequency
   element for each element in the array'''

def NFG(a, n):

    if (n <= 0):
        print("List empty")
        return []

    # stack data structure to store the position
    # of array element
    stack = [0]*n

    # freq is a dictionary which maintains the
    # frequency of each element
    freq = {}
    for i in a:
        freq[a[i]] = 0
    for i in a:
        freq[a[i]] += 1

    # res to store the value of next greater
    # frequency element for each element
    res = [0]*n

    # initialize top of stack to -1
    top = -1

    # push the first position of array in the stack
    top += 1
    stack[top] = 0

    # now iterate for the rest of elements
    for i in range(1, n):

        ''' If the frequency of the element which is 
            pointed by the top of stack is greater 
            than frequency of the current element
            then push the current position i in stack'''
        if (freq[a[stack[top]]] > freq[a[i]]):
            top += 1
            stack[top] = i

        else:
            ''' If the frequency of the element which 
            is pointed by the top of stack is less 
            than frequency of the current element, then 
            pop the stack and continuing popping until 
            the above condition is true while the stack
            is not empty'''

            while (top > -1 and freq[a[stack[top]]] < freq[a[i]]):
                res[stack[top]] = a[i]
                top -= 1

            # now push the current element
            top += 1
            stack[top] = i

    '''After iterating over the loop, the remaining
    position of elements in stack do not have the 
    next greater element, so print -1 for them'''
    while (top > -1):
        res[stack[top]] = -1
        top -= 1

    # return the res list containing next
    # greater frequency element
    return res

# Driver Code
print(NFG([1, 1, 2, 3, 4, 2, 1], 7))

```

## C#

```cs

// C# program of Next Greater Frequency Element
using System;
using System.Collections;

class GFG {

    /*NFG function to find the
    next greater frequency
    element for each element
    in the array*/
    static void NFG(int[] a, int n, int[] freq)
    {

        // stack data structure to store
        // the position of array element
        Stack s = new Stack();
        s.Push(0);

        // res to store the value of next greater
        // frequency element for each element
        int[] res = new int[n];
        for (int i = 0; i < n; i++)
            res[i] = 0;

        for (int i = 1; i < n; i++) {
            /* If the frequency of the element which is
                pointed by the top of stack is greater
                than frequency of the current element
                then Push the current position i in stack*/

            if (freq[a[(int)s.Peek()]] > freq[a[i]])
                s.Push(i);
            else {
                /*If the frequency of the element which
                is pointed by the top of stack is less
                than frequency of the current element, then
                Pop the stack and continuing Popping until
                the above condition is true while the stack
                is not empty*/

                while (freq[a[(int)(int)s.Peek()]]
                           < freq[a[i]]
                       && s.Count > 0) {
                    res[(int)s.Peek()] = a[i];
                    s.Pop();
                }

                // now Push the current element
                s.Push(i);
            }
        }

        while (s.Count > 0) {
            res[(int)s.Peek()] = -1;
            s.Pop();
        }

        for (int i = 0; i < n; i++) {

            // Print the res list containing next
            // greater frequency element
            Console.Write(res[i] + " ");
        }
    }

    // Driver code
    public static void Main(String[] args)
    {

        int[] a = { 1, 1, 2, 3, 4, 2, 1 };
        int len = 7;
        int max = int.MinValue;
        for (int i = 0; i < len; i++) {
            // Getting the max element of the array
            if (a[i] > max) {
                max = a[i];
            }
        }
        int[] freq = new int[max + 1];

        for (int i = 0; i < max + 1; i++)
            freq[i] = 0;

        // Calculating frequency of each element
        for (int i = 0; i < len; i++) {
            freq[a[i]]++;
        }
        NFG(a, len, freq);
    }
}

// This code is contributed by Arnab Kundu

```

**输出**：

```
[-1, -1, 1, 2, 2, 1, -1]

```

**时间复杂度**：`O(n)`。

本文由 **Sruti Rai** 提供。 感谢 [Koustav](https://www.facebook.com/ironDEvil) 的宝贵支持。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的内容，或者想分享有关上述主题的更多信息，请发表评论。

