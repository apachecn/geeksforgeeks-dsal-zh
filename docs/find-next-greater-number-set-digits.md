# 用相同的数字组找到下一个更大的数字

> 原文:[https://www . geeksforgeeks . org/find-next-better-number-set-digits/](https://www.geeksforgeeks.org/find-next-greater-number-set-digits/)

给定一个数字 n，找出与 n 有相同数字集且大于 n 的最小数字。如果 n 是其数字集的最大可能数，则打印“不可能”。

示例:
为了实现简单，我们将输入数字视为字符串。

```
Input:  n = "218765"
Output: "251678"

Input:  n = "1234"
Output: "1243"

Input: n = "4321"
Output: "Not Possible"

Input: n = "534976"
Output: "536479"
```

以下是对下一个更大数字的一些观察。
1)如果所有数字按降序排序，那么输出总是“不可能”。比如 4321。
2)如果所有数字都按升序排序，那么我们需要交换最后两位数字。比如 1234。
3)对于其他情况，我们需要从最右侧处理数字(为什么？因为我们需要找到所有更大数字中最小的一个)

你现在可以尝试自己开发一个算法。
下面是寻找下一个更大数字的算法。
**I)** 从最右边的数字开始遍历给定的数字，继续遍历，直到找到一个比之前遍历的数字小的数字。例如，如果输入的数字是“534976”，我们会在 **4** 处停止，因为 4 比下一个数字 9 小。如果我们找不到这样的数字，那么输出就是“不可能”。

**II)** 现在在上面找到的数字‘d’的右侧搜索大于‘d’的最小数字。对于“53 **4** 976”，4 的右侧包含“976”。大于 4 的最小数字是 **6** 。

**III)** 互换上面找到的两位数，我们得到上面例子中的 53 **6** 97 **4** 。

**IV)** 现在将所有数字从“d”旁边的位置排序到数字的末尾。排序后得到的数字就是输出。例如，我们用粗体 536 **974** 对数字进行排序。我们得到“536 **479** ”，这是输入 534976 的下一个更大的数字。

以下是上述方法的实现。

## C++

```
// C++ program to find the smallest number which greater than a given number
// and has same set of digits as given number
#include <iostream>
#include <cstring>
#include <algorithm>
using namespace std;

// Utility function to swap two digits
void swap(char *a, char *b)
{
    char temp = *a;
    *a = *b;
    *b = temp;
}

// Given a number as a char array number[], this function finds the
// next greater number.  It modifies the same array to store the result
void findNext(char number[], int n)
{
    int i, j;

    // I) Start from the right most digit and find the first digit that is
    // smaller than the digit next to it.
    for (i = n-1; i > 0; i--)
        if (number[i] > number[i-1])
           break;

    // If no such digit is found, then all digits are in descending order
    // means there cannot be a greater number with same set of digits
    if (i==0)
    {
        cout << "Next number is not possible";
        return;
    }

    // II) Find the smallest digit on right side of (i-1)'th digit that is
    // greater than number[i-1]
    int x = number[i-1], smallest = i;
    for (j = i+1; j < n; j++)
        if (number[j] > x && number[j] < number[smallest])
            smallest = j;

    // III) Swap the above found smallest digit with number[i-1]
    swap(&number[smallest], &number[i-1]);

    // IV) Sort the digits after (i-1) in ascending order
    sort(number + i, number + n);

    cout << "Next number with same set of digits is " << number;

    return;
}

// Driver program to test above function
int main()
{
    char digits[] = "534976";
    int n = strlen(digits);
    findNext(digits, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find next greater
// number with same set of digits.
import java.util.Arrays;

public class nextGreater
{
    // Utility function to swap two digit
    static void swap(char ar[], int i, int j)
    {
        char temp = ar[i];
        ar[i] = ar[j];
        ar[j] = temp;
    }

    // Given a number as a char array number[],
    // this function finds the next greater number.
    // It modifies the same array to store the result
    static void findNext(char ar[], int n)
    {
        int i;

        // I) Start from the right most digit
        // and find the first digit that is smaller
        // than the digit next to it.
        for (i = n - 1; i > 0; i--)
        {
            if (ar[i] > ar[i - 1]) {
                break;
            }
        }

        // If no such digit is found, then all
        // digits are in descending order means
        // there cannot be a greater number with
        // same set of digits
        if (i == 0)
        {
            System.out.println("Not possible");
        }
        else
        {
            int x = ar[i - 1], min = i;

            // II) Find the smallest digit on right
            // side of (i-1)'th digit that is greater
            // than number[i-1]
            for (int j = i + 1; j < n; j++)
            {
                if (ar[j] > x && ar[j] < ar[min])
                {
                    min = j;
                }
            }

            // III) Swap the above found smallest
            // digit with number[i-1]
            swap(ar, i - 1, min);

            // IV) Sort the digits after (i-1)
            // in ascending order
            Arrays.sort(ar, i, n);
            System.out.print("Next number with same" +
                                    " set of digits is ");
            for (i = 0; i < n; i++)
                System.out.print(ar[i]);
        }
    }

    public static void main(String[] args)
    {
        char digits[] = { '5','3','4','9','7','6' };
        int n = digits.length;
        findNext(digits, n);
    }
}
```

## 计算机编程语言

```
# Python program to find the smallest number which
# is greater than a given no. has same set of
# digits as given number

# Given number as int array, this function finds the
# greatest number and returns the number as integer
def findNext(number,n):

     # Start from the right most digit and find the first
     # digit that is smaller than the digit next to it
     for i in range(n-1,0,-1):
         if number[i] > number[i-1]:
             break

     # If no such digit found,then all numbers are in
     # descending order, no greater number is possible
     if i == 1 and number[i] <= number[i-1]:
         print "Next number not possible"
         return

     # Find the smallest digit on the right side of
     # (i-1)'th digit that is greater than number[i-1]
     x = number[i-1]
     smallest = i
     for j in range(i+1,n):
         if number[j] > x and number[j] < number[smallest]:
             smallest = j

     # Swapping the above found smallest digit with (i-1)'th
     number[smallest],number[i-1] = number[i-1], number[smallest]

     # X is the final number, in integer datatype
     x = 0
     # Converting list upto i-1 into number
     for j in range(i):
         x = x * 10 + number[j]

     # Sort the digits after i-1 in ascending order
     number = sorted(number[i:])
     # converting the remaining sorted digits into number
     for j in range(n-i):
         x = x * 10 + number[j]

     print "Next number with set of digits is",x

# Driver Program to test above function
digits = "534976"        

# converting into integer array,
# number becomes [5,3,4,9,7,6]
number = map(int ,digits)
findNext(number, len(digits))

# This code is contributed by Harshit Agrawal
```

## C#

```
// C# program to find next greater
// number with same set of digits.
using System;

public class nextGreater
{
    // Utility function to swap two digit
    static void swap(char []ar, int i, int j)
    {
        char temp = ar[i];
        ar[i] = ar[j];
        ar[j] = temp;
    }

    // Given a number as a char array number[],
    // this function finds the next greater number.
    // It modifies the same array to store the result
    static void findNext(char []ar, int n)
    {
        int i;

        // I) Start from the right most digit
        // and find the first digit that is smaller
        // than the digit next to it.
        for (i = n - 1; i > 0; i--)
        {
            if (ar[i] > ar[i - 1])
            {
                break;
            }
        }

        // If no such digit is found, then all
        // digits are in descending order means
        // there cannot be a greater number with
        // same set of digits
        if (i == 0)
        {
            Console.WriteLine("Not possible");
        }
        else
        {
            int x = ar[i - 1], min = i;

            // II) Find the smallest digit on right
            // side of (i-1)'th digit that is greater
            // than number[i-1]
            for (int j = i + 1; j < n; j++)
            {
                if (ar[j] > x && ar[j] < ar[min])
                {
                    min = j;
                }
            }

            // III) Swap the above found smallest
            // digit with number[i-1]
            swap(ar, i - 1, min);

            // IV) Sort the digits after (i-1)
            // in ascending order
            Array.Sort(ar, i, n-i);
            Console.Write("Next number with same" +
                                    " set of digits is ");
            for (i = 0; i < n; i++)
                Console.Write(ar[i]);
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        char []digits = { '5','3','4','9','7','6' };
        int n = digits.Length;
        findNext(digits, n);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to find the
// smallest number which is greater
// than a given no. has same set of
// digits as given number

// Given number as int array, this
// function finds the greatest number
// and returns the number as integer
function findNext(number, n)
{

    // Start from the right most digit
    // and find the first digit that is
    // smaller than the digit next to it
    for(var i = n - 1; i >= 0; i--)
    {
        if (number[i] > number[i - 1])
            break;
    }

    // If no such digit found,then all
    // numbers are in descending order,
    // no greater number is possible
    if (i == 1 && number[i] <= number[i - 1])
    {
        document.write("Next number not possible");
        return;
    }  

    // Find the smallest digit on the
    // right side of (i-1)'th digit
    // that is greater than number[i-1]
    let x = number[i - 1];
    let smallest = i;

    for(let j = i + 1; j < n; j++)
    {
        if (number[j] > x &&
            number[j] < number[smallest])
        smallest = j;
    }

    // Swapping the above found smallest
    // digit with (i-1)'th
    let temp = number[smallest];
    number[smallest] = number[i - 1];
    number[i - 1] = temp;

    // X is the final number, in integer datatype
    x = 0

    // Converting list upto i-1 into number
    for(let j = 0; j < i; j++)
        x = x * 10 + number[j];

    // Sort the digits after i-1 in ascending order
    number = number.slice(i, number.length + 1);
    number.sort()

    // Converting the remaining sorted
    // digits into number
    for(let j = 0; j < n - i; j++)
        x = x * 10 + number[j];

    document.write("Next number with " +
                   "set of digits is " + x);
}

// Driver code
let digits = "534976"      

// Converting into integer array,
// number becomes [5,3,4,9,7,6]
let number = []
for(let i = 0; i < digits.length; i++)
    number[i] = Number(digits[i]);

findNext(number, digits.length);

// This code is contributed by rohan07

</script>
```

**Output**

```
Next number with same set of digits is 536479
```

**时间复杂度:** O(N*logN)
**辅助空间:** O(1)

上述实现可以通过以下方式进行优化。
1)我们可以用第二步的二分搜索法代替线性搜索。
2)第四步，不用做简单的排序，可以应用一些巧妙的技巧在线性时间内完成。提示:我们知道除了一个被交换的数字外，所有的数字都是按逆序线性排序的。
通过以上优化，可以说该方法的时间复杂度为 O(n)。

**优化方法:**

1.这里，我们不是对(i-1)索引后的数字进行排序，而是按照上述优化点所述对数字进行反转。
2。由于它们将按降序排列，因此为了从正确的部分找到可能的最小元素，我们只需反转它们，从而降低时间复杂度。

下面是上述方法的实现:

## C++14

```
#include <bits/stdc++.h>
using namespace std;

vector<int> nextPermutation(int n, vector<int> arr)
{
    // If number of digits is 1 then just return the vector
    if (n == 1)
        return arr;

    // Start from the right most digit and find the first
    // digit that is
    // smaller than the digit next to it.
    int i = 0;
    for (i = n - 1; i > 0; i--) {
        if (arr[i] > arr[i - 1])
            break;
    }

    // If there is a possibility of a next greater element
    if (i != 0) {
        // Find the smallest digit on right side of (i-1)'th
        // digit that is
        // greater than number[i-1]
        for (int j = n - 1; j >= i; j--) {
            if (arr[i - 1] < arr[j]) {
                // Swap the found smallest digit i.e. arr[j]
                // with arr[i-1]
                swap(arr[i - 1], arr[j]);
                break;
            }
        }
    }

    // Reverse the digits after (i-1) because the digits
    // after (i-1) are in decreasing order and thus we will
    // get the smallest element possible from these digits
    reverse(arr.begin() + i, arr.end());

    // If i is 0 that means elements are in decreasing order
    // Therefore, no greater element possible then we just
    // return the lowest possible
    // order/element formed from these digits by just
    // reversing the vector

    return arr;
}

int main()
{
    int n = 6;
    vector<int> v{ 5,3,4,9,7,6 };
    vector<int> res;
    res = nextPermutation(n, v);
    for (int i = 0; i < res.size(); i++) {
        cout << res[i] << " ";
    }
}
```

## 蟒蛇 3

```
# A python program to find the next greatest number
def nextPermutation(arr):

      # find the length of the array
    n = len(arr)

    # start from the right most digit and find the first
    # digit that is smaller than the digit next to it.
    k = n - 2
    while k >= 0:
        if arr[k] < arr[k + 1]:
            break
        k -= 1

    # reverse the list if the digit that is smaller than the
    # digit next to it is not found.
    if k < 0:
        arr = arr[::-1]
    else:

          # find the first greatest element than arr[k] from the
        # end of the list
        for l in range(n - 1, k, -1):
            if arr[l] > arr[k]:
                break

        # swap the elements at arr[k] and arr[l     
        arr[l], arr[k] = arr[k], arr[l]

        # reverse the list from k + 1 to the end to find the
        # most nearest greater number to the given input number
        arr[k + 1:] = reversed(arr[k + 1:])

    return arr

# Driver code
arr = [5, 3, 4, 9, 7, 6]
print(*nextPermutation(arr))

# This code is contributed by Manish Thapa
```

## java 描述语言

```
<script>

function nextPermutation(n, arr)
{
    // If number of digits is 1 then just return the vector
    if (n == 1)
        return arr;

    // Start from the right most digit and find the first
    // digit that is
    // smaller than the digit next to it.
    let i = 0;
    for (i = n - 1; i > 0; i--) {
        if (arr[i] > arr[i - 1])
            break;
    }

    // If there is a possibility of a next greater element
    if (i != 0)
    {

        // Find the smallest digit on right side of (i-1)'th
        // digit that is
        // greater than number[i-1]
        for (let j = n - 1; j >= i; j--)
        {
            if (arr[i - 1] < arr[j])
            {
                // Swap the found smallest digit i.e. arr[j]
                // with arr[i-1]

                let temp = arr[i - 1];
                arr[i - 1] = arr[j];
                arr[j] = temp;
                break;
            }
        }
    }

    // Reverse the digits after (i-1) because the digits
    // after (i-1) are in decreasing order and thus we will
    // get the smallest element possible from these digits
    arr = arr.slice(0,i).concat(arr.slice(i,arr.length).reverse());

    // If i is 0 that means elements are in decreasing order
    // Therefore, no greater element possible then we just
    // return the lowest possible
    // order/element formed from these digits by just
    // reversing the vector
    return arr;
}

let v = [5,3,4,9,7,6];
let n = 6;
let res = nextPermutation(n, v);
for (let i = 0; i < res.length; i++) {
    document.write(res[i] + " ")
}

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output**

```
5 3 6 4 7 9 
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)

本文由**拉胡尔·贾恩**供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息