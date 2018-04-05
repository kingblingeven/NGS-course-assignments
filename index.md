
# Week 2 assignment

## 王亮勻 (NTU GIBMS)

Rbfox3 is one of the main research targets in our lab. My seniors had compared the whole-genome expression profiles between wild-type and Rbfox3 homozygous knockout mice through RNA-seq, and identified the expression of two genes - Arc and Egr4, were modulated by Rbfox3 1.
However, whether the expression level of these genes were similarily associated with Rbfox3 level in Human is currently unknown.
Therefore, in this assignment, I explore a database consists of microarray samples derived from one human brain 2, to see if there's a similar expression pattern in human as well as in mice. The database consists of 6 files and the information I needed is unfortunately scattered across those files. Hence, I tidy the data manually, leaving only the information I'm currently interested 3.


```R
# Kernel density plots for mpg
# grouped by number of gears (indicated by color)
qplot(mpg, data=mtcars, geom="density", fill=gear, alpha=I(.5), 
   main="Distribution of Gas Milage", xlab="Miles Per Gallon", 
   ylab="Density")
```




![png](output_3_1.png)



```R
# Scatterplot of mpg vs. hp for each combination of gears and cylinders
# in each facet, transmittion type is represented by shape and color
qplot(hp, mpg, data=mtcars, shape=am, color=am, 
   facets=gear~cyl, size=I(3),
   xlab="Horsepower", ylab="Miles per Gallon") 
```




![png](output_4_1.png)



```R
# Separate regressions of mpg on weight for each number of cylinders
qplot(wt, mpg, data=mtcars, geom=c("point", "smooth"), 
   method="lm", formula=y~x, color=cyl, 
   main="Regression of MPG on Weight", 
   xlab="Weight", ylab="Miles per Gallon")
```

    Warning message:
    “Ignoring unknown parameters: method, formula”




![png](output_5_2.png)



```R
# Boxplots of mpg by number of gears 
# observations (points) are overlayed and jittered
qplot(gear, mpg, data=mtcars, geom=c("boxplot", "jitter"), 
   fill=gear, main="Mileage by Gear Number",
   xlab="", ylab="Miles per Gallon")
```




![png](output_6_1.png)

