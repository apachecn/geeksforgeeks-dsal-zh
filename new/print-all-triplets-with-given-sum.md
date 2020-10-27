# 打印具有给定总和的所有三胞胎

给定一系列不同的元素。 任务是在数组中找到三元组，其总和等于给定数。

**示例**：

```
Input: arr[] = {0, -1, 2, -3, 1}
        sum = -2
Output:  0 -3  1
        -1  2 -3
If we calculate the sum of the output,
0 + (-3) + 1 = -2
(-1) + 2 + (-3) = -2

Input: arr[] = {1, -2, 1, 0, 5}
       sum = 0
Output: 1 -2  1
If we calculate the sum of the output,
1 + (-2) + 1 = 0

```

**<u>方法 1</u> **：蛮力。

**方法**：这些类型问题中的蛮力方法旨在检查数组中存在的所有可能的三元组。 答案为 **sum = Target sum** 的三元组。 现在出现的问题是如何检查所有可能的三胞胎。 要检查所有可能的**重复项**，请将指针固定在一个元素上，然后为每个此类元素遍历数组并检查和。 这将是所有可能的**小片段**的总和。
同样，为了检查所有可能的**三元组**，可以固定两个指针并将第三个指针移到数组上，并在到达数组末尾时立即增加第二个指针并再次重复该指针。

**算法**：

1.  取三个指针 **i** ， **j** ， **k** 。
2.  将 **i** 初始化为零，并为 **i** 启动嵌套循环。
3.  用**（i + 1）**初始化 **j** 并为 **j** 启动嵌套循环。
4.  用**（j + 1）**初始化 **k** 并启动 **k** 的循环。
5.  如果**目标== arr [i] + arr [j] + arr [k]，则**中断循环并打印 **arr [i]，arr [j]，arr [k]** 的值 ]。
6.  否则保持 **k** 递增，直到等于**最后索引**为止。
7.  **转到步骤 2** 并递增 **j** ，对于 **j** 的每个值，运行 **k** 的内部循环。
8.  如果 **j** 等于**倒数第二个索引** **转到步骤 1** 并递增 **i** 的值，直到**倒数第三个索引**，然后再次继续整个过程，直到 **i** 的值等于最后一个索引。

## C++

```cpp

// A simple C++ program to find three elements 
// whose sum is equal to given sum 
#include <bits/stdc++.h> 
using namespace std; 

// Prints all triplets in arr[] with given sum 
void findTriplets(int arr[], int n, int sum) 
{ 
    for (int i = 0; i < n - 2; i++) { 
        for (int j = i + 1; j < n - 1; j++) { 
            for (int k = j + 1; k < n; k++) { 
                if (arr[i] + arr[j] + arr[k] == sum) { 
                    cout << arr[i] << " "
                         << arr[j] << " "
                         << arr[k] << endl; 
                } 
            } 
        } 
    } 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 0, -1, 2, -3, 1 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    findTriplets(arr, n, -2); 
    return 0; 
} 

```

## Java

```java

// A simple Java program 
// to find three elements 
// whose sum is equal to 
// given sum 
import java.io.*; 

class GFG { 

    // Prints all triplets in 
    // arr[] with given sum 
    static void findTriplets(int arr[], 
                             int n, int sum) 
    { 
        for (int i = 0; 
             i < n - 2; i++) { 
            for (int j = i + 1; 
                 j < n - 1; j++) { 
                for (int k = j + 1; 
                     k < n; k++) { 
                    if (arr[i] + arr[j] + arr[k] == sum) { 
                        System.out.println( 
                            arr[i] + " " + arr[j] 
                            + " " + arr[k]); 
                    } 
                } 
            } 
        } 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        int arr[] = { 0, -1, 2, -3, 1 }; 
        int n = arr.length; 
        findTriplets(arr, n, -2); 
    } 
} 

// This code is contributed by m_kit 

```

## Python 3

```

# A simple Python 3 program 
# to find three elements 
# whose sum is equal to  
# given sum 

# Prints all triplets in 
# arr[] with given sum 
def findTriplets(arr, n, sum): 

    for i in range(0, n - 2):  
        for j in range(i + 1, n - 1):  
            for k in range(j + 1, n): 
                if (arr[i] + arr[j] + 
                    arr[k] == sum):  
                    print(arr[i], " ",  
                          arr[j], " ",  
                          arr[k], sep = "") 

# Driver code 
arr = [ 0, -1, 2, -3, 1 ] 
n = len(arr)  
findTriplets(arr, n, -2) 

# This code is contributed  
# by Smitha 

```

## C#

```cs

// A simple C# program 
// to find three elements 
// whose sum is equal to 
// given sum 
using System; 

class GFG { 

    // Prints all triplets in 
    // arr[] with given sum 
    static void findTriplets(int[] arr, 
                             int n, int sum) 
    { 
        for (int i = 0; 
             i < n - 2; i++) { 
            for (int j = i + 1; 
                 j < n - 1; j++) { 
                for (int k = j + 1; 
                     k < n; k++) { 
                    if (arr[i] + arr[j] + arr[k] == sum) { 
                        Console.WriteLine( 
                            arr[i] + " " + arr[j] 
                            + " " + arr[k]); 
                    } 
                } 
            } 
        } 
    } 

    // Driver code 
    static public void Main() 
    { 
        int[] arr = { 0, -1, 2, -3, 1 }; 
        int n = arr.Length; 
        findTriplets(arr, n, -2); 
    } 
} 
// This code is contributed by akt_mit 

```

## PHP

```php

<?php 
// A simple PHP program to  
// find three elements whose 
// sum is equal to given sum 

// Prints all triplets in 
// arr[] with given sum 
function findTriplets($arr, $n, $sum) 
{ 
    for ($i = 0; $i < $n - 2; $i++)  
    { 
        for ($j = $i + 1; $j < $n - 1; $j++) 
        { 
            for ($k = $j + 1; $k < $n; $k++) 
            { 
                if ($arr[$i] + $arr[$j] +  
                    $arr[$k] == $sum)  
                { 
                    echo $arr[$i], " ", 
                         $arr[$j], " ", 
                         $arr[$k], "\n"; 
                } 
            } 
        } 
    } 
} 

// Driver code 
$arr = array (0, -1, 2, -3, 1); 
$n = sizeof($arr); 
findTriplets($arr, $n, -2); 

// This code is contributed by aj_36 
?> 

```

**Output :**

```
0 -3 1
-1 2 -3

```

**复杂度分析**：

*   **时间复杂度**：O（n <sup>3</sup> ）。
    由于使用了三个嵌套的 for 循环。
*   **辅助空间**：O（1）。
    由于尚未使用任何数据结构来存储值。

**<u>方法 2</u> **：哈希。
**方法**：
散列可用于解决此问题。 HashTable 或 HashMaps 允许我们以恒定的时间复杂度执行查找或搜索操作。 如果可以发现对于每个可能的二元组，数组中已经存在一个可以使 **sum = target sum** 的元素，那么该问题将以有效的方式解决。

要实现哈希，我们可以在 C++ 中使用 [unordered_set 或在 Java](https://www.geeksforgeeks.org/unorderd_set-stl-uses/) 中使用 [HashSet。](https://www.geeksforgeeks.org/hashset-in-java/)

*   当我们修复第一个指针**（例如 a）**时，使用第二个指针**（例如 b）**遍历数组，并继续将遇到的元素存储在 **HashTable** 中。
*   一旦我们发现等于 **HashTable** 中已经存在的剩余总和**（目标总和-（a + b））**的元素，就打印三元组。

**算法**：

1.  从 **i = 0** 直到第**（n-2）个**索引开始外循环。
2.  对于每次迭代，请创建无序集合，然后进入内部循环。
3.  从 **j =（i + 1）**开始内部循环[（因为我们已经检查过的值不会出现在有效的三元组中），直到**最后一个索引为止。**
4.  检查是否存在元素 **x =目标-（arr [i] + arr [j]）**，然后找到三元组并进行打印。
5.  否则将值推入集合以供以后参考。
6.  **i** 的增量，然后转到步骤 2。

**伪代码**：

```
Run a loop from i=0 to n-2
  Create an empty hash table
  Run inner loop from j=i+1 to n-1
      If -(arr[i] + arr[j]) is present in hash table
         print arr[i], arr[j] and -(arr[i] + arr[j])
      Else
         Insert arr[j] in hash table.

```

## C++

```cpp

// C++ program to find triplets in a given 
// array whose sum is equal to given sum. 
#include <bits/stdc++.h> 
using namespace std; 

// function to print triplets with given sum 
void findTriplets(int arr[], int n, int sum) 
{ 
    for (int i = 0; i < n - 1; i++) { 
        // Find all pairs with sum equals to 
        // "sum-arr[i]" 
        unordered_set<int> s; 
        for (int j = i + 1; j < n; j++) { 
            int x = sum - (arr[i] + arr[j]); 
            if (s.find(x) != s.end()) 
                printf("%d %d %d\n", x, arr[i], arr[j]); 
            else
                s.insert(arr[j]); 
        } 
    } 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 0, -1, 2, -3, 1 }; 
    int sum = -2; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    findTriplets(arr, n, sum); 
    return 0; 
} 

```

## Java

```java

// Java program to find triplets in a given 
// array whose sum is equal to given sum. 
import java.util.*; 

class GFG { 

    // function to print triplets with given sum 
    static void findTriplets(int arr[], int n, int sum) 
    { 
        for (int i = 0; i < n - 1; i++) { 
            // Find all pairs with sum equals to 
            // "sum-arr[i]" 
            HashSet<Integer> s = new HashSet<>(); 
            for (int j = i + 1; j < n; j++) { 
                int x = sum - (arr[i] + arr[j]); 
                if (s.contains(x)) 
                    System.out.printf( 
                        "%d %d %d\n", x, arr[i], arr[j]); 
                else
                    s.add(arr[j]); 
            } 
        } 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        int arr[] = { 0, -1, 2, -3, 1 }; 
        int sum = -2; 
        int n = arr.length; 
        findTriplets(arr, n, sum); 
    } 
} 

// This code is contributed by Rajput-Ji 

```

## Python3

```py

# Python3 program to find triplets in a given 
# array whose Sum is equal to given sum. 
import math as mt 

# function to print triplets with given sum 
def findTriplets(arr, n, Sum): 

    for i in range(n - 1): 

        # Find all pairs with Sum equals 
        # to "Sum-arr[i]" 
        s = dict() 
        for j in range(i + 1, n): 
            x = Sum - (arr[i] + arr[j]) 
            if x in s.keys(): 
                print(x, arr[i], arr[j]) 
            else: 
                s[arr[j]] = 1

# Driver code 
arr = [ 0, -1, 2, -3, 1 ] 
Sum = -2
n = len(arr) 
findTriplets(arr, n, Sum) 

# This code is contributed  
# by mohit kumar 29 

```

## C#

```cs

// C# program to find triplets in a given 
// array whose sum is equal to given sum. 
using System; 
using System.Collections.Generic; 

public class GFG { 

    // function to print triplets with given sum 
    static void findTriplets(int[] arr, int n, int sum) 
    { 
        for (int i = 0; i < n - 1; i++) { 
            // Find all pairs with sum equals to 
            // "sum-arr[i]" 
            HashSet<int> s = new HashSet<int>(); 
            for (int j = i + 1; j < n; j++) { 
                int x = sum - (arr[i] + arr[j]); 
                if (s.Contains(x)) 
                    Console.Write("{0} {1} {2}\n", x, arr[i], arr[j]); 
                else
                    s.Add(arr[j]); 
            } 
        } 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        int[] arr = { 0, -1, 2, -3, 1 }; 
        int sum = -2; 
        int n = arr.Length; 
        findTriplets(arr, n, sum); 
    } 
} 
// This code is contributed by Princi Singh 

```

**Output:**

```
-3 0 1
2 -1 -3

```

**复杂度分析**：

*   **时间复杂度**：O（n <sup>2</sup> ）。
    使用嵌套的 for 循环将时间复杂度提高到 n <sup>2</sup> 。
*   **辅助空间**：O（n）。
    由于 unordered_set 数据结构已用于存储值。

**<u>方法 3</u>** ：此方法使用排序和两指针技术的方法来解决上述问题。 该执行将涉及 O（n <sup>2</sup> ））时间复杂度和 O（1）空间复杂度。 这个想法基于这个帖子的[方法 2。](https://www.geeksforgeeks.org/find-a-triplet-that-sum-to-a-given-value/)

**方法**：使用排序技术可以将**两指针技术**付诸实践。 在二指针技术中，人们可以在**线性时间**中搜索具有目标和的一对。 这里的想法是固定一个指针**（例如 a）**，并使用其余指针在（a）处有效地找到具有所需总和**目标值的对。
现在，我们讨论如何使用两个指针技术来有效地找到所需的货币对。 用于两个指针技术的指针称为**（l 和 r）**。**

*   因此，如果**总和=值（a）+值（l）+值（r），则**超过了要求的总和，对于相同的**（a，l）**，要求的**值（ r）**应该小于前一个。 因此，递减 **r** 指针。
*   如果**和=值（a）+值（l）+值（r），则**小于所需的和，对于相同的**（a，r）**，所需的**值 （l）**应大于先前的值。 因此，增加 **l** 指针。

**算法**：

1.  对数组进行排序，然后为每个元素 **arr [i]** 搜索其他两个元素 **arr [l]，arr [r]** ，使得 **arr [i] + arr [ l] + arr [r] =目标总和**。
2.  使用**两指针技术**可以有效地搜索其他两个元素，因为对数组进行了排序。
3.  运行一个以 contol 变量为 **i** 的外循环，并为每次迭代初始化一个值 **l** ，它是 **i + 1** 和 **r [** 和最后一个索引。
4.  现在进入一个 while 循环，直到 **l < r** 的值运行。
5.  如果 **arr [i] + arr [l] + arr [r] >目标总和**，则将 **r** 减少 **1** ，因为所需总和小于 当前的总和减少值将是有需要的。
6.  如果 **arr [i] + arr [l] + arr [r] <目标总和**，则将 **l** 增加 **1** ，因为所需总和小于 当前的总和并增加的价值将是有需要的。
7.  如果 **arr [i] + arr [l] + arr [r] ==目标总和**，则打印值。
8.  递增 **i** 转到步骤 3。

**伪代码**：

```
1\. Sort all element of array
2\. Run loop from i=0 to n-2.
     Initialize two index variables l=i+1 and r=n-1
4\. while (l < r) 
     Check sum of arr[i], arr[l], arr[r] is
     given sum or not if sum is 'sum', then print 
     the triplet and do l++ and r--.
5\. If sum is less than given sum then l++
6\. If sum is greater than given sum then r--
7\. If not exist in array then print not found.

```

## C++

```cpp

// C++ program to find triplets in a given 
// array whose sum is given sum. 
#include <bits/stdc++.h> 
using namespace std; 

// Function to print triplets with given sum 
void findTriplets(int arr[], int n, int sum) 
{ 
    // Sort array elements 
    sort(arr, arr + n); 

    for (int i = 0; i < n - 1; i++) { 

        // initialize left and right 
        int l = i + 1; 
        int r = n - 1; 
        int x = arr[i]; 
        while (l < r) { 
            if (x + arr[l] + arr[r] == sum) { 

                // Print elements if it's sum is given sum. 
                printf("%d %d %d\n", x, arr[l], arr[r]); 
                l++; 
                r--; 
            } 

            // If sum of three elements is less 
            // than 'sum' then increment in left 
            else if (x + arr[l] + arr[r] < sum) 
                l++; 

            // if sum is greater than given sum, then 
            // decrement in right side 
            else
                r--; 
        } 
    } 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 0, -1, 2, -3, 1 }; 
    int sum = -2; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    findTriplets(arr, n, sum); 
    return 0; 
} 

```

## Java

```java

// Java program to find triplets 
// in a given array whose sum 
// is given sum. 
import java.io.*; 
import java.util.*; 

class GFG { 

    // function to print 
    // triplets with given sum 
    static void findTriplets(int[] arr, 
                             int n, int sum) 
    { 
        // sort array elements 
        Arrays.sort(arr); 

        for (int i = 0; 
             i < n - 1; i++) { 
            // initialize left and right 
            int l = i + 1; 
            int r = n - 1; 
            int x = arr[i]; 
            while (l < r) { 
                if (x + arr[l] + arr[r] == sum) { 
                    // print elements if it's 
                    // sum is given sum. 
                    System.out.println( 
                        x + " " + arr[l] + " "
                        + arr[r]); 
                    l++; 
                    r--; 
                } 

                // If sum of three elements 
                // is less than 'sum' then 
                // increment in left 
                else if (x + arr[l] + arr[r] < sum) 
                    l++; 

                // if sum is greater than 
                // given sum, then decrement 
                // in right side 
                else
                    r--; 
            } 
        } 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        int[] arr = new int[] { 0, -1, 2, -3, 1 }; 
        int sum = -2; 
        int n = arr.length; 
        findTriplets(arr, n, sum); 
    } 
} 

// This code is contributed 
// by Akanksha Rai(Abby_akku) 

```

## Python3

```py

# Python3 program to find triplets in a  
# given array whose sum is given sum. 

# function to print triplets with 
# given sum 
def findTriplets(arr, n, sum): 

    # sort array elements 
    arr.sort(); 

    for i in range(0, n - 1):  

        # initialize left and right 
        l = i + 1; 
        r = n - 1; 
        x = arr[i]; 
        while (l < r) : 
            if (x + arr[l] + arr[r] == sum) : 

                # print elements if it's sum  
                # is given sum. 
                print(x, arr[l], arr[r]); 
                l = l + 1; 
                r = r - 1; 

            # If sum of three elements is less 
            # than 'sum' then increment in left 
            elif (x + arr[l] + arr[r] < sum): 
                l = l + 1; 

            # if sum is greater than given sum,  
            # then decrement in right side 
            else: 
                r = r - 1; 

# Driver code 
arr = [ 0, -1, 2, -3, 1 ]; 
sum = -2; 
n = len(arr); 
findTriplets(arr, n, sum); 

# This code is contributed by  
# Shivi_Aggarwal  

```

## C#

```cs

// C# program to find triplets 
// in a given array whose sum 
// is given sum. 
using System; 

class GFG { 

    // function to print 
    // triplets with given sum 
    static void findTriplets(int[] arr, 
                             int n, int sum) 
    { 
        // sort array elements 
        Array.Sort(arr); 

        for (int i = 0; i < n - 1; i++) { 
            // initialize left and right 
            int l = i + 1; 
            int r = n - 1; 
            int x = arr[i]; 
            while (l < r) { 
                if (x + arr[l] + arr[r] == sum) { 
                    // print elements if it's 
                    // sum is given sum. 
                    Console.WriteLine(x + " " + arr[l] + " " + arr[r]); 
                    l++; 
                    r--; 
                } 

                // If sum of three elements 
                // is less than 'sum' then 
                // increment in left 
                else if (x + arr[l] + arr[r] < sum) 
                    l++; 

                // if sum is greater than 
                // given sum, then decrement 
                // in right side 
                else
                    r--; 
            } 
        } 
    } 

    // Driver code 
    static int Main() 
    { 
        int[] arr = new int[] { 0, -1, 2, -3, 1 }; 
        int sum = -2; 
        int n = arr.Length; 
        findTriplets(arr, n, sum); 
        return 0; 
    } 
} 

// This code is contributed by rahul 

```

## PHP

```php

<?php 
// PHP program to find triplets 
// in a given array whose sum  
// is given sum. 

// function to print triplets  
// with given sum 
function findTriplets($arr, $n, $sum) 
{ 
    // sort array elements 
    sort($arr); 

    for ($i = 0; $i < $n - 1; $i++) 
    { 
        // initialize left and right 
        $l = $i + 1; 
        $r = $n - 1; 
        $x = $arr[$i]; 
        while ($l < $r)  
        { 
            if ($x + $arr[$l] +  
                $arr[$r] == $sum)  
            { 
                // print elements if it's  
                // sum is given sum. 
                echo $x, " ", $arr[$l],  
                         " ", $arr[$r], "\n"; 
                $l++; 
                $r--; 
            } 

            // If sum of three elements 
            // is less than 'sum' then  
            // increment in left 
            else if ($x + $arr[$l] +  
                     $arr[$r] < $sum) 
                $l++; 

            // if sum is greater  
            // than given sum, then 
            // decrement in right side 
            else
                $r--; 
        } 
    } 
} 

// Driver code 
$arr = array(0, -1, 2, -3, 1); 
$sum = -2; 
$n = sizeof($arr); 
findTriplets($arr, $n, $sum); 

// This code is contributed by ajit 
?> 

```

**Output:**

```
-3 -1 2
-3 0 1

```

**复杂度分析**：

*   **时间复杂度**：O（n <sup>2</sup> ）。
    使用嵌套循环（一个用于迭代，另一个用于两指针技术）将时间复杂度提高到 O（n <sup>2</sup> ）。
*   **辅助空间**：O（1）。
    由于不使用其他数据结构。



* * *

* * *



