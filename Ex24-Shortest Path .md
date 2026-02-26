# Ex24 Shortest Path and Reachability in a Heritage Town using BFS
## DATE:26.02.26
## AIM:
To design and implement a java program that, given a map of attractions in a heritage town connected by walking paths, recommends:
The shortest number of paths (minimum hops) from a starting attraction to a target attraction.
The number of reachable attractions from the same starting point using Breadth-First Search (BFS)


## Algorithm
1. Start the program.
2. Read integers.
3. Create an adjacency list graph of size n.
4. Build the Graph.
5. Read Start and Target.
6. Initialize BFS.
7. Initialize DFS
8. Counting Reachable Attractions and Print.
9. End the program.  

## Program:
```
/*
Program to determine Shortest Path and Reachability in a Heritage Town using BFS
Developed by: VIJAY K
RegisterNumber:  212223040236
*/
```
```
import java.util.*;

public class TouristNavigation {
    
    public static int shortestPath(List<List<Integer>> graph, int start, int target, int n) {
        
        boolean[] visited = new boolean[n];
        int[] distance = new int[n];
        Queue<Integer> queue = new LinkedList<>();

        visited[start] = true;
        queue.add(start);
        distance[start] = 0;

        while (!queue.isEmpty()) {
            int node = queue.poll();

            if (node == target)
                return distance[node];

            for (int neighbor : graph.get(node)) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    distance[neighbor] = distance[node] + 1;
                    queue.add(neighbor);
                }
            }
        }

        return -1; // unreachable
    }

    public static void reachableAttractions(List<List<Integer>> graph, boolean[] visited, int node) {
        visited[node] = true;

        for (int neighbor : graph.get(node)) {
            if (!visited[neighbor]) {
                reachableAttractions(graph, visited, neighbor);
            }
        }
    }

    public static int countReachable(boolean[] visited) {
        int count = 0;
        for (boolean v : visited) {
            if (v) count++;
        }
        return count;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt(), e = sc.nextInt();
        List<List<Integer>> graph = new ArrayList<>();

        for (int i = 0; i < n; i++)
            graph.add(new ArrayList<>());

        for (int i = 0; i < e; i++) {
            int u = sc.nextInt(), v = sc.nextInt();
            graph.get(u).add(v);
            graph.get(v).add(u);
        }

        int start = sc.nextInt();
        int target = sc.nextInt();

        int shortest = shortestPath(graph, start, target, n);

        boolean[] visited = new boolean[n];
        reachableAttractions(graph, visited, start);
        int reachable = countReachable(visited);

        System.out.println("Shortest path from start to target: " + shortest);
        System.out.println("Total reachable attractions from start: " + reachable);
    }
}
```

## Output:
<img width="1185" height="382" alt="image" src="https://github.com/user-attachments/assets/6b74ef81-43a4-46dc-a831-4766feafbfcc" />

## Result:
The program has been successfully implemented and executed.
It correctly computes:
The shortest number of paths (minimum hops) between two attractions.
The total number of reachable attractions from a given starting point using BFS traversal.
