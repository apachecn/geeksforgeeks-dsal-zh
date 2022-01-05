# 反转移动到前方变换

> 原文:[https://www . geeksforgeeks . org/reving-move-front-transform/](https://www.geeksforgeeks.org/inverting-move-front-transform/)

**先决条件:** [移动到前方数据变换算法](https://www.geeksforgeeks.org/move-front-data-transform-algorithm/)

**MTF 变换逆运算背后的主要思想:**

1.计算 MTF 变换的逆就是撤销 MTF 变换，恢复原始字符串。我们有**“input _ arr”**和**“n”**，前者是 MTF 变换，**“input _ arr”**中的元素数量。

2.我们的任务是维护一个有序的字符列表(在我们的例子中是 a 到 z)，并从**“input _ arr”**中一次读入一个**“ith”**元素。

3.然后，以该元素为索引 **j** ，在列表中打印**“jth”**字符。

```
Illustration for "[15 1 14 1 14 1]"
List initially contains English alphabets in order.
We move characters at indexes depicted by input 
to front of the list one by one.

input arr chars   output str  list
15                p           abcdefghijklmnopqrstuvwxyz
1                 pa          pabcdefghijklmnoqrstuvwxyz
14                pan         apbcdefghijklmnoqrstuvwxyz
1                 pana        napbcdefghijklmoqrstuvwxyz
14                panam       anpbcdefghijklmoqrstuvwxyz
1                 panama      manpbcdefghijkloqrstuvwxyz

```

**示例:**

```
Input : arr[] = {15, 1, 14, 1, 14, 1}
Output : panama

Input : arr[] = {6, 5, 0, 10, 18, 8, 15, 18, 
                6, 6, 0, 6, 6};
Output : geeksforgeeks

```

下面是上面解释的 idea 代码:

```
// C program to find Inverse of Move to Front
// Transform of a given string
#include<stdio.h>
#include<stdlib.h>
#include<string.h>

// Takes index of printed character as argument
// to bring that character to the front of the list
void moveToFront(int index, char *list)
{
    char record[27];
    strcpy(record, list);

    // Characters pushed one position right
    // in the list up until index
    strncpy(list+1, record, index);

    // Character at index stored at 0th position
    list[0] = record[index];
}

// Move to Front Decoding
void mtfDecode(int arr[], int n)
{
    // Maintains an ordered list of legal symbols
    char list[] = "abcdefghijklmnopqrstuvwxyz";

    int i;
    printf("\nInverse of Move to Front Transform: ");
    for (i = 0; i < n; i++)
    {
        // Printing characters of Inverse MTF as output
        printf("%c", list[arr[i]]);

        // Moves the printed character to the front 
        // of the list
        moveToFront(arr[i], list);
    }
}

// Driver program to test functions above
int main()
{
    // MTF transform and number of elements in it.
    int arr[] = {15, 1, 14, 1, 14, 1};
    int n = sizeof(arr)/sizeof(arr[0]);

    // Computes Inverse of Move to Front transform
    // of given text
    mtfDecode(arr, n);

    return 0;
}
```

**输出:**

```
Inverse of Move to Front Transform: panama

```

**时间复杂度:** O(n^2)

**练习:**在一个程序中一起实现 MTF 编码和解码，检查原始消息是否恢复。

**来源:**
[http://www . cs . Princeton . edu/courses/archive/fall 07/cos226/assignments/burrows . html](http://www.cs.princeton.edu/courses/archive/fall07/cos226/assignments/burrows.html)