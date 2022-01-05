# 鸡尾酒分类 Java 程序

> 原文:[https://www . geeksforgeeks . org/Java-程序为鸡尾酒排序/](https://www.geeksforgeeks.org/java-program-for-cocktail-sort/)

鸡尾酒排序是[气泡排序](https://www.geeksforgeeks.org/bubble-sort/)的变体。冒泡排序算法总是从左侧遍历元素，并在第一次迭代中将最大的元素移动到正确的位置，在第二次迭代中将第二大元素移动到正确的位置，以此类推。鸡尾酒排序交替地在两个方向上遍历给定的数组。

 **算法:**
算法的每次迭代分为 2 个阶段:

1.  第一阶段从左到右循环遍历数组，就像冒泡排序一样。在循环过程中，比较相邻的项目，如果左边的值大于右边的值，则交换值。在第一次迭代结束时，最大的数字将位于数组的末尾。
2.  第二阶段以相反的方向在数组中循环——从最近排序的项之前的项开始，然后移回数组的开头。此外，还会比较相邻的项目，并在需要时进行交换。

```
// Java program for implementation of Cocktail Sort
public class CocktailSort {
    void cocktailSort(int a[])
    {
        boolean swapped = true;
        int start = 0;
        int end = a.length;

        while (swapped == true) {
            // reset the swapped flag on entering the
            // loop, because it might be true from a
            // previous iteration.
            swapped = false;

            // loop from bottom to top same as
            // the bubble sort
            for (int i = start; i < end - 1; ++i) {
                if (a[i] > a[i + 1]) {
                    int temp = a[i];
                    a[i] = a[i + 1];
                    a[i + 1] = temp;
                    swapped = true;
                }
            }

            // if nothing moved, then array is sorted.
            if (swapped == false)
                break;

            // otherwise, reset the swapped flag so that it
            // can be used in the next stage
            swapped = false;

            // move the end point back by one, because
            // item at the end is in its rightful spot
            end = end - 1;

            // from top to bottom, doing the
            // same comparison as in the previous stage
            for (int i = end - 1; i >= start; i--) {
                if (a[i] > a[i + 1]) {
                    int temp = a[i];
                    a[i] = a[i + 1];
                    a[i + 1] = temp;
                    swapped = true;
                }
            }

            // increase the starting point, because
            // the last stage would have moved the next
            // smallest number to its rightful spot.
            start = start + 1;
        }
    }

    /* Prints the array */
    void printArray(int a[])
    {
        int n = a.length;
        for (int i = 0; i < n; i++)
            System.out.print(a[i] + " ");
        System.out.println();
    }

    // Driver method
    public static void main(String[] args)
    {
        CocktailSort ob = new CocktailSort();
        int a[] = { 5, 1, 4, 2, 8, 0, 2 };
        ob.cocktailSort(a);
        System.out.println("Sorted array");
        ob.printArray(a);
    }
}
```

**Output:**

```
Sorted array
0 1 2 2 4 5 8

```

更多详情请参考[鸡尾酒排序](https://www.geeksforgeeks.org/cocktail-sort/)整篇文章！