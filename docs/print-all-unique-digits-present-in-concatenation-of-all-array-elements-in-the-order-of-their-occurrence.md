# 按照出现的顺序打印所有数组元素串联中出现的所有唯一数字

> 原文:[https://www . geeksforgeeks . org/print-all-unique-digits-in-present-in-concation-in-all-array-elements-in-in-order-of-then-then-then-then-then-then-then-then-then-then](https://www.geeksforgeeks.org/print-all-unique-digits-present-in-concatenation-of-all-array-elements-in-the-order-of-their-occurrence/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是打印该数字的所有唯一数字，这些数字是在排除前导零后，按照出现的顺序串联所有数组元素而形成的。

### 示例:

> **输入:** arr[] = {122，474，612，932}
> **输出:** 7 6 9 3
> **解释:**
> 数组元素串联形成的数为“ **122474612932** ”。
> 数字中出现的唯一数字是 **7 6 9 3** (按照出现的顺序)。
> 
> **输入:** arr[]={0，912，231，14}
> **输出:** 9 3 4
> **解释:**
> 数组元素串联形成的数为“**091223114”**。
> 去除前导 0 后得到的最终编号为**“91223114”。**
> 数字中出现的唯一数字是 **9 3 4** (按出现的顺序)。

**方法**:想法是[将所有数组元素转换成它们的等价字符串](https://www.geeksforgeeks.org/different-ways-for-integer-to-string-conversions-in-java/)并连接这些字符串，然后使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)来查找所获得的数字中存在的唯一数字。

按照以下步骤解决问题。

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr**[][将每个数组元素转换为其等价字符串](https://www.geeksforgeeks.org/convert-integer-to-string-in-python/)，并将所有字符串串联在一个变量中，比如 **S** 。
*   使用[打字](https://www.geeksforgeeks.org/typecasting-in-c/)将字符串 **S** 转换为等效整数(比如 **N** )(去掉前导 0)
*   初始化一个大小为 **10** 的[哈希表](https://www.geeksforgeeks.org/hashtable-in-java/)，存储数字**【0，9】**的频率。
*   初始化一个空列表，说**列出**
*   现在，对于数字 **N** 的每个数字，增加[散列表](https://www.geeksforgeeks.org/hashtable-in-java/)中该索引的计数。
*   对于数字 **N** 的每个数字，执行以下操作:
    *   检查是否是 ***拜访了***
    *   如果号码是<u>，如果其频率是 **1、**，则将该数字追加到 **<u>列表</u>** <u>中。</u>将该指标的值设为 ***<u>已访问。</u>***</u>
*   <u>[**反向列表**](https://www.geeksforgeeks.org/python-reversing-list/) **列出**并打印</u>

<u>下面是上述方法的实现:</u>

## <u>C++</u>

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print long unique elements
void printUnique(vector<long long> lis)
{

    // Reverse the list
    reverse(lis.begin(),lis.end());

    // Traverse the list
    for(long long i:lis)
        cout << i << " ";
}

// Function which check for
// all unique digits
void checkUnique(string st)
{

    // Stores the final number
    vector<long long> lis;

       // Stores the count of
    // unique digits
    long long res = 0;

    // Converting string to long longer
    // to remove leading zeros
    long long N = stoll(st);

    // Stores count of digits
    vector<long long> cnt(10, 0), cnt1(10, 0);

    // Iterate over the digits of N
    while (N > 0)
    {

        // Retrieve the last digit of N
        long long rem = N % 10;

        // Increase the count
        // of the last digit
        cnt[rem] += 1;

        // Remove the last digit of N
        N = N /10;
      }

    // Converting string to long longer again
    N = stoll(st);

    // Iterate over the digits of N
    while (N > 0)
    {

        // Retrieve the last digit of N
        long long rem = N % 10;

        // If the value of this digit
        // is not visited
        if(cnt1[rem] == 0)
        {

            // If its frequency is 1 (unique)
            if(cnt[rem] == 1)
                lis.push_back(rem);
        }

        // Mark the digit visited
        cnt1[rem] = 1;

        // Remove the last digit of N
        N = N /10;
      }

    // Passing this list to print long
    // the reversed list
    printUnique(lis);
}

// Function to concatenate array elements
void combineArray(vector<long long> lis)
{

    // Stores the concatenated number
    string st = "";

    // Traverse the array
    for (long long el : lis)
    {
        // Convert to equivalent string
        string ee = to_string(el);

        // Concatenate the string
        st = st + ee;
      }

    // Passing string to checkUnique function
    checkUnique(st);
}

// Driver Code
int main()
{
  vector<long long> arr = {122, 474, 612, 932};

  // Function call to prlong long unique
  // digits present in the
  // concatenation of array elements
  combineArray(arr);

  return 0;
}

// This code is contributed by mohit kumar 29.
```

## <u>蟒蛇 3</u>

```
# Python implementation
# of above approach

# Function to print unique elements
def printUnique(lis):

    # Reverse the list
    lis.reverse()

    # Traverse the list
    for i in lis:
        print(i, end =" ")

# Function which check for
# all unique digits
def checkUnique(string):

    # Stores the final number
    lis = []

       # Stores the count of
    # unique digits
    res = 0

    # Converting string to integer
    # to remove leading zeros
    N = int(string)

    # Stores count of digits
    cnt = [0] * 10

    # Iterate over the digits of N
    while (N > 0):

        # Retrieve the last digit of N
        rem = N % 10

        # Increase the count
        # of the last digit
        cnt[rem] += 1

        # Remove the last digit of N
        N = N // 10

    # Converting string to integer again
    N = int(string)

    # Iterate over the digits of N
    while (N > 0):

        # Retrieve the last digit of N
        rem = N % 10

        # If the value of this digit
        # is not visited
        if(cnt[rem] != 'visited'):

            # If its frequency is 1 (unique)
            if(cnt[rem] == 1):

                lis.append(rem)

        # Mark the digit visited
        cnt[rem] = 'visited'

        # Remove the last digit of N
        N = N // 10

    # Passing this list to print
    # the reversed list
    printUnique(lis)

# Function to concatenate array elements
def combineArray(lis):

    # Stores the concatenated number
    string = ""

    # Traverse the array
    for el in lis:

        # Convert to equivalent string
        el = str(el)

        # Concatenate the string
        string = string + el

    # Passing string to checkUnique function
    checkUnique(string)

# Driver Code

# Input
arr = [122, 474, 612, 932]

# Function call to print unique
# digits present in the
# concatenation of array elements
combineArray(arr)
```

## <u>java 描述语言</u>

```
<script>

// Javascript program for the above approach

// Function to print long unique elements
function printUnique(lis)
{

    // Reverse the list
    lis.reverse();

    // Traverse the list
    for(var i=0; i<lis.length; i++)
    {
        document.write(lis[i]+" ")
    }

}

// Function which check for
// all unique digits
function checkUnique(st)
{

    // Stores the final number
    var lis = [];

       // Stores the count of
    // unique digits
    var res = 0;

    // Converting string to long longer
    // to remove leading zeros
    var N = parseInt(st);

    // Stores count of digits
    var cnt = Array(10).fill(0);
    var cnt1 = Array(10).fill(0);

    // Iterate over the digits of N
    while (N > 0)
    {

        // Retrieve the last digit of N
        var rem = N % 10;

        // Increase the count
        // of the last digit
        cnt[rem] += 1;

        // Remove the last digit of N
        N = parseInt(N /10);
      }

    // Converting string to long longer again
    N = parseInt(st);

    // Iterate over the digits of N
    while (N > 0)
    {

        // Retrieve the last digit of N
        var rem = N % 10;

        // If the value of this digit
        // is not visited
        if(cnt1[rem] == 0)
        {

            // If its frequency is 1 (unique)
            if(cnt[rem] == 1)
                lis.push(rem);
        }

        // Mark the digit visited
        cnt1[rem] = 1;

        // Remove the last digit of N
        N = parseInt(N /10);
      }

    // Passing this list to print long
    // the reversed list
    printUnique(lis);
}

// Function to concatenate array elements
function combineArray(lis)
{

    // Stores the concatenated number
    var st = "";

    // Traverse the array
    for(var i =0; i< lis.length; i++)
    {
        // Convert to equivalent string
        var ee = (lis[i].toString());

        // Concatenate the string
        st = st + ee;
      }

    // Passing string to checkUnique function
    checkUnique(st);
}

// Driver Code
var arr = [122, 474, 612, 932];
// Function call to print long unique
// digits present in the
// concatenation of array elements
combineArray(arr);

</script>
```

<u>**Output:** 

```
7 6 9 3
```</u> 

<u>***时间复杂度** : O(N)*
***辅助空间:** O(N)*</u>