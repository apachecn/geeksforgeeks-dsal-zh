# 缩小数组，使每个元素最多出现 K 次

> 原文:[https://www . geesforgeks . org/reduce-the-array-so-每个元素最多出现 k 次/](https://www.geeksforgeeks.org/reduce-the-array-such-that-each-element-appears-at-most-k-times/)

给定一个大小为 **N** 的排序数组 **arr** ，任务是缩小数组，使每个元素最多出现 K 次。
**例:**

> **输入:** arr[] = {1，2，2，2，3}，K = 2
> **输出:** {1，2，2，3}
> **解释:**
> 去掉 2 一次，因为它出现 2 次以上。
> **输入:** arr[] = {3，3，3}，K = 1
> **输出:** {3}
> **解释:**
> 去掉 3 两次，因为它出现 1 次以上。

**进场:**

1.  遍历给定的数组 **arr**
2.  遍历时，使用指针 **i** 保持数组中每个唯一元素的[计数](https://www.geeksforgeeks.org/count-distinct-elements-in-an-array/)
3.  如果 arr[i]直到索引 I 的当前频率小于或等于 K，则将元素 arr[i]添加到新的简化数组中，并将频率增加 1。
4.  如果 arr[i]直到索引 I 的当前频率大于 K，跳过直到找到下一个唯一元素。
5.  遍历结束后，打印缩减的数组。

以下是上述方法的实现:

## C++

```
// C++ program to reduce the array
// such that each element appears
// at most K times

#include <bits/stdc++.h>
using namespace std;

// Function to reduce the array
void reduceArray(int arr[], int n, int K)
{
    // Vector to store the reduced array
    vector<int> vec;
    int size = 0;
    int curr_ele = arr[0], curr_freq = 1;

    // Iterate over the array
    for (int i = 0; i < n; i++) {

        if (curr_ele == arr[i]
            && curr_freq <= K) {
            vec.push_back(arr[i]);
            size++;
        }
        else if (curr_ele != arr[i]) {
            curr_ele = arr[i];
            vec.push_back(arr[i]);
            size++;
            curr_freq = 1;
        }
        curr_freq++;
    }

    // Print the reduced array
    cout << "{";
    for (int i = 0; i < size; i++) {
        cout << vec[i] << ", ";
    }
    cout << "}";
}

// Driver code
int main()
{
    int arr[]
        = { 1, 1, 1, 2,
            2, 2, 3, 3,
            3, 3, 3, 3,
            4, 5 };

    int n = sizeof(arr)
            / sizeof(arr[0]);
    int K = 2;

    // Function call
    reduceArray(arr, n, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reduce the array
// such that each element appears
// at most K times
import java.util.*;

class GFG{

// Function to reduce the array
static void reduceArray(int arr[], int n, int K)
{
    // Vector to store the reduced array
    Vector<Integer> vec = new Vector<Integer>();
    int size = 0;
    int curr_ele = arr[0], curr_freq = 1;

    // Iterate over the array
    for (int i = 0; i < n; i++) {

        if (curr_ele == arr[i]
            && curr_freq <= K) {
            vec.add(arr[i]);
            size++;
        }
        else if (curr_ele != arr[i]) {
            curr_ele = arr[i];
            vec.add(arr[i]);
            size++;
            curr_freq = 1;
        }
        curr_freq++;
    }

    // Print the reduced array
    System.out.print("{");
    for (int i = 0; i < size; i++) {
        System.out.print(vec.get(i)+ ", ");
    }
    System.out.print("}");
}

// Driver code
public static void main(String[] args)
{
    int arr[]
        = { 1, 1, 1, 2,
            2, 2, 3, 3,
            3, 3, 3, 3,
            4, 5 };

    int n = arr.length;
    int K = 2;

    // Function call
    reduceArray(arr, n, K);

}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to reduce the array
# such that each element appears
# at most K times

# Function to reduce the array
def reduceArray(arr, n, K) :

    # List to store the reduced array
    vec = [];
    size = 0;
    curr_ele = arr[0]; curr_freq = 1;

    # Iterate over the array
    for i in range(n) :

        if (curr_ele == arr[i]
            and curr_freq <= K) :
            vec.append(arr[i]);
            size += 1;

        elif (curr_ele != arr[i]) :
            curr_ele = arr[i];
            vec.append(arr[i]);
            size += 1;
            curr_freq = 1;

        curr_freq += 1;

    # Print the reduced array
    print("{",end= "");
    for i in range(size) :
        print(vec[i] ,end= ", ");

    print("}",end="");

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 1, 1, 2,
           2, 2, 3, 3,
            3, 3, 3, 3,
            4, 5 ];

    n = len(arr)
    K = 2;

    # Function call
    reduceArray(arr, n, K);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to reduce the array
// such that each element appears
// at most K times
using System;
using System.Collections.Generic;

class GFG{

// Function to reduce the array
static void reduceArray(int []arr, int n, int K)
{
    // List to store the reduced array
    List<int> vec = new List<int>();
    int size = 0;
    int curr_ele = arr[0], curr_freq = 1;

    // Iterate over the array
    for (int i = 0; i < n; i++) {

        if (curr_ele == arr[i]
            && curr_freq <= K) {
            vec.Add(arr[i]);
            size++;
        }
        else if (curr_ele != arr[i]) {
            curr_ele = arr[i];
            vec.Add(arr[i]);
            size++;
            curr_freq = 1;
        }
        curr_freq++;
    }

    // Print the reduced array
    Console.Write("{");
    for (int i = 0; i < size; i++) {
        Console.Write(vec[i]+ ", ");
    }
    Console.Write("}");
}

// Driver code
public static void Main(String[] args)
{
    int []arr
        = { 1, 1, 1, 2,
            2, 2, 3, 3,
            3, 3, 3, 3,
            4, 5 };

    int n = arr.Length;
    int K = 2;

    // Function call
    reduceArray(arr, n, K);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program to reduce the array
// such that each element appears
// at most K times

// Function to reduce the array
function reduceArray( arr, n,  K)
{
    // Vector to store the reduced array
    var vec=[];
    var size = 0;
    var curr_ele = arr[0], curr_freq = 1;

    // Iterate over the array
    for (var i = 0; i < n; i++) {

        if (curr_ele == arr[i]
            && curr_freq <= K) {
            vec.push(arr[i]);
            size++;
        }
        else if (curr_ele != arr[i]) {
            curr_ele = arr[i];
            vec.push(arr[i]);
            size++;
            curr_freq = 1;
        }
        curr_freq++;
    }

    // Print the reduced array
    document.write( "{");
    for (var i = 0; i < size; i++) {
        document.write( vec[i] +", ");
    }
    document.write("}");
}

var arr
        = [ 1, 1, 1, 2,
            2, 2, 3, 3,
            3, 3, 3, 3,
            4, 5 ];

    var n = 14;
    var K = 2;

    // Function call
    reduceArray(arr, n, K);

</script>
```

**Output:** 

```
{1, 1, 2, 2, 3, 3, 4, 5, }
```

***时间复杂度:** O(N)*
***空间复杂度:** O(1)*