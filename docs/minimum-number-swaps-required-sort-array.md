# 排序数组所需的最小交换次数

> 原文： [https://www.geeksforgeeks.org/minimum-number-swaps-required-sort-array/](https://www.geeksforgeeks.org/minimum-number-swaps-required-sort-array/)

给定`n`个不同元素的数组，请找到对数组进行排序所需的最小交换次数。

**示例**：

```
Input : {4, 3, 2, 1}
Output : 2
Explanation : Swap index 0 with 3 and 1 with 2 to 
              form the sorted array {1, 2, 3, 4}.

Input : {1, 5, 4, 3, 2}
Output : 2

```



通过将问题可视化为图形，可以轻松完成此操作。 如果第`i`个索引的元素必须存在于第`j`个索引中，则我们将有`n`个节点和一条从节点`i`指向节点`j`的边。 排序后的数组。

```

Graph for {4, 3, 2, 1}

```

该图现在将包含许多不相交的循环。 现在，具有 2 个节点的循环只需要进行 1 次交换即可达到正确的顺序，类似地，具有 3 个节点的循环也只需进行 2 次交换即可。

```

Graph for {4, 5, 2, 1, 5}

```

因此，

```
ans = Σ(cycle_size – 1), i = 1 ~ k
```

其中`k`是周期数。

以下是该想法的实现。

## C++ 

```cpp

// C++ program to find  minimum number of swaps 
// required to sort an array 
#include<bits/stdc++.h> 

using namespace std; 

// Function returns the minimum number of swaps 
// required to sort the array 
int minSwaps(int arr[], int n) 
{ 
    // Create an array of pairs where first 
    // element is array element and second element 
    // is position of first element 
    pair<int, int> arrPos[n]; 
    for (int i = 0; i < n; i++) 
    { 
        arrPos[i].first = arr[i]; 
        arrPos[i].second = i; 
    } 

    // Sort the array by array element values to 
    // get right position of every element as second 
    // element of pair. 
    sort(arrPos, arrPos + n); 

    // To keep track of visited elements. Initialize 
    // all elements as not visited or false. 
    vector<bool> vis(n, false); 

    // Initialize result 
    int ans = 0; 

    // Traverse array elements 
    for (int i = 0; i < n; i++) 
    { 
        // already swapped and corrected or 
        // already present at correct pos 
        if (vis[i] || arrPos[i].second == i) 
            continue; 

        // find out the number of  node in 
        // this cycle and add in ans 
        int cycle_size = 0; 
        int j = i; 
        while (!vis[j]) 
        { 
            vis[j] = 1; 

            // move to next node 
            j = arrPos[j].second; 
            cycle_size++; 
        } 

        // Update answer by adding current cycle.  
        if (cycle_size > 0) 
        { 
            ans += (cycle_size - 1); 
        } 
    } 

    // Return result 
    return ans; 
} 

// Driver program to test the above function 
int main() 
{ 
    int arr[] = {1, 5, 4, 3, 2}; 
    int n = (sizeof(arr) / sizeof(int)); 
    cout << minSwaps(arr, n); 
    return 0; 
} 

```

## Java

```java
// Java program to find  
// minimum number of swaps
// required to sort an array
import javafx.util.Pair;
import java.util.ArrayList;
import java.util.*;
 
class GfG
{
    // Function returns the 
    // minimum number of swaps
    // required to sort the array
    public static int minSwaps(int[] arr)
    {
        int n = arr.length;
 
        // Create two arrays and 
        // use as pairs where first
        // array is element and second array
        // is position of first element
        ArrayList <Pair <Integer, Integer> > arrpos =
                  new ArrayList <Pair <Integer, 
                                      Integer> > ();
        for (int i = 0; i < n; i++)
             arrpos.add(new Pair <Integer, 
                               Integer> (arr[i], i));
 
        // Sort the array by array element values to
        // get right position of every element as the
        // elements of second array.
        arrpos.sort(new Comparator<Pair<Integer, 
                                         Integer>>()
        {
            @Override
            public int compare(Pair<Integer, Integer> o1,
                               Pair<Integer, Integer> o2)
            {
                if (o1.getKey() > o2.getKey())
                    return -1;
 
                // We can change this to make 
                // it then look at the
                // words alphabetical order
                else if (o1.getKey().equals(o2.getKey()))
                    return 0;
 
                else
                    return 1;
            }
        });
 
        // To keep track of visited elements. Initialize
        // all elements as not visited or false.
        Boolean[] vis = new Boolean[n];
        Arrays.fill(vis, false);
 
        // Initialize result
        int ans = 0;
 
        // Traverse array elements
        for (int i = 0; i < n; i++)
        {
            // already swapped and corrected or
            // already present at correct pos
            if (vis[i] || arrpos.get(i).getValue() == i)
                continue;
 
            // find out the number of  node in
            // this cycle and add in ans
            int cycle_size = 0;
            int j = i;
            while (!vis[j])
            {
                vis[j] = true;
 
                // move to next node
                j = arrpos.get(j).getValue();
                cycle_size++;
            }
 
            // Update answer by adding current cycle.
            if(cycle_size > 0)
            {
                ans += (cycle_size - 1);
            }
        }
 
        // Return result
        return ans;
    }
}
 
// Driver class
class MinSwaps
{
    // Driver program to test the above function
    public static void main(String[] args)
    {
        int []a = {1, 5, 4, 3, 2};
        GfG g = new GfG();
        System.out.println(g.minSwaps(a));
    }
}
// This code is contributed by Saksham Seth
```

## Python3

```py
# Python3 program to find  minimum number 
# of swaps required to sort an array
 
# Function returns the minimum 
# number of swaps required to sort the array
def minSwaps(arr):
    n = len(arr)
     
    # Create two arrays and use 
    # as pairs where first array 
    # is element and second array
    # is position of first element
    arrpos = [*enumerate(arr)]
     
    # Sort the array by array element 
    # values to get right position of 
    # every element as the elements 
    # of second array.
    arrpos.sort(key = lambda it:it[1])
     
    # To keep track of visited elements. 
    # Initialize all elements as not 
    # visited or false.
    vis = {k:False for k in range(n)}
     
    # Initialize result
    ans = 0
    for i in range(n):
         
        # alreadt swapped or 
        # alreadt present at 
        # correct position
        if vis[i] or arrpos[i][0] == i:
            continue
             
        # find number of nodes 
        # in this cycle and
        # add it to ans
        cycle_size = 0
        j = i
        while not vis[j]:
             
            # mark node as visited
            vis[j] = True
             
            # move to next node
            j = arrpos[j][0]
            cycle_size += 1
             
        # update answer by adding
        # current cycle
        if cycle_size > 0:
            ans += (cycle_size - 1)
    # return answer
    return ans
 
# Driver Code     
arr = [1, 5, 4, 3, 2]
print(minSwaps(arr))
 
# This code is contributed
# by Dharan Aditya
```

输出：

```
2
```

时间复杂度：`O(n Log n)`。

辅助空间：`O(n)`。

直接解决方案：

在数组上进行迭代时，请检查当前元素，如果位置不正确，请将该元素替换为应该在该位置出现的元素的索引。

下面是上述方法的实现：

## Java

```java
// Java program to find
// minimum number of swaps
// required to sort an array
import java.util.*;
import java.io.*;
 
class GfG 
{
 
    // Return the minimum number
    // of swaps required to sort the array
    public int minSwaps(int[] arr, int N)
    {
        int ans = 0;
        int[] temp = Arrays.copyOfRange(arr, 0, N);
        Arrays.sort(temp);
        for (int i = 0; i < N; i++) 
        {
 
            // This is checking whether
            // the current element is
            // at the right place or not
            if (arr[i] != temp[i]) 
            {
                ans++;
 
                // Swap the current element
                // with the right index
                // so that arr[0] to arr[i] is sorted
                swap(arr, i, indexOf(arr, temp[i]));
            }
        }
        return ans;
    }
    public void swap(int[] arr, int i, int j)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
    public int indexOf(int[] arr, int ele)
    {
        for (int i = 0; i < arr.length; i++) 
        {
            if (arr[i] == ele) {
                return i;
            }
        }
        return -1;
    }
}
// Driver class
class Main 
{
     
    // Driver program to test 
    // the above function
    public static void main(String[] args) 
                             throws Exception
    {
        int[] a
            = { 101, 758, 315, 730, 472, 
                         619, 460, 479 };
        int n = a.length;
        // Output will be 5
        System.out.println(new GfG().minSwaps(a, n));
    }
}
```

输出：

```
5
```

时间复杂度：`O(n * n)`。

辅助空间：`O(n)`。

我们仍然可以通过使用哈希图来提高复杂性。 这里的主要操作是循环内部的`indexOf`方法，这使我们付出了`n * n`的代价。 通过使用哈希图存储索引，我们可以将此部分改进为`O(n)`。 仍然使用排序方法，因此复杂度无法提高到`O(n Log n)`。

使用`HashMap`的方法：

与以前一样，创建一个新数组（称为`temp`），这是输入数组的排序形式。 我们知道我们需要以最少的交换次数将输入数组转换为新数组（`temp`）。 制作一个映射，该映射存储输入数组的元素及其对应的索引。

因此，在给定数组中，每个`i`从 0 到`N`开始，其中`N`是数组的大小：

1.  如果我根据排序后的数组不在正确的位置，则

2.  我们将使用我们构建的哈希表中的正确元素填充该位置。 我们知道应该在此处的正确元素是`temp[i]`，因此我们从哈希图中查找该元素的索引。

3.  交换所需元素后，我们将哈希图的内容相应地更新，如`temp[i]`到第`i`个位置，以及`arr[i]`到`temp[i]`的较早位置。

下面是上述方法的实现：

## Java

```java
// Java program to find
// minimum number of swaps
// required to sort an array
import java.util.*;
import java.io.*;
 
class GfG 
{
 
    // Return the minimum number
    // of swaps required to sort the array
    public int minSwaps(int[] arr, int N)
    {
 
        int ans = 0;
        int[] temp = Arrays.copyOfRange(arr, 0, N);
 
        // Hashmap which stores the
        // indexes of the input array
        HashMap<Integer, Integer> h
            = new HashMap<Integer, Integer>();
 
        Arrays.sort(temp);
        for (int i = 0; i < N; i++) 
        {
            h.put(arr[i], i);
        }
        for (int i = 0; i < N; i++) 
        {
 
            // This is checking whether
            // the current element is
            // at the right place or not
            if (arr[i] != temp[i]) 
            {
                ans++;
                int init = arr[i];
 
                // If not, swap this element
                // with the index of the
                // element which should come here
                swap(arr, i, h.get(temp[i]));
 
                // Update the indexes in
                // the hashmap accordingly
                h.put(init, h.get(temp[i]));
                h.put(temp[i], i);
            }
        }
        return ans;
    }
    public void swap(int[] arr, int i, int j)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
}
 
// Driver class
class Main 
{
 
    // Driver program to test the above function
    public static void main(String[] args) 
                           throws Exception
    {
        int[] a
            = { 101, 758, 315, 730, 472, 
                        619, 460, 479 };
        int n = a.length;
        // Output will be 5
        System.out.println(new GfG().minSwaps(a, n));
    }
}
```

输出：

```
5
```

时间复杂度：`O(n Log n)`。

辅助空间：`O(n)`。