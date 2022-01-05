# 桶排序

> 原文:[https://www.geeksforgeeks.org/bucket-sort-2/](https://www.geeksforgeeks.org/bucket-sort-2/)

当输入在一个范围内均匀分布时，桶排序主要是有用的。例如，考虑以下问题。
*对一大组 0.0-1.0 范围内的浮点数进行排序，这些浮点数在范围内均匀分布。我们如何有效地对数字进行排序？*
一个简单的方法是应用基于比较的排序算法。基于比较的排序算法的[下限](https://www.geeksforgeeks.org/lower-bound-on-comparison-based-sorting-algorithms/)(合并排序、堆排序、快速排序..etc)是ω(n Log n)，即它们不能比 n Log n 做得更好。
可以线性时间排序数组吗？[计数排序](https://www.geeksforgeeks.org/counting-sort/)在这里不能应用，因为我们在计数排序中使用键作为索引。这里的键是浮点数。
思路是用桶排序。下面是桶算法。

```
bucketSort(arr[], n)
1) Create n empty buckets (Or lists).
2) Do following for every array element arr[i].
.......a) Insert arr[i] into bucket[n*array[i]]
3) Sort individual buckets using insertion sort.
4) Concatenate all sorted buckets.
```

![BucketSort](img/e9b00b92408ba3e056a6ed4b6750264a.png)

**时间复杂度:**如果我们假设桶中的插入需要 O(1)个时间，那么上述算法的步骤 1 和 2 显然需要 O(n)个时间。如果我们使用链表来表示一个桶，那么 O(1)很容易实现(在下面的代码中，为了简单起见，使用了 C++向量)。步骤 4 也需要 O(n)个时间，因为所有存储桶中将有 n 个项目。
分析的主要步骤是第三步。如果所有的数字都是均匀分布的话，这一步平均也需要 O(n)个时间(详见 [CLRS 书](http://www.flipkart.com/introduction-algorithms-3rd/p/itmdvd93bzvrnc7b?pid=9788120340077&affid=sandeepgfg))
以下是上述算法的实现。

## C++

```
// C++ program to sort an
// array using bucket sort
#include <algorithm>
#include <iostream>
#include <vector>
using namespace std;

// Function to sort arr[] of
// size n using bucket sort
void bucketSort(float arr[], int n)
{

    // 1) Create n empty buckets
    vector<float> b[n];

    // 2) Put array elements
    // in different buckets
    for (int i = 0; i < n; i++) {
        int bi = n * arr[i]; // Index in bucket
        b[bi].push_back(arr[i]);
    }

    // 3) Sort individual buckets
    for (int i = 0; i < n; i++)
        sort(b[i].begin(), b[i].end());

    // 4) Concatenate all buckets into arr[]
    int index = 0;
    for (int i = 0; i < n; i++)
        for (int j = 0; j < b[i].size(); j++)
            arr[index++] = b[i][j];
}

/* Driver program to test above function */
int main()
{
    float arr[]
        = { 0.897, 0.565, 0.656, 0.1234, 0.665, 0.3434 };
    int n = sizeof(arr) / sizeof(arr[0]);
    bucketSort(arr, n);

    cout << "Sorted array is \n";
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort an array
// using bucket sort
import java.util.*;
import java.util.Collections;

class GFG {

    // Function to sort arr[] of size n
    // using bucket sort
    static void bucketSort(float arr[], int n)
    {
        if (n <= 0)
            return;

        // 1) Create n empty buckets
        @SuppressWarnings("unchecked")
        Vector<Float>[] buckets = new Vector[n];

        for (int i = 0; i < n; i++) {
            buckets[i] = new Vector<Float>();
        }

        // 2) Put array elements in different buckets
        for (int i = 0; i < n; i++) {
            float idx = arr[i] * n;
            buckets[(int)idx].add(arr[i]);
        }

        // 3) Sort individual buckets
        for (int i = 0; i < n; i++) {
            Collections.sort(buckets[i]);
        }

        // 4) Concatenate all buckets into arr[]
        int index = 0;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < buckets[i].size(); j++) {
                arr[index++] = buckets[i].get(j);
            }
        }
    }

    // Driver code
    public static void main(String args[])
    {
        float arr[] = { (float)0.897, (float)0.565,
                        (float)0.656, (float)0.1234,
                        (float)0.665, (float)0.3434 };

        int n = arr.length;
        bucketSort(arr, n);

        System.out.println("Sorted array is ");
        for (float el : arr) {
            System.out.print(el + " ");
        }
    }
}

// This code is contributed by Himangshu Shekhar Jha
```

## 蟒蛇 3

```
# Python3 program to sort an array
# using bucket sort
def insertionSort(b):
    for i in range(1, len(b)):
        up = b[i]
        j = i - 1
        while j >= 0 and b[j] > up:
            b[j + 1] = b[j]
            j -= 1
        b[j + 1] = up    
    return b    

def bucketSort(x):
    arr = []
    slot_num = 10 # 10 means 10 slots, each
                  # slot's size is 0.1
    for i in range(slot_num):
        arr.append([])

    # Put array elements in different buckets
    for j in x:
        index_b = int(slot_num * j)
        arr[index_b].append(j)

    # Sort individual buckets
    for i in range(slot_num):
        arr[i] = insertionSort(arr[i])

    # concatenate the result
    k = 0
    for i in range(slot_num):
        for j in range(len(arr[i])):
            x[k] = arr[i][j]
            k += 1
    return x

# Driver Code
x = [0.897, 0.565, 0.656,
     0.1234, 0.665, 0.3434]
print("Sorted Array is")
print(bucketSort(x))

# This code is contributed by
# Oneil Hsiao
```

## C#

```
// C# program to sort an array
// using bucket sort
using System;
using System.Collections;
using System.Collections.Generic;
class GFG {

  // Function to sort arr[] of size n
  // using bucket sort
  static void bucketSort(float []arr, int n)
  {
    if (n <= 0)
      return;

    // 1) Create n empty buckets
    List<float>[] buckets = new List<float>[n];

    for (int i = 0; i < n; i++) {
      buckets[i] = new List<float>();
    }

    // 2) Put array elements in different buckets
    for (int i = 0; i < n; i++) {
      float idx = arr[i] * n;
      buckets[(int)idx].Add(arr[i]);
    }

    // 3) Sort individual buckets
    for (int i = 0; i < n; i++) {
      buckets[i].Sort();
    }

    // 4) Concatenate all buckets into arr[]
    int index = 0;
    for (int i = 0; i < n; i++) {
      for (int j = 0; j < buckets[i].Count; j++) {
        arr[index++] = buckets[i][j];
      }
    }
  }

  // Driver code
  public static void Main()
  {
    float []arr = { (float)0.897, (float)0.565,
                   (float)0.656, (float)0.1234,
                   (float)0.665, (float)0.3434 };

    int n = arr.Length;
    bucketSort(arr, n);

    Console.WriteLine("Sorted array is ");
    foreach(float el in arr) {
      Console.Write(el + " ");
    }
  }
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// Javascript program to sort an array
// using bucket sort

// Function to sort arr[] of size n
// using bucket sort
function bucketSort(arr,n)
{
    if (n <= 0)
            return;

        // 1) Create n empty buckets      
        let buckets = new Array(n);

        for (let i = 0; i < n; i++)
        {
            buckets[i] = [];
        }

        // 2) Put array elements in different buckets
        for (let i = 0; i < n; i++) {
            let idx = arr[i] * n;
            buckets[Math.floor(idx)].push(arr[i]);
        }

        // 3) Sort individual buckets
        for (let i = 0; i < n; i++) {
            buckets[i].sort(function(a,b){return a-b;});
        }

        // 4) Concatenate all buckets into arr[]
        let index = 0;
        for (let i = 0; i < n; i++) {
            for (let j = 0; j < buckets[i].length; j++) {
                arr[index++] = buckets[i][j];
            }
        }
}

// Driver code
let arr = [0.897, 0.565,
         0.656, 0.1234,
         0.665, 0.3434];
let n = arr.length;
bucketSort(arr, n);

document.write("Sorted array is <br>");
for (let el of arr.values()) {
    document.write(el + " ");
}

// This code is contributed by unknown2108
</script>
```

**Output**

```
Sorted array is 
0.1234 0.3434 0.565 0.656 0.665 0.897 
```