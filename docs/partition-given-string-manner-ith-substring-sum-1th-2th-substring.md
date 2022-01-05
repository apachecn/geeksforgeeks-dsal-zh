# 对给定的字符串进行划分，使得第 I 个子串是第(i-1)个和第(i-2)个子串的和

> 原文:[https://www . geesforgeks . org/partition-given-string-mode-ith-substring-sum-1 th-2 th-substring/](https://www.geeksforgeeks.org/partition-given-string-manner-ith-substring-sum-1th-2th-substring/)

以这样的方式划分给定的字符串，即第 I 个子字符串是第(i-1)个和第(i-2)个子字符串的和。

示例:

```
Input : "11235813"
Output : ["1", "1", "2", "3", "5", "8", "13"]

Input : "1111223"
Output : ["1", "11", "12", "23"]

Input : "1111213"
Output : ["11", "1", "12", "13"]

Input : "11121114"
Output : []

```

1.通过每次从一个数字开始选取 3 个数字(第一个、第二个和第三个)来遍历给定的字符串。
2。如果 first + second = third，递归调用 check()，第二个作为第一个，第三个作为第二个。第三个是根据下一个可能的位数挑选的。(两个数相加的结果可以有一个最大值。秒的&三位数+ 1)
3。否则，首先增加第三个(通过增加更多的数字)直到极限(这里的极限是第一个和第二个的总和)。
4。增加三分之一后，出现以下情况。
a)当不匹配时，增加第二个偏移量。
b)当不匹配时，增加第一个偏移量。
c)注意:一旦在增加第三个偏移量后调用 check()，不要更改第二个或第一个偏移量，因为它们已经完成。
5。当到达字符串末尾且条件满足时，在空列表中添加“第二”和“第三”。回滚递归堆栈时，将“第一个”放在列表前面，以便保持顺序。

```
// Java program to check if we can partition a 
// string in a way that value of i-th string is
// sum of (i-1)-th and (i-2)-th substrings.
import java.util.LinkedList;

public class SumArray {

  private static LinkedList<Integer> resultList = 
                                   new LinkedList<>();

  private static boolean check(char[] chars, int offset1, 
       int offset2, int offset3, boolean freezeFirstAndSecond) {

    // Find subarrays according to given offsets
    int first = intOf(subArr(chars, 0, offset1));
    int second = intOf(subArr(chars, offset1, offset2));
    int third = intOf(subArr(chars, offset1 + offset2, offset3));

    // If condition is satisfied for current subarrays
    if (first + second == third) {

      // If whole array is covered.
      if (offset1 + offset2 + offset3 >= chars.length) {
        resultList.add(first);
        resultList.add(second);
        resultList.add(third);
        return true;
      }

      // Check if remaining array also satisfies the condition
      boolean result = check(subArr(chars, offset1, 
           chars.length - offset1), offset2, offset3,
                  Math.max(offset2, offset3), true);
      if (result) {
        resultList.addFirst(first);
      }
      return result;
    }

    // If not satisfied, try incrementing third
    if (isValidOffSet(offset1, offset2, 1 + offset3, chars.length)) {
      if (check(chars, offset1, offset2, 1 + offset3, false)) 
        return true;      
    }

    // If first and second have been finalized, do not 
    // alter already computed results
    if (freezeFirstAndSecond)
      return false;

    // If first and second are not finalized
    if (isValidOffSet(offset1, 1 + offset2, Math.max(offset1, 
                           1 + offset2),  chars.length)) {

      // Try incrementing second
      if (check(chars, offset1, 1 + offset2,
           Math.max(offset1, 1 + offset2), false)) 
        return true;      
    }

    // Try incrementing first
    if (isValidOffSet(1 + offset1, offset2, Math.max(1 + offset1,
                                  offset2),  chars.length)) {
     if (check(chars, 1 + offset1, offset2, Math.max(1 + offset1,
                                             offset2), false)) 
        return true;
    }
    return false;
  }

  // Check if given three offsets are valid (Within array length
  // and third offset can represent sum of first two)
  private static boolean isValidOffSet(int offset1, int offset2, 
                                   int offset3, int length) {
    return (offset1 + offset2 + offset3 <= length &&
            (offset3 == Math.max(offset1, offset2) ||
             offset3 == 1 + Math.max(offset1, offset2)));
  }

  // To get a subarray with starting from given 
  // index and offset
  private static char[] subArr(char[] chars, int index, int offset) {
    int trueOffset = Math.min(chars.length - index, offset);
    char[] destArr = new char[trueOffset];
    System.arraycopy(chars, index, destArr, 0, trueOffset);
    return destArr;
  }

  private static int intOf(char... chars) {
    return Integer.valueOf(new String(chars));
  }

  public static void main(String[] args) {
    String numStr = "11235813";
    char[] chars = numStr.toCharArray();
    System.out.println(check(chars, 1, 1, 1, false));
    System.out.println(resultList);
  }
}
```

**Output:**

```
true
[1, 1, 2, 3, 5, 8, 13]

```