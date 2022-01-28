---
title:  "R Exercise: Working with Data from JSON API and Performing EDA"
date:   2022-02-11 01:29:17 +0545
categories: R Exercise
tags:
  - Data Analysis
  - R
header:
  teaser: "assets/r_exercise/json_api/output_78_0.png"
  overlay_image: "assets/r_exercise/json_api/output_78_0.png"
toc: true
---
##  Import any data from JSON API 

We are using data from https://data.askbhunte.com/api/v1/covid.

We are going to use below packages.

* `jsonlite` : It implements a bidirectional mapping between JSON data and the most important R data types.
* `RCurl` : Which help to provides the necessary tools for accessing URIs, data and services via HTTP.


```R
install.packages('RCurl')

```

    Installing package into ‘/usr/local/lib/R/site-library’
    (as ‘lib’ is unspecified)
    
    also installing the dependency ‘bitops’
    
    
    


```R
library(jsonlite)
library(RCurl)
url <- getURL("https://data.askbhunte.com/api/v1/covid",
.opts=list(followlocation=TRUE, ssl.verifyhost=FALSE, ssl.verifypeer=FALSE))


```

## Now, save the imported data as "covidtbl" data frame in R



```R
covidtbl <- fromJSON(txt=url, flatten=TRUE)
#covidtbl 
```

## Check whether the saved "covidtbl" data passes the three conditions of the "tidy" data or not! If not, make it a tidy data with explanations of rows, columns and cells in the data

The three conditions of tidy data are,

*  Each variable must have its own column
* Each observation must have its own row
* Each value must have its own cell.

Apply these condition to our covidtbl data set satisfy all the conditions mention above so, without a doubt our dataset is tidy data.



```R
covidtbl
```

## Check if there are duplicate cases in the data using "id" variable, remove duplicate cases, if found, using R base functions: duplicated or unique

Function `duplicated()` ensure that wether there is present of duplicated value or not. If duplicate value is found it return `TRUE` other wise `FALSE`. So, in our care there no present of duplicated values.

similarly function `unique()` is used to erase the duplicated value or to find the unique value in dataframe.


```R
duplicated(covidtbl)
```


```R
unique(covidtbl)
```

## Clean the "gender" variable and show the number and percentage of males and females in the data

We must take care of following points while cleaning our data,

* Free of duplicate rows/values
* Error-free (e.g. free of misspellings)
* Relevant (e.g. free of special characters)
* The appropriate data type for analysis
* Free of outliers (or only contain outliers have been identified/understood), and
* Follows a “tidy data” structure

In case of our data there are some missing value as well as starting letter of some data are in small letter or in capital letter. To slove this problem we install the package 

`stringer` : It is used to convert the first letter of every word of a string to Uppercase and the rest of the letters are converted to lower case.


```R
install.packages("stringr")
```

    Installing package into ‘/usr/local/lib/R/site-library’
    (as ‘lib’ is unspecified)
    
    

Following code loads the stringr library and remove the missing values present in our gender column.


```R
df<- covidtbl[complete.cases(covidtbl$gender),]



```

In following case, first load the string library and then change all the gender data in upper case and by using `str_to_title()` function change all letter except first to lower case.


```R
library(stringr)
df <-toupper(df$gender)
df <- str_to_title(df)

```

Now, it is time to calculate total number of male and female from gender column.


```R
df1<- table(df)
df1
```


    df
    Female   Male 
     21403  56355 


To find the percentage of male and female we can do,


```R
prop.table(df1)
```


    df
       Female      Male 
    0.2752514 0.7247486 


##  Clean the "age" variable and show the summary statistics of the age variable
In our age column there are so many missing value. First we should remove the missing values.


```R

df_age <- covidtbl[complete.cases(covidtbl$age),]
age <- df_age$age

age

```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>28</li><li>34</li><li>26</li><li>29</li><li>20</li><li>72</li><li>60</li><li>24</li><li>58</li><li>52</li><li>41</li><li>41</li><li>34</li><li>41</li><li>28</li><li>28</li><li>28</li><li>22</li><li>25</li><li>40</li><li>33</li><li>18</li><li>65</li><li>32</li><li>20</li><li>37</li><li>55</li><li>36</li><li>55</li><li>19</li><li>65</li><li>21</li><li>34</li><li>65</li><li>81</li><li>19</li><li>27</li><li>32</li><li>57</li><li>26</li><li>44</li><li>35</li><li>9</li><li>32</li><li>34</li><li>50</li><li>25</li><li>62</li><li>21</li><li>34</li><li>40</li><li>55</li><li>60</li><li>30</li><li>55</li><li>29</li><li>65</li><li>80</li><li>17</li><li>60</li><li>26</li><li>27</li><li>58</li><li>60</li><li>52</li><li>30</li><li>65</li><li>37</li><li>4</li><li>35</li><li>11</li><li>40</li><li>22</li><li>24</li><li>65</li><li>32</li><li>18</li><li>18</li><li>38</li><li>45</li><li>63</li><li>30</li><li>25</li><li>27</li><li>28</li><li>28</li><li>45</li><li>32</li><li>60</li><li>16</li><li>61</li><li>22</li><li>24</li><li>25</li><li>28</li><li>28</li><li>32</li><li>59</li><li>55</li><li>61</li><li>22</li><li>28</li><li>32</li><li>32</li><li>4</li><li>10</li><li>28</li><li>20</li><li>35</li><li>22</li><li>40</li><li>18</li><li>36</li><li>32</li><li>27</li><li>25</li><li>25</li><li>22</li><li>49</li><li>36</li><li>29</li><li>20</li><li>28</li><li>23</li><li>30</li><li>36</li><li>75</li><li>36</li><li>9</li><li>23</li><li>47</li><li>10</li><li>28</li><li>29</li><li>65</li><li>17</li><li>18</li><li>18</li><li>30</li><li>36</li><li>37</li><li>26</li><li>25</li><li>25</li><li>32</li><li>25</li><li>48</li><li>39</li><li>48</li><li>28</li><li>30</li><li>33</li><li>21</li><li>25</li><li>25</li><li>29</li><li>42</li><li>21</li><li>30</li><li>22</li><li>18</li><li>19</li><li>19</li><li>22</li><li>23</li><li>20</li><li>28</li><li>30</li><li>40</li><li>27</li><li>42</li><li>41</li><li>51</li><li>27</li><li>37</li><li>26</li><li>26</li><li>28</li><li>30</li><li>46</li><li>17</li><li>18</li><li>53</li><li>55</li><li>22</li><li>22</li><li>45</li><li>74</li><li>19</li><li>35</li><li>34</li><li>35</li><li>24</li><li>30</li><li>27</li><li>34</li><li>19</li><li>38</li><li>45</li><li>27</li><li>⋯</li><li>62</li><li>73</li><li>53</li><li>67</li><li>54</li><li>56</li><li>33</li><li>58</li><li>62</li><li>74</li><li>47</li><li>30</li><li>67</li><li>29</li><li>65</li><li>51</li><li>30</li><li>64</li><li>66</li><li>66</li><li>76</li><li>74</li><li>22</li><li>88</li><li>48</li><li>66</li><li>41</li><li>82</li><li>31</li><li>75</li><li>77</li><li>65</li><li>70</li><li>70</li><li>62</li><li>50</li><li>32</li><li>23</li><li>37</li><li>90</li><li>83</li><li>76</li><li>69</li><li>39</li><li>63</li><li>59</li><li>87</li><li>62</li><li>35</li><li>34</li><li>86</li><li>54</li><li>82</li><li>76</li><li>67</li><li>39</li><li>56</li><li>65</li><li>83</li><li>52</li><li>55</li><li>45</li><li>51</li><li>52</li><li>71</li><li>72</li><li>72</li><li>92</li><li>77</li><li>40</li><li>77</li><li>65</li><li>40</li><li>70</li><li>50</li><li>20</li><li>74</li><li>88</li><li>65</li><li>72</li><li>86</li><li>65</li><li>74</li><li>55</li><li>89</li><li>70</li><li>75</li><li>55</li><li>18</li><li>65</li><li>20</li><li>70</li><li>47</li><li>40</li><li>97</li><li>60</li><li>60</li><li>72</li><li>80</li><li>67</li><li>40</li><li>75</li><li>35</li><li>70</li><li>64</li><li>45</li><li>77</li><li>73</li><li>80</li><li>67</li><li>83</li><li>38</li><li>61</li><li>76</li><li>43</li><li>78</li><li>85</li><li>51</li><li>45</li><li>70</li><li>59</li><li>83</li><li>55</li><li>62</li><li>85</li><li>70</li><li>61</li><li>73</li><li>47</li><li>40</li><li>73</li><li>55</li><li>63</li><li>72</li><li>60</li><li>55</li><li>36</li><li>61</li><li>55</li><li>55</li><li>58</li><li>35</li><li>64</li><li>86</li><li>34</li><li>96</li><li>66</li><li>69</li><li>20</li><li>61</li><li>62</li><li>50</li><li>51</li><li>50</li><li>34</li><li>38</li><li>47</li><li>86</li><li>60</li><li>66</li><li>85</li><li>50</li><li>59</li><li>72</li><li>49</li><li>58</li><li>61</li><li>17</li><li>68</li><li>88</li><li>58</li><li>73</li><li>84</li><li>62</li><li>55</li><li>52</li><li>63</li><li>50</li><li>34</li><li>75</li><li>78</li><li>55</li><li>50</li><li>39</li><li>68</li><li>70</li><li>32</li><li>84</li><li>39</li><li>73</li><li>75</li><li>51</li><li>58</li><li>72</li><li>60</li><li>70</li><li>57</li><li>53</li><li>39</li><li>76</li></ol>



Now, we removed the NA values. To show summary statistics of the age,


```R
summary(age)
```


       Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
       1.00   23.00   35.00   38.93   53.00  523.00 


Looking at summary statistics of age minimum age of people in covidbl table is 1, 
* first quartile is 23 
* median age of group is 35 
* average age of people is 38.93 
* third quartile age group is 53 
* maximum age group of people in this table is 523.

## Transform cleaned age variable into broad age groups i.e. <15, 15-59, 60+ years, define it as factor variable and get number and percentage of this variable


```R
less_then_15 <- df_age$age < 15
below_15<- df_age[less_then_15,]$age
below_15<- factor(below_15)
table(below_15)

```


    below_15
     1  2  3  4  5  6  7  8  9 10 11 12 13 14 
     4  8  2 12  5  5  4  7  6  5  5  5  3  6 



```R
prop.table(table(below_15))*100

```


    below_15
            1         2         3         4         5         6         7         8 
     5.194805 10.389610  2.597403 15.584416  6.493506  6.493506  5.194805  9.090909 
            9        10        11        12        13        14 
     7.792208  6.493506  6.493506  6.493506  3.896104  7.792208 



```R
between_15_59 <- (df_age$age <= 59)
between_15_59<- df_age[between_15_59,]$age
between_15_59 <- between_15_59[between_15_59>=15]
between_15_59<- factor(between_15_59)
table(between_15_59)

```


    between_15_59
    15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 
    11 19 27 50 35 47 24 45 34 24 47 26 36 32 21 43 16 36 14 31 41 34 17 24 16 48 
    41 42 43 44 45 46 47 48 49 50 51 52 53 54 55 56 57 58 59 
    18 14  6  3 34 11  8 14  9 28 13 14  9 10 27  8  7 16 11 



```R
prop.table(table(between_15_59))*100
```


    between_15_59
           15        16        17        18        19        20        21        22 
    1.0396975 1.7958412 2.5519849 4.7258979 3.3081285 4.4423440 2.2684310 4.2533081 
           23        24        25        26        27        28        29        30 
    3.2136106 2.2684310 4.4423440 2.4574669 3.4026465 3.0245747 1.9848771 4.0642722 
           31        32        33        34        35        36        37        38 
    1.5122873 3.4026465 1.3232514 2.9300567 3.8752363 3.2136106 1.6068053 2.2684310 
           39        40        41        42        43        44        45        46 
    1.5122873 4.5368620 1.7013233 1.3232514 0.5671078 0.2835539 3.2136106 1.0396975 
           47        48        49        50        51        52        53        54 
    0.7561437 1.3232514 0.8506616 2.6465028 1.2287335 1.3232514 0.8506616 0.9451796 
           55        56        57        58        59 
    2.5519849 0.7561437 0.6616257 1.5122873 1.0396975 



```R
greater_than_60 <- df_age$age >= 60
above_60 <- df_age[greater_than_60,]$age
above_60 <- factor(above_60)
print(above_60)
```

      [1] 72  60  65  65  65  81  62  60  65  80  60  60  65  65  63  60  61  61 
     [19] 75  65  74  69  70  62  60  60  60  76  76  60  70  60  74  85  65  85 
     [37] 83  72  61  62  82  77  61  68  74  68  85  69  75  62  60  64  60  72 
     [55] 75  73  67  78  65  64  62  60  84  62  70  72  78  68  523 60  63  70 
     [73] 77  80  84  75  60  70  60  60  60  70  60  60  68  65  70  65  65  82 
     [91] 75  63  78  70  62  70  76  64  72  65  68  65  68  60  70  64  80  85 
    [109] 71  75  78  67  72  61  60  62  60  63  82  79  80  82  85  73  68  76 
    [127] 71  74  87  60  76  60  81  77  65  65  70  64  69  65  76  68  60  70 
    [145] 70  71  74  65  70  68  77  62  73  67  62  74  67  65  64  66  66  76 
    [163] 74  88  66  82  75  77  65  70  70  62  90  83  76  69  63  87  62  86 
    [181] 82  76  67  65  83  71  72  72  92  77  77  65  70  74  88  65  72  86 
    [199] 65  74  89  70  75  65  70  97  60  60  72  80  67  75  70  64  77  73 
    [217] 80  67  83  61  76  78  85  70  83  62  85  70  61  73  73  63  72  60 
    [235] 61  64  86  96  66  69  61  62  86  60  66  85  72  61  68  88  73  84 
    [253] 62  63  75  78  68  70  84  73  75  72  60  70  76 
    35 Levels: 60 61 62 63 64 65 66 67 68 69 70 71 72 73 74 75 76 77 78 79 ... 523
    

## Number of days between recovered and reported dates, clean it if required, and get the summary statistics of this variable

In column reportedOn and reportedOn we can see many values are missing so our  first attempt is removing these values and then our columns are in string format another task to do is change them in date formate finally difference is calculate.


```R
colnames(covidtbl)
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>'id'</li><li>'province'</li><li>'district'</li><li>'municipality'</li><li>'createdOn'</li><li>'modifiedOn'</li><li>'label'</li><li>'gender'</li><li>'age'</li><li>'occupation'</li><li>'reportedOn'</li><li>'recoveredOn'</li><li>'deathOn'</li><li>'currentState'</li><li>'isReinfected'</li><li>'source'</li><li>'comment'</li><li>'type'</li><li>'nationality'</li><li>'ward'</li><li>'relatedTo'</li><li>'point.type'</li><li>'point.coordinates'</li></ol>




```R
covidtbl_2 <-covidtbl[complete.cases(covidtbl$recoveredOn),]
date_of_recoveredOn <-as.Date(covidtbl_2$recoveredOn)
covidtbl_1 <-covidtbl[complete.cases(covidtbl$reportedOn),]
date_of_reportedOn<- as.Date(covidtbl_2$reportedOn)

diff1<- date_of_recoveredOn - date_of_reportedOn
#print(diff1)

```


```R
fivenum(diff1)
```


    Time differences in days
    [1]   0   1  15  27 179


From the above fivenum summary average days different between recovered and reported dates is 15 and median days difference is 27 similarly maximum days difference is 179. Data are highly skewed.

## Number of days between deaths and reported dates, and summary statistics of this variable



```R
covidtbl_3 <-covidtbl[complete.cases(covidtbl$deathOn),]
death_date <- covidtbl_3$deathOn

death_date<- as.Date(death_date)
diff2 <- death_date - date_of_reportedOn
#list(diff2)

```

    Warning message in unclass(time1) - unclass(time2):
    “longer object length is not a multiple of shorter object length”
    


```R
fivenum(diff2) 

```


    Time differences in days
    [1] -135   -8   16   53  156


From above data we can see that average days difference beween deaths and reported dates is 16 and median days different beween corresponding variable is 53 maximum days difference is 156.

## Which measures of central tendency and dispersion is most appropriate for the age, diff1 and diff2 variables? 

In case of age median is appropriate measure of central tendency. Because of following reasons.

* There are a few extreme scores in the distribution of the data. (NOTE: R
* single outlier can have a great effect on the mean.
* There are some missing or undetermined values in your data. c.
* There is an open ended distribution  
Corresponding measure of dispersion for age is IQR.

In case of diff1  median is approprate measure of central tendency. Because while watching data there are negative value, extermely differnt values. And corresponding measure of disperson is IQR.

Similarly, for diff2 data are skewed more so appropriate measure of central tendency is median and corresponding measure of dispersion is IRQ.

 


```R
hist(df_age$age, xlim=c(1,100), ylim=c(0,300), breaks = 100)
```


    
![png]({{site.url}}/assets/r_exercises/json_api/output_41_0.png)
    


From histogram above we can notice that age groups with heigest frequency belong to the interval 20 - 40.


```R
summary(age)
```


       Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
       1.00   23.00   35.00   38.93   53.00  523.00 



```R
boxplot(age)
```


    
![png]({{site.url}}/assets/r_exercises/json_api/output_44_0.png)
    


From boxt plot we can see minimum value of age are 1 average value is appromately 39. We can see that there is presence of outliers.


```R
hist(as.numeric(diff1))
```


    
![png]({{site.url}}/assets/r_exercises/json_api/output_46_0.png)
    



```R
colnames(covidtbl)
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>'id'</li><li>'province'</li><li>'district'</li><li>'municipality'</li><li>'createdOn'</li><li>'modifiedOn'</li><li>'label'</li><li>'gender'</li><li>'age'</li><li>'occupation'</li><li>'reportedOn'</li><li>'recoveredOn'</li><li>'deathOn'</li><li>'currentState'</li><li>'isReinfected'</li><li>'source'</li><li>'comment'</li><li>'type'</li><li>'nationality'</li><li>'ward'</li><li>'relatedTo'</li><li>'point.type'</li><li>'point.coordinates'</li></ol>



## Number and percentage of the "current state" variable


```R
current_state <- covidtbl$currentState
num_current_sate<-table(current_state)
```


```R
prop.table(num_current_sate)*100
```


    current_state
       active     death recovered 
    26.846319  0.639963 72.513718 


Current state variable have three types of values active, death, recovered and about 72% people are recovered similarly approximately 27% people have covid posite and as compared to recoved ratio only 0.63% were deaths. From the data above maximum people can recovered from covid.

## Number and percentage of the "isReinfected" variable, what percentage of cases were re-infected in Nepal at the given time period in the database? Was it realistic?


```R
isreinfected <- covidtbl$isReinfected
num_isreinfected <- table(isreinfected)
prop.table(num_isreinfected)*100
```


    isreinfected
           FALSE         TRUE 
    99.996144801  0.003855199 


About 0.0038% people were reinfected from covid In Nepal. That ratio is too small few of the recovered people might be reinfected.

## Number and percentage of "type" variable


```R
type <- covidtbl$type
type_count <- table(type)
prop.table(type_count)*100

```


    type
              imported local_transmission 
              57.89474           42.10526 


## Number and percentage of "nationality" variable


```R
nationality <- covidtbl$nationality
covidtbl_4<- covidtbl[complete.cases(covidtbl$nationality),]
currted_nationality <- covidtbl_4$nationality
nationality_count <- table(currted_nationality)
print(nationality_count)
prop.table(nationality_count)*100
```

    currted_nationality
     2  3  4 
    42 14  1 
    


    currted_nationality
            2         3         4 
    73.684211 24.561404  1.754386 


Nationality column is also suffered from missing values. Due to the missing values our analysis might not be accurate.

##  Cross-tabulation of province (row variable) and current status (column variable) with row percentage


```R
cross_tabul<- table(covidtbl$province, covidtbl$currentState)
cross_tabul
```


       
        active death recovered
      1    643    56      6276
      2   1825   133     13061
      3  13086   187     16462
      4   1108    28      3293
      5   2496    76      8563
      6    593     5      2950
      7   1140    13      5823



```R
prop.table(cross_tabul)*100
```


       
              active        death    recovered
      1  0.826297596  0.071963710  8.065075755
      2  2.345245897  0.170913811 16.784250228
      3 16.816376884  0.240307388 21.154760528
      4  1.423853400  0.035981855  4.231723145
      5  3.207525348  0.097665035 11.004022257
      6  0.762044283  0.006425331  3.790945423
      7  1.464975519  0.016705861  7.482940746


Maximum corona active were in provience 3, minimum corona active were in provience 6 similarly maximum people were died from corona in provience 3 also maximum people recovered from coron in same provience.

## Cross-tabulation of sex (row variable) and current status (column variable) with row percentage


```R
gender<- covidtbl$gender
gender <- str_to_title(gender)
cross_tabul<- table(gender, covidtbl$currentState)
cross_tabul
```


            
    gender   active death recovered
      Female   6960   149     14294
      Male    13931   348     42076



```R
prop.table(cross_tabul)*100
```


            
    gender       active      death  recovered
      Female  8.9508475  0.1916202 18.3826745
      Male   17.9158415  0.4475424 54.1114741


Male were affected from corona more than female similarly death, recovered ratio of male is maximum than female.

## Cross-tabulation of broad age groups (row variable) and current status (column variable) with row percentage


```R
combined <- unlist(list(below_15,above_60, between_15_59))
borad_age <- as.numeric(combined)
```


```R
cross_tabul<- table(borad_age, df_age$currentState)
cross_tabul
```

Above data show that death rate of broad age above 60 is maximum compared to the others. Recovered rate of broad age group between 15 to 59 is maximum compared others.

## Scatterplot of province (x-axis) and cleaned age (y-axis) and appropriate correlation coefficient for this bi-variate data


```R
plot(covidtbl$province,covidtbl$age)
```


    
![png]({{site.url}}/assets/r_exercises/json_api/output_73_0.png)
    


Scatter plot does not show any specific pattern, it is not linear so in above case spearman rank correlation is appropriate.


```R
cor.test(covidtbl$province,covidtbl$age, method = "spearman")
```

    Warning message in cor.test.default(covidtbl$province, covidtbl$age, method = "spearman"):
    “Cannot compute exact p-value with ties”
    


    
    	Spearman's rank correlation rho
    
    data:  covidtbl$province and covidtbl$age
    S = 509628932, p-value = 1.796e-05
    alternative hypothesis: true rho is not equal to 0
    sample estimates:
           rho 
    -0.1143495 
    


There is low degree of negative correlation

## Scatterplot of age (x-axis) and diff1 (y-axis) and appropriate correlation coefficient


```R
plot(covidtbl$age,diff1)
```


    
![png]({{site.url}}/assets/r_exercises/json_api/output_78_0.png)
    


Above scatterplot do not show any specific pattern so spearman rank correlation coefficent is appropriate.


```R
cor.test(covidtbl$age,as.numeric(diff1), method = "spearman")
```

    Warning message in cor.test.default(covidtbl$age, as.numeric(diff1), method = "spearman"):
    “Cannot compute exact p-value with ties”
    


    
    	Spearman's rank correlation rho
    
    data:  covidtbl$age and as.numeric(diff1)
    S = 592527576, p-value < 2.2e-16
    alternative hypothesis: true rho is not equal to 0
    sample estimates:
           rho 
    -0.2956149 
    


Between age and difference there is low degree of negative correlation.
 
