# Classpad programs

## https://classpad.github.io

This repository is a compilation of classpad programs I used in year 12.

They are licensed under the gnu public license v3 (See `COPYING` for more information). Please read the license before modifying the files.

---
## How can I use this repository?
---

## User installation

### Option 1: Install eActivity.

In this directory there is a file named `spec_method_programs-(eActivity).xcp`. Connect your classpad to a computer and copy this eActivity file to the autoimport directory of the classpad. 

From here you can copy the programs to the `library` directory in the classpad using the variable manager (while the eActivity is opened), to use the programs outside of the eActivity, for example, in the `main` application.


### Option 2: Install individual programs
Go to the `binary/` directory. Located there are files with the `.XCP` extension. Connect your classpad to a computer and copy the programs files you want to the autoimport directory of the classpad.

See section 15-2 of the classpad manual for more information on transferring files.

---
## Using source code
---

The source is included in `source/`

Classpad programs, like all other data files, are encoded in the `.XCP` format, which is unfortunately a binary format. Some have decoded this format but I have no intention to do so. Therefore, the only option is to copy the raw text (Below the line `--- ONLY COPY BELOW THIS SECTION ---`), then in Classpad manager use `Paste Special` when in the program editor. 

Do not forget to copy/paste the arguments into the top bar, detailed in the `'Args` line.

Note that some editing may be requried. These `Manual replacements` are detailed at the header of each source file. For example, subscripts which do not copy over well.

The original source files (What I actually used in my WACE exams) are also included in the `original_source/` directory.

---
## Why the odd function names?
---
It's because as part of my workflow, I made extensive use of shift-keys. Because I had shift-keys assigned for every button, I just ended up using existing shift-keys and appending a number to the end. My workflow became `shift+key -> left arrow -> number -> right arrow`, which was only marginally slower. Unfortunately that means the programs are less readable. However **feel free to rename the programs in the variable manager** to whatever you want.

---
## Guide/Explanation of each program
---
## `cis0(power, C)`
[v1.0.0]

De Moivre root finder. Lists all possible roots of `z^power = C`, in both polar/rectangular form. Ensures the angles are within the definition of `arg(z)` (`-pi=<\theta=<pi`).

## `diff0(expression)`
[v1.0.0]

Analyzes an _expression_ (MUST BE IN TERMS OF `x`) and returns the critical points (maximum, minimum, inflection, undulation points) in a neat tabular form, along with the differentiatied functions and the global maximum/minimum.

* LMAX (Local maximum): `dy/dx = 0, d^2y/dx^2 < 0`
* LMIN (Local minimum): `dy/dx = 0, d^2y/dx^2 > 0`
* INFL (Inflection): `d^2y/dx^2 > 0, d^3y/dx^3 != 0`
* UNDULATN (Undulation): `d^2y/dx^2 = 0, d^3y/dx^3 = 0`

A point of undulation appears to be an inflection looking at the second derivative, but in reality is not. An example function is `x^4`, which has a point of undulation (and a minimum) at `(0,0)`

Please note that this program may struggle with periodic functions (`sin`, `cos`, `tan`, etc.), due to the `constn(n)` variable. It is up to you to manually evaluate the table for each value of `constn`. You can do this by taking the output and using `ans|{constn(0)=n1,constn(1)=n2,...}`.

Additionally, you need to enable `complex` mode when evaluating anything that can return complex numbers, or else it'll fail. For example, with the expression `ln(x)-x`. For methods students, ignore anything containing `i`.

## `impDiff0(equation)`
[v1.0.0]

Analyzes an _equation_ (MUST BE IN TERMS OF `y` AND `x`) and returns the differentiated function and points where `dy/dx=0` and `d^2y/dx^2=0`. Feel free to cancel the calculation in the middle if the second step takes to long (Finding solutions for `d^2y/dx^2=0` is more intensive).

Note that this does not evaluate the nature of the points. I'm leaving that up to you to do. I may add this feature in a future version.

## `ln0([x],[P(X=x)])`
[v1.0.0]

Creates a summary list for a discrete random variable

Requires _two column matrices_. The first one contains the values of `x`, the second the probabilities for each value of `x` [ `P(X=x)` ]. It returns the expected value, the expected value of the squares of x and the variance/standard deviation.

A warning is emitted if the sum of the probabilities is NOT 1.

You may ask, _"why did you go through the trouble of making this when there's literally an identical program in the `statistics` tab?"_. Firstly, switching from `main` wastes time. Yes, there is a `DispStat` function but I don't like how it displays more than we need. Also it's displaying approximate values, not exact. So the reason is basically because I don't like the workflow of `statistics` tab.

## `ln1(expression,a,b)` 
## or `ln1(expression,n,n)`
[v1.0.0]

Creates a summary list for a continuous random variable, similar to `ln0`.

Has two operating modes. **First** mode evaluates this summary list from the lower limit `a` to the upper limit `b` for an `expression` IN TERMS OF `x` (The probability density function/PDF). Returns expected value, variance/standard deviation, median (approximate), "median expression" (You can find the exact median by using `solve(0.5=<median expression>)`) and the CDF (as a complete piecewise function).

The **second** operating mode finds another limit given some known limit, `n`. It does this by ensuring the integral equals 1. It has no problems working with limits to infinity (like in PDFs which have an asymptote).

## `solve0([linear system])`
[v1.0.0]

Solves a linear system in matrix form. Matrix must be `m*(m+1)` (One wider than tall), as it contains the constant each row is equal to.

Solutions are returned as a row matrix, each element corresponding to the variable describing one column of the input

Returns echelon matrix and solution (as a column matrix)

## `solve1({y=f(t),x=g(t)})`
[v1.0.0]

**Important note!** This function doesn't always work. Sometimes it just wastes classpad time trying to find a solution. Never rely on this for an answer.

Attempts to find the equation `y=h(x)`. The input must be a list (use curly braces) which contains two functions, one equal to `x` and one equal to `y`, both in terms of `t`. It then returns two solutions as a list, both in the form `y=h(x)`. You must evaluate which of the two is correct (if any). The `t`-values substituted to calculate each solution are then printed.

## `θθ(p,n)`
[v1.0.0]

Multipurpose probability utility

* Outputs a table of conditions (n >= 30, np >= 10, n(1-p) >= 10) which need to be met for a sample size to be considered 'large enough' to approximate a normal distribution (CLT). 
    * 1st row is the condition
    * 2nd row states if the condition is met
    * 3rd row states is the value of the condition
    * 4th row the minimum value to satisfy the condition.
* Outputs the standard deviation (`SD(σ)`)
* Outputs a table of confidence intervals and their margin of error, `M_ERR`, at commonly-used confidence levels (90,95,99)
* Sets a series of variables to commonly-used constants. All of these variables are prefixed with `θ`. Best used with a shift-key for `θ` [ `SHIFT+)` ].
    * `θ90`,`θ95`,`θ99`: Z-scores for confidence intervals of 90,95 and 99
    * `θ36`: A matrix containing values for two-die (I know this is basic stuff, but sometimes I want to manually validate something just to be safe. Also dice questions come up all the time.)

## ~~`tan0(y=f(x),a,b)`~~
[v1.0.0]

~~Evaluates volumes of solids of revolution for a function `y=f(x)` (MUST include `y` and `x`). It will then prompt the user for which axis `a -> b` are located on. It returns a table containing volume rotated around x and y, and volume to an axis rotated about the other axis.~~

### **DO NOT USE** - use eActivity VSR tab instead.