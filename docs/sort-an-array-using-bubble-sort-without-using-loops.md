# 使用冒泡排序对数组进行排序，不使用循环

> 原文:[https://www . geesforgeks . org/sort-a-array-use-bubble-sort-not-use-loops/](https://www.geeksforgeeks.org/sort-an-array-using-bubble-sort-without-using-loops/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是使用[冒泡排序](https://www.geeksforgeeks.org/bubble-sort/)对给定数组进行排序，而不使用[循环](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)。

**示例:**

> **输入:** arr[] = {1，3，4，2，5}
> **输出:** 1 2 3 4 5
> 
> **输入:** arr[] = {1，3，4，2}
> **输出:** 1 2 3 4

**方法:**在不使用循环的情况下实现[冒泡排序](https://www.geeksforgeeks.org/bubble-sort/)的想法基于以下观察:

*   [冒泡排序](https://www.geeksforgeeks.org/bubble-sort/)的排序算法执行如下步骤:
    *   外环[遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**(N–1)**次。
    *   内环[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，如果**arr【I】>arr【I+1】**，对于范围**【0，N–1】**内的每一个 **i** ，交换两个相邻的元素。
*   可以观察到，在每一次**N–1**迭代中，范围**【0，N–1–I】**上的[最大元素在范围**【0，N–1】**上每一次 **i** 移动到位置**(N–1–I)**。](https://www.geeksforgeeks.org/maximum-occurred-integer-n-ranges/)
*   因此，想法是使用[递归](https://www.geeksforgeeks.org/recursion/)来避免循环。

按照以下步骤解决问题:

*   考虑以下基本情况:
    *   如果数组包含单个元素，只需打印该数组。
    *   如果数组包含两个元素，交换这一对元素(如果需要)以获得数组元素的排序序列。打印排序后的数组。
*   将当前数组的前两个元素存储在变量中，比如 **a** 和 **b** 。
*   初始化一个数组，比如 **bs[]** ，来存储剩余的数组元素。
*   将 **a** 和 **b** 中较小的值放在当前数组的前面。
*   递归地重复上述步骤，在 **a** 和 **b** 中较大值的末尾添加**bs【】**形成一个新数组。
*   将返回的排序列表存储在一个变量中，比如 **res[]** 。
*   现在，递归地用一个新数组重复上述步骤，该数组是通过在 RES[RES . size()–1](最后一个元素)的末尾追加 **res[]** (不包括最后一个元素)而形成的。
*   完成以上步骤后，[打印返回列表](https://www.geeksforgeeks.org/print-lists-in-python-4-different-ways/)。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to implement bubble
// sort without using loops
vector<int> bubble_sort(vector<int> ar)
{

  // Base Case: If array
  // contains a single element
  if (ar.size() <= 1)
    return ar;

  // Base Case: If array
  // contains two elements
  if (ar.size() == 2){
    if(ar[0] < ar[1])
      return ar;
    else
      return {ar[1], ar[0]};
  }

  // Store the first two elements
  // of the list in variables a and b
  int a = ar[0];
  int b = ar[1];

  // Store remaining elements
  // in the list bs
  vector<int> bs;
  for(int i = 2; i < ar.size(); i++)
    bs.push_back(ar[i]);

  // Store the list after
  // each recursive call
  vector<int> res;

  // If a < b
  if (a < b){
    vector<int> temp1;
    temp1.push_back(b);
    for(int i = 0; i < bs.size(); i++)
      temp1.push_back(bs[i]);
    vector<int> v = bubble_sort(temp1);
    v.insert(v.begin(), a);
    res = v;
  }

  // Otherwise, if b >= a
  else{
    vector<int> temp1;
    temp1.push_back(a);
    for(int i = 0; i < bs.size(); i++)
      temp1.push_back(bs[i]);
    vector<int> v = bubble_sort(temp1);
    v.insert(v.begin(), b);
    res = v;
  }

  // Recursively call for the list
  // less than the last element and
  // and return the newly formed list
  vector<int> pass;
  for(int i = 0; i < res.size() - 1; i++)
    pass.push_back(res[i]);

  vector<int> ans = bubble_sort(pass);
  ans.push_back(res[res.size() - 1]);
  return ans;

}

// Driver Code
int main()
{

  vector<int> arr{1, 3, 4, 5, 6, 2};
  vector<int> res = bubble_sort(arr);

  // Print the array
  for(int i = 0; i < res.size(); i++)
    cout << res[i] << " ";
}

// This code is contributed by ipg2016107.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {

  // Function to implement bubble
  // sort without using loops
  static ArrayList<Integer> bubble_sort(ArrayList<Integer> ar)
  {

    // Base Case: If array
    // contains a single element
    if (ar.size() <= 1)
      return ar;

    // Base Case: If array
    // contains two elements
    if (ar.size() == 2) {
      if (ar.get(0) < ar.get(1))
        return ar;
      else
        return new ArrayList<Integer>(
        Arrays.asList(ar.get(1), ar.get(0)));
    }

    // Store the first two elements
    // of the list in variables a and b
    int a = ar.get(0);
    int b = ar.get(1);

    // Store remaining elements
    // in the list bs
    ArrayList<Integer> bs = new ArrayList<>();
    for (int i = 2; i < ar.size(); i++)
      bs.add(ar.get(i));

    // Store the list after
    // each recursive call
    ArrayList<Integer> res = new ArrayList<>();

    // If a < b
    if (a < b) {
      ArrayList<Integer> temp1 = new ArrayList<>();
      temp1.add(b);
      for (int i = 0; i < bs.size(); i++)
        temp1.add(bs.get(i));

      ArrayList<Integer> v = bubble_sort(temp1);
      v.add(0, a);
      res = v;
    }

    // Otherwise, if b >= a
    else {
      ArrayList<Integer> temp1 = new ArrayList<>();
      temp1.add(a);
      for (int i = 0; i < bs.size(); i++)
        temp1.add(bs.get(i));

      ArrayList<Integer> v = bubble_sort(temp1);
      v.add(0, b);
      res = v;
    }

    // Recursively call for the list
    // less than the last element and
    // and return the newly formed list
    ArrayList<Integer> pass = new ArrayList<>();
    for (int i = 0; i < res.size() - 1; i++)
      pass.add(res.get(i));

    ArrayList<Integer> ans = bubble_sort(pass);
    ans.add(res.get(res.size() - 1));
    return ans;
  }

  // Driver Code
  public static void main(String[] args)
  {

    ArrayList<Integer> arr = new ArrayList<Integer>(
      Arrays.asList(1, 3, 4, 5, 6, 2));
    ArrayList<Integer> res = bubble_sort(arr);

    // Print the array
    for (int i = 0; i < res.size(); i++)
      System.out.print(res.get(i) + " ");
  }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to implement bubble
# sort without using loops
def bubble_sort(ar):

    # Base Case: If array
    # contains a single element
    if len(ar) <= 1:
        return ar

    # Base Case: If array
    # contains two elements
    if len(ar) == 2:
        return ar if ar[0] < ar[1] else [ar[1], ar[0]]

    # Store the first two elements
    # of the list in variables a and b
    a, b = ar[0], ar[1]

    # Store remaining elements
    # in the list bs
    bs = ar[2:]

    # Store the list after
    # each recursive call
    res = []

    # If a < b
    if a < b:
        res = [a] + bubble_sort([b] + bs)

    # Otherwise, if b >= a
    else:
        res = [b] + bubble_sort([a] + bs)

    # Recursively call for the list
    # less than the last element and
    # and return the newly formed list
    return bubble_sort(res[:-1]) + res[-1:]

# Driver Code

arr = [1, 3, 4, 5, 6, 2]
res = bubble_sort(arr)

# Print the array
print(*res)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to implement bubble
// sort without using loops
static List<int> bubble_sort(List<int> ar)
{

    // Base Case: If array
    // contains a single element
    List<int> temp = new List<int>();

    if (ar.Count <= 1)
        return ar;

    // Base Case: If array
    // contains two elements
    if (ar.Count == 2)
    {
        if (ar[0] < ar[1])
            return ar;
        else
        {
            temp.Add(ar[1]);
            temp.Add(ar[0]);
            return temp;
        }
    }

    // Store the first two elements
    // of the list in variables a and b
    int a = ar[0];
    int b = ar[1];

    // Store remaining elements
    // in the list bs
    List<int> bs = new List<int>();
    for(int i = 2; i < ar.Count; i++)
        bs.Add(ar[i]);

    // Store the list after
    // each recursive call
    List<int> res = new List<int>();

    // If a < b
    if (a < b)
    {
        List<int> temp1 = new List<int>();
        temp1.Add(b);

        for(int i = 0; i < bs.Count; i++)
            temp1.Add(bs[i]);

        List<int> v = bubble_sort(temp1);
        v.Insert(0, a);
        res = v;
    }

    // Otherwise, if b >= a
    else
    {
        List<int> temp1 = new List<int>();
        temp1.Add(a);

        for(int i = 0; i < bs.Count; i++)
            temp1.Add(bs[i]);

        List<int> v = bubble_sort(temp1);
        v.Insert(0, b);
        res = v;
    }

    // Recursively call for the list
    // less than the last element and
    // and return the newly formed list
    List<int> pass = new List<int>();
    for(int i = 0; i < res.Count - 1; i++)
        pass.Add(res[i]);

    List<int> ans = bubble_sort(pass);
    ans.Add(res[res.Count - 1]);
    return ans;
}

// Driver Code
public static void Main()
{
    List<int> arr = new List<int>{ 1, 3, 4, 5, 6, 2 };
    List<int> res = bubble_sort(arr);

    // Print the array
    for(int i = 0; i < res.Count; i++)
        Console.Write(res[i] + " ");
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to implement bubble
  // sort without using loops
function bubble_sort(ar)
{
    // Base Case: If array
    // contains a single element
    if (ar.length <= 1)
      return ar;

    // Base Case: If array
    // contains two elements
    if (ar.length == 2) {
      if (ar[0] < ar[1])
        return ar;
      else
        return [ar[1], ar[0]];
    }

    // Store the first two elements
    // of the list in variables a and b
    let a = ar[0];
    let b = ar[1];

    // Store remaining elements
    // in the list bs
    let bs = [];
    for (let i = 2; i < ar.length; i++)
      bs.push(ar[i]);

    // Store the list after
    // each recursive call
    let res = [];

    // If a < b
    if (a < b) {
      let temp1 = [];
      temp1.push(b);
      for (let i = 0; i < bs.length; i++)
        temp1.push(bs[i]);

      let v = bubble_sort(temp1);
      v.unshift(a);
      res = v;
    }

    // Otherwise, if b >= a
    else {
      let temp1 = [];
      temp1.push(a);
      for (let i = 0; i < bs.length; i++)
        temp1.push(bs[i]);

      let v = bubble_sort(temp1);
      v.unshift(b);
      res = v;
    }

    // Recursively call for the list
    // less than the last element and
    // and return the newly formed list
    let pass = [];
    for (let i = 0; i < res.length - 1; i++)
      pass.push(res[i]);

    let ans = bubble_sort(pass);
    ans.push(res[res.length - 1]);
    return ans;
}

// Driver Code
let  arr =[1, 3, 4, 5, 6, 2];
let res = bubble_sort(arr);
document.write(res.join(" "));

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
1 2 3 4 5 6
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*