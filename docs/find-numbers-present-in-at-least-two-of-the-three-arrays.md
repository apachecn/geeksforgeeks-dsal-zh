# 找出三个数组中至少两个数组中的数字

> 原文:[https://www . geesforgeks . org/find-numbers-在三个数组中的至少两个数组中出现/](https://www.geeksforgeeks.org/find-numbers-present-in-at-least-two-of-the-three-arrays/)

给定 3 个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)、**arr【】**、**brr【】**和**crr【】**，任务是从给定的 3 个数组
**示例**中找到至少 2 个数组中的公共元素:

> **输入** : arr[] = {1，1，3，2，4}，brr[] = {2，3，5}，crr[] = {3，6}
> **输出** : {2，3}
> **解释**:元素 2 和 3 出现在至少 2 个数组中
> 
> **输入**:**【arr[]= { 3.1}，【br[]= { 2.3 }，【crr[]= { 1.2 }
> 输出**【2，3，1 })****

******接近**:可以借助 [HashSet](https://www.geeksforgeeks.org/hashset-in-java/) 解决任务，按照以下步骤解决问题:****

*   ****创建三个 hashsets、s2 和 s3)来存储三个数组的不同元素，还创建一个 HashSet 来存储所有三个数组的不同元素。****
*   ****迭代集合，检查至少两个集合(s1，s2)、(s1，s3)和(s2，s3)中的公共元素。****
*   ****如果一个元素满足上述条件，打印该元素。**** 

****下面是上述代码的实现:****

## ****C++****

```
**// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

void get(vector<int>& p, vector<int>& c, vector<int>& m)
{

    // Store distinct elements of array arr[]
    set<int> s1;

    // Store distinct elements of array brr[]
    set<int> s2;

    // Store distinct elements of array crr[]
    set<int> s3;

    // Store the distinct elements
    // of all three arrays
    set<int> set;
    for (auto i : p) {
        s1.insert(i);
        set.insert(i);
    }

    for (auto i : c) {
        s2.insert(i);
        set.insert(i);
    }

    for (int i : m) {
        s3.insert(i);
        set.insert(i);
    }

    // Stores the common elements
    vector<int> result;
    for (auto i : set) {
        if (s1.count(i) && s2.count(i)
            || s2.count(i) && s3.count(i)
            || s1.count(i) && s3.count(i))
            cout << i << " ";
    }
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 1, 3, 2, 4 };
    vector<int> brr = { 2, 3, 5 };
    vector<int> crr = { 3, 6 };
    get(arr, brr, crr);

    return 0;
}

    // This code is contributed by rakeshsahni**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java implementation of above approach

import java.io.*;
import java.util.*;

class GFG {
    public static void get(
        int[] p, int[] c, int[] m)
    {

        // Store distinct elements of array arr[]
        Set<Integer> s1 = new HashSet<>();

        // Store distinct elements of array brr[]
        Set<Integer> s2 = new HashSet<>();

        // Store distinct elements of array crr[]
        Set<Integer> s3 = new HashSet<>();

        // Store the distinct elements
        // of all three arrays
        Set<Integer> set = new HashSet<>();
        for (int i : p) {
            s1.add(i);
            set.add(i);
        }

        for (int i : c) {
            s2.add(i);
            set.add(i);
        }

        for (int i : m) {
            s3.add(i);
            set.add(i);
        }

        // Stores the common elements
        List<Integer> result
            = new ArrayList<>();
        for (int i : set) {
            if (s1.contains(i)
                    && s2.contains(i)
                || s2.contains(i)
                       && s3.contains(i)
                || s1.contains(i)
                       && s3.contains(i))
                System.out.print(i + " ");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 1, 1, 3, 2, 4 };
        int[] brr = { 2, 3, 5 };
        int[] crr = { 3, 6 };
        get(arr, brr, crr);
    }
}**
```

## ****蟒蛇 3****

```
**# Python3 implementation of above approach
def get(p, c, m) :

    # Store distinct elements of array arr[]
    s1 = set();

    # Store distinct elements of array brr[]
    s2 = set();

    # Store distinct elements of array crr[]
    s3 = set();

    # Store the distinct elements
    # of all three arrays
    set_obj = set();

    for i in p :
        s1.add(i);
        set_obj.add(i);

    for i in c :
        s2.add(i);
        set_obj.add(i);

    for i in m :
        s3.add(i);
        set_obj.add(i);

    # Stores the common elements
    result = [];
    for i in set_obj :
        if (list(s1).count(i) and list(s2).count(i)
            or list(s2).count(i) and list(s3).count(i)
            or list(s1).count(i) and list(s3).count(i)) :
            print(i,end= " ");

# Driver Code
if __name__ == "__main__" :

    arr = [ 1, 1, 3, 2, 4 ];
    brr = [ 2, 3, 5 ];
    crr = [ 3, 6 ];
    get(arr, brr, crr);

    # This code is contributed by AnkThon**
```

## ****C#****

```
**// C# implementation of above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG {
    static void get(
        int[] p, int[] c, int[] m)
    {

        // Store distinct elements of array arr[]
        HashSet<int> s1 = new HashSet<int>();

        // Store distinct elements of array brr[]
        HashSet<int> s2 = new HashSet<int>();

        // Store distinct elements of array crr[]
        HashSet<int> s3 = new HashSet<int>();

        // Store the distinct elements
        // of all three arrays
        HashSet<int> set = new HashSet<int>();
        foreach (int i in p) {
            s1.Add(i);
            set.Add(i);
        }

        foreach (int i in c) {
            s2.Add(i);
            set.Add(i);
        }

        foreach (int i in m) {
            s3.Add(i);
            set.Add(i);
        }

        // Stores the common elements
        ArrayList result
            = new ArrayList();
        foreach (int i in set) {
            if (s1.Contains(i)
                    && s2.Contains(i)
                || s2.Contains(i)
                       && s3.Contains(i)
                || s1.Contains(i)
                       && s3.Contains(i))
                Console.Write(i + " ");
        }
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 1, 1, 3, 2, 4 };
        int[] brr = { 2, 3, 5 };
        int[] crr = { 3, 6 };
        get(arr, brr, crr);
    }
}

// This code is contributed by Samim Hossain Mondal.**
```

## ****java 描述语言****

```
**<script>
// Javascript implementation of above approach
function get(p, c, m)
{

  // Store distinct elements of array arr[]
  let s1 = new Set();

  // Store distinct elements of array brr[]
  let s2 = new Set();

  // Store distinct elements of array crr[]
  let s3 = new Set();

  // Store the distinct elements
  // of all three arrays
  let set = new Set();
  for (i of p) {
    s1.add(i);
    set.add(i);
  }

  for (i of c) {
    s2.add(i);
    set.add(i);
  }

  for (i of m) {
    s3.add(i);
    set.add(i);
  }

  // Stores the common elements
  let result = [];
  for (i of [...set].reverse()) {
    if (s1.has(i) && s2.has(i)
      || s2.has(i) && s3.has(i)
      || s1.has(i) && s3.has(i))
      document.write(i + " ");
  }
}

// Driver Code
let arr = [1, 1, 3, 2, 4];
let brr = [2, 3, 5];
let crr = [3, 6];
get(arr, brr, crr);

// This code is contributed by gfgking
</script>**
```

******Output**

```
2 3 
```**** 

*******时间复杂度*** : O(n1+n2+n3)(其中 n1、n2 和 n3 为给定数组的长度)
***辅助空间*** : O(n1+n2+n3)****