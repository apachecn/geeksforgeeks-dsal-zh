# 安排每对使其彼此相邻所需的最小交换次数

> 原文： [https://www.geeksforgeeks.org/minimum-number-of-swaps-required-for-arranging-pairs-adjacent-to-each-other/](https://www.geeksforgeeks.org/minimum-number-of-swaps-required-for-arranging-pairs-adjacent-to-each-other/)

有`n`对，因此有`2n`个人。 每个人都有一个唯一的数字，范围从 1 到`2n`。 所有这些`2n`个人以大小为`2n`的数组随机排列。 我们也得到了谁是谁的伙伴。 查找安排这些对以使所有对彼此相邻所需的最小交换次数。

例：

```
Input:
n = 3  
pairs[] = {1->3, 2->6, 4->5}  // 1 is partner of 3 and so on
arr[] = {3, 5, 6, 4, 1, 2}

Output: 2
We can get {3, 1, 5, 4, 6, 2} by swapping 5 & 6, and 6 & 1
```

**我们强烈建议您最小化浏览器，然后自己尝试。**

这个想法是从第一个和第二个元素开始，然后重复其余元素。 以下是详细步骤/

```
1) If first and second elements are pair, then simply recur 
   for remaining n-1 pairs and return the value returned by 
   recursive call.

2) If first and second are NOT pair, then there are two ways to 
   arrange. So try both of them return the minimum of two.
   a) Swap second with pair of first and recur for n-1 elements. 
      Let the value returned by recursive call be 'a'.
   b) Revert the changes made by previous step.
   c) Swap first with pair of second and recur for n-1 elements. 
      Let the value returned by recursive call be 'b'.
   d) Revert the changes made by previous step before returning
      control to parent call.
   e) Return 1 + min(a, b)

```

下面是上述算法的实现。

## C++ 

```cpp

// C++ program to find minimum number of swaps required so that 
// all pairs become adjacent. 
#include<bits/stdc++.h> 
using namespace std; 

// This function updates indexes of elements 'a' and 'b' 
void updateindex(int index[], int a, int ai, int b, int bi) 
{ 
    index[a] = ai; 
    index[b] = bi; 
} 

// This function returns minimum number of swaps required to arrange 
// all elements of arr[i..n] become aranged 
int minSwapsUtil(int arr[], int pairs[], int index[], int i, int n) 
{ 
    // If all pairs procesed so no swapping needed return 0 
    if (i > n) return 0; 

    // If current pair is valid so DO NOT DISTURB this pair 
    // and move ahead. 
    if (pairs[arr[i]] == arr[i+1]) 
         return minSwapsUtil(arr, pairs, index, i+2, n); 

    // If we reach here, then arr[i] and arr[i+1] don't form a pair 

    // Swap pair of arr[i] with arr[i+1] and recursively compute 
    // minimum swap required if this move is made. 
    int one = arr[i+1]; 
    int indextwo = i+1; 
    int indexone = index[pairs[arr[i]]]; 
    int two = arr[index[pairs[arr[i]]]]; 
    swap(arr[i+1], arr[indexone]); 
    updateindex(index, one, indexone, two, indextwo); 
    int a = minSwapsUtil(arr, pairs, index, i+2, n); 

    // Backtrack to previous configuration. Also restore the 
    // previous indices, of one and two 
    swap(arr[i+1], arr[indexone]); 
    updateindex(index, one, indextwo, two, indexone); 
    one = arr[i], indexone = index[pairs[arr[i+1]]]; 

    // Now swap arr[i] with pair of arr[i+1] and recursively 
    // compute minimum swaps required for the subproblem 
    // after this move 
    two = arr[index[pairs[arr[i+1]]]], indextwo = i; 
    swap(arr[i], arr[indexone]); 
    updateindex(index, one, indexone, two, indextwo); 
    int b = minSwapsUtil(arr, pairs, index, i+2, n); 

    // Backtrack to previous configuration.  Also restore 
    // the previous indices, of one and two 
    swap(arr[i], arr[indexone]); 
    updateindex(index, one, indextwo, two, indexone); 

    // Return minimum of two cases 
    return 1 + min(a, b); 
} 

// Returns minimum swaps required 
int minSwaps(int n, int pairs[], int arr[]) 
{ 
    int index[2*n + 1]; // To store indices of array elements 

    // Store index of each element in array index 
    for (int i = 1; i <= 2*n; i++) 
        index[arr[i]] = i; 

    // Call the recursive function 
    return minSwapsUtil(arr, pairs, index, 1, 2*n); 
} 

// Driver program 
int main() 
{ 
    // For simplicity, it is assumed that arr[0] is 
    // not used.  The elements from index 1 to n are 
    // only valid elements 
    int arr[] = {0, 3, 5, 6, 4, 1, 2}; 

    // if (a, b) is pair than we have assigned elements 
    // in array such that pairs[a] = b and pairs[b] = a 
    int pairs[] = {0, 3, 6, 1, 5, 4, 2}; 
    int m = sizeof(arr)/sizeof(arr[0]); 

    int n = m/2;  // Number of pairs n is half of total elements 

    // If there are n elements in array, then 
    // there are n pairs 
    cout << "Min swaps required is " << minSwaps(n, pairs, arr); 
    return 0; 
} 

```

## Java

```java
// Java program to find minimum number 
// of swaps required so that 
// all pairs become adjacent. 
  
class GFG { 
      
// This function updates indexes 
// of elements 'a' and 'b' 
static void updateindex(int index[], int a,  
                     int ai, int b, int bi)  
{ 
    index[a] = ai; 
    index[b] = bi; 
} 
  
// This function returns minimum number 
// of swaps required to arrange 
// all elements of arr[i..n] become aranged 
static int minSwapsUtil(int arr[], int pairs[], 
                     int index[], int i, int n)  
{ 
    // If all pairs procesed so 
    // no swapping needed return 0 
    if (i > n) 
    return 0; 
  
    // If current pair is valid so  
    // DO NOT DISTURB this pair 
    // and move ahead. 
    if (pairs[arr[i]] == arr[i + 1]) 
    return minSwapsUtil(arr, pairs, index, i + 2, n); 
  
    // If we reach here, then arr[i] and 
    // arr[i+1] don't form a pair 
  
    // Swap pair of arr[i] with arr[i+1] 
    // and recursively compute minimum swap 
    // required if this move is made. 
    int one = arr[i + 1]; 
    int indextwo = i + 1; 
    int indexone = index[pairs[arr[i]]]; 
    int two = arr[index[pairs[arr[i]]]]; 
    arr[i + 1] = arr[i + 1] ^ arr[indexone] ^ 
                (arr[indexone] = arr[i + 1]); 
    updateindex(index, one, indexone, two, indextwo); 
    int a = minSwapsUtil(arr, pairs, index, i + 2, n); 
  
    // Backtrack to previous configuration. 
    // Also restore the previous  
    // indices, of one and two 
    arr[i + 1] = arr[i + 1] ^ arr[indexone] ^  
                (arr[indexone] = arr[i + 1]); 
    updateindex(index, one, indextwo, two, indexone); 
    one = arr[i]; 
    indexone = index[pairs[arr[i + 1]]]; 
  
    // Now swap arr[i] with pair of arr[i+1]  
    // and recursively compute minimum swaps 
    // required for the subproblem 
    // after this move 
    two = arr[index[pairs[arr[i + 1]]]]; 
    indextwo = i; 
    arr[i] = arr[i] ^ arr[indexone] ^ (arr[indexone] = arr[i]); 
    updateindex(index, one, indexone, two, indextwo); 
    int b = minSwapsUtil(arr, pairs, index, i + 2, n); 
  
    // Backtrack to previous configuration. Also restore 
    // the previous indices, of one and two 
    arr[i] = arr[i] ^ arr[indexone] ^ (arr[indexone] = arr[i]); 
    updateindex(index, one, indextwo, two, indexone); 
  
    // Return minimum of two cases 
    return 1 + Math.min(a, b); 
} 
  
// Returns minimum swaps required 
static int minSwaps(int n, int pairs[], int arr[])  
{ 
    // To store indices of array elements 
    int index[] = new int[2 * n + 1];  
  
    // Store index of each element in array index 
    for (int i = 1; i <= 2 * n; i++) 
    index[arr[i]] = i; 
  
    // Call the recursive function 
    return minSwapsUtil(arr, pairs, index, 1, 2 * n); 
} 
  
// Driver code 
public static void main(String[] args) { 
      
    // For simplicity, it is assumed that arr[0] is 
    // not used. The elements from index 1 to n are 
    // only valid elements 
    int arr[] = {0, 3, 5, 6, 4, 1, 2}; 
  
    // if (a, b) is pair than we have assigned elements 
    // in array such that pairs[a] = b and pairs[b] = a 
    int pairs[] = {0, 3, 6, 1, 5, 4, 2}; 
    int m = pairs.length; 
  
    // Number of pairs n is half of total elements 
    int n = m / 2;  
  
    // If there are n elements in array, then 
    // there are n pairs 
    System.out.print("Min swaps required is " + 
                      minSwaps(n, pairs, arr)); 
} 
} 
  
// This code is contributed by Anant Agarwal. 
```

## Python3

```py
# Python program to find 
# minimum number of swaps 
# required so that 
# all pairs become adjacent. 
  
# This function updates 
# indexes of elements 'a' and 'b' 
def updateindex(index,a,ai,b,bi): 
  
    index[a] = ai 
    index[b] = bi 
  
   
# This function returns minimum 
# number of swaps required to arrange 
# all elements of arr[i..n] 
# become aranged 
def minSwapsUtil(arr,pairs,index,i,n): 
  
    # If all pairs procesed so 
    # no swapping needed return 0 
    if (i > n): 
        return 0
   
    # If current pair is valid so 
    # DO NOT DISTURB this pair 
    # and move ahead. 
    if (pairs[arr[i]] == arr[i+1]): 
         return minSwapsUtil(arr, pairs, index, i+2, n) 
   
    # If we reach here, then arr[i] 
    # and arr[i+1] don't form a pair 
   
    # Swap pair of arr[i] with 
    # arr[i+1] and recursively compute 
    # minimum swap required 
    # if this move is made. 
    one = arr[i+1] 
    indextwo = i+1
    indexone = index[pairs[arr[i]]] 
    two = arr[index[pairs[arr[i]]]] 
    arr[i+1],arr[indexone]=arr[indexone],arr[i+1] 
  
    updateindex(index, one, indexone, two, indextwo) 
  
    a = minSwapsUtil(arr, pairs, index, i+2, n) 
   
    # Backtrack to previous configuration. 
    # Also restore the 
    # previous indices, 
    # of one and two 
    arr[i+1],arr[indexone]=arr[indexone],arr[i+1] 
    updateindex(index, one, indextwo, two, indexone) 
    one = arr[i] 
    indexone = index[pairs[arr[i+1]]] 
   
    # Now swap arr[i] with pair  
    # of arr[i+1] and recursively 
    # compute minimum swaps 
    # required for the subproblem 
    # after this move 
    two = arr[index[pairs[arr[i+1]]]] 
    indextwo = i 
    arr[i],arr[indexone]=arr[indexone],arr[i] 
    updateindex(index, one, indexone, two, indextwo) 
    b = minSwapsUtil(arr, pairs, index, i+2, n) 
   
    # Backtrack to previous 
    # configuration.  Also restore 
    # 3 the previous indices, 
    # of one and two 
    arr[i],arr[indexone]=arr[indexone],arr[i] 
    updateindex(index, one, indextwo, two, indexone) 
   
    # Return minimum of two cases 
    return 1 + min(a, b) 
  
# Returns minimum swaps required 
def minSwaps(n,pairs,arr): 
  
    index=[] # To store indices of array elements 
    for i in range(2*n+1+1): 
        index.append(0) 
  
    # Store index of each 
    # element in array index 
    for i in range(1,2*n+1): 
        index[arr[i]] = i 
   
    # Call the recursive function 
    return minSwapsUtil(arr, pairs, index, 1, 2*n) 
  
# Driver code 
  
# For simplicity, it is 
# assumed that arr[0] is 
# not used.  The elements 
# from index 1 to n are 
# only valid elements 
arr = [0, 3, 5, 6, 4, 1, 2] 
   
# if (a, b) is pair than 
# we have assigned elements 
# in array such that 
# pairs[a] = b and pairs[b] = a 
pairs= [0, 3, 6, 1, 5, 4, 2] 
m = len(pairs) 
   
n = m//2  # Number of pairs n 
          # is half of total elements 
   
# If there are n  
# elements in array, then 
# there are n pairs 
print("Min swaps required is ",minSwaps(n, pairs, arr)) 
  
# This code is contributed 
# by Anant Agarwal. 
```

## C#

```cs
// C# program to find minimum number 
// of swaps required so that 
// all pairs become adjacent. 
using System; 
  
class GFG { 
  
    // This function updates indexes  
    // of elements 'a' and 'b'  
    public static void updateindex(int[] index, int a, 
                             int ai, int b, int bi) { 
        index[a] = ai; 
        index[b] = bi; 
    } 
  
    // This function returns minimum number  
    // of swaps required to arrange  
    // all elements of arr[i..n] become aranged  
    public static int minSwapsUtil(int[] arr,  
     int[] pairs, int[] index, int i, int n) { 
           
        // If all pairs procesed so  
        // no swapping needed return 0  
        if (i > n) { 
            return 0; 
        } 
  
        // If current pair is valid so  
        // DO NOT DISTURB this pair  
        // and move ahead.  
        if (pairs[arr[i]] == arr[i + 1]) { 
            return minSwapsUtil(arr, pairs,  
                          index, i + 2, n); 
        } 
  
        // If we reach here, then arr[i] and  
        // arr[i+1] don't form a pair  
        // Swap pair of arr[i] with arr[i+1]  
        // and recursively compute minimum swap  
        // required if this move is made.  
        int one = arr[i + 1]; 
          
        int indextwo = i + 1; 
        int indexone = index[pairs[arr[i]]]; 
        int two = arr[index[pairs[arr[i]]]]; 
        arr[i + 1] = arr[i + 1] ^ arr[indexone] ^  
                     (arr[indexone] = arr[i + 1]); 
                       
        updateindex(index, one, indexone, two, indextwo); 
        int a = minSwapsUtil(arr, pairs, index, i + 2, n); 
  
        // Backtrack to previous configuration.  
        // Also restore the previous  
        // indices, of one and two  
        arr[i + 1] = arr[i + 1] ^ arr[indexone] ^  
                     (arr[indexone] = arr[i + 1]); 
                       
        updateindex(index, one, indextwo, two, indexone); 
        one = arr[i]; 
        indexone = index[pairs[arr[i + 1]]]; 
  
        // Now swap arr[i] with pair of arr[i+1]  
        // and recursively compute minimum swaps  
        // required for the subproblem  
        // after this move  
        two = arr[index[pairs[arr[i + 1]]]]; 
        indextwo = i; 
        arr[i] = arr[i] ^ arr[indexone] ^  
                 (arr[indexone] = arr[i]); 
                   
        updateindex(index, one, indexone, two, indextwo); 
        int b = minSwapsUtil(arr, pairs, index, i + 2, n); 
  
        // Backtrack to previous configuration. 
        // Also restore the previous indices, 
        // of one and two  
        arr[i] = arr[i] ^ arr[indexone] ^  
                (arr[indexone] = arr[i]); 
                  
        updateindex(index, one, indextwo, two, indexone); 
  
        // Return minimum of two cases  
        return 1 + Math.Min(a, b); 
    } 
  
    // Returns minimum swaps required  
    public static int minSwaps(int n, int[] pairs, int[] arr) { 
        // To store indices of array elements  
        int[] index = new int[2 * n + 1]; 
  
        // Store index of each element in array index  
        for (int i = 1; i <= 2 * n; i++) { 
            index[arr[i]] = i; 
        } 
  
        // Call the recursive function  
        return minSwapsUtil(arr, pairs, index, 1, 2 * n); 
    } 
  
// Driver code  
public static void Main(string[] args) 
{ 
  
    // For simplicity, it is assumed that arr[0] is  
    // not used. The elements from index 1 to n are  
    // only valid elements  
    int[] arr = new int[]  
    { 
        0, 
        3, 
        5, 
        6, 
        4, 
        1, 
        2 
    }; 
  
    // if (a, b) is pair than we have assigned elements  
    // in array such that pairs[a] = b and pairs[b] = a  
    int[] pairs = new int[]  
    { 
        0, 
        3, 
        6, 
        1, 
        5, 
        4, 
        2 
    }; 
      
    int m = pairs.Length; 
  
    // Number of pairs n is half of total elements  
    int n = m / 2; 
  
    // If there are n elements in array, then  
    // there are n pairs  
    Console.Write("Min swaps required is " + 
                   minSwaps(n, pairs, arr)); 
} 
} 
  
// This code is contributed by Shrikant13 
```

输出：

```
Min swaps required is 2
```

感谢 Gaurav Ahirwar 提供了上述解决方案。