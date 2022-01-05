# 检查两垛是否相等，无变化

> 原文:[https://www . geeksforgeeks . org/check-如果两个堆栈相等或不相等，则不进行更改/](https://www.geeksforgeeks.org/check-if-two-stacks-are-equal-or-not-without-alteration/)

给定两个[栈](https://www.geeksforgeeks.org/stack-class-in-java/)**【S1】**和 **S2** ，任务是[检查两个栈是否相等](https://www.geeksforgeeks.org/check-if-the-two-given-stacks-are-same/)或者不在同一顺序而不丢失原始栈。如果两个栈相等，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** S1 = {3，4，2，1}，S2 = {3，4，2，1 }
> T3】输出:是
> 
> **输入:** S1 = {3，4，6}，S2 = {7，2，1 }
> T3】输出:否

**方法:**给定的问题可以通过在给定的两个[堆栈](https://www.geeksforgeeks.org/stack-class-in-java/)之间移动一些元素来解决，用于检查两个堆栈中的每个对应元素。按照以下步骤解决问题:

*   将堆栈大小 **S1** 和 **S2** 分别存储在变量 **N** 和 **M** 中。
*   如果 **N** 不等于 **M** ，则打印“ **No** ”返回。
*   迭代范围**【1，N】**并执行以下操作:
    *   [将](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/)[顶](https://www.geeksforgeeks.org/stack-top-c-stl/)T4(N–I)元素叠加 **S1** 推至叠加 **S2** 。
    *   现在，将 **S1** 栈的[顶元素存储在一个变量中，比如 **val** 。](https://www.geeksforgeeks.org/queue-using-stacks/)
    *   现在，[将](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/)[顶](https://www.geeksforgeeks.org/stack-top-c-stl/)**2 *(N–I)**元素从堆栈 **S2** 推到堆栈 **S1** 。
    *   如果 **val** 的值不等于栈顶值[**【S2】**](https://www.geeksforgeeks.org/stack-peek-method-in-c-sharp/)[则](https://www.geeksforgeeks.org/stack-peek-method-in-c-sharp/)打印 **No** 并返回。
    *   否则，通过从堆叠 **S1** 推顶**(N–I)**元素到堆叠 **S2** 来恢复[堆叠。](https://www.geeksforgeeks.org/merging-sorting-two-unsorted-stacks/)
*   完成上述步骤后，如果上述情况都不满足，则打印“**是**”。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to push the elements from
// one stack element into another stack
void pushElements(stack<int> s1, stack<int> s2, int len)
{
    int i = 1;
    while (i <= len) {

        // Update the stack
        if (s1.size() > 0) {
            s2.push(s1.top());
            s1.pop();
        }

        // Increment i
        i++;
    }
}

// Function to compare two given stacks
string compareStacks(stack<int> s1, stack<int> s2)
{
    // Stores the size of S1 stack
    int N = s1.size();

    // Stores the size of S2 stack
    int M = s2.size();

    // If N is not equal to M
    if (N != M) {
        return "No";
    }

    // Traverse the range [1, N]
    for (int i = 1; i <= N; i++) {

        // Push N-i elements to stack
        // S2 from stack S1
        pushElements(s1, s2, N - i);

        // Stores the top value of S1
        int val = s1.top();

        // Pushes the 2 * (N-i)
        // elements from S2 to S1
        pushElements(s2, s1, 2 * (N - i));

        // If val is not equal
        // to the top of S2
        if (val != s2.top())
            return "No";

        // Restores the stacks
        pushElements(s1, s2, N - i);
    }

    // Return
    return "Yes";
}

// Driver Code
int main()
{
    stack<int> S1, S2;

    S1.push(1);
    S1.push(2);
    S1.push(4);
    S1.push(3);

    S2.push(1);
    S2.push(2);
    S2.push(4);
    S2.push(3);

    cout << (compareStacks(S1, S2));
}

// This code is contributed by ukassp.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG {

    // Function to compare two given stacks
    static String compareStacks(
        Stack<Integer> s1,
        Stack<Integer> s2)
    {
        // Stores the size of S1 stack
        int N = s1.size();

        // Stores the size of S2 stack
        int M = s2.size();

        // If N is not equal to M
        if (N != M) {
            return "No";
        }

        // Traverse the range [1, N]
        for (int i = 1; i <= N; i++) {

            // Push N-i elements to stack
            // S2 from stack S1
            pushElements(s1, s2, N - i);

            // Stores the top value of S1
            int val = s1.peek();

            // Pushes the 2 * (N-i)
            // elements from S2 to S1
            pushElements(s2, s1, 2 * (N - i));

            // If val is not equal
            // to the top of S2
            if (val != s2.peek())
                return "No";

            // Restores the stacks
            pushElements(s1, s2, N - i);
        }

        // Return
        return "Yes";
    }

    // Function to push the elements from
    // one stack element into another stack
    static void pushElements(
        Stack<Integer> s1, Stack<Integer> s2,
        int len)
    {
        int i = 1;
        while (i <= len) {

            // Update the stack
            s2.push(s1.pop());

            // Increment i
            i++;
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        Stack<Integer> S1 = new Stack<>();
        Stack<Integer> S2 = new Stack<>();

        S1.push(1);
        S1.push(2);
        S1.push(4);
        S1.push(3);

        S2.push(1);
        S2.push(2);
        S2.push(4);
        S2.push(3);

        System.out.println(
            compareStacks(S1, S2));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to compare two given stacks
def compareStacks(s1, s2):
    # Stores the size of S1 stack
    N = len(s1)

    # Stores the size of S2 stack
    M = len(s2)

    # If N is not equal to M
    if (N != M):
        return "No"

    # Traverse the range [1, N]
    for i in range(1, N + 1):

        # Push N-i elements to stack
        # S2 from stack S1
        pushElements(s1, s2, N - i)

        # Stores the top value of S1
        val = s1[-1]

        # Pushes the 2 * (N-i)
        # elements from S2 to S1
        pushElements(s2, s1, 2 * (N - i))

        # If val is not equal
        # to the top of S2
        if (val != s2[-1]):
            return "No"

        # Restores the stacks
        pushElements(s1, s2, N - i)

    # Return
    return "Yes"

# Function to push the elements from
# one stack element into another stack
def pushElements(s1, s2, len):
    i = 1
    while (i <= len):

        # Update the stack
        s2.append(s1[-1])
        del s1[-1]

        # Increment i
        i += 1

# Driver Code
if __name__ == '__main__':
    S1 = []
    S2 = []

    S1.append(1)
    S1.append(2)
    S1.append(4)
    S1.append(3)

    S2.append(1)
    S2.append(2)
    S2.append(4)
    S2.append(3)

    print(compareStacks(S1, S2))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach

using System;
using System.Collections.Generic;

public class GFG {

    // Function to compare two given stacks
    static String compareStacks(
        Stack<int> s1,
        Stack<int> s2)
    {
        // Stores the size of S1 stack
        int N = s1.Count;

        // Stores the size of S2 stack
        int M = s2.Count;

        // If N is not equal to M
        if (N != M) {
            return "No";
        }

        // Traverse the range [1, N]
        for (int i = 1; i <= N; i++) {

            // Push N-i elements to stack
            // S2 from stack S1
            pushElements(s1, s2, N - i);

            // Stores the top value of S1
            int val = s1.Peek();

            // Pushes the 2 * (N-i)
            // elements from S2 to S1
            pushElements(s2, s1, 2 * (N - i));

            // If val is not equal
            // to the top of S2
            if (val != s2.Peek())
                return "No";

            // Restores the stacks
            pushElements(s1, s2, N - i);
        }

        // Return
        return "Yes";
    }

    // Function to push the elements from
    // one stack element into another stack
    static void pushElements(
        Stack<int> s1, Stack<int> s2,
        int len)
    {
        int i = 1;
        while (i <= len) {

            // Update the stack
            s2.Push(s1.Pop());

            // Increment i
            i++;
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        Stack<int> S1 = new Stack<int>();
        Stack<int> S2 = new Stack<int>();

        S1.Push(1);
        S1.Push(2);
        S1.Push(4);
        S1.Push(3);

        S2.Push(1);
        S2.Push(2);
        S2.Push(4);
        S2.Push(3);

        Console.WriteLine(
            compareStacks(S1, S2));
    }
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to push the elements from
// one stack element into another stack
function pushElements(s1, s2, len)
{
    var i = 1;
    while (i <= len) {

        // Update the stack
        if (s1.length > 0) {
            s2.push(s1[s1.length-1]);
            s1.pop();
        }

        // Increment i
        i++;
    }
}

// Function to compare two given stacks
function compareStacks(s1, s2)
{
    // Stores the size of S1 stack
    var N = s1.length;

    // Stores the size of S2 stack
    var M = s2.length;

    // If N is not equal to M
    if (N != M) {
        return "No";
    }

    // Traverse the range [1, N]
    for (var i = 1; i <= N; i++) {

        // Push N-i elements to stack
        // S2 from stack S1
        pushElements(s1, s2, N - i);

        // Stores the top value of S1
        var val = s1[s1.length-1];

        // Pushes the 2 * (N-i)
        // elements from S2 to S1
        pushElements(s2, s1, 2 * (N - i));

        // If val is not equal
        // to the top of S2
        if (val != s2[s2.length-1])
            return "No";

        // Restores the stacks
        pushElements(s1, s2, N - i);
    }

    // Return
    return "Yes";
}

// Driver Code
var S1 = [], S2 = [];
S1.push(1);
S1.push(2);
S1.push(4);
S1.push(3);
S2.push(1);
S2.push(2);
S2.push(4);
S2.push(3);
document.write(compareStacks(S1, S2));

//This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*