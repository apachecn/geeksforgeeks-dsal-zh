# 计算总数小于给定值的三元组

> 原文： [https://www.geeksforgeeks.org/count-triplets-with-sum-smaller-that-a-given-value/](https://www.geeksforgeeks.org/count-triplets-with-sum-smaller-that-a-given-value/)

给定一个由不同整数组成的数组和一个求和值。 查找总和小于给定总和值的三元组的数量。 预期时间复杂度为 `O(n^2)`。

**示例**：

```
Input : arr[] = {-2, 0, 1, 3}
        sum = 2.
Output : 2
Explanation :  Below are triplets with sum less than 2
               (-2, 0, 1) and (-2, 0, 3) 

Input : arr[] = {5, 1, 3, 4, 7}
        sum = 12.
Output : 4
Explanation :  Below are triplets with sum less than 12
               (1, 3, 4), (1, 3, 5), (1, 3, 7) and 
               (1, 4, 5)
```



一个**简单解决方案**是运行三个循环，一个接一个地考虑所有三元组。 对于每个三元组，如果三元组的总和小于给定的总和，则比较总和和增量计数。

## C++ 

```cpp

// A Simple C++ program to count triplets with sum smaller 
// than a given value 
#include<bits/stdc++.h> 
using namespace std; 

int countTriplets(int arr[], int n, int sum) 
{ 
    // Initialize result 
    int ans = 0; 

    // Fix the first element as A[i] 
    for (int i = 0; i < n-2; i++) 
    { 
       // Fix the second element as A[j] 
       for (int j = i+1; j < n-1; j++) 
       { 
           // Now look for the third number 
           for (int k = j+1; k < n; k++) 
               if (arr[i] + arr[j] + arr[k] < sum) 
                   ans++; 
       } 
    } 

    return ans; 
} 

// Driver program 
int main() 
{ 
    int arr[] = {5, 1, 3, 4, 7}; 
    int n = sizeof arr / sizeof arr[0]; 
    int sum = 12; 
    cout << countTriplets(arr, n, sum) << endl; 
    return 0; 
} 

```

## Java

```
// A Simple Java program to count triplets with sum smaller 
// than a given value 
  
class Test 
{ 
    static int arr[] = new int[]{5, 1, 3, 4, 7}; 
      
    static int countTriplets(int n, int sum) 
    { 
        // Initialize result 
        int ans = 0; 
       
        // Fix the first element as A[i] 
        for (int i = 0; i < n-2; i++) 
        { 
           // Fix the second element as A[j] 
           for (int j = i+1; j < n-1; j++) 
           { 
               // Now look for the third number 
               for (int k = j+1; k < n; k++) 
                   if (arr[i] + arr[j] + arr[k] < sum) 
                       ans++; 
           } 
        } 
       
        return ans; 
    } 
      
    // Driver method to test the above function 
    public static void main(String[] args)  
    { 
        int sum = 12;  
        System.out.println(countTriplets(arr.length, sum)); 
    } 
}
```

## Python 3

```
# A Simple Python 3 program to count triplets with sum smaller 
# than a given value 
#include<bits/stdc++.h> 
def countTriplets(arr, n, sum): 
  
    # Initialize result 
    ans = 0
  
    # Fix the first element as A[i] 
    for i in range( 0 ,n-2): 
      
        # Fix the second element as A[j] 
        for j in range( i+1 ,n-1): 
      
            # Now look for the third number 
            for k in range( j+1, n): 
                if (arr[i] + arr[j] + arr[k] < sum): 
                    ans+=1
      
    return ans 
  
# Driver program 
arr = [5, 1, 3, 4, 7] 
n = len(arr) 
sum = 12
print(countTriplets(arr, n, sum)) 
  
#Contributed by Smitha
```

## C#

```
// A Simple C# program to count triplets with sum smaller 
// than a given value 
   
using System; 
class Test 
{ 
    static int[] arr = new int[]{5, 1, 3, 4, 7}; 
       
    static int countTriplets(int n, int sum) 
    { 
        // Initialize result 
        int ans = 0; 
        
        // Fix the first element as A[i] 
        for (int i = 0; i < n-2; i++) 
        { 
           // Fix the second element as A[j] 
           for (int j = i+1; j < n-1; j++) 
           { 
               // Now look for the third number 
               for (int k = j+1; k < n; k++) 
                   if (arr[i] + arr[j] + arr[k] < sum) 
                       ans++; 
           } 
        } 
        
        return ans; 
    } 
       
    // Driver method to test the above function 
    public static void Main()  
    { 
        int sum = 12;  
        Console.Write(countTriplets(arr.Length, sum)); 
    } 
}
```

输出：

```
4
```

上述解决方案的时间复杂度为`O(n ^ 3)`。 一个有效的解决方案可以通过先对数组进行排序，然后在循环中使用此方法的方法 1，来计算`O(n ^ 2)`中的三元组。

```
1) Sort the input array in increasing order.
2) Initialize result as 0.
3) Run a loop from i = 0 to n-2.  An iteration of this loop finds all
   triplets with arr[i] as first element.
     a) Initialize other two elements as corner elements of subarray
        arr[i+1..n-1], i.e., j = i+1 and k = n-1
     b) Move j and k toward each other until they meet, i.e., while (j = sum), then do k--

            // Else for current i and j, there can (k-j) possible third elements
            // that satisfy the constraint.
            (ii) Else Do ans += (k - j) followed by j++ 
```

以下是上述想法的实现。

## C++

```
// C++ program to count triplets with sum smaller than a given value 
#include<bits/stdc++.h> 
using namespace std; 
  
int countTriplets(int arr[], int n, int sum) 
{ 
    // Sort input array 
    sort(arr, arr+n); 
  
    // Initialize result 
    int ans = 0; 
  
    // Every iteration of loop counts triplet with 
    // first element as arr[i]. 
    for (int i = 0; i < n - 2; i++) 
    { 
        // Initialize other two elements as corner elements 
        // of subarray arr[j+1..k] 
        int j = i + 1, k = n - 1; 
  
        // Use Meet in the Middle concept 
        while (j < k) 
        { 
            // If sum of current triplet is more or equal, 
            // move right corner to look for smaller values 
            if (arr[i] + arr[j] + arr[k] >= sum) 
                k--; 
  
            // Else move left corner 
            else
            { 
                // This is important. For current i and j, there 
                // can be total k-j third elements. 
                ans += (k - j); 
                j++; 
            } 
        } 
    } 
    return ans; 
} 
  
// Driver program 
int main() 
{ 
    int arr[] = {5, 1, 3, 4, 7}; 
    int n = sizeof arr / sizeof arr[0]; 
    int sum = 12; 
    cout << countTriplets(arr, n, sum) << endl; 
    return 0; 
}
```

## Java

```
// A Simple Java program to count triplets with sum smaller 
// than a given value 
  
import java.util.Arrays; 
  
class Test 
{ 
    static int arr[] = new int[]{5, 1, 3, 4, 7}; 
      
    static int countTriplets(int n, int sum) 
    { 
        // Sort input array 
        Arrays.sort(arr); 
       
        // Initialize result 
        int ans = 0; 
       
        // Every iteration of loop counts triplet with 
        // first element as arr[i]. 
        for (int i = 0; i < n - 2; i++) 
        { 
            // Initialize other two elements as corner elements 
            // of subarray arr[j+1..k] 
            int j = i + 1, k = n - 1; 
       
            // Use Meet in the Middle concept 
            while (j < k) 
            { 
                // If sum of current triplet is more or equal, 
                // move right corner to look for smaller values 
                if (arr[i] + arr[j] + arr[k] >= sum) 
                    k--; 
       
                // Else move left corner 
                else
                { 
                    // This is important. For current i and j, there 
                    // can be total k-j third elements. 
                    ans += (k - j); 
                    j++; 
                } 
            } 
        } 
        return ans; 
    } 
      
    // Driver method to test the above function 
    public static void main(String[] args)  
    { 
        int sum = 12;  
        System.out.println(countTriplets(arr.length, sum)); 
    } 
}
```

## Python3

```
# Python3 program to count triplets with  
# sum smaller than a given value  
  
  
# Function to count triplets with sum smaller 
# than a given value          
def countTriplets(arr,n,sum): 
      
    # Sort input array 
    arr.sort() 
      
    # Initialize result  
    ans = 0
      
    # Every iteration of loop counts triplet with  
    # first element as arr[i]. 
    for i in range(0,n-2): 
          
        # Initialize other two elements as corner elements  
        # of subarray arr[j+1..k]  
        j = i + 1
        k = n-1
  
        # Use Meet in the Middle concept  
        while(j < k): 
              
            # If sum of current triplet is more or equal,  
            # move right corner to look for smaller values 
            if (arr[i]+arr[j]+arr[k] >=sum): 
                k = k-1
              
            # Else move left corner  
            else: 
                  
                # This is important. For current i and j, there  
                # can be total k-j third elements.  
                ans += (k - j) 
                j = j+1
      
    return ans 
  
# Driver program  
if __name__=='__main__': 
    arr = [5, 1, 3, 4, 7]  
    n = len(arr)  
    sum = 12
    print(countTriplets(arr, n, sum))  
      
# This code is contributed by  
# Yatin Gupta
```

## C#

```
// A Simple C# program to count  
// triplets with sum smaller 
// than a given value 
using System; 
  
class GFG 
{ 
    static int []arr = new int[]{5, 1, 3, 4, 7}; 
      
    static int countTriplets(int n, int sum) 
    { 
        // Sort input array 
        Array.Sort(arr); 
      
        // Initialize result 
        int ans = 0; 
      
        // Every iteration of loop 
        // counts triplet with 
        // first element as arr[i]. 
        for (int i = 0; i < n - 2; i++) 
        { 
            // Initialize other two  
            // elements as corner elements 
            // of subarray arr[j+1..k] 
            int j = i + 1, k = n - 1; 
      
            // Use Meet in the Middle concept 
            while (j < k) 
            { 
                // If sum of current triplet  
                // is more or equal, move right  
                // corner to look for smaller values 
                if (arr[i] + arr[j] + arr[k] >= sum) 
                    k--; 
      
                // Else move left corner 
                else
                { 
                    // This is important. For  
                    // current i and j, there 
                    // can be total k-j third elements. 
                    ans += (k - j); 
                    j++; 
                } 
            } 
        } 
        return ans; 
    } 
      
    // Driver Code 
    public static void Main()  
    { 
        int sum = 12;  
        Console.Write(countTriplets(arr.Length, sum)); 
    } 
} 
  
// This code is contributed by Smitha
```

输出：

```
4
```

感谢 Gaurav Ahirwar 提出了此解决方案。