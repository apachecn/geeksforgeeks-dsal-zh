# 任意次互换可形成的最大偶数

> 原文:[https://www . geeksforgeeks . org/由任意数量的互换形成的最大偶数/](https://www.geeksforgeeks.org/largest-even-number-that-can-be-formed-by-any-number-of-swaps/)

给定一个字符串形式的整数 **N** ，任务是当你被允许进行任意次数的交换(交换数字的位数)时，从给定的数字中找出最大的偶数。如果不能形成偶数，则打印 **-1** 。

**示例:**

> **输入:**N = 1324
> T3】输出: 4312
> 
> **输入:** N = 135
> **输出:** -1
> 奇数不能组成偶数。

**方法:**按降序对字符串进行排序，然后我们将获得给定数字的最大可能数，但它可能是也可能不是偶数。为了使它成为偶数(如果还没有的话)，数字中的一个偶数必须与最后一个数字交换，为了使偶数最大化，要交换的偶数必须是数字中最小的偶数。

**注意**由于最差情况下需要排序的不同元素的数量最多为 **10** ，因此可以对数字的位数使用频率数组在线性时间内进行排序。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
const int MAX = 10;

// Function to return the maximum
// even number that can be formed
// with any number of digit swaps
string getMaxEven(string str, int len)
{

    // To store the frequencies of
    // all the digits
    int freq[MAX] = { 0 };

    // To store the minimum even digit
    // and the minimum overall digit
    int i, minEvenDigit = MAX;
    for (i = 0; i < len; i++) {
        int digit = str[i] - '0';
        freq[digit]++;

        // If digit is even then update
        // the minimum even digit
        if (digit % 2 == 0)
            minEvenDigit = min(digit, minEvenDigit);
    }

    // If there is no even digit then
    // it is not possible to generate
    // an even number with swaps
    if (minEvenDigit == MAX)
        return "-1";

    // Decrease the frequency of the
    // digits that need to be swapped
    freq[minEvenDigit]--;

    i = 0;
    // Take every digit starting from the maximum
    // in order to maximize the number
    for (int j = MAX - 1; j >= 0; j--) {

        // Take current digit number of times
        // it appeared in the original number
        for (int k = 0; k < freq[j]; k++)
            str[i++] = (char)(j + '0');
    }

    // Append once instance of the minimum
    // even digit in the end to make the number even
    str[i] = (char)(minEvenDigit + '0');

    return str;
}

// Driver code
int main()
{
    string str = "1023422";
    int len = str.length();

    // Function call
    cout << getMaxEven(str, len);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    static int MAX = 10;

    // Function to return the maximum
    // even number that can be formed
    // with any number of digit swaps
    static String getMaxEven(String str, int len)
    {
      //To store the max even number
        String maxEven="";
        // To store the frequencies of
        // all the digits
        int[] freq = new int[MAX];

        // To store the minimum even digit
        int i, minEvenDigit = MAX;
        for (i = 0; i < len; i++) {
            int digit = str.charAt(i) - '0';
            freq[digit]++;

            // If digit is even then update
            // the minimum even digit
            if (digit % 2 == 0)
                minEvenDigit
                    = Math.min(digit, minEvenDigit);

        }

        // If there is no even digit then
        // it is not possible to generate
        // an even number with swaps
        if (minEvenDigit == MAX)
            return "-1";

        // Decrease the frequency of the
        // minEvenDigit
        freq[minEvenDigit]--;

        i = MAX-1;

        // Take every digit starting from the maximum
        // in order to maximize the number
       while(i>=0)
       {
           // Take current digit number of times
            // it appeared in the original number
           if(freq[i]>0)
           {
             maxEven= maxEven+i;
             freq[i]--;
           }else
             i--;

        }

        // Append the minimum even digit
        // in the end to make the number even
         maxEven= maxEven+minEvenDigit;

        return maxEven;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "1023422";
        int len = str.length();

        // Function call
        System.out.println(getMaxEven(str, len));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

MAX = 10

# Function to return the maximum
# even number that can be formed
# with any number of digit swaps

def getMaxEven(string, length):

    string = list(string)

    # To store the frequencies of
    # all the digits
    freq = [0]*MAX

    # To store the minimum even digit
    # and the minimum overall digit
    minEvenDigit = MAX
    minDigit = MAX
    for i in range(length):
        digit = ord(string[i]) - ord('0')
        freq[digit] += 1

        # If digit is even then update
        # the minimum even digit
        if (digit % 2 == 0):
            minEvenDigit = min(digit, minEvenDigit)

        # Update the overall minimum digit
        minDigit = min(digit, minDigit)

    # If there is no even digit then
    # it is not possible to generate
    # an even number with swaps
    if (minEvenDigit == MAX):
        return "-1"

    # Decrease the frequency of the
    # digits that need to be swapped
    freq[minEvenDigit] -= 1
    freq[minDigit] -= 1

    i = 0

    # Take every digit starting from the maximum
    # in order to maximize the number
    for j in range(MAX - 1, -1, -1):

        # Take current digit number of times
        # it appeared in the original number
        for k in range(freq[j]):
            string[i] = chr(j + ord('0'))
            i += 1

        # If current digit equals to the
        # minimum even digit then one instance of it
        # needs to be swapped with the minimum overall digit
        # i.e. append the minimum digit here
        if (j == minEvenDigit):
            string[i] = chr(minDigit + ord('0'))
            i += 1

    # Append once instance of the minimum
    # even digit in the end to make the number even
    string[-1] = chr(minEvenDigit + ord('0'))

    return "".join(string)

# Driver code
if __name__ == "__main__":
    string = "1023422"
    length = len(string)

    # Function call
    print(getMaxEven(string, length))

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    static int MAX = 10;

    // Function to return the maximum
    // even number that can be formed
    // with any number of digit swaps
    static String getMaxEven(char[] str, int len)
    {

        // To store the frequencies of
        // all the digits
        int[] freq = new int[MAX];

        // To store the minimum even digit
        // and the minimum overall digit
        int i, minEvenDigit = MAX, minDigit = MAX;
        for (i = 0; i < len; i++) {
            int digit = str[i] - '0';
            freq[digit]++;

            // If digit is even then update
            // the minimum even digit
            if (digit % 2 == 0)
                minEvenDigit
                    = Math.Min(digit, minEvenDigit);

            // Update the overall minimum digit
            minDigit = Math.Min(digit, minDigit);
        }

        // If there is no even digit then
        // it is not possible to generate
        // an even number with swaps
        if (minEvenDigit == MAX)
            return "-1";

        // Decrease the frequency of the
        // digits that need to be swapped
        freq[minEvenDigit]--;
        freq[minDigit]--;

        i = 0;

        // Take every digit starting from the maximum
        // in order to maximize the number
        for (int j = MAX - 1; j >= 0; j--) {

            // Take current digit number of times
            // it appeared in the original number
            for (int k = 0; k < freq[j]; k++)
                str[i++] = (char)(j + '0');

            // If current digit equals to the
            // minimum even digit then one instance of it
            // needs to be swapped with the minimum overall
            // digit i.e. append the minimum digit here
            if (j == minEvenDigit)
                str[i++] = (char)(minDigit + '0');
        }

        // Append once instance of the minimum
        // even digit in the end to make the number even
        str[i - 1] = (char)(minEvenDigit + '0');

        return String.Join("", str);
    }

    // Driver code
    public static void Main(String[] args)
    {
        char[] str = "1023422".ToCharArray();
        int len = str.Length;

        // Function call
        Console.WriteLine(getMaxEven(str, len));
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    let MAX = 10;

    // Function to return the maximum
    // even number that can be formed
    // with any number of digit swaps
    function getMaxEven(str, len)
    {

        // To store the frequencies of
        // all the digits
        let freq = new Array(MAX);
        freq.fill(0);

        // To store the minimum even digit
        // and the minimum overall digit
        let i, minEvenDigit = MAX, minDigit = MAX;
        for (i = 0; i < len; i++) {
            let digit = str[i].charCodeAt() - '0'.charCodeAt();
            freq[digit]++;

            // If digit is even then update
            // the minimum even digit
            if (digit % 2 == 0)
                minEvenDigit
                    = Math.min(digit, minEvenDigit);

            // Update the overall minimum digit
            minDigit = Math.min(digit, minDigit);
        }

        // If there is no even digit then
        // it is not possible to generate
        // an even number with swaps
        if (minEvenDigit == MAX)
            return "-1";

        // Decrease the frequency of the
        // digits that need to be swapped
        freq[minEvenDigit]--;
        freq[minDigit]--;

        i = 0;

        // Take every digit starting from the maximum
        // in order to maximize the number
        for (let j = MAX - 1; j >= 0; j--) {

            // Take current digit number of times
            // it appeared in the original number
            for (let k = 0; k < freq[j]; k++)
                str[i++] = String.fromCharCode(j + '0'.charCodeAt());

            // If current digit equals to the
            // minimum even digit then one instance of it
            // needs to be swapped with the minimum overall
            // digit i.e. append the minimum digit here
            if (j == minEvenDigit)
                str[i++] = String.fromCharCode(minDigit + '0'.charCodeAt());
        }

        // Append once instance of the minimum
        // even digit in the end to make the number even
        str[i - 1] = String.fromCharCode(minEvenDigit + '0'.charCodeAt());

        return str.join("");
    }

    let str = "1023422".split('');
    let len = str.length;

    // Function call
    document.write(getMaxEven(str, len));

</script>
```

**Output:** 

```
4322210
```

**时间复杂度:** O(n)