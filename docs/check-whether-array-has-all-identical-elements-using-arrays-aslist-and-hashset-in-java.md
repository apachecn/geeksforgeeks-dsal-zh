# 使用 Arrays.asList()和 Java 中的 HashSet 检查数组是否有所有相同的元素

> 原文:[https://www . geeksforgeeks . org/check-array-是否具有全部相同的元素-使用数组-as list-and-hashset-in-Java/](https://www.geeksforgeeks.org/check-whether-array-has-all-identical-elements-using-arrays-aslist-and-hashset-in-java/)

给定一个由 **N** 个元素组成的数组 **arr[]** ，任务是在不使用循环的情况下检查该数组是否有所有相同(相同)的元素。如果所有元素都相同，则打印“是”，否则打印“否”

**示例:**

> **输入:** arr[] = {2，2，2，2，2}
> **输出:**是
> 给定数组具有所有相同的元素，即 2。
> 
> **输入:** arr[] = {2，3，3，3，3，2，2 }
> T3】输出:否

**方法:**首先，我们检查数组的大小如果一个数组的大小是 0 或 1，那么这个数组就是相同的。如果它的大小是 **> 1** ，那么我们取一个集合，使用 [Arrays.asList()](https://www.geeksforgeeks.org/arrays-aslist-method-in-java-with-examples/) 复制集合中数组的所有元素。然后我们计算集合的大小，如果集合的大小是 **1** ，那么数组中有所有相同的元素，否则没有。

下面是上述方法的实现:

```
// Java implementation of the approach
import java.util.*;

class GFG {

    // Generic function to check whether the given array
    // has all identical element or not
    public static <T> void checkIdentical(T array[])
    {

        // Create the Set by passing the Array
        // as parameter in the constructor
        Set<T> set = new HashSet<>(Arrays.asList(array));

        // Check the size of set, f size is 0 or 1 then
        // array has only identical elements
        if (set.size() == 1 || set.isEmpty()) {
            System.out.print("Yes");
        }
        else {
            System.out.print("No");
        }
    }

    // Driver code
    public static void main(String args[])
    {
        Integer arr[] = { 2, 2, 2, 2, 2, 2 };
        checkIdentical(arr);
    }
}
```

**Output:**

```
Yes

```