# Parkinsons-Data-Analysis-using-R

# Background
Parkinson’s disease (PD) is a neurodegenerative disease where the neurons begin to die in the basal ganglia - the area of the brain that coordinates movement. The brain also slows its production of dopamine and norepinephrine, which are important for creating body movement and regulating the heart rate and blood pressure. 
The Unified Parkinson’s Disease Rating Scale (UPDRS) is a neurological and motor test designed to assess the severity of Parkinson's Disease, with a scale that spans from 0 (representing total health) to 199 (indicating total disability).

# Research Question
In this project, I'm using the [dataset](https://archive.ics.uci.edu/ml/datasets/Parkinsons+Telemonitoring) from a study that used dysphonia to distinguish between healthy people and people with Parkinson’s (PWP) to assess the best measure to separate them. Ways to measure dysphonia in the study included F0, absolute sound pressure level, jitter(the extent of variation in speech F0 from vocal cycle to vocal cycle), shimmer (the extent of variation in speech amplitude from cycle to cycle), and noise to harmonics ratios.  
In this study, my objective is to investigate whether the vocal attributes assessed in individuals with Parkinson's disease can be employed to elucidate or anticipate their UPDRS diagnostic scores.

| **Parameter** | **Role/Type** | **Description** |
| --- | --- | --- |
| $\beta_1$ = Time | Continuous/Predictor | Time since recruitment into the trial |
| $\beta_2$ = Age | Continuous/Predictor | Subject age |
| $\beta_3$ = PPE | Continuous/Predictor | A nonlinear measure of fundamental frequency variation. Is called Pitch Period Entropy |
| $\beta_4$ = RPDE | Continuous/Predictor | A nonlinear dynamical complexity measure. Is called Recurrence Period Density Entropy |
| $\beta_5$ = Sex| Catergorial/Predictor | Subject gender '0' - male, '1' - female |
| $\beta_6$ = Shimmer | Continuous/Predictor | Measure of variation in amplitude |
| $\beta_7$ = Jitter | Continuous/Predictor | Measure of variation in fundamental frequency |
| $\beta_8$ = HNR | Continuous/Predictor | Harmonics-to-Noise Ratio |
| $\beta_9$ = NHR | Continuous/Predictor | Noise-to-Harmonics Ratio |
| $\beta_10$ = DFA | Continuous/Predictor | Signal fractal scaling exponent |
| Y = Total UPDRS | Continuous/Response | Clinician's total UPDRS score, the score we have to predict. The higher the score the worse Parkinson’s the patient has |

# Analysis
The following techniques were used to test the hypothesis and build models: 
- Outlier Removal: Outliers were eliminated from the dataset using DFFITS, Cook's Distanceand DFBETAS to enhance data integrity and accuracy.
-  Brown-Forsythe Test: The Brown-Forsythe test was used to assess the homogeneity of variance across groups or conditions.
- Shapiro-Wilk Test: The Shapiro-Wilk test was conducted to evaluate the normality of the data distribution
- Box-Cox Transformation on Y: A Box-Cox transformation was applied to the dependent variable (Y) to improve model assumptions.
- Bootstrapping: Bootstrapping techniques were utilized to estimate sampling distributions and evaluate parameter uncertainties.
- General Linear Test (GLT): The General Linear Test was employed to analyze relationships and variances in the data.

***
## Question 1
For the first research question where I tested whether measures of vocal entropy (PPE and RPDE) significantly impacted a subject’s UPDRS score even when taking subject age and the effects of passing time into account, I concluded that atleast one of those measures significantly impacted the UPDRS score, even when accounting for the age and time of data collection within 180 days.

$H_0$ : $\beta_3$ = $\beta_4 = 0$ | $\beta_1$, $\beta_2$

$H_a$ : $\beta_3 \not= 0$ or $\beta_4 \not= 0$ | $\beta_1, \beta_2$

## Question 2
For the second research question, I examined the impact of vocal qualities (Shimmer, PPE, and HNR) and Sex on UPDRS scores to find that the vocal qualities and their interaction terms with sex have a significant impact on the UPDRS score.

$H_0 : \beta_6 = \beta_8 = \beta_9 = \beta_{651} = \beta_{652} = \beta_{851} = \beta_{852} = \beta_{951} = \beta_{952} = 0$

$H_a$ : At least one of the vocal qualities and the cocal qualities interaction terms with sex has a significant linear impact on their UPDRS score.

## Question 3
Question 3 assesses whether the age groups defined as (36, 45.8], (45.8, 55.6], (55.6, 65.4], (65.4, 75.2], and (75.2, 85] exhibit uniform total_UPDRS scores for any NHR, DFA, and HNR values. On analysis, we find that the age ranges produce different total_UPDRS scores for any NHR, DFA, and HNR values, hence rejecting the null hypothesis.

$H_0: \beta_{21} = \beta_{22} = \beta_{23} = \beta_{24} = \beta_{921} = \beta_{1021} = \beta_{821} = \beta_{922} = \beta_{1022} = \beta_{822} = \beta_{923} = \beta_{1023} = \beta_{823} = \beta_{924} = \beta_{1024} = \beta_{824} = 0$

$H_a:$ At least one of $\beta_{21}, \beta_{22}, \beta_{23}, \beta_{24}, \beta_{921}, \beta_{1021}, \beta_{821}, \beta_{922}, \beta_{1022}, \beta_{822}, \beta_{923}, \beta_{1023}, \beta_{823}, \beta_{924}, \beta_{1024}, \beta_{824} \not= 0$

# Final Model
The model that can best predict the UPDRS score is using all the variables used in this study.

$Y= \beta_1 X_1 + \beta_3 X_3 + \beta_4 X_4 + \beta_6 X_6 + \beta_7 X_7 + \beta_8 X_8 + \beta_9 X_9 + \beta_{10} X_{10}$

Diagnostic measures like boxcox transformation and weighted least squares were taken to fix non-normality and non-constant variance issues.

# Limitations of the study:
- 42 people participated in the study. Even though there was more than 5000 rows of data available, since they are all coming from only 42 subjects, many data points will potentially be repeated, since data was collected from each participant multiple times in a day.
- Some models didn't achieve normality and constant variance, so there is room for improvement in finding better models to answer these questions.
  
