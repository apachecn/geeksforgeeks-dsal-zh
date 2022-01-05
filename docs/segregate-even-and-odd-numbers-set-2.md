# 隔离偶数和奇数|设置 2

> 原文:[https://www . geesforgeks . org/separate-偶数和奇数-set-2/](https://www.geeksforgeeks.org/segregate-even-and-odd-numbers-set-2/)

给定一个大小为 **N** 的[阵](https://www.geeksforgeeks.org/introduction-to-arrays/) **阵**，任务是隔离偶数和奇数。先打印所有偶数，然后打印奇数。

**示例:**

> **输入:** arr[] = {8，22，65，70，33，60，2，34，43，21}
> **输出:** {8，22，70，60，2，34，65，33，43，21}
> 
> **输入:** arr[] = {18，52，37，70，3，63，2，34}
> **输出:** {18，52，70，2，34，37，3，63}

**线性逼近:**这个问题可以看作是[荷兰国旗问题](https://www.geeksforgeeks.org/sort-an-array-of-0s-1s-and-2s/)的变种。关于解决问题的所有线性方法，请参考[上一篇文章](https://www.geeksforgeeks.org/segregate-even-and-odd-numbers/)。

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**使用**[**stable _ partition()**](https://www.geeksforgeeks.org/stdstable_partition-in-c/)**函数的方法:****stable _ partition()**算法排列由**开始**和**结束**定义的序列，使得由用户定义的谓词函数指定的谓词返回 **True** 的所有元素都在函数返回 **False** 的元素之前。分区是稳定的。因此，序列的相对顺序得以保留。

**语法:**

> 模板
> BiIter 稳定 _ 分区(BiIter 开始，BiIter 结束，UnPred pfn)

**参数:**

> **开始:**要重新排序的元素范围
> **结束:**要重新排序的元素范围
> **pfn:** 用户定义的谓词函数对象，它定义了要对元素进行分类时要满足的条件。
> 谓词接受单个参数并返回**真**或**假**。
> **返回值:**向谓词为假的元素的开头返回一个迭代器。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to segregate
// odd and even numbers
void segregate(vector<int> arr)
{

    // Using stable partition
    // with lambda expression
    stable_partition(arr.begin(),
                     arr.end(),
                     [](int a) {
                         return a % 2 == 0;
                     });

    // Print array after partition
    for (int num : arr)
        cout << num << " ";
}

// Driver Code
int main()
{
    // Given array arr[]
    vector<int> arr = { 18, 52, 37, 70,
                        3, 63, 2, 34 };

    // Function Call
    segregate(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

static int[] stable_partition(int arr[])
{
  // Initialize left and
  // right indexes
  int left = 0,
      right = arr.length - 1;

  while (left < right)
  {
    // Increment left index while
    // we see 0 at left
    while (arr[left] % 2 == 0 &&
           left < right)
      left++;

    // Decrement right index while
    // we see 1 at right
    while (arr[right] % 2 == 1 &&
           left < right)
      right--;

    if (left < right)
    {
      // Swap arr[left] and
      // arr[right]
      int temp = arr[left];
      arr[left] = arr[right];
      arr[right] = temp;
      left++;
      right--;
    }
  }
  return arr;
}

// Function to segregate
// odd and even numbers
static void segregate(int[] arr)
{
  // Using stable partition
  // with lambda expression
  int []ans = stable_partition(arr);

  // Print array after partition
  for (int num : ans)
    System.out.print(num + " ");
}

// Driver Code
public static void main(String[] args)
{
  // Given array arr[]
  int[] arr = {18, 52, 37, 70,
               3, 63, 2, 34};

  // Function Call
  segregate(arr);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to segregate
# odd and even numbers
def segregate(arr):

    # Using stable partition
    # with lambda expression
    odd = []
    even = []

    for x in arr:
        if (x % 2 == 0):
            even.append(x)
        else:
            odd.append(x)

    for x in even:
        print(x, end = " ")
    for x in odd:
        print(x, end = " ")

# Driver Code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 18, 52, 37, 70, 3, 63, 2, 34 ]

    # Function Call
    segregate(arr)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG{

static void stable_partition(int []arr)
{
  // Initialize left and
  // right indexes
  List<int> odd = new List<int>();
  List<int> even = new List<int>();

  foreach(int i in arr)
  {
    if(i % 2 == 1)
      odd.Add(i);
    else
      even.Add(i);
  }

  foreach(int i in even)
    Console.Write(i +" ");

  foreach(int i in odd)
    Console.Write(i +" ");
}

// Function to segregate
// odd and even numbers
static void segregate(int[] arr)
{
  // Using stable partition
  // with lambda expression
  stable_partition(arr);

}

// Driver Code
public static void Main(String[] args)
{
  // Given array []arr
  int[] arr = {18, 52, 37, 70,
               3, 63, 2, 34};

  // Function Call
  segregate(arr);
}
}

// This code is contributed by 29AjayKumar
```

**Output**

```
18 52 70 2 34 37 3 63 
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)