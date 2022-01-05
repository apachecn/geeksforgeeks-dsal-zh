# 检查是否可以使用三重循环移位对递减数组进行排序

> 原文:[https://www . geesforgeks . org/check-if-a-reduced-array-can-sorted-use-triple-cyclic-shift/](https://www.geeksforgeeks.org/check-if-a-decreasing-array-can-be-sorted-using-triple-cyclic-shift/)

给定大小为 **N** 的 **arr[]** ，其元素按降序排序。任务是通过执行最少次数的三重循环右交换来确定给定数组是否可以按升序排序。打印每个三重循环右交换中涉及的索引。

> **三重循环右移**指三重循环右移，其中:
> 
> **arr[I]->arr[j]->arr[k]->arr[I]，**其中 0 < = i，j，k < N 和 I，j 和 k 必须不同。

**注意:**以下示例有基于 1 的索引。
**例:**

> **输入:** arr[] = {100，90，80，70，60}
> **输出:**YES
> 2
> 【1 2 5】
> 【2 5 4】
> **说明:**
> 第一次操作选择的指标为 **1、2、5** 。
> arr[1]= arr[5]= 60
> arr[2]= arr[1]= 100
> arr[5]= arr[2]= 90
> 第一次循环右移后更新的数组为 **{60 100 80 70 90}**
> 第一次操作选择的索引为 **2、5 和 4** 。
> arr[2]= arr[4]= 70
> arr[5]= arr[2]= 100
> arr[4]= arr[5]= 90
> 第二次循环右移后的更新数组为 **{60 70 80 90 100}**
> 因此数组仅通过 2 次循环右移操作排序。
> **输入:** arr[] = {7，6，5，4，3，2，1}
> **输出:** NO
> **说明:**
> 无法对此数组执行任何循环右移操作，因此无法按升序排序。

**进场:**
进行以下观察:

*   对于有 3 个元素的数组，答案是否定的。因为中间的元素在正确的位置，我们将剩下两个元素，而循环右移需要三个元素。
*   如果 **(N % 4) == 0** 或 **(N % 4) == 1** ，则可以排序，否则无法排序。
    从上述方法可以看出，在每两次循环右移时，对四个元素进行排序。
*   当 **N % 4 == 0 时** :
    让我们考虑数组【4 3 2 1】。在索引 1 2 4 和 2 4 3(按顺序)的两次移位之后，数组被排序为 1 2 3 4。
*   当 **N % 4 == 1** :
    时，上述在数组中使用 5 个元素的示例 1 适用。索引 3 处的元素保持不变，而其他 4 个元素以 2 次循环右移进行排序。
*   当 **N % 4 == 2** :
    对数组进行排序是不可能的，因为在对 4 个元素的组进行排序后，最终会有 2 个元素以不正确的顺序留下，这是永远无法排序的，因为排序只需要 3 个元素。
*   当 **N % 4 == 3** :
    无法对数组进行排序，因为在 4 个元素组成的组之后，最后 3 个元素会以不正确的顺序留下，这是永远无法排序的，因为这 3 个未排序元素中的中间元素从一开始就保持在正确的位置。这就给我们留下了 2 个永远无法排序的元素，因为排序只需要 3 个元素。

按照以下步骤解决问题。

*   如果 N 模 4 的值是 2 或 3，打印**否**。
*   如果模 4 的值是 0 或 1，
    1.  打印**是**
    2.  打印**楼层(N / 2)**的值，因为楼层(N/2)是要执行的循环右交换操作的数量。
    3.  将变量 **K** 初始化为 1。
    4.  循环右交换操作只能成对执行。配对为**【K，K+1，N】**和**【K+1，N，N-1】。**一旦打印了对，将 K 值增加 2，将 N 值减少 2。
    5.  继续执行步骤 4，直到所有**楼层(N/2)** 操作打印完毕。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

void sortarray(int arr[],int N)
{

    // If array is 3 2 1 can't
    // be sorted because 2 is in
    // its correct position, 1
    // and 3 can't shift right
    // because cyclic right shift
    // takes place between 3 elements
    if(N == 3)
        cout << "NO" << endl;

    // Check if its possible to sort
    else if(N % 4 == 0 || N % 4 == 1)
    {
        cout << "YES" << endl;

        // Number of swap is
        // N / 2 always
        // for this approach
        cout << (N / 2) << endl;
        int k = 1;

        // Printing index of the
        // cyclic right shift
        for(int l = 0; l < (N / 4); l++)
        {
        cout << k << " " << k + 1
                << " " << N << endl;
        cout << k + 1 << " " << N
                << " " << N - 1 << endl;
        k = k + 2;
        N = N - 2;
        }
    }
    else
        cout << "NO" << endl;
}

// Driver code
int main()
{
    int N = 5;
    int arr[] = { 5, 4, 3, 2, 1 };

    sortarray(arr, N);
    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

static void sortarray(int arr[], int N)
{

    // If array is 3 2 1 can't
    // be sorted because 2 is in
    // its correct position, 1
    // and 3 can't shift right
    // because cyclic right shift
    // takes place between 3 elements
    if(N == 3)
    System.out.println("NO");

    // Check if its possible to sort
    else if(N % 4 == 0 || N % 4 == 1)
    {
        System.out.println("YES");

        // Number of swap is
        // N / 2 always
        // for this approach
        System.out.println(N / 2);
        int k = 1, l;

        // Printing index of the
        // cyclic right shift
        for(l = 0; l < (N / 4); l++)
        {
        System.out.println(k + " " + (k + 1) +
                               " " + N);
        System.out.println(k + 1 + " " +
                           N + " " + (N - 1));
        k = k + 2;
        N = N - 2;
        }
    }
    else
        System.out.println("NO");
}

// Driver code
public static void main (String []args)
{
    int N = 5;
    int arr[] = { 5, 4, 3, 2, 1 };

    sortarray(arr, N);
}
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 program for the above approach
def sortarray(arr, N):

    # if array is 3 2 1 can't
    # be sorted because 2 is in
    # its correct position, 1
    # and 3 can't shift right
    # because cyclic right shift
    # takes place between 3 elements
    if(N == 3):
        print("NO")

    # check if its possible to sort
    elif(N % 4 == 0
        or N % 4 == 1):
        print("YES")

        # Number of swap is
        # N / 2 always
        # for this approach
        print(N // 2)
        k = 1

        # printing index of the
        # cyclic right shift
        for l in range(N // 4):
            print(k, k + 1, N)
            print(k + 1, N, N-1)
            k = k + 2
            N = N - 2
    else:
        print("NO")

# Driver code
if __name__ == "__main__":

    N = 5
    arr = [5, 4, 3, 2, 1]
    sortarray(arr, N)
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static void sortarray(int[] arr, int N)
{

    // If array is 3 2 1 can't
    // be sorted because 2 is in
    // its correct position, 1
    // and 3 can't shift right
    // because cyclic right shift
    // takes place between 3 elements
    if(N == 3)
        Console.WriteLine("NO");

    // Check if its possible to sort
    else if(N % 4 == 0 || N % 4 == 1)
    {
        Console.WriteLine("YES");

        // Number of swap is
        // N / 2 always
        // for this approach
        Console.WriteLine(N / 2);
        int k = 1;

        // Printing index of the
        // cyclic right shift
        for(int l = 0; l < (N / 4); l++)
        {
            Console.WriteLine(k + " " + (k + 1) +
                                  " " + N);
            Console.WriteLine(k + 1 + " " + N +
                                      " " + (N - 1));
            k = k + 2;
            N = N - 2;
        }
    }
    else
        Console.WriteLine("NO");
}

// Driver code
public static void Main()
{
    int N = 5;
    int []arr = { 5, 4, 3, 2, 1 };

    sortarray(arr, N);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program for the above approach

function sortarray(arr,N)
{
    // If array is 3 2 1 can't
    // be sorted because 2 is in
    // its correct position, 1
    // and 3 can't shift right
    // because cyclic right shift
    // takes place between 3 elements
    if(N == 3)
        document.write("NO<br>");

    // Check if its possible to sort
    else if(N % 4 == 0 || N % 4 == 1)
    {
        document.write("YES<br>");

        // Number of swap is
        // N / 2 always
        // for this approach
        document.write(Math.floor(N / 2)+"<br>");
        let k = 1, l;

        // Printing index of the
        // cyclic right shift
        for(l = 0; l < Math.floor(N / 4); l++)
        {
        document.write(k + " " + (k + 1) +
                               " " + N+"<br>");
        document.write(k + 1 + " " +
                           N + " " + (N - 1)+"<br>");
        k = k + 2;
        N = N - 2;
        }
    }
    else
        document.write("NO<br>");
}

// Driver code
let N = 5;
let arr=[ 5, 4, 3, 2, 1];
sortarray(arr, N);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
YES
2
1 2 5
2 5 4
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*