Activity 3
================
Solution

Today you will be creating and manipulating vectors, lists, and data
frames to uncover a top secret message.

As you work through this document with your Team members, remember to:

-   Ask questions
-   Google is your friend! If an error is confusing, copy it into Google
    and see what other people are saying. If you don’t know how to do
    something, search for it.
-   Just because there is no error message doesn’t mean everything went
    smoothly. Use the console to check each step and make sure you have
    accomplished what you wanted to accomplish.

Do not edit this first R code chunk. This will allow you to knit your
document and view errors within the knitted report.

### Setup

Each of the following R chunks will cause an error and/or do the desired
task incorrectly. Find the mistake, and correct it to complete the
intended action.

Create three vectors that contain: 1) the lower case letters, 2) the
lower case letters, and 3) some punctuation marks.

``` r
lower_case <- c("a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k", "l", "m", "n", "o", "p", "q", "r", "s", "t", "u", "v", "w", "x", "y", "z")

upper_case <- c("A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M", "N", "O", "P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z")

punctuation <- c(".", ",", "!", "?", "'", "\"", "(", ")", " ", "-", ";", ":")
```

Comment on what you noticed about the errors and how you used this
information to correct the issues.

**First Message**:
`Error: unexpected string constant in "upper_case <- c("A", "B", "C", "D", "E", "F", "G", "H" "I""`

**Comment**: The “unexpected string constant” statement is somewhat
confusing, but this usually means that there is a missing special
character. Looking at the end of the code snippet, you can see that
there is a missing comma between `"H"` and `"I"`. Looking in the code
above, `"I"` is underlined with a red-squiggle line indicating this is
around where R encountered the error. Finally, hovering your mouse
cursor over the red “x” on the left-hand column suggests that `"I"` is
unexpected.

**Second Message**:
`Error: unexpected string constant in "punctuation <- c(".", ",", "!", "?", "'", """, ""`

**Comment**: Again, “unexpected string constant” is not very clear.
Looking at the code snippet provided in the message is also not very
helpful so we can got to the code above and start look at the first
red-squiggle line. This occurs under the left-parentheses after `c`, but
we know that this should be here so we move onto the next red-squiggle
line. The next one occurs under `", "` near the middle of the line and
we see that R is trying to pair up quotations: the first two are one
pair, then `", "` are the next pair. We however want the second
quotation mark to be a string so we need to indicate this to R by
“escaping” it with a backslash: `\`. We will talk more about escaping
special characters later in this course, but after we update `"""` to be
`"\""` we see that the other red-squiggle lines go away.

Make one long vector containing all the symbols.

``` r
my_symbols <- c(lower_case, upper_case, punctuation)
```

Comment on what you noticed about the errors and how you used this
information to correct the issues.

**First Message**:
`number of rows of result is not a multiple of vector length (arg 3)`

**Comment**: This code ran, but we are getting a warning that is saying
that the lengths of each of these vectors is not the same and that the
third argument (i.e., `punctuation`) is the culprit. Looking at the help
documentation for `cbind` (by typing `?cbind` in the **Console**), we
see that this function takes multiple vectors and combines them to be
different columns. If we look in the **Environment** pane, we can see
that `my_symbols` has rows 1 through 26 and columns 1 through 3 (so it
is a matrix - type `class(my_symbols)` in the **Console** to verify). We
wanted a vector, not a matrix so `cbind` is not the right function to
use here. To make a vector in R, we use the `c` function (i.e., “combine
values into a vector or list).

Turn the `my_symbols` vector into a data frame, with the variable name
“Symbol”.

``` r
my_symbols <- data.frame(my_symbols)
names(my_symbols) <- "Symbol"
```

Comment on what you noticed about the errors and how you used this
information to correct the issues.

**First Message**:
`Error in dataframe(my_symbols) : could not find function "dataframe"`

**Comment**: This message is pretty clear - `dataframe` is not a
function. We need to use `data.frame`.

**Second Message**: `Error: object 'Symbol' not found`

**Comment**: We have not assigned anything to `Symbol` so R does not
know what to do here. We need to provide quotations around `Symbol` to
let R know we are providing a string name. I would also recommend
changing the `=` to an assignment operator `<-` since we are not
specifying an argument within a function.

Find the total number of symbols we have in our data frame.

``` r
len <- nrow(my_symbols)
```

Comment on what you noticed about the errors and how you used this
information to correct the issues.

**No messages!** Except this does not give us the expected result.
Looking at `my_symbols` in the **Environment** pane, we can see that
there are 64 observations, but `len` is only saying that there is 1. The
`length()` function works for vectors, but `my_symbols` is currently a
`data.frame` (we changed this above). To find the number of symbols, we
need to count the number of rows. The function for this is `nrow`

5.  Create a new variable in your dataframe that assigns a number to
    each symbol.

``` r
my_symbols$Num <- 1:len
```

Comment on what you noticed about the errors and how you used this
information to correct the issues.

**First Message**:
`Error: unexpected input in "my_symbols%Num <- 1:len"`

**Comment**: Using the red-squiggle line method, we can see that the
issue is with `%`. To extract column information from or create a new
column in a `data.frame`, we use the `$` operator.

![](README-img/noun_pause.png) **Planned Pause Point**: If things made
sense, feel free to continue on while you wait. Otherwise, contact your
instructor to have them verify your work.

### Decoding the secret message.

This chunk will load up the encoded secret message data and assign it as
a vector. There are no errors here.

``` r
# Read in full csv file
top_secret <- readr::read_csv("data/secret_code.csv", col_names = FALSE)
```

    ## 
    ## -- Column specification --------------------------------------------------------
    ## cols(
    ##   X1 = col_double()
    ## )

``` r
# Pick off only the column X1
top_secret <- top_secret$X1
```

By altering this top secret set of numbers, you will be able to create a
message. Write your own code to complete the steps below.

1.  Add 14 to every number.
2.  Multiply every number by 18, then subtract 257.
3.  Exponentiate every number. (That is, do e ^ \[each number\]. You may
    need to Google how to this!)
4.  Square every number.

``` r
# Step 1
top_secret <- top_secret + 14

# Step 2
top_secret <- top_secret * 18 - 257

# Step 3
top_secret <- exp(top_secret)

# Step 4
top_secret <- top_secret ^ 2
```

**Note** that I am overwriting `top_secret` each time. There are pros
(cleaner) and cons (harder to debug) with this method.

**HQ UPDATE:** Headquarters has informed you that at this stage of
decoding, there should be 496 numbers in the secret message that are
below 17.

``` r
# HQ Check
sum(top_secret < 17)
```

    ## [1] 497

**Note** that it seems there might be a rounding issue - I got 497 not
496.

5.  Turn your vector of numbers into a matrix with 5 columns.
6.  Separately from your top secret numbers, create a vector of all the
    even numbers between 1 and 502. Name it “`evens`”. That is, `evens`
    should be an R object that contain the values 2, 4, 6, 8, …, 502.
7.  Subtract the “evens” vector from the first column of your secret
    message matrix.
8.  Subtract 100 from all numbers 18-24th rows of the 3rd column.
9.  Multiply all numbers in the 4th and 5th column by 2.
10. Turn your matrix back into a vector.

``` r
# Step 5
top_secret <- matrix(top_secret, ncol = 5)

# Step 6
evens <- seq(from = 2, to = 502, by = 2)

# Step 7
top_secret[,1] <- top_secret[,1] - evens

# Step 8
top_secret[18:24,3] <- top_secret[18:24,3] - 100

# Step 9
top_secret[,4:5] <- top_secret[,4:5] * 2

# Step 10
top_secret <- c(top_secret)
```

**HQ UPDATE:** Headquarters has informed you that at this stage of
decoding, all numbers in indices 500 and beyond are below 100.

``` r
# HQ Check

# Number of indicies
length(500:length(top_secret))
```

    ## [1] 756

``` r
# Number of values below 100
sum(top_secret[500:length(top_secret)] < 100)
```

    ## [1] 756

11. Take the square root of all numbers in indices 38 to 465.
12. Round all numbers to the nearest whole number.
13. Replace all instances of the number 39 with 20.

``` r
# Step 11
top_secret[38:465] <- sqrt(top_secret[38:465])

# Step 12
top_secret <- round(top_secret)

# Step 13
top_secret[top_secret == 39] <- 20
```

**HQ UPDATE:** Headquarters has informed you that your final message
should have 421 even numbers.

``` r
# HQ Check

# "top_secret mod 2" checks returns the remainder of dividing a number by 2
# if this returns a 0, then the number is even
sum( (top_secret %% 2) == 0 )
```

    ## [1] 421

![](README-img/noun_pause.png) **Planned Pause Point**: If things made
sense, feel free to continue on while you wait. Otherwise, contact your
instructor to have them verify your work.

## The secret message!

Use your final vector of numbers as indices for `my_symbols` to discover
the final message, by running the following code:

``` r
stringr::str_c(my_symbols$Symbol[top_secret], collapse = "")
```

    ## [1] "Oh yeah In France a skinny man died of a big disease with a little name By chance his girlfriend came across a needle and soon she did the same At home there are seventeen-year-old boys and their idea of fun Is being in a gang called The Disciples, high on crack, totin' a machine gun Time Time  Hurricane Annie ripped the ceiling off a church and killed everyone inside You turn on the telly and every other story is tellin' you somebody died Sister killed her baby 'cause she couldn't afford to feed it And we're sending people to the moon September my cousin tried reefer for the very first time Now he's doing horse; it's June Time Time  It's silly, no? When a rocket ship explodes And everybody still wants to fly Some say a man ain't happy Unless a man truly dies Oh, why? Time Time  Baby make a speech, star wars fly Neighbors just shine it on But if a night falls and a bomb falls Will anybody see the dawn Time Time  Is it silly, no? When a rocket blows up And everybody still wants to fly Some say man ain't happy, truly Until a man truly dies Oh, why? Oh, why? Sign o' the Times Time Time  Sign o' the times mess with your mind Hurry before it's too late Let's fall in love, get married, have a baby We'll call him Nate, if it's a boy Time Time"

Google the first line of this message, if you do not recognize it, to
see what it is.

![](https://media.giphy.com/media/9pbkGeBmJMPDHaq1r0/giphy.gif?cid=ecf05e474hm2h603270c5ky0woddi1vnn6w8tgmed3fabgly&rid=giphy.gif&ct=g)

Knit, then stage everything listed in your **Git** pane, commit (with a
meaningful commit message), and push to your GitHub repo. Go to GitHub
and verify that your `activity03-r-intro.Rmd` file appears as you
intended it to.

You can now go back to the `README` file.

## Attribution

This activity is based on a lab from [Dr. Kelly
Bodwin](https://www.kelly-bodwin.com/)’s Stat 331 course
