# 对选择排序略有改进的排序算法

> 原文:[https://www . geesforgeks . org/sorting-algorithm-略微改进-selection-sort/](https://www.geeksforgeeks.org/sorting-algorithm-slightly-improves-selection-sort/)

正如我们所知，[选择排序](https://www.geeksforgeeks.org/selection-sort/)算法在数组的每一遍取最小值，并将其放在正确的位置。
我们的想法是在每一关都取最大值，并将其放在正确的位置。因此，在每一遍中，我们都跟踪最大值和最小值，数组从两端开始排序。

**示例:**

```
First example: 7 8 5 4 9 2 
Input :pass 1:|7 8 5 4 9 2| 
       pass 2: 2|8 5 4 7|9
       pass 3: 2 4|5 7|8 9       
Output :A sorted array:  2 4 5 7 8 9

second example: 23 78 45 8 32 56 1      
Input :pass 1:|23 78 45 8 32 56 1|
       pass 2: 1|23 45 8 32 56 |78
       pass 3: 1 8|45 23 32|56 78
       pass 4: 1 8 23 |32|45 56 78
       in a case of odd elements, so one element
       left for sorting, so sorting stops and the
       array is sorted.
Output : A sorted array: 1 8 23 32 45 56 78
```

## C++

```
// C++ program to implement min max selection
// sort.
#include <iostream>
using namespace std;

void minMaxSelectionSort(int* arr, int n)
{
    for (int i = 0, j = n - 1; i < j; i++, j--) {
        int min = arr[i], max = arr[i];
        int min_i = i, max_i = i;
        for (int k = i; k <= j; k++)  {
            if (arr[k] > max) {
                max = arr[k];
                max_i = k;
            } else if (arr[k] < min) {
                min = arr[k];
                min_i = k;
            }
        }

        // shifting the min.
        swap(arr[i], arr[min_i]);

        // Shifting the max. The equal condition
        // happens if we shifted the max to arr[min_i]
        // in the previous swap.
        if (arr[min_i] == max)
            swap(arr[j], arr[min_i]);
        else
            swap(arr[j], arr[max_i]);
    }
}

// Driver code
int main()
{
    int arr[] = { 23, 78, 45, 8, 32, 56, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    minMaxSelectionSort(arr, n);
    printf("Sorted array:\n");
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement min max selection
// sort.
class GFG
{
static void minMaxSelectionSort(int[] arr, int n)
{
    for (int i = 0, j = n - 1; i < j; i++, j--)
    {
        int min = arr[i], max = arr[i];
        int min_i = i, max_i = i;
        for (int k = i; k <= j; k++)
        {
            if (arr[k] > max)
            {
                max = arr[k];
                max_i = k;
            }

            else if (arr[k] < min)
            {
                min = arr[k];
                min_i = k;
            }
        }

        // shifting the min.
        swap(arr, i, min_i);

        // Shifting the max. The equal condition
        // happens if we shifted the max to arr[min_i]
        // in the previous swap.
        if (arr[min_i] == max)
            swap(arr, j, min_i);
        else
            swap(arr, j, max_i);
    }
}

static int[] swap(int []arr, int i, int j)
{
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 23, 78, 45, 8, 32, 56, 1 };
    int n = arr.length;
    minMaxSelectionSort(arr, n);
    System.out.printf("Sorted array:\n");
    for (int i = 0; i < n; i++)
        System.out.print(arr[i] + " ");
    System.out.println("");
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to implement min
# max selection sort.

def minMaxSelectionSort(arr, n):
    i = 0
    j = n - 1
    while(i < j):
        min = arr[i]
        max = arr[i]
        min_i = i
        max_i = i
        for k in range(i, j + 1, 1):
            if (arr[k] > max):
                max = arr[k]
                max_i = k
            elif (arr[k] < min):
                min = arr[k]
                min_i = k

        # shifting the min.
        temp = arr[i]
        arr[i] = arr[min_i]
        arr[min_i] = temp

        # Shifting the max. The equal condition
        # happens if we shifted the max to
        # arr[min_i] in the previous swap.
        if (arr[min_i] == max):
            temp = arr[j]
            arr[j] = arr[min_i]
            arr[min_i] = temp
        else:
            temp = arr[j]
            arr[j] = arr[max_i]
            arr[max_i] = temp

        i += 1
        j -= 1

    print("Sorted array:", end = " ")
    for i in range(n):
        print(arr[i], end = " ")

# Driver code
if __name__== '__main__':
    arr = [23, 78, 45, 8, 32, 56, 1]
    n = len(arr)
    minMaxSelectionSort(arr, n)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to implement min max selection
// sort.
using System;

class GFG
{
static void minMaxSelectionSort(int[] arr, int n)
{
    for (int i = 0, j = n - 1;
             i < j; i++, j--)
    {
        int min = arr[i], max = arr[i];
        int min_i = i, max_i = i;
        for (int k = i; k <= j; k++)
        {
            if (arr[k] > max)
            {
                max = arr[k];
                max_i = k;
            }

            else if (arr[k] < min)
            {
                min = arr[k];
                min_i = k;
            }
        }

        // shifting the min.
        swap(arr, i, min_i);

        // Shifting the max. The equal condition
        // happens if we shifted the max to arr[min_i]
        // in the previous swap.
        if (arr[min_i] == max)
            swap(arr, j, min_i);
        else
            swap(arr, j, max_i);
    }
}

static int[] swap(int []arr, int i, int j)
{
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 23, 78, 45, 8, 32, 56, 1 };
    int n = arr.Length;
    minMaxSelectionSort(arr, n);
    Console.Write("Sorted array:\n");
    for (int i = 0; i < n; i++)
        Console.Write(arr[i] + " ");
    Console.WriteLine("");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to implement min
// max selection sort.
function swap(arr, xp, yp)
{
    var temp = arr[xp];
    arr[xp] = arr[yp];
    arr[yp] = temp;
}

function minMaxSelectionSort(arr, n)
{
    for(var i = 0, j = n - 1; i < j; i++, j--)
    {
        var min = arr[i];
        var max = arr[i];
        var min_i = i;
        var max_i = i;

        for(var k = i; k <= j; k++)
        {
            if (arr[k] > max)
            {
                max = arr[k];
                max_i = k;
            }
            else if (arr[k] < min)
            {
                min = arr[k];
                min_i = k;
            }
        }

        // Shifting the min.
        swap(arr, i, min_i);

        // Shifting the max. The equal condition
        // happens if we shifted the max to arr[min_i]
        // in the previous swap.
        if (arr[min_i] == max)
            swap(arr, j, min_i);
        else
            swap(arr, j, max_i);
    }
}

// Driver code
var arr = [ 23, 78, 45, 8, 32, 56, 1 ];
var n = 7;

minMaxSelectionSort(arr, n);

document.write("Sorted array:\n");
for(var i = 0; i < n; i++)
    document.write(arr[i] + " ");

document.write("<br>");

// This code is contributed by akshitsaxenaa09

</script>
```

**输出:**

```
 Sorted array: 1 8 23 32 45 56 78
```

本文由 [**什洛米·埃尔海亚尼**](https://www.facebook.com/shlomi.elhaiani) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。