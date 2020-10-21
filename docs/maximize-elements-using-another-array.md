# 使用另一个数组最大化元素

> 原文： [https://www.geeksforgeeks.org/maximize-elements-using-another-array/](https://www.geeksforgeeks.org/maximize-elements-using-another-array/)

给定两个大小为`n`的数组，请使用第二个数组中的元素来最大化第一个数组，以使形成的新数组包含两个数组中`n`个最大但唯一的元素，从而赋予第二个数组优先级（第二个数组的所有元素都出现在第一个数组之前 ）。 元素的出现顺序在输出中与在输入中保持相同。

**示例**：

> 输入：
> 
> `arr1[] = {2, 4, 3}`
> 
> `arr2[] = {5, 6, 1}`
> 
> 输出：`5 6 4`
> 
> 由于 5、6 和 4 是来自两个数组的最大元素，给第二个数组更高的优先级。 元素的顺序在输出中与在输入中相同。
> 
> 输入：
> 
> `arr1[] = {7, 4, 8, 0, 1}`
> 
> `arr2[] = {9, 7, 2, 3, 6}`
> 
> 输出：`9 7 6 4 8`


**方法**：我们创建一个大小为`2 * n`的辅助数组，并将第二个数组的元素存储在该辅助数组中，然后将第一个数组的元素存储在其中。 之后，我们将按降序对辅助数组进行排序。 为了保持元素根据输入数组的顺序，我们将使用哈希表。 我们将在哈希表中存储辅助数组的第 1 个最大的唯一元素。 现在，我们遍历第二个数组并将第二个数组的元素存储在哈希表中的辅助数组中。 同样，我们将遍历第一个数组并存储哈希表中存在的元素。 这样，我们可以从辅助数组中的两个数组中获得`n`个唯一且最大的元素，同时保持元素的出现顺序相同。

下面是上述方法的实现：

## C++ 

```cpp

// CPP program to print the maximum elements 
// giving second array higher priority 
#include <bits/stdc++.h> 
using namespace std; 

// Compare function used to sort array  
// in decreasing order 
bool compare(int a, int b) 
{ 
    return a > b; 
} 

// Function to maximize array elements 
void maximizeArray(int arr1[], int arr2[], 
                                   int n) 
{ 
    // auxiliary array arr3 to store  
    // elements of arr1 & arr2 
    int arr3[2*n], k = 0; 
    for (int i = 0; i < n; i++)  
        arr3[k++] = arr1[i]; 
    for (int i = 0; i < n; i++) 
        arr3[k++] = arr2[i]; 

    // hash table to store n largest 
    // unique elements 
    unordered_set<int> hash; 

    // sorting arr3 in decreasing order 
    sort(arr3, arr3 + 2 * n, compare); 

    // finding n largest unique elements 
    // from arr3 and storing in hash 
    int i = 0; 
    while (hash.size() != n) { 

        // if arr3 element not present in hash, 
        // then store this element in hash 
        if (hash.find(arr3[i]) == hash.end())  
            hash.insert(arr3[i]); 

        i++; 
    } 

    // store that elements of arr2 in arr3 
    // that are present in hash 
    k = 0; 
    for (int i = 0; i < n; i++) { 

        // if arr2 element is present in hash, 
        // store it in arr3 
        if (hash.find(arr2[i]) != hash.end()) { 
            arr3[k++] = arr2[i]; 
            hash.erase(arr2[i]); 
        } 
    } 

    // store that elements of arr1 in arr3 
    // that are present in hash 
    for (int i = 0; i < n; i++) { 

        // if arr1 element is present in hash, 
        // store it in arr3 
        if (hash.find(arr1[i]) != hash.end()) { 
            arr3[k++] = arr1[i]; 
            hash.erase(arr1[i]); 
        } 
    } 

    // copying 1st n elements of arr3 to arr1 
    for (int i = 0; i < n; i++)  
        arr1[i] = arr3[i];     
} 

// Function to print array elements 
void printArray(int arr[], int n) 
{ 
    for (int i = 0; i < n; i++)  
        cout << arr[i] << " ";     
    cout << endl; 
} 

// Driver Code 
int main() 
{ 
    int array1[] = { 7, 4, 8, 0, 1 }; 
    int array2[] = { 9, 7, 2, 3, 6 }; 
    int size = sizeof(array1) / sizeof(array1[0]); 
    maximizeArray(array1, array2, size); 
    printArray(array1, size); 
} 

```

## Java

```
// Java program to print the maximum elements 
// giving second array higher priority 
import java.util.*; 
  
class GFG  
{ 
  
// Function to maximize array elements 
static void maximizeArray(int[] arr1,int[] arr2) 
{ 
    // auxiliary array arr3 to store  
    // elements of arr1 & arr2 
    int arr3[] = new int[10];  
    for(int i = 0; i < arr3.length; i++) 
    { 
        //arr2 has high priority 
        arr3[i] = 0; 
    } 
      
    // Arraylist to store n largest 
    // unique elements 
    ArrayList<Integer> al = new ArrayList<Integer>(); 
      
    for(int i = 0; i < arr2.length; i++) 
    { 
        if(arr3[arr2[i]] == 0)  
        {  
            // to avoid repetition of digits of arr2 in arr3 
            arr3[arr2[i]] = 2; 
              
            // simultaneously setting arraylist to  
            // preserve order of arr2 and arr3 
            al.add(arr2[i]);  
        } 
    } 
      
    for(int i = 0; i < arr1.length; i++) 
    { 
        if(arr3[arr1[i]] == 0) 
        { 
            // if digit is already present in arr2 
            // then priority is arr2 
            arr3[arr1[i]] = 1; 
              
            // simultaneously setting arraylist to 
            // preserve order of arr1 
            al.add(arr1[i]);  
        } 
    } 
  
    // to get only highest n elements(arr2+arr1) 
    // and remove others from arraylist 
    int count = 0; 
    for(int j = 9; j >= 0; j--) 
    { 
        if(count < arr1.length &  
          (arr3[j] == 2 || arr3[j] == 1)) 
        { 
            // to not allow those elements  
            // which are absent in both arrays 
            count++; 
        } 
        else
        { 
            al.remove(Integer.valueOf(j)); 
        } 
    } 
  
    int i = 0; 
    for(int x:al) 
    { 
        arr1[i++] = x; 
    } 
} 
  
// Function to print array elements 
static void printArray(int[] arr) 
{ 
    for(int x:arr) 
    { 
        System.out.print(x + " "); 
    } 
} 
  
// Driver Code 
public static void main(String args[]) 
{ 
    int arr1[] = {7, 4, 8, 0, 1}; 
    int arr2[] = {9, 7, 2, 3, 6}; 
    maximizeArray(arr1,arr2); 
    printArray(arr1); 
} 
} 
  
// This code is contributed by KhwajaBilkhis
```

## Python3

```
# Python3 program to print the maximum elements 
# giving second array higher priority 
  
# Function to maximize array elements 
def maximizeArray(arr1, arr2, n): 
      
    # Auxiliary array arr3 to store 
    # elements of arr1 & arr2 
    arr3 = [0] * (2 * n) 
    k = 0
      
    for i in range(n): 
        arr3[k] = arr1[i] 
        k += 1
          
    for i in range(n): 
        arr3[k] = arr2[i] 
        k += 1
  
    # Hash table to store n largest 
    # unique elements 
    hash = {} 
  
    # Sorting arr3 in decreasing order 
    arr3 = sorted(arr3) 
    arr3 = arr3[::-1] 
  
    # Finding n largest unique elements 
    # from arr3 and storing in hash 
    i = 0
    while (len(hash) != n): 
  
        # If arr3 element not present in hash, 
        # then store this element in hash 
        if (arr3[i] not in hash): 
            hash[arr3[i]] = 1
  
        i += 1
  
    # Store that elements of arr2 in arr3 
    # that are present in hash 
    k = 0
    for i in range(n): 
  
        # If arr2 element is present in  
        # hash, store it in arr3 
        if (arr2[i] in hash): 
            arr3[k] = arr2[i] 
            k += 1
              
            del hash[arr2[i]] 
  
    # Store that elements of arr1 in arr3 
    # that are present in hash 
    for i in range(n): 
  
        # If arr1 element is present  
        # in hash, store it in arr3 
        if (arr1[i] in hash): 
            arr3[k] = arr1[i] 
            k += 1
              
            del hash[arr1[i]] 
  
    # Copying 1st n elements of 
    # arr3 to arr1 
    for i in range(n): 
        arr1[i] = arr3[i] 
  
# Function to prarray elements 
def printArray(arr, n): 
      
    for i in arr: 
        print(i, end = " ") 
          
    print() 
  
# Driver Code 
if __name__ == '__main__': 
      
    array1 = [ 7, 4, 8, 0, 1 ] 
    array2 = [ 9, 7, 2, 3, 6 ] 
    size = len(array1) 
      
    maximizeArray(array1, array2, size) 
    printArray(array1, size) 
      
# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to print the maximum elements 
// giving second array higher priority 
using System; 
using System.Collections.Generic; 
  
class GFG  
{ 
  
// Function to maximize array elements 
static void maximizeArray(int[] arr1, int[] arr2) 
{ 
    // auxiliary array arr3 to store  
    // elements of arr1 & arr2 
    int []arr3 = new int[10];  
    for(int i = 0; i < arr3.Length; i++) 
    { 
        //arr2 has high priority 
        arr3[i] = 0; 
    } 
      
    // Arraylist to store n largest 
    // unique elements 
    List<int> al = new List<int>(); 
      
    for(int i = 0; i < arr2.Length; i++) 
    { 
        if(arr3[arr2[i]] == 0)  
        {  
            // to avoid repetition of digits of arr2 in arr3 
            arr3[arr2[i]] = 2; 
              
            // simultaneously setting arraylist to  
            // preserve order of arr2 and arr3 
            al.Add(arr2[i]);  
        } 
    } 
      
    for(int i = 0; i < arr1.Length; i++) 
    { 
        if(arr3[arr1[i]] == 0) 
        { 
            // if digit is already present in arr2 
            // then priority is arr2 
            arr3[arr1[i]] = 1; 
              
            // simultaneously setting arraylist to 
            // preserve order of arr1 
            al.Add(arr1[i]);  
        } 
    } 
  
    // to get only highest n elements(arr2+arr1) 
    // and remove others from arraylist 
    int count = 0; 
    for(int j = 9; j >= 0; j--) 
    { 
        if(count < arr1.Length &  
        (arr3[j] == 2 || arr3[j] == 1)) 
        { 
            // to not allow those elements  
            // which are absent in both arrays 
            count++; 
        } 
        else
        { 
            al.Remove(j); 
        } 
    } 
  
    int c = 0; 
    foreach(int x in al) 
    { 
        arr1[c++] = x; 
    } 
} 
  
// Function to print array elements 
static void printArray(int[] arr) 
{ 
    foreach(int x in arr) 
    { 
        Console.Write(x + " "); 
    } 
} 
  
// Driver Code 
public static void Main(String []args) 
{ 
    int []arr1 = {7, 4, 8, 0, 1}; 
    int []arr2 = {9, 7, 2, 3, 6}; 
    maximizeArray(arr1, arr2); 
    printArray(arr1); 
} 
} 
  
// This code is contributed by PrinciRaj1992
```

输出：

```
9 7 6 4 8
```

时间复杂度：`O(n * log n)`。