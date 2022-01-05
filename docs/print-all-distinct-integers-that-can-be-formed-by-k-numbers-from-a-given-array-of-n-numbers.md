# 打印所有不同的整数，这些整数可以由 N 个数字的给定数组中的 K 个数字组成

> 原文:[https://www . geesforgeks . org/print-all-distinct-整数-可以由给定的 n-numbers 数组中的 k-numbers 构成/](https://www.geeksforgeeks.org/print-all-distinct-integers-that-can-be-formed-by-k-numbers-from-a-given-array-of-n-numbers/)

给定一个由 N 个元素和一个整数 K 组成的数组，打印所有不同的整数，这些整数可以通过从给定的 N 个数字中选择 K 个数字来形成。一个数组中的数字可以被选择任意次。

**示例:**

> **输入:** k = 2，a[] = {3，8，17，5}
> **输出:**这 10 个不同的整数是:
> 6 8 10 11 13 16 20 22 25 34
> 选择的 2 个元素是:
> 3+3 = 6，5+3 = 8，5+5 = 10，8+3 = 11，8+5 = 13
> 8+8 = 16，17+3 = 20
> 
> **输入:** k = 3，a[] = {3，8，17}
> **输出:**这 10 个不同的整数是:
> 9 14 19 23 24 28 33 37 42 51

**方法:**用递归的方法解决问题。所有的组合都是要尝试的，当选择的元素个数等于 k 时，我们保留[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)中形成的*数*，这样重复的元素就不会被重复计算两次。函数 ***generateNumber(int count，int a[]，int n，int num，int k)*** 是一个递归函数，其中的基本情况是当计数变为 K 时，这表示已经从数组中选择了 K 个元素。参数中的*数字*表示由数字的计数形成的数字。在函数中，迭代数组，对于每个元素，调用递归函数，count 为 count+1，num 为 num+a[i]。

下面是上述方法的实现:

## C++

```
// C++ program to print all distinct
// integers that can be formed by K numbers
// from a given array of N numbers.
#include <bits/stdc++.h>
using namespace std;

// stores all the distinct integers formed
set<int> s;

// Function to generate all possible numbers
void generateNumber(int count, int a[], int n,
                    int num, int k)
{

    // Base case when K elements
    // are chosen
    if (k == count) {
        // insert it in set
        s.insert(num);
        return;
    }

    // Choose every element and call the function
    for (int i = 0; i < n; i++) {
        generateNumber(count + 1, a, n, num + a[i], k);
    }
}
// Function to print the distinct integers
void printDistinctIntegers(int k, int a[], int n)
{
    generateNumber(0, a, n, 0, k);
    cout << "The " << s.size()
         << " distinct integers are:\n";

    // prints all the elements in the set
    while (!s.empty()) {
        cout << *s.begin() << " ";

        // erase the number after printing it
        s.erase(*s.begin());
    }
}
// Driver Code
int main()
{
    int a[] = { 3, 8, 17, 5 };
    int n = sizeof(a) / sizeof(a[0]);
    int k = 2;

    // Calling Function
    printDistinctIntegers(k, a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all
// distinct integers that can
// be formed by K numbers from
// a given array of N numbers.
import java.util.*;
import java.lang.*;

class GFG
{
    // stores all the distinct
    // integers formed
    static TreeSet<Integer> set =
                   new TreeSet<Integer>();

    // Function to generate
    // all possible numbers
    public static void generateNumber(int count, int a[],
                                      int n, int num, int k)
    {
        // Base case when K
        // elements are chosen
        if(count == k)
        {
            set.add(num);
            return;
        }

        // Choose every element
        // and call the function
        for(int i = 0; i < n; i++)
        generateNumber(count + 1, a, n,
                       num + a[i], k);
    }

    // Function to print
    // the distinct integers
    public static void printDistinctIntegers(int k,
                                             int a[], int n)
    {
        generateNumber(0, a, n, 0, k);
        System.out.print("The" + " " + set.size() +
                         " " + "distinct integers are: ");
        System.out.println();
        Iterator<Integer> i = set.iterator();

        // prints all the
        // elements in the set
        while(set.isEmpty() == false)
        {

            while(i.hasNext())
            {
                System.out.print(i.next() + " ");
                //set.remove(i.next());
            }  
        }
    }

    // Driver Code
    public static void main (String[] args)
    {
        int arr[] = {3, 8, 17, 5};
        int n = arr.length;
        int k = 2;

        // Calling Function
        printDistinctIntegers(k, arr, n);
    }
}
```

## 蟒蛇 3

```
# Python3 program to print all distinct
# integers that can be formed by K numbers
# from a given array of N numbers.

# stores all the distinct integers formed
s = set()

# Function to generate all possible numbers
def generateNumber(count, a, n, num, k):

    # Base case when K elements are chosen
    if k == count:

        # insert it in set
        s.add(num)
        return

    # Choose every element and call the function
    for i in range(0, n):
        generateNumber(count + 1, a, n,    
                         num + a[i], k)

# Function to print the distinct integers
def printDistinctIntegers(k, a, n):

    generateNumber(0, a, n, 0, k)
    print("The", len(s),
          "distinct integers are:")

    # prints all the elements in the set
    for i in sorted(s):
        print(i, end = " ")

# Driver Code
if __name__ == "__main__":

    a = [3, 8, 17, 5]
    n, k = len(a), 2

    # Calling Function
    printDistinctIntegers(k, a, n)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to print all
// distinct integers that can
// be formed by K numbers from
// a given array of N numbers.
using System;
using System.Collections.Generic;

class GFG
{
    // stores all the distinct
    // integers formed
    static SortedSet<int> set =
                new SortedSet<int>();

    // Function to generate
    // all possible numbers
    public static void generateNumber(int count, int []a,
                                    int n, int num, int k)
    {
        // Base case when K
        // elements are chosen
        if(count == k)
        {
            set.Add(num);
            return;
        }

        // Choose every element
        // and call the function
        for(int i = 0; i < n; i++)
        generateNumber(count + 1, a, n,
                    num + a[i], k);
    }

    // Function to print
    // the distinct integers
    public static void printDistinctIntegers(int k,
                                            int []a, int n)
    {
        generateNumber(0, a, n, 0, k);
        Console.Write("The" + " " + set.Count +
                        " " + "distinct integers are: ");
        Console.WriteLine();

        // prints all the
        // elements in the set
        foreach(int sets in set)
        {
                Console.Write(sets + " ");

        }
    }

    // Driver Code
    public static void Main (String[] args)
    {
        int []arr = {3, 8, 17, 5};
        int n = arr.Length;
        int k = 2;

        // Calling Function
        printDistinctIntegers(k, arr, n);
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to print all distinct
// integers that can be formed by K numbers
// from a given array of N numbers.

// stores all the distinct integers formed
var s = new Set();

// Function to generate all possible numbers
function generateNumber(count, a, n, num, k)
{

    // Base case when K elements
    // are chosen
    if (k == count)
    {

        // Insert it in set
        s.add(num);
        return;
    }

    // Choose every element and call the function
    for(var i = 0; i < n; i++)
    {
        generateNumber(count + 1, a, n,
                         num + a[i], k);
    }
}

// Function to print the distinct integers
function printDistinctIntegers(k, a, n)
{
    generateNumber(0, a, n, 0, k);
    document.write("The " + s.size +
                   " distinct integers are:<br>");

    // prints all the elements in the set
    while (s.size != 0)
    {
        var tmp = [...s].sort((a, b) => a - b)[0]
        document.write(tmp + " ");

        // Erase the number after printing it
        s.delete(tmp);
    }
}

// Driver Code
var a = [ 3, 8, 17, 5 ];
var n = a.length;
var k = 2;

// Calling Function
printDistinctIntegers(k, a, n);

// This code is contributed by itsok

</script>
```

**Output:** 

```
The 10 distinct integers are:
6 8 10 11 13 16 20 22 25 34
```