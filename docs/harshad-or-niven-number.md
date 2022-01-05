# 哈沙德(或尼文)号

> 原文:[https://www.geeksforgeeks.org/harshad-or-niven-number/](https://www.geeksforgeeks.org/harshad-or-niven-number/)

基数为 10 的整数，可被其位数的和整除，称为哈沙德数。一个 *n-harshad* 数是一个整数，可被其基数 *n* 中的数字之和整除。
下面是以 10 为基数表示的前几个哈沙德数字:
1、2、3、4、5、6、7、8、9、10、12、18、20……
给定一个以 10 为基数的数字，我们的任务是检查它是否是哈沙德数字。

**示例:**

```
Input: 3
Output: 3 is a Harshad Number

Input: 18
Output: 18 is a Harshad Number

Input: 15
Output: 15 is not a Harshad Number
```

1.使用%运算符提取数字中的所有数字，并计算总和。
2。检查这个数是否能被和整除。

下面是上述想法的实现:

## C++

```
// C++ program to check if a number is Harshad
// Number or not.
#include <bits/stdc++.h>
using namespace std;

// function to check Harshad Number
bool checkHarshad(int n)
{
    // calculate sum of digits
    int sum = 0;
    for (int temp = n; temp > 0; temp /= 10)
        sum += temp % 10;

    // Return true if sum of digits is multiple
    // of n
    return (n % sum == 0);
}

// driver program to check above function
int main()
{
    checkHarshad(12) ? cout << "Yes\n" : cout << "No\n";
    checkHarshad(15) ? cout << "Yes\n" : cout << "No\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a number is Harshad
// Number or not

public class GFG {
    // method to check Harshad Number
    static boolean checkHarshad(int n)
    {
        // calculate sum of digits
        int sum = 0;
        for (int temp = n; temp > 0; temp /= 10)
            sum += temp % 10;

        // Return true if sum of digits is multiple
        // of n
        return (n % sum == 0);
    }

    // Driver program to test above functions
    public static void main(String[] args)
    {
        System.out.println(checkHarshad(12) ? "Yes" : "No");
        System.out.println(checkHarshad(15) ? "Yes" : "No");
    }
}
```

## 计算机编程语言

```
# Python program to check
# if a number is Harshad
# Number or not.

def checkHarshad( n ) :
    sum = 0
    temp = n
    while temp > 0 :
        sum = sum + temp % 10
        temp = temp // 10
    # Return true if sum of
    # digits is multiple of n
    return n % sum == 0

# Driver Code
if(checkHarshad(12)) : print("Yes")
else : print ("No")

if (checkHarshad(15)) : print("Yes")
else : print ("No")

# This code is contributed
# by Nikita Tiwari
```

## C#

```
// C# program to check if a number is Harshad
// Number or not
using System;

public class GFG {

    // method to check Harshad Number
    static bool checkHarshad(int n)
    {

        // calculate sum of digits
        int sum = 0;
        for (int temp = n; temp > 0; temp /= 10)
            sum += temp % 10;

        // Return true if sum of digits is
        // multiple of n
        return (n % sum == 0);
    }

    // Driver program to test above functions
    public static void Main()
    {
        Console.WriteLine(checkHarshad(12) ? "Yes" : "No");

        Console.WriteLine(checkHarshad(15) ? "Yes" : "No");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php program to check if
// a number is Harshad
// Number or not.

// function to check
// Harshad Number
function checkHarshad($n)
{
    // calculate sum of digits
    $sum = 0;
    for ($temp = $n; $temp > 0;
                     $temp /= 10)
        $sum += $temp % 10;

    // Return true if sum of
    // digits is multiple of n
    return ($n % $sum == 0);
}

// Driver Code
$k = checkHarshad(12) ? "Yes\n" : "No\n";
     echo($k);
$k = checkHarshad(15) ? "Yes\n" : "No\n";
     echo($k);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
    // Javascript program to check if a number is Harshad Number or not

    // method to check Harshad Number
    function checkHarshad(n)
    {

        // calculate sum of digits
        let sum = 0;
        for (let temp = n; temp > 0; temp = parseInt(temp / 10, 10))
            sum += temp % 10;

        // Return true if sum of digits is
        // multiple of n
        return (n % sum == 0);
    }

    document.write(checkHarshad(12) ? "Yes" + "</br>" : "No" + "</br>");

      document.write(checkHarshad(15) ? "Yes" + "</br>" : "No" + "</br>");

</script>
```

**输出:**

```
Yes
No
```

**方法 2:使用字符串:**

*   我们必须通过取一个新的变量把给定的数字转换成字符串。
*   遍历字符串，将每个元素转换为整数，并将其相加。
*   如果这个数可以被和整除，那么它就是 Harshad 数。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include<bits/stdc++.h>
using namespace std;

string checkHarshad(int n)
{

    // Converting integer to string
    string st = to_string(n);

    // Initialising sum to 0
    int sum = 0;
    int length = st.length();

    // Traversing through the string
    for(char i : st)
    {

        // Converting character to int
        sum = sum + (i - '0');
    }

    // Comparing number and sum
    if (n % sum == 0)
    {
        return "Yes";
    }
    else
    {
        return "No";
    }
}

// Driver Code
int main()
{
    int number = 18;

    // Passing this number to get result function
    cout << checkHarshad(number) << endl;
}

// This code is contributed by rrrtnx
```

## 蟒蛇 3

```
# Python implementation of above approach
def checkHarshad(n):

    # Converting integer to string
    st = str(n)

    # Initialising sum to 0
    sum = 0
    length = len(st)

    # Traversing through the string
    for i in st:

        # Converting character to int
        sum = sum + int(i)

    # Comparing number and sum
    if (n % sum == 0):
        return "Yes"
    else:
        return "No"

# Driver Code
number = 18
# passing this number to get result function
print(checkHarshad(number))

# This code is contributed by vikkycirus
```

## java 描述语言

```
<script>
// Javascript implementation of above approach
function checkHarshad(n){

    // Converting integer to string
    let st = String(n)

    // Initialising sum to 0
    let sum = 0
    let length = st.length

    // Traversing through the string
    for(i in st){
        // Converting character to int
        sum = sum + parseInt(i)
    }

    // Comparing number and sum
    if (n % sum == 0){
        return "Yes"
    }
    else{
        return "No"
    }
}

// Driver Code
let number = 18
// passing this number to get result function
document.write(checkHarshad(number))

// This code is contributed by _saurabh_jaiswal
</script>
```

**输出:**

```
Yes
```

**时间复杂度:** O(n)

**参考文献:**
[【https://en.wikipedia.org/wiki/Harshad_number】](https://en.wikipedia.org/wiki/Harshad_number)
本文由 [**Harsh Agarwal**](https://www.facebook.com/harsh.agarwal.16752) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。