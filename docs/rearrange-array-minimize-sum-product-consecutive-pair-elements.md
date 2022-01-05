# 重新排列一个数组，以最小化连续对元素的乘积之和

> 原文:[https://www . geeksforgeeks . org/rearray-array-minimum-sum-product-continuous-pair-elements/](https://www.geeksforgeeks.org/rearrange-array-minimize-sum-product-consecutive-pair-elements/)

给我们一个偶数大小的数组，我们必须对数组进行排序，使得交替元素的乘积之和最小，我们还必须找到最小和。
**例:**

```
Input : arr[] = {9, 2, 8, 4, 5, 7, 6, 0}
Output : Minimum sum of the product of 
         consecutive pair elements: 74
         Sorted arr[] for minimum sum: 
         {9, 0, 8, 2, 7, 4, 6, 5}
Explanation : We get 74 using below
calculation in rearranged array.
9*0 + 8*2 + 7*4 + 6*5 = 74

Input : arr[] = {1, 2, 1, 4, 0, 5, 6, 0}
Output : Minimum sum of the product of 
         consecutive pair elements: 6
         Sorted arr[] for minimum sum: 
         {6, 0, 5, 0, 4, 1, 2, 1}
Explanation : We get 6 using below:
6*0 + 5*0 + 4*1 + 2*1 = 6
```

这个问题是[的一个变种，在允许排列的情况下最小化两个数组的乘积之和](https://www.geeksforgeeks.org/minimize-sum-product-two-arrays-permutations-allowed/)。
为了重新排列数组，使得我们应该得到的连续元素对的乘积之和最小，我们应该让所有偶数索引元素以递减的顺序排列，奇数索引元素以递增的顺序排列，所有 n/2 个最大元素作为偶数索引，接下来的 n/2 个元素作为奇数索引，反之亦然。
现在，我们的想法很简单，我们应该对主数组进行排序，并进一步分别创建两个辅助数组 evenArr[]和 oddArr[]。我们遍历输入数组，在 evenArr[]中放置 n/2 个最大元素，在 oddArr[]中放置下一个 n/2 个元素。然后我们按照降序对 evenArr[]进行排序，按照升序对 oddArr[]进行排序。最后，逐元素复制 evenArr[]和 oddArr[]以获得所需的结果，并且应该计算出所需的最小和。
以下是上述方法的实施:

## C++

```
// C++ program to sort an array such that
// sum of product of alternate element
// is minimum.
#include <bits/stdc++.h>
using namespace std;

int minSum(int arr[], int n)
{
    // create evenArr[] and oddArr[]
    vector<int> evenArr;
    vector<int> oddArr;

    // sort main array in ascending order
    sort(arr, arr+n );

    // Put elements in oddArr[] and evenArr[]
    // as per desired value.
    for (int i = 0; i < n; i++)
    {
        if (i < n/2)
            oddArr.push_back(arr[i]);
        else
            evenArr.push_back(arr[i]);
    }

    // sort evenArr[] in descending order
    sort(evenArr.begin(), evenArr.end(), greater<int>());

    // merge both sub-array and
    // calculate minimum sum of
    // product of alternate elements
    int i = 0, sum = 0;
    for (int j=0; j<evenArr.size(); j++)
    {
        arr[i++] = evenArr[j];
        arr[i++] = oddArr[j];
        sum += evenArr[j] * oddArr[j];
    }

    return sum;
}

// Driver Program
int main()
{
    int arr[] = { 1, 5, 8, 9, 6, 7, 3, 4, 2, 0 };
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << "Minimum required sum = " << minSum(arr, n);
    cout << "\nSorted array in required format : ";
    for (int i=0; i<n; i++)
       cout << arr[i] << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort an array such that
// sum of product of alternate element
// is minimum.

import java.util.Arrays;
import java.util.Collections;
import java.util.Comparator;
import java.util.Vector;

class GFG {

    static int minSum(int arr[], int n) {
        // create evenArr[] and oddArr[]
        Vector<Integer> evenArr = new Vector<>();
        Vector<Integer> oddArr = new Vector<>();

        // sort main array in ascending order
        Arrays.sort(arr);

        // Put elements in oddArr[] and evenArr[]
        // as per desired value.
        for (int i = 0; i < n; i++) {
            if (i < n / 2) {
                oddArr.add(arr[i]);
            } else {
                evenArr.add(arr[i]);
            }
        }

        // sort evenArr[] in descending order
        Comparator comparator = Collections.reverseOrder();
        Collections.sort(evenArr,comparator);

        // merge both sub-array and
        // calculate minimum sum of
        // product of alternate elements
        int i = 0, sum = 0;
        for (int j = 0; j < evenArr.size(); j++) {
            arr[i++] = evenArr.get(j);
            arr[i++] = oddArr.get(j);
            sum += evenArr.get(j) * oddArr.get(j);
        }

        return sum;
    }

// Driver program
    public static void main(String[] args) {

        int arr[] = {1, 5, 8, 9, 6, 7, 3, 4, 2, 0};
        int n = arr.length;
        System.out.println("Minimum required sum = "
                                  + minSum(arr, n));
        System.out.println("Sorted array in required format : ");
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }

    }

}
```

## 蟒蛇 3

```
# Python 3 program to sort an array such
# that sum of product of alternate element
# is minimum.
def minSum(arr, n):

    # create evenArr[] and oddArr[]
    evenArr = []
    oddArr = []

    # sort main array in ascending order
    arr.sort()

    # Put elements in oddArr[] and
    # evenArr[] as per desired value.
    for i in range(n):

        if (i < n // 2):
            oddArr.append(arr[i])
        else:
            evenArr.append(arr[i])

    # sort evenArr[] in descending order
    evenArr.sort(reverse = True)

    # merge both sub-array and
    # calculate minimum sum of
    # product of alternate elements
    i = 0
    sum = 0
    for j in range(len(evenArr)):
        arr[i] = evenArr[j]
        i += 1
        arr[i] = oddArr[j]
        i += 1
        sum += evenArr[j] * oddArr[j]

    return sum

# Driver Code
if __name__ == "__main__":

    arr = [ 1, 5, 8, 9, 6, 7, 3, 4, 2, 0 ]
    n = len(arr)
    print( "Minimum required sum =",
                      minSum(arr, n))
    print("Sorted array in required format : ",
                                      end = "")
    for i in range(n):
        print(arr[i], end = " ")

# This code is contributed by ita_c
```

## C#

```
// Program to sort an array such that
// sum of product of alternate element
// is minimum.
using System;
using System.Collections.Generic;

class GFG
{
static int minSum(int []arr, int n)
{
    // create evenArr[] and oddArr[]
    List<int> evenArr = new List<int>();
    List<int> oddArr = new List<int>();
    int i;

    // sort main array in ascending order
    Array.Sort(arr);

    // Put elements in oddArr[] and
    // evenArr[] as per desired value.
    for (i = 0; i < n; i++)
    {
        if (i < n / 2)
        {
            oddArr.Add(arr[i]);
        }
        else
        {
            evenArr.Add(arr[i]);
        }
    }

    // sort evenArr[] in descending order
    evenArr.Sort();
    evenArr.Reverse();

    // merge both sub-array and
    // calculate minimum sum of
    // product of alternate elements
    int k = 0, sum = 0;
    for (int j = 0; j < evenArr.Count; j++)
    {
        arr[k++] = evenArr[j];
        arr[k++] = oddArr[j];
        sum += evenArr[j] * oddArr[j];
    }

    return sum;
}

// Driver Code
public static void Main()
{
    int []arr = {1, 5, 8, 9, 6,
                 7, 3, 4, 2, 0};
    int n = arr.Length;
    Console.WriteLine("Minimum required sum = " +
                                 minSum(arr, n));
    Console.WriteLine("Sorted array in " +
                    "required format : ");
    for (int i = 0; i < n; i++)
    {
        Console.Write(arr[i] + " ");
    }
}
}

// This code contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to sort an array such that
// sum of product of alternate element
// is minimum.

    function minSum(arr,n)
    {
        // create evenArr[] and oddArr[]
        let evenArr =[];
        let oddArr = [];

        // sort main array in ascending order
        arr.sort(function(a,b){return a-b;});

        // Put elements in oddArr[] and evenArr[]
        // as per desired value.
        for (let i = 0; i < n; i++) {
            if (i < Math.floor(n / 2)) {
                oddArr.push(arr[i]);
            } else {
                evenArr.push(arr[i]);
            }
        }

        // sort evenArr[] in descending order
        evenArr.sort(function(a,b){return b-a;});

        // merge both sub-array and
        // calculate minimum sum of
        // product of alternate elements
        let i = 0, sum = 0;
        for (let j = 0; j < evenArr.length; j++) {
            arr[i++] = evenArr[j];
            arr[i++] = oddArr[j];
            sum += evenArr[j] * oddArr[j];
        }

        return sum;
    }

    // Driver program
    let arr=[1, 5, 8, 9, 6, 7, 3, 4, 2, 0];
    let n = arr.length;
    document.write("Minimum required sum = "
                                  + minSum(arr, n)+"<br>");

    document.write("Sorted array in required format : ");
    for (let i = 0; i < n; i++) {
        document.write(arr[i] + " ");
    }

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
Minimum required sum = 60
Sorted array in required format : 9 0 8 1 7 2 6 3 5 4 
```

本文由[**Shivam Pradhan(anuj _ charm)**](https://www.facebook.com/anuj.charm)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。