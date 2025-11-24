# EX 5A 0/1 Knapsack Problem - Branch&Bound
## DATE : 15-11-2025

## AIM:

To Write a Java program to solve 0/1 Knapsack problem using Branch and Bound Approach.
You are heading a college entrepreneurship cell that can invest in up to N student‑startups.

For each startup i you know: cost[i]  — the amount (in ₹ lakh) required to join the showcase profit[i] — the estimated profit (in ₹ lakh) you’ll gain if it succeeds You have a total budget of B ₹ lakh. Pick a subset of startups so that the sum of costs ≤ B and the sum of profits is maximised.

Because N can be as large as 50, a plain exhaustive search (2^N) is too slow.

The recommended approach is Branch & Bound with a fractional‑knapsack upper bound (but any algorithm that meets the constraints is accepted).

Input Format

N

B

cost[1] cost[2] … cost[N]

profit[1] profit[2] … profit[N]

1 ≤ N ≤ 50

1 ≤ B ≤ 1 000 000

1 ≤ cost[i], profit[i] ≤ 10 000

Output Format

maxProfit

## Algorithm

1. Sort the items by **profit-to-cost ratio** in descending order for the fractional knapsack bound.
2. Use a **priority queue (max heap)** to explore promising nodes first based on upper bound.
3. Each node represents: current level, profit, cost, and estimated upper bound.
4. Expand nodes by including or excluding the next item; prune nodes where cost > budget or bound < current max profit.
5. Return the maximum profit found after all feasible nodes are explored.

#### Developed By: Kurapati Vishnu Vardhan Reddy

#### Register Number: 212223040103

## Program:

### to implement 0/1 Knapsack Problem

```java
import java.util.*;

public class Main {

    static class Item implements Comparable<Item> {
        int cost, profit;
        double ratio;

        Item(int cost, int profit) {
            this.cost = cost;
            this.profit = profit;
            this.ratio = (double) profit / cost;
        }

        public int compareTo(Item other) {
            return Double.compare(other.ratio, this.ratio); // descending
        }
    }

    static class Node implements Comparable<Node> {
        int level, profit, cost;
        double bound;

        Node(int level, int profit, int cost) {
            this.level = level;
            this.profit = profit;
            this.cost = cost;
        }

        public int compareTo(Node other) {
            return Double.compare(other.bound, this.bound); // max-heap
        }
    }

    public static int knapsack(int[] cost, int[] profit, int B) {
        int N = cost.length;
        Item[] items = new Item[N];
        for (int i = 0; i < N; i++) items[i] = new Item(cost[i], profit[i]);
        Arrays.sort(items);

        PriorityQueue<Node> pq = new PriorityQueue<>();
        Node u = new Node(-1, 0, 0);
        u.bound = bound(u, N, B, items);
        pq.offer(u);

        int maxProfit = 0;

        while (!pq.isEmpty()) {
            Node v = pq.poll();

            if (v.bound <= maxProfit || v.level == N - 1) continue;

            // Take next item
            Node with = new Node(v.level + 1, v.profit + items[v.level + 1].profit,
                                 v.cost + items[v.level + 1].cost);
            if (with.cost <= B && with.profit > maxProfit) maxProfit = with.profit;
            with.bound = bound(with, N, B, items);
            if (with.bound > maxProfit) pq.offer(with);

            // Do not take next item
            Node without = new Node(v.level + 1, v.profit, v.cost);
            without.bound = bound(without, N, B, items);
            if (without.bound > maxProfit) pq.offer(without);
        }

        return maxProfit;
    }

    private static double bound(Node u, int N, int B, Item[] items) {
        if (u.cost > B) return 0;
        double profitBound = u.profit;
        int j = u.level + 1;
        int totWeight = u.cost;

        while (j < N && totWeight + items[j].cost <= B) {
            totWeight += items[j].cost;
            profitBound += items[j].profit;
            j++;
        }

        if (j < N) profitBound += (B - totWeight) * items[j].ratio;

        return profitBound;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int N = sc.nextInt();
        int B = sc.nextInt();

        int[] cost = new int[N];
        int[] profit = new int[N];

        for (int i = 0; i < N; i++) cost[i] = sc.nextInt();
        for (int i = 0; i < N; i++) profit[i] = sc.nextInt();

        System.out.println(knapsack(cost, profit, B));
        sc.close();
    }
}
```

## Output:

```
input:
4
50
10 20 30 40
60 100 120 240

output:
300
```

## Result:

The program successfully solved 0/1 Knapsack problem using branch & bound and output is verified.
