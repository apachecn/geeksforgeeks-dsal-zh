# 根据给定的索引对数组重新排序，允许重复

> 原文:[https://www . geesforgeks . org/reorder-a-array-根据给定的索引-允许重复/](https://www.geeksforgeeks.org/reorder-an-array-according-to-given-indices-with-repetition-allowed/)

给定两个大小为 **N** 的整数数组 **arr** 和**索引**，任务是通过在**索引**数组给定的索引处插入 **arr** 数组给定的元素来创建一个新数组。如果特定位置出现多次，则右移右侧数组元素，然后在给定索引处插入元素。

**注:**给出了索引数组中所有的索引都在[0，N]的范围内。

**示例:**

> **输入:**arr =【0，1，2，3，4】，索引=【0，1，2，2，1】
> **输出:**【0，4，1，3，2】
> **解释:**
> 首先我们在第 0，1，2 个索引处插入，这样数组就会变成【0，1，2】
> 然后我们在第 2 个位置再次插入，右移所有右侧元素，这样数组就会变成【0，1，3，2】
> 
> **输入:** arr = [1，2，3，4，0]，索引= [0，1，2，3，0]
> **输出:**【0，1，2，3，4】

**方法(使用静态数组):**
如果我们使用静态数组，那么给定的问题可以通过以下步骤解决:

*   创建一个大小为 **N** 的新数组**最终数组**，以存储结果输出。
*   对于给定 **arr** 数组中的每个元素，将其插入到由**索引**数组给出的相应给定索引处，只需使用:

```
finalArr[index[i]] = arr[i]

where i is the current
position during iteration
```

*   如果索引重复，则右移所有右侧元素，然后最后在该位置插入。

**方法(使用动态数组):**
如果我们使用一个动态的类似数组的结构，像 Vectors 等；然后我们可以简单地在给定的索引处插入给定的元素，而不用担心重复。当向量数据结构在每次插入时扩展时，它自己负责右移。

1.  创建一个新向量 **vec** ，以存储结果输出。
2.  对于给定 **arr** 数组中的每个元素，只需使用向量的 [insert()函数，将其插入到**索引**数组给出的相应给定索引处。这将在特定位置插入，并自动处理重复位置。](https://www.geeksforgeeks.org/vector-insert-function-in-c-stl/)

以下是上述方法的实现:

## C++

```
// C++ program to reorder an Array
// according to given indices
// with repetition allowed

#include <bits/stdc++.h>
using namespace std;

// Function that returns the
// modified vector according to indices
vector<int> createTargetArray(
    vector<int>& nums, vector<int>& index)
{
    // create an ans vector
    vector<int> ans;

    int n = nums.size();

    for (int i = 0; i < n; i++)

        // insert at particular position
        // mention in index array.
        ans.insert(ans.begin() + index[i],
                   nums[i]);

    // finally return ans
    return ans;
}

// Function to reorder and
// print the given array
void reorder(
    vector<int>& arr, vector<int>& index)
{
    vector<int> ans;
    ans = createTargetArray(arr, index);

    // print ans vector
    for (int i = 0; i < ans.size(); i++) {
        cout << ans[i] << " ";
    }
}

// Driver Code
int main()
{
    vector<int> arr = { 0, 1, 2, 3, 4 };
    vector<int> index = { 0, 1, 2, 2, 1 };

    reorder(arr, index);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reorder an Array
// according to given indices
// with repetition allowed
import java.util.*;

class GFG {

// Function that returns the
// modified List according to indices
static List<Integer> createTargetArray(List<Integer> nums,
                                       List<Integer> index)
{

    // Create an ans List
    List<Integer> ans = new ArrayList<>();

    int n = nums.size();

    for(int i = 0; i < n; i++)
    { 
       // Insert at particular position
       // mention in index array
       ans.add(index.get(i), nums.get(i));
    }

    // Finally return ans
    return ans;
}

// Function to reorder and
// print the given array
static void reorder(List<Integer> arr,
                    List<Integer> index)
{
    List<Integer> ans;
    ans = createTargetArray(arr, index);

    // Print ans list
    for(int i = 0; i < ans.size(); i++)
    {
       System.out.print(ans.get(i) + " ");
    }
}

// Driver code
public static void main(String[] args)
{

    List<Integer> arr = Arrays.asList(0, 1, 2, 3, 4);
    List<Integer> index = Arrays.asList(0, 1, 2, 2, 1);

    reorder(arr, index);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to reorder an array
# according to given indices
# with repetition allowed

# Function that returns the modified
# vector according to indices
def createTargetArray(nums, index):

    # Create an ans vector
    ans = []

    n = len(nums)
    for i in range(n):

        # Insert at particular position
        # mention in index array.
        ans.insert(index[i], nums[i])

    # Finally return ans
    return ans

# Function to reorder and
# print the given array
def reorder(arr, index):

    ans = createTargetArray(arr, index)

    # Print ans vector
    for i in range(len(ans)):
        print(ans[i], end = " ")

# Driver Code
if __name__ == "__main__":

    arr = [ 0, 1, 2, 3, 4 ]
    index = [ 0, 1, 2, 2, 1 ]

    reorder(arr, index)

# This code is contributed by chitranayal
```

## C#

```
// C# program to reorder an Array
// according to given indices
// with repetition allowed
using System;
using System.Collections.Generic;

class GFG{

// Function that returns the
// modified List according to indices
static List<int> createTargetArray(List<int> nums,
                                   List<int> index)
{

    // Create an ans List
    List<int> ans = new List<int>();

    int n = nums.Count;

    for(int i = 0; i < n; i++)
    {

        // Insert at particular position
        // mention in index array
        ans.Insert(index[i], nums[i]);
    }

    // Finally return ans
    return ans;
}

// Function to reorder and
// print the given array
static void reorder(List<int> arr,
                    List<int> index)
{
    List<int> ans;
    ans = createTargetArray(arr, index);

    // Print ans list
    for(int i = 0; i < ans.Count; i++)
    {
        Console.Write(ans[i] + " ");
    }
}

// Driver code
public static void Main()
{
    List<int> arr = new List<int>{ 0, 1, 2, 3, 4 };
    List<int> index = new List<int>{ 0, 1, 2, 2, 1 };

    reorder(arr, index);
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// Javascript program to reorder an Array
// according to given indices
// with repetition allowed

// Function that returns the
// modified vector according to indices
function createTargetArray( nums, index)
{
    // create an ans vector
    var ans = [];

    var n = nums.length;

    for (var i = 0; i < n; i++)

        // insert at particular position
        // mention in index array.
        ans.splice(index[i],0,
                   nums[i]);

    // finally return ans
    return ans;
}

// Function to reorder and
// print the given array
function reorder( arr, index)
{
    var ans = [];
    ans = createTargetArray(arr, index);

    // print ans vector
    for (var i = 0; i < ans.length; i++) {
        document.write( ans[i] + " ");
    }
}

// Driver Code
var arr = [0, 1, 2, 3, 4 ];
var index = [0, 1, 2, 2, 1 ];
reorder(arr, index);

</script>
```

**Output:** 

```
0 4 1 3 2
```