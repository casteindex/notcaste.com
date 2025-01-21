+++
title = 'Excel interpolation-lookup formula'
date = 2024-07-08T16:30:13-06:00
tags = ["excel"]
draft = false
+++

The three most used methods to look up data from tables or ranges in Excel are: `VLOOKUP`, `INDEX MATCH`, and since Excel 2021, `XLOOKUP`. While these functions are super useful, they share a common limitation: they only allow for exact matches, or the preceding or next value in the table. But what if we need intermediate values? How can we perform both lookup and interpolation at the same time?

Say you have the following table:

| A   | B   |
| --- | --- |
| 1   | 10  |
| 2   | 20  |
| 3   | 30  |

With the lookup methods mentioned above, if your lookup value is `2.333`, you could get `20` as a result, or `30`, or an error. But what if you want to take the two neighboring numbers of lookup value (`2` and `3`) and their respective Y-values (`20` and `30`) to make an interpolation and get `23.33` as a result? Well, here's a very neat way to do this with just three Excel functions.

## The formula

For maximum compatibility:

```s
=FORECAST.LINEAR(
    C1,
    INDEX(B:B, MATCH(C1, A:A, 1) + {0, 1}),
    INDEX(A:A, MATCH(C1, A:A, 1) + {0, 1})
)
```

To avoid reduntant calculations, you can use this other version that uses `LET` (note that this will only work with Excel 2021 or newer versions):

```s
=LET(
    rows, MATCH(C1, A:A, 1) + {0, 1},
    x_values, INDEX(A:A, rows),
    y_values, INDEX(B:B, rows),
    FORECAST.LINEAR(C1, y_values, x_values)
)
```

## How it works

First, we locate the position of the largest value that is less than or equal to lookup value with this: `MATCH(C1, A:A, 1)`.

Now comes the clever part. Since `INDEX` can return arrays, we can use `+ {0, 1}` to return an array of just two numbers, the largest value before the lookup value and the smallest number after the lookup value. We do that for the `known_x's` and `known_y's` that the `FORECAST.LINEAR` function requires.
