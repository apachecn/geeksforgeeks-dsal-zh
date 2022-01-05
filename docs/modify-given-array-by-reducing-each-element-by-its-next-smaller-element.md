# 修改给定的数组，将每个元素减少下一个较小的元素

> 原文:[https://www . geesforgeks . org/modify-给定数组-按下一个更小的元素逐个减少每个元素/](https://www.geeksforgeeks.org/modify-given-array-by-reducing-each-element-by-its-next-smaller-element/)

给定一个长度为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是修改给定数组，如果可能的话，用下一个更小的元素替换给定数组的每个元素。打印修改后的数组作为所需答案。

**示例:**

> **输入:** arr[] = {8，4，6，2，3}
> **输出:** 4 2 4 2 3
> **解释:**操作可执行如下:
> 
> *   对于 arr[0]，arr[1]是下一个较小的元素。
> *   对于 arr[1]，arr[3]是下一个较小的元素。
> *   对于 arr[2]，arr[3]是下一个较小的元素。
> *   对于 arr[3]，其后没有更小的元素。
> *   对于 arr[4]，其后没有更小的元素。
> 
> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 1 2 3 4 5

**天真方法:**最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个元素，遍历它后面的剩余元素，检查是否有更小的元素存在。如果找到，将该元素减少第一个获得的较小元素。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print the final array
// after reducing each array element
// by its next smaller element
void printFinalPrices(vector<int>& arr)
{
    // Stores the resultant array
    vector<int> ans;

    // Traverse the array
    for (int i = 0; i < arr.size(); i++) {
        int flag = 1;
        for (int j = i + 1; j < arr.size(); j++) {

            // If a smaller element is found
            if (arr[j] <= arr[i]) {

                // Reduce current element by
                // next smaller element
                ans.push_back(arr[i] - arr[j]);
                flag = 0;
                break;
            }
        }

        // If no smaller element is found
        if (flag == 1)
            ans.push_back(arr[i]);
    }

    // Print the answer
    for (int i = 0; i < ans.size(); i++)
        cout << ans[i] << " ";
}

// Driver Code
int main()
{
    // Given array
    vector<int> arr = { 8, 4, 6, 2, 3 };

    // Function Call
    printFinalPrices(arr);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to print the final array
// after reducing each array element
// by its next smaller element
static void printFinalPrices(int[] arr)
{

    // Stores the resultant array
    ArrayList<Integer> ans = new ArrayList<Integer>();

    // Traverse the array
    for(int i = 0; i < arr.length; i++)
    {
        int flag = 1;
        for(int j = i + 1; j < arr.length; j++)
        {

            // If a smaller element is found
            if (arr[j] <= arr[i])
            {

                // Reduce current element by
                // next smaller element
                ans.add(arr[i] - arr[j]);
                flag = 0;
                break;
            }
        }

        // If no smaller element is found
        if (flag == 1)
            ans.add(arr[i]);
    }

    // Print the answer
    for(int i = 0; i < ans.size(); i++)
        System.out.print(ans.get(i) + " ");
} 

// Driver Code
public static void main(String[] args)
{

    // Given array
    int[] arr = { 8, 4, 6, 2, 3 };

    // Function Call
    printFinalPrices(arr);
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print the final array
# after reducing each array element
# by its next smaller element
def printFinalarr(arr):

  # Stores resultant array
    ans = []

    # Traverse the given array
    for i in range(len(arr)):
        flag = 1
        for j in range(i + 1, len(arr)):

            # If a smaller element is found
            if arr[j] <= arr[i]:

                # Reduce current element by
                # next smaller element
                ans.append(arr[i] - arr[j])
                flag = 0
                break
        if flag:

            # If no smaller element is found
            ans.append(arr[i])

    # Print the final array
    for k in range(len(ans)):
        print(ans[k], end =' ')

# Driver Code
if __name__ == '__main__':

  # Given array
    arr = [8, 4, 6, 2, 3]

  # Function call
    printFinalarr(arr)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to print the final array
// after reducing each array element
// by its next smaller element
static void printFinalPrices(int[] arr)
{

    // Stores the resultant array
    List<int> ans = new List<int>();

    // Traverse the array
    for(int i = 0; i < arr.Length; i++)
    {
        int flag = 1;
        for(int j = i + 1; j < arr.Length; j++)
        {

            // If a smaller element is found
            if (arr[j] <= arr[i])
            {

                // Reduce current element by
                // next smaller element
                ans.Add(arr[i] - arr[j]);
                flag = 0;
                break;
            }
        }

        // If no smaller element is found
        if (flag == 1)
            ans.Add(arr[i]);
    }

    // Print the answer
    for(int i = 0; i < ans.Count; i++)
        Console.Write(ans[i] + " ");
} 

// Driver code
static void Main()
{

    // Given array
    int[] arr = { 8, 4, 6, 2, 3 };

    // Function Call
    printFinalPrices(arr);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
// Js program for the above approach
// Function to print the final array
// after reducing each array element
// by its next smaller element
function printFinalPrices( arr)
{
    // Stores the resultant array
    let ans = [];

    // Traverse the array
    for (let i = 0; i < arr.length; i++) {
        let flag = 1;
        for (let j = i + 1; j < arr.length; j++) {

            // If a smaller element is found
            if (arr[j] <= arr[i]) {

                // Reduce current element by
                // next smaller element
                ans.push(arr[i] - arr[j]);
                flag = 0;
                break;
            }
        }

        // If no smaller element is found
        if (flag == 1)
            ans.push(arr[i]);
    }

    // Print the answer
    for (let i = 0; i < ans.length; i++)
        document.write(ans[i], " ");
}

// Driver Code
// Given array
    let arr = [ 8, 4, 6, 2, 3 ];

    // Function Call
    printFinalPrices(arr);

</script>
```

**Output:** 

```
4 2 4 2 3
```

**高效方法:**优化上述方法，思路是使用[栈数据结构](https://www.geeksforgeeks.org/stack-data-structure/)。按照以下步骤解决问题:

1.  初始化一个[堆栈](https://www.geeksforgeeks.org/stack-data-structure/) 和一个大小为 **N** 的数组 **ans[]** ，以存储结果数组。
2.  [在索引**I = N–1 至 0** 上遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。
3.  [如果堆栈为空](https://www.geeksforgeeks.org/stack-empty-and-stack-size-in-c-stl/)，[将当前元素**arr【I】**推至堆栈顶部](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/)。
4.  否则，如果当前元素大于堆栈顶部[的元素](https://www.geeksforgeeks.org/stack-top-c-stl/)，[将其推入堆栈](https://www.geeksforgeeks.org/stack-push-method-in-java/)，然后[从堆栈](https://www.geeksforgeeks.org/stack-removeint-method-in-java-with-example/)中移除元素，直到堆栈变空或找到小于或等于**arr【I】**的元素。之后，如果堆栈不是空的，设置**ans[I]= arr[I]–堆栈的顶部元素**，然后将其从堆栈中移除。
5.  否则，从堆栈中移除顶部元素，并将 **ans[i]** 设置为等于堆栈中的顶部元素，然后将其从堆栈中移除。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the final array
// after reducing each array element
// by its next smaller element
void printFinalPrices(vector<int>& arr)
{

    // Initialize stack
    stack<int> minStk;

    // Array size
    int n = arr.size();

    // To store the corresponding element
    vector<int> reduce(n, 0);
    for (int i = n - 1; i >= 0; i--) {

        // If stack is not empty
        if (!minStk.empty()) {

            // If top element is smaller
            // than the current element
            if (minStk.top() <= arr[i]) {
                reduce[i] = minStk.top();
            }
            else {

                // Keep popping until stack is empty
                // or top element is greater than
                // the current element
                while (!minStk.empty()
                       && (minStk.top() > arr[i])) {
                    minStk.pop();
                }

                // If stack is not empty
                if (!minStk.empty()) {
                    reduce[i] = minStk.top();
                }
            }
        }

        // Push current element
        minStk.push(arr[i]);
    }

    // Print the final array
    for (int i = 0; i < n; i++)
        cout << arr[i] - reduce[i] << " ";
}

// Driver Code
int main()
{

    // Given array
    vector<int> arr = { 8, 4, 6, 2, 3 };

    // Function call
    printFinalPrices(arr);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to print the final array
// after reducing each array element
// by its next smaller element
static void printFinalPrices(int[] arr)
{

    // Initialize stack
    Stack<Integer> minStk = new Stack<>();

    // Array size
    int n = arr.length;

    // To store the corresponding element
    int[] reduce = new int[n];
    for(int i = n - 1; i >= 0; i--)
    {

        // If stack is not empty
        if (!minStk.isEmpty())
        {

            // If top element is smaller
            // than the current element
            if (minStk.peek() <= arr[i])
            {
                reduce[i] = minStk.peek();
            }
            else
            {

                // Keep popping until stack is empty
                // or top element is greater than
                // the current element
                while (!minStk.isEmpty() &&
                       (minStk.peek() > arr[i]))
                {
                    minStk.pop();
                }

                // If stack is not empty
                if (!minStk.isEmpty())
                {
                    reduce[i] = minStk.peek();
                }
            }
        }

        // Push current element
        minStk.add(arr[i]);
    }

    // Print the final array
    for(int i = 0; i < n; i++)
        System.out.print(arr[i] - reduce[i] + " ");
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int[] arr = { 8, 4, 6, 2, 3 };

    // Function call
    printFinalPrices(arr);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print the final array
# after reducing each array element
# by its next smaller element
def printFinalPrices(arr):

  # Initialize stack
    minStk = []

    # To store the corresponding element
    reduce = [0] * len(arr)
    for i in range(len(arr) - 1, -1, -1):

       # If stack is not empty
        if minStk:

            # If top element is smaller
            # than the current element
            if minStk[-1] <= arr[i]:
                reduce[i] = minStk[-1]
            else:

              # Keep popping until stack is empty
                # or top element is greater than
                # the current element
                while minStk and minStk[-1] > arr[i]:
                    minStk.pop()

                if minStk:

                  # Corresponding elements
                    reduce[i] = minStk[-1]

        # Push current element
        minStk.append(arr[i])

    # Final array
    for i in range(len(arr)):
        print(arr[i] - reduce[i], end =' ')

# Driver Code
if __name__ == '__main__':

  # Given array
    arr = [8, 4, 6, 2, 3]

   # Function Call
    printFinalPrices(arr)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to print the readonly array
// after reducing each array element
// by its next smaller element
static void printFinalPrices(int[] arr)
{

    // Initialize stack
    Stack<int> minStk = new Stack<int>();

    // Array size
    int n = arr.Length;

    // To store the corresponding element
    int[] reduce = new int[n];
    for(int i = n - 1; i >= 0; i--)
    {

        // If stack is not empty
        if (minStk.Count != 0)
        {

            // If top element is smaller
            // than the current element
            if (minStk.Peek() <= arr[i])
            {
                reduce[i] = minStk.Peek();
            }
            else
            {

                // Keep popping until stack is empty
                // or top element is greater than
                // the current element
                while (minStk.Count != 0 &&
                       (minStk.Peek() > arr[i]))
                {
                    minStk.Pop();
                }

                // If stack is not empty
                if (minStk.Count != 0)
                {
                    reduce[i] = minStk.Peek();
                }
            }
        }

        // Push current element
        minStk.Push(arr[i]);
    }

    // Print the readonly array
    for(int i = 0; i < n; i++)
        Console.Write(arr[i] - reduce[i] + " ");
}

// Driver Code
public static void Main(String[] args)
{

    // Given array
    int[] arr = { 8, 4, 6, 2, 3 };

    // Function call
    printFinalPrices(arr);
}
}

// This code contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to print the final array
// after reducing each array element
// by its next smaller element
function printFinalPrices(arr)
{

    // Initialize stack
    var minStk = []

    // Array size
    var n = arr.length;
    var i;

    // To store the corresponding element
    var reduce = Array(n).fill(0);
    for (i = n - 1; i >= 0; i--) {

        // If stack is not empty
        if (minStk.length>0) {

            // If top element is smaller
            // than the current element
            if (minStk[minStk.length-1] <= arr[i]) {
                reduce[i] = minStk[minStk.length-1];
            }
            else {

                // Keep popping until stack is empty
                // or top element is greater than
                // the current element
                while (minStk.length>0
                       && (minStk[minStk.length-1] > arr[i])) {
                    minStk.pop();
                }

                // If stack is not empty
                if (minStk.length>0) {
                    reduce[i] = minStk[minStk.length-1];
                }
            }
        }

        // Push current element
        minStk.push(arr[i]);
    }

    // Print the final array
    for (i = 0; i < n; i++)
        document.write(arr[i] - reduce[i] + " ");
}

// Driver Code

    // Given array
    var arr = [8, 4, 6, 2, 3];

    // Function call
    printFinalPrices(arr);

// This code is contributed by ipg2016107.
</script>
```

**Output:** 

```
4 2 4 2 3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)