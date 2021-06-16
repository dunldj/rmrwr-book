---
title: "Errors in R"
author: "Peter Higgins"
date: "12/12/2020"
output: html_document
---



# Interpreting Error Messages

Especially when you are starting out, it can be very difficult to interpret error messages, because these can be quite jargon-y.

Let's start with a table of the most common error messages, and the likely cause in each case.

Note that when reading an error message, there are two parts - the part before the colon, which identifies in which function the error occurred, and the part after the colon, which names the error. A typical error message is usually in the format:\
<br>

`Error in` Where the error occurred : what the error was

here is an example

`Error in as_flextable(.) : object 'errors' not found`

On the left, you are being told that the error occurred when the `as_flextable()` function was called. This can be helpful if you have run a long pipeline of functions, as it helps you isolate the problem.

On the right, you are being told what the error was. In this case, the function looked for the object `errors` in the working environment (see your Environment tab at the top right in RStudio), and could not find it.

::: {.tip}
Note that sometimes syntax errors caused by missing components (a missing comma, a missing parenthesis, a missing pipe symbol `%>%` , or a missing `+` sign in a ggplot pipe) will cause an error in the **next** function in the pipeline. Watch out for this, especially when the function where the error is found looks fine - often it occurs because there is a missing piece just *before* this function.
:::

Then we will walk through examples of how to create each error, and how to fix them, one by one.

## The Common Errors Table

Examine the error message from R, particularly the part that comes after the colon (:). The error messages listed in the left column will be what appears after the colon (:)

+------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Error Message                                                                      | What it Means                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
+====================================================================================+==============================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================+
| could not find function                                                            | This usually means that you made a typographical error in the function name (including Capitalization - R **is** case-sensitive), or that the package you are intending to use (which contains the function) is not installed - with \`install.packages('package_name')\`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|                                                                                    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|                                                                                    | or the package is not loaded - with \`library(package)\`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
+------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| object 'object-name' not found                                                     | This usually means that the function looked for an object (like a data frame or a vector) in your working environment (check your Environment pane) and could not find it. This commonly happens when you                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|                                                                                    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|                                                                                    | (1) mistype the name of the object (double-check this, easy to fix), or                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|                                                                                    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|                                                                                    | (2) you did not actually create or save this object to your working environment - confirm by checking your Environment tab at the top right in RStudio.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
+------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| filename does not exist in current working directory ('path/to/working/directory') | This usually means one of three things:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|                                                                                    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|                                                                                    | 1.  you mistyped the name of the file, or part of the path,                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|                                                                                    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|                                                                                    | <!-- -->                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|                                                                                    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|                                                                                    | (2) you are not in the directory where the file is, or                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|                                                                                    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|                                                                                    | (3) the file you thought you had saved does not exist (check your Files tab in the lower right pane in RStudio).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
+------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| error in if                                                                        | This usually means that you have an \*if\* statement that is trying to make a branch-point decision, but the logical statement that you wrote is not providing either a TRUE or a FALSE value. The most common reasons are typographical errors s in the logical statement, or an NA in one of the underlying values, which yields an NA from the logical statement. You may need to use a \`na.rm = TRUE\` option in your logical statement (the na.rm issue often comes up with means and medians).                                                                                                                                                                                                                                                                        |
+------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| error in eval                                                                      | This usually occurs when you are trying to run a function on an object that does not exist in your environment. Check to make sure in your Environment pane, and consider that you may not have saved/assigned the object in a previous step. Alternatively, you may have a typographical error in the object name. Worth checking.                                                                                                                                                                                                                                                                                                                                                                                                                                          |
+------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| cannot open                                                                        | This usually occurs when you are attempting to access or read a file that either does not exist, or is not in the folder that you thought it was. Check your working directory and find the file in your file structure. This can often be prevented by working in RStudio projects and using the here() function for paths to files.                                                                                                                                                                                                                                                                                                                                                                                                                                        |
+------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| no applicable method                                                               | This usually occurs when you are using a function that expects a particular data structure (vector, list, dataframe), but you have given it a different data structure as the input. Check the data structure of your object, and check the documentation for your function. For example, if you want to use a function that acts on vectors, this function will not work on a dataframe object. You may have to use the \`pull(variable)\`function to "pull" this variable out of the dataframe into a vector before using this function.                                                                                                                                                                                                                                   |
+------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| subscript out of bounds                                                            | you are trying to access an item in an environment object (like a vector, dataframe, or list) that does not exist, like the 9th item in a vector that is 7 items long, or the negative 2nd row of a dataframe. Check the length of the item, and the math that you used to count the item number (loops that go too long are often a culprit)                                                                                                                                                                                                                                                                                                                                                                                                                                |
+------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| replacement has [x] rows, data has [y] rows                                        | This usually occurs when you are trying to code for a new variable, or replace a variable in a dataframe. But somehow (missing values, NAs), what you are trying to add to the dataframe is **not** the same length (number of rows) as the rest of the existing dataframe. Use a length() function to check your building of this vector at each step, to figure out where your length went wrong.                                                                                                                                                                                                                                                                                                                                                                          |
+------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| package not available for R version x.y.z                                          | This occurs when you are trying to install a package, and your R version is newly updated. The problem is that the package version available on CRAN has not caught up to your shiny new version of R. This can happen after an R update when the package developer is working on updating their package, but the new version has not made it onto CRAN yet. This is often fixable if you know where the developer stores their development code (usually on GitHub). For example, if the package is {medicaldata}, and the developer's Github userid is higgi13425, then you can install the *development* version of this package with `remotes::install_github('higgi13425/medicaldata')`. This assumes that you have already installed and loaded the {remotes} package. |
+------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| non-numeric argument to a binary operator                                          | A binary operator, like `+` or `*`, is a mathematical operation that takes two values (operands) and produces another value. It gets grumpy when trying to do math on things that are not numbers. A typical input to produce this error would be `1 + 'one'` - one operand is numeric, and the other `'one'` is a character string - the non-numeric argument.                                                                                                                                                                                                                                                                                                                                                                                                              |
+------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| object of type closure is not subsettable                                          | This occurs when you try to extract a subset of something - but it is actually a function, not an object. This most commonly occurs when you try to subset a particular object that does not exist, like `df$patient_id` or `data$sbp`, when you have not created the objects `df` or `data`. The reason you get this strange error message, rather than simply `Error: object 'df' not found` , is that `df()` and `data()` are defined functions in base R. It is good practice to **avoid** naming **any** objects `data` or `df` for this reason. It gets very confusing, and this is best avoided.                                                                                                                                                                      |
+------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

: Common Error Messages in R

## Examples of Common Errors and How to fix them

### Missing Parenthesis

This is a very common error. It is easy to lose track of how many sets of parentheses you have open in putting together a complicated function.

Here is an example, where a closing parenthesis is missing from a *mutate()* function.


```r
prostate %>% 
  select(t_vol, p_vol, age, aa) %>% 
  mutate(ratio = t_vol/p_vol,
         older_aa = case_when(age >65 & aa == 1 ~ 1,
                              TRUE ~0) %>% 
  filter(older_aa ==1)
```

In this case, no output is produced, and the console does not return to the `>` prompt. Instead, it offers a `+` prompt - in effect, asking you for something more. If you type in an extra closing parenthesis (after the filter function), it will give you an error.

The error you get is:

> Error: Problem with \`mutate()\` input \`older_aa\`. x no applicable method for 'filter\_' applied to an object of class "c('double', 'numeric')" ℹ Input \`older_aa\` is \`\`%\>%\`(...)\`.

R identifies a problem with the input "older_aa" to mutate - the parentheses are not closed.\
It then fails on the next function - filter, and gives you a strange error message - `filter_` applied to... - because the input to the filter step (the next step after the error) was incoherent. This can be a bit confusing. But if you inspect the input older_aa, you will find the mis-matched parentheses. This is **much** easier to find with "rainbow parentheses" turned on in Tools/Global Options. When this option is on, you can be sure your parentheses are **right** when you end on **red**.

Sometimes the very thin parentheses of some fonts can make it difficult to identify your red close parenthesis. The red vs. yellow parentheses may be easier to differentiate if you use a **bold** font for your code. You can change this with RStudio Tools/Global Options/Appearance. I am currently using FiraCode-Bold and the Crimson Editor theme in RStudio, which seems to help me.

In this case, adding the missing parenthesis to the mutate step fixes it.

::: {.tip}
Parentheses that end on **red** are all **right**.
:::

### An Extra Parenthesis

What if you go the other way, with an extra parenthesis after some misguided copy-paste adventures? Let's see what happens.


```r
prostate %>% 
  select(t_vol, p_vol, age, aa) %>% 
  mutate(ratio = t_vol/p_vol,
         older_aa = case_when(age >65 & aa == 1 ~ 1,
                              TRUE ~0))) %>% 
  filter(older_aa ==1)
```

In this code block, you will end up with two red closing parentheses, and when you click to the right of the final closing parenthesis, there will be no matching highlighted open parenthesis (note that the preceding closing parentheses both have matching highlighted open parentheses. Both of these are clues that this last one is an extra.

The error you get from R is

> Error in filter(older_aa == 1) : object 'older_aa' not found

The **left side** of the error message identifies the *filter* step as where the error occurs, and the **right side** of the error message states that the error is an object not found. The error occurs when R gets to the **next** function. It also tells you that older_aa was not successfully created - suggesting that the problem is in the step **before** the filter function.

In this case, removing the extra parenthesis from the mutate step fixes it.

### Missing pipe `%>%` in a data wrangling pipeline

This is a common error. It is easy to cut out one of your `%>%` connectors when you are editing/debugging a data wrangling pipeline.

Here is an example, where a `%>%` is missing. Can you spot it?


```r
prostate %>% 
  select(t_vol, p_vol, age, aa)  
  mutate(ratio = t_vol/p_vol,
         older_aa = case_when(age >65 & aa == 1 ~ 1,
                              TRUE ~0)) %>% 
  filter(older_aa ==1)
```

In this case, the error you get is:

> Error in mutate(ratio = t_vol/p_vol, older_aa = case_when(age \> 65 & aa == : object 't_vol' not found

The **left side** of the error message identifies the *mutate* step as where the error occurs, and the **right side** of the error message states that the error is an object not found. This is a bit misleading, as the problem is not in the mutate step. But mutate is where the pipeline crashes, as it can not find the variable `t_vol`. You have to backtrack upwards line-by-line to find the error. Every line of a data wrangling pipeline should end in `%>%`. Since this is such a common error, this should be one of your "usual suspects". And the select line, just above the mutate line, is where the problem is.

In this case, adding the missing `%>%` to the end of the select step fixes your data wrangling pipeline.

::: {.tip}
Use one function per line in a pipeline.\
Check every data wrangling pipeline to make sure each step (except the last) ends in a pipe `%>%`
:::

### Missing + in a ggplot pipeline

This is a common error. It is easy to cut out one of your + connectors when you are editing/debugging a ggplot.

Here is an example, where a + is missing in the middle of a ggplot pipeline.


```r
prostate %>% 
  select(t_vol, p_vol, age, aa) %>% 
  ggplot(aes(x = factor(t_vol), y =p_vol)) 
  geom_boxplot() +
  labs(x = "tumor volume", y = "prostate volume") +
  theme_minimal()
```

In this case, you get a ggplot output, but without any boxplots. It is also missing your custom labels for the x and y axes, and the theme you wanted. Essentially, the code stops running after the initial ggplot() statement and the remaining lines of code are ignored. This can be pretty puzzling, as you do get a plot, but not what you intended. There is a partial plot in the Plots tab, but you get a somewhat helpful error in the Console.

The error you get is:

> Error: Cannot add ggproto objects together. Did you forget to add this object to a ggplot object?

R identifies a problem with the last 3 lines of code, starting with geom_boxplot() - it can not add these `ggproto` objects (the components of a ggplot) to the existing plot. It asks, "Did you forget to **add**?" which should be a clue that there is a missing `+` sign between lines of ggplot code. Since the theme and labels are the defaults, and there are no boxplots, suggest that these last 3 lines were not run at all, and that the missing plus sign should be found just before these lines of code.

In this case, adding the missing `+` to the end of the ggplot step fixes your plot.

::: {.tip}
Use one function per line in a pipeline.\
Check every ggplot pipeline to make sure each step (except the last) ends in a plus sign `+`
:::

### Pipe `%>%` in Place of a `+`

This is a common error. It is easy to start with your dataset, do some data wrangling steps with the pipe `%>%` and keep piping out of habit, even after you start your ggplot. Unfortunately, once you start to ggplot, you have to use + as your code connector. Having a pipe instead will cause an error.

Here is an example, where a `%>%` is used instead of `+` in a ggplot pipeline. It usually happens at the beginning of the ggplot, when you are still in piping mode.


```r
prostate %>% 
  select(t_vol, p_vol, age, aa) %>% 
  ggplot(aes(x = factor(t_vol), y =p_vol)) %>% 
  geom_boxplot() +
  labs(x = "tumor volume", y = "prostate volume") +
  theme_minimal()
```

In this case, you will not get a ggplot output, and you will get an error in the console.

The error you get is:

> Error: \`mapping\` must be created by \`aes()\` Did you use %\>% instead of +?

The error message identifies the *aes()* step as where the error occurs. R identifies a problem that causes the aes function to fail to create a mapping. The first line is not very helpful (other than identifying aes() as a problem), but in the next line, R asks, "Did you use %\>% instead of +?" which is **very** helpful. Once you know this, look at the line where *aes()* failed. This is where there is a pipe in place of a plus.

In this case, replacing the `%>%` with a `+` fixes your plot.

### Missing Comma Within a Function()

This is a common error. It is easy to start a series of arguments to a function, like multiple variables in a mutate step, and miss a comma between them.

Here is an example, where a comma is missing in a series of mutate steps. Note that it is a good habit to put one mutate step on each line, with each line ending in a comma. This will help you find the missing comma if (no, when) you make this mistake.


```r
prostate %>% 
  select(t_vol, p_vol, age, aa) %>% 
  mutate(ratio = t_vol/p_vol,
         older_aa = case_when(age >65 & aa == 1 ~ 1,
                              TRUE ~0)
         age_decade = floor(age / 10)) %>% 
  filter(older_aa ==1)
```

In this case, you will not get a tibble output, and you will get an error in the console.

The error you get is:

> Error in filter(older_aa == 1) : object 'older_aa' not found

The **left side** of the error message identifies the *filter* step as where the error occurs, and the **right side** of the error message states that the error is an object not found. R identifies a problem that causes the filter function to fail, but this is actually a problem in the line prior. The variable `older_aa` was not created and is not available to filter. It should have been created in the mutate step, but this step is where the failure occurred. Because you formatted the mutate step with one mutate statement per line, it is easy to check each line for a comma - and the older_aa line is missing its comma.

In this case, adding a comma at the end of the older_aa line (after "TRUE \~0)" fixes your data wrangling pipeline.

### A Missing Object

This is a common error. You may have created or modified a dataframe, but forgot to assign it to a new object name. Or maybe you did this assignment in a different session, but have not done it in your current session. Or maybe you made a typographical error in calling the object ("covvid" instead of "covid"). Either way, this object is not yet loaded into your computing environment (the Environment tab).

In this example, we request data from the {medicaldata} package, but forget to assign it to an object.

So it does not exist when we try to use it to start a pipeline. This does not work.


```r
medicaldata::covid_testing

covid %>% 
  select(subject_id, age, result, ct_result, patient_class) %>% 
  mutate(high_titer = case_when(ct_result < 18,
                                    TRUE ~ 0),
         age_decade = floor(age / 10)) %>% 
  filter(age >50)
```

In this case, you will not get a tibble output, and you will get an error in the console.

The error you get is:

> Error in select(., subject_id, age, result, ct_result, patient_class) : object 'covid' not found

The portion to the left of the comma identifies where the error occurs - in the select step. The portion to the right of the comma identifies the error. This one is easy. The object 'covid' was not found. You can check your Environment pane, and it will not be there. What the coder intended was to call `medicaldata::covid_testing` and assign it (with an arrow) to a new object named covid. But that assignment did not happen, and R is unable to guess what you meant.

In this case, adding an assignment arrow `->` to the end of the `medicaldata::covid_testing` line and then `covid` completes the assignment, creates the covid object, and\
fixes your data wrangling pipeline.

### One Equals Sign When you Need Two

This is a **very** common error. The equals sign is commonly used in two ways in R.

1.  To **assign** a parameter or argument of a function, like x = p_vol, or ratio = p_vol/t_vol, or color = "blue". In all of these assignment cases, you use ***one*** equals sign.
2.  To **test** a logical statement, like age == 60, or fam_hx == 1, or location == "Outpatient". In all of these logical tests, you use ***two*** equals signs.

It is very common to use one equals sign in a logical statement. This causes errors. Watch the last filter step below.


```r
prostate %>% 
  select(t_vol, p_vol, age, aa) %>% 
  mutate(ratio = t_vol/p_vol,
         older_aa = case_when(age >65 & aa == 1 ~ 1, TRUE ~0),
         age_decade = floor(age / 10)) %>% 
  filter(older_aa ==1)
```

In this case, the error you receive is very helpful:

> Error: Problem with \`filter()\` input \`..1\`. x Input \`..1\` is named. ℹ This usually means that you've used \`=\` instead of \`==\`. ℹ Did you mean \`older_aa == 1\`?

The problem is with the *filter* step. The error starts out very jargon-y. "input \`..1\`. x Input \`..1\` is named" - means the input to filter is actually named (an assignment). But then it gets a lot more helpful. It recognizes that you have made a common error, and suggests an appropriate fix.

In this case, adding a 2nd equals sign in the filter step fixes your data wrangling pipeline.

::: {.warning}
Testing for equality with `==` is a big problem with real numbers, rather than integers. Computers use algorithms to do math which are not quite exact, leading to small differences in decimals. The `==` equality test is very strict, so that something like `sqrt(2)^2 == 2` is FALSE because of small differences far to the right of the decimal point, which can trip you up. You can see these if you run the modulo 2: `sqrt(2)^2 %% 2`, which gives you the remainder after you divide by 2, which is the very tiny 0.0000000000000004440892. In this situation, you should use the near() function, as `near(sqrt(2)^2, 2)` is TRUE. The *near* function has a built-in tolerance of 0.00000001490116, which will be able to handle any computer-generated small, stray decimals. You can set your own tolerance argument if needed.
:::

### Non-numeric argument to a binary operator

This happens when you try to do math on things that are not numbers. It usually occurs when you have a variable(column) that *looks* like it is numeric (it contains numbers), but somewhere along the way it became a character string variable. This often occurs when data are being entered into a spreadsheet, and one value in the column has characters in it. This often happens when you have a column of systolic blood pressures, and one value is entered as "this was not done", or "102, but taken standing up". Having comments, even if only one character string in a column in Excel **makes the whole column** into the character string data type.

This is not apparent until you try to do math with this variable, as in


```r
data %>% 
  mutate(mean_art_pressure = sbp/3 + 2/3* dbp)
```

This will give you the error:

> Error in mutate(mean_art_pressure: non-numeric argument to binary operator

To fix this, you will have to

1.  Determine which variable, sbp or dbp, is non-numeric (`glimpse(data)` will help).

2.  Review the values of the problem variable (possibly with table()) to find which is non-numeric.

3.  Fix these values manually in your code, and document with comments

    1.  Which values are being fixed (e.g. sbp for subject 007, at visit 2)\
        `data$sbp[subject == 007 & visit == 2] <- 102`

    2.  What the original value was, and what the new value will be

    3.  Who made the change to the data

    4.  Why the data change was made

    5.  On what date the data change was made

    6.  **Never** over-write your original data - keep a complete audit trail!

## Errors Beyond This List

This is where the internet comes in handy. Whatever errors you can create, **someone** has already run into. And they have asked for help on the internet, and most of the time, someone has helped them solve their error.

You should copy your entire error message, and paste it into a web search. Google will often yield multiple similar examples, with various ways to solve the problem.

In a future chapter, we will explore more effective ways to seek help, using a **minimal reprex** to describe your problem accurately to other people on sites like [community.rstudio.com](community.rstudio.com).

**Remember** that the error may have occurred because of a problem in the previous line of code (missing parenthesis, comma, etc.), so don't forget to check one line above.

The **Add-One-Line** debugging strategy is another good strategy. Select the code for your pipeline from the beginning to 2 lines of code before the error. If that runs without errors, add one line to your selection, and run it. Keep adding lines to your selection and running until you hit the error. Then try to find the problem and fix it.

## When Things Get Weird

### Restart your R Session (Shift-Cmd-F10)

If you are running code that has worked before, and it is not working now, it is possible that you have created something odd in your working Environment that is interfering with your code. Sometimes it is an old object from a previous session (it is always better to start from a clean slate). Completely restart your R session (click on Session/Restart R, or use the keyboard shortcut), make sure the Environment is clean, then run your code from start to finish to give it a new try. Sometimes a clean slate will make all the difference.

## References:

These are some helpful general references on troubleshooting in R, particularly focused on error messages encountered by beginners to R. Click on some of the links to check these out.

<https://bookdown.org/yih_huynh/Guide-to-R-Book/trouble.html>

<https://medium.com/analytics-vidhya/common-errors-in-r-and-debugging-techniques-f11af3f1c7d3>

<https://rpubs.com/Altruimetavasi/Troubleshooting-in-R>

<https://github.com/noamross/zero-dependency-problems/blob/master/misc/stack-overflow-common-r-errors.md>

<https://www.r-bloggers.com/2016/06/common-r-programming-errors-faced-by-beginners/>

<https://www.r-bloggers.com/2015/03/the-most-common-r-error-messages/>

<https://rpubs.com/Altruimetavasi/Troubleshooting-in-R>

<https://statisticsglobe.com/errors-warnings-r>
