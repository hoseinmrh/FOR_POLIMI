# How to Model

Here we will take a look at different case of modeling for the FOR course. I believe this is the best note that can be used during the exam (:

1. [Simple LP Modeling](#1-Simple-LP-Modeling)
2. [Simple ILP Modeling](#2-Simple-ILP-Modeling)
3. [ILP and Binary Variables Modeling](#3-ILP-Binary-Variables-Modeling)
4. [Big M Modeling](#4-Big-M-Modeling)
5. [Somehow I Model](#5-Somehow-I-Model)

### 1. Simple LP Modeling

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
-   $J$: Set of Gasolines, $J \in \{A,B\}$

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

-   $\sum_{j \in J} x_{ij} \le a_i \ \ \ i \in I \ \ \ \text{(Availability)}$
-   $\sum_{i \in I} x_{ij} = y_j \ \ \ j \in J \ \ \ (Conservation)$
-   $x_{ij} \ge y_j * qMin_{ij} \ \ \ j \in J \ \ i \in I \ \ \ (Minimum \ Quanitity)$
-   $x_{ij} \le y_j * qMax_{ij} \ \ \ j \in J \ \ i \in I \ \ \ (Maximum \ Quanitity)$
-   $x_{ij} \ge 0$
-   $y_{ij} \ge 0$

For better understanding check exercise 1.2 of the course.

---

### 2. Simple ILP Modeling

A manager needs to plan the shoe production for a single day. Five models of shoes can be produced, utilizing the labor of three workers. The time required by each worker to manufacture a shoe of each model is shown in the following table (hours/unit):

| Model/Worker | Worker 1 | Worker 2 | Worker 3 |
| ------------ | -------- | -------- | -------- |
| 1            | 1.5      | 3.5      | 4        |
| 2            | 1.8      | 2        | 3        |
| 3            | 2        | 1        | 2.5      |
| 4            | 2.5      | 1.5      | 3.5      |
| 5            | 3.5      | 3.5      | 4.2      |

Due to production constraints imposed by the unions, each worker must work no less than 8 hours a day, but no more than 10.

The next table shows, for each model of shoes, the selling price and an estimation of the maximal market demand:

| Model | Price (€) | Demand (units) |
| ----- | --------- | -------------- |
| 1     | 56        | 4              |
| 2     | 86        | 3              |
| 3     | 45        | 3              |
| 4     | 42        | 5              |
| 5     | 65        | 8              |

**Problem Statement:**

Formulate an Integer Linear Programming (ILP) model to maximize the revenue, subject to the following constraints:

1. Each worker must work between 8 and 10 hours.
2. The production of each model must not exceed its market demand.

---

**Sets:**

-   $I$: Set of workers
-   $J$: Set of models of electronic devices

**Parameters:**

-   $t_{ij}$: Manufacturing time for worker $i \in I$ and model of electronic device $j \in J$
-   $p_j$: Selling price for model of electronic device $j \in J$
-   $q_j$: Demand for model of electronic device $j \in J$
-   $T_{\text{min}}$: Minimum amount of working hours
-   $T_{\text{max}}$: Maximum amount of working hours

**Decision Variables:**

-   $x_{ij}$: Number of electronic devices of model $j$ manufactured by worker $i$, $i \in I, j \in J$

**Objective Function:**

$$
\max \sum_{j \in J} p_j \sum_{i \in I} x_{ij} \quad \text{(revenue)}
$$

**Constraints:**

-   $\sum_{j \in J} t_{ij} x_{ij} \geq T_{\text{min}}, \quad \forall i \in I \quad \text{(minimum working hours)}$

-   $\sum_{j \in J} t_{ij} x_{ij} \leq T_{\text{max}}, \quad \forall i \in I \quad \text{(maximum working hours)}$

-   $\sum_{i \in I} x_{ij} \leq q_j, \quad \forall j \in J \quad \text{(demand)}$

-   $x_{ij} \in \mathbb{Z}^+, \quad \forall i \in I, j \in J \quad \text{(non-negativity and integrality)}$

---

### 3. ILP Binary Variables Modeling

A distribution company has to supply a single type of good to $n$ clients. Let $d_j$ denote the
demand of client $j$, where $j \in J = \{1,2,...,n\}$. The goods must be stocked in warehouses before
being delivered to the clients. The warehouses can be located in $m$ candidate sites. Let $f_i$ denote the cost for opening a warehouse at the candidate site $i \in I = \{1,2,...,m\}$, and $b_i$ denote its maximum capacity. Let $c_{ij}$ be the unit transportation cost from warehouse $i$ to client
$j$, and $q_{ij}$ be the maximum quantity to be transported from warehouse $i$ to client $j$.

Give an integer linear programming formulation to decide where to locate the warehouses
and how to satisfy the client demands so as to minimize the total costs, i.e., the total opening costs plus the total transportation costs.

**Sets and Parameters:**

Sets and parameters are well described in the text.

**Decision Variables:**

-   $x_{ij}$: Amount of goods to be transported from the warehouse in candidate site $i \in I$ to client $j \in J$
-   $y_i$: Equals 1 if the warehouse in candidate site $i \in I$ is opened, and 0 otherwise.

**Objective Function:**

$$
\min \sum_{i \in I,j \in J} c_{ij}x_{ij} + \sum_{i} f_i y_i
$$

**Constraints:**

-   $\sum_{i \in I} x_{ij} \ge d_j \ \ \forall j \in J \quad \text{(demand)}$
-   $\sum_{j \in J} x_{ij} \le b_i \ \ \forall i \in I \quad \text{(availability)}$
-   $0 \le x_{ij} \le y_iq_{ij} \ \ \forall i \in I \ \ j \in J \quad \text{(bounds and link capacity)}$
-   $y_i \in \{0,1\} \quad \text{(binary variable)}$

Please note that when you are using binary variables, somewhere you should bound it with other variables like the 3rd constraint here.

For better understanding checkout the exercise 1.7

---

### 4. Big M Modeling

A company **A**, which produces one type of high-precision measuring instrument, has to plan the production for the next **3 months**.

Each month, **A** can produce at most **110 units**, at a unit cost of **300 Euro**. Moreover, each month, up to **60 additional units** can be produced by another company **B** at a unit cost of **330 Euro**.

Unsold units can be stored, and the inventory cost is **10 Euro per unit** of the product, per month.

Sales forecasts indicate a demand of **100, 130, and 150 units** of the product for the next **3 months**.

Give a mixed-integer linear programming formulation for the variant of the problem where production lots have a minimum size. In particular, if any strictly positive quantity is produced in a given month, this quantity cannot be smaller than 15 units.

**Sets:**

-   $T = \{1, 2, 3\}$: Set of months.

**Parameters:**

-   $b$: Production capacity of $A$.
-   $b'$: Production capacity of $B$.
-   $c$: Unit production cost for $A$.
-   $c'$: Unit production cost for $B$.
-   $m$: Inventory cost per unit and per month.
-   $d_t$: Sales forecasts for month $t$, where $t \in T$.

-   $l$: Minimum lot size = 15
-   $M$: Some large value

**Variables:**

-   $x_t$: Units produced by $A$ in month $t$, for $t \in T$.
-   $x'_t$: Units bought from $B$ in month $t$, for $t \in T$.
-   $z_t$: Units in inventory at the end of month $t$, for $t \in T \cup \{0\}$.
-   $y_t$: 1 if production is active at month $t$, 0 otherwise, for $t \in T$

**Model:**

$$
\min \quad \sum_{t \in T} \big( c x_t + c' x'_t + m z_t \big) \quad \text{(cost)}
$$

**Constraints:**

-   $x_t \leq b \quad \text{for } t \in T \quad \text{(capacity of A)}$

-   $x'_t \leq b' \quad \text{for } t \in T \quad \text{(capacity of B)}$

-   $z_{t-1} + x_t + x'_t \geq d_t \quad \text{for } t \in T \quad \text{(demand)}$

-   $z_{t-1} + x_t + x'_t - d_t = z_t \quad \text{for } t \in T \quad \text{(inventory balance)}$

-   $z_0 = 0 \quad \text{(starting condition)}$

-   $x_t \ge ly_t \quad \text{(minumum lot size)}$

-   $x_t \le My_t$

-   $x_t, x'\_t, z_t \geq 0 \quad \text{for } t \in T \quad \text{(nonnegative variables)}$

M is a large enough value, such that constraint
$x_t \le My_t$ is redundant when $y_t = 1$

For better understanding checkout exercise 1.4.

---

### 5. Somehow I Model

This example shows how to do a simple trick in order to have the best modeling. Nameing is a reference to Michael Scott's book `Somehow I manage`.

An ICT services company has estimated the following demand for maintenance and consultancy for the next 5 months:

| Month          | 1    | 2    | 3    | 4    | 5     |
| -------------- | ---- | ---- | ---- | ---- | ----- |
| Demand (hours) | 6000 | 7000 | 8000 | 9500 | 11000 |

At the beginning of the planning period, 50 technicians are available. Each technician works at most 160 hours per month. To satisfy the demand, new technicians must be hired and trained. During the training period, which lasts one month, an expert technician must coach the newly hired one for 50 hours.

Expert technicians are paid 2000 Euros per month, while the newly hired ones are paid 1000 Euros during the training month. We suppose that, at the end of each month, 5% of the expert technicians leave the company to join competitors.

Give a mathematical programming formulation for the problem of minimizing the total costs.

Here is the updated Markdown with the requested formatting applied to the entire content, including the model:

**Sets:**

-   $I = \{1, \dots, 5\}$: months

**Parameters:**

-   $d_i$: demand for month $i$, $i \in I$

**Decision Variables:**

-   $x_i$: number of expert technicians available in month $i$, $i \in I$
-   $y_i$: number of technicians training during month $i$, $i \in I$

**Objective Function:**

$$
\min 2000 \sum_{i \in I} x_i + 1000 \sum_{i \in I} y_i
$$

**Constraints:**

-   $160x_i - 50y_i \ge d_i \quad \forall i \in I \quad \text{(time demand)}$

-   $\lfloor 0.95x_i \rfloor + y_i = x_{i+1} \quad \forall i \in I \quad \text{(number of experts)}$

-   $x_1 = 50 \quad \text{(initial experts)}$

-   $x_i, y_i \in \mathbb{Z}^+ \quad \forall i \in I \quad \text{(nonnegative integer variables)}$

The second constraint is clearly not linear. So what should we do?

By dropping the $\lfloor \cdot \rfloor$ operator, we obtain the constraint:

$0.95x_i + y_i = x_{i+1}, \quad i \in I$

which is not correct since, due to the integrality requirements on the variables, it forces $x_i$ to be a multiple of 100 (such that $0.95x_i$ will always be an integer value).

Constraint (number) can be formulated in a linear way by introducing, for each $i \in I$, an auxiliary integer variable $z_i$ that represents $\lfloor 0.95x_i \rfloor$, and by adding the auxiliary constraints:

-   $z_i + y_i = x_{i+1}, \quad i \in I$

-   $100z_i \leq 95x_i \leq 100z_i + 100, \quad i \in I$

-   $z_i \in \mathbb{Z}^+, \quad i \in I \quad \text{(nonnegative integer variables)}$

Then we clearly have $z_i = \lfloor 0.95x_i \rfloor$.

## For better understanding checkout exercise 1.6

Some notes:

1. The easiest part is to determine the objectove funtion. What do you need for that? Variables! Exactly. So, how to define variables?
2. Take a look at what is the cost, revenue, time or anything that you want to minimize and maximize. If it is $c_{ij}$ the cost for some $ij$, then the decision variable is also $sth_{ij}$.
3. If you sense that you need to apply some selection, then you need to use **Binary** variables.
4. Be aware of bouding **Binary** and **Integer** variables if it is needed. Likek the example 3.
