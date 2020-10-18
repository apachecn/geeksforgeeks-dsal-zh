# 使用最少数量的比较的数组的最大值和最小值

> 原文： [https://www.geeksforgeeks.org/maximum-and-minimum-in-an-array/](https://www.geeksforgeeks.org/maximum-and-minimum-in-an-array/)

**编写 C 函数以返回数组中的最小值和最大值。 您的程序应进行最少的比较。**



首先，我们如何从 C 函数返回多个值？ 我们可以使用结构或指针来做到这一点。

我们创建了一个名为`pair`（包含最小和最大）的结构以返回多个值。

```

struct pair  
{ 
  int min; 
  int max; 
};   

```

并且函数声明变为：`struct pair getMinMax(int arr[], int n)`其中`arr[]`是大小为`n`的数组，需要最小和最大值。

**方法 1（简单线性搜索）**：

分别将`min`和`max`值初始化为前两个元素的最小值和最大值。 从 3 开始，将每个元素与`max`和`min`进行比较，并相应地更改`max`和`min`（即，如果元素小于`min`则更改`min`，否则，如果元素大于`max`则更改`max`，否则忽略该元素）

## C++

```cpp
er_none
edit
play_arrow

brightness_4
// C++ program of above implementation  
#include<iostream> 
using namespace std; 
  
// Pair struct is used to return  
// two values from getMinMax() 
struct Pair  
{ 
    int min; 
    int max; 
};  
  
struct Pair getMinMax(int arr[], int n) 
{ 
    struct Pair minmax;      
    int i; 
      
    // If there is only one element  
    // then return it as min and max both 
    if (n == 1) 
    { 
        minmax.max = arr[0]; 
        minmax.min = arr[0];      
        return minmax; 
    }  
      
    // If there are more than one elements, 
    // then initialize min and max 
    if (arr[0] > arr[1])  
    { 
        minmax.max = arr[0]; 
        minmax.min = arr[1]; 
    }  
    else
    { 
        minmax.max = arr[1]; 
        minmax.min = arr[0]; 
    }  
      
    for(i = 2; i < n; i++) 
    { 
        if (arr[i] > minmax.max)      
            minmax.max = arr[i]; 
              
        else if (arr[i] < minmax.min)      
            minmax.min = arr[i]; 
    } 
    return minmax; 
} 
  
// Driver code 
int main() 
{ 
    int arr[] = { 1000, 11, 445,  
                  1, 330, 3000 }; 
    int arr_size = 6; 
      
    struct Pair minmax = getMinMax(arr, arr_size); 
      
    cout << "Minimum element is " 
         << minmax.min << endl; 
    cout << "Maximum element is " 
         << minmax.max; 
           
    return 0; 
}  
  
// This code is contributed by nik_3112 
```

## C

```c

/* structure is used to return two values from minMax() */
#include<stdio.h> 
struct pair  
{ 
  int min; 
  int max; 
};   

struct pair getMinMax(int arr[], int n) 
{ 
  struct pair minmax;      
  int i; 

  /*If there is only one element then return it as min and max both*/
  if (n == 1) 
  { 
     minmax.max = arr[0]; 
     minmax.min = arr[0];      
     return minmax; 
  }     

  /* If there are more than one elements, then initialize min  
      and max*/
  if (arr[0] > arr[1])   
  { 
      minmax.max = arr[0]; 
      minmax.min = arr[1]; 
  }   
  else
  { 
      minmax.max = arr[1]; 
      minmax.min = arr[0]; 
  }     

  for (i = 2; i<n; i++) 
  { 
    if (arr[i] >  minmax.max)       
      minmax.max = arr[i]; 

    else if (arr[i] <  minmax.min)       
      minmax.min = arr[i]; 
  } 

  return minmax; 
} 

/* Driver program to test above function */
int main() 
{ 
  int arr[] = {1000, 11, 445, 1, 330, 3000}; 
  int arr_size = 6; 
  struct pair minmax = getMinMax (arr, arr_size); 
  printf("nMinimum element is %d", minmax.min); 
  printf("nMaximum element is %d", minmax.max); 
  getchar(); 
}   

```

## Java

```java
// Java program of above implementation 
public class GFG { 
/* Class Pair is used to return two values from getMinMax() */
    static class Pair { 
  
        int min; 
        int max; 
    } 
  
    static Pair getMinMax(int arr[], int n) { 
        Pair minmax = new  Pair(); 
        int i; 
  
        /*If there is only one element then return it as min and max both*/
        if (n == 1) { 
            minmax.max = arr[0]; 
            minmax.min = arr[0]; 
            return minmax; 
        } 
  
        /* If there are more than one elements, then initialize min  
    and max*/
        if (arr[0] > arr[1]) { 
            minmax.max = arr[0]; 
            minmax.min = arr[1]; 
        } else { 
            minmax.max = arr[1]; 
            minmax.min = arr[0]; 
        } 
  
        for (i = 2; i < n; i++) { 
            if (arr[i] > minmax.max) { 
                minmax.max = arr[i]; 
            } else if (arr[i] < minmax.min) { 
                minmax.min = arr[i]; 
            } 
        } 
  
        return minmax; 
    } 
  
    /* Driver program to test above function */
    public static void main(String args[]) { 
        int arr[] = {1000, 11, 445, 1, 330, 3000}; 
        int arr_size = 6; 
        Pair minmax = getMinMax(arr, arr_size); 
        System.out.printf("\nMinimum element is %d", minmax.min); 
        System.out.printf("\nMaximum element is %d", minmax.max); 
  
    } 
  
} 
```

## Python3

```py
# Python program of above implementation 
  
# structure is used to return two values from minMax() 
  
class pair: 
    def __init__(self): 
        self.min = 0
        self.max = 0
  
def getMinMax(arr: list, n: int) -> pair: 
    minmax = pair() 
  
    # If there is only one element then return it as min and max both 
    if n == 1: 
        minmax.max = arr[0] 
        minmax.min = arr[0] 
        return minmax 
  
    # If there are more than one elements, then initialize min 
    # and max 
    if arr[0] > arr[1]: 
        minmax.max = arr[0] 
        minmax.min = arr[1] 
    else: 
        minmax.max = arr[1] 
        minmax.min = arr[0] 
  
    for i in range(2, n): 
        if arr[i] > minmax.max: 
            minmax.max = arr[i] 
        elif arr[i] < minmax.min: 
            minmax.min = arr[i] 
  
    return minmax 
  
# Driver Code 
if __name__ == "__main__": 
    arr = [1000, 11, 445, 1, 330, 3000] 
    arr_size = 6
    minmax = getMinMax(arr, arr_size) 
    print("Minimum element is", minmax.min) 
    print("Maximum element is", minmax.max) 
  
# This code is contributed by 
# sanjeev2552 
```

## C#

```cs
// C# program of above implementation 
using System; 
  
class GFG  
{ 
    /* Class Pair is used to return  
    two values from getMinMax() */
    class Pair  
    { 
        public int min; 
        public int max; 
    } 
  
    static Pair getMinMax(int []arr, int n) 
    { 
        Pair minmax = new Pair(); 
        int i; 
  
        /* If there is only one element  
        then return it as min and max both*/
        if (n == 1) 
        { 
            minmax.max = arr[0]; 
            minmax.min = arr[0]; 
            return minmax; 
        } 
  
        /* If there are more than one elements, 
        then initialize min and max*/
        if (arr[0] > arr[1]) 
        { 
            minmax.max = arr[0]; 
            minmax.min = arr[1]; 
        }  
        else
        { 
            minmax.max = arr[1]; 
            minmax.min = arr[0]; 
        } 
  
        for (i = 2; i < n; i++) 
        { 
            if (arr[i] > minmax.max)  
            { 
                minmax.max = arr[i]; 
            }  
            else if (arr[i] < minmax.min) 
            { 
                minmax.min = arr[i]; 
            } 
        } 
        return minmax; 
    } 
  
    // Driver Code 
    public static void Main(String []args)  
    { 
        int []arr = {1000, 11, 445, 1, 330, 3000}; 
        int arr_size = 6; 
        Pair minmax = getMinMax(arr, arr_size); 
        Console.Write("Minimum element is {0}", 
                                   minmax.min); 
        Console.Write("\nMaximum element is {0}",  
                                     minmax.max); 
    } 
} 
  
// This code is contributed by PrinciRaj1992 
```

输出：

```
Minimum element is 1
Maximum element is 3000
```

时间复杂度：`O(n)`。

在这种方法中，最坏情况下的比较总数为`1 + 2(n-2)`，最好情况下为`1 + n – 2`。

在上述实现中，当元素以降序排序时，最坏的情况发生，而当元素以升序排序时，最好的情况发生。

方法 2（比赛方法）：

将数组分为两部分，比较两部分的最大值和最小值，以获得整个数组的最大值和最小值。

```
Pair MaxMin(array, array_size)
   if array_size = 1
      return element as both max and min
   else if arry_size = 2
      one comparison to determine max and min
      return that pair
   else    /* array_size  > 2 */
      recur for max and min of left half
      recur for max and min of right half
      one comparison determines true max of the two candidates
      one comparison determines true min of the two candidates
      return the pair of max and min
```

实现：

## C++

```cpp
// C++ program of above implementation  
#include<iostream> 
using namespace std; 
  
// structure is used to return  
// two values from minMax()  
struct Pair  
{ 
    int min; 
    int max; 
};  
  
struct Pair getMinMax(int arr[], int low, 
                                 int high) 
{ 
    struct Pair minmax, mml, mmr;      
    int mid; 
      
    // If there is only on element  
    if (low == high) 
    { 
        minmax.max = arr[low]; 
        minmax.min = arr[low];      
        return minmax; 
    }  
      
    // If there are two elements  
    if (high == low + 1) 
    {  
        if (arr[low] > arr[high])  
        { 
            minmax.max = arr[low]; 
            minmax.min = arr[high]; 
        }  
        else
        { 
            minmax.max = arr[high]; 
            minmax.min = arr[low]; 
        }  
        return minmax; 
    } 
      
    // If there are more than 2 elements  
    mid = (low + high) / 2;  
    mml = getMinMax(arr, low, mid); 
    mmr = getMinMax(arr, mid + 1, high);  
      
    // Compare minimums of two parts 
    if (mml.min < mmr.min) 
        minmax.min = mml.min; 
    else
        minmax.min = mmr.min;      
      
    // Compare maximums of two parts 
    if (mml.max > mmr.max) 
        minmax.max = mml.max; 
    else
        minmax.max = mmr.max;      
      
    return minmax; 
} 
  
// Driver code 
int main() 
{ 
    int arr[] = { 1000, 11, 445, 
                  1, 330, 3000 }; 
    int arr_size = 6; 
      
    struct Pair minmax = getMinMax(arr, 0,  
                             arr_size - 1); 
                               
    cout << "Minimum element is " 
         << minmax.min << endl; 
    cout << "Maximum element is " 
         << minmax.max; 
           
    return 0; 
} 
  
// This code is contributed by nik_3112 
```

## C

```c
/* structure is used to return two values from minMax() */
#include<stdio.h> 
struct pair  
{ 
  int min; 
  int max; 
};   
  
struct pair getMinMax(int arr[], int low, int high) 
{ 
  struct pair minmax, mml, mmr;        
  int mid; 
    
  /* If there is only on element */
  if (low == high) 
  { 
     minmax.max = arr[low]; 
     minmax.min = arr[low];      
     return minmax; 
  }     
    
  /* If there are two elements */
  if (high == low + 1) 
  {   
     if (arr[low] > arr[high])   
     { 
        minmax.max = arr[low]; 
        minmax.min = arr[high]; 
     }   
     else
     { 
        minmax.max = arr[high]; 
        minmax.min = arr[low]; 
     }   
     return minmax; 
  } 
    
  /* If there are more than 2 elements */
  mid = (low + high)/2;   
  mml = getMinMax(arr, low, mid); 
  mmr = getMinMax(arr, mid+1, high);   
    
  /* compare minimums of two parts*/
  if (mml.min < mmr.min) 
    minmax.min = mml.min; 
  else
    minmax.min = mmr.min;      
  
  /* compare maximums of two parts*/
  if (mml.max > mmr.max) 
    minmax.max = mml.max; 
  else
    minmax.max = mmr.max;      
   
  return minmax; 
} 
  
/* Driver program to test above function */
int main() 
{ 
  int arr[] = {1000, 11, 445, 1, 330, 3000}; 
  int arr_size = 6; 
  struct pair minmax = getMinMax(arr, 0, arr_size-1); 
  printf("nMinimum element is %d", minmax.min); 
  printf("nMaximum element is %d", minmax.max); 
  getchar(); 
} 
```

## Java

```java
// Java program of above implementation 
public class GFG { 
/* Class Pair is used to return two values from getMinMax() */
    static class Pair { 
  
        int min; 
        int max; 
    } 
  
    static Pair getMinMax(int arr[], int low, int high) { 
        Pair minmax = new Pair(); 
        Pair mml = new Pair(); 
        Pair mmr = new Pair(); 
        int mid; 
  
        /* If there is only on element */
        if (low == high) { 
            minmax.max = arr[low]; 
            minmax.min = arr[low]; 
            return minmax; 
        } 
  
        /* If there are two elements */
        if (high == low + 1) { 
            if (arr[low] > arr[high]) { 
                minmax.max = arr[low]; 
                minmax.min = arr[high]; 
            } else { 
                minmax.max = arr[high]; 
                minmax.min = arr[low]; 
            } 
            return minmax; 
        } 
  
        /* If there are more than 2 elements */
        mid = (low + high) / 2; 
        mml = getMinMax(arr, low, mid); 
        mmr = getMinMax(arr, mid + 1, high); 
  
        /* compare minimums of two parts*/
        if (mml.min < mmr.min) { 
            minmax.min = mml.min; 
        } else { 
            minmax.min = mmr.min; 
        } 
  
        /* compare maximums of two parts*/
        if (mml.max > mmr.max) { 
            minmax.max = mml.max; 
        } else { 
            minmax.max = mmr.max; 
        } 
  
        return minmax; 
    } 
  
    /* Driver program to test above function */
    public static void main(String args[]) { 
        int arr[] = {1000, 11, 445, 1, 330, 3000}; 
        int arr_size = 6; 
        Pair minmax = getMinMax(arr, 0, arr_size - 1); 
        System.out.printf("\nMinimum element is %d", minmax.min); 
        System.out.printf("\nMaximum element is %d", minmax.max); 
  
    } 
} 
```

## Python3

```py
# Python program of above implementation 
def getMinMax(low, high, arr): 
    arr_max = arr[low] 
    arr_min = arr[low] 
      
    # If there is only one element  
    if low == high: 
        arr_max = arr[low] 
        arr_min = arr[low] 
        return (arr_max, arr_min) 
          
    # If there is only two element 
    elif high == low + 1: 
        if arr[low] > arr[high]: 
            arr_max = arr[low] 
            arr_min = arr[high] 
        else: 
            arr_max = arr[high] 
            arr_min = arr[low] 
        return (arr_max, arr_min) 
    else: 
          
        # If there are more than 2 elements 
        mid = int((low + high) / 2) 
        arr_max1, arr_min1 = getMinMax(low, mid, arr) 
        arr_max2, arr_min2 = getMinMax(mid + 1, high, arr) 
  
    return (max(arr_max1, arr_max2), min(arr_min1, arr_min2)) 
  
# Driver code 
arr = [1000, 11, 445, 1, 330, 3000] 
high = len(arr) - 1
low = 0
arr_max, arr_min = getMinMax(low, high, arr) 
print('Minimum element is ', arr_min) 
print('nMaximum element is ', arr_max) 
  
# This code is contributed by DeepakChhitarka 
```

## C#

```cs
// C# implementation of the approach 
using System; 
                      
public class GFG { 
/* Class Pair is used to return two values from getMinMax() */
    public class Pair { 
   
        public int min; 
        public int max; 
    } 
   
    static Pair getMinMax(int []arr, int low, int high) { 
        Pair minmax = new Pair(); 
        Pair mml = new Pair(); 
        Pair mmr = new Pair(); 
        int mid; 
   
        /* If there is only on element */
        if (low == high) { 
            minmax.max = arr[low]; 
            minmax.min = arr[low]; 
            return minmax; 
        } 
   
        /* If there are two elements */
        if (high == low + 1) { 
            if (arr[low] > arr[high]) { 
                minmax.max = arr[low]; 
                minmax.min = arr[high]; 
            } else { 
                minmax.max = arr[high]; 
                minmax.min = arr[low]; 
            } 
            return minmax; 
        } 
   
        /* If there are more than 2 elements */
        mid = (low + high) / 2; 
        mml = getMinMax(arr, low, mid); 
        mmr = getMinMax(arr, mid + 1, high); 
   
        /* compare minimums of two parts*/
        if (mml.min < mmr.min) { 
            minmax.min = mml.min; 
        } else { 
            minmax.min = mmr.min; 
        } 
   
        /* compare maximums of two parts*/
        if (mml.max > mmr.max) { 
            minmax.max = mml.max; 
        } else { 
            minmax.max = mmr.max; 
        } 
   
        return minmax; 
    } 
   
    /* Driver program to test above function */
    public static void Main(String []args) { 
        int []arr = {1000, 11, 445, 1, 330, 3000}; 
        int arr_size = 6; 
        Pair minmax = getMinMax(arr, 0, arr_size - 1); 
        Console.Write("\nMinimum element is {0}", minmax.min); 
        Console.Write("\nMaximum element is {0}", minmax.max); 
   
    } 
} 
  
// This code contributed by Rajput-Ji 
```

输出：

```
Minimum element is 1
Maximum element is 3000
```

时间复杂度：`O(n)`。

比较总数：让比较数为`T(n)`。 `T(n)`可以写为：

算法范式：分而治之。

```
  T(n) = T(floor(n/2)) + T(ceil(n/2)) + 2  
  T(2) = 1
  T(1) = 0
```

如果`n`是 2 的幂，那么我们可以将`T(n)`写成：

```
   T(n) = 2T(n/2) + 2 
```

解决以上递归后，我们得到：

```
  T(n)  = 3n/2 -2 
```

因此，如果`n`是 2 的幂，则该方法进行`3n / 2 - 2`比较，如果`n`不是 2 的幂，则该方法进行超过`3n / 2 - 2`比较。

方法 3（成对比较）：

如果`n`为奇数，则将`min`和`max`初始化为第一个元素。

如果`n`为偶数，则将`min`和`max`分别初始化为前两个元素的最小值和最大值。

对于其余元素，请成对选择它们并进行比较。

最大值和最小值分别为`max`和`min`。

## C++

```cpp
// C++ program of above implementation  
#include<iostream> 
using namespace std; 
  
// Structure is used to return  
// two values from minMax()  
struct Pair  
{ 
    int min; 
    int max; 
};  
  
struct Pair getMinMax(int arr[], int n) 
{ 
    struct Pair minmax;      
    int i;  
      
    // If array has even number of elements  
    // then initialize the first two elements  
    // as minimum and maximum  
    if (n % 2 == 0) 
    { 
        if (arr[0] > arr[1])      
        { 
            minmax.max = arr[0]; 
            minmax.min = arr[1]; 
        }  
        else
        { 
            minmax.min = arr[0]; 
            minmax.max = arr[1]; 
        } 
          
        // Set the startung index for loop  
        i = 2;  
    }  
      
    // If array has odd number of elements 
    // then initialize the first element as 
    // minimum and maximum 
    else
    { 
        minmax.min = arr[0]; 
        minmax.max = arr[0]; 
          
        // Set the startung index for loop  
        i = 1;  
    } 
      
    // In the while loop, pick elements in 
    // pair and compare the pair with max  
    // and min so far 
    while (i < n - 1)  
    {          
        if (arr[i] > arr[i + 1])          
        { 
            if(arr[i] > minmax.max)      
                minmax.max = arr[i]; 
                  
            if(arr[i + 1] < minmax.min)          
                minmax.min = arr[i + 1];      
        }  
        else        
        { 
            if (arr[i + 1] > minmax.max)      
                minmax.max = arr[i + 1]; 
                  
            if (arr[i] < minmax.min)          
                minmax.min = arr[i];      
        } 
          
        // Increment the index by 2 as  
        // two elements are processed in loop 
        i += 2;  
    }          
    return minmax; 
}  
  
// Driver code 
int main() 
{ 
    int arr[] = { 1000, 11, 445,  
                  1, 330, 3000 }; 
    int arr_size = 6; 
      
    Pair minmax = getMinMax(arr, arr_size); 
      
    cout << "nMinimum element is " 
         << minmax.min << endl; 
    cout << "nMaximum element is "
         << minmax.max; 
           
    return 0; 
} 
  
// This code is contributed by nik_3112 
```

## C

```c
#include<stdio.h> 
  
/* structure is used to return two values from minMax() */
struct pair  
{ 
  int min; 
  int max; 
};   
  
struct pair getMinMax(int arr[], int n) 
{ 
  struct pair minmax;      
  int i;   
  
  /* If array has even number of elements then  
    initialize the first two elements as minimum and  
    maximum */
  if (n%2 == 0) 
  {          
    if (arr[0] > arr[1])      
    { 
      minmax.max = arr[0]; 
      minmax.min = arr[1]; 
    }   
    else
    { 
      minmax.min = arr[0]; 
      minmax.max = arr[1]; 
    } 
    i = 2;  /* set the startung index for loop */
  }   
  
   /* If array has odd number of elements then  
    initialize the first element as minimum and  
    maximum */ 
  else
  { 
    minmax.min = arr[0]; 
    minmax.max = arr[0]; 
    i = 1;  /* set the startung index for loop */
  } 
    
  /* In the while loop, pick elements in pair and  
     compare the pair with max and min so far */    
  while (i < n-1)   
  {           
    if (arr[i] > arr[i+1])           
    { 
      if(arr[i] > minmax.max)         
        minmax.max = arr[i]; 
      if(arr[i+1] < minmax.min)           
        minmax.min = arr[i+1];         
    }  
    else         
    { 
      if (arr[i+1] > minmax.max)         
        minmax.max = arr[i+1]; 
      if (arr[i] < minmax.min)           
        minmax.min = arr[i];         
    }         
    i += 2; /* Increment the index by 2 as two  
               elements are processed in loop */
  }             
  
  return minmax; 
}     
  
/* Driver program to test above function */
int main() 
{ 
  int arr[] = {1000, 11, 445, 1, 330, 3000}; 
  int arr_size = 6; 
  struct pair minmax = getMinMax (arr, arr_size); 
  printf("nMinimum element is %d", minmax.min); 
  printf("nMaximum element is %d", minmax.max); 
  getchar(); 
} 
```

## Java

```java
// Java program of above implementation 
public class GFG { 
  
/* Class Pair is used to return two values from getMinMax() */
    static class Pair { 
  
        int min; 
        int max; 
    } 
  
    static Pair getMinMax(int arr[], int n) { 
        Pair minmax = new Pair(); 
        int i; 
        /* If array has even number of elements then   
    initialize the first two elements as minimum and   
    maximum */
        if (n % 2 == 0) { 
            if (arr[0] > arr[1]) { 
                minmax.max = arr[0]; 
                minmax.min = arr[1]; 
            } else { 
                minmax.min = arr[0]; 
                minmax.max = arr[1]; 
            } 
            i = 2; 
            /* set the startung index for loop */
        } /* If array has odd number of elements then   
    initialize the first element as minimum and   
    maximum */ else { 
            minmax.min = arr[0]; 
            minmax.max = arr[0]; 
            i = 1; 
            /* set the startung index for loop */
        } 
  
        /* In the while loop, pick elements in pair and   
     compare the pair with max and min so far */
        while (i < n - 1) { 
            if (arr[i] > arr[i + 1]) { 
                if (arr[i] > minmax.max) { 
                    minmax.max = arr[i]; 
                } 
                if (arr[i + 1] < minmax.min) { 
                    minmax.min = arr[i + 1]; 
                } 
            } else { 
                if (arr[i + 1] > minmax.max) { 
                    minmax.max = arr[i + 1]; 
                } 
                if (arr[i] < minmax.min) { 
                    minmax.min = arr[i]; 
                } 
            } 
            i += 2; 
            /* Increment the index by 2 as two   
               elements are processed in loop */
        } 
  
        return minmax; 
    } 
  
    /* Driver program to test above function */
    public static void main(String args[]) { 
        int arr[] = {1000, 11, 445, 1, 330, 3000}; 
        int arr_size = 6; 
        Pair minmax = getMinMax(arr, arr_size); 
        System.out.printf("\nMinimum element is %d", minmax.min); 
        System.out.printf("\nMaximum element is %d", minmax.max); 
  
    } 
} 
```

## Python3

```py
# Python3 program of above implementation  
def getMinMax(arr): 
      
    n = len(arr) 
      
    # If array has even number of elements then  
    # initialize the first two elements as minimum  
    # and maximum  
    if(n % 2 == 0): 
        mx = max(arr[0], arr[1]) 
        mn = min(arr[0], arr[1]) 
          
        # set the starting index for loop  
        i = 2
          
    # If array has odd number of elements then  
    # initialize the first element as minimum  
    # and maximum  
    else: 
        mx = mn = arr[0] 
          
        # set the starting index for loop  
        i = 1
          
    # In the while loop, pick elements in pair and  
    # compare the pair with max and min so far  
    while(i < n - 1): 
        if arr[i] < arr[i + 1]: 
            mx = max(mx, arr[i + 1]) 
            mn = min(mn, arr[i]) 
        else: 
            mx = max(mx, arr[i]) 
            mn = min(mn, arr[i + 1]) 
              
        # Increment the index by 2 as two  
        # elements are processed in loop  
        i += 2
      
    return (mx, mn) 
      
# Driver Code 
if __name__ =='__main__': 
      
    arr = [1000, 11, 445, 1, 330, 3000] 
    mx, mn = getMinMax(arr) 
    print("Minimum element is", mn) 
    print("Maximum element is", mx) 
      
# This code is contributed by Kaustav 
```

## C#

```cs
// C# program of above implementation 
using System; 
      
class GFG  
{ 
  
    /* Class Pair is used to return  
       two values from getMinMax() */
    public class Pair  
    { 
        public int min; 
        public int max; 
    } 
  
    static Pair getMinMax(int []arr, int n) 
    { 
        Pair minmax = new Pair(); 
        int i; 
          
        /* If array has even number of elements  
        then initialize the first two elements  
        as minimum and maximum */
        if (n % 2 == 0)  
        { 
            if (arr[0] > arr[1]) 
            { 
                minmax.max = arr[0]; 
                minmax.min = arr[1]; 
            }  
            else
            { 
                minmax.min = arr[0]; 
                minmax.max = arr[1]; 
            } 
            i = 2; 
        } 
          
        /* set the startung index for loop */
        /* If array has odd number of elements then  
        initialize the first element as minimum and  
        maximum */ 
        else 
        { 
            minmax.min = arr[0]; 
            minmax.max = arr[0]; 
            i = 1; 
            /* set the startung index for loop */
        } 
  
        /* In the while loop, pick elements in pair and  
        compare the pair with max and min so far */
        while (i < n - 1)  
        { 
            if (arr[i] > arr[i + 1])  
            { 
                if (arr[i] > minmax.max)  
                { 
                    minmax.max = arr[i]; 
                } 
                if (arr[i + 1] < minmax.min) 
                { 
                    minmax.min = arr[i + 1]; 
                } 
            }  
            else
            { 
                if (arr[i + 1] > minmax.max) 
                { 
                    minmax.max = arr[i + 1]; 
                } 
                if (arr[i] < minmax.min) 
                { 
                    minmax.min = arr[i]; 
                } 
            } 
            i += 2; 
              
            /* Increment the index by 2 as two  
            elements are processed in loop */
        } 
        return minmax; 
    } 
  
    // Driver Code 
    public static void Main(String []args)  
    { 
        int []arr = {1000, 11, 445, 1, 330, 3000}; 
        int arr_size = 6; 
        Pair minmax = getMinMax(arr, arr_size); 
        Console.Write("Minimum element is {0}", 
                                   minmax.min); 
        Console.Write("\nMaximum element is {0}",  
                                     minmax.max); 
    } 
} 
  
// This code is contributed by 29AjayKumar 
```

输出：

```
Minimum element is 1
Maximum element is 3000
```

时间复杂度：`O(n)`。

比较总数：偶数和奇数`n`不同，请参见下文：

```
       If n is odd:    3*(n-1)/2  
       If n is even:   1 Initial comparison for initializing min and max, 
                           and 3(n-2)/2 comparisons for rest of the elements  
                      =  1 + 3*(n-2)/2 = 3n/2 -2
```

当`n`为 2 的幂时，第二种和第三种方法进行的比较次数相等。

通常，方法 3 似乎是最好的。