# 尾呼消除

> 原文:[https://www.geeksforgeeks.org/tail-call-elimination/](https://www.geeksforgeeks.org/tail-call-elimination/)

我们已经讨论过(在[尾部递归](https://www.geeksforgeeks.org/tail-recursion/)中)如果递归调用是函数执行的最后一件事，那么递归函数就是尾部递归。

## C++

```
// An example of tail recursive function
void print(int n)
{
    if (n < 0) 
       return;
    cout << " " << n;

    // The last executed statement is recursive call
    print(n-1);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// An example of tail recursive function
static void print(int n)
{
    if (n < 0) 
       return;

      System.out.print(" " + n);

    // The last executed statement
    // is recursive call
    print(n - 1);
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# An example of tail recursive function
def print(n):

    if (n < 0):
       return

    print(" ", n)

    # The last executed statement is recursive call
    print(n - 1)

# This code is contributed by sanjoy_62
```

## C#

```
// An example of tail recursive function
static void print(int n)
{
    if (n < 0) 
       return;

      Console.Write(" " + n);

    // The last executed statement
    // is recursive call
    print(n - 1);
}

// This code is contributed by pratham76
```

## java 描述语言

```
<script>

// An example of tail recursive function
function print(n)
{
    if (n < 0) 
       return;
    document.write( " " + n);

    // The last executed statement is recursive call
    print(n-1);
}

</script>
```

我们还讨论了尾部递归<u>优于</u>和<u>非尾部递归，因为尾部递归可以被现代编译器优化。现代编译器基本上是</u>做**<u>尾调用消去</u>** <u>来优化</u>尾-递归<u>代码。</u>

如果我们仔细看看上面的函数，我们可以用 goto 移除最后一个调用。下面是尾部呼叫消除的例子。

## C++

```
// Above code after tail call elimination
void print(int n)
{
start:
    if (n < 0)
       return;
    cout << " " << n;

    // Update parameters of recursive call
    // and replace recursive call with goto
    n = n-1
    goto start;
}
```

[**快速排序**](http://geeksquiz.com/quick-sort/) **:再举一个例子**
快速排序也是尾部递归(注意 [MergeSort](http://geeksquiz.com/merge-sort/) 不是尾部递归，这也是快速排序表现更好的原因之一)

## C++

```
/* Tail recursive function for QuickSort
 arr[] --> Array to be sorted,
  low  --> Starting index,
  high  --> Ending index */
void quickSort(int arr[], int low, int high)
{
    if (low < high)
    {
        /* pi is partitioning index, arr[p] is now
           at right place */
        int pi = partition(arr, low, high);

        // Separately sort elements before
        // partition and after partition
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}
// See below link for complete running code
// http://geeksquiz.com/quick-sort/
```

尾呼消除后跟随可以代替上述功能。

## C++

```
/* QuickSort after tail call elimination
  arr[] --> Array to be sorted,
  low  --> Starting index,
  high  --> Ending index */
void quickSort(int arr[], int low, int high)
{
start:
    if (low < high)
    {
        /* pi is partitioning index, arr[p] is now
           at right place */
        int pi = partition(arr, low, high);

        // Separately sort elements before
        // partition and after partition
        quickSort(arr, low, pi - 1);

        // Update parameters of recursive call
        // and replace recursive call with goto
        low = pi+1;
        high = high;
        goto start;
    }
}
// See below link for complete running code
// https://ide.geeksforgeeks.org/dbq4yl
```

因此，编译器的工作是识别尾部递归，在开头添加一个标签，在结尾更新参数，然后添加最后一个 goto 语句。

**尾调用消除中的函数栈帧管理:**
递归使用栈来跟踪函数调用。每次函数调用时，都会有一个新的框架被推送到堆栈上，其中包含该调用的局部变量和数据。假设一个堆栈帧需要 0(1)，即恒定的内存空间，那么对于 **N** 递归调用，所需的内存将是 0(N)。

尾调用消除降低了从 O(N)到 O(1)递归的空间复杂度。由于取消了函数调用，因此不会创建新的堆栈帧，并且函数会在恒定的内存空间中执行。

函数可以在常量内存空间中执行，因为在尾部递归函数中，调用语句之后没有语句，所以不需要保留父函数的状态和框架。子函数被调用并立即完成，它不必将控制返回给父函数。

由于不对返回值执行任何计算，也没有语句等待执行，因此可以根据当前函数调用的要求修改当前帧。因此，不需要保留先前函数调用的堆栈帧，函数在恒定的内存空间中执行。这使得尾部递归更快，并且对内存友好。

**下一篇:**
[快速排序尾呼优化(将最坏情况空间减少到 Log n )](https://www.geeksforgeeks.org/quicksort-tail-call-optimization-reducing-worst-case-space-log-n/)
本文由 **Dheeraj Jain** 供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息