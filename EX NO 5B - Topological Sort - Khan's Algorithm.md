# EX 5B Topological Sort - Khan's Algorithm
## DATE : 15-11-2025
## AIM:

To write a Java program to for given constraints.
Problem Description:
A software development team is preparing for a product release. The release consists of multiple tasks, each dependent on other tasks being completed first. You are to determine a valid order in which all tasks can be completed. If it's not possible due to cyclic dependencies, output that the release cannot be scheduled.

Each task is labeled from 0 to n-1. The dependencies are provided in the form of pairs [a, b] which means task a depends on task b.

Implement a program to find a valid task execution order using topological sort.

Input Format:

An integer n — number of tasks.

An integer m — number of dependencies.

m lines follow with two integers a and b — representing a depends on b.

Output Format:

If a valid order exists, print the task numbers in a possible execution order (space-separated).

If not, print "Release cannot be scheduled".

<img width="341" height="363" alt="image" src="https://github.com/user-attachments/assets/f0355541-4f66-49da-bcd3-171a799a7c1f" />

## Algorithm

1. Build a directed graph using adjacency lists from the given dependencies.
2. Compute in-degrees of all tasks.
3. Use a queue to process all tasks with in-degree 0 (no dependencies).
4. Remove processed tasks from the graph, updating in-degrees of neighbors.
5. If all tasks are processed, print the order; otherwise, a cycle exists and the release cannot be scheduled.

#### Developed By: Kurapati Vishnu Vardhan Reddy
#### Register Number: 212223040103

## Program:to implement Topological Sort

```java
import java.util.*;

public class Main {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt(); // number of tasks
        int m = sc.nextInt(); // number of dependencies

        List<List<Integer>> graph = new ArrayList<>();
        int[] inDegree = new int[n];

        for (int i = 0; i < n; i++) graph.add(new ArrayList<>());

        for (int i = 0; i < m; i++) {
            int a = sc.nextInt();
            int b = sc.nextInt();
            graph.get(b).add(a); // b → a (a depends on b)
            inDegree[a]++;
        }

        Queue<Integer> queue = new LinkedList<>();
        for (int i = 0; i < n; i++) if (inDegree[i] == 0) queue.offer(i);

        List<Integer> order = new ArrayList<>();

        while (!queue.isEmpty()) {
            int task = queue.poll();
            order.add(task);

            for (int neighbor : graph.get(task)) {
                inDegree[neighbor]--;
                if (inDegree[neighbor] == 0) queue.offer(neighbor);
            }
        }

        if (order.size() != n) {
            System.out.println("Release cannot be scheduled");
        } else {
            for (int i = 0; i < order.size(); i++) {
                System.out.print(order.get(i));
                if (i < order.size() - 1) System.out.print(" ");
            }
        }

        sc.close();
    }
}
```

## Output:

```
input:
6
6
5 2
5 0
4 0
4 1
2 3
3 1

output:
4 5 0 2 3 1
```

## Result:

The program successfully implemented and the expected output is verified.
