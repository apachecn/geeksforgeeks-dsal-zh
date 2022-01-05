# Java 中的排序

> 原文:[https://www.geeksforgeeks.org/sorting-in-java/](https://www.geeksforgeeks.org/sorting-in-java/)

每当我们听到排序算法开始发挥作用时，比如选择排序、冒泡排序、插入排序、基数排序、桶排序等等，但是如果我们仔细看这里，我们不会被要求使用任何类型的算法。借助 java 中存在的线性和非线性数据结构，它就像排序一样简单。因此，在 java 中，排序是在循环的帮助下借助蛮力完成的，在 Java 中，有两种内置的排序方法。

**Java 中的排序方式**

1.  使用循环
2.  使用数组类的 sort()方法
3.  使用集合类的排序方法
4.  在子阵列上排序

让我们讨论这四个问题，并为每个问题提出一个代码。

**方式 1:** 使用循环

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to sort an elements
// by bringing Arrays into play

// Main class
class GFG {

    // Main driver method
    public static void main(String[] args)
    {

        // Custom input array
        int arr[] = { 4, 3, 2, 1 };

        // Outer loop
        for (int i = 0; i < arr.length; i++) {

            // Inner nested loop pointing 1 index ahead
            for (int j = i + 1; j < arr.length; j++) {

                // Checking elements
                int temp = 0;
                if (arr[j] < arr[i]) {

                    // Swapping
                    temp = arr[i];
                    arr[i] = arr[j];
                    arr[j] = temp;
                }
            }

            // Printing sorted array elements
            System.out.print(arr[i] + " ");
        }
    }
}
```

**Output**

```
1 2 3 4 
```

**方式二:**使用数组类**的排序()方法**

[数组。Sort()](https://www.geeksforgeeks.org/arrays-sort-in-java-with-examples/) 适用于原始数据类型的数组，默认情况下，这些数组也按升序排序。

**例 1**

## Java 语言（一种计算机语言，尤用于创建网站）

```
// Java program to demonstrate working of
// sort() method of Arrays class

// Importing Arrays class from java.util package
import java.util.Arrays;

// Main class
public class GFG {

    // Main driver method
    public static void main(String[] args)
    {
        // Custom input array
        int[] arr = { 13, 7, 6, 45, 21, 9, 101, 102 };

        // Calling the sort() method present
        // inside Arrays class
        Arrays.sort(arr);

        // Printing and display sorted array
        System.out.printf("Modified arr[] : %s",
                          Arrays.toString(arr));
    }
}
```

**Output**

```
Modified arr[] : [6, 7, 9, 13, 21, 45, 101, 102]
```

**例 2**

## Java 语言（一种计算机语言，尤用于创建网站）

```
// A sample Java program to sort an array
// in descending order using Arrays.sort().
import java.util.Arrays;
import java.util.Collections;

public class GFG {
    public static void main(String[] args)
    {
        // Note that we have Integer here instead of
        // int[] as Collections.reverseOrder doesn't
        // work for primitive types.
        Integer[] arr = { 13, 7, 6, 45, 21, 9, 2, 100 };

        // Sorts arr[] in descending order
        Arrays.sort(arr, Collections.reverseOrder());

        System.out.printf("Modified arr[] : %s",
                          Arrays.toString(arr));
    }
}
```

**Output**

```
Modified arr[] : [100, 45, 21, 13, 9, 7, 6, 2]
```

**方式 3:** 使用 Collections 类的 sort()方法

[Collections.sort()](https://www.geeksforgeeks.org/collections-sort-java-examples/) 适用于数组列表和链接列表等对象集合。

**例**

## Java 语言（一种计算机语言，尤用于创建网站）

```
// Java program to demonstrate working of Collections.sort()
import java.util.*;

public class GFG {
    public static void main(String[] args)
    {
        // Create a list of strings
        ArrayList<String> al = new ArrayList<String>();
        al.add("Geeks For Geeks");
        al.add("Friends");
        al.add("Dear");
        al.add("Is");
        al.add("Superb");

        /* Collections.sort method is sorting the
        elements of ArrayList in ascending order. */
        Collections.sort(al);

        // Let us print the sorted list
        System.out.println("List after the use of"
                           + " Collection.sort() :\n" + al);
    }
}
```

**Output**

```
List after the use of Collection.sort() :
[Dear, Friends, Geeks For Geeks, Is, Superb]
```

**例 2**

## Java 语言（一种计算机语言，尤用于创建网站）

```
// Java program to demonstrate working of Collections.sort()
// to descending order.
import java.util.*;

public class GFG {
    public static void main(String[] args)
    {
        // Create a list of strings
        ArrayList<String> al = new ArrayList<String>();
        al.add("Geeks For Geeks");
        al.add("Friends");
        al.add("Dear");
        al.add("Is");
        al.add("Superb");

        /* Collections.sort method is sorting the
        elements of ArrayList in ascending order. */
        Collections.sort(al, Collections.reverseOrder());

        // Let us print the sorted list
        System.out.println("List after the use of"
                           + " Collection.sort() :\n" + al);
    }
}
```

**Output**

```
List after the use of Collection.sort() :
[Superb, Is, Geeks For Geeks, Friends, Dear]
```

**方式 4:** 只排序一个子阵列

## Java 语言（一种计算机语言，尤用于创建网站）

```
// Java program to sort a subarray
// using Arrays.sort()

// Importing Arrays class from java.util package
import java.util.Arrays;

// Main class
public class GFG {

    // Main drive method
    public static void main(String[] args)
    {
        // Custom input array
        int[] arr = { 13, 7, 6, 45, 21, 9, 2, 100 };

        // Sort subarray from index 1 to 4, i.e.,
        // only sort subarray {7, 6, 45, 21} and
        // keep other elements as it is.
        Arrays.sort(arr, 1, 5);

        // Printing sorted array
        System.out.printf("Modified arr[] : %s",
                          Arrays.toString(arr));
    }
}
```

**Output**

```
Modified arr[] : [13, 6, 7, 21, 45, 9, 2, 100]
```

> **注:**
> 
> *   【Java 在 sort()中使用哪种排序算法？
>     以前，Java 的 Arrays.sort 方法对基元数组使用快速排序，对对象数组使用合并排序。在最新版本的 Java 中，Arrays.sort 方法和 Collection.sort()使用的是 Timsort。
> *   **默认做哪种排序顺序？**
>     默认按升序排序。
> *   **数组或列表如何降序排序？**
>     可以借助 Collections.reverseOrder()完成。
> *   **如何用 Java 编写自己的排序函数？**
>     请参见 Java 程序中的[快速排序](https://www.geeksforgeeks.org/java-program-for-quicksort/)[合并排序](https://www.geeksforgeeks.org/java-program-for-merge-sort/)[插入排序](https://www.geeksforgeeks.org/java-program-for-insertion-sort/)[选择排序](https://www.geeksforgeeks.org/java-program-for-selection-sort/)[堆排序](https://www.geeksforgeeks.org/java-program-for-heap-sort/)[冒泡排序](https://www.geeksforgeeks.org/java-program-for-bubble-sort/)