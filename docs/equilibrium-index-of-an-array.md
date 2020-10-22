# 数组的平衡指数

> 原文： [https://www.geeksforgeeks.org/equilibrium-index-of-an-array/](https://www.geeksforgeeks.org/equilibrium-index-of-an-array/)

数组的平衡索引是一个索引，以使较低索引处的元素之和等于较高索引处的元素之和。 例如，在数组`A`中：

**示例**：

> 输入：`A[] = {-7, 1, 5, 2, -4, 3, 0}`
> 
> 输出：3
> 
> 3 是平衡指数， 因为：
> 
> `A[0] + A[1] + A[2] = A[4] + A[5] + A[6]`
> 
> 输入：`A[] = {1, 2, 3}`
> 
> 输出：-1

写一个函数`int balance(int[] arr, int n)`；给定大小为`n`的序列`arr[]`的结果，返回平衡指数（如果有的话）；如果不存在平衡指数，则返回 -1。



**方法 1（简单但效率低下）**：

使用两个循环。 外循环遍历所有元素，内循环查找外循环选取的当前索引是否为平衡索引。 该解决方案的时间复杂度为`O(n ^ 2)`。

## C++ 

```cpp

// C++ program to find equilibrium 
// index of an array 
#include <bits/stdc++.h> 
using namespace std; 

int equilibrium(int arr[], int n) 
{ 
    int i, j; 
    int leftsum, rightsum; 

    /* Check for indexes one by one until  
    an equilibrium index is found */
    for (i = 0; i < n; ++i)  
    {      

        /* get left sum */
        leftsum = 0;  
        for (j = 0; j < i; j++) 
            leftsum += arr[j]; 

        /* get right sum */
        rightsum = 0;  
        for (j = i + 1; j < n; j++) 
            rightsum += arr[j]; 

        /* if leftsum and rightsum   
        are same, then we are done */
        if (leftsum == rightsum) 
            return i; 
    } 

    /* return -1 if no equilibrium  
    index is found */
    return -1; 
} 

// Driver code 
int main() 
{ 
    int arr[] = { -7, 1, 5, 2, -4, 3, 0 }; 
    int arr_size = sizeof(arr) / sizeof(arr[0]); 
    cout << equilibrium(arr, arr_size); 
    return 0; 
} 

// This code is contributed  
// by Akanksha Rai(Abby_akku) 

```

## C

```c
// C program to find equilibrium 
// index of an array 
  
#include <stdio.h> 
  
int equilibrium(int arr[], int n) 
{ 
    int i, j; 
    int leftsum, rightsum; 
  
    /* Check for indexes one by one until  
      an equilibrium index is found */
    for (i = 0; i < n; ++i) {        
  
        /* get left sum */
        leftsum = 0;  
        for (j = 0; j < i; j++) 
            leftsum += arr[j]; 
  
        /* get right sum */
        rightsum = 0;  
        for (j = i + 1; j < n; j++) 
            rightsum += arr[j]; 
  
        /* if leftsum and rightsum are same,  
           then we are done */
        if (leftsum == rightsum) 
            return i; 
    } 
  
    /* return -1 if no equilibrium index is found */
    return -1; 
} 
  
// Driver code 
int main() 
{ 
    int arr[] = { -7, 1, 5, 2, -4, 3, 0 }; 
    int arr_size = sizeof(arr) / sizeof(arr[0]); 
    printf("%d", equilibrium(arr, arr_size)); 
  
    getchar(); 
    return 0; 
}
```

## Java

```java
// Java program to find equilibrium 
// index of an array 
  
class EquilibriumIndex { 
    int equilibrium(int arr[], int n) 
    { 
        int i, j; 
        int leftsum, rightsum; 
  
        /* Check for indexes one by one until  
           an equilibrium index is found */
        for (i = 0; i < n; ++i) { 
  
            /* get left sum */
            leftsum = 0;   
            for (j = 0; j < i; j++) 
                leftsum += arr[j]; 
  
            /* get right sum */
            rightsum = 0; 
            for (j = i + 1; j < n; j++) 
                rightsum += arr[j]; 
  
            /* if leftsum and rightsum are same,  
               then we are done */
            if (leftsum == rightsum) 
                return i; 
        } 
  
        /* return -1 if no equilibrium index is found */
        return -1; 
    } 
    // Driver code 
    public static void main(String[] args) 
    { 
        EquilibriumIndex equi = new EquilibriumIndex(); 
        int arr[] = { -7, 1, 5, 2, -4, 3, 0 }; 
        int arr_size = arr.length; 
        System.out.println(equi.equilibrium(arr, arr_size)); 
    } 
} 
  
// This code has been contributed by Mayank Jaiswal
```

## Python3

```py
# Python program to find equilibrium  
# index of an array 
  
# function to find the equilibrium index 
def equilibrium(arr): 
    leftsum = 0
    rightsum = 0
    n = len(arr) 
  
    # Check for indexes one by one  
    # until an equilibrium index is found 
    for i in range(n): 
        leftsum = 0
        rightsum = 0
      
        # get left sum 
        for j in range(i): 
            leftsum += arr[j] 
          
        # get right sum 
        for j in range(i + 1, n): 
            rightsum += arr[j] 
          
        # if leftsum and rightsum are same, 
        # then we are done 
        if leftsum == rightsum: 
            return i 
      
    # return -1 if no equilibrium index is found 
    return -1
              
# driver code 
arr = [-7, 1, 5, 2, -4, 3, 0] 
print (equilibrium(arr)) 
  
# This code is contributed by Abhishek Sharama
```

## C#

```cs
// C# program to find equilibrium 
// index of an array 
  
using System; 
  
class GFG { 
    static int equilibrium(int[] arr, int n) 
    { 
        int i, j; 
        int leftsum, rightsum; 
  
        /* Check for indexes one by  
         one until an equilibrium 
        index is found */
        for (i = 0; i < n; ++i) { 
  
            // initialize left sum 
            // for current index i 
            leftsum = 0; 
  
            // initialize right sum 
            // for current index i 
            rightsum = 0; 
  
            /* get left sum */
            for (j = 0; j < i; j++) 
                leftsum += arr[j]; 
  
            /* get right sum */
            for (j = i + 1; j < n; j++) 
                rightsum += arr[j]; 
  
            /* if leftsum and rightsum are 
             same, then we are done */
            if (leftsum == rightsum) 
                return i; 
        } 
  
        /* return -1 if no equilibrium  
         index is found */
        return -1; 
    } 
  
    // driver code 
    public static void Main() 
    { 
        int[] arr = { -7, 1, 5, 2, -4, 3, 0 }; 
        int arr_size = arr.Length; 
  
        Console.Write(equilibrium(arr, arr_size)); 
    } 
} 
  
// This code is contributed by Sam007
```

## PHP

```php
<?php  
// PHP program to find equilibrium  
// index of an array  
  
function equilibrium($arr, $n)  
{  
    $i; $j;  
    $leftsum; 
    $rightsum;  
  
    /* Check for indexes one by one until  
    an equilibrium index is found */
    for ($i = 0; $i < $n; ++$i)  
    {      
  
        /* get left sum */
        $leftsum = 0;  
        for ($j = 0; $j < $i; $j++)  
            $leftsum += $arr[$j];  
  
        /* get right sum */
        $rightsum = 0;  
        for ($j = $i + 1; $j < $n; $j++)  
            $rightsum += $arr[$j];  
  
        /* if leftsum and rightsum  
        are same, then we are done */
        if ($leftsum == $rightsum)  
            return $i;  
    }  
  
    /* return -1 if no equilibrium 
       index is found */
    return -1;  
}  
  
// Driver code  
$arr = array( -7, 1, 5, 2, -4, 3, 0 );  
$arr_size = sizeof($arr);  
echo equilibrium($arr, $arr_size);  
  
// This code is contributed  
// by akt_mit 
?>
```

时间复杂度：`O（n ^ 2）`。

方法 2（棘手而又高效）：

这个想法是首先获得数组的总和。 然后遍历数组，并继续更新初始化为零的剩余和。 在循环中，我们可以通过将元素一一减去来获得正确的总和。 感谢 Sambasiva 建议该解决方案并为此提供代码。

```
1) Initialize leftsum  as 0
2) Get the total sum of the array as sum
3) Iterate through the array and for each index i, do following.
    a)  Update sum to get the right sum.  
           sum = sum - arr[i] 
       // sum is now right sum
    b) If leftsum is equal to sum, then return current index. 
       // update leftsum for next iteration.
    c) leftsum = leftsum + arr[i]
4) return -1 
// If we come out of loop without returning then
// there is no equilibrium index
```

下图显示了上述方法的模拟运行：

![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20190620123235/Equilibrium-index-of-an-array1.png)

下面是上述方法的实现：

## C++

```cpp
// C++ program to find equilibrium  
// index of an array  
#include <bits/stdc++.h> 
using namespace std; 
  
int equilibrium(int arr[], int n)  
{  
    int sum = 0; // initialize sum of whole array  
    int leftsum = 0; // initialize leftsum  
  
    /* Find sum of the whole array */
    for (int i = 0; i < n; ++i)  
        sum += arr[i];  
  
    for (int i = 0; i < n; ++i)  
    {  
        sum -= arr[i]; // sum is now right sum for index i  
  
        if (leftsum == sum)  
            return i;  
  
        leftsum += arr[i];  
    }  
  
    /* If no equilibrium index found, then return 0 */
    return -1;  
}  
  
// Driver code  
int main()  
{  
    int arr[] = { -7, 1, 5, 2, -4, 3, 0 };  
    int arr_size = sizeof(arr) / sizeof(arr[0]);  
    cout << "First equilibrium index is " << equilibrium(arr, arr_size);  
    return 0;  
}  
  
// This is code is contributed by rathbhupendra
```

## C

```c
// C program to find equilibrium 
// index of an array 
  
#include <stdio.h> 
  
int equilibrium(int arr[], int n) 
{ 
    int sum = 0; // initialize sum of whole array 
    int leftsum = 0; // initialize leftsum 
  
    /* Find sum of the whole array */
    for (int i = 0; i < n; ++i) 
        sum += arr[i]; 
  
    for (int i = 0; i < n; ++i) { 
        sum -= arr[i]; // sum is now right sum for index i 
  
        if (leftsum == sum) 
            return i; 
  
        leftsum += arr[i]; 
    } 
  
    /* If no equilibrium index found, then return 0 */
    return -1; 
} 
  
// Driver code 
int main() 
{ 
    int arr[] = { -7, 1, 5, 2, -4, 3, 0 }; 
    int arr_size = sizeof(arr) / sizeof(arr[0]); 
    printf("First equilibrium index is %d",  
                 equilibrium(arr, arr_size)); 
  
    getchar(); 
    return 0; 
}
```

## Java

```java
// Java program to find equilibrium 
// index of an array 
  
class EquilibriumIndex { 
    int equilibrium(int arr[], int n) 
    { 
        int sum = 0; // initialize sum of whole array 
        int leftsum = 0; // initialize leftsum 
  
        /* Find sum of the whole array */
        for (int i = 0; i < n; ++i) 
            sum += arr[i]; 
  
        for (int i = 0; i < n; ++i) { 
            sum -= arr[i]; // sum is now right sum for index i 
  
            if (leftsum == sum) 
                return i; 
  
            leftsum += arr[i]; 
        } 
  
        /* If no equilibrium index found, then return 0 */
        return -1; 
    } 
  
   // Driver code 
    public static void main(String[] args) 
    { 
        EquilibriumIndex equi = new EquilibriumIndex(); 
        int arr[] = { -7, 1, 5, 2, -4, 3, 0 }; 
        int arr_size = arr.length; 
        System.out.println("First equilibrium index is " +  
                          equi.equilibrium(arr, arr_size)); 
    } 
} 
  
// This code has been contributed by Mayank Jaiswal
```

## Python3

```py
# Python program to find the equilibrium 
# index of an array 
  
# function to find the equilibrium index 
def equilibrium(arr): 
  
    # finding the sum of whole array 
    total_sum = sum(arr) 
    leftsum = 0
    for i, num in enumerate(arr): 
          
        # total_sum is now right sum 
        # for index i 
        total_sum -= num 
          
        if leftsum == total_sum: 
            return i 
        leftsum += num 
       
      # If no equilibrium index found,  
      # then return -1 
    return -1
      
# Driver code 
arr = [-7, 1, 5, 2, -4, 3, 0] 
print ('First equilibrium index is ', 
       equilibrium(arr)) 
  
# This code is contributed by Abhishek Sharma
```

## C#

```cs
// C# program to find the equilibrium 
//  index of an array 
  
using System; 
  
class GFG { 
    static int equilibrium(int[] arr, int n) 
    { 
        // initialize sum of whole array 
        int sum = 0; 
  
        // initialize leftsum 
        int leftsum = 0; 
  
        /* Find sum of the whole array */
        for (int i = 0; i < n; ++i) 
            sum += arr[i]; 
  
        for (int i = 0; i < n; ++i) { 
  
            // sum is now right sum 
            // for index i 
            sum -= arr[i]; 
  
            if (leftsum == sum) 
                return i; 
  
            leftsum += arr[i]; 
        } 
  
        /* If no equilibrium index found,  
        then return 0 */
        return -1; 
    } 
  
    // Driver code 
    public static void Main() 
    { 
        int[] arr = { -7, 1, 5, 2, -4, 3, 0 }; 
        int arr_size = arr.Length; 
  
        Console.Write("First equilibrium index is " + 
                           equilibrium(arr, arr_size)); 
    } 
} 
// This code is contributed by Sam007
```

## PHP

```php
<?php 
// PHP program to find equilibrium  
// index of an array  
  
function equilibrium($arr, $n)  
{  
    $sum = 0; // initialize sum of  
              // whole array  
    $leftsum = 0; // initialize leftsum  
  
    /* Find sum of the whole array */
    for ($i = 0; $i < $n; ++$i)  
        $sum += $arr[$i];  
  
    for ($i = 0; $i < $n; ++$i)  
    {  
        // sum is now right sum  
        // for index i  
        $sum -= $arr[$i];  
  
        if ($leftsum == $sum)  
            return $i;  
  
        $leftsum += $arr[$i];  
    }  
  
    /* If no equilibrium index  
    found, then return 0 */
    return -1;  
}  
  
// Driver code 
$arr = array( -7, 1, 5, 2, -4, 3, 0 );  
$arr_size = sizeof($arr);  
echo "First equilibrium index is ",  
      equilibrium($arr, $arr_size);  
  
// This code is contributed by ajit 
?>
```

输出：

```
First equilibrium index is 3
```

时间复杂度：`O(n)`。

正如 Sameer 指出的那样，我们可以删除`return`语句并添加一条`print`语句以打印所有均衡指数，而不是仅返回一个。