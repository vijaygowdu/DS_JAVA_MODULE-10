# Ex10 Count the Number of Nodes in the Left Subtree of a Binary Tree
## DATE : 26.02.26
## Developed by: VIJAY K
## RegisterNumber: 212223040236
## AIM:
To design and implement a java program that constructs a binary tree from given level order input and counts the number of nodes present in the left subtree of the root node

## Algorithm
1. Start the program.
   
2. Define a Node class containing data, left child, and right child references.
   
4. Construct the binary tree using level order input:

   Use a queue to insert nodes level by level.
   
   For each node, assign left and right children based on input values.

4. Create a function to count the nodes in the left subtree of the root:

   Recursively count nodes using: count = 1 + count(left child) + count(right child)

5. Call the function using the left child of the root node.

6. Display the total number of nodes in the left subtree.

7. Stop the program.
   
## Program:
```
/*
Program to constructs a binary tree from given level order input and counts the number of nodes 
*/
import java.util.*;

class Node {
    int data;
    Node left, right;

    Node(int value) {
        data = value;
        left = right = null;
    }
}

public class LeftSubtreeCount {

    public static Node buildTreeLevelOrder(int[] arr) {
        if (arr.length == 0) return null;

        Node root = new Node(arr[0]);
        Queue<Node> queue = new LinkedList<>();
        queue.add(root);

        int i = 1;
        while (!queue.isEmpty() && i < arr.length) {
            Node current = queue.poll();

            // Insert left child
            if (i < arr.length) {
                current.left = new Node(arr[i++]);
                queue.add(current.left);
            }

            // Insert right child
            if (i < arr.length) {
                current.right = new Node(arr[i++]);
                queue.add(current.right);
            }
        }
        return root;
    }

    // Count nodes recursively
    public static int countNodes(Node root) {
        if (root == null) return 0;
        return 1 + countNodes(root.left) + countNodes(root.right);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter number of nodes: ");
        int n = sc.nextInt();

        int[] arr = new int[n];
        System.out.println("Enter level order elements:");
        for (int i = 0; i < n; i++) {
            arr[i] = sc.nextInt();
        }

        Node root = buildTreeLevelOrder(arr);

        int countLeft = countNodes(root.left);

        System.out.println("Number of nodes in the left subtree: " + countLeft);
        sc.close();
    }
}
```

## Output:
<img width="381" height="365" alt="image" src="https://github.com/user-attachments/assets/763990a7-1e36-489b-a003-4a9be74c0d4c" />



## Result:
The program has been successfully implemented and executed.
It correctly constructs the binary tree from level order input and counts the number of nodes in the left subtree of the root node.

# Ex22 Searching for a Book ID in a Binary Search Tree (BST)
## AIM:
To design and implement java program that constructs a Binary Search Tree (BST) using given Book IDs and checks whether a specific Book ID exists in the BST.
## Algorithm
1. Start the program.
   
2. Create a Node class with integer data, and left and right child references.
   
3. Create an insert() method to insert Book IDs into the BST:

   If the tree is empty, insert the new node as the root.

   Otherwise, traverse left or right depending on whether the value is smaller or larger.

4. Create a search() method to find a specified Book ID:

   If the node is null, return false.

   If the key matches, return true.

   Recursively search left or right according to BST rules.

5. Read Book IDs from the user and insert them into the BST.

6. Input a Book ID to search in the tree.

7. Display whether the Book ID exists or not.

8. Stop the program.
  

## Program:
```
/*
Program to construct a Binary Search Tree (BST) using given Book IDs 
and search for a specific Book ID
*/

import java.util.*;

class Node {
    int data;
    Node left, right;

    Node(int value) {
        data = value;
        left = right = null;
    }
}

public class Main {   // <- Make sure the file name is Main.java
    
    public static Node insert(Node root, int value) {
        if (root == null) {
            root = new Node(value);
            return root;
        }
        if (value < root.data) {
            root.left = insert(root.left, value);
        } else if (value > root.data) {
            root.right = insert(root.right, value);
        }
        return root;
    }

    public static boolean search(Node root, int key) {
        if (root == null) return false;
        if (root.data == key) return true;

        if (key < root.data)
            return search(root.left, key);
        else
            return search(root.right, key);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Node root = null;

        System.out.print("Enter number of Book IDs: ");
        int n = sc.nextInt();

        System.out.println("Enter Book IDs:");
        for (int i = 0; i < n; i++) {
            int id = sc.nextInt();
            root = insert(root, id);
        }

        System.out.print("Enter Book ID to search: ");
        int key = sc.nextInt();

        if (search(root, key))
            System.out.println("Book ID Found");
        else
            System.out.println("Book ID Not Found");

        sc.close();
    }
}


```

## Output:
<img width="377" height="246" alt="image" src="https://github.com/user-attachments/assets/c7aa913c-c232-4db1-a309-d8d7d25b588a" />


## Result:
The program has been successfully implemented and executed.
It constructs a Binary Search Tree from the given Book IDs and accurately determines whether a queried Book ID exists in the library system.


# Ex23 Breadth-First Search (BFS) Traversal of a City Junction Map
## AIM:
To design and implement a java program to perform Breadth-First Search (BFS) traversal on a city’s junction map represented as a graph, and find all reachable locations from a given source junction.
## Algorithm
1. Start the program.
2. Read the number of junctions and create an adjacency list to represent the graph.
3. Read the connections (edges) between city junctions.
4. Initialize a queue and a visited array to track visited junctions.
5. Insert the starting junction into the queue and mark it as visited.
6. While the queue is not empty:
 
   Remove the front node from the queue and print it.

   Add all unvisited adjacent junctions to the queue and mark them visited.

7. Display all traversed junctions in BFS order.

8. Stop the program.

## Program:
```
/*
Program to perform Breadth-First Search (BFS) traversal on a city’s junction map represented as a graph
*/

import java.util.*;

public class BFS_CityJunction {

    static void bfsTraversal(List<List<Integer>> graph, int start, int n) {
        boolean[] visited = new boolean[n];
        Queue<Integer> queue = new LinkedList<>();

        visited[start] = true;
        queue.add(start);

        System.out.print("BFS Traversal: ");

        while (!queue.isEmpty()) {
            int node = queue.poll();
            System.out.print(node + " ");

            for (int neighbor : graph.get(node)) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.add(neighbor);
                }
            }
        }
        System.out.println();
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter number of junctions: ");
        int n = sc.nextInt();

        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            graph.add(new ArrayList<>());
        }

        System.out.print("Enter number of roads (edges): ");
        int e = sc.nextInt();

        System.out.println("Enter each road (junction1 junction2):");
        for (int i = 0; i < e; i++) {
            int u = sc.nextInt();
            int v = sc.nextInt();
            graph.get(u).add(v);
            graph.get(v).add(u);  // For undirected city map
        }

        System.out.print("Enter source junction: ");
        int start = sc.nextInt();

        bfsTraversal(graph, start, n);

        sc.close();
    }
}
```

## Output:
<img width="380" height="409" alt="image" src="https://github.com/user-attachments/assets/052e429b-8647-451f-a222-f5ab3a1a89bd" />



## Result:
The program has been successfully implemented and executed.
It performs Breadth-First Search (BFS) traversal on a city junction map and correctly lists all reachable locations from the given source node.


# Ex24 Shortest Path and Reachability in a Heritage Town using BFS
## AIM:
To design and implement a java program that, given a map of attractions in a heritage town connected by walking paths, recommends:
The shortest number of paths (minimum hops) from a starting attraction to a target attraction.
The number of reachable attractions from the same starting point using Breadth-First Search (BFS)


## Algorithm
1. Start the program.
2. Read the number of attractions and initialize an adjacency list.
3. Read the walking paths (edges) connecting attractions.
4. Use BFS to find:

   Shortest path (minimum hops) from start node to destination node using a distance array.

   Reachability count, i.e., number of attractions reachable from the start.

5. Initialize arrays for visited and distance, and a queue for BFS.
6. Set the starting node as visited and enqueue it.
7. While the queue is not empty:
   
  Dequeue the current node.

  For each adjacent node, if not visited, enqueue it and update its distance.

8. After BFS completes:

9. Display reachable attractions and count.

10. Display the shortest distance to the destination node.

11. Stop the program.

## Program:
```
/*
Program to determine Shortest Path and Reachability in a Heritage Town using BFS
*/
import java.util.*;

public class HeritageTownBFS {

    public static void bfs(int start, List<List<Integer>> graph, int n, int destination) {
        boolean[] visited = new boolean[n];
        int[] distance = new int[n];
        Arrays.fill(distance, -1);

        Queue<Integer> queue = new LinkedList<>();
        visited[start] = true;
        distance[start] = 0;
        queue.add(start);

        int reachableCount = 0;

        System.out.print("Reachable Attractions: ");

        while (!queue.isEmpty()) {
            int node = queue.poll();
            System.out.print(node + " ");
            reachableCount++;

            for (int next : graph.get(node)) {
                if (!visited[next]) {
                    visited[next] = true;
                    distance[next] = distance[node] + 1;
                    queue.add(next);
                }
            }
        }

        System.out.println("\nTotal reachable attractions: " + reachableCount);

        if (distance[destination] != -1)
            System.out.println("Shortest path (minimum hops) to attraction " + destination + ": " + distance[destination]);
        else
            System.out.println("Destination attraction is not reachable.");
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter number of attractions: ");
        int n = sc.nextInt();
        List<List<Integer>> graph = new ArrayList<>();

        for (int i = 0; i < n; i++) {
            graph.add(new ArrayList<>());
        }

        System.out.print("Enter number of walking paths: ");
        int e = sc.nextInt();

        System.out.println("Enter paths (attraction1 attraction2):");
        for (int i = 0; i < e; i++) {
            int u = sc.nextInt();
            int v = sc.nextInt();
            graph.get(u).add(v);
            graph.get(v).add(u); // undirected
        }

        System.out.print("Enter starting attraction: ");
        int start = sc.nextInt();

        System.out.print("Enter destination attraction: ");
        int destination = sc.nextInt();

        bfs(start, graph, n, destination);
        sc.close();
    }
}
```

## Output:

<img width="538" height="500" alt="image" src="https://github.com/user-attachments/assets/5c316122-d16b-4743-b5b3-341f81b28788" />


## Result:
The program has been successfully implemented and executed.
It correctly computes:
The shortest number of paths (minimum hops) between two attractions.
The total number of reachable attractions from a given starting point using BFS traversal.

# Ex25 Finding the Fastest Route to a Charging Station using Dijkstra’s Algorithm
## AIM:
To design and implement a java program that helps an electric vehicle (EV) find the shortest travel time from its current block to the nearest charging station using Dijkstra’s shortest path algorithm.
## Algorithm
1. Start the program and input the number of blocks (nodes) and roads (edges).
2. Construct a graph using an adjacency matrix or adjacency list where each edge contains the time taken to travel between blocks.
3. Input the current block of the EV and the list of blocks that contain charging stations.
4. Apply Dijkstra’s algorithm from the EV’s current block to compute the shortest travel time to every other block.
5. Identify the block from the charging station list that has the minimum travel time.
6. Display the shortest time and the corresponding charging station.
7. If no charging station is reachable, display an appropriate message.
8. Stop the program.

## Program:
```
/*
Program to find the Fastest Route to a Charging Station using Dijkstra’s Algorithm
*/
import java.util.*;

class DijkstraEV {
    private static final int INF = Integer.MAX_VALUE;

    public static int dijkstra(int[][] graph, int src, boolean[] charger) {
        int V = graph.length;
        int[] dist = new int[V];
        boolean[] visited = new boolean[V];

        Arrays.fill(dist, INF);
        dist[src] = 0;

        for (int i = 0; i < V - 1; i++) {
            int u = getMinDistanceNode(dist, visited);
            visited[u] = true;

            for (int v = 0; v < V; v++) {
                if (!visited[v] && graph[u][v] != 0 && dist[u] != INF &&
                    dist[u] + graph[u][v] < dist[v]) {
                    dist[v] = dist[u] + graph[u][v];
                }
            }
        }

        int minTime = INF;
        for (int i = 0; i < V; i++) {
            if (charger[i] && dist[i] < minTime) {
                minTime = dist[i];
            }
        }
        return minTime;
    }

    private static int getMinDistanceNode(int[] dist, boolean[] visited) {
        int min = INF, minIndex = -1;
        for (int v = 0; v < dist.length; v++) {
            if (!visited[v] && dist[v] < min) {
                min = dist[v];
                minIndex = v;
            }
        }
        return minIndex;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter number of blocks: ");
        int V = sc.nextInt();

        int[][] graph = new int[V][V];
        System.out.println("Enter travel time matrix (0 if no direct connection): ");
        for (int i = 0; i < V; i++) {
            for (int j = 0; j < V; j++) {
                graph[i][j] = sc.nextInt();
            }
        }

        System.out.print("Enter current EV position (0 to " + (V - 1) + "): ");
        int src = sc.nextInt();

        boolean[] charger = new boolean[V];
        System.out.print("Enter number of charging stations: ");
        int n = sc.nextInt();
        System.out.println("Enter charging station positions:");
        for (int i = 0; i < n; i++) {
            charger[sc.nextInt()] = true;
        }

        int minTime = dijkstra(graph, src, charger);

        if (minTime == INF) {
            System.out.println("No reachable charging station!");
        } else {
            System.out.println("Shortest travel time to nearest charging station: " + minTime + " minutes");
        }
    }
}
```

## Output:

<img width="648" height="443" alt="image" src="https://github.com/user-attachments/assets/1b009bad-d4fe-40aa-85a0-5afa4ecc7836" />


## Result:
The program has been successfully implemented and executed.
It uses Dijkstra’s algorithm to determine the shortest travel time from the EV’s current location to the nearest charging station and correctly handles cases where no station is reachable.
