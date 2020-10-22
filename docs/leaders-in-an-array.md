# 领导者数组

> 原文： [https://www.geeksforgeeks.org/leaders-in-an-array/](https://www.geeksforgeeks.org/leaders-in-an-array/)

编写程序以打印数组中的所有领导者。 如果一个元素大于其右侧的所有元素，则为领导者。 最右边的元素始终是领导者。 例如，在数组`{16, 17, 4, 4, 3, 5, 2}`中，前导是 17、5 和 2。

令输入数组为`arr[]`，数组的大小为`size`。



**方法 1（简单）**：

使用两个循环。 外循环从 0 到大小 -1，然后从左到右依次选择所有元素。 内部循环将拾取的元素与其右侧的所有元素进行比较。 如果拾取的元素大于其右侧的所有元素，则拾取的元素为前导。

## C++ 

```cpp

#include<iostream> 
using namespace std; 

/*C++ Function to print leaders in an array */
void printLeaders(int arr[], int size) 
{ 
    for (int i = 0; i < size; i++) 
    { 
        int j; 
        for (j = i+1; j < size; j++) 
        { 
            if (arr[i] <= arr[j]) 
                break; 
        }     
        if (j == size) // the loop didn't break 
            cout << arr[i] << " "; 
  } 
} 

/* Driver program to test above function */
int main() 
{ 
    int arr[] = {16, 17, 4, 3, 5, 2}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    printLeaders(arr, n); 
    return 0; 
} 

```

## Java

```java
class LeadersInArray  
{ 
    /*Java Function to print leaders in an array */
    void printLeaders(int arr[], int size)  
    { 
        for (int i = 0; i < size; i++)  
        { 
            int j; 
            for (j = i + 1; j < size; j++)  
            { 
                if (arr[i] < arr[j]) 
                    break; 
            } 
            if (j == size) // the loop didn't break 
                System.out.print(arr[i] + " "); 
        } 
    } 
  
    /* Driver program to test above functions */
    public static void main(String[] args)  
    { 
        LeadersInArray lead = new LeadersInArray(); 
        int arr[] = new int[]{16, 17, 4, 3, 5, 2}; 
        int n = arr.length; 
        lead.printLeaders(arr, n); 
    } 
}
```

## Python

```py
# Python Function to print leaders in array  
  
def printLeaders(arr,size):  
      
    for i in range(0, size):  
        for j in range(i+1, size):  
            if arr[i]<arr[j]:  
                break
        if j == size-1: # If loop didn't break  
            print arr[i],  
  
# Driver function  
arr=[16, 17, 4, 3, 5, 2]  
printLeaders(arr, len(arr))  
  
# This code is contributed by _Devesh Agrawal__
```

## C#

```cs
// C# program to print 
// leaders in array 
using System; 
class GFG  
{ 
    void printLeaders(int []arr,  
                      int size)  
    { 
        for (int i = 0; i < size; i++)  
        { 
            int j; 
            for (j = i + 1; j < size; j++)  
            { 
                if (arr[i] < arr[j]) 
                    break; 
            } 
              
            // the loop didn't break 
            if (j == size)  
                Console.Write(arr[i] + " "); 
        } 
    } 
  
    // Driver Code 
    public static void Main()  
    { 
        GFG lead = new GFG(); 
        int []arr = new int[]{16, 17, 4, 3, 5, 2}; 
        int n = arr.Length; 
        lead.printLeaders(arr, n); 
    } 
} 
  
// This code is contributed by 
// Akanksha Rai(Abby_akku)
```

## PHP

```php
<?php 
// PHP Function to print 
// leaders in an array  
function printLeaders($arr, $size) 
{ 
    for ($i = 0; $i < $size; $i++) 
    { 
        for ($j = $i + 1; 
             $j < $size; $j++) 
        { 
            if ($arr[$i] < $arr[$j]) 
                break; 
        }  
          
        // the loop didn't break 
        if ($j == $size) 
            echo($arr[$i] . " ");  
        } 
} 
  
// Driver Code 
$arr = array(16, 17, 4, 3, 5, 2); 
$n = sizeof($arr); 
printLeaders($arr, $n); 
      
// This code is contributed  
// by Shivi_Aggarwal 
?>
```

方法 2（从右扫描）：

从右到左扫描数组中的所有元素，并一直跟踪到现在为止的最大值。 当最大值更改其值时，将其打印。

下图是上述方法的模拟：

![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20190620130246/Leaders-in-an-array.png)

下面是上述方法的实现：

## C++

```cpp
#include <iostream> 
using namespace std; 
  
/* C++ Function to print leaders in an array */
void printLeaders(int arr[], int size) 
{ 
    int max_from_right =  arr[size-1]; 
  
    /* Rightmost element is always leader */
    cout << max_from_right << " "; 
      
    for (int i = size-2; i >= 0; i--) 
    { 
        if (max_from_right <= arr[i])  
        {            
            max_from_right = arr[i]; 
            cout << max_from_right << " "; 
        } 
    }     
} 
  
/* Driver program to test above function*/
int main() 
{ 
    int arr[] = {16, 17, 4, 3, 5, 2}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    printLeaders(arr, n); 
    return 0; 
}
```

## Java

```java
class LeadersInArray  
{ 
    /* Java Function to print leaders in an array */
    void printLeaders(int arr[], int size) 
    { 
        int max_from_right =  arr[size-1]; 
   
        /* Rightmost element is always leader */
        System.out.print(max_from_right + " "); 
       
        for (int i = size-2; i >= 0; i--) 
        { 
            if (max_from_right <= arr[i]) 
            {            
            max_from_right = arr[i]; 
            System.out.print(max_from_right + " "); 
            } 
        }     
    } 
  
    /* Driver program to test above functions */
    public static void main(String[] args)  
    { 
        LeadersInArray lead = new LeadersInArray(); 
        int arr[] = new int[]{16, 17, 4, 3, 5, 2}; 
        int n = arr.length; 
        lead.printLeaders(arr, n); 
    } 
}
```

## Python

```py
# Python function to print leaders in array 
def printLeaders(arr, size): 
     
    max_from_right = arr[size-1]    
    print max_from_right,     
    for i in range( size-2, -1, -1):         
        if max_from_right <= arr[i]:         
            print arr[i], 
            max_from_right = arr[i] 
          
# Driver function 
arr = [16, 17, 4, 3, 5, 2] 
printLeaders(arr, len(arr)) 
  
# This code contributed by _Devesh Agrawal__
```

## C#

```cs
// C# program to find Leaders in an array 
using System; 
  
class LeadersInArray { 
      
    // C# Function to print leaders 
    // in an array  
    void printLeaders(int []arr, int size) 
    { 
        int max_from_right = arr[size - 1]; 
  
        // Rightmost element is always leader 
        Console.Write(max_from_right +" "); 
      
        for (int i = size - 2; i >= 0; i--) 
        { 
            if (max_from_right <= arr[i])     
            {      
                max_from_right = arr[i]; 
                Console.Write(max_from_right +" "); 
            } 
        }  
    } 
  
    // Driver Code 
    public static void Main(String[] args)  
    { 
        LeadersInArray lead = new LeadersInArray(); 
        int []arr = new int[]{16, 17, 4, 3, 5, 2}; 
        int n = arr.Length; 
        lead.printLeaders(arr, n); 
    } 
} 
  
// This code is contributed  
// by Akanksha Rai(Abby_akku)
```

## PHP

```php
<?php 
// PHP Function to print 
// leaders in an array  
function printLeaders(&$arr, $size) 
{ 
    $max_from_right = $arr[$size - 1]; 
  
    // Rightmost element  
    // is always leader  
    echo($max_from_right); 
    echo(" "); 
      
    for ($i = $size - 2;  
         $i >= 0; $i--) 
    { 
        if ($max_from_right <= $arr[$i])     
        {          
            $max_from_right = $arr[$i]; 
            echo($max_from_right); 
            echo(" "); 
        } 
    }  
} 
  
// Driver Code 
$arr = array(16, 17, 4, 3, 5, 2); 
$n = sizeof($arr); 
printLeaders($arr, $n); 
  
// This code is contributed  
// by Shivi_Aggarwal 
?>
```

输出：

```
2 5 17
```

时间复杂度：`O(n)`。