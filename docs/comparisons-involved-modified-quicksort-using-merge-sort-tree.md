# 使用合并排序树修改快速排序时涉及的比较

> 原文:[https://www . geeksforgeeks . org/comparison-涉案-修改-快速排序-使用-合并-排序-树/](https://www.geeksforgeeks.org/comparisons-involved-modified-quicksort-using-merge-sort-tree/)

在[快速排序](https://www.geeksforgeeks.org/quick-sort/)中，理想的情况是始终选择中间值作为枢轴，因为这导致时间最短。在本文中，[合并排序树](https://www.geeksforgeeks.org/merge-sort-tree-smaller-or-equal-elements-in-given-row-range/)用于在快速排序中查找不同范围的中间值，并分析比较的次数。
示例:

```
Input : arr = {4, 3, 5, 1, 2}
Output : 11
Explanation
We have to make 11 comparisons when we 
apply quick sort to the array.
```

如果我们仔细分析快速排序算法，那么每当数组被赋予快速排序函数时，数组总是由 L 到 r 范围内的数字排列组成。最初，它是[1 到 N]，然后是[1 到 pivot–1]和[pivot + 1 到 N]等等。此外，不容易观察到每个可能数组中数字的相对顺序没有变化。现在为了得到枢轴元素，我们只需要得到中间的数字，即数组中的(r–l+2)/2<sup>第</sup>个数字。
要有效地做到这一点，我们可以使用[持久段树](https://www.geeksforgeeks.org/persistent-segment-tree-set-1-introduction/)、[分支树](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)或[合并排序树](https://www.geeksforgeeks.org/merge-sort-tree-smaller-or-equal-elements-in-given-row-range/)。本文主要讨论合并排序树的实现。
在修改后的快速排序算法中，我们选择了数组的枢轴元素作为数组的中值。现在，确定中值需要我们在对数组进行排序后找到所考虑的中间元素，这本身就是一个 O(n*log(n))运算，其中 n 是数组的大小。
假设我们有一个范围 L 到 R，那么这个范围的中值计算如下:

```
Median of A[L; R] = Middle element of sorted(A[L; R])
                  = (R - L + 1)/2th element of 
                    sorted(A[L; R])
```

让我们考虑在快速排序算法中我们有 P 个分区，这意味着我们必须通过对从 L 到 R 的数组范围进行排序来找到轴心，其中 L 和 R 是每个分区的起点和终点。这是昂贵的。
**但是**，我们在每个分区中都有一个从 L 到 R 的数字排列，所以我们可以找到天花板((R–L+1)/2)<sup>这个范围内的最小数字，因为我们知道当我们对这个分区进行排序时，总是这个元素会作为中间元素结束，结果也是枢轴。现在，小于 pivot 的元素转到左边的子树，大于 pivot 的元素转到右边的子树，并保持它们的顺序。
我们对所有分区 P 重复这个过程，并找出每个分区中涉及的比较。因为在当前分区中，从 L 到 R 的所有元素都与枢轴进行比较，所以我们在当前分区中进行(R–L+1)比较。我们还需要通过递归计算来考虑左右子树的总比较。由此我们得出结论，</sup> 

```
Total Comparisons =  Comparisons in Current Partition +
                     Comparisons in Left partition +
                     Comparisons in right partition
```

我们在上面讨论了使用合并排序树有效查找枢轴元素的方法
[K <sup>第</sup>个顺序统计可以用来查找与上面讨论的相同的内容。](https://www.geeksforgeeks.org/merge-sort-tree-for-range-order-statistics/) 

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to implement number of comparisons
// in modified quick sort
#include <bits/stdc++.h>
using namespace std;

const int MAX = 1000;

// Constructs a segment tree and stores tree[]
void buildTree(int treeIndex, int l, int r, int arr[],
               vector<int> tree[])
{

    /*  l => start of range,
        r => ending of a range
        treeIndex => index in the Segment Tree/Merge
                     Sort Tree  */
    /* leaf node */
    if (l == r) {
        tree[treeIndex].push_back(arr[l - 1]);
        return;
    }

    int mid = (l + r) / 2;

    /* building left subtree */
    buildTree(2 * treeIndex, l, mid, arr, tree);

    /* building left subtree */
    buildTree(2 * treeIndex + 1, mid + 1, r, arr, tree);

    /* merging left and right child in sorted order */
    merge(tree[2 * treeIndex].begin(),
          tree[2 * treeIndex].end(),
          tree[2 * treeIndex + 1].begin(),
          tree[2 * treeIndex + 1].end(),
          back_inserter(tree[treeIndex]));
}

// Returns the Kth smallest number in query range
int queryRec(int segmentStart, int segmentEnd,
             int queryStart, int queryEnd, int treeIndex,
             int K, vector<int> tree[])
{
    /*  segmentStart => start of a Segment,
        segmentEnd   => ending of a Segment,
        queryStart   => start of a query range,
        queryEnd     => ending of a query range,
        treeIndex    => index in the Segment
                        Tree/Merge Sort Tree,
        K  => kth smallest number to find  */
    if (segmentStart == segmentEnd)
        return tree[treeIndex][0];

    int mid = (segmentStart + segmentEnd) / 2;

    // finds the last index in the segment
    // which is <= queryEnd
    int last_in_query_range =
             (upper_bound(tree[2 * treeIndex].begin(),
               tree[2 * treeIndex].end(), queryEnd)
                    - tree[2 * treeIndex].begin());

    // finds the first index in the segment
    // which is >= queryStart
    int first_in_query_range =
              (lower_bound(tree[2 * treeIndex].begin(),
              tree[2 * treeIndex].end(), queryStart)
                       - tree[2 * treeIndex].begin());

    int M = last_in_query_range - first_in_query_range;

    if (M >= K) {

        // Kth smallest is in left subtree,
        // so recursively call left subtree for Kth
        // smallest number
        return queryRec(segmentStart, mid, queryStart,
                        queryEnd, 2 * treeIndex, K, tree);
    }

    else {

        // Kth smallest is in right subtree,
        // so recursively call right subtree for the
        // (K-M)th smallest number
        return queryRec(mid + 1, segmentEnd, queryStart,
                queryEnd, 2 * treeIndex + 1, K - M, tree);
    }
}

// A wrapper over query()
int query(int queryStart, int queryEnd, int K, int n, int arr[],
          vector<int> tree[])
{

    return queryRec(1, n, queryStart, queryEnd,
                    1, K, tree);
}

/* Calculates total Comparisons Involved in Quick Sort
   Has the following parameters:

   start => starting index of array
   end   => ending index of array
   n     => size of array
   tree  => Merge Sort Tree */

int quickSortComparisons(int start, int end, int n, int arr[],
                         vector<int> tree[])
{
    /* Base Case */
    if (start >= end)
        return 0;

    // Compute the middle point of range and the pivot
    int middlePoint = (end - start + 2) / 2;
    int pivot = query(start, end, middlePoint, n, arr, tree);

    /* Total Comparisons = (Comparisons in Left part +
                            Comparisons of right +
                            Comparisons in parent) */

    // count comparisons in parent array
    int comparisons_in_parent = (end - start + 1);

    // count comparisons involved in left partition
    int comparisons_in_left_part =
     quickSortComparisons(start, pivot - 1, n, arr, tree);

    // count comparisons involved in right partition
    int comparisons_in_right_part =
      quickSortComparisons(pivot + 1, end, n, arr, tree);

    // Return Total Comparisons
    return comparisons_in_left_part +
           comparisons_in_parent +
           comparisons_in_right_part;
}

// Driver code
int main()
{
    int arr[] = { 4, 3, 5, 1, 2 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Construct segment tree in tree[]
    vector<int> tree[MAX];
    buildTree(1, 1, n, arr, tree);

    cout << "Number of Comparisons = "
        << quickSortComparisons(1, n, n, arr, tree);;

    return 0;
}
```

输出:

```
Number of Comparisons = 11
```

计算中枢
的每个查询的复杂度为 0(log<sup>2</sup>(n))