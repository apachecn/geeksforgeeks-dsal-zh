# 对数组进行排序，使相邻元素的绝对差值按递增顺序排列

> 原文:[https://www . geeksforgeeks . org/sort-array-so-相邻元素的绝对差按递增顺序排列/](https://www.geeksforgeeks.org/sort-array-such-that-absolute-difference-of-adjacent-elements-is-in-increasing-order/)

给定一个长度为 N 的未排序数组，任务是对数组进行排序，使得所有 0 的**ABS(a[I]-a[I+1])<= ABS(a[I+1]-a[I+2])**即 ABS(a[0]-a[1])<= ABS(a[1]-a[2])<= ABS(a[2]-a[3])等等。
**例:**

```
Input:  arr[] = {7, 4, 9, 9, -1, 9}
Output:  {9, 7, 9, 4, 9, -1}
Explanation:
For first two elements the difference is abs(9-7)=2
For next two elements the difference is abs(7-9)=2
For next two elements the difference is abs(9-4)=5
For next two elements the difference is abs(7-4)=3
For next two elements the difference is abs(4-(-1))=5
Hence, difference array is 0, 0, 2, 3, 5.

Input: arr[] = {1, 4, 6, 7} 
Output: {6, 4, 7, 1} 
Explanation:
For first two elements the difference is abs(6-4)=2
For next two elements the difference is abs(4-7)=3
For next two elements the difference is abs(7-1)=6
Hence, difference array is 2, 3, 6.
```

**方法:**
为了解决上面提到的问题，我们按照升序对给定的未排序数组进行排序。然后运行从 i = 1 到 i < n/2 的循环，并分别从前半部分和后半部分交替地在**堆栈**中推送元素，即推送一次[i]和一次[n-i-1],直到整个数组元素被推入堆栈。
对问题的主要观察是检查给定数组的长度是否为奇数，然后在索引 n/2 处额外推送元素，以便让数组的所有元素都在堆栈中。然后遍历整个堆栈，直到堆栈不为空，然后从堆栈中弹出元素并将其打印出来。
下面是讨论的方法的实现:

## C++

```
// C++ implementation to Sort a given
// unsorted array of length n
// according to the given condition
#include <bits/stdc++.h>
using namespace std;

// Function
void solve(int a[], int n)
{

    // sort the array in ascending order
    sort(a, a + n);

    // declare a stack data structure
    stack<int> st;

    // run a loop from i=0 to i<n/2 and
    // push elements alternatively to stack
    for (int i = 0; i < n / 2; i++) {

        // push elements from
        // first half of array
        st.push(a[i]);

        // push elements from
        // second half of the array
        st.push(a[n - i - 1]);
    }

    // check if array has odd length,
    // then push a[n/2] to the stack
    if (n % 2 == 1)

        st.push(a[n / 2]);

    // loop until stack is not empty)
    while (!st.empty()) {

        int x = st.top();

        printf("%d ", x);

        // pop the topmost
        // element from the stack
        st.pop();
    }
}

// Driver code
int main()
{

    // declaration of unsorted array
    int a[] = { 7, 4, 9, 9, -1, 9 };

    // given size of unsorted array
    int n = sizeof(a) / sizeof(a[0]);

    solve(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to Sort a given
// unsorted array of length n
// according to the given condition
import java.util.*;
class GFG{

// Function
static void solve(int a[], int n)
{

    // sort the array in ascending order
    Arrays.sort(a);

    // declare a stack data structure
    Stack<Integer> st = new Stack<Integer>();

    // run a loop from i=0 to i<n/2 and
    // push elements alternatively to stack
    for (int i = 0; i < n / 2; i++)
    {

        // push elements from
        // first half of array
        st.add(a[i]);

        // push elements from
        // second half of the array
        st.add(a[n - i - 1]);
    }

    // check if array has odd length,
    // then push a[n/2] to the stack
    if (n % 2 == 1)

        st.add(a[n / 2]);

    // loop until stack is not empty)
    while (!st.isEmpty())
    {
        int x = st.peek();
        System.out.printf("%d ", x);

        // pop the topmost
        // element from the stack
        st.pop();
    }
}

// Driver code
public static void main(String[] args)
{

    // declaration of unsorted array
    int a[] = { 7, 4, 9, 9, -1, 9 };

    // given size of unsorted array
    int n = a.length;

    solve(a, n);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 implementation to sort a
# given unsorted array of length n
# according to the given condition

# Function
def solve(a, n):

    # Sort the array in ascending
    # order
    a.sort()

    # Declare a list used as a
    # stack data structure
    st = []

    # Run a loop from i=0 to i<n/2 and
    # push elements alternatively to stack
    for i in range(n // 2):

        # Push elements from
        # first half of array
        st.append(a[i])

        # Push elements from
        # second half of the array
        st.append(a[n - i - 1])

    # Check if array has odd length,
    # then push a[n/2] to the stack
    if(n % 2 == 1):

        st.append(a[n // 2])

    # Loop until stack is not empty
    while(st != []):
        x = st[-1]
        print(x, end = " ")

        # Pop the topmost element
        # from the stack
        st.pop()

# Driver code
if __name__ == '__main__':

    # Declaration of unsorted array
    a = [ 7, 4, 9, 9, -1, 9 ]

    # Given size of unsorted array
    n = len(a)

    solve(a, n)

# This code is contributed by Shivam Singh
```

## C#

```
// C# implementation to Sort a given
// unsorted array of length n
// according to the given condition
using System;
using System.Collections;

class GFG{

// Function
static void solve(int[] a, int n)
{

    // Sort the array in ascending order
    Array.Sort(a);

    // Declare a stack data structure
    Stack st = new Stack();

    // Run a loop from i=0 to i<n/2 and
    // push elements alternatively to stack
    for(int i = 0; i < n / 2; i++)
    {

        // Push elements from
        // first half of array
        st.Push(a[i]);

        // Push elements from
        // second half of the array
        st.Push(a[n - i - 1]);
    }

    // Check if array has odd length,
    // then push a[n/2] to the stack
    if (n % 2 == 1)
        st.Push(a[n / 2]);

    // Loop until stack is not empty)
    while (st.Count != 0)
    {
        Console.Write(st.Peek() + " ");

        // Pop the topmost
        // element from the stack
        st.Pop();
    }
}

// Driver code
public static void Main(String[] args)
{

    // Declaration of unsorted array
    int[] a = { 7, 4, 9, 9, -1, 9 };

    // Given size of unsorted array
    int n = a.Length;

    solve(a, n);
}
}

// This code is contributed by jrishabh99
```

## java 描述语言

```
<script>
    // Javascript implementation to Sort a given
    // unsorted array of length n
    // according to the given condition

    // Function
    function solve(a, n)
    {

        // Sort the array in ascending order
        a.sort(function(a, b){return a - b});

        // Declare a stack data structure
        let st = [];

        // Run a loop from i=0 to i<n/2 and
        // push elements alternatively to stack
        for(let i = 0; i < parseInt(n / 2, 10); i++)
        {

            // Push elements from
            // first half of array
            st.push(a[i]);

            // Push elements from
            // second half of the array
            st.push(a[n - i - 1]);
        }

        // Check if array has odd length,
        // then push a[n/2] to the stack
        if (n % 2 == 1)
            st.push(a[parseInt(n / 2, 10)]);

        // Loop until stack is not empty)
        while (st.length != 0)
        {
            document.write(st[st.length - 1] + " ");

            // Pop the topmost
            // element from the stack
            st.pop();
        }
    }

    // Declaration of unsorted array
    let a = [ 7, 4, 9, 9, -1, 9 ];

    // Given size of unsorted array
    let n = a.length;

    solve(a, n);

// This code is contributed by vaibhavrabadiya117.
</script>
```

**Output:** 

```
9 7 9 4 9 -1
```