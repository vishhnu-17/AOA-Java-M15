# EX 5D Flower Planting.
## DATE : 15-11-2025

## AIM:

To write a Java program to for given constraints.
You are given n gardens, labelled from 1 to n.

You also have a list called paths, where each element paths[i] = [xi, yi] represents a bidirectional road connectingthe garden xi and garden yi.

You want to plant one flower in each garden, and there are exactly 4 types of flowers labelled as 1, 2, 3, and 4.

Your goal is to plant flowers such that:

No two connected gardens (i.e., connected via a path) have the same flower type.

Return any valid flower assignment as an array where:

answer[i] is the flower type planted in the (i+1) ᵗʰ garden

It is guaranteed that:

No garden is connected to more than 3 other gardens

A valid flower assignment always exists

<img width="177" height="292" alt="image" src="https://github.com/user-attachments/assets/36aa40cb-1cdd-4746-b1a6-fc51ce6e96aa" />

## Algorithm

1. Represent the gardens and paths as an adjacency list.
2. Initialize an array `flowers` of size `n` to store the flower type for each garden.
3. Iterate over each garden and check the flower types already used by its neighbors.
4. Assign the smallest available flower type (1–4) not used by neighbors.
5. Return the `flowers` array.

#### Developed By: Kurapati Vishnu Vardhan Reddy
#### Register Number: 212223040103

## Program:

### to implement graph coloring

```java
import java.util.*;

public class Main {

    public static int[] gardenNoAdj(int n, int[][] paths) {
        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++) graph.add(new ArrayList<>());

        for (int[] path : paths) {
            int u = path[0] - 1;
            int v = path[1] - 1;
            graph.get(u).add(v);
            graph.get(v).add(u);
        }

        int[] flowers = new int[n];

        for (int i = 0; i < n; i++) {
            boolean[] used = new boolean[5]; // flower types 1-4

            for (int neighbor : graph.get(i)) {
                used[flowers[neighbor]] = true;
            }

            for (int f = 1; f <= 4; f++) {
                if (!used[f]) {
                    flowers[i] = f;
                    break;
                }
            }
        }

        return flowers;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter number of gardens: ");
        int n = sc.nextInt();
        System.out.print("Enter number of paths: ");
        int m = sc.nextInt();

        int[][] paths = new int[m][2];
        System.out.println("Enter paths (two numbers per line):");
        for (int i = 0; i < m; i++) {
            paths[i][0] = sc.nextInt();
            paths[i][1] = sc.nextInt();
        }

        int[] result = gardenNoAdj(n, paths);
        for (int f : result) System.out.print(f + " ");

        sc.close();
    }
}
```

## Output:

```
input:
4
3
1 2
2 3
3 4

output:
1 2 1 2
```

## Result:

The program successfully implemented and the expected output is verified.
