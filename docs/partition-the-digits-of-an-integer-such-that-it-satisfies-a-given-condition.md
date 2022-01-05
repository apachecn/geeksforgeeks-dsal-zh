# 对整数的数字进行划分，使其满足给定的条件

> 原文:[https://www . geeksforgeeks . org/partition-整数的位数使其满足给定的条件/](https://www.geeksforgeeks.org/partition-the-digits-of-an-integer-such-that-it-satisfies-a-given-condition/)

给定一个整数 **X** ，任务是将其数字分成两个组: **A** 或 **B** ,使得当组 A 的所有数字从左到右排列在组 B 的所有数字之后时，数字序列不递减，如同它们出现在 **X** 中一样。打印 **-1** 如果不可能这样划分，否则返回一个与 **X** 相同长度的字符串 **S** ，其中***S【I】***或者是 **A** 或者是 **B** 。

**示例:**

> **输入:**X = 5164
> T3】输出:BABA
> A 组的位数是 1 和 4，B 组的位数是 5 和 6。这个分区满足这样的条件:当 A 的所有数字都被写入，然后 B 的所有数字都被写入，因为它们从左到右出现在 X 中，序列是非递减的，即 1456。
> 
> **输入:** X = 654
> **输出:** -1
> 不可能有可能导致非递减顺序的分区。例如，如果我们考虑 BBA 并写出序列，结果是 465。同样，对于 BAA，它是 546。而对于 AAA 来说是 654。

**进场:**

1.  让我们假设一个数字 **D** 使得所有小于 **D** 的数字进入组 **A** 并且所有大于 **D** 的数字进入组 **B** 。
2.  对于等于 **D** 的数字，只有组 **B** 的任意一个数字出现在它之前，它才会进入组 **A** ，否则它会进入组 **B** 。
3.  在这样的划分之后，检查它是否形成非递减序列。否则尝试一些不同的 **D** 。
4.  **D** 的值范围为 0 到 9。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to generate sequence
// from the given string
vector<int> makeSeq(string s, int a[])
{
    // Initialize vector to
    // store sequence
    vector<int> seq;

    // First add all the digits
    // of group A from left to right
    for (int i = 0; i < s.size(); i++)
        if (s[i] == 'A')
            seq.push_back(a[i]);

    // Then add all the digits
    // of group B from left to right
    for (int i = 0; i < s.size(); i++)
        if (s[i] == 'B')
            seq.push_back(a[i]);

    // Return the sequence
    return seq;
}

// Function that returns true if
// the sequence is non-decreasing
bool checkSeq(vector<int> v)
{
    // Initialize result
    bool check = true;

    for (int i = 1; i < v.size(); i++)
        if (v[i] < v[i - 1])
            check = false;

    return check;
}

// Function to partition the digits
// of an integer such that it satisfies
// the given conditions
string digitPartition(int X)
{
    // Convert the integer to string
    string num = to_string(X);

    // Length of the string
    int l = num.size();

    // Array to store the digits
    int a[l];

    // Storing the digits of X in array
    for (int i = 0; i < l; i++)
        a[i] = (num[i] - '0');

    for (int D = 0; D < 10; D++) {

        // Initialize the result
        string res = "";

        // Loop through the digits
        for (int i = 0; i < l; i++) {

            // Put into group A if
            // digit less than D
            if (a[i] < D)
                res += 'A';

            // Put into group B if
            // digit greater than D
            else if (a[i] > D)
                res += 'B';

            // Put into group C if
            // digit equal to D
            else
                res += 'C';
        }

        bool flag = false;

        // Loop through the digits
        // to decide for group C digits
        for (int i = 0; i < l; i++) {

            // Set flag equal to true
            // if group B digit present
            if (res[i] == 'B')
                flag = true;

            // If flag is true put in
            // group A or else put in B
            if (res[i] == 'C')
                res[i] = flag ? 'A' : 'B';
        }

        // Generate the sequence from partition
        vector<int> seq = makeSeq(res, a);

        // Check if the sequence is
        // non decreasing
        if (checkSeq(seq))
            return res;
    }

    // Return -1 if no such
    // partition is possible
    return "-1";
}

// Driver code
int main()
{
    int X = 777147777;

    cout << digitPartition(X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to generate sequence
// from the given String
static Vector<Integer> makeSeq(String s, int a[])
{
    // Initialize vector to
    // store sequence
    Vector<Integer> seq = new Vector<Integer>();

    // First add all the digits
    // of group A from left to right
    for (int i = 0; i < s.length(); i++)
        if (s.charAt(i) == 'A')
            seq.add(a[i]);

    // Then add all the digits
    // of group B from left to right
    for (int i = 0; i < s.length(); i++)
        if (s.charAt(i) == 'B')
            seq.add(a[i]);

    // Return the sequence
    return seq;
}

// Function that returns true if
// the sequence is non-decreasing
static boolean checkSeq(Vector<Integer> v)
{
    // Initialize result
    boolean check = true;

    for (int i = 1; i < v.size(); i++)
        if (v.get(i) < v.get(i - 1))
            check = false;

    return check;
}

// Function to partition the digits
// of an integer such that it satisfies
// the given conditions
static String digitPartition(int X)
{
    // Convert the integer to String
    String num = String.valueOf(X);

    // Length of the String
    int l = num.length();

    // Array to store the digits
    int []a = new int[l];

    // Storing the digits of X in array
    for (int i = 0; i < l; i++)
        a[i] = (num.charAt(i) - '0');

    for (int D = 0; D < 10; D++) 
    {

        // Initialize the result
        String res = "";

        // Loop through the digits
        for (int i = 0; i < l; i++) 
        {

            // Put into group A if
            // digit less than D
            if (a[i] < D)
                res += 'A';

            // Put into group B if
            // digit greater than D
            else if (a[i] > D)
                res += 'B';

            // Put into group C if
            // digit equal to D
            else
                res += 'C';
        }

        boolean flag = false;

        // Loop through the digits
        // to decide for group C digits
        for (int i = 0; i < l; i++) 
        {

            // Set flag equal to true
            // if group B digit present
            if (res.charAt(i) == 'B')
                flag = true;

            // If flag is true put in
            // group A or else put in B
            if (res.charAt(i) == 'C')
                res = res.substring(0, i) + 
                (flag ? 'A' : 'B') + res.substring(i + 1);
        }

        // Generate the sequence from partition
        Vector<Integer> seq = makeSeq(res, a);

        // Check if the sequence is
        // non decreasing
        if (checkSeq(seq))
            return res;
    }

    // Return -1 if no such
    // partition is possible
    return "-1";
}

// Driver code
public static void main(String[] args)
{
    int X = 777147777;

    System.out.print(digitPartition(X));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach 

# Function to generate sequence 
# from the given string 
def makeSeq(s, a) : 

    # Initialize vector to 
    # store sequence 
    seq = []; 

    # First add all the digits 
    # of group A from left to right 
    for i in range(len(s)) :
        if (s[i] == 'A') :
            seq.append(a[i]); 

    # Then add all the digits 
    # of group B from left to right 
    for i in range(len(s)) :
        if (s[i] == 'B') :
            seq.append(a[i]); 

    # Return the sequence 
    return seq; 

# Function that returns true if 
# the sequence is non-decreasing 
def checkSeq(v) : 

    # Initialize result 
    check = True; 

    for i in range(1, len(v)) :
        if (v[i] < v[i - 1]) :
            check = False; 

    return check; 

# Function to partition the digits 
# of an integer such that it satisfies 
# the given conditions 
def digitPartition(X) : 

    # Convert the integer to string 
    num = str(X); 

    # Length of the string 
    l = len(num); 

    # Array to store the digits 
    a = [0]*l; 

    # Storing the digits of X in array 
    for i in range(l) : 
        a[i] = (ord(num[i]) - ord('0')); 

    for D in range(10) :

        # Initialize the result 
        res = ""; 

        # Loop through the digits 
        for i in range(l) : 

            # Put into group A if 
            # digit less than D 
            if (a[i] < D) :
                res += 'A'; 

            # Put into group B if 
            # digit greater than D 
            elif (a[i] > D) :
                res += 'B'; 

            # Put into group C if 
            # digit equal to D 
            else :
                res += 'C'; 

        flag = False; 

        # Loop through the digits 
        # to decide for group C digits 
        for i in range(l) :

            # Set flag equal to true 
            # if group B digit present 
            if (res[i] == 'B') :
                flag = True; 

            # If flag is true put in 
            # group A or else put in B 
            res = list(res);

            if (res[i] == 'C') :
                res[i] = 'A' if flag else 'B'; 

        # Generate the sequence from partition 
        seq = makeSeq(res, a); 

        # Check if the sequence is 
        # non decreasing 
        if (checkSeq(seq)) :
            return "".join(res); 

    # Return -1 if no such 
    # partition is possible 
    return "-1"; 

# Driver code 
if __name__ == "__main__" : 

    X = 777147777; 

    print(digitPartition(X)); 

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to generate sequence
// from the given String
static List<int> makeSeq(String s, int []a)
{
    // Initialize vector to
    // store sequence
    List<int> seq = new List<int>();

    // First add all the digits
    // of group A from left to right
    for (int i = 0; i < s.Length; i++)
        if (s[i] == 'A')
            seq.Add(a[i]);

    // Then add all the digits
    // of group B from left to right
    for (int i = 0; i < s.Length; i++)
        if (s[i] == 'B')
            seq.Add(a[i]);

    // Return the sequence
    return seq;
}

// Function that returns true if
// the sequence is non-decreasing
static bool checkSeq(List<int> v)
{
    // Initialize result
    bool check = true;

    for (int i = 1; i < v.Count; i++)
        if (v[i] < v[i - 1])
            check = false;

    return check;
}

// Function to partition the digits
// of an integer such that it satisfies
// the given conditions
static String digitPartition(int X)
{
    // Convert the integer to String
    String num = String.Join("",X);

    // Length of the String
    int l = num.Length;

    // Array to store the digits
    int []a = new int[l];

    // Storing the digits of X in array
    for (int i = 0; i < l; i++)
        a[i] = (num[i] - '0');

    for (int D = 0; D < 10; D++) 
    {

        // Initialize the result
        String res = "";

        // Loop through the digits
        for (int i = 0; i < l; i++) 
        {

            // Put into group A if
            // digit less than D
            if (a[i] < D)
                res += 'A';

            // Put into group B if
            // digit greater than D
            else if (a[i] > D)
                res += 'B';

            // Put into group C if
            // digit equal to D
            else
                res += 'C';
        }

        bool flag = false;

        // Loop through the digits
        // to decide for group C digits
        for (int i = 0; i < l; i++) 
        {

            // Set flag equal to true
            // if group B digit present
            if (res[i] == 'B')
                flag = true;

            // If flag is true put in
            // group A or else put in B
            if (res[i] == 'C')
                res = res.Substring(0, i) + 
                (flag ? 'A' : 'B') + res.Substring(i + 1);
        }

        // Generate the sequence from partition
        List<int> seq = makeSeq(res, a);

        // Check if the sequence is
        // non decreasing
        if (checkSeq(seq))
            return res;
    }

    // Return -1 if no such
    // partition is possible
    return "-1";
}

// Driver code
public static void Main(String[] args)
{
    int X = 777147777;

    Console.Write(digitPartition(X));
}
}

// This code is contributed by Rajput-Ji
```

**Output:**

```
BBBAABBBB

```