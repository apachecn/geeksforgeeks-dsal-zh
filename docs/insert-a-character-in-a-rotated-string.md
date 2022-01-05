# 在旋转的字符串中插入一个字符

> 原文:[https://www . geesforgeks . org/insert-a-character-in-a-rotated-string/](https://www.geeksforgeeks.org/insert-a-character-in-a-rotated-string/)

给定一组大小为 **N** 的字符 **arr[]** 和一个整数 **K** 。您必须将字符一个接一个地插入一个空字符串中，这样每次插入都是在前一次插入的右侧 **K** 位置之后完成的，并且字符串是圆形的。任务是找到最后一次插入的字符

**示例:**

> **输入:** arr[] = {'1 '，' 2 '，' 3 '，' 4 '，' 5'}，K = 2
> **输出:** 1
> 在第一个插入字符串变成“1”
> 之后在第二个插入字符串变成“12”
> 之后在第三个插入之后，如同先前的插入是在位置 2。
> 因此，当前插入必须在 2 + 2，即第 4 个位置。
> 由于字符串是圆形的，所以向右移动 2 个位置
> 将是“1 | 2”->“12 |”，最后一个字符串将是第四次插入后的“123”
> ，“123”->“1 | 23”->“12 | 3”即第五次插入后的“1243”
> ，“1243”->“1243 |”->“1 | 243”
> 
> **输入:** arr[] = {'1 '，' 2 '，' 3 '，' 4 '，' 5'}，K = 1
> T3】输出: 1
> 最终字符串为“15324”

**方法:**对于每个字符，将其插入到所需的位置，并跟踪前一个位置和前一次插入后的字符。插入所有字符后，打印最后一次插入的字符。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to insert the character
char Insert(char arr[], int n, int k)
{
    // To store last position where
    // the insertion is done
    int ind = 0;

    // To store size of the string
    int sz = 0;

    // To store the modified string
    string s = "";

    // To store characters
    char ch = arr[0];

    // Add first character to the string
    s += ch;

    // Update the size
    sz = 1;

    // Update the index of last insertion
    ind = 0;

    // Insert all other characters to the string
    for (int i = 1; i < n; i++) {

        // Take the character
        ch = arr[i];

        // Take substring upto ind
        string s1 = s.substr(0, ind + 1);

        // Take modulo value of k with
        // the size of the string
        int temp = k % sz;

        // Check if we need to move to
        // the start of the string
        int ro = temp - min(temp, sz - ind - 1);

        // If we don't need to move to start of the string
        if (ro == 0) {

            // Take substring from upto temp
            string s2 = s.substr(ind + 1, temp);

            // Take substring which will be after
            // the inserted character
            string s3 = s.substr(ind + temp + 1,
                                 sz - ind - temp - 1);

            // Insert into the string
            s = s1 + s2 + ch + s3;

            // Store new inserted position
            ind = s1.size() + s2.size();

            // Store size of the new string
            // Technically sz + 1
            sz = s.size();
        }

        // If we need to move to start of the string
        else {

            // Take substring which will before
            // the inserted character
            string s2 = s.substr(0, ro);

            // Take substring which will be after
            // the inserted character
            string s3 = s.substr(ro, sz - ro);

            // Insert into the string
            s = s2 + ch + s3;

            // Store new inserted position
            ind = s2.size();

            // Store size of the new string
            // Technically sz + 1
            sz = s.size();
        }
    }

    // Return the required character
    if (ind == 0)
        return s[sz - 1];
    else
        return s[ind - 1];
}

// Driver code
int main()
{
    char arr[] = { '1', '2', '3', '4', '5' };

    int k = 2;

    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << Insert(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG{

// Function to insert the character
public static char Insert(char arr[], int n, int k)
{

    // To store last position where
    // the insertion is done
    int ind = 0;

    // To store size of the string
    int sz = 0;

    // To store the modified string
    String s = "";

    // To store characters
    char ch = arr[0];

    // Add first character to the string
    s += ch;

    // Update the size
    sz = 1;

    // Update the index of last insertion
    ind = 0;

    // Insert all other characters to the string
    for(int i = 1; i < n; i++)
    {

        // Take the character
        ch = arr[i];

        // Take substring upto ind
        String s1 = s.substring(0, ind + 1);

        // Take modulo value of k with
        // the size of the string
        int temp = k % sz;

        // Check if we need to move to
        // the start of the string
        int ro = temp - Math.min(temp, sz - ind - 1);

        // If we don't need to move to
        // start of the string
        if (ro == 0)
        {

            // Take substring from upto temp
            String s2 = s.substring(ind + 1,
                                    ind + 1 + temp);

            // Take substring which will be after
            // the inserted character
            String s3 = s.substring(ind + temp + 1, sz);

            // Insert into the string
            s = s1 + s2 + ch + s3;

            // Store new inserted position
            ind = s1.length() + s2.length();

            // Store size of the new string
            // Technically sz + 1
            sz = s.length();
        }

        // If we need to move to start of the string
        else
        {

            // Take substring which will before
            // the inserted character
            String s2 = s.substring(0, ro);

            // Take substring which will be after
            // the inserted character
            String s3 = s.substring(ro, sz);

            // Insert into the string
            s = s2 + ch + s3;

            // Store new inserted position
            ind = s2.length();

            // Store size of the new string
            // Technically sz + 1
            sz = s.length();
        }
    }

    // Return the required character
    if (ind == 0)
    {
        return s.charAt(sz - 1);
    }
    else
    {
        return s.charAt(ind - 1);
    }
}

// Driver code
public static void main(String []args)
{
    char arr[] = { '1', '2', '3', '4', '5' };
    int k = 2;
    int n = arr.length;

    // Function call
    System.out.println(Insert(arr, n, k));
}
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to insert the character
def insert(arr: list, n: int, k: int) -> chr:

    # To store last position where
    # the insertion is done
    ind = 0

    # To store size of the string
    sz = 0

    # To store the modified string
    s = ""

    # To store characters
    ch = arr[0]

    # Add first character to the string
    s += ch

    # Update the size
    sz = 1

    # Update the index of last insertion
    ind = 0

    # Insert all other characters to the string
    for i in range(1, n):

        # Take the character
        ch = arr[i]

        # Take substring upto ind
        s1 = s[0:ind + 1]

        # Take modulo value of k with
        # the size of the string
        temp = k % sz

        # Check if we need to move to
        # the start of the string
        ro = temp - min(temp, sz - ind - 1)

        # If we don't need to move to start of the string
        if ro == 0:

            # Take substring from upto temp
            s2 = s[ind + 1:ind + 1 + temp]

            # Take substring which will be after
            # the inserted character
            s3 = s[ind + temp + 1:sz]

            # Insert into the string
            s = s1 + s2 + ch + s3

            # Store new inserted position
            ind = len(s1) + len(s2)

            # Store size of the new string
            # Technically sz + 1
            sz = len(s)

        # If we need to move to start of the string
        else:

            # Take substring which will before
            # the inserted character
            s2 = s[:ro]

            # Take substring which will be after
            # the inserted character
            s3 = s[ro:sz]

            # Insert into the string
            s = s2 + ch + s3

            # Store new inserted position
            ind = len(s2)

            # Store size of the new string
            # Technically sz + 1
            sz = len(s)

    # Return the required character
    if ind == 0:
        return s[sz - 1]
    else:
        return s[ind - 1]

# Driver Code
if __name__ == "__main__":
    arr = ['1', '2', '3', '4', '5']
    k = 2
    n = len(arr)

    # Function call
    print(insert(arr, n, k))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of the approach
using System;

class GFG{

// Function to insert the character
static char Insert(char[] arr, int n, int k)
{

    // To store last position where
    // the insertion is done
    int ind = 0;

    // To store size of the string
    int sz = 0;

    // To store the modified string
    String s = "";

    // To store characters
    char ch = arr[0];

    // Add first character to the string
    s += ch;

    // Update the size
    sz = 1;

    // Update the index of last insertion
    ind = 0;

    // Insert all other characters to the string
    for(int i = 1; i < n; i++)
    {

        // Take the character
        ch = arr[i];

        // Take substring upto ind
        string s1 = s.Substring(0, ind + 1);

        // Take modulo value of k with
        // the size of the string
        int temp = k % sz;

        // Check if we need to move to
        // the start of the string
        int ro = temp - Math.Min(temp, sz - ind - 1);

        // If we don't need to move to
        // start of the string
        if (ro == 0)
        {

            // Take substring from upto temp
            string s2 = s.Substring(ind + 1, temp);

            // Take substring which will be after
            // the inserted character
            string s3 = s.Substring(ind + temp + 1,
                               sz - ind - temp - 1);

            // Insert into the string
            s = s1 + s2 + ch + s3;

            // Store new inserted position
            ind = s1.Length + s2.Length;

            // Store size of the new string
            // Technically sz + 1
            sz = s.Length;
        }

        // If we need to move to start of the string
        else
        {

            // Take substring which will before
            // the inserted character
            string s2 = s.Substring(0, ro);

            // Take substring which will be after
            // the inserted character
            string s3 = s.Substring(ro, sz - ro);

            // Insert into the string
            s = s2 + ch + s3;

            // Store new inserted position
            ind = s2.Length;

            // Store size of the new string
            // Technically sz + 1
            sz = s.Length;
        }
    }

    // Return the required character
    if (ind == 0)
    {
        return s[sz - 1];
    }
    else
    {
        return s[ind - 1];
    }
}

// Driver code
static public void Main()
{
    char[] arr = { '1', '2', '3', '4', '5' };
    int k = 2;
    int n = arr.Length;

    // Function call
    Console.WriteLine(Insert(arr, n, k));
}
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to insert the character
function Insert(arr,n,k)
{
    // To store last position where
    // the insertion is done
    let ind = 0;

    // To store size of the string
    let sz = 0;

    // To store the modified string
    let s = "";

    // To store characters
    let ch = arr[0];

    // Add first character to the string
    s += ch;

    // Update the size
    sz = 1;

    // Update the index of last insertion
    ind = 0;

    // Insert all other characters to the string
    for(let i = 1; i < n; i++)
    {

        // Take the character
        ch = arr[i];

        // Take substring upto ind
        let s1 = s.substring(0, ind + 1);

        // Take modulo value of k with
        // the size of the string
        let temp = k % sz;

        // Check if we need to move to
        // the start of the string
        let ro = temp - Math.min(temp, sz - ind - 1);

        // If we don't need to move to
        // start of the string
        if (ro == 0)
        {

            // Take substring from upto temp
            let s2 = s.substring(ind + 1,
                                    ind + 1 + temp);

            // Take substring which will be after
            // the inserted character
            let s3 = s.substring(ind + temp + 1, sz);

            // Insert into the string
            s = s1 + s2 + ch + s3;

            // Store new inserted position
            ind = s1.length + s2.length;

            // Store size of the new string
            // Technically sz + 1
            sz = s.length;
        }

        // If we need to move to start of the string
        else
        {

            // Take substring which will before
            // the inserted character
            let s2 = s.substring(0, ro);

            // Take substring which will be after
            // the inserted character
            let s3 = s.substring(ro, sz);

            // Insert into the string
            s = s2 + ch + s3;

            // Store new inserted position
            ind = s2.length;

            // Store size of the new string
            // Technically sz + 1
            sz = s.length;
        }
    }

    // Return the required character
    if (ind == 0)
    {
        return s[sz - 1];
    }
    else
    {
        return s[ind - 1];
    }
}

// Driver code
let arr=['1', '2', '3', '4', '5' ];
let  k = 2;
let n = arr.length;

document.write(Insert(arr, n, k));

// This code is contributed by ab2127
</script>
```

**Output:** 

```
1
```