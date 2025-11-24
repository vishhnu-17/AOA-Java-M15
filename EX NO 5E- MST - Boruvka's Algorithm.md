# EX 5E Minimum Spanning Tree -Boruvka's Algorithm
## DATE : 15-11-2025
## AIM:

To write a Java program to for given constraints.
Boruvka's Algorithm - Minimum Spanning Tree

Find the MST using Boruvka's Algorithm for a weighted undirected graph.
<img width="292" height="235" alt="image" src="https://github.com/user-attachments/assets/06246b27-37a9-40a8-bd7a-37a1d5187cd1" />

## Algorithm

1. Initialize each vertex as a separate component.
2. While there is more than one component:
   - For each component, find the **cheapest edge** connecting it to a different component.
   - Add these cheapest edges to the MST.
   - Merge connected components using union-find.
3. Repeat until all vertices belong to a single component.
4. Keep track of the MST edges and total weight.
5. Output the MST edges and total weight.

### Developed by : Kurapati Vishnu Vardhan Reddy
### Register Number : 212223040103

## Program:

### to implement Minimum Spanning Tree (MST)

```java
import java.util.*;

public class Main {

    static class Edge {
        int u, v, weight;
        Edge(int u, int v, int w) { this.u = u; this.v = v; this.weight = w; }
    }

    static int find(int[] parent, int i) {
        if (parent[i] != i) parent[i] = find(parent, parent[i]);
        return parent[i];
    }

    static void union(int[] parent, int[] rank, int x, int y) {
        int xroot = find(parent, x);
        int yroot = find(parent, y);

        if (rank[xroot] < rank[yroot]) parent[xroot] = yroot;
        else if (rank[xroot] > rank[yroot]) parent[yroot] = xroot;
        else {
            parent[yroot] = xroot;
            rank[xroot]++;
        }
    }

    public static void boruvkaMST(int V, List<Edge> edges) {
        int[] parent = new int[V];
        int[] rank = new int[V];

        for (int i = 0; i < V; i++) parent[i] = i;

        int numComponents = V;
        int mstWeight = 0;
        List<Edge> mstEdges = new ArrayList<>();

        while (numComponents > 1) {
            Edge[] cheapest = new Edge[V];

            for (Edge e : edges) {
                int set1 = find(parent, e.u);
                int set2 = find(parent, e.v);

                if (set1 != set2) {
                    if (cheapest[set1] == null || e.weight < cheapest[set1].weight)
                        cheapest[set1] = e;
                    if (cheapest[set2] == null || e.weight < cheapest[set2].weight)
                        cheapest[set2] = e;
                }
            }

            for (int i = 0; i < V; i++) {
                Edge e = cheapest[i];
                if (e != null) {
                    int set1 = find(parent, e.u);
                    int set2 = find(parent, e.v);

                    if (set1 != set2) {
                        mstWeight += e.weight;
                        mstEdges.add(e);
                        union(parent, rank, set1, set2);
                        numComponents--;
                    }
                }
            }
        }

        System.out.println("Edges in MST:");
        for (Edge e : mstEdges) {
            System.out.println(e.u + " - " + e.v + " : " + e.weight);
        }
        System.out.println("Total weight of MST: " + mstWeight);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter number of vertices: ");
        int V = sc.nextInt();
        System.out.print("Enter number of edges: ");
        int E = sc.nextInt();

        List<Edge> edges = new ArrayList<>();
        System.out.println("Enter edges (u v weight):");
        for (int i = 0; i < E; i++) {
            int u = sc.nextInt();
            int v = sc.nextInt();
            int w = sc.nextInt();
            edges.add(new Edge(u, v, w));
        }

        boruvkaMST(V, edges);
        sc.close();
    }
}
```

## Output:

```
input:
4
5
0 1 10
0 2 6
0 3 5
1 3 15
2 3 4

output:
Edges in MST:
2 - 3 : 4
0 - 3 : 5
0 - 1 : 10
Total weight of MST: 19
```

## Result:

The program successfully implemented and the expected output is verified.
