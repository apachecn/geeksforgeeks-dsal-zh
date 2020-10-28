# 查找数组

中重复的前三名

给定大小为 N 的重复数字数组，您必须找到前三个重复数字。

注意：如果 Number 出现相同的次数，那么我们的输出将是

数组中第一个出现的示例：

> 输入：arr [] = {3，4，2，3，16，3，15，16，15，15，16，2，3}
> 输出：三个最大的元素是 3 16 15
> 说明： 在这里，3 次出现 4 次，16 次出现 3 次，15 次出现 3 次。
> 
> 输入：arr [] = {2，4，3，2，3，4，5，5，3，2，2，5}
> 输出：三个最大的元素是 2 3 5

**在**中问： [Zoho](https://www.geeksforgeeks.org/zoho-interview-experience-set-34-off-campus/)

首先，我们必须在哈希表 **freq** 中找到每个元素的频率。 现在我们的任务是[在哈希表中查找前 3 个元素](https://www.geeksforgeeks.org/find-the-largest-three-elements-in-an-array/)，要找到它，我们只使用三个对类型变量（假设 x，y，z），其中第一个存储频率，第二个存储实际数字 。

**算法**

```
1) Initialize the largest three elements
   as Minimum value.
    x.first = y.first = z.first = Minus-Infinite

2) Iterate through all elements of the 
   hash table freq.
   a) Let current array element be p.
   b) If (fre[p] !=0 && fre[p] > x.first)
      {
          // This order of assignment is important
          z = y
          y = x
          x.first = fre[p]
          x.second = p;   
       }
   c) Else if (fre[p] !=0 && free[p] > y.first)
      {
          z = y
          y.first = fre[p]
          y.second = p 
      }
   d) Else if (fre[p] !=0 && free[p] > z.first)
      {
          z.first = fre[p]
          z.second = p  
      }

// Modify frequency of Current element 
// as zero because We Traverse Initial 
// array arr[]. So it don't take same 
// values again
3) fre[p] = 0

3) Print x.second, y.second and z.second. 
```

## C++

```cpp

// C++ Program to Find the top three repeated numbers 
#include <bits/stdc++.h> 
using namespace std; 

/* Function to print top three repeated numbers */
void top3Repeated(int arr[], int n) 
{ 
    // There should be atleast two elements 
    if (n < 3) { 
        cout << "Invalid Input"; 
        return; 
    } 

    // Count Frequency of each element 
    unordered_map<int, int> fre; 
    for (int i = 0; i < n; i++) 
        fre[arr[i]]++; 

    // Initialize first value of each variable 
    // of Pair type is INT_MIN 
    pair<int, int> x, y, z; 
    x.first = y.first = z.first = INT_MIN; 

    for (auto curr : fre) { 

        // If frequency of current element 
        // is not zero and greater than 
        // frequency of first largest element 
        if (curr.second > x.first) { 

            // Update second and third largest 
            z = y; 
            y = x; 

            // Modify values of x Number 
            x.first = curr.second; 
            x.second = curr.first; 
        } 

        // If frequency of current element is 
        // not zero and frequency of current 
        // element is less than frequency of 
        // first largest element, but greater 
        // than y element 
        else if (curr.second > y.first) { 

            // Modify values of third largest 
            z = y; 

            // Modify values of second largest 
            y.first = curr.second; 
            y.second = curr.first; 
        } 

        // If frequency of current element 
        // is not zero and frequency of 
        // current element is less than 
        // frequency of first element and 
        // second largest, but greater than 
        // third largest. 
        else if (curr.second > z.first) { 

            // Modify values of z Number 
            z.first = curr.second; 
            z.second = curr.first; 
        } 
    } 

    cout << "Three largest elements are "
         << x.second << " " << y.second 
         << " " << z.second; 
} 

// Driver's Code 
int main() 
{ 
    int arr[] = { 3, 4, 2, 3, 16, 3, 15, 
                  16, 15, 15, 16, 2, 3 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    top3Repeated(arr, n); 
    return 0; 
} 

```

## Java

```java

// Java Program to Find the top three repeated numbers 
import java.io.*; 
import java.util.*; 

// User defined Pair class 
class Pair { 
    int first, second; 
} 

class GFG { 

    // Function to print top three repeated numbers 
    static void top3Repeated(int[] arr, int n) 
    { 
        // There should be atleast two elements 
        if (n < 3) { 
            System.out.print("Invalid Input"); 
            return; 
        } 

        // Count Frequency of each element 
        TreeMap<Integer, Integer> freq = new TreeMap<>(); 
        for (int i = 0; i < n; i++) 
            if (freq.containsKey(arr[i])) 
                freq.put(arr[i], 1 + freq.get(arr[i])); 
            else
                freq.put(arr[i], 1); 

        // Initialize first value of each variable 
        // of Pair type is INT_MIN 
        Pair x = new Pair(); 
        Pair y = new Pair(); 
        Pair z = new Pair(); 
        x.first = y.first = z.first = Integer.MIN_VALUE; 

        for (Map.Entry curr : freq.entrySet()) { 
            // If frequency of current element 
            // is not zero and greater than 
            // frequency of first largest element 
            if (Integer.parseInt(String.valueOf(curr.getValue())) > x.first) { 

                // Update second and third largest 
                z.first = y.first; 
                z.second = y.second; 
                y.first = x.first; 
                y.second = x.second; 

                // Modify values of x Number 
                x.first = Integer.parseInt(String.valueOf(curr.getValue())); 
                x.second = Integer.parseInt(String.valueOf(curr.getKey())); 
            } 

            // If frequency of current element is 
            // not zero and frequency of current 
            // element is less than frequency of 
            // first largest element, but greater 
            // than y element 
            else if (Integer.parseInt(String.valueOf(curr.getValue())) > y.first) { 
                // Modify values of third largest 
                z.first = y.first; 
                z.second = y.second; 

                // Modify values of second largest 
                y.first = Integer.parseInt(String.valueOf(curr.getValue())); 
                y.second = Integer.parseInt(String.valueOf(curr.getKey())); 
            } 

            // If frequency of current element 
            // is not zero and frequency of 
            // current element is less than 
            // frequency of first element and 
            // second largest, but greater than 
            // third largest. 
            else if (Integer.parseInt(String.valueOf(curr.getValue())) > z.first) { 

                // Modify values of z Number 
                z.first = Integer.parseInt(String.valueOf(curr.getValue())); 
                z.second = Integer.parseInt(String.valueOf(curr.getKey())); 
            } 
        } 

        System.out.print("Three largest elements are " + x.second + " "
                         + y.second + " " + z.second); 
    } 

    // Driver's Code 
    public static void main(String args[]) 
    { 
        int[] arr = { 3, 4, 2, 3, 16, 3, 15, 
                      16, 15, 15, 16, 2, 3 }; 
        int n = arr.length; 
        top3Repeated(arr, n); 
    } 
} 

// This code is contributed by rachana soma 

```

**Output:**

```
Three largest elements are 3 15 16

```

**时间复杂度**：O（n）

**辅助空间**：O（n）



* * *

* * *



