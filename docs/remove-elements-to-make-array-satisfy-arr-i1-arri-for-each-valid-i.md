# 移除元素，使数组满足每个有效 I 的 arr[I+1]<arr[I]

> 原文:[https://www . geesforgeks . org/remove-elements-to-make-arr-submit-arr-i1-arri-for-ever-valid-I/](https://www.geeksforgeeks.org/remove-elements-to-make-array-satisfy-arr-i1-arri-for-each-valid-i/)

给定非负整数的数组 **arr[]** 。我们必须从这个数组中删除元素，这样每个有效的 **i** 的**arr【I+1】>arr【j】**将被计为一步。我们必须应用相同的操作，直到数组变得严格递减。现在的任务是计算获得所需数组所需的步骤数。

**示例:**

> **输入:** arr[] = {6，5，8，4，7，10，9}
> **输出:** 2
> 最初 8，7 和 10 不满足条件
> ，所以在第一步
> 中它们都被删除，数组变成{6，5，4，9}
> 在下一步 9 被删除，
> 数组变成{6，5，4}，严格递减。
> 
> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 1

**方法:**想法是只保留需要针对特定元素进行检查的必需元素的索引。因此，我们使用向量只存储所需的索引。如果满足以下条件，我们在后面插入每个索引，然后从后面移除索引。

> **arr[请参见后面()] ≥ val[i]**

我们采用另一个数组，其中我们更新了特定元素删除的步骤数。
如果**状态[i] = -1** ，则元素不被删除，0 表示第一步，以此类推。这就是为什么我们将在答案中添加 1。
在弹出索引的同时，我们反复更新元素的状态。如果弹出所有索引，即 **vect.size() = 0** ，则不删除该元素，因此将其状态更改为 **-1** 。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
int status[100000];

// Function to return the required
// number of steps
int countSteps(int* val, int n)
{
    int sol = 0;
    vector<int> vec(1, 0);
    status[0] = -1;

    // Compute the number of steps
    for (int i = 1; i < n; ++i) {

        // Current status is to
        // delete in first step
        status[i] = 0;

        // Pop the indices while
        // condition is satisfied
        while (vec.size() > 0
               && val[vec.back()] >= val[i]) {

            // Inserting the correct
            // step no to delete
            status[i] = max(status[i],
                            status[vec.back()] + 1);
            vec.pop_back();
        }
        if (vec.size() == 0) {

            // Status changed to not delete
            status[i] = -1;
        }

        // Pushing a new index in the vector
        vec.push_back(i);

        // Build the solution from
        // smaller to larger size
        sol = max(sol, status[i] + 1);
    }
    return sol;
}

// Driver code
int main()
{
    int val[] = { 6, 5, 8, 4, 7, 10, 9 };
    int n = sizeof(val) / sizeof(val[0]);

    cout << countSteps(val, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java implementation of the approach
import java.util.*;

class GFG 
{

static int []status = new int[100000];

// Function to return the required
// number of steps
static int countSteps(int[]val, int n)
{
    int sol = 0;
    Vector<Integer> vec = new Vector<>(1);
    vec.add(0);
    status[0] = -1;

    // Compute the number of steps
    for (int i = 1; i < n; ++i) 
    {

        // Current status is to
        // delete in first step
        status[i] = 0;

        // Pop the indices while
        // condition is satisfied
        while (vec.size() > 0
            && val[vec.lastElement()] >= val[i])
        {

            // Inserting the correct
            // step no to delete
            status[i] = Math.max(status[i],
                            status[vec.lastElement()] + 1);
            vec.remove(vec.lastElement());
        }
        if (vec.isEmpty())
        {

            // Status changed to not delete
            status[i] = -1;
        }

        // Pushing a new index in the vector
        vec.add(i);

        // Build the solution from
        // smaller to larger size
        sol = Math.max(sol, status[i] + 1);
    }
    return sol;
}

// Driver code
public static void main(String[] args) 
{
    int val[] = { 6, 5, 8, 4, 7, 10, 9 };
    int n = val.length;

    System.out.println(countSteps(val, n));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the approach 

status = [0]*100000; 

# Function to return the required 
# number of steps 
def countSteps(val, n) :

    sol = 0; 
    vec = [1, 0]; 
    status[0] = -1; 

    # Compute the number of steps 
    for i in range(n) :

        # Current status is to 
        # delete in first step 
        status[i] = 0; 

        # Pop the indices while 
        # condition is satisfied 
        while (len(vec) > 0
            and val[vec[len(vec)-1]] >= val[i]) : 

            # Inserting the correct 
            # step no to delete 
            status[i] = max(status[i], 
                            status[len(vec)-1] + 1); 
            vec.pop(); 

        if (len(vec) == 0) :

            # Status changed to not delete 
            status[i] = -1; 

        # Pushing a new index in the vector 
        vec.append(i); 

        # Build the solution from 
        # smaller to larger size 
        sol = max(sol, status[i] + 1); 

    return sol; 

# Driver code 
if __name__ == "__main__" : 

    val = [ 6, 5, 8, 4, 7, 10, 9 ]; 
    n = len(val); 

    print(countSteps(val, n)); 

# This code is contributed by AnkitRai01
```

## C#

```
// A C# implementation of the approach 
using System;
using System.Collections.Generic;

class GFG 
{ 

static int []status = new int[100000]; 

// Function to return the required 
// number of steps 
static int countSteps(int[]val, int n) 
{ 
    int sol = 0; 
    List<int> vec = new List<int>(1); 
    vec.Add(0); 
    status[0] = -1; 

    // Compute the number of steps 
    for (int i = 1; i < n; ++i) 
    { 

        // Current status is to 
        // delete in first step 
        status[i] = 0; 

        // Pop the indices while 
        // condition is satisfied 
        while (vec.Count > 0
            && val[vec[vec.Count-1]] >= val[i]) 
        { 

            // Inserting the correct 
            // step no to delete 
            status[i] = Math.Max(status[i], 
                            status[vec[vec.Count-1]] + 1); 
            vec.Remove(vec[vec.Count-1]); 
        } 
        if (vec.Count == 0) 
        { 

            // Status changed to not delete 
            status[i] = -1; 
        } 

        // Pushing a new index in the vector 
        vec.Add(i); 

        // Build the solution from 
        // smaller to larger size 
        sol = Math.Max(sol, status[i] + 1); 
    } 
    return sol; 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    int []val = { 6, 5, 8, 4, 7, 10, 9 }; 
    int n = val.Length; 

    Console.WriteLine(countSteps(val, n)); 
} 
} 

// This code contributed by Rajput-Ji
```

**Output:**

```
2

```