# EX 5C Graph coloring
## DATE : 15-11-2025

## AIM:

To write a Java program to for given constraints.
Problem Description:
In a hilly region, several radio towers are installed to provide communication services. However, due to signal interference, two adjacent towers (i.e., in communication range of each other) must not use the same frequency channel.

You are given N radio towers and their communication ranges represented as an undirected graph. Your task is to assign channels (colors) to these towers using at most M channels such that no two adjacent towers use the same channel.

Write a program to determine if such an assignment is possible or not.

Input Format:
First line contains two integers: N (number of towers), and M (number of available frequency channels).

Next line contains an integer E — number of edges representing the communication range.

Next E lines contain two integers u and v — representing that tower u and tower v are within range (0-based index).

Output Format:
Print "YES" if it's possible to assign frequencies to towers such that no two adjacent towers have the same frequency.

Otherwise, print "NO".

<img width="182" height="440" alt="image" src="https://github.com/user-attachments/assets/b32078a2-c79d-4a25-88c4-e51144b5456f" />

## Algorithm

1. Represent the communication network as an adjacency list or adjacency matrix.
2. Use backtracking to try assigning each tower a channel from 1 to M.
3. Before assigning a channel, check if any adjacent tower already has that channel.
4. Recursively assign channels to the next tower.
5. If all towers are assigned valid channels, return YES; otherwise, after exploring all possibilities, return NO.

#### Developed By: Kurapati Vishnu Vardhan Reddy
#### Register Number: 212223040103

## Program:

### to implement Reverse a String

```java
import java.util.*;

public class Main {

    static int N, M;
    static List<List<Integer>> graph;

    public static boolean canColor(int[] color, int node) {
        if (node == N) return true;

        for (int c = 1; c <= M; c++) {
            boolean valid = true;
            for (int neighbor : graph.get(node)) {
                if (color[neighbor] == c) {
                    valid = false;
                    break;
                }
            }

            if (valid) {
                color[node] = c;
                if (canColor(color, node + 1)) return true;
                color[node] = 0; // backtrack
            }
        }
        return false;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        N = sc.nextInt();
        M = sc.nextInt();
        int E = sc.nextInt();

        graph = new ArrayList<>();
        for (int i = 0; i < N; i++) graph.add(new ArrayList<>());

        for (int i = 0; i < E; i++) {
            int u = sc.nextInt();
            int v = sc.nextInt();
            graph.get(u).add(v);
            graph.get(v).add(u);
        }

        int[] color = new int[N];
        if (canColor(color, 0)) System.out.println("YES");
        else System.out.println("NO");

        sc.close();
    }
}
```

## Output:

```
input:
4 3
5
0 1
0 2
1 2
1 3
2 3

output:
YES
```

## Result:

The program successfully implemented and the expected output is verified.
