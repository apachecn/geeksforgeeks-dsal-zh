# 根据数组的模值及其频率对数组进行排序

> 原文:[https://www . geeksforgeeks . org/sort-array-根据它们的值与它们的频率的模/](https://www.geeksforgeeks.org/sort-array-according-to-modulus-of-their-values-with-their-frequencies/)

给定一个包含正整数 **N** 的数组 **arr** ，根据它们的值随频率的增加而增加的模对它们进行排序。

**示例:**

> **输入:** arr[]={1，1，5，3，2，3，3，4，5，4，5}
> **输出:**2 4 1 4 1 5 5 3 3 3
> **解释:**
> 元素按以下顺序排序:
> 2 %频率(2) = 2 % 1 = 0
> 4 %频率(4) = 4 % 2 = 0
> 1 %频率(1) = 1 % 2
> 
> **输入:** arr[]={2，9，8，2，8，9，2，8，5}
> **输出:**5 9 2 8 8 8

**方法:**要解决这个问题，将每个数字的频率存储在地图中，然后创建一个自定义的比较器，它将进行排序。该比较函数将接受两个整数值，比如说 **A** 和 **B** 作为参数，该比较器对数组进行排序的条件是:

> **(A %频率(A)) > (B %频率(B))**

下面是上述方法的实现。

## C++

```
// C++ code for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to sort the numbers in an array
// according to the modulus of their values
// with their frequencies
void customSort(vector<int>& arr)
{

    // Map to store
    // the frequencies of each number
    unordered_map<int, int> freq;
    for (auto x : arr) {
        freq[x]++;
    }

    // Sorting them using
    // a custom comparator
    sort(arr.begin(), arr.end(),
         [&](int A, int B) {
             if (A % freq[A] == B % freq[B]) {
                 return A < B;
             }
             return A % freq[A] < B % freq[B];
         });

    // Printing the numbers
    for (auto x : arr) {
        cout << x << ' ';
    }
}

// Driver Code
int main()
{
    vector<int> arr = { 2, 9, 8, 2, 8,
                        9, 2, 8, 5 };
    customSort(arr);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.*;

class GFG{

// Function to sort the numbers in an array
// according to the modulus of their values
// with their frequencies
static void customSort(Integer []arr)
{

    // Map to store
    // the frequencies of each number
    HashMap<Integer,Integer> freq = new HashMap<Integer,Integer>();
    for (int x : arr) {
        if(freq.containsKey(x)){
            freq.put(x, freq.get(x)+1);
        }
        else{
            freq.put(x, 1);
        }
    }

    // Sorting them using
    // a custom comparator
    Arrays.sort(arr, new Comparator<Integer>(){

        @Override
        public int compare(Integer a, Integer b)
        {
            // If both are odd or even
            // then sorting in increasing order
            if ((a % freq.get(a)) == (b % freq.get(b))) {
                return a < b?-1:1;
            }

            // Sorting on the basis of last bit if
            // if one is odd and the other one is even
            return ((a % freq.get(a)) < (b % freq.get(b)))?-1:1;
        }

    });
    // Printing the numbers
    for (int x : arr) {
        System.out.print(x +" ");
    }
}

// Driver Code
public static void main(String[] args)
{
    Integer []arr = { 2, 9, 8, 2, 8,
                        9, 2, 8, 5 };
    customSort(arr);
}
}

// This code is contributed by 29AjayKumar
```

## C#

```
// C# code for the above approach

using System;
using System.Collections.Generic;

class GFG
{

    // Function to sort the numbers in an array
    // according to the modulus of their values
    // with their frequencies
    static void customSort(int[] arr)
    {

        // Map to store
        // the frequencies of each number
        Dictionary<int, int> freq = new Dictionary<int, int>();
        foreach (int x in arr)
        {
            if (freq.ContainsKey(x))
            {
                freq[x] += 1;
            }
            else
            {
                freq[x] = 1;
            }
        }

        // Sorting them using
        // a custom comparator
        Array.Sort(arr, (a, b)
             =>
        {
            // If both are odd or even
            // then sorting in increasing order
            if ((a % freq[a]) == (b % freq[b]))
            {
                return a < b ? -1 : 1;
            }

            // Sorting on the basis of last bit if
            // if one is odd and the other one is even
            return ((a % freq[a]) < (b % freq[b])) ? -1 : 1;
        });
        // Printing the numbers

        foreach (int x in arr)
        {
            Console.Write(x + " ");
        }
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 2, 9, 8, 2, 8,
                        9, 2, 8, 5 };
        customSort(arr);
    }
}

// This code is contributed by Saurabh Jaiswal
```

## java 描述语言

```
<script>
// Javascript code for the above approach

// Function to sort the numbers in an array
// according to the modulus of their values
// with their frequencies
function customSort(arr) {

    // Map to store
    // the frequencies of each number
    let freq = new Map();
    for (x of arr) {
        if (freq.has(x)) {
            freq.set(x, freq.get(x) + 1)
        } else {
            freq.set(x, 1)
        }
    }

    freq = new Map([...freq].sort((a, b) => a[0] - b[0]));

    // Sorting them using
    // a custom comparator
    arr.sort((A, B) => {
        if (A % freq.get(A) == B % freq.get(B)) {
            return A - B;
        }

        return ((A % freq.get(A)) - (B % freq.get(B)));
    });

    // Printing the numbers
    for (x of arr) {
        document.write(x + ' ');
    }
}

// Driver Code
let arr = [2, 9, 8, 2, 8, 9, 2, 8, 5];
customSort(arr);

// This code is contributed by gfgking.
</script>
```

**Output**

```
5 9 9 2 2 2 8 8 8 
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)