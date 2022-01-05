# 冒泡排序、选择排序和插入排序的比较

> 原文:[https://www . geesforgeks . org/对比-冒泡-排序-选择-排序-插入-排序/](https://www.geeksforgeeks.org/comparison-among-bubble-sort-selection-sort-and-insertion-sort/)

### 1.[气泡排序](https://www.geeksforgeeks.org/bubble-sort/)

[**冒泡排序**](https://www.geeksforgeeks.org/bubble-sort/) 在每一遍中重复比较和交换(如果需要)相邻元素。在冒泡排序的**第 I 遍**(升序)**最后(i-1)个元素已经排序**，第 I 个最大的元素被放置在第(N-i)个位置，即第 I 个最后位置。

**算法:**

```
BubbleSort (Arr, N) // Arr is an array of size N.
{
    For ( I:= 1 to (N-1) ) // N elements => (N-1) pass
    {
    // Swap adjacent elements of Arr[1:(N-I)]such that
    // largest among { Arr[1], Arr[2], ..., Arr[N-I] } reaches to Arr[N-I]
        For ( J:= 1 to  (N-I) ) // Execute the pass
        {
            If ( Arr [J] > Arr[J+1] ) 
                Swap( Arr[j], Arr[J+1] );
        }
    }
}
```

**<u>算法优化</u> :** 检查内循环(传递执行循环)是否发生交换操作。如果在任何过程中没有交换，这意味着数组现在已经完全排序，因此不需要继续，停止排序操作。因此，当数组在所有遍数完成之前排序时，我们可以优化遍数。它还可以在第一遍中检测给定/输入数组是否排序。

```
BubbleSort (Arr, N) // Arr is an array of size N.
{
    For ( I:= 1 to (N-1) ) // N elements => (N-1) pass
    {
    // Swap adjacent elements of Arr[1:(N-I)]such that
    // largest among { Arr[1], Arr[2], ..., Arr[N-I] } reaches to Arr[N-I]
        noSwap = true; // Check occurrence of swapping in inner loop
        For ( J:= 1 to  (N-I) ) // Execute the pass
        {
            If ( Arr [J] > Arr[J+1] )
            { 
                Swap( Arr[j], Arr[J+1] );
                noSwap = false;
            }
        }
        If (noSwap) // exit the loop
            break;
    }
}
```

**<u>【时间复杂度】</u>** :

*   **最佳情况**排序数组作为输入。或者几乎所有的元素都在适当的位置。【 **O(N)** 】。 **O(1)** 互换。
*   **最差情况**:反向排序/很少元素在合适的位置。【 **O(N <sup>2</sup> )** 】。 **O(N <sup>2</sup> )** 互换。
*   **平均情况**:【**O(N<sup>2</sup>)**】。 **O(N <sup>2</sup> )** 互换。

**<u>空间复杂度</u>** :一个临时变量用于交换【辅助， **O(1)** 】。因此它是就地排序。

**<u>优势</u>** :

1.  这是最简单的排序方法。
2.  最佳情况复杂度为 **O(N)** 【针对优化方法】同时对数组进行排序。
3.  使用**优化方法**，它**可以检测第一遍**中已经排序的数组，时间复杂度为 **O(N)** 。
4.  稳定排序:不改变键相等的元素的相对顺序。
5.  就地排序。

**<u>劣势</u>** :

1.  冒泡排序是比较慢的算法。

### 2.[选择排序](https://www.geeksforgeeks.org/selection-sort/)

[选择排序](https://www.geeksforgeeks.org/selection-sort/)选择第 I 个最小元素，放在第 I 个位置。该算法将数组分为两部分:已排序(左)和未排序(右)子数组。它从未排序的子阵列中选择最小的元素，并放置在该子阵列的第一个位置(升序)。它反复选择下一个最小的元素。

**<u>算法</u> :**

```
SelectionSort (Arr, N) // Arr is an array of size N.
{
    For ( I:= 1 to (N-1) ) // N elements => (N-1) pass
    {
    // I=N is ignored, Arr[N] is already at proper place.
    // Arr[1:(I-1)] is sorted subarray, Arr[I:N] is undorted subarray
    // smallest among { Arr[I], Arr[I+1], Arr[I+2], ..., Arr[N] } is at place min_index

        min_index = I;
        For ( J:= I+1 to N ) // Search Unsorted Subarray (Right lalf)
        {
            If ( Arr [J] < Arr[min_index] ) 
                min_index = J; // Current minimum
        }
        // Swap I-th smallest element with current I-th place element
        If (min_Index != I)
              Swap ( Arr[I], Arr[min_index] ); 

    }
}
```

**<u>【时间复杂度】</u>** :

*   **最佳案例**【**O(N<sup>2</sup>)**】。和 **O(1)** 互换。
*   **最差情况**:反向排序，内循环最大比较时。【 **O(N <sup>2</sup> )** 】。此外， **O(N)** 互换。
*   **平均情况**:【**O(N<sup>2</sup>)**】。同样 **O(N)** 互换。

**<u>空间复杂度</u>** :【辅助， **O(1)** 】。就地排序。(当元素被移动而不是被交换时(即 temp=a[min]，然后将元素从 ar[i]移动到 ar[min-1]一个位置，然后放入 a[i]=temp)。如果选择交换，则算法不在原位。)

**<u>优势</u>** :

1.  它也可以用于列表结构，使添加和删除有效，如链表。只需移除未排序部分的最小元素，并在已排序部分的末尾结束。
2.  互换的数量减少了。 **O(N)** 在所有情况下互换。
3.  就地排序。

**<u>劣势</u>** :

1.  所有情况下的时间复杂度都是 **O(N <sup>2</sup> )** ，没有最佳情况场景。

### 3.[插入输出](https://www.geeksforgeeks.org/insertion-sort/)

[插入排序](https://www.geeksforgeeks.org/insertion-sort/)是一个简单的基于比较的排序算法。它将每个数组元素插入到其正确的位置。在第 I 次迭代中，先前的(i-1)元素(即子阵列 Arr[1:(i-1)])已经被排序，并且第 I 个元素(Arr[i])被插入到先前排序的子阵列中的适当位置。
在本 [GFG 链接](https://www.geeksforgeeks.org/insertion-sort/)中查找更多详情。

**<u>算法</u> :**

```
InsertionSort (Arr, N) // Arr is an array of size N.
{
    For ( I:= 2 to N ) // N elements => (N-1) pass
    {
    // Pass 1 is trivially sorted, hence not considered
    // Subarray { Arr[1], Arr[2], ..., Arr[I-I] } is already sorted

        insert_at = I; // Find suitable position insert_at, for Arr[I]
        // Move subarray Arr [ insert_at: I-1 ] to one position right

        item = Arr[I]; J=I-1;
        While ( J ? 1 && item < Arr[J] ) 
        {
                Arr[J+1] = Arr[J]; // Move to right   
                // insert_at = J;
                J--;
            }
            insert_at = J+1; // Insert at proper position
            Arr[insert_at] = item; // Arr[J+1] = item;
        }
    }
}
```

**<u>【时间复杂度】</u>** :

*   **最佳情况**排序数组作为输入，【 **O(N)** 】。和 **O(1)** 互换。
*   **最差情况**:反向排序，内环最大比较时，【 **O(N <sup>2</sup> )** 】。和 **O(N <sup>2</sup> )** 互换。
*   **平均情况**:【**O(N<sup>2</sup>)**】。和 **O(N <sup>2</sup> )** 互换。

**<u>空间复杂度</u>** :【辅助， **O(1)** 】。就地排序。

**<u>优势</u>** :

1.  它很容易计算。
2.  最佳情况复杂度为 **O(N)** ，而数组已经排序。
3.  互换数量比泡沫排序减少。
4.  对于较小的 N 值，插入排序的执行效率与其他二次排序算法类似。
5.  稳定型。
6.  Adaptive:减少部分排序数组的总步骤数。
7.  就地排序。

**<u>劣势</u>** :

1.  一般在 N 值较小时使用。对于**较大的 N** 值，是**低效**。

**时空复杂度:**

<figure class="table">

| 分类算法 | 时间复杂性 | 空间复杂性 |
| --- | --- | --- |
|   | 最佳案例 | 平均案例 | 最坏情况 | 最坏情况 |
| 冒泡排序 | **O(N)** | **O(N <sup>2</sup> )** | **O(N <sup>2</sup> )** | **O(1)** |
| 选择排序 | **O(N <sup>2</sup> )** | **O(N <sup>2</sup> )** | **O(N <sup>2</sup> )** | **O(1)** |
| 插入排序 | **O(N)** | **O(N <sup>2</sup> )** | **O(N <sup>2</sup> )** | **O(1)** |

</figure>