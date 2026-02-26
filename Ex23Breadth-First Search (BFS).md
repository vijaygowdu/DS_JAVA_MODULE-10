# Ex23 Breadth-First Search (BFS) Traversal of a City Junction Map
## DATE:26.02.26
## AIM:
To design and implement a java program to perform Breadth-First Search (BFS) traversal on a city’s junction map represented as a graph, and find all reachable locations from a given source junction.
## Algorithm
1. Start the program.
2. Read two integers.
3. Create an adjacency list g of size n.
4. Repeat e times.
5. Read the source node.
6. Initialize a boolean array of size n, all set to false.
7. Create an empty queue.
8. Mark src as visited and enqueue it.
9. Continue until all reachable nodes are processed.
10. Stop the program.

## Program:
```
/*
Program to perform Breadth-First Search (BFS) traversal on a city’s junction map represented as a graph
Developed by: VIJAY K
RegisterNumber:  212223040236
*/
```
```
import java.util.*;

public class EmergencyRouteBFS {

    public static void addEdge(List<List<Integer>> g, int u, int v) {
        g.get(u).add(v);
        g.get(v).add(u); // Undirected graph
    }

    public static void bfs(List<List<Integer>> g, int src, boolean[] visited) {
        Queue<Integer> queue = new LinkedList<>();

        visited[src] = true;
        queue.add(src);

        while (!queue.isEmpty()) {
            int current = queue.poll();
            System.out.print(current + " ");

            for (int neighbor : g.get(current)) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.add(neighbor);
                }
            }
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt(), e = sc.nextInt();
        List<List<Integer>> g = new ArrayList<>();

        for (int i = 0; i < n; i++)
            g.add(new ArrayList<>());

        for (int i = 0; i < e; i++)
            addEdge(g, sc.nextInt(), sc.nextInt());

        int src = sc.nextInt();
        bfs(g, src, new boolean[n]);
    }
}
```

## Output:
<img width="470" height="373" alt="image" src="https://github.com/user-attachments/assets/c8ae4ece-0d8d-4612-b85c-d30c5557c3f5" />

## Result:
The program has been successfully implemented and executed.
It performs Breadth-First Search (BFS) traversal on a city junction map and correctly lists all reachable locations from the given source node.
