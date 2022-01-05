# 找到最大间隔重叠的点

> 原文:[https://www . geesforgeks . org/find-最大间隔重叠点/](https://www.geeksforgeeks.org/find-the-point-where-maximum-intervals-overlap/)

考虑一个大型聚会，其中保存了客人进出时间的日志记录。找出聚会中客人最多的时间。请注意，寄存器中的条目没有任何顺序。
**例:**

```
Input: arrl[] = {1, 2, 9, 5, 5}
       exit[] = {4, 5, 12, 9, 12}
First guest in array arrives at 1 and leaves at 4, 
second guest arrives at 2 and leaves at 5, and so on.

Output: 5
There are maximum 3 guests at time 5\.  
```

下面是一个**简单的方法**来解决这个问题。
1)遍历所有时间间隔，找出最小和最大时间(第一个客人到达的时间和最后一个客人离开的时间)
2)创建一个大小为“最大–最小+ 1”的计数数组。让数组为 count[]。
3)对于每个间隔[x，y]，运行 i = x 到 y 的循环，并在循环中执行以下操作。
计数[I–min]+++；
4)求计数数组中最大元素的索引。让这个索引为“max_index”，返回 max_index + min。
上述解决方案需要 0(最大-最小+1)个额外空间。上述解决方案的时间复杂度也取决于间隔的长度。在最坏的情况下，如果所有的时间间隔都是从“最小”到“最大”，那么时间复杂度就变成了 O((最大-最小+1)*n)，其中 n 是时间间隔的数量。
一个**高效的解决方案**就是利用排序 n O(nLogn)时间。其思想是以排序的顺序考虑所有事件(所有到达和离开)。一旦我们将所有事件按顺序排序，我们就可以随时跟踪客人的数量，跟踪已经到达但尚未离开的客人。
考虑上面的例子。

```
    arr[]  = {1, 2, 10, 5, 5}
    dep[]  = {4, 5, 12, 9, 12}

Below are all events sorted by time.  Note that in sorting, if two
events have same time, then arrival is preferred over exit.
 Time     Event Type         Total Number of Guests Present
------------------------------------------------------------
   1        Arrival                  1
   2        Arrival                  2
   4        Exit                     1
   5        Arrival                  2
   5        Arrival                  3    // Max Guests
   5        Exit                     2
   9        Exit                     1
   10       Arrival                  2 
   12       Exit                     1
   12       Exit                     0 
```

任何时间的总客人数可以通过从该时间的总到达人数中减去
总退出人数得到。
所以在时间 5 最多有三个客人。
以下是上述办法的实施情况。请注意，该实现没有创建所有事件的单个排序列表，而是单独对 arr[]和 dep[]数组进行排序，然后使用 merge sort 的 merge process 将它们作为单个排序数组一起处理。

## C++

```
// Program to find maximum guest at any time in a party
#include<iostream>
#include<algorithm>
using namespace std;

void findMaxGuests(int arrl[], int exit[], int n)
{
   // Sort arrival and exit arrays
   sort(arrl, arrl+n);
   sort(exit, exit+n);

   // guests_in indicates number of guests at a time
   int guests_in = 1, max_guests = 1, time = arrl[0];
   int i = 1, j = 0;

   // Similar to merge in merge sort to process
   // all events in sorted order
   while (i < n && j < n)
   {
      // If next event in sorted order is arrival,
      // increment count of guests
      if (arrl[i] <= exit[j])
      {
          guests_in++;

          // Update max_guests if needed
          if (guests_in > max_guests)
          {
              max_guests = guests_in;
              time = arrl[i];
          }
          i++;  //increment index of arrival array
      }
      else // If event is exit, decrement count
      {    // of guests.
          guests_in--;
          j++;
      }
   }

   cout << "Maximum Number of Guests = " << max_guests
        << " at time " << time;
}

// Driver program to test above function
int main()
{
    int arrl[] = {1, 2, 10, 5, 5};
    int exit[] = {4, 5, 12, 9, 12};
    int n = sizeof(arrl)/sizeof(arrl[0]);
    findMaxGuests(arrl, exit, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find maximum guest
// at any time in a party
import java.util.*;

class GFG {

    static void findMaxGuests(int arrl[], int exit[],
                                          int n)   
    {  
    // Sort arrival and exit arrays
    Arrays.sort(arrl);
    Arrays.sort(exit);

    // guests_in indicates number of guests at a time
    int guests_in = 1, max_guests = 1, time = arrl[0];
    int i = 1, j = 0;

    // Similar to merge in merge sort to process
    // all events in sorted order
    while (i < n && j < n)
    {
        // If next event in sorted order is arrival,
        // increment count of guests
        if (arrl[i] <= exit[j])
        {
            guests_in++;

            // Update max_guests if needed
            if (guests_in > max_guests)
            {
                max_guests = guests_in;
                time = arrl[i];
            }
            i++; //increment index of arrival array
        }
        else // If event is exit, decrement count
        { // of guests.
            guests_in--;
            j++;
        }
    }

    System.out.println("Maximum Number of Guests = "+
                    max_guests + " at time " + time);
    }

    // Driver program to test above function
    public static void main(String[] args)
    {
        int arrl[] = {1, 2, 10, 5, 5};
        int exit[] = {4, 5, 12, 9, 12};
        int n = arrl.length;
        findMaxGuests(arrl, exit, n);
    }
}
// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Program to find maximum guest
# at any time in a party
def findMaxGuests(arrl, exit, n):

    # Sort arrival and exit arrays
    arrl.sort();
    exit.sort();

    # guests_in indicates number of
    # guests at a time
    guests_in = 1;
    max_guests = 1;
    time = arrl[0];
    i = 1;
    j = 0;

    # Similar to merge in merge sort to
    # process all events in sorted order
    while (i < n and j < n):

        # If next event in sorted order is
        # arrival, increment count of guests
        if (arrl[i] <= exit[j]):

            guests_in = guests_in + 1;

        # Update max_guests if needed
            if(guests_in > max_guests):

                max_guests = guests_in;
                time = arrl[i];

            # increment index of arrival array
            i = i + 1;

        else:
            guests_in = guests_in - 1;
            j = j + 1;

    print("Maximum Number of Guests =",
           max_guests, "at time", time)

# Driver Code
arrl = [1, 2, 10, 5, 5];
exit = [4, 5, 12, 9, 12];
n = len(arrl);
findMaxGuests(arrl, exit, n);

# This code is contributed
# by Shivi_Aggarwal
```

## C#

```
// C# Program to find maximum guest
// at any time in a party
using System;
class GFG
{
    static void findMaxGuests(int []arrl,
                              int []exit,
                              int n)
    {
    // Sort arrival and exit arrays
    Array.Sort(arrl);
    Array.Sort(exit);

    // guests_in indicates number
    // of guests at a time
    int guests_in = 1,
        max_guests = 1,
        time = arrl[0];
    int i = 1, j = 0;

    // Similar to merge in merge sort
    // to process all events in sorted order
    while (i < n && j < n)
    {
        // If next event in sorted
        // order is arrival,
        // increment count of guests
        if (arrl[i] <= exit[j])
        {
            guests_in++;

            // Update max_guests if needed
            if (guests_in > max_guests)
            {
                max_guests = guests_in;
                time = arrl[i];
            }

            //increment index of arrival array
            i++;
        }

         // If event is exit, decrement
         // count of guests.
        else
        {
            guests_in--;
            j++;
        }
    }

    Console.Write("Maximum Number of Guests = "+
                                    max_guests +
                            " at time " + time);
    }

    // Driver Code
    public static void Main()
    {
        int []arrl = {1, 2, 10, 5, 5};
        int []exit = {4, 5, 12, 9, 12};
        int n = arrl.Length;
        findMaxGuests(arrl, exit, n);
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find maximum
// guest at any time in a party

function findMaxGuests($arrl, $exit, $n)
{

    // Sort arrival and exit arrays
    sort($arrl);
    sort($exit);

    // guests_in indicates number
    // of guests at a time
    $guests_in = 1;
    $max_guests = 1;
    $time = $arrl[0];
    $i = 1;
    $j = 0;

    // Similar to merge in merge
    // sort to process all events
    // in sorted order
    while ($i < $n and $j < $n)
    {

        // If next event in sorted
        // order is arrival,
        // increment count of guests
        if ($arrl[$i] <= $exit[$j])
        {
            $guests_in++;

            // Update max_guests if needed
            if ($guests_in > $max_guests)
            {
                $max_guests = $guests_in;
                $time = $arrl[$i];
            }

            // increment index of
            // arrival array
            $i++;
        }

        // If event is exit, decrement
        // count of guests.
        else
        {                            
            $guests_in--;
            $j++;
        }
    }

    echo "Maximum Number of Guests = " , $max_guests
                               , " at time " , $time;
}

    // Driver Code
    $arr1 = array(1, 2, 10, 5, 5);
    $exit = array(4, 5, 12, 9, 120);
    $n = count($arr1);
    findMaxGuests($arr1, $exit, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

    // Javascript Program to find maximum guest
    // at any time in a party
    function findMaxGuests(arrl, exit, n)
    {

       // Sort arrival and exit arrays
       arrl.sort(function(a, b){return a - b});
       exit.sort(function(a, b){return a - b});

       // guests_in indicates number of guests at a time
       let guests_in = 1, max_guests = 1, time = arrl[0];
       let i = 1, j = 0;

       // Similar to merge in merge sort to process
       // all events in sorted order
       while (i < n && j < n)
       {

          // If next event in sorted order is arrival,
          // increment count of guests
          if (arrl[i] <= exit[j])
          {
              guests_in++;

              // Update max_guests if needed
              if (guests_in > max_guests)
              {
                  max_guests = guests_in;
                  time = arrl[i];
              }
              i++;  //increment index of arrival array
          }
          else // If event is exit, decrement count
          {    // of guests.
              guests_in--;
              j++;
          }
       }

       document.write("Maximum Number of Guests =
       " + max_guests + " at time " + time);
    }

    let arrl = [1, 2, 10, 5, 5];
    let exit = [4, 5, 12, 9, 12];
    let n = arrl.length;
    findMaxGuests(arrl, exit, n);

    // This code is contributed by divyeshrabadiya07.

</script>
```

**输出:**

```
Maximum Number of Guests = 3 at time 5
```

该方法的时间复杂度为 0。
感谢 Gaurav Ahirwar 提出这个方法。
**另一种高效解决方案:**
**方法:**
1)。创建一个用于存储起点和终点动态数据的辅助数组。
2)。循环遍历整个元素数组，将起点处的值增加 1，同样将终点之后的值减少 1。
【这里我们使用了表达式“x[start[i]]-=1”和“x[end[I]+1]-= 1”]
3】。循环时，在计算辅助数组后:将当前索引处的值永久相加，并检查从左向右遍历的最大值索引。

## C++

```
#include<bits/stdc++.h>
using namespace std;

void maxOverlap(vector<int>& start, vector<int>& end )
{

    int n= start.size();

    // Finding maximum starting time O(n)
    int maxa=*max_element(start.begin(), start.end());

    // Finding maximum ending time O(n)
    int maxb=*max_element(end.begin(), end.end());

    int maxc = max(maxa, maxb);

    int x[maxc + 2];
    memset(x, 0, sizeof x);

        int cur = 0, idx;

        // Creating and auxiliary array O(n)
        for(int i = 0; i < n; i++)
        {
            //Lazy addition
            ++x[start[i]];
            --x[end[i]+1];
        }

        int maxy = INT_MIN;

        //Lazily Calculating value at index i O(n)
        for(int i = 0; i <= maxc; i++)
        {
            cur += x[i];
            if(maxy < cur)
            {
                maxy = cur;
                idx = i;

            }        
        }
        cout<<"Maximum value is "<<maxy<<" at position "<<idx<<endl;
}

// Driver code
int main()
{    
        vector<int> start = {13, 28, 29, 14, 40, 17, 3},
                    end = {107, 95, 111, 105, 70, 127, 74};

        maxOverlap(start,end);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;
import java.util.*;
import java.text.*;
import java.math.*;
import java.util.regex.*;

class GFG
{

public static void maxOverlap(int []start,int [] end ,int n)
{
    // Finding maximum starting time
    int maxa = Arrays.stream(start).max().getAsInt();

    // Finding maximum ending time
    int maxb = Arrays.stream(end).max().getAsInt();

    int maxc = Math.max(maxa,maxb);

    int []x = new int[maxc + 2];
    Arrays.fill(x, 0);

    int cur=0,idx=0;

    // reating an auxiliary array
    for(int i = 0; i < n; i++)
    {
        // Lazy addition
        ++x[start[i]];
        --x[end[i]+1];
    }

    int maxy=Integer.MIN_VALUE;

    //Lazily Calculating value at index i
    for(int i = 0; i <= maxc; i++)
    {
        cur+=x[i];
        if(maxy < cur)
        {
            maxy = cur;
            idx = i;

        }        
    }
        System.out.println("Maximum value is:"+
                        maxy+" at position: "+idx+"");

}

// Driver code
public static void main(String[] args)
{
    int [] start = new int[]{13, 28, 29, 14, 40, 17, 3 };
    int [] end = new int[]{107, 95, 111, 105, 70, 127, 74};
    int n = start.length;

    maxOverlap(start,end,n);
}
}
```

## 蟒蛇 3

```
import sys

def maxOverlap(start,end):

    n= len(start)
    maxa = max(start)# Finding maximum starting time
    maxb = max(end)  # Finding maximum ending time
    maxc=max(maxa,maxb)
    x =(maxc+2)*[0]
    cur=0; idx=0

    for i in range(0,n) :# CREATING AN AUXILIARY ARRAY
        x[start[i]]+=1 # Lazy addition
        x[end[i]+1]-=1

    maxy=-1
    #Lazily Calculating value at index i
    for i in range(0,maxc+1):
        cur+=x[i]
        if maxy<cur :
            maxy=cur
            idx=i    
    print("Maximum value is: {0:d}".format(maxy),
                     " at position: {0:d}".format(idx))
if __name__ == "__main__":

    start=[13,28,29,14,40,17,3]
    end=[107,95,111,105,70,127,74]

    maxOverlap(start,end)
```

## C#

```
// C# implementation of above approach
using System;
using System.Linq;

class GFG
{

public static void maxOverlap(int []start,int [] end ,int n)
{
    // Finding maximum starting time
    int maxa = start.Max();

    // Finding maximum ending time
    int maxb = end.Max();

    int maxc = Math.Max(maxa,maxb);

    int[] x = new int[maxc + 2];

    int cur = 0,idx = 0;

    // reating an auxiliary array
    for(int i = 0; i < n; i++)
    {
        // Lazy addition
        ++x[start[i]];
        --x[end[i]+1];
    }

    int maxy=int.MinValue;

    //Lazily Calculating value at index i
    for(int i = 0; i <= maxc; i++)
    {
        cur+=x[i];
        if(maxy < cur)
        {
            maxy = cur;
            idx = i;

        }    
    }
        Console.WriteLine("Maximum value is "+
                        maxy+" at position: "+idx+"");

}

// Driver code
public static void Main()
{
    int []start = {13, 28, 29, 14, 40, 17, 3 };
    int []end = {107, 95, 111, 105, 70, 127, 74};
    int n = start.Length;

    maxOverlap(start,end,n);
}
}

// This code is contributed by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

function maxOverlap($start, $end )
{

    $n= count($start);

    // Finding maximum starting time O(n)
    $maxa = max($start);

    //Finding maximum ending time O(n)
    $maxb = max($end);

    $maxc = max($maxa, $maxb);

    $x = array_fill(0, $maxc + 2, 0);

        $cur = 0;

        // Creating and auxiliary array O(n)
        for($i = 0; $i < $n; $i++)
        {
            // Lazy addition
            ++$x[$start[$i]];
            --$x[$end[$i]+1];
        }

        $maxy=-PHP_INT_MAX;

        // Lazily Calculating value at index i O(n)
        for($i = 0; $i <= $maxc; $i++)
        {
            $cur += $x[$i];
            if($maxy < $cur)
            {
                $maxy = $cur;
                $idx = $i;
            }    
        }
        echo "Maximum value is ".$maxy." at position ".$idx."\n";
}

    // Driver code
        $start = array(13,28,29,14,40,17,3);
        $end = array(107,95,111,105,70,127,74);

        maxOverlap($start,$end);

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>

    // Javascript implementation of above approach

    function maxOverlap(start, end, n)
    {
        // Finding maximum starting time
        let maxa = 0;
        for(let i = 0; i < start.length; i++)
        {
            maxa = Math.max(maxa, start[i]);
        }

        // Finding maximum ending time
        let maxb = 0;
        for(let i = 0; i < end.length; i++)
        {
            maxb = Math.max(maxb, end[i]);
        }

        let maxc = Math.max(maxa,maxb);

        let x = new Array(maxc + 2);
        x.fill(0);

        let cur = 0,idx = 0;

        // reating an auxiliary array
        for(let i = 0; i < n; i++)
        {
            // Lazy addition
            ++x[start[i]];
            --x[end[i]+1];
        }

        let maxy = Number.MIN_VALUE;

        //Lazily Calculating value at index i
        for(let i = 0; i <= maxc; i++)
        {
            cur+=x[i];
            if(maxy < cur)
            {
                maxy = cur;
                idx = i;

            }   
        }
        document.write(
"Maximum value is "+ maxy+" at position: "+idx+""
        );
    }

    let start = [13, 28, 29, 14, 40, 17, 3 ];
    let end = [107, 95, 111, 105, 70, 127, 74];
    let n = start.length;

    maxOverlap(start,end,n);

</script>
```

**输出:**

```
Maximum value is 7 at position 40
```

**时间复杂度:** O(最大(出发时间))
**辅助空间:** O(最大(出发时间))
感谢哈什特·赛尼提出这个方法。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。