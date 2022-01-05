# 检查一个数字在 Java 中是否为二进制

> 原文:[https://www . geesforgeks . org/check-如果一个数字是二进制的或不是 java 中的/](https://www.geeksforgeeks.org/check-if-a-number-is-binary-or-not-in-java/)

给定一个数字 **N** ，任务是首先检查给定的[数是否为二进制](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)，其值应大于 1。如果 **N** 是二进制表示，打印**真**否则打印**假**。

**示例:**

> **输入:** N = 1010
> **输出:**真
> **说明:**
> 给定数大于 1 且其位数都不大于 1。因此，它是一个大于 1 的二进制数。
> 
> **例:** N = 1234
> **输出:**假
> **说明:**
> 给定数大于 1 但其部分位数{ 2，3，4}大于 1。因此，它不是二进制数。

**迭代方法:**

1.  检查该数字是否小于或等于 1。如果是，则打印 false。
2.  否则，如果数字大于 1，则检查数字的每个数字是 **1 还是 0** 。
3.  如果该数字的任意一位大于 **1** ，则打印**假**，否则打印**真**。

下面是上述方法的实现:

Java 语言(一种计算机语言，尤用于创建网站)

```
 // Java program for the above approach
class GFG {

    // Function to check if number
    // is binary or not
    public static boolean isBinaryNumber(int num)
    {

        // Return false if a number
        // is either 0 or 1 or a
        // negative number
        if (num == 0 || num == 1
            || num < 0) {
            return false;
        }

        // Get the rightmost digit of
        // the number with the help
        // of remainder '%' operator
        // by dividing it with 10
        while (num != 0) {

            // If the digit is greater
            // than 1 return false
            if (num % 10 > 1) {
                return false;
            }
            num = num / 10;
        }
        return true;
    }

    public static void main(String args[])
    {
        // Given Number N
        int N = 1010;

        // Function Call
        System.out.println(isBinaryNumber(N));
    }
} 
```