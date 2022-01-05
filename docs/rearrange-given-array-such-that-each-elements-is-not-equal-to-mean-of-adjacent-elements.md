# 重新排列给定的数组，使每个元素不等于相邻元素的平均值

> 原文:[https://www . geeksforgeeks . org/relay-给定数组-这样-每个元素不等于相邻元素的平均值/](https://www.geeksforgeeks.org/rearrange-given-array-such-that-each-elements-is-not-equal-to-mean-of-adjacent-elements/)

给定一个由 **N** 个唯一整数组成的数组 **arr** ，任务是重新排列数组，使得数组的索引 **i** 处的元素不应该是相邻元素(即索引 i-1 和 i+1)的平均值。任何可能的重排都可以返回。

示例:

> **输入:**arr =【5，4，3，2，1】
> **输出:**【5，3，4，2，1】
> **解释:**在输入数组中:
> Mean(5，3) = (5 + 3)/2 = 4，
> Mean(4，2) = (4+ 2 )/2 = 3，
> Mean(3，1) = (3 + 1)/2 = 2。
> 将数组重新排列为[5，3，4，2，1]后，现在没有元素是相邻元素的平均值:(5 + 4)/2 ≠ 3，(3 + 2)/2 ≠ 4，(4 + 1)/2 ≠ 2
> 
> **输入:**arr =【6，9，12，25，50 75】
> **输出:**【6，12，9，25，50，75】

**处理方法:**解决这个问题的主要观察是，对于 3 个数字 a、b、c，要满足 b 不应该是 a、c 的平均值的条件，[a、b、c]一定不能排序。因此，这个问题可以通过以下步骤解决:

*   [从 1 到(N-1)迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)
*   检查(arr[I–1]+arr[I+1])/2 = = arr[I])
*   如果条件满足，交换元素 arr[i]和 arr[i+1]

下面是上述方法的实现:

## C++

```
// C++ code for above implementation
#include <bits/stdc++.h>
using namespace std;

// Function to rearrange the array
void Rearrange(int arr[], int N)
{

    // Iterating for array
    for (int i = 1; i < (N - 1); i++) {

        // Checking whether the element i
        // is mean of i-1 and i+1
        if ((arr[i - 1] + arr[i + 1]) / 2 == arr[i]) {

            // Rearrange by swapping arr[i] and arr[i+1]
            swap(arr[i], arr[i + 1]);
        }
    }

    // Printing the output array
    for (int i = 0; i < N; i++) {
        cout << arr[i] << " ";
    }
}

// Driver code
int main()
{
    int arr[] = { 6, 9, 12, 25, 50, 75 };
    int N = sizeof(arr) / sizeof(int);

    // calling the function
    Rearrange(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {
  // Function to rearrange the array

static void Rearrange(int arr[], int N)
{

    // Iterating for array
    for (int i = 1; i < (N - 1); i++) {

        // Checking whether the element i
        // is mean of i-1 and i+1
        if ((arr[i - 1] + arr[i + 1]) / 2 == arr[i]) {

            // Rearrange by swapping arr[i] and arr[i+1]

          int temp = arr[i];
        arr[i] = arr[i + 1];
        arr[i + 1] = temp;
        }
    }

    // Printing the output array
    for (int i = 0; i < N; i++) {
         System.out.print(arr[i] +" ");
    }
}

// Driver code
    public static void main (String[] args) {
      int arr[] = { 6, 9, 12, 25, 50, 75 };
    int N = arr.length;

    // calling the function
    Rearrange(arr, N);
    }
}
// This code is contributed by Potta Lokesh
```

## C#

// C#程序为上述方法

使用系统；

类 GFG {
//函数重新排列数组

静态无效重新排列(int []arr，int N)
{ 0

//对数组
进行迭代(int I = 1；一<(N–1)；i++){ 0

//检查元素 i
//是否为 i-1 和 i+1
的平均值，如果((arr[I–1]+arr[I+1])/2 = = arr[I]){

//通过交换 arr[i]和 arr[i+1]重新排列

int temp = arr[I]；
arr[I]= arr[I+1]；
arr[I+1]= temp；
}

//打印输出数组
为(int I = 0；一<N；i++) {
控制台。write(arr[I]+" ")；
}

//驱动程序代码
公共静态 void Main(String[]args)
{
int[]arr = { 6，9，12，25，50，75 }；
int N = arr。长度；

//调用函数
重新排列(arr，N)；
}
}
//本代码由 shivanisinghss2110 提供

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to rearrange the array
def Rearrange(arr, N) :

    # Iterating for array
    for i in range(1, N - 1) :

        # Checking whether the element i
        # is mean of i-1 and i+1
        if ((arr[i - 1] + arr[i + 1]) // 2 == arr[i]) :

            # Rearrange by swapping arr[i] and arr[i+1]
            arr[i], arr[i + 1] = arr[i + 1], arr[i];

    # Printing the output array
    for i in range(N) :
        print(arr[i],end= " " )

# Driver code
if __name__ == "__main__" :

    arr = [ 6, 9, 12, 25, 50, 75 ];
    N = len(arr);

    # calling the function
    Rearrange(arr, N);

    # This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// JavaScript program for the above approach
// Function to rearrange the array

function Rearrange(arr, N)
{

    // Iterating for array
    for (var i = 1; i < (N - 1); i++) {

        // Checking whether the element i
        // is mean of i-1 and i+1
        if ((arr[i - 1] + arr[i + 1]) / 2 == arr[i]) {

            // Rearrange by swapping arr[i] and arr[i+1]

        var temp = arr[i];
        arr[i] = arr[i + 1];
        arr[i + 1] = temp;
        }
    }

    // Printing the output array
    for (var i = 0; i < N; i++) {
        document.write(arr[i] +" ");
    }
}

// Driver code
var arr = [ 6, 9, 12, 25, 50, 75 ];
var N = arr.length;

// calling the function
Rearrange(arr, N);

// This code is contributed by shivanisinghss2110

</script>
```

**Output**

```
6 12 9 25 75 50 
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)