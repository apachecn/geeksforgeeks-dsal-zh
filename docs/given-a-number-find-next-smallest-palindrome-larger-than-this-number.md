# 给定一个数字，找到下一个最小的回文

> 原文:[https://www . geesforgeks . org/给定一个数字-查找下一个最小的回文-大于这个数字/](https://www.geeksforgeeks.org/given-a-number-find-next-smallest-palindrome-larger-than-this-number/)

给定一个数，找出比这个数大的下一个最小的回文。例如，如果输入数字是“2 3 5 4 5”，则输出应该是“2 3 6 3 2”。如果输入数字是“9 9 9”，输出应该是“1 0 0 1”。
假设输入是一个数组。数组中的每个条目代表输入数字中的一个数字。让数组为“num[]”，数组大小为“n”

可能有三种不同类型的输入需要分别处理。
**1)** 输入的数字是回文，全是 9。比如“9 9 9”。输出应为“1 0 0 1”
**2)**输入的数字不是回文。例如“1 2 3 4”。输出应该是“1 3 3 1”
**3)**输入的数字是回文，不全是 9。例如“1 2 2 1”。输出应该是“1 3 3 1”。

输入类型 1 的解决方案很简单。输出包含 n + 1 个数字，其中角位数字为 1，角位数字之间的所有数字均为 0。
现在我们先来说说输入类型 2 和 3。如何将给定的数字转换成更大的回文？为了理解解决方案，让我们首先定义以下两个术语:

*左侧:*给定数字的左半部分。“1 2 3 4 5 6”的左侧是“1 2 3”，而“1 2 3 4 5”的左侧是“1 2”

*右侧:*给定数字的右半部分。“1 2 3 4 5 6”的右侧是“4 5 6”，而“1 2 3 4 5”的右侧是“4 5”

要转换成回文，我们可以取其左侧的镜像，也可以取其右侧的镜像。然而，如果我们取右边的镜子，那么这样形成的回文不一定会是下一个更大的回文。所以，我们必须把左边的镜子复制到右边。但是有些案件必须以不同的方式处理。请参见以下步骤。
我们将从两个索引 I 和 j. i 开始，指向两个中间元素(或者在 n 为奇数的情况下，指向中间元素周围的两个元素)。我们一个接一个地把 I 和 j 移开。

**第一步。**最初，忽略左侧与右侧对应部分相同的部分。例如，如果数字是“8 3 **4 2 2 4** 6 9”，我们忽略中间的四个元素。我现在指向元素 3，j 现在指向元素 6。

**第二步。**第 1 步后，出现以下情况:
**情况 1:** 指数 i & j 越界。
输入数字为回文时出现这种情况。在这种情况下，我们只需在中间的数字上加 1(或者在 n 为偶数的情况下加数字)，将进位传播到左侧的 MSB 数字，同时将左侧的镜像复制到右侧。
例如，如果给定的数是“1 2 9 2 1”，我们将 9 增加到 10 并传播进位。所以数字变成了“1 3 0 3 1”

**情况 2:** 左侧和右侧之间留有不相同的数字。所以，我们只需将左侧镜像到右侧&尽量减少形成的数字，以保证下一个最小的回文。
在这种情况下，可以有**两个子例**。

**2.1)** 将左侧复制到右侧就足够了，我们不需要增加任何数字，结果只是左侧的镜像。下面是这个子案例的一些例子。
下一个回文为“7 **8** 3 3 2 2”是“7 8 3 8 7”
下一个回文为“1 2 **5** 3 2”是“1 2 5 5 2 1”
下一个回文为“1 4 **5** 8 7 6 7 8 3 2”是“1 4 5 8 7 7 8 5 4 1”
如何检查这个子例？我们只需要检查第 1 步中被忽略部分后面的数字。这个数字在上面的例子中突出显示。如果这个数字大于右侧数字中对应的数字，那么将左侧复制到右侧就足够了，我们不需要做任何其他事情。

**2.2)** 将左侧复制到右侧是不够的。当上面定义的左边数字较小时，就会出现这种情况。以下是这种情况的一些例子。
下一个回文为“7 **1** 3 3 2 2”是“7 1 4 4 1 7”
下一个回文为“1 2 **3** 4 6 2 8”是“1 2 3 5 3 2 1”
下一个回文为“9 4 **1** 8 7 9 7 8 3 2”是“9 4 1 8 8 0 8 1 4 9”
我们像处理案例 1 一样处理这个子案例。我们只需在中间的数字(或 n 为偶数时的数字)上加 1，将进位向左侧的 MSB 数字传播，同时将左侧的镜像复制到右侧。

**方法 1:** 寻找下一个最小回文数的基本方法。

## C++

```
#include <bits/stdc++.h>
using namespace std;
// Function to check whether number is palindrome or not
int isPalindrome(int num)
{
    // Declaring variables
    int n, k, rev = 0;
    // storing num in n so that we can compare it later
    n = num;
    // while num is not 0 we find its reverse and store in
    // rev
    while (num != 0) {
        k = num % 10;
        rev = (rev * 10) + k;
        num = num / 10;
    }
    // check if num and its reverse are same
    if (n == rev) {
        return 1;
    }
    else {
        return 0;
    }
}
int main()
{
    // Take any number to find its next palindrome number
    int num = 9687;
    // If number is not Palindrome we go to the next number
    // using while loop
    while (!isPalindrome(num)) {
        num = num + 1;
    }
    // now we get the next Palindrome so let's print it
    cout << "Next Palindrome :";
    cout << num;
    return 0;
}
// Contribute by :- Tejas Bhavsar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;

class GFG
{

    // Function to check whether number is palindrome or not
    static int isPalindrome(int num)
    {

        // Declaring variables
        int n, k, rev = 0;

        // storing num in n so that we can compare it later
        n = num;

        // while num is not 0 we find its reverse and store
        // in rev
        while (num != 0) {
            k = num % 10;
            rev = (rev * 10) + k;
            num = num / 10;
        }

        // check if num and its reverse are same
        if (n == rev) {
            return 1;
        }
        else {
            return 0;
        }
    }

  // Driver code
    public static void main(String[] args)
    {

        // Take any number to find its next palindrome
        // number
        int num = 9687;

        // If number is not Palindrome we go to the next
        // number using while loop
        while (isPalindrome(num) == 0) {
            num = num + 1;
        }

        // now we get the next Palindrome so let's print it
        System.out.print("Next Palindrome :");
        System.out.print(num);
    }
}

// This code is contributed by subhammahato348.
```

## 计算机编程语言

```
# Program to print find next palindrome
# number greater than given number.

# function to check a number is
# palindrome or not
def isPalindrome(num):

  # Declaring variables

  # storing num in n so that we can compare it later
    n = num
    rev = 0

    # while num is not 0 we find its reverse and store
    # in rev
    while (num > 0):
        k = num % 10
        rev = (rev * 10) + k
        num = num / 10

    # check if num and its reverse are same
    if (n == rev):
        return True
    else:
        return False

# input number
num = 9687

# start check from next num;
num = num + 1

# Loop checks all numbers from given no.
# (num + 1) to next palindrome no.
while (True):
    if (isPalindrome(num)):
        break
    num = num + 1

# printing the next palindrome
print("Next Palindrome :")
print(num)

# This code is contributed by sidharthsingh7898.
```

## C#

```
using System;
class GFG {

    // Function to check whether number is palindrome or not
    static int isPalindrome(int num)
    {

        // Declaring variables
        int n, k, rev = 0;

        // storing num in n so that we can compare it later
        n = num;

        // while num is not 0 we find its reverse and store
        // in rev
        while (num != 0) {
            k = num % 10;
            rev = (rev * 10) + k;
            num = num / 10;
        }

        // check if num and its reverse are same
        if (n == rev) {
            return 1;
        }
        else {
            return 0;
        }
    }

    // Driver code
    public static void Main()
    {

        // Take any number to find its next palindrome
        // number
        int num = 9687;

        // If number is not Palindrome we go to the next
        // number using while loop
        while (isPalindrome(num) == 0) {
            num = num + 1;
        }

        // now we get the next Palindrome so let's print it
        Console.Write("Next Palindrome :");
        Console.Write(num);
    }
}

// This code is contributed by subhammahato348.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

    // Function to check whether number is palindrome or not
    function isPalindrome(num)
    {

        // Declaring variables
        let n, k, rev = 0;

        // storing num in n so that we can compare it later
        n = num;

        // while num is not 0 we find its reverse and store
        // in rev
        while (num != 0) {
            k = num % 10;
            rev = (rev * 10) + k;
            num = Math.floor(num / 10);
        }

        // check if num and its reverse are same
        if (n == rev) {
            return 1;
        }
        else {
            return 0;
        }
    }

// Driver Code

    // Take any number to find its next palindrome
        // number
        let num = 9687;

        // If number is not Palindrome we go to the next
        // number using while loop
        while (isPalindrome(num) == 0) {
            num = num + 1;
        }

        // now we get the next Palindrome so let's prlet it
        document.write("Next Palindrome :");
        document.write(num);

// This code is contributed by splevel62.
</script>
```

**Output**

```
Next Palindrome :9779
```

***时间复杂度:** O(num * |num|)*

## C++

```
#include <iostream>
using namespace std;

// Utility that prints out an array on a line
void printArray(int arr[], int n)
{
    int i;
    for(i = 0; i < n; i++)
        printf("%d ", arr[i]);

    printf("\n");
}

// A utility function to check if num has all 9s
int AreAll9s(int* num, int n )
{
    int i;
    for(i = 0; i < n; ++i)
        if (num[i] != 9)
            return 0;

    return 1;
}

// Returns next palindrome of a given number num[].
// This function is for input type 2 and 3
void generateNextPalindromeUtil (int num[], int n )
{

    // Find the index of mid digit
    int mid = n / 2;

    // A bool variable to check if copy of left
    // side to right is sufficient or not
    bool leftsmaller = false;

    // End of left side is always 'mid -1'
    int i = mid - 1;

    // Beginning of right side depends
    // if n is odd or even
    int j = (n % 2) ? mid + 1 : mid;

   // Initially, ignore the middle same digits
    while (i >= 0 && num[i] == num[j])
        i--, j++;

    // Find if the middle digit(s) need to be
    // incremented or not (or copying left
    // side is not sufficient)
    if (i < 0 || num[i] < num[j])
        leftsmaller = true;

    // Copy the mirror of left to tight
    while (i >= 0)
    {
        num[j] = num[i];
        j++;
        i--;
    }

    // Handle the case where middle digit(s) must
    // be incremented. This part of code is for
    // CASE 1 and CASE 2.2
    if (leftsmaller == true)
    {
        int carry = 1;
        i = mid - 1;

        // If there are odd digits, then increment
        // the middle digit and store the carry
        if (n % 2 == 1)
        {
            num[mid] += carry;
            carry = num[mid] / 10;
            num[mid] %= 10;
            j = mid + 1;
        }
        else
            j = mid;

        // Add 1 to the rightmost digit of the
        // left side, propagate the carry towards
        // MSB digit and simultaneously copying
        // mirror of the left side to the right side.
        while (i >= 0)
        {
            num[i] += carry;
            carry = num[i] / 10;
            num[i] %= 10;

            // Copy mirror to right
            num[j++] = num[i--];
        }
    }
}

// The function that prints next palindrome
// of a given number num[] with n digits.
void generateNextPalindrome(int num[], int n)
{
    int i;

    printf("Next palindrome is:");

    // Input type 1: All the digits are 9, simply o/p 1
    // followed by n-1 0's followed by 1.
    if (AreAll9s(num, n))
    {
        printf("1 ");
        for(i = 1; i < n; i++)
            printf("0 ");

        printf("1");
    }

    // Input type 2 and 3
    else
    {
        generateNextPalindromeUtil(num, n);

        // print the result
        printArray (num, n);
    }
}

// Driver code
int main()
{
    int num[] = { 9, 4, 1, 8, 7, 9, 7, 8, 3, 2, 2 };

    int n = sizeof(num) / sizeof(num[0]);

    generateNextPalindrome(num, n);

    return 0;
}

// This code is contributed by rohan07
```

## C

```
#include <stdio.h>

// A utility function to print an array
void printArray (int arr[], int n);

// A utility function to check if num has all 9s
int AreAll9s (int num[], int n );

// Returns next palindrome of a given number num[].
// This function is for input type 2 and 3
void generateNextPalindromeUtil (int num[], int n )
{
    // find the index of mid digit
    int mid = n/2;

    // A bool variable to check if copy of left side to right is sufficient or not
    bool leftsmaller = false;

    // end of left side is always 'mid -1'
    int i = mid - 1;

    // Beginning of right side depends if n is odd or even
    int j = (n % 2)? mid + 1 : mid;

   // Initially, ignore the middle same digits
    while (i >= 0 && num[i] == num[j])
        i--,j++;

    // Find if the middle digit(s) need to be incremented or not (or copying left
    // side is not sufficient)
    if ( i < 0 || num[i] < num[j])
        leftsmaller = true;

    // Copy the mirror of left to tight
    while (i >= 0)
    {
        num[j] = num[i];
        j++;
        i--;
    }

    // Handle the case where middle digit(s) must be incremented.
    // This part of code is for CASE 1 and CASE 2.2
    if (leftsmaller == true)
    {
        int carry = 1;
        i = mid - 1;

        // If there are odd digits, then increment
        // the middle digit and store the carry
        if (n%2 == 1)
        {
            num[mid] += carry;
            carry = num[mid] / 10;
            num[mid] %= 10;
            j = mid + 1;
        }
        else
            j = mid;

        // Add 1 to the rightmost digit of the left side, propagate the carry
        // towards MSB digit and simultaneously copying mirror of the left side
        // to the right side.
        while (i >= 0)
        {
            num[i] += carry;
            carry = num[i] / 10;
            num[i] %= 10;
            num[j++] = num[i--]; // copy mirror to right
        }
    }
}

// The function that prints next palindrome of a given number num[]
// with n digits.
void generateNextPalindrome( int num[], int n )
{
    int i;

    printf("Next palindrome is:");

    // Input type 1: All the digits are 9, simply o/p 1
    // followed by n-1 0's followed by 1.
    if( AreAll9s( num, n ) )
    {
        printf( "1 ");
        for( i = 1; i < n; i++ )
            printf( "0 " );
        printf( "1" );
    }

    // Input type 2 and 3
    else
    {
        generateNextPalindromeUtil ( num, n );

        // print the result
        printArray (num, n);
    }
}

// A utility function to check if num has all 9s
int AreAll9s( int* num, int n )
{
    int i;
    for( i = 0; i < n; ++i )
        if( num[i] != 9 )
            return 0;
    return 1;
}

/* Utility that prints out an array on a line */
void printArray(int arr[], int n)
{
    int i;
    for (i=0; i < n; i++)
        printf("%d ", arr[i]);
    printf("\n");
}

// Driver Program to test above function
int main()
{
    int num[] = {9, 4, 1, 8, 7, 9, 7, 8, 3, 2, 2};

    int n = sizeof (num)/ sizeof(num[0]);

    generateNextPalindrome( num, n );

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find next smallest
// palindrome

public class nextplaindrome
{
    // Returns next palindrome of a given
    // number num[]. This function is for
    // input type 2 and 3
    static void generateNextPalindromeUtil(int num[], int n)
    {
        int mid = n / 2;

        // end of left side is always 'mid -1'
        int i = mid - 1;

        // Beginning of right side depends
        // if n is odd or even
        int j = (n % 2 == 0) ? mid : mid + 1;

        // A bool variable to check if copy of left
        // side to right
        // is sufficient or not
        boolean leftsmaller = false;

        // Initially, ignore the middle same digits
        while (i >= 0 && num[i] == num[j])
        {
            i--;
            j++;
        }

        // Find if the middle digit(s) need to
        // be incremented or not (or copying left
        // side is not sufficient)
        if (i < 0 || num[i] < num[j])
        {
            leftsmaller = true;
        }

        // Copy the mirror of left to tight
        while (i >= 0)
        {
            num[j++] = num[i--];
        }

        // Handle the case where middle digit(s)
        // must be incremented. This part of code
        // is for CASE 1 and CASE 2.2
        if (leftsmaller)
        {
            int carry = 1;

            // If there are odd digits, then increment
            // the middle digit and store the carry
            if (n % 2 == 1) {
                num[mid] += 1;
                carry = num[mid] / 10;
                num[mid] %= 10;
            }
            i = mid - 1;
            j = (n % 2 == 0 ? mid : mid + 1);

            // Add 1 to the rightmost digit of the left
            // side, propagate the carry towards MSB digit
            // and simultaneously copying mirror of the
            // left side to the right side.
            //when carry is zero no need to loop through till i>=0
            while (i >= 0 && carry>0) 
            {
                num[i] = num[i] + carry;
                carry = num[i] / 10;
                num[i] %= 10;
                num[j] = num[i];// copy mirror to right
                i--;
                j++;
            }

        }
    }

    // The function that prints next palindrome
    // of a given number num[] with n digits.
    static void generateNextPalindrome(int num[], int n)
    {
        System.out.println("Next Palindrome is:");

        // Input type 1: All the digits are 9,
        // simply o/p 1 followed by n-1 0's
        // followed by 1.
        if (isAll9(num, n)) {
            System.out.print("1");
            for (int i = 0; i < n - 1; i++)
                System.out.print("0");
            System.out.println("1");

        }

        // Input type 2 and 3
        else {
            generateNextPalindromeUtil(num, n);
            printarray(num);
        }
    }

    // A utility function to check if num has all 9s
    static boolean isAll9(int num[], int n) {
        for (int i = 0; i < n; i++)
            if (num[i] != 9)
                return false;
        return true;
    }

    /* Utility that prints out an array on a line */
    static void printarray(int num[]) {
        for (int i = 0; i < num.length; i++)
            System.out.print(num[i]);
        System.out.println();
    }

    public static void main(String[] args)
    {
        int num[] = { 9, 4, 1, 8, 7, 9, 7, 8, 3, 2, 2 };
        generateNextPalindrome(num, num.length);
    }
}
```

## 蟒蛇 3

```
# Returns next palindrome of a given number num[].
# This function is for input type 2 and 3
def generateNextPalindromeUtil (num, n) :

    # find the index of mid digit
    mid = int(n/2 )

    # A bool variable to check if copy of left
    # side to right is sufficient or not
    leftsmaller = False

    # end of left side is always 'mid -1'
    i = mid - 1

    # Beginning of right side depends
    # if n is odd or even
    j = mid + 1 if (n % 2) else mid

    # Initially, ignore the middle same digits
    while (i >= 0 and num[i] == num[j]) :
        i-=1
        j+=1

    # Find if the middle digit(s) need to be
    # incremented or not (or copying left
    # side is not sufficient)
    if ( i < 0 or num[i] < num[j]):
        leftsmaller = True

    # Copy the mirror of left to tight
    while (i >= 0) :

        num[j] = num[i]
        j+=1
        i-=1

    # Handle the case where middle
    # digit(s) must be incremented.
    # This part of code is for CASE 1 and CASE 2.2
    if (leftsmaller == True) :

        carry = 1
        i = mid - 1

        # If there are odd digits, then increment
        # the middle digit and store the carry
        if (n%2 == 1) :

            num[mid] += carry
            carry = int(num[mid] / 10 )
            num[mid] %= 10
            j = mid + 1

        else:
            j = mid

        # Add 1 to the rightmost digit of the
        # left side, propagate the carry
        # towards MSB digit and simultaneously
        # copying mirror of the left side
        # to the right side.
        while (i >= 0) :

            num[i] += carry
            carry = int(num[i] / 10)
            num[i] %= 10
            num[j] = num[i] # copy mirror to right
            j+=1
            i-=1

# The function that prints next
# palindrome of a given number num[]
# with n digits.
def generateNextPalindrome(num, n ) :

    print("\nNext palindrome is:")

    # Input type 1: All the digits are 9, simply o/p 1
    # followed by n-1 0's followed by 1.
    if( AreAll9s( num, n ) == True) :

        print( "1")
        for i in range(1, n):
            print( "0" )
        print( "1")

    # Input type 2 and 3
    else:

        generateNextPalindromeUtil ( num, n )

        # print the result
        printArray (num, n)

# A utility function to check if num has all 9s
def AreAll9s(num, n ):
    for i in range(1, n):
        if( num[i] != 9 ) :
            return 0
    return 1

# Utility that prints out an array on a line
def printArray(arr, n):

    for i in range(0, n):
        print(int(arr[i]),end=" ")
    print()

# Driver Program to test above function
if __name__ == "__main__":
    num = [9, 4, 1, 8, 7, 9, 7, 8, 3, 2, 2]
    n = len(num)
    generateNextPalindrome( num, n )

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// C# program to find next smallest  palindrome
using System;
public class GFG {

    // Returns next palindrome of a given
    // number num[]. This function is for
    // input type 2 and 3
    static void generateNextPalindromeUtil(int []num, int n)
    {
        int mid = n / 2;

        // end of left side is always 'mid -1'
        int i = mid - 1;

        // Beginning of right side depends
        // if n is odd or even
        int j = (n % 2 == 0) ? mid : mid + 1;

        // A bool variable to check if copy of left
        // side to right
        // is sufficient or not
        bool leftsmaller = false;

        // Initially, ignore the middle same digits
        while (i >= 0 && num[i] == num[j])
        {
            i--;
            j++;
        }

        // Find if the middle digit(s) need to
        // be incremented or not (or copying left
        // side is not sufficient)
        if (i < 0 || num[i] < num[j])
        {
            leftsmaller = true;
        }

        // Copy the mirror of left to tight
        while (i >= 0)
        {
            num[j++] = num[i--];
        }

        // Handle the case where middle digit(s)
        // must be incremented. This part of code
        // is for CASE 1 and CASE 2.2
        if (leftsmaller)
        {
            int carry = 1;

            // If there are odd digits, then increment
            // the middle digit and store the carry
            if (n % 2 == 1) {
                num[mid] += 1;
                carry = num[mid] / 10;
                num[mid] %= 10;
            }
            i = mid - 1;
            j = (n % 2 == 0 ? mid : mid + 1);

            // Add 1 to the rightmost digit of the left
            // side, propagate the carry towards MSB digit
            // and simultaneously copying mirror of the
            // left side to the right side.
            while (i >= 0)
            {
                num[i] = num[i] + carry;
                carry = num[i] / 10;
                num[i] %= 10;
                num[j] = num[i];// copy mirror to right
                i--;
                j++;
            }

        }
    }

    // The function that prints next palindrome
    // of a given number num[] with n digits.
    static void generateNextPalindrome(int []num, int n)
    {
        Console.WriteLine("Next Palindrome is:");

        // Input type 1: All the digits are 9,
        // simply o/p 1 followed by n-1 0's
        // followed by 1.
        if (isAll9(num, n)) {
            Console.Write("1");
            for (int i = 0; i < n - 1; i++)
                Console.Write("0");
            Console.Write("1");

        }

        // Input type 2 and 3
        else {
            generateNextPalindromeUtil(num, n);
            printarray(num);
        }
    }

    // A utility function to check if num has all 9s
    static bool isAll9(int[] num, int n) {
        for (int i = 0; i < n; i++)
            if (num[i] != 9)
                return false;
        return true;
    }

    /* Utility that prints out an array on a line */
    static void printarray(int []num) {
        for (int i = 0; i < num.Length; i++)
            Console.Write(num[i]+ " ");
        Console.Write(" ");
    }

    // Driver code
    public static void Main()
    {
        int []num = { 9, 4, 1, 8, 7, 9, 7, 8, 3, 2, 2 };
        generateNextPalindrome(num, num.Length);
    }
}

// This code is contributed by Smitha.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find next
// smallest palindrome

// Returns next palindrome
// of a given number num[].
// This function is for
// input type 2 and 3
function generateNextPalindromeUtil($num, $n)
{
    $mid = (int)($n / 2);

    // end of left side
    // is always 'mid -1'
    $i = $mid - 1;

    // Beginning of right
    // side depends if n
    // is odd or even
    $j = ($n % 2 == 0) ?
                  $mid : ($mid + 1);

    // A bool variable to check
    // if copy of left side to
    // right is sufficient or not
    $leftsmaller = false;

    // Initially, ignore the
    // middle same digits
    while ($i >= 0 &&
           $num[$i] == $num[$j])
    {
        $i--;
        $j++;
    }

    // Find if the middle digit(s)
    // need to be incremented or
    // not (or copying left side
    // is not sufficient)
    if ($i < 0 || $num[$i] < $num[$j])
    {
        $leftsmaller = true;
    }

    // Copy the mirror
    // of left to tight
    while ($i >= 0)
    {
        $num[$j++] = $num[$i--];
    }

    // Handle the case where
    // middle digit(s) must be
    // incremented. This part
    // of code is for CASE 1
    // and CASE 2.2
    if ($leftsmaller)
    {
        $carry = 1;

        // If there are odd digits,
        // then increment the middle
        // digit and store the carry
        if ($n % 2 == 1)
        {
            $num[$mid] += 1;
            $carry = (int)($num[$mid] / 10);
            $num[$mid] %= 10;
        }
        $i = $mid - 1;
        $j = ($n % 2 == 0 ?
                     $mid : $mid + 1);

        // Add 1 to the rightmost digit
        // of the left side, propagate
        // the carry towards MSB digit
        // and simultaneously copying
        // mirror of the left side to
        // the right side.
        while ($i >= 0)
        {
            $num[$i] = $num[$i] + $carry;
            $carry = (int)($num[$i] / 10);
            $num[$i] %= 10;

            // copy mirror to right
            $num[$j] = $num[$i];
            $i--;
            $j++;
        }

    }
return $num;
}

// The function that prints
// next palindrome of a given
// number num[] with n digits.
function generateNextPalindrome($num, $n)
{
    echo "Next Palindrome is:\n";

    // Input type 1: All the
    // digits are 9, simply
    // o/p 1 followed by n-1
    // 0's followed by 1.
    if (isAll9($num, $n))
    {
        echo "1";
        for ($i = 0; $i < $n - 1; $i++)
            echo "0";
        echo "1";

    }

    // Input type 2 and 3
    else
    {
        $num = generateNextPalindromeUtil($num, $n);
            printarray($num);
    }
}

// A utility function to
// check if num has all 9s
function isAll9($num, $n)
{
    for ($i = 0; $i < $n; $i++)
        if ($num[$i] != 9)
            return false;
    return true;
}

/* Utility that prints out
an array on a line */
function printarray($num)
{
    for ($i = 0;
         $i < count($num); $i++)
        echo $num[$i];
    echo "\n";
}

// Driver code
$num = array(9, 4, 1, 8, 7,
             9, 7, 8, 3, 2, 2);
generateNextPalindrome($num,
               count($num));

// This code is contributed by mits.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find next smallest
// palindrome

// Returns next palindrome of a given
// number num. This function is for
// input type 2 and 3
function generateNextPalindromeUtil(num , n)
{
    var mid = parseInt(n / 2);

    // end of left side is always 'mid -1'
    var i = mid - 1;

    // Beginning of right side depends
    // if n is odd or even
    var j = (n % 2 == 0) ? mid : mid + 1;

    // A bool variable to check if copy of left
    // side to right
    // is sufficient or not
    leftsmaller = false;

    // Initially, ignore the middle same digits
    while (i >= 0 && num[i] == num[j])
    {
        i--;
        j++;
    }

    // Find if the middle digit(s) need to
    // be incremented or not (or copying left
    // side is not sufficient)
    if (i < 0 || num[i] < num[j])
    {
        leftsmaller = true;
    }

    // Copy the mirror of left to tight
    while (i >= 0)
    {
        num[j++] = num[i--];
    }

    // Handle the case where middle digit(s)
    // must be incremented. This part of code
    // is for CASE 1 and CASE 2.2
    if (leftsmaller)
    {
        var carry = 1;

        // If there are odd digits, then increment
        // the middle digit and store the carry
        if (n % 2 == 1) {
            num[mid] += 1;
            carry = parseInt(num[mid] / 10);
            num[mid] %= 10;
        }
        i = mid - 1;
        j = (n % 2 == 0 ? mid : mid + 1);

        // Add 1 to the rightmost digit of the left
        // side, propagate the carry towards MSB digit
        // and simultaneously copying mirror of the
        // left side to the right side.
        //when carry is zero no need to loop through till i>=0
        while (i >= 0 && carry>0) 
        {
            num[i] = num[i] + carry;
            carry = parseInt(num[i] / 10);
            num[i] %= 10;
            num[j] = num[i];// copy mirror to right
            i--;
            j++;
        }

    }
}

// The function that prints next palindrome
// of a given number num with n digits.
function generateNextPalindrome(num , n)
{
    document.write("Next Palindrome is: <br>");

    // Input type 1: All the digits are 9,
    // simply o/p 1 followed by n-1 0's
    // followed by 1.
    if (isAll9(num, n)) {
        document.write("1");
        for (i = 0; i < n - 1; i++)
            document.write("0");
        document.write("1");

    }

    // Input type 2 and 3
    else {
        generateNextPalindromeUtil(num, n);
        printarray(num);
    }
}

// A utility function to check if num has all 9s
function isAll9(num , n) {
    for (i = 0; i < n; i++)
        if (num[i] != 9)
            return false;
    return true;
}

/* Utility that prints out an array on a line */
function printarray(num) {
    for (i = 0; i < num.length; i++)
        document.write(num[i]+"\n");
}

var num = [ 9, 4, 1, 8, 7, 9, 7, 8, 3, 2, 2 ];
generateNextPalindrome(num, num.length);

// This code is contributed by 29AjayKumar

</script>
```

**Output**

```
Next palindrome is:9 4 1 8 8 0 8 8 1 4 9 
```

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。