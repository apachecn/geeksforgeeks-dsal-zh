# 检查 K 是否可以通过对数组的任意排列进行算术运算得到

> 原文:[https://www . geeksforgeeks . org/check-if-k-可通过对数组的任意排列执行算术运算获得/](https://www.geeksforgeeks.org/check-if-k-can-be-obtained-by-performing-arithmetic-operations-on-any-permutation-of-an-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 和一个整数 **K** ，任务是检查在分配算术运算符( **+、-、/、*** )后为给定数组的任何排列形成的表达式是否给出值 **K** 。如果发现为真，则打印执行操作的顺序。否则，打印**-1”**。
**注意:**应用除法运算符“/”后，结果可以是浮点数。

**示例:**

> **输入:** arr[] = {2，0，0，2}，K = 4
> **输出:** 2 + 0 = > 2 + 2 = > 4 + 0 = > 4
> 
> **输入:** arr[] = {1，2，4，7}，K = 50
> **输出:** -1

**方法:**思路是使用[回溯](https://www.geeksforgeeks.org/backtracking-introduction/)，通过生成赋值运算符的所有可能组合，找到结果方程的值。以下是步骤:

1.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并选择前两个元素，应用所有可能的操作。让上述操作的结果为 **X** 。
2.  现在，对 **X** 和数组的下一个元素执行所有可能的操作，以此类推。
3.  重复以上所有步骤，直到执行所有可能的操作组合。
4.  现在，如果任何操作组合产生结果 **K** ，则打印该组合。
5.  否则，打印“**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function that finds the string of
// possible combination of operations
bool find(vector<double>& v, int n,
          double dest, string s)
{
    // If only one number left then
    // check for result
    if (n == 1) {

        // If resultant value is K
        if (abs(v[0] - dest) <= 0.0000001) {

            cout << s + to_string(int(dest))
                 << " ";
            return 1;
        }

        // Else return 0
        return 0;
    }

    // Choose all combination of numbers
    // and operators and operate them
    for (int i = 0; i < n; i++) {

        for (int j = i + 1; j < n; j++) {

            double a = v[i], b = v[j];

            // Choose the first two and
            // operate it with '+'
            string p = s;
            v[i] = a + b;

            // Place it to 0th position
            v[j] = v[n - 1];

            // Place (n-1)th element on
            // 1st position
            s = (s + to_string(int(a)) + '+'
                 + to_string(int(b))
                 + " => ");

            // Evaluate the expression
            // with current combination
            if (find(v, n - 1, dest, s))
                return 1;

            // Now, we have N - 1 elements
            s = p;

            v[i] = a - b;

            // Try '-' operation
            v[j] = v[n - 1];

            s = (s + to_string(int(a)) + '-'
                 + to_string(int(b))
                 + " => ");

            // Evaluate the expression
            // with current combination
            if (find(v, n - 1, dest, s))
                return 1;
            s = p;

            v[i] = b - a;

            // Try reverse '-'
            v[j] = v[n - 1];

            s = (s + to_string(int(b)) + '-'
                 + to_string(int(a))
                 + " => ");

            // Evaluate the expression
            // with current combination
            if (find(v, n - 1, dest, s))
                return 1;
            s = p;

            v[i] = a * b;

            // Try '*' operation
            v[j] = v[n - 1];
            s = (s + to_string(int(a))
                 + '*'
                 + to_string(int(b))
                 + " => ");

            // Evaluate the expression
            // with current combination
            if (find(v, n - 1, dest, s))
                return 1;

            s = p;

            if (b != 0) {

                v[i] = a / b;

                // Try '/'
                v[j] = v[n - 1];

                s = (s + to_string(int(a))
                     + '/'
                     + to_string(int(b))
                     + " => ");

                // Evaluate the expression
                // with current combination
                if (find(v, n - 1, dest, s))
                    return 1;
            }

            s = p;

            if (a != 0) {

                v[i] = b / a;

                // Try reverse '/'
                v[j] = v[n - 1];
                s = (s + to_string(int(b))
                     + '/'
                     + to_string(int(a))
                     + " => ");

                // Evaluate the expression
                // with current combination
                if (find(v, n - 1, dest, s))
                    return 1;
            }

            s = p;

            // Backtracking Step
            v[i] = a;
            v[j] = b;
        }
    }

    // Return 0 if there doesnt exist
    // any combination that gives K
    return 0;
}

// Function that finds the possible
// combination of operation to get the
// resultant value K
void checkPossibleOperation(
    vector<double>& arr, double K)
{
    // Store the resultant operation
    string s = "";

    // Function Call
    if (!find(arr, arr.size(), K, s)) {
        cout << "-1";
    }
}

// Driver Code
int main()
{
    // Given array arr[]
    vector<double> arr = { 2, 0, 0, 2 };

    // Resultant value K
    double K = 4;

    // Function Call
    checkPossibleOperation(arr, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
class GFG{

// Function that finds the string of
// possible combination of operations
static boolean find(double[] v, int n,
                    double dest, String s)
{

    // If only one number left then
    // check for result
    if (n == 1)
    {

        // If resultant value is K
        if (Math.abs(v[0] - dest) <= 0.0000001)
        {
            System.out.println(s +
            String.valueOf((int)dest) + " ");

            return true;
        }

    // Else return 0
    return false;
    }

    // Choose all combination of numbers
    // and operators and operate them
    for(int i = 0; i < n; i++)
    {
        for(int j = i + 1; j < n; j++)
        {
            double a = v[i], b = v[j];

            // Choose the first two and
            // operate it with '+'
            String p = s;
            v[i] = a + b;

            // Place it to 0th position
            v[j] = v[n - 1];

            // Place (n-1)th element on
            // 1st position
            s = (s + String.valueOf((int)a) +
               '+' + String.valueOf((int)b) +
                " => ");

            // Evaluate the expression
            // with current combination
            if (find(v, n - 1, dest, s))
                return true;

            // Now, we have N - 1 elements
            s = p;

            v[i] = a - b;

            // Try '-' operation
            v[j] = v[n - 1];

            s = (s + String.valueOf((int)a) +
               '-' + String.valueOf((int)b) +
                " => ");

            // Evaluate the expression
            // with current combination
            if (find(v, n - 1, dest, s))
                return true;

            s = p;
            v[i] = b - a;

            // Try reverse '-'
            v[j] = v[n - 1];

            s = (s + String.valueOf((int)b) +
               '-' + String.valueOf((int)a) +
                " => ");

            // Evaluate the expression
            // with current combination
            if (find(v, n - 1, dest, s))
                return true;

            s = p;
            v[i] = a * b;

            // Try '*' operation
            v[j] = v[n - 1];
            s = (s + String.valueOf((int)a) +
               '*' + String.valueOf((int)b) +
                " => ");

            // Evaluate the expression
            // with current combination
            if (find(v, n - 1, dest, s))
                return true;

            s = p;

            if (b != 0)
            {
                v[i] = a / b;

                // Try '/'
                v[j] = v[n - 1];

                s = (s + String.valueOf((int)a) +
                   '/' + String.valueOf((int)b) +
                    " => ");

                // Evaluate the expression
                // with current combination
                if (find(v, n - 1, dest, s))
                    return true;
            }
            s = p;

            if (a != 0)
            {
                v[i] = b / a;

                // Try reverse '/'
                v[j] = v[n - 1];
                s = (s + String.valueOf((int)b) +
                   '/' + String.valueOf((int)a) +
                    " => ");

                // Evaluate the expression
                // with current combination
                if (find(v, n - 1, dest, s))
                    return true;
            }
            s = p;

            // Backtracking Step
            v[i] = a;
            v[j] = b;
        }
    }

    // Return 0 if there doesnt exist
    // any combination that gives K
    return false;
}

// Function that finds the possible
// combination of operation to get the
// resultant value K
static void checkPossibleOperation(double[] arr,
                                   double K)
{

    // Store the resultant operation
    String s = "";

    // Function call
    if (!find(arr, arr.length, K, s))
    {
        System.out.println("-1");
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    double[] arr = { 2, 0, 0, 2 };

    // Resultant value K
    double K = 4;

    // Function call
    checkPossibleOperation(arr, K);
}
}

// This code is contributed by Dadi Madhav
```

## 蟒蛇 3

```
# Python3 program for the above approach
# Function that finds the string of
# possible combination of operations
def find(v, n, dest, s):

    # If only one number left then
    # check for result
    if (n == 1):

        # If resultant value is K
        if (abs(v[0] - dest) <= 0.0000001):
            print (s + str(int(dest)) ,end = " ")
            return 1

        #;Else return 0
        return 0

    # Choose all combination of numbers
    # and operators and operate them
    for i in range (n):
        for j in range (i + 1,  n):
            a = v[i]
            b = v[j]

            # Choose the first two and
            # operate it with '+'
            p = s
            v[i] = a + b

            # Place it to 0th position
            v[j] = v[n - 1]

            # Place (n-1)th element on
            # 1st position
            s = (s + str(int(a)) + '+' +
                 str(int(b)) + " => ")

            # Evaluate the expression
            # with current combination
            if (find(v, n - 1, dest, s)):
                return 1

            # Now, we have N - 1 elements
            s = p

            v[i] = a - b

            # Try '-' operation
            v[j] = v[n - 1]

            s = (s + str(int(a)) + '-' +
                 str(int(b)) +" => ")

            # Evaluate the expression
            # with current combination
            if (find(v, n - 1, dest, s)):
                return 1
            s = p
            v[i] = b - a

            # Try reverse '-'
            v[j] = v[n - 1]

            s = (s + str(int(b)) + '-' +
                 str(int(a)) + " => ")

            # Evaluate the expression
            # with current combination
            if (find(v, n - 1, dest, s)):
                return 1
            s = p
            v[i] = a * b

            # Try '*' operation
            v[j] = v[n - 1]
            s = (s + str(int(a)) + '*' +
                 str(int(b)) + " => ");

            # Evaluate the expression
            # with current combination
            if (find(v, n - 1, dest, s)):
                return 1
            s = p

            if (b != 0):
                v[i] = a // b

                # Try '/'
                v[j] = v[n - 1]

                s = (s + str(int(a)) + '/' +
                     str(int(b)) + " => ")

                # Evaluate the expression
                # with current combination
                if (find(v, n - 1, dest, s)):
                    return 1
            s = p

            if (a != 0):
                v[i] = b // a

                # Try reverse '/'
                v[j] = v[n - 1]
                s = (s + str(int(b)) + '/' +
                     str(int(a)) + " => ")

                # Evaluate the expression
                # with current combination
                if (find(v, n - 1, dest, s)):
                    return 1         
            s = p

            # Backtracking Step
            v[i] = a
            v[j] = b

    # Return 0 if there doesnt exist
    # any combination that gives K
    return 0

# Function that finds the possible
# combination of operation to get the
# resultant value K
def checkPossibleOperation(arr, K):

    # Store the resultant operation
    s = ""

    # Function Call
    if (not find(arr, len(arr), K, s)):
        print ("-1")

# Driver Code
if __name__ == "__main__":

    # Given array arr[]
    arr = [2, 0, 0, 2]

    # Resultant value K
    K = 4

    # Function Call
    checkPossibleOperation(arr, K)

#This code is contributed by Chitranayal
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function that finds the string of
// possible combination of operations
static bool find(double[] v, int n,
                 double dest, String s)
{
  // If only one number left then
  // check for result
  if (n == 1)
  {
    // If resultant value is K
    if (Math.Abs(v[0] - dest) <= 0.0000001)
    {
      Console.WriteLine(s + String.Join("",
                                        (int)dest) + " ");
      return true;
    }

    // Else return 0
    return false;
  }

  // Choose all combination of numbers
  // and operators and operate them
  for(int i = 0; i < n; i++)
  {
    for(int j = i + 1; j < n; j++)
    {
      double a = v[i], b = v[j];

      // Choose the first two and
      // operate it with '+'
      String p = s;
      v[i] = a + b;

      // Place it to 0th position
      v[j] = v[n - 1];

      // Place (n-1)th element on
      // 1st position
      s = (s + String.Join("", (int)a) +
           '+' + String.Join("", (int)b) +
           " => ");

      // Evaluate the expression
      // with current combination
      if (find(v, n - 1, dest, s))
        return true;

      // Now, we have N - 1 elements
      s = p;

      v[i] = a - b;

      // Try '-' operation
      v[j] = v[n - 1];

      s = (s + String.Join("", (int)a) +
           '-' + String.Join("", (int)b) +
           " => ");

      // Evaluate the expression
      // with current combination
      if (find(v, n - 1, dest, s))
        return true;

      s = p;
      v[i] = b - a;

      // Try reverse '-'
      v[j] = v[n - 1];

      s = (s + String.Join("", (int)b) +
           '-' + String.Join("", (int)a) +
           " => ");

      // Evaluate the expression
      // with current combination
      if (find(v, n - 1, dest, s))
        return true;

      s = p;
      v[i] = a * b;

      // Try '*' operation
      v[j] = v[n - 1];
      s = (s + String.Join("", (int)a) +
           '*' + String.Join("", (int)b) +
           " => ");

      // Evaluate the expression
      // with current combination
      if (find(v, n - 1, dest, s))
        return true;

      s = p;

      if (b != 0)
      {
        v[i] = a / b;

        // Try '/'
        v[j] = v[n - 1];

        s = (s + String.Join("", (int)a) +
             '/' + String.Join("", (int)b) +
             " => ");

        // Evaluate the expression
        // with current combination
        if (find(v, n - 1, dest, s))
          return true;
      }
      s = p;

      if (a != 0)
      {
        v[i] = b / a;

        // Try reverse '/'
        v[j] = v[n - 1];
        s = (s + String.Join("", (int)b) +
             '/' + String.Join("", (int)a) +
             " => ");

        // Evaluate the expression
        // with current combination
        if (find(v, n - 1, dest, s))
          return true;
      }
      s = p;

      // Backtracking Step
      v[i] = a;
      v[j] = b;
    }
  }

  // Return 0 if there doesnt exist
  // any combination that gives K
  return false;
}

// Function that finds the possible
// combination of operation to get the
// resultant value K
static void checkPossibleOperation(double[] arr,
                                   double K)
{
  // Store the resultant operation
  String s = "";

  // Function call
  if (!find(arr, arr.Length, K, s))
  {
    Console.WriteLine("-1");
  }
}

// Driver Code
public static void Main(String[] args)
{   
  // Given array []arr
  double[] arr = {2, 0, 0, 2};

  // Resultant value K
  double K = 4;

  // Function call
  checkPossibleOperation(arr, K);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript program for above approach

// Function that finds the string of
// possible combination of operations
function find(v,n,dest,s)
{
    // If only one number left then
    // check for result
    if (n == 1)
    {

        // If resultant value is K
        if (Math.abs(v[0] - dest) <= 0.0000001)
        {
            document.write(s +
            (dest).toString() + " <br>");

            return true;
        }

    // Else return 0
    return false;
    }

    // Choose all combination of numbers
    // and operators and operate them
    for(let i = 0; i < n; i++)
    {
        for(let j = i + 1; j < n; j++)
        {
            let a = v[i], b = v[j];

            // Choose the first two and
            // operate it with '+'
            let p = s;
            v[i] = a + b;

            // Place it to 0th position
            v[j] = v[n - 1];

            // Place (n-1)th element on
            // 1st position
            s = (s + a.toString() +
               '+' + b.toString() +
                " => ");

            // Evaluate the expression
            // with current combination
            if (find(v, n - 1, dest, s))
                return true;

            // Now, we have N - 1 elements
            s = p;

            v[i] = a - b;

            // Try '-' operation
            v[j] = v[n - 1];

            s = (s + a.toString() +
               '-' + b.toString() +
                " => ");

            // Evaluate the expression
            // with current combination
            if (find(v, n - 1, dest, s))
                return true;

            s = p;
            v[i] = b - a;

            // Try reverse '-'
            v[j] = v[n - 1];

            s = (s + b.toString() +
               '-' + a.toString() +
                " => ");

            // Evaluate the expression
            // with current combination
            if (find(v, n - 1, dest, s))
                return true;

            s = p;
            v[i] = a * b;

            // Try '*' operation
            v[j] = v[n - 1];
            s = (s + a.toString() +
               '*' + b.toString() +
                " => ");

            // Evaluate the expression
            // with current combination
            if (find(v, n - 1, dest, s))
                return true;

            s = p;

            if (b != 0)
            {
                v[i] = a / b;

                // Try '/'
                v[j] = v[n - 1];

                s = (s + a.toString() +
                   '/' + b.toString() +
                    " => ");

                // Evaluate the expression
                // with current combination
                if (find(v, n - 1, dest, s))
                    return true;
            }
            s = p;

            if (a != 0)
            {
                v[i] = b / a;

                // Try reverse '/'
                v[j] = v[n - 1];
                s = (s + b.toString() +
                   '/' + a.toString() +
                    " => ");

                // Evaluate the expression
                // with current combination
                if (find(v, n - 1, dest, s))
                    return true;
            }
            s = p;

            // Backtracking Step
            v[i] = a;
            v[j] = b;
        }
    }

    // Return 0 if there doesnt exist
    // any combination that gives K
    return false;
}

// Function that finds the possible
// combination of operation to get the
// resultant value K
function checkPossibleOperation(arr,k)
{
    // Store the resultant operation
    let s = "";

    // Function call
    if (!find(arr, arr.length, K, s))
    {
        document.write("-1");
    }
}

// Driver Code
// Given array arr[]
let arr=[2, 0, 0, 2 ];
// Resultant value K
let K = 4;
// Function call
checkPossibleOperation(arr, K);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
2+0 => 2+2 => 4+0 => 4
```

***时间复杂度:** O(N！*4 <sup>N</sup> )*
***辅助空间:** O(N)*