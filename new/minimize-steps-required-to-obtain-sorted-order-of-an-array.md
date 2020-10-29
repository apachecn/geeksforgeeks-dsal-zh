# 最小化获得阵列的排序顺序所需的步骤

> 原文：[https://www.geeksforgeeks.org/minimize-steps-required-to-obtain-sorted-order-of-an-array/](https://www.geeksforgeeks.org/minimize-steps-required-to-obtain-sorted-order-of-an-array/)

给定一个数组 **arr []** ，该数组由整数 **[1，N]** 的排列组成，通过重新排列排序的顺序 **[1，N]** ，该任务 通过重复相同的过程从步骤中从排序的序列中获得 arr []，找到**的最小步数**，此后将重复排序的顺序 **[1，N]** 。 每一步。

**范例**：

> **输入**：arr [] = {3，6，5，4，1，2}
> **输出**：6 ]增加排列：{1、2、3、4、5、6}
> 步骤 1：arr [] = {3、6、5、4、1、2}（给定数组）
> 步骤 2： arr [] = {5，2，1，4，4，3} 6
> 步骤 3：arr [] = {1，6，3，4，5，2}
> 步骤 4：arr [] = {3，2，5，4，1，1，6}
> 步骤 5：arr [] = {5，6，1，4，4，3，2}
> 步骤 6：arr [] = {1，2 ，3，4，5，6}（增加排列）
> 因此，总步数为 6。
> 
> **输入**：arr [] = [5，1，4，3，2]
> **输出**：6

**方法**：

此问题可以简单地通过使用[直接寻址](https://www.geeksforgeeks.org/direct-address-table/)的概念来解决。 请按照以下步骤解决问题：

*   初始化数组 **dat []** 以进行直接寻址。

*   对 **[1，N]** 进行迭代，并按照排序顺序从每个元素的索引中计算当前索引的差。

*   计算数组 **dat []** 的 LCM。

*   现在，将获得的 LCM 打印为获得排序顺序所需的**最小步骤**。

下面是上述方法的实现：

## C++ 14

```

// C++ Program to implement  
// the above approach  
#include <bits/stdc++.h>  
using namespace std;  

// Function to find  
// GCD of two numbers  
int gcd(int a, int b)  
{  
    if (b == 0)  
        return a;  

    return gcd(b, a % b);  
}  

// Function to calculate the  
// LCM of array elements  
int findlcm(int arr[], int n)  
{  
    // Initialize result  
    int ans = 1;  

    for (int i = 1; i <= n; i++)  
        ans = (((arr[i] * ans))  
            / (gcd(arr[i], ans)));  

    return ans;  
}  

// Function to find minimum steps  
// required to obtain sorted sequence  
void minimumSteps(int arr[], int n)  
{  

    // Inititalize dat[] array for  
    // Direct Address Table.  
    int i, dat[n + 1];  

    for (i = 1; i <= n; i++)  

        dat[arr[i - 1]] = i;  

    int b[n + 1], j = 0, c;  

    // Calculating steps required  
    // for each element to reach  
    // its sorted position  
    for (i = 1; i <= n; i++) {  
        c = 1;  
        j = dat[i];  
        while (j != i) {  
            c++;  
            j = dat[j];  
        }  
        b[i] = c;  
    }  

    // Calculate LCM of the array  
    cout << findlcm(b, n);  
}  

// Driver Code  
int main()  
{  

    int arr[] = { 5, 1, 4, 3, 2, 7, 6 };  

    int N = sizeof(arr) / sizeof(arr[0]);  

    minimumSteps(arr, N);  

    return 0;  
}  

```

## Java

```java

// Java program to implement 
// the above approach 
class GFG{ 

// Function to find 
// GCD of two numbers 
static int gcd(int a, int b) 
{ 
    if (b == 0) 
        return a; 

    return gcd(b, a % b); 
} 

// Function to calculate the 
// LCM of array elements 
static int findlcm(int arr[], int n) 
{ 

    // Initialize result 
    int ans = 1; 

    for(int i = 1; i <= n; i++) 
        ans = (((arr[i] * ans)) /  
            (gcd(arr[i], ans))); 

    return ans; 
} 

// Function to find minimum steps 
// required to obtain sorted sequence 
static void minimumSteps(int arr[], int n) 
{ 

    // Inititalize dat[] array for 
    // Direct Address Table. 
    int i; 
    int dat[] = new int[n + 1]; 

    for(i = 1; i <= n; i++) 
        dat[arr[i - 1]] = i; 

    int b[] = new int[n + 1]; 
    int j = 0, c; 

    // Calculating steps required 
    // for each element to reach 
    // its sorted position 
    for(i = 1; i <= n; i++) 
    { 
        c = 1; 
        j = dat[i]; 

        while (j != i)  
        { 
            c++; 
            j = dat[j]; 
        } 
        b[i] = c; 
    } 

    // Calculate LCM of the array 
    System.out.println(findlcm(b, n)); 
} 

// Driver code     
public static void main(String[] args) 
{ 
    int arr[] = { 5, 1, 4, 3, 2, 7, 6 }; 

    int N = arr.length; 

    minimumSteps(arr, N); 
} 
} 

// This code is contributed by rutvik_56 

```

## Python3

```py

# Python3 program to implement  
# the above approach  

# Function to find  
# GCD of two numbers  
def gcd(a, b):  

    if(b == 0):  
        return a  

    return gcd(b, a % b)  

# Function to calculate the  
# LCM of array elements  
def findlcm(arr, n):  

    # Initialize result  
    ans = 1

    for i in range(1, n + 1):  
        ans = ((arr[i] * ans) //
            (gcd(arr[i], ans)))  

    return ans  

# Function to find minimum steps  
# required to obtain sorted sequence  
def minimumSteps(arr, n):  

    # Inititalize dat[] array for  
    # Direct Address Table.  
    dat = [0] * (n + 1)  

    for i in range(1, n + 1):  
        dat[arr[i - 1]] = i  

    b = [0] * (n + 1)  
    j = 0

    # Calculating steps required  
    # for each element to reach  
    # its sorted position  
    for i in range(1, n + 1):  
        c = 1
        j = dat[i]  
        while(j != i):  
            c += 1
            j = dat[j]  

        b[i] = c  

    # Calculate LCM of the array  
    print(findlcm(b, n))  

# Driver Code  
arr = [ 5, 1, 4, 3, 2, 7, 6 ]  

N = len(arr)  

minimumSteps(arr, N)  

# This code is contributed by Shivam Singh  

```

## C#

```cs

// C# program to implement 
// the above approach 
using System; 

class GFG{ 

// Function to find 
// GCD of two numbers 
static int gcd(int a, int b) 
{ 
    if (b == 0) 
        return a; 

    return gcd(b, a % b); 
} 

// Function to calculate the 
// LCM of array elements 
static int findlcm(int []arr, int n) 
{ 

    // Initialize result 
    int ans = 1; 

    for(int i = 1; i <= n; i++) 
        ans = (((arr[i] * ans)) /  
            (gcd(arr[i], ans))); 

    return ans; 
} 

// Function to find minimum steps 
// required to obtain sorted sequence 
static void minimumSteps(int []arr, int n) 
{ 

    // Inititalize dat[] array for 
    // Direct Address Table. 
    int i; 
    int []dat = new int[n + 1]; 

    for(i = 1; i <= n; i++) 
        dat[arr[i - 1]] = i; 

    int []b = new int[n + 1]; 
    int j = 0, c; 

    // Calculating steps required 
    // for each element to reach 
    // its sorted position 
    for(i = 1; i <= n; i++) 
    { 
        c = 1; 
        j = dat[i]; 

        while (j != i)  
        { 
            c++; 
            j = dat[j]; 
        } 
        b[i] = c; 
    } 

    // Calculate LCM of the array 
    Console.WriteLine(findlcm(b, n)); 
} 

// Driver code  
public static void Main(String[] args) 
{ 
    int []arr = { 5, 1, 4, 3, 2, 7, 6 }; 

    int N = arr.Length; 

    minimumSteps(arr, N); 
} 
} 

// This code is contributed by gauravrajput1  

```

**Output:** 

```
6

```

***时间复杂度**：O（NlogN）*

***辅助空间**：`O(n)`*



* * *

* * *



