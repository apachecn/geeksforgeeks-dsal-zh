# 从两个数组最大化唯一对

> 原文： [https://www.geeksforgeeks.org/maximizing-unique-pairs-two-arrays/](https://www.geeksforgeeks.org/maximizing-unique-pairs-two-arrays/)

给定两个大小为`N`的数组，使用它们的元素形成最大对数，一个元素来自第一个数组，第二个元素来自第二个数组，这样每个数组中的元素最多使用一次，并且用于形成一对的所选元素之间的绝对差，小于或等于给定元素`K`。

**示例**：

```
Input : a[] = {3, 4, 5, 2, 1}
        b[] = {6, 5, 4, 7, 15}
          k = 3
Output : 4
The maximum number of pairs that can be formed
using the above 2 arrays is 4 and the corresponding
pairs are [1, 4], [2, 5], [3, 6], [4, 7], we can't 
pair the remaining elements.
Other way of pairing under given constraint is 
[2, 5], [3, 6], [4, 4], but count of pairs here
is 3 which is less than the result 4.

```



**简单方法**：通过举几个例子，我们可以观察到如果对两个数组都进行排序。 然后，通过为每个元素选择最接近的可行元素，我们得到最佳答案。

在这种方法中，我们首先对两个数组都进行排序，然后将第一个数组中的每个元素与第二个数组中的每个元素比较可能的一对，如果有可能形成一对，我们就组成该对，并对第一个数组的下一个元素检查下一个可能的偶对。

## C++ 

```cpp

// C++ implementation of above approach 
#include <bits/stdc++.h> 
#define ll long long int 
using namespace std; 

// Returns count of maximum pairs that caan 
// be formed from a[] and b[] under given 
// constraints. 
ll findMaxPairs(ll a[], ll b[], ll n, ll k) 
{ 
    sort(a, a+n); // Sorting the first array. 
    sort(b, b+n); // Sorting the second array. 

    // To keep track of visited elements of b[] 
    bool flag[n]; 
    memset(flag, false, sizeof(flag)); 

    // For every element of a[], find a pair 
    // for it and break as soon as a pair is 
    // found. 
    int result = 0; 
    for (int i=0; i<n; i++) 
    { 
        for (int j=0; j<n; j++) 
        { 
            if (abs(a[i]-b[j])<=k && flag[j]==false) 
            { 
                // Increasing the count if a pair is formed. 
                result++; 

                /* Making the corresponding flag array 
                   element as 1 indicating the element 
                   in the second array element has 
                   been used. */
                flag[j] = true; 

                // We break the loop to make sure an 
                // element of a[] is used only once. 
                break; 
            } 
        } 
    } 
    return result; 
} 

// Driver code 
int main() 
{ 
    ll a[] = {10, 15, 20}, b[] = {17, 12, 24}; 
    int n = sizeof(a)/sizeof(a[0]); 
    int k = 3; 
    cout << findMaxPairs(a, b, n, k); 
    return 0; 
} 

```

## Java

```java

// Java implementation of above approach 
import java.util.*; 

class solution 
{ 

// Returns count of maximum pairs that caan 
// be formed from a[] and b[] under given 
// constraints. 
static int findMaxPairs(int a[], int b[], int n, int k) 
{ 
    Arrays.sort(a); // Sorting the first array. 
    Arrays.sort(b); // Sorting the second array. 

    // To keep track of visited elements of b[] 
    boolean []flag = new boolean[n]; 
    Arrays.fill(flag,false); 

    // For every element of a[], find a pair 
    // for it and break as soon as a pair is 
    // found. 
    int result = 0; 
    for (int i=0; i<n; i++) 
    { 
        for (int j=0; j<n; j++) 
        { 
            if (Math.abs(a[i]-b[j])<=k && flag[j]==false) 
            { 
                // Increasing the count if a pair is formed. 
                result++; 

                /* Making the corresponding flag array 
                element as 1 indicating the element 
                in the second array element has 
                been used. */
                flag[j] = true; 

                // We break the loop to make sure an 
                // element of a[] is used only once. 
                break; 
            } 
        } 
    } 
    return result; 
} 

// Driver code 
public static void main(String args[]) 
{ 
    int[] a = {10, 15, 20}; 
    int[] b = {17, 12, 24}; 
    int n = a.length; 
    int k = 3; 
    System.out.println(findMaxPairs(a, b, n, k)); 

} 
} 

// This code is contributed by 
// Shashank_Sharma 

```

## Python 3

```py

# Returns count of maximum pairs  
# that can be formed from a[] and  
# b[] under given constraints. 
def findMaxPairs(a, b, n, k): 

    a.sort() # Sorting the first array. 
    b.sort() # Sorting the second array. 

    # To keep track of visited 
    # elements of b[] 
    flag = [False] * n 

    # For every element of a[], find  
    # a pair for it and break as soon  
    # as a pair is found. 
    result = 0
    for i in range(n): 
        for j in range(n): 
            if (abs(a[i] - b[j]) <= k and 
                         flag[j] == False): 

                # Increasing the count if  
                # a pair is formed. 
                result += 1

                ''' Making the corresponding flag array 
                element as 1 indicating the element 
                in the second array element has 
                been used. '''
                flag[j] = True

                # We break the loop to make sure an 
                # element of a[] is used only once. 
                break
    return result 

# Driver code 
if __name__ == "__main__": 
    a = [10, 15, 20] 
    b = [17, 12, 24] 
    n = len(a) 
    k = 3
    print(findMaxPairs(a, b, n, k)) 

# This code is contributed 
# by ChitraNayal 

```

## C# 

```cs

// C# implementation of above approach 
using System;  

class GFG  
{  

    // Returns count of maximum pairs that caan  
    // be formed from a[] and b[] under given  
    // constraints.  
    static int findMaxPairs(int []a, int []b,  
                                int n, int k)  
    {  
        Array.Sort(a); // Sorting the first array.  
        Array.Sort(b); // Sorting the second array.  

        // To keep track of visited elements of b[]  
        bool []flag = new bool[n];  

        //Arrays.fill(flag,false);  

        // For every element of a[], find a pair  
        // for it and break as soon as a pair is  
        // found.  
        int result = 0;  
        for (int i = 0; i < n; i++)  
        {  
            for (int j = 0; j < n; j++)  
            {  
                if (Math.Abs(a[i] - b[j]) <= k && flag[j] == false)  
                {  
                    // Increasing the count if a pair is formed.  
                    result++;  

                    /* Making the corresponding flag array  
                    element as 1 indicating the element  
                    in the second array element has  
                    been used. */
                    flag[j] = true;  

                    // We break the loop to make sure an  
                    // element of a[] is used only once.  
                    break;  
                }  
            }  
        }  
        return result;  
    }  

    // Driver code  
    public static void Main()  
    {  
        int[] a = {10, 15, 20};  
        int[] b = {17, 12, 24};  
        int n = a.Length;  
        int k = 3;  
        Console.WriteLine(findMaxPairs(a, b, n, k));  
    }  
}  

// This code is contributed by Rajput-Ji 

```

**输出**：

```
2

```

**时间复杂度**：`O(n^2)`。

**辅助空间**：`O(n)`。

**高效方法**：在这种方法中，我们不检查所有可能的对组合，而是通过使用 2 指针方法仅检查对的可行组合来优化代码。

## C++

```cpp

#include <bits/stdc++.h> 
#define ll long long int 
using namespace std; 

// Returns count of maximum pairs that caan 
// be formed from a[] and b[] under given 
// constraints. 
ll findMaxPairs(ll a[], ll b[], ll n, ll k) 
{ 
    sort(a, a+n); // Sorting the first array. 
    sort(b, b+n); // Sorting the second array. 

    int result = 0; 
    for (int i=0, j=0; i<n && j<n;) 
    { 
        if (abs(a[i] - b[j]) <= k) 
        { 
            result++; 

            // Increasing array pointer of 
            // both the first and the second array. 
            i++; 
            j++; 
        } 

        // Increasing array pointer of the second array. 
        else if(a[i] > b[j]) 
            j++; 

        // Increasing array pointer of the first array. 
        else
            i++; 
    } 
    return result; 
} 

// Driver code 
int main() 
{ 
    ll a[] = {10, 15, 20}; 
    ll b[] = {17, 12, 24}; 
    int n = sizeof(a)/sizeof(a[0]); 
    int k = 3; 
    cout << findMaxPairs(a, b, n, k); 
    return 0; 
} 

```

## Java

```java

// Java program for Maximizing Unique Pairs  
// from two arrays 
import java.util.*; 

class GFG 
{ 

// Returns count of maximum pairs that caan 
// be formed from a[] and b[] under given 
// constraints. 
static int findMaxPairs(int a[], int b[],  
                        int n, int k) 
{ 
    Arrays.sort(a); // Sorting the first array. 
    Arrays.sort(b); // Sorting the second array. 

    int result = 0; 
    for (int i = 0, j = 0; i < n && j < n;) 
    { 
        if (Math.abs(a[i] - b[j]) <= k) 
        { 
            result++; 

            // Increasing array pointer of 
            // both the first and the second array. 
            i++; 
            j++; 
        } 

        // Increasing array pointer  
        // of the second array. 
        else if(a[i] > b[j]) 
            j++; 

        // Increasing array pointer  
        // of the first array. 
        else
            i++; 
    } 
    return result; 
} 

// Driver code 
public static void main(String args[]) 
{ 
    int a[] = {10, 15, 20}; 
    int b[] = {17, 12, 24}; 
    int n = a.length; 
    int k = 3; 
    System.out.println(findMaxPairs(a, b, n, k)); 
} 
} 

// This code is contributed by 
// Sanjit_Prasad 

```

## Python3

```py

# Python3 program for 
# Maximizing Unique Pairs  
# from two arrays 

# Returns count of maximum pairs that caan  
# be formed from a[] and b[] under given  
# constraints.  
def findMaxPairs(a,b,n,k): 

    # Sorting the first array. 
    a.sort() 

    # Sorting the second array. 
    b.sort()  

    result =0
    j=0
    for i in range(n): 
        if j<n: 
            if abs(a[i]-b[j])<=k: 
                result+=1

            # Increasing array pointer of  
            # both the first and the second array.  
                j +=1

            # Increasing array pointer of  
            # the second array.  
            elif a[i]>b[j]: 
                j+=1
    return result 

# Driver code 
if __name__=='__main__': 
    a = [10,15,20] 
    b = [17,12,24] 
    n = len(a) 
    k =3
    print(findMaxPairs(a,b,n,k)) 

# This code is contributed by  
# Shrikant13 

```

## C#

```cs

// C# program for Maximizing Unique Pairs  
// from two arrays 
using System; 

class GFG 
{ 

// Returns count of maximum pairs that caan 
// be formed from a[] and b[] under given 
// constraints. 
static int findMaxPairs(int []a, int []b,  
                        int n, int k) 
{ 
    Array.Sort(a); // Sorting the first array. 
    Array.Sort(b); // Sorting the second array. 

    int result = 0; 
    for (int i = 0, j = 0; i < n && j < n;) 
    { 
        if (Math.Abs(a[i] - b[j]) <= k) 
        { 
            result++; 

            // Increasing array pointer of 
            // both the first and the second array. 
            i++; 
            j++; 
        } 

        // Increasing array pointer  
        // of the second array. 
        else if(a[i] > b[j]) 
            j++; 

        // Increasing array pointer  
        // of the first array. 
        else
            i++; 
    } 
    return result; 
} 

// Driver code 
public static void Main(String []args) 
{ 
    int []a = {10, 15, 20}; 
    int []b = {17, 12, 24}; 
    int n = a.Length; 
    int k = 3; 
    Console.WriteLine(findMaxPairs(a, b, n, k)); 
} 
} 

// This code has been contributed by 29AjayKumar 

```

**输出**：

```
2

```

**时间复杂度**：`O(N log N)`。

**辅助空间**：`O(1)`。



