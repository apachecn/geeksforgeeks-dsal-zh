# 通过给定的操作

将阵列减少到一个元素

> 原文:[https://www . geeksforgeeks . org/按给定操作将阵列减少到一个元素/](https://www.geeksforgeeks.org/reduce-the-array-to-atmost-one-element-by-the-given-operations/)

给定一个整数数组 **arr[]** ，任务是在执行以下操作后找到数组中的剩余元素:

*   在每一轮中，从数组中选择两个最大整数 X 和 Y。
*   如果 X == Y，则从数组中移除这两个元素。
*   如果 X！= Y，在数组中插入一个等于**ABS(X–Y)**的元素。

**注意:**如果没有剩余元素，打印 0。
**例:**

> **输入:**arr[]=【3，4，6，2，7，1】
> **输出:** 1
> **解释:**
> 元素 7 和 6 减少为 1，因此数组转换为【3，4，2，1，1】
> 元素 3 和 4 减少为 2，因此数组转换为【2，1，1，1】
> 元素 2 和 1 减少为 1，因此数组转换为【1，1，1】
> 
> **输入:** arr[] = [1，2，3，4，5]
> **输出:** 1
> **解释:**
> 元素 4 和 5 减少为 1，因此数组转换为[1，2，3，1]
> 元素 2 和 3 减少为 1，因此数组转换为[1，1，1]
> 元素 1 被另一个 1 完全破坏，因此数组在末尾是[1]。

**方法:**
为了解决上面提到的问题，我们需要使用[堆数据结构](https://www.geeksforgeeks.org/heap-data-structure/)。使用堆是因为我们只需要每个瞬间的当前最大元素，而不关心其余的元素。

*   根据给定数组的元素创建[最大堆](https://www.geeksforgeeks.org/max-heap-in-java/)。
*   每次迭代都要提取两次[](https://www.geeksforgeeks.org/priority_queuetop-c-stl/)**元素。如果它们的绝对差值不为零，[将把它们的差值推回队列。](https://www.geeksforgeeks.org/priority_queuepush-priority_queuepop-c-stl/)**
*   **继续，直到只剩下一个或没有元素。**
*   **如果没有剩余元素，则打印 0。否则，打印剩余的元素。**

**以下是上述方法的实现:** 

## **C++**

```
// C++ Program to reduce the
// array to almost one element
// by the given operations

#include <bits/stdc++.h>
using namespace std;

// Function to find the remaining
// element of array
int reduceArray(vector<int>& arr)
{
    priority_queue<int> p;

    // Build a priority queue
    // using the array
    for (int i = 0; i < arr.size(); ++i)
        p.push(arr[i]);

    // Continue until the priority
    // queue has one or no elements
    // remaining
    while (p.size() > 1) {

        // Top-most integer from heap
        int y = p.top();
        p.pop();

        // Second integer from heap
        int x = p.top();
        p.pop();

        // Resultant value
        int val = y - x;
        if (val != 0)
            p.push(val);
    }

    // Return 0 if no elements are left
    if (p.size() == 0)
        return 0;

    // Return top value of the heap
    return p.top();
}

// Driver code
int main()
{

    vector<int> arr
        = { 3, 4, 6, 2, 7, 1 };
    cout << reduceArray(arr)
         << "\n";
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to reduce the
// array to almost one element
// by the given operations
import java.util.*;

class GFG{

// Function to find the remaining
// element of array
static int reduceArray(int[] arr)
{
    PriorityQueue<Integer> p = new PriorityQueue<>(
        11, Collections.reverseOrder());

    // Build a priority queue
    // using the array
    for(int i = 0; i < arr.length; ++i)
        p.add(arr[i]);

    // Continue until the priority
    // queue has one or no elements
    // remaining
    while (p.size() > 1)
    {

        // Top-most integer from heap
        int y = p.poll();

        // Second integer from heap
        int x = p.poll();

        // Resultant value
        int val = y - x;
        if (val != 0)
            p.add(val);
    }

    // Return 0 if no elements are left
    if (p.size() == 0)
        return 0;

    // Return top value of the heap
    return p.poll();
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 3, 4, 6, 2, 7, 1 };

    System.out.println(reduceArray(arr));
}
}

// This code is contributed by jrishabh99
```

## **蟒蛇 3**

```
# Python3 program to reduce the
# array to almost one element
# by the given operations

# Function to find the remaining
# element of array
def reduceArray(arr):

    p = []

    # Build a priority queue
    # using the array
    for i in range(len(arr)):
        p.append(arr[i])
    p.sort(reverse = True)

    # Continue until the priority
    # queue has one or no elements
    # remaining
    while (len(p) > 1):

        # Top-most integer from heap
        y = p[0]
        p = p[1:]

        # Second integer from heap
        x = p[0]
        p = p[1:]

        # Resultant value
        val = y - x

        if (val != 0):
            p.append(val)
        p.sort(reverse = True)

    # Return 0 if no elements are left
    if (len(p) == 0):
        return 0

    # Return top value of the heap
    return p[0]

# Driver code
if __name__ == '__main__':

    arr = [ 3, 4, 6, 2, 7, 1 ]

    print(reduceArray(arr))

# This code is contributed by Surendra_Gangwar
```

****Output:** 

```
1
```** 

*****时间复杂度:** O(NlogN)***