# 通过用位于相邻元素中间的元素替换每个元素来重新排列给定的数组

> 原文:[https://www . geeksforgeeks . org/通过用相邻元素的平均值替换每个元素来重新排列给定的数组/](https://www.geeksforgeeks.org/rearrange-given-array-by-replacing-every-element-with-the-element-located-at-mean-of-adjacent-elements/)

给定数组 **arr[]** 。数组只包含从 **0** 到 **N-1** 的数字，其中 **N** 是**arr【】**的大小。任务是修改数组，使每个 **i** 从 **0≤i < N** ，**arr[I]= arr[(arr[I-1]+arr[I+1])/2]**

有几个例外:

*   对于数组的第一个元素，**arr[I-1]= 0**；因为以前的索引不存在。
*   对于数组的最后一个元素，**arr[I+1]= 0**；因为下一个索引不存在。

**示例:**

> **输入:** arr[]= {3，2，1，4，1，8，6，8，7}
> **输出:**【2，1，4，2，6，4，7，6，1】
> **说明:**以下是为达到所需输出而执行的操作。
> 对于索引 0，arr[i-1]=0 和 arr[i+1]=2，arr[0]= arr[(0+2)/2]= arr[1]= 2
> 对于索引 3，arr[i-1]=1 和 arr[i+1]=1，arr[3]= arr[(1+1)/2] = arr[1] = 2
> 
> **输入:** arr[]= {2，5，3，4，0，1}
> **输出:**【3，3，0，5，3，2】
> **说明:**以下是为达到所需输出而执行的操作。
> 对于索引 1，arr[i-1]=2 和 arr[i+1]=3，arr[1]= arr[(2+3)/2]= arr[2]= 3
> 对于索引 4，arr[i-1]=4 和 arr[i+1]=1，arr[4]= arr[(4+1)/2] = arr[2] = 3

**天真方法:**最简单的方法是创建一个新的数组，并使用给定的数组计算每个索引的值，但这将占用额外的空间。对于每个索引，获取上一个和下一个索引的值，并计算它们的平均值。该平均值将是其值必须复制到新数组中所选索引处的索引。因此，将实现**arr[I]= arr[(arr[I-1]+arr[I+1])/2]**。

**时间复杂度:** O(N)，N 是 arr[]的大小。
**辅助空间:** O(N)

**高效的方法:**这种方法遍历同一个数组一次，最后会找到想要的数组。跟踪前一个索引元素，这样即使它的值被修改，旧的值也可以被计算。在这种情况下，只使用了 **O(1** )空间，用于存储前一个元素的值的临时变量。

**如何实现这一点？**

考虑两个数字 **x** 和 **y** ，都小于 **N** 。目的是更新 **x (x = y)** 的值，使得旧值 **(x=x)** 不会丢失。基本上，只需在同一个变量中持有 **x** 的两个值。为此，首先，将 x 值增加因子 **y*N** 。更新后的 x 变为 **x+y*N** 。 **x** 的旧值可以通过取更新值的 mod 得到； **(x+y*N % N)** 。x 的新值可以通过取除以 N 的商得到， **(x+y*N/N)** 。按照以下步骤解决给定的问题。

*   从左到右迭代数组 **arr[]** 。
*   对于每个索引，将元素增加**arr[(arr[I-1]+arr[I+1])/2]* N**。
*   要获取第个元素的前一个，请使用 **N** 求模，即 **arr[i-1]%N** 。
*   要得到元素的下一个元素，求 **N** 的商，即 **arr[i+1]/N** 。
*   再次从头到尾遍历数组。
*   将 ith 元素除以 **N** 后打印出 ith 元素，即**数组【I/N】**。

下面是上述方法的实现。

## C++

```
// Program to modify the given array
// as per given constraint.
#include <iostream>
using namespace std;

// Functionn to find the previous val
int FindPrev(int i, int a, int n)
{
    if (i == 0)
        return 0;
    else
        return a % n;
}

// Function to find the next value
int FindNext(int i, int a, int n)
{
    if (i == n - 1)
        return 0;
    else
        return a;
}

// The function to rearrange an array
// in-place so that arr[i] becomes
// arr[(arr[i-1]+arr[i+1])/2].
void ModifyTheArray(int arr[], int n)
{
    int new_ind, new_ind_val, next, prev;

    // Traverse the array arr[]
    for (int i = 0; i < n; i++) {
        prev = FindPrev(i, arr[i - 1], n);
        next = FindNext(i, arr[i + 1], n);
        new_ind = (prev + next) / 2;
        new_ind_val = arr[new_ind] % n;
        arr[i] = arr[i] + n * new_ind_val;
    }

    for (int i = 0; i < n; i++)
        arr[i] /= n;
}

// A utility function to display the array of size n
void DisplayArray(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;
}

// Driver Code
int main()
{
    int arr[] = { 3, 2, 1, 4, 1, 8, 6, 8, 7 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << "Given array is=> \n";
    DisplayArray(arr, N);

    ModifyTheArray(arr, N);

    cout << "Modified array is=> \n";
    DisplayArray(arr, N);

    return 0;
}
```

## java 描述语言

```
<script>

// JavaScript program to modify the given array
// as per given constraint.

// Function to find the previous val
function FindPrev(i, a, n)
{
    if (i == 0)
        return 0;
    else
        return a % n;
}

// Function to find the next value
function FindNext(i, a, n)
{
    if (i == n - 1)
        return 0;
    else
        return a;
}

// The function to rearrange an array
// in-place so that arr[i] becomes
// arr[(arr[i-1]+arr[i+1])/2].
function ModifyTheArray(arr, n)
{
    let new_ind, new_ind_val, next, prev;

    // Traverse the array arr[]
    for(let i = 0; i < n; i++)
    {
        prev = FindPrev(i, arr[i - 1], n);
        next = FindNext(i, arr[i + 1], n);
        new_ind = Math.floor((prev + next) / 2);
        new_ind_val = arr[new_ind] % n;
        arr[i] = arr[i] + n * new_ind_val;
    }

    for(let i = 0; i < n; i++)
        arr[i] = Math.floor(arr[i] / n);
}

// A utility function to display the array of size n
function DisplayArray(arr, n)
{
    for(let i = 0; i < n; i++)
        document.write(arr[i] + " ")

    document.write('<br')
}

// Driver Code
let arr = [ 3, 2, 1, 4, 1, 8, 6, 8, 7 ];
let N = arr.length;

document.write("Given array is=> " + "<br>");
DisplayArray(arr, N);

ModifyTheArray(arr, N);

document.write("Modified array is=> " + "<br>");
DisplayArray(arr, N);

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
Given array is=> 
3 2 1 4 1 8 6 8 7 
Modified array is=> 
2 1 4 2 6 4 7 6 1 
```

**时间复杂度:** O(N)，N 是 arr[]的大小。

**空间复杂度:** O(1)