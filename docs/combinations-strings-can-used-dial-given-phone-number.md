# 可用于拨打号码的所有字符串组合

> 原文:[https://www . geesforgeks . org/combinations-strings-can-use-dial-给定电话号码/](https://www.geeksforgeeks.org/combinations-strings-can-used-dial-given-phone-number/)

给定一个号码，打印所有可能的字符串组合，这些字符串可用于拨打具有以下规格的电话中的给定号码。

在给定的电话中，我们可以拨打，
2 使用 A 或 B 或 C，
3 使用 D 或 E 或 F，
………………。
8 使用 T 或 U 或 V，
9 使用 W 或 X 或 Y 或 Z，
1 仅使用 1
0 使用 0。

例如，如果 23 是给定的电话号码，程序应该打印 AD、AE、AF、BD、BE、BF、CD、CE、CF

其思想是在哈希映射中存储数字到字符的映射。该地图存储了可用于拨打数字的所有字符。我们为当前数字放置每个可能的字符，并为剩余的数字重复出现。下面是这个想法的 Java 实现。

```
// Java program to print all possible key strings
// that can be used to dial a phone number.
import java.util.HashMap;

class ConvertToString
{
    // A Recursive function to print all combinations
    // that can be used to dial a given number.
    // phNo ==> Given Phone Number
    // i    ==> Current digit of phNo to be processed
    // hm   ==> Stores characters that can be used to
    //          to dial a digit.
    // str  ==> Current output string
    static void printStrings(String phNo, int i,
                    HashMap<Character, String> hm,
                    StringBuilder str)
    {
        // If all digits are processed, print output
        // string
        if (i == phNo.length())
        {
            System.out.print(str + " ");
            return;
        }

        // Get current digit of phNo, and recur for all
        // characters that can be used to dial it.
        String s = hm.get(phNo.charAt(i));
        for (int j = 0; j < s.length(); j++)
        {
            str.append(s.charAt(j));
            printStrings(phNo, i+1, hm, str);
            str.deleteCharAt(str.length()-1);
        }
    }

    // Prints all possible combinations of strings that
    // can be used to dial c[].
    static void printStringForNumber(String phNo)
    {
        // Create a HashMap
        HashMap<Character, String> hm =
                    new HashMap<Character, String>();

        // For every digit, store characters that can
        // be used to dial it.
        hm.put('2', "ABC");
        hm.put('3', "DEF");
        hm.put('4', "GHI");
        hm.put('5', "JKL");
        hm.put('6', "MNO");
        hm.put('7', "PQRS");
        hm.put('8', "TUV");
        hm.put('9', "WXYZ");
        hm.put('1', "1");
        hm.put('0', "0");

        // Create a string to store a particular output
        // string
        StringBuilder str = new StringBuilder();

        // Call recursive function
        printStrings(phNo, 0, hm, str);
    }

    // Driver code to test above methods
    public static void main(String args[])
    {
        // Prints
        printStringForNumber("23");
    }
}
```

输出:

```
AD AE AF BD BE BF CD CE CF 
```

本文由 **Phalgun** 供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论