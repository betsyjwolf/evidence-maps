# Average Differences in Effect Sizes by Outcome Measure Type
This repository provides open access to data in the working paper, "Average differences in effect sizes by outcome measure type" found [HERE](https://www.tandfonline.com/doi/full/10.1080/19345747.2020.1726537).

## Abstract

The What Works Clearinghouse (WWC) seeks to provide educators information about “what works in education.” One challenge in understanding “what works” is that effect sizes may not be comparable across studies, which limits the ability to compare the relative effectiveness of multiple interventions. One factor that consistently relates to the magnitude of effect sizes is the type of outcome measure. This paper uses WWC study data to examine differences in average effect sizes by outcome measure type. Controlling for other factors and using advanced meta-analysis, effect sizes found on researcher and developer measures are substantially larger on average than those found on independent measures not related to the intervention under study or the study authors. One implication of this finding is that the WWC should consider whether findings based on researcher and developer measures should be differentiated from those based on independent measures to meet the evidence needs of all WWC stakeholders. 

## What's Included Here

This repository includes the open access dataset and figures presented in the working paper.

```
Study data available here:
```
- [Data](public_use_dataset.xlsx)

```
Study figures:
```
* Box Plots of Effect Sizes for English Language Arts (ELA) Interventions by Developer-Commissioned and Independent Studies
![](https://github.com/betsyjwolf/Effect-Sizes-in-Developer-and-Independent-Studies/blob/master/Figure%201.jpg)

* Box Plots of Effect Sizes for Math Interventions by Developer-Commissioned and Independent Studies
![](https://github.com/betsyjwolf/Effect-Sizes-in-Developer-and-Independent-Studies/blob/master/Figure%202.jpg)

* Distributions of Empirical Bayes Effect Size Predictions for Developer-Commissioned and Independent Studies
![](https://github.com/betsyjwolf/Effect-Sizes-in-Developer-and-Independent-Studies/blob/master/Figure%203.jpg)

```
Code for conducting the meta-analysis:
```
R Code

library(metafor)  

library(clubSandwich)

#Specify the observed covariance matrix: data=name of dataset, vij=observed effect-size-level variances, 
#.80=assumed correlation among effect sizes within studies

matrix_name <- impute_covariance_matrix(vi = data$vij, cluster = data$studyid, r = .80)

#Run the model: effect_size=variable containing finding-level effect sizes, mods=moderator variables

model_name <- rma.mv(yi=effect_size, V = matrix_name, mods = ~ covarate1 + covariate2 + …, random = ~1 | studyid/findingid, test= "t", data=data, method="REML")

#Produce RVE estimates robust to model misspecification: “CR2”=estimation method

rve_based <- coef_test(model_name, cluster=data$studyid, vcov = "CR2")

## License to Use These Data

These data are made available under the [Open Data Commons Attribution License](http://opendatacommons.org/licenses/by/). You may use, share, and adapt the data so long as you agree to acknowledge this project as the source of these data. Please cite the data as:

Wolf, R., Morrison, J., Inns, A., Slavin, R., & Risman, K. (2019). Data archive for "Differences in average effect sizes in developer-commissioned and independent studies." Towson, MD: Center for Research and Reform in Education (CRRE), Johns Hopkins University. Retrieved from https://github.com/betsyjwolf/Effect-Sizes-in-Developer-and-Independent-Studies

## Authors

The authors are researchers at the [Center for Research and Reform in Education (CRRE)](https://education.jhu.edu/crre/) at [Johns Hopkins University (JHU)](https://www.jhu.edu/).

* **Betsy Wolf, PhD** - [Faculty Profile](https://education.jhu.edu/directory/rebecca-wolf-phd/)

## Programs and Packages Used in this Project

* H. Wickham. ggplot2: Elegant Graphics for Data Analysis. Springer-Verlag New York, 2016.
* Hadley Wickham (2011). The Split-Apply-Combine Strategy for Data Analysis. Journal of Statistical
  Software, 40(1), 1-29. URL http://www.jstatsoft.org/v40/i01/
* James Pustejovsky (2019). clubSandwich: Cluster-Robust (Sandwich) Variance Estimators with
  Small-Sample Corrections. R package version 0.3.5.
  https://CRAN.R-project.org/package=clubSandwich
* Kathleen M. Coburn and Jack L. Vevea (2019). weightr: Estimating Weight-Function Models for
  Publication Bias. R package version 2.0.2. https://CRAN.R-project.org/package=weightr
* R Core Team (2013). R: A language and environment for statistical computing. R Foundation for Statistical Computing, Vienna, Austria.   URL http://www.R-project.org/
* StataCorp. 2019. Stata Statistical Software: Release 16. College Station, TX: StataCorp LLC.
* Viechtbauer, W. (2010). Conducting meta-analyses in R with the metafor package. Journal of
  Statistical Software, 36(3), 1-48. URL: http://www.jstatsoft.org/v36/i03/





