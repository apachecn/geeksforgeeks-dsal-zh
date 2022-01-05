# 使用 atmost 两次交换形成最大回文数

> 原文:[https://www . geesforgeks . org/form-最大-回文-数字-使用-atmat-two-swaps/](https://www.geeksforgeeks.org/form-largest-palindromic-number-using-atmost-two-swaps/)

给定一个非负回文数字 **num** 包含 **n** 位数。问题是对数字**数**最多应用两次交换操作，这样结果就是最大可能的回文数。
**举例:**

```
Input  : 4697557964
Output : 9647557469
In, 4697557964 the highlighted digits were
swapped to get the largest palindromic number 
9647557469.

Input : 54345
Output : 54345
No swapping of digits required.
```

**方法:**如果 n < 3，那么**数**本身就是最大可能的回文数。否则计算**中间**=(n/2)–1。然后创建一个大小为 **(mid + 1)** 的数组 **rightMax[]** 。 **rightMax[i]** 包含最大数字的索引，位于 **num[i]** 右侧，也大于 **num[i]** 和 0 < = i < = mid。如果不存在这样的数字，则**右最大[i]** = -1。现在，从 i = 0 到 m 遍历 **rightMax[]** 数组，找到第一个有 rightMax[i]的元素！= -1.执行**交换(num[i]、num[rightMax[i]])** 和**交换(num[n–I–1]、num[n–right max[I]–1])操作和中断。** 

## C++

```
// C++ implementation to form the largest palindromic
// number using atmost two swaps
#include <bits/stdc++.h>

using namespace std;

// function to form the largest palindromic
// number using atmost two swaps
void largestPalin(char num[], int n)
{
    // if length of number is less than '3'
    // then no higher palindromic number
    // can be formed
    if (n <= 3)
        return;

    // find the index of last digit
    // in the 1st half of 'num'
    int mid = n / 2 - 1;

    int rightMax[mid + 1], right;

    // as only the first half of 'num[]' is
    // being considered, therefore
    // for the rightmost digit in the first half
    // of 'num[]', there will be no greater right digit
    rightMax[mid] = -1;

    // index of the greatest right digit till the
    // current index from the right direction
    right = mid;

    // traverse the array from second right element
    // in the first half of 'num[]' up to the
    // left element
    for (int i = mid - 1; i >= 0; i--) {

        // if 'num[i]' is less than the greatest digit
        // encountered so far
        if (num[i] < num[right])
            rightMax[i] = right;

        else {

            // there is no greater right digit
            // for 'num[i]'
            rightMax[i] = -1;

            // update 'right' index
            right = i;
        }
    }

    // traverse the 'rightMax[]' array from left to right
    for (int i = 0; i <= mid; i++) {

        // if for the current digit, greater right digit exists
        // then swap it with its greater right digit and also
        // perform the required swap operation in the right halft
        // of 'num[]' to maintain palindromic property, then break
        if (rightMax[i] != -1) {

            // performing the required swap operations
            swap(num[i], num[rightMax[i]]);
            swap(num[n - i - 1], num[n - rightMax[i] - 1]);
            break;
        }
    }
}

// Driver program to test above
int main()
{
    char num[] = "4697557964";
    int n = strlen(num);
    largestPalin(num, n);

    // required largest palindromic number
    cout << "Largest Palindrome: "
         << num;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to form the largest palindromic
// number using atmost two swaps
class GFG
{

// function to form the largest palindromic
// number using atmost two swaps
static void largestPalin(char num[], int n)
{
    // if length of number is less than '3'
    // then no higher palindromic number
    // can be formed
    if (n <= 3)
        return;

    // find the index of last digit
    // in the 1st half of 'num'
    int mid = n / 2 - 1;

    int []rightMax = new int[mid + 1];int right;

    // as only the first half of 'num[]' is
    // being considered, therefore
    // for the rightmost digit in the first half
    // of 'num[]', there will be no greater right digit
    rightMax[mid] = -1;

    // index of the greatest right digit till the
    // current index from the right direction
    right = mid;

    // traverse the array from second right element
    // in the first half of 'num[]' up to the
    // left element
    for (int i = mid - 1; i >= 0; i--)
    {

        // if 'num[i]' is less than the greatest digit
        // encountered so far
        if (num[i] < num[right])
            rightMax[i] = right;

        else
        {

            // there is no greater right digit
            // for 'num[i]'
            rightMax[i] = -1;

            // update 'right' index
            right = i;
        }
    }

    // traverse the 'rightMax[]' array from left to right
    for (int i = 0; i <= mid; i++)
    {

        // if for the current digit, greater right digit exists
        // then swap it with its greater right digit and also
        // perform the required swap operation in the right halft
        // of 'num[]' to maintain palindromic property, then break
        if (rightMax[i] != -1)
        {

            // performing the required swap operations
            swap(num,i, rightMax[i]);
            swap(num,n - i - 1, n - rightMax[i] - 1);
            break;
        }
    }
}

static char[] swap(char []arr, int i, int j)
{
    char temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}

// Driver code
public static void main(String[] args)
{
    char num[] = "4697557964".toCharArray();
    int n = num.length;
    largestPalin(num, n);

    // required largest palindromic number
    System.out.println("Largest Palindrome: "
        + String.valueOf(num));
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python implementation to form the largest
# palindromic number using atmost two swaps

# function to form the largest palindromic
# number using atmost two swaps
def largestPalin(num, n):

    # if length of number is less than '3'
    # then no higher palindromic number
    # can be formed
    if n <= 3:
        return

    # find the index of last digit
    # in the 1st half of 'num'
    mid = n // 2 + 1

    rightMax = [0] * (mid + 1)

    # as only the first half of 'num[]' is
    # being considered, therefore
    # for the rightmost digit in the first half
    # of 'num[]', there will be no greater right digit
    rightMax[mid] = -1

    # index of the greatest right digit till the
    # current index from the right direction
    right = mid

    # traverse the array from second right element
    # in the first half of 'num[]' up to the
    # left element
    for i in range(mid-1, -1, -1):

        # if 'num[i]' is less than the greatest digit
        # encountered so far
        if num[i] < num[right]:
            rightMax[i] = right

        else:

            # there is no greater right digit
            # for 'num[i]'
            rightMax[i] = -1

            # update 'right' index
            right = i

    # traverse the 'rightMax[]' array from left to right
    for i in range(mid + 1):

        # if for the current digit, greater right digit exists
        # then swap it with its greater right digit and also
        # perform the required swap operation in the right halft
        # of 'num[]' to maintain palindromic property, then break
        if rightMax[i] != -1:

            # performing the required swap operations
            num[i], num[rightMax[i]] = num[rightMax[i]], num[i]
            num[n-i-1], num[n - rightMax[i] - 1] = num[n - rightMax[i] - 1], num[n - i - 1]
            break

# Driver Code
if __name__ == "__main__":
    num = "4697557964"
    n = len(num)

    # Required as string object do not
    # support item assignment
    num = list(num)
    largestPalin(num, n)

    # making string again from list
    num = ''.join(num)
    print("Largest Palindrome: ",num)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation to form the largest
// palindromic number using atmost two swaps
using System;

class GFG
{

// function to form the largest palindromic
// number using atmost two swaps
static void largestPalin(char []num, int n)
{
    // if length of number is less than '3'
    // then no higher palindromic number
    // can be formed
    if (n <= 3)
        return;

    // find the index of last digit
    // in the 1st half of 'num'
    int mid = n / 2 - 1;

    int []rightMax = new int[mid + 1]; int right;

    // as only the first half of 'num[]' is
    // being considered, therefore
    // for the rightmost digit in the first half
    // of 'num[]', there will be no greater right digit
    rightMax[mid] = -1;

    // index of the greatest right digit till the
    // current index from the right direction
    right = mid;

    // traverse the array from second right element
    // in the first half of 'num[]' up to the
    // left element
    for (int i = mid - 1; i >= 0; i--)
    {

        // if 'num[i]' is less than the greatest
        // digit encountered so far
        if (num[i] < num[right])
            rightMax[i] = right;

        else
        {

            // there is no greater right digit
            // for 'num[i]'
            rightMax[i] = -1;

            // update 'right' index
            right = i;
        }
    }

    // traverse the 'rightMax[]' array
    // from left to right
    for (int i = 0; i <= mid; i++)
    {

        // if for the current digit, greater right
        // digit exists then swap it with its greater
        // right digit and also perform the required
        // swap operation in the right half of 'num[]'
        // to maintain palindromic property, then break
        if (rightMax[i] != -1)
        {

            // performing the required swap operations
            swap(num, i, rightMax[i]);
            swap(num, n - i - 1, n - rightMax[i] - 1);
            break;
        }
    }
}

static char[] swap(char []arr, int i, int j)
{
    char temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}

// Driver code
public static void Main(String[] args)
{
    char []num = "4697557964".ToCharArray();
    int n = num.Length;
    largestPalin(num, n);

    // required largest palindromic number
    Console.WriteLine("Largest Palindrome: " +
                        String.Join("", num));
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation to form the largest palindromic
// number using atmost two swaps

// function to form the largest palindromic
// number using atmost two swaps
function largestPalin(num,n)
{
    // if length of number is less than '3'
    // then no higher palindromic number
    // can be formed
    if (n <= 3)
        return;

    // find the index of last digit
    // in the 1st half of 'num'
    let mid = Math.floor(n / 2) - 1;

    let rightMax = new Array(mid + 1);
    let right;

    // as only the first half of 'num[]' is
    // being considered, therefore
    // for the rightmost digit in the first half
    // of 'num[]', there will be no greater right digit
    rightMax[mid] = -1;

    // index of the greatest right digit till the
    // current index from the right direction
    right = mid;

    // traverse the array from second right element
    // in the first half of 'num[]' up to the
    // left element
    for (let i = mid - 1; i >= 0; i--)
    {

        // if 'num[i]' is less than the greatest digit
        // encountered so far
        if (num[i] < num[right])
            rightMax[i] = right;

        else
        {

            // there is no greater right digit
            // for 'num[i]'
            rightMax[i] = -1;

            // update 'right' index
            right = i;
        }
    }

    // traverse the 'rightMax[]' array from left to right
    for (let i = 0; i <= mid; i++)
    {

        // if for the current digit, greater right digit exists
        // then swap it with its greater right digit and also
        // perform the required swap operation in the right halft
        // of 'num[]' to maintain palindromic property, then break
        if (rightMax[i] != -1)
        {

            // performing the required swap operations
            swap(num,i, rightMax[i]);
            swap(num,n - i - 1, n - rightMax[i] - 1);
            break;
        }
    }
}

function swap(arr,i,j)
{
    let temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}

// Driver code
let num = "4697557964".split("");
let n = num.length;
largestPalin(num, n);

// required largest palindromic number
document.write("Largest Palindrome: "
        + (num).join(""));

// This code is contributed by rag2127

</script>
```

**输出:**

```
Largest Palindrome: 9647557469
```

**时间复杂度:** O(n)。
**辅助空间:** O(n)。