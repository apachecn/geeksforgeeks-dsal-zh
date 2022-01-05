# Python 中的 itertools.combinations()模块，用于打印所有可能的组合

> 原文:[https://www . geesforgeks . org/ITER tools-组合-模块-python-print-可能-组合/](https://www.geeksforgeeks.org/itertools-combinations-module-python-print-possible-combinations/)

给定大小为 n 的数组，生成并打印数组中 r 个元素的所有可能组合。

示例:

```
Input : arr[] = [1, 2, 3, 4],  
            r = 2
Output : [[1, 2], [1, 3], [1, 4], [2, 3], [2, 4], [3, 4]]

```

此问题已有递归解决方案请参考[打印给定大小 n 的数组中 r 个元素的所有可能组合](https://www.geeksforgeeks.org/print-all-possible-combinations-of-r-elements-in-a-given-array-of-size-n/)链接。我们将使用 **itertools.combinations()** 模块在 python 中解决这个问题。

### itertools.combinations()是做什么的？

它从输入表中返回 r 长度的元素子序列。组合按字典排序顺序发出。因此，如果输入的可迭代表被排序，组合元组将按排序顺序产生。

*   **<u>ITER tools . combinations(ITER able，r) :</u>**
    它以排序顺序返回 r 长度的元组，没有重复的元素。例如，组合(' ABCD '，2)=>[AB，AC，AD，BC，BD，CD]。
*   **<u>itertools.combinations_with_replacement(iterable, r) :</u>**
    It return r-length tuples in sorted order with repeated elements. For Example, combinations_with_replacement(‘ABCD’, 2) ==> [AA, AB, AC, AD, BB, BC, BD, CC, CD, DD].

    ```
    # Function which returns subset or r length from n
    from itertools import combinations

    def rSubset(arr, r):

        # return list of all subsets of length r
        # to deal with duplicate subsets use 
        # set(list(combinations(arr, r)))
        return list(combinations(arr, r))

    # Driver Function
    if __name__ == "__main__":
        arr = [1, 2, 3, 4]
        r = 2
        print (rSubset(arr, r))
    ```

    输出:

    ```
    [[1, 2], [1, 3], [1, 4], [2, 3], [2, 4], [3, 4]]

    ```

    本文由 [**沙莎克·米什拉(古卢)**](https://auth.geeksforgeeks.org/profile.php?user=Shashank Mishra) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

    如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。