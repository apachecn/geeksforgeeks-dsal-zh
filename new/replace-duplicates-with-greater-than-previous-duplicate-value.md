# 用大于以前的重复值

替换重复项

给定一个元素数组，并以使该数组上的所有元素都不同的方式更改该数组。 如果要替换值，则替换值应大于先前的值，并且修改后元素的总和应尽可能小。

**示例**：

> 输入：arr = {1,2,2,5,8,8,8}
> 输出：1 2 3 5 8 9 10
> 8 替换为 9（大于 8 的不存在的元素）。 下一个重复出现的 8 被替换为 10。
> 
> 输入：arr = {1、2、5、7、8、8、7}
> 输出：1 2 5 7 8 9 10
> 
> 输入：arr = {9，9，9，9，9}
> 输出：9 10 11 12 13

**来源**： [Paytm 面试体验 30](https://www.geeksforgeeks.org/paytm-interview-experience-set-30/) 。

此问题是本文的[的变体。 在上面的文章中，我们必须用迄今为止最大的价值替换重复项。 但是在这个问题中，我们必须用大于先前重复值的重复项替换元素。

的想法是找到下一个要替换的更大的元素，以使总和最小化。 为了找到下一个更大的元素，我们必须从重复的元素进行迭代，直到找到 **INT_MAX** ，直到找到下一个更大的元素。](https://www.geeksforgeeks.org/replace-repeating-elements-with-greater-that-greatest-values/)

下面是上述方法的实现。

## C++

```cpp

// CPP program to replace every repeating 
// element with next greater element. 
#include <bits/stdc++.h> 
using namespace std; 

void replaceElements(int arr[], int n) 
{ 
    unordered_set<int> s; 

    for (int i = 0; i < n; i++) { 

        // check whether the element is 
        // repeated or not 
        if (s.find(arr[i]) == s.end()) 
            s.insert(arr[i]); 

        else { 

            // find the next greatest element 
            for (int j = arr[i] + 1; j < INT_MAX; j++) { 
                if (s.find(j) == s.end()) { 
                    arr[i] = j; 
                    s.insert(j); 
                    break; 
                } 
            } 
        } 
    } 
} 

int main() 
{ 
    int arr[] = { 1, 2, 5, 7, 8, 8, 7 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    replaceElements(arr, n); 

    for (int i = 0; i < n; i++) 
        cout << arr[i] << " "; 
    cout << "\n"; 
} 

```

## Java

```java

// Java program to replace every repeating 
// element with next greater element. 
import java.util.HashSet; 
import java.util.Set; 

public class ReplaceDuplicateWithGreaterThanPreviousDuplicate { 

    private static void replaceElements(int[] arr, int n) 
    { 
        Set<Integer> st = new HashSet<>(); 
        for (int i = 0; i < n; i++) { 
            // check whether the element is 
            // repeated or not 
            if (!st.contains(arr[i])) { 
                st.add(arr[i]); 
            } 
            else { 
                // find the next greatest element 
                for (int j = arr[i] + 1; j < Integer.MAX_VALUE; j++) { 
                    if (!st.contains(j)) { 
                        arr[i] = j; 
                        st.add(j); 
                        break; 
                    } 
                } 
            } 
        } 
    } 
    public static void main(String[] args) 
    { 
        int[] arr = new int[] { 1, 2, 5, 7, 8, 8, 7 }; 
        int n = arr.length; 
        replaceElements(arr, n); 

        for (int i = 0; i < n; i++) { 
            System.out.print(arr[i] + " "); 
        } 
    } 
} 

```

## Python3

```py

# Python3 program to replace every repeating 
# element with next greater element. 
import sys 

def replaceElements(arr, n): 

    s = [] 

    for i in range (n): 

        # check whether the element  
        # is repeated or not 
        if arr[i] not in s: 
            s.append(arr[i]) 

        else : 

            # find the next greatest element 
            for j in range(arr[i] + 1, sys.maxsize) : 
                if j not in s: 
                    arr[i] = j 
                    s.append(j) 
                    break

# Driver Code 
if __name__ == "__main__": 

    arr = [ 1, 2, 5, 7, 8, 8, 7 ] 
    n = len(arr) 

    replaceElements(arr, n) 

    for i in range(n): 
        print (arr[i], end = " ") 
    print () 

# This code is contributed  
# by ChitraNayal 

```

## C#

```cs

// C# program to replace every repeating  
// element with next greater element.  
using System; 
using System.Collections.Generic; 

public class ReplaceDuplicateWithGreaterThanPreviousDuplicate  
{  
    private static void replaceElements(int[] arr, int n)  
    {  
        HashSet<int> st = new HashSet<int>();  
        for (int i = 0; i < n; i++)  
        {  
            // check whether the element is  
            // repeated or not  
            if (!st.Contains(arr[i]))  
            {  
                st.Add(arr[i]);  
            }  
            else
            {  
                // find the next greatest element  
                for (int j = arr[i] + 1; j < int.MaxValue; j++)  
                {  
                    if (!st.Contains(j)) 
                    {  
                        arr[i] = j;  
                        st.Add(j);  
                        break;  
                    }  
                }  
            }  
        }  
    }  

    // Driver Code 
    public static void Main(String[] args)  
    {  
        int[] arr = new int[] { 1, 2, 5, 7, 8, 8, 7 };  
        int n = arr.Length;  
        replaceElements(arr, n);  

        for (int i = 0; i < n; i++)  
        {  
            Console.Write(arr[i] + " ");  
        }  
    }  
}  

// This code is contributed by PrinciRaj1992 

```

**Output:**

```
1 2 5 7 8 9 10

```



* * *

* * *



