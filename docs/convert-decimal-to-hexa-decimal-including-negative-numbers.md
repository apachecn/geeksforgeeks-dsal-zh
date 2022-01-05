# 将十进制转换为包含负数的六进制

> 原文:[https://www . geesforgeks . org/convert-decimal-to-hexal-decimal-包括负数/](https://www.geeksforgeeks.org/convert-decimal-to-hexa-decimal-including-negative-numbers/)

给定十进制格式的数字 N，任务是将其转换为字符串形式的 N 的十六进制表示。负数以 2 的补码形式存储。
**例:**

> **输入:** N = 134
> **输出:** 86
> **解释:**
> 134 = 0000000000000000000001000000000000000000000000000000000000000000000000000000000000000 分组为四个大小的块，并将每个块转换为等效的十六进制数，得到 88。同样，我们可以看到 8*16 + 6 = 134。我们也将通过在其他[帖子](https://www.geeksforgeeks.org/program-decimal-hexadecimal-conversion/)中讨论的余数技巧得到相同的结果。
> **输入:** N = -1
> **输出:** ffffffff

**方法:**
ides 是以更大的大小存储负数，以欺骗编译器将其读取为正数而不是负数，然后使用正常的余数技术。将 num 存储在 u_int 中，u_it 的大小更大，因为 MSB 为 0，所以它将是正的。
以下是上述办法的实施:

## C++

```
// C++ program to convert decimal
// to hexadecimal covering negative numbers

#include <bits/stdc++.h>
using namespace std;

// Function to convert decimal no.
// to hexadecimal number
string Hex(int num)
{
    // map for decimal to hexa, 0-9 are
    // straightforward, alphabets a-f used
    // for 10 to 15.
    map<int, char> m;

    char digit = '0';
    char c = 'a';

    for (int i = 0; i <= 15; i++) {
        if (i < 10) {
            m[i] = digit++;
        }
        else {
            m[i] = c++;
        }
    }

    // string to be returned
    string res = "";

    // check if num is 0 and directly return "0"
    if (!num) {
        return "0";
    }
    // if num>0, use normal technique as
    // discussed in other post
    if (num > 0) {
        while (num) {
            res = m[num % 16] + res;
            num /= 16;
        }
    }
    // if num<0, we need to use the elaborated
    // trick above, lets see this
    else {
        // store num in a u_int, size of u_it is greater,
        // it will be positive since msb is 0
        u_int n = num;

        // use the same remainder technique.
        while (n) {
            res = m[n % 16] + res;
            n /= 16;
        }
    }

    return res;
}

// Driver Code
int main()
{
    int x = 134, y = -1, z = -234;

    cout << "Hexa representation for" << endl;
    cout << x << " is " << Hex(x) << endl;
    cout << y << " is " << Hex(y) << endl;
    cout << z << " is " << Hex(z) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert decimal
// to hexadecimal covering negative numbers
import java.util.*;
import java.util.HashMap;
import java.util.Map;

class GFG
{

// Function to convert decimal no.
// to hexadecimal number
static String Hex(int num)
{
    // map for decimal to hexa, 0-9 are
    // straightforward, alphabets a-f used
    // for 10 to 15.

    HashMap<Integer, Character> m = new HashMap<Integer, Character>();

    char digit = '0';
    char c = 'a';

    for (int i = 0; i <= 15; i++) {
        if (i < 10) {
            m.put(i, digit);
            digit++;
        }
        else {
            m.put(i, c);
            c++;
        }
    }

    // string to be returned
    String res = "";

    // check if num is 0 and directly return "0"
    if (num == 0) {
        return "0";
    }
    // if num>0, use normal technique as
    // discussed in other post
    if (num > 0) {
        while (num != 0) {
            res = m.get(num % 16) + res;
            num /= 16;
        }
    }
    // if num<0, we need to use the elaborated
    // trick above, lets see this
    else {
        // store num in a u_int, size of u_it is greater,
        // it will be positive since msb is 0
        int n = num;

        // use the same remainder technique.
        while (n != 0) {
            res = m.get(n % 16) + res;
            n /= 16;
        }
    }

    return res;
}

// Driver Code
public static void main(String []args)
{
    int x = 134, y = -1, z = -234;

    System.out.println("Hexa representation for" );
    System.out.println(x +" is " + Hex(x));
    System.out.println( y +" is " + Hex(y));
    System.out.println( z + " is " + Hex(z));   
}
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 program to convert decimal
# to hexadecimal covering negative numbers

# Function to convert decimal no.
# to hexadecimal number
def Hex(num) :

    # map for decimal to hexa, 0-9 are
    # straightforward, alphabets a-f used
    # for 10 to 15.
    m = dict.fromkeys(range(16), 0);

    digit = ord('0');
    c = ord('a');

    for i in range(16) :
        if (i < 10) :
            m[i] = chr(digit);
            digit += 1;

        else :
            m[i] = chr(c);
            c += 1

    # string to be returned
    res = "";

    # check if num is 0 and directly return "0"
    if (not num) :
        return "0";

    # if num>0, use normal technique as
    # discussed in other post
    if (num > 0) :
        while (num) :
            res = m[num % 16] + res;
            num //= 16;

    # if num<0, we need to use the elaborated
    # trick above, lets see this
    else :

        # store num in a u_int, size of u_it is greater,
        # it will be positive since msb is 0
        n = num + 2**32;

        # use the same remainder technique.
        while (n) :
            res = m[n % 16] + res;
            n //= 16;

    return res;

# Driver Code
if __name__ == "__main__" :

    x = 134; y = -1; z = -234;

    print("Hexa representation for");
    print(x, "is", Hex(x));
    print(y, "is", Hex(y));
    print(z, "is", Hex(z));

# This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// JavaScript program to convert decimal
// to hexadecimal covering negative numbers

// Function to convert decimal no.
// to hexadecimal number
function Hex(num)
{
    // map for decimal to hexa, 0-9 are
    // straightforward, alphabets a-f used
    // for 10 to 15.

    let m = new Map();

    let digit = '0'.charCodeAt(0);
    let c = 'a'.charCodeAt(0);

    for (let i = 0; i <= 15; i++) {
        if (i < 10) {
            m.set(i, String.fromCharCode(digit));
            digit++;
        }
        else {
            m.set(i, String.fromCharCode(c));
            c++;
        }
    }

    // string to be returned
    let res = "";

    // check if num is 0 and directly return "0"
    if (num == 0) {
        return "0";
    }
    // if num>0, use normal technique as
    // discussed in other post
    if (num > 0) {
        while (num != 0) {
            res = m.get(num % 16) + res;
            num =Math.floor(num/ 16);
        }
    }
    // if num<0, we need to use the elaborated
    // trick above, lets see this
    else {
        // store num in a u_int, size of u_it is greater,
        // it will be positive since msb is 0
        let n = num+Math.pow(2,32);

        // use the same remainder technique.
        while (n != 0) {
            res = m.get(n % 16) + res;
            n = Math.floor(n/16);
        }
    }

    return res;
}

// Driver Code
let x = 134, y = -1, z = -234;
document.write("Hexa representation for<br>" );
document.write(x +" is " + Hex(x)+"<br>");
document.write( y +" is " + Hex(y)+"<br>");
document.write( z + " is " + Hex(z)+"<br>");

// This code is contributed by rag2127

</script>
```

**Output:** 

```
Hexa representation for
134 is 86
-1 is ffffffff
-234 is ffffff16
```