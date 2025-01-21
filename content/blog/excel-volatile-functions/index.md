+++
title = 'Excel volatile functions'
date = 2025-01-20T18:24:28-06:00
tags = ["excel"]
draft = false
+++

Since I worte my [previous post](/excel-interpolation-lookup-formula/), I learned about the concept of volatile functions in Excel, which has made me change many of the formulas that I use everyday, inluding the one discussed in that post.

:memo: **Note:** The previous post has now been updated and the formula that I recommend there no longer uses volatile functions.
{ .note }

Cells that contain volatile functions get recalculated every time that Excel recalculates (basically, every time you hit Enter). Therefore, they should be avoided when possible.

Some functions are obvioulsy volatile, like `NOW` and `RAND`, but other frequently used ones, like `OFFSET`, are too. Here is a list of all the volatile functions in Excel:[^1]

-   `NOW`
-   `TODAY`
-   `RAND` and `RANDBETWEEN`
-   `OFFSET`
-   `INDIRECT`
-   `INFO` (depending on its arguments)
-   `CELL` (depending on its arguments)
-   `SUMIF` (depending on its arguments)

It's fine to use these functions here and there, but if you plan to use them in table columns, where the formula will be calculated in hundreds or thousands of rows, then you should look for alternatives, as using volatile functions will severly slow down your workbook.

## References

[^1]: https://learn.microsoft.com/en-us/office/client-developer/excel/excel-recalculation#volatile-and-non-volatile-functions
