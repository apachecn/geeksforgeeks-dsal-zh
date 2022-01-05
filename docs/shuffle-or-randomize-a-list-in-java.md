# 在 Java 中打乱或随机化列表

> 原文:[https://www . geesforgeks . org/shuffle-or-随机化-a-list-in-java/](https://www.geeksforgeeks.org/shuffle-or-randomize-a-list-in-java/)

*   **洗牌列表**
    [collections . shuffle()](https://www.geeksforgeeks.org/collections-shuffle-java-examples/)是 java 中用来洗牌的列表。
    等级体系:

```
java
   ↳ util
      ↳ Collections
```

语法:

```
Collections.shuffle(list);
```

示例:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to demonstrate working of shuffle()
import java.util.*;

public class GFG {
    public static void main(String[] args)
    {
        ArrayList<String> mylist = new ArrayList<String>();
        mylist.add("ide");
        mylist.add("quiz");
        mylist.add("geeksforgeeks");
        mylist.add("quiz");
        mylist.add("practice");
        mylist.add("qa");

        System.out.println("Original List : \n" + mylist);

        Collections.shuffle(mylist);

        System.out.println("\nShuffled List : \n" + mylist);
    }
}
```

**Output:** 

```
Original List : 
[ide, quiz, geeksforgeeks, quiz, practice, qa]

Shuffled List : 
[ide, practice, quiz, qa, geeksforgeeks, quiz]
```

*   **使用用户提供的随机对象**
    对列表进行洗牌语法:

```
Collections.shuffle(list, Random object);
```

示例:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to demonstrate working of shuffle()
// with user provided source of randomness.
import java.util.*;

public class GFG {
    public static void main(String[] args)
    {
        ArrayList<String> mylist = new ArrayList<String>();
        mylist.add("ide");
        mylist.add("quiz");
        mylist.add("geeksforgeeks");
        mylist.add("quiz");
        mylist.add("practice");
        mylist.add("qa");

        System.out.println("Original List : \n" + mylist);

        // Here we use Random() to shuffle given list.
        Collections.shuffle(mylist, new Random());
        System.out.println("\nShuffled List with Random() : \n"
                           + mylist);

        // Here we use Random(3) to shuffle given list. Here 3
        // is seed value for Random.
        Collections.shuffle(mylist, new Random(3));
        System.out.println("\nShuffled List with Random(3) : \n"
                           + mylist);

        // Here we use Random(5) to shuffle given list.  Here 5
        // is seed value for Random.
        Collections.shuffle(mylist, new Random(5));
        System.out.println("\nShuffled List with Random(5) : \n"
                           + mylist);
    }
}
```

**Output:** 

```
Original List : 
[ide, quiz, geeksforgeeks, quiz, practice, qa]

Shuffled List with Random() : 
[geeksforgeeks, practice, qa, ide, quiz, quiz]

Shuffled List with Random(3) : 
[quiz, ide, practice, quiz, geeksforgeeks, qa]

Shuffled List with Random(5) : 
[ide, quiz, geeksforgeeks, quiz, practice, qa]
```

*   **如何编写自己的 Shuffle 方法？**
    我们可以使用[费希尔-耶茨洗牌算法](https://www.geeksforgeeks.org/shuffle-a-given-array/)，该算法在 0(n)时间内有效。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to shuffle a given array
import java.util.Random;
import java.util.Arrays;
public class ShuffleRand
{
    // A Function to generate a random permutation of arr[]
    static void randomize( int arr[], int n)
    {
        // Creating a object for Random class
        Random r = new Random();

        // Start from the last element and swap one by one. We don't
        // need to run for the first element that's why i > 0
        for (int i = n-1; i > 0; i--) {

            // Pick a random index from 0 to i
            int j = r.nextInt(i);

            // Swap arr[i] with the element at random index
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }

        // Prints the random array
        System.out.println(Arrays.toString(arr));
    }

    // Driver Program to test above function
    public static void main(String[] args)
    {        
         int[] arr = {1, 2, 3, 4, 5, 6, 7, 8};
         int n = arr.length;
         randomize (arr, n);
    }
}
```

**Output:** 

```
[5, 7, 1, 3, 6, 8, 4, 2]
```