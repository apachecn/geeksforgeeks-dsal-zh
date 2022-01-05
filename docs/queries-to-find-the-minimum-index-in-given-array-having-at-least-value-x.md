# 查询查找给定数组中至少有值 X 的最小索引

> 原文:[https://www . geesforgeks . org/query-to-find-给定数组中的最小索引-至少具有-x 值/](https://www.geeksforgeeks.org/queries-to-find-the-minimum-index-in-given-array-having-at-least-value-x/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个由 **M** 个整数组成的[数组](https://www.geeksforgeeks.org/vector-in-cpp-stl/)**，每个整数代表一个查询，每个查询的任务**Q【I】**是找到一个值大于或等于**Q【I】**的数组元素的最小索引。如果没有这样的索引，则打印 **-1** 。**

****示例:****

> ****输入:** arr[] = { 1，9 }，Q[] = { 7，10，0 }
> **输出:** 1 -1 0
> **说明:**
> 值大于 Q[0]的 arr[]的最小索引为 1。
> arr[]中不存在值大于 Q[1]的索引。
> 值大于 Q[2]的 arr[]的最小索引为 0。
> 因此，要求的输出为 1 -1 0。**
> 
> ****输入:** arr[] = {2，3，4}，Q[] = {2，3，4 }
> T3】输出: 0 1 2**

****方法:**使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)和[前缀求和技术](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)可以解决问题。按照以下步骤解决问题:**

*   **初始化一个形式为 **{第一，第二}** 的[数组](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)，比如**storarridx[]**，来存储数组元素和索引。**
*   **[按照数组元素](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)的升序排列数组**storarridx[]**。**
*   **[按递增顺序对数组 arr[]进行排序](https://www.geeksforgeeks.org/sort-c-stl/)。**
*   **初始化一个数组，比如说 **minIdx[]** ，这样 **minIdx[i]** 存储一个数组元素的最小索引，该数组元素的值大于或等于 **arr[i]** 。**
*   **[使用变量 **i** 反向遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**storarridx[]**。对于每个 **i <sup>th</sup>** 索引，更新 **minIdx[i] = min(minIdx[i + 1]，storarridx[I]。第二)**。**
*   **[导线阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)T2【Q】使用变量 **i** 。每进行一次 **i <sup>th</sup>** 查询，将**Q【I】**的[下界](https://www.geeksforgeeks.org/lower_bound-in-cpp/)的索引查找到**arr【】**中，检查得到的索引是否小于 **N** 。如果发现为真，则打印 **minIdx[i]** 。**
*   **否则，打印 **-1** 。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest index
// of an array element whose value is
// less than or equal to Q[i]
void minimumIndex(vector<int>& arr,
                  vector<int>& Q)
{

    // Stores size of array
    int N = arr.size();

    // Stores coun of queries
    int M = Q.size();

    // Store array elements along
    // with the index
    vector<pair<int, int> > storeArrIdx;

    // Store smallest index of an array
    // element whose value is greater
    // than or equal to i
    vector<int> minIdx(N);

    // Traverse the array
    for (int i = 0; i < N; ++i) {

        // Insert {arr[i], i} into
        // storeArrIdx[]
        storeArrIdx.push_back({ arr[i], i });
    }

    // Sort the array
    sort(arr.begin(), arr.end());

    // Sort the storeArrIdx
    sort(storeArrIdx.begin(),
         storeArrIdx.end());

    // Stores index of arr[N - 1] in
    // sorted order
    minIdx[N - 1]
        = storeArrIdx[N - 1].second;

    // Traverse the array storeArrIdx[]
    for (int i = N - 2; i >= 0; i--) {

        // Update minIdx[i]
        minIdx[i] = min(minIdx[i + 1],
                        storeArrIdx[i].second);
    }

    // Traverse the array Q[]
    for (int i = 0; i < M; i++) {

        // Store the index of
        // lower_bound of Q[i]
        int pos
            = lower_bound(arr.begin(),
                          arr.end(), Q[i])
              - arr.begin();

        // If no index found whose value
        // greater than or equal to arr[i]
        if (pos == N) {
            cout << -1 << " ";
            continue;
        }

        // Print smallest index whose value
        // greater than or equal to Q[i]
        cout << minIdx[pos] << " ";
    }
}

// Driver Code
int main()
{

    vector<int> arr = { 1, 9 };
    vector<int> Q = { 7, 10, 0 };

    minimumIndex(arr, Q);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for above approach
import java.util.*;
import java.lang.*;
class pair
{
  int element,index;
  pair(int element, int index)
  {
    this.element = element;
    this.index = index;
  }
}
class GFG
{

  // Function to find the smallest index
  // of an array element whose value is
  // less than or equal to Q[i]
  static void minimumIndex(int[] arr,
                           int[] Q)
  {

    // Stores size of array
    int N = arr.length;

    // Stores coun of queries
    int M = Q.length;

    // Store array elements along
    // with the index
    ArrayList<pair> storeArrIdx = new ArrayList<>();

    // Store smallest index of an array
    // element whose value is greater
    // than or equal to i
    int[] minIdx = new int[N];

    // Traverse the array
    for (int i = 0; i < N; ++i)
    {

      // Insert {arr[i], i} into
      // storeArrIdx[]
      storeArrIdx.add(new pair(arr[i], i));
    }

    // Sort the array
    Arrays.sort(arr);

    // Sort the storeArrIdx
    Collections.sort(storeArrIdx, (a, b)->a.element-b.element);

    // Stores index of arr[N - 1] in
    // sorted order
    minIdx[N - 1]
      = storeArrIdx.get(N - 1).index;

    // Traverse the array storeArrIdx[]
    for (int i = N - 2; i >= 0; i--) {

      // Update minIdx[i]
      minIdx[i] =Math.min(minIdx[i + 1],
                          storeArrIdx.get(i).index);
    }

    // Traverse the array Q[]
    for (int i = 0; i < M; i++) {

      // Store the index of
      // lower_bound of Q[i]
      int pos
        = lower_bound(arr, Q[i]);

      // If no index found whose value
      // greater than or equal to arr[i]
      if (pos == N) {
        System.out.print("-1"+" ");
        continue;
      }

      // Print smallest index whose value
      // greater than or equal to Q[i]
      System.out.print(minIdx[pos]+" ");
    }
  }
  static int lower_bound(int[] arr,int element)
  {
    for(int i = 0; i < arr.length; i++)
      if(element <= arr[i])
        return i;

    return arr.length; 
  }

  // Driver function
  public static void main (String[] args)
  {
    int[] arr = { 1, 9 };
    int[] Q = { 7, 10, 0 };

    minimumIndex(arr, Q);
  }
}

// This code is contributed by offbeat
```

## **蟒蛇 3**

```
# Python3 program to implement
# the above approachf
from bisect import bisect_left

# Function to find the smallest index
# of an array element whose value is
# less than or equal to Q[i]
def minimumIndex(arr, Q):

    # Stores size of array
    N = len(arr)

    # Stores coun of queries
    M = len(Q)

    # Store array elements along
    # with the index
    storeArrIdx = []

    # Store smallest index of an array
    # element whose value is greater
    # than or equal to i
    minIdx = [0]*(N)

    # Traverse the array
    for i in range(N):

        # Insert {arr[i], i} into
        # storeArrIdx[]
        storeArrIdx.append([arr[i], i])

    # Sort the array
    arr = sorted(arr)

    # Sort the storeArrIdx
    storeArrIdx = sorted(storeArrIdx)

    # Stores index of arr[N - 1] in
    # sorted order
    minIdx[N - 1] = storeArrIdx[N - 1][1]

    # Traverse the array storeArrIdx[]
    for i in range(N - 2, -1, -1):

        # Update minIdx[i]
        minIdx[i] = min(minIdx[i + 1], storeArrIdx[i][1])

    # Traverse the array Q[]
    for i in range(M):

        # Store the index of
        # lower_bound of Q[i]
        pos = bisect_left(arr, Q[i])

        # If no index found whose value
        # greater than or equal to arr[i]
        if (pos == N):
            print(-1, end = " ")
            continue

        # Prsmallest index whose value
        # greater than or equal to Q[i]
        print(minIdx[pos], end = " ")

# Driver Code
if __name__ == '__main__':
    arr = [1, 9]
    Q = [7, 10, 0]
    minimumIndex(arr, Q)

    # This code is contributed by mohit kumar 29
```

## **java 描述语言**

```
<script>

// JavaScript program for above approach

class pair
{
    constructor(element,index)
    {
        this.element = element;
        this.index = index;
    }
}

// Function to find the smallest index
  // of an array element whose value is
  // less than or equal to Q[i]
function minimumIndex(arr,Q)
{
    // Stores size of array
    let N = arr.length;

    // Stores coun of queries
    let M = Q.length;

    // Store array elements along
    // with the index
    let storeArrIdx = [];

    // Store smallest index of an array
    // element whose value is greater
    // than or equal to i
    let minIdx = new Array(N);
     for(let i=0;i<N;i++)
    {
        minIdx[i]=0;
    }
    // Traverse the array
    for (let i = 0; i < N; ++i)
    {

      // Insert {arr[i], i} into
      // storeArrIdx[]
      storeArrIdx.push([arr[i], i]);
    }

    // Sort the array
    (arr).sort(function(a,b){return a-b;});

    // Sort the storeArrIdx
    storeArrIdx.sort(function(a, b){ return a[0]-b[0]});

    // Stores index of arr[N - 1] in
    // sorted order
    minIdx[N - 1]
      = storeArrIdx[N - 1][1];

    // Traverse the array storeArrIdx[]
    for (let i = N - 2; i >= 0; i--) {

      // Update minIdx[i]
      minIdx[i] =Math.min(minIdx[i + 1],
                          storeArrIdx[i][1]);
    }

    // Traverse the array Q[]
    for (let i = 0; i < M; i++) {

      // Store the index of
      // lower_bound of Q[i]
      let pos
        = lower_bound(arr, Q[i]);

      // If no index found whose value
      // greater than or equal to arr[i]
      if (pos == N) {
        document.write("-1"+" ");
        continue;
      }

      // Print smallest index whose value
      // greater than or equal to Q[i]
      document.write(minIdx[pos]+" ");
    }
}

function lower_bound(arr,element)
{
    for(let i = 0; i < arr.length; i++)
      if(element <= arr[i])
        return i;

    return arr.length;
}

// Driver function
let arr=[1, 9];
let Q=[7, 10, 0 ];

minimumIndex(arr, Q);

// This code is contributed by patel2127

</script>
```

****Output:** 

```
1 -1 0
```** 

*****时间复杂度:** O(N * log(N))*
***辅助空间:** O(N)***