# 到达终点的最小跳数

> 原文： [https://www.geeksforgeeks.org/minimum-number-of-jumps-to-reach-end-of-a-given-array/](https://www.geeksforgeeks.org/minimum-number-of-jumps-to-reach-end-of-a-given-array/)

给定一个整数数组，其中每个元素代表可以从该元素进行的最大步数。 编写一个函数以返回到达数组末尾（从第一个元素开始）的最小跳转数。 如果一个元素为 0，则不能在该元素中移动。

**示例**：

```
Input: arr[] = {1, 3, 5, 8, 9, 2, 6, 7, 6, 8, 9}
Output: 3 (1-> 3 -> 8 -> 9)
Explanation: Jump from 1st element 
to 2nd element as there is only 1 step, 
now there are three options 5, 8 or 9\. 
If 8 or 9 is chosen then the end node 9 
can be reached. So 3 jumps are made.

Input:  arr[] = {1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1}
Output: 10
Explanation: In every step a jump 
is needed so the count of jumps is 10.

```

第一个元素是 1，因此只能转到 3。第二个元素是 3，因此最多可以执行 3 个步骤，例如到 5 或 8 或 9。



 **方法 1**：朴素递归方法。

**方法**：朴素的方法是从第一个元素开始，然后递归调用从第一个元素可到达的所有元素。 可以使用从第一个可到达元素开始到达终点所需的最小跳数来计算从第一个到达终点的最小跳数。

`minJumps(start, end) = Min(minJumps(k. end))`，从开始就可以到达所有`k`。

## C++ 

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to return the minimum number 
// of jumps to reach arr[h] from arr[l] 
int minJumps(int arr[], int n) 
{ 

    // Base case: when source and 
    // destination are same 
    if (n == 1) 
        return 0; 

    // Traverse through all the points 
    // reachable from arr[l] 
    // Recursivel, get the minimum number 
    // of jumps needed to reach arr[h] from 
    // these reachable points 
    int res = INT_MAX; 
    for (int i = n - 2; i >= 0; i--) { 
        if (i + arr[i] >= n - 1) { 
            int sub_res = minJumps(arr, i + 1); 
            if (sub_res != INT_MAX) 
                res = min(res, sub_res + 1); 
        } 
    } 

    return res; 
} 

// Driver Code 
int main() 
{ 
    int arr[] = { 1, 3, 6, 3, 2, 
                  3, 6, 8, 9, 5 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << "Minimum number of jumps to"; 
    cout << " reach the end is " << minJumps(arr, n); 
    return 0; 
} 

// This code is contributed 
// by Shivi_Aggarwal 

```

## Java

```java
// Javaprogram to find Minimum 
// number of jumps to reach end 
import java.util.*; 
import java.io.*; 
  
class GFG { 
    // Returns minimum number of 
    // jumps to reach arr[h] from arr[l] 
    static int minJumps(int arr[], int l, int h) 
    { 
        // Base case: when source 
        // and destination are same 
        if (h == l) 
            return 0; 
  
        // When nothing is reachable 
        // from the given source 
        if (arr[l] == 0) 
            return Integer.MAX_VALUE; 
  
        // Traverse through all the points 
        // reachable from arr[l]. Recursively 
        // get the minimum number of jumps 
        // needed to reach arr[h] from these 
        // reachable points. 
        int min = Integer.MAX_VALUE; 
        for (int i = l + 1; i <= h 
                            && i <= l + arr[l]; 
             i++) { 
            int jumps = minJumps(arr, i, h); 
            if (jumps != Integer.MAX_VALUE && jumps + 1 < min) 
                min = jumps + 1; 
        } 
        return min; 
    } 
  
    // Driver code 
    public static void main(String args[]) 
    { 
        int arr[] = { 1, 3, 6, 3, 2, 3, 6, 8, 9, 5 }; 
        int n = arr.length; 
        System.out.print("Minimum number of jumps to reach end is "
                         + minJumps(arr, 0, n - 1)); 
    } 
} 
  
// This code is contributed by Sahil_Bansall
```

## Python3

```py
# Python3 program to find Minimum  
# number of jumps to reach end 
  
# Returns minimum number of jumps 
# to reach arr[h] from arr[l] 
def minJumps(arr, l, h): 
  
    # Base case: when source and 
    # destination are same 
    if (h == l): 
        return 0
  
    # when nothing is reachable  
    # from the given source 
    if (arr[l] == 0): 
        return float('inf') 
  
    # Traverse through all the points  
    # reachable from arr[l]. Recursively  
    # get the minimum number of jumps  
    # needed to reach arr[h] from  
    # these reachable points. 
    min = float('inf') 
    for i in range(l + 1, h + 1): 
        if (i < l + arr[l] + 1): 
            jumps = minJumps(arr, i, h) 
            if (jumps != float('inf') and 
                       jumps + 1 < min): 
                min = jumps + 1
  
    return min
  
# Driver program to test above function 
arr = [1, 3, 6, 3, 2, 3, 6, 8, 9, 5] 
n = len(arr) 
print('Minimum number of jumps to reach', 
     'end is', minJumps(arr, 0, n-1)) 
  
# This code is contributed by Soumen Ghosh
```

## C#

```cs
// C# program to find Minimum 
// number of jumps to reach end 
using System; 
  
class GFG { 
    // Returns minimum number of 
    // jumps to reach arr[h] from arr[l] 
    static int minJumps(int[] arr, int l, int h) 
    { 
        // Base case: when source 
        // and destination are same 
        if (h == l) 
            return 0; 
  
        // When nothing is reachable 
        // from the given source 
        if (arr[l] == 0) 
            return int.MaxValue; 
  
        // Traverse through all the points 
        // reachable from arr[l]. Recursively 
        // get the minimum number of jumps 
        // needed to reach arr[h] from these 
        // reachable points. 
        int min = int.MaxValue; 
        for (int i = l + 1; i <= h && i <= l + arr[l]; i++) { 
            int jumps = minJumps(arr, i, h); 
            if (jumps != int.MaxValue && jumps + 1 < min) 
                min = jumps + 1; 
        } 
        return min; 
    } 
  
    // Driver code 
    public static void Main() 
    { 
        int[] arr = { 1, 3, 6, 3, 2, 3, 6, 8, 9, 5 }; 
        int n = arr.Length; 
        Console.Write("Minimum number of jumps to reach end is "
                      + minJumps(arr, 0, n - 1)); 
    } 
} 
  
// This code is contributed by Sam007
```

## PHP

```php
<?php 
// php program to find Minimum  
// number of jumps to reach end 
  
// Returns minimum number of jumps  
// to reach arr[h] from arr[l] 
function minJumps($arr, $l, $h) 
{ 
      
    // Base case: when source and 
    // destination are same 
    if ($h == $l) 
        return 0; 
      
    // When nothing is reachable 
    // from the given source 
    if ($arr[$l] == 0) 
        return INT_MAX; 
      
    // Traverse through all the points  
    // reachable from arr[l]. Recursively 
    // get the minimum number of jumps 
    // needed to reach arr[h] from these 
    // reachable points. 
    $min = 999999; 
      
    for ($i = $l+1; $i <= $h &&  
             $i <= $l + $arr[$l]; $i++) 
    { 
        $jumps = minJumps($arr, $i, $h); 
          
        if($jumps != 999999 &&  
                     $jumps + 1 < $min) 
            $min = $jumps + 1; 
    } 
      
    return $min; 
} 
  
// Driver program to test above function 
$arr = array(1, 3, 6, 3, 2, 3, 6, 8, 9, 5); 
$n = count($arr); 
  
echo "Minimum number of jumps to reach "
     . "end is ". minJumps($arr, 0, $n-1); 
      
// This code is contributed by Sam007 
?>
```

输出：

```
Minimum number of jumps to reach end is 4
```

复杂度分析：

+   时间复杂度：`O(n ^ n)`。

    从一个元素移出最多`n`种可能的方式。 因此最大步数可以为`N ^ N`，因此时间复杂度的上限为`O(n ^ n)`。

+   辅助空间：`O(1)`。

    不需要空间（如果递归堆栈空间被忽略）。

注意：如果跟踪此方法的执行，则可以看到会有重叠的子问题。 例如，`minJumps(3, 9)`将被调用两次，因为从`arr[1]`和`arr[2]`可以到达`arr[3]`。 因此，此问题同时具有动态编程的属性（最佳子结构和重叠子问题）。

方法 2 - 动态编程：

方法：

1.  这样，从左到右创建一个`jumps[]`数组，使`jumps[i]`指示从`arr[0]`达到`arr[i]`所需的最小跳转数。
2.  要填充跳转数组，请运行一个嵌套循环内循环计数器为`j`，外循环计数为`i`。
3.  从 1 到`n-1`的外循环，从 0 到`n-1`的内循环。
4.  如果`i`小于`j + arr [j]`，则将`jumps[i]`设置为`jumps[i]`和`jumps [j] + 1`的最小值。最初将`jump[i]`设置为`INT_MAX`。
5.  最后，返回`jump[n-1]`。

## C++

```cpp
// C++ program for Minimum number 
// of jumps to reach end 
#include <bits/stdc++.h> 
using namespace std; 
  
int min(int x, int y) { return (x < y) ? x : y; } 
  
// Returns minimum number of jumps 
// to reach arr[n-1] from arr[0] 
int minJumps(int arr[], int n) 
{ 
    // jumps[n-1] will hold the result 
    int* jumps = new int[n]; 
    int i, j; 
  
    if (n == 0 || arr[0] == 0) 
        return INT_MAX; 
  
    jumps[0] = 0; 
  
    // Find the minimum number of jumps to reach arr[i] 
    // from arr[0], and assign this value to jumps[i] 
    for (i = 1; i < n; i++) { 
        jumps[i] = INT_MAX; 
        for (j = 0; j < i; j++) { 
            if (i <= j + arr[j] && jumps[j] != INT_MAX) { 
                jumps[i] = min(jumps[i], jumps[j] + 1); 
                break; 
            } 
        } 
    } 
    return jumps[n - 1]; 
} 
  
// Driver code 
int main() 
{ 
    int arr[] = { 1, 3, 6, 1, 0, 9 }; 
    int size = sizeof(arr) / sizeof(int); 
    cout << "Minimum number of jumps to reach end is "
         << minJumps(arr, size); 
    return 0; 
} 
  
// This is code is contributed by rathbhupendra
```

## C

```c
#include <limits.h> 
#include <stdio.h> 
  
int min(int x, int y) { return (x < y) ? x : y; } 
  
// Returns minimum number of 
// jumps to reach arr[n-1] from arr[0] 
int minJumps(int arr[], int n) 
{ 
    // jumps[n-1] will hold the result 
    int jumps[n]; 
    int i, j; 
  
    if (n == 0 || arr[0] == 0) 
        return INT_MAX; 
  
    jumps[0] = 0; 
  
    // Find the minimum number of 
    // jumps to reach arr[i] 
    // from arr[0], and assign this 
    // value to jumps[i] 
    for (i = 1; i < n; i++) { 
        jumps[i] = INT_MAX; 
        for (j = 0; j < i; j++) { 
            if (i <= j + arr[j] && jumps[j] != INT_MAX) { 
                jumps[i] = min(jumps[i], jumps[j] + 1); 
                break; 
            } 
        } 
    } 
    return jumps[n - 1]; 
} 
  
// Driver program to test above function 
int main() 
{ 
    int arr[] = { 1, 3, 6, 1, 0, 9 }; 
    int size = sizeof(arr) / sizeof(int); 
    printf("Minimum number of jumps to reach end is %d ", 
           minJumps(arr, size)); 
    return 0; 
}
```

## Java

```java
// JAVA Code for Minimum number 
// of jumps to reach end 
class GFG { 
  
    private static int minJumps(int[] arr, int n) 
    { 
        // jumps[n-1] will hold the 
        int jumps[] = new int[n]; 
        // result 
        int i, j; 
  
        // if first element is 0, 
        if (n == 0 || arr[0] == 0) 
            return Integer.MAX_VALUE; 
        // end cannot be reached 
  
        jumps[0] = 0; 
  
        // Find the minimum number of jumps to reach arr[i] 
        // from arr[0], and assign this value to jumps[i] 
        for (i = 1; i < n; i++) { 
            jumps[i] = Integer.MAX_VALUE; 
            for (j = 0; j < i; j++) { 
                if (i <= j + arr[j] 
                    && jumps[j] 
                           != Integer.MAX_VALUE) { 
                    jumps[i] = Math.min(jumps[i], jumps[j] + 1); 
                    break; 
                } 
            } 
        } 
        return jumps[n - 1]; 
    } 
  
    // driver program to test above function 
    public static void main(String[] args) 
    { 
        int arr[] = { 1, 3, 6, 1, 0, 9 }; 
  
        System.out.println("Minimum number of jumps to reach end is : "
                           + minJumps(arr, arr.length)); 
    } 
} 
  
// This code is contributed by Arnav Kr. Mandal.
```

## Python3

```py
# Python3 program to find Minimum  
# number of jumps to reach end 
  
# Returns minimum number of jumps 
# to reach arr[n-1] from arr[0] 
def minJumps(arr, n): 
    jumps = [0 for i in range(n)] 
  
    if (n == 0) or (arr[0] == 0): 
        return float('inf') 
  
    jumps[0] = 0
  
    # Find the minimum number of  
    # jumps to reach arr[i] from  
    # arr[0] and assign this  
    # value to jumps[i] 
    for i in range(1, n): 
        jumps[i] = float('inf') 
        for j in range(i): 
            if (i <= j + arr[j]) and (jumps[j] != float('inf')): 
                jumps[i] = min(jumps[i], jumps[j] + 1) 
                break
    return jumps[n-1] 
  
# Driver Program to test above function 
arr = [1, 3, 6, 1, 0, 9] 
size = len(arr) 
print('Minimum number of jumps to reach', 
      'end is', minJumps(arr, size)) 
  
# This code is contributed by Soumen Ghosh
```

## C#

```cs
// C# Code for Minimum number of jumps to reach end 
using System; 
  
class GFG { 
    static int minJumps(int[] arr, int n) 
    { 
        // jumps[n-1] will hold the 
        // result 
        int[] jumps = new int[n]; 
  
        // if first element is 0, 
        if (n == 0 || arr[0] == 0) 
  
            // end cannot be reached 
            return int.MaxValue; 
  
        jumps[0] = 0; 
  
        // Find the minimum number of 
        // jumps to reach arr[i] 
        // from arr[0], and assign 
        // this value to jumps[i] 
        for (int i = 1; i < n; i++) { 
            jumps[i] = int.MaxValue; 
            for (int j = 0; j < i; j++) { 
                if (i <= j + arr[j] && jumps[j] != int.MaxValue) { 
                    jumps[i] = Math.Min(jumps[i], jumps[j] + 1); 
                    break; 
                } 
            } 
        } 
        return jumps[n - 1]; 
    } 
  
    // Driver program 
    public static void Main() 
    { 
        int[] arr = { 1, 3, 6, 1, 0, 9 }; 
        Console.Write("Minimum number of jumps to reach end is : " + minJumps(arr, arr.Length)); 
    } 
} 
  
// This code is contributed by Sam007
```

## PHP

```php
<?php 
// PHP code for Minimum number of 
// jumps to reach end 
  
// Returns minimum number of jumps 
// to reach arr[n-1] from arr[0] 
function minJumps($arr, $n) 
{ 
    // jumps[n-1] will 
    // hold the result 
    $jumps = array($n); 
      
    if ($n == 0 || $arr[0] == 0) 
        return 999999; 
  
    $jumps[0] = 0; 
  
    // Find the minimum number of 
    // jumps to reach arr[i] 
    // from arr[0], and assign  
    // this value to jumps[i] 
    for ($i = 1; $i < $n; $i++) 
    { 
        $jumps[$i] = 999999; 
        for ($j = 0; $j < $i; $j++) 
        { 
            if ($i <= $j + $arr[$j] &&  
                $jumps[$j] != 999999) 
            { 
                $jumps[$i] = min($jumps[$i],  
                             $jumps[$j] + 1); 
                break; 
            } 
        } 
    } 
    return $jumps[$n-1]; 
} 
  
    // Driver Code 
    $arr = array(1, 3, 6, 1, 0, 9); 
    $size = count($arr); 
    echo "Minimum number of jumps to reach end is ".  
                             minJumps($arr, $size); 
                               
// This code is contributed by Sam007 
?>
```

输出：

```
Minimum number of jumps to reach end is 3
```

感谢 paras 建议使用此方法。

时间复杂度：`O(n ^ 2)`。

方法 3：动态规划：

在此方法中，我们从右到左构建了`jumps[]`数组，使得`jumps[i]`表示从`arr[i]`达到`arr[n-1]`所需的最小跳转数。 最后，我们返回`arr[0]`。

## C++

```cpp
// CPP program to find Minimum 
// number of jumps to reach end 
#include <bits/stdc++.h> 
using namespace std; 
  
// Returns Minimum number of 
// jumps to reach end 
int minJumps(int arr[], int n) 
{ 
    // jumps[0] will hold the result 
    int* jumps = new int[n]; 
    int min; 
  
    // Minimum number of jumps needed 
    // to reach last element from last 
    // elements itself is always 0 
    jumps[n - 1] = 0; 
  
    // Start from the second element, 
    // move from right to left and 
    // construct the jumps[] array where 
    // jumps[i] represents minimum number 
    // of jumps needed to reach 
    // arr[m-1] from arr[i] 
    for (int i = n - 2; i >= 0; i--) { 
        // If arr[i] is 0 then arr[n-1] 
        // can't be reached from here 
        if (arr[i] == 0) 
            jumps[i] = INT_MAX; 
  
        // If we can direcly reach to 
        // the end point from here then 
        // jumps[i] is 1 
        else if (arr[i] >= n - i - 1) 
            jumps[i] = 1; 
  
        // Otherwise, to find out the minimum 
        // number of jumps needed to reach 
        // arr[n-1], check all the points 
        // reachable from here and jumps[] 
        // value for those points 
        else { 
            // initialize min value 
            min = INT_MAX; 
  
            // following loop checks with all 
            // reachable points and takes 
            // the minimum 
            for (int j = i + 1; j < n && j <= arr[i] + i; j++) { 
                if (min > jumps[j]) 
                    min = jumps[j]; 
            } 
  
            // Handle overflow 
            if (min != INT_MAX) 
                jumps[i] = min + 1; 
            else
                jumps[i] = min; // or INT_MAX 
        } 
    } 
  
    return jumps[0]; 
} 
  
// Driver program to test above function 
int main() 
{ 
    int arr[] = { 1, 3, 6, 1, 0, 9 }; 
    int size = sizeof(arr) / sizeof(int); 
    cout << "Minimum number of jumps to reach"
         << " end is " << minJumps(arr, size); 
    return 0; 
}
```

## Java

```java
// Java program to find Minimum 
// number of jumps to reach end 
class GFG { 
    // Returns Minimum number 
    // of jumps to reach end 
    static int minJumps(int arr[], 
                        int n) 
    { 
        // jumps[0] will 
        // hold the result 
        int[] jumps = new int[n]; 
        int min; 
  
        // Minimum number of jumps 
        // needed to reach last 
        // element from last elements 
        // itself is always 0 
        jumps[n - 1] = 0; 
  
        // Start from the second 
        // element, move from right 
        // to left and construct the 
        // jumps[] array where jumps[i] 
        // represents minimum number of 
        // jumps needed to reach arr[m-1] 
        // from arr[i] 
        for (int i = n - 2; i >= 0; i--) { 
            // If arr[i] is 0 then arr[n-1] 
            // can't be reached from here 
            if (arr[i] == 0) 
                jumps[i] = Integer.MAX_VALUE; 
  
            // If we can direcly reach to 
            // the end point from here then 
            // jumps[i] is 1 
            else if (arr[i] >= n - i - 1) 
                jumps[i] = 1; 
  
            // Otherwise, to find out 
            // the minimum number of 
            // jumps needed to reach 
            // arr[n-1], check all the 
            // points reachable from 
            // here and jumps[] value 
            // for those points 
            else { 
                // initialize min value 
                min = Integer.MAX_VALUE; 
  
                // following loop checks 
                // with all reachable points 
                // and takes the minimum 
                for (int j = i + 1; j < n && j <= arr[i] + i; j++) { 
                    if (min > jumps[j]) 
                        min = jumps[j]; 
                } 
  
                // Handle overflow 
                if (min != Integer.MAX_VALUE) 
                    jumps[i] = min + 1; 
                else
                    jumps[i] = min; // or Integer.MAX_VALUE 
            } 
        } 
  
        return jumps[0]; 
    } 
  
    // Driver Code 
    public static void main(String[] args) 
    { 
        int[] arr = { 1, 3, 6, 1, 0, 9 }; 
        int size = arr.length; 
        System.out.println("Minimum number of"
                           + " jumps to reach end is " + minJumps(arr, size)); 
    } 
} 
  
// This code is contributed by mits.
```

## Python3

```py
# Python3 progrma to find Minimum  
# number of jumps to reach end 
  
# Returns Minimum number of 
# jumps to reach end 
def minJumps(arr, n): 
      
    # jumps[0] will hold the result 
    jumps = [0 for i in range(n)]  
  
    # Minimum number of jumps needed 
    # to reach last element from  
    # last elements itself is always 0 
    # jumps[n-1] is also initialized to 0 
  
    # Start from the second element,  
    # move from right to left and  
    # construct the jumps[] array where 
    # jumps[i] represents minimum number 
    # of jumps needed to reach arr[m-1] 
    # form arr[i] 
    for i in range(n-2, -1, -1): 
          
        # If arr[i] is 0 then arr[n-1] 
        # can't be reached from here 
        if (arr[i] == 0): 
            jumps[i] = float('inf') 
  
        # If we can directly reach to  
        # the end point from here then 
        # jumps[i] is 1 
        elif (arr[i] >= n - i - 1): 
            jumps[i] = 1
  
        # Otherwise, to find out the  
        # minimum number of jumps 
        # needed to reach arr[n-1],  
        # check all the points 
        # reachable from here and  
        # jumps[] value for those points 
        else: 
            # initialize min value 
            min = float('inf')  
  
            # following loop checks with  
            # all reachavle points and 
            # takes the minimum 
            for j in range(i + 1, n): 
                if (j <= arr[i] + i): 
                    if (min > jumps[j]): 
                        min = jumps[j] 
                          
            # Handle overflow 
            if (min != float('inf')): 
                jumps[i] = min + 1
            else: 
                # or INT_MAX 
                jumps[i] = min 
  
    return jumps[0] 
  
# Driver program to test above function 
arr = [1, 3, 6, 3, 2, 3, 6, 8, 9, 5] 
n = len(arr) 
print('Minimum number of jumps to reach', 
      'end is', minJumps(arr, n-1)) 
        
# This code is contributed by Soumen Ghosh
```

## C#

```cs
// C# program to find Minimum 
// number of jumps to reach end 
using System; 
  
class GFG { 
    // Returns Minimum number 
    // of jumps to reach end 
    public static int minJumps(int[] arr, int n) 
    { 
        // jumps[0] will 
        // hold the result 
        int[] jumps = new int[n]; 
        int min; 
  
        // Minimum number of jumps needed to 
        // reach last element from last elements 
        // itself is always 0 
        jumps[n - 1] = 0; 
  
        // Start from the second element, move 
        // from right to left and construct the 
        // jumps[] array where jumps[i] represents 
        // minimum number of jumps needed to reach 
        // arr[m-1] from arr[i] 
        for (int i = n - 2; i >= 0; i--) { 
            // If arr[i] is 0 then arr[n-1] 
            // can't be reached from here 
            if (arr[i] == 0) { 
                jumps[i] = int.MaxValue; 
            } 
  
            // If we can direcly reach to the end 
            // point from here then jumps[i] is 1 
            else if (arr[i] >= n - i - 1) { 
                jumps[i] = 1; 
            } 
  
            // Otherwise, to find out the minimum 
            // number of jumps needed to reach 
            // arr[n-1], check all the points 
            // reachable from here and jumps[] value 
            // for those points 
            else { 
                // initialize min value 
                min = int.MaxValue; 
  
                // following loop checks with all 
                // reachable points and takes the minimum 
                for (int j = i + 1; j < n && j <= arr[i] + i; j++) { 
                    if (min > jumps[j]) { 
                        min = jumps[j]; 
                    } 
                } 
  
                // Handle overflow 
                if (min != int.MaxValue) { 
                    jumps[i] = min + 1; 
                } 
                else { 
                    jumps[i] = min; // or Integer.MAX_VALUE 
                } 
            } 
        } 
  
        return jumps[0]; 
    } 
  
    // Driver Code 
    public static void Main(string[] args) 
    { 
        int[] arr = new int[] { 1, 3, 6, 1, 0, 9 }; 
        int size = arr.Length; 
        Console.WriteLine("Minimum number of"
                          + " jumps to reach end is " + minJumps(arr, size)); 
    } 
} 
  
// This code is contributed by Shrikant13
```

## PHP

```php
<?php 
// PHP program to find Minimum  
// number of jumps to reach end 
  
// Returns Minimum number of jumps 
// to reach end 
function minJumps($arr, $n) 
{  
    // jumps[0] will hold the result 
    $jumps[$n] = array();  
    $min; 
  
    // Minimum number of jumps needed  
    // to reach last element from last 
    // elements itself is always 0 
    $jumps[$n-1] = array(0); 
  
    // Start from the second element,  
    // move from right to left and  
    // construct the jumps[] array where 
    // jumps[i] represents minimum number 
    // of jumps needed to reach  
    // arr[m-1] from arr[i] 
    for ($i = $n - 2; $i >= 0; $i--) 
    { 
        // If arr[i] is 0 then arr[n-1]  
        // can't be reached from here 
        if ($arr[$i] == 0) 
            $jumps[$i] = PHP_INT_MAX; 
  
        // If we can direcly reach to  
        // the end point from here then 
        // jumps[i] is 1 
        else if ($arr[$i] >= ($n - $i) - 1) 
            $jumps[$i] = 1; 
  
        // Otherwise, to find out the minimum 
        // number of jumps needed to reach  
        // arr[n-1], check all the points  
        // reachable from here and jumps[]  
        // value for those points 
        else
        {  
            // initialize min value 
            $min = PHP_INT_MAX;  
  
            // following loop checks with all 
            // reachable points and takes  
            // the minimum 
            for ($j = $i + 1; $j < $n && 
                 $j <= $arr[$i] + $i; $j++) 
            { 
                if ($min > $jumps[$j]) 
                    $min = $jumps[$j]; 
            }  
  
            // Handle overflow  
            if ($min != PHP_INT_MAX) 
                $jumps[$i] = $min + 1; 
            else
                $jumps[$i] = $min; // or INT_MAX 
        } 
    } 
  
    return $jumps[0]; 
} 
  
// Driver Code 
$arr = array(1, 3, 6, 1, 0, 9); 
$size = sizeof($arr); 
echo "Minimum number of jumps to reach", 
     " end is ", minJumps($arr, $size); 
  
// This code is contributed by ajit. 
?>
```

输出：

```
Minimum number of jumps to reach end is 3
```

复杂度分析：

+   时间复杂度：`O(n ^ 2)`。

    需要对数组进行嵌套遍历。
+   辅助空间：`O(n)`。
    
    要存储 DP 阵列，需要线性空间。

[到达终点的最小跳数 | 系列 2（`O(n)`解）](https://www.geeksforgeeks.org/minimum-number-jumps-reach-endset-2on-solution/)。