# 数组中给定索引范围的 GCD

> 原文： [https://www.geeksforgeeks.org/gcds-of-a-given-index-ranges-in-an-array/](https://www.geeksforgeeks.org/gcds-of-a-given-index-ranges-in-an-array/)

给定一个数组`a[0 ... n-1]`。 我们应该能够有效地找到从索引`qs`（查询开始）到`qe`（查询结束）的 GCD，其中`0 <= qs <= qe <= n-1`。

范例：

```
Input : a[] = {2, 3, 60, 90, 50};
        Index Ranges : {1, 3}, {2, 4}, {0, 2}
Output: GCDs of given ranges are 3, 10, 1

```



**方法 1（简单）**：

一个简单的解决方案是运行从`qs`到`qe`的循环，并找到给定范围内的 GCD。 在最坏的情况下，此解决方案需要`O(n)`时间。

**方法 2（二维数组）**：

另一种解决方案是创建 2D 数组，其中条目`[i, j]`将 GCD 存储在`arr[i..j]`范围内。 现在可以以`O(1)`时间计算给定范围的 GCD，但是预处理需要`O(n ^ 2)`时间。 同样，这种方法需要`O(n ^ 2)`额外的空间，这对于大型输入数组可能会变得很大。

**方法 3（段树）**：

先决条件：[段树系列 1](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)，[段树系列 2](https://www.geeksforgeeks.org/segment-tree-set-1-range-minimum-query/)

段树可用于在适当的时间内进行预处理和查询。 使用段树，预处理时间为`O(n)`，到 GCD 查询的时间为`O(Logn)`。 存储段树所需的额外空间为`O(n)`。

**段树**的表示形式：

*   叶节点是输入数组的元素。

*   每个内部节点代表其下所有叶子的 GCD。

树的数组表示法用于表示段树，即对于索引`i`处的每个节点，

*   左子级在索引`2 * i + 1`

*   右子级为`2 * i + 2`，父级为`floor((i-1) / 2)`。

**从给定数组**构造段树：

*   从段`arr[0 ... n-1]`开始，并继续分为两半。 每次我们将当前段分为两半（如果尚未将其变成长度为 1 的段），然后在两个半段上调用相同的过程，对于每个这样的段，我们将 GCD 值存储在段树节点中。

*   除最后一个级别外，已构建的段树的所有级别都将被完全填充。 而且，该树将是完整的二叉树（每个节点都有 0 个或两个孩子），因为我们总是在每个级别将分段分为两半。

*   由于构造的树始终是具有`n`个叶的完整二叉树，因此将有`n-1`个内部节点。 因此，节点总数将为`2 * n – 1`。

*   段树的高度将为`⌈log2(n)⌉`。 由于树是使用数组表示的，并且必须保持父索引和子索引之间的关系，因此分配给段树的内存大小将为`2 * 2^⌈log2(n)⌉ – 1`

**查询给定范围**的 GCD

```
/ qs --> query start index, qe --> query end index
int GCD(node, qs, qe)
{
   if range of node is within qs and qe
      return value in node
   else if range of node is completely 
      outside qs and qe
      return INFINITE
   else
      return GCD( GCD(node's left child, qs, qe), 
                  GCD(node's right child, qs, qe) )
}

```

以下是此方法的实现。

## C++ 

```cpp

// C++ Program to find GCD of a number in a given Range 
// using segment Trees 
#include <bits/stdc++.h> 
using namespace std; 

// To store segment tree 
int *st; 

/*  A recursive function to get gcd of given 
    range of array indexes. The following are parameters for 
    this function. 

    st    --> Pointer to segment tree 
    si --> Index of current node in the segment tree. Initially 
               0 is passed as root is always at index 0 
    ss & se  --> Starting and ending indexes of the segment 
                 represented by current node, i.e., st[index] 
    qs & qe  --> Starting and ending indexes of query range */
int findGcd(int ss, int se, int qs, int qe, int si) 
{ 
    if (ss>qe || se < qs) 
        return 0; 
    if (qs<=ss && qe>=se) 
        return st[si]; 
    int mid = ss+(se-ss)/2; 
    return __gcd(findGcd(ss, mid, qs, qe, si*2+1), 
               findGcd(mid+1, se, qs, qe, si*2+2)); 
} 

//Finding The gcd of given Range 
int findRangeGcd(int ss, int se, int arr[],int n) 
{ 
    if (ss<0 || se > n-1 || ss>se) 
    { 
        cout << "Invalid Arguments" << "\n"; 
        return -1; 
    } 
    return findGcd(0, n-1, ss, se, 0); 
} 

// A recursive function that constructs Segment Tree for 
// array[ss..se]. si is index of current node in segment 
// tree st 
int constructST(int arr[], int ss, int se, int si) 
{ 
    if (ss==se) 
    { 
        st[si] = arr[ss]; 
        return st[si]; 
    } 
    int mid = ss+(se-ss)/2; 
    st[si] = __gcd(constructST(arr, ss, mid, si*2+1), 
                 constructST(arr, mid+1, se, si*2+2)); 
    return st[si]; 
} 

/* Function to construct segment tree from given array. 
   This function allocates memory for segment tree and 
   calls constructSTUtil() to fill the allocated memory */
int *constructSegmentTree(int arr[], int n) 
{ 
   int height = (int)(ceil(log2(n))); 
   int size = 2*(int)pow(2, height)-1; 
   st = new int[size]; 
   constructST(arr, 0, n-1, 0); 
   return st; 
} 

// Driver program to test above functions 
int main() 
{ 
    int a[] = {2, 3, 6, 9, 5}; 
    int n = sizeof(a)/sizeof(a[0]); 

    // Build segment tree from given array 
    constructSegmentTree(a, n); 

    // Starting index of range. These indexes are 0 based. 
    int l = 1; 

    // Last index of range.These indexes are 0 based. 
    int r = 3; 
    cout << "GCD of the given range is:"; 
    cout << findRangeGcd(l, r, a, n) << "\n"; 

    return 0; 
} 

```

## Java

```java

// Java Program to find GCD of a number in a given Range 
// using segment Trees 
import java.io.*; 

public class Main 
{ 
    private static int[] st; // Array to store segment tree 

    /* Function to construct segment tree from given array. 
       This function allocates memory for segment tree and 
       calls constructSTUtil() to fill the allocated memory */
    public static int[] constructSegmentTree(int[] arr) 
    { 
        int height = (int)Math.ceil(Math.log(arr.length)/Math.log(2)); 
        int size = 2*(int)Math.pow(2, height)-1; 
        st = new int[size]; 
        constructST(arr, 0, arr.length-1, 0); 
        return st; 
    } 

    // A recursive function that constructs Segment 
    // Tree for array[ss..se]. si is index of current 
    // node in segment tree st 
    public static int constructST(int[] arr, int ss, 
                                  int se, int si) 
    { 
        if (ss==se) 
        { 
            st[si] = arr[ss]; 
            return st[si]; 
        } 
        int mid = ss+(se-ss)/2; 
        st[si] = gcd(constructST(arr, ss, mid, si*2+1), 
                     constructST(arr, mid+1, se, si*2+2)); 
        return st[si]; 
    } 

    // Function to find gcd of 2 numbers. 
    private static int gcd(int a, int b) 
    { 
        if (a < b) 
        { 
            // If b greater than a swap a and b 
            int temp = b; 
            b = a; 
            a = temp; 
        } 

        if (b==0) 
            return a; 
        return gcd(b,a%b); 
    } 

    //Finding The gcd of given Range 
    public static int findRangeGcd(int ss, int se, int[] arr) 
    { 
        int n = arr.length; 

        if (ss<0 || se > n-1 || ss>se) 
            throw new IllegalArgumentException("Invalid arguments"); 

        return findGcd(0, n-1, ss, se, 0); 
    } 

    /*  A recursive function to get gcd of given 
    range of array indexes. The following are parameters for 
    this function. 

    st    --> Pointer to segment tree 
    si --> Index of current node in the segment tree. Initially 
               0 is passed as root is always at index 0 
    ss & se  --> Starting and ending indexes of the segment 
                 represented by current node, i.e., st[si] 
    qs & qe  --> Starting and ending indexes of query range */
    public static int findGcd(int ss, int se, int qs, int qe, int si) 
    { 
        if (ss>qe || se < qs) 
            return 0; 

        if (qs<=ss && qe>=se) 
            return st[si]; 

        int mid = ss+(se-ss)/2; 

        return gcd(findGcd(ss, mid, qs, qe, si*2+1), 
                   findGcd(mid+1, se, qs, qe, si*2+2)); 
    } 

    // Driver Code 
    public static void main(String[] args)throws IOException 
    { 
        int[] a = {2, 3, 6, 9, 5}; 

        constructSegmentTree(a); 

        int l = 1; // Starting index of range. 
        int r = 3; //Last index of range. 
        System.out.print("GCD of the given range is: "); 
        System.out.print(findRangeGcd(l, r, a)); 
    } 
}

```

## C# 

```cs

// C# Program to find GCD of a number in a given Range 
// using segment Trees 
using System; 

class GFG 
{ 
    private static int[] st; // Array to store segment tree 

    /* Function to construct segment tree from given array. 
    This function allocates memory for segment tree and 
    calls constructSTUtil() to fill the allocated memory */
    public static int[] constructSegmentTree(int[] arr) 
    { 
        int height = (int)Math.Ceiling(Math.Log(arr.Length)/Math.Log(2)); 
        int size = 2*(int)Math.Pow(2, height) - 1; 
        st = new int[size]; 
        constructST(arr, 0, arr.Length - 1, 0); 
        return st; 
    } 

    // A recursive function that constructs Segment 
    // Tree for array[ss..se]. si is index of current 
    // node in segment tree st 
    public static int constructST(int[] arr, int ss, 
                                int se, int si) 
    { 
        if (ss == se) 
        { 
            st[si] = arr[ss]; 
            return st[si]; 
        } 
        int mid = ss + (se - ss) / 2; 
        st[si] = gcd(constructST(arr, ss, mid, si * 2 + 1), 
                    constructST(arr, mid + 1, se, si * 2 + 2)); 
        return st[si]; 
    } 

    // Function to find gcd of 2 numbers. 
    private static int gcd(int a, int b) 
    { 
        if (a < b) 
        { 
            // If b greater than a swap a and b 
            int temp = b; 
            b = a; 
            a = temp; 
        } 

        if (b == 0) 
            return a; 
        return gcd(b,a % b); 
    } 

    // Finding The gcd of given Range 
    public static int findRangeGcd(int ss,  
                        int se, int[] arr) 
    { 
        int n = arr.Length; 

        if (ss < 0 || se > n-1 || ss > se) 
        { 
            Console.WriteLine("Invalid arguments"); 
            return int.MinValue; 
        } 

        return findGcd(0, n - 1, ss, se, 0); 
    } 

    /* A recursive function to get gcd of given 
    range of array indexes. The following are parameters for 
    this function. 

    st --> Pointer to segment tree 
    si --> Index of current node in the segment tree. Initially 
            0 is passed as root is always at index 0 
    ss & se --> Starting and ending indexes of the segment 
                represented by current node, i.e., st[si] 
    qs & qe --> Starting and ending indexes of query range */
    public static int findGcd(int ss, int se, int qs, int qe, int si) 
    { 
        if (ss > qe || se < qs) 
            return 0; 

        if (qs <= ss && qe >= se) 
            return st[si]; 

        int mid = ss + (se - ss)/2; 

        return gcd(findGcd(ss, mid, qs, qe, si * 2 + 1), 
                findGcd(mid + 1, se, qs, qe, si * 2 + 2)); 
    } 

    // Driver Code 
    public static void Main(String[] args) 
    { 
        int[] a = {2, 3, 6, 9, 5}; 

        constructSegmentTree(a); 

        int l = 1; // Starting index of range. 
        int r = 3; //Last index of range. 
        Console.Write("GCD of the given range is: "); 
        Console.Write(findRangeGcd(l, r, a)); 
    } 
} 

// This code has been contributed by 29AjayKumar 

```

**输出**：

```
 GCD of the given range is: 3
```

**时间复杂度**：树结构的时间复杂度为`O(n * log(min(a, b)))`，其中`n`是模式数，`a`和`b`是在合并操作期间计算 GCD 的节点 。 总共有`2n-1`个节点，并且在树结构中每个节点的值仅计算一次。 查询的时间复杂度为`O(Log n * Log n)`。

