# 对数组中所有偶数进行排序，不改变奇数元素的顺序

> 原文:[https://www . geesforgeks . org/sort-数组中所有偶数不改变奇数元素的顺序/](https://www.geeksforgeeks.org/sort-all-even-numbers-in-the-array-without-changing-order-of-odd-elements/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是对数组中的所有偶数进行排序，而不改变奇数元素的顺序
**示例**:

> **输入** : arr[] = {4，7，2，11，15}
> **输出** : {2，7，4，11，15}
> **说明**:偶数在对应的位置排序，不改变奇数元素的顺序
> 
> **输入** : arr[] = {12，6}
> 输出 : {6，12}

**接近**:可以通过将偶数元素分离到另一个容器中来解决任务，比如说“**偶数**”、**对这个容器进行排序**，在迭代数组的同时，**用存储在**偶数**中的**排序**偶数元素替换**偶数元素

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to get the required array
void solve(int arr[], int n)
{

    // Store even elements
    vector<int> evens;
    for (int i = 0; i < n; i++) {
        if (arr[i] % 2 == 0)
            evens.push_back(arr[i]);
    }

    // Sort all even elements
    sort(evens.begin(), evens.end());
    int l = 0;

    // Placing even elements in sorted order
    for (int i = 0; i < n; i++) {
        if (arr[i] % 2 == 0)
            arr[i] = evens[l++];
    }

    // Updated array
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Driver Code
int main()
{
    int N = 5;
    int arr[N] = { 4, 7, 2, 11, 15 };
    solve(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*; 

public class GFG {

    // Function to get the required array
    static void solve(int []arr, int n)
    {

        // Store even elements
        ArrayList<Integer> evens = new ArrayList<Integer>();
        for (int i = 0; i < n; i++) {
            if (arr[i] % 2 == 0)
                evens.add(arr[i]);
        }

        // Sort all even elements
        Collections.sort(evens); 

        int l = 0;

        // Placing even elements in sorted order
        for (int i = 0; i < n; i++) {
            if (arr[i] % 2 == 0)
                arr[i] = evens.get(l++);
        }

        // Updated array
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
    }

    // Driver function
    public static void main(String []args)
    {
        int N = 5;
        int []arr = { 4, 7, 2, 11, 15 };
        solve(arr, N);

    }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# python program of the above approach

# Function to get the required array
def solve(arr, n):

        # Store even elements
    evens = []
    for i in range(0, n):
        if (arr[i] % 2 == 0):
            evens.append(arr[i])

        # Sort all even elements
    evens.sort()
    l = 0

    # Placing even elements in sorted order
    for i in range(0, n):
        if (arr[i] % 2 == 0):
            arr[i] = evens[l]
            l += 1

        # Updated array
    for i in range(0, n):
        print(arr[i], end=" ")

# Driver Code
if __name__ == "__main__":

    N = 5
    arr = [4, 7, 2, 11, 15]
    solve(arr, N)

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG {

    // Function to get the required array
    static void solve(int []arr, int n)
    {

        // Store even elements
        List<int> evens = new List<int>();
        for (int i = 0; i < n; i++) {
            if (arr[i] % 2 == 0)
                evens.Add(arr[i]);
        }

        // Sort all even elements
        evens.Sort();
        int l = 0;

        // Placing even elements in sorted order
        for (int i = 0; i < n; i++) {
            if (arr[i] % 2 == 0)
                arr[i] = evens[l++];
        }

        // Updated array
        for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
    }

    // Driver function
    public static void Main()
    {
        int N = 5;
        int []arr = new int[] { 4, 7, 2, 11, 15 };
        solve(arr, N);

    }
}

// This code is contributed by Samim Hossain Mondal
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to get the required array
function solve(arr, n)
{
    // Store even elements
    let evens = [];
    for (let i = 0; i < n; i++) {
        if (arr[i] % 2 == 0)
            evens.push(arr[i]);
    }

    // Sort all even elements
    evens.sort();
    let l = 0;

    // Placing even elements in sorted order
    for (let i = 0; i < n; i++) {
        if (arr[i] % 2 == 0)
            arr[i] = evens[l++];
    }

    // Updated array
    for (let i = 0; i < n; i++)
        document.write(arr[i] + " ");
}

// Driver Code
  let N = 5;
  let arr = [ 4, 7, 2, 11, 15 ];
  solve(arr, N);

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output**

```
2 7 4 11 15 
```

***时间复杂度*** : O(NlogN)
***辅助空间*** : O(N)