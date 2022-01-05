# 重复删除 LIS 后的数组大小

> 原文:[https://www . geesforgeks . org/size-array-repeated-delete-lis/](https://www.geeksforgeeks.org/size-array-repeated-deletion-lis/)

给定数组 arr[0..正元素的 n-1]。任务是在重复删除 LIS(大小大于 1)后打印 arr[]的剩余元素。如果有多个长度相同的 LIS，我们需要选择最先结束的 LIS。
**例:**

```
Input : arr[] = {1, 2, 5, 3, 6, 4, 1}
Output : 1
Explanation : 
{1, 2, 5, 3, 6, 4, 1} - {1, 2, 5, 6} = {3, 4, 1}
{3, 4, 1} - {3, 4} = {1}

Input : arr[] = {1, 2, 3, 1, 5, 2}
Output : -1
Explanation : 
{1, 2, 3, 1, 5, 2} - {1, 2, 3, 5} = {1, 2}
{1, 2} - {1, 2} = {}

Input : arr[] = {5, 3, 2}
Output : 3
```

我们反复寻找 LIS 并从数组中移除它的元素。

```
// input vector array = arr[]
// max-sum LIS vector array = maxArray[]
while (arr.size())
{
    // find LIS 
    lis = findLIS(arr, arr.size());
    if (lis.size() < 2)
        break;

    // Remove lis elements from current array. Note
    // that both lis[] and arr[] are sorted in
    // increasing order.
    for (i=0; i<arr.size() && lis.size()>0; i++)
    {
        if (arr[i] == lis[0])
        {            
            // Remove lis element from arr[]
            arr.erase(arr.begin()+i) ;
            i--;

            // erase the element from lis[]. This is
            // needed to make sure that next element
            // to be removed is first element of lis[]
            lis.erase(lis.begin()) ;          
        }
    }
}
// print remaining element of array
for (i=0; i<arr.size(); i++)
    cout  << arr[i] << " ";
if (i == 0)
    cout << "-1";
```

## C++

```
/* C++ program to find size of array after repeated
  deletion of LIS */
#include <bits/stdc++.h>
using namespace std;

// Function to construct Maximum Sum LIS
vector<int> findLIS(vector<int> arr, int n)
{
    // L[i] - The Maximum Sum Increasing
    // Subsequence that ends with arr[i]
    vector <vector<int> > L(n);

    // L[0] is equal to arr[0]
    L[0].push_back(arr[0]);

    // start from index 1
    for (int i = 1; i < n; i++)
    {
        // for every j less than i
        for (int j = 0; j < i; j++)
        {
            /* L[i] = {MaxSum(L[j])} + arr[i]
            where j < i and arr[j] < arr[i] */
            if (arr[i] > arr[j] && (L[i].size() < L[j].size()))
                L[i] = L[j];
        }

        // L[i] ends with arr[i]
        L[i].push_back(arr[i]);
    }

    // set lis =  LIS
    // whose size is max among all
    int maxSize = 1;
    vector<int> lis;
    for (vector<int> x : L)
    {
        // The > sign makes sure that the LIS
        // ending first is chose.   
        if (x.size() > maxSize)
        {
            lis = x;
            maxSize = x.size();
        }
    }

    return lis;
}

// Function to minimize array
void minimize(int input[], int n)
{
    vector<int> arr(input, input + n);

    while (arr.size())
    {
        // Find LIS of current array
        vector<int> lis = findLIS(arr, arr.size());

        // If all elements are in decreasing order
        if (lis.size() < 2)
            break;

        // Remove lis elements from current array. Note
        // that both lis[] and arr[] are sorted in
        // increasing order.
        for (int i=0; i<arr.size() && lis.size()>0; i++)
        {
            // If first element of lis[] is found
            if (arr[i] == lis[0])
            {
                // Remove lis element from arr[]
                arr.erase(arr.begin()+i) ;
                i--;

                // Erase first element of lis[]
                lis.erase(lis.begin()) ;
            }
        }
    }

    // print remaining element of array
    int i;
    for (i=0; i < arr.size(); i++)
        cout  << arr[i] << " ";

    // print -1 for empty array
    if (i == 0)
        cout << "-1";
}

// Driver function
int main()
{
    int input[] = { 3, 2, 6, 4, 5, 1 };
    int n = sizeof(input) / sizeof(input[0]);

    // minimize array after deleting LIS
    minimize(input, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find size
//  of array after repeated
// deletion of LIS
import java.util.*;
class GFG{

// Function to conMaximum Sum LIS
static Vector<Integer> findLIS(Vector<Integer> arr,
                               int n)
{
  // L[i] - The Maximum Sum Increasing
  // Subsequence that ends with arr[i]
  Vector<Integer> []L = new Vector[n];

  for (int i = 0; i < L.length; i++)
    L[i] = new Vector<Integer>();

  // L[0] is equal to arr[0]
  L[0].add(arr.elementAt(0));

  // Start from index 1
  for (int i = 1; i < n; i++)
  {
    // For every j less than i
    for (int j = 0; j < i; j++)
    {
      // L[i] = {MaxSum(L[j])} + arr[i]
      // where j < i and arr[j] < arr[i]
      if (arr.elementAt(i) > arr.elementAt(j) &&
          (L[i].size() < L[j].size()))
        L[i] = L[j];
    }

    // L[i] ends with arr[i]
    L[i].add(arr.elementAt(i));
  }

  // Set lis =  LIS
  // whose size is max among all
  int maxSize = 1;
  Vector<Integer> lis = new Vector<>();

  for (Vector<Integer> x : L)
  {
    // The > sign makes sure that the LIS
    // ending first is chose.   
    if (x.size() > maxSize)
    {
      lis = x;
      maxSize = x.size();
    }
  }
  return lis;
}

// Function to minimize array
static void minimize(int input[],
                     int n)
{
  Vector<Integer> arr = new Vector<>();
  for(int i = 0; i < n; i++)
    arr.add(input[i]);

  while (arr.size() != 0)
  {
    // Find LIS of current array
    Vector<Integer> lis = findLIS(arr,
                                  arr.size());

    // If all elements are
    // in decreasing order
    if (lis.size() < 2)
      break;

    // Remove lis elements from
    // current array. Note that both
    // lis[] and arr[] are sorted in
    // increasing order.
    for (int i = 0; i < arr.size() &&
             lis.size() > 0; i++)
    {
      // If first element of lis[] is found
      if (arr.elementAt(i) == lis.elementAt(0))
      {
        // Remove lis element from arr[]
        arr.removeAll(lis);
        i--;

        // Erase first element of lis[]
        lis.remove(0);
      }
    }
  }

  // print remaining element of array
  int i;
  for (i = 1; i < arr.size(); i++)
    System.out.print(arr.elementAt(i) + " ");

  // print -1 for empty array
  if (i == 0)
    System.out.print("-1");
}

// Driver function
public static void main(String[] args)
{
  int input[] = {3, 2, 6, 4, 5, 1};
  int n = input.length;

  // minimize array after deleting LIS
  minimize(input, n);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
''' Python program to find size of array after repeated
  deletion of LIS '''

# Function to construct Maximum Sum LIS
from typing import List

def findLIS(arr: List[int], n: int) -> List[int]:

    # L[i] - The Maximum Sum Increasing
    # Subsequence that ends with arr[i]
    L = [0] * n
    for i in range(n):
        L[i] = []

    # L[0] is equal to arr[0]
    L[0].append(arr[0])

    # start from index 1
    for i in range(1, n):

        # for every j less than i
        for j in range(i):

            ''' L[i] = MaxSum(L[j]) + arr[i]
            where j < i and arr[j] < arr[i] '''
            if (arr[i] > arr[j] and
                (len(L[i]) < len(L[j]))):
                L[i] = L[j].copy()

        # L[i] ends with arr[i]
        L[i].append(arr[i])

    # set lis =  LIS
    # whose size is max among all
    maxSize = 1
    lis: List[int] = []
    for x in L:

        # The > sign makes sure that the LIS
        # ending first is chose.
        if (len(x) > maxSize):

            lis = x.copy()
            maxSize = len(x)

    return lis

# Function to minimize array
def minimize(input: List[int], n: int) -> None:

    arr = input.copy()

    while len(arr):

        # Find LIS of current array
        lis = findLIS(arr, len(arr))

        # If all elements are in decreasing order
        if (len(lis) < 2):
            break

        # Remove lis elements from current array. Note
        # that both lis[] and arr[] are sorted in
        # increasing order.
        i = 0
        while i < len(arr) and len(lis) > 0:

            # If first element of lis[] is found
            if (arr[i] == lis[0]):

                # Remove lis element from arr[]
                arr.remove(arr[i])
                i -= 1

                # Erase first element of lis[]
                lis.remove(lis[0])
            i += 1

    # print remaining element of array
    i = 0
    while i < len(arr):
        print(arr[i], end=" ")
        i += 1

    # print -1 for empty array
    if (i == 0):
        print("-1")

# Driver function
if __name__ == "__main__":

    input = [3, 2, 6, 4, 5, 1]
    n = len(input)

    # minimize array after deleting LIS
    minimize(input, n)

# This code is contributed by sanjeev2552
```

**输出:**

```
1
```

本文由[**Shivam Pradhan(anuj _ charm)**](https://www.facebook.com/anuj.charm)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。