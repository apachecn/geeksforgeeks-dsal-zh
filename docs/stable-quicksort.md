# 稳定快速排序

> 原文:[https://www.geeksforgeeks.org/stable-quicksort/](https://www.geeksforgeeks.org/stable-quicksort/)

如果一个[排序算法](https://www.geeksforgeeks.org/sorting-algorithms/)在键相等的情况下保持记录的相对顺序，则称其为[稳定](https://www.geeksforgeeks.org/stability-in-sorting-algorithms/)。

> 输入:(1，5)，(3，2) (1，2) (5，4) (6，4)
> 我们需要按照第一个数字的键的递增顺序对键值对进行排序
> 对于键相同的两对有两种可能的解决方案，即(1，5)和(1，2)，如下所示:
> OUTPUT1: (1，5)，(1，2)，(3，2)，(5，4)，(6，4)
> OUTPUT2: (1，2)，(1，5)，(3，2)，(5)，(5，4)您可以看到，在排序顺序中(1，5)在(1，2)之前，这是原始顺序，即在给定的输入中，(1，5)在(1，2)之前。
> 秒输出只能由不稳定的算法产生。您可以看到，在第二个输出中，(1，2)在(1，5)之前，而在原始输入中不是这样。

有些排序算法本质上是稳定的，比如[插入排序](https://www.geeksforgeeks.org/insertion-sort/)、[合并排序](https://www.geeksforgeeks.org/merge-sort/)、[冒泡排序](https://www.geeksforgeeks.org/bubble-sort/)等。而有些排序算法则不是，比如[堆排序](https://www.geeksforgeeks.org/heap-sort/)、[快速排序](https://www.geeksforgeeks.org/quick-sort/)等。
快速排序是一个不稳定的算法，因为我们根据枢轴的位置来交换元素(不考虑它们的原始位置)。
**如何让快速排序稳定？**

快速排序可以是稳定的，但通常不是这样实现的。要使它稳定，要么需要 N 阶存储(就像在一个简单的实现中一样)，要么需要一点额外的逻辑来实现一个就地版本。
在下面的实现中，我们使用了额外的空间。想法是制作两个单独的列表:
1)第一个列表包含小于 pivot 的项目。
2)第二个列表包含大于枢轴的项目。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement Stable QuickSort.
// The code uses middle element as pivot.
import java.util.*;
class GFG
{
    public static ArrayList<Integer> quickSort(ArrayList<Integer> ar)
    {

        // Base case
        if(ar.size() <= 1)
        {
            return ar;
        }
        else
        {

            // Let us choose middle element a pivot            
            int mid = ar.size() / 2;
            int pivat = ar.get(mid);

           // key element is used to break the array
            // into 2 halves according to their values
            ArrayList<Integer> smaller = new ArrayList<>();
            ArrayList<Integer> greater = new ArrayList<>();

            // Put greater elements in greater list,
           // smaller elements in smaller list. Also,
           // compare positions to decide where to put.        
           for(int ind = 0; ind < ar.size(); ind++)
           {
               int val = ar.get(ind);
               if( ind != mid )
               {
                   if( val < pivat )
                   {
                       smaller.add(val);
                   }
                   else if(val > pivat)
                   {
                       greater.add(val);
                   }
                   else
                   {

                       // If value is same, then considering
                       // position to decide the list.                   
                       if(ind < mid)
                       {
                           smaller.add(val);
                       }
                       else
                       {
                           greater.add(val);
                       }
                   }
               }
           }

           ArrayList<Integer> ans = new ArrayList<Integer>();              
           ArrayList<Integer> sa1 = quickSort(smaller);
           ArrayList<Integer> sa2 = quickSort(greater);

           // add all elements of smaller list into ans list
           for(Integer val1 : sa1)
                ans.add(val1);

           // add pivat element into ans list   
           ans.add(pivat);

           // add all elements of greater list into ans list
           for(Integer val2 : sa2)
                ans.add(val2);

           // return ans list
           return ans;        
        }
    }

    // Driver code 
    public static void main(String args[])
    {      
        int ar[] = {10, 7, 8, 9, 1, 5};
        ArrayList<Integer> al = new ArrayList<>();
        al.add(10);
        al.add(7);
        al.add(8);
        al.add(9);
        al.add(1);
        al.add(5);       
        ArrayList<Integer> sortedAr = quickSort(al);
        System.out.println(sortedAr);
    }
}

// This code is contributed by Naresh Saharan
```

## 蟒蛇 3

```
# Python code to implement Stable QuickSort.
# The code uses middle element as pivot.
def quickSort(ar):

    # Base case
    if len(ar) <= 1:
        return ar

    # Let us choose middle element a pivot
    else:
        mid = len(ar)//2
        pivot = ar[mid]

        # key element is used to break the array
        # into 2 halves according to their values
        smaller,greater = [],[]

        # Put greater elements in greater list,
        # smaller elements in smaller list. Also,
        # compare positions to decide where to put.
        for indx, val in enumerate(ar):
            if indx != mid:
                if val < pivot:
                    smaller.append(val)
                elif val > pivot:
                    greater.append(val)

                # If value is same, then considering
                # position to decide the list.
                else:
                    if indx < mid:
                        smaller.append(val)
                    else:
                        greater.append(val)
        return quickSort(smaller)+[pivot]+quickSort(greater)

# Driver code to test above
ar = [10, 7, 8, 9, 1, 5]
sortedAr = quickSort(ar)
print(sortedAr)
```

**Output**

```
[1, 5, 7, 8, 9, 10]
```

在上面的代码中，我们有意使用中间元素作为轴心来演示如何将位置作为比较的一部分。如果我们使用最后一个元素作为轴心，代码会简化很多。在最后一个元素的情况下，我们总是可以在较小的列表中推送相等的元素。