# Ex21 Count the Number of Nodes in the Left Subtree of a Binary Tree
## DATE:26.02.26
## AIM:
To design and implement a java program that constructs a binary tree from given level order input and counts the number of nodes present in the left subtree of the root node

## Algorithm
1. Start the program.
2. Read integer.
3. Create an array of size n.
4.  Read n integers and store them in array.
5.   Building the Tree (Level-Order).
6. Counting Left Subtree Nodes.
7. Print the result.
8. Stop the program.  

## Program:
```
/*
Program to constructs a binary tree from given level order input and counts the number of nodes 
Developed by: VIJAY K
RegisterNumber:  212223040236
*/
```
```
import java.util.*;

class Node {
    int data;
    Node left, right;

    Node(int data) {
        this.data = data;
        left = right = null;
    }
}

public class Main {

    static Node buildTree(int[] arr) {
        if (arr.length == 0) return null;

        Node root = new Node(arr[0]);
        Queue<Node> queue = new LinkedList<>();
        queue.add(root);

        int i = 1;
        while (i < arr.length) {
            Node current = queue.poll();

            if (i < arr.length) {
                current.left = new Node(arr[i++]);
                queue.add(current.left);
            }

            if (i < arr.length) {
                current.right = new Node(arr[i++]);
                queue.add(current.right);
            }
        }
        return root;
    }

    static int count(Node root) {
        if (root == null) return 0;
        return 1 + count(root.left) + count(root.right);
    }

    static void countNodes(Node root) {
        if (root == null || root.left == null) {
            System.out.println(0);
            return;
        }
        System.out.println(count(root.left));
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();
        int[] arr = new int[n];

        for (int i = 0; i < n; i++)
            arr[i] = sc.nextInt();

        Node root = buildTree(arr);
        countNodes(root);
    }
}
```

## Output:
<img width="396" height="278" alt="image" src="https://github.com/user-attachments/assets/679c6749-21ed-495f-b157-3d2a5995ff3e" />

## Result:
The program has been successfully implemented and executed.
It correctly constructs the binary tree from level order input and counts the number of nodes in the left subtree of the root node.
