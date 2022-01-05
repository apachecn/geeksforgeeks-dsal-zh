# 通过删除大于其左侧所有元素的元素来缩小数组

> 原文:[https://www . geesforgeks . org/通过删除大于其左侧所有元素的元素来减少数组/](https://www.geeksforgeeks.org/reduce-the-array-by-deleting-elements-which-are-greater-than-all-elements-to-its-left/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是从给定数组中删除左边小于它的元素。继续从数组中删除元素，直到没有元素的左边相邻元素变小。在上述操作后打印结果数组。

**示例:**

> **输入:** arr[] = {2，4，1，3，4}
> **输出:** 2 1
> **解释:**
> 由于 4 大于 2，去掉 4，arr 变成{2，1，3，4}。
> 现在 3 大于 1，所以去掉 3，arr 变成{2，1，4}。
> 现在 4 大于 1，所以去掉 4，arr 变成{2，1}。
> 现在没有元素满足移除标准，因此结果数组为{2，1}。
> 
> **输入:** arr[] = {5，4，3，2，1}
> **输出:** 5 4 3 2 1

**方法:**思路是使用[合并排序](https://www.geeksforgeeks.org/merge-sort/)的概念。

1.  将输入数组分成子数组，直到每个子数组的大小变成 1。
2.  开始合并元素。
3.  合并时，从左子阵列中删除元素，直到它是最右边的元素，该元素的值大于右子阵列最左边的元素。
4.  在每个合并步骤中重复上述步骤，这样所有左边值较小的元素都被删除了。
5.  最后打印结果数组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to implement merging of arr[]
vector<int> merge(vector<int> x, vector<int> y)
{
    for(auto i : y)
    {
        if (x[x.size() - 1] > i)
            x.push_back(i);
    }
    return x;
}

// Function to delete all elements which
// satisfy the condition A[i] > A[i-1]
vector<int> mergeDel(vector<int> l)
{

    // Divide array into its subarray
    if (l.size() == 1)
        return l;

    int m = l.size() / 2;

    vector<int> temp1 = {l.begin() + 0,
                         l.begin() + m};
    vector<int> temp2 = {l.begin() + m,
                         l.end()};

    // Getting back merged array with all 
    // its right element greater than
    // left one.
    return merge(mergeDel(temp1),
                 mergeDel(temp2));
}

// Driver Code
int main()
{

    // Given array arr[]
    vector<int> arr({ 5, 4, 3, 2, 1 });
    vector<int> ans = mergeDel(arr);

    cout << "[ ";
    for(auto x: ans)
        cout << x << ", ";

    cout << "]";
}

// This code is contributed by SURENDRA_GANGWAR
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.ArrayList;
import java.util.Arrays;

class GFG{

// Function to implement merging of arr[]
static ArrayList<Integer> merge(ArrayList<Integer> x,
                                ArrayList<Integer> y)
{
    for(Integer i : y)
    {
        if (x.get(x.size() - 1) > i)
            x.add(i);
    }
    return x;
}

// Function to delete all elements which
// satisfy the condition A[i] > A[i-1]
static ArrayList<Integer> mergeDel(ArrayList<Integer> l)
{

    // Divide array into its subarray
    if (l.size() == 1)
        return l;

    int m = l.size() / 2;

    ArrayList<Integer> temp1 = new ArrayList<>(
        l.subList(0, m));
    ArrayList<Integer> temp2 = new ArrayList<>(
        l.subList(m, l.size()));

    // Getting back merged array with all
    // its right element greater than
    // left one.
    return merge(mergeDel(temp1), mergeDel(temp2));
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    Integer[] ar = { 5, 4, 3, 2, 1 };

    ArrayList<Integer> arr = new ArrayList<>(
        Arrays.asList(ar));
    ArrayList<Integer> ans = mergeDel(arr);

    System.out.print("[ ");
    for(Integer x : ans)
        System.out.print(x + ", ");

    System.out.println("]");
}
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to delete all elements which
# satisfy the condition A[i] > A[i-1]
def mergeDel(l):

    # Divide array into its subarray
    if len(l) == 1:

        return l

    m = int( len(l) / 2)

    # Getting back merged array with all
    # its right element greater than left one.
    return merge(mergeDel(l[ 0 : m ]),
                 mergeDel(l[ m : len(l)]) )

# Function to implement merging of arr[]
def merge(x, y):

    for i in y:

        if x[-1] > i :

            x = x + [i]

    return x

# Driver Code

# Function defination for main()
def main():

# Given array arr[]
    arr = [5, 4, 3, 2, 1]
    print(mergeDel(arr))

main()
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to implement merging of arr[]
static List<int> merge(List<int> x, List<int> y)
{
    foreach(int i in y)
    {
        if (x[x.Count - 1] > i)
            x.Add(i);
    }
    return x;
}

// Function to delete all elements which
// satisfy the condition A[i] > A[i-1]
static List<int> mergeDel(List<int> l)
{

    // Divide array into its subarray
    if (l.Count == 1)
        return l;

    int m = l.Count / 2;

    List<int> temp1 = l.GetRange(0, m);
    List<int> temp2 = l.GetRange(m, l.Count - m);

    // Getting back merged array with all
    // its right element greater than
    // left one.
    return merge(mergeDel(temp1),
                 mergeDel(temp2));
}

// Driver Code
public static void Main(string[] args)
{

    // Given array arr[]
    List<int> arr = new List<int>{ 5, 4, 3, 2, 1 };

    List<int> ans = mergeDel(arr);

    Console.Write("[ ");
    foreach(int x in ans)
        Console.Write(x + ", ");

    Console.Write("]");
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to implement merging of arr[]
function  merge(x,y)
{
    for(let i=0;i<y.length;i++)
    {
        if (x[x.length - 1] > y[i])
            x.push(y[i]);
    }
    return x;
}

// Function to delete all elements which
// satisfy the condition A[i] > A[i-1]
function mergeDel(l)
{
    // Divide array into its subarray
    if (l.length == 1)
        return l;

    let m = Math.floor(l.length / 2);

    let temp1 = l.slice(0, m);
    let temp2 = l.slice(m, l.length);

    // Getting back merged array with all
    // its right element greater than
    // left one.
    return merge(mergeDel(temp1), mergeDel(temp2));
}
// Driver Code

// Given array arr[]
let arr=[5, 4, 3, 2, 1];
let ans = mergeDel(arr);
document.write("[ ");
document.write(ans.join(", "));
document.write("]<br>");

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
[5, 4, 3, 2, 1]
```

**时间复杂度:***O(N * log N)*
T5】辅助空间: *O(1)*