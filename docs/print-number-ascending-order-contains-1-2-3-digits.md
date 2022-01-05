# 以升序打印数字，数字中包含 1、2 和 3。

> 原文:[https://www . geesforgeks . org/print-number-升序-contains-1-2-3-digits/](https://www.geeksforgeeks.org/print-number-ascending-order-contains-1-2-3-digits/)

给定一个数字数组，任务是按升序打印这些数字，用逗号分隔，数字中有 1、2 和 3。如果没有包含数字 1、2 和 3 的数字，则打印-1。

**示例:**

```
Input : numbers[] = {123, 1232, 456, 234, 32145}
Output : 123, 1232, 32145

Input : numbers[] = {9821, 627183, 12, 1234}
Output : 1234, 627183

Input : numbers[] = {12, 232, 456, 234}
Output : -1

```

**问于:**高盛
T3】方法:首先从包含 **1，2 & 3** 的数组中找出所有的数字，然后按照 1，2，3 排序，然后打印出来。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to print all number containing 
// 1, 2 and 3 in any order.
#include<bits/stdc++.h>
using namespace std;

// convert the number to string and find 
// if it contains 1, 2 & 3.
bool findContainsOneTwoThree(int number)
{    
    string str = to_string(number);
    int countOnes = 0, countTwo = 0, countThree = 0;
    for(int i = 0; i < str.length(); i++) {
        if(str[i] == '1') countOnes++;
        else if(str[i] == '2') countTwo++;
        else if(str[i] == '3') countThree++;
    }         
    return (countOnes && countTwo && countThree);
}
// prints all the number containing 1, 2, 3 
string printNumbers(int numbers[], int n)
{
    vector<int> oneTwoThree;
    for (int i = 0; i < n; i++) 
    {
        // check if the number contains 1, 
        // 2 & 3 in any order
        if (findContainsOneTwoThree(numbers[i]))
            oneTwoThree.push_back(numbers[i]);
    }

    // sort all the numbers
    sort(oneTwoThree.begin(), oneTwoThree.end());

    string result = "";
    for(auto number: oneTwoThree) 
    {
        int value = number;
        if (result.length() > 0)
            result += ", ";

        result += to_string(value);
    }

    return (result.length() > 0) ? result : "-1";
}

// Driver Code
int main() {
    int numbers[] = { 123, 1232, 456, 234, 32145 };

    int n = sizeof(numbers)/sizeof(numbers[0]);

    string result = printNumbers(numbers, n);
    cout << result;
    return 0;
}
// This code is contributed 
// by Sirjan13
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all number containing 
// 1, 2 and 3 in any order.
import java.io.FileNotFoundException;
import java.util.ArrayList;
import java.util.Collections;
import java.util.Iterator;

class GFG {

    // prints all the number containing 1, 2, 3 
    // in any order
    private static String printNumbers(int[] numbers)
    {

        ArrayList<Integer> array = new ArrayList<>();
        for (int number : numbers) {

            // check if the number contains 1, 
            // 2 & 3 in any order
            if (findContainsOneTwoThree(number))
                array.add(number);
        }

        // sort all the numbers
        Collections.sort(array);

        StringBuffer strbuf = new StringBuffer();
        Iterator it = array.iterator();        
        while (it.hasNext()) {

            int value = (int)it.next();
            if (strbuf.length() > 0)
                strbuf.append(", ");

            strbuf.append(Integer.toString(value));
        }

        return (strbuf.length() > 0) ? 
                     strbuf.toString() : "-1";
    }

    // convert the number to string and find 
    // if it contains 1, 2 & 3.
    private static boolean findContainsOneTwoThree(
                                         int number)
    {

        String str = Integer.toString(number);        
        return (str.contains("1") && str.contains("2") && 
                                    str.contains("3"));
    }

    public static void main(String[] args) 
    {        
        int[] numbers = { 123, 1232, 456, 234, 32145 };        
        System.out.println(printNumbers(numbers));
    }
}
```

## 计算机编程语言

```
# Python program for printing 
# all numbers containing 1,2 and 3

def printNumbers(numbers):

    # convert all numbers
    # to strings
    numbers = map(str, numbers)
    result = []
    for num in numbers:

        # check if each number 
        # in the list has 1,2 and 3
        if ('1' in num and 
            '2' in num and 
            '3' in num):
            result.append(num)

    # if there are no
    # valid numbers
    if not result:
        result = ['-1']

    return sorted(result);

# Driver Code
numbers = [123, 1232, 456, 
           234, 32145]
result = printNumbers(numbers)
print ', '.join(num for num in result)

# This code is contributed 
# by IshitaTripathi
```

## C#

```
// C# program to print all number 
// containing 1, 2 and 3 in any order.
using System;
using System.Collections.Generic;
using System.Text;

class GFG
{

    // prints all the number
    // containing 1, 2, 3 
    // in any order 
    private static string printNumbers(int[] numbers)
    {

        List<int> array = new List<int>();
        foreach (int number in numbers)
        {

            // check if the number contains 1, 
            // 2 & 3 in any order 
            if (findContainsOneTwoThree(number))
            {
                array.Add(number);
            }
        }

        // sort all the numbers 
        array.Sort();

        StringBuilder strbuf = new StringBuilder();
        System.Collections.IEnumerator it = 
                     array.GetEnumerator();
        while (it.MoveNext())
        {

            int value = (int)it.Current;
            if (strbuf.Length > 0)
            {
                strbuf.Append(", ");
            }

            strbuf.Append(Convert.ToString(value));
        }

        return (strbuf.Length > 0) ? strbuf.ToString() : "-1";
    }

    // convert the number
    // to string and find 
    // if it contains 1, 2 & 3. 
    private static bool findContainsOneTwoThree(int number)
    {

        string str = Convert.ToString(number);
        return (str.Contains("1") && 
         str.Contains("2") && str.Contains("3"));
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int[] numbers = new int[] {123, 1232, 
                            456, 234, 32145};
        Console.WriteLine(printNumbers(numbers));
    }
}

// This code is contributed by Shrikant13
```

**Output:**

```
123, 1232, 32145

```

**时间复杂度:**上述方法的时间复杂度为 **O(nlg(n))** 。