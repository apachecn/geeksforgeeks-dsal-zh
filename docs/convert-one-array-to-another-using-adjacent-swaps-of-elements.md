# 使用相邻的元素交换将一个数组转换成另一个数组

> 原文:[https://www . geesforgeks . org/convert-一个数组到另一个数组-使用相邻元素交换/](https://www.geeksforgeeks.org/convert-one-array-to-another-using-adjacent-swaps-of-elements/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr1[]** 和 **arr2[]** 的 **N** 整数。我们可以从数组**arr 1【】**中选择任意两个相邻的元素，如果它们是相反的奇偶性，则交换它们，任务是通过对**arr 1【】**执行给定的操作，检查是否有可能将数组**arr 1【】**转换为数组**arr 2【】**。如果可以将数组 **arr1[]** 转换为 **arr2[]** 则打印**“是”**否则打印**“否”**。
**举例:**

> **输入:** arr1[] = {5，7，8，2，10，13}，arr2[] = {8，5，2，7，13，10}
> **输出:**是
> **解释:**
> 一开始，交换 10 和 13 所以 arr1[] = [5，7，8，2，13，10]。
> 现在，交换 7 和 8，这样 arr1[] = [5，8，7，2，13，10]。
> 现在，交换 5 和 8，这样 arr1[] = [8，5，7，2，13，10]。
> 现在，交换 7 和 2，这样 arr1[] = [8，5，2，7，13，10] = arr2[]。
> 在每个操作中，我们交换具有不同奇偶性的相邻元素。
> **输入:** arr1[] = {0，1，13，3，4，14，6}，arr2[] = {0，1，14，3，4，13，6}
> **输出:**否
> **说明:**
> 13，14 不相邻，不可能互换。

**进场:**使用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。因为我们不能交换任何两个偶数或奇数。因此[偶数和奇数在数组](https://www.geeksforgeeks.org/count-number-even-odd-elements-array/)**arr 1【】**和**arr 2【】**中的相对位置必须完全相同，以使两个数组在给定的操作下相等。以下是步骤:

1.  创建两个数组(比如**偶数[]** 和**奇数[]** )分别在**偶数[]** 和**奇数[]** 中插入来自 **arr1[]** 的所有偶数和奇数。
2.  现在检查**arr 2【】**中的偶数和奇数的顺序是否与**偶数【】**和**奇数【】**中的顺序相同。
3.  如果以上步骤没有给出**偶[]** 和**奇[]** 数组中不按数字顺序排列的 **arr2[]** 的任何数字，则打印**“是”**否则打印**“否”**。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function which checks if it is
// possible to convert arr1[] to
// arr2[] by given operations
void convert(int a[], int b[], int n)
{

    // even[] will store the even
    // elements of a[]

    // odd[] will store the odd
    // elements of a[]
    vector<int> even, odd;

    // Traverse a[] and insert the even
    // and odd element respectively
    for (int x = 0; x < n; x++) {

        if (a[x] % 2 == 0)
            even.push_back(a[x]);
        else
            odd.push_back(a[x]);
    }

    // ei points to the next
    // available even element

    // oi points to the next
    // available odd element
    int ei = 0, oi = 0;

    // poss will store whether the
    // given transformation
    // of a[] to b[] is possible
    bool poss = true;

    // Traverse b[]
    for (int x = 0; x < n; x++) {

        if (b[x] % 2 == 0) {

            // Check if both even
            // elements are equal
            if (ei < even.size()
                && b[x] == even[ei]) {
                ei++;
            }
            else {
                poss = false;
                break;
            }
        }
        else {

            // Check if both odd
            // elements are equal
            if (oi < odd.size()
                && b[x] == odd[oi]) {
                oi++;
            }
            else {
                poss = false;
                break;
            }
        }
    }

    // If poss is true, then we can
    // transform a[] to b[]
    if (poss)

        cout << "Yes" << endl;

    else

        cout << "No" << endl;
}

// Driver Code
int main()
{
    // Given arrays
    int arr1[] = { 0, 1, 13, 3, 4, 14, 6 };
    int arr2[] = { 0, 1, 14, 3, 4, 13, 6 };

    int N = sizeof(arr1) / sizeof(arr1[0]);

    // Function Call
    convert(arr1, arr2, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function which checks if it is
// possible to convert arr1[] to
// arr2[] by given operations
static void convert(int a[], int b[], int n)
{

    // even[] will store the even
    // elements of a[]

    // odd[] will store the odd
    // elements of a[]
    Vector<Integer> even = new Vector<Integer>(),
                     odd = new Vector<Integer>();

    // Traverse a[] and insert the even
    // and odd element respectively
    for(int x = 0; x < n; x++)
    {
       if (a[x] % 2 == 0)
           even.add(a[x]);
       else
           odd.add(a[x]);
    }

    // ei points to the next
    // available even element

    // oi points to the next
    // available odd element
    int ei = 0, oi = 0;

    // poss will store whether the
    // given transformation
    // of a[] to b[] is possible
    boolean poss = true;

    // Traverse b[]
    for(int x = 0; x < n; x++)
    {
       if (b[x] % 2 == 0)
       {

           // Check if both even
           // elements are equal
           if (ei < even.size() &&
               b[x] == even.get(ei))
           {
               ei++;
           }
           else
           {
               poss = false;
               break;
           }
       }
       else
       {

           // Check if both odd
           // elements are equal
           if (oi < odd.size() &&
               b[x] == odd.get(oi))
           {
               oi++;
           }
           else
           {
               poss = false;
               break;
           }
       }
    }

    // If poss is true, then we can
    // transform a[] to b[]
    if (poss)
        System.out.print("Yes" + "\n");
    else
        System.out.print("No" + "\n");
}

// Driver Code
public static void main(String[] args)
{

    // Given arrays
    int arr1[] = { 0, 1, 13, 3, 4, 14, 6 };
    int arr2[] = { 0, 1, 14, 3, 4, 13, 6 };

    int N = arr1.length;

    // Function Call
    convert(arr1, arr2, N);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function which checks if it is
# possible to convert arr1[] to
# arr2[] by given operations
def convert(a, b, n):

    # even[] will store the even
    # elements of a[]

    # odd[] will store the odd
    # elements of a[]
    even = []
    odd = []

    # Traverse a[] and insert the even
    # and odd element respectively
    for x in range(n):
        if (a[x] % 2 == 0):
            even.append(a[x])
        else:
            odd.append(a[x])

    # ei points to the next
    # available even element

    # oi points to the next
    # available odd element
    ei, oi = 0, 0

    # poss will store whether the
    # given transformation
    # of a[] to b[] is possible
    poss = True

    # Traverse b[]
    for x in range(n):
        if (b[x] % 2 == 0):

            # Check if both even
            # elements are equal
            if (ei < len(even) and
                 b[x] == even[ei]):
                ei += 1

            else:
                poss = False
                break
        else:

            # Check if both odd
            # elements are equal
            if (oi < len(odd) and
                 b[x] == odd[oi]):
                oi += 1

            else:
                poss = False
                break

    # If poss is true, then we can
    # transform a[] to b[]
    if (poss):
        print("Yes")
    else:
        print("No")

# Driver Code
if __name__ == "__main__":

    # Given arrays
    arr1 = [ 0, 1, 13, 3, 4, 14, 6 ]
    arr2 = [ 0, 1, 14, 3, 4, 13, 6 ]

    N = len(arr1)

    # Function call
    convert(arr1, arr2, N)

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function which checks if it is
// possible to convert arr1[] to
// arr2[] by given operations
static void convert(int []a, int []b, int n)
{

    // even[] will store the even
    // elements of []a

    // odd[] will store the odd
    // elements of []a
    List<int> even = new List<int>(),
               odd = new List<int>();

    // Traverse []a and insert the even
    // and odd element respectively
    for(int x = 0; x < n; x++)
    {
        if (a[x] % 2 == 0)
            even.Add(a[x]);
        else
            odd.Add(a[x]);
    }

    // ei points to the next
    // available even element

    // oi points to the next
    // available odd element
    int ei = 0, oi = 0;

    // poss will store whether the
    // given transformation
    // of []a to []b is possible
    bool poss = true;

    // Traverse []b
    for(int x = 0; x < n; x++)
    {
        if (b[x] % 2 == 0)
        {

            // Check if both even
            // elements are equal
            if (ei < even.Count &&
                b[x] == even[ei])
            {
                ei++;
            }
            else
            {
                poss = false;
                break;
            }
        }
        else
        {

            // Check if both odd
            // elements are equal
            if (oi < odd.Count &&
                b[x] == odd[oi])
            {
                oi++;
            }
            else
            {
                poss = false;
                break;
            }
        }
    }

    // If poss is true, then we can
    // transform []a to []b
    if (poss)
        Console.Write("Yes" + "\n");
    else
        Console.Write("No" + "\n");
}

// Driver Code
public static void Main(String[] args)
{

    // Given arrays
    int []arr1 = { 0, 1, 13, 3, 4, 14, 6 };
    int []arr2 = { 0, 1, 14, 3, 4, 13, 6 };

    int N = arr1.Length;

    // Function call
    convert(arr1, arr2, N);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function which checks if it is
// possible to convert arr1[] to
// arr2[] by given operations
function convert(a, b, n)
{

    // even[] will store the even
    // elements of a[]

    // odd[] will store the odd
    // elements of a[]
    var even = [], odd = [];

    // Traverse a[] and insert the even
    // and odd element respectively
    for (var x = 0; x < n; x++) {

        if (a[x] % 2 == 0)
            even.push(a[x]);
        else
            odd.push(a[x]);
    }

    // ei points to the next
    // available even element

    // oi points to the next
    // available odd element
    var ei = 0, oi = 0;

    // poss will store whether the
    // given transformation
    // of a[] to b[] is possible
    var poss = true;

    // Traverse b[]
    for (var x = 0; x < n; x++) {

        if (b[x] % 2 == 0) {

            // Check if both even
            // elements are equal
            if (ei < even.length
                && b[x] == even[ei]) {
                ei++;
            }
            else {
                poss = false;
                break;
            }
        }
        else {

            // Check if both odd
            // elements are equal
            if (oi < odd.length
                && b[x] == odd[oi]) {
                oi++;
            }
            else {
                poss = false;
                break;
            }
        }
    }

    // If poss is true, then we can
    // transform a[] to b[]
    if (poss)

        document.write( "Yes" );

    else

        document.write( "No" );
}

// Driver Code

// Given arrays
var arr1 = [0, 1, 13, 3, 4, 14, 6 ];
var arr2 = [0, 1, 14, 3, 4, 13, 6 ];
var N = arr1.length;

// Function Call
convert(arr1, arr2, N);

</script>
```

**Output:** 

```
No
```

**时间复杂度:** *O(N)* ，其中 N 为数组中元素的个数。
**辅助空间:** *O(N)* ，其中 N 为数组中的元素个数。