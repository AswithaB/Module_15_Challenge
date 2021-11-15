# Module 15 Challenge - AutosRUs MechaCar Statistical Analysis - Statistics and R

## Overview

### Purpose

The purpose of this project is to analyze production difficulties
of AutoRUs' newest prototype, the MechaCar.

Production data will be analyzed statistically to look for insights
that may help the manufacturing team to alleviate production difficulties.

### Tasks

1. Perform multiple linear regression analysis to identify which variables in the dataset predict the mpg of MechaCar prototypes.
2. Collect summary statistics on the pounds per square inch (PSI) of the suspension coils from the manufacturing lots.
3. Run t-tests to determine if the manufacturing lots are statistically different from the mean population.
4. Design a statistical study to compare vehicle performance of the MechaCar vehicles against vehicles from other manufacturers.
5. Write a summary interpretation for each statistical analysis (here, in this README.md)

### Approach

- Use R and RStudio for this internal analysis.

### Deliverables

1. Linear Regression to Predict MPG
2. Summary Statistics on Suspension Coils
3. T-Test on Suspension Coils
4. Design a Study Comparing the MechaCar to the Competition

### Deliverable 1

#### Linear Regression to Predict MPG

After the `MechaCar_mpg.csv` data was imported into R, a Multiple Linear Regression was performed
using all of the other measured quantities in the dataset to see which, if any, independent variables had an impact on the Miles-per-Gallon (mpg) of the MechaCar.

The summary output from this Multiple Linear Regression is shown here:

![Multiple Linear Regression Summary](Images/Linear_Model_Summary.png "Linear Model Summary")

As an aid in interpretation, simplified Univariate Linear Regressions were also performed on the 4 Independent Variables with Continuous Measures (`vehicle_length`, `vehicle_weight`, `spoiler_angle`, and `ground_clearance`),
and a pair of boxplots was generated for the `AWD` which is a Boolean Independent Variable. Since Multiple Linear Regressions are difficult if not impossible to visualize, these simplified models will be useful to refer back
to when interpreting the results from the Multiple Linear Regression above.

Plots of these linear regressions are shown here in Figure 1, reproduced as a Gallery in Miniature.

(Full-Size Versions are Archived in `Images` Directory of this GitHub Repository)

**Figure 1: Linear Regressions and Boxplots for Independent Variables in `MechaCar_mpg.csv`**

![Figure 1](Images/Figure_00.png "Figure 1")

- Q: Which variables/coefficients provided a non-random amount of variance to the mpg values in the dataset?
	- A: For this project, we are starting with a baseline p-Value Significance Level of 0.05. With this in mind, looking at the summary output of the Multiple Linear Regression,
	`vehicle_length` and `ground_clearance` provide a non-random amount of variance to the mpg values. `vehicle_weight` also has a level of non-random contribution, but it is slightly
	above our 0.05 cutoff. This interpretation is backed up by consulting our series of Univariate Linear Regressions, where Vehicle Length and Ground Clearance both show positive
	correlation to mpg, with the highest Coefficient of Determination (r-squared) values among the variables modeled.

- Q: Is the slope of the linear model considered to be zero? Why or why not?
	- A: No, the slope of the linear model is not considered to be zero. This is because the two values that provide a non-random amount of variance to the mpg values
	have non-zero slopes for their regression equations.

- Q: Does this linear model predict mpg of MechaCar prototypes effectively? Why or why not?
	- A: Yes, this linear model effectively predicts the mpg of MechaCar prototypes. With a Combined Coefficient of Determination of 0.7, this shows that 70% of the variation of mpg values
	can be attributed to the 5 variables modeled against mpg. This result is better than chance, and would be a good starting point for helping to guide engineering decisions for
	future prototypes, if maximizing mpg was a stated design outcome.

### Deliverable 2

#### Summary Statistics on Suspension Coils

After the `Suspension_Coil.csv` data was imported into R, summary statistics were generated for the quality control test results, for all samples overall, and grouped by Lot Number.

These summary statistics are shown below in Figures 2 & 3.

**Figure 2: Summary Statistics for All Suspension Coils**

![Figure 2](Images/total_summary.png "Figure 2")

**Figure 3: Summary Statistics for All Suspension Coils, Grouped by Lot Number**

![Figure 3](Images/lot_summary.png "Figure 3")

- Q: The design specifications for the MechaCar suspension coils dictate that the variance of the suspension coils must not exceed 100 pounds per square inch. Does the current manufacturing data meet this design specification for all manufacturing lots in total and each lot individually? Why or why not?
	- A: **Yes**, According to the current manufacturing data, all lots in total do meet this design specification. This can be seen above in Figure 2.
	- However, if the lots are examined individually, **No**, Lot 3 does not meet this design specification, as shown above in Figure 3.
	- This is because if all samples are examined at once, there are enough coils within specification in Lots 1 and 2 to average out the variance present in Lot 3,
	so that the overall variance is within the specification of being under 100 pounds per square inch.

### Deliverable 3

#### T-Tests on Suspension Coils

Another alternative to compare manufacturing lots against the population is to implement a series of statistical t-tests which compare means of a sample from a population of data against the mean of the population of data as a whole.

For reference purposes, the population size for the Suspension Coils is 150, and all sample sizes are 50.

As a baseline to look at a sampling of the original population first, 50 random samples were taken from the population and a t-test was implemented using this random sample.

Following this, Lot 1, Lot 2, and Lot 3 were each also tested against the population.

As before, we will continue to utilize a p-Value Significance Level of 0.05.

According to these tests, for the 50 Random Samples we fail to reject the Null Hypothesis, meaning that the means are statistically similar. For Lot 1, we reject the Null Hypothesis and determine that the mean of the
sample is not statistically similar to the mean of the population. For Lot 2, we reject the Null Hypothesis and determine that the mean of the sample is not statistically similar to the mean of the population. For Lot 3,
we fail to reject the Null Hypotheses and determine that the means are statistically similar.

It should be noted that the t-test is only used to compare the means of a sample versus a population, under the assumption that the variances are similar. As was demonstrated above in Deliverable 2,
in this case the variances of these samples are not in fact similar, therefore the conclusions drawn from these t-tests results should bear that fact in mind and remember that with the exception of the means, these
sample and population distributions are not otherwise similar.

The results obtained are summarized here in Table 1.

**Table 1: Summary of t-test Results**
| Sample           | Mean          | Population Mean     | p-value      | Test Outcome
|------------------|---------------|---------------------|--------------|-------------
| 50 Random        | 1499.76       | 1498.78             | 0.306        | Fail to reject Null Hypothesis. Means are statistically similar.
| Lot1             | 1500.00       | 1498.78             | 1.568e-11    | Reject Null Hypothesis. Means are NOT statistically similar.
| Lot2             | 1500.20       | 1498.78             | 0.0005911    | Reject Null Hypothesis. Means are NOT statistically similar.
| Lot3             | 1496.14       | 1498.78             | 0.1589       | Fail to reject Null Hypothesis. Means are statistically similar.

Screenshots of the 4 t-tests are shown here to provide additional information than is summarized above in Table 3.

**Figure 4: t-test Results on 50 Random Samples**

![Figure 4](Images/t-test_50_Random_Samples.png "Figure 4")

**Figure 5: t-test Results for Lot 1**

![Figure 5](Images/t-test_Lot1.png "Figure 5")

**Figure 6: t-test Results for Lot 2**

![Figure 6](Images/t-test_Lot2.png "Figure 6")

**Figure 7: t-test Results for Lot 3**

![Figure 7](Images/t-test_Lot3.png "Figure 7")

### Deliverable 4

#### Study Design: MechaCar vs Competition

How do the MechaCar Prototypes stack up against their competition? What metrics will we use to guide
our final design decisions as the MechaCar moves from the Prototype stage into Regular Production?

- Q: What metric or metrics will be tested?
	- A: Despite what features and style of automobiles are being marketed to American consumers, we Hypothesize that their buying decisions can
	reliably be predicted by a combination of **Cost** and **City Fuel Efficiency**.

- Q: What is the Null Hypothesis or Alternative Hypothesis?
	- A: To test our Hypothesis, we will need to specify a Null Hypothesis.

	Namely: There is no statistical correlation between Number of Vehicle Units sold within a given year and vehicle Model
	and either that vehicle Model's **Cost** or **City Fuel Efficiency**.

- Q: What statistical test(s) will be used and why?
	- A: In order to test our Hypothesis, we will use a series of Paired Two-Sample t-tests, Two-Way Analysis of Variance, and Multiple Linear Regression. For all tests where
	p-value carries significance, a significance level of 0.05 will be used.

	The Paired Two-Sample t-tests will help to determine variability between Cost and City Fuel Efficiency of different Vehicle Models. Analysis of Variance will help us to
	measure how closely the different Independent Variables correlate to the Dependent Variable of Number of Vehicle Model Units Sold. Multiple Linear Regression will help
	us to quantify and predict which Cost and City Fuel Efficiency design goals should be implemented to achieve a desired outcome in Number of Vehicle Units Sold.


- Q: What data is needed?
	- A: In order to test our Hypothesis, we will need to combine data from a few different sources. To narrow the scope of our study, we will limit our analysis to
	the most recent complete 5 year periods prior to the COVID-19 Pandemic, or Calendar Year 2015-2020 in the Continental United States.
	
	Baseline data for Total Auto Unit Sales can be obtained from the US Bureau of Economic Analysis. Additional Internal Estimations May have to be performed to
	classify these Total Auto Unit Sales Figures into separate Vehicle Classes.

	City Fuel Economy Data can be obtained from the US Environmental Protection Agency.

	Cost Data (meaning "Actual Sales Price") can be obtained from Black Book API (current pricing unknown, but the data **IS** theoretically available).

-- END --
