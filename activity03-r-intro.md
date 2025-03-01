Activity 3
================
Summer

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

punctuation <- c(".", ",", "!", "?", "'", ",", "(",")", "-", ";", ":")
```

Comment on what you noticed about the errors and how you used this
information to correct the issues.

**Response**: A quotation mark can’t be used at all except as part of
the coding language. I was surprised becaue it looks like parentheses
around a comma will exempt the comma from being read as code, but when I
tried that for the parenthesis, no dice.

Make one long vector containing all the symbols.

``` r
my_symbols <- c(lower_case, upper_case, punctuation)
```

Comment on what you noticed about the errors and how you used this
information to correct the issues.

**Response**: Uhhh.. there is a problem with the third list. When I look
at it, it’s only 11 items long instead of 26 like the other two. I
didn’t realize it wouldn’t just run the data frame anyway, so that’s
interesting. I tried to run it with just the two, but bubkis. Clearly
I’m missing something. Oh, yeah, “c” is for vectors, not “cbind”.

Turn the `my_symbols` vector into a data frame, with the variable name
“Symbol”.

``` r
my_symbols <- data.frame(my_symbols)
names(my_symbols) = "Symbol"
```

Comment on what you noticed about the errors and how you used this
information to correct the issues.

**Response**: It was easy to spot the missing . in dataframes. Took me a
minute to realize Symbols needed quotation marks around it.

Find the total number of symbols we have in our data frame.

``` r
len <- nrow(my_symbols)
```

Comment on what you noticed about the errors and how you used this
information to correct the issues.

**Response**: ?length didn’t give me anything about data frames, so I
was lost. Looked at the comment. How the heck was I supposed to know
about nrow? It wasn’t in the primer or the textbook! Grrrr…

5.  Create a new variable in your dataframe that assigns a number to
    each symbol.

``` r
my_symbols$Num <- 1:len
```

Comment on what you noticed about the errors and how you used this
information to correct the issues.

**Response**:Magic red squiggle says no % allowed. The only one I’ve
seen is the $ so I tried that.

<img src="README-img/noun_pause.png" alt="pause" width = "20"/>
<b>Planned Pause Point</b>: If you feel that you have a good
understanding of these Base R commands, feel free to start working on
your project. The remainder of this activity will help to expand these
Base R commands and I will post a solution on Blackboard by the end of
class.

### Decoding the secret message.

This chunk will load up the encoded secret message data and assign it as
a vector. There are no errors here.

``` r
# Read in full csv file
top_secret <- readr::read_csv("data/secret_code.csv", col_names = FALSE)
```

    ## 
    ## ── Column specification ────────────────────────────────────────────────────────
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
3.  Exponentiate every number. (You may need to Google how to this in
    R!)
4.  Square every number.

``` r
sum(top_secret < 17)
```

    ## [1] 1255

**HQ UPDATE:** Headquarters has informed you that at this stage of
decoding, there should be 496 numbers in the secret message that are
below 17.

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
length(500:length(top_secret))
```

    ## [1] 756

**HQ UPDATE:** Headquarters has informed you that at this stage of
decoding, all numbers in indices 500 and beyond are below 100.

11. Take the square root of all numbers in indices 38 to 465.
12. Round all numbers to the nearest whole number.
13. Replace all instances of the number 39 with 20.

``` r
top_secret[top_secret == 39] <- 20
```

**HQ UPDATE:** Headquarters has informed you that your final message
should have 421 even numbers.

![](README-img/noun_pause.png) **Planned Pause Point**: If things made
sense, feel free to continue on while you wait. Otherwise, contact your
instructor to have them verify your work.

## The secret message!

Use your final vector of numbers as indices for `my_symbols` to discover
the final message, by running the following code:

``` r
stringr::str_c(my_symbols$Symbol[top_secret], collapse = "")
```

    ## [1] ""

Google the first line of this message, if you do not recognize it, to
see what it is.

\[1\]
"Oh-yeah-In-France-a-skinny-man-died-of-a-big-disease-with-a-little-name-By-chance-his-girlfriend-came-across-a-needle-and-soon-she-did-the-same-At-home-there-are-seventeen;year;old-boys-and-their-idea-of-fun-Is-being-in-a-gang-called-The-Disciples,-high-on-crack,-totin’-a-machine-gun-Time-Time…

**Response**: I ran this several times with increasing frustration until
I read the whole activity more slowly and realized that the secret\_code
files was getting overwritten every time. No wonder my numbers kept
being so off! I deleted and re-upload the file a couple times until I
realized I could edit (copy/paste) directly into R. This took forever
because, as I’ve said before, this process is the opposite of the way my
brain works. I like to see the whole thing first, break down what it
does, then build new. This way of seeing it broken into pieces first,
then putting it together for something, takes me a long time to work
through. But I’m also learning it’s just a big fancy calculator and that
helps!

Knit, then stage everything listed in your **Git** pane, commit (with a
meaningful commit message), and push to your GitHub repo. Go to GitHub
and verify that your `activity03-r-intro.Rmd` file appears as you
intended it to.

You can now go back to the `README` file.

## Attribution

This activity is based on a lab from [Dr. Kelly
Bodwin](https://www.kelly-bodwin.com/)’s Stat 331 course
