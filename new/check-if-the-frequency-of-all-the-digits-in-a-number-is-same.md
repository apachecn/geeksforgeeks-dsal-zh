# 检查一个数字中所有数字的频率是否相同

> 原文：[https://www.geeksforgeeks.org/check-if-the-frequency-of-all-the-digits-in-a-number-is-same/](https://www.geeksforgeeks.org/check-if-the-frequency-of-all-the-digits-in-a-number-is-same/)

给定正数“ N”，任务是查找“ N”是否平衡。 如果“ N”是一个平衡数字，则输出“ YES”，否则为“ NO”。

> 如果数字中所有数字的频率相同，即所有数字出现相同的次数，则该数字是平衡的。

**示例**：

```
Input: N = 1234567890
Output: YES
The frequencies of all the digits are same.
i.e. every digit appears same number of times.

Input: N = 1337
Output: NO

```

**方法**：

*   创建一个大小为 10 的数组 freq []，该数组会将每个数字的频率存储在“ N”中。

*   然后，检查“ N”的所有数字的频率是否相同。

*   如果是，则打印“是”或“否”。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// returns true if the number
// passed as the argument
// is a balanced number.
bool isNumBalanced(int N)
{

    string st = to_string(N);
    bool isBalanced = true;

    // frequency array to store
    // the frequencies of all
    // the digits of the number
    int freq[10] = { 0 };
    int i = 0;
    int n = st.size();

    for (i = 0; i < n; i++)

        // store the frequency of
        // the current digit
        freq[st[i] - '0']++;

    for (i = 0; i < 9; i++) {

        // if freq[i] is not
        // equal to freq[i + 1] at
        // any index 'i' then set
        // isBalanced to false
        if (freq[i] != freq[i + 1])
            isBalanced = false;
    }

    // return true if
    // the string is balanced
    if (isBalanced)
        return true;
    else
        return false;
}

// Driver code
int main()
{
    int N = 1234567890;

    // Function call
    bool flag = isNumBalanced(N);

    if (flag)
        cout << "YES";
    else
        cout << "NO";
}

// This code is contributed by ihritik

```

## Java

```java

// JAVA implementation using Hashmap and Collection
import java.util.*;

public class Num_balanced {

    public static boolean isNumBalanced(int n)
    {
        // Calling integer to char array convert function
        char[] num = num_to_arr(n);

        // HashMap is used to store key value pairs
        HashMap<Character, Integer> hp
            = new HashMap<Character, Integer>();

        // traverse char array and store array elements as
        // key and their frequency as their value
        for (int i = 0; i < num.length; i++) 
        {

            // if element already exists in the HashMap, so
            // we increment its previous value
            if (hp.containsKey(num[i])) 
            {
                hp.put(num[i], hp.get(num[i]) + 1);
            }

            // element does'nt exist in the HashMap, so we
            // initialize its value with 1
            else
            {
                hp.put(num[i], 1);
            }
        }

        // use Collection to store values of all the keys
        Collection c = (Collection)hp.values();

        // use iterator to iterate over each value
        Iterator<?> iterator = c.iterator();
        int temp = (Integer) iterator.next();

        while (iterator.hasNext()) 
        {
            // compare each value to be equal, if not return
            // false
            if ((int) iterator.next() != temp) {
                return false;
            }
        }

        // each value was equal so return true
        return true;
    }

    // This function converts integer into char array
    public static char[] num_to_arr(int num)
    {
        // Convert integer into String
        String str = Integer.toString(num);
        char[] arr = new char[str.length()];

        // Insert characters of the string into char array
        for (int i = 0; i < str.length(); i++) {
            arr[i] = str.charAt(i);
        }
        return arr;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n_1 = 1234567890;

        // Function call
        if (isNumBalanced(n_1)) 
        { 
            // if number is balanced
            System.out.println("YES");
        }
        else
        {  
            // if number is not balanced
            System.out.println("NO");

        }
    }
}
// Code Contributed by YESHU GARG

```

## Java

```java

// Implementation of JAVA to check the
// given number is Balanced or not
import java.util.*;
public class Main 
{
    // returns true if the number
    // passed as the argument
    // is a balanced number.
    public static boolean isNumBalanced(int num)
    {
        // to get the absolute value of the number
        num = Math.abs(num);

        // to convert the int number into a String
        String str = num + "";

        // to convert the String into Character Array
        char[] ch_arr = str.toCharArray();

        // HashSet is used to remove the duplicates
        // in the Character Array
        HashSet<Character> hs = new HashSet<Character>();
        for (char ch : ch_arr) 
        {
            // Adding the Characters in the Array in the Set
            hs.add(ch);
        }
        // getting the length of the String
        int str_len = str.length();

        // getting the numbers of elemnts in the HashSet
        int hs_len = hs.size();

        // return true if
        // the number is balanced
        // checks for the number is balanced or not by
        // comparing length of String and HashSet
        if (hs_len <= str_len / 2 || hs_len == str_len) 
        {
            return true;
        }
        return false;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 1234567890;

        // Function call
        boolean flag = isNumBalanced(N);

        if (flag)
            System.out.println("YES");
        else
            System.out.println("NO");
    }
}
// This code is contributed by Mano

```

## Python3

```py

# Python3 implementation of the above approach

> 原文：[https://www.geeksforgeeks.org/check-if-the-frequency-of-all-the-digits-in-a-number-is-same/](https://www.geeksforgeeks.org/check-if-the-frequency-of-all-the-digits-in-a-number-is-same/)

# Returns true if the number passed as

> 原文：[https://www.geeksforgeeks.org/check-if-the-frequency-of-all-the-digits-in-a-number-is-same/](https://www.geeksforgeeks.org/check-if-the-frequency-of-all-the-digits-in-a-number-is-same/)
# the argument is a balanced number.

> 原文：[https://www.geeksforgeeks.org/check-if-the-frequency-of-all-the-digits-in-a-number-is-same/](https://www.geeksforgeeks.org/check-if-the-frequency-of-all-the-digits-in-a-number-is-same/)

def isNumBalanced(N):

    st = str(N)
    isBalanced = True

    # Frequency array to store the frequencies
    # of all the digits of the number
    freq = [0] * 10
    n = len(st)

    for i in range(0, n):

        # store the frequency of the
        # current digit
        freq[int(st[i])] += 1

    for i in range(0, 9):

        # if freq[i] is not equal to
        # freq[i + 1] at any index 'i'
        # then set isBalanced to false
        if freq[i] != freq[i + 1]:
            isBalanced = False

    # Return true if the string
    # is balanced
    if isBalanced:
        return True
    else:
        return False

# Driver code

> 原文：[https://www.geeksforgeeks.org/check-if-the-frequency-of-all-the-digits-in-a-number-is-same/](https://www.geeksforgeeks.org/check-if-the-frequency-of-all-the-digits-in-a-number-is-same/)
if __name__ == "__main__":

    N = 1234567890

    # Function call
    flag = isNumBalanced(N)

    if flag:
        print("YES")
    else:
        print("NO")

# This code is contributed by Rituraj Jain

> 原文：[https://www.geeksforgeeks.org/check-if-the-frequency-of-all-the-digits-in-a-number-is-same/](https://www.geeksforgeeks.org/check-if-the-frequency-of-all-the-digits-in-a-number-is-same/)

```

## C#

```cs

// CSHARP implementation of the above approach
using System;

class Program 
{
    // returns true if the number
    // passed as the argument
    // is a balanced number.
    static bool isNumBalanced(int N)
    {
        String st = "" + N;
        bool isBalanced = true;

        // frequency array to store
        // the frequencies of all
        // the digits of the number
        int[] freq = new int[10];
        int i = 0;
        int n = st.Length;
        for (i = 0; i < n; i++)

            // store the frequency of
            // the current digit
            freq[st[i] - '0']++;
        for (i = 0; i < 9; i++) 
        {
            // if freq[i] is not
            // equal to freq[i + 1] at
            // any index ‘i’ then set
            // isBalanced to false
            if (freq[i] != freq[i + 1])
                isBalanced = false;
        }

        // return true if
        // the string is balanced
        if (isBalanced)
            return true;
        else
            return false;
    }

    // Driver code
    static void Main()
    {
        int N = 1234567890;

        // Function call
        bool flag = isNumBalanced(N);
        if (flag)
            Console.WriteLine("YES");
        else
            Console.WriteLine("NO");
    }
    // This code is contributed by ANKITRAI1
}

```

## PHP

```php

<?php
// PHP implementation of the approach

// returns true if the number
// passed as the argument
// is a balanced number.
function isNumBalanced($N)
{
    $st = "" . strval($N);
    $isBalanced = true;

    // frequency array to store
    // the frequencies of all
    // the digits of the number
    $freq = array_fill(0, 10, 0);
    $i = 0;
    $n = strlen($st);

    for ($i = 0; $i < $n; $i++)

        // store the frequency of
        // the current digit
        $freq[ord($st[$i]) - ord('0')]++;

    for ($i = 0; $i < 9; $i++) 
    {

        // if freq[i] is not
        // equal to freq[i + 1] at
        // any index 'i' then set
        // isBalanced to false
        if ($freq[$i] != $freq[$i + 1])
            $isBalanced = false;
    }

    // return true if
    // the string is balanced
    if ($isBalanced)
        return true;
    else
        return false;
}

// Driver code
$N = 1234567890;

// Function call
$flag = isNumBalanced($N);

if ($flag)
    echo "YES\n";
else
    echo "NO\n";

// This code is contributed by mits
?>

```

**Output**

```
YES
```



* * *

* * *



