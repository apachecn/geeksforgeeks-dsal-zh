# 在 Java 中的排序数组中搜索相等、更大或更小

> 原文:[https://www . geeksforgeeks . org/search-equal-big-or-small-in-sorted-array-in-Java/](https://www.geeksforgeeks.org/search-equal-bigger-or-smaller-in-a-sorted-array-in-java/)

给定排序整数数组，搜索键和搜索首选项查找数组位置。搜索首选项可以是:
1)EQUAL–仅搜索 EQUAL 键，如果未找到，则搜索-1。这是一个普通的二分搜索法。
2)EQUAL _ OR _ small–仅搜索 EQUAL 键或最接近的 small。-1 如果没有找到。
3)EQUAL _ OR _ BIGGER–仅搜索 EQUAL 关键字或最接近的 BIGGER。-1 如果没有找到。

示例:

```
Input : { 0, 2, 4, 6 }, key -1, EQUAL 
Output : -1

Input : { 0, 2, 4, 6 }, key -1, EQUAL_OR_BIGGER
Output : 0

Input : { 0, 2, 4, 6 }, key 7, EQUAL_OR_BIGGER
Output : -1

Input : { 0, 2, 4, 6 }, key 7, EQUAL_OR_SMALLER
Output : 3

```

在常规二分搜索法算法中，只要子阵列大小大于 0，就执行评估和除法。
在我们的例子中，如果我们想要保持单一功能，我们需要在大小=2 的子阵列中执行最终评估。只有在子阵列大小==2 的情况下，才能同时检查 EQUAL _ OR _ SMALLER 和 EQUAL_OR_BIGGER 条件。

在下面的代码中， **SC 代表搜索标准**。

```
public class BinarySearchEqualOrClose {

    private static void printResult(int key, int pos,
                                    SC sC)
    {
        System.out.println("" + key + ", " + sC + ":" + pos);
    }

    enum SC {
        EQUAL,
        EQUAL_OR_BIGGER,
        EQUAL_OR_SMALLER
    };

    public static int searchEqualOrClose(int key, int[] arr, SC sC)
    {
        if (arr == null || arr.length == 0) {
            return -1;
        }

        if (arr.length == 1) { // just eliminate case of length==1

            // since algorithm needs min array size==2
            // to start final evaluations
            if (arr[0] == key) {
                return 0;
            }
            if (arr[0] < key && sC == SC.EQUAL_OR_SMALLER) {
                return 0;
            }
            if (arr[0] > key && sC == SC.EQUAL_OR_BIGGER) {
                return 0;
            }
            return -1;
        }
        return searchEqualOrClose(arr, key, 0, arr.length - 1, sC);
    }

    private static int searchEqualOrClose(int[] arr, int key,
                                          int start, int end, SC sC)
    {
        int midPos = (start + end) / 2;
        int midVal = arr[midPos];
        if (midVal == key) {
            return midPos; // equal is top priority
        }

        if (start >= end - 1) {
            if (arr[end] == key) {
                return end;
            }
            if (sC == SC.EQUAL_OR_SMALLER) {

                // find biggest of smaller element
                if (arr[start] > key && start != 0) {

                    // even before if "start" is not a first
                    return start - 1;
                }
                if (arr[end] < key) {
                    return end;
                }
                if (arr[start] < key) {
                    return start;
                }
                return -1;
            }
            if (sC == SC.EQUAL_OR_BIGGER) {

                // find smallest of bigger element
                if (arr[end] < key && end != arr.length - 1) {

                    // even after if "end" is not a last
                    return end + 1;
                }
                if (arr[start] > key) {
                    return start;
                }
                if (arr[end] > key) {
                    return end;
                }
                return -1;
            }
            return -1;
        }
        if (midVal > key) {
            return searchEqualOrClose(arr, key, start, midPos - 1, sC);
        }
        return searchEqualOrClose(arr, key, midPos + 1, end, sC);
    }

    public static void main(String[] args)
    {
        int[] arr = new int[] { 0, 2, 4, 6 };

        // test full range of xs and SearchCriteria
        for (int x = -1; x <= 7; x++) {
            int pos = searchEqualOrClose(x, arr, SC.EQUAL);
            printResult(x, pos, SC.EQUAL);
            pos = searchEqualOrClose(x, arr, SC.EQUAL_OR_SMALLER);
            printResult(x, pos, SC.EQUAL_OR_SMALLER);
            pos = searchEqualOrClose(x, arr, SC.EQUAL_OR_BIGGER);
            printResult(x, pos, SC.EQUAL_OR_BIGGER);
        }
    }
}
```

**Output:**

```
-1, EQUAL:-1
-1, EQUAL_OR_SMALLER:-1
-1, EQUAL_OR_BIGGER:0
0, EQUAL:0
0, EQUAL_OR_SMALLER:0
0, EQUAL_OR_BIGGER:0
1, EQUAL:-1
1, EQUAL_OR_SMALLER:0
1, EQUAL_OR_BIGGER:1
2, EQUAL:1
2, EQUAL_OR_SMALLER:1
2, EQUAL_OR_BIGGER:1
3, EQUAL:-1
3, EQUAL_OR_SMALLER:1
3, EQUAL_OR_BIGGER:2
4, EQUAL:2
4, EQUAL_OR_SMALLER:2
4, EQUAL_OR_BIGGER:2
5, EQUAL:-1
5, EQUAL_OR_SMALLER:2
5, EQUAL_OR_BIGGER:3
6, EQUAL:3
6, EQUAL_OR_SMALLER:3
6, EQUAL_OR_BIGGER:3
7, EQUAL:-1
7, EQUAL_OR_SMALLER:3
7, EQUAL_OR_BIGGER:-1

```

时间复杂度:0(对数 n)