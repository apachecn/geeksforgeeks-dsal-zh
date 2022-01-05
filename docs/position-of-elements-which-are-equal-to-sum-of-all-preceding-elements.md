# 等于所有前面元素之和的元素位置

> 原文:[https://www . geeksforgeeks . org/等于所有前置元素总和的元素位置/](https://www.geeksforgeeks.org/position-of-elements-which-are-equal-to-sum-of-all-preceding-elements/)

给定正整数的数组**Arr[]****N**。任务是找到所有元素的位置，这些位置等于前面所有元素的总和。如果不存在这样的元素，打印-1。
**例:**

> **输入:** Arr[] = {1，2，3，6，3，15，5}
> **输出:** 3 4 6
> 这里，索引“3”处的元素即 3 等于前面元素(1 + 2)的和。
> 同样，在索引 4，6 = 1+2+3(所有前面元素的和)。
> 索引 6 处的元素，即 15 = 1 + 2 + 3 + 6 + 3。
> **输入:** Arr[] = {7，5，17，25}
> **输出:** -1

**方法:**
在遍历数组**Arr【】**时，保持一个 **sum** 变量，该变量存储元素的总和直到**I–1**。将总和与当前元素 **Arr[i]** 进行比较。如果相等，将此元素的索引推入答案向量。
以下是上述方法的实施:

## C++

```
// C++ implementation
#include <bits/stdc++.h>
using namespace std;

// function to return valid indexes
vector<int> find_idx(int ar[], int n)
{

    // Vector to store the answer
    vector<int> answer;

    // Initial sum would always
    // be first element
    int sum = ar[0];

    for (int i = 1; i < n; i++) {

        // Check if sum till now
        // is equal to current element
        if (sum == ar[i]) {
            answer.push_back(i + 1);
        }

        // Updating the sum by
        // adding the current
        // element in each
        // iteration.
        sum += ar[i];
    }

    return answer;
}

// Driver code
int main()
{
    int ar[] = { 1, 2, 3, 6, 3, 15, 5 };
    int n = sizeof(ar) / sizeof(int);

    vector<int> ans = find_idx(ar, n);

    if (ans.size() != 0) {
        for (int i : ans) {
            cout << i << " ";
        }
    }
    else {
        cout << "-1";
    }

    cout << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// function to return valid indexes
static Vector<Integer> find_idx(int ar[], int n)
{

    // Vector to store the answer
    Vector<Integer> answer = new Vector<Integer>();

    // Initial sum would always
    // be first element
    int sum = ar[0];

    for (int i = 1; i < n; i++)
    {

        // Check if sum till now
        // is equal to current element
        if (sum == ar[i])
        {
            answer.add(i + 1);
        }

        // Updating the sum by adding the
        // current element in each iteration.
        sum += ar[i];
    }
    return answer;
}

// Driver code
public static void main(String[] args)
{
    int ar[] = { 1, 2, 3, 6, 3, 15, 5 };
    int n = ar.length;

    Vector<Integer> ans = find_idx(ar, n);

    if (ans.size() != 0)
    {
        for (int i : ans)
        {
            System.out.print(i + " ");
        }
    }
    else
    {
        System.out.println("-1");
    }
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# function to return valid indexes
def find_idx(ar, n) :

    # Vector to store the answer
    answer = [];

    # Initial sum would always
    # be first element
    sum = ar[0];

    for i in range(1, n) :

        # Check if sum till now
        # is equal to current element
        if (sum == ar[i]) :
            answer.append(i + 1);

        # Updating the sum by
        # adding the current
        # element in each
        # iteration.
        sum += ar[i];

    return answer;

# Driver code
if __name__ == "__main__" :

    ar = [ 1, 2, 3, 6, 3, 15, 5 ];
    n = len(ar);

    ans = find_idx(ar, n);

    if (len(ans) != 0) :

        for i in ans :
            print(i, end = " ");

    else :

        print("-1");

    print();

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// function to return valid indexes
static List<int> find_idx(int []ar, int n)
{

    // Vector to store the answer
    List<int> answer = new List<int>();

    // Initial sum would always
    // be first element
    int sum = ar[0];

    for (int i = 1; i < n; i++)
    {

        // Check if sum till now
        // is equal to current element
        if (sum == ar[i])
        {
            answer.Add(i + 1);
        }

        // Updating the sum by adding the
        // current element in each iteration.
        sum += ar[i];
    }
    return answer;
}

// Driver code
public static void Main(String[] args)
{
    int []ar = { 1, 2, 3, 6, 3, 15, 5 };
    int n = ar.Length;

    List<int> ans = find_idx(ar, n);

    if (ans.Count != 0)
    {
        foreach (int i in ans)
        {
            Console.Write(i + " ");
        }
    }
    else
    {
        Console.WriteLine("-1");
    }
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript implementation

// function to return valid indexes
function find_idx(ar, n) {

    // Vector to store the answer
    let answer = [];

    // Initial sum would always
    // be first element
    let sum = ar[0];

    for (let i = 1; i < n; i++) {

        // Check if sum till now
        // is equal to current element
        if (sum == ar[i]) {
            answer.push(i + 1);
        }

        // Updating the sum by
        // adding the current
        // element in each
        // iteration.
        sum += ar[i];
    }

    return answer;
}

// Driver code

let ar = [1, 2, 3, 6, 3, 15, 5];
let n = ar.length;

let ans = find_idx(ar, n);

if (ans.length != 0) {
    for (let i of ans) {
        document.write(i + " ");
    }
}
else {
    document.write("-1");
}

document.write("<br>");

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
3 4 6
```