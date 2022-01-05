# 计数所有不同数字出现在 K 中的数组元素

> 原文:[https://www . geeksforgeeks . org/count-array-elements-其全异数字出现在-k/](https://www.geeksforgeeks.org/count-array-elements-whose-all-distinct-digits-appear-in-k/)

给定一个由 **N** 个正整数和一个正整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是找出其不同数字是 **K** 的数字子集的数组元素的计数。

**例:**

> **输入:** arr[] = { 1，12，1222，13，2 }，K = 12
> **输出:** 4
> **解释:**
> K 的不同数字是{ 1，2 }
> arr[0]的不同数字是{ 1 }，这是 K 的数字的子集 这是 k 的数字子集。
> arr[3]的不同数字是{ 1，3 }，这不是 k 的数字子集。
> arr[4]的不同数字是{ 2 }，这是 k 的数字子集。
> 因此，所需的输出是 4。
> 
> **输入** : arr = {1，2，3，4，1234}，K = 1234
> **输出:** 5

**天真方法:**解决问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**并针对每个数组元素，检查[其所有不同的数字](https://www.geeksforgeeks.org/count-of-unique-digits-in-a-given-number-n/)是否出现在 **K** 中。如果发现为真，则增加计数。最后，打印获得的计数。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check a digit occurs
// in the digit of K or not
static bool isValidDigit(int digit, int K)
{

    // Iterate over all possible
    // digits of K
    while (K != 0)
    {

        // If current digit
        // equal to digit
        if (K % 10 == digit)
        {
            return true;
        }

        // Update K
        K = K / 10;
    }
    return false;
}

// Function to find the count of array
// elements whose distinct digits are
// a subset of digits of K
int noOfValidNumbers(int K, int arr[], int n)
{

    // Stores count of array elements
    // whose distinct digits are subset
    // of digits of K
    int count = 0;

    // Traverse the array, []arr
    for(int i = 0; i < n; i++)
    {

        // Stores the current element
        int no = arr[i];

        // Check if all the digits arr[i]
        // is a subset of the digits of
        // K or not
        bool flag = true;

        // Iterate over all possible
        // digits of arr[i]
        while (no != 0)
        {

            // Stores current digit
            int digit = no % 10;

            // If current digit does not
            // appear in K
            if (!isValidDigit(digit, K))
            {

                // Update flag
                flag = false;
                break;
            }

            // Update no
            no = no / 10;
        }

        // If all the digits arr[i]
        // appear in K
        if (flag == true)
        {

            // Update count
            count++;
        }
    }

    // Finally print count
    return count;
}

// Driver Code
int main()
{
    int K = 12;
    int arr[] = { 1, 12, 1222, 13, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << noOfValidNumbers(K, arr, n);

    return 0;
}

// This code is contributed by susmitakundugoaldanga
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

    // Function to check a digit occurs
    // in the digit of K or not
    static boolean isValidDigit(int digit, int K)
    {
        // Iterate over all possible
        // digits of K
        while (K != 0) {

            // If current digit
            // equal to digit
            if (K % 10 == digit) {
                return true;
            }

            // Update K
            K = K / 10;
        }

        return false;
    }

    // Function to find the count of array elements
    // whose distinct digits are a subset of digits of K
    static int noOfValidNumbers(int K, int arr[])
    {

        // Stores count of array elements
        // whose distinct digits are subset
        // of digits of K
        int count = 0;

        // Traverse the array, arr[]
        for (int i = 0; i < arr.length; i++) {

            // Stores the current element
            int no = arr[i];

            // Check if all the digits arr[i]
            // is a subset of the digits of
            // K or not
            boolean flag = true;

            // Iterate over all possible
            // digits of arr[i]
            while (no != 0) {

                // Stores current digit
                int digit = no % 10;

                // If current digit does not
                // appear in K
                if (!isValidDigit(digit, K)) {

                    // Update flag
                    flag = false;
                    break;
                }

                // Update no
                no = no / 10;
            }

            // If all the digits arr[i] appear in K
            if (flag == true) {

                // Update count
                count++;
            }
        }

        // Finally print count
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int K = 12;
        int arr[] = { 1, 12, 1222, 13, 2 };
        System.out.println(noOfValidNumbers(K, arr));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check a digit occurs
# in the digit of K or not
def isValidDigit(digit, K):

    # Iterate over all possible
    # digits of K
    while (K != 0):

        # If current digit
        # equal to digit
        if (K % 10 == digit):
            return True

        # Update K
        K = K // 10
    return False

# Function to find the count of array
# elements whose distinct digits are
# a subset of digits of K
def noOfValidNumbers(K, arr, n):

    # Stores count of array elements
    # whose distinct digits are subset
    # of digits of K
    count = 0

    # Traverse the array, []arr
    for i in range(n):

        # Stores the current element
        no = arr[i]

        # Check if all the digits arr[i]
        # is a subset of the digits of
        # K or not
        flag = True

        # Iterate over all possible
        # digits of arr[i]
        while (no != 0):

            # Stores current digit
            digit = no % 10

            # If current digit does not
            # appear in K
            if (not isValidDigit(digit, K)):

                # Update flag
                flag = False
                break

            # Update no
            no = no // 10

        # If all the digits arr[i]
        # appear in K
        if (flag == True):

            # Update count
            count += 1

    # Finally print count
    return count

# Driver Code
if __name__ == "__main__":
    K = 12
    arr = [1, 12, 1222, 13, 2]
    n = len(arr)
    print(noOfValidNumbers(K, arr, n))

    # This code is contributed by chitranayal.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check a digit occurs
// in the digit of K or not
static bool isValidDigit(int digit, int K)
{

    // Iterate over all possible
    // digits of K
    while (K != 0)
    {

        // If current digit
        // equal to digit
        if (K % 10 == digit)
        {
            return true;
        }

        // Update K
        K = K / 10;
    }

    return false;
}

// Function to find the count of array elements
// whose distinct digits are a subset of digits of K
static int noOfValidNumbers(int K, int []arr)
{

    // Stores count of array elements
    // whose distinct digits are subset
    // of digits of K
    int count = 0;

    // Traverse the array, []arr
    for(int i = 0; i < arr.Length; i++)
    {

        // Stores the current element
        int no = arr[i];

        // Check if all the digits arr[i]
        // is a subset of the digits of
        // K or not
        bool flag = true;

        // Iterate over all possible
        // digits of arr[i]
        while (no != 0)
        {

            // Stores current digit
            int digit = no % 10;

            // If current digit does not
            // appear in K
            if (!isValidDigit(digit, K))
            {

                // Update flag
                flag = false;
                break;
            }

            // Update no
            no = no / 10;
        }

        // If all the digits arr[i] appear in K
        if (flag == true)
        {

            // Update count
            count++;
        }
    }

    // Finally print count
    return count;
}

// Driver Code
public static void Main(String[] args)
{
    int K = 12;
    int []arr = { 1, 12, 1222, 13, 2 };

    Console.WriteLine(noOfValidNumbers(K, arr));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check a digit occurs
// in the digit of K or not
function isValidDigit(digit, K)
{

    // Iterate over all possible
    // digits of K
    while (K != 0)
    {

        // If current digit
        // equal to digit
        if (K % 10 == digit)
        {
            return true;
        }

        // Update K
        K = parseInt(K / 10);
    }
    return false;
}

// Function to find the count of array
// elements whose distinct digits are
// a subset of digits of K
function noOfValidNumbers(K, arr, n)
{

    // Stores count of array elements
    // whose distinct digits are subset
    // of digits of K
    let count = 0;

    // Traverse the array, []arr
    for(let i = 0; i < n; i++)
    {

        // Stores the current element
        let no = arr[i];

        // Check if all the digits arr[i]
        // is a subset of the digits of
        // K or not
        let flag = true;

        // Iterate over all possible
        // digits of arr[i]
        while (no != 0)
        {

            // Stores current digit
            let digit = no % 10;

            // If current digit does not
            // appear in K
            if (!isValidDigit(digit, K))
            {

                // Update flag
                flag = false;
                break;
            }

            // Update no
            no = parseInt(no / 10);
        }

        // If all the digits arr[i]
        // appear in K
        if (flag == true)
        {

            // Update count
            count++;
        }
    }

    // Finally print count
    return count;
}

// Driver Code
    let K = 12;
    let arr = [ 1, 12, 1222, 13, 2 ];
    let n = arr.length;

    document.write(noOfValidNumbers(K, arr, n));

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N * log<sub>10</sub>(K)* log<sub>10</sub>(Max))，Max 为最大阵元*
***辅助空间:** O(1)*

**高效方法:**上述方法可以使用[哈希集](https://www.geeksforgeeks.org/hashset-in-java/)进行优化。按照以下步骤解决问题:

1.  迭代 **K** 的数字，并将所有数字插入到一个[哈希集中](https://www.geeksforgeeks.org/hashset-in-java/)说**设置**
2.  [遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)**arr【】**，对于每个数组元素，迭代当前元素的所有数字，并检查所有数字是否存在于集合中。如果发现为真，则增加计数。
3.  最后，打印获得的计数。

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to the count of array elements whose
// distinct digits are a subset of the digits of K
static int noOfValidKbers(int K, vector<int> arr)
{

    // Stores distinct digits of K
    map<int,int> set;

    // Iterate over all the digits of K
    while (K != 0)
    {

        // Insert current digit into set
        set[K % 10] = 1;

        // Update K
        K = K / 10;
    }

    // Stores the count of array elements
    // whose distinct digits are a subset
    // of the digits of K
    int count = 0;

    // Traverse the array, arr[]
    for (int i = 0; i < arr.size(); i++)
    {

        // Stores current element
        int no = arr[i];

        // Check if all the digits of arr[i]
        // are present in K or not
        bool flag = true;

        // Iterate over all the digits of arr[i]
        while (no != 0)
        {

            // Stores current digit
            int digit = no % 10;

            // If digit not present in the set
            if (set.find(digit)==set.end())
            {

                // Update flag
                flag = false;
                break;
            }

            // Update no
            no = no / 10;
        }

        // If all the digits of
        // arr[i] present in set
        if (flag == true)
        {

            // Update count
            count++;
        }
    }
    return count;
}

// Driver Code
int main()
{
    int K = 12;
    vector<int> arr = { 1, 12, 1222, 13, 2 };
    cout<<(noOfValidKbers(K, arr));
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to the count of array elements whose
    // distinct digits are a subset of the digits of K
    static int noOfValidKbers(int K, int arr[])
    {

        // Stores distinct digits of K
        HashSet<Integer> set = new HashSet<>();

        // Iterate over all the digits of K
        while (K != 0) {

            // Insert current digit into set
            set.add(K % 10);

            // Update K
            K = K / 10;
        }

        // Stores the count of array elements
        // whose distinct digits are a subset
        // of the digits of K
        int count = 0;

        // Traverse the array, arr[]
        for (int i = 0; i < arr.length; i++) {

            // Stores current element
            int no = arr[i];

            // Check if all the digits of arr[i]
            // are present in K or not
            boolean flag = true;

            // Iterate over all the digits of arr[i]
            while (no != 0) {

                // Stores current digit
                int digit = no % 10;

                // If digit not present in the set
                if (!set.contains(digit)) {

                    // Update flag
                    flag = false;
                    break;
                }

                // Update no
                no = no / 10;
            }

            // If all the digits of
            // arr[i] present in set
            if (flag == true) {

                // Update count
                count++;
            }
        }
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int K = 12;
        int arr[] = { 1, 12, 1222, 13, 2 };
        System.out.println(noOfValidKbers(K, arr));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to implement
# the above approach

# Function to the count of array elements whose
# distinct digits are a subst of the digits of K
def noOfValidKbers(K, arr):

    # Stores distinct digits of K
    st = {}

    # Iterate over all the digits of K
    while(K != 0):

        # Insert current digit into st
        if(K % 10 in st):
            st[K % 10] = 1
        else:
            st[K % 10] = st.get(K % 10, 0) + 1

        # Update K
        K = K // 10

    # Stores the count of array elements
    # whose distinct digits are a subst
    # of the digits of K
    count = 0

    # Traverse the array, arr[]
    for i in range(len(arr)):

        # Stores current element
        no = arr[i]

        # Check if all the digits of arr[i]
        # are present in K or not
        flag = True

        # Iterate over all the digits of arr[i]
        while(no != 0):

            # Stores current digit
            digit = no % 10

            # If digit not present in the st
            if (digit not in st):

                # Update flag
                flag = False
                break

            # Update no
            no = no//10

        # If all the digits of
        # arr[i] present in st
        if (flag == True):

            # Update count
            count += 1
    return count

# Driver Code
if __name__ == '__main__':
    K = 12
    arr =  [1, 12, 1222, 13, 2]
    print(noOfValidKbers(K, arr))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to the count of array elements whose
// distinct digits are a subset of the digits of K
static int noOfValidKbers(int K, int []arr)
{

    // Stores distinct digits of K
    HashSet<int> set = new HashSet<int>();

    // Iterate over all the digits of K
    while (K != 0)
    {

        // Insert current digit into set
        set.Add(K % 10);

        // Update K
        K = K / 10;
    }

    // Stores the count of array elements
    // whose distinct digits are a subset
    // of the digits of K
    int count = 0;

    // Traverse the array, []arr
    for(int i = 0; i < arr.Length; i++)
    {

        // Stores current element
        int no = arr[i];

        // Check if all the digits of arr[i]
        // are present in K or not
        bool flag = true;

        // Iterate over all the digits of arr[i]
        while (no != 0)
        {

            // Stores current digit
            int digit = no % 10;

            // If digit not present in the set
            if (!set.Contains(digit))
            {

                // Update flag
                flag = false;
                break;
            }

            // Update no
            no = no / 10;
        }

        // If all the digits of
        // arr[i] present in set
        if (flag == true)
        {

            // Update count
            count++;
        }
    }
    return count;
}

// Driver Code
public static void Main(String[] args)
{
    int K = 12;
    int []arr = { 1, 12, 1222, 13, 2 };

    Console.WriteLine(noOfValidKbers(K, arr));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach
    // Function to the count of array elements whose
    // distinct digits are a subset of the digits of K
    function noOfValidKbers(K , arr) {

        // Stores distinct digits of K
        var set = new Set();

        // Iterate over all the digits of K
        while (K != 0) {

            // Insert current digit into set
            set.add(K % 10);

            // Update K
            K = parseInt(K / 10);
        }

        // Stores the count of array elements
        // whose distinct digits are a subset
        // of the digits of K
        var count = 0;

        // Traverse the array, arr
        for (i = 0; i < arr.length; i++) {

            // Stores current element
            var no = arr[i];

            // Check if all the digits of arr[i]
            // are present in K or not
            var flag = true;

            // Iterate over all the digits of arr[i]
            while (no != 0) {

                // Stores current digit
                var digit = no % 10;

                // If digit not present in the set
                if (!set.has(digit)) {

                    // Update flag
                    flag = false;
                    break;
                }

                // Update no
                no = parseInt(no / 10);
            }

            // If all the digits of
            // arr[i] present in set
            if (flag == true) {

                // Update count
                count++;
            }
        }
        return count;
    }

    // Driver Code

        var K = 12;
        var arr = [ 1, 12, 1222, 13, 2 ];
        document.write(noOfValidKbers(K, arr));

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N * log <sub>10</sub> (Max))，其中 Max 为最大阵元*
***辅助空间:** O(10)*