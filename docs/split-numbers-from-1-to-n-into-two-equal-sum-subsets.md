# 将从 1 到 N 的数字分成两个相等的和子集

> 原文:[https://www . geesforgeks . org/split-numbers-from-1-n-in-two-equal-sum-subset/](https://www.geeksforgeeks.org/split-numbers-from-1-to-n-into-two-equal-sum-subsets/)

给定一个整数 **N** ，任务是将从 **1** 到 **N** 的数字分成两个非空子集，使得集合中元素的和相等。打印子集中的元素。如果我们不能形成任何子集，那么打印 **-1** 。

**示例:**

> **输入** N = 4
> **输出:**
> 子集 1 的大小为:2
> 子集的元素为:1 4
> 子集 2 的大小为:2
> 子集的元素为:2 3
> **说明:**
> 第一个和第二个集合的和相等即 5。
> 
> **输入:** N = 8
> **输出:**
> 子集 1 的大小为:4
> 子集的元素为:1 8 3 6
> 子集 2 的大小为:4
> 子集的元素为:2 7 4 5
> **说明:**
> 第一个和第二个集合的和相等即 1 8。

**方法:**为了解决上面提到的问题，我们必须观察整数 **N.** 的三种情况。以下是观察结果:

1.  **前 N 个自然数之和为奇数**:解不出来，答案为-1。因为我们不能把奇数和分成 2 个相等的一半。
2.  **前 N 个自然数之和为偶数:**只需从最后一个元素循环到第一个元素，取集合-1 中值小于和的一半的元素，维护另一个集合-2，存储集合-1 中未包含的 ans。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// function to display elements
void display(vector<int> &v) {
  for (auto i : v) {
    cout << i << " ";
  }
  cout << endl;
}

void FindAns(int n) {

  // sum of first n natural numbers
  int sum = n * (n + 1) / 2;

  // two array to store two sets
  vector<int> a, b;

  // if sum is odd then we can't split in two sets
  if (sum % 2 == 1) {
    cout << -1 << endl;
    return;
  }
  else {
    int ans = sum / 2; // for dividing into two sets

    // traverse from last element and include those who's values are less than or equal to ans

    for (int i = n; i >= 1; i--) {

      //  if we can include in our set then take it
      if (i <= ans) {
        a.push_back(i);
        ans -= i;
      }
      //  else move it to other set
      else {
        b.push_back(i);
      }
    }
    // print the elements of first set
    cout << "Size of subset 1 is : ";
    cout << a.size() << endl;
    cout << "Elements of subset are : ";
    display(a);

    // print the elements of second set
    cout << "Size of subset 2 is : ";
    cout << b.size() << endl;
    cout << "Elements of subset are : ";
    display(b);
  }
}

// Driver code
int main() {
  // Given number
  int n = 8;

  // function call
  FindAns(n);

  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to print the two set
public static void findAns(int N)
{
    // Base case
    if (N <= 2)
    {
        System.out.print("-1");
        return;
    }

    // Sum of first numbers upto N
    int value = (N * (N + 1)) / 2;

    // Answer don't exist
      if(value&1)
    {
      System.out.print("-1");
      return;
    }

    // To store the first set
    Vector<Integer> v1 = new Vector<Integer>();

    // To store the second set
    Vector<Integer> v2 = new Vector<Integer>();

    // When N is even
    if ((N & 1) == 0)
    {
        int turn = 1;
        int start = 1;
        int last = N;
        while (start < last)
        {
            if (turn == 1)
            {
                v1.add(start);
                v1.add(last);
                turn = 0;
            }
            else
            {
                v2.add(start);
                v2.add(last);
                turn = 1;
            }

            // Increment start
            start++;

            // Decrement last
            last--;
        }
    }

    // When N is odd
    else
    {

        // Required sum of the subset
        int rem = value / 2;

        // Boolean array to keep
        // track of used elements
        boolean[] vis = new boolean[N + 1];

        for(int i = 1; i <= N; i++)
            vis[i] = false;

        vis[0] = true;

        // Iterate from N to 1
        for(int i = N; i >= 1; i--)
        {
            if (rem > i)
            {
                v1.add(i);
                vis[i] = true;
                rem -= i;
            }
            else
            {
                v1.add(rem);
                vis[rem] = true;
                break;
            }
        }

        // Assigning the unused
        // elements to second subset
        for(int i = 1; i <= N; i++)
        {
            if (!vis[i])
                v2.add(i);
        }
    }

    // Print the elements of first set
    System.out.print("Size of subset 1 is: ");
    System.out.println(v1.size());
    System.out.print("Elements of the subset are: ");

    for(Integer c : v1)    
        System.out.print(c + " ");

    System.out.println();

    // Print the elements of second set
    System.out.print("Size of subset 2 is: ");
    System.out.println(v2.size());
    System.out.print("Elements of the subset are: ");

    for(Integer c : v2)    
        System.out.print(c + " ");
}

// Driver code
public static void main(String[] args)
{

    // Given Number
    int N = 8;

    // Function Call
    findAns(N);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to print
# the two set
def findAns(N):

    # Base case
    if (N <= 2):
        print ("-1")
        return

    # Sum of first numbers upto N
    value = (N * (N + 1)) // 2

    # Answer don't exist
    if(value & 1):
        print ("-1")
        return

    # To store the first set
    v1 = []

    # To store the second set
    v2 = []

    # When N is even
    if (not (N & 1)):
        turn = 1
        start = 1
        last = N

        while (start < last):
            if (turn):
                v1.append(start)
                v1.append(last)
                turn = 0           
            else:
                v2.append(start)
                v2.append(last)
                turn = 1

            # Increment start
            start += 1

            # Decrement last
            last -= 1

    # When N is odd
    else:

        # Required sum of
        # the subset
        rem = value // 2

        # Boolean array to keep
        # track of used elements
        vis = [False] * (N + 1)

        for i in range (1, N + 1):
            vis[i] = False

        vis[0] = True

        # Iterate from N to 1
        for i in range (N , 0, -1):
            if (rem > i):
                v1.append(i)
                vis[i] = True
                rem -= i           
            else:
                v1.append(rem)
                vis[rem] = True
                break

        # Assigning the unused
        # elements to second subset
        for i in range (1, N + 1):
            if (not vis[i]):
               v2.append(i)

    # Print the elements of
    # first set
    print ("Size of subset 1 is: ",
           end = "")
    print (len( v1))
    print ("Elements of the subset are: ",
           end = "")

    for c in v1:
      print (c, end = " ")

    print ()

    # Print the elements of
    # second set
    print ("Size of subset 2 is: ",
           end = "")
    print(len( v2))
    print ("Elements of the subset are: ",
           end = "")

    for c in v2:
       print (c, end = " ")

# Driver Code
if __name__ == "__main__":

    # Given Number
    N = 8

    # Function Call
    findAns(N)

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to print the two set
public static void findAns(int N)
{

    // Base case
    if (N <= 2)
    {
        Console.Write("-1");
        return;
    }

    // Sum of first numbers upto N
    int value = (N * (N + 1)) / 2;

    // Answer don't exist
    if(value&1)
    {
      Console.Write("-1");
      return;
    }

    // To store the first set
    List<int> v1 = new List<int>();

    // To store the second set
    List<int> v2 = new List<int>();

    // When N is even
    if ((N & 1) == 0)
    {
        int turn = 1;
        int start = 1;
        int last = N;

        while (start < last)
        {
            if (turn == 1)
            {
                v1.Add(start);
                v1.Add(last);
                turn = 0;
            }
            else
            {
                v2.Add(start);
                v2.Add(last);
                turn = 1;
            }

            // Increment start
            start++;

            // Decrement last
            last--;
        }
    }

    // When N is odd
    else
    {

        // Required sum of the subset
        int rem = value / 2;

        // Boolean array to keep
        // track of used elements
        bool[] vis = new bool[N + 1];

        for(int i = 1; i <= N; i++)
            vis[i] = false;

        vis[0] = true;

        // Iterate from N to 1
        for(int i = N; i >= 1; i--)
        {
            if (rem > i)
            {
                v1.Add(i);
                vis[i] = true;
                rem -= i;
            }
            else
            {
                v1.Add(rem);
                vis[rem] = true;
                break;
            }
        }

        // Assigning the unused
        // elements to second subset
        for(int i = 1; i <= N; i++)
        {
            if (!vis[i])
                v2.Add(i);
        }
    }

    // Print the elements of first set
    Console.Write("Size of subset 1 is: ");
    Console.WriteLine(v1.Count);
    Console.Write("Elements of the subset are: ");

    foreach(int c in v1)    
        Console.Write(c + " ");

    Console.WriteLine();

    // Print the elements of second set
    Console.Write("Size of subset 2 is: ");
    Console.WriteLine(v2.Count);
    Console.Write("Elements of the subset are: ");

    foreach(int c in v2)    
        Console.Write(c + " ");
}

// Driver code
public static void Main(String[] args)
{

    // Given number
    int N = 8;

    // Function call
    findAns(N);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to print the two set
function findAns(N)
{
    // Base case
    if (N <= 2)
    {
        document.write("-1");
        return;
    }

    // Sum of first numbers upto N
    let value = Math.floor((N * (N + 1)) / 2);

    // Answer don't exist
      if(value&1)
    {
      document.write("-1");
      return;
    }

    // To store the first set
    let v1 = [];

    // To store the second set
    let v2 = [];

    // When N is even
    if ((N & 1) == 0)
    {
        let turn = 1;
        let start = 1;
        let last = N;
        while (start < last)
        {
            if (turn == 1)
            {
                v1.push(start);
                v1.push(last);
                turn = 0;
            }
            else
            {
                v2.push(start);
                v2.push(last);
                turn = 1;
            }

            // Increment start
            start++;

            // Decrement last
            last--;
        }
    }

    // When N is odd
    else
    {

        // Required sum of the subset
        let rem = Math.floor(value / 2);

        // Boolean array to keep
        // track of used elements
        let vis = new Array(N + 1);

        for(let i = 1; i <= N; i++)
            vis[i] = false;

        vis[0] = true;

        // Iterate from N to 1
        for(let i = N; i >= 1; i--)
        {
            if (rem > i)
            {
                v1.push(i);
                vis[i] = true;
                rem -= i;
            }
            else
            {
                v1.push(rem);
                vis[rem] = true;
                break;
            }
        }

        // Assigning the unused
        // elements to second subset
        for(let i = 1; i <= N; i++)
        {
            if (!vis[i])
                v2.push(i);
        }
    }

    // Print the elements of first set
    document.write("Size of subset 1 is: ");
    document.write(v1.length+'<br>');
    document.write("Elements of the subset are: ");

    for(let c=0;c<v1.length;c++)   
        document.write(v1 + " ");

    document.write("<br>");

    // Print the elements of second set
    document.write("Size of subset 2 is: ");
    document.write(v2.length+"<br>");
    document.write("Elements of the subset are: ");

    for(let c=0;c< v2.length;c++)   
        document.write(v2 + " ");
}

// Driver code
// Given Number
let N = 8;

// Function Call
findAns(N);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
Size of subset 1 is: 4
Elements of the subset are: 1 8 3 6 
Size of subset 2 is: 4
Elements of the subset are: 2 7 4 5
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(N)*