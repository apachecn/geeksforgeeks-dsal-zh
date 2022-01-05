# 电话记忆 Java 程序

> 原文:[https://www . geesforgeks . org/Java-电话程序助记符/](https://www.geeksforgeeks.org/java-program-for-phone-mnemonics/)

![](img/3f6170241de260d8c542246c846f2060.png)

在日常生活中，我们必须记住很多电话号码。大多数人觉得很难记住这么大的 10 位数电话号码。一个简单解决方案是将电话号码与一些已知的单词联系起来。
例如，我们可以根据拨号键盘中的字符将电话号码 32627287 与大马士革联系起来。(我们可以用表盘上对应的**字符**中的任意一个来替换**数字**。例如，我们的拨号盘在 2 下面提到了 ABC。所以我们可以用 A 或者 B 或者 c 来表示 **2，同样我们可以用 D 或者 E 或者 F** 来代替 3。

写一个程序，输入一个电话号码，打印出我们字典中所有可能的单词。

让我们考虑样本输入 23。
这里，
2 可以用 A 或 B 或 c 代替，
3 可以用 D 或 E 或 f 代替。
所以一个有效的组合是 AD，对应 623。
另一个可以是光盘等等。
我们正在生成所有可能的排列，从{A 或 B 或 C}开始，然后是{D 或 E 或 F}。然而，只有那些在我们字典里的排列才会被打印出来。这些选定的单词将代表我们的样本输出。

但是，像 1 和 0 这样的数字将被空字符串替换，因为它们不代表拨号键盘上的任何字符，即 1 和 0 将代表" "。

示例:

```
Input : 23
Output : [BE]

Input : 623
Output : [MAD, OCD]

Input : 726
Output : [PAN, PCM, PCO, RAM, SAM]

Input : 2
Output : [A, B, C]

Input : 123
Output : [BE]

```

。
**【幼稚方法】**
这个程序使用回溯生成所有可能的单词。点击[这里](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)了解更多。回溯的概念已经在那里解释过了。

```
import java.util.*;

public class PhoneMnemonics {
    static ArrayList<String> dictionary = new ArrayList<String>();

    /* List all the phone mnemonics for the given digit sequence.
     * @param input a digit sequence, like "23432" */
    public static ArrayList<String> listMnemonics(String input)
    {
        ArrayList<String> list = new ArrayList<String>();
        String[] dic = { "A", "B", "C", "D", "E", "F", "G", 
                        "H", "I", "J", "K", "L", "M", "N",
                        "O", "P", "Q", "R", "S", "T", "U", 
                         "V", "W", "X", "Y", "Z", "MAD",
                         "OCD", "PAN", "PCM", "PCO", "RAM", "SAM", "BE" };
        for (String i : dic)
            dictionary.add(i);
        listMnemonics("", input, list);
        return list;
    }

    /* Helper recursive method to list phone mnemonics. This works by finding
     * all possibilities for the first digit, then recursing on the rest of the
     * string. For example, if prefix is "AB" and remaining is "2", then the
     * mnemonics "ABA", "ABB", and "ABC" would be printed.
     * 
     * @param prefix : the part of the mnemonic that has already been built
     * @param remaining :  the remaining digits to include in the mnemonic  */
    private static void listMnemonics(String prefix, String remaining, 
                                                ArrayList<String> list)
    {
        // Base case: when there are no more characters to process,
        // just print out the mnemonic that we've already built.
        if (remaining.isEmpty()) {
            if (!list.contains(prefix) && dictionary.contains(prefix))
                list.add(prefix);
            return;
        }

        // Recursive case.
        if (remaining.charAt(0) == '1' || remaining.charAt(0) == '0') {
            listMnemonics(prefix, remaining.substring(1), list);
        }

        String digits = digitLetters(remaining.charAt(0));
        for (int i = 0; i < digits.length(); i++) {
            String newPrefix = prefix + digits.charAt(i);
            String newRemaining = remaining.substring(1);
            listMnemonics(newPrefix, newRemaining, list);
        }
    }

    /**
     * Get the letters appearing on a given key of a standard phone keypad.
     * @param ch the character representation of a digit on the phone keypad
     *            (like '2')
     * @return a string containing the letters on the given key, or the empty
     *         string if the key is not recognized
     */
    private static String digitLetters(char ch)
    {
        switch (ch) {
        case '2':
            return "ABC";
        case '3':
            return "DEF";
        case '4':
            return "GHI";
        case '5':
            return "JKL";
        case '6':
            return "MNO";
        case '7':
            return "PQRS";
        case '8':
            return "TUV";
        case '9':
            return "WXYZ";
        }
        return "";
    }

    public static void main(String[] args)
    {
        String str = "123";
        ArrayList<String> list = listMnemonics(str);
        System.out.println(list);
    }
}
```

**Output:**

```
[BE]

```

注意:一旦我们添加了单词字典以及它们的使用频率，这个程序将变得更加方便用户。使用字典，以下输出可以根据用户使用的频率进行优化，以打印 MAD、OCD 等。查看此链接:[https://phonespell.org/](https://phonespell.org/)。
 **相关文章用 C++实现:** [从电话号码中打印所有可能的单词](https://www.geeksforgeeks.org/find-possible-words-phone-digits/)

 **参考:**
**通过**埃里克·罗伯茨**递归思考**。