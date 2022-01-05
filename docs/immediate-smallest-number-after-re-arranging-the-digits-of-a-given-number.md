# 重新排列给定数字的数字后立即最小的数字

> 原文:[https://www . geeksforgeeks . org/给定号码重新排列位数后立即最小号码/](https://www.geeksforgeeks.org/immediate-smallest-number-after-re-arranging-the-digits-of-a-given-number/)

给定一个数字，打印由给定数字的数字重新排列形成的最小数字。
如果不可能得到最小的数字，则打印“不可能”。
**例:**

> 输入:n = 1234
> 输出:不可能
> 输入:n = 3544
> 输出:3454
> 输入:n = 2536
> 输出:2365

**来源** : [D-e-Shaw 面试心得](https://www.geeksforgeeks.org/d-e-shaw-interview-experience/)
这个问题是[这篇](https://www.geeksforgeeks.org/smallest-number-rearranging-digits-given-number/)文章的一个变体。在这篇文章中，我们必须找到立即最小的数字，所以想法是遍历从最后一个数字，如果我们发现第(i-1)个数字大于第(I)个数字，然后存储这个索引。然后找到(index-1)第一个数字右边比数字[index-1]小的最大数字，并交换它们。之后，按降序对第(index-1)位之后的数字进行排序。
以下是上述方法的实施:

## C++

```
// C++ program for immediate smallest number
// after re-arranging the digits of a given number

#include <bits/stdc++.h>
using namespace std;

// Utility function to swap two digits
void swap(char* a, char* b)
{
    char temp = *a;
    *a = *b;
    *b = temp;
}

void immediateSmallest(char digits[], int l)
{

    // Find the last digit which is smaller
    // than previous digit
    int index = -1;
    for (int i = l - 1; i > 0; i--) {
        if (digits[i] < digits[i - 1]) {
            index = i;
            break;
        }
    }
    // If no such digit is found, then all digits are in ascending order
    // means there cannot be a smaller number with same set of digits
    if (index == -1) {
        cout << "Not Possible\n";
        return;
    }
    // Find the greatest digit on right side of (index-1)'th digit that is
    // smaller than digits[index-1]
    int x = digits[index - 1];
    int greatest = index;
    for (int i = index + 1; i < l; i += 1) {
        if (digits[i] < x && digits[i] > digits[greatest])
            greatest = i;
    }
    // Swap the above found greatest digit with digits[index-1]
    swap(&digits[greatest], &digits[index - 1]);

    // Sort the digits after (index-1) in descending order
    sort(digits + index, digits + l);
    reverse(digits + index, digits + l);

    cout << "Immediate Smaller No. is " << digits << endl;

    return;
}

int main()
{
    char digits[] = "2536";
    int l = strlen(digits);
    immediateSmallest(digits, l);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for immediate smallest number
// after re-arranging the digits of a given number
import java.util.Arrays;
class GfG {
    // Function to sort a string in descending order
    public static String ReverseSort(String inputString)
    {
        // convert input string to char array
        char tempArray[] = inputString.toCharArray();
        // sort tempArray
        Arrays.sort(tempArray);
        // return new reverse sorted string
        String ans = "";
        for (int i = tempArray.length - 1; i >= 0; i--) {
            ans += tempArray[i];
        }
        return ans;
    }
    static void immediateSmallest(String s)
    {
        int l = s.length();
        char ch[] = s.toCharArray();
        // Find the last digit which is smaller
        // than the previous digit
        int index = -1;
        for (int i = l - 1; i > 0; i--) {
            if (ch[i] < ch[i - 1]) {
                index = i;
                break;
            }
        }
        // If no such digit is found, then all digits are in ascending order
        // means there cannot be a greater number with same set of digits
        if (index == -1) {
            System.out.println("Not Possible");
            return;
        }

        // Find the greatest digit on right side of (index-1)'th digit that is
        // smaller than number[index-1]
        char c = ch[index - 1];
        int x = Character.getNumericValue(c);
        int greatest = index;
        for (int i = index + 1; i < l; i++) {
            char c1 = ch[i];
            char c2 = ch[greatest];
            int current = Character.getNumericValue(c1);
            int max_so_far = Character.getNumericValue(c2);
            if (current < x && current > max_so_far) {
                greatest = i;
            }
        }

        // Swap the above found greatest digit with digits[index-1]
        char temp = 'g';
        temp = ch[index - 1];
        ch[index - 1] = ch[greatest];
        ch[greatest] = temp;

        String new_string = new String(ch);
        String left = new_string.substring(0, index);
        String right = new_string.substring(index, l);

        // Sort the digits after (index-1) in descending order
        String new_right = ReverseSort(right);

        String result = left + new_right;
        System.out.println(result);
        return;
    }

    public static void main(String[] args)
    {
        int n = 2536;
        String s = Integer.toString(n);
        immediateSmallest(s);
    }
}
// This code was contributed by Ankit Chawla
```

## 计算机编程语言

```
# Python program for immediate smallest number
# after re-arranging the digits of a given number

def immediateSmallest(digits, l):
    # Find the last digit which is smaller
    # than previous digit
    index =-1
    for i in range(l-1, 0, -1):
        if digits[i]<digits[i-1]:
            index = i
            break
    # If no such digit is found, then all digits are in ascending order
    # means there cannot be a smaller number with same set of digits
    if(index ==-1):
        print "Not Possible"
        return

    # Find the greatest digit on right side of (index-1)'th digit that is
    # smaller than digits[index-1]
    x = digits[index-1]
    greatest = index

    for i in range(index + 1, l):
        if digits[i]<x and digits[i]>digits[greatest]:
            greatest = i

    # Swap the above found greatest digit with digits[index-1]

    (digits[greatest], digits[index-1])=(digits[index-1], digits[greatest])

    # Sort the digits after (index-1) in descending order

    left = digits[0:index]
    right = digits[index:]
    right = sorted(right)
    ans =""
    for i in range(len(left)):
        ans+= str(left[i])
    for i in range(len(right)-1, -1, -1):
        ans+= str(right[i])
    print ans

digits ="2536"
l = len(digits)
digit_array =[0 for i in range(l)]
for i in range(l):
    digit_array[i]= int(digits[i])

immediateSmallest(digit_array, l)
# This code is contributed by Ankit Chawla
```

## C#

```
// C# program for immediate smallest
// number after re-arranging the
// digits of a given number
class GFG {

    static void immediateSmallest(string s)
    {
        char temp = 'g';

        // Find the last digit which is
        // greater han previous digit
        // and swap it with previous digit
        int l = s.Length;
        char[] ch = s.ToCharArray();
        for (int i = l - 1; i > 0; i--) {
            if (ch[i] < ch[i - 1]) {
                temp = ch[i];
                ch[i] = ch[i - 1];
                ch[i - 1] = temp;
                string s1 = new string(ch);
                System.Console.WriteLine(s1);
                return;
            }
        }

        System.Console.WriteLine("Not Possible");
    }

    // Driver Code
    static void Main()
    {
        int n = 3532;
        string s = System.Convert.ToString(n);
        immediateSmallest(s);
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for immediate smallest
// number after re-arranging the
// digits of a given number

function immediateSmallest($s)
{
    $temp = "g";

    // Find the last digit which is
    // greater han previous digit
    // and swap it with previous digit
    $l = strlen($s);
    for ($i = $l - 1; $i > 0; $i--)
    {
        if ($s[$i] < $s[$i - 1])
        {
            $temp = $s[$i];
            $s[$i] = $s[ $i - 1];
            $s[$i - 1] = $temp;
            print($s);
            return;
        }
    }

    print("Not Possible");
}

// Driver Code
$n = 3532;
$s = strval($n);
immediateSmallest($s);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program for immediate smallest
// number after re-arranging the
// digits of a given number

function immediateSmallest(s,l)
{
var temp ;

        // Find the last digit which is
        // greater han previous digit
        // and swap it with previous digit
       // var l = s.length;
        var ch = new Array(l);
        for(var i=0;i<l;i++)
        {
          ch[i]=s[i];
        }

        for (var i = l - 1; i > 0; i--)
        {
            if (ch[i] < ch[i - 1])
            {
                temp = ch[i];
                ch[i] = ch[i - 1];
                ch[i - 1] = temp;
                s1 = ch.join("");
                document.write(s1);
                return;
            }
        }

        document.write("Not Possible");
    }

var n = "3532";
var s = n.length;
immediateSmallest(n, s);

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
Immediate Smaller No. is 2365
```