# 给定数组中计数大小为 3 的倒排的 Javascript 程序

> 原文:[https://www . geesforgeks . org/JavaScript-程序到计数-给定数组中三个大小的反转/](https://www.geeksforgeeks.org/javascript-program-to-count-inversions-of-size-three-in-a-given-array/)

给定大小为 n 的数组 arr[]。如果 a[i] > a[j] >a[k]和 i < j < k. Find total number of inversions of size 3.
**的话，三个元素 arr[i]、arr[j]和 arr[k]形成大小为 3 的反转。示例:**

```
Input:  {8, 4, 2, 1}
Output: 4
The four inversions are (8,4,2), (8,4,1), (4,2,1) and (8,2,1).

Input:  {9, 6, 4, 5, 8}
Output:  2
The two inversions are {9, 6, 4} and {9, 6, 5}
```

我们已经通过[合并排序](https://www.geeksforgeeks.org/counting-inversions/)、[自平衡 BST](https://www.geeksforgeeks.org/count-inversions-in-an-array-set-2-using-self-balancing-bst/) 和 [BIT](https://www.geeksforgeeks.org/count-inversions-array-set-3-using-bit/) 讨论了大小二的反转计数。
**简单方法:-** 循环 I、j 和 k 的所有可能值，并检查条件 a[i] > a[j] > a[k]和 I<j<k

## java 描述语言

```
<script>
// A simple Javascript implementation  to count inversion of size 3

    // returns count of inversion of size 3
    function getInvCount(arr, n)
    {
        let invcount = 0; // initialize result

        for(let i = 0 ; i < n - 2; i++)
        {
            for(let j = i + 1; j < n - 1; j++)
            {
                if(arr[i] > arr[j])
                {
                    for(let k = j + 1; k < n; k++)
                    {
                        if(arr[j] > arr[k])
                            invcount++;
                    }
                }
            }
        }
        return invcount;
    }

    // driver program to test above function
    let arr = [8, 4, 2, 1];
    let n = arr.length;
    document.write("Inversion count : " + 
                    getInvCount(arr, n));

    // This code is contributed by rag2127

</script>
```

输出:

```
Inversion Count : 4 
```

**时间复杂度**这个方法是:O(n^3)
**更好的方法:**
我们可以降低复杂度，如果我们把每个元素 arr[i]看作求逆的中间元素，找出所有大于 a[i]且指数小于 I 的数字，找出所有小于 a[i]且指数大于 I 的数字，我们把大于 a[i]的元素数乘以小于 a[i]的元素数，加到结果中。
下面是想法的实现。

## java 描述语言

```
<script>
// A O(n^2) Javascript  program to count inversions of size 3

    // returns count of inversion of size 3
    function getInvCount(arr, n)
    {
        let invcount = 0; // initialize result

        for (let i = 0 ; i < n - 1; i++)
        {
            // count all smaller elements on right of arr[i]
            let small = 0;
            for (let j = i + 1; j < n; j++)
                if (arr[i] > arr[j])
                    small++;

            // count all greater elements on left of arr[i]
            let great = 0;
            for (let j = i - 1; j >= 0; j--)
                    if (arr[i] < arr[j])
                        great++;

            // update inversion count by adding all inversions
            // that have arr[i] as middle of three elements
            invcount += great*small;
        }
        return invcount;
    }

    // driver program to test above function
    let arr=[8, 4, 2, 1];
    let n = arr.length;
    document.write("Inversion count : " +getInvCount(arr, n));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
Inversion Count : 4 
```

**时间复杂度**这种方法:O(n^2)
**二进制索引树方法:**
像大小为 2 的逆矩阵一样，我们可以使用二进制索引树来寻找大小为 3 的逆矩阵。强烈建议先参考下面的文章。
[使用 BIT](https://www.geeksforgeeks.org/count-inversions-array-set-3-using-bit/)
计算大小二的倒位，思路与上述方法类似。我们计算所有元素中较大元素和较小元素的数量，然后将较大的[]乘以较小的[]并将其添加到结果中。
**解决方案:**

1.  为了找出索引中较小元素的数量，我们从 n-1 迭代到 0。对于每个元素 a[i]，我们计算(a[i]-1)的 getSum()函数，该函数给出直到 a[i]-1 的元素数量。
2.  为了找出索引中较大元素的数量，我们从 0 迭代到 n-1。对于每个元素 a[i]，我们通过 getSum()计算直到 a[i]为止的数字总和(小于或等于 a[i]的总和)，并将其从 I 中减去(因为 I 是直到该点为止的元素总数)，这样我们就可以得到大于 a[i]的元素数量。

更多细节请参考完整的文章[计算给定数组](https://www.geeksforgeeks.org/count-inversions-of-size-three-in-a-give-array/)中大小为三的反转！