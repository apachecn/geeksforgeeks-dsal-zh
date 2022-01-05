# 桶排序对负数数组进行排序

> 原文:[https://www . geeksforgeeks . org/bucket-sort-to-sort-a-array-with-negative-numbers/](https://www.geeksforgeeks.org/bucket-sort-to-sort-an-array-with-negative-numbers/)

我们已经在[桶排序](https://www.geeksforgeeks.org/bucket-sort-2/)的主帖子中讨论了桶排序。
桶排序主要用于输入在一定范围内均匀分布的情况。例如，考虑对一大组浮点数进行排序的问题，这些浮点数在 0.0 到 1.0 的范围内，并且在整个范围内均匀分布。在上面的文章中，我们讨论了桶排序来对大于零的数字进行排序。
**如何修改 Bucket Sort 同时对正数和负数进行排序？**
例:

```
Input : arr[] = { -0.897, 0.565, 0.656, -0.1234, 0, 0.3434 } 
Output : -0.897 -0.1234  0 0.3434 0.565 0.656 
```

这里我们考虑的数字范围是-1.0 到 1.0(浮点数)
算法:

```
sortMixed(arr[], n)
1) Split array into two parts 
   create two Empty vector Neg[], Pos[] 
   (for negative and positive element respectively)
   Store all negative element in Neg[] by converting
   into positive (Neg[i] = -1 * Arr[i] )
   Store all +ve in pos[]  (pos[i] =  Arr[i])
2) Call function bucketSortPositive(Pos, pos.size())
   Call function bucketSortPositive(Neg, Neg.size())

bucketSortPositive(arr[], n)
3) Create n empty buckets (Or lists).
4) Do following for every array element arr[i]. 
       a) Insert arr[i] into bucket[n*array[i]]
5) Sort individual buckets using insertion sort.
6) Concatenate all sorted buckets. 
```

以下是上述想法的实现(对于浮点数)

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to sort an array of positive
// and negative numbers using bucket sort
#include <bits/stdc++.h>
using namespace std;

// Function to sort arr[] of size n using
// bucket sort
void bucketSort(vector<float> &arr, int n)
{
    // 1) Create n empty buckets
    vector<float> b[n];

    // 2) Put array elements in different
    //    buckets
    for (int i=0; i<n; i++)
    {
        int bi = n*arr[i]; // Index in bucket
        b[bi].push_back(arr[i]);
    }

    // 3) Sort individual buckets
    for (int i=0; i<n; i++)
        sort(b[i].begin(), b[i].end());

    // 4) Concatenate all buckets into arr[]
    int index = 0;
    arr.clear();
    for (int i = 0; i < n; i++)
        for (int j = 0; j < b[i].size(); j++)
            arr.push_back(b[i][j]);
}

// This function mainly splits array into two
// and then calls bucketSort() for two arrays.
void sortMixed(float arr[], int n)
{
    vector<float>Neg ;
    vector<float>Pos;

    // traverse array elements
    for (int i=0; i<n; i++)
    {
        if (arr[i] < 0)

            // store -Ve elements by
            // converting into +ve element
            Neg.push_back (-1 * arr[i]) ;
        else
            // store +ve elements
            Pos.push_back (arr[i]) ;
    }

    bucketSort(Neg, (int)Neg.size());
    bucketSort(Pos, (int)Pos.size());

    // First store elements of Neg[] array
    // by converting into -ve
    for (int i=0; i < Neg.size(); i++)
        arr[i] = -1 * Neg[ Neg.size() -1 - i];

    // store +ve element
    for(int j=Neg.size(); j < n; j++)
        arr[j] = Pos[j - Neg.size()];
}

/* Driver program to test above function */
int main()
{
    float arr[] = {-0.897, 0.565, 0.656,
                   -0.1234, 0, 0.3434};
    int n = sizeof(arr)/sizeof(arr[0]);
    sortMixed(arr, n);

    cout << "Sorted array is \n";
    for (int i=0; i<n; i++)
        cout << arr[i] << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort an array of positive
// and negative numbers using bucket sort
import java.util.*;
class GFG
{

  // Function to sort arr[] of size n using
  // bucket sort
  static void bucketSort(Vector<Double> arr, int n)
  {

    // 1) Create n empty buckets
    @SuppressWarnings("unchecked")
    Vector<Double> b[] = new Vector[n];
    for (int i = 0; i < b.length; i++)
      b[i] = new Vector<Double>();

    // 2) Put array elements in different
    // buckets
    for (int i = 0; i < n; i++)
    {
      int bi = (int)(n*arr.get(i)); // Index in bucket
      b[bi].add(arr.get(i));
    }

    // 3) Sort individual buckets
    for (int i = 0; i < n; i++)
      Collections.sort(b[i]);

    // 4) Concatenate all buckets into arr[]
    int index = 0;
    arr.clear();
    for (int i = 0; i < n; i++)
      for (int j = 0; j < b[i].size(); j++)
        arr.add(b[i].get(j));
  }

  // This function mainly splits array into two
  // and then calls bucketSort() for two arrays.
  static void sortMixed(double arr[], int n)
  {
    Vector<Double>Neg = new Vector<>();
    Vector<Double>Pos = new Vector<>(); 

    // traverse array elements
    for (int i = 0; i < n; i++)
    {
      if (arr[i] < 0)

        // store -Ve elements by
        // converting into +ve element
        Neg.add (-1 * arr[i]) ;
      else

        // store +ve elements
        Pos.add (arr[i]) ;
    }
    bucketSort(Neg, (int)Neg.size());
    bucketSort(Pos, (int)Pos.size());

    // First store elements of Neg[] array
    // by converting into -ve
    for (int i = 0; i < Neg.size(); i++)
      arr[i] = -1 * Neg.get( Neg.size() -1 - i);

    // store +ve element
    for(int j = Neg.size(); j < n; j++)
      arr[j] = Pos.get(j - Neg.size());
  }

  /* Driver program to test above function */
  public static void main(String[] args)
  {
    double arr[] = {-0.897, 0.565, 0.656,
                    -0.1234, 0, 0.3434};
    int n = arr.length;
    sortMixed(arr, n);

    System.out.print("Sorted array is \n");
    for (int i = 0; i < n; i++)
      System.out.print(arr[i] + " ");
  }
}

// This code is contributed by Rajput-Ji
```

## C#

```
// C# program to sort an array of positive
// and negative numbers using bucket sort
using System;
using System.Collections.Generic;

public class GFG
{

  // Function to sort []arr of size n using
  // bucket sort
  static void bucketSort(List<Double> arr, int n)
  {

    // 1) Create n empty buckets

    List<Double> []b = new List<Double>[n];
    for (int i = 0; i < b.Length; i++)
      b[i] = new List<Double>();

    // 2) Put array elements in different
    // buckets
    for (int i = 0; i < n; i++)
    {
      int bi = (int)(n*arr[i]); // Index in bucket
      b[bi].Add(arr[i]);
    }

    // 3) Sort individual buckets
    for (int i = 0; i < n; i++)
      b[i].Sort();

    // 4) Concatenate all buckets into []arr
    int index = 0;
    arr.Clear();
    for (int i = 0; i < n; i++)
      for (int j = 0; j < b[i].Count; j++)
        arr.Add(b[i][j]);
  }

  // This function mainly splits array into two
  // and then calls bucketSort() for two arrays.
  static void sortMixed(double []arr, int n)
  {
    List<Double>Neg = new List<Double>();
    List<Double>Pos = new List<Double>(); 

    // traverse array elements
    for (int i = 0; i < n; i++)
    {
      if (arr[i] < 0)

        // store -Ve elements by
        // converting into +ve element
        Neg.Add (-1 * arr[i]) ;
      else

        // store +ve elements
        Pos.Add (arr[i]) ;
    }
    bucketSort(Neg, (int)Neg.Count);
    bucketSort(Pos, (int)Pos.Count);

    // First store elements of Neg[] array
    // by converting into -ve
    for (int i = 0; i < Neg.Count; i++)
      arr[i] = -1 * Neg[ Neg.Count -1 - i];

    // store +ve element
    for(int j = Neg.Count; j < n; j++)
      arr[j] = Pos[j - Neg.Count];
  }

  /* Driver program to test above function */
  public static void Main(String[] args)
  {
    double []arr = {-0.897, 0.565, 0.656,
                    -0.1234, 0, 0.3434};
    int n = arr.Length;
    sortMixed(arr, n);

    Console.Write("Sorted array is \n");
    for (int i = 0; i < n; i++)
      Console.Write(arr[i] + " ");
  }
}

// This code is contributed by Rajput-Ji
```

输出:

```
Sorted array is 
-0.897  -0.1234 0 0.3434 0.565 0.656 
```

本文由 [**尼尚·辛格**](https://practice.geeksforgeeks.org/user-profile.php?user=_code) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。