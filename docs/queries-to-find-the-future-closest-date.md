# 查询查找未来最近的日期

> 原文:[https://www . geesforgeks . org/query-to-find-the-future-close-date/](https://www.geeksforgeeks.org/queries-to-find-the-future-closest-date/)

给定一个由 **N** 个字符串组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个由 **Q** 个查询组成的数组**查询【】**。数组 **arr[]** 和 **Query[]** 中的每个字符串都是 **D/M/Y** 的形式，其中 **D** 、 **M** 和 **Y** 表示日期、月份和年份。对于每个查询，任务是打印给定数组中下一个最近的日期 **arr[]** 。如果没有这样的日期，打印**-1”**。

**示例:**

> **输入:**arr[]= {“22/4/1233”、“1/3/633”、“23/5/56645”、“4/12/233”}，Q = 2，
> 查询[]= {“23/3/4345”、“12/3/2”}
> **输出:**T6】23/5/56645
> 4/12/233
> **说明: ****查询 2:**“12/3/2”之后最近的日期为“4/12/233”。****
> 
> **输入:**arr[]= {“22/4/1233”、“4/12/233”、“1/3/633”、“23/5/56645”}，Q = 1，
> Query[]= {“4/4/34234234”}
> T4】输出: -1

**天真方法:**数组中每个查询最简单的方法**查询【】**是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**对于每个日期，检查它是否大于当前日期，以及它是否最接近当前日期。完成数组遍历后，打印获得的最近日期。如果没有找到日期，打印 **-1** 。

***时间复杂度:** O(N*Q)*
***辅助空间:** O(1)*

**高效方法:**想法是使用[比较器功能](https://www.geeksforgeeks.org/comparator-class-in-c-with-examples/)对给定数组 **arr[]** 进行[排序。然后用一个](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)[二分搜索法](https://www.geeksforgeeks.org/binary-search/)在**查询[]** 中找到最接近每个日期的未来日期。按照以下步骤解决问题:

1.  [通过首先比较**年**，然后是**月**，接着是**日**，对日期数组**arr【】**进行排序。](https://www.geeksforgeeks.org/arrays-sort-in-java-with-examples/)
2.  对上一步中的数组进行排序后，对于每个查询，使用 **[【二分搜索法】](https://www.geeksforgeeks.org/binary-search/)** 查找最近的日期，使用比较器函数比较两个日期。
3.  如果没有找到有效日期，则打印**-1”**。
4.  否则，打印找到的最近日期。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.awt.*;
import java.io.*;
import java.util.*;

class GFG {

    // Comparator function to compare
    // the two dates
    public static int comp(String s,
                           String t)
    {

        // Split the dates strings
        // when a "/" found
        String[] ss = s.split("/");
        String[] tt = t.split("/");

        int date1[] = new int[3];
        int date2[] = new int[3];

        // Store the dates in form
        // of arrays
        for (int i = 0; i < 3; i++) {
            date1[i]
                = Integer.parseInt(ss[i]);
            date2[i]
                = Integer.parseInt(tt[i]);
        }

        // If years are not same
        if (date1[2] != date2[2]) {
            return date1[2] - date2[2];
        }

        // If months are not same
        else if (date1[1] != date2[1]) {
            return date1[1] - date2[1];
        }

        // If days are not same
        else if (date1[0] != date2[0]) {
            return date1[0] - date2[0];
        }

        // If two date is same
        return 0;
    }

    // Function to print the next
    // closest date
    public static String
    nextClosestDate(String arr[],
                    String q)
    {
        // Sort date array
        Arrays.sort(arr,
                    new Comparator<String>() {

                        @Override
                        public int compare(String o1,
                                           String o2)
                        {
                            return comp(o1, o2);
                        }
                    });

        // Perform the Binary search
        // to answer the queries
        int l = 0, r = arr.length - 1;
        int ind = -1;

        // Iterate until l <= r
        while (l <= r) {

            // Find mid m
            int m = (l + r) / 2;

            // Comparator function call
            int c = comp(q, arr[m]);

            // If comp function return 0
            // next closest date is found
            if (c == 0) {
                ind = m;
                break;
            }

            // If comp function return
            // less than 0, search in
            // the left half
            else if (c < 0) {
                r = m - 1;
                ind = m;
            }

            // If comp function return
            // greater than 0, search
            // in the right half
            else {
                l = m + 1;
            }
        }

        // Return the result
        if (ind == -1) {
            return "-1";
        }
        else {
            return arr[ind];
        }
    }

    public static void
        performQueries(String[] arr,
                       String[] Q)
    {
        // Traverse the queries of date
        for (int i = 0; i < Q.length; i++) {

            // Function Call
            System.out.println(
                nextClosestDate(arr, Q[i]));
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array of dates
        String arr[] = { "22/4/1233",
                         "1/3/633",
                         "23/5/56645",
                         "4/12/233" };

        // Given Queries
        String Q[]
            = { "23/3/4345",
                "4/4/34234234",
                "12/3/2" };

        // Function Call
        performQueries(arr, Q);
    }
}
```

**Output:**

```
23/5/56645
-1
4/12/233

```

***时间复杂度:** O((N*log N) + (Q*log N))
**辅助空间:** O(1)*