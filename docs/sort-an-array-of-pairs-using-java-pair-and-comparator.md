# 使用 Java Pair 和 Comparator 对数组进行排序

> 原文:[https://www . geesforgeks . org/sort-a-array-of-of-pair-use-Java-pair-and-comparator/](https://www.geeksforgeeks.org/sort-an-array-of-pairs-using-java-pair-and-comparator/)

给定整数对的数组。任务是根据数组对中的第二个元素对数组进行排序。

示例:

```
Input: [(1, 2), (3, 5), (2, 6), (1, 7)]
Output: [(1, 2), (3, 5), (2, 6), (1, 7)]

Input: [(10, 20), (20, 30), (5, 6), (2, 5)]
Output: [(2, 5), (5, 6), (10, 20), (20, 30)]

```

**进场:**

*   使用用户定义的*配对类*将配对存储在数组中。
*   重写比较器方法，根据第一个元素对数组进行排序。
*   根据第一个元素对数组进行排序。

下面是上述方法的实现:

```
// Java code to sort the array
// according to second element
import java.io.*;
import java.util.*;

// User defined Pair class
class Pair {
    int x;
    int y;

    // Constructor
public Pair(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
}

// class to define user defined conparator
class Compare {

    static void compare(Pair arr[], int n)
    {
        // Comparator to sort the pair according to second element
        Arrays.sort(arr, new Comparator<Pair>() {
            @Override public int compare(Pair p1, Pair p2)
            {
                return p1.y - p2.y;
            }
        });

        for (int i = 0; i < n; i++) {
            System.out.print(arr[i].x + " " + arr[i].y + " ");
        }
        System.out.println();
    }
}

// Driver class
class GFG {

    // Driver code
public static void main(String[] args)
    {
        Scanner sc = new Scanner(System.in);

        // length of array
        int n = 5;

        // Array of Pair
        Pair arr[] = new Pair[n];

        arr[0] = new Pair(10, 20);
        arr[1] = new Pair(1, 2);
        arr[2] = new Pair(3, 1);
        arr[3] = new Pair(10, 8);
        arr[4] = new Pair(4, 3);

        Compare obj = new Compare();

        obj.compare(arr, n);
    }
}
```

**Output:**

```
3 1 1 2 4 3 10 8 10 20

```