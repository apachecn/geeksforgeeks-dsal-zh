# 将 Array 的每个元素替换为其相应的等级

> 原文：[https://www.geeksforgeeks.org/replace-each-element-of-array-with-its-corresponding-rank/](https://www.geeksforgeeks.org/replace-each-element-of-array-with-its-corresponding-rank/)

给定 **N** 个整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr []** ，任务是用数组中的[等级替换 Array 的每个元素。](https://www.geeksforgeeks.org/rank-elements-array/)

> 元素的**等级定义为当数组以升序排列时，元素与数组的第一个元素之间的距离。 如果数组中两个或两个以上相同，则它们的排名也将与元素首次出现的排名相同。
> **例如**：假设给定数组 arr [] = {2，2，1，6}，则元素的等级由下式给出：
> 排序后的数组为：
> arr [ ] = {1、2、2、6}
> 等级（1）= 1（在索引 0） 索引 2）
> 排名（6）= 4（在索引 3 处）**

**示例**：

> **输入**：arr [] = [100，5，70，2]
> **输出**：[4，2，3，1]
> **说明：[
> 2 的排名是 1、5 是 2、70 是 3 和 100 是 4。**
> 
> **输入**：arr [] = [100，2，70，2]
> **输出**：[3，1，2，1]
> **说明：[
> 2 的排名是 1，70 是 2，100 是 3。**

**朴素的方法**：朴素的方法是查找每个元素的等级为 **1 +** [**数组**](https://www.geeksforgeeks.org/count-smaller-equal-elements-sorted-array/) 中较小元素的数量 当前元素。

 ***时间复杂度**：`O(N ^ 2)`

**辅助空间**：`O(1)`

**高效方法**：要优化上述幼稚方法，请找到元素的等级，然后将等级分配给元素。 步骤如下：

1.  要计算元素的等级，请首先制作给定 **arr []** 的副本，然后以升序对复制的数组进行排序。

2.  然后遍历复制的数组，并通过获取等级变量将其等级放入 **HashMap** 中。

3.  如果元素已经存在于 HashMap 中，则不要更新等级，否则更新[，HashMap](http://www.geeksforgeeks.org/java-util-hashmap-in-java/) 中元素的等级以及递增等级变量。

4.  遍历给定数组 **arr []** ，使用存储在 HashMap 中的等级分配每个元素的等级。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach  
#include <bits/stdc++.h> 
using namespace std; 

// Function to assign rank to  
// array eleements  
void changeArr(int input[], int N)  
{  

    // Copy input array into newArray  
    int newArray[N]; 
    copy(input, input + N, newArray); 

    // Sort newArray[] in ascending order  
    sort(newArray, newArray + N);  
    int i;  

    // Map to store the rank of  
    // the array element  
    map<int, int> ranks; 

    int rank = 1;  

    for(int index = 0; index < N; index++) 
    {  

        int element = newArray[index];  

        // Update rank of element  
        if (ranks[element] == 0)  
        {  
            ranks[element] = rank;  
            rank++;  
        }  
    }  

    // Assign ranks to elements  
    for(int index = 0; index < N; index++)  
    {  
        int element = input[index];  
        input[index] = ranks[input[index]];  
    }  
}  

// Driver code     
int main() 
{ 

    // Given array arr[]  
    int arr[] = { 100, 2, 70, 2 };  

    int N = sizeof(arr) / sizeof(arr[0]); 

    // Function call  
    changeArr(arr, N);  

    // Print the array elements  
    cout << "["; 
    for(int i = 0; i < N - 1; i++) 
    { 
        cout << arr[i] << ", "; 
    } 
    cout << arr[N - 1] << "]"; 
    return 0; 
} 

// This code is contributed by divyeshrabadiya07 

```

## Java

```java

// Java program for the above approach  
import java.util.*;  

class GFG {  

    // Function to assign rank to  
    // array eleements  
    static void changeArr(int[] input)  
    {  
        // Copy input array into newArray  
        int newArray[]  
            = Arrays  
                .copyOfRange(input,  
                            0,  
                            input.length);  

        // Sort newArray[] in ascending order  
        Arrays.sort(newArray);  
        int i;  

        // Map to store the rank of  
        // the array element  
        Map<Integer, Integer> ranks  
            = new HashMap<>();  

        int rank = 1;  

        for (int index = 0;  
            index < newArray.length;  
            index++) {  

            int element = newArray[index];  

            // Update rank of element  
            if (ranks.get(element) == null) {  

                ranks.put(element, rank);  
                rank++;  
            }  
        }  

        // Assign ranks to elements  
        for (int index = 0;  
            index < input.length;  
            index++) {  

            int element = input[index];  
            input[index]  
                = ranks.get(input[index]);  

        }  
    }  

    // Driver Code  
    public static void main(String[] args)  
    {  
        // Given array arr[]  
        int[] arr = { 100, 2, 70, 2 };  

        // Function Call  
        changeArr(arr);  

        // Print the array elements  
        System  
            .out  
            .println(Arrays  
                        .toString(arr));  
    }  
}  

```

## Python3

```py

# Python3 program for the above approach  

# Function to assign rank to  
# array eleements  
def changeArr(input1):  

    # Copy input array into newArray  
    newArray = input1.copy()  

    # Sort newArray[] in ascending order  
    newArray.sort()  

    # Dictionary to store the rank of  
    # the array element  
    ranks = {}  

    rank = 1

    for index in range(len(newArray)):  
        element = newArray[index];  

        # Update rank of element  
        if element not in ranks:  
            ranks[element] = rank  
            rank += 1

    # Assign ranks to elements  
    for index in range(len(input1)):  
        element = input1[index]  
        input1[index] = ranks[input1[index]]  

# Driver Code  
if __name__ == "__main__":  

    # Given array arr[]  
    arr = [ 100, 2, 70, 2 ]  

    # Function call  
    changeArr(arr)  

    # Print the array elements  
    print(arr)  

# This code is contributed by chitranayal  

```

## C#

```cs

// C# program for the above approach  
using System;  
using System.Collections.Generic;  
using System.Text;  

class GFG{  

// Function to assign rank to  
// array eleements  
static void changeArr(int[] input)  
{  

    // Copy input array into newArray  
    int []newArray = new int[input.Length];  
    Array.Copy(input, newArray, input.Length);  

    // Sort newArray[] in ascending order  
    Array.Sort(newArray);  

    // To store the rank of  
    // the array element  
    Dictionary<int,  
            int> ranks= new Dictionary<int,  
                                        int>();  

    int rank = 1;  

    for(int index = 0;  
            index < newArray.Length;  
            index++)  
    {  
        int element = newArray[index];  

        // Update rank of element  
        if (!ranks.ContainsKey(element))  
        {  
            ranks[element] = rank;  
            rank++;  
        }  
    }  

    // Assign ranks to elements  
    for(int index = 0;  
            index < input.Length;  
            index++)  
    {  
        input[index] = ranks[input[index]];  
    }  
}  

// Driver Code  
public static void Main(string[] args)  
{  

    // Given array arr[]  
    int[] arr = { 100, 2, 70, 2 };  

    // Function call  
    changeArr(arr);  

    // Print the array elements  
    Console.WriteLine("[{0}]",  
        string.Join(", ", arr));  
}  
}  

// This code is contributed by rutvik_56  

```

```
[3, 1, 2, 1]
```

**时间复杂度**：*`O(N * log N)`*

**辅助空间**：*`O(n)`*



* * *

* * *



