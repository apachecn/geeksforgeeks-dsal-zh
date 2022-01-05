# 在给定大小的组中反转数组|集合 3(单次遍历)

> 原文:[https://www . geeksforgeeks . org/给定大小组中的反向数组-集合-3-单遍历/](https://www.geeksforgeeks.org/reverse-an-array-in-groups-of-given-size-set-3-single-traversal/)

给定一个数组，反转由连续 k 个元素组成的每个子数组。

**示例:**

> **输入:** arr = [1，2，3，4，5，6，7，8，9，10]，k = 3。
> **输出:**【3、2、1、6、5、4、9、8、7、10】
> **输入:**arr =【1、2、3、4、5、6、7】，k = 5。
> **输出:**【5、4、3、2、1、7、6】

**进场:**

1.  我们将使用两个指针技术来解决这个问题。
2.  首先，我们将使用值 k-1 ( **d = k-1** )和值 2 ( **m = 2** )的变量 m 初始化第一个指针 d。
3.  现在，我们将使用第二个指针 I 迭代数组并检查
    *   如果 **i < d** ，则交换(arr[i]，arr[d])，并将 d 减 1。否则，
    *   使**d = k * m–1**，**I = k *(m–1)–1**和 **m = m + 1。**

下面是上述方法的实现。

## C++

```
// C++ program to reverse every sub-array
// formed by consecutive k elements
#include<bits/stdc++.h>
using namespace std;

// Function to reverse every sub-array
// formed by consecutive k elements
void ReverseInGroup(int arr[], int n, int k)
{
    if(n < k)
    {
        k = n;
    }

    // Initialize variables
    int d = k - 1, m = 2;
    int i = 0;

    for(i = 0; i < n; i++)
    {

       if (i >= d)
       {
           // Update the variables
           d = k * (m);
           if(d >= n)
           {
               d = n;        
           }    
           i = k * (m - 1) - 1;
           m++;
       }
       else
       {
           int t = arr[i];
           arr[i] = arr[d];
           arr[d] = t;
       }
       d = d - 1;
    }
    return;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6, 7 };
    int k = 3;
    int n = sizeof(arr) / sizeof(arr[0]);

    ReverseInGroup(arr, n, k);

    for(int i = 0; i < n; i++)
       cout << arr[i] << " ";

    return 0;
}

// This code is contributed by Code_Mech
```

## C

```
// C program to reverse every sub-array
// formed by consecutive k elements
#include<stdio.h>

// Function to reverse every sub-array
// formed by consecutive k elements
void ReverseInGroup(int arr[], int n, int k)
{
    if(n<k)
    {
       k=n;
    }

    // Initialize variables
    int d = k-1, m=2;
    int i = 0;

    for (i = 0; i < n; i++)
    {
        if (i >= d)
        {  
            // Update the variables
            d = k * (m);
            if(d>=n)
            {
                d = n;            
            }          
            i = k * (m - 1)-1;
            m++;

        }
        else
        {
            int t = arr[i];
            arr[i] = arr[d];
            arr[d] = t;
        }

     d = d - 1;     

    }
    return;

}

// Driver code
int main()
{
    int arr[] = {1, 2, 3, 4, 5, 6, 7};
    int k = 3;

    int n = sizeof(arr) / sizeof(arr[0]);

    ReverseInGroup(arr, n, k);

    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reverse every sub-array
// formed by consecutive k elements
class GFG{

// Function to reverse every sub-array
// formed by consecutive k elements
static void ReverseInGroup(int arr[],
                           int n, int k)
{
    if(n < k)
    {
        k = n;
    }

    // Initialize variables
    int d = k - 1, m = 2;
    int i = 0;

    for(i = 0; i < n; i++)
    {
       if (i >= d)
       {

           // Update the variables
           d = k * (m);
           if(d >= n)
           {
               d = n;            
           }        
           i = k * (m - 1) - 1;
           m++;
       }
       else
       {
           int t = arr[i];
           arr[i] = arr[d];
           arr[d] = t;
       }
       d = d - 1;    
    }
    return;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5, 6, 7 };
    int k = 3;
    int n = arr.length;

    ReverseInGroup(arr, n, k);

    for(int i = 0; i < n; i++)
       System.out.printf("%d ", arr[i]);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to reverse
# every sub-array formed by
# consecutive k elements

# Function to reverse every
# sub-array formed by consecutive
# k elements
def ReverseInGroup(arr, n, k):

    if(n < k):
        k = n

    # Initialize variables
    d = k - 1
    m = 2
    i = 0

    while i < n:
        if (i >= d):

            # Update the
            # variables
            d = k * (m)

            if(d >= n):
                d = n

            i = k * (m - 1) - 1
            m += 1

        else:
            arr[i], arr[d] = (arr[d],
                              arr[i])
        d = d - 1
        i += 1

    return

# Driver code
if __name__ == "__main__":

    arr = [1, 2, 3,
           4, 5, 6, 7]
    k = 3
    n = len(arr)
    ReverseInGroup(arr, n, k)

    for i in range(n):
        print(arr[i],
              end = " ")

# This code is contributed by Chitranayal
```

## C#

```
// C# program to reverse every sub-array
// formed by consecutive k elements
using System;
class GFG{

// Function to reverse every sub-array
// formed by consecutive k elements
static void ReverseInGroup(int []arr,
                           int n, int k)
{
    if(n < k)
    {
        k = n;
    }

    // Initialize variables
    int d = k - 1, m = 2;
    int i = 0;

    for(i = 0; i < n; i++)
    {
        if (i >= d)
        {

            // Update the variables
            d = k * (m);
            if(d >= n)
            {
                d = n;            
            }        
            i = k * (m - 1) - 1;
            m++;
        }
        else
        {
            int t = arr[i];
            arr[i] = arr[d];
            arr[d] = t;
        }
        d = d - 1;    
    }
    return;
}

// Driver code
public static void Main()
{
    int []arr = { 1, 2, 3, 4, 5, 6, 7 };
    int k = 3;
    int n = arr.Length;

    ReverseInGroup(arr, n, k);

    for(int i = 0; i < n; i++)
        Console.Write(arr[i] + " ");
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
// Javascript program to reverse every sub-array
// formed by consecutive k elements

// Function to reverse every sub-array
// formed by consecutive k elements
function ReverseInGroup(arr, n, k)
{
    if(n < k)
    {
        k = n;
    }

    // Initialize variables
    let d = k - 1, m = 2;
    let i = 0;

    for(i = 0; i < n; i++)
    {

        if (i >= d)
        {
            // Update the variables
            d = k * (m);
            if(d >= n)
            {
              d = n;       
            }   
            i = k * (m - 1) - 1;
            m++;
        }
        else
        {
            let t = arr[i];
            arr[i] = arr[d];
            arr[d] = t;
        }
        d = d - 1;
    }
    return;
}

// Driver code

    let arr = [ 1, 2, 3, 4, 5, 6, 7 ];
    let k = 3;
    let n = arr.length;

    ReverseInGroup(arr, n, k);

    for(let i = 0; i < n; i++)
    document.write(arr[i] + " ");

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
3 2 1 6 5 4 7
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)