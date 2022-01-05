# 使用给定的随机-0-1-生成器

实现随机-0-6-生成器

> 原文:[https://www . geesforgeks . org/implement-random-0-6-generator-使用给定的-random-0-1-generator/](https://www.geeksforgeeks.org/implement-random-0-6-generator-using-the-given-random-0-1-generator/)

给定一个随机给出 0 或 1 的函数 random01Generator()，实现一个利用该函数的函数，并生成 0 到 6(包括 0 和 6)之间的数字。所有的数字都应该有相同的出现概率。

示例:

```
on multiple runs, it gives 
3
2
3
6
0

```

**逼近:**这里的思路是找到大于给定范围的最小数的范围。这里，因为范围是 6，所以确定 2^3 是大于 6 的最小数字。因此，这里的 k 将是 3。

因此，尝试每次形成一个由 3 个字符组成的二进制数，一旦获得所有 3 个字符，查找该二进制数的相应十进制表示并返回该值。

例如，如果它在第一次随机 01 调用中给出 0，然后在下一次调用中给出 1，最后在下一次调用中再次给出 1，则可以说这样形成的二进制数是 011，它是数字 3 的十进制表示，因此返回 3。万一它给出 111，也就是超出范围的 7。所以，只要丢弃这个数字，并再次重复整个过程，直到它给出所需范围内的数字。

在调用 random01Generator() 6 次时，数字出现的概率不会相同。例如，第一次，0 出现的概率是 1/2。现在，第二次，概率是 1/2，总概率是 1/4。如果通过调用随机函数 6 次来重复这个过程 6 次，这将使 0 出现的概率为 1/(2^6).类似地，遵循二项式分布模式，1 的出现概率将大于 0，2 的出现概率将大于 1，以此类推。

这样做将确保所有的概率都是相等的，因为它只考虑可以生成这些数字的范围，并拒绝任何给我们的结果大于最大指定范围的情况。因此，上述方法。

显然，这个想法可以扩展，如果有一些其他的随机生成器，比如说 random0mGenerator()并且需要生成 0 到 n 之间的数字，其中 n>m。在这种情况下，修改下面的函数以合并 m 和 n。

**先决条件:**Java 中的 [BigInteger。](https://www.geeksforgeeks.org/biginteger-class-in-java/)

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to generate random numbers
import java.math.BigInteger;
import java.util.Random;

public class RandomImp{

    public int random01Generator() {

        Random rand = new Random();
        return rand.nextInt(2); 
    }

    // function will use the above
    // method and return numbers 
    // between 0 and 6 inclusive.
    public void random06Generator(){

        Random rand = new Random();
        int val = 7;
        while (val >= 7) {

            String res = "";
            for (int i = 0; i < 3; i++) 
                res += 
                 String.valueOf(random01Generator());            

            BigInteger bg = new BigInteger(res,2);

            val = bg.intValue();
        }

        System.out.println(val);
    }

    // Driver Code
    public static void main(String[] args){
        RandomImp r = new RandomImp();
        r.random06Generator();
    }
}
```

Output :

```
3
2
4
1

```

这个问题的灵感来自于这个 [stackoverflow 链接](https://stackoverflow.com/questions/13209162/creating-a-random-number-generator-from-a-coin-toss)