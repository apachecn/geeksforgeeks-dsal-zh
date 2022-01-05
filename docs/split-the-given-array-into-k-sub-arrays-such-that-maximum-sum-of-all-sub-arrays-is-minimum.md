# 将给定的阵列分割成 K 个子阵列，使得所有子阵列的最大和最小

> 原文:[https://www . geeksforgeeks . org/将给定的数组拆分成 k 个子数组，这样所有子数组的最大和就是最小值/](https://www.geeksforgeeks.org/split-the-given-array-into-k-sub-arrays-such-that-maximum-sum-of-all-sub-arrays-is-minimum/)

给定一个由 N 个元素组成的数组[]和一个数字 k(1<= K <= N ) . Split the given array into K subarrays (they must cover all the elements). The maximum subarray sum achievable out of K subarrays formed, must be the minimum possible. Find that possible subarray sum.
**)示例:**

> **输入:**数组[] = {1，2，3，4}，K = 3
> **输出:** 4
> 最优分割为{1，2}、{3}、{4}。所有子阵列的最大和为 4，这是 3 个分裂的最小可能。
> **输入:**数组[] = {1，1，2} K = 2
> **输出:** 2

**天真的方法:**

*   想法是找出所有的可能性。
*   为了找出所有的可能性，我们使用 ***【回溯】*** 。
*   在每一步中，我们将数组划分为子数组，求出子数组的和，并更新最大和

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;
int ans = 100000000;
// the answer is stored in ans
// we call this function solve
void solve(int a[], int n, int k, int index, int sum,
           int maxsum)
{
    // K=1 is the base Case
    if (k == 1) {
        maxsum = max(maxsum, sum);
        sum = 0;
        for (int i = index; i < n; i++) {
            sum += a[i];
        }
        // we update maxsum
        maxsum = max(maxsum, sum);
        // the answer is stored in ans
        ans = min(ans, maxsum);
        return;
    }
    sum = 0;
    // using for loop to divide the array into K-subarray
    for (int i = index; i < n; i++) {
        sum += a[i];
        // for each subarray we calculate sum ans update
        // maxsum
        maxsum = max(maxsum, sum);
        // calling function again
        solve(a, n, k - 1, i + 1, sum, maxsum);
    }
}
// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int k = 3; // K divisions
    int n = 4; // Size of Array
    solve(arr, n, k, 0, 0, 0);
    cout << ans << "\n";
}
```

## C

```
#include <stdio.h>
int ans = 100000000;
// the answer is stored in ans
// we call this function solve
// max function is used to find max of two elements
int max(int a, int b) { return a > b ? a : b; }
// min function is used to find min of two elements
int min(int a, int b) { return a < b ? a : b; }
void solve(int a[], int n, int k, int index, int sum,
           int maxsum)
{
    // K=1 is the base Case
    if (k == 1) {
        maxsum = max(maxsum, sum);
        sum = 0;
        for (int i = index; i < n; i++) {
            sum += a[i];
        }
        // we update maxsum
        maxsum = max(maxsum, sum);
        // the answer is stored in ans
        ans = min(ans, maxsum);
        return;
    }
    sum = 0;
    // using for loop to divide the array into K-subarray
    for (int i = index; i < n; i++) {
        sum += a[i];
        // for each subarray we calculate sum ans update
        // maxsum
        maxsum = max(maxsum, sum);
        // calling function again
        solve(a, n, k - 1, i + 1, sum, maxsum);
    }
}
// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int k = 3; // K divisions
    int n = 4; // Size of Array
    solve(arr, n, k, 0, 0, 0);
    printf("%d", ans);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG {
    public static int ans = 10000000;
    public static void solve(int a[], int n, int k,
                             int index, int sum, int maxsum)
    {
        // K=1 is the base Case
        if (k == 1) {
            maxsum = Math.max(maxsum, sum);
            sum = 0;
            for (int i = index; i < n; i++) {
                sum += a[i];
            }
            // we update maxsum
            maxsum = Math.max(maxsum, sum);
            // the answer is stored in ans
            ans = Math.min(ans, maxsum);
            return;
        }
        sum = 0;
        // using for loop to divide the array into
        // K-subarray
        for (int i = index; i < n; i++) {
            sum += a[i];
            // for each subarray we calculate sum ans update
            // maxsum
            maxsum = Math.max(maxsum, sum);
            // calling function again
            solve(a, n, k - 1, i + 1, sum, maxsum);
        }
    }
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3, 4 };
        int k = 3; // K divisions
        int n = 4; // Size of Array
        solve(arr, n, k, 0, 0, 0);
        System.out.println(ans + "\n");
    }
}
```

## C#

```
using System;
class GFG {
    public static int ans = 10000000;
    public static void solve(int []a, int n, int k,
                            int index, int sum, int maxsum)
    {

        // K=1 is the base Case
        if (k == 1) {
            maxsum = Math.Max(maxsum, sum);
            sum = 0;
            for (int i = index; i < n; i++) {
                sum += a[i];
            }

            // we update maxsum
            maxsum = Math.Max(maxsum, sum);

            // the answer is stored in ans
            ans = Math.Min(ans, maxsum);
            return;
        }
        sum = 0;

        // using for loop to divide the array into
        // K-subarray
        for (int i = index; i < n; i++) {
            sum += a[i];

            // for each subarray we calculate sum ans update
            // maxsum
            maxsum = Math.Max(maxsum, sum);

            // calling function again
            solve(a, n, k - 1, i + 1, sum, maxsum);
        }
    }

  // Driver code
    public static void Main(String[] args)
    {
        int []arr = { 1, 2, 3, 4 };
        int k = 3; // K divisions
        int n = 4; // Size of Array
        solve(arr, n, k, 0, 0, 0);
        Console.Write(ans + "\n");
    }
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
var ans = 10000000;

function solve(a, n, k, index, sum, maxsum)
    {
        // K=1 is the base Case
        if (k == 1) {
            maxsum = Math.max(maxsum, sum);
            sum = 0;
            for (var i = index; i < n; i++) {
                sum += a[i];
            }
            // we update maxsum
            maxsum = Math.max(maxsum, sum);
            // the answer is stored in ans
            ans = Math.min(ans, maxsum);
            return;
        }
        sum = 0;

        // using for loop to divide the array into
        // K-subarray
        for (var i = index; i < n; i++) {
            sum += a[i];

            // for each subarray we calculate sum ans update
            // maxsum
            maxsum = Math.max(maxsum, sum);

            // calling function again
            solve(a, n, k - 1, i + 1, sum, maxsum);
        }
    }

        var arr = [ 1, 2, 3, 4 ];
        var k = 3; // K divisions
        var n = 4; // Size of Array
        solve(arr, n, k, 0, 0, 0);
        document.write(ans + "\n");

        // this code is contributed by shivanisinghss2110
</script>
```

**Output**

```
4
```

**时间复杂度**:O((n1)c(k1)(**注:**‘c’在这里表示组合(即(n-1)！/((n-k)！*(k-1)！)

其中 N 是数组的元素个数，K 是除法的个数。

**有效方法:**

*   想法是利用二分搜索法找到一个最优解。
*   对于二分搜索法，最小和可以是 1，最大和可以是所有元素的和。
*   检查 mid 是否是可能的最大子阵列和。保持子阵列的计数，包括子阵列中所有可能的元素，直到它们的总和小于 mid。在此评估之后，如果计数小于或等于 K，则 mid 是可实现的，否则不可实现。(因为如果计数小于 K，我们可以进一步划分任何子阵列，它的和永远不会在中间增加)。
*   找到满足条件的 mid 的最小可能值。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if mid can
// be maximum sub - arrays sum
bool check(int mid, int array[], int n, int K)
{
    int count = 0;
    int sum = 0;
    for (int i = 0; i < n; i++) {

        // If individual element is greater
        // maximum possible sum
        if (array[i] > mid)
            return false;

        // Increase sum of current sub - array
        sum += array[i];

        // If the sum is greater than
        // mid increase count
        if (sum > mid) {
            count++;
            sum = array[i];
        }
    }
    count++;

    // Check condition
    if (count <= K)
        return true;
    return false;
}

// Function to find maximum subarray sum
// which is minimum
int solve(int array[], int n, int K)
{
    int* max = max_element(array, array + n);
    int start = *max; //Max subarray sum, considering subarray of length 1
    int end = 0;

    for (int i = 0; i < n; i++) {
        end += array[i]; //Max subarray sum, considering subarray of length n
    }

    // Answer stores possible
    // maximum sub array sum
    int answer = 0;
    while (start <= end) {
        int mid = (start + end) / 2;

        // If mid is possible solution
        // Put answer = mid;
        if (check(mid, array, n, K)) {
            answer = mid;
            end = mid - 1;
        }
        else {
            start = mid + 1;
        }
    }

    return answer;
}

// Driver Code
int main()
{
    int array[] = { 1, 2, 3, 4 };
    int n = sizeof(array) / sizeof(array[0]);
    int K = 3;
    cout << solve(array, n, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG {

    // Function to check if mid can
    // be maximum sub - arrays sum
    static boolean check(int mid, int array[], int n, int K)
    {

        int count = 0;
        int sum = 0;
        for (int i = 0; i < n; i++) {

            // If individual element is greater
            // maximum possible sum
            if (array[i] > mid)
                return false;

            // Increase sum of current sub - array
            sum += array[i];

            // If the sum is greater than
            // mid increase count
            if (sum > mid) {
                count++;
                sum = array[i];
            }
        }
        count++;

        // Check condition
        if (count <= K)
            return true;
        return false;
    }

    // Function to find maximum subarray sum
    // which is minimum
    static int solve(int array[], int n, int K)
    {
        int start = 1;
        for (int i = 0; i < n; ++i) {
            if (array[i] > start)
                start = array[i]; //Max subarray sum, considering subarray of length 1
        }
        int end = 0;

        for (int i = 0; i < n; i++) {
            end += array[i]; //Max subarray sum, considering subarray of length n
        }

        // Answer stores possible
        // maximum sub array sum
        int answer = 0;
        while (start <= end) {
            int mid = (start + end) / 2;

            // If mid is possible solution
            // Put answer = mid;
            if (check(mid, array, n, K)) {
                answer = mid;
                end = mid - 1;
            }
            else {
                start = mid + 1;
            }
        }

        return answer;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int array[] = { 1, 2, 3, 4 };
        int n = array.length;
        int K = 3;
        System.out.println(solve(array, n, K));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python 3 implementation of the above approach

# Function to check if mid can
# be maximum sub - arrays sum
def check(mid, array, n, K):
    count = 0
    sum = 0
    for i in range(n):

        # If individual element is greater
        # maximum possible sum
        if (array[i] > mid):
            return False

        # Increase sum of current sub - array
        sum += array[i]

        # If the sum is greater than
        # mid increase count
        if (sum > mid):
            count += 1
            sum = array[i]
    count += 1

    # Check condition
    if (count <= K):
        return True
    return False

# Function to find maximum subarray sum
# which is minimum
def solve(array, n, K):

    start = max(array) #Max subarray sum, considering subarray of length 1
    end = 0

    for i in range(n):
        end += array[i] #Max subarray sum, considering subarray of length n

    # Answer stores possible
    # maximum sub array sum
    answer = 0
    while (start <= end):
        mid = (start + end) // 2

        # If mid is possible solution
        # Put answer = mid;
        if (check(mid, array, n, K)):
            answer = mid
            end = mid - 1
        else:
            start = mid + 1

    return answer

# Driver Code
if __name__ == '__main__':
    array = [1, 2, 3, 4]
    n = len(array)
    K = 3
    print(solve(array, n, K))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to check if mid can
    // be maximum sub - arrays sum
    static Boolean check(int mid, int []array,
                                int n, int K)
    {

        int count = 0;
        int sum = 0;
        for (int i = 0; i < n; i++)
        {

            // If individual element is greater
            // maximum possible sum
            if (array[i] > mid)
                return false;

            // Increase sum of current sub - array
            sum += array[i];

            // If the sum is greater than
            // mid increase count
            if (sum > mid)
            {
                count++;
                sum = array[i];
            }
        }
        count++;

        // Check condition
        if (count <= K)
            return true;
        return false;
    }

    // Function to find maximum subarray sum
    // which is minimum
    static int solve(int []array, int n, int K)
    {
        int start = 1;
        for (int i = 0; i < n; ++i) {
            if (array[i] > start)
                start = array[i]; //Max subarray sum, considering subarray of length 1
        }
        int end = 0;

        for (int i = 0; i < n; i++)
        {
            end += array[i];  //Max subarray sum, considering subarray of length n
        }

        // Answer stores possible
        // maximum sub array sum
        int answer = 0;
        while (start <= end)
        {
            int mid = (start + end) / 2;

            // If mid is possible solution
            // Put answer = mid;
            if (check(mid, array, n, K))
            {
                answer = mid;
                end = mid - 1;
            }
            else
            {
                start = mid + 1;
            }
        }

        return answer;
    }

    // Driver Code
    public static void Main (String[] args)
    {
        int []array = { 1, 2, 3, 4 };
        int n = array.Length ;
        int K = 3;
        Console.WriteLine(solve(array, n, K));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

// Function to check if mid can
// be maximum sub - arrays sum
function check(mid, array, n, K)
{
    var count = 0;
    var sum = 0;
    for (var i = 0; i < n; i++) {

        // If individual element is greater
        // maximum possible sum
        if (array[i] > mid)
            return false;

        // Increase sum of current sub - array
        sum += array[i];

        // If the sum is greater than
        // mid increase count
        if (sum > mid) {
            count++;
            sum = array[i];
        }
    }
    count++;

    // Check condition
    if (count <= K)
        return true;
    return false;
}

// Function to find maximum subarray sum
// which is minimum
function solve(array, n, K)
{
    var max = array.reduce((a,b)=>Math.max(a,b));
    var start = max; //Max subarray sum, considering subarray of length 1
    var end = 0;

    for (var i = 0; i < n; i++) {
        end += array[i]; //Max subarray sum, considering subarray of length n
    }

    // Answer stores possible
    // maximum sub array sum
    var answer = 0;
    while (start <= end) {
        var mid = parseInt((start + end) / 2);

        // If mid is possible solution
        // Put answer = mid;
        if (check(mid, array, n, K)) {
            answer = mid;
            end = mid - 1;
        }
        else {
            start = mid + 1;
        }
    }

    return answer;
}

// Driver Code
var array = [1, 2, 3, 4];
var n = array.length;
var K = 3;
document.write( solve(array, n, K));

</script>
```

**Output**

```
4
```

**时间复杂度:** O(N*log(Sum))
其中 N 是数组的元素个数，Sum 是数组所有元素的和。