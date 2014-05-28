# Functions and control structures (for, if/else etc.)

## User defined functions
Functions are useful for transforming larger chunks of code to reusable pieces of code. Generally, if you need to execute certain tasks with variable parameters then it is time you write a function. A function in R takes different arguments and returns a definite output, much like mathematical functions. Here is a simple function takes two arguments, x and y, and returns the sum of their squares.


```r
sqSum <- function(x, y) {
    result = x^2 + y^2
    return(result)
}
# now try the function out
sqSum(2, 3)
```

```
## [1] 13
```



Functions can also output plots and/or messages to the terminal. Here is a function that prints a message to the terminal:

```r
sqSumPrint <- function(x, y) {
    result = x^2 + y^2
    cat("here is the result:", result, "\n")
}
# now try the function out
sqSumPrint(2, 3)
```

```
## here is the result: 13
```


Sometimes we would want to execute a certain part of the code only if certain condition is satisfied. This condition can be anything from the type of an object (Ex: if object is a matrix execute certain code), or it can be more compicated such as if object value is between certain thresholds. Let us see how they can be used3. They can be used anywhere in your code, now we will use it in a function.


```r
cpgi.df <- read.table("../data/subset.cpgi.hg18.bed", header = FALSE)
# function takes input one row of CpGi data frame
largeCpGi <- function(bedRow) {
    cpglen = bedRow[3] - bedRow[2] + 1
    if (cpglen > 1500) {
        cat("this is large\n")
    } else if (cpglen <= 1500 & cpglen > 700) {
        cat("this is normal\n")
    } else {
        cat("this is short\n")
    }
}
largeCpGi(cpgi.df[10, ])
largeCpGi(cpgi.df[100, ])
largeCpGi(cpgi.df[1000, ])
```


## Loops and looping structures in R
When you need to repeat a certain task or a execute a function multiple times, you can do that with the help of loops. A loop will execute the task until a certain condition is reached. The loop below is called a “for-loop” and it executes the task sequentially 10 times.

```r
for (i in 1:10) {
    # number of repetitions
    cat("This is iteration")  # the task to be repeated
    print(i)
}
```

```
## This is iteration[1] 1
## This is iteration[1] 2
## This is iteration[1] 3
## This is iteration[1] 4
## This is iteration[1] 5
## This is iteration[1] 6
## This is iteration[1] 7
## This is iteration[1] 8
## This is iteration[1] 9
## This is iteration[1] 10
```

The task above is a bit pointless, normally in a loop, you would want to do something meaningful. Let us calculate the length of the CpG islands we read in earlier. Although this is not the most efficient way of doing that particular task, it serves as a good example for looping. The code below will be execute hundred times, and it will calculate the length of the CpG islands for the first 100 islands in
the data frame (by subtracting the end coordinate from the start coordinate).


**Note:**If you are going to run a loop that has a lot of repetitions, it is smart to try the loop with few repetitions first and check the results. This will help you make sure the code in the loop works before executing it for thousands of times.


```r
# this is where we will keep the lenghts for now it is an empty vector
result = c()
# start the loop
for (i in 1:100) {
    # calculate the length
    len = cpgi.df[i, 3] - cpgi.df[i, 2] + 1
    # append the length to the result
    result = c(result, len)
}
```

```
## Error: object 'cpgi.df' not found
```

```r
# check the results
head(result)
```

```
## NULL
```




