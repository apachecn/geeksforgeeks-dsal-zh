# 频率大于其他元素的元素的最小子阵列

> 原文:[https://www . geeksforgeeks . org/最小子阵列具有频率大于其他元素的元素/](https://www.geeksforgeeks.org/smallest-subarray-having-an-element-with-frequency-greater-than-that-of-other-elements/)

给定一个正整数数组 **arr** ，任务是找到长度大于 1 的最小长度子数组，其中一个元素出现的次数比任何其他元素都多。

**示例:**

> **输入:** arr[] = {2，3，2，4，5}
> **输出:** 2 3 2
> **解释:**子阵列{2，3，2}的元素 2 出现的次数比子阵列中的任何其他元素都多。
> 
> **输入:** arr[] = {2，3，4，5，2，6，7，6}
> **输出:** 6 7 6
> **解释:**子阵列{2，3，4，5，2}和{6，7，6}包含的元素出现的次数比其中的任何其他元素都多。但是子阵列{6，7，6}的长度最小。

**天真方法:**解决问题的天真方法可以是找到所有子阵中有一个元素满足给定条件的子阵，然后找到所有那些子阵中的最小值。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效方法:**问题可以简化为找出如果有任何元素在一个子阵列中出现两次，那么它可以是一个潜在的答案。因为这种子阵列的最小长度可以是两个相同元件之间的最小距离

其思想是使用一个额外的数组来维护给定数组中元素的最后一次出现。然后找出元素最后一次出现的位置和当前位置之间的距离，并找出所有这些长度的最小值。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find subarray
void FindSubarray(int arr[], int n)
{
    // If the array has only one element,
    // then there is no answer.
    if (n == 1) {
        cout << "No such subarray!"
             << endl;
    }

    // Array to store the last occurrences
    // of the elements of the array.
    int vis[n + 1];
    memset(vis, -1, sizeof(vis));
    vis[arr[0]] = 0;

    // To maintain the length
    int len = INT_MAX, flag = 0;

    // Variables to store
    // start and end indices
    int start, end;

    for (int i = 1; i < n; i++) {
        int t = arr[i];

        // Check if element is occurring
        // for the second time in the array
        if (vis[t] != -1) {
            // Find distance between last
            // and current index
            // of the element.
            int distance = i - vis[t] + 1;

            // If the current distance
            // is less then len
            // update len and
            // set 'start' and 'end'
            if (distance < len) {
                len = distance;
                start = vis[t];
                end = i;
            }
            flag = 1;
        }

        // Set the last occurrence
        // of current element to be 'i'.
        vis[t] = i;
    }

    // If flag is equal to 0,
    // it means there is no answer.
    if (flag == 0)
        cout << "No such subarray!"
             << endl;
    else {
        for (int i = start; i <= end; i++)
            cout << arr[i] << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 2, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    FindSubarray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find subarray
public static void FindSubarray(int[] arr,
                                int n)
{

    // If the array has only one element,
    // then there is no answer.
    if (n == 1)
    {
        System.out.println("No such subarray!");
    }

    // Array to store the last occurrences
    // of the elements of the array.
    int[] vis = new int[n + 1];
    Arrays.fill(vis, -1);
    vis[arr[0]] = 0;

    // To maintain the length
    int len = Integer.MAX_VALUE, flag = 0;

    // Variables to store
    // start and end indices
    int start = 0, end = 0;

    for(int i = 1; i < n; i++)
    {
        int t = arr[i];

        // Check if element is occurring
        // for the second time in the array
        if (vis[t] != -1)
        {

            // Find distance between last
            // and current index
            // of the element.
            int distance = i - vis[t] + 1;

            // If the current distance
            // is less then len
            // update len and
            // set 'start' and 'end'
            if (distance < len)
            {
                len = distance;
                start = vis[t];
                end = i;
            }
            flag = 1;
        }

        // Set the last occurrence
        // of current element to be 'i'.
        vis[t] = i;
    }

    // If flag is equal to 0,
    // it means there is no answer.
    if (flag == 0)
        System.out.println("No such subarray!");

    else
    {
        for(int i = start; i <= end; i++)
            System.out.print(arr[i] + " ");
    }
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 3, 2, 4, 5 };
    int n = arr.length;

    FindSubarray(arr, n);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to find subarray
def FindSubarray(arr, n):

    # If the array has only one element,
    # then there is no answer.
    if (n == 1):
        print("No such subarray!")

    # Array to store the last occurrences
    # of the elements of the array.
    vis = [-1] * (n + 1)
    vis[arr[0]] = 0

    # To maintain the length
    length = sys.maxsize
    flag = 0

    for i in range(1, n):
        t = arr[i]

        # Check if element is occurring
        # for the second time in the array
        if (vis[t] != -1):

            # Find distance between last
            # and current index
            # of the element.
            distance = i - vis[t] + 1

            # If the current distance
            # is less then len
            # update len and
            # set 'start' and 'end'
            if (distance < length):
                length = distance
                start = vis[t]
                end = i

            flag = 1

        # Set the last occurrence
        # of current element to be 'i'.
        vis[t] = i

    # If flag is equal to 0,
    # it means there is no answer.
    if (flag == 0):
        print("No such subarray!")
    else:
        for i in range(start, end + 1):
            print(arr[i], end = " ")

# Driver Code
if __name__ == "__main__":

    arr = [ 2, 3, 2, 4, 5 ]
    n = len(arr)

    FindSubarray(arr, n)

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to find subarray
public static void FindSubarray(int[] arr,
                                int n)
{

    // If the array has only one element,
    // then there is no answer.
    if (n == 1)
    {
        Console.WriteLine("No such subarray!");
    }

    // Array to store the last occurrences
    // of the elements of the array.
    int[] vis = new int[n + 1];
    for(int i = 0; i < n + 1; i++)
        vis[i] = -1;
    vis[arr[0]] = 0;

    // To maintain the length
    int len = int.MaxValue, flag = 0;

    // Variables to store
    // start and end indices
    int start = 0, end = 0;

    for(int i = 1; i < n; i++)
    {
        int t = arr[i];

        // Check if element is occurring
        // for the second time in the array
        if (vis[t] != -1)
        {

            // Find distance between last
            // and current index
            // of the element.
            int distance = i - vis[t] + 1;

            // If the current distance
            // is less then len
            // update len and
            // set 'start' and 'end'
            if (distance < len)
            {
                len = distance;
                start = vis[t];
                end = i;
            }
            flag = 1;
        }

        // Set the last occurrence
        // of current element to be 'i'.
        vis[t] = i;
    }

    // If flag is equal to 0,
    // it means there is no answer.
    if (flag == 0)
        Console.WriteLine("No such subarray!");

    else
    {
        for(int i = start; i <= end; i++)
            Console.Write(arr[i] + " ");
    }
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 2, 3, 2, 4, 5 };
    int n = arr.Length;

    FindSubarray(arr, n);
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find subarray
function FindSubarray(arr, n)
{

    // If the array has only one element,
    // then there is no answer.
    if (n == 1)
    {
        document.write("No such subarray!");
    }

    // Array to store the last occurrences
    // of the elements of the array.
    let vis = new Array(n + 1);
    for(let i = 0; i < (n + 1); i++)
        vis[i] = -1;

    vis[arr[0]] = 0;

    // To maintain the length
    let len = Number.MAX_VALUE, flag = 0;

    // Variables to store
    // start and end indices
    let start = 0, end = 0;

    for(let i = 1; i < n; i++)
    {
        let t = arr[i];

        // Check if element is occurring
        // for the second time in the array
        if (vis[t] != -1)
        {

            // Find distance between last
            // and current index
            // of the element.
            let distance = i - vis[t] + 1;

            // If the current distance
            // is less then len
            // update len and
            // set 'start' and 'end'
            if (distance < len)
            {
                len = distance;
                start = vis[t];
                end = i;
            }
            flag = 1;
        }

        // Set the last occurrence
        // of current element to be 'i'.
        vis[t] = i;
    }

    // If flag is equal to 0,
    // it means there is no answer.
    if (flag == 0)
        document.write("No such subarray!");

    else
    {
        for(let i = start; i <= end; i++)
            document.write(arr[i] + " ");
    }
}

// Driver code
let arr = [ 2, 3, 2, 4, 5 ];
let n = arr.length;

FindSubarray(arr, n);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
2 3 2
```

***时间复杂度:** O(N)* ，其中 N 为数组长度。

***辅助空间:** O(N)* 。