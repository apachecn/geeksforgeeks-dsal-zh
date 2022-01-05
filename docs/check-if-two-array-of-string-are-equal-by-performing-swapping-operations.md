# 通过执行交换操作来检查两个字符串数组是否相等

> 原文:[https://www . geesforgeks . org/通过执行交换操作检查字符串数组是否相等/](https://www.geeksforgeeks.org/check-if-two-array-of-string-are-equal-by-performing-swapping-operations/)

给定两个相同大小的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 和 **brr[]** ，其中包含相等长度的[字符串](https://www.geeksforgeeks.org/string-data-structure/)。在一个操作中， **brr[]** 中任意字符串的任意两个字符可以相互交换，或者交换 brr[]中的任意两个字符串。任务是发现 **brr[]** 是否可以等于 **arr[]** 。

**示例:**

> **输入:**arr[]= {“BCD”、“AAC”}，brr[]= {“ACA”、“DBC”}
> **输出:**真
> **说明:**在 brr[]中执行以下交换操作，使 arr[]等于 brr[]。
> 交换(brr[0][1]，brr[0][2])->brr[0]变为“aac”，等于 arr[1]。
> 交换(brr[1][0]，brr[1][1])->brr[1]更改为“bdc”。
> 交换(brr[1][1]，brr[1][2])->brr[1]变为“bcd”，等于 arr[0]。
> 交换(brr[0]，brr[1])，将 brr[]更改为{“BCD”，“AAC”}，等于 arr[]。
> 
> 因此，通过执行上述操作，可以使 brr[]等于 arr[]。
> 
> **输入:arr[]**= {“ab”、“c”}，brr = {“AC”、“b”}
> **输出:**假

**方法:**给定的问题可以使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决。只有当一个[字符串](https://www.geeksforgeeks.org/string-data-structure/)中的每个字符的频率等于另一个字符串时，才可以通过交换使两个字符串相等。如果两个字符串都被排序，那么所有的字符都被排列好，然后只看两个排序的字符串是否相等就知道答案了。按照以下步骤解决给定的问题。

*   在 **arr[]** 以及 **brr[]** 中对每个字符串进行排序。
*   排序 **arr[]** 和 **brr[]** 。
*   用变量 **i** 迭代**arr【】**，对于每个 **i**
    *   检查**是否 arr[i] == brr[i]** 。
        *   如果为真，则继续比较剩余的字符串。
        *   如果为 false，则表示至少有一个字符串不在 **brr[]** 中。因此返回 false。
*   检查后，返回 true 作为最终答案。

下面是上述方法的实现:

## C++14

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check whether brr[] can be made
// equal to arr[] by doing swapping operations
bool checkEqualArrays(vector<string> arr,
                      vector<string> brr,
                      int N)
{

    // siz variable to store siz of string
    int siz = arr[0].size();

    // iterate till N to sort strings
    for (int i = 0; i < N; i++) {
        // sort each string in arr[]
        sort(arr[i].begin(), arr[i].end());

        // sort each string in brr[]
        sort(brr[i].begin(), brr[i].end());
    }

    // Sort both the vectors so that all
    // the comparable strings will be arranged
    sort(arr.begin(), arr.end());
    sort(brr.begin(), brr.end());

    // iterate till N
    // to compare string in arr[]
    // and brr[]
    for (int i = 0; i < N; i++) {

        // Compare each string
        if (arr[i] != brr[i]) {

            // Return false because
            // if atleast one
            // string is not equal
            // then brr[] cannot
            // be converted to arr[]
            return false;
        }
    }

    // All the strings
    // are compared so at last
    // return true.
    return true;
}

// Driver code
int main()
{

    int N = 2;
    vector<string> arr = { "bcd", "aac" };
    vector<string> brr = { "aca", "dbc" };

    // Store the answer in variable
    bool ans = checkEqualArrays(arr, brr, N);

    if (ans)
        cout << "true";
    else
        cout << "false";

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for above approach

# Function to check whether brr[] can be made
# equal to arr[] by doing swapping operations
def checkEqualArrays(arr,brr, N) :

    # siz variable to store size of string
    siz = len(arr[0]);

    # iterate till N to sort strings
    for i in range(N) :

        # sort each string in arr[]
        temp1 = list(arr[i]);
        temp1.sort();
        arr[i] = "".join(temp1)

        # sort each string in brr[]
        temp2 = list(brr[i]);
        temp2.sort();
        brr[i] = "".join(temp2);

    # Sort both the vectors so that all
    # the comparable strings will be arranged
    arr.sort()
    brr.sort()

    # iterate till N
    # to compare string in arr[]
    # and brr[]
    for i in range(N) :

        # Compare each string
        if (arr[i] != brr[i]) :

            # Return false because
            # if atleast one
            # string is not equal
            # then brr[] cannot
            # be converted to arr[]
            return False;

    # All the strings
    # are compared so at last
    # return true.
    return True;

# Driver code
if __name__ == "__main__" :

    N = 2;
    arr = [ "bcd", "aac" ];
    brr = [ "aca", "dbc" ];

    # Store the answer in variable
    ans = checkEqualArrays(arr, brr, N);

    if (ans) :
        print("true");
    else :
        print("false");

    # This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// Javascript program for above approach

// Function to check whether brr[] can be made
// equal to arr[] by doing swapping operations
function checkEqualArrays(arr, brr, N)
{

    // siz variable to store siz of string
    let siz = arr[0].length;

    // iterate till N to sort strings
    for (let i = 0; i < N; i++)
    {

        // sort each string in arr[]
        arr[i] = arr[i].split("").sort().join("")

        // sort each string in brr[]
        brr[i] = brr[i].split("").sort().join("")

    }

    // Sort both the vectors so that all
    // the comparable strings will be arranged
    arr.sort()
    brr.sort()

    // iterate till N
    // to compare string in arr[]
    // and brr[]
    for (let i = 0; i < N; i++) {

        // Compare each string
        if (arr[i] != brr[i]) {

            // Return false because
            // if atleast one
            // string is not equal
            // then brr[] cannot
            // be converted to arr[]
            return false;
        }
    }

    // All the strings
    // are compared so at last
    // return true.
    return true;
}

// Driver code
    let N = 2;
    let arr = [ "bcd", "aac" ];
    let brr = [ "aca", "dbc" ];

    // Store the answer in variable
    let ans = checkEqualArrays(arr, brr, N);

    if (ans)
        document.write("true");
    else
        document.write("false");

        // This code is contributed by saurabh_jaiswal.
</script>
```

**Output**

```
true
```

**时间复杂度:** O(2* (N * logN) + 2 * (N * logM))，其中 N 是数组的大小，M 是每个字符串的大小。
**辅助空间:** O(1)