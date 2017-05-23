# revisit: an R Package for Statistical Reproducibility and Alternate Analysis

### The reproducibility crisis

In recent years, scientists, especially those who run academic journals
or fund research projects, have been greatly concerned about lack of
*reproducibility* of research.  A study performed by one research group,
with certain findings, is then attempted by another group, with
different findings.  

In addition, there is a related problem, lack of *transparency*. In
reading a paper reporting on certain research, it is often not clear
exactly what procedures the authors used.

[As reported for
instance](http://www.nature.com/news/1-500-scientists-lift-the-lid-on-reproducibility-1.19970)
in the journal *Nature*, the problem is considered by many to have
reached crisis stage.

Much of the concern is statistical in nature. As noted in the above
*Nature* report (emphasis added):

> The survey asked scientists what led to problems in reproducibility.
> More than 60% of respondents said that each of two factors — pressure to
> publish and selective reporting — always or often contributed. More than
> half pointed to insufficient replication in the lab, poor oversight or
> low statistical power.
> 
> Respondents were asked to rate 11 different approaches to improving
> reproducibility in science, and all got ringing endorsements. Nearly 90%
> — more than 1,000 people — ticked "More robust experimental design"
> "better statistics"...

### The **revisit** package 

The package is, made available as open source, is
aimed to help remedy such problems with data/statistics.
In one sense, it might be termed a *statistical audit*, allowing users
to check the statistical analyses of the original authors of a study,
but it really is much more.  In our referring to "users" below, keep in
mind that this could mean various kinds of people, such as:

* The various authors of the study, during the period when the study is
  being conducted.  The package will facilitate collaboration among the
  authors at that time.

* Reviewers of a manuscript on the study, presented for possible
  publication.  The package will facilitate the reviewers' checking of
  the statistical analyses in the paper, not only verifying the steps
  but, even more importantly, allowing the reviewer to explore
  alternative analyses.

* Other scientists, who are reading a published paper on the study.  The
  package will facilitate these scientists also trying various
  alternative analyses.

The package has two main aspects:

<UL>

<li> It makes it easier and more convenient for the user to explore the
effects of various changes that might be made to the analyses.
The package facilitates replaying, changing and recording various new
versions of the analyses. 
</li> </p> 

<li>  The package spots troublesome statistical situations, and issues
advice and warnings, in light of concerns that too many "false
positives" are being reported in published research.  For example, the
package may:
</p>

   <UL>

      <li>  Point out that a p-value is small and may not to correspond to an
       effect of practical importance." 
      </li> </p> 

       <li> Point out that a "nonsignificant" value corresponds to a
       confidence interval containing both large positive and large
       negative values, so n is too small for a "no significant
       difference finding.
      </li> </p> 
       
      <li> Suggest that the user employ a multiple inference procedure
      (provided in the package).
      </li> </p> 

      <li>  Detect the presence of highly influential outliers, and suggest
        that a robust method, e.g. quantile regression be used.
       </li> </p> 

      <li> Etc.
      </li> </p> 

</UL>

</UL>

More specifically, the user might go through the following thought
processes, and take action using the facilities in the package:

*  The user thinks of questions involving alternate scenarios.  What,
   for instance, would occur if one were to more aggressively weed out
   outliers, or use outlier-resistant methods?  How would the results 
   change?  What if different predictor variables were used, or 
   squared and interaction terms added?  How valid are the models and 
   assumptions?  What about entirely different statistical approaches?

*  In exploring such questions, the user will modify the original
   code, producing at least one new version of the code, and
   likely several versions.  Say for instance the user is considering
   making two changes to the original analysis, one to possibly
   use outlier-resistant methods and another to use multiple-inference
   procedures. That potentially sets up four different versions.
   The **revisit** package facilitates this, making easier for the 
   user to make changes, try them out and record them into different 
   *branches* of the code.  In other words, the package facilitates
   exploration of alternative analyses.

*  In addition, the user may wish to share the results of her exploration 
   of alternate analyses of the data with others.  Since 
   each of her branches is conveniently packaged into a separate file, 
   she then simply sends the files to the other researchers.  The
   package allows the latter to easily "replay" the analyses, and they
   in turn may use the package to produce further branches.

* *Note, though, that the package is not aimed to "automate" statistical
analysis.*  The user decides which analyses to try, with the 
package consisting of tools to help by making it easy to explore, record and
package alternative analyses.

If the original data file is, say, **x.R**, then the branches will be
given names by the users, say **x.1.R**, **x.2.R** and so on.  Each
branch will have a brief, user-supplied description.


### Language and interface

The software is written in R, and is currently *in prototype form*. The
author of the original research is assumed to do all data/statistical
analysis in R.

Both text-based and graphical (GUI) interfaces are available.
The GUI uses RStudio *add-ins*.  The text-based version provides more
flexiblity, while the GUI provides convenience.

### Overview of the package

Let's get started, using the GUI.  (See installation instructions
below.)

We start up RStudio (either by icon or by typing 'rstudio' into a
command window), then load the 'revisit' library by typing
'library(revisit)' into the RStudio R console, then (near the top of the
screen) select Addins | Revisit.

In this example, we have copied the package file **examples/pima.R** to
the file **pima.R** in the directory/folder from which we started
RStudio.  We write 'pima' into the Filename box, and click Load Code.

As an illustration, suppose this code was written by the
author of the study.  The dataset is that of the famous Pima diabetes
study at the UCI data repository.

The screen now looks like this:

![alt text](Screen0.png)

RStudio is running in the background, and the foreground window shows
the **revisit** add-in running.  The original author's code is shown in
the editor portion in the bottom half of the window.  One can edit the
code, re-run in full or in part, save/load branches and so on.  All output
will be displayed in the R console portion of the background window.

By the way, **revisit** has automatically created branch 0, identical to
the original author code, but with an identifying comment line.

To replay the author's code, we click Run/Continue .  The new screen is:

![alt text](Screen1.png)

The results of the 8 confidence interval computations is shown in the R
console.  (There are 8 variables other than Diab, so the intervals
concern diabetics versus nondiabetics.)

We as the user may now think, "Hmm, one really should use a multiple
inference procedure here."  So we change line 12 to use **revisit** own
function, employing the Bonferroni method with number of comparisons
equal to 8.W

We then re-run.  *There is no need to start from the beginning*, so we
change the Run Start Line box to 11 and click Run/Continue, yielding:

![alt text](Screen2.png)

Ah, the confidence intervals did indeed get wider, as expected, now in
line with statistical fairness.  (Note that the Run Start Line box then
reverted to 1.)

Say we believe this branch is worth saving.  The Save Branch# box tells
us the next branch will be named branch 1 (we could change that), which
we now create by clicking Save Code.

We should also check whether the author did a good job of data cleaning.
As a crude measure, we can find the range of each of the variables, say
by running the code

``` r
print(apply(pima[,1:8],2,range))
```

We could simply run this code directly if we were in the text-based
version of **revisit**, since there we would have direct control of the
R console, which is not the case in the GUI version. So instead, we add
it temporarily at the end of code editor, as line 15. We change the Run
Start Line box to 15, and hit Run/Continue:

![alt text](Screen3.png)

Those 0s are troubling. How can variables such as Glucose and BMI be 0?
So we add code to remove cases with 0s.

### Main functions

**rvinit():**  Initializes the **revisit** system.

**makebranch0(origcodenm):**  Inputs the original author's code and
forms a branch copy of it.

**loadb(br):**  Loads a branch.

**runb(startline,throughline):**  Runs a branch through a user-specified
set of lines in the code, pausing at the end.  By default, these are the
numbers of the first and last lines of the code, but other numbers can
be specified.  Use 'c' to continue from the current line, or 's' to
execute just the current line.  (*Restriction:* The start and finish
lines cannot be inside a function, including loops and if-then-else.)  

**saveb(branchnum,desc):**  Save all the code changes to a new branch
with the given name and brief description.

**pause():**  Insert of this call will pause execution at the given
point, useful for instance immediately following a plotting function to
give the user a chance to view the plot.

**t.test.rv(x,y,alpha,bonf):**  Substitute for R's **t.test()**.  Calls the
latter but warns the user if a small p-value arises merely from a large
sample size rather than from a substantial effect.  If **bonf** is
larger than 1, **alpha** will be divided by **bonf** to implement
Bonferroni Inequality-based multiple inference.
Many more of these are planned.

**edt():**  Make a change to the current code.  Primitive for now.

**lcc():**  Display the current code.


### First example

Let's start with something very simple.  Here is code that the original
author might submit:

``` r
data(pima)  # load data
# divide into diabetic, non-diabetics
d <- which(pima$Diab == 1)
diab <- pima[d,]
nondiab <- pima[-d,]
# form a confidence interval for each variable, difference between
# diabetics and non-diabetics
for (i in 1:8)  {
   tmp <- t.test(diab[,i],nondiab[,i])$conf.int
   cat(names(pima)[i],'  ',tmp[1],tmp[2],'\n')
}
```

Suppose the author supplied that code in a file **pima.R**, in the
directory from which **revisit** is being run.  (This file is in the
**examples** directory in the package.) We could "replay" the code:


``` r
> rvinit()  # initialize 'revisit'
> makebranch0('pima.R')  # convert to 'revisit' form
> loadb('pima.0.R')  # load branch 0
> runb()  # run it

```

The output is

``` r
NPreg   1.046125 2.089219
Gluc   26.80786 35.74707
BP   -0.388326 5.66958
Thick   0.007076644 4.993282
Insul   12.75944 50.3282
BMI   3.735`811 5.940864
Genet   0.06891135 0.1726207
Age   4.209236 7.545092
```

But we might think, "Hmm, the author doesn't seem to have done any data
cleaning."  As a quick check, we might apply R's **range()** function to
each of the predictor variables.

``` r
> for (i in 1:8) {
+   rng <- range(pima[,i])
+    cat(names(pima)[i],rng,'\n')
+ }
NPreg 0 17 
Gluc 0 199 
BP 0 122 
Thick 0 99 
Insul 0 846 
BMI 0 67.1 
Genet 0.078 2.42 
Age 21 81 
```

Those 0s are troubling. How can variables such as Glucose and BMI be 0?
So, we add code to remove cases like that.  We'd call **edt()** (not
shown here), inserting

``` r
any0 <- function(pimarow) any(pimarow[c(2,3,4,6)] == 0) 
badrows <- apply(pima,1,any0) 
pima <- pima[-badrows,] 
```

after

```
data(pima)
```

We could check that the new code looks right:

```
1 # original code 
2 data(pima) 
3 any0 <- function(pimarow) any(pimarow[c(2,3,4,6)] == 0) 
4 badrows <- apply(pima,1,any0) 
5 pima <- pima[-badrows,] 
6 # divide into diabetic, non-diabetics 
7 d <- which(pima$Diab == 1) 
8 diab <- pima[d,] 
9 nondiab <- pima[-d,] 
10 # form a confidence interval for each variable, difference between 
11 # diabetics and non-diabetics 
12 for (i in 1:8)  { 
13 *    tmp <- t.test(diab[,i],nondiab[,i])$conf.int 
14    cat(names(pima)[i],'  ',tmp[1],tmp[2],'\n') 
15 } 

```

We then call **runb()** again:

```
> runb()
NPreg    1.040483 2.086364 
Gluc    26.77046 35.73396 
BP    -0.4010154 5.673465 
Thick    -0.04601711 4.950227 
Insul    13.0941 50.74512 
BMI    3.739046 5.949183 
Genet    0.06848236 0.1724766 
Age    4.159615 7.497838 
```

Not much change from before, but those 0s may have had impacts on other
analyses, say regression.

If we find this worthwhile, we call **saveb()** to save the current
code to a new branch:

```
> saveb('rm 0s','adds removal of suspicious 0s')
```

This creates branch 1, in a file **pima.1.R**. The description, "adds
removal...," is inserted as a new comment first line at the top of the file, 
in order to help us remember which branch is which if we have several of
them.

Next, we might say, "Really, we should use muliple comparisons here." We
are forming 8 confidence intervals, so it may be desirable to have at
least some protection.  We then call **edt()** again, replacing R's
**t.test()** function by the one in **revisit**, named **t.test.rv()**.
Since we are forming 8 confidence intervals, we set the argument
**bonf** to 8.  After calling **edt()** to make the change, we check the
code:

``` r
> lcc()
1 # original code 
2 data(pima) 
3 any0 <- function(pimarow) any(pimarow[c(2,3,4,6)] == 0) 
4 badrows <- apply(pima,1,any0) 
5 pima <- pima[-badrows,] 
6 # divide into diabetic, non-diabetics 
7 d <- which(pima$Diab == 1) 
8 diab <- pima[d,] 
9 nondiab <- pima[-d,] 
10 # form a confidence interval for each variable, difference between 
11 # diabetics and non-diabetics 
12 for (i in 1:8)  { 
13    tmp <- t.test.rv(diab[,i],nondiab[,i],bonf=8)$conf.int 
14    cat(names(pima)[i],'  ',tmp[1],tmp[2],'\n') 
15 } 
```

And run again()

``` r
> runb()
NPreg    0.8323935 2.294453 
Gluc    24.98722 37.5172 
BP    -1.609321 6.88177 
Thick    -1.039828 5.944038 
Insul    5.597938 58.24128 
BMI    3.299954 6.388275 
Genet    0.04779111 0.1931679 
Age    3.496427 8.161026 
```

Of course, the confidence intervals are now somewhat wider than before.
If we think it worthwhile, we can now call **saveb()** again, creating
**pima.1.R**,

