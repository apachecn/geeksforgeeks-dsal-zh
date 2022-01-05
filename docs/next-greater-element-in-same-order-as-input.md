# 与输入相同顺序的下一个较大元素

> 原文:[https://www . geesforgeks . org/next-大元同序输入/](https://www.geeksforgeeks.org/next-greater-element-in-same-order-as-input/)

给定一个数组，为每个元素打印下一个更大的元素(NGE)。元素 x 的下一个较大元素是数组中 x 右侧的第一个较大元素。不存在更大元素的元素，将下一个更大的元素视为-1。下一个较大的元素应该按照与输入数组相同的顺序打印。

**示例:**

> 输入:arr[] = [4，5，2，25}
> 输出:5 25 25 -1
> 
> 输入:arr[] = [4，5，2，25，10}
> 输出:5 25 25 -1 -1

我们在这里讨论了一个解决方案，它不打印相同的订单。这里我们从最右边的元素开始遍历数组。

1.  在这种方法中，我们已经开始从最后一个元素(第 n 个)迭代到第一个(第 1 个)元素
    的好处是，当我们到达某个索引时，他的下一个更大的元素将已经在堆栈中，并且我们可以在相同的索引处直接获得这个元素。
2.  在达到某个索引后，我们将弹出堆栈，直到我们从当前元素中获得最大的元素，该元素将是当前元素的答案
3.  如果堆栈在执行弹出操作时变空，那么答案将是-1
    ，然后我们将答案存储在当前索引的数组中。

下面是上述方法的实现:

## C++

```
// A Stack based C++ program to find next
// greater element for all array elements
// in same order as input.
#include <bits/stdc++.h>
using namespace std;

/* prints element and NGE pair for all 
elements of arr[] of size n */
void printNGE(int arr[], int n)
{
    stack<int> s;

    int arr1[n];

    // iterating from n-1 to 0
    for (int i = n - 1; i >= 0; i--)
    {
        /*We will pop till we get the
        greater element on top or stack gets empty*/
        while (!s.empty() && s.top() <= arr[i])
            s.pop();

        /*if stack gots empty means there
        is no element on right which is greater
        than the current element.
        if not empty then the next greater
        element is on top of stack*/
        if (s.empty())
            arr1[i] = -1;        
        else
            arr1[i] = s.top();       

        s.push(arr[i]);
    }

    for (int i = 0; i < n; i++)
        cout << arr[i] << " ---> " << arr1[i] << endl;
}

/* Driver program to test above functions */
int main()
{
    int arr[] = { 11, 13, 21, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);
    printNGE(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Stack based Java program to find next
// greater element for all array elements
// in same order as input.
import java.util.*;
class GfG {

/* prints element and NGE pair for all
elements of arr[] of size n */
static void printNGE(int arr[], int n)
{
    Stack<Integer> s = new Stack<Integer>();

    int arr1[] = new int[n];

    // iterating from n-1 to 0
    for (int i = n - 1; i >= 0; i--)
    {
        /*We will pop till we get the
        greater element on top or stack gets empty*/
        while (!s.isEmpty() && s.peek() <= arr[i])
            s.pop();

        /*if stack gots empty means there
        is no element on right which is greater
        than the current element.
        if not empty then the next greater
        element is on top of stack*/
        if (s.empty())
            arr1[i] = -1;        
        else
            arr1[i] = s.peek();        

        s.push(arr[i]);
    }

    for (int i = 0; i < n; i++)
        System.out.println(arr[i] + " ---> " + arr1[i]);
}

/* Driver program to test above functions */
public static void main(String[] args)
{
    int arr[] = { 11, 13, 21, 3 };
    int n = arr.length;
    printNGE(arr, n);
}
}
```

## 蟒蛇 3

```
# A Stack based Python3 program to find next
# greater element for all array elements
# in same order as input.

# prints element and NGE pair for all
# elements of arr[] of size n
def printNGE(arr, n):

    s = list()

    arr1 = [0 for i in range(n)]

    # iterating from n-1 to 0
    for i in range(n - 1, -1, -1):

        # We will pop till we get the greater 
        # element on top or stack gets empty
        while (len(s) > 0 and s[-1] <= arr[i]):
            s.pop()

        # if stack gots empty means there
        # is no element on right which is
        # greater than the current element.
        # if not empty then the next greater
        # element is on top of stack
        if (len(s) == 0):
            arr1[i] = -1       
        else:
            arr1[i] = s[-1]    

        s.append(arr[i])

    for i in range(n):
        print(arr[i], " ---> ", arr1[i] )

# Driver Code
arr = [ 11, 13, 21, 3 ]
n = len(arr)
printNGE(arr, n)

# This code is contributed by Mohit kumar 29
```

## C#

```
// A Stack based C# program to find next
// greater element for all array elements
// in same order as input.
using System;
using System.Collections.Generic;

class GFG
{

/* prints element and NGE pair for all
elements of arr[] of size n */
static void printNGE(int []arr, int n)
{
    Stack<int> s = new Stack<int>();

    int []arr1 = new int[n];

    // iterating from n-1 to 0
    for (int i = n - 1; i >= 0; i--)
    {
        /*We will pop till we get the
        greater element on top or stack gets empty*/
        while (s.Count != 0 && s.Peek() <= arr[i])
            s.Pop();

        /*if stack gots empty means there
        is no element on right which is greater
        than the current element.
        if not empty then the next greater
        element is on top of stack*/
        if (s.Count == 0)
            arr1[i] = -1;        
        else
            arr1[i] = s.Peek();        

        s.Push(arr[i]);
    }

    for (int i = 0; i < n; i++)
        Console.WriteLine(arr[i] + " ---> " +
                          arr1[i]);
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 11, 13, 21, 3 };
    int n = arr.Length;
    printNGE(arr, n);
}
}

// This code is contributed by Ajay Kumar
```

## java 描述语言

```
<script>

// A Stack based Javascript program to find next
// greater element for all array elements
// in same order as input.

// prints element and NGE pair for all
// elements of arr[] of size n
function printNGE(arr, n)
{
    let s = [];
    let arr1 = new Array(n);

    // Iterating from n-1 to 0
    for (let i = n - 1; i >= 0; i--)
    {

        // We will pop till we get the
        // greater element on top or
        // stack gets empty
        while (!s.length == 0 &&
              s[s.length - 1] <= arr[i])
            s.pop();

        // If stack gots empty means there
        // is no element on right which is greater
        // than the current element.
        // if not empty then the next greater
        // element is on top of stack
        if (s.length == 0)
            arr1[i] = -1;        
        else
            arr1[i] = s[s.length - 1];        

        s.push(arr[i]);
    }
    for(let i = 0; i < n; i++)
        document.write(arr[i] + " ---> " +
                      arr1[i] + "<br>");
}

// Driver code
let arr = [ 11, 13, 21, 3 ];
let n = arr.length;

printNGE(arr, n);

// This code is contributed by patel2127

</script>
```

**输出:**

```
11 -- 13
13 -- 21
21 -- -1
3 -- -1
```

**时间复杂度:** O(n)
**辅助空间:** O(n)如果要按照输入的相反顺序打印每个元素的下一个较大值(表示首先打印最后一个元素，然后是第二个最后一个元素，以此类推，直到第一个元素)