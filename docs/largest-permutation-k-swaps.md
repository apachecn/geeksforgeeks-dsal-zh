# 最多 k 次互换后的最大排列

> 原文:[https://www.geeksforgeeks.org/largest-permutation-k-swaps/](https://www.geeksforgeeks.org/largest-permutation-k-swaps/)

给定作为数组的第一个 **n 个**自然数和一个整数 **k 个**的排列。最多交换 **k** 次后，打印字典上最大的排列

**示例:**

```
Input: arr[] = {4, 5, 2, 1, 3}
       k = 3
Output: 5 4 3 2 1
Swap 1st and 2nd elements: 5 4 2 1 3 
Swap 3rd and 5th elements: 5 4 3 1 2 
Swap 4th and 5th elements: 5 4 3 2 1 

Input: arr[] = {2, 1, 3}
       k = 1
Output: 3 1 2
Swap 1st and 3re elements: 3 1 2
```

**<u>天真方法</u> :** 想法是按照字典顺序递减的顺序生成一个个排列。将每个生成的排列与原始数组进行比较，[计算转换](https://www.geeksforgeeks.org/minimum-swaps-to-make-two-array-identical/)所需的交换次数。如果计数小于或等于 k，打印此排列。这种方法的问题是很难实现，并且肯定会因为 n 的大值而超时

**算法:**

1.  要找到将一个数组转换为另一个数组的最小交换，请阅读[这篇](https://www.geeksforgeeks.org/minimum-swaps-to-make-two-array-identical/)文章。
2.  复制原始数组，并按降序对该数组进行排序。所以排序后的数组是原始数组的最大排列。
3.  现在按照字典顺序递减顺序生成所有排列。使用*prev _ 置换()*函数计算前一次置换。
4.  如果计数小于或等于 k，找出将新数组(按降序排列)转换为原始数组所需的最小步骤。然后打印数组并中断。

## C++14

```
#include <bits/stdc++.h>
using namespace std;

// Function returns the minimum number
// of swaps required to sort the array
// This method is taken from below post
// https:// www.geeksforgeeks.org/
// minimum-number-swaps-required-sort-array/
int minSwapsToSort(int arr[], int n)
{
    // Create an array of pairs where first
    // element is array element and second
    // element is position of first element
    pair<int, int> arrPos[n];
    for (int i = 0; i < n; i++) {
        arrPos[i].first = arr[i];
        arrPos[i].second = i;
    }

    // Sort the array by array element
    // values to get right position of
    // every element as second
    // element of pair.
    sort(arrPos, arrPos + n);

    // To keep track of visited elements.
    // Initialize all elements as not
    // visited or false.
    vector<bool> vis(n, false);

    // Initialize result
    int ans = 0;

    // Traverse array elements
    for (int i = 0; i < n; i++) {
        // Already swapped and corrected or
        // already present at correct pos
        if (vis[i] || arrPos[i].second == i)
            continue;

        // Find out the number of  node in
        // this cycle and add in ans
        int cycle_size = 0;
        int j = i;
        while (!vis[j]) {
            vis[j] = 1;

            // move to next node
            j = arrPos[j].second;
            cycle_size++;
        }

        // Update answer by adding current
        // cycle.
        ans += (cycle_size - 1);
    }

    // Return result
    return ans;
}

// method returns minimum number of
// swap to make array B same as array A
int minSwapToMakeArraySame(
    int a[], int b[], int n)
{
    // Map to store position of elements
    // in array B we basically store
    // element to index mapping.
    map<int, int> mp;
    for (int i = 0; i < n; i++)
        mp[b[i]] = i;

    // now we're storing position of array
    // A elements in array B.
    for (int i = 0; i < n; i++)
        b[i] = mp[a[i]];

    /* We can uncomment this section to
      print modified b array
    for (int i = 0; i < N; i++)
        cout << b[i] << " ";
    cout << endl; */

    // Returning minimum swap for sorting
    // in modified array B as final answer
    return minSwapsToSort(b, n);
}

// Function to calculate largest
// permutation after atmost K swaps
void KswapPermutation(
    int arr[], int n, int k)
{
    int a[n];

    // copy the array
    for (int i = 0; i < n; i++)
        a[i] = arr[i];

    // Sort the array in descending order
    sort(arr, arr + n, greater<int>());

    // generate permutation in lexicographically
    // decreasing order.
    do {
        // copy the array
        int a1[n], b1[n];
        for (int i = 0; i < n; i++) {
            a1[i] = arr[i];
            b1[i] = a[i];
        }

        // Check if it can be made same in k steps
        if (
            minSwapToMakeArraySame(
                a1, b1, n)
            <= k) {
            // Print the array
            for (int i = 0; i < n; i++)
                cout << arr[i] << " ";
            break;
        }

        // move to previous permutation
    } while (prev_permutation(arr, arr + n));
}

int main()
{
    int arr[] = { 4, 5, 2, 1, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 3;

    cout << "Largest permutation after "
         << k << " swaps:\n";

    KswapPermutation(arr, n, k);
    return 0;
}
```

**Output**

```
Largest permutation after 3 swaps:
5 4 3 2 1 
```

**复杂度分析:**

*   **时间复杂度:** O(N！).
    生成所有排列 O(N！)需要时间复杂度。
*   **空间复杂度:** O(n)。
    存储新数组需要 O(n)空间。

**<u>另一个值得考虑的做法:</u>**

这个问题可以看作是“受控”选择排序的一个实例。我们所说的受控，是指我们不对整个数组执行选择排序操作。相反，我们将自己构建为只允许我们执行的交换总数 K。

所以在下面的方法中，我们所需要做的就是让选择排序进行 k 次，不能超过 k 次。此外，我们需要检查我们将要与当前位置 I 交换的最大数字的位置是否等于该位置已经存在的数字，我们需要跳过这种特殊情况，以免浪费我们有限的交换次数。

## C++14

```
#include <bits/stdc++.h>
using namespace std;
void KswapPermutation(
    int arr[], int n, int k)
{
    for(int i=0;i<n-1;i++)
    {
        if( k>0)
        {
            int max = i;
            for(int j=i+1;j<n;j++)
            if(arr[j]>arr[max])
            max = j;

          // this condition checks whether the max value has changed since when
          // we started , or is it the same.
          // We need to ignore the swap if the value is same.
          // It means that the number ought to be present at the ith position , is already
          // there.
            if(max!=i)
            {
            int temp = arr[max];
            arr[max] = arr[i];
            arr[i] = temp;
            k--;
            }
        }
        else
        break;
    }
}

// Driver code
int main()
{
    int arr[] = { 4, 5, 2, 1, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 3;
    KswapPermutation(arr, n, k);
    cout << "Largest permutation after "
         << k << " swaps:"<<endl;
    for (int i = 0; i < n; ++i)
        cout<<arr[i]<<" ";
    return 0;
}
```

**Output**

```
Largest permutation after 3 swaps:
5 4 3 2 1 
```

**复杂度分析**:

*   **时间复杂度** : O(n^2)，因为这种方法利用了选择排序
*   **空间复杂度** : O(1)，因为排序已经到位，不需要额外的空间

**<u>高效进场</u> :** 这是贪婪进场。当最大的元素在数组的前面时，找到最大的排列，即最大的元素按降序排列。最多有 k 个互换，因此将第 1 个 <sup>st</sup> 、第 2 个 <sup>nd</sup> 、第 3 个 <sup>rd</sup> 、…、k <sup>th</sup> 最大的元素放在各自的位置。

**注意:**如果允许的交换次数等于数组的大小，那么就不需要迭代整个数组。答案只是反向排序的数组。

**算法:**

1.  创建一个 HashMap 或长度为 n 的数组来存储元素-索引对或将元素映射到它的索引。
2.  现在运行 k 次循环。
3.  在每次迭代中，用元素 n–I 交换 ith 元素，其中 I 是循环的索引或计数。也交换他们的位置，即更新散列表或数组。因此在这一步中，剩余元素中最大的元素被交换到前面。
4.  打印输出数组。

**实现 1:** 这使用简单的数组来得出解决方案。

## C++

```
// Below is C++ code to print largest
// permutation after at most K swaps
#include <bits/stdc++.h>
using namespace std;

// Function to calculate largest
// permutation after atmost K swaps
void KswapPermutation(
    int arr[], int n, int k)
{
    // Auxiliary dictionary of
    // storing the position of elements
    int pos[n + 1];

    for (int i = 0; i < n; ++i)
        pos[arr[i]] = i;

    for (int i = 0; i < n && k; ++i) {
        // If element is already i'th largest,
        // then no need to swap
        if (arr[i] == n - i)
            continue;

        // Find position of i'th
        // largest value, n-i
        int temp = pos[n - i];

        // Swap the elements position
        pos[arr[i]] = pos[n - i];
        pos[n - i] = i;

        // Swap the ith largest value with the
        // current value at ith place
        swap(arr[temp], arr[i]);

        // decrement number of swaps
        --k;
    }
}

// Driver code
int main()
{
    int arr[] = { 4, 5, 2, 1, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 3;

    KswapPermutation(arr, n, k);
    cout << "Largest permutation after "
         << k << " swaps:n";
    for (int i = 0; i < n; ++i)
        printf("%d ", arr[i]);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Below is Java code to print
// largest permutation after
// atmost K swaps
class GFG {

    // Function to calculate largest
    // permutation after atmost K swaps
    static void KswapPermutation(
        int arr[], int n, int k)
    {

        // Auxiliary dictionary of storing
        // the position of elements
        int pos[] = new int[n + 1];

        for (int i = 0; i < n; ++i)
            pos[arr[i]] = i;

        for (int i = 0; i < n && k > 0; ++i) {

            // If element is already i'th
            // largest, then no need to swap
            if (arr[i] == n - i)
                continue;

            // Find position of i'th largest
            // value, n-i
            int temp = pos[n - i];

            // Swap the elements position
            pos[arr[i]] = pos[n - i];
            pos[n - i] = i;

            // Swap the ith largest value with the
            // current value at ith place
            int tmp1 = arr[temp];
            arr[temp] = arr[i];
            arr[i] = tmp1;

            // decrement number of swaps
            --k;
        }
    }

    // Driver method
    public static void main(String[] args)
    {

        int arr[] = { 4, 5, 2, 1, 3 };
        int n = arr.length;
        int k = 3;

        KswapPermutation(arr, n, k);

        System.out.print(
            "Largest permutation "
            + "after " + k + " swaps:\n");

        for (int i = 0; i < n; ++i)
            System.out.print(arr[i] + " ");
    }
}

// This code is contributed by Anant Agarwal.
```

## 计算机编程语言

```
# Python code to print largest permutation after K swaps

def KswapPermutation(arr, n, k):

    # Auxiliary array of storing the position of elements
    pos = {}
    for i in range(n):
        pos[arr[i]] = i

    for i in range(n):

        # If K is exhausted then break the loop
        if k == 0:
            break

        # If element is already largest then no need to swap
        if (arr[i] == n-i):
            continue

        # Find position of i'th largest value, n-i
        temp = pos[n-i]

        # Swap the elements position
        pos[arr[i]] = pos[n-i]
        pos[n-i] = i

        # Swap the ith largest value with the value at
        # ith place
        arr[temp], arr[i] = arr[i], arr[temp]

        # Decrement K after swap
        k = k-1

# Driver code
arr = [4, 5, 2, 1, 3]
n = len(arr)
k = 3
KswapPermutation(arr, N, K)

# Print the answer
print "Largest permutation after", K, "swaps: "
print " ".join(map(str, arr))
```

## C#

```
// Below is C# code to print largest
// permutation after atmost K swaps.
using System;

class GFG {

    // Function to calculate largest
    // permutation after atmost K
    // swaps
    static void KswapPermutation(int[] arr,
                                 int n, int k)
    {

        // Auxiliary dictionary of storing
        // the position of elements
        int[] pos = new int[n + 1];

        for (int i = 0; i < n; ++i)
            pos[arr[i]] = i;

        for (int i = 0; i < n && k > 0; ++i) {

            // If element is already i'th
            // largest, then no need to swap
            if (arr[i] == n - i)
                continue;

            // Find position of i'th largest
            // value, n-i
            int temp = pos[n - i];

            // Swap the elements position
            pos[arr[i]] = pos[n - i];
            pos[n - i] = i;

            // Swap the ith largest value with
            // the current value at ith place
            int tmp1 = arr[temp];
            arr[temp] = arr[i];
            arr[i] = tmp1;

            // decrement number of swaps
            --k;
        }
    }

    // Driver method
    public static void Main()
    {

        int[] arr = { 4, 5, 2, 1, 3 };
        int n = arr.Length;
        int k = 3;

        KswapPermutation(arr, n, k);

        Console.Write("Largest permutation "
                      + "after " + k + " swaps:\n");

        for (int i = 0; i < n; ++i)
            Console.Write(arr[i] + " ");
    }
}

// This code is contributed nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to print largest permutation
// after atmost K swaps

// Function to calculate largest
// permutation after atmost K swaps
function KswapPermutation(&$arr, $n, $k)
{

    for ($i = 0; $i < $n; ++$i)
        $pos[$arr[$i]] = $i;

    for ($i = 0; $i < $n && $k; ++$i)
    {
        // If element is already i'th largest,
        // then no need to swap
        if ($arr[$i] == $n - $i)
            continue;

        // Find position of i'th largest
        // value, n-i
        $temp = $pos[$n - $i];

        // Swap the elements position
        $pos[$arr[$i]] = $pos[$n - $i];
        $pos[$n - $i] = $i;

        // Swap the ith largest value with the
        // current value at ith place
        $t = $arr[$temp];
        $arr[$temp] = $arr[$i];
        $arr[$i] = $t;

        // decrement number of swaps
        --$k;
    }
}

// Driver code
$arr = array(4, 5, 2, 1, 3);
$n = sizeof($arr);
$k = 3;

KswapPermutation($arr, $n, $k);
echo ("Largest permutation after ");
echo ($k);
echo (" swaps:\n");
for ($i = 0; $i < $n; ++$i)
{
    echo ($arr[$i] );
    echo (" ");
}

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

    // Below is Javascript code to print largest
    // permutation after at most K swaps

    // Function to calculate largest
    // permutation after atmost K swaps
    function KswapPermutation(arr, n, k)
    {
        // Auxiliary dictionary of
        // storing the position of elements
        let pos = new Array(n + 1);

        for (let i = 0; i < n; ++i)
            pos[arr[i]] = i;

        for (let i = 0; i < n && k; ++i) {
            // If element is already i'th largest,
            // then no need to swap
            if (arr[i] == n - i)
                continue;

            // Find position of i'th
            // largest value, n-i
            let temp = pos[n - i];

            // Swap the elements position
            pos[arr[i]] = pos[n - i];
            pos[n - i] = i;

            // Swap the ith largest value with the
            // current value at ith place
            let tmp1 = arr[temp];
            arr[temp] = arr[i];
            arr[i] = tmp1;

            // decrement number of swaps
            --k;
        }
    }

     let arr = [ 4, 5, 2, 1, 3 ];
    let n = arr.length;
    let k = 3;

    KswapPermutation(arr, n, k);
    document.write("Largest permutation after " + k + " swaps:" + "</br>");
    for (let i = 0; i < n; ++i)
        document.write(arr[i] + " ");

</script>
```

**Output**

```
Largest permutation after 3 swaps:n5 4 3 2 1 
```

**输出:**

```
Largest permutation after 3 swaps:
5 4 3 2 1
```

**实现 2:** 这使用一个 hashmap 来得出解决方案。

## C++

```
// C++ Program to find the
// largest permutation after
// at most k swaps using unordered_map.
#include <bits/stdc++.h>
#include <unordered_map>
using namespace std;

// Function to find the largest
// permutation after k swaps
void bestpermutation(
    int arr[], int k, int n)
{
    // Storing the elements and
    // their index in map
    unordered_map<int, int> h;
    for (int i = 0; i < n; i++) {
        h.insert(make_pair(arr[i], i));
    }

    // If number of swaps allowed
    // are equal to number of elements
    // then the resulting permutation
    // will be descending order of
    // given permutation.
    if (n <= k) {
        sort(arr, arr + n, greater<int>());
    }
    else {

        for (int j = n; j >= 1; j--) {
            if (k > 0) {

                int initial_index = h[j];
                int best_index = n - j;

                // if j is not at it's best index
                if (initial_index != best_index) {

                    h[j] = best_index;

                    // Change the index of the element
                    // which was at position 0\. Swap
                    // the element basically.
                    int element = arr[best_index];
                    h[element] = initial_index;
                    swap(
                        arr[best_index],
                        arr[initial_index]);

                    // decrement number of swaps
                    k--;
                }
            }
        }
    }
}

// Driver code
int main()
{
    int arr[] = { 3, 1, 4, 2, 5 };

    // K is the number of swaps
    int k = 10;

    // n is the size of the array
    int n = sizeof(arr) / sizeof(int);

    // Function calling
    bestpermutation(arr, k, n);

    cout << "Largest possible permutation after "
         << k << " swaps is ";
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";

    return 0;
}
// This method is contributed by Kishan Mishra.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the
// largest permutation after
// at most k swaps using unordered_map.
import java.util.*;
class GFG
{

  // Function to find the largest
  // permutation after k swaps
  static void bestpermutation(ArrayList<Integer> arr, int k, int n)
  {

    // Storing the elements and
    // their index in map
    HashMap<Integer, Integer> h =  
      new HashMap<Integer, Integer>(); 
    for (int i = 0; i < n; i++)
    {
      h.put(arr.get(i), i);
    }

    // If number of swaps allowed
    // are equal to number of elements
    // then the resulting permutation
    // will be descending order of
    // given permutation.
    if (n <= k) {
      Collections.sort(arr, Collections.reverseOrder()); 
    }
    else {

      for (int j = n; j >= 1; j--)
      {
        if (k > 0)
        {

          int initial_index = h.get(j);
          int best_index = n - j;

          // if j is not at it's best index
          if (initial_index != best_index)
          {
            h.put(j, best_index);

            // Change the index of the element
            // which was at position 0\. Swap
            // the element basically.
            int element = arr.get(best_index);
            h.put(element, initial_index);
            int temp = arr.get(best_index);
            arr.set(best_index, arr.get(initial_index));
            arr.set(initial_index, temp);

            // decrement number of swaps
            k--;
          }
        }
      }
    }
  }

  // Driver code
  public static void main(String []args)
  {

    ArrayList<Integer> arr = new ArrayList<Integer>();
    arr.add(3);
    arr.add(1);
    arr.add(4);
    arr.add(2);
    arr.add(5);

    // K is the number of swaps
    int k = 10;

    // n is the size of the array
    int n = arr.size();

    // Function calling
    bestpermutation(arr, k, n);

    System.out.print("Largest possible permutation after " + k + " swaps is ");

    for (int i = 0; i < n; i++)
      System.out.print(arr.get(i) + " ");
  }
}

// This code is contributed by rutvik_56.
```

## 蟒蛇 3

```
# Python3 program to find the
# largest permutation after
# at most k swaps using unordered_map.

# Function to find the largest
# permutation after k swaps
def bestpermutation(arr, k, n):

    # Storing the elements and
    # their index in map
    h = {}
    for i in range(n):
        h[arr[i]] = i

    # If number of swaps allowed
    # are equal to number of elements
    # then the resulting permutation
    # will be descending order of
    # given permutation.
    if (n <= k):
        arr.sort()
        arr.reverse()
    else:

        for j in range(n, 0, -1):
            if (k > 0):
                initial_index = h[j]
                best_index = n - j

                # If j is not at it's best index
                if (initial_index != best_index):
                    h[j] = best_index

                    # Change the index of the element
                    # which was at position 0\. Swap
                    # the element basically.
                    element = arr[best_index]
                    h[element] = initial_index
                    arr[best_index], arr[initial_index] = (arr[initial_index],
                                                           arr[best_index])

                    # Decrement number of swaps
                    k -= 1

# Driver Code
arr = [ 3, 1, 4, 2, 5 ]

# K is the number of swaps
k = 10

# n is the size of the array
n = len(arr)

# Function calling
bestpermutation(arr, k, n)

print("Largest possible permutation after",
      k, "swaps is", end = " ")

for i in range(n):
    print(arr[i], end = " ")

# This code is contributed by divyesh072019
```

## C#

```
// C# Program to find the
// largest permutation after
// at most k swaps using unordered_map.
using System;
using System.Collections.Generic;
class GFG {

    // Function to find the largest
    // permutation after k swaps
    static void bestpermutation(List<int> arr, int k, int n)
    {
        // Storing the elements and
        // their index in map
        Dictionary<int, int> h =  
                       new Dictionary<int, int>(); 
        for (int i = 0; i < n; i++) {
            h.Add(arr[i], i);
        }

        // If number of swaps allowed
        // are equal to number of elements
        // then the resulting permutation
        // will be descending order of
        // given permutation.
        if (n <= k) {
            arr.Sort();
            arr.Reverse();
        }
        else {

            for (int j = n; j >= 1; j--) {
                if (k > 0) {

                    int initial_index = h[j];
                    int best_index = n - j;

                    // if j is not at it's best index
                    if (initial_index != best_index) {

                        h[j] = best_index;

                        // Change the index of the element
                        // which was at position 0\. Swap
                        // the element basically.
                        int element = arr[best_index];
                        h[element] = initial_index;
                        int temp = arr[best_index];
                        arr[best_index] = arr[initial_index];
                        arr[initial_index] = temp;

                        // decrement number of swaps
                        k--;
                    }
                }
            }
        }
    }

  static void Main() {
    List<int> arr = new List<int>(new int[] {3, 1, 4, 2, 5 });

    // K is the number of swaps
    int k = 10;

    // n is the size of the array
    int n = arr.Count;

    // Function calling
    bestpermutation(arr, k, n);

    Console.Write("Largest possible permutation after " + k + " swaps is ");
    for (int i = 0; i < n; i++)
        Console.Write(arr[i] + " ");
  }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// JavaScript Program to find the
// largest permutation after
// at most k swaps using unordered_map.

// Function to find the largest
  // permutation after k swaps
function bestpermutation(arr,k,n)
{
    // Storing the elements and
    // their index in map
    let h = 
      new Map();
    for (let i = 0; i < n; i++)
    {
      h.set(arr[i], i);
    }

    // If number of swaps allowed
    // are equal to number of elements
    // then the resulting permutation
    // will be descending order of
    // given permutation.
    if (n <= k) {
      arr.sort(function(a,b){return b-a;});
    }
    else {

      for (let j = n; j >= 1; j--)
      {
        if (k > 0)
        {

          let initial_index = h[j];
          let best_index = n - j;

          // if j is not at it's best index
          if (initial_index != best_index)
          {
            h.set(j, best_index);

            // Change the index of the element
            // which was at position 0\. Swap
            // the element basically.
            let element = arr.get(best_index);
            h.set(element, initial_index);
            let temp = arr[best_index];
            arr.set(best_index, arr[initial_index]);
            arr.set(initial_index, temp);

            // decrement number of swaps
            k--;
          }
        }
      }
    }
}

// Driver code
let arr=[3,1,4,2,5];
// K is the number of swaps
let k = 10;

// n is the size of the array
let n = arr.length;

// Function calling
bestpermutation(arr, k, n);

document.write(
"Largest possible permutation after " + k + " swaps is "
);

for (let i = 0; i < n; i++)
    document.write(arr[i] + " ");

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output**

```
Largest possible permutation after 10 swaps is 5 4 3 2 1 
```

**输出:**

```
Largest possible permutation after 10 swaps is 5 4 3 2 1
```

**复杂度分析:**

*   **时间复杂度:** O(N)。
    只需要遍历一次数组。
*   **空间复杂度:** O(n)。
    存储新数组需要 O(n)空间。

本文由 [Shubham Bansal](https://www.facebook.com/banalshubham) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。