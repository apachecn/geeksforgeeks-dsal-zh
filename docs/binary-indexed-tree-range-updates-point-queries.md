# 二进制索引树:范围更新和点查询

> 原文:[https://www . geesforgeks . org/binary-indexed-tree-range-updates-point-query/](https://www.geeksforgeeks.org/binary-indexed-tree-range-updates-point-queries/)

给定数组 arr[0..n-1]。需要执行以下操作。

1.  **更新(l，r，val)** :从[l，r]向数组中的所有元素添加‘val’。
2.  **getElement(i)** : Find element in the array indexed at ‘i’.

    最初，数组中的所有元素都是 0。查询可以是任何顺序，即在点查询之前可以有许多更新。

    **例:** 

    ```
    Input : arr = {0, 0, 0, 0, 0}
    Queries: update : l = 0, r = 4, val = 2
             getElement : i = 3
             update : l = 3, r = 4, val = 3 
             getElement : i = 3

    Output: Element at 3 is 2
            Element at 3 is 5

    Explanation : Array after first update becomes
                  {2, 2, 2, 2, 2}
                  Array after second update becomes
                  {2, 2, 2, 5, 5}

    ```

    **方法 1【更新:O(n)，getElement():O(1)】**

    1.  **更新(l，r，val) :** 从 l 到 r 迭代子阵，用 val 增加所有元素。
    2.  **getElement(i)** :要获取第 I 个索引处的元素，只需返回 arr[i]。

    最坏情况下的时间复杂度为 O(q*n)，其中 q 为查询数，n 为元素数。

    **方法 2【更新:O(1)，getElement():O(n)】**

    我们可以避免更新所有元素，并且只能更新数组的 2 个索引！

    1.  **更新(l，r，val) :** 将“val”添加到 l <sup>第</sup>元素中，并从(r+1) <sup>第</sup>元素中减去“val”，对所有更新查询执行此操作。

        ```
          arr[l]   = arr[l] + val
          arr[r+1] = arr[r+1] - val 

        ```

    2.  **getElement(i)** :要得到数组中第 i <sup>个</sup>元素，求数组中从 0 到 I(前缀和)的所有整数的和。

Let’s analyze the update query. **Why to add val to l<sup>th</sup> index?** Adding val to l<sup>th</sup> index means that all the elements after l are increased by val, since we will be computing the prefix sum for every element. **Why to subtract val from (r+1)<sup>th</sup> index?** A range update was required from [l,r] but what we have updated is [l, n-1] so we need to remove val from all the elements after r i.e., subtract val from (r+1)<sup>th</sup> index. Thus the val is added to range [l,r]. Below is implementation of above approach.

## C++

```
// C++ program to demonstrate Range Update 
// and Point Queries Without using BIT 
#include <bits/stdc++.h> 
using namespace std; 

// Updates such that getElement() gets an increased 
// value when queried from l to r. 
void update(int arr[], int l, int r, int val) 
{ 
    arr[l] += val; 
    arr[r+1] -= val; 
} 

// Get the element indexed at i 
int getElement(int arr[], int i) 
{ 
    // To get ith element sum of all the elements 
    // from 0 to i need to be computed 
    int res = 0; 
    for (int j = 0 ; j <= i; j++) 
        res += arr[j]; 

    return res; 
} 

// Driver program to test above function 
int main() 
{ 
    int arr[] = {0, 0, 0, 0, 0}; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    int l = 2, r = 4, val = 2; 
    update(arr, l, r, val); 

    //Find the element at Index 4 
    int index = 4; 
    cout << "Element at index " << index << " is " << 
         getElement(arr, index) << endl; 

    l = 0, r = 3, val = 4; 
    update(arr,l,r,val); 

    //Find the element at Index 3 
    index = 3; 
    cout << "Element at index " << index << " is " << 
         getElement(arr, index) << endl; 

    return 0; 
} 
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to demonstrate Range Update 
// and Point Queries Without using BIT 
class GfG { 

// Updates such that getElement() gets an increased 
// value when queried from l to r. 
static void update(int arr[], int l, int r, int val) 
{ 
    arr[l] += val;
    if(r + 1 < arr.length)
    arr[r+1] -= val; 
} 

// Get the element indexed at i 
static int getElement(int arr[], int i) 
{ 
    // To get ith element sum of all the elements 
    // from 0 to i need to be computed 
    int res = 0; 
    for (int j = 0 ; j <= i; j++) 
        res += arr[j]; 

    return res; 
} 

// Driver program to test above function 
public static void main(String[] args) 
{ 
    int arr[] = {0, 0, 0, 0, 0}; 
    int n = arr.length; 

    int l = 2, r = 4, val = 2; 
    update(arr, l, r, val); 

    //Find the element at Index 4 
    int index = 4; 
    System.out.println("Element at index " + index + " is " +getElement(arr, index)); 

    l = 0;
    r = 3;
    val = 4; 
    update(arr,l,r,val); 

    //Find the element at Index 3 
    index = 3; 
    System.out.println("Element at index " + index + " is " +getElement(arr, index)); 

}
} 
```

## 蟒蛇 3

```
# Python3 program to demonstrate Range 
# Update and PoQueries Without using BIT 

# Updates such that getElement() gets an 
# increased value when queried from l to r. 
def update(arr, l, r, val):
    arr[l] += val
    if r + 1 < len(arr):
        arr[r + 1] -= val

# Get the element indexed at i 
def getElement(arr, i):

    # To get ith element sum of all the elements 
    # from 0 to i need to be computed 
    res = 0
    for j in range(i + 1):
        res += arr[j] 

    return res

# Driver Code
if __name__ == '__main__': 
    arr = [0, 0, 0, 0, 0] 
    n = len(arr) 

    l = 2
    r = 4
    val = 2
    update(arr, l, r, val) 

    # Find the element at Index 4 
    index = 4
    print("Element at index", index, 
          "is", getElement(arr, index)) 

    l = 0
    r = 3
    val = 4
    update(arr, l, r, val) 

    # Find the element at Index 3 
    index = 3
    print("Element at index", index,
          "is", getElement(arr, index))

# This code is contributed by PranchalK
```

## C#

```
// C# program to demonstrate Range Update 
// and Point Queries Without using BIT 
using System;

class GfG 
{ 

// Updates such that getElement() 
// gets an increased value when
// queried from l to r. 
static void update(int []arr, int l, 
                    int r, int val) 
{ 
    arr[l] += val; 
    if(r + 1 < arr.Length) 
    arr[r + 1] -= val; 
} 

// Get the element indexed at i 
static int getElement(int []arr, int i) 
{ 
    // To get ith element sum of all the elements 
    // from 0 to i need to be computed 
    int res = 0; 
    for (int j = 0 ; j <= i; j++) 
        res += arr[j]; 

    return res; 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    int []arr = {0, 0, 0, 0, 0}; 
    int n = arr.Length; 

    int l = 2, r = 4, val = 2; 
    update(arr, l, r, val); 

    //Find the element at Index 4 
    int index = 4; 
    Console.WriteLine("Element at index " + 
                        index + " is " +
                        getElement(arr, index)); 

    l = 0; 
    r = 3; 
    val = 4; 
    update(arr,l,r,val); 

    //Find the element at Index 3 
    index = 3; 
    Console.WriteLine("Element at index " + 
                            index + " is " +
                            getElement(arr, index)); 
} 
} 

// This code is contributed by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to demonstrate Range Update 
// and Point Queries Without using BIT 

// Updates such that getElement() gets an 
// increased value when queried from l to r. 
function update(&$arr, $l, $r, $val) 
{ 
    $arr[$l] += $val;
    if($r + 1 < sizeof($arr))
    $arr[$r + 1] -= $val; 
} 

// Get the element indexed at i 
function getElement(&$arr, $i) 
{ 
    // To get ith element sum of all the elements 
    // from 0 to i need to be computed 
    $res = 0; 
    for ($j = 0 ; $j <= $i; $j++) 
        $res += $arr[$j]; 

    return $res; 
} 

// Driver Code
$arr = array(0, 0, 0, 0, 0); 
$n = sizeof($arr); 

$l = 2; $r = 4; $val = 2; 
update($arr, $l, $r, $val); 

// Find the element at Index 4 
$index = 4; 
echo("Element at index " . $index . 
     " is " . getElement($arr, $index) . "\n"); 

$l = 0;
$r = 3;
$val = 4; 
update($arr, $l, $r, $val); 

// Find the element at Index 3 
$index = 3; 
echo("Element at index " . $index . 
     " is " . getElement($arr, $index)); 

// This code is contributed by Code_Mech
?>
```

**Output:**

```
Element at index 4 is 2
Element at index 3 is 6

```

**时间复杂度** : O(q*n)，其中 q 为查询数。

**方法 3(使用二进制索引树)**

在方法 2 中，我们已经看到问题可以简化为更新和前缀求和查询。我们已经看到 [BIT 可以在 O(Logn)时间内做更新和前缀求和查询。](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)

下面是实现。

## C++

```
// C++ code to demonstrate Range Update and
// Point Queries on a Binary Index Tree
#include <bits/stdc++.h>
using namespace std;

// Updates a node in Binary Index Tree (BITree) at given index
// in BITree. The given value 'val' is added to BITree[i] and
// all of its ancestors in tree.
void updateBIT(int BITree[], int n, int index, int val)
{
    // index in BITree[] is 1 more than the index in arr[]
    index = index + 1;

    // Traverse all ancestors and add 'val'
    while (index <= n)
    {
        // Add 'val' to current node of BI Tree
        BITree[index] += val;

        // Update index to that of parent in update View
        index += index & (-index);
    }
}

// Constructs and returns a Binary Indexed Tree for given
// array of size n.
int *constructBITree(int arr[], int n)
{
    // Create and initialize BITree[] as 0
    int *BITree = new int[n+1];
    for (int i=1; i<=n; i++)
        BITree[i] = 0;

    // Store the actual values in BITree[] using update()
    for (int i=0; i<n; i++)
        updateBIT(BITree, n, i, arr[i]);

    // Uncomment below lines to see contents of BITree[]
    //for (int i=1; i<=n; i++)
    //      cout << BITree[i] << " ";

    return BITree;
}

// SERVES THE PURPOSE OF getElement()
// Returns sum of arr[0..index]. This function assumes
// that the array is preprocessed and partial sums of
// array elements are stored in BITree[]
int getSum(int BITree[], int index)
{
    int sum = 0; // Iniialize result

    // index in BITree[] is 1 more than the index in arr[]
    index = index + 1;

    // Traverse ancestors of BITree[index]
    while (index>0)
    {
        // Add current element of BITree to sum
        sum += BITree[index];

        // Move index to parent node in getSum View
        index -= index & (-index);
    }
    return sum;
}

// Updates such that getElement() gets an increased
// value when queried from l to r.
void update(int BITree[], int l, int r, int n, int val)
{
    // Increase value at 'l' by 'val'
    updateBIT(BITree, n, l, val);

    // Decrease value at 'r+1' by 'val'
    updateBIT(BITree, n, r+1, -val);
}

// Driver program to test above function
int main()
{
    int arr[] = {0, 0, 0, 0, 0};
    int n = sizeof(arr)/sizeof(arr[0]);
    int *BITree = constructBITree(arr, n);

    // Add 2 to all the element from [2,4]
    int l = 2, r = 4, val = 2;
    update(BITree, l, r, n, val);

    // Find the element at Index 4
    int index = 4;
    cout << "Element at index " << index << " is " <<
         getSum(BITree,index) << "\n";

    // Add 2 to all the element from [0,3]
    l = 0, r = 3, val = 4;
    update(BITree, l, r, n, val);

    // Find the element at Index 3
    index = 3;
    cout << "Element at index " << index << " is " <<
         getSum(BITree,index) << "\n" ;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java code to demonstrate Range Update and
* Point Queries on a Binary Index Tree.
* This method only works when all array
* values are initially 0.*/
class GFG
{

    // Max tree size
    final static int MAX = 1000;

    static int BITree[] = new int[MAX];

    // Updates a node in Binary Index
    // Tree (BITree) at given index
    // in BITree. The given value 'val'
    // is added to BITree[i] and
    // all of its ancestors in tree.
    public static void updateBIT(int n, 
                                 int index, 
                                 int val)
    {
        // index in BITree[] is 1 
        // more than the index in arr[]
        index = index + 1;

        // Traverse all ancestors 
        // and add 'val'
        while (index <= n)
        {
            // Add 'val' to current 
            // node of BITree
            BITree[index] += val;

            // Update index to that 
            // of parent in update View
            index += index & (-index);
        }
    }

    // Constructs Binary Indexed Tree 
    // for given array of size n.

    public static void constructBITree(int arr[],
                                       int n)
    {
        // Initialize BITree[] as 0
        for(int i = 1; i <= n; i++)
            BITree[i] = 0;

        // Store the actual values 
        // in BITree[] using update()
        for(int i = 0; i < n; i++)
            updateBIT(n, i, arr[i]);

        // Uncomment below lines to 
        // see contents of BITree[]
        // for (int i=1; i<=n; i++)
        //     cout << BITree[i] << " ";
    }

    // SERVES THE PURPOSE OF getElement()
    // Returns sum of arr[0..index]. This 
    // function assumes that the array is
    // preprocessed and partial sums of
    // array elements are stored in BITree[]
    public static int getSum(int index)
    {
        int sum = 0; //Initialize result

        // index in BITree[] is 1 more 
        // than the index in arr[]
        index = index + 1;

        // Traverse ancestors
        // of BITree[index]
        while (index > 0)
        {

            // Add current element 
            // of BITree to sum
            sum += BITree[index];

            // Move index to parent 
            // node in getSum View
            index -= index & (-index);
        }

        // Return the sum
        return sum;
    }

    // Updates such that getElement() 
    // gets an increased value when 
    // queried from l to r.
    public static void update(int l, int r, 
                              int n, int val)
    {
        // Increase value at 
        // 'l' by 'val'
        updateBIT(n, l, val);

        // Decrease value at
        // 'r+1' by 'val'
        updateBIT(n, r + 1, -val);
    }

    // Driver Code
    public static void main(String args[])
    {
        int arr[] = {0, 0, 0, 0, 0};
        int n = arr.length;

        constructBITree(arr,n);

        // Add 2 to all the
        // element from [2,4]
        int l = 2, r = 4, val = 2;
        update(l, r, n, val);

        int index = 4;

        System.out.println("Element at index "+ 
                                index + " is "+ 
                                getSum(index));

        // Add 2 to all the 
        // element from [0,3]
        l = 0; r = 3; val = 4;
        update(l, r, n, val);

        // Find the element
        // at Index 3
        index = 3;
        System.out.println("Element at index "+ 
                                index + " is "+ 
                                getSum(index));
    }
}
// This code is contributed
// by Puneet Kumar.
```

## 蟒蛇 3

```
# Python3 code to demonstrate Range Update and
# PoQueries on a Binary Index Tree

# Updates a node in Binary Index Tree (BITree) at given index
# in BITree. The given value 'val' is added to BITree[i] and
# all of its ancestors in tree.
def updateBIT(BITree, n, index, val):

    # index in BITree[] is 1 more than the index in arr[]
    index = index + 1

    # Traverse all ancestors and add 'val'
    while (index <= n):

        # Add 'val' to current node of BI Tree
        BITree[index] += val

        # Update index to that of parent in update View
        index += index & (-index)

# Constructs and returns a Binary Indexed Tree for given
# array of size n.
def constructBITree(arr, n):

    # Create and initialize BITree[] as 0
    BITree = [0]*(n+1)

    # Store the actual values in BITree[] using update()
    for i in range(n):
        updateBIT(BITree, n, i, arr[i])

    return BITree

# SERVES THE PURPOSE OF getElement()
# Returns sum of arr[0..index]. This function assumes
# that the array is preprocessed and partial sums of
# array elements are stored in BITree[]
def getSum(BITree, index):
    sum = 0 # Iniialize result

    # index in BITree[] is 1 more than the index in arr[]
    index = index + 1

    # Traverse ancestors of BITree[index]
    while (index > 0):

        # Add current element of BITree to sum
        sum += BITree[index]

        # Move index to parent node in getSum View
        index -= index & (-index)
    return sum

# Updates such that getElement() gets an increased
# value when queried from l to r.
def update(BITree, l, r, n, val):

    # Increase value at 'l' by 'val'
    updateBIT(BITree, n, l, val)

    # Decrease value at 'r+1' by 'val'
    updateBIT(BITree, n, r+1, -val)

# Driver code
arr = [0, 0, 0, 0, 0]
n = len(arr)
BITree = constructBITree(arr, n)

# Add 2 to all the element from [2,4]
l = 2
r = 4
val = 2
update(BITree, l, r, n, val)

# Find the element at Index 4
index = 4
print("Element at index", index, "is", getSum(BITree, index))

# Add 2 to all the element from [0,3]
l = 0
r = 3
val = 4
update(BITree, l, r, n, val)

# Find the element at Index 3
index = 3
print("Element at index", index, "is", getSum(BITree,index))

# This code is contributed by mohit kumar 29
```

## C#

```
using System;

/* C# code to demonstrate Range Update and 
* Point Queries on a Binary Index Tree. 
* This method only works when all array 
* values are initially 0.*/
public class GFG
{

    // Max tree size 
    public const int MAX = 1000;

    public static int[] BITree = new int[MAX];

    // Updates a node in Binary Index 
    // Tree (BITree) at given index 
    // in BITree. The given value 'val' 
    // is added to BITree[i] and 
    // all of its ancestors in tree. 
    public static void updateBIT(int n, int index, int val)
    {
        // index in BITree[] is 1  
        // more than the index in arr[] 
        index = index + 1;

        // Traverse all ancestors  
        // and add 'val' 
        while (index <= n)
        {
            // Add 'val' to current  
            // node of BITree 
            BITree[index] += val;

            // Update index to that  
            // of parent in update View 
            index += index & (-index);
        }
    }

    // Constructs Binary Indexed Tree  
    // for given array of size n. 

    public static void constructBITree(int[] arr, int n)
    {
        // Initialize BITree[] as 0 
        for (int i = 1; i <= n; i++)
        {
            BITree[i] = 0;
        }

        // Store the actual values  
        // in BITree[] using update() 
        for (int i = 0; i < n; i++)
        {
            updateBIT(n, i, arr[i]);
        }

        // Uncomment below lines to  
        // see contents of BITree[] 
        // for (int i=1; i<=n; i++) 
        //     cout << BITree[i] << " "; 
    }

    // SERVES THE PURPOSE OF getElement() 
    // Returns sum of arr[0..index]. This  
    // function assumes that the array is 
    // preprocessed and partial sums of 
    // array elements are stored in BITree[] 
    public static int getSum(int index)
    {
        int sum = 0; //Initialize result

        // index in BITree[] is 1 more  
        // than the index in arr[] 
        index = index + 1;

        // Traverse ancestors 
        // of BITree[index] 
        while (index > 0)
        {

            // Add current element  
            // of BITree to sum 
            sum += BITree[index];

            // Move index to parent  
            // node in getSum View 
            index -= index & (-index);
        }

        // Return the sum 
        return sum;
    }

    // Updates such that getElement()  
    // gets an increased value when  
    // queried from l to r. 
    public static void update(int l, int r, int n, int val)
    {
        // Increase value at  
        // 'l' by 'val' 
        updateBIT(n, l, val);

        // Decrease value at 
        // 'r+1' by 'val' 
        updateBIT(n, r + 1, -val);
    }

    // Driver Code 
    public static void Main(string[] args)
    {
        int[] arr = new int[] {0, 0, 0, 0, 0};
        int n = arr.Length;

        constructBITree(arr,n);

        // Add 2 to all the 
        // element from [2,4] 
        int l = 2, r = 4, val = 2;
        update(l, r, n, val);

        int index = 4;

        Console.WriteLine("Element at index " + index + " is " + getSum(index));

        // Add 2 to all the  
        // element from [0,3] 
        l = 0;
        r = 3;
        val = 4;
        update(l, r, n, val);

        // Find the element 
        // at Index 3 
        index = 3;
        Console.WriteLine("Element at index " + index + " is " + getSum(index));
    }
}

  // This code is contributed by Shrikant13
```

**输出:**

```
Element at index 4 is 2
Element at index 3 is 6

```

**时间复杂度:** O(q * log n) + O(n * log n)，其中 q 为查询数。

当大多数查询是 getElement()时，方法 1 是有效的，当大多数查询是 updates()时，方法 2 是有效的，当两个查询混合时，方法 3 是优选的。

本文由 **Chirag Agarwal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。