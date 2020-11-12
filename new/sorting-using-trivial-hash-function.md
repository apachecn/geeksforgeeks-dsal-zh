# 使用普通哈希函数排序

> 原文：[https://www.geeksforgeeks.org/sorting-using-trivial-hash-function/](https://www.geeksforgeeks.org/sorting-using-trivial-hash-function/)

使用[普通哈希](https://www.geeksforgeeks.org/index-mapping-or-trivial-hashing-with-negatives-allowed/)函数排序。

**示例**：

```
Input :  9 4 3 5 8 
Output : 3 4 5 8 9

```

我们已经阅读了各种排序算法，例如[堆排序](https://www.geeksforgeeks.org/heap-sort/)，[冒泡排序](https://www.geeksforgeeks.org/bubble-sort/)，[合并排序](https://www.geeksforgeeks.org/merge-sort/)等。

在这里，我们将看到如何使用哈希数组对`N`个元素排序。 但是该算法有局限性。 我们只能对元素的值不大（通常不超过`10 ^ 6`）的`N`个元素排序。

**使用哈希排序的说明**：

**步骤 1**：创建一个大小为`max_element`的哈希数组，因为这是最大值，因此我们需要：

**步骤 2**：遍历所有元素并保存特定元素的出现数量。

**步骤 3**：在对哈希表中所有元素的出现次数进行计数之后，只需从 0 迭代到哈希数组中的`max_element`。

**步骤 4**：在哈希数组中，如果我们发现存储在任何哈希位置的值大于 0，则表明该元素在原始元素列表中至少存在一次。

**步骤 5**：`Hash[i]`具有列表中元素存在的次数计数，因此当其大于 0 时，我们将打印元素的次数。

如果要存储元素，请使用另一个数组以排序方式存储它们。

如果要按降序对其排序，则只需从`max`遍历到 0 并重复相同的过程即可。

**下面是上述方法的实现**：

## C++

```cpp

// C++ program to sort an array using hash 
// function 
#include <bits/stdc++.h> 
using namespace std; 

void sortUsingHash(int a[], int n) 
{ 
    // find the maximum element 
    int max = *std::max_element(a, a + n); 

    // create a hash function upto the max size 
    int hash[max + 1] = { 0 }; 

    // traverse through all the elements and  
    // keep a count 
    for (int i = 0; i < n; i++) 
        hash[a[i]] += 1; 

    // Traverse upto all elements and check if  
    // it is present or not. If it is present,  
    // then print the element the number of times 
    // it's present. Once we have printed n times,  
    // that means we have printed n elements 
    // so break out of the loop 
    for (int i = 0; i <= max; i++) { 

        // if present 
        if (hash[i]) { 

            // print the element that number of  
            // times it's present 
            for (int j = 0; j < hash[i]; j++) { 
                cout << i << " "; 
            } 
        } 
    } 
} 

// driver program  
int main() 
{ 
    int a[] = { 9, 4, 3, 2, 5, 2, 1, 0, 4,  
              3, 5, 10, 15, 12, 18, 20, 19 }; 
    int n = sizeof(a) / sizeof(a[0]); 

    sortUsingHash(a, n); 
    return 0; 
} 

```

## Java

```java

// Java program to sort an array using hash 
// function 
import java.util.*; 

class GFG 
{ 

static void sortUsingHash(int a[], int n) 
{ 
    // find the maximum element 
    int max = Arrays.stream(a).max().getAsInt(); 

    // create a hash function upto the max size 
    int hash[] = new int[max + 1]; 

    // traverse through all the elements and  
    // keep a count 
    for (int i = 0; i < n; i++) 
        hash[a[i]] += 1; 

    // Traverse upto all elements and check if  
    // it is present or not. If it is present,  
    // then print the element the number of times 
    // it's present. Once we have printed n times,  
    // that means we have printed n elements 
    // so break out of the loop 
    for (int i = 0; i <= max; i++) 
    { 

        // if present 
        if (hash[i] != 0) 
        { 

            // print the element that number of  
            // times it's present 
            for (int j = 0; j < hash[i]; j++) 
            { 
                System.out.print(i+" "); 
            } 
        } 
    } 
} 

// Driver code  
public static void main(String[] args) 
{ 
    int a[] = { 9, 4, 3, 2, 5, 2, 1, 0, 4,  
            3, 5, 10, 15, 12, 18, 20, 19 }; 
    int n = a.length; 

    sortUsingHash(a, n); 
} 
} 

// This code contributed by Rajput-Ji 

```

## Python3

```py

# Python3 program to sort an array  
# using hash function  
def sortUsingHash(a, n):  

    # find the maximum element  
    Max = max(a)  

    # create a hash function upto  
    # the max size  
    Hash = [0] * (Max + 1)  

    # traverse through all the elements  
    # and keep a count  
    for i in range(0, n):  
        Hash[a[i]] += 1

    # Traverse upto all elements and check  
    # if it is present or not. If it is  
    # present, then print the element the  
    # number of times it's present. Once we  
    # have printed n times, that means we  
    # have printed n elements so break out  
    # of the loop  
    for i in range(0, Max + 1):  

        # if present  
        if Hash[i] != 0:  

            # print the element that number  
            # of times it's present  
            for j in range(0, Hash[i]):  
                print(i, end = " ")  

# Driver Code 
if __name__ == "__main__":  

    a = [9, 4, 3, 2, 5, 2, 1, 0, 4,  
         3, 5, 10, 15, 12, 18, 20, 19]  
    n = len(a) 

    sortUsingHash(a, n)  

# This code is contributed by Rituraj Jain 

```

## C#

```cs

// C# program to sort an array using hash 
// function 
using System; 
using System.Linq; 

class GFG 
{ 

static void sortUsingHash(int []a, int n) 
{ 
    // find the maximum element 
    int max = a.Max(); 

    // create a hash function upto the max size 
    int []hash = new int[max + 1]; 

    // traverse through all the elements and  
    // keep a count 
    for (int i = 0; i < n; i++) 
        hash[a[i]] += 1; 

    // Traverse upto all elements and check if  
    // it is present or not. If it is present,  
    // then print the element the number of times 
    // it's present. Once we have printed n times,  
    // that means we have printed n elements 
    // so break out of the loop 
    for (int i = 0; i <= max; i++) 
    { 

        // if present 
        if (hash[i] != 0) 
        { 

            // print the element that number of  
            // times it's present 
            for (int j = 0; j < hash[i]; j++) 
            { 
                Console.Write(i+" "); 
            } 
        } 
    } 
} 

// Driver code  
public static void Main(String[] args) 
{ 
    int []a = { 9, 4, 3, 2, 5, 2, 1, 0, 4,  
            3, 5, 10, 15, 12, 18, 20, 19 }; 
    int n = a.Length; 

    sortUsingHash(a, n); 
} 
} 

/* This code contributed by PrinciRaj1992 */

```

**输出**：

```
0 1 2 2 3 3 4 4 5 5 9 10 12 15 18 19 20 

```

**如何处理负数？**

如果数组具有**负数**和**正数**，我们保留两个散列数组以跟踪正负元素。

如果数组具有负数和正数，则使用散列排序的说明：

**步骤 1** ：创建两个哈希数组，一个用于正数，另一个用于负数。

**步骤 2**：正哈希数组的大小为`max`，负数组数组的大小为`min`。

**步骤 3**：在负哈希数组中从`min`遍历到 0，和我们为正数做的一样。

**步骤 4**：对正元素从 0 遍历到最大值，并按上述相同的方式打印它们。

下面是上述方法的实现：

## C++

```cpp

// C++ program to sort an array using hash 
// function with negative values allowed. 
#include <bits/stdc++.h> 
using namespace std; 

void sortUsingHash(int a[], int n) 
{ 
    // find the maximum element 
    int max = *std::max_element(a, a + n); 
    int min = abs(*std::min_element(a, a + n)); 

    // create a hash function upto the max size 
    int hashpos[max + 1] = { 0 }; 
    int hashneg[min + 1] = { 0 }; 

    // traverse through all the elements and 
    // keep a count 
    for (int i = 0; i < n; i++) { 
        if (a[i] >= 0) 
            hashpos[a[i]] += 1; 
        else
            hashneg[abs(a[i])] += 1; 
    } 

    // Traverse up to all negative elements and  
    // check if it is present or not. If it is  
    // present, then print the element the number 
    // of times it's present. Once we have printed 
    // n times, that means we have printed n elements 
    // so break out of the loop 
    for (int i = min; i > 0; i--) { 
        if (hashneg[i]) { 

            // print the element that number of times  
            // it's present. Print the negative element 
            for (int j = 0; j < hashneg[i]; j++) {                 
                cout << (-1) * i << " "; 
            } 
        } 
    } 

    // Traverse upto all elements and check if it is  
    // present or not. If it is present, then print  
    // the element the number of times it's present 
    // once we have printed n times, that means we  
    // have printed n elements, so break out of the  
    // loop 
    for (int i = 0; i <= max; i++) { 

        // if present 
        if (hashpos[i]) { 

            // print the element that number of times 
            // it's present 
            for (int j = 0; j < hashpos[i]; j++) { 
                 cout << i << " "; 
            } 
        } 
    } 
} 

// driver program to test the above function 
int main() 
{ 
    int a[] = { -1, -2, -3, -4, -5, -6, 8, 7, 
                        5, 4, 3, 2, 1, 0 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    sortUsingHash(a, n); 
    return 0; 
} 

```

## Java

```java

// Java program to sort an array using hash 
// function with negative values allowed. 
import java.util.Arrays; 
class GFG { 

static void sortUsingHash(int a[], int n) 
{ 
    // find the maximum element 
    int max = Arrays.stream(a).max().getAsInt(); 
    int min = Math.abs(Arrays.stream(a).min().getAsInt()); 

    // create a hash function upto the max size 
    int hashpos[] = new int[max + 1]; 
    int hashneg[] = new int[min + 1]; 

    // traverse through all the elements and 
    // keep a count 
    for (int i = 0; i < n; i++) 
    { 
        if (a[i] >= 0) 
            hashpos[a[i]] += 1; 
        else
            hashneg[Math.abs(a[i])] += 1; 
    } 

    // Traverse up to all negative elements and  
    // check if it is present or not. If it is  
    // present, then print the element the number 
    // of times it's present. Once we have printed 
    // n times, that means we have printed n elements 
    // so break out of the loop 
    for (int i = min; i > 0; i--)  
    { 
        if (hashneg[i] > 0)  
        { 

            // print the element that number of times  
            // it's present. Print the negative element 
            for (int j = 0; j < hashneg[i]; j++)  
            {  
                System.out.print((-1)*i+" "); 
            } 
        } 
    } 

    // Traverse upto all elements and check if it is  
    // present or not. If it is present, then print  
    // the element the number of times it's present 
    // once we have printed n times, that means we  
    // have printed n elements, so break out of the  
    // loop 
    for (int i = 0; i <= max; i++) 
    { 

        // if present 
        if (hashpos[i] > 0)  
        { 

            // print the element that number of times 
            // it's present 
            for (int j = 0; j < hashpos[i]; j++)  
            { 
                System.out.print(i+" "); 
            } 
        } 
    } 
} 

// Driver program to test the above function 
public static void main(String[] args)  
{ 
    int a[] = { -1, -2, -3, -4, -5, -6, 8, 7, 
                        5, 4, 3, 2, 1, 0 }; 
    int n = a.length; 
    sortUsingHash(a, n); 
} 
} 

// This code has been contributed by 29AjayKumar 

```

## Python3

```py

# Python3 program to sort an array using hash  
# function with negative values allowed.  
def sortUsingHash(a, n):  

    # find the maximum element  
    Max = max(a)  
    Min = abs(min(a))  

    # create a hash function upto the max size  
    hashpos = [0] * (Max + 1)  
    hashneg = [0] * (Min + 1)  

    # traverse through all the elements and  
    # keep a count  
    for i in range(0, n):  
        if a[i] >= 0:  
            hashpos[a[i]] += 1
        else: 
            hashneg[abs(a[i])] += 1

    # Traverse up to all negative elements  
    # and check if it is present or not.  
    # If it is present, then print the  
    # element the number of times it's present.  
    # Once we have printed n times, that means 
    # we have printed n elements so break out  
    # of the loop  
    for i in range(Min, 0, -1):  
        if hashneg[i] != 0: 

            # print the element that number of times  
            # it's present. Print the negative element  
            for j in range(0, hashneg[i]):                  
                print((-1) * i, end = " ")  

    # Traverse upto all elements and check if  
    # it is present or not. If it is present,  
    # then print the element the number of  
    # times it's present once we have printed  
    # n times, that means we have printed n   
    # elements, so break out of the loop  
    for i in range(0, Max + 1):  

        # if present  
        if hashpos[i] != 0:  

            # print the element that number  
            # of times it's present  
            for j in range(0, hashpos[i]):  
                print(i, end = " ") 

# Driver Code 
if __name__ == "__main__":  

    a = [-1, -2, -3, -4, -5, -6,  
         8, 7, 5, 4, 3, 2, 1, 0]  

    n = len(a)  
    sortUsingHash(a, n)  

# This code is contributed by Rituraj Jain 

```

## C#

```cs

// C# program to sort an array using hash  
// function with negative values allowed.  
using System; 
using System.Linq; 

class GFG  
{  

static void sortUsingHash(int []a, int n)  
{  
    // find the maximum element  
    int max = a.Max();  
    int min = Math.Abs(a.Min());  

    // create a hash function upto the max size  
    int []hashpos = new int[max + 1];  
    int []hashneg = new int[min + 1];  

    // traverse through all the elements and  
    // keep a count  
    for (int i = 0; i < n; i++)  
    {  
        if (a[i] >= 0)  
            hashpos[a[i]] += 1;  
        else
            hashneg[Math.Abs(a[i])] += 1;  
    }  

    // Traverse up to all negative elements and  
    // check if it is present or not. If it is  
    // present, then print the element the number  
    // of times it's present. Once we have printed  
    // n times, that means we have printed n elements  
    // so break out of the loop  
    for (int i = min; i > 0; i--)  
    {  
        if (hashneg[i] > 0)  
        {  

            // print the element that number of times  
            // it's present. Print the negative element  
            for (int j = 0; j < hashneg[i]; j++)  
            {  
                Console.Write((-1)*i+" ");  
            }  
        }  
    }  

    // Traverse upto all elements and check if it is  
    // present or not. If it is present, then print  
    // the element the number of times it's present  
    // once we have printed n times, that means we  
    // have printed n elements, so break out of the  
    // loop  
    for (int i = 0; i <= max; i++)  
    {  

        // if present  
        if (hashpos[i] > 0)  
        {  

            // print the element that number of times  
            // it's present  
            for (int j = 0; j < hashpos[i]; j++)  
            {  
                Console.Write(i+" ");  
            }  
        }  
    }  
}  

// Driver code  
public static void Main(String[] args)  
{  
    int []a = { -1, -2, -3, -4, -5, -6, 8, 7,  
                        5, 4, 3, 2, 1, 0 };  
    int n = a.Length;  
    sortUsingHash(a, n);  
}  
}  

/* This code contributed by PrinciRaj1992 */

```

**输出**：

```
-6 -5 -4 -3 -2 -1 0 1 2 3 4 5 7 8 

```

**复杂度**：

此排序函数可以具有复杂度`O(max_element)`。 因此，性能取决于所提供的数据集。

**局限性**：

1.  只能对有限范围的数组元素排序（通常从`-10 ^ 6`到`10 ^ 6`）

2.  在最坏的情况下，辅助空间为`O(max_element + min_element)`。



* * *

* * *



