[DecisionToolkit]: https://crates.io/crates/dsntk

# Introduction to decision tables

## What is a decision table?

### From "Decision Tables: Theory and Practice" (1971)

> Tables are a familiar part of everyone's life. From mathematical tables to the box score of yesterday's
> baseball game, they provide us with an orderly presentation of data. While such tables often assist us
> in making a decision, they are not decision tables. A decision table is a special form of table that
> codifies a set of decision rules based on a specific, clearly identified set of conditions and resulting
> actions. While the history of tables in general can be told in terms of centuries,
> decision tables are fairly recent phenomenon. 

_Pollack, S.L., Hicks, H.T.Jr., Harrison, W.J.: "Decision Tables: Theory and Practice", Wiley-Interscience 1971_

### Wikipedia (2024)

> [Decision table](https://en.wikipedia.org/wiki/Decision_table)
> 
> Decision tables are a concise visual representation for specifying which actions to perform depending on given conditions.
> They are algorithms whose output is a set of actions. The information expressed in decision tables could also be represented
> as decision trees or in a programming language as a series of if-then-else and switch-case statements.

### DMN (2015-present)

[Decision Model and Notation specification v1.5](https://www.omg.org/spec/DMN)

> A decision table is a tabular representation of a set of related input and output expressions, organized into rules
> indicating which output entry applies to a specific set of input entries. The decision table contains all (and only) the
> inputs required to determine the output. Moreover, a complete table contains all possible combinations of input
> values (all the rules). Decision tables and decision table hierarchies have a proven track record in decision
> logic representation. It is one of the purposes of **DMN** to standardize different forms and types of decision tables.

### ChatGPT (2024)

> A decision table is a structured representation of decision logic that helps in organizing complex decision-making processes.
> It's a tool used in systems analysis and software engineering for specifying, organizing, and modeling complex logic.
> Decision tables are particularly useful when dealing with multiple conditions and actions, making them popular in fields
> like business analysis, software development, and operations research.
>
> In a decision table, each column represents a condition or input variable, and each row represents a combination of conditions.
> The intersection of a row and column represents a specific scenario or combination of conditions.
> The table then specifies the actions or outcomes associated with each combination of conditions.
>
> Decision tables are often used in conjunction with decision trees and other decision-making tools to model and analyze
> complex decision processes. They provide a clear and concise way to document decision logic, making it easier to understand,
> validate, and modify decision-making rules. Additionally, decision tables can aid in identifying redundancies,
> inconsistencies, or gaps in decision logic.

### Functional programming

> Decision table is a **pure function**.
> 
> As a **pure function**, decision table has the following characteristics:
> - **Determinism**: Decision table always produces the same output for a given set of inputs, regardless of the external
>   conditions or the state of the program. In other words, the output of decision table is solely determined by its
>   input parameters, and it does not rely on any external state or side effects.
> - **No side effects**: Decision table does not modify any state outside its scope, such as global variables,
>   mutable data structures, or input/output streams. It does not perform any actions that could have observable
>   effects beyond returning its output value.
>
> Decision tables are highly desirable in functional programming paradigms because they offer several advantages:
> - **Referential transparency**: Since decision tables always produce the same output for the same input,
>   they can be replaced with their return values without changing the behavior of the program.
>   This property simplifies reasoning about code and facilitates optimization.
> - **Concurrency and parallelism**: Decision tables are inherently thread-safe because they do not rely on shared mutable state.
>   This makes it easier to write concurrent and parallel programs without worrying about race conditions or synchronization issues.
> - **Testability**: Decision tables are easy to test, because their behavior is predictable and isolated.
>   Unit tests can be written to verify the output of a decision table based on different input values,
>   without needing complex setup or mocking.

## Examples

### Truth table

The [truth table](https://en.wikipedia.org/wiki/Truth_table) can be perceived as an ancestor of decision table,
like logical AND shown below:

![logical-and](./assets/logical-and.png)

### Early decision tables (1957-2015)

![early-decision-table-structure](./assets/early-decision-table-structure.png)

Example in Unicode:

![early-decision-table](./assets/early-decision-table.png)

### Decision tables standarized in DMN (2015-present)

> ### Rules as columns

![rules-as-columns](./assets/rules-as-columns.png)

Example in Unicode:

![rules-as-columns](./assets/rules-as-columns-uni.png)

```text
┌──────────┐
│ Discount │
├──────────┴───┬───────────────────────╥─────────────────┬───────────┐
│ Customer     │ "Business", "Private" ║    "Business"   │ "Private" │
├──────────────┼───────────────────────╫────────┬────────┼───────────┤
│ Order size   │       <10, >=10       ║   <10  │  >=10  │     -     │
╞══════════════╪═══════════════════════╬════════╪════════╪═══════════╡
│ Discount     │   0.10, 0.15, 0.05    ║  0.10  │  0.15  │   0.05    │
╞══════════════╪═══════════════════════╬════════╪════════╪═══════════╡
│ Description  │                       ║ Desc 1 │ Desc 2 │   Desc 3  │
├──────────────┼───────────────────────╫────────┼────────┼───────────┤
│ Reference    │                       ║ Ref 4  │ Ref 4  │   Ref 5   │
├──────────────┼───────────────────────╫────────┼────────┼───────────┤
│      U       │                       ║   1    │   2    │     3     │
└──────────────┴───────────────────────╨────────┴────────┴───────────┘
```

Example in Markdown:

> #### Discount

| U           |                       |       |     1      |     2      |     3     |
|:------------|:---------------------:|:-----:|:----------:|:----------:|:---------:|
| Customer    | "Business", "Private" | `In`  | "Business" | "Business" | "Private" |
| Order size  |       <10, >=10       | `In`  |    <10     |    >=10    |     -     |
| Discount    |   0.10, 0.15, 0.05    | `Out` |    0.10    |    0.15    |   0.05    |
| Description |                       | `Ann` |   Desc 1   |   Desc 2   |  Desc 3   |
| Reference   |                       | `Ann` |   Ref 4    |   Ref 4    |   Ref 5   |

> ### Rules as rows

![rules-as-rows](./assets/rules-as-rows.png)

Example in Unicode:

![rules-as-rows](./assets/rules-as-rows-uni.png)

```text
┌───────────────┐
│   Discount    │
├───┬───────────┴───────────┬────────────╥──────────────────╥─────────────┬───────────┐
│ U │       Customer        │ Order size ║    Discount      ║ Description │ Reference │
│   ├───────────────────────┼────────────╫──────────────────╫─────────────┼───────────┤
│   │ "Business", "Private" │ <10, >=10  ║ 0.10, 0.15, 0.05 ║             │           │
╞═══╪═══════════════════════╪════════════╬══════════════════╬═════════════╪═══════════╡
│ 1 │      "Business"       │     <10    ║       0.10       ║    Desc 1   │   Ref 4   │
├───┼───────────────────────┼────────────╫──────────────────╫─────────────┼───────────┤
│ 2 │      "Business"       │    >=10    ║       0.15       ║    Desc 1   │   Ref 4   │
├───┼───────────────────────┼────────────╫──────────────────╫─────────────┼───────────┤
│ 3 │      "Private"        │     -      ║       0.05       ║    Desc 1   │   Ref 5   │
└───┴───────────────────────┴────────────╨──────────────────╨─────────────┴───────────┘
```

Example in Markdown:

> #### Discount

| U |       Customer        | Order size |     Discount     | Description | Reference |
|:--|:---------------------:|:----------:|:----------------:|:-----------:|:---------:|
|   | "Business", "Private" | <10, >=10  | 0.10, 0.15, 0.05 |             |           |
|   |         `In`          |    `In`    |      `Out`       |    `Ann`    |   `Ann`   |
| 1 |      "Business"       |    <10     |       0.10       |   Desc 1    |   Ref 4   |
| 2 |      "Business"       |    >=10    |       0.15       |   Desc 2    |   Ref 4   |
| 3 |       "Private"       |     -      |       0.05       |   Desc 3    |   Ref 5   |

## Does it work? Yes!

First, clone this repository and install [DecisionToolkit]: 

```shell
$ cargo install dsntk
```

Change the current directory to `assets` and run: 

```shell
$ cd assets
$ dsntk edt input.ctx rules-as-rows.uni 
$ dsntk edt input.ctx rules-as-columns.uni
```

## Exercise

### Question:

> How to convert this truth table into decision table?

![truth-table](./assets/logical-and.png)

### Answer:

> Add the hit policy and rule numbers before the first column.

![decision-table](./exercise/table.png)

```shell
$ cd exercise
$ dsntk edt input.ctx table.uni
```

Output:

```js
true
```

See [exercise](./exercise) directory for details.

---

All source files are in [assets](./assets) and [exercise](./exercise) directories. 
