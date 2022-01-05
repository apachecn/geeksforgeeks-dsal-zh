# 生成一个序列，使得数组元素的浮点除法最大化

> 原文:[https://www . geeksforgeeks . org/generate-a-sequence-so-float-division-of-array-elements-被最大化/](https://www.geeksforgeeks.org/generate-a-sequence-such-that-float-division-of-array-elements-is-maximized/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是使用括号**'(**和**')**和除法运算符**/**找到表达式，以最大化数组元素的后续[浮点除法](https://www.geeksforgeeks.org/program-compute-division-upto-n-decimal-places/)的表达式值。

**示例:**

> **输入:** arr[] = {1000，100，10，2}
> **输出:**“1000/(100/10/2)”
> **说明:**
> 表达式 1000/(100/10/2)的值可以计算为 1000/((100/10)/2) = 200。
> 
> **输入:** arr[] = {2，3，4}
> **输出:**“2/(3/4)”

**方法:**这个想法是基于这样的观察:对于每个除法，只有当分母最小时，结果才是最大的。因此，任务简化为以分母最小的方式放置括号和运算符。考虑下面的例子来解决这个问题:

> 考虑一个表达式 **1000 / 100 / 10 / 2** 。
> 要使其值最大，分母需要最小化。因此，分母需要在序列 100、10、2 中。
> 现在，考虑以下情况:
> 
> *   100 / (10 / 2) = (100 × 2) / 10 = 20
> *   (100 / 10) / 2 = 10 / 2 = 5
> 
> 因此，对于第二种情况，获得了表达式的最小值。因此，1000 / (100 / 10 / 2)是所需的序列。

因此，从上面的例子可以得出结论，括号需要放在序列的第一个整数之后，这使得整个序列从第二个整数减少到最小值成为可能。
按照以下步骤解决问题:

*   初始化一个字符串 **S** 为 **""** ，存储最终表达式。
*   如果 **N** 等于 **1** ，则以字符串形式打印整数。
*   否则，追加 **S** 中的**arr【0】**、**/(**)，然后追加**arr【】**的所有剩余整数，用**/**隔开。
*   最后，在字符串 **S** 中追加**”**，打印字符串 **S** 作为结果。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to place the parenthesis
// such that the result is maximized
void generateSequence(int arr[], int n)
{
    // Store the required string
    string ans;

    // Add the first integer to string
    ans = to_string(arr[0]);

    // If the size of array is 1
    if (n == 1)
        cout << ans;

    // If the size of array is 2, print
    // the 1st integer followed by / operator
    // followed by the next integer
    else if (n == 2) {
        cout << ans + "/"
             << to_string(arr[1]);
    }

    // If size of array is exceeds two,
    // print 1st integer concatenated
    // with operators '/', '(' and next
    // integers with the operator '/'
    else {
        ans += "/(" + to_string(arr[1]);

        for (int i = 2; i < n; i++) {
            ans += "/" + to_string(arr[i]);
        }

        // Add parenthesis at the end
        ans += ")";

        // Print the final expression
        cout << ans;
    }
}

// Driver Code
int main()
{
    int arr[] = { 1000, 100, 10, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);
    generateSequence(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

// Function to place the parenthesis
// such that the result is maximized
static void generateSequence(int arr[], int n)
{

    // Store the required string
    String ans;

    // Add the first integer to string
    ans = Integer.toString(arr[0]);

    // If the size of array is 1
    if (n == 1)
        System.out.println(ans);

    // If the size of array is 2, print
    // the 1st integer followed by / operator
    // followed by the next integer
    else if (n == 2) {
        System.out.println(ans + "/"
            + Integer.toString(arr[1]));
    }

    // If size of array is exceeds two,
    // print 1st integer concatenated
    // with operators '/', '(' and next
    // integers with the operator '/'
    else {
        ans += "/(" + Integer.toString(arr[1]);

        for (int i = 2; i < n; i++) {
            ans += "/" + Integer.toString(arr[i]);
        }

        // Add parenthesis at the end
        ans += ")";

        // Print the final expression
        System.out.println(ans);
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1000, 100, 10, 2 };
    int N = arr.length;
    generateSequence(arr, N);
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to place the parenthesis
# such that the result is maximized
def generateSequence(arr, n):

    # Store the required string
    ans = ""

    # Add the first integer to string
    ans = str(arr[0])

    # If the size of array is 1
    if (n == 1):
        print(ans)

    # If the size of array is 2, print
    # the 1st integer followed by / operator
    # followed by the next integer
    elif (n == 2):
        print(ans + "/"+str(arr[1]))

    # If size of array is exceeds two,
    # pr1st integer concatenated
    # with operators '/', '(' and next
    # integers with the operator '/'
    else:
        ans += "/(" + str(arr[1])

        for i in range(2, n):
            ans += "/" + str(arr[i])

        # Add parenthesis at the end
        ans += ")"

        # Prthe final expression
        print(ans)

# Driver Code
if __name__ == '__main__':
    arr = [1000, 100, 10, 2]
    N = len(arr)
    generateSequence(arr, N)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

// Function to place the parenthesis
// such that the result is maximized
static void generateSequence(int []arr, int n)
{

    // Store the required string
    string ans="";

    // Add the first integer to string
    ans = arr[0].ToString();

    // If the size of array is 1
    if (n == 1)
        Console.WriteLine(ans);

    // If the size of array is 2, print
    // the 1st integer followed by / operator
    // followed by the next integer
    else if (n == 2) {
        Console.WriteLine(ans + "/"
            + arr[1].ToString());
    }

    // If size of array is exceeds two,
    // print 1st integer concatenated
    // with operators '/', '(' and next
    // integers with the operator '/'
    else {
        ans += "/(" + arr[1].ToString();

        for (int i = 2; i < n; i++) {
            ans += "/" + arr[i].ToString();
        }

        // Add parenthesis at the end
        ans += ")";

        // Print the final expression
        Console.WriteLine(ans);
    }
}

// Driver Code
public static void Main(string[] args)
{
    int []arr = { 1000, 100, 10, 2 };
    int N = arr.Length;
    generateSequence(arr, N);
}
}

// This code is contributed by chitranayal.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to place the parenthesis
// such that the result is maximized
function generateSequence(arr, n)
{
    // Store the required string
    var ans;

    // Add the first integer to string
    ans = (arr[0].toString());

    // If the size of array is 1
    if (n == 1)
        document.write( ans);

    // If the size of array is 2, print
    // the 1st integer followed by / operator
    // followed by the next integer
    else if (n == 2) {
        document.write( ans + "/"
             + (arr[1].toString()));
    }

    // If size of array is exceeds two,
    // print 1st integer concatenated
    // with operators '/', '(' and next
    // integers with the operator '/'
    else {
        ans += "/(" + (arr[1].toString());

        for (var i = 2; i < n; i++) {
            ans += "/" + (arr[i].toString());
        }

        // Add parenthesis at the end
        ans += ")";

        // Print the final expression
        document.write( ans);
    }
}

// Driver Code
var arr = [1000, 100, 10, 2];
var N = arr.length;
generateSequence(arr, N);

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
1000/(100/10/2)
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)