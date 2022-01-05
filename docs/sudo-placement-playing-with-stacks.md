# Sudo 放置【1.3】|玩牌

> 原文:[https://www . geesforgeks . org/sudo-placement-playing-stacks/](https://www.geeksforgeeks.org/sudo-placement-playing-with-stacks/)

给你 3 个栈，A(输入栈)，B(辅助栈)和 C(输出栈)。最初堆栈 A 包含从 1 到 N 的数字，你需要将所有数字从堆栈 A 按排序顺序转移到堆栈 C，也就是说，最后，堆栈 C 应该在底部有最小的元素，在顶部有最大的元素。您可以使用堆栈 B，即在任何时候，您也可以将元素推入/弹出堆栈 B。在堆栈 A 的末尾，B 应该是空的。

**示例:**

> **输入:** A = {4，3，1，2，5}
> **输出:**是 7
> 
> **输入:** A = {3，4，1，2，5}
> 输出:否

**方法:**从给定堆栈的底部迭代。将*所需的*初始化为堆栈中最后的最底层元素，即 1。遵循下面给出的算法来解决上述问题。

*   如果堆栈元素等于所需元素，那么传输次数将是从 A 到 c 的传输计数
*   如果它不等于所需的元素，则通过将其与堆栈中最上面的元素进行比较来检查是否可以传输它。
    1.  如果 stackC 中最上面的元素大于 stackA[i]元素，则不可能以排序的方式传输它，
    2.  否则，将元素推送到 stackC 并递增传输。
*   在 stackC 中迭代，弹出最上面的元素，直到它等于所需的和所需的增量，并在每个步骤中传递。

下面是上述方法的实现:

## C++

```
// C++ program for
// Sudo Placement | playing with stacks
#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible
// count the number of steps
void countSteps(int sa[], int n)
{

    // Another stack
    stack<int> sc;

    // variables to count transfers
    int required = 1, transfer = 0;

    // iterate in the stack in reverse order
    for (int i = 0; i < n; i++) {

        // if the last element has to be
        // inserted by removing elements
        // then count the number of steps
        if (sa[i] == required) {
            required++;
            transfer++;
        }
        else {
            // if stack is not empty and top element
            // is smaller than current element
            if (!sc.empty() && sc.top() < sa[i]) {
                cout << "NO";
                return;
            }
            // push into stack and count operation
            else {

                sc.push(sa[i]);
                transfer++;
            }
        }
        // stack not empty, then pop the top element
        // pop out all elements till is it equal to required
        while (!sc.empty() && sc.top() == required) {
            required++;
            sc.pop();
            transfer++;
        }
    }

    // print the steps
    cout << "YES " << transfer;
}

// Driver Code
int main()
{
    int sa[] = { 4, 3, 1, 2, 5 };
    int n = sizeof(sa) / sizeof(sa[0]);
    countSteps(sa, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for Sudo
// Placement | playing with stacks
import java.util.*;

class GFG
{

    // Function to check if it is possible
    // count the number of steps
    static void countSteps(int sa[], int n)
    {

        // Another stack
        Stack<Integer> sc = new Stack<Integer>();

        // variables to count transfers
        int required = 1, transfer = 0;

        // iterate in the stack in reverse order
        for (int i = 0; i < n; i++)
        {

            // if the last element has to be
            // inserted by removing elements
            // then count the number of steps
            if (sa[i] == required)
            {
                required++;
                transfer++;
            }
            else
            // if stack is not empty and top element
            // is smaller than current element
            if (!sc.empty() && sc.peek() < sa[i])
            {
                System.out.print("NO");
                return;
            }

            // push into stack and count operation
            else
            {

                sc.push(sa[i]);
                transfer++;
            }
            // stack not empty, then pop the top element
            // pop out all elements till is it equal to required
            while (!sc.empty() && sc.peek() == required)
            {
                required++;
                sc.pop();
                transfer++;
            }
        }

        // print the steps
        System.out.println("YES " + transfer);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int sa[] = {4, 3, 1, 2, 5};
        int n = sa.length;
        countSteps(sa, n);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 program for
# Sudo Placement | playing with stacks
from typing import List

# Function to check if it is possible
# count the number of steps
def countSteps(sa: List[int], n: int) -> None:

    # Another stack
    sc = []

    # Variables to count transfers
    required = 1
    transfer = 0

    # Iterate in the stack in reverse order
    for i in range(n):

        # If the last element has to be
        # inserted by removing elements
        # then count the number of steps
        if (sa[i] == required):
            required += 1
            transfer += 1

        else:

            # If stack is not empty and top element
            # is smaller than current element
            if (sc and sc[-1] < sa[i]):
                print("NO")
                return

            # push into stack and count operation
            else:
                sc.append(sa[i])
                transfer += 1

        # stack not empty, then pop the top
        # element pop out all elements till
        # is it equal to required
        while (sc and sc[-1] == required):
            required += 1
            sc.pop()
            transfer += 1

    # Print the steps
    print("YES {}".format(transfer))

# Driver Code
if __name__ == "__main__":

    sa = [ 4, 3, 1, 2, 5 ]
    n = len(sa)

    countSteps(sa, n)

# This code is contributed by sanjeev2552
```

## C#

```
// C# program for Sudo
// Placement | playing with stacks
using System;
using System.Collections.Generic;   

public class GFG
{

    // Function to check if it is possible
    // count the number of steps
    static void countSteps(int []sa, int n)
    {

        // Another stack
        Stack<int> sc = new Stack<int>();

        // variables to count transfers
        int required = 1, transfer = 0;

        // iterate in the stack in reverse order
        for (int i = 0; i < n; i++)
        {

            // if the last element has to be
            // inserted by removing elements
            // then count the number of steps
            if (sa[i] == required)
            {
                required++;
                transfer++;
            }
            else
            // if stack is not empty and top element
            // is smaller than current element
            if (sc.Count!=0 && sc.Peek() < sa[i])
            {
                Console.Write("NO");
                return;
            }

            // push into stack and count operation
            else
            {

                sc.Push(sa[i]);
                transfer++;
            }
            // stack not empty, then pop the top element
            // pop out all elements till is it equal to required
            while (sc.Count!=0 && sc.Peek() == required)
            {
                required++;
                sc.Pop();
                transfer++;
            }
        }

        // print the steps
        Console.WriteLine("YES " + transfer);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int []sa = {4, 3, 1, 2, 5};
        int n = sa.Length;
        countSteps(sa, n);
    }
}
// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program for Sudo
// Placement | playing with stacks

// Function to check if it is possible
// count the number of steps
function countSteps(sa, n)
{

    // Another stack
        let sc = [];

        // variables to count transfers
        let required = 1, transfer = 0;

        // iterate in the stack in reverse order
        for (let i = 0; i < n; i++)
        {

            // if the last element has to be
            // inserted by removing elements
            // then count the number of steps
            if (sa[i] == required)
            {
                required++;
                transfer++;
            }
            else

            // if stack is not empty and top element
            // is smaller than current element
            if (sc.length!=0 && sc[sc.length-1] < sa[i])
            {
                document.write("NO");
                return;
            }

            // push into stack and count operation
            else
            {

                sc.push(sa[i]);
                transfer++;
            }

            // stack not empty, then pop the top element
            // pop out all elements till is it equal to required
            while (sc.length!=0 && sc[sc.length-1] == required)
            {
                required++;
                sc.pop();
                transfer++;
            }
        }

        // print the steps
        document.write("YES " + transfer+"<br>");
}

// Driver Code
let sa=[4, 3, 1, 2, 5];
let n = sa.length;
countSteps(sa, n);

// This code is contributed by rag2127
</script>
```

**Output:** 

```
YES 7
```