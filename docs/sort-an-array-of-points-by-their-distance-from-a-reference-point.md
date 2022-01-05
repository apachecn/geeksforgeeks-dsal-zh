# 根据点与参考点的距离对点阵列进行排序

> 原文:[https://www . geeksforgeeks . org/按参考点距离排序点数组/](https://www.geeksforgeeks.org/sort-an-array-of-points-by-their-distance-from-a-reference-point/)

给定一个包含 **N** 点和一个参考点 **P** 的数组 **arr[]** ，任务是根据这些点与给定点 **P** 的距离对它们进行排序。

**示例:**

> **输入:** arr[] = {{5，0}，{4，0}，{3，0}，{2，0}，{1，0}}，P = (0，0)
> **输出:** (1，0) (2，0) (3，0) (4，0) (5，0)
> **解释:**
> (0，0)与(1，0) = 1
> 之间的距离(0，0)与(2，0) =
> 
> 因此，点的排序数组将是:{(1，0) (2，0) (3，0) (4，0) (5，0)}
> **输入:** arr[] = {{5，0}，{0，4}，{0，3}，{2，0}，{1，0}}，P = (0，0)
> **输出:** (1，0) (2，0) (0，3) (0，4) (5，0)
> **解释:【T8 0)和(0，3) = 3
> 之间的距离(0，0)和(0，4) = 4
> 之间的距离(0，0)和(5，0) = 5
> 因此，点的排序数组将是:{(1，0) (2，0) (0，3) (0，4) (5，0)}**

**方法:**思想是将每个元素存储在一个[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)中距离给定点 P 的距离处，然后根据存储的距离对[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)的所有元素进行排序。

*   对于每个给定的点:
    *   求该点距参考点 P 的[距离，公式如下:](https://www.geeksforgeeks.org/program-calculate-distance-two-points/)

```
Distance = 
```

*   在数组中追加距离
*   对距离数组进行排序，并根据排序后的距离打印点。
    *   **时间复杂度:**和上面的方法一样，有一个长度为 N 的数组的排序，在最坏的情况下需要 O(N*logN)的时间。因此，时间复杂度将是**O(N *对数 N)** 。
    *   **辅助空间复杂度:**和上面的方法一样，有额外的空间用来存储距离和成对的点。因此，辅助空间的复杂性将是 **O(N)** 。

## java 描述语言

```
<script>
// Javascript program

function sortFunction(a, b) {
    if (a[0] === b[0]) {
        return 0;
    }
    else {
        return (a[0] < b[0]) ? -1 : 1;
    }
}

// Function to sort the array of
// points by its distance from P
function sortArr(arr, n, p)
{
    // Vector to store the distance
    // with respective elements

    var vp = new Array(n);
    // Storing the distance with its
    // distance in the vector array
    for (var i = 0; i < n; i++) {

        var dist = Math.pow((p[0] - arr[i][0]), 2)
              + Math.pow((p[1] - arr[i][1]), 2);
        vp[i] = [dist, [arr[i][0], arr[i][1]]];
    }

    // Sorting the array with
    // respect to its distance
    vp.sort(sortFunction);

    // Output
    for (var i = 0; i < n; i++) {
        document.write("(" + vp[i][1][0] + ", " + vp[i][1][1] + ") ");
    }
}

var arr = [[ 5, 5 ], [ 6, 6 ], [ 1, 0], [ 2, 0 ], [ 3, 1 ], [ 1, -2 ]];
var n = 6;
var p = [ 0, 0 ];
// Function to perform sorting
sortArr(arr, n, p);
</script>
```

输出:

```
(1, 0) (2, 0) (1, -2) (3, 1) (5, 5) (6, 6) 
```