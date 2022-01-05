# 打印下一个更大数量的 Q 查询

> 原文:[https://www . geesforgeks . org/print-next-better-number-q-query/](https://www.geeksforgeeks.org/print-next-greater-number-q-queries/)

给定 n 个元素和 q 个查询的数组，对于每个有索引 I 的查询，找到下一个更大的元素并打印它的值。如果它的右边没有更大的元素，那么打印-1。
**例:**

```
Input : arr[] = {3, 4, 2, 7, 5, 8, 10, 6} 
        query indexes = {3, 6, 1}
Output: 8 -1 7 
Explanation : 
For the 1st query index is 3, element is 7 and 
the next greater element at its right is 8 

For the 2nd query index is 6, element is 10 and 
there is no element greater then 10 at right, 
so print -1.

For the 3rd query index is 1, element is 4 and
the next greater element at its right is 7.
```

**Normal Approach:** 一个正常的方法是让每个查询在一个循环中从 index 移动到 n，找出下一个更大的元素并打印出来，但在最坏的情况下，这将需要 n 次迭代，如果查询数量很高，这将是一个很大的循环。
时间复杂度:O(n^2)
辅助空间> : O(1)
**高效进场:**
高效进场基于[下一个更大的元素](https://www.geeksforgeeks.org/next-greater-element/)。我们将下一个较大元素的索引存储在数组中，对于每个查询过程，在 **O(1)** 中回答查询，这将使其更高效。
但是要找出数组中每个索引的下一个更大的元素，有两种方法。
取 **o(n^2)** 和 **O(n)** 空间，对索引 I 处的每个元素从 I+1 迭代到 n，找出 ext greater 元素并存储。
但是更有效的方法是使用 stack，我们使用索引来比较并存储在 next[]下一个更大的元素索引中。
1)将第一个索引推入堆栈。
2)逐个选择其余索引，并循环执行以下步骤。
……。a)将当前元素标记为 i.
…。b)如果堆栈不为空，则从堆栈中弹出一个索引，并将一个[索引]与一个[I]进行比较。
…。c)如果 a[I]大于 a[索引]，则 a[I]是 a[索引]的下一个更大的元素。
…。d)当弹出的索引元素小于 1 时，继续从堆栈中弹出。a[I]成为所有此类弹出元素的下一个更大的元素
…。g)如果一个[I]小于弹出的索引元素，则将弹出的索引推回。
3)步骤 2 中的循环结束后，从堆栈中弹出所有索引，并打印-1 作为它们的下一个索引。

## C++

```
// C++ program to print
// next greater number
// of Q queries
#include <bits/stdc++.h>
using namespace std;

// array to store the next
// greater element index
void next_greatest(int next[],
                   int a[], int n)
{
    // use of stl
    // stack in c++
    stack<int> s;

    // push the 0th
    // index to the stack
    s.push(0);

    // traverse in the
    // loop from 1-nth index
    for (int i = 1; i < n; i++)
    {

        // iterate till loop is empty
        while (!s.empty()) {

            // get the topmost
            // index in the stack
            int cur = s.top();

            // if the current element is 
            // greater then the top indexth
            // element, then this will be
            // the next greatest index
            // of the top indexth element
            if (a[cur] < a[i])
            {

                // initialise the cur
                // index position's
                // next greatest as index
                next[cur] = i;

                // pop the cur index
                // as its greater
                // element has been found
                s.pop();
            }

            // if not greater
            // then break
            else
                break;
        }
        // push the i index so that its
        // next greatest can be found
        s.push(i);
    }

    // iterate for all other
    // index left inside stack
    while (!s.empty())
    {
        int cur = s.top();

        // mark it as -1 as no
        // element in greater
        // then it in right
        next[cur] = -1;

        s.pop();
    }
}

// answers all
// queries in O(1)
int answer_query(int a[], int next[],
                 int n, int index)
{
    // stores the next greater
    // element positions
    int position = next[index];

    // if position is -1 then no
    // greater element is at right.
    if (position == -1)
        return -1;

    // if there is a index that
    // has greater element
    // at right then return its
    // value as a[position]
    else
        return a[position];
}

// Driver Code
int main()
{

    int a[] = {3, 4, 2, 7,
               5, 8, 10, 6 };

    int n = sizeof(a) / sizeof(a[0]);

    // initializes the
    // next array as 0
    int next[n] = { 0 };

    // calls the function
    // to pre-calculate
    // the next greatest
    // element indexes
    next_greatest(next, a, n);

    // query 1 answered
    cout << answer_query(a, next, n, 3) << " ";

    // query 2 answered
    cout << answer_query(a, next, n, 6) << " ";

    // query 3 answered
    cout << answer_query(a, next, n, 1) << " ";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print
// next greater number
// of Q queries
import java.util.*;

class GFG
{
public static int[] query(int arr[],
                          int query[])
{
    int ans[] = new int[arr.length];// this array contains
                                    // the next greatest
                                    // elements of all the elements
    Stack<Integer> s = new Stack<>();
    // push the 0th index
    // to the stack
    s.push(arr[0]);
    int j = 0;
    //traverse rest
    // of the array
    for(int i = 1; i < arr.length; i++)
    {
        int next = arr[i];

        if(!s.isEmpty())
        {
            // get the topmost
            // element in the stack
            int element = s.pop();

            /* If the popped element
            is smaller than next,
            then a) store the pair
            b) keep popping while
            elements are smaller and
            stack is not empty */
            while(next > element)
            {
                ans[j] = next;
                j++;
                if(s.isEmpty())
                    break;
                element = s.pop();
            }

            /* If element is greater
            than next, then
            push the element back */
            if (element > next)
                s.push(element);
        }
        /* push next to stack so
        that we can find next
        greater for it */
        s.push(next);
    }
    /* After iterating over the
    loop, the remaining elements
    in stack do not have the next
    greater element, so -1 for them */
    while(!s.isEmpty())
    {
        int element = s.pop();
        ans[j] = -1;
        j++;
    }

    // return the next
    // greatest array
    return ans;
}

// Driver Code   
public static void main(String[] args)
{
    int arr[] = {3, 4, 2, 7,
                 5, 8, 10, 6};
    int query[] = {3, 6, 1};
    int ans[] = query(arr,query);

    // getting output array
    // with next greatest elements
    for(int i = 0; i < query.length; i++)
    {
        // displaying the next greater
        // element for given set of queries
        System.out.print(ans[query[i]] + " ");
    }
}
}

// This code was contributed
// by Harshit Sood
```

## 蟒蛇 3

```
# Python3 program to print
# next greater number
# of Q queries

# array to store the next
# greater element index
def next_greatest(next, a, n):

    # use of stl
    # stack in c++
    s = []

    # push the 0th
    # index to the stack
    s.append(0);

    # traverse in the
    # loop from 1-nth index
    for  i in range(1, n):

        # iterate till loop is empty
        while (len(s) != 0):

            # get the topmost
            # index in the stack
            cur = s[-1]

            # if the current element is 
            # greater then the top indexth
            # element, then this will be
            # the next greatest index
            # of the top indexth element
            if (a[cur] < a[i]):

                # initialise the cur
                # index position's
                # next greatest as index
                next[cur] = i;

                # pop the cur index
                # as its greater
                # element has been found
                s.pop();

            # if not greater
            # then break
            else:
                break;

        # push the i index so that its
        # next greatest can be found
        s.append(i);

    # iterate for all other
    # index left inside stack
    while(len(s) != 0):
        cur = s[-1]

        # mark it as -1 as no
        # element in greater
        # then it in right
        next[cur] = -1;
        s.pop();

# answers all
# queries in O(1)
def answer_query(a, next, n, index):

    # stores the next greater
    # element positions
    position = next[index];

    # if position is -1 then no
    # greater element is at right.
    if(position == -1):
        return -1;

    # if there is a index that
    # has greater element
    # at right then return its
    # value as a[position]
    else:
        return a[position];

# Driver Code
if __name__=='__main__':

    a = [3, 4, 2, 7, 5, 8, 10, 6 ]
    n = len(a)

    # initializes the
    # next array as 0
    next=[0 for i in range(n)]

    # calls the function
    # to pre-calculate
    # the next greatest
    # element indexes
    next_greatest(next, a, n);

    # query 1 answered
    print(answer_query(a, next, n, 3), end = ' ')

    # query 2 answered
    print(answer_query(a, next, n, 6), end = ' ')

    # query 3 answered
    print(answer_query(a, next, n, 1), end = ' ')

# This code is contributed by rutvik_56.
```

## C#

```
// C# program to print next greater
// number of Q queries
using System;
using System.Collections.Generic;

class GFG
{
public static int[] query(int[] arr,
                          int[] query)
{
    int[] ans = new int[arr.Length]; // this array contains
                                     // the next greatest
                                     // elements of all the elements
    Stack<int> s = new Stack<int>();

    // push the 0th index to the stack
    s.Push(arr[0]);
    int j = 0;

    // traverse rest of the array
    for (int i = 1; i < arr.Length; i++)
    {
        int next = arr[i];

        if (s.Count > 0)
        {
            // get the topmost element in the stack
            int element = s.Pop();

            /* If the popped element is smaller
            than next, then
            a) store the pair
            b) keep popping while
            elements are smaller and
            stack is not empty */
            while (next > element)
            {
                ans[j] = next;
                j++;
                if (s.Count == 0)
                {
                    break;
                }
                element = s.Pop();
            }

            /* If element is greater
            than next, then
            push the element back */
            if (element > next)
            {
                s.Push(element);
            }
        }
        /* push next to stack so that we
        can find next greater for it */
        s.Push(next);
    }

    /* After iterating over the
    loop, the remaining elements
    in stack do not have the next
    greater element, so -1 for them */
    while (s.Count > 0)
    {
        int element = s.Pop();
        ans[j] = -1;
        j++;
    }

    // return the next greatest array
    return ans;
}

// Driver Code    
public static void Main(string[] args)
{
    int[] arr = new int[] {3, 4, 2, 7, 5, 8, 10, 6};
    int[] query = new int[] {3, 6, 1};
    int[] ans = GFG.query(arr, query);

    // getting output array
    // with next greatest elements
    for (int i = 0; i < query.Length; i++)
    {
        // displaying the next greater
        // element for given set of queries
        Console.Write(ans[query[i]] + " ");
    }
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// JavaScript program to print
// next greater number
// of Q queries

// array to store the next
// greater element index
function next_greatest(next, a, n)
{
    // use of stl
    // stack in c++
    var s = [];

    // push the 0th
    // index to the stack
    s.push(0);

    // traverse in the
    // loop from 1-nth index
    for (var i = 1; i < n; i++)
    {

        // iterate till loop is empty
        while (s.length!=0) {

            // get the topmost
            // index in the stack
            var cur = s[s.length-1];

            // if the current element is 
            // greater then the top indexth
            // element, then this will be
            // the next greatest index
            // of the top indexth element
            if (a[cur] < a[i])
            {

                // initialise the cur
                // index position's
                // next greatest as index
                next[cur] = i;

                // pop the cur index
                // as its greater
                // element has been found
                s.pop();
            }

            // if not greater
            // then break
            else
                break;
        }
        // push the i index so that its
        // next greatest can be found
        s.push(i);
    }

    // iterate for all other
    // index left inside stack
    while (s.length!=0)
    {
        var cur = s[s.length-1];

        // mark it as -1 as no
        // element in greater
        // then it in right
        next[cur] = -1;

        s.pop();
    }
}

// answers all
// queries in O(1)
function answer_query(a, next, n, index)
{
    // stores the next greater
    // element positions
    var position = next[index];

    // if position is -1 then no
    // greater element is at right.
    if (position == -1)
        return -1;

    // if there is a index that
    // has greater element
    // at right then return its
    // value as a[position]
    else
        return a[position];
}

// Driver Code
var a = [3, 4, 2, 7,
           5, 8, 10, 6];
var n = a.length;
// initializes the
// next array as 0
var next = Array(n).fill(0);
// calls the function
// to pre-calculate
// the next greatest
// element indexes
next_greatest(next, a, n);
// query 1 answered
document.write( answer_query(a, next, n, 3) + " ");
// query 2 answered
document.write( answer_query(a, next, n, 6) + " ");
// query 3 answered
document.write( answer_query(a, next, n, 1) + " ");

</script>
```

**输出:**

```
8 -1 7 
```

**时间复杂度:**最大(O(n)，O(q))，O(n)用于预处理下一个[]数组，O(1)用于每个查询。
**辅助空间:** O(n)
本文由[**Raja vikramatitya(Raj)**](https://www.facebook.com/raja.vikramaditya.7)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。