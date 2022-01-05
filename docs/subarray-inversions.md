# 子阵列反转

> 原文:[https://www.geeksforgeeks.org/subarray-inversions/](https://www.geeksforgeeks.org/subarray-inversions/)

我们有一个由 n 个整数组成的数组，我们计划对其进行排序。具体来说，我们想知道数组离排序有多近。为了实现这一点，我们引入了*反转*的概念。数组中的反转是一对两个索引 *i* 和 *j* ，这样 *i* < *j* 和*A【I】*>*A【j】*。如果我们的数组包含一个反转，我们只需要交换 *A[i]* 和 *A[j]* 就可以对数组进行排序。根据定义，包含 *0* 反转的数组是排序的。

**问题:**给定一个由 *n* 个整数组成的数组 *A* ，求所有长度为 *k* 的子阵中的逆序数之和。为了澄清，必须确定长度为 *k* 的*n–k+1*子阵列中的每个子阵列中的反转数量，并将它们相加。
输入:第一行包含两个空格分隔的整数 *n* 和 *k* 。下一行包含一个由 *n* 个空格分隔的整数组成的序列，其中序列中的第 *i* 个整数是*A【I】*。

**示例:**

```
Input : arr[] = {1 2 3 4 5 6}
        k = 2
Output : 0

Input : arr[] = {1 6 7 2}
        k = 3
Output : 2
There are two subarrays of size 3,
{1, 6, 7} and {6, 7, 2}. Count of
inversions in first subarray is 0
and count of inversions in second
subarray is 2\. So sum is 0 + 2 = 2

Input :  8 4
12 3 14 8 15 1 4 22
Output : 14

Input :  10 5
15 51 44 44 76 50 29 88 48 50
Output : 25
```

**【1】天真方法**
这个问题刚开始看起来相当琐碎，我们可以很容易地实现一个天真的算法来强行解决。我们只需创建一个长度为 *k* 的窗口，并沿着 *A* 滚动该窗口，在每次迭代中添加该窗口中的反转数量。要找到反转的数量，最简单的方法是使用两个 for 循环来考虑所有元素对，如果元素对形成反转，则增加一个计数器。

这种方法很容易实现，但它有效率吗？我们来分析一下算法。最外面的循环运行*n–k+1*次，对于 *A* 的每个 *k* 子阵列一次。在每一次迭代中，我们都会在窗口中找到反转的次数。为此，我们考虑元素 *1* 和元素 *2* ，…， *n* ，然后元素 *2* 和元素 *3* ，…， *n* 直到元素*n–1*和元素 *n* 。实际上，我们正在执行*n+(n–1)+(n–2)+…+1 = n(n+1)/2*运算。因此，我们的算法执行近似的*(n–k+1)(n)(n+1)/2*运算，即*o(n^3–kn^2)*。由于 k 的范围可以从 1 到 n，当 *k = n/2* 时，该算法的最坏情况性能是 *O(n^3)* 。我们可以做得更好！

## C++

```
// C++ implementation of above approach
#include <iostream>
using namespace std;

// Helper function, counts number of inversions
// via bubble sort loop
int bubble_count(int arr[], int start, int end)
{
    int count = 0;
    for (int i = start; i < end; i++)
    {
        for (int j = i + 1; j < end; j++)
        {
            if (arr[i] > arr[j])
            {
                count++;
            }
        }
    }
    return count;
}

// Inversion counting method, slides window of
// [start, end] across array
int inversion_count(int n, int k, int a[])
{
    int count = 0;
    for (int start = 0; start < n - k + 1; start++)
    {
        int end = start + k;
        count += bubble_count(a, start, end);
    }
    return count;
}

// Driver Code
int main()
{
    int n = 10;
    int arr[n] = { 15, 51, 44, 44, 76,
                   50, 29, 88, 48, 50 };
    int k = 5;

    int result = inversion_count(n, k, arr);
    cout << result;
    return 0;
}

// This code is contributed by PrinciRaj1992
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
public class Subarray_Inversions {

    // Inversion counting method, slides window of [start,
    // end] across array
    static int inversion_count(int n, int k, int[] a)
    {
        int count = 0;
        for (int start = 0; start < n - k + 1; start++) {
            int end = start + k;
            count += bubble_count(a, start, end);
        }
        return count;
    }

    // Helper function, counts number of inversions via
    // bubble sort loop
    public static int bubble_count(int[] arr, int start, int end)
    {
        int count = 0;
        for (int i = start; i < end; i++) {
            for (int j = i + 1; j < end; j++) {
                if (arr[i] > arr[j]) {
                    count++;
                }
            }
        }
        return count;
    }

    public static void main(String[] args)
    {
        int n = 10;
        int[] arr = { 15, 51, 44, 44, 76, 50, 29, 88, 48, 50 };
        int k = 5;

        long result = inversion_count(n, k, arr);
        System.out.println(result);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Helper function, counts number of inversions
# via bubble sort loop
def bubble_count(arr, start, end):
    count = 0;
    for i in range(start, end):

        for j in range(i + 1, end):

            if (arr[i] > arr[j]):
                count += 1;

    return count;

# Inversion counting method, slides window
# of [start, end] across array
def inversion_count(n, k, a):
    count = 0;
    for start in range(0, n - k + 1):
        end = start + k;
        count += bubble_count(a, start, end);

    return count;

# Driver Code
if __name__ == '__main__':
    n = 10;
    arr = [15, 51, 44, 44, 76,
           50, 29, 88, 48, 50];
    k = 5;

    result = inversion_count(n, k, arr);
    print(result);

# This code is contributed by Rajput-Ji
```

## C#

```
// C# implementation of above approach
using System;

public class Subarray_Inversions
{

    // Inversion counting method, slides window of [start,
    // end] across array
    static int inversion_count(int n, int k, int[] a)
    {
        int count = 0;
        for (int start = 0; start < n - k + 1; start++)
        {
            int end = start + k;
            count += bubble_count(a, start, end);
        }
        return count;
    }

    // Helper function, counts number of inversions via
    // bubble sort loop
    public static int bubble_count(int[] arr, int start, int end)
    {
        int count = 0;
        for (int i = start; i < end; i++)
        {
            for (int j = i + 1; j < end; j++)
            {
                if (arr[i] > arr[j])
                {
                    count++;
                }
            }
        }
        return count;
    }

    // Driver code
    public static void Main()
    {
        int n = 10;
        int[] arr = { 15, 51, 44, 44, 76, 50, 29, 88, 48, 50 };
        int k = 5;

        long result = inversion_count(n, k, arr);
        Console.WriteLine(result);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // Inversion counting method, slides window of [start,
    // end] across array
    function inversion_count(n,k,a)
    {
        let count = 0;
        for (let start = 0; start < n - k + 1; start++) {
            let end = start + k;
            count += bubble_count(a, start, end);
        }
        return count;
    }

    // Helper function, counts number of inversions via
    // bubble sort loop
    function bubble_count(arr,start,end)
    {
        let count = 0;
        for (let i = start; i < end; i++) {
            for (let j = i + 1; j < end; j++) {
                if (arr[i] > arr[j]) {
                    count++;
                }
            }
        }
        return count;
    }

        let n = 10;
        let arr = [ 15, 51, 44, 44, 76, 50, 29, 88, 48, 50 ];
        let k = 5;

        let result = inversion_count(n, k, arr);
        document.write(result);

// This code is contributed by G.Sravan Kumar (171FA07058)

</script>
```

**输出:**

```
 25
```

**【2】基于合并排序的实现**
我们可以做的一个优化是改进我们低效的二次时间反演计数方法。一种方法是使用本文中概述的基于合并排序的方法。由于这在 *O(nlogn)* 中运行，我们的整体运行时间减少到 *O(n^2logn)* ，这更好，但是仍然不能处理 *n = 10^6* 的情况。

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

public class Subarray_Inversions {

    // Inversion counting method, slides window of [start,
    // end] across array
    static int inversion_count(int n, int k, int[] a)
    {
        int count = 0;
        for (int start = 0; start < n - k + 1; start++) {
            int[] sub_array = new int[k];
            for (int i = start; i < start + k; i++) {
                sub_array[i - start] = a[i];
            }
            count += subarray_inversion_count(sub_array);
        }
        return count;
    }

    // Counts number of inversions when merging
    public static long merge_inversion_count(int[] arr,
                                int[] left, int[] right)
    {
        int i = 0, j = 0, count = 0;
        while (i < left.length || j < right.length) {
            if (i == left.length) {
                arr[i + j] = right[j];
                j++;
            } else if (j == right.length) {
                arr[i + j] = left[i];
                i++;
            } else if (left[i] <= right[j]) {
                arr[i + j] = left[i];
                i++;
            } else {
                arr[i + j] = right[j];
                count += left.length - i;
                j++;
            }
        }
        return count;
    }

    // Divide and conquer approach -- splits array and counts
    // inversions via merge method
    public static long subarray_inversion_count(int[] arr)
    {
        if (arr.length < 2)
            return 0;

        int m = (arr.length + 1) / 2;
        int left[] = Arrays.copyOfRange(arr, 0, m);
        int right[] = Arrays.copyOfRange(arr, m, arr.length);

        return subarray_inversion_count(left) +
               subarray_inversion_count(right) +
               merge_inversion_count(arr, left, right);
    }

    public static void main(String[] args)
    {
        int n = 10;
        int[] arr = { 15, 51, 44, 44, 76, 50, 29, 88, 48, 50 };
        int k = 5;

        long result = inversion_count(n, k, arr);
        System.out.println(result);
    }
}
```

## C#

```
using System;
using System.Collections.Generic;

public class Subarray_Inversions {

    // Inversion counting method, slides window of [start,
    // end] across array
    static int inversion_count(int n, int k, int[] a)
    {
        int count = 0;
        for (int start = 0; start < n - k + 1; start++) {
            int[] sub_array = new int[k];
            for (int i = start; i < start + k; i++) {
                sub_array[i - start] = a[i];
            }
            count += subarray_inversion_count(sub_array);
        }
        return count;
    }

    // Counts number of inversions when merging
    public static int merge_inversion_count(int[] arr,
                                int[] left, int[] right)
    {
        int i = 0, j = 0, count = 0;
        while (i < left.Length || j < right.Length) {
            if (i == left.Length) {
                arr[i + j] = right[j];
                j++;
            } else if (j == right.Length) {
                arr[i + j] = left[i];
                i++;
            } else if (left[i] <= right[j]) {
                arr[i + j] = left[i];
                i++;
            } else {
                arr[i + j] = right[j];
                count += left.Length - i;
                j++;
            }
        }
        return count;
    }

    // Divide and conquer approach -- splits array and counts
    // inversions via merge method
    public static int subarray_inversion_count(int[] arr)
    {
        if (arr.Length < 2)
            return 0;

        int m = (arr.Length + 1) / 2;
        int []left = new int[m];
        Array.Copy(arr, 0, left,0, m);
        int []right = new int[arr.Length - m];
        Array.Copy(arr, m, right,0, arr.Length - m);

        return subarray_inversion_count(left) +
               subarray_inversion_count(right) +
               merge_inversion_count(arr, left, right);
    }

    public static void Main(String[] args)
    {
        int n = 10;
        int[] arr = { 15, 51, 44, 44, 76, 50, 29, 88, 48, 50 };
        int k = 5;

        long result = inversion_count(n, k, arr);
        Console.WriteLine(result);
    }
}

// This code is contributed by Rajput-Ji
```

**输出:**

```
 25
```

**【3】重叠子阵列实现**
让我们重新审视我们的整体方法。我们在看窗口*【0，k)* 求逆序数，然后看*【1，k+1)* 。这个范围有一个明显的重叠:我们已经在第一次迭代的时候统计了*【1，k)* 中的反转次数，现在我们又开始统计了！让我们计算从一个窗口到下一个窗口的反转变化，而不是计算反转。实际上，移动窗口只是在窗口的头部添加一个元素，从尾部移除一个元素，窗口的主体保持不变。检查内部元素之间的反转是多余的；我们所需要做的就是把新元素引起的反转数相加，再减去被去掉的元素引起的反转数。我们现在只需要计算第一个窗口中的反转次数，这可以在 *O(klogk)* 时间内完成，对于每个*n–k*的附加窗口，我们只需通过数组中的 *k* 元素进行一次迭代，就可以找到反转次数的变化。我们的整体运行时间现在是*o(k(n–k)+klogk)*=*o(NK–k)*这仍然是最坏的情况 *O(n^2)* 。

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

public class Subarray_Inversions {

    // Inversion counting method, slides window of [start,
    // end] across array
    static long inversion_count(int n, int m, int[] arr)
    {
        long count = 0;
        count += subarray_inversion_count_initial(Arrays.copyOfRange(arr, 0, m));
        long subarray_count = subarray_inversion_count_initial(Arrays.copyOfRange(arr, 1, m));
        for (int start = 1; start <= n - m; start++) {
            int end = start + m - 1;
            long[] ans = subarray_inversion_count(arr, start, end, subarray_count);
            count += ans[0];
            subarray_count = ans[1];
        }
        return count;
    }

    // start >=1; find inversion in interval [start, end)
    public static long[] subarray_inversion_count(int[] arr, int start,
                                          int end, long subarray_count)
    {
        int new_element = arr[end];
        long count = subarray_count;
        for (int i = start; i < end; i++) {
            if (new_element < arr[i])
                count++;
        }
        long totalSum = count;
        int last_element = arr[start];
        for (int i = start + 1; i <= end; i++) {
            if (last_element > arr[i])
                count--;
        }
        long[] ans = { totalSum, count };
        return ans;
    }

    // Counts number of inversions when merging
    public static long merge_inversion_count(int[] arr, int[] left,
                                                       int[] right)
    {
        int i = 0, j = 0, count = 0;
        while (i < left.length || j < right.length) {
            if (i == left.length) {
                arr[i + j] = right[j];
                j++;
            } else if (j == right.length) {
                arr[i + j] = left[i];
                i++;
            } else if (left[i] <= right[j]) {
                arr[i + j] = left[i];
                i++;
            } else {
                arr[i + j] = right[j];
                count += left.length - i;
                j++;
            }
        }
        return count;
    }

    // Divide and conquer approach -- splits array and counts
    // inversions via merge method
    public static long subarray_inversion_count_initial(int[] arr)
    {
        if (arr.length < 2)
            return 0;

        int m = (arr.length + 1) / 2;
        int left[] = Arrays.copyOfRange(arr, 0, m);
        int right[] = Arrays.copyOfRange(arr, m, arr.length);

        return subarray_inversion_count_initial(left) +
               subarray_inversion_count_initial(right) +
               merge_inversion_count(arr, left, right);
    }

    public static void main(String[] args) throws Exception
    {
        int n = 10;
        int[] arr = { 15, 51, 44, 44, 76, 50, 29, 88, 48, 50 };
        int k = 5;

        long result = inversion_count(n, k, arr);
        System.out.println(result);
    }
}
```

**输出:**

```
 25
```

**【4】二进制索引树实现**
迭代每个窗口似乎是不可避免的，所以这里的瓶颈似乎是我们处理窗口的方式。我们知道连续的窗口明显重叠，所以我们需要知道的是元素数量大于新添加的元素，元素数量小于新移除的元素。很多时候，重复执行相同或相似操作的算法可以通过使用更健壮的数据结构来改进。在我们的例子中，我们正在寻找一种动态数据结构，它可以有效地回答关于元素排序时相对位置的查询。我们可以使用自平衡二叉树来实际维护一个排序列表，但是插入/移除需要对数时间。我们可以使用二进制索引树或芬威克树在恒定时间内做到这一点。

二进制索引树是以数组形式表示的树。它使用巧妙的位操作来非常高效地计算元素的累积和。我们可以调用函数 *update(index，val)* 函数将 *val* 添加到*BIT【index】*和 index 的所有祖先。函数 *read(index)* 返回存储在*BIT【index】*中的值与树中 *index* 的所有祖先的总和。因此，调用 *read(index)* 返回 *BIT* 中所有元素的累计和小于或等于 *index* 。如果我们简单地存储 *1* 而不是存储值，我们可以使用 *read(index + 1)* 来确定小于 index 的元素数量。现在，我们可以通过插入第一个窗口的元素(更新)来构建二进制索引树。对于后续的窗口，我们可以通过调用 *update(tail_element，-1)* 来移除尾部元素，并用 *update(head_element，1)* 来添加新元素。由于这是一棵树，最长可能的根节点路径是 *O(logk)* ，因此，我们实现了*O(nlogk+klogk)*=*O(nlogk)*！

还是我们…？请记住，二进制索引树为范围*【0，max _ element】*中的每个可能值分配内存，因此这需要 *O(max_element)* 时间和空间。对于非常稀疏的阵列，这可能相当昂贵。相反，我们可以定义一个散列函数来。我们可以这样做，因为我们只关心反演——只要我们保持相对大小不变(即*A【I】*<=*A*=>*A【哈希(I)】*<=*A【哈希(j)】*)，我们的解决方案仍然是正确的。因此，我们可以将 *A* 中的所有元素映射到集合 *{0，1，2，…，n}* ，产生 *O(nlogk)* 的保证运行时间。

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

public class Subarray_Inversions {

    // Declare binary indexed tree with global scope
    static BIT bit;

    // first window, counts first k elements and creates
    // BIT
    static long inversionCountBIT1(int[] arr, int start,
                                               int end)
    {
        bit = new BIT(arr.length);
        long count = 0;
        for (int index = start; index >= end; index--) {
            count += bit.read(arr[index]);
            bit.update(arr[index], 1);
        }
        return count;
    }

    // subsequent windows, removes previous element, adds
    // new element, and increments change in inversions
    static long inversionCountBIT2(int[] arr, int start,
                                       int end, long val)
    {
        bit.update(arr[start + 1], -1); // remove trailing element

        // find number of elements in range [start, end-1]
        // greater than first
        int numGreaterThanFirst = start - end - bit.read(arr[start + 1] + 1);
        long count = val + bit.read(arr[end]) - numGreaterThanFirst;
        bit.update(arr[end], 1); // adds leading element

        return count;
    }

    // Main method to count inversions in size k subarrays
    public static long inversionCount(int n, int k, int[] arr)
    {
        bit = new BIT(n);
        HashMap<Integer, Integer> freq = new HashMap<Integer, Integer>();
        int[] asort = arr.clone();

        // Map elements from [A[0]...A[n-1]] to [1...n]
        Arrays.sort(asort);
        int index = 0;
        int current = 1;
        for (int i = 0; i < n; i++) {
            if (!freq.containsKey(asort[i])) {
                freq.put(asort[i], current);
                current++;
            }
        }
        for (int i = 0; i < n; i++) {
            arr[i] = freq.get(arr[i]);
        }

        long count = 0;
        long val = 0;

        //[start - end] ==> start - end = k+1
        for (int start = n - 1; start >= k - 1; start--) {
            int end = start - k + 1;
            if (start == n - 1) { // First pass
                val = inversionCountBIT1(arr, n - 1, n - k);
            } else { // subsequent passes
                val = inversionCountBIT2(arr, start, end, val);
            }
            count += val;
        }
        return count;
    }

    public static void main(String[] args) throws Exception
    {
        int n = 10;
        int[] arr = { 15, 51, 44, 44, 76, 50, 29, 88, 48, 50 };
        int k = 5;

        long result = inversionCount(n, k, arr);
        System.out.println(result);
    }

    // Implementation of Binary Indexed Tree
    static class BIT {
        int[] tree;
        int maxVal;
    public BIT(int N)
        {
            tree = new int[N + 1];
            maxVal = N;
        }

        // Updates BIT, starting with element at index
        // and all ancestors
        void update(int index, int val)
        {
            while (index <= maxVal) {
                tree[index] += val;
                index += (index & -index);
            }
        }

        // Returns the cumulative frequency of index
        // starting with element at index and all ancestors
        int read(int index)
        {
            --index;
            int cumulative_sum = 0;
            while (index > 0) {
                cumulative_sum += tree[index];
                index -= (index & -index);
            }
            return cumulative_sum;
        }
    };
}
```

## C#

```
using System;
using System.Collections.Generic;

class Subarray_Inversions{

// Implementation of Binary Indexed Tree
public class BIT
{
    public int[] tree;
    public int maxVal;

    public BIT(int N)
    {
        tree = new int[N + 1];
        maxVal = N;
    }

    // Updates BIT, starting with element
    // at index and all ancestors
    public void update(int index, int val)
    {
        while (index <= maxVal)
        {
            tree[index] += val;
            index += (index & -index);
        }
    }

    // Returns the cumulative frequency
    // of index starting with element at
    // index and all ancestors
    public int read(int index)
    {
        --index;
        int cumulative_sum = 0;

        while (index > 0)
        {
            cumulative_sum += tree[index];
            index -= (index & -index);
        }
        return cumulative_sum;
    }
};

// Declare binary indexed tree
// with global scope
static BIT bit;

// First window, counts first k elements
// and creates BIT
static long inversionCountBIT1(int[] arr, int start,
                               int end)
{
    bit = new BIT(arr.Length);
    long count = 0;

    for(int index = start; index >= end; index--)
    {
        count += bit.read(arr[index]);
        bit.update(arr[index], 1);
    }
    return count;
}

// Subsequent windows, removes previous element, adds
// new element, and increments change in inversions
static long inversionCountBIT2(int[] arr, int start,
                               int end, long val)
{

    // Remove trailing element
    bit.update(arr[start + 1], -1);

    // Find number of elements in
    // range [start, end-1] greater
    // than first
    int numGreaterThanFirst = start - end -
                 bit.read(arr[start + 1] + 1);
    long count = val + bit.read(arr[end]) -
                 numGreaterThanFirst;

    bit.update(arr[end], 1); // Adds leading element

    return count;
}

// Main method to count inversions in size k subarrays
public static long inversionCount(int n, int k, int[] arr)
{
    bit = new BIT(n);
    Dictionary<int,
               int> freq = new Dictionary<int,
                                          int>();

    int[] asort = (int[])arr.Clone();

    // Map elements from [A[0]...A[n-1]] to [1...n]
    Array.Sort(asort);
    //int index = 0;
    int current = 1;

    for(int i = 0; i < n; i++)
    {
        if (!freq.ContainsKey(asort[i]))
        {
            freq.Add(asort[i], current);
            current++;
        }
    }
    for(int i = 0; i < n; i++)
    {
        arr[i] = freq[arr[i]];
    }

    long count = 0;
    long val = 0;

    //[start - end] ==> start - end = k+1
    for(int start = n - 1; start >= k - 1; start--)
    {
        int end = start - k + 1;

        if (start == n - 1)// First pass
        {
            val = inversionCountBIT1(arr, n - 1,
                                          n - k);
        }
        else // subsequent passes
        {
            val = inversionCountBIT2(arr, start,
                                     end, val);
        }
        count += val;
    }
    return count;
}

// Driver code
public static void Main(String[] args)
{
    int n = 10;
    int[] arr = { 15, 51, 44, 44, 76,
                  50, 29, 88, 48, 50 };
    int k = 5;
    long result = inversionCount(n, k, arr);

    Console.WriteLine(result);
}
}

// This code is contributed by Amit Katiyar
```

**输出:**

```
 25
```

本文由**乔尔·亚伯拉罕**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。