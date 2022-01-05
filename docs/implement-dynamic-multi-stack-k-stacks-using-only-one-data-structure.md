# 仅使用一个数据结构实现动态多栈(K 栈)

> 原文:[https://www . geesforgeks . org/implement-dynamic-multi-stack-k-stacks-仅使用一个数据结构/](https://www.geeksforgeeks.org/implement-dynamic-multi-stack-k-stacks-using-only-one-data-structure/)

在本文中，我们将看到如何创建一个 [**数据结构**](https://www.geeksforgeeks.org/data-structures/) ，该数据结构可以处理多个 [**堆栈**](https://www.geeksforgeeks.org/stack-data-structure/) 以及可增长的大小。数据结构需要处理三个操作:

> *   **push(x, stackNum)** = Push the value x to the stack numbered stackNum.
> *   **pop (stackNum)** = Pop the top element from the stack numbered stacknum.
> *   **Top (stack num)** = Displays the topmost element stacknum in the stack.

### 示例:

> 假设给定的多堆栈是[{1，2}、{4，6}、{9，10}]
> 
> **输入:**推(3，0)，顶(0)
> 推(7，1)，顶(1)
> 弹出(2)，顶(2)
> 
> **输出:** 3，7，9
> 
> **说明:**栈 0 推 3 时，栈变成{1，2，3}。所以最上面的元素是 3。
> 当 7 被推入堆栈 1 时，堆栈变成{4，6，7}。所以最上面的元素是 7。
> 当栈 2 弹出最顶层元素时，栈变成{9}。所以最上面的元素是 9

**方法:**遵循下面提到的方法来实现这个想法。

*   将每个堆栈的**大小**和**顶部索引**存储在数组中**大小[]** 和 **topIndex[]** 。
*   大小将存储在 [**前缀和数组**](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/) 中(使用前缀和数组将帮助我们在 O(1)时间内找到堆栈的开始/大小)
*   如果堆栈的大小达到**最大**保留容量，**扩展**保留大小(乘以 2)
*   如果堆栈的大小降至保留大小的四分之一**则缩小保留大小(除以 2)**
*   每当我们需要扩展/收缩数据结构中的一个堆栈时，其他堆栈的索引可能会改变，因此我们需要注意这一点。这可以通过增加/减少 sizes 和 topIndex[]数组的值来实现(我们可以在 O(堆栈数量)时间内做到这一点)。

下面是实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

template <typename T>

// Class to implement multistack
class MultiStack {
    int numberOfStacks;
    vector<T> values;
    vector<int> sizes, topIndex;

public:
    // Constructor to create k stacks
    // (by default 1)
    MultiStack(int k = 1)
        : numberOfStacks(k)
    {
        // reserve 2 elements for each stack first
        values = vector<T>(numberOfStacks << 1);

        // For each stack store the index
        // of the element on the top
        // and the size (starting point)
        sizes = vector<int>(numberOfStacks);
        topIndex = vector<int>(numberOfStacks);

        // Sizes is a prefix sum vector
        for (int size = 2, i = 0; i < numberOfStacks;
             i++, size += 2)
            sizes[i] = size, topIndex[i] = size - 2;
    }

    // Push a value in a stack
    void push(int stackNum, T val)
    {

        // Check if the stack is full,
        // if so Expand it
        if (isFull(stackNum))
            Expand(stackNum);

        // Add the value to the top of the stack
        // and increment the top index
        values[topIndex[stackNum]++] = val;
    }

    // Pop the top value and
    // return it form a stack
    T pop(int stackNum)
    {

        // If the stack is empty
        // throw an error
        if (empty(stackNum))
            throw("Empty Stack!");

        // Save the top value
        T val = values[topIndex[stackNum] - 1];

        // Set top value to default data type
        values[--topIndex[stackNum]] = T();

        // Shrink the reserved size if needed
        Shrink(stackNum);

        // Return the pop-ed value
        return val;
    }

    // Return the top value form a stack
    // Same as pop (but without removal)
    T top(int stackNum)
    {
        if (empty(stackNum))
            throw("Empty Stack!");
        return values[topIndex[stackNum] - 1];
    }

    // Return the size of a stack
    // (the number of elements in the stack,
    // not the reserved size)
    int size(int stackNum)
    {
        if (!stackNum)
            return topIndex[0];
        return topIndex[stackNum] - sizes[stackNum - 1];
    }

    // Check if a stack is empty or not
    // (has no elements)
    bool empty(int stackNum)
    {
        int offset;
        if (!stackNum)
            offset = 0;
        else
            offset = sizes[stackNum - 1];
        int index = topIndex[stackNum];
        return index == offset;
    }

    // Helper function to check
    // if a stack size has reached
    // the reserved size of that stack
    bool isFull(int stackNum)
    {
        int offset = sizes[stackNum];
        int index = topIndex[stackNum];
        return index >= offset;
    }

    // Function to expand the reserved size
    // of a stack (multiply by 2)
    void Expand(int stackNum)
    {

        // Get the reserved_size of the stack()
        int reserved_size = size(stackNum);

        // Update the prefix sums (sizes)
        // and the top index of the next stacks
        for (int i = stackNum + 1; i < numberOfStacks; i++)
            sizes[i] += reserved_size,
                topIndex[i] += reserved_size;

        // Update the size of the recent stack
        sizes[stackNum] += reserved_size;

        // Double the size of the stack by
        // inserting 'reserved_size' elements
        values.insert(values.begin() + topIndex[stackNum],
                      reserved_size, T());
    }

    // Function to shrink the reserved size
    // of a stack (divide by2)
    void Shrink(int stackNum)
    {

        // Get the reserved size and the current size
        int reserved_size, current_size;
        if (!stackNum)
            reserved_size = sizes[0],
            current_size = topIndex[0];
        else
            reserved_size
                = sizes[stackNum] - sizes[stackNum - 1],
                current_size
                = topIndex[stackNum] - sizes[stackNum - 1];

        // Shrink only if the size is
        // lower than a quarter of the
        // reserved size and avoid shrinking
        // if the reserved size is 2
        if (current_size * 4 > reserved_size
            || reserved_size == 2)
            return;

        // Divide the size by 2 and update
        // the prefix sums (sizes) and
        // the top index of the next stacks
        int dif = reserved_size / 2;
        for (int i = stackNum + 1; i < numberOfStacks; i++)
            sizes[i] -= dif, topIndex[i] -= dif;
        sizes[stackNum] -= dif;

        // Erase half of the reserved size
        values.erase(values.begin() + topIndex[stackNum],
                     values.begin() + topIndex[stackNum]
                         + dif);
    }
};

// Driver code
int main()
{
    // create 3 stacks
    MultiStack<int> MStack(3);

    // push elements in stack 0:
    MStack.push(0, 21);
    MStack.push(0, 13);
    MStack.push(0, 14);

    // Push one element in stack 1:
    MStack.push(1, 15);

    // Push two elements in stack 2:
    MStack.push(2, 1);
    MStack.push(2, 2);
    MStack.push(2, 3);

    // Print the top elements of the stacks
    cout << MStack.top(0) << '\n';
    cout << MStack.top(1) << '\n';
    cout << MStack.top(2) << '\n';

    return 0;
}
```

**Output**

```
14
15
3
```

**时间复杂度:**

*   O(1)为**顶()**功能。
*   [摊销](https://www.geeksforgeeks.org/analysis-algorithm-set-5-amortized-analysis-introduction/) O(1)为**推()**和 **pop()** 功能。

**辅助空间:** O(N)其中 N 为堆叠数