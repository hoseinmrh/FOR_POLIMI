# How to Model

Here we will take a look at different case of modeling for the FOR course. I believe this is the best note that can be used during the exam (:

1. [Simple LP Modeling](#1-Simple-LP-Model)
2. [Simple ILP Modeling](#2-Simple-ILP-Model)
3. [ILP and Binary Variables Modeling](#3-ILP-Binary-Variables-Model)
4. [Big M Modeling](#4-Big-M-Model)
5. [Somehow I Model](#5-Somehow-I-Model)

### 1. Simple LP Model

A refinery produces two types of gasoline by mixing three basic oils according to the following gasoline mixture rules:

| Gasoline   | Oil 1 | Oil 2 | Oil 3 | Revenue (€/barrel) |
| ---------- | ----- | ----- | ----- | ------------------ |
| Gasoline A | ≤ 30% | ≥ 40% | -     | 5.5                |
| Gasoline B | ≤ 50% | ≥ 10% | -     | 4.5                |

The last column of the previous table indicates the profit (€/barrel). The availability of each type of oil (in barrels) and its cost (€/barrel) are as follows:

| Oil | Availability (barrels) | Cost (€/barrel) |
| --- | ---------------------- | --------------- |
| 1   | 3000                   | 3               |
| 2   | 2000                   | 6               |
| 3   | 4000                   | 4               |

**Problem Statement:**

Formulate a Linear Programming problem to determine a mixture that maximizes the profit (difference between revenues and costs).

**Solution:**

**Sets:**

-   $I$: Set of Oils, $I \in \{1,2,3\}$
-   $J&: Set of Gasolines, $J \in \{A,B\}$

**Parameters:**

-   $c_i$: Cost of Oil $i \in I$
-   $r_j$: Revenue of Gasoline $j \in J$
-   $a_i$: Availability of Oil $i \in I$
-   $qMax_{ij}$: Maximum percentage of Gasoline $j$ which is of Oil $i$
-   $qMin_{ij}$: Minimum percentage of Gasoline $j$ which is of Oil $i$

P.S: For maximum and minimum, here I take the general case. For this csae you only need to specify it for the stated ones.

**Decision Variables:**

-   $x_{ij}$: Barrels of Oil $i$ which is used to make Gasoline $j$
-   $y_{j}$: Barrels of Gasoline $j$ to make

**Objective Function:**

$$
\max \sum_{j \in J} r_j yj - \sum_{i \in I, j \in J} c_i x_{ij}
$$

**Constraints:**

-   $\sum_{j \in J} x_{ij} \le a_i \ \ \ i \in I \ \ \ (Availability)$
-   $\sum_{i \in I} x_{ij} = y_j \ \ \ j \in J \ \ \ (Conservation)$
-   $x_{ij} \ge y_j * qMin_{ij} \ \ \ j \in J \ \ i \in I \ \ \ (Minimum \ Quanitity)$
-   $x_{ij} \le y_j * qMax_{ij} \ \ \ j \in J \ \ i \in I \ \ \ (Maximum \ Quanitity)$
-   $x_{ij} \ge 0$
-   $y_{ij} \ge 0$
