# 使用堆栈对数组进行排序

> 原文:[https://www.geeksforgeeks.org/sorting-array-using-stacks/](https://www.geeksforgeeks.org/sorting-array-using-stacks/)

给定一个元素数组，任务是使用堆栈对这些元素进行排序。

**先决条件:** [堆叠](https://www.geeksforgeeks.org/stack-data-structure/)

**示例:**

```
Input :  8 5 7 1 9 12 10
Output : 1 5 7 8 9 10 12 
Explanation :
Output is sorted element set

Input :  7 4 10 20 2 5 9 1
Output : 1 2 4 5 7 9 10 20 
```

我们基本上使用[使用临时堆栈](https://www.geeksforgeeks.org/sort-stack-using-temporary-stack/)对堆栈进行排序。然后我们将排序后的堆栈元素放回数组。

## C++

```
// C++ program to sort an array using stack
#include <bits/stdc++.h>
using namespace std;

// This function return the sorted stack
stack<int> sortStack(stack<int> input)
{
    stack<int> tmpStack;

    while (!input.empty())
    {
        // pop out the first element
        int tmp = input.top();
        input.pop();

        // while temporary stack is not empty
        // and top of stack is smaller than temp
        while (!tmpStack.empty() &&
                tmpStack.top() < tmp)
        {
            // pop from temporary stack and
            // push it to the input stack
            input.push(tmpStack.top());
            tmpStack.pop();
        }

        // push temp in temporary of stack
        tmpStack.push(tmp);
    }

    return tmpStack;
}

void sortArrayUsingStacks(int arr[], int n)
{
    // Push array elements to stack
    stack<int> input;
    for (int i=0; i<n; i++)
       input.push(arr[i]);

    // Sort the temporary stack
    stack<int> tmpStack = sortStack(input);

    // Put stack elements in arrp[]
    for (int i=0; i<n; i++)
    {
        arr[i] = tmpStack.top();
        tmpStack.pop();
    }
}

// main function
int main()
{
    int arr[] = {10, 5, 15, 45};
    int n = sizeof(arr)/sizeof(arr[0]);

    sortArrayUsingStacks(arr, n);

    for (int i=0; i<n; i++)
       cout << arr[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort an
// array using stack
import java.io.*;
import java.util.*;

class GFG
{
    // This function return
    // the sorted stack
    static Stack<Integer> sortStack(Stack<Integer> input)
    {
        Stack<Integer> tmpStack =
                       new Stack<Integer>();

        while (!input.empty())
        {
            // pop out the
            // first element
            int tmp = input.peek();
            input.pop();

            // while temporary stack is
            // not empty and top of stack
            // is smaller than temp
            while (!tmpStack.empty() &&
                    tmpStack.peek() < tmp)
            {
                // pop from temporary
                // stack and push it
                // to the input stack
                input.push(tmpStack.peek());
                tmpStack.pop();
            }

            // push temp in
            // temporary of stack
            tmpStack.push(tmp);
        }

        return tmpStack;
    }

    static void sortArrayUsingStacks(int []arr,
                                     int n)
    {
        // push array elements
        // to stack
        Stack<Integer> input =
                       new Stack<Integer>();
        for (int i = 0; i < n; i++)
            input.push(arr[i]);

        // Sort the temporary stack
        Stack<Integer> tmpStack =
                       sortStack(input);

        // Put stack elements
        // in arrp[]
        for (int i = 0; i < n; i++)
        {
            arr[i] = tmpStack.peek();
            tmpStack.pop();
        }
    }

    // Driver Code
    public static void main(String args[])
    {
        int []arr = {10, 5, 15, 45};
        int n = arr.length;

        sortArrayUsingStacks(arr, n);

        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 蟒蛇 3

```
# Python3 program to sort an array using stack

# This function return the sorted stack
def sortStack(input):
    tmpStack = []
    while (len(input) > 0):

        # pop out the first element
        tmp = input[-1]
        input.pop()

        # while temporary stack is not empty
        # and top of stack is smaller than temp
        while (len(tmpStack) > 0 and tmpStack[-1] < tmp):

            # pop from temporary stack and
            # append it to the input stack
            input.append(tmpStack[-1])
            tmpStack.pop()

        # append temp in temporary of stack
        tmpStack.append(tmp)

    return tmpStack

def sortArrayUsingStacks(arr, n):

    # append array elements to stack
    input = []
    i = 0
    while ( i < n ):
        input.append(arr[i])
        i = i + 1

    # Sort the temporary stack
    tmpStack = sortStack(input)
    i = 0

    # Put stack elements in arrp[]
    while (i < n):
        arr[i] = tmpStack[-1]
        tmpStack.pop()
        i = i + 1

    return arr

# Driver code
arr = [10, 5, 15, 45]
n = len(arr)

arr = sortArrayUsingStacks(arr, n)
i = 0

while (i < n):
    print(arr[i] ,end= " ")
    i = i + 1

# This code is contributed by Arnab Kundu
```

## C#

```
// C# program to sort an
// array using stack
using System;
using System.Collections.Generic;

class GFG
{
    // This function return
    // the sorted stack
    static Stack<int> sortStack(Stack<int> input)
    {
        Stack<int> tmpStack = new Stack<int>();

        while (input.Count != 0)
        {
            // pop out the
            // first element
            int tmp = input.Peek();
            input.Pop();

            // while temporary stack is
            // not empty and top of stack
            // is smaller than temp
            while (tmpStack.Count != 0 &&
                    tmpStack.Peek() < tmp)
            {
                // pop from temporary
                // stack and push it
                // to the input stack
                input.Push(tmpStack.Peek());
                tmpStack.Pop();
            }

            // push temp in
            // temporary of stack
            tmpStack.Push(tmp);
        }

        return tmpStack;
    }

    static void sortArrayUsingStacks(int []arr,
                                     int n)
    {
        // Push array elements
        // to stack
        Stack<int> input = new Stack<int>();
        for (int i = 0; i<n; i++)
        input.Push(arr[i]);

        // Sort the temporary stack
        Stack<int> tmpStack = sortStack(input);

        // Put stack elements in arrp[]
        for (int i = 0; i < n; i++)
        {
            arr[i] = tmpStack.Peek();
            tmpStack.Pop();
        }
    }

    // Driver Code
    static void Main()
    {
        int []arr = new int[] {10, 5,
                               15, 45};
        int n = arr.Length;

        sortArrayUsingStacks(arr, n);

        for (int i = 0; i < n; i++)
        Console.Write(arr[i] + " ");
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## java 描述语言

```
<script>

// Javascript program to sort an array using stack

// This function return the sorted stack
function sortStack(input)
{
    var tmpStack = [];

    while (input.length!=0)
    {
        // pop out the first element
        var tmp = input[input.length-1];
        input.pop();

        // while temporary stack is not empty
        // and top of stack is smaller than temp
        while (tmpStack.length!=0 &&
                tmpStack[tmpStack.length-1] < tmp)
        {
            // pop from temporary stack and
            // push it to the input stack
            input.push(tmpStack[tmpStack.length-1]);
            tmpStack.pop();
        }

        // push temp in temporary of stack
        tmpStack.push(tmp);
    }

    return tmpStack;
}

function sortArrayUsingStacks(arr, n)
{
    // Push array elements to stack
    var input = [];
    for (var i=0; i<n; i++)
       input.push(arr[i]);

    // Sort the temporary stack
    var tmpStack = sortStack(input);

    // Put stack elements in arrp[]
    for (var i=0; i<n; i++)
    {
        arr[i] = tmpStack[tmpStack.length-1];
        tmpStack.pop();
    }
}

// main function
var arr = [10, 5, 15, 45];
var n = arr.length;
sortArrayUsingStacks(arr, n);
for (var i=0; i<n; i++)
   document.write( arr[i] + " ");

</script>
```

**Output:** 

```
5 10 15 45
```

**时间复杂度:** O(n*n)