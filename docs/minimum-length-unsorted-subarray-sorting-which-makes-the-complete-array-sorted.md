# 找到最小长度未排序子数组，进行排序，使整个数组排序

> 原文： [https://www.geeksforgeeks.org/minimum-length-unsorted-subarray-sorting-which-makes-the-complete-array-sorted/](https://www.geeksforgeeks.org/minimum-length-unsorted-subarray-sorting-which-makes-the-complete-array-sorted/)

给定大小为`n`的未排序数组`arr[0..n-1]`，找到最小长度的子数组`arr[s..e]`，以便对该子数组进行排序可使整个数组排序。

**示例**：

1.  如果输入数组为`[10, 12, 20, 30, 25, 40, 32, 31, 35, 50, 60]`，您的程序应该能够找到子数组位于索引 3 和 8 之间。

2.  如果输入数组为`[0, 1, 15, 25, 6, 7, 30, 40, 50]`，则程序应该能够找到子数组位于索引 2 和 5 之间。



**解决方案**：

**（1）找到候选未排序子数组。**

1.  从左向右扫描，找到比下一个元素大的第一个元素。 令`s`为此类元素的索引。 在上面的示例 1 中，`s`为 3（索引为 30）。

2.  从右向左扫描，找到第一个元素（从右到左的顺序为第一个），该元素小于下一个元素（从右到左的顺序为下一个）。 令`e`为该元素的索引。 在上面的示例 1 中，`e`为 7（索引为 31）。

**（2）检查对候选未排序子数组进行排序是否可以对整个数组进行排序。 如果不是，则在子数组中包含更多元素。**

1.  在`arr[s..e]`中找到最小值和最大值。 令最小值和最大值为`min`和`max`。`[30, 25, 40, 32, 31]`的`min`和`max`分别为 25 和 40。

2.  在`arr[0..s-1]`中找到大于`min`的第一个元素（如果有），更改`s`索引此元素。 在上面的示例 1 中没有此类元素。

3.  在`arr[e + 1..n-1]`中找到小于最大值的最后一个元素（如果有），更改`e`索引此元素。 在上面的示例 1 中，`e`更改为 8（索引为 35）

**（3）打印`s`和`e`。** 

**实现**：

## C++ 

```cpp

// C++ program to find the Minimum length Unsorted Subarray,  
// sorting which makes the complete array sorted 
#include<bits/stdc++.h> 
using namespace std; 

void printUnsorted(int arr[], int n) 
{ 
int s = 0, e = n-1, i, max, min;  

// step 1(a) of above algo 
for (s = 0; s < n-1; s++) 
{ 
    if (arr[s] > arr[s+1]) 
    break; 
} 
if (s == n-1) 
{ 
    cout << "The complete array is sorted"; 
    return; 
} 

// step 1(b) of above algo 
for(e = n - 1; e > 0; e--) 
{ 
    if(arr[e] < arr[e-1]) 
    break; 
} 

// step 2(a) of above algo 
max = arr[s]; min = arr[s]; 
for(i = s + 1; i <= e; i++) 
{ 
    if(arr[i] > max) 
    max = arr[i]; 
    if(arr[i] < min) 
    min = arr[i]; 
} 

// step 2(b) of above algo 
for( i = 0; i < s; i++) 
{ 
    if(arr[i] > min) 
    {  
    s = i; 
    break; 
    }      
}  

// step 2(c) of above algo 
for( i = n -1; i >= e+1; i--) 
{ 
    if(arr[i] < max) 
    { 
    e = i; 
    break; 
    }  
}  

// step 3 of above algo 
cout << "The unsorted subarray which" 
     << " makes the given array" << endl 
     << "sorted lies between the indees " 
     << s << " and " << e; 
return; 
} 

int main() 
{ 
    int arr[] = {10, 12, 20, 30, 25, 
                 40, 32, 31, 35, 50, 60}; 
    int arr_size = sizeof(arr)/sizeof(arr[0]); 
    printUnsorted(arr, arr_size); 
    getchar(); 
    return 0; 
} 

// This code is contributed  
// by Akanksha Rai 

```

## C

```
// C program to find the Minimum length Unsorted Subarray,  
// sorting which makes the complete array sorted 
#include<stdio.h> 
   
void printUnsorted(int arr[], int n) 
{ 
  int s = 0, e = n-1, i, max, min;    
   
  // step 1(a) of above algo 
  for (s = 0; s < n-1; s++) 
  { 
    if (arr[s] > arr[s+1]) 
      break; 
  } 
  if (s == n-1) 
  { 
    printf("The complete array is sorted"); 
    return; 
  } 
   
  // step 1(b) of above algo 
  for(e = n - 1; e > 0; e--) 
  { 
    if(arr[e] < arr[e-1]) 
      break; 
  } 
   
  // step 2(a) of above algo 
  max = arr[s]; min = arr[s]; 
  for(i = s + 1; i <= e; i++) 
  { 
    if(arr[i] > max) 
      max = arr[i]; 
    if(arr[i] < min) 
      min = arr[i]; 
  } 
   
  // step 2(b) of above algo 
  for( i = 0; i < s; i++) 
  { 
    if(arr[i] > min) 
    {   
      s = i; 
      break; 
    }       
  }  
   
  // step 2(c) of above algo 
  for( i = n -1; i >= e+1; i--) 
  { 
    if(arr[i] < max) 
    { 
      e = i; 
      break; 
    }  
  }   
       
  // step 3 of above algo 
  printf(" The unsorted subarray which makes the given array "
         " sorted lies between the indees %d and %d", s, e); 
  return; 
} 
   
int main() 
{ 
  int arr[] = {10, 12, 20, 30, 25, 40, 32, 31, 35, 50, 60}; 
  int arr_size = sizeof(arr)/sizeof(arr[0]); 
  printUnsorted(arr, arr_size); 
  getchar(); 
  return 0; 
}
```

## Java

```
// Java program to find the Minimum length Unsorted Subarray,  
// sorting which makes the complete array sorted 
class Main 
{ 
    static void printUnsorted(int arr[], int n) 
    { 
      int s = 0, e = n-1, i, max, min;    
        
      // step 1(a) of above algo 
      for (s = 0; s < n-1; s++) 
      { 
        if (arr[s] > arr[s+1]) 
          break; 
      } 
      if (s == n-1) 
      { 
        System.out.println("The complete array is sorted"); 
        return; 
      } 
        
      // step 1(b) of above algo 
      for(e = n - 1; e > 0; e--) 
      { 
        if(arr[e] < arr[e-1]) 
          break; 
      } 
        
      // step 2(a) of above algo 
      max = arr[s]; min = arr[s]; 
      for(i = s + 1; i <= e; i++) 
      { 
        if(arr[i] > max) 
          max = arr[i]; 
        if(arr[i] < min) 
          min = arr[i]; 
      } 
        
      // step 2(b) of above algo 
      for( i = 0; i < s; i++) 
      { 
        if(arr[i] > min) 
        {   
          s = i; 
          break; 
        }       
      }  
        
      // step 2(c) of above algo 
      for( i = n -1; i >= e+1; i--) 
      { 
        if(arr[i] < max) 
        { 
          e = i; 
          break; 
        }  
      }   
            
      // step 3 of above algo 
      System.out.println(" The unsorted subarray which"+ 
                         " makes the given array sorted lies"+ 
                       "  between the indices "+s+" and "+e); 
      return; 
    } 
        
    public static void main(String args[]) 
    { 
      int arr[] = {10, 12, 20, 30, 25, 40, 32, 31, 35, 50, 60}; 
      int arr_size = arr.length; 
      printUnsorted(arr, arr_size); 
    } 
}
```

## Python3

```
# Python3 program to find the Minimum length Unsorted Subarray,  
# sorting which makes the complete array sorted 
def printUnsorted(arr, n): 
    e = n-1
    # step 1(a) of above algo 
    for s in range(0,n-1): 
        if arr[s] > arr[s+1]: 
            break
          
    if s == n-1: 
        print ("The complete array is sorted") 
        exit() 
  
    # step 1(b) of above algo 
    e= n-1
    while e > 0: 
        if arr[e] < arr[e-1]: 
            break
        e -= 1
  
    # step 2(a) of above algo 
    max = arr[s] 
    min = arr[s] 
    for i in range(s+1,e+1): 
        if arr[i] > max: 
            max = arr[i] 
        if arr[i] < min: 
            min = arr[i] 
              
    # step 2(b) of above algo 
    for i in range(s): 
        if arr[i] > min: 
            s = i 
            break
  
    # step 2(c) of above algo 
    i = n-1
    while i >= e+1: 
        if arr[i] < max: 
            e = i 
            break
        i -= 1
      
    # step 3 of above algo 
    print ("The unsorted subarray which makes the given array") 
    print ("sorted lies between the indexes %d and %d"%( s, e)) 
  
arr = [10, 12, 20, 30, 25, 40, 32, 31, 35, 50, 60] 
arr_size = len(arr) 
printUnsorted(arr, arr_size) 
  
# This code is contributed by Shreyanshi Arun
```

## C#

```
// C# program to find the Minimum length Unsorted Subarray,  
// sorting which makes the complete array sorted 
  
using System; 
  
class GFG 
{ 
    static void printUnsorted(int []arr, int n) 
    { 
    int s = 0, e = n-1, i, max, min;  
          
    // step 1(a) of above algo 
    for (s = 0; s < n-1; s++) 
    { 
        if (arr[s] > arr[s+1]) 
        break; 
    } 
    if (s == n-1) 
    { 
        Console.Write("The complete " + 
                            "array is sorted"); 
        return; 
    } 
          
    // step 1(b) of above algo 
    for(e = n - 1; e > 0; e--) 
    { 
        if(arr[e] < arr[e-1]) 
        break; 
    } 
          
    // step 2(a) of above algo 
    max = arr[s]; min = arr[s]; 
      
    for(i = s + 1; i <= e; i++) 
    { 
        if(arr[i] > max) 
            max = arr[i]; 
          
        if(arr[i] < min) 
            min = arr[i]; 
    } 
          
    // step 2(b) of above algo 
    for( i = 0; i < s; i++) 
    { 
        if(arr[i] > min) 
        {  
            s = i; 
            break; 
        }      
    }  
          
    // step 2(c) of above algo 
    for( i = n -1; i >= e+1; i--) 
    { 
        if(arr[i] < max) 
        { 
            e = i; 
            break; 
        }  
    }  
              
    // step 3 of above algo 
    Console.Write(" The unsorted subarray which"+ 
            " makes the given array sorted lies \n"+ 
              " between the indices "+s+" and "+e); 
    return; 
    } 
          
    public static void Main() 
    { 
        int []arr = {10, 12, 20, 30, 25, 40, 
                                32, 31, 35, 50, 60}; 
        int arr_size = arr.Length; 
          
        printUnsorted(arr, arr_size); 
    } 
} 
  
// This code contributed by Sam007
```

## PHP

```
<?php  
// PHP program to find the Minimum length Unsorted Subarray,  
// sorting which makes the complete array sorted 
function printUnsorted(&$arr, $n) 
{ 
    $s = 0; 
    $e = $n - 1; 
      
    // step 1(a) of above algo 
    for ($s = 0; $s < $n - 1; $s++) 
    { 
        if ($arr[$s] > $arr[$s + 1]) 
        break; 
    } 
    if ($s == $n - 1) 
    { 
        echo "The complete array is sorted"; 
        return; 
    } 
      
    // step 1(b) of above algo 
    for($e = $n - 1; $e > 0; $e--) 
    { 
        if($arr[$e] < $arr[$e - 1]) 
        break; 
    } 
      
    // step 2(a) of above algo 
    $max = $arr[$s];  
    $min = $arr[$s]; 
    for($i = $s + 1; $i <= $e; $i++) 
    { 
        if($arr[$i] > $max) 
            $max = $arr[$i]; 
        if($arr[$i] < $min) 
            $min = $arr[$i]; 
    } 
      
    // step 2(b) of above algo 
    for( $i = 0; $i < $s; $i++) 
    { 
        if($arr[$i] > $min) 
        {  
            $s = $i; 
            break; 
        }      
    }  
      
    // step 2(c) of above algo 
    for( $i = $n - 1; $i >= $e + 1; $i--) 
    { 
        if($arr[$i] < $max) 
        { 
            $e = $i; 
            break; 
        }  
    }  
          
    // step 3 of above algo 
    echo " The unsorted subarray which makes " .  
                     "the given array " . "\n" .  
            " sorted lies between the indees " .  
                              $s . " and " . $e; 
    return; 
} 
  
// Driver code 
$arr = array(10, 12, 20, 30, 25, 40,  
             32, 31, 35, 50, 60); 
$arr_size = sizeof($arr); 
printUnsorted($arr, $arr_size); 
  
// This code is contributed  
// by ChitraNayal 
?>
```

输出：

```
 The unsorted subarray which makes the given array 
sorted lies between the indees 3 and 8
```

时间复杂度：`O(n)`。