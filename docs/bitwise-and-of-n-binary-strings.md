# N 个二进制字符串的按位“与”

> 原文:[https://www . geeksforgeeks . org/n 位二进制字符串与/](https://www.geeksforgeeks.org/bitwise-and-of-n-binary-strings/)

给定二进制字符串的数组 **arr[]** ，任务是计算所有这些字符串的按位“与”，并打印结果字符串。

**示例:**

```
Input: arr[] = {"101", "110110", "111"}
Output: 000100
(000101) & (110110) & (000111) = 000100

Input: arr[] = {"110010101", "111101001"}
Output: 110000001
```

**方法 1:** 类似于添加两个位串(https://www . geeksforgeeks . org/Add-两个位串/)
给定一个 N 个二进制字符串的数组。我们首先计算前两个二进制字符串的与运算，然后用第三个二进制字符串执行这个“结果”，以此类推，直到最后一个二进制字符串。
例如字符串 arr[]= {“101”、“110110”、“111”}；
第一步:结果= 101 和 110110；
步骤 2:结果=结果(步骤 1)和 111；
依此类推..

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Helper method: given two unequal sized
// bit strings, converts them to
// same length by adding leading 0s in the
// smaller string. Returns the the new length
int makeEqualLength(string &a, string &b)
{
    int len_a = a.length();
    int len_b = b.length();

    int num_zeros = abs(len_a-len_b);

    if (len_a<len_b)
    {
        for (int i = 0 ; i<num_zeros; i++)
        {
            a = '0' + a;
        }
        // Return len_b which is highest.
        // No need to proceed further!
        return len_b;
    }
    else
    {
        for (int i = 0 ; i<num_zeros; i++)
        {
            b = '0' + b;
        }
    }
    // Return len_a which is greater or
    // equal to len_b
    return len_a;
}

// The main function that performs AND
// operation of two-bit sequences
// and returns the resultant string
string andOperationBitwise(string s1, string s2)
{
    // Make both strings of same length with the
    // maximum length of s1 & s2.
    int length = makeEqualLength(s1,s2);

    // Initialize res as NULL string
    string res = "";

    // We start from left to right as we have
    // made both strings of same length.
    for (int i = 0 ; i<length; i++)
    {
        // Convert s1[i] and s2[i] to int and perform
        // bitwise AND operation, append to "res" string
        res = res + (char)((s1[i] - '0' & s2[i]-'0')+'0');
    }
    return res;
}

//Driver Code
int main()
{
    string arr[] = {"101", "110110", "111"};
    int n = sizeof(arr)/sizeof(arr[0]);

    string result;

    // Check corner case: If there is just one
    // binary string, then print it and return.
    if (n<2)
    {
        cout<<arr[n-1]<<endl;
        return 0;
    }
    result = arr[0];
    for (int i = 1; i<n; i++)
    {
        result = andOperationBitwise(result, arr[i]);
    }
    cout <<result<<endl;
}
// This code has been contributed by sharathmaidargi
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# this function takes two unequal sized
# bit strings, converts them to
# same length by adding leading 0s in the
# smaller string. Returns the the new length
def makeEqualLength(a, b):
    len_a = len(a)
    len_b = len(b)

    num_zeros = abs(len_a - len_b)

    if (len_a < len_b):
        for i in range(num_zeros):
            a = '0' + a

        # Return len_b which is highest.
        # No need to proceed further!
        return len_b, a, b

    else:
        for i in range(num_zeros):
            b = '0' + b

    # Return len_a which is greater or
    # equal to len_b
    return len_a, a, b

# The main function that performs AND
# operation of two-bit sequences
# and returns the resultant string
def andOperationBitwise(s1, s2):

    # Make both strings of same length
    # with the maximum length of s1 & s2.
    length, s1, s2 = makeEqualLength(s1, s2)

    # Initialize res as NULL string
    res = ""

    # We start from left to right as we have
    # made both strings of same length.
    for i in range(length):

        # Convert s1[i] and s2[i] to int
        # and perform bitwise AND operation,
        # append to "res" string
        res = res + str(int(s1[i]) & int(s2[i]))

    return res

# Driver Code
arr = ["101", "110110", "111"]
n = len(arr)
if (n < 2):
    print(arr[n - 1])

else:
    result = arr[0]
    for i in range(n):
        result = andOperationBitwise(result, arr[i]);

    print(result)

# This code is contributed by
# ANKITKUMAR34
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Helper method: given two unequal sized
// bit strings, converts them to
// same length by adding leading 0s in the
// smaller string. Returns the the new length
let s1, s2;

function makeEqualLength()
{
    let len_a = s1.length;
    let len_b = s2.length;

    let num_zeros = Math.abs(len_a - len_b);

    if (len_a < len_b)
    {
        for(let i = 0; i < num_zeros; i++)
        {
            s1 = '0' + s1;
        }

        // Return len_b which is highest.
        // No need to proceed further!
        return len_b;
    }
    else
    {
        for(let i = 0; i < num_zeros; i++)
        {
            s2 = '0' + s2;
        }
    }

    // Return len_a which is greater or
    // equal to len_b
    return len_a;
}

// The main function that performs AND
// operation of two-bit sequences
// and returns the resultant string
function andOperationBitwise()
{

    // Make both strings of same length with the
    // maximum length of s1 & s2.
    let length = makeEqualLength();

    // Initialize res as NULL string
    let res = "";

    // We start from left to right as we have
    // made both strings of same length.
    for(let i = 0 ; i<length; i++)
    {

        // Convert s1[i] and s2[i] to int
        // and perform bitwise AND operation,
        // append to "res" string
        res = res + String.fromCharCode((s1[i].charCodeAt() -
                                           '0'.charCodeAt() &
                                         s2[i].charCodeAt() -
                                           '0'.charCodeAt()) +
                                           '0'.charCodeAt());
    }
    return res;
}

// Driver code
let arr = [ "101", "110110", "111" ];
let n = arr.length;
let result;

// Check corner case: If there is just one
// binary string, then print it and return.
if (n < 2)
{
    document.write(arr[n - 1] + "</br>");
}
result = arr[0];
for(let i = 1; i<n; i++)
{
    s1 = result;
    s2 = arr[i];
    result = andOperationBitwise();
}
document.write(result);

// This code is contributed by vaibhavrabadiya3

</script>
```

**Output:** 

```
000100
```

**方法 2:** 找出最小和最大字符串的大小。我们需要这个来给我们的结果加上(最大-最小)零。例如，如果我们有 0010 和 11，那么这些字符串上的“与”将是 0010(因为我们可以将 11 写成 0011)。然后对每个位执行“与”运算。
我们只能通过查找任意字符串中的当前位是否为 0 来实现这一点。如果任何给定字符串中的当前位为 0，则对该位的“与”运算将为 0。如果当前位置的所有位都是 1，那么“与”运算将是 1。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the bitwise AND of
// all the binary strings
string strBitwiseAND(string* arr, int n)
{
    string res;

    // To store the largest and the smallest
    // string's size, We need this to add '0's
    // in the resultant string
    int smallest_size = INT_MAX;
    int largest_size = INT_MIN;

    // Reverse each string
    // Since we need to perform AND operation
    // on bits from Right to Left
    for (int i = 0; i < n; i++) {
        reverse(arr[i].begin(), arr[i].end());

        // Update the respective length values
        smallest_size = min(smallest_size, (int)arr[i].size());
        largest_size = max(largest_size, (int)arr[i].size());
    }

    // Traverse bits from 0 to smallest string's size
    for (int i = 0; i < smallest_size; i++) {
        bool all_ones = true;

        for (int j = 0; j < n; j++) {

            // If at this bit position, there is a 0
            // in any of the given strings then AND
            // operation on current bit position
            // will be 0
            if (arr[j][i] == '0') {

                all_ones = false;
                break;
            }
        }

        // Add resultant bit to result
        res += (all_ones ? '1' : '0');
    }

    // Add 0's to the string.
    for (int i = 0; i < largest_size - smallest_size; i++)
        res += '0';

    // Reverse the string
    // Since we started from LEFT to RIGHT
    reverse(res.begin(), res.end());

    // Return the resultant string
    return res;
}

// Driver code
int main()
{
    string arr[] = { "101", "110110", "111" };

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << strBitwiseAND(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GfG
{

    // Function to find the bitwise AND of
    // all the binary strings
    static String strBitwiseAND(String[] arr, int n)
    {
        String res = "";

        // To store the largest and the smallest
        // string's size, We need this to add
        // '0's in the resultant string
        int smallest_size = Integer.MAX_VALUE;
        int largest_size = Integer.MIN_VALUE;

        // Reverse each string
        // Since we need to perform AND operation
        // on bits from Right to Left
        for (int i = 0; i < n; i++)
        {

            StringBuilder temp = new StringBuilder();
            temp.append(arr[i]);
            arr[i] = temp.reverse().toString();

            // Update the respective length values
            smallest_size = Math.min(smallest_size, arr[i].length());
            largest_size = Math.max(largest_size, arr[i].length());
        }

        // Traverse bits from 0 to smallest string's size
        for (int i = 0; i < smallest_size; i++)
        {
            boolean all_ones = true;

            for (int j = 0; j < n; j++)
            {

                // If at this bit position, there is a 0
                // in any of the given strings then AND
                // operation on current bit position
                // will be 0
                if (arr[j].charAt(i) == '0')
                {

                    all_ones = false;
                    break;
                }
            }

            // Add resultant bit to result
            res += (all_ones ? '1' : '0');
        }

        // Add 0's to the string.
        for (int i = 0; i < largest_size - smallest_size; i++)
            res += '0';

        // Reverse the string
        // Since we started from LEFT to RIGHT
        StringBuilder temp = new StringBuilder();
        temp.append(res);
        res = temp.reverse().toString();

        // Return the resultant string
        return res;
    }

    // Driver code
    public static void main(String []args)
    {

        String arr[] = { "101", "110110", "111" };
        int n = arr.length;

        System.out.println(strBitwiseAND(arr, n));
    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
import sys;

# Function to find the bitwise AND of
# all the binary strings
def strBitwiseAND(arr, n) :

    res = ""

    # To store the largest and the smallest
    # string's size, We need this to add '0's
    # in the resultant string
    smallest_size = sys.maxsize;
    largest_size = -(sys.maxsize - 1);

    # Reverse each string
    # Since we need to perform AND operation
    # on bits from Right to Left
    for i in range(n) :
        arr[i] = arr[i][::-1] ;

        # Update the respective length values
        smallest_size = min(smallest_size, len(arr[i]));
        largest_size = max(largest_size, len(arr[i]));

    # Traverse bits from 0 to smallest string's size
    for i in range(smallest_size) :
        all_ones = True;

        for j in range(n) :

            # If at this bit position, there is a 0
            # in any of the given strings then AND
            # operation on current bit position
            # will be 0
            if (arr[j][i] == '0') :
                all_ones = False;
                break;

        # Add resultant bit to result
        if all_ones :
            res += '1' ;
        else :
            res += '0' ;

    # Add 0's to the string.
    for i in range(largest_size - smallest_size) :
        res += '0';

    # Reverse the string
    # Since we started from LEFT to RIGHT
    res = res[::-1];

    # Return the resultant string
    return res;

# Driver code
if __name__ == "__main__" :

    arr = [ "101", "110110", "111" ];

    n = len(arr) ;

    print(strBitwiseAND(arr, n));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the above approach:
using System;

class GfG
{

    // Function to find the bitwise AND of
    // all the binary strings
    static String strBitwiseAND(String[] arr, int n)
    {
        String res = "";

        // To store the largest and the smallest
        // string's size, We need this to add
        // '0's in the resultant string
        int smallest_size = int.MaxValue;
        int largest_size = int.MinValue;

        // Reverse each string
        // Since we need to perform AND operation
        // on bits from Right to Left
        String temp ="";
        for (int i = 0; i < n; i++)
        {

            temp+=arr[i];
            arr[i] = reverse(temp);

            // Update the respective length values
            smallest_size = Math.Min(smallest_size, arr[i].Length);
            largest_size = Math.Max(largest_size, arr[i].Length);
        }

        // Traverse bits from 0 to smallest string's size
        for (int i = 0; i < smallest_size; i++)
        {
            bool all_ones = true;

            for (int j = 0; j < n; j++)
            {

                // If at this bit position, there is a 0
                // in any of the given strings then AND
                // operation on current bit position
                // will be 0
                if (arr[j][i] == '0')
                {

                    all_ones = false;
                    break;
                }
            }

            // Add resultant bit to result
            res += (all_ones ? '1' : '0');
        }

        // Add 0's to the string.
        for (int i = 0; i < largest_size - smallest_size; i++)
            res += '0';

        // Reverse the string
        // Since we started from LEFT to RIGHT
        String temp1 = "";
        temp1+=res;
        res = reverse(temp1);

        // Return the resultant string
        return res;
    }

    static String reverse(String input)
    {
        char[] temparray = input.ToCharArray();
        int left, right = 0;
        right = temparray.Length - 1;

        for (left = 0; left < right; left++, right--)
        {
            // Swap values of left and right
            char temp = temparray[left];
            temparray[left] = temparray[right];
            temparray[right] = temp;
        }
        return String.Join("",temparray);
    }

    // Driver code
    public static void Main(String []args)
    {

        String []arr = { "101", "110110", "111" };
        int n = arr.Length;

        Console.WriteLine(strBitwiseAND(arr, n));
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript implementation of the above approach:

    // Function to find the bitwise AND of
    // all the binary strings
    function strBitwiseAND(arr, n)
    {
        let res = "";

        // To store the largest and the smallest
        // string's size, We need this to add
        // '0's in the resultant string
        let smallest_size = Number.MAX_VALUE;
        let largest_size = Number.MIN_VALUE;

        // Reverse each string
        // Since we need to perform AND operation
        // on bits from Right to Left
        let temp ="";
        for (let i = 0; i < n; i++)
        {

            temp+=arr[i];
            arr[i] = reverse(temp);

            // Update the respective length values
            smallest_size = Math.min(smallest_size, arr[i].length);
            largest_size = Math.max(largest_size, arr[i].length);
        }

        // Traverse bits from 0 to smallest string's size
        for (let i = 0; i < smallest_size; i++)
        {
            let all_ones = true;

            for (let j = 0; j < n; j++)
            {

                // If at this bit position, there is a 0
                // in any of the given strings then AND
                // operation on current bit position
                // will be 0
                if (arr[j][i] == '0')
                {

                    all_ones = false;
                    break;
                }
            }

            // Add resultant bit to result
            res += (all_ones ? '1' : '0');
        }

        // Add 0's to the string.
        for (let i = 0; i < largest_size - smallest_size; i++)
            res += '0';

        // Reverse the string
        // Since we started from LEFT to RIGHT
        let temp1 = "";
        temp1+=res;
        res = reverse(temp1);

        // Return the resultant string
        let temparray1 = res;
        let Temparray = "";
        for(let i = 6; i < temparray1.length; i++)
        {
            Temparray = Temparray + temparray1[i];
        }
        return Temparray;
    }

    function reverse(input)
    {
        let temparray = input.split('');
        let left, right = 0;
        right = temparray.length - 1;

        for (left = 0; left < right; left++, right--)
        {
            // Swap values of left and right
            let temp = temparray[left];
            temparray[left] = temparray[right];
            temparray[right] = temp;
        }
        return temparray.join("");
    }

    let arr = [ "101", "110110", "111" ];
    let n = arr.length;

    document.write(strBitwiseAND(arr, n));

</script>
```

**Output:** 

```
000100
```