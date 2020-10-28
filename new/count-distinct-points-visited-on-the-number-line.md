# 计算在数字行

> 原文：[https://www.geeksforgeeks.org/count-distinct-points-visited-on-the-number-line/](https://www.geeksforgeeks.org/count-distinct-points-visited-on-the-number-line/)

上访问过的不同点

给定某人的位置 **current_pos** 和二进制字符串**路径**，即该人执行的移动，如果 **path [i] ='0'**，则 人向左移动了一步，并且如果 **path [i] ='1'**，那么人向右移动了一步。 任务是找到该人拜访的不同职位的数量。

**示例**：

> **输入**：current_pos = 5，路径=“ 011101”
> **输出**：4
> 给定的移动是左，右，右，右，左和右
> 即 5-> 4-> 5-> 6-> 7-> 6-> 7
> 不同位置的数目是 4（4、5、6 和 7） 。
> 
> **输入**：current_pos = 3，路径=“ 110100”
> **输出**：3
> 3-> 4-> 5-> 4-> 5-> 4-> 3

**方法**：

*   声明一个数组 **points []** ，以存储该人经过的所有点。

*   将此数组的第一个位置初始化为当前位置 **current_pos** 。

*   遍历字符串**路径**并执行以下操作：

    *   如果当前字符为**'0'**，则此人向左走。 因此，将当前位置减小 **1** 并将其存储在**点[]** 中。

    *   如果当前字符为**‘1’**，则此人向右行驶。 因此，将当前位置增加 **1** 并将其存储在**点[]** 中。

*   计算**点[]** 中不同元素的总数。 有关对数组中的不同元素进行计数的不同方法，请参考[对数组中的不同元素进行计数](https://www.geeksforgeeks.org/count-distinct-elements-in-an-array/)。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Utility function to return the number 
// of distinct elements in an array 
int countDistinct(int arr[], int len) 
{ 

    set<int> hs; 

    for (int i = 0; i < len; i++) { 
        // add all the elements to the HashSet 
        hs.insert(arr[i]); 
    } 

    // Return the size of hashset as 
    // it consists of all unique elements 
    return hs.size(); 
} 

// Function to return the count of 
// positions the person went to 
int getDistinctPoints(int current_pos, string path) 
{ 

    // Length of path 
    int len = path.length(); 

    // Array to store all the points traveled 
    int points[len + 1]; 

    // The first point is the current_pos 
    points[0] = current_pos; 

    // For all the directions in path 
    for (int i = 0; i < len; i++) { 

        // Get whether the direction was left or right 
        char ch = path[i]; 

        // If the direction is left 
        if (ch == '0') { 

            // Decrement the current position by 1 
            current_pos--; 

            // Store the current position in array 
            points[i + 1] = current_pos; 
        } 

        // If the direction is right 
        else { 

            // Increment the current position by 1 
            current_pos++; 

            // Store the current position in array 
            points[i + 1] = current_pos; 
        } 
    } 

    return countDistinct(points, len + 1); 
} 

// Driver code 
int main() 
{ 
    int current_pos = 5; 
    string path = "011101"; 

    cout << (getDistinctPoints(current_pos, path)); 

    return 0; 
} 
// contributed by Arnab Kundu 

```

## Java

```java

// Java implementation of the approach 
import java.util.*; 
class GFG { 

    // Function to return the count of 
    // positions the person went to 
    public static int getDistinctPoints(int current_pos, String path) 
    { 

        // Length of path 
        int len = path.length(); 

        // Array to store all the points traveled 
        int points[] = new int[len + 1]; 

        // The first point is the current_pos 
        points[0] = current_pos; 

        // For all the directions in path 
        for (int i = 0; i < len; i++) { 

            // Get whether the direction was left or right 
            char ch = path.charAt(i); 

            // If the direction is left 
            if (ch == '0') { 

                // Decrement the current position by 1 
                current_pos--; 

                // Store the current position in array 
                points[i + 1] = current_pos; 
            } 

            // If the direction is right 
            else { 

                // Increment the current position by 1 
                current_pos++; 

                // Store the current position in array 
                points[i + 1] = current_pos; 
            } 
        } 

        return countDistinct(points, len + 1); 
    } 

    // Utility function to return the number 
    // of distinct elements in an array 
    public static int countDistinct(int arr[], int len) 
    { 

        HashSet<Integer> hs = new HashSet<Integer>(); 

        for (int i = 0; i < len; i++) { 
            // add all the elements to the HashSet 
            hs.add(arr[i]); 
        } 

        // Return the size of hashset as 
        // it consists of all unique elements 
        return hs.size(); 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        int current_pos = 5; 
        String path = "011101"; 

        System.out.print(getDistinctPoints(current_pos, path)); 
    } 
} 

```

## Python3

```py

# Utility function to return the number 
# of distinct elements in an array 
def countDistinct(arr, Len): 

    hs = dict() 

    for i in range(Len): 

        # add all the elements to the HashSet 
        hs[arr[i]] = 1

    # Return the size of hashset as 
    # it consists of all unique elements 
    return len(hs) 

# Function to return the count of 
# positions the person went to 
def getDistinctPoints(current_pos, path): 

    # Length of path 
    Len = len(path) 

    # Array to store all the points traveled 
    points = [0 for i in range(Len + 1)] 

    # The first pois the current_pos 
    points[0] = current_pos 

    # For all the directions in path 
    for i in range(Len): 

        # Get whether the direction  
        # was left or right 
        ch = path[i] 

        # If the direction is left 
        if (ch == '0'): 

            # Decrement the current position by 1 
            current_pos -= 1

            # Store the current position in array 
            points[i + 1] = current_pos 

        # If the direction is right 
        else: 

            # Increment the current position by 1 
            current_pos += 1

            # Store the current position in array 
            points[i + 1] = current_pos 

    return countDistinct(points, Len + 1) 

# Driver code 
current_pos = 5
path = "011101"

print(getDistinctPoints(current_pos, path)) 

# This code is contributed by mohit kumar 

```

## C#

```cs

// C# implementation of the approach 
using System; 
using System.Collections.Generic; 

class GFG { 

    // Function to return the count of 
    // positions the person went to 
    public static int getDistinctPoints(int current_pos, 
                                        string path) 
    { 

        // Length of path 
        int len = path.Length; 

        // Array to store all the points traveled 
        int[] points = new int[len + 1]; 

        // The first point is the current_pos 
        points[0] = current_pos; 

        // For all the directions in path 
        for (int i = 0; i < len; i++) { 

            // Get whether the direction was left or right 
            char ch = path[i]; 

            // If the direction is left 
            if (ch == '0') { 

                // Decrement the current position by 1 
                current_pos--; 

                // Store the current position in array 
                points[i + 1] = current_pos; 
            } 

            // If the direction is right 
            else { 

                // Increment the current position by 1 
                current_pos++; 

                // Store the current position in array 
                points[i + 1] = current_pos; 
            } 
        } 

        return countDistinct(points, len + 1); 
    } 

    // Utility function to return the number 
    // of distinct elements in an array 
    public static int countDistinct(int[] arr, int len) 
    { 

        HashSet<int> hs = new HashSet<int>(); 

        for (int i = 0; i < len; i++) { 
            // add all the elements to the HashSet 
            hs.Add(arr[i]); 
        } 

        // Return the size of hashset as 
        // it consists of all unique elements 
        return hs.Count; 
    } 

    // Driver code 
    public static void Main(string[] args) 
    { 
        int current_pos = 5; 
        string path = "011101"; 

        Console.Write(getDistinctPoints(current_pos, path)); 
    } 
} 

// This code is contributed by shrikanth13 

```

## PHP

```php

<?php 
// PHP implementation of the approach  

// Utility function to return the number  
// of distinct elements in an array  
function countDistinct($arr, $len)  
{   
    $hs = array();  

    for ($i = 0; $i < $len; $i++)  
    {  
        // add all the elements to the HashSet  
        array_push($hs, $arr[$i]);  
    }  

    $hs = array_unique($hs); 

    // Return the size of hashset as  
    // it consists of all unique elements  
    return count($hs);  
}  

// Function to return the count of  
// positions the person went to  
function getDistinctPoints($current_pos, $path)  
{  

    // Length of path  
    $len = strlen($path);  

    // Array to store all the points traveled  
    $points = array();  

    // The first point is the current_pos  
    $points[0] = $current_pos;  

    // For all the directions in path  
    for ($i = 0; $i < $len; $i++) 
    {  

        // Get whether the direction was left or right  
        $ch = $path[$i];  

        // If the direction is left  
        if ($ch == '0') 
        {  

            // Decrement the current position by 1  
            $current_pos--;  

            // Store the current position in array  
            $points[$i + 1] = $current_pos;  
        }  

        // If the direction is right  
        else 
        {  

            // Increment the current position by 1  
            $current_pos++;  

            // Store the current position in array  
            $points[$i + 1] = $current_pos;  
        }  
    }  

    return countDistinct($points, $len + 1);  
}  

// Driver code  
$current_pos = 5;  
$path = "011101";  

echo getDistinctPoints($current_pos, $path);  

// This code is contributed by Ryuga  
?> 

```

**Output:**

```
4

```



* * *

* * *



