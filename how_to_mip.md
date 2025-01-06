# How to MIP

What is **MIP**?

MIP is a simple python package that can be used in order to solve optimization problems.

To solve a problem you need to do a series of steps:

1. Create your model.
2. Define the decision variables.
3. Set the objective function.
4. Add constraints.
5. Solve the problem.

We now see how to tackle each part in detail.

### 1. Create your Model

In order to create your model, you need to call the `Model` constructor on the mip package.

```
model = mip.Model()
```

---

### 2. Define the Decision Variable

In order to define the decision variables, you need to use the `add_var` method.

Now let\'s take a look at different examples and situations.

1. Defining a simple list of variables

    ```
    x = [model.add_var(name = i, lb = 0) for i I]
    ```

    Here for every i in the list I we are assiging a variable, th `name` option gives us the ability to set the the name, `lb` sets the lower bound and you can also use other parametes like `ub` to set the upper bound.

    The result here is a list of variables with the initial values of 0 which can take fractional values.

---

2. One Step Forward

    Now let\'s imagine we want to create variables with the following definitions:

    - $x_{ij}$: units of oil of type $i \in I$ used for gasoline of type $j \in J$

    Now the code looks like this:

    ```
    x = {(i, j): model.add_var(name=`name`, lb=0) for i in I for j in J}
    ```

---

3. Integer Variables

    If you want your variables to take integer values, you can use the `var_type` parameter of the `add_var` method.

    ```
    x = {(i, j):model.add_var(name = 'name', var_type=INTEGER, lb=0) for i in I for j in J}
    ```

    There are two ways to use `INTERGE` as `var_type`:

    ```
    # Import it and use it directly like the example above

    from mip import INTEGER

    # Use it by dot notation

    var_type = mip.INTERGE
    ```

---

4. Binary Variables

    It\'s similar to defining integer variables however, instead of usign `INTEGER` as `var_type` we use `BINARY`.

    ```
     x = {(i, j):model.add_var(name = 'name', var_type=BINARY) for i in I for j in J}
    ```
