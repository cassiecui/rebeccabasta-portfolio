---
title: "Data Analysis"
---

::: {.cell}

```{.r .cell-code}
#load dslabs package
library(dslabs)
library(tidyverse)
```

::: {.cell-output .cell-output-stderr}

```
── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
✔ dplyr     1.2.0     ✔ readr     2.1.6
✔ forcats   1.0.1     ✔ stringr   1.6.0
✔ ggplot2   4.0.2     ✔ tibble    3.3.1
✔ lubridate 1.9.5     ✔ tidyr     1.3.2
✔ purrr     1.2.1     
── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
✖ dplyr::filter() masks stats::filter()
✖ dplyr::lag()    masks stats::lag()
ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors
```


:::

```{.r .cell-code}
#help(gapminder)
#The str functions is used to look at observations and variables in the dataset  
str(gapminder)
```

::: {.cell-output .cell-output-stdout}

```
'data.frame':	10545 obs. of  9 variables:
 $ country         : Factor w/ 185 levels "Albania","Algeria",..: 1 2 3 4 5 6 7 8 9 10 ...
 $ year            : int  1960 1960 1960 1960 1960 1960 1960 1960 1960 1960 ...
 $ infant_mortality: num  115.4 148.2 208 NA 59.9 ...
 $ life_expectancy : num  62.9 47.5 36 63 65.4 ...
 $ fertility       : num  6.19 7.65 7.32 4.43 3.11 4.55 4.82 3.45 2.7 5.57 ...
 $ population      : num  1636054 11124892 5270844 54681 20619075 ...
 $ gdp             : num  NA 1.38e+10 NA NA 1.08e+11 ...
 $ continent       : Factor w/ 5 levels "Africa","Americas",..: 4 1 1 2 2 3 2 5 4 3 ...
 $ region          : Factor w/ 22 levels "Australia and New Zealand",..: 19 11 10 2 15 21 2 1 22 21 ...
```


:::

```{.r .cell-code}
#get a summary of data
summary(gapminder)
```

::: {.cell-output .cell-output-stdout}

```
                country           year      infant_mortality life_expectancy
 Albania            :   57   Min.   :1960   Min.   :  1.50   Min.   :13.20  
 Algeria            :   57   1st Qu.:1974   1st Qu.: 16.00   1st Qu.:57.50  
 Angola             :   57   Median :1988   Median : 41.50   Median :67.54  
 Antigua and Barbuda:   57   Mean   :1988   Mean   : 55.31   Mean   :64.81  
 Argentina          :   57   3rd Qu.:2002   3rd Qu.: 85.10   3rd Qu.:73.00  
 Armenia            :   57   Max.   :2016   Max.   :276.90   Max.   :83.90  
 (Other)            :10203                  NA's   :1453                    
   fertility       population             gdp               continent   
 Min.   :0.840   Min.   :3.124e+04   Min.   :4.040e+07   Africa  :2907  
 1st Qu.:2.200   1st Qu.:1.333e+06   1st Qu.:1.846e+09   Americas:2052  
 Median :3.750   Median :5.009e+06   Median :7.794e+09   Asia    :2679  
 Mean   :4.084   Mean   :2.701e+07   Mean   :1.480e+11   Europe  :2223  
 3rd Qu.:6.000   3rd Qu.:1.523e+07   3rd Qu.:5.540e+10   Oceania : 684  
 Max.   :9.220   Max.   :1.376e+09   Max.   :1.174e+13                  
 NA's   :187     NA's   :185         NA's   :2972                       
             region    
 Western Asia   :1026  
 Eastern Africa : 912  
 Western Africa : 912  
 Caribbean      : 741  
 South America  : 684  
 Southern Europe: 684  
 (Other)        :5586  
```


:::

```{.r .cell-code}
#determine the type of object gapminder is
#The class function is a data frame that allows us to look at a class of the dataset
class(gapminder)
```

::: {.cell-output .cell-output-stdout}

```
[1] "data.frame"
```


:::

```{.r .cell-code}
#Using the gapminder dataset, I've created a new dataframe that will only include countries that have Africa as the continent
africadata <- gapminder[gapminder$continent == "Africa", ]

#Check the structure and summary of africadata
str(africadata)
```

::: {.cell-output .cell-output-stdout}

```
'data.frame':	2907 obs. of  9 variables:
 $ country         : Factor w/ 185 levels "Albania","Algeria",..: 2 3 18 22 26 27 29 31 32 33 ...
 $ year            : int  1960 1960 1960 1960 1960 1960 1960 1960 1960 1960 ...
 $ infant_mortality: num  148 208 187 116 161 ...
 $ life_expectancy : num  47.5 36 38.3 50.3 35.2 ...
 $ fertility       : num  7.65 7.32 6.28 6.62 6.29 6.95 5.65 6.89 5.84 6.25 ...
 $ population      : num  11124892 5270844 2431620 524029 4829291 ...
 $ gdp             : num  1.38e+10 NA 6.22e+08 1.24e+08 5.97e+08 ...
 $ continent       : Factor w/ 5 levels "Africa","Americas",..: 1 1 1 1 1 1 1 1 1 1 ...
 $ region          : Factor w/ 22 levels "Australia and New Zealand",..: 11 10 20 17 20 5 10 20 10 10 ...
```


:::

```{.r .cell-code}
summary(africadata)
```

::: {.cell-output .cell-output-stdout}

```
         country          year      infant_mortality life_expectancy
 Algeria     :  57   Min.   :1960   Min.   : 11.40   Min.   :13.20  
 Angola      :  57   1st Qu.:1974   1st Qu.: 62.20   1st Qu.:48.23  
 Benin       :  57   Median :1988   Median : 93.40   Median :53.98  
 Botswana    :  57   Mean   :1988   Mean   : 95.12   Mean   :54.38  
 Burkina Faso:  57   3rd Qu.:2002   3rd Qu.:124.70   3rd Qu.:60.10  
 Burundi     :  57   Max.   :2016   Max.   :237.40   Max.   :77.60  
 (Other)     :2565                  NA's   :226                     
   fertility       population             gdp               continent   
 Min.   :1.500   Min.   :    41538   Min.   :4.659e+07   Africa  :2907  
 1st Qu.:5.160   1st Qu.:  1605232   1st Qu.:8.373e+08   Americas:   0  
 Median :6.160   Median :  5570982   Median :2.448e+09   Asia    :   0  
 Mean   :5.851   Mean   : 12235961   Mean   :9.346e+09   Europe  :   0  
 3rd Qu.:6.860   3rd Qu.: 13888152   3rd Qu.:6.552e+09   Oceania :   0  
 Max.   :8.450   Max.   :182201962   Max.   :1.935e+11                  
 NA's   :51      NA's   :51          NA's   :637                        
                       region   
 Eastern Africa           :912  
 Western Africa           :912  
 Middle Africa            :456  
 Northern Africa          :342  
 Southern Africa          :285  
 Australia and New Zealand:  0  
 (Other)                  :  0  
```


:::

```{.r .cell-code}
#Create a dataframe with infant mortality and life expectancy
africa_mort_life <- africadata[, c("infant_mortality", "life_expectancy")]

#Inspect the structure and summary
str(africa_mort_life)
```

::: {.cell-output .cell-output-stdout}

```
'data.frame':	2907 obs. of  2 variables:
 $ infant_mortality: num  148 208 187 116 161 ...
 $ life_expectancy : num  47.5 36 38.3 50.3 35.2 ...
```


:::

```{.r .cell-code}
summary(africa_mort_life)
```

::: {.cell-output .cell-output-stdout}

```
 infant_mortality life_expectancy
 Min.   : 11.40   Min.   :13.20  
 1st Qu.: 62.20   1st Qu.:48.23  
 Median : 93.40   Median :53.98  
 Mean   : 95.12   Mean   :54.38  
 3rd Qu.:124.70   3rd Qu.:60.10  
 Max.   :237.40   Max.   :77.60  
 NA's   :226                     
```


:::

```{.r .cell-code}
#Create a dataframe with population and life expectancy
africa_pop_life <- africadata[, c("population", "life_expectancy")]

#Inspect the structure and summary
str(africa_pop_life)
```

::: {.cell-output .cell-output-stdout}

```
'data.frame':	2907 obs. of  2 variables:
 $ population     : num  11124892 5270844 2431620 524029 4829291 ...
 $ life_expectancy: num  47.5 36 38.3 50.3 35.2 ...
```


:::

```{.r .cell-code}
summary(africa_pop_life)
```

::: {.cell-output .cell-output-stdout}

```
   population        life_expectancy
 Min.   :    41538   Min.   :13.20  
 1st Qu.:  1605232   1st Qu.:48.23  
 Median :  5570982   Median :53.98  
 Mean   : 12235961   Mean   :54.38  
 3rd Qu.: 13888152   3rd Qu.:60.10  
 Max.   :182201962   Max.   :77.60  
 NA's   :51                         
```


:::
:::


This analysis looks at African countries using the Gapminder dataset on R. The data is first subset to only include African countries. Then two smaller datasets are created to look at life expectancy with infant mortality and population with infant mortality. 


::: {.cell}

```{.r .cell-code}
#Plot life expectancy vs infant mortality for African countries
#Using the plot function to make the plot
plot(
    #Using the infant_mortality column and makes them the x-axis values
  africa_mort_life$infant_mortality,
  #Using the life_expectancy column and makes them the y-axis values
  africa_mort_life$life_expectancy,
  #labels the x-axis infant mortality and the y-axis Life expectancy
  xlab = "Infant Mortality",
  ylab = "Life Expectancy",
  #Makes the title of the plot Life expectancy vs infant mortality in Africa
  main = "Life Expectancy vs Infant Mortality in Africa",
  pch = 16
)
```

::: {.cell-output-display}
![](starter-analysis-exercise_files/figure-html/unnamed-chunk-2-1.png){width=672}
:::

```{.r .cell-code}
#Plot life expectancy vs population size for African countries
#Using the plot function to make the plot
plot(
    #Using the population column and makes them the x-axis values
  africa_pop_life$population,
  #Using the life expectancy column and makes them the y-axis values
  africa_pop_life$life_expectancy,
  #labels the x-axis population size and the y-axis Life expectancy
  xlab = "Population Size (log scale)",
  ylab = "Life Expectancy",
  #Makes the title of the plot Life expectancy vs population size in Africa
  main = "Life Expectancy vs Population Size in Africa",
  pch = 16,
  #Setting the scale of the x-axis to be logarithmic
  log = "x"
)
```

::: {.cell-output-display}
![](starter-analysis-exercise_files/figure-html/unnamed-chunk-2-2.png){width=672}
:::
:::


The first plot shows a negative relationship between infant mortality and life expectancy. The second plot shows a positive relationship between population size and life expectancy. The streaks in the plots are most likley due to individual countries obsereved over multiple years. This shows more in the second plot because there is data for the same countries over several years, which is likely to show gradual differences. These gradual differences may form streaks in the plots.


::: {.cell}

```{.r .cell-code}
#Identifies which years have missing data for infant mortality 
#is.na() functions chacks if each value in the dataframe is NA or not
missing_im <- is.na(africadata$infant_mortality)

#Lists the years when infant mortality is missing
missing_years <- sort(unique(africadata$year[missing_im]))
missing_years
```

::: {.cell-output .cell-output-stdout}

```
 [1] 1960 1961 1962 1963 1964 1965 1966 1967 1968 1969 1970 1971 1972 1973 1974
[16] 1975 1976 1977 1978 1979 1980 1981 2016
```


:::

```{.r .cell-code}
#Extract data for the year 2000 only
africa_2000 <- africadata[africadata$year == 2000, ]

#Check the structure of the new dataset
str(africa_2000)
```

::: {.cell-output .cell-output-stdout}

```
'data.frame':	51 obs. of  9 variables:
 $ country         : Factor w/ 185 levels "Albania","Algeria",..: 2 3 18 22 26 27 29 31 32 33 ...
 $ year            : int  2000 2000 2000 2000 2000 2000 2000 2000 2000 2000 ...
 $ infant_mortality: num  33.9 128.3 89.3 52.4 96.2 ...
 $ life_expectancy : num  73.3 52.3 57.2 47.6 52.6 46.7 54.3 68.4 45.3 51.5 ...
 $ fertility       : num  2.51 6.84 5.98 3.41 6.59 7.06 5.62 3.7 5.45 7.35 ...
 $ population      : num  31183658 15058638 6949366 1736579 11607944 ...
 $ gdp             : num  5.48e+10 9.13e+09 2.25e+09 5.63e+09 2.61e+09 ...
 $ continent       : Factor w/ 5 levels "Africa","Americas",..: 1 1 1 1 1 1 1 1 1 1 ...
 $ region          : Factor w/ 22 levels "Australia and New Zealand",..: 11 10 20 17 20 5 10 20 10 10 ...
```


:::

```{.r .cell-code}
#View summary statistics for the year 2000 data
summary(africa_2000)
```

::: {.cell-output .cell-output-stdout}

```
         country        year      infant_mortality life_expectancy
 Algeria     : 1   Min.   :2000   Min.   : 12.30   Min.   :37.60  
 Angola      : 1   1st Qu.:2000   1st Qu.: 60.80   1st Qu.:51.75  
 Benin       : 1   Median :2000   Median : 80.30   Median :54.30  
 Botswana    : 1   Mean   :2000   Mean   : 78.93   Mean   :56.36  
 Burkina Faso: 1   3rd Qu.:2000   3rd Qu.:103.30   3rd Qu.:60.00  
 Burundi     : 1   Max.   :2000   Max.   :143.30   Max.   :75.00  
 (Other)     :45                                                  
   fertility       population             gdp               continent 
 Min.   :1.990   Min.   :    81154   Min.   :2.019e+08   Africa  :51  
 1st Qu.:4.150   1st Qu.:  2304687   1st Qu.:1.274e+09   Americas: 0  
 Median :5.550   Median :  8799165   Median :3.238e+09   Asia    : 0  
 Mean   :5.156   Mean   : 15659800   Mean   :1.155e+10   Europe  : 0  
 3rd Qu.:5.960   3rd Qu.: 17391242   3rd Qu.:8.654e+09   Oceania : 0  
 Max.   :7.730   Max.   :122876723   Max.   :1.329e+11                
                                                                      
                       region  
 Eastern Africa           :16  
 Western Africa           :16  
 Middle Africa            : 8  
 Northern Africa          : 6  
 Southern Africa          : 5  
 Australia and New Zealand: 0  
 (Other)                  : 0  
```


:::

```{.r .cell-code}
#Plot life expectancy vs infant mortality for Africa in the year 2000
#Using the plot function to make the plot
plot(
     #Using the infant mortality column and makes them the x-axis values
  africa_2000$infant_mortality,
   #Using the life expectancy column and makes them the y-axis values
  africa_2000$life_expectancy,
  #labels the x-axis infant mortality and the y-axis Life expectancy
  xlab = "Infant Mortality",
  ylab = "Life Expectancy",
  #Makes the title of the plot Life expectancy vs infant mortality in Africa in 2000
  main = "Life Expectancy vs Infant Mortality in Africa in 2000",
  pch = 16
)
```

::: {.cell-output-display}
![](starter-analysis-exercise_files/figure-html/unnamed-chunk-3-1.png){width=672}
:::

```{.r .cell-code}
# Plot life expectancy vs population size for Africa in the year 2000
#Using the plot function to make the plot
plot(
     #Using the population column and makes them the x-axis values
  africa_2000$population,
   #Using the life expectancy column and makes them the y-axis values
  africa_2000$life_expectancy,
  #labels the x-axis population size and the y-axis Life expectancy
  xlab = "Population Size (log scale)",
  ylab = "Life Expectancy",
  #Makes the title of the plot Life expectancy vs population size in Africa in 2000
  main = "Life Expectancy vs Population Size in Africa in 2000",
  pch = 16,
  #Setting the scale of the x-axis to be logarithmic
  log = "x"
)
```

::: {.cell-output-display}
![](starter-analysis-exercise_files/figure-html/unnamed-chunk-3-2.png){width=672}
:::

```{.r .cell-code}
#Models life expectancy as a function of infant mortality
#lm is used to fit linear models
lm_infant <- lm(life_expectancy ~ infant_mortality, data = africa_2000)

# Models life expectancy as a function of population size
lm_population <- lm(life_expectancy ~ population, data = africa_2000)

# prints results for both models
summary(lm_infant)
```

::: {.cell-output .cell-output-stdout}

```

Call:
lm(formula = life_expectancy ~ infant_mortality, data = africa_2000)

Residuals:
     Min       1Q   Median       3Q      Max 
-22.6651  -3.7087   0.9914   4.0408   8.6817 

Coefficients:
                 Estimate Std. Error t value Pr(>|t|)    
(Intercept)      71.29331    2.42611  29.386  < 2e-16 ***
infant_mortality -0.18916    0.02869  -6.594 2.83e-08 ***
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 6.221 on 49 degrees of freedom
Multiple R-squared:  0.4701,	Adjusted R-squared:  0.4593 
F-statistic: 43.48 on 1 and 49 DF,  p-value: 2.826e-08
```


:::

```{.r .cell-code}
summary(lm_population)
```

::: {.cell-output .cell-output-stdout}

```

Call:
lm(formula = life_expectancy ~ population, data = africa_2000)

Residuals:
    Min      1Q  Median      3Q     Max 
-18.429  -4.602  -2.568   3.800  18.802 

Coefficients:
             Estimate Std. Error t value Pr(>|t|)    
(Intercept) 5.593e+01  1.468e+00  38.097   <2e-16 ***
population  2.756e-08  5.459e-08   0.505    0.616    
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 8.524 on 49 degrees of freedom
Multiple R-squared:  0.005176,	Adjusted R-squared:  -0.01513 
F-statistic: 0.2549 on 1 and 49 DF,  p-value: 0.6159
```


:::
:::


The relationship between life expectancy and infant mortality are highly significant, and negatively correlated. The negative correlation is indicated by the negative slope. The relationship between population size and life expectancy is not significant because the p-value is 0.6159.


## Additional contribution

This section contributed by Kexin (Cassie) Cui.

### Data overview
Dataset picked from dslabs: admissions

::: {.cell}

```{.r .cell-code}
# Load required packages
library(dplyr)    
library(ggplot2) 

# Load the dataset into the session
data("admissions") 

# Preview the first 6 rows
head(admissions) 
```

::: {.cell-output .cell-output-stdout}

```
  major gender admitted applicants
1     A    men       62        825
2     B    men       63        560
3     C    men       37        325
4     D    men       33        417
5     E    men       28        191
6     F    men        6        373
```


:::

```{.r .cell-code}
# Get basic summary statistics for each column
summary(admissions) 
```

::: {.cell-output .cell-output-stdout}

```
    major              gender             admitted       applicants   
 Length:12          Length:12          Min.   : 6.00   Min.   : 25.0  
 Class :character   Class :character   1st Qu.:27.00   1st Qu.:291.5  
 Mode  :character   Mode  :character   Median :34.50   Median :374.0  
                                       Mean   :39.92   Mean   :377.2  
                                       3rd Qu.:62.25   3rd Qu.:452.8  
                                       Max.   :82.00   Max.   :825.0  
```


:::

```{.r .cell-code}
# Check for missing values in each column
colSums(is.na(admissions)) 
```

::: {.cell-output .cell-output-stdout}

```
     major     gender   admitted applicants 
         0          0          0          0 
```


:::
:::


### Descriptive analysis and visualization


::: {.cell}

```{.r .cell-code}
# Compute total applicants and mean admission percentage by gender
admissions |> 
  group_by(gender) |> 
  summarize(
    total_applicants   = sum(applicants), 
    mean_admitted_pct  = mean(admitted), 
    .groups = "drop"           
  )
```

::: {.cell-output .cell-output-stdout}

```
# A tibble: 2 × 3
  gender total_applicants mean_admitted_pct
  <chr>             <dbl>             <dbl>
1 men                2691              38.2
2 women              1835              41.7
```


:::

```{.r .cell-code}
ggplot(admissions, aes(x = major, y = applicants, fill = gender)) +
  geom_col(position = "dodge") +
  labs(
    x = "Major",
    y = "Number of applicants",
    fill = "Gender"
  )
```

::: {.cell-output-display}
![](starter-analysis-exercise_files/figure-html/unnamed-chunk-5-1.png){width=672}
:::

```{.r .cell-code}
# Plot applicants by major, faceted by gender
ggplot(admissions, aes(x = major, y = applicants)) + 
  geom_col() +             
  facet_wrap(~ gender) +                             # separate panels by gender
  labs(
    x = "Major",                                     
    y = "Number of applicants"                      
  )
```

::: {.cell-output-display}
![](starter-analysis-exercise_files/figure-html/unnamed-chunk-5-2.png){width=672}
:::

```{.r .cell-code}
# Plot admission percentage by major and gender
ggplot(admissions, aes(x = major, y = admitted, group = gender)) + 
  geom_point(size = 2) +                  
  geom_line() +                                                  
  facet_wrap(~ gender) + 
  labs(
    x = "Major",                                                 
    y = "Admission percentage"                           
  )
```

::: {.cell-output-display}
![](starter-analysis-exercise_files/figure-html/unnamed-chunk-5-3.png){width=672}
:::
:::



### Binomial logistic regression for admission outcome


::: {.cell}

```{.r .cell-code}
# Create integer counts for admitted and rejected applicants
admissions_glm <- admissions |>
  mutate(
    admitted_num = round(admitted * applicants / 100),  
    rejected_num = applicants - admitted_num   
  )

# Fit a binomial logistic regression model
# Outcome: number admitted out of total applicants
# Predictors: gender and major
glm1 <- glm(
  cbind(admitted_num, rejected_num) ~ gender + major,
  family = binomial(link = "logit"),
  data = admissions_glm
)

# Display model results
summary(glm1)
```

::: {.cell-output .cell-output-stdout}

```

Call:
glm(formula = cbind(admitted_num, rejected_num) ~ gender + major, 
    family = binomial(link = "logit"), data = admissions_glm)

Coefficients:
            Estimate Std. Error z value Pr(>|z|)    
(Intercept)  0.58205    0.06899   8.436   <2e-16 ***
genderwomen  0.09987    0.08085   1.235    0.217    
majorB      -0.04340    0.10984  -0.395    0.693    
majorC      -1.26260    0.10663 -11.841   <2e-16 ***
majorD      -1.29461    0.10582 -12.234   <2e-16 ***
majorE      -1.73931    0.12611 -13.792   <2e-16 ***
majorF      -3.30648    0.16998 -19.452   <2e-16 ***
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

(Dispersion parameter for binomial family taken to be 1)

    Null deviance: 877.056  on 11  degrees of freedom
Residual deviance:  20.204  on  5  degrees of freedom
AIC: 103.14

Number of Fisher Scoring iterations: 4
```


:::
:::


After fitting a binomial logistic regression model, gender was not a significant predictor of admission probability after adjusting for major (p = 0.217). In contrast, admission rates differed substantially across majors, with several majors showing much lower odds of admission compared to Major A (p < 0.001). The large reduction in deviance indicates that major explains most of the variation in admission outcomes.
