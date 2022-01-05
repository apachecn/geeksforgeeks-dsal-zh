# 找到满足给定条件的字典最小字符串

> 原文:[https://www . geeksforgeeks . org/find-满足给定条件的字典最小字符串/](https://www.geeksforgeeks.org/find-the-lexicographically-smallest-string-which-satisfies-the-given-condition/)

给定一个数组，**arr[]****N**整数，其中 **arr[i]** 表示字符串 **S** 的长度 **(i + 1)** 前缀中不同字符的数量。任务是找到满足给定前缀数组的字典最小字符串(如果存在)。字符串应该是小写英文字母[a-z]。如果不存在这样的字符串，则打印 **-1** 。

**示例:**

> **输入:** arr[] = {1，1，2，3}
> **输出:** aabc
> 前缀【0】有 1 个不同的字符
> 前缀【1】有 1 个不同的字符
> 前缀【2】有 2 个不同的字符
> 前缀【3】有 3 个不同的字符
> 并且字符串是最小的可能。
> 
> **输入:** arr[] = {1，2，2，3，3，4 }
> T3】输出: abacad
> 
> **输入:** arr[] = {1，1，3，3}
> **输出:** -1

**方法:**每个字符串的第一个字符总是**‘a’**。因为我们必须找到字典上最小的字符串。因此，如果长度为 **i** 和 **i + 1** 的前缀中不同字符的数量相同，那么 **(i+1)第**个字符将为 **'a'** ，否则它将是与长度为 **i** 的所有字符不同的字符，并且它将比长度为 **i** 的前缀中最大的字符大一个。

**例如**，如果前缀数组是 **{1，2，2，3，4}** ，那么第一个字符将是 **'a'** ，第二个字符将是 **'b'** ，因为不同字符的数量是 **2** (也可以是 **'c'** 或 **'d'** 等，但我们必须取字典上最小的)。第三个字符将是**‘a’**或**‘b’**但我们取**‘a’**，因为**“阿坝”**比**“abb”**小。
同样，第四个和第五个字符将分别是**‘c’**和**‘d’**。因此，满足给定前缀数组的结果字符串将是**“abacd”**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the required string
string smallestString(int N, int A[])
{
    // First character will always be 'a'
    char ch = 'a';

    // To store the resultant string
    string S = "";

    // Since length of the string should be
    // greater than 0 and first element
    // of array should be 1
    if (N < 1 || A[0] != 1) {
        S = "-1";
        return S;
    }

    S += ch;
    ch++;

    // Check one by one all element of given prefix array
    for (int i = 1; i < N; i++) {
        int diff = A[i] - A[i - 1];

        // If the difference between any two
        // consecutive elements of the prefix array
        // is greater than 1 then there will be no such
        // string possible that satisfies the given array
        // Also, string cannot have more than
        // 26 distinct characters
        if (diff > 1 || diff < 0 || A[i] > 26) {
            S = "-1";
            return S;
        }

        // If difference is 0 then the (i + 1)th character
        // will be same as the ith character
        else if (diff == 0)
            S += 'a';

        // If difference is 1 then the (i + 1)th character
        // will be different from the ith character
        else {
            S += ch;
            ch++;
        }
    }

    // Return the resultant string
    return S;
}

// Driver code
int main()
{
    int arr[] = { 1, 1, 2, 3, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << smallestString(n, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

    // Function to return the required string
    static String smallestString(int N, int []A)
    {
        // First character will always be 'a'
        char ch = 'a';

        // To store the resultant string
        String S = "";

        // Since length of the string should be
        // greater than 0 and first element
        // of array should be 1
        if (N < 1 || A[0] != 1)
        {
            S = "-1";
            return S;
        }

        S += ch;
        ch++;

        // Check one by one all element of given prefix array
        for (int i = 1; i < N; i++)
        {
            int diff = A[i] - A[i - 1];

            // If the difference between any two
            // consecutive elements of the prefix array
            // is greater than 1 then there will be no such
            // string possible that satisfies the given array
            // Also, string cannot have more than
            // 26 distinct characters
            if (diff > 1 || diff < 0 || A[i] > 26)
            {
                S = "-1";
                return S;
            }

            // If difference is 0 then the (i + 1)th character
            // will be same as the ith character
            else if (diff == 0)
                S += 'a';

            // If difference is 1 then the (i + 1)th character
            // will be different from the ith character
            else
            {
                S += ch;
                ch++;
            }
        }

        // Return the resultant string
        return S;
    }

    // Driver code
    public static void main(String args[])
    {
        int []arr = { 1, 1, 2, 3, 3 };
        int n = arr.length;
        System.out.println(smallestString(n, arr));
    }
}

// This code is contributed by Ryuga
```

## 蟒蛇 3

```
# Function to return the required string
def smallestString(N, A):

    # First character will always be 'a'
    ch = 'a'

    # To store the resultant string
    S = ""

    # Since length of the string should be
    # greater than 0 and first element
    # of array should be 1
    if (N < 1 or A[0] != 1):
        S = "-1"
        return S

    S += str(ch)
    ch = chr(ord(ch) + 1)

    # Check one by one all element of
    # given prefix array
    for i in range(1, N):
        diff = A[i] - A[i - 1]

        # If the difference between any two
        # consecutive elements of the prefix
        # array is greater than 1 then there
        # will be no such string possible that
        # satisfies the given array.
        # Also, string cannot have more than
        # 26 distinct characters
        if (diff > 1 or diff < 0 or A[i] > 26):
            S = "-1"
            return S

        # If difference is 0 then the
        # (i + 1)th character will be
        # same as the ith character
        elif (diff == 0):
            S += 'a'

        # If difference is 1 then the
        # (i + 1)th character will be
        # different from the ith character
        else:
            S += ch
            ch = chr(ord(ch) + 1)

    # Return the resultant string
    return S

# Driver code
arr = [1, 1, 2, 3, 3]
n = len(arr)
print(smallestString(n, arr))

# This code is contributed
# by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the required string
static string smallestString(int N, int []A)
{
    // First character will always be 'a'
    char ch = 'a';

    // To store the resultant string
    string S = "";

    // Since length of the string should be
    // greater than 0 and first element
    // of array should be 1
    if (N < 1 || A[0] != 1)
    {
        S = "-1";
        return S;
    }

    S += ch;
    ch++;

    // Check one by one all element of given prefix array
    for (int i = 1; i < N; i++)
    {
        int diff = A[i] - A[i - 1];

        // If the difference between any two
        // consecutive elements of the prefix array
        // is greater than 1 then there will be no such
        // string possible that satisfies the given array
        // Also, string cannot have more than
        // 26 distinct characters
        if (diff > 1 || diff < 0 || A[i] > 26)
        {
            S = "-1";
            return S;
        }

        // If difference is 0 then the (i + 1)th character
        // will be same as the ith character
        else if (diff == 0)
            S += 'a';

        // If difference is 1 then the (i + 1)th character
        // will be different from the ith character
        else
        {
            S += ch;
            ch++;
        }
    }

    // Return the resultant string
    return S;
}

// Driver code
static void Main()
{
    int []arr = { 1, 1, 2, 3, 3 };
    int n = arr.Length;
    Console.WriteLine(smallestString(n, arr));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?PHP
// PHP implementation of the above approach
// Function to return the required string
function smallestString($N, $A)
{
    // First character will always be 'a'
    $ch = 'a';

    // To store the resultant string
    $S = "";

    // Since length of the string should be
    // greater than 0 and first element
    // of array should be 1
    if ($N < 1 || $A[0] != 1)
    {
        $S = "-1";
        return $S;
    }

    $S .= $ch;
    $ch++;

    // Check one by one all element of given prefix array
    for ($i = 1; $i < $N; $i++)
    {
        $diff = $A[$i] - $A[$i - 1];

        // If the difference between any two
        // consecutive elements of the prefix array
        // is greater than 1 then there will be no such
        // string possible that satisfies the given array
        // Also, string cannot have more than
        // 26 distinct characters
        if ($diff > 1 || $diff < 0 || $A[$i] > 26)
        {
            $S = "-1";
            return $S;
        }

        // If difference is 0 then the (i + 1)th character
        // will be same as the ith character
        else if ($diff == 0)
            $S .= 'a';

        // If difference is 1 then the (i + 1)th character
        // will be different from the ith character
        else
        {
            $S .= $ch;
            $ch++;
        }
    }

    // Return the resultant string
    return $S;
}

// Driver code
$arr = array( 1, 1, 2, 3, 3 );
$n = sizeof($arr);
echo(smallestString($n, $arr));

// This code is contributed by Code_Mech
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the required string
function smallestString(N, A)
{

    // First character will always be 'a'
    let ch = 'a';

    // To store the resultant string
    let S = "";

    // Since length of the string should be
    // greater than 0 and first element
    // of array should be 1
    if (N < 1 || A[0] != 1)
    {
        S = "-1";
        return S;
    }

    S += ch;
    ch = String.fromCharCode(ch.charCodeAt(0) + 1);

    // Check one by one all element of
    // given prefix array
    for(let i = 1; i < N; i++)
    {
        let diff = A[i] - A[i - 1];

        // If the difference between any two
        // consecutive elements of the prefix
        // array is greater than 1 then there
        // will be no such string possible that
        // satisfies the given array. Also,
        // string cannot have more than
        // 26 distinct characters
        if (diff > 1 || diff < 0 || A[i] > 26)
        {
            S = "-1";
            return S;
        }

        // If difference is 0 then the (i + 1)th
        // character will be same as the ith character
        else if (diff == 0)
            S += 'a';

        // If difference is 1 then the (i + 1)th
        // character will be different from the
        // ith character
        else
        {
            S += ch;
            ch = String.fromCharCode(
                ch.charCodeAt(0) + 1);
        }
    }

    // Return the resultant string
    return S;
}

// Driver code
let arr = [ 1, 1, 2, 3, 3 ];
let n = arr.length;

document.write(smallestString(n, arr));

// This code is contributed by souravmahato348

</script>
```

**Output:** 

```
aabca
```