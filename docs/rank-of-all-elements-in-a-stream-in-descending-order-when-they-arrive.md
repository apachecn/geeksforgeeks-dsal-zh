# 一个流中所有元素到达时按降序排列

> 原文:[https://www . geesforgeks . org/按到达时间降序排列所有元素的等级/](https://www.geeksforgeeks.org/rank-of-all-elements-in-a-stream-in-descending-order-when-they-arrive/)

给定一个数字流作为 **arr** ，任务是当它们到达时，按照降序找到流中每个元素的等级。

> Rank 被定义为大于到达元素的元素总数，其中 rank 1 定义了流中的最大值。数组中的每个值都是唯一的。

**例:**

> **输入:**arr =【88，14，69，30，29，89】
> **输出:** 1 2 2 3 4 1
> **解释:**
> 第一个 88 到达，所以它的等级是 1。
> 当 14 到来时，14 小于 88，所以它的等级是 2。
> 69 到的时候，69 小于 88 大于 14，所以排名是 2。
> 30 到了，30 小于 88 和 69，所以排名是 3。
> 29 到的时候，29 比 88 少，69 少，30 比 29 少，所以它的排名是 4。
> 当 89 到达时，89 大于所有值，因此其等级为 1。
> 数组 1 2 2 3 4 1
> **元素的秩输入:**arr =【100，110，80，85，88，89】
> **输出:**1 3 3 3 3
> **解释:**
> 前 100 个到达，所以它的秩是 1。
> 当 110 到达时，110 大于 100，所以它的等级是 1。
> 当 80 到达时，80 小于 110 和 100，所以它的等级是 3。
> 当 85 到达时，85 小于 110 和 100，所以它的等级是 3。
> 当 88 到达时，88 小于 110 和 100，所以它的等级是 3。
> 当 89 到达时，89 小于 110 和 100，所以它的等级是 3。
> 数组 1 1 3 3 3 3 元素的秩

**天真的方法:**

1.  数组的第一个元素将始终具有秩 1。

2.  迭代数组，如果元素在前几个元素中最大，那么它的排名是 1。

3.  如果元素不大于之前比较的元素。那么这个元素的等级将是它之前的更大元素的数量。
    例如，假设它大于 2 个先前的元素，那么它的等级是 3。

以下是上述方法的实现:

## C++

```
// C++ program to rank of all elements
// in a Stream in descending order
// when they arrive
#include <iostream>
using namespace std;

    // FindRank function to find rank
        void FindRank(int arr[], int length)
    {
        // Rank of first element is always 1
        cout << "1" <<  " ";

        // Iterate over array
        for (int i = 1; i < length; i++)
        {
            // As element let say its rank is 1
            int rank = 1;

            // Element is compared
            // with previous elements
            for (int j = 0; j < i; j++)
            {
                // If greater than previous
                // than rank is incremented
                if(arr[j] > arr[i])
                    rank++;

            }

            // print rank
            cout <<  rank  << " ";
        }
    }

// Driver code
int main() {

        // array named arr
        int arr[] = {88, 14, 69, 30, 29, 89};

        // length of arr
        int len = sizeof(arr)/sizeof(arr[0]);

        FindRank(arr, len);

    return 0;
}

// This code is contributed by AnkitRai01
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to rank of all elements
// in a Stream in descending order
// when they arrive
import java.util.*;

class GFG{

    // FindRank function to find rank
    static void FindRank(int arr[], int length)
    {
        // Rank of first element is always 1
        System.out.print("1" + " ");

        // Iterate over array
        for (int i = 1; i < arr.length; i++)
        {
            // As element let say its rank is 1
            int rank = 1;

            // Element is compared
            // with previous elements
            for (int j = 0; j < i; j++)
            {
                // If greater than previous
                // than rank is incremented
                if(arr[j] > arr[i])
                    rank++;

            }

            // print rank
            System.out.print(rank + " ");
        }
    }

    // Driver code
    public static void main(String args[]){

        // array named arr
        int arr[] = {88, 14, 69, 30, 29, 89};

        // length of arr
        int len = arr.length;

        FindRank(arr, len);
    }
}

// This code is contributed by AbhiThakur
```

## 蟒蛇 3

```
# Python program to rank of all elements
# in a Stream in descending order
# when they arrive

# FindRank function to find rank
def FindRank(arr, length):

    # Rank of first element is always 1
    print(1, end =" ")

    # Iterate over array
    for i in range(1, length):

        # As element let say its rank is 1
        rank = 1

        # Element is compared
        # with previous elements
        for j in range(0, i):

            # If greater than previous
            # than rank is incremented
            if(arr[j] > arr[i]):
                rank = rank + 1

        # print rank
        print(rank, end =" ")

# Driver code
if __name__ == '__main__':

    # array named arr
    arr = [88, 14, 69, 30, 29, 89]

    # length of arr
    length = len(arr)

    FindRank(arr, length)
```

## C#

```
// C# program to rank of all elements
// in a Stream in descending order
// when they arrive
using System;

class GFG{

    // FindRank function to find rank
    static void FindRank(int[] arr, int length)
    {
        // Rank of first element is always 1
        Console.Write("1" + " ");

        // Iterate over array
        for (int i = 1; i < arr.Length; i++)
        {
            // As element let say its rank is 1
            int rank = 1;

            // Element is compared
            // with previous elements
            for (int j = 0; j < i; j++)
            {
                // If greater than previous
                // than rank is incremented
                if(arr[j] > arr[i])
                    rank++;

            }

            // print rank
            Console.Write(rank + " ");
        }
    }

    // Driver code
    public static void Main(){

        // array named arr
        int[] arr = {88, 14, 69, 30, 29, 89};

        // length of arr
        int len = arr.Length;

        FindRank(arr, len);
    }
}

// This code is contributed by AbhiThakur
```

## java 描述语言

```
<script>
// javascript program to rank of all elements
// in a Stream in descending order
// when they arrive

    // FindRank function to find rank
    function FindRank(arr , length) {
        // Rank of first element is always 1
        document.write("1" + " ");

        // Iterate over array
        for (i = 1; i < arr.length; i++) {
            // As element let say its rank is 1
            var rank = 1;

            // Element is compared
            // with previous elements
            for (j = 0; j < i; j++) {
                // If greater than previous
                // than rank is incremented
                if (arr[j] > arr[i])
                    rank++;

            }

            // prvar rank
            document.write(rank + " ");
        }
    }

    // Driver code

        // array named arr
        var arr = [ 88, 14, 69, 30, 29, 89 ];

        // length of arr
        var len = arr.length;

        FindRank(arr, len);

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
1 2 2 3 4 1
```

***时间复杂度:** O(N <sup>2</sup> )* ，其中 N 为阵长。
***空间复杂度:** O(1)*
**高效方法:**思路是用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)来求数字的秩。它将给出大于给定数字的数字计数。
以下是上述方法的实施:

## 蟒蛇 3

```
# Python program to rank of all elements
# in a Stream in descending order
# when they arrive

# import of bisect to use bisect.insort()
import bisect

# FindRank function to find rank
def FindRank(arr, length):
    # rank list to store values of
    # array in ascending order
    rank = []

    first = arr[0]
    rank.append(first)
    # Rank of first element is always 1
    print(1, end =" ")

    # Iterate over remaining array
    for i in range(1, length):
        val = arr[i]

        # element inserted in the rank list
        # using the binary method

        bisect.insort(rank, val)

        # To find rank of that element

        # length of rank array - index of element
        # in rank array
        eleRank = len(rank)-rank.index(val)

        # print of rank of element of array
        print(eleRank, end =" ")

# Driver code
if __name__ == '__main__':

    # array named arr
    arr = [88, 14, 69, 30, 29, 89]

    # lenght of arr
    length = len(arr)

    FindRank(arr, length)
```

**Output:** 

```
1 2 2 3 4 1
```

***时间复杂度:** O(N * log N)，其中 N 为数组长度。*
***空间复杂度:** O(N)*