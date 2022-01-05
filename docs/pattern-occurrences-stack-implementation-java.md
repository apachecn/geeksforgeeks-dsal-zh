# 模式出现:堆栈实现 Java

> 原文:[https://www . geesforgeks . org/pattern-occurs-stack-implementation-Java/](https://www.geeksforgeeks.org/pattern-occurrences-stack-implementation-java/)

假设我们有两个字符串:-模式和文本
**模式:**由独特的字符组成
**文本:**由任意长度组成

我们需要从**文本**中找到**模式**的数量，去掉文本中模式的每一个出现。

**<u>例</u>** :

```
Input : 
Pattern : ABC
Text : ABABCABCC
Output :
3
Occurrences found at: 
4 7 8
Explanation
Occurrences and their removal in the order
1\. AB<u>ABC</u>ABCC
2\. AB<u>ABC</u>C
3\. <u>ABC</u>

```

想法是使用堆栈数据结构。
1。初始化一个**指针**开始匹配模式中出现的 0 和**计数器**到 0。
2。检查模式和文本在当前索引中是否具有相同的字符。
3。如果指针指向模式的末尾，这意味着所有先前的字符都已按照**递增的顺序**找到，则将**计数器**递增 1。
4。如果不是，如果字符相同，继续将**指针**增加 1。
5。如果两个字符串中的字符不同，请检查字符是否与模式的第一个字符相同(即指针= 0)。
6。如果是，将当前指针中的剩余字符添加到堆栈的模式长度中，并检查它们是否存在，以便从堆栈中形成模式。另外，现在将指针初始化为 1，因为我们已经检查过指针= 0(在**步骤 5** 中)。
7。如果匹配，清空堆栈至**空**。否则，删除第一个字符，并继续添加子字符串的剩余部分，以检查后续步骤。
8。如果任何添加到堆栈中的字符串与模式相匹配**将计数器增加 1** ，并将**指针初始化 0** 。
9。对文本长度的所有索引重复所有这些步骤**。
10。打印计数器和事件。
11。堆栈的基本任务是**处理可能发生的未决操作**。**

**<u>根据以上算法</u>** 示例说明:

```
TEXT: ABABCABCC
PATTERN: ABC
pointer = 0
counter = 0
A B A B C A B C C
0 1 2 3 4 5 6 7 8

at index = 0
pointer = 0
stack = []

at index = 1
pointer = 1
stack = []

at index = 2
pointer = 0
stack = ['C']

at index = 3
pointer = 1
stack = ['C']

at index = 4
pointer = 2
counter += 1
pointer = 0 
stack = ['C']

same for index 5,6,7 according to above method

at index = 8
pop from Stack
counter += 1
clear Stack 

```

**算法的 Java 代码** :
先决条件:[Java 中的堆栈类](https://www.geeksforgeeks.org/stack-class-in-java/)

```
import java.util.ArrayList;
import java.util.Stack;

class StackImplementation
{
  // custom class for returning multiple values
  class Data
  {
    ArrayList<Integer> present;
    int count;

    public Data(ArrayList<Integer> present, int count)
    {
      this.present = present;
      this.count = count;
    }
  }
  public Data Solution(char pattern[], char text[])
  {
    // stores the indices for all occurrences
    ArrayList<Integer> list = new ArrayList<>();
    Stack<String>  stack = new Stack<>();

    // present index pointer searched for in
    // the entire array of string characters
    int p = 0;

    //count of all the number of occurrences
    int counter = 0 ;

    // any random number less than 0 to mark
    // the previous index where the occurrence
    // was found
    int lastOccurrence = -10;

    // traversing all the indexes of the text
    // searching for possible pattern
    for (int i = 0; i < text.length; i ++)
    {
      // if the present index and the pointer in
      // the pattern is at same character
      if(text[i] == pattern[p])
      {
        // and if that character is the end of
        // the pattern to be found
        if(text[i] == pattern[pattern.length - 1])
        {
          //index at which pattern is found
          list.add(i);

          // incrementing total occurrences by 1
          counter ++;

          // last found index to be initizalized
          // to present index
          lastOccurrence = i;

          // begin the search for the next pointer
          // again from 0th index of the pattern
          p = 0;
        }
        else
        {
          // if present character at pattern and index
          // is same but still not the end of pattern
          p ++;
        }
      }

      // if characters are not same
      else
      {
        // if the present character is same as the 1st
        // character of the pattern
        // here 0 = pointer in the pattern fixed to 0
        if(text[i] == pattern[0])
        {
          // assume a temporary string
          String temp = "";

          // and add all characters to it to the pattern
          // length from the present pointer to the end
          for (int i1 = p; i1 < pattern.length; i1 ++)
            temp += pattern[i1];

          // push the present pattern length into the stack
          // for checking if pattern is same as subsequence
          // of the text
          stack.push(temp);

          //pattern at pointer = 0 already checked so we
          // start from 1 for the next step
          p = 1;
        }
        else
        {
          // if the previous occurrence was just before
          // the present index
          if (lastOccurrence == i - 1)
          {
            // if the stack is empty place the pointer = 0
            if (stack.isEmpty())
              p = 0;
            else
            {
              // pick up the present possible pattern
              String temp = stack.pop();

              // check if it's character has the matching
              // occurrence
              if (temp.charAt(0) == text[i])
              {
                //increment last index by the present index
                // so that net index is checked
                lastOccurrence = i;

                // check if stack character is last character
                // in the pattern
                if (temp.charAt(0) == pattern[pattern.length - 1])
                {
                  // index found
                  list.add(i);

                  // increment occurrences by 1
                  counter ++;
                }
                else
                {
                  // if present index character doesn't
                  // match the last character in the pattern
                  // remove the first character which was same
                  // and check for further occurrences of the
                  // remaining letters in the stack string
                  temp = temp.substring(1, temp.length());

                  // add the remaining string back to stack
                  // for further review
                  stack.push(temp);
                }
              }
              // if first string character in the stack doesn't
              // match the present character in the text
              else
              {
                // if stack is not empty empty it.
                if (!stack.isEmpty())
                  stack.clear();

                // reinitialize the pointer back to 0 for
                // checking pattern from beginning
                p = 0;
              }
            }
          }
          else
          {
            // empty the stack under any other circumstances
            if (!stack.isEmpty())
              stack.clear();

            // reinitialize the pointer back to 0 for
            // checking pattern from beginning
            p = 0;
          }
        }
      }
    }
    // return the result
    return new Data(list, counter);
  }

  public static void main(String args[])
  {
    // the simple pattern to be matched
    char[] pattern = "ABC".toCharArray();

    // the input string in which the number of
    // occurrences can be found out after removing
    // each occurrence.
    char[] text = "ABABCABCC".toCharArray();

    StackImplementation obj = new StackImplementation();
    Data data = obj.Solution(pattern, text);

    int count = data.count;
    ArrayList<Integer> list = data.present;
    System.out.println(count);
    if (count > 0)
    {
      System.out.println("Occurrences found at:");
      for (int i : list)
        System.out.print(i + " ");
    }
  }
}
```

输出:

```
3
Occurrences found at:
4 7 8

```

**参考文献** :
1。[堆叠 Java 文档。](https://docs.oracle.com/javase/7/docs/api/java/util/Stack.html)
2。[Java 中的自定义数组列表和类。](https://www.geeksforgeeks.org/custom-arraylist-java/)
3。[更多堆栈操作。](https://www.geeksforgeeks.org/data-structures/#Stack)

本文由 **Shubham Saxena** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。