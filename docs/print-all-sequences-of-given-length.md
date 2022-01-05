# 打印给定长度的所有序列

> 原文:[https://www . geesforgeks . org/print-所有给定长度的序列/](https://www.geeksforgeeks.org/print-all-sequences-of-given-length/)

给定两个整数 k 和 n，编写一个函数，打印由数字 1，2 组成的所有长度为 k 的序列..你需要按排序顺序打印这些序列。
**例:**

```
Input: k = 2, n = 3

Output: 
1 1
1 2
1 3
2 1
2 2
2 3
3 1
3 2
3 3
```

```
Input:  k = 3, n = 4

Output: 
1 1 1
1 1 2
1 1 3
1 1 4
1 2 1
.....
.....
4 3 4
4 4 1
4 4 2
4 4 3
4 4 4
```

**方法 1(简单且迭代):**
按排序顺序打印所有序列的简单思路是从{1 1 … 1}开始，并在序列没有变成{n n … n}时不断递增序列。下面是详细的过程。
1)创建大小为 k 的输出数组 arr[]。将数组初始化为{1，1…1}。
2)打印数组 arr[]。
3)更新 arr[]数组，使其成为自身的直接后继(待打印)。例如，{1，1，1}的直接继任者是{1，1，2}，{1，4，4}的直接继任者是{2，1，1}，{4，4，3}的直接继任者是{4 4 4}。
4)当有后续阵列时，重复步骤 2 和 3。换句话说，虽然输出数组 arr[]没有变成{n，n..n}
现在我们来谈谈如何修改数组，使其包含直接后继。根据定义，直接后继应该有相同的第一个 p 项和更大的第(p+l)项。在原始数组中，(p+1)第项(或 arr[p])小于 n，arr[p]之后的所有项，即 arr[p+1]、arr[p+2]、… arr[k-1]都是 n.
为了找到直接的后继项，我们在之前打印的数组中找到点 p。为了找到点 p，我们从最右边开始，一直移动，直到找到一个数字 arr[p]，使得 arr[p]小于 n(或者不是 n)。一旦我们找到这样一个点，我们将它递增 arr[p]1，并使 arr[p]之后的所有元素都为 1，也就是说，我们确实 arr[p+1] = 1，arr[p+2] = 1..arr[k-1] = 1。以下是获取 arr[]的直接后继者的详细步骤:
1)从最右边的术语 arr[k-1]开始，向左移动。找到与 n 不相同的第一个元素 arr[p]。
2)将 arr[p]增加 1
3)从 arr[p+1]开始到 arr[k-1]，将所有项的值设置为 1。

## C++

```
// CPP program of above approach
#include<iostream>
using namespace std;
/* A utility function that prints a given arr[] of length size*/
void printArray(int arr[], int size)
{
    for(int i = 0; i < size; i++)
        cout <<" "<< arr[i];
    cout <<"\n";
    return;
}

/* This function returns 0 if there are no more sequences to be printed, otherwise
   modifies arr[] so that arr[] contains next sequence to be printed */
int getSuccessor(int arr[], int k, int n)
{
    /* start from the rightmost side and find the first number less than n */
    int p = k - 1;
    while (arr[p] == n)
        p--;

    /* If all numbers are n in the array then there is no successor, return 0 */
    if (p < 0)
        return 0;

    /* Update arr[] so that it contains successor */
    arr[p] = arr[p] + 1;
    for(int i = p + 1; i < k; i++)
        arr[i] = 1;

    return 1;
}

/* The main function that prints all sequences from 1, 1, ..1 to n, n, ..n */
void printSequences(int n, int k)
{
    int *arr = new int[k];

    /* Initialize the current sequence as the first sequence to be printed */
    for(int i = 0; i < k; i++)
        arr[i] = 1;

    /* The loop breaks when there are no more successors to be printed */
    while(1)
    {
        /* Print the current sequence */
        printArray(arr, k);

        /* Update arr[] so that it contains next sequence to be printed. And if
           there are no more sequences then break the loop */
        if(getSuccessor(arr, k, n) == 0)
          break;
    }

    delete(arr); // free dynamically allocated array
    return;
}

/* Driver Program to test above functions */
int main()
{
    int n = 3;
    int k = 2;
    printSequences(n, k);
    return 0;
}

// this code is contributed by shivanisinghss2110
```

## C

```
// CPP program of above approach
#include<stdio.h>

/* A utility function that prints a given arr[] of length size*/
void printArray(int arr[], int size)
{
    for(int i = 0; i < size; i++)
        printf("%d ", arr[i]);
    printf("\n");
    return;
}

/* This function returns 0 if there are no more sequences to be printed, otherwise
   modifies arr[] so that arr[] contains next sequence to be printed */
int getSuccessor(int arr[], int k, int n)
{
    /* start from the rightmost side and find the first number less than n */
    int p = k - 1;
    while (arr[p] == n)
        p--;

    /* If all numbers are n in the array then there is no successor, return 0 */
    if (p < 0)
        return 0;

    /* Update arr[] so that it contains successor */
    arr[p] = arr[p] + 1;
    for(int i = p + 1; i < k; i++)
        arr[i] = 1;

    return 1;
}

/* The main function that prints all sequences from 1, 1, ..1 to n, n, ..n */
void printSequences(int n, int k)
{
    int *arr = new int[k];

    /* Initialize the current sequence as the first sequence to be printed */
    for(int i = 0; i < k; i++)
        arr[i] = 1;

    /* The loop breaks when there are no more successors to be printed */
    while(1)
    {
        /* Print the current sequence */
        printArray(arr, k);

        /* Update arr[] so that it contains next sequence to be printed. And if
           there are no more sequences then break the loop */
        if(getSuccessor(arr, k, n) == 0)
          break;
    }

    delete(arr); // free dynamically allocated array
    return;
}

/* Driver Program to test above functions */
int main()
{
    int n = 3;
    int k = 2;
    printSequences(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program of above approach

class GFG
{

    /* A utility function that prints a given arr[] of length size*/
    static void printArray(int arr[], int size)
    {
        for (int i = 0; i < size; i++)
        {
            System.out.printf("%d ", arr[i]);
        }
        System.out.printf("\n");
        return;
    }

    /* This function returns 0 if there are
    no more sequences to be printed, otherwise
    modifies arr[] so that arr[] contains
    next sequence to be printed */
    static int getSuccessor(int arr[], int k, int n)
    {
        /* start from the rightmost side and
        find the first number less than n */
        int p = k - 1;
        while (arr[p] == n)
        {
            p--;
            if (p < 0)
            {
                break;
            }
        }

        /* If all numbers are n in the array
        then there is no successor, return 0 */
        if (p < 0)
        {
            return 0;
        }

        /* Update arr[] so that it contains successor */
        arr[p] = arr[p] + 1;
        for (int i = p + 1; i < k; i++)
        {
            arr[i] = 1;
        }
        return 1;
    }

    /* The main function that prints all
    sequences from 1, 1, ..1 to n, n, ..n */
    static void printSequences(int n, int k)
    {
        int[] arr = new int[k];

        /* Initialize the current sequence as
        the first sequence to be printed */
        for (int i = 0; i < k; i++)
        {
            arr[i] = 1;
        }

        /* The loop breaks when there are
        no more successors to be printed */
        while (true)
        {
            /* Print the current sequence */
            printArray(arr, k);

            /* Update arr[] so that it contains
            next sequence to be printed. And if
            there are no more sequences then
            break the loop */
            if (getSuccessor(arr, k, n) == 0)
            {
                break;
            }
        }
    }

    /* Driver code */
    public static void main(String[] args)
    {
        int n = 3;
        int k = 2;
        printSequences(n, k);
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program of above approach

# A utility function that prints
# a given arr[] of length size#
def printArray(arr, size):
    for i in range(size):
        print(arr[i], end = " ")
    print()
    return

# This function returns 0 if there are
# no more sequences to be printed, otherwise
# modifies arr[] so that arr[] contains
# next sequence to be printed #
def getSuccessor(arr, k, n):

    # start from the rightmost side and
    # find the first number less than n
    p = k - 1
    while (arr[p] == n and 0 <= p < k):
        p -= 1

    # If all numbers are n in the array
    # then there is no successor, return 0
    if (p < 0):
        return 0

    # Update arr[] so that it contains successor
    arr[p] = arr[p] + 1
    i = p + 1
    while(i < k):
        arr[i] = 1
        i += 1
    return 1

# The main function that prints all sequences
# from 1, 1, ..1 to n, n, ..n
def printSequences(n, k):
    arr = [0] * k

    # Initialize the current sequence as
    # the first sequence to be printed #
    for i in range(k):
        arr[i] = 1

    # The loop breaks when there are
    # no more successors to be printed
    while(1):

        # Print the current sequence
        printArray(arr, k)

        # Update arr[] so that it contains
        # next sequence to be printed. And if
        # there are no more sequences then
        # break the loop
        if(getSuccessor(arr, k, n) == 0):
            break
    return

# Driver code
n = 3
k = 2
printSequences(n, k)

# This code is contributed by shubhamsingh10
```

## C#

```
// C# program of above approach
using System;

class GFG
{

    /* A utility function that prints
    a given []arr of length size*/
    static void printArray(int []arr, int size)
    {
        for (int i = 0; i < size; i++)
        {
            Console.Write("{0} ", arr[i]);
        }
        Console.Write("\n");
        return;
    }

    /* This function returns 0 if there are
    no more sequences to be printed, otherwise
    modifies []arr so that []arr contains
    next sequence to be printed */
    static int getSuccessor(int []arr, int k, int n)
    {
        /* start from the rightmost side and
        find the first number less than n */
        int p = k - 1;
        while (arr[p] == n)
        {
            p--;
            if (p < 0)
            {
                break;
            }
        }

        /* If all numbers are n in the array
        then there is no successor, return 0 */
        if (p < 0)
        {
            return 0;
        }

        /* Update []arr so that it contains successor */
        arr[p] = arr[p] + 1;
        for (int i = p + 1; i < k; i++)
        {
            arr[i] = 1;
        }
        return 1;
    }

    /* The main function that prints all
    sequences from 1, 1, ..1 to n, n, ..n */
    static void printSequences(int n, int k)
    {
        int[] arr = new int[k];

        /* Initialize the current sequence as
        the first sequence to be printed */
        for (int i = 0; i < k; i++)
        {
            arr[i] = 1;
        }

        /* The loop breaks when there are
        no more successors to be printed */
        while (true)
        {
            /* Print the current sequence */
            printArray(arr, k);

            /* Update []arr so that it contains
            next sequence to be printed. And if
            there are no more sequences then
            break the loop */
            if (getSuccessor(arr, k, n) == 0)
            {
                break;
            }
        }
    }

    /* Driver code */
    public static void Main(String[] args)
    {
        int n = 3;
        int k = 2;
        printSequences(n, k);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// javascript program of above approach

/* A utility function that prints a
given arr of length size*/
function printArray(arr , size)
{
    for (i = 0; i < size; i++)
    {
        document.write(arr[i]+" ");
    }
    document.write("<br>");
    return;
}

/* This function returns 0 if there are
no more sequences to be printed, otherwise
modifies arr so that arr contains
next sequence to be printed */
function getSuccessor(arr , k , n)
{
    /* start from the rightmost side and
    find the first number less than n */
    var p = k - 1;
    while (arr[p] == n)
    {
        p--;
        if (p < 0)
        {
            break;
        }
    }

    /* If all numbers are n in the array
    then there is no successor, return 0 */
    if (p < 0)
    {
        return 0;
    }

    /* Update arr so that it contains successor */
    arr[p] = arr[p] + 1;
    for (i = p + 1; i < k; i++)
    {
        arr[i] = 1;
    }
    return 1;
}

/* The main function that prints all
sequences from 1, 1, ..1 to n, n, ..n */
function printSequences(n , k)
{
    var arr = Array.from({length: k}, (_, i) => 0);

    /* Initialize the current sequence as
    the first sequence to be printed */
    for (i = 0; i < k; i++)
    {
        arr[i] = 1;
    }

    /* The loop breaks when there are
    no more successors to be printed */
    while (true)
    {
        /* Print the current sequence */
        printArray(arr, k);

        /* Update arr so that it contains
        next sequence to be printed. And if
        there are no more sequences then
        break the loop */
        if (getSuccessor(arr, k, n) == 0)
        {
            break;
        }
    }
}

/* Driver code */
var n = 3;
var k = 2;
printSequences(n, k);

// This code is contributed by 29AjayKumar

</script>
```

**输出:**

```
1 1
1 2
1 3
2 1
2 2
2 3
3 1
3 2
3 3
```

*时间复杂度:*总共有 n^k 序列。打印一个序列并找到它的后继序列需要很长时间。所以上述实现的时间复杂度是 O(k*n^k).

*辅助空间:* O(k)
**方法 2(棘手且递归)**
递归函数*print sequence recurse*生成并打印长度为 k 的所有序列，其思想是多使用一个参数索引。函数*打印顺序递归*将 arr[]中的所有项保持在正常状态，直到索引，更新索引处的值，并在索引后递归调用自身以获取更多项。

## C++

```
// C++ program of above approach
#include<iostream>
using namespace std;

/* A utility function that prints a given arr[] of length size*/
void printArray(int arr[], int size)
{
    for(int i = 0; i < size; i++)
        cout<< "  "<< arr[i];
    cout<<"\n";
    return;
}

/* The core function that recursively generates and prints all sequences of
  length k */
void printSequencesRecur(int arr[], int n, int k, int index)
{
   int i;
   if (k == 0)
   {
     printArray(arr, index);
   }
   if (k > 0)
   {
      for(i = 1; i<=n; ++i)
      {
        arr[index] = i;
        printSequencesRecur(arr, n, k-1, index+1);
      }
   }
}

/* A function that uses printSequencesRecur() to prints all sequences
   from 1, 1, ..1 to n, n, ..n */
void printSequences(int n, int k)
{
    int *arr = new int[k];
    printSequencesRecur(arr, n, k, 0);

    delete(arr); // free dynamically allocated array
    return;
}

/* Driver Program to test above functions */
int main()
{
    int n = 3;
    int k = 2;
    printSequences(n, k);
    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// C++ program of above approach
#include<stdio.h>

/* A utility function that prints a given arr[] of length size*/
void printArray(int arr[], int size)
{
    for(int i = 0; i < size; i++)
        printf("%d ", arr[i]);
    printf("\n");
    return;
}

/* The core function that recursively generates and prints all sequences of
  length k */
void printSequencesRecur(int arr[], int n, int k, int index)
{
   int i;
   if (k == 0)
   {
     printArray(arr, index);
   }
   if (k > 0)
   {
      for(i = 1; i<=n; ++i)
      {
        arr[index] = i;
        printSequencesRecur(arr, n, k-1, index+1);
      }
   }
}

/* A function that uses printSequencesRecur() to prints all sequences
   from 1, 1, ..1 to n, n, ..n */
void printSequences(int n, int k)
{
    int *arr = new int[k];
    printSequencesRecur(arr, n, k, 0);

    delete(arr); // free dynamically allocated array
    return;
}

/* Driver Program to test above functions */
int main()
{
    int n = 3;
    int k = 2;
    printSequences(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of above approach

class GfG {

/* A utility function that prints a given arr[] of length size*/
static void printArray(int arr[], int size)
{
    for(int i = 0; i < size; i++)
        System.out.print(arr[i] + " ");
System.out.println();
    return;
}

/* The core function that recursively generates and prints all sequences of
length k */
static void printSequencesRecur(int arr[], int n, int k, int index)
{
int i;
if (k == 0)
{
    printArray(arr, index);
}
if (k > 0)
{
    for(i = 1; i<=n; ++i)
    {
        arr[index] = i;
        printSequencesRecur(arr, n, k-1, index+1);
    }
}
}

/* A function that uses printSequencesRecur() to prints all sequences
from 1, 1, ..1 to n, n, ..n */
static void printSequences(int n, int k)
{
    int arr[] = new int[k];
    printSequencesRecur(arr, n, k, 0);

return ;
}

/* Driver Program to test above functions */
public static void main(String[] args)
{
    int n = 3;
    int k = 2;
    printSequences(n, k);
}
}
```

## 蟒蛇 3

```
# Python3 program of above approach

# A utility function that prints a
# given arr[] of length size
def printArray(arr, size):

    for i in range(size):
        print(arr[i], end = " ");
    print("");
    return;

# The core function that recursively
# generates and prints all sequences
# of length k
def printSequencesRecur(arr, n, k, index):
    if (k == 0):
        printArray(arr, index);

    if (k > 0):
        for i in range(1, n + 1):
            arr[index] = i;
            printSequencesRecur(arr, n, k - 1,
                                    index + 1);

# A function that uses printSequencesRecur() to
# prints all sequences from 1, 1, ..1 to n, n, ..n
def printSequences(n, k):
    arr = [0] * n;
    printSequencesRecur(arr, n, k, 0);

    return;

# Driver Code
n = 3;
k = 2;
printSequences(n, k);

# This code is contributed mits
```

## C#

```
// C# program of above approach
using System;

class GFG
{

/* A utility function that prints a given
arr[] of length size*/
static void printArray(int []arr, int size)
{
    for(int i = 0; i < size; i++)
        Console.Write(arr[i] + " ");
    Console.WriteLine();
    return;
}

/* The core function that recursively generates
and prints all sequences of length k */
static void printSequencesRecur(int []arr, int n,
                                int k, int index)
{
    int i;
    if (k == 0)
    {
        printArray(arr, index);
    }
    if (k > 0)
    {
        for(i = 1; i<=n; ++i)
        {
            arr[index] = i;
            printSequencesRecur(arr, n, k - 1, index + 1);
        }
    }
}

/* A function that uses printSequencesRecur() to
prints all sequences from 1, 1, ..1 to n, n, ..n */
static void printSequences(int n, int k)
{
    int[] arr = new int[k];
    printSequencesRecur(arr, n, k, 0);

    return;
}

// Driver Code
public static void Main()
{
    int n = 3;
    int k = 2;
    printSequences(n, k);
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program of above approach

/* A utility function that prints a
given arr[] of length size*/
function printArray($arr, $size)
{
    for($i = 0; $i < $size; $i++)
        echo $arr[$i] . " ";
    echo "\n";
    return;
}

/* The core function that recursively generates
and prints all sequences of length k */
function printSequencesRecur($arr, $n, $k, $index)
{
    if ($k == 0)
    {
        printArray($arr, $index);
    }
    if ($k > 0)
    {
        for($i = 1; $i <= $n; ++$i)
        {
            $arr[$index] = $i;
            printSequencesRecur($arr, $n,
                                $k - 1, $index + 1);
        }
    }
}

/* A function that uses printSequencesRecur() to
prints all sequences from 1, 1, ..1 to n, n, ..n */
function printSequences($n, $k)
{
    $arr = array();
    printSequencesRecur($arr, $n, $k, 0);

    return;
}

// Driver Code
$n = 3;
$k = 2;
printSequences($n, $k);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// javascript program of above approach

/* A utility function that prints a given arr of length size*/
function printArray(arr, size)
{
    for(i = 0; i < size; i++)
        document.write(arr[i] + " ");
    document.write("<br>");
    return;
}

/* The core function that recursively
generates and prints all sequences of
length k */
function printSequencesRecur(arr , n , k , index)
{
    var i;
    if (k == 0)
    {
        printArray(arr, index);
    }
    if (k > 0)
    {
        for(i = 1; i <= n; ++i)
        {
            arr[index] = i;
            printSequencesRecur(arr, n, k - 1, index+1);
        }
    }
}

/* A function that uses printSequencesRecur()
to prints all sequences from 1, 1, ..1 to n, n, ..n */
function printSequences(n, k)
{
    var arr = Array.from({length: k}, (_, i) => 0);
    printSequencesRecur(arr, n, k, 0);

return ;
}

/* Driver Program to test above functions */
var n = 3;
var k = 2;
printSequences(n, k);

// This code is contributed by Amit Katiyar.
</script>
```

**输出:**

```
1 1
1 2
1 3
2 1
2 2
2 3
3 1
3 2
3 3
```

*时间复杂度:*有 n^k 序列，打印一个序列需要 O(k)个时间。所以时间复杂性就是 O(k*n^k).

***辅助空间:** O(k)*
感谢**莫普赛勇士**提示上述方法。正如 **alphayoung** 所建议的，我们可以避免对能够适合一个整数的小序列使用数组。以下是相同的实现。

## C++

```
// C++ program of above approach

/* The core function that generates and
prints all sequences of length k */
void printSeqRecur(int num, int pos, int k, int n)
{
    if (pos == k)
    {
        cout << num << endl;
        return;
    }
    for (int i = 1; i <= n; i++)
    {
        printSeqRecur(num * 10 + i, pos + 1, k, n);
    }
}

/* A function that uses printSequencesRecur()
to prints all sequences
from 1, 1, ..1 to n, n, ..n */
void printSequences(int k, int n)
{
    printSeqRecur(0, 0, k, n);
}

// This code is contributed by SHUBHAMSINGH10
```

## C

```
// C program of above approach
/* The core function that generates and prints all sequences of length k */
void printSeqRecur(int num, int pos, int k, int n)
{
    if (pos == k) {
        printf("%d \n", num);
        return;
    }
    for (int i = 1; i <= n; i++) {
        printSeqRecur(num * 10 + i, pos + 1, k, n);
    }
}

/* A function that uses printSequencesRecur() to prints all sequences
   from 1, 1, ..1 to n, n, ..n */
void printSequences(int k, int n)
{
    printSeqRecur(0, 0, k, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of above approach

/* The core function that generates and prints all sequences of length k */
static void printSeqRecur(int num, int pos, int k, int n)
{
    if (pos == k) {
        System.out.print(num + " ");
        return;
    }
    for (int i = 1; i <= n; i++) {
        printSeqRecur(num * 10 + i, pos + 1, k, n);
    }
}

/* A function that uses printSequencesRecur() to prints all sequences
from 1, 1, ..1 to n, n, ..n */
static void printSequences(int k, int n)
{
    printSeqRecur(0, 0, k, n);
}
```

## 蟒蛇 3

```
# Python program of above approach
# We have used number instead of
# arrays to prevent linear time
# required to print each string
def printSeqRecur ( num , n, k ):
    if n == 0: # if total digits become equal
                # to n, print the number and return
        print(num )
        return

    for _ in range(1, k + 1):
        printSeqRecur (num * 10 + _, n - 1, k)

# Driver Code
if __name__ == "__main__":
    k = 3 # length of k-ary string
    n = 2 # string can take values
          # from 1,2,3...n
    printSeqRecur(0, n, k)

# This code is contributed
# by shivam purohit
```

## C#

```
// C# program of above approach

/* The core function that generates
and prints all sequences of length k */
static void printSeqRecur(int num, int pos,
                            int k, int n)
{
    if (pos == k)
    {
        Console.Write(num + " ");
        return;
    }
    for (int i = 1; i <= n; i++)
    {
        printSeqRecur(num * 10 + i, pos + 1, k, n);
    }
}

/* A function that uses printSequencesRecur()
to prints all sequences from 1, 1, ..1 to n, n, ..n */
static void printSequences(int k, int n)
{
    printSeqRecur(0, 0, k, n);
}

// This code is contributed by Code_Mech
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program of above approach
// We have used number instead of
// arrays to prevent linear time
// required to print each string
function printSeqRecur ($num ,$n, $k)
{
    if ($n == 0)
    {
        # if total digits become equal
        # to n, print the number and return
        print($num . "\n");
        return;
    }

    for ($i = 1; $i < $k + 1; $i++)
        printSeqRecur($num * 10 +
                      $i, $n - 1, $k);
}

// Driver Code
$k = 3; // length of k-ary string
$n = 2; // string can take values
        // from 1,2,3...n
printSeqRecur(0, $n, $k);

// This code is contributed mits
?>
```

## java 描述语言

```
<script>

// Javascript program of above approach

/* The core function that generates and
prints all sequences of length k */
function printSeqRecur( num,  pos,  k,  n)
{
    if (pos == k)
    {
       document.write( num + "<br>" );
        return;
    }
    for (var i = 1; i <= n; i++)
    {
        printSeqRecur(num * 10 + i, pos + 1, k, n);
    }
}

/* A function that uses printSequencesRecur()
to prints all sequences
from 1, 1, ..1 to n, n, ..n */
function printSequences( k,  n)
{
    printSeqRecur(0, 0, k, n);
}

// This code is contributed by SoumikMondal
</script>
```

***时间复杂度:** O(k*n^k)*

***辅助空间:** O(n * k)*

**参考文献:**
[算法与编程:沈山大](http://www.amazon.com/Algorithms-Programming-Solutions-Alexander-Shen/dp/0817638474)
的问题与解决方案如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论。