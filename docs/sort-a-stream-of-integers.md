# 排序整数流

> 原文:[https://www.geeksforgeeks.org/sort-a-stream-of-integers/](https://www.geeksforgeeks.org/sort-a-stream-of-integers/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)、 **arr[]** ，其元素从左到右必须作为输入的整数流读取，任务是对整数流进行排序并相应地打印。

**示例:**

> **输入:** arr[] = {2，4，1，7，3}
> **输出:** 1 2 3 4 7
> **解释:**
> 流中的第一个元素:2 →排序列表:{2}
> 流中的第二个元素:4 →排序列表:{2，4}
> 流中的第三个元素:1 →排序列表:{1，2，4}
> 流中的第四个元素:7 →排序列表:{1，2，4，7}
> 
> **输入:** arr[] = {4，1，7，6，2}
> **输出:** 1 2 4 6 7
> **解释:**
> 流中的第一个元素:4 →排序列表:{4}
> 流中的第二个元素:1 →排序列表:{1，4}
> 流中的第三个元素:7 →排序列表:{1，4，7}
> 流中的第四个元素:6 →排序列表:{1，4，6，7}

**天真方法:**最简单的方法是<a href = " https://www . geeksforgeeks . org/c-program-to-traverse-a-array/">遍历数组，对于每个数组元素，[线性扫描数组](https://www.geeksforgeeks.org/linear-search/)找到该元素的正确位置，并将其放入数组中。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to sort a stream of integers
void Sort(vector<int>& ans, int num)
{
    // Stores the position of
    // array elements
    int pos = -1;

    // Traverse through the array
    for (int i = 0; i < ans.size(); i++) {

        // If any element is found to be
        // greater than the current element
        if (ans[i] >= num) {
            pos = i;
            break;
        }
    }

    // If an element > num is not present
    if (pos == -1)
        ans.push_back(num);

    // Otherwise, place the number
    // at its right position
    else
        ans.insert(ans.begin() + pos, num);
}

// Function to print the sorted stream of integers
void sortStream(int arr[], int N)
{
    // Stores the sorted stream of integers
    vector<int> ans;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Function Call
        Sort(ans, arr[i]);

        // Print the array after
        // every insertion
        for (int i = 0; i < ans.size(); i++) {
            cout << ans[i] << " ";
        }
        cout << endl;
    }
}

// Driver Code
int main()
{
    int arr[] = { 4, 1, 7, 6, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);

    sortStream(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to sort a stream of integers
static void Sort(Vector<Integer> ans, int num)
{

    // Stores the position of
    // array elements
    int pos = -1;

    // Traverse through the array
    for(int i = 0; i < ans.size(); i++)
    {

        // If any element is found to be
        // greater than the current element
        if (ans.get(i) >= num)
        {
            pos = i;
            break;
        }
    }

    // If an element > num is not present
    if (pos == -1)
        ans.add(num);

    // Otherwise, place the number
    // at its right position
    else
        ans.add(pos, num);
}

// Function to print the sorted stream of integers
static void sortStream(int arr[], int N)
{

    // Stores the sorted stream of integers
    Vector<Integer> ans = new Vector<Integer>();

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Function Call
        Sort(ans, arr[i]);

        // Print the array after
        // every insertion
        for(int j = 0; j < ans.size(); j++)
        {
            System.out.print(ans.get(j) + " ");
        }
        System.out.println();
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 4, 1, 7, 6, 2 };
    int N = arr.length;

    sortStream(arr, N);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to sort a stream of integers
def Sort(ans, num):

    # Stores the position of
    # array elements
    pos = -1;

    # Traverse through the array
    for  i in range(len(ans)):

        # If any element is found to be
        # greater than the current element
        if (ans[i] >= num):
            pos = i;
            break;

    # If an element > num is not present
    if (pos == -1):
        ans.append(num);

    # Otherwise, place the number
    # at its right position
    else:
        ans.insert(pos,num);
    return ans;

# Function to print the sorted stream of integers
def sortStream(arr, N):

    # Stores the sorted stream of integers
    ans = list();

    # Traverse the array
    for i in range(N):

        # Function Call
        ans = Sort(ans, arr[i]);

        # Print the array after
        # every insertion
        for j in range(len(ans)):
            print(ans[j], end = " ");

        print();

# Driver Code
if __name__ == '__main__':
    arr = [4, 1, 7, 6, 2];
    N = len(arr);

    sortStream(arr, N);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to sort a stream of integers
static void Sort(List<int> ans, int num)
{

    // Stores the position of
    // array elements
    int pos = -1;

    // Traverse through the array
    for(int i = 0; i < ans.Count; i++)
    {

        // If any element is found to be
        // greater than the current element
        if (ans[i] >= num)
        {
            pos = i;
            break;
        }
    }

    // If an element > num is not present
    if (pos == -1)
        ans.Add(num);

    // Otherwise, place the number
    // at its right position
    else
        ans.Insert(pos, num);
}

// Function to print the sorted stream of integers
static void sortStream(int []arr, int N)
{

    // Stores the sorted stream of integers
    List<int> ans = new List<int>();

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Function Call
        Sort(ans, arr[i]);

        // Print the array after
        // every insertion
        for(int j = 0; j < ans.Count; j++)
        {
            Console.Write(ans[j] + " ");
        }
        Console.WriteLine();
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 4, 1, 7, 6, 2 };
    int N = arr.Length;
    sortStream(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

**Output:** 

```
4 
1 4 
1 4 7 
1 4 6 7 
1 2 4 6 7
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效方法:**对上述方法进行优化，思路是用一个[二分搜索法](https://www.geeksforgeeks.org/binary-search/)找到每个元素在排序列表中的正确位置。按照以下步骤解决问题:

*   初始化一个数组**和**来存储最终排序的数字流。
*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**作为一个数字流，并执行以下步骤:
    *   如果阵列 **ans** 为空，将**arr【I】**推至 **ans** 。
    *   否则，使用[下界()](https://www.geeksforgeeks.org/lower_bound-in-cpp/)在已经排序的数组**ans【】**中找到 **arr[i]** 的正确位置，并将 **arr[i]** 推到其正确位置。
*   完成以上步骤后，打印数组 **ans[]** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to sort a stream of integers
void Sort(vector<int>& ans, int num)
{
    // If the element is greater than
    // all the elements in the sorted
    // array, then it push at the back
    if (lower_bound(ans.begin(),
                    ans.end(), num)
        == ans.end()) {
        ans.push_back(num);
    }

    // Otherwise, find its correct position
    else {
        int pos = lower_bound(ans.begin(),
                              ans.end(),
                              num)
                  - ans.begin();

        // Insert the element
        ans.insert(ans.begin() + pos,
                   num);
    }
}

// Function to print the sorted stream of integers
void sortStream(int arr[], int N)
{
    // Stores the sorted stream of integers
    vector<int> ans;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Function Call
        Sort(ans, arr[i]);

        // Print the array after
        // every insertion
        for (int i = 0; i < ans.size(); i++) {
            cout << ans[i] << " ";
        }
        cout << endl;
    }
}

// Driver Code
int main()
{
    int arr[] = { 4, 1, 7, 6, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);

    sortStream(arr, N);

    return 0;
}
```

**Output:** 

```
4 
1 4 
1 4 7 
1 4 6 7 
1 2 4 6 7
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*