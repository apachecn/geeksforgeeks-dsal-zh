# 打印给定阵列的所有可能旋转

> 原文:[https://www . geeksforgeeks . org/print-给定数组的所有可能旋转数/](https://www.geeksforgeeks.org/print-all-possible-rotations-of-a-given-array/)

给定一个大小为 **N** 的整数数组 **arr[]** ，任务是打印数组的所有可能旋转。
**例:**

> **输入:** arr[] = {1，2，3，4}
> **输出:** {1，2，3，4}，{4，1，2，3}，{3，4，1，2}，{2，3，4，1}
> **解释:**
> 初始 arr[] = {1，2，3，4}
> 第一次旋转后 arr[] = {4，1，2，3}
> 第二次旋转后 arr[]= { 0
> **输入:** arr[] = [1]
> **输出:**【1】

**方法:**
按照以下步骤解决问题:

1.  通过逐个执行阵列的[左旋转，生成阵列的所有可能旋转。](https://www.geeksforgeeks.org/print-left-rotation-array/)
2.  打印数组的所有可能旋转，直到遇到相同的数组旋转。

下面是上述方法的实现:

## C++

```
// C++ program to print
// all possible rotations
// of the given array
#include <iostream>
using namespace std;  

// Global declaration of array
int arr[10000];

// Function to reverse array
// between indices s and e
void reverse(int arr[],
             int s, int e)
{
  while(s < e)
  {
    int tem = arr[s];
    arr[s] = arr[e];
    arr[e] = tem;
    s = s + 1;
    e = e - 1;
  }
}

// Function to generate all
// possible rotations of array
void fun(int arr[], int k)
{
  int n = 4 - 1;
  int v = n - k;

  if (v >= 0)
  {
    reverse(arr, 0, v);
    reverse(arr, v + 1, n);
    reverse(arr, 0, n);
  }
}

// Driver code
int main()
{
  arr[0] = 1;
  arr[1] = 2;
  arr[2] = 3;
  arr[3] = 4;

  for(int i = 0; i < 4; i++)
  {
    fun(arr, i);
    cout << ("[");

    for(int j = 0; j < 4; j++)
    {
      cout << (arr[j]) << ", ";
    }
    cout << ("]");
  }
}

// This code is contributed by Princi Singh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print
// all possible rotations
// of the given array
class GFG{

// Global declaration of array
static int arr[] = new int[10000];

// Function to reverse array
// between indices s and e
public static void reverse(int arr[],
                           int s, int e)
{
    while(s < e)
    {
        int tem = arr[s];
        arr[s] = arr[e];
        arr[e] = tem;
        s = s + 1;
        e = e - 1;
    }
}

// Function to generate all
// possible rotations of array
public static void fun(int arr[], int k)
{
    int n = 4 - 1;
    int v = n - k;

    if (v >= 0)
    {
        reverse(arr, 0, v);
        reverse(arr, v + 1, n);
        reverse(arr, 0, n);
    }
}

// Driver code
public static void main(String args[])
{
    arr[0] = 1;
    arr[1] = 2;
    arr[2] = 3;
    arr[3] = 4;

    for(int i = 0; i < 4; i++)
    {
        fun(arr, i);

        System.out.print("[");
        for(int j = 0; j < 4; j++)
        {
            System.out.print(arr[j] + ", ");
        }
        System.out.print("]");
    }
}
}

// This code is contributed by gk74533
```

## 计算机编程语言

```
# Python program to print
# all possible rotations
# of the given array

# Function to reverse array
# between indices s and e
def reverse(arr, s, e):
    while s < e:
        tem = arr[s]
        arr[s] = arr[e]
        arr[e] = tem
        s = s + 1
        e = e - 1
# Function to generate all
# possible rotations of array
def fun(arr, k):
    n = len(arr)-1
    # k = k % n
    v = n - k
    if v>= 0:
        reverse(arr, 0, v)
        reverse(arr, v + 1, n)
        reverse(arr, 0, n)
        return arr
# Driver Code
arr = [1, 2, 3, 4]
for i in range(0, len(arr)):
    count = 0
    p = fun(arr, i)
    print(p, end =" ")
```

## C#

```
// C# program to print
// all possible rotations
// of the given array
using System;
class GFG{

// Global declaration of array
static int []arr = new int[10000];

// Function to reverse array
// between indices s and e
public static void reverse(int []arr,
                           int s, int e)
{
  while(s < e)
  {
    int tem = arr[s];
    arr[s] = arr[e];
    arr[e] = tem;
    s = s + 1;
    e = e - 1;
  }
}

// Function to generate all
// possible rotations of array
public static void fun(int []arr, int k)
{
  int n = 4 - 1;
  int v = n - k;

  if (v >= 0)
  {
    reverse(arr, 0, v);
    reverse(arr, v + 1, n);
    reverse(arr, 0, n);
  }
}

// Driver code
public static void Main(String []args)
{
  arr[0] = 1;
  arr[1] = 2;
  arr[2] = 3;
  arr[3] = 4;

  for(int i = 0; i < 4; i++)
  {
    fun(arr, i);
    Console.Write("[");

    for(int j = 0; j < 4; j++)
    {
      Console.Write(arr[j] + ", ");
    }
    Console.Write("]");
  }
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// javascript program to print
// all possible rotations
// of the given array

// Global declaration of array
arr = Array.from({length: 10000}, (_, i) => 0);

// Function to reverse array
// between indices s and e
function reverse(arr, s , e)
{
    while(s < e)
    {
        var tem = arr[s];
        arr[s] = arr[e];
        arr[e] = tem;
        s = s + 1;
        e = e - 1;
    }
}

// Function to generate all
// possible rotations of array
function fun(arr , k)
{
    var n = 4 - 1;
    var v = n - k;

    if (v >= 0)
    {
        reverse(arr, 0, v);
        reverse(arr, v + 1, n);
        reverse(arr, 0, n);
    }
}

// Driver code

    arr[0] = 1;
    arr[1] = 2;
    arr[2] = 3;
    arr[3] = 4;

    for(i = 0; i < 4; i++)
    {
        fun(arr, i);

        document.write("[");
        for(j = 0; j < 4; j++)
        {
            document.write(arr[j] + ", ");
        }
        document.write("]<br>");
    }

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
[1, 2, 3, 4] [4, 1, 2, 3] [2, 3, 4, 1] [3, 4, 1, 2]
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O (1)*