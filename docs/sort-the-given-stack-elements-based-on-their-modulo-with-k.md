# 根据给定堆栈元素与 K 的模对其进行排序

> 原文:[https://www . geeksforgeeks . org/基于给定堆栈元素的 k 模排序/](https://www.geeksforgeeks.org/sort-the-given-stack-elements-based-on-their-modulo-with-k/)

给定一个整数堆栈和一个整数 **K** ，任务是使用另一个堆栈按照与 **K** 模的递增顺序对给定堆栈的元素进行排序。如果两个数有相同的余数，那么较小的数应该排在第一位。
**例**

> **输入:** stack = {10，3，2，6，12}，K = 4
> **输出:** 12 2 6 10 3
> {12，2，6，10，3}是所需的排序顺序，因为 K = 4 的这些元素的模
> 是{2，3，2，2，0}
> 
> **输入:**堆栈= {3，4，5，10，11，1}，K = 3
> T3】输出: 3 1 4 10 5 11

**方法:**使用另一个临时堆栈对堆栈的元素进行[排序的方法已经在](https://www.geeksforgeeks.org/merge-sort/)[这篇](https://www.geeksforgeeks.org/sort-stack-using-temporary-stack/)文章中讨论过了，这里可以使用相同的方法根据元素与 **K** 的模对元素进行排序，唯一的区别是当被比较的元素给出相同的模值时，它们将根据它们的值进行比较。

下面是上述方法的实现:

## C++

```
// C++ implementation of the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to sort the stack using
// another stack based on the
// values of elements modulo k
void sortStack(stack<int>& input, int k)
{
    stack<int> tmpStack;

    while (!input.empty()) {

        // Pop out the first element
        int tmp = input.top();
        input.pop();

        // While temporary stack is not empty
        while (!tmpStack.empty()) {
            int tmpStackMod = tmpStack.top() % k;
            int tmpMod = tmp % k;

            // The top of the stack modulo k is
            // greater than (temp & k) or if they
            // are equal then compare the values
            if ((tmpStackMod > tmpMod)
                || (tmpStackMod == tmpMod
                    && tmpStack.top() > tmp)) {

                // Pop from temporary stack and push
                // it to the input stack
                input.push(tmpStack.top());
                tmpStack.pop();
            }
            else
                break;
        }

        // Push temp in temporary of stack
        tmpStack.push(tmp);
    }

    // Push all the elements in the original
    // stack to get the ascending order
    while (!tmpStack.empty()) {
        input.push(tmpStack.top());
        tmpStack.pop();
    }

    // Print the sorted elements
    while (!input.empty()) {
        cout << input.top() << " ";
        input.pop();
    }
}

// Driver code
int main()
{
    stack<int> input;
    input.push(10);
    input.push(3);
    input.push(2);
    input.push(6);
    input.push(12);

    int k = 4;

    sortStack(input, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to sort the stack using
// another stack based on the
// values of elements modulo k
static void sortStack(Stack<Integer> input, int k)
{
    Stack<Integer> tmpStack = new Stack<Integer>();

    while (!input.isEmpty())
    {

        // Pop out the first element
        int tmp = input.peek();
        input.pop();

        // While temporary stack is not empty
        while (!tmpStack.isEmpty())
        {
            int tmpStackMod = tmpStack.peek() % k;
            int tmpMod = tmp % k;

            // The top of the stack modulo k is
            // greater than (temp & k) or if they
            // are equal then compare the values
            if ((tmpStackMod > tmpMod) ||
                (tmpStackMod == tmpMod &&
                 tmpStack.peek() > tmp))
            {

                // Pop from temporary stack and push
                // it to the input stack
                input.push(tmpStack.peek());
                tmpStack.pop();
            }
            else
                break;
        }

        // Push temp in temporary of stack
        tmpStack.push(tmp);
    }

    // Push all the elements in the original
    // stack to get the ascending order
    while (!tmpStack.isEmpty())
    {
        input.push(tmpStack.peek());
        tmpStack.pop();
    }

    // Print the sorted elements
    while (!input.empty())
    {
        System.out.print(input.peek() + " ");
        input.pop();
    }
}

// Driver code
public static void main(String args[])
{
    Stack<Integer> input = new Stack<Integer>();
    input.push(10);
    input.push(3);
    input.push(2);
    input.push(6);
    input.push(12);

    int k = 4;

    sortStack(input, k);
}
}

// This code is contributed by adityapande88
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to sort the stack using
# another stack based on the
# values of elements modulo k
def sortStack(input1, k):

    tmpStack = []

    while (len(input1) != 0):

        # Pop out the first element
        tmp = input1[-1]
        input1.pop()

        # While temporary stack is
        # not empty
        while (len(tmpStack) != 0):
            tmpStackMod = tmpStack[-1] % k
            tmpMod = tmp % k

            # The top of the stack modulo
            # k is greater than (temp & k)
            # or if they are equal then
            # compare the values
            if ((tmpStackMod > tmpMod) or
                (tmpStackMod == tmpMod and
                 tmpStack[-1] > tmp)):

                # Pop from temporary stack
                # and push it to the input
                # stack
                input1.append(tmpStack[-1])
                tmpStack.pop()
            else:
                break

        # Push temp in temporary of stack
        tmpStack.append(tmp)

    # Push all the elements in
    # the original stack to get
    # the ascending order
    while (len(tmpStack) != 0):
        input1.append(tmpStack[-1])
        tmpStack.pop()

    # Print the sorted elements
    while (len(input1) != 0):
        print(input1[-1], end = " ")
        input1.pop()

# Driver code
if __name__ == "__main__":

    input1 = []
    input1.append(10)
    input1.append(3)
    input1.append(2)
    input1.append(6)
    input1.append(12)
    k = 4
    sortStack(input1, k)

# This code is contributed by Chitranayal
```

## C#

```
// C# implementation of the
// above approach
using System;
using System.Collections;
class GFG{

// Function to sort the stack using
// another stack based on the
// values of elements modulo k
static void sortStack(Stack input,
                      int k)
{
  Stack tmpStack = new Stack();

  while(input.Count != 0)
  {
    // Pop out the first element
    int tmp = (int)input.Peek();
    input.Pop();

    // While temporary stack is not empty
    while (tmpStack.Count != 0)
    {
      int tmpStackMod = (int)tmpStack.Peek() % k;
      int tmpMod = tmp % k;

      // The top of the stack modulo k is
      // greater than (temp & k) or if they
      // are equal then compare the values
      if ((tmpStackMod > tmpMod) ||
          (tmpStackMod == tmpMod &&
          (int)tmpStack.Peek() > tmp))
      {
        // Pop from temporary stack and push
        // it to the input stack
        input.Push((int)tmpStack.Peek());
        tmpStack.Pop();
      }
      else
        break;
    }

    // Push temp in temporary of stack
    tmpStack.Push(tmp);
  }

  // Push all the elements in the original
  // stack to get the ascending order
  while (tmpStack.Count != 0)
  {
    input.Push((int)tmpStack.Peek());
    tmpStack.Pop();
  }

  // Print the sorted elements
  while (input.Count != 0)
  {
    Console.Write((int)input.Peek() + " ");
    input.Pop();
  }
}

// Driver Code
public static void Main(string[] args)
{
  Stack input = new Stack();
  input.Push(10);
  input.Push(3);
  input.Push(2);
  input.Push(6);
  input.Push(12);
  int k = 4;
  sortStack(input, k);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// JavaScript implementation of the
// above approach

// Function to sort the stack using
// another stack based on the
// values of elements modulo k
function sortStack(input,k)
{
    let tmpStack = [];

    while (input.length!=0)
    {

        // Pop out the first element
           let tmp = input.pop();

        // While temporary stack is not empty
        while (tmpStack.length!=0)
        {
            let tmpStackMod = tmpStack[tmpStack.length-1] % k;
            let tmpMod = tmp % k;

            // The top of the stack modulo k is
            // greater than (temp & k) or if they
            // are equal then compare the values
            if ((tmpStackMod > tmpMod) ||
                (tmpStackMod == tmpMod &&
                 tmpStack[tmpStack.length-1] > tmp))
            {

                // Pop from temporary stack and push
                // it to the input stack
                input.push(tmpStack[tmpStack.length-1]);
                tmpStack.pop();
            }
            else
                break;
        }

        // Push temp in temporary of stack
        tmpStack.push(tmp);
    }

    // Push all the elements in the original
    // stack to get the ascending order
    while (tmpStack.length!=0)
    {
        input.push(tmpStack[tmpStack.length-1]);
        tmpStack.pop();
    }

    // Print the sorted elements
    while (input.length!=0)
    {
        document.write(input.pop() + " ");

    }
}

// Driver code
let input =[];
input.push(10);
input.push(3);
input.push(2);
input.push(6);
input.push(12);

let k = 4;

sortStack(input, k);

// This code is contributed by rag2127

</script>
```

**Output:** 

```
12 2 6 10 3
```