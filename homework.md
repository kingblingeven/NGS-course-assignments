
# Week 2 assignment

## 王亮勻 (NTU GIBMS)

*Rbfox3* is one of the main research targets in our lab. My seniors had compared the whole-genome expression profiles between wild-type and *Rbfox3* homozygous knockout mice through RNA-seq, and identified the expression of two genes - *Arc* and *Egr4*, were modulated by *Rbfox3* [1](https://www.nature.com/articles/srep17383).<Br />
However, whether the expression level of these genes were similarily associated with Rbfox3 level in Human is currently unknown.
Therefore, in this assignment, I explore a database consists of microarray samples derived from one **human** brain [2](http://human.brain-map.org/api/v2/well_known_file_download/178238387), to see if there's a similar expression pattern in human as well as in mice. The database consists of 6 files and the information I needed is unfortunately scattered across those files. Hence, I tidy the data manually, leaving only the information I'm currently interested [3](https://www.dropbox.com/s/9r5m26gnu66jmu1/Donor%209861.xlsx?dl=0).


```R
> library(readxl)
> Donor_9861 <- read_excel("C:/Users/user/Desktop/Donor 9861.xlsx")
> View(Donor_9861)
```

Every row in this tidy dataset present a sample derived from different part of the brain.<Br />
Each column present the normalized gene expression value of a microarray probe. Some genes have more than one probe, in that case, I preserve data from all the probes and then average them.

I then examined the Pearson's correlation coefficient between Rbfox3 and the following genes:<Br />

1. ***Arc***<Br />
2. ***Egr4***<Br />
3. ***Nestin***: This gene is the marker for neuroprogenitor cells4. Since Rbfox3 is expressed only in mature, post-mitotic neurons, I supposed the expression of this gene is negatively correlated with Rbfox3.<Br />
4. ***GFAP***: Same as Nestin, to seved as a negative control. GFAP is thought to be a marker specific for astrocytes.<Br />
5. ***ASCL1***: Yet another negative control, becuase ASCL1 is a marker for immature neurons.[5](http://dev.biologists.org/content/141/12/2366)<Br />
6. ***Opsin4***: The gene encoded melanopsin, a photopigment inside the retina. I guess the expression of this gene is unrelated to the Rbfox3, since its expression is structure-specific, unlike "Rbfox3", which is a universal neural marker.<Br />
7. ***OR2A25***: Gene encoded olfactory receptors. The purpose of included this gene here is the same as Opsin4.



```R
> cor(Rbfox3,Arc_avg,use = "complete.obs")
[1] 0.5863444
> cor(Rbfox3,Egr4_Avg,use = "complete.obs")
[1] 0.7584867
> cor(Rbfox3,Nestin_avg,use = "complete.obs")
[1] -0.5162297
> cor(Rbfox3,GFAP,use = "complete.obs")
[1] -0.7483123
> cor(Rbfox3,ASCL1,use = "complete.obs")
[1] -0.06757373
> cor(Rbfox3,Opsin4_avg,use = "complete.obs")
[1] 0.0385974
> cor(Rbfox3,OR2A25_avg,use = "complete.obs")
[1] -0.249009
```

To visualize the correlation between pairs of genes, I drew the scatter plot:


```R
> par(mfrow=c(3,3))
> plot.default(Rbfox3,Arc_avg,ylab="Arc") 
> plot.default(Rbfox3,Egr4_Avg,ylab="Egr4")
> plot.default(Rbfox3,Nestin_avg,ylab="Nestin")
> plot.default(Rbfox3,GFAP)
> plot.default(Rbfox3,ASCL1)
> plot.default(Rbfox3,Opsin4_avg,ylab="Opsin4")
> plot.default(Rbfox3,OR2A25_avg,ylab="OR2A25")
```

Although farther statstics analysis is needed, the preliminary results here suggested that:<Br />

1. *Arc* and *Egr4* might be positively correlated to *Rbfox3*.<Br />
2. *Nestin*, *GFAP* might be negatively correlated to *Rbfox3*, which are as expected. However, the expression level of *ASCL1* seems unrelated to *Rbfox3*. This phenomenon may be the consequence of brain trauma [6](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5617972/)or tumor [7](https://www.sciencedirect.com/science/article/pii/B9780124059436000026). Since the phenotypes of the donor is unknown, to answer this question further investigations and more human samples might be needed.<Br />
3. The expression level of *Opsin4* and *OR2A25* might be unrelated to *Rbfox3* as well.

To further confirm this preliminary finding, I will have to investigate other 5 human brain microarray datasets in Allen's Brain Atlas, as well as conduct hypothesis test to see whether the expression between these pairs of genes were significantly correlated or not.
