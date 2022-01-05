# 减少阵列所需的最小步骤

> 原文:[https://www . geesforgeks . org/制作递减数组所需的最少步骤/](https://www.geeksforgeeks.org/minimum-steps-required-to-make-an-array-decreasing/)

给定一个数组 **arr[]** ，任务是找到使一个数组递减所需的最少步骤，其中在每个步骤中移除大于其左边元素的所有元素。
**例:**

> **输入:** arr[] = {3，2，1，7，5}
> **输出:** 2
> **解释:**
> 在上面的数组中，需要两个步骤来使数组递减–
> **步骤 1:** 在步骤 1 中，有一个元素大于它的左边，即 7 > 1。
> **第二步:**在第二步中有一个元素大于它的左边，那就是 5 > 1。
> **输入:** arr[] = {6，5，8，4，7，10，9}
> **输出:** 2
> 在上述数组中，需要两个步骤来使数组递减–
> **步骤 1:** 在步骤 1 中，有三个元素大于其左边的元素，即 8 > 5、7 > 4 和 10 > 7。
> **第二步:**在第二步中有三个只有一个元素大于它的左边是 9 > 4。

**天真方法:**迭代数组并计算大于其左边的元素，如果元素不大于其左边，则将元素推入另一个数组(比如 **arr1** )，在数组完全迭代后，将 arr1 的所有元素复制到初始数组，并重复相同的过程，直到在一个步骤中移除的元素计数为 0。这种方法在最坏的情况下需要 0(N<sup>2</sup>)的时间和 0(N)的空间。
**高效方法:**想法是使用堆栈，只有当元素大于其前一个元素时，才将其推入堆栈，否则计算扫描和弹出的次数。
我们只关心较小的元素。

## C++

```
//C++ implementation to make an
// array decreasing

#include<bits/stdc++.h>
using namespace std;

// Structure to store elements
struct Node
{
    int elementID;
    int stepsToeliminate;
};

// Function to find the
// minimum steps required
void minSteps(int arr[], int N)
{
    stack<Node> s;

    s.push({ 0, -1 });

    // Minimum steps
    int maxStepsToeliminate = -1;

    // Loop to iterate
    // over the array
    for (int i = 1; i < N; i++)
    {
        int stepsToeliminate = 1;

        // Traversing the stack until
        // it is not empty
        while (!s.empty())
        {
            // Condition if the top of the
            // stack is greater than the
            // current element
            if (arr[s.top().elementID] >=
                                   arr[i])
            {
                stepsToeliminate = max(stepsToeliminate,
                           s.top().stepsToeliminate + 1);
                s.pop();
            }
            else
            {
                break;
            }
        }

        // Condition if no previous
        // elements value less than
        // this element then steps is -1
        if (s.empty())
        {
            stepsToeliminate = -1;
        }

        maxStepsToeliminate = max(
            maxStepsToeliminate, stepsToeliminate
            );
        s.push({ i, stepsToeliminate });
    }

    cout << (maxStepsToeliminate < 0 ? 0 :
              maxStepsToeliminate) << endl;
}

// Driver Code
int main()
{
    int arr[] = {3, 2, 1, 7, 5};

    int size = sizeof(arr)/sizeof(arr[0]);

    minSteps(arr, size);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to make an
// array decreasing
import java.util.*;

class GFG{

// Structure to store elements
static class Node
{
    int elementID;
    int stepsToeliminate;
    public Node(int elementID, int stepsToeliminate) {
        super();
        this.elementID = elementID;
        this.stepsToeliminate = stepsToeliminate;
    }

};

// Function to find the
// minimum steps required
static void minSteps(int arr[], int N)
{
    Stack<Node> s = new Stack<Node>();

    s.add(new Node( 0, -1 ));

    // Minimum steps
    int maxStepsToeliminate = -1;

    // Loop to iterate
    // over the array
    for (int i = 1; i < N; i++)
    {
        int stepsToeliminate = 1;

        // Traversing the stack until
        // it is not empty
        while (!s.isEmpty())
        {
            // Condition if the top of the
            // stack is greater than the
            // current element
            if (arr[s.peek().elementID] >=
                                   arr[i])
            {
                stepsToeliminate = Math.max(stepsToeliminate,
                           s.peek().stepsToeliminate + 1);
                s.pop();
            }
            else
            {
                break;
            }
        }

        // Condition if no previous
        // elements value less than
        // this element then steps is -1
        if (s.isEmpty())
        {
            stepsToeliminate = -1;
        }

        maxStepsToeliminate = Math.max(
            maxStepsToeliminate, stepsToeliminate
            );
        s.add(new Node(i, stepsToeliminate ));
    }

    System.out.print((maxStepsToeliminate < 0 ? 0 :
              maxStepsToeliminate) +"\n");
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = {3, 2, 1, 7, 5};

    int size = arr.length;

    minSteps(arr, size);    
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 implementation to make an
# array decreasing

# Function to find the
# minimum steps required
def minSteps(arr,  N) :

    s = [];

    s.append(( 0, -1 ));

    # Minimum steps
    maxStepsToeliminate = -1;

    # Loop to iterate
    # over the array
    for i in range(1, N) :

        stepsToeliminate = 1;

        # Traversing the stack until
        # it is not empty
        while (len(s) != 0) :

            # Condition if the top of the
            # stack is greater than the
            # current element
            if (arr[s[-1][0]] >= arr[i]) :
                stepsToeliminate = max(stepsToeliminate, s[-1][1] + 1);
                s.pop();

            else :

                break;

        # Condition if no previous
        # elements value less than
        # this element then steps is -1
        if (len(s) == 0) :

            stepsToeliminate = -1;

        maxStepsToeliminate = max( maxStepsToeliminate, stepsToeliminate );

        s.append(( i, stepsToeliminate ));

    print(  0 if (maxStepsToeliminate < 0 ) else  maxStepsToeliminate );

# Driver Code
if __name__ == "__main__" :

    arr = [3, 2, 1, 7, 5];

    size = len(arr);

    minSteps(arr, size);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation to make an
// array decreasing
using System;
using System.Collections.Generic;

class GFG{

// Structure to store elements
class Node
{
    public int elementID;
    public int stepsToeliminate;
    public Node(int elementID, int stepsToeliminate) {
        this.elementID = elementID;
        this.stepsToeliminate = stepsToeliminate;
    }

};

// Function to find the
// minimum steps required
static void minSteps(int []arr, int N)
{
    Stack<Node> s = new Stack<Node>();

    s.Push(new Node( 0, -1 ));

    // Minimum steps
    int maxStepsToeliminate = -1;

    // Loop to iterate
    // over the array
    for (int i = 1; i < N; i++)
    {
        int stepsToeliminate = 1;

        // Traversing the stack until
        // it is not empty
        while (s.Count!=0)
        {
            // Condition if the top of the
            // stack is greater than the
            // current element
            if (arr[s.Peek().elementID] >=
                                   arr[i])
            {
                stepsToeliminate = Math.Max(stepsToeliminate,
                           s.Peek().stepsToeliminate + 1);
                s.Pop();
            }
            else
            {
                break;
            }
        }

        // Condition if no previous
        // elements value less than
        // this element then steps is -1
        if (s.Count!=0)
        {
            stepsToeliminate = -1;
        }

        maxStepsToeliminate = Math.Max(
            maxStepsToeliminate, stepsToeliminate
            );
        s.Push(new Node(i, stepsToeliminate ));
    }

    Console.Write((maxStepsToeliminate < 0 ? 0 :
              maxStepsToeliminate) +"\n");
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = {3, 2, 1, 7, 5};

    int size = arr.Length;

    minSteps(arr, size);    
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
    // Javascript implementation to make an array decreasing

    // Structure to store elements
    class Node
    {
        constructor(elementID, stepsToeliminate) {
           this.elementID = elementID;
           this.stepsToeliminate = stepsToeliminate;
        }
    }

    // Function to find the
    // minimum steps required
    function minSteps(arr, N)
    {
        let s = [];

        s.push(new Node( 0, -1 ));

        // Minimum steps
        let maxStepsToeliminate = -1;

        // Loop to iterate
        // over the array
        for (let i = 1; i < N; i++)
        {
            let stepsToeliminate = 1;

            // Traversing the stack until
            // it is not empty
            while (s.length!=0)
            {
                // Condition if the top of the
                // stack is greater than the
                // current element
                if (arr[s[s.length - 1].elementID] >= arr[i])
                {
                    stepsToeliminate = Math.max(stepsToeliminate,
                               s[s.length - 1].stepsToeliminate + 1);
                    s.pop();
                }
                else
                {
                    break;
                }
            }

            // Condition if no previous
            // elements value less than
            // this element then steps is -1
            if (s.length!=0)
            {
                stepsToeliminate = -1;
            }

            maxStepsToeliminate = Math.max(maxStepsToeliminate, stepsToeliminate);
            s.push(new Node(i, stepsToeliminate ));
        }

        document.write((maxStepsToeliminate < 0 ? 0 :
                  maxStepsToeliminate) +"</br>");
    }

    let arr = [3, 2, 1, 7, 5];

    let size = arr.length;

    minSteps(arr, size);

    // This code is contributed by rameshtravel07.
</script>
```

**Output:** 

```
2
```

**业绩分析:**

*   **时间复杂度:**和上面的方法一样，有一个需要 O(N)时间的循环，因此时间复杂度为 **O(N)** 。
*   **空间复杂度:**和上面的方法一样，有一个栈用来存储前面的元素，因此空间复杂度为 **O(N)** 。