# 按递增顺序排列偶数元素，按递减顺序排列奇数元素

> 原文:[https://www . geesforgeks . org/sort-偶数-放置-元素-递增-奇数-放置-递减-顺序/](https://www.geeksforgeeks.org/sort-even-placed-elements-increasing-odd-placed-decreasing-order/)

给我们一个 n 个不同数字的数组。任务是将所有偶数按递增顺序排序，奇数按递减顺序排序。修改后的数组应该包含所有已排序的偶数，后跟反向排序的奇数。
注意，第一个元素由于其索引 0 而被认为是偶数。

**示例:**

```
Input:  arr[] = {0, 1, 2, 3, 4, 5, 6, 7}
Output: arr[] = {0, 2, 4, 6, 7, 5, 3, 1}
Even-place elements : 0, 2, 4, 6
Odd-place elements : 1, 3, 5, 7
Even-place elements in increasing order : 
0, 2, 4, 6
Odd-Place elements in decreasing order : 
7, 5, 3, 1

Input: arr[] = {3, 1, 2, 4, 5, 9, 13, 14, 12}
Output: {2, 3, 5, 12, 13, 14, 9, 4, 1}
Even-place elements : 3, 2, 5, 13, 12
Odd-place elements : 1, 4, 9, 14
Even-place elements in increasing order : 
2, 3, 5, 12, 13
Odd-Place elements in decreasing order : 
14, 9, 4, 1 
```

想法很简单。我们分别创建了两个辅助数组 evenArr[]和 oddArr[]。我们遍历输入数组，将所有偶数位置的元素放在 evenArr[]中，将奇数位置的元素放在 oddArr[]中。然后我们按照升序对 evenArr[]进行排序，按照降序对 oddArr[]进行排序。最后，复制 evenArr[]和 oddArr[]以获得所需的结果。

## C++

```
// Program to separately sort even-placed and odd
// placed numbers and place them together in sorted
// array.
#include <bits/stdc++.h>
using namespace std;

void bitonicGenerator(int arr[], int n)
{
    // create evenArr[] and oddArr[]
    vector<int> evenArr;
    vector<int> oddArr;

    // Put elements in oddArr[] and evenArr[] as
    // per their position
    for (int i = 0; i < n; i++) {
        if (!(i % 2))
            evenArr.push_back(arr[i]);
        else
            oddArr.push_back(arr[i]);
    }

    // sort evenArr[] in ascending order
    // sort oddArr[] in descending order
    sort(evenArr.begin(), evenArr.end());
    sort(oddArr.begin(), oddArr.end(), greater<int>());

    int i = 0;
    for (int j = 0; j < evenArr.size(); j++)
        arr[i++] = evenArr[j];
    for (int j = 0; j < oddArr.size(); j++)
        arr[i++] = oddArr[j];
}

// Driver Program
int main()
{
    int arr[] = { 1, 5, 8, 9, 6, 7, 3, 4, 2, 0 };
    int n = sizeof(arr) / sizeof(arr[0]);
    bitonicGenerator(arr, n);
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to separately sort
// even-placed and odd placed numbers
// and place them together in sorted
// array.
import java.util.*;

class GFG {

    static void bitonicGenerator(int arr[], int n)
    {
        // create evenArr[] and oddArr[]
        Vector<Integer> evenArr = new Vector<Integer>();
        Vector<Integer> oddArr = new Vector<Integer>();

        // Put elements in oddArr[] and evenArr[] as
        // per their position
        for (int i = 0; i < n; i++) {
            if (i % 2 != 1) {
                evenArr.add(arr[i]);
            }
            else {
                oddArr.add(arr[i]);
            }
        }

        // sort evenArr[] in ascending order
        // sort oddArr[] in descending order
        Collections.sort(evenArr);
        Collections.sort(oddArr, Collections.reverseOrder());

        int i = 0;
        for (int j = 0; j < evenArr.size(); j++) {
            arr[i++] = evenArr.get(j);
        }
        for (int j = 0; j < oddArr.size(); j++) {
            arr[i++] = oddArr.get(j);
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 5, 8, 9, 6, 7, 3, 4, 2, 0 };
        int n = arr.length;
        bitonicGenerator(arr, n);
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 program to separately sort
# even-placed and odd placed numbers
# and place them together in sorted array.
def bitonicGenerator(arr, n):

    # create evenArr[] and oddArr[]
    evenArr = []
    oddArr = []

    # Put elements in oddArr[] and evenArr[]
    # as per their position
    for i in range(n):
        if ((i % 2) == 0):
            evenArr.append(arr[i])
        else:
            oddArr.append(arr[i])

    # sort evenArr[] in ascending order
    # sort oddArr[] in descending order
    evenArr = sorted(evenArr)
    oddArr = sorted(oddArr)
    oddArr = oddArr[::-1]

    i = 0
    for j in range(len(evenArr)):
        arr[i] = evenArr[j]
        i += 1
    for j in range(len(oddArr)):
        arr[i] = oddArr[j]
        i += 1

# Driver Code
arr = [1, 5, 8, 9, 6, 7, 3, 4, 2, 0]
n = len(arr)
bitonicGenerator(arr, n)
for i in arr:
    print(i, end = " ")

# This code is contributed by Mohit Kumar
```

## C#

```
// C# Program to separately sort
// even-placed and odd placed numbers
// and place them together in sorted
// array.
using System;
using System.Collections.Generic;

class GFG
{

    static void bitonicGenerator(int []arr, int n)
    {
        // create evenArr[] and oddArr[]
        List<int> evenArr = new List<int>();
        List<int> oddArr = new List<int>();
        int i = 0;

        // Put elements in oddArr[] and evenArr[] as
        // per their position
        for (i = 0; i < n; i++)
        {
            if (i % 2 != 1)
            {
                evenArr.Add(arr[i]);
            }
            else
            {
                oddArr.Add(arr[i]);
            }
        }

        // sort evenArr[] in ascending order
        // sort oddArr[] in descending order
        evenArr.Sort();
        oddArr.Sort();
        oddArr.Reverse();

        i = 0;
        for (int j = 0; j < evenArr.Count; j++)
        {
            arr[i++] = evenArr[j];
        }
        for (int j = 0; j < oddArr.Count; j++)
        {
            arr[i++] = oddArr[j];
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = { 1, 5, 8, 9, 6, 7, 3, 4, 2, 0 };
        int n = arr.Length;
        bitonicGenerator(arr, n);
        for (int i = 0; i < n; i++)
        {
            Console.Write(arr[i] + " ");
        }
    }
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript Program to separately sort
// even-placed and odd placed numbers
// and place them together in sorted
// array.

    function bitonicGenerator(arr,n)
    {
        // create evenArr[] and oddArr[]
        let evenArr = [];
        let oddArr = [];

        // Put elements in oddArr[] and evenArr[] as
        // per their position
        for (let i = 0; i < n; i++) {
            if (i % 2 != 1) {
                evenArr.push(arr[i]);
            }
            else {
                oddArr.push(arr[i]);
            }
        }

        // sort evenArr[] in ascending order
        // sort oddArr[] in descending order
        evenArr.sort(function(a,b){return a-b;});
        oddArr.sort(function(a,b){return b-a;});

        let i = 0;
        for (let j = 0; j < evenArr.length; j++) {
            arr[i++] = evenArr[j];
        }
        for (let j = 0; j < oddArr.length; j++) {
            arr[i++] = oddArr[j];
        }
    }

     // Driver code
    let arr=[1, 5, 8, 9, 6, 7, 3, 4, 2, 0 ];
    let  n = arr.length;
    bitonicGenerator(arr, n);
    for (let i = 0; i < n; i++) {
        document.write(arr[i] + " ");
    }

    // This code is contributed by unknown2108
</script>
```

**输出:**

```
1 2 3 6 8 9 7 5 4 0
```

**时间复杂度:**O(n Log n)
T3】空间复杂度: O(n)

上述问题也可以在不使用辅助空间的情况下解决。其思想是将前半个奇数索引位置与后半个偶数索引位置交换，然后按升序对前半个数组进行排序，按降序对后半个数组进行排序。感谢 **SWARUPANANDA DHUA** 提出这个建议。

## C++

```
// Program to sort even-placed elements in increasing and
// odd-placed in decreasing order with constant space complexity

#include <bits/stdc++.h>
using namespace std;

void bitonicGenerator(int arr[], int n)
{
    // first odd index
    int i = 1;

    // last index
    int j = n - 1;

    // if last index is odd
    if (j % 2 != 0)
        // decrement j to even index
        j--;

    // swapping till half of array
    while (i < j) {
        swap(arr[i], arr[j]);
        i += 2;
        j -= 2;
    }

    // Sort first half in increasing
    sort(arr, arr + (n + 1) / 2);

    // Sort second half in decreasing
    sort(arr + (n + 1) / 2, arr + n, greater<int>());
}

// Driver Program
int main()
{
    int arr[] = { 1, 5, 8, 9, 6, 7, 3, 4, 2, 0 };
    int n = sizeof(arr) / sizeof(arr[0]);
    bitonicGenerator(arr, n);
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    return 0;
}
// This code is contributed by SWARUPANANDA DHUA
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to sort even-placed elements in increasing and
// odd-placed in decreasing order with constant space complexity
import java.util.Arrays;
class GFG {

    static void bitonicGenerator(int arr[], int n)
    {
        // first odd index
        int i = 1;

        // last index
        int j = n - 1;

        // if last index is odd
        if (j % 2 != 0)
            // decrement j to even index
            j--;

        // swapping till half of array
        while (i < j) {
            arr = swap(arr, i, j);
            i += 2;
            j -= 2;
        }

        // Sort first half in increasing
        Arrays.sort(arr, 0, (n + 1) / 2);

        // Sort second half in decreasing
        Arrays.sort(arr, (n + 1) / 2, n);
        int low = (n + 1) / 2, high = n - 1;
        // Reverse the second half
        while (low < high) {
            Integer temp = arr[low];
            arr[low] = arr[high];
            arr[high] = temp;
            low++;
            high--;
        }
    }
    static int[] swap(int[] arr, int i, int j)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
        return arr;
    }
    // Driver Program
    public static void main(String[] args)
    {
        int arr[] = { 1, 5, 8, 9, 6, 7, 3, 4, 2, 0 };
        int n = arr.length;
        bitonicGenerator(arr, n);
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
    }
}
// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 Program to sort even-placed elements in increasing and
# odd-placed in decreasing order with constant space complexity
def bitonicGenerator(arr, n):

    # first odd index
    i = 1

    # last index
    j = n - 1

    # if last index is odd
    if (j % 2 != 0):

        # decrement j to even index
        j = j - 1

    # swapping till half of array
    while (i < j) :
        arr[j], arr[i] = arr[i], arr[j]
        i = i + 2
        j = j - 2

    arr_f = []
    arr_s = []

    for i in range(int((n + 1) / 2)) :
        arr_f.append(arr[i])

    i = int((n + 1) / 2)
    while( i < n ) :
        arr_s.append(arr[i])
        i = i + 1

    # Sort first half in increasing
    arr_f.sort()

    # Sort second half in decreasing
    arr_s.sort(reverse = True)

    for i in arr_s:
        arr_f.append(i)

    return arr_f

# Driver Program
arr = [ 1, 5, 8, 9, 6, 7, 3, 4, 2, 0]
n = len(arr)
arr = bitonicGenerator(arr, n)
print(arr)

# This code is contributed by Arnab Kundu
```

## C#

```
// Program to sort even-placed elements in
// increasing and odd-placed in decreasing order
// with constant space complexity
using System;

class GFG
{
    static void bitonicGenerator(int []arr, int n)
    {
        // first odd index
        int i = 1;

        // last index
        int j = n - 1;

        // if last index is odd
        if (j % 2 != 0)

            // decrement j to even index
            j--;

        // swapping till half of array
        while (i < j)
        {
            arr = swap(arr, i, j);
            i += 2;
            j -= 2;
        }

        // Sort first half in increasing
        Array.Sort(arr, 0, (n + 1) / 2);

        // Sort second half in decreasing
        Array.Sort(arr, (n + 1) / 2,
                   n - ((n + 1) / 2));
        int low = (n + 1) / 2, high = n - 1;

        // Reverse the second half
        while (low < high)
        {
            int temp = arr[low];
            arr[low] = arr[high];
            arr[high] = temp;
            low++;
            high--;
        }
    }

    static int[] swap(int[] arr, int i, int j)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
        return arr;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int []arr = { 1, 5, 8, 9, 6, 7, 3, 4, 2, 0 };
        int n = arr.Length;
        bitonicGenerator(arr, n);
        for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Program to sort even-placed elements in increasing and
// odd-placed in decreasing order with constant space complexity
function bitonicGenerator(arr, n)
{

    // first odd index
        let i = 1;

        // last index
        let j = n - 1;

        // if last index is odd
        if (j % 2 != 0)
            // decrement j to even index
            j--;

        // swapping till half of array
        while (i < j) {
            arr = swap(arr, i, j);
            i += 2;
            j -= 2;
        }

        // Sort first half in increasing
        // Sort second half in decreasing
        let temp1 = arr.slice(0,Math.floor((n+1)/2)).sort(function(a,b){return a-b;});
        let temp2 = arr.slice(Math.floor((n+1)/2),n).sort(function(a,b){return b-a;});
        arr = temp1.concat(temp2);

        return arr;
}

function swap(arr, i, j)
{
    let temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
        return arr;
}

// Driver Program
let arr = [1, 5, 8, 9, 6, 7, 3, 4, 2, 0 ];
let n = arr.length;
arr = bitonicGenerator(arr, n);
document.write(arr.join(" "));

// This code is contributed by rag2127
</script>
```

**输出:**

```
1 2 3 6 8 9 7 5 4 0
```

**时间复杂度:**O(n Log n)
T3】空间复杂度: O(1)

本文由[**Shivam Pradhan(anuj _ charm)**](https://www.facebook.com/anuj.charm)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。