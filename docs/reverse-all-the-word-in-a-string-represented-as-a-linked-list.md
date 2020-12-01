# 反转表示为链表的字符串中的所有单词

> 原文：[https://www.geeksforgeeks.org/reverse-all-the-word-in-a-string-represented-as-a-linked-list/](https://www.geeksforgeeks.org/reverse-all-the-word-in-a-string-represented-as-a-linked-list/)

给定一个表示句子`S`的链表，使得每个节点代表一个字母，任务是在不反转单个单词的情况下反转该句子。

例如，对于给定的句子`I love Geeks for Geeks`，[链表](http://www.geeksforgeeks.org/data-structures/linked-list/)表示为：

`I -> -> l -> o  -> v -> e -> -> G -> e -> e -> k -> s -> -> f -> o -> r -> -> G -> e -> e -> k -> s`

**示例**：

> **输入**：`I love Geeks for Geeks`
>
> **输出**：`Geeks for Geeks love I`
> 
> **输入**：`practice makes a man perfect`
>
> **输出**：`perfect man a makes practice`

**方法**：想法是从头开始导航链表。 每次遇到空格时，请将空格交换到该单词的开头。 重复此步骤，直到到达最后一个节点。 最后，将第一个单词的最后一个字母设置为指向`null`，它将成为最后一个节点，并不断更改指针。

下面是该方法的实现：

## Java

```java

// Linked List Implementation 
public class Node { 
    public Node(char data, Node next) 
    { 
        Data = data; 
        Next = next; 
    } 
    public char Data; 
    public Node Next; 
} 
class GFG { 

    // Function to create a linked list 
    // from the given String 
    private static Node CreateLinkedList(String s) 
    { 
        Node header = null; 
        Node temp = null; 
        // Generates characters from the given string 
        for (int i = 0; i < s.length(); i++) { 
            char c = s.charAt(i); 
            Node node = new Node(c, null); 

            if (header == null) { 
                header = node; 
                temp = header; 
            } 
            else { 
                temp.Next = node; 
                temp = temp.Next; 
            } 
        } 
        return header; 
    } 

    // Function to reverse the words 
    // Assume str = "practice makes man perfect" 
    // to understand proper understanding of the code 
    private static Node Reverse(Node header) 
    { 
        if (header == null) 
            return header; 

        Node wordStartPosition = null; 
        Node endOfSentence = null; 
        Node sentenceStartPosition = null; 

        // Initialize wordStartPosition to header 
        // ie. node 'p' first letter of the word 'practice' 
        wordStartPosition = header; 

        // Navigate the linked list until 
        // a space(' ') is found or header is null 
        //(this is for handing if there is 
        // only one word in the given sentence) 
        while (header != null && header.Data != ' ') { 

            // Keep track the previous node. 
            // This will become the 
            // last node of the linked list 
            endOfSentence = header; 

            // Keep moving to the next node 
            header = header.Next; 
        } 

        // After the above while loop, 
        // endOfSentence points to 
        // the last letter 'e'of word 'practice' 
        // header points to the space(' ') 
        // which is next to word 'practice' 

        // If header is null then there is only 
        // one word in the given sentance 
        // so set header to the 
        // first/wordStartPosition node and return. 
        if (header == null) { 
            header = wordStartPosition; 
            return header; 
        } 

        do { 

            // Swapping the space ie. 
            // convert 'practice<space>' to 
            //'<space>practice' 

            // store the node which is next to space(' ') 
            // 'm' which is the first letter of the word 'make' 
            Node temp = header.Next; 
            header.Next = wordStartPosition; 
            wordStartPosition = header; 
            header = temp; 

            Node prev = null; 
            // Setting sentenceStartPosition to node 'm' 
            //(first letter of the word 'make') 
            sentenceStartPosition = header; 

            // Again Navigate the linked list until 
            // a space(' ') is found or 
            // header == null end of the linked list 
            while (header != null && header.Data != ' ') { 
                prev = header; 
                header = header.Next; 
            } 

            // When the next space is found, 
            // change the pointer to point the previous space 
            // ie. the word is being converted to 
            // "m->a->k->e->s-> ->p->r->a->c->t->i->c->e" 
            prev.Next = wordStartPosition; 

            // Newly found space will point to 
            //'m' first letter of the word 'make' 
            wordStartPosition = sentenceStartPosition; 
            if (header == null) 
                break; 

            // Repeat the loop until 
            // the end of the linked list is reached 
        } while (header != null); 

        header = sentenceStartPosition; 

        // Set the last node's next to null 
        // ie. ->m->a->k->e->s-> ->p->r->a->->c->t->i->c->e->null 
        endOfSentence.Next = null; 
        return header; 
    } 

    // Function to print the Linked List 
    private static void PrintList(Node Header) 
    { 
        Node temp = Header; 
        // Navigate till the end and print the data in each node 
        while (temp != null) { 
            System.out.print(temp.Data); 
            temp = temp.Next; 
        } 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        String s = "practice makes a man perfect"; 

        // Convert given string to a linked list 
        // with character as data in each node 
        Node header = CreateLinkedList(s); 

        System.out.println("Before:"); 
        PrintList(header); 

        header = Reverse(header); 

        System.out.println("\nAfter:"); 
        PrintList(header); 
    } 
} 

```

## C#

```cs

using System; 

// Linked List Implementation 
public class Node  
{ 
    public Node(char data, Node next) 
    { 
        Data = data; 
        Next = next; 
    } 
    public char Data; 
    public Node Next; 
} 

class GFG  
{ 

    // Function to create a linked list 
    // from the given String 
    private static Node CreateList(String s) 
    { 
        Node header = null; 
        Node temp = null; 

        // Generates characters from the given string 
        for (int i = 0; i < s.Length; i++) 
        { 
            char c = s[i]; 
            Node node = new Node(c, null); 

            if (header == null)  
            { 
                header = node; 
                temp = header; 
            } 
            else 
            { 
                temp.Next = node; 
                temp = temp.Next; 
            } 
        } 
        return header; 
    } 

    // Function to reverse the words 
    // Assume str = "practice makes man perfect" 
    // to understand proper understanding of the code 
    private static Node Reverse(Node header) 
    { 
        if (header == null) 
            return header; 

        Node wordStartPosition = null; 
        Node endOfSentence = null; 
        Node sentenceStartPosition = null; 

        // Initialize wordStartPosition to header 
        // ie. node 'p' first letter of the word 'practice' 
        wordStartPosition = header; 

        // Navigate the linked list until 
        // a space(' ') is found or header is null 
        //(this is for handing if there is 
        // only one word in the given sentence) 
        while (header != null && header.Data != ' ') 
        { 

            // Keep track the previous node. 
            // This will become the 
            // last node of the linked list 
            endOfSentence = header; 

            // Keep moving to the next node 
            header = header.Next; 
        } 

        // After the above while loop, 
        // endOfSentence points to 
        // the last letter 'e'of word 'practice' 
        // header points to the space(' ') 
        // which is next to word 'practice' 

        // If header is null then there is only 
        // one word in the given sentance 
        // so set header to the 
        // first/wordStartPosition node and return. 
        if (header == null)  
        { 
            header = wordStartPosition; 
            return header; 
        } 

        do 
        { 

            // Swapping the space ie. 
            // convert 'practice<space>' to 
            //'<space>practice' 

            // store the node which is next to space(' ') 
            // 'm' which is the first letter of the word 'make' 
            Node temp = header.Next; 
            header.Next = wordStartPosition; 
            wordStartPosition = header; 
            header = temp; 

            Node prev = null; 

            // Setting sentenceStartPosition to node 'm' 
            //(first letter of the word 'make') 
            sentenceStartPosition = header; 

            // Again Navigate the linked list until 
            // a space(' ') is found or 
            // header == null end of the linked list 
            while (header != null && header.Data != ' ')  
            { 
                prev = header; 
                header = header.Next; 
            } 

            // When the next space is found, 
            // change the pointer to point the previous space 
            // ie. the word is being converted to 
            // "m->a->k->e->s-> ->p->r->a->c->t->i->c->e" 
            prev.Next = wordStartPosition; 

            // Newly found space will point to 
            //'m' first letter of the word 'make' 
            wordStartPosition = sentenceStartPosition; 
            if (header == null) 
                break; 

            // Repeat the loop until 
            // the end of the linked list is reached 
        } 

        while (header != null); 
        header = sentenceStartPosition; 

        // Set the last node's next to null 
        // ie. ->m->a->k->e->s-> ->p->r->a->->c->t->i->c->e->null 
        endOfSentence.Next = null; 
        return header; 
    } 

    // Function to print the Linked List 
    private static void PrintList(Node Header) 
    { 
        Node temp = Header; 

        // Navigate till the end and print  
        // the data in each node 
        while (temp != null) 
        { 
            Console.Write(temp.Data); 
            temp = temp.Next; 
        } 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        String s = "practice makes a man perfect"; 

        // Convert given string to a linked list 
        // with character as data in each node 
        Node header = CreateList(s); 

        Console.WriteLine("Before:"); 
        PrintList(header); 

        header = Reverse(header); 

        Console.WriteLine("\nAfter:"); 
        PrintList(header); 
    } 
} 

// This code is contributed by Rajput-Ji 

```

**输出**：

```
Before:
practice makes a man perfect
After:
perfect man a makes practice

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。