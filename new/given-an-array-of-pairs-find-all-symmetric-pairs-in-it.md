# 给定数组对，在其中找到所有对称对

> 原文：[https://www.geeksforgeeks.org/given-an-array-of-pairs-find-all-symmetric-pairs-in-it/](https://www.geeksforgeeks.org/given-an-array-of-pairs-find-all-symmetric-pairs-in-it/)

如果 c 等于 b 且 a 等于 d，则认为两对（a，b）和（c，d）是对称的。 例如，（10，20）和（20，10）是对称的。 给定成对的数组，找到其中的所有对称对。

可以假设所有对中的第一个元素都是不同的。

**示例**：

```
Input: arr[] = {{11, 20}, {30, 40}, {5, 10}, {40, 30}, {10, 5}}
Output: Following pairs have symmetric pairs
        (30, 40)
        (5, 10)  

```

**我们强烈建议您最小化浏览器，然后自己尝试。**

一个**简单解决方案**将遍历每对，并检查其他每对是否对称。 该解决方案需要`O(N ^ 2)`时间。

**更好的解决方案**是使用排序。 将所有对按第一个元素排序。 对于每对，请对给定数组中的第二个元素进行二分搜索，即检查该对中的第二个元素是否作为数组中的第一个元素存在。 如果找到，则将对中的第一个元素与第二个元素进行比较。 该解决方案的时间复杂度为`O(NlogN)`。

**有效解决方案**将使用哈希。 对的第一个元素用作键，第二个元素用作值。 想法是一遍遍所有对。 对于每对，检查其第二个元素是否在哈希表中。 如果是，则将第一个元素与哈希表的匹配条目的值进行比较。 如果值和第一个元素匹配，那么我们找到对称对。 否则，插入第一个元素作为键，插入第二个元素作为值。

以下是该想法的实现。

## C/C++

```cpp

#include<bits/stdc++.h> 
using namespace std; 

// A C++ program to find all symmetric pairs in a given array of pairs 
// Print all pairs that have a symmetric counterpart 
void findSymPairs(int arr[][2], int row) 
{ 
    // Creates an empty hashMap hM 
    unordered_map<int, int> hM; 

    // Traverse through the given array 
    for (int i = 0; i < row; i++) 
    { 
        // First and second elements of current pair 
        int first = arr[i][0]; 
        int sec   = arr[i][1]; 

        // If found and value in hash matches with first 
        // element of this pair, we found symmetry 
        if (hM.find(sec) != hM.end() && hM[sec] == first) 
            cout << "(" << sec << ", " << first << ")" <<endl; 

        else  // Else put sec element of this pair in hash 
            hM[first] = sec; 
    } 
} 

// Driver method 
int main() 
{ 
    int arr[5][2]; 
    arr[0][0] = 11; arr[0][1] = 20; 
    arr[1][0] = 30; arr[1][1] = 40; 
    arr[2][0] = 5;  arr[2][1] = 10; 
    arr[3][0] = 40;  arr[3][1] = 30; 
    arr[4][0] = 10;  arr[4][1] = 5; 
    findSymPairs(arr, 5); 
} 

//This is contributed by Chhavi 

```

## Java

```java

// A Java program to find all symmetric pairs in a given array of pairs 
import java.util.HashMap; 

class SymmetricPairs { 

    // Print all pairs that have a symmetric counterpart 
    static void findSymPairs(int arr[][]) 
    { 
        // Creates an empty hashMap hM 
        HashMap<Integer, Integer> hM = new HashMap<Integer, Integer>(); 

        // Traverse through the given array 
        for (int i = 0; i < arr.length; i++) 
        { 
            // First and second elements of current pair 
            int first = arr[i][0]; 
            int sec   = arr[i][1]; 

            // Look for second element of this pair in hash 
            Integer val = hM.get(sec); 

            // If found and value in hash matches with first 
            // element of this pair, we found symmetry 
            if (val != null && val == first) 
               System.out.println("(" + sec + ", " + first + ")"); 

            else  // Else put sec element of this pair in hash 
               hM.put(first, sec); 
        } 
    } 

    // Driver method 
    public static void main(String arg[]) 
    { 
        int arr[][] = new int[5][2]; 
        arr[0][0] = 11; arr[0][1] = 20; 
        arr[1][0] = 30; arr[1][1] = 40; 
        arr[2][0] = 5;  arr[2][1] = 10; 
        arr[3][0] = 40;  arr[3][1] = 30; 
        arr[4][0] = 10;  arr[4][1] = 5; 
        findSymPairs(arr); 
    } 
} 

```

## Python3

```py

# A Python3 program to find all symmetric  
# pairs in a given array of pairs. 

# Print all pairs that have 
# a symmetric counterpart 
def findSymPairs(arr, row): 

    # Creates an empty hashMap hM 
    hM = dict() 

    # Traverse through the given array 
    for i in range(row): 

        # First and second elements  
        # of current pair 
        first = arr[i][0] 
        sec = arr[i][1] 

        # If found and value in hash matches with first 
        # element of this pair, we found symmetry 
        if (sec in hM.keys() and hM[sec] == first): 
            print("(", sec,",", first, ")") 

        else: # Else put sec element of 
              # this pair in hash 
            hM[first] = sec 

# Driver Code 
if __name__ == '__main__': 
    arr = [[0 for i in range(2)]  
              for i in range(5)] 
    arr[0][0], arr[0][1] = 11, 20
    arr[1][0], arr[1][1] = 30, 40
    arr[2][0], arr[2][1] = 5, 10
    arr[3][0], arr[3][1] = 40, 30
    arr[4][0], arr[4][1] = 10, 5
    findSymPairs(arr, 5) 

# This code is contributed by Mohit Kumar 

```

## C#

```cs

// C# program to find all symmetric  
// pairs in a given array of pairs  
using System; 
using System.Collections.Generic; 

public class SymmetricPairs  
{ 

    // Print all pairs that have a symmetric counterpart 
    static void findSymPairs(int [,]arr) 
    { 
        // Creates an empty hashMap hM 
        Dictionary<int,int> hM = new Dictionary<int,int>(); 
        int val = 0; 

        // Traverse through the given array 
        for (int i = 0; i < arr.GetLength(0); i++) 
        { 
            // First and second elements of current pair 
            int first = arr[i, 0]; 
            int sec = arr[i, 1]; 

            // Look for second element of this pair in hash 
            if(hM.ContainsKey(sec)) 
            val = hM[sec]; 

            // If found and value in hash matches with first 
            // element of this pair, we found symmetry 
            if (val != 0 && val == first) 
            Console.WriteLine("(" + sec + ", " + first + ")"); 

            else // Else put sec element of this pair in hash 
            hM.Add(first, sec); 
        } 
    } 

    // Driver code 
    public static void Main(String []arg) 
    { 
        int [,]arr = new int[5, 2]; 
        arr[0, 0] = 11; arr[0, 1] = 20; 
        arr[1, 0] = 30; arr[1, 1] = 40; 
        arr[2, 0] = 5; arr[2, 1] = 10; 
        arr[3, 0] = 40; arr[3, 1] = 30; 
        arr[4, 0] = 10; arr[4, 1] = 5; 
        findSymPairs(arr); 
    } 
} 

// This code has been contributed by 29AjayKumar 

```

**Output:**

```
Following pairs have symmetric pairs
(30, 40)
(5, 10)
```

在哈希搜索和插入方法在`O(1)`时间内起作用的假设下，此解决方案的时间复杂度为`O(n)`。

本文由 **Shivam Agrawal** 提供。 如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

