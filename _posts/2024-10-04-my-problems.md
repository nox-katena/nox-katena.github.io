---
redirect_from: /_posts/2024-10-04-my-problems/
title: Solutions to Problems I Authored 
tags:
  - Baekjoon Online Judge
  - Project PS
---

Solution sketches to problems I authored. Will keep updating with more problems. All solutions are in English. Problem statements may not be in English. (Last Updated : 2024-10-04)

## /<30872> Hanyang Cherry Picking Contest

- Link : https://www.acmicpc.net/problem/30872
- Intended Difficulty : <span style="color:#27E2A4">Platinum III</span>
- Source : 10th HCPC (Beginner Division Problem E)

Co-authored with hibye1217.

#### Solution (Tree DP + Game Theory)

Let's denote Sehun's score as $S$ and Cheolmin's score as $C$. Then we can define the total score of the game as $S - C$. Sehun's goal is to maximize this score while Cheolmin's goal is to minimize this score. For now let's call this score $T$.

Now let's make some observations about the game.

1. Once you enter a node $v$, you cannot leave the subtree rooted at $v$ until all nodes in the subtree are taken.
2. Since you take one node a turn, who the next player after the players exit the subtree rooted at $v$ depends on whether the number of nodes in the subtree is even or odd.

Based on the observations, we can think about saving the following information about each subtree.

- $T_v$ : The score of the game considering only the subtree rooted at $v$.
- $C_v$ : The number of nodes in the subtree rooted at $v$.

Both of these values can be calculated using dynamic programming.

Now let's think of the optimal strategy. First, the game always begins with Sehun taking the root. Now, Cheolmin wants to take the nodes with maximum score while maintaining his turn. That is, all children whose $T_w \ge 0$ and $C_w \equiv 0 \mod 2$.

After this, Cheolmin and Sehun will take turns taking the children with maximum $S_w$ whose $C_w$ value is odd.

The player who receives the turn at the end of the above process will take all children whose $T_w < 0$ and $C_w \equiv 0 \mod 2$.

The winner is then decided on whether $T_1$ is positive or negative.

## /<30879> I Wonder What's for Dinner...

- Link : https://www.acmicpc.net/problem/30879
- Intended Difficulty : <span style="color:#27E2A4">Platinum III</span>
- Source : 10th HCPC (Advanced Division Problem B)

#### Solution (2-SAT + Binary Search)

Fancy way of calling this problem would be "Offline Incremental 2-Satisfiability" maybe.

If a query of type 2 was only given at the end, then it's easy to see that the problem is solvable with 2-SAT.

Let's define $chk(x)$ to be a boolean function which returns whether or not the answer to a query of type 2 would be "YES" or "NO" after processing the first $x$ queries.

We can notice that there exists some $v$ such that $chk(v)$ is $\texttt{true}$ but $chk(v + 1)$ is $\texttt{false}$ and for all $u$ such that $u \ge v + 1$, $chk(u)$ is $\texttt{false}$.

This is because we are dealing with only clause additions. Thus, there exists some point in time where we added a clause and it caused the boolean expression to be unsatisfiable.

Again, since we are only dealing with addition, the answer to type 2 queries will not change after that.

If we store all queries first and process them offline, we can think about finding $v$ using binary search. Since 2-SAT is solvable in linear time and binary search is $logN$, the total time complexity is something around $NlogN$.

Also, if anyone knows an **online solution** or an **offline fully dynamic version** of this problem please do reach out. I initially wanted to set it as the "Hard version" of this problem but failed to solve it efficiently.

## /<30885> Φ²

- Link : https://www.acmicpc.net/problem/30885
- Intended Difficulty : <span style="color:#D28500">Gold V</span>
- Source : 10th HCPC (Advanced Division Problem J)

#### Solution (Data Structures, Simulation)

Simply simulate the given problem using an efficient enough data structure. Here, I will introduce a linked list solution and why it looks like it would be quadratic or $NlogN$ but is actually $N$.

Store the sizes of the microorganisms in a linked list. Until the size of the linked list is $1$, iterate through the linked list and if the current element is larger than its neighbors, remove them from the list. Removal from a linked list if you know the position is $\mathcal{O}(1)$.

The key observation here is that for a pair of adjacent microorganisms, one must end up absorbing the other. What this guarantees is that the size of the list reduces by half each run.

If you've come this far you should be able to solve the problem with the conclusion that the time complexity is somewhere around $NlogN$. However, the true time complexity is lower than this.

Again, notice that the size of the list reduces by half each run. Since the time complexity of the run is proportional to the size of the list as we iterate through each remaining element, the time complexity would be $N + \frac{N}{2} + \frac{N}{4} + \dots$

Using the formula for infinite geometric series,

$$N + \frac{N}{2} + \frac{N}{4} + \dots = N\frac{1}{1-\frac{1}{2}} = 2N$$

Thus, the time complexity is bound by $2N$ and thus $\mathcal{O}(N)$.