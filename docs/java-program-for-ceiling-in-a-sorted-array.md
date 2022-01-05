# 排序数组中天花板的 Java 程序

> 原文:[https://www . geeksforgeeks . org/Java-程序换天花板排序数组/](https://www.geeksforgeeks.org/java-program-for-ceiling-in-a-sorted-array/)

给定一个已排序的数组和值 x，x 的上限是数组中大于或等于 x 的最小元素，下限是小于或等于 x 的最大元素，假设数组按非递减顺序排序。写高效函数求楼层和天花板的 x.
**例:**

```
For example, let the input array be {1, 2, 8, 10, 10, 12, 19}
For x = 0:    floor doesn't exist in array,  ceil  = 1
For x = 1:    floor  = 1,  ceil  = 1
For x = 5:    floor  = 2,  ceil  = 8
For x = 20:   floor  = 19,  ceil doesn't exist in array
```

在下面的方法中，我们只实现了上限搜索功能。楼层搜索也可以用同样的方式实现。
**方法 1(线性搜索)**
搜索 x 上限的算法:
1)如果 x 小于或等于数组中的第一个元素，则返回 0(第一个元素的索引)
2)否则线性搜索索引 I，使 x 位于 arr[i]和 arr[i+1]之间。
3)如果在步骤 2 中没有找到索引 I，则返回-1

## Java 语言(一种计算机语言，尤用于创建网站)

```
class Main
{
    /* Function to get index of ceiling 
       of x in arr[low..high] */
    static int ceilSearch(int arr[], int low, int high, int x)
    {
      int i;    

      /* If x is smaller than or equal to first 
         element,then return the first element */
      if(x <= arr[low])
        return low;  

      /* Otherwise, linearly search for ceil value */
      for(i = low; i < high; i++)
      {
        if(arr[i] == x)
          return i;

        /* if x lies between arr[i] and arr[i+1] 
        including arr[i+1], then return arr[i+1] */
        if(arr[i] < x && arr[i+1] >= x)
           return i+1;
      }         

      /* If we reach here then x is greater than the 
      last element of the array,  return -1 in this case */
      return -1;
    }

    /* Driver program to check above functions */
    public static void main (String[] args)
    {
       int arr[] = {1, 2, 8, 10, 10, 12, 19};
       int n = arr.length;
       int x = 3;
       int index = ceilSearch(arr, 0, n-1, x);
       if(index == -1)
         System.out.println("Ceiling of "+x+" doesn't exist in array");
       else
         System.out.println("ceiling of "+x+" is "+arr[index]);
    }  
}
```

**输出:**

```
ceiling of 3 is 8
```

**时间复杂度:** O(n)
**方法 2(二分搜索法)**
这里不用线性搜索，而是用二分搜索法来找出索引。二分搜索法将时间复杂度降低到 0(Logn)。

## Java 语言(一种计算机语言，尤用于创建网站)

```
class Main
{
    /* Function to get index of 
       ceiling of x in arr[low..high]*/
    static int ceilSearch(int arr[], int low, int high, int x)
    {
      int mid;    

      /* If x is smaller than or equal to the 
         first element, then return the first element */
      if(x <= arr[low])
        return low; 

      /* If x is greater than the last 
         element, then return -1 */
      if(x > arr[high])
        return -1;  

      /* get the index of middle element 
         of arr[low..high]*/
      mid = (low + high)/2;  /* low + (high - low)/2 */

      /* If x is same as middle element, 
         then return mid */
      if(arr[mid] == x)
        return mid;

      /* If x is greater than arr[mid], then 
         either arr[mid + 1] is ceiling of x or 
         ceiling lies in arr[mid+1...high] */ 
      else if(arr[mid] < x)
      {
        if(mid + 1 <= high && x <= arr[mid+1])
          return mid + 1;
        else
          return ceilSearch(arr, mid+1, high, x);
      }

      /* If x is smaller than arr[mid], 
         then either arr[mid] is ceiling of x 
         or ceiling lies in arr[low...mid-1] */   
      else
      {
        if(mid - 1 >= low && x > arr[mid-1])
          return mid;
        else    
          return ceilSearch(arr, low, mid - 1, x);
      }
    }

    /* Driver program to check above functions */
    public static void main (String[] args)
    {
       int arr[] = {1, 2, 8, 10, 10, 12, 19};
       int n = arr.length;
       int x = 8;
       int index = ceilSearch(arr, 0, n-1, x);
       if(index == -1)
         System.out.println("Ceiling of "+x+" doesn't exist in array");
       else 
         System.out.println("ceiling of "+x+" is "+arr[index]);
    }  
}
```

**输出:**

```
Ceiling of 20 doesn't exist in array 
```

时间复杂度:O(Logn)

**相关文章:**
[排序数组中的 floor](https://www.geeksforgeeks.org/floor-in-a-sorted-array/)
[在未排序数组中查找 Floor 和 ceil](https://www.geeksforgeeks.org/find-floor-ceil-unsorted-array/)
如果您发现以上代码/算法中有任何一个不正确，或者找到更好的方法来解决相同的问题，或者想要为 Floor 实现共享代码，请写评论。

更多详情请参考完整文章[排序数组](https://www.geeksforgeeks.org/ceiling-in-a-sorted-array/)中的上限！