# 右侧的 NGE 数量

> 原文：[https://www.geeksforgeeks.org/number-nges-right/](https://www.geeksforgeeks.org/number-nges-right/)



给定`n`个整数数组和`q`个查询，打印给定索引元素的右边的[下一个更大元素](https://www.geeksforgeeks.org/next-greater-element/)的数量。

**示例**：

```
Input: a[] = {3, 4, 2, 7, 5, 8, 10, 6}  
              q = 2 
              index = 0, 
              index = 5
Output: 6
        1 
Explanation:
The next greater elements
to the right of 3(index 0) are 4,7,5,8,10,6\. 
The next greater elements to the right
of 8(index 5) are 10.

```

**朴素的方法**是针对从索引到结尾的每个查询进行迭代，并找出右边的下一个更大元素的数量。 由于我们运行了两个嵌套循环，因此效率不够高。

**时间复杂度**：`O(n)`回答查询。

**辅助空间**：`O(1)`。

**更好的方法**是存储每个元素的下一个更大的索引，并对从索引迭代的每个查询运行循环，并将递增计数器保持为`j = next[i]`。 这将避免检查所有元素，并将直接跳转到每个元素的下一个更大的元素。 但这在`1 2 3 4 5 6`之类的情况下效率不高，在此情况下，下一个更大的元素依次增加，最终导致每个查询取`O(n)`。

**时间复杂度**：`O(n)`回答查询。

**辅助空间**：`O(n)`用于下一个更大的元素。

**高效方法**是使用`next[]`数组中的下一个更大元素存储下一个更大元素的索引。 然后创建一个从`n-2`开始的`dp[]`数组，因为第`n-1`个索引的右边将没有元素，并且`dp[n-1] = 0`。从后向遍历时，我们使用动态规划来计算右边的元素数，我们将记忆作为`dp[next[i]]`使用，它使我们可以对当前元素的下一个更大元素的右边的数字进行计数，因此我们对其加 1。 如果`next[i] = -1`，那么我们右边没有任何元素，因此`dp[i] = 0`。 `dp[index]`存储右边的下一个更大元素的数量计数。

下面是上述方法的实现。

## C++

```cpp

#include <bits/stdc++.h>
using namespace std;

// array to store the next greater element index
void fillNext(int next[], int a[], int n)
{
    // use of stl stack in c++
    stack<int> s;

    // push the 0th index to the stack
    s.push(0);

    // traverse in the loop from 1-nth index
    for (int i = 1; i < n; i++) {

        // iterate till loop is empty
        while (!s.empty()) {

            // get the topmost index in the stack
            int cur = s.top();

            // if the current element is greater
            // then the top index-th element, then
            // this will be the next greatest index
            // of the top index-th element
            if (a[cur] < a[i]) {

                // initialize the cur index position's
                // next greatest as index
                next[cur] = i;

                // pop the cur index as its greater
                // element has been found
                s.pop();
            }

            // if not greater then break
            else
                break;
        }

        // push the i index so that its next greatest
        // can be found
        s.push(i);
    }

    // iterate for all other index left inside stack
    while (!s.empty()) {

        int cur = s.top();

        // mark it as -1 as no element in greater
        // then it in right
        next[cur] = -1;

        s.pop();
    }
}

// Function to count the number of 
// next greater numbers to the right
void count(int a[], int dp[], int n)
{
    // initializes the next array as 0
    int next[n];
    memset(next, 0, sizeof(next));

    // calls the function to pre-calculate
    // the next greatest element indexes
    fillNext(next, a, n);

    for (int i = n - 2; i >= 0; i--) {

        // if the i-th element has no next
        // greater element to right
        if (next[i] == -1)
            dp[i] = 0;

        // Count of next greater numbers to right.
        else
            dp[i] = 1 + dp[next[i]];
    }
}

// answers all queries in O(1)
int answerQuery(int dp[], int index)
{
    // returns the number of next greater
    // elements to the right.
    return dp[index];
}

// driver program to test the above function
int main()
{
    int a[] = { 3, 4, 2, 7, 5, 8, 10, 6 };
    int n = sizeof(a) / sizeof(a[0]);

    int dp[n];

    // calls the function to count the number
    // of greater elements to the right for
    // every element.
    count(a, dp, n);

    // query 1 answered
    cout << answerQuery(dp, 3) << endl;

    // query 2 answered
    cout << answerQuery(dp, 6) << endl;

    // query 3 answered
    cout << answerQuery(dp, 1) << endl;

    return 0;
}

```

## Java

```java

// Java program to print number of NGEs to the right
import java.util.*;

class GFG
{

// array to store the next greater element index
static void fillNext(int next[], int a[], int n)
{
    // Use stack
    Stack<Integer> s = new Stack<Integer>();

    // push the 0th index to the stack
    s.push(0);

    // traverse in the loop from 1-nth index
    for (int i = 1; i < n; i++) 
    {

        // iterate till loop is empty
        while (s.size() > 0) 
        {

            // get the topmost index in the stack
            int cur = s.peek();

            // if the current element is greater
            // then the top index-th element, then
            // this will be the next greatest index
            // of the top index-th element
            if (a[cur] < a[i])
            {

                // initialize the cur index position's
                // next greatest as index
                next[cur] = i;

                // pop the cur index as its greater
                // element has been found
                s.pop();
            }

            // if not greater then break
            else
                break;
        }

        // push the i index so that its next greatest
        // can be found
        s.push(i);
    }

    // iterate for all other index left inside stack
    while (s.size() > 0) 
    {

        int cur = s.peek();

        // mark it as -1 as no element in greater
        // then it in right
        next[cur] = -1;

        s.pop();
    }
}

// function to count the number of 
// next greater numbers to the right
static void count(int a[], int dp[], int n)
{
    // initializes the next array as 0
    int next[] = new int[n];
    for(int i = 0; i < n; i++)
    next[i] = 0;

    // calls the function to pre-calculate
    // the next greatest element indexes
    fillNext(next, a, n);

    for (int i = n - 2; i >= 0; i--) 
    {

        // if the i-th element has no next
        // greater element to right
        if (next[i] == -1)
            dp[i] = 0;

        // Count of next greater numbers to right.
        else
            dp[i] = 1 + dp[next[i]];
    }
}

// answers all queries in O(1)
static int answerQuery(int dp[], int index)
{
    // returns the number of next greater
    // elements to the right.
    return dp[index];
}

// driver code
public static void main(String args[])
{
    int a[] = { 3, 4, 2, 7, 5, 8, 10, 6 };
    int n = a.length;

    int dp[] = new int[n];

    // calls the function to count the number
    // of greater elements to the right for
    // every element.
    count(a, dp, n);

    // query 1 answered
    System.out.println(answerQuery(dp, 3));

    // query 2 answered
    System.out.println( answerQuery(dp, 6));

    // query 3 answered
    System.out.println( answerQuery(dp, 1) );

}
}

// This code is contributed by Arnab Kundu

```

## C#

```cs

// C# program to print number of 
// NGEs to the right
using System;
using System.Collections;

class GFG
{

// array to store the next greater element index
static void fillNext(int []next, int []a, int n)
{
    // Use stack
    Stack s = new Stack();

    // Push the 0th index to the stack
    s.Push(0);

    // traverse in the loop from 1-nth index
    for (int i = 1; i < n; i++) 
    {

        // iterate till loop is empty
        while (s.Count > 0) 
        {

            // get the topmost index in the stack
            int cur = (int)s.Peek();

            // if the current element is greater
            // then the top index-th element, then
            // this will be the next greatest index
            // of the top index-th element
            if (a[cur] < a[i])
            {

                // initialize the cur index position's
                // next greatest as index
                next[cur] = i;

                // Pop the cur index as its greater
                // element has been found
                s.Pop();
            }

            // if not greater then break
            else
                break;
        }

        // Push the i index so that its next 
        // greatest can be found
        s.Push(i);
    }

    // iterate for all other index 
    // left inside stack
    while (s.Count > 0) 
    {

        int cur =(int) s.Peek();

        // mark it as -1 as no element in 
        // greater then it in right
        next[cur] = -1;

        s.Pop();
    }
}

// function to count the number of 
// next greater numbers to the right
static void count(int []a, int []dp, int n)
{
    // initializes the next array as 0
    int []next = new int[n];
    for(int i = 0; i < n; i++)
        next[i] = 0;

    // calls the function to pre-calculate
    // the next greatest element indexes
    fillNext(next, a, n);

    for (int i = n - 2; i >= 0; i--) 
    {

        // if the i-th element has no next
        // greater element to right
        if (next[i] == -1)
            dp[i] = 0;

        // Count of next greater numbers to right.
        else
            dp[i] = 1 + dp[next[i]];
    }
}

// answers all queries in O(1)
static int answerQuery(int []dp, int index)
{
    // returns the number of next greater
    // elements to the right.
    return dp[index];
}

// Driver code
public static void Main(String []args)
{
    int []a = { 3, 4, 2, 7, 5, 8, 10, 6 };
    int n = a.Length;

    int []dp = new int[n];

    // calls the function to count the number
    // of greater elements to the right for
    // every element.
    count(a, dp, n);

    // query 1 answered
    Console.WriteLine(answerQuery(dp, 3));

    // query 2 answered
    Console.WriteLine( answerQuery(dp, 6));

    // query 3 answered
    Console.WriteLine( answerQuery(dp, 1));
}
}

// This code is contributed by Arnab Kundu

```

**输出**：

```
2
0
3

```

**时间复杂度**：`O(1)`回答查询。

**辅助空间**：`O(n)`。

**替代的更短实现**：

## C++

```cpp

#include <bits/stdc++.h>
using namespace std;

vector<int> no_NGN(int arr[], int n)
{
    vector<int> nxt;

    // use of stl stack in c++
    stack<int> s;

    nxt.push_back(0);
    // push the (n-1)th index to the stack
    s.push(n - 1);

    // traverse in reverse order
    for (int i = n - 2; i >= 0; i--) {
        while (!s.empty() && arr[i] >= arr[s.top()])
            s.pop();

        // if no element is greater than arr[i] the 
        // number of NGEs to right is 0
        if (s.empty()) 
            nxt.push_back(0);

        else

            // number of NGEs to right of arr[i] is 
            // one greater than the number of NGEs to right 
            // of higher number to its right
            nxt.push_back(nxt[n - s.top() - 1] + 1);

        s.push(i);
    }

    // reverse again because values are in reverse order
    reverse(nxt.begin(), nxt.end());

    // returns the vector of number of next
    // greater elements to the right of each index.
    return nxt;
}

int main()
{
    int n = 8;

    int arr[] = { 3, 4, 2, 7, 5, 8, 10, 6 };

    vector<int> nxt = no_NGN(arr, n);

    // query 1 answered
    cout << nxt[3] << endl;

    // query 2 answered
    cout << nxt[6] << endl;

    // query 3 answered
    cout << nxt[1] << endl;

    return 0;
}

```

**输出**：

```
2
0
3

```

本文由 [**Raja Vikramaditya**](https://www.facebook.com/raja.vikramaditya.7) 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的内容，或者想分享有关上述主题的更多信息，请发表评论。

