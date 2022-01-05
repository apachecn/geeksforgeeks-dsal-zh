# 按排序顺序打印字符串数组，无需将一个字符串复制到另一个字符串中

> 原文:[https://www . geesforgeks . org/print-array-strings-sorted-order-not-copy-one-string-other/](https://www.geeksforgeeks.org/print-array-strings-sorted-order-without-copying-one-string-another/)

给定 n 个字符串的数组。任务是按排序顺序打印字符串。方法应该是在排序过程中不应该将任何字符串复制到另一个字符串。

**示例:**

```
Input : {"geeks", "for", "geeks", "quiz")
Output : for geeks geeks quiz

Input : {"ball", "pen", "apple", "kite"}
Output : apple ball kite pen
```

**进场:**有以下步骤:

1.  维护另一个数组 **indexed_arr** ，该数组存储/维护每个字符串的索引。
2.  我们可以对这个 **indexed_arr** 应用任何排序技术。

**插图:**

```
--> str[] = {"world", "hello"}
--> corresponding index array will be
    indexed_arr = {0, 1}
--> Now, how the strings are compared and 
    accordingly values in indexed_arr are changed.
--> Comparison process:
    if (str[index[0]].compare(str[index[1]] > 0
        temp = index[0]
        index[0] = index[1]
        index[1] = temp

// after sorting values of
// indexed_arr = {1, 0}
--> for i=0 to 1
        print str[index[i]]

This is how the strings are compared and their 
corresponding indexes in the indexed_arr
are being manipulated/swapped so that after the sorting process
is completed, the order of indexes in the indexed_arr
gives us the sorted order of the strings.
```

## C++

```
// C++ implementation to print array of strings in sorted
// order without copying one string into another
#include <bits/stdc++.h>

using namespace std;

// function to print strings in sorted order
void printInSortedOrder(string arr[], int n)
{
    int index[n];
    int i, j, min;

    // Initially the index of the strings
    // are assigned to the 'index[]'
    for (i=0; i<n; i++)
        index[i] = i;

    // selection sort technique is applied   
    for (i=0; i<n-1; i++)   
    {
        min = i;
        for (j=i+1; j<n; j++)
        {
            // with the help of 'index[]'
            // strings are being compared
            if (arr[index[min]].compare(arr[index[j]]) > 0)
                min = j;
        }

        // index of the smallest string is placed
        // at the ith index of 'index[]'
        if (min != i)
        {
            int temp = index[min];
            index[min] = index[i];
            index[i] = temp;
        }
    }

    // printing strings in sorted order
    for (i=0; i<n; i++)
        cout << arr[index[i]] << " ";
}

// Driver program to test above
int main()
{
    string arr[] = {"geeks", "quiz", "geeks", "for"};
    int n = 4;
    printInSortedOrder(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation to print array of strings in sorted
// order without copying one string into another

class GFG {

    // function to print strings in sorted order
    static void printInSortedOrder(String arr[], int n) {
        int index[] = new int[n];
        int i, j, min;

        // Initially the index of the strings
        // are assigned to the 'index[]'
        for (i = 0; i < n; i++) {
            index[i] = i;
        }

        // selection sort technique is applied   
        for (i = 0; i < n - 1; i++) {
            min = i;
            for (j = i + 1; j < n; j++) {
                // with the help of 'index[]'
                // strings are being compared
                if (arr[index[min]].compareTo(arr[index[j]]) > 0) {
                    min = j;
                }
            }

            // index of the smallest string is placed
            // at the ith index of 'index[]'
            if (min != i) {
                int temp = index[min];
                index[min] = index[i];
                index[i] = temp;
            }
        }

        // printing strings in sorted order
        for (i = 0; i < n; i++) {
            System.out.print(arr[index[i]] + " ");
        }
    }

    // Driver program to test above
    static public void main(String[] args) {
        String arr[] = {"geeks", "quiz", "geeks", "for"};
        int n = 4;
        printInSortedOrder(arr, n);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation to print array
# of strings in sorted order without
# copying one string into another

# function to print strings in sorted order
def printInSortedOrder(arr, n):
    index = [0] * n

    # Initially the index of the strings
    # are assigned to the 'index[]'
    for i in range(n):
        index[i] = i

    # selection sort technique is applied
    for i in range(n - 1):
        min = i
        for j in range(i + 1, n):

            # with the help of 'index[]'
            # strings are being compared
            if (arr[index[min]] > arr[index[j]]):
                min = j

        # index of the smallest string is placed
        # at the ith index of 'index[]'
        if (min != i):
            index[min], index[i] = index[i], index[min]

    # printing strings in sorted order
    for i in range(n):
        print(arr[index[i]], end = " ")

# Driver Code
if __name__ == "__main__":

    arr = ["geeks", "quiz", "geeks", "for"]
    n = 4
    printInSortedOrder(arr, n)

# This code is contributed by ita_c
```

## C#

```

//C# implementation to print an array of strings in sorted
// order without copying one string into another
 using System;
public class GFG {

    // function to print strings in sorted order
    static void printInSortedOrder(String []arr, int n) {
        int []index = new int[n];
        int i, j, min;

        // Initially the index of the strings
        // are assigned to the 'index[]'
        for (i = 0; i < n; i++) {
            index[i] = i;
        }

        // selection sort technique is applied   
        for (i = 0; i < n - 1; i++) {
            min = i;
            for (j = i + 1; j < n; j++) {
                // with the help of 'index[]'
                // strings are being compared
                if (arr[index[min]].CompareTo(arr[index[j]]) > 0) {
                    min = j;
                }
            }

            // index of the smallest string is placed
            // at the ith index of 'index[]'
            if (min != i) {
                int temp = index[min];
                index[min] = index[i];
                index[i] = temp;
            }
        }

        // printing strings in sorted order
        for (i = 0; i < n; i++) {
            Console.Write(arr[index[i]] + " ");
        }
    }

    // Driver program to test above
    static public void Main() {
        String []arr = {"geeks", "quiz", "geeks", "for"};
        int n = 4;
        printInSortedOrder(arr, n);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
//Javascript implementation to print array of strings in sorted
// order without copying one string into another

    // function to print strings in sorted order
    function printInSortedOrder(arr,n)
    {
        let index = new Array(n);
        let i, j, min;

        // Initially the index of the strings
        // are assigned to the 'index[]'
        for (i = 0; i < n; i++) {
            index[i] = i;
        }

        // selection sort technique is applied   
        for (i = 0; i < n - 1; i++) {
            min = i;
            for (j = i + 1; j < n; j++) {
                // with the help of 'index[]'
                // strings are being compared
                if (arr[index[min]]>(arr[index[j]]) ) {
                    min = j;
                }
            }

            // index of the smallest string is placed
            // at the ith index of 'index[]'
            if (min != i) {
                let temp = index[min];
                index[min] = index[i];
                index[i] = temp;
            }
        }

        // printing strings in sorted order
        for (i = 0; i < n; i++) {
            document.write(arr[index[i]] + " ");
        }
    }

    // Driver program to test above
    let arr=["geeks", "quiz", "geeks", "for"];
    let n = 4;
    printInSortedOrder(arr, n);

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
for geeks geeks quiz
```

**时间复杂度:** O(n <sup>2</sup> )
当我们必须最小化**盘写入**的数量时，该方法可以有它的用途，就像在结构阵列的情况下一样。结构值被比较，但是它们的值没有被交换，相反，它们的索引被保持在另一个数组中，该数组被操作来保持索引以表示结构的排序数组的顺序。