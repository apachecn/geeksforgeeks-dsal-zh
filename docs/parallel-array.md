# 平行阵列

> 原文:[https://www.geeksforgeeks.org/parallel-array/](https://www.geeksforgeeks.org/parallel-array/)

**并行数组:**也称为结构化数组(SoA)，多个大小相同的数组，使得每个数组的第 I 个元素紧密相关，所有第 I 个元素一起表示一个对象或实体。一个平行阵列的例子是代表 n 个点的 x 和 y 坐标的两个阵列。
下面是另一个例子，我们将 5 个人的名字、姓氏和身高存储在三个不同的数组中。

```
first_name = ['Bones', 'Welma', 'Frank', 'Han', 'Jack']
last_name  = ['Smith', 'Seger', 'Mathers', 'Solo', 'Jackles']
height     = [169, 158, 201, 183, 172]
```

通过这种方式，我们可以轻松地存储信息，对于访问，每个数组的第一个索引对应于属于同一个人的数据。
**应用程序:**
对数组或记录执行的两个最重要的应用程序是搜索和排序。

*   **搜索:**并行数组中的每个索引对应于记录中属于同一实体的数据。因此，为了基于属性的特定值来搜索实体，例如，在上面的例子中，我们需要找到具有高度> 200 厘米的人的名字。因此，我们在高度数组中搜索值大于 200 的索引。现在，一旦我们获得了索引，我们就在名字和姓氏数组中打印索引的值。这种方式在并行数组中搜索变得很容易。
*   **排序:**现在，使用相同的事实，即每个索引对应于对应于同一实体的不同数组中的数据项。因此，我们根据相同的标准对所有数组进行排序。例如，在上面显示的示例中，我们需要按照人们各自身高的递增顺序对他们进行排序。因此，当我们交换两个高度时，我们甚至会交换使用相同索引的其他数组中的相应值。

**搜索:**
根据数组或并行数组结构中的特定属性，执行以下步骤来搜索实体。

*   使用[线性搜索](https://www.geeksforgeeks.org/linear-search/) **/** [二分搜索法](https://www.geeksforgeeks.org/binary-search/)方法中的任意一种，在相应数组中搜索所需属性的值(例如，在上述示例中搜索大于 200 的值)。
*   存储数组中获得以下值的索引
*   打印其他数组中评估索引处的值

**排序**
数组可以以任何方式排序，数字、字母或任何其他方式，但元素被放置在等间距的地址。任何排序技术都可以用来根据指定的标准对记录进行排序。执行以下步骤对记录进行排序。

*   在序列无效的地方找到数组中的索引(根据指定的标准进行排序的数组)(即，我们需要计算排序序列失败的两个索引，这将通过交换这些索引处的值来纠正)。
*   现在交换所有数组中这两个计算索引的值。

因此，按照上述步骤，一旦选择的阵列(根据指定标准选择的阵列)被排序，所有阵列将相对于选择的阵列被排序。
**实现:**
1)下面的代码存储了 10 个学生的名、名、高。
2)使用[快速排序](https://www.geeksforgeeks.org/quick-sort/)算法按照高度的递增顺序对它们进行排序。
3)在记录中搜索第二高的学生、第三矮的学生和身高等于 158 厘米的学生的名字。

## C++

```
// C++ implementation of parallel arrays
// and operations on them
#include <iostream>
using namespace std;

/* This function takes the last element as
   pivot places the pivot element at its
   correct position in a sorted array, and
   places all smaller (smaller than pivot)
   to left of the pivot and all greater elements
   to right of pivot */
int partition(string first_name[], string
                                       last_name[],
              int height[], int low, int high)
{
    int pivot = height[high]; // pivot
    int i = (low - 1); // Index of smaller element

    for (int j = low; j <= high - 1; j++) {

        // If current element is smaller than
        // or equal to pivot. This means are
        // sorting sequence condition fails if
        // the condition becomes true. Thus the
        // two indices which shall be obtained
        // here will be i and j and therefore
        // we will be swapping values of i and j
        // in all the arrays.
        if (height[j] <= pivot) {

            // increment index of smaller element
            i++;

            // Swapping values of i and j in
            // all the arrays
            string temp = first_name[i];
            first_name[i] = first_name[j];
            first_name[j] = temp;
            temp = last_name[i];
            last_name[i] = last_name[j];
            last_name[j] = temp;
            int temp1 = height[i];
            height[i] = height[j];
            height[j] = temp1;
        }
    }
    string temp = first_name[i + 1];
    first_name[i + 1] = first_name[high];
    first_name[high] = temp;
    temp = last_name[i + 1];
    last_name[i + 1] = last_name[high];
    last_name[high] = temp;
    int temp1 = height[i + 1];
    height[i + 1] = height[high];
    height[high] = temp1;
    return (i + 1);
}

// Function which implements quick sort
void quickSort(string first_name[], string last_name[],
               int height[], int low, int high)
{
    if (low < high) {
        /* pi is partitioning index, arr[p] is now
           at right place */
        int pi = partition(first_name, last_name,
                           height, low, high);

        // Separately sort elements before
        // partition and after partition
        quickSort(first_name, last_name, height,
                  low, pi - 1);
        quickSort(first_name, last_name, height,
                  pi + 1, high);
    }
}

// Function which binary searches the height
// array for value 158 and if found, prints
// the corresponding value in other arrays
// at that index.
void binarySearch(string first_name[], string
                                           last_name[],
                  int height[], int value, int n)
{

    int low = 0, high = n - 1;
    int index;
    while (low <= high) {

        index = (high + low) / 2;
        if (height[index] == 158) {

            // This index of height array
            // corresponds to the name
            // of the person in first name
            // and last name array.
            cout << "Person having height 158"
                    " cms is "
                 << first_name[index]
                 << " " << last_name[index] << endl;
            return;
        }
        else if (height[index] > 158)
            high = index - 1;
        else
            low = index + 1;
    }
    cout << "Sorry, no such person with"
            " height 158 cms";
    cout << "is found in the record";
}

// Printing same index of each array. This
// will give meaningful data as in parallel
// array indices point to values in different
// arrays belonging to the same entity
void printParallelArray(string first_name[],
                        string last_name[], int height[], int n)
{

    cout << "Name of people in increasing";
    cout << "order of their height: " << endl;
    for (int i = 0; i < n; i++) {

        cout << first_name[i] << " "
             << last_name[i] << " has height "
             << height[i] << " cms\n";
    }
    cout << endl;
}

// Driver Function
int main()
{

    // These arrays together form a set
    // of arrays known as parallel array
    int n = 10;
    string first_name[] = { "Bones", "Welma",
                            "Frank", "Han", "Jack", "Jinny", "Harry",
                            "Emma", "Tony", "Sherlock" };
    string last_name[] = { "Smith", "Seger",
                           "Mathers", "Solo", "Jackles", "Weasly",
                           "Potter", "Watson", "Stark", "Holmes" };
    int height[] = { 169, 158, 201, 183, 172,
                     152, 160, 163, 173, 185 };

    // Sorting the above arrays using quickSort
    // technique based on increasing order of
    // their heights.
    quickSort(first_name, last_name, height,
              0, n - 1);
    printParallelArray(first_name, last_name,
                       height, n);

    // Second tallest person in the sorted
    // list will be the second person from the
    // right end.
    cout << "Name of the second tallest person"
            " is "
         << first_name[n - 2] << " "
         << last_name[n - 2] << endl;

    // Third shortest person in the sorted
    // list will be the third person from the
    // left end.
    cout << "Name of the third shortest person is "
         << first_name[2] << " " << last_name[2]
         << endl;

    // We binary search the height array to
    // search for a person having height 158
    // cms.
    binarySearch(first_name, last_name, height,
                 158, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of parallel arrays
// and operations on them
import java.util.*;
import java.lang.*;

class parallel_array_java {

    /* This function takes the last element as
      pivot, places the pivot element at its
      correct position in sorted array, and
      places all smaller (smaller than pivot)
     to left of pivot and all greater elements
     to right   of pivot */
    static int partition(String first_name[],
                         String last_name[], int height[], int low,
                         int high)
    {

        int pivot = height[high]; // pivot
        int i = (low - 1); // Index of smaller element

        for (int j = low; j <= high - 1; j++) {

            // If current element is smaller than
            // or equal to pivot. This means are
            // sorting sequence condition fails if
            // the condition becomes true. Thus the
            // two indices which shall be obtained
            // here will be i and jand therefore
            // we will be swapping values of i and j
            // in all the arrays.
            if (height[j] <= pivot) {

                i++; // increment index of smaller element
                // Swapping values of i and j in all the arrays
                String temp = first_name[i];
                first_name[i] = first_name[j];
                first_name[j] = temp;
                temp = last_name[i];
                last_name[i] = last_name[j];
                last_name[j] = temp;
                int temp1 = height[i];
                height[i] = height[j];
                height[j] = temp1;
            }
        }
        String temp = first_name[i + 1];
        first_name[i + 1] = first_name[high];
        first_name[high] = temp;
        temp = last_name[i + 1];
        last_name[i + 1] = last_name[high];
        last_name[high] = temp;
        int temp1 = height[i + 1];
        height[i + 1] = height[high];
        height[high] = temp1;
        return (i + 1);
    }

    // Function which implements quick sort
    static void quickSort(String first_name[],
                          String last_name[], int height[], int low,
                          int high)
    {

        if (low < high) {

            /* pi is partitioning index, arr[p]
              is now at right place */
            int pi = partition(first_name, last_name,
                               height, low, high);

            // Separately sort elements before
            // partition and after partition
            quickSort(first_name, last_name, height,
                      low, pi - 1);
            quickSort(first_name, last_name, height,
                      pi + 1, high);
        }
    }

    // Function which binary searches the height array
    // for value 158 and if found, prints the
    // corresponding value in other arrays at that index.
    static void binarySearch(String first_name[],
                             String last_name[], int height[], int value, int n)
    {

        int low = 0, high = n - 1;
        int index;
        while (low <= high) {

            index = (high + low) / 2;
            if (height[index] == 158) {

                // This index of height array corresponds
                // to the name of the person in first
                // name and last name array.
                System.out.println("Person having height"
                                   + " 158 cms is " + first_name[index] + " " + last_name[index]);
                return;
            }
            else if (height[index] > 158)
                high = index - 1;
            else
                low = index + 1;
        }
        System.out.print("Sorry, no such person"
                         + " with height");
        System.out.println("158 cms is found in"
                           + " the record");
    }

    // Printing same index of each array. This
    // will give meaningful data as in parallel
    // array indices point to the values in
    // different arrays belonging to the same
    // entity
    static void printParallelArray(String first_name[],
                                   String last_name[], int height[], int n)
    {

        System.out.print("Name of people in increasing"
                         + " order of");
        System.out.println("their height: ");
        for (int i = 0; i < n; i++) {

            System.out.println(first_name[i] + " " + last_name[i] + " has height " + height[i] + " cms");
        }
        System.out.println();
    }
    public static void main(String args[])
    {

        // These arrays together form a set of arrays
        // known as parallel array
        int n = 10;
        String[] first_name = { "Bones", "Welma",
                                "Frank", "Han", "Jack", "Jinny", "Harry",
                                "Emma", "Tony", "Sherlock" };
        String[] last_name = { "Smith", "Seger",
                               "Mathers", "Solo", "Jackles", "Weasly",
                               "Potter", "Watson", "Stark", "Holmes" };
        int[] height = { 169, 158, 201, 183, 172,
                         152, 160, 163, 173, 185 };

        // Sorting the above arrays using quickSort
        // technique based on increasing order of
        // their heights.
        quickSort(first_name, last_name, height,
                  0, n - 1);
        printParallelArray(first_name, last_name,
                           height, n);

        // Second tallest person in the sorted list
        // will be the second person from the right end.
        System.out.println("Name of the second tallest"
                           + "person is " + first_name[n - 2] + " " + last_name[n - 2]);

        // Third shortest person in the sorted list
        // will be the third person from the left end.
        System.out.println("Name of the third shortest"
                           + " person is " + first_name[2] + " " + last_name[2]);

        // We binary search the height array to
        // search for a person having height 158 cms.
        binarySearch(first_name, last_name, height, 158, n);
    }
}
```

## C#

```
// C# implementation of parallel arrays
// and operations on them
using System;

class GFG {

    /* This function takes last element
    as pivot, places the pivot element
    at its correct position in sorted
    array, and places all smaller
    (smaller than pivot) to left of
    pivot and all greater elements to
    right of pivot */
    static int partition(String[] first_name,
                          String[] last_name,
                       int[] height, int low,
                                    int high)
    {

        // pivot
        int pivot = height[high];

        // Index of smaller element
        int i = (low - 1);

        for (int j = low; j <= high - 1; j++)
        {

            // If current element is smaller
            // than or equal to pivot. This
            // means are sorting sequence
            // condition fails if the condition
            // becomes true. Thus the two
            // indices which shall be obtained
            // here will be i and jand therefore
            // we will be swapping values of i
            // and j in all the arrays.
            if (height[j] <= pivot) {

                // increment index of smaller
                // element
                i++;

                // Swapping values of i and j
                // in all the arrays
                String temp = first_name[i];
                first_name[i] = first_name[j];
                first_name[j] = temp;
                temp = last_name[i];
                last_name[i] = last_name[j];
                last_name[j] = temp;
                int temp1 = height[i];
                height[i] = height[j];
                height[j] = temp1;
            }
        }

        String tempp = first_name[i + 1];
        first_name[i + 1] = first_name[high];
        first_name[high] = tempp;
        tempp = last_name[i + 1];
        last_name[i + 1] = last_name[high];
        last_name[high] = tempp;
        int temp2 = height[i + 1];
        height[i + 1] = height[high];
        height[high] = temp2;
        return (i + 1);
    }

    // Function which implements quick sort
    static void quickSort(String[] first_name,
                           String[] last_name,
                        int[] height, int low,
                                     int high)
    {

        if (low < high) {

            /* pi is partitioning index,
            arr[p] is now at right place */
            int pi = partition(first_name,
                        last_name, height,
                               low, high);

            // Separately sort elements before
            // partition and after partition
            quickSort(first_name, last_name,
                       height, low, pi - 1);

            quickSort(first_name, last_name,
                      height, pi + 1, high);
        }
    }

    // Function which binary searches the
    // height array for value 158 and if
    // found, prints the corresponding value
    // in other arrays at that index.
    static void binarySearch(String[] first_name,
                              String[] last_name,
                         int[] height, int value,
                                           int n)
    {

        int low = 0, high = n - 1;
        int index;
        while (low <= high) {

            index = (high + low) / 2;
            if (height[index] == 158) {

                // This index of height array
                // corresponds to the name of
                // the person in first name and
                // last name array.
                Console.Write("Person having height"
                                 + " 158 cms is " +
                                first_name[index] +
                             " " + last_name[index]);

                return;
            }
            else if (height[index] > 158)
                high = index - 1;
            else
                low = index + 1;
        }

        Console.Write("Sorry, no such person"
                 + " with height 158 cms is "
                    + "found in the record");
    }

    // Printing same index of each array. This
    // will give meaningful data as in parallel
    // array indices point to the values in
    // different arrays belonging to the same
    // entity
    static void printParallelArray(String[] first_name,
                                    String[] last_name,
                                   int[] height, int n)
    {

        Console.WriteLine("Name of people in increasing"
                    + " order of their height: ");
        for (int i = 0; i < n; i++) {

            Console.WriteLine(first_name[i] + " " +
                    last_name[i] + " has height " +
                                height[i] + " cms");
        }

        Console.WriteLine();
    }

    // Driver function
    public static void Main()
    {

        // These arrays together form a set of
        // arrays known as parallel array
        int n = 10;
        String[] first_name = { "Bones", "Welma",
                          "Frank", "Han", "Jack",
                        "Jinny", "Harry", "Emma",
                            "Tony", "Sherlock" };

        String[] last_name = { "Smith", "Seger",
                   "Mathers", "Solo", "Jackles",
                   "Weasly", "Potter", "Watson",
                            "Stark", "Holmes" };

        int[] height = { 169, 158, 201, 183, 172,
                       152, 160, 163, 173, 185 };

        // Sorting the above arrays using quickSort
        // technique based on increasing order of
        // their heights.
        quickSort(first_name, last_name, height,
                                        0, n - 1);

        printParallelArray(first_name, last_name,
                                       height, n);

        // Second tallest person in the sorted list
        // will be the second person from the right end.
        Console.WriteLine("Name of the second tallest"
                    + "person is " + first_name[n - 2]
                            + " " + last_name[n - 2]);

        // Third shortest person in the sorted list
        // will be the third person from the left end.
        Console.WriteLine("Name of the third shortest"
                       + " person is " + first_name[2]
                                + " " + last_name[2]);

        // We binary search the height array to
        // search for a person having height 158 cms.
        binarySearch(first_name, last_name, height,
                                             158, n);
    }
}

// This codecontribute by parashar.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of parallel
// arrays and operations on them

/* This function takes last element
as pivot, places the pivot element
at its correct position in sorted
array, and places all smaller
(smaller than pivot) to left of pivot
and all greater elements to right
of pivot */
function partition(&$first_name, &$last_name,
                   &$height, $low, $high)
{
    $pivot = $height[$high]; // pivot
    $i = ($low - 1); // Index of smaller element

    for ($j = $low; $j <= $high - 1; $j++)
    {

        // If current element is smaller
        // than or equal to pivot. This
        // means are sorting sequence
        // condition fails if the condition
        // becomes true. Thus the two indices
        // which shall be obtained here will
        // be i and j and therefore we will
        // be swapping values of i and j
        // in all the arrays.
        if ($height[$j] <= $pivot)
        {

            // increment index of
            // smaller element
            $i++;

            // Swapping values
            // of i and j in
            // all the arrays
            $temp = $first_name[$i];
            $first_name[$i] = $first_name[$j];
            $first_name[$j] = $temp;
            $temp = $last_name[$i];
            $last_name[$i] = $last_name[$j];
            $last_name[$j] = $temp;
            $temp1 = $height[$i];
            $height[$i] = $height[$j];
            $height[$j] = $temp1;
        }
    }
    $temp = $first_name[$i + 1];
    $first_name[$i + 1] = $first_name[$high];
    $first_name[$high] = $temp;
    $temp = $last_name[$i + 1];
    $last_name[$i + 1] = $last_name[$high];
    $last_name[$high] = $temp;
    $temp1 = $height[$i + 1];
    $height[$i + 1] = $height[$high];
    $height[$high] = $temp1;
    return ($i + 1);
}

// Function which
// implements quick sort
function quickSort(&$first_name, &$last_name,
                   &$height, $low, $high)
{
    if ($low < $high)
    {
        /* pi is partitioning
        index, arr[p] is now
        at right place */
        $pi = partition($first_name, $last_name,
                        $height, $low, $high);

        // Separately sort elements
        // before partition and
        // after partition
        quickSort($first_name, $last_name,
                  $height, $low, $pi - 1);
        quickSort($first_name, $last_name,
                  $height, $pi + 1, $high);
    }
}

// Function which binary searches
// the height array for value 158
// and if found, prints the
// corresponding value in other
// arrays at that index.
function binarySearch(&$first_name, &$last_name,
                      &$height, $value, $n)
{

    $low = 0; $high = $n - 1;
    $index = 0;
    while ($low <= $high)
    {

        $index = ($high + $low) / 2;
        if ($height[$index] == 158)
        {

            // This index of height array
            // corresponds to the name
            // of the person in first name
            // and last name array.
            echo ("Person having height 158".
                  " cms is " . $first_name[$index] .
                  " " . $last_name[$index] . "\n");
            return;
        }
        else if ($height[$index] > 158)
            $high = $index - 1;
        else
            $low = $index + 1;
    }
    echo ("Sorry, no such person with" .
                     " height 158 cms");
    echo ("is found in the record");
}

// Printing same index of each
// array. This will give meaningful
// data as in parallel array indices
// po$to values in different arrays
// belonging to the same entity
function printParallelArray(&$first_name,
                            &$last_name,
                            &$height, &$n)
{
    echo ("Name of people in increasing");
    echo (" order of their height: " . "\n");
    for ($i = 0; $i < $n; $i++)
    {
        echo ($first_name[$i] . " " .
              $last_name[$i] . " has height " .
              $height[$i] . " cms\n");
    }
    echo ("\n");
}

// Driver Code

// These arrays together
// form a set of arrays
// known as parallel array
$n = 10;
$first_name = array("Bones", "Welma",
                    "Frank", "Han",
                    "Jack", "Jinny",
                    "Harry", "Emma",
                    "Tony", "Sherlock");
$last_name = array("Smith", "Seger",
                   "Mathers", "Solo",
                   "Jackles", "Weasly",
                   "Potter", "Watson",
                   "Stark", "Holmes");
$height = array(169, 158, 201, 183, 172,
                152, 160, 163, 173, 185);

// Sorting the above arrays
// using quickSort technique
// based on increasing order
// of their heights.
quickSort($first_name, $last_name,
           $height, 0, $n - 1);
printParallelArray($first_name,
                   $last_name,
                   $height, $n);

// Second tallest person in
// the sorted list will be
// second person from the
// right end.
echo ("Name of the second ".
      "tallest person is " .
       $first_name[$n - 2] .
  " " . $last_name[$n - 2] . "\n");

// Third shortest person in
// the sorted list will be
// third person from the
// left end.
echo ("Name of the third shortest person is " .
         $first_name[2] . " " . $last_name[2] . "\n");

// We binary search the height
// array to search for a person
// having height 158 cms.
binarySearch($first_name, $last_name,
             $height, 158, $n);

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>
// Javascript implementation of parallel arrays
// and operations on them

/* This function takes the last element as
pivot, places the pivot element at its
correct position in sorted array, and
places all smaller (smaller than pivot)
to left of pivot and all greater elements
to right of pivot */
function partition(first_name, last_name, height, low, high) {

    let pivot = height[high]; // pivot
    let i = (low - 1); // Index of smaller element

    for (let j = low; j <= high - 1; j++) {

        // If current element is smaller than
        // or equal to pivot. This means are
        // sorting sequence condition fails if
        // the condition becomes true. Thus the
        // two indices which shall be obtained
        // here will be i and jand therefore
        // we will be swapping values of i and j
        // in all the arrays.
        if (height[j] <= pivot) {

            i++; // increment index of smaller element
            // Swapping values of i and j in all the arrays
            let temp = first_name[i];
            first_name[i] = first_name[j];
            first_name[j] = temp;
            temp = last_name[i];
            last_name[i] = last_name[j];
            last_name[j] = temp;
            let temp1 = height[i];
            height[i] = height[j];
            height[j] = temp1;
        }
    }
    let temp = first_name[i + 1];
    first_name[i + 1] = first_name[high];
    first_name[high] = temp;
    temp = last_name[i + 1];
    last_name[i + 1] = last_name[high];
    last_name[high] = temp;
    let temp1 = height[i + 1];
    height[i + 1] = height[high];
    height[high] = temp1;
    return (i + 1);
}

// Function which implements quick sort
function quickSort(first_name, last_name, height, low, high) {

    if (low < high) {

        /* pi is partitioning index, arr[p]
        is now at right place */
        let pi = partition(first_name, last_name,
            height, low, high);

        // Separately sort elements before
        // partition and after partition
        quickSort(first_name, last_name, height,
            low, pi - 1);
        quickSort(first_name, last_name, height,
            pi + 1, high);
    }
}

// Function which binary searches the height array
// for value 158 and if found, prints the
// corresponding value in other arrays at that index.
function binarySearch(first_name, last_name, height, value, n) {

    let low = 0, high = n - 1;
    let index;
    while (low <= high) {

        index = Math.floor((high + low) / 2);
        if (height[index] == 158) {

            // This index of height array corresponds
            // to the name of the person in first
            // name and last name array.
            document.write("Person having height"
                + " 158 cms is " + first_name[index] + " " + last_name[index] + "<br>");
            return;
        }
        else if (height[index] > 158)
            high = index - 1;
        else
            low = index + 1;
    }
    document.write("Sorry, no such person"
        + " with height" + "<br>");
    document.write("158 cms is found in"
        + " the record <br>");
}

// Printing same index of each array. This
// will give meaningful data as in parallel
// array indices point to the values in
// different arrays belonging to the same
// entity
function printParallelArray(first_name, last_name, height, n) {

    document.write("Name of people in increasing"
        + " order of their height: <br>");
    for (let i = 0; i < n; i++) {

        document.write(first_name[i] + " " + last_name[i] + " has height " + height[i] + " cms <br>");
    }
    document.write();
}

// These arrays together form a set of arrays
// known as parallel array
let n = 10;
let first_name = ["Bones", "Welma",
    "Frank", "Han", "Jack", "Jinny", "Harry",
    "Emma", "Tony", "Sherlock"];
let last_name = ["Smith", "Seger",
    "Mathers", "Solo", "Jackles", "Weasly",
    "Potter", "Watson", "Stark", "Holmes"];
let height = [169, 158, 201, 183, 172,
    152, 160, 163, 173, 185];

// Sorting the above arrays using quickSort
// technique based on increasing order of
// their heights.
quickSort(first_name, last_name, height,
    0, n - 1);
printParallelArray(first_name, last_name,
    height, n);

// Second tallest person in the sorted list
// will be the second person from the right end.
document.write("<br><br>Name of the second tallest"
    + " person is " + first_name[n - 2] + " " + last_name[n - 2] + "<br>");

// Third shortest person in the sorted list
// will be the third person from the left end.
document.write("Name of the third shortest"
    + " person is " + first_name[2] + " " + last_name[2] + "<br>");

// We binary search the height array to
// search for a person having height 158 cms.
binarySearch(first_name, last_name, height, 158, n);

// This code is contributed by gfgking.
</script>
```

**输出:**

```
Name of people in increasing order of their height:
Jinny Weasly has height 152 cms
Welma Seger has height 158 cms
Harry Potter has height 160 cms
Emma Watson has height 163 cms
Bones Smith has height 169 cms
Jack Jackles has height 172 cms
Tony Stark has height 173 cms
Han Solo has height 183 cms
Sherlock Holmes has height 185 cms
Frank Mathers has height 201 cms

Name of the second tallest person is Sherlock Holmes
Name of the third shortest person is Harry Potter
Person having height 158 cms is Welma Seger
```

**优势:**

*   它们可以用在只支持基元类型数组而不支持记录的语言中(或者根本不支持记录)。
*   并行数组易于理解和使用，并且经常在声明记录比它的价值更麻烦的地方使用。
*   在某些情况下，它们可以通过避免对齐问题来节省大量空间。
*   如果项的数量很少，数组索引占用的空间会比全指针少得多，尤其是在具有大词的架构上。

*   在现代机器上，顺序检查数组中每个记录的单个字段非常快，因为这相当于单个数组的线性遍历，表现出理想的引用局部性和缓存行为。

**缺点:**

*   当不按顺序访问记录并检查每个记录的多个字段时，它们的引用位置明显更差。
*   它们几乎没有直接的语言支持(该语言及其语法通常不表示并行数组中数组之间的关系)。
*   由于必须重新分配几个阵列中的每一个，它们的增长或收缩都很昂贵。多级数组可以改善这个问题，但是会影响性能，因为需要额外的间接性来找到所需的元素。