# 求和的总面积等于 k 的最大面积的矩形子矩阵

> 原文：[https://www.geeksforgeeks.org/find-the-largest-area-rectangular-sub-matrix-whose-sum-is-equal-to-k/](https://www.geeksforgeeks.org/find-the-largest-area-rectangular-sub-matrix-whose-sum-is-equal-to-k/)

给定二维矩阵 **mat [] []** 和值 **k** 。 求和等于 **k** 的最大矩形子矩阵。

例：

```
Input : mat = { { 1, 7, -6, 5 }, 
            { -8, 6, 7, -2 }, 
            { 10, -15, 3, 2 }, 
            { -5, 2, 0, 9 } }
        k = 7 

Output : (Top, Left): (0, 1)
         (Bottom, Right): (2, 3)
         7 -6 5 
         6 7 -2 
        -15 3 2 

```

**朴素的方法**：检查给定 2D 数组中总和等于“ k”的每个可能的矩形，并打印最大的矩形。 该解决方案需要 4 个嵌套循环，并且该解决方案的时间复杂度为 O（n ^ 4）。

**高效方法**：[一维阵列的总和为](https://www.geeksforgeeks.org/longest-sub-array-sum-k/)的最长子阵列可用于将时间复杂度降低至 O（n ^ 3）。 这个想法是一一固定左列和右列，并为每个左列和右列对找到连续行的最长子数组，其总和等于“ k”。 我们基本上为每个固定的左和右列对找到顶部和底部行号（它们是最大子矩阵的一部分）。 要找到顶部和底部的行号，请计算从左到右每一行中元素的总和，并将这些总和存储在一个名为 temp []的数组中。 因此，temp [i]表示第 i 行中从左到右的元素总和。 现在，在 temp []上应用具有总和 k 的[最长子阵列](https://www.geeksforgeeks.org/longest-sub-array-sum-k/) 1D 算法，并获得总和等于 temp []的“ k”的最长子阵列。 该长度将是最大可能的长度，其中左侧和右侧为边界列。 设置左对右列对的“顶部”和“底部”行索引并计算面积。 以类似的方式获取总和等于“ k”的其他子矩阵的顶部，底部，左侧，右侧索引，并打印具有最大面积的索引。

## C++

```cpp

// C++ implementation to find the largest area rectangular 
// sub-matrix whose sum is equal to k 
#include <bits/stdc++.h> 
using namespace std; 

const int MAX = 100; 

// This function basically finds largest 'k' 
// sum subarray in arr[0..n-1]. If 'k' sum 
// doesn't exist, then it returns false. Else 
// it returns true and sets starting and 
// ending indexes as start and end. 
bool sumEqualToK(int arr[], int& start, 
                 int& end, int n, int k) 
{ 
    // unordered_map 'um' implemented 
    // as hash table 
    unordered_map<int, int> um; 
    int sum = 0, maxLen = 0; 

    // traverse the given array 
    for (int i = 0; i < n; i++) { 

        // accumulate sum 
        sum += arr[i]; 

        // when subarray starts from index '0' 
        // update maxLength and start and end points 
        if (sum == k) { 
            maxLen = i + 1; 
            start = 0; 
            end = i; 
        } 

        // make an entry for 'sum' if it is 
        // not present in 'um' 
        if (um.find(sum) == um.end()) 
            um[sum] = i; 

        // check if 'sum-k' is present in 'um' 
        // or not 
        if (um.find(sum - k) != um.end()) { 

            // update maxLength and start and end points 
            if (maxLen < (i - um[sum - k])) { 
                maxLen = i - um[sum - k]; 
                start = um[sum - k] + 1; 
                end = i; 
            } 
        } 
    } 

    // Return true if maximum length is non-zero 
    return (maxLen != 0); 
} 

// function to find the largest area rectangular 
// sub-matrix whose sum is equal to k 
void sumZeroMatrix(int mat[][MAX], int row, int col, int k) 
{ 
    // Variables to store the temporary values 
    int temp[row], area; 
    bool sum; 
    int up, down; 

    // Variables to store the final output 
    int fup = 0, fdown = 0, fleft = 0, fright = 0; 
    int maxArea = INT_MIN; 

    // Set the left column 
    for (int left = 0; left < col; left++) { 
        // Initialize all elements of temp as 0 
        memset(temp, 0, sizeof(temp)); 

        // Set the right column for the left column 
        // set by outer loop 
        for (int right = left; right < col; right++) { 
            // Calculate sum between current left 
            // and right column for every row 'i' 
            for (int i = 0; i < row; i++) 
                temp[i] += mat[i][right]; 

            // Find largest subarray with 'k' sum in 
            // temp[]. The sumEqualToK() function also 
            // sets values of 'up' and 'down;'. So 
            // if 'sum' is true then rectangle exists between 
            // (up, left) and (down, right) which are the 
            // boundary values. 
            sum = sumEqualToK(temp, up, down, row, k); 
            area = (down - up + 1) * (right - left + 1); 

            // Compare no. of elements with previous 
            // no. of elements in sub-Matrix. 
            // If new sub-matrix has more elements 
            // then update maxArea and final boundaries 
            // like fup, fdown, fleft, fright 
            if (sum && maxArea < area) { 
                fup = up; 
                fdown = down; 
                fleft = left; 
                fright = right; 
                maxArea = area; 
            } 
        } 
    } 

    // If there is no change in boundaries 
    // than check if mat[0][0] equals 'k' 
    // If it is not equal to 'k' then print 
    // that no such k-sum sub-matrix exists 
    if (fup == 0 && fdown == 0 && fleft == 0 && 
        fright == 0 && mat[0][0] != k) { 
        cout << "No sub-matrix with sum " << k << " exists"; 
        return; 
    } 

    // Print final values 

    cout << "(Top, Left): "
         << "(" << fup << ", " << fleft 
         << ")" << endl; 

    cout << "(Bottom, Right): "
         << "(" << fdown << ", " << fright 
         << ")" << endl; 

    for (int j = fup; j <= fdown; j++) { 
        for (int i = fleft; i <= fright; i++) 
            cout << mat[j][i] << " "; 
        cout << endl; 
    } 
} 

// Driver program to test above 
int main() 
{ 
    int mat[][MAX] = { { 1, 7, -6, 5 }, 
                       { -8, 6, 7, -2 }, 
                       { 10, -15, 3, 2 }, 
                       { -5, 2, 0, 9 } }; 

    int row = 4, col = 4; 
    int k = 7; 
    sumZeroMatrix(mat, row, col, k); 
    return 0; 
} 

```

## Java

```java

// Java implementation to find  
// the largest area rectangular 
// sub-matrix whose sum is equal to k 
import java.util.*; 

class GFG 
{ 

static int MAX = 100; 
static int start, end; 

// This function basically finds largest 'k' 
// sum subarray in arr[0..n-1]. If 'k' sum 
// doesn't exist, then it returns false. Else 
// it returns true and sets starting and 
// ending indexes as start and end. 
static boolean sumEqualToK(int arr[], int n, int k) 
{ 
    // unordered_map 'um' implemented 
    // as hash table 
    HashMap<Integer,Integer> um =  
    new HashMap<Integer,Integer>(); 

    int sum = 0, maxLen = 0; 

    // traverse the given array 
    for (int i = 0; i < n; i++) 
    { 

        // accumulate sum 
        sum += arr[i]; 

        // when subarray starts from index '0' 
        // update maxLength and start and end points 
        if (sum == k) 
        { 
            maxLen = i + 1; 
            start = 0; 
            end = i; 
        } 

        // make an entry for 'sum' if it is 
        // not present in 'um' 
        if (!um.containsKey(sum)) 
            um.put(sum, i); 

        // check if 'sum-k' is present in 'um' 
        // or not 
        if (um.containsKey(sum - k))  
        { 

            // update maxLength and start and end points 
            if (maxLen < (i - um.get(sum - k)))  
            { 
                maxLen = i - um.get(sum - k); 
                start = um.get(sum - k) + 1; 
                end = i; 
            } 
        } 
    } 

    // Return true if maximum length is non-zero 
    return (maxLen != 0); 
} 

// function to find the largest area rectangular 
// sub-matrix whose sum is equal to k 
static void sumZeroMatrix(int mat[][], int row,  
                            int col, int k) 
{ 
    // Variables to store the temporary values 
    int []temp = new int[row]; 
    int area; 
    boolean sum = false; 

    // Variables to store the final output 
    int fup = 0, fdown = 0, fleft = 0, fright = 0; 
    int maxArea = Integer.MIN_VALUE; 

    // Set the left column 
    for (int left = 0; left < col; left++) 
    { 

        // Initialize all elements of temp as 0 
        temp = memset(temp, 0); 

        // Set the right column for the left column 
        // set by outer loop 
        for (int right = left; right < col; right++) 
        { 
            // Calculate sum between current left 
            // and right column for every row 'i' 
            for (int i = 0; i < row; i++) 
                temp[i] += mat[i][right]; 

            // Find largest subarray with 'k' sum in 
            // temp[]. The sumEqualToK() function also 
            // sets values of 'up' and 'down;'. So 
            // if 'sum' is true then rectangle exists between 
            // (up, left) and (down, right) which are the 
            // boundary values. 
            sum = sumEqualToK(temp, row, k); 
            area = (end - start + 1) * (right - left + 1); 

            // Compare no. of elements with previous 
            // no. of elements in sub-Matrix. 
            // If new sub-matrix has more elements 
            // then update maxArea and final boundaries 
            // like fup, fdown, fleft, fright 
            if (sum && maxArea < area)  
            { 
                fup = start; 
                fdown = end; 
                fleft = left; 
                fright = right; 
                maxArea = area; 
            } 
        } 
    } 

    // If there is no change in boundaries 
    // than check if mat[0][0] equals 'k' 
    // If it is not equal to 'k' then print 
    // that no such k-sum sub-matrix exists 
    if (fup == 0 && fdown == 0 && fleft == 0 && 
        fright == 0 && mat[0][0] != k) 
    { 
        System.out.print("No sub-matrix with sum " 
                        + k + " exists"); 
        return; 
    } 

    // Print final values 
    System.out.print("(Top, Left): "
        + "(" + fup+ ", " + fleft 
        + ")" +"\n"); 

    System.out.print("(Bottom, Right): "
        + "(" + fdown+ ", " + fright 
        + ")" +"\n"); 

    for (int j = fup; j <= fdown; j++) 
    { 
        for (int i = fleft; i <= fright; i++) 
            System.out.print(mat[j][i] + " "); 
        System.out.println(); 
    } 
} 
static int[] memset(int []arr, int val) 
{ 
    for(int i = 0; i < arr.length; i++) 
        arr[i] = val; 
    return arr; 
} 

// Driver code 
public static void main(String[] args) 
{ 
    int mat[][] = { { 1, 7, -6, 5 }, 
                    { -8, 6, 7, -2 }, 
                    { 10, -15, 3, 2 }, 
                    { -5, 2, 0, 9 } }; 

    int row = 4, col = 4; 
    int k = 7; 
    sumZeroMatrix(mat, row, col, k); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

## C#

```cs

// C# implementation to find  
// the largest area rectangular 
// sub-matrix whose sum is equal to k 
using System; 
using System.Collections.Generic; 

class GFG 
{ 

static int MAX = 100; 
static int start, end; 

// This function basically finds largest 'k' 
// sum subarray in arr[0..n-1]. If 'k' sum 
// doesn't exist, then it returns false. Else 
// it returns true and sets starting and 
// ending indexes as start and end. 
static bool sumEqualToK(int []arr, int n, int k) 
{ 
    // unordered_map 'um' implemented 
    // as hash table 
    Dictionary<int,int> um =  
    new Dictionary<int,int>(); 

    int sum = 0, maxLen = 0; 

    // traverse the given array 
    for (int i = 0; i < n; i++) 
    { 

        // accumulate sum 
        sum += arr[i]; 

        // when subarray starts from index '0' 
        // update maxLength and start and end points 
        if (sum == k) 
        { 
            maxLen = i + 1; 
            start = 0; 
            end = i; 
        } 

        // make an entry for 'sum' if it is 
        // not present in 'um' 
        if (!um.ContainsKey(sum)) 
            um.Add(sum, i); 

        // check if 'sum-k' is present in 'um' 
        // or not 
        if (um.ContainsKey(sum - k))  
        { 

            // update maxLength and start and end points 
            if (maxLen < (i - um[sum - k]))  
            { 
                maxLen = i - um[sum - k]; 
                start = um[sum - k] + 1; 
                end = i; 
            } 
        } 
    } 

    // Return true if maximum length is non-zero 
    return (maxLen != 0); 
} 

// function to find the largest area rectangular 
// sub-matrix whose sum is equal to k 
static void sumZeroMatrix(int [,]mat, int row,  
                            int col, int k) 
{ 
    // Variables to store the temporary values 
    int []temp = new int[row]; 
    int area; 
    bool sum = false; 

    // Variables to store the readonly output 
    int fup = 0, fdown = 0, fleft = 0, fright = 0; 
    int maxArea = int.MinValue; 

    // Set the left column 
    for (int left = 0; left < col; left++) 
    { 

        // Initialize all elements of temp as 0 
        temp = memset(temp, 0); 

        // Set the right column for the left column 
        // set by outer loop 
        for (int right = left; right < col; right++) 
        { 
            // Calculate sum between current left 
            // and right column for every row 'i' 
            for (int i = 0; i < row; i++) 
                temp[i] += mat[i, right]; 

            // Find largest subarray with 'k' sum in 
            // []temp. The sumEqualToK() function also 
            // sets values of 'up' and 'down;'. So 
            // if 'sum' is true then rectangle exists between 
            // (up, left) and (down, right) which are the 
            // boundary values. 
            sum = sumEqualToK(temp, row, k); 
            area = (end - start + 1) * (right - left + 1); 

            // Compare no. of elements with previous 
            // no. of elements in sub-Matrix. 
            // If new sub-matrix has more elements 
            // then update maxArea and readonly boundaries 
            // like fup, fdown, fleft, fright 
            if (sum && maxArea < area)  
            { 
                fup = start; 
                fdown = end; 
                fleft = left; 
                fright = right; 
                maxArea = area; 
            } 
        } 
    } 

    // If there is no change in boundaries 
    // than check if mat[0,0] equals 'k' 
    // If it is not equal to 'k' then print 
    // that no such k-sum sub-matrix exists 
    if (fup == 0 && fdown == 0 && fleft == 0 && 
        fright == 0 && mat[0, 0] != k) 
    { 
        Console.Write("No sub-matrix with sum "
                        + k + " exists"); 
        return; 
    } 

    // Print readonly values 
    Console.Write("(Top, Left): "
        + "(" + fup+ ", " + fleft 
        + ")" +"\n"); 

    Console.Write("(Bottom, Right): "
        + "(" + fdown+ ", " + fright 
        + ")" +"\n"); 

    for (int j = fup; j <= fdown; j++) 
    { 
        for (int i = fleft; i <= fright; i++) 
            Console.Write(mat[j, i] + " "); 
        Console.WriteLine(); 
    } 
} 
static int[] memset(int []arr, int val) 
{ 
    for(int i = 0; i < arr.Length; i++) 
        arr[i] = val; 
    return arr; 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    int [,]mat = { { 1, 7, -6, 5 }, 
                    { -8, 6, 7, -2 }, 
                    { 10, -15, 3, 2 }, 
                    { -5, 2, 0, 9 } }; 

    int row = 4, col = 4; 
    int k = 7; 
    sumZeroMatrix(mat, row, col, k); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

**输出**：

```
(Top, Left): (0, 1)
(Bottom, Right): (2, 3)
7 -6 5 
6 7 -2 
-15 3 2 

```

**时间复杂度**：O（n ^ 3）。

**辅助空间**：`O(n)`。



* * *

* * *



