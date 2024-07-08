+++
title = 'Excel interpolation-lookup formula'
date = 2024-07-08T16:30:13-06:00
tags = ["excel"]
draft = false
+++

The three most used methods to look up data from tables or ranges in Excel are: `VLOOKUP`, `INDEX MATCH`, and since Excel 2021, `XLOOKUP`. While these methods are powerful, they share a common limitation: they only allow for exact matches, or the preceding or next value present in the table. But what if we need intermediate values? How can we perform both lookup and interpolation at the same time?

## How it works

The base of our formula will be the `FORECAST` or `FORECAST.LINEAR` function. This are Excel's built-in interpolation functions. They take three arguments: The data point for which you want to predict a value (in our case, the lookup value), the dependent array or range of data, and the independent array or range of data.

**Note:** According to Microsoft, the `FORECAST` function will eventually be deprecated. However, it is still available for backward compatibility[^1].

In our case, independent array (known_x’s) will consist of the smallest value and the next largest value for a given lookup value.

To obtain the previous value, `X0`, we will use `INDEX MATCH`, bout you can also use `XLOOKUP` (it might even be preferable if you’re sharing the file with other people, since its syntax is easier to understand). Check out [this blog post](https://www.ablebits.com/office-addins-blog/xlookup-vs-index-match-excel/) if you want to know more about the differences between the two methods.

To obtain the next largest value, we can use the OFFSET function, given that the lookup column is sorted. We just need to set the `height` parameter to 2.

## Formula

If you are using Excel 2019 or older, or you want to ensure compatibility with these versions, use this formula:

```c
=FORECAST(
  A1,
  OFFSET(INDEX(Table1[X],MATCH(A1,Table1[X],1)),,1,2),
  OFFSET(INDEX(Table1[X],MATCH(A1,Table1[X],1)),,,2)
)
```

If you are are using Excel 2021 or recent, I suggest this other version:

```c
=LET(
  X0,INDEX(Table1[X],MATCH(A1,Table1[X],1)),
  KnownX,OFFSET(X0,,,2),
  KnownY,OFFSET(X0,,1,2),
  FORECAST.LINEAR(A1,KnownY,KnownX)
)
```

The use of the `LET` function allows us to reuse the `X0` variable, which means that we only need to run `INDEX MATCH` once, increasing its performance. It also allows us to use local variables, which improve the readability of the formula, albeit making it slightly longer.

## References

[^1]: https://support.microsoft.com/en-us/office/forecast-and-forecast-linear-functions-50ca49c9-7b40-4892-94e4-7ad38bbeda99
