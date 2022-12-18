---
authors:
- admin
categories:
- R
date: "2022-12-18"
draft: false
featured: false
projects: [R]
subtitle: "Posters about R。"
summary: "Minimization for clinical trials groups allocation"
tags:
- Minimization
- R
- 随机动态分组
title: Minimization (dynamic allocation)
---

Recently, one of my former colleagues asked me whether R can do minimization, a dynamic randomization method. He is a medical doctor and is planning to enroll patients for his clinical research. Because he doesn’t have the data of all patients he gonna to enroll, he need to dynamically allocate patients to different treatment groups based on several prognostic factors, such as sex, age, and surgery location. To be honest, I never heard of minimization before. But fortunately, R does have one package specifically for minimization. Thus, I made a shiny app for him to do this. Today, in this poster, I am going to explain more details about minimization, a very useful technique for randomization in clinical trials.

Randomization is used to prevent selection bias and to maximize the precision of treatment effect estimates in clinical trials. For moderate-sized to large clinical trials, randomization helps ensure balance on both identified and unknown prognostic factors. Nevertheless, imbalance of treatment allocation may occur, especially in smaller trials. For a trial with 30 patients, a binary covariate exhibited in 30% of a population will result in chance imbalances of more than 10% between two treatment groups with probability 0.45. Such imbalances will reduce the precision of treatment estimates in smaller trails, particularly if the unbalanced factors are highly correlated with the study’s endpoints. Moreover, imbalance on covariates may affect the credibility of the study when reviewed by colleagues. 

To circumvent imbalance over important covariates, stratification is widely used. In stratification, blocked randomization is performed within each pre-specified combination of covariate levels, known as strata. However, increasing the number of strata may increase the imbalance of the number of complete blocks within strata, thus nullifying the benefits of stratification. 

In the middle of 1970s, an adaptive randomization technique called minimization was proposed that allowed for balancing over a larger number of covariates than was feasible for stratification. In many instances, minimization has been shown to be superior to stratification in terms of minimizing treatment imbalance and maximizing trail efficiency. 

In 1975, Pocock and Simon presented the minimization method. Minimization sequentially assigns patients to treatment by attempting to minimize the total imbalance between treatment groups over important prognostic factors. 

Pocock and Simon provided a general framework for minimization that describes an individual factor balance function D,  an overall balance function G, and a set of treatment assignment probabilities P. Let there be K treatments and M prognostic factors. For an arbitrary instance in a trial, denote xijk as the number of patients with factor i at the level of j assigned to treatment k. Let the next patient entering the trial have prognostic factor levels r1, r2,...., rM. If the new patient is assigned to treatment K, then only Xirik for i = 1 to N will change. That is, the number of patients assigned to treatment K will only change for the factor levels that the new patient exhibits. The function D and G will be used to determine which treatment assignment will result in the least overall imbalance in treatment based on these changed xirik values.

Consider dik = D(xiri1, … , xiriN) where dik measures the resulting imbalance among treatment groups for factor i at the level of ri if the patient is assigned to treatment k. The function D could be chosen as range, standard deviation or variance of the number of patients assigned to each treatment at factor i and level ri.

Then consider Gk = G(d1k, ...., dMk) for k =1 to N, where G is a function that calculates the resulting overall imbalance of the treatment assignments if the patient is assigned to treatment k. Then function G could be chosen to simply sum up the dik values, or G could be a weighted sum of the dik values to reflect the desire to obtain balance for certain prognostic factors more than others.

The overall imbalance functions corresponding to each treatment k can then be ranked from the smallest overall imbalance value to the largest, with the motivation that one would assign a patient to a treatment with a low G score with a high probability so as to increase the chance of maximizing balance among the factors. In a purely deterministic procedure, assuming that there are no ties in the scores for G, the treatment assignment k with the lowest G function would be picked with probability one. But, other values for p = (p1 ... pN) could be chosen. The patient is then assigned to a treatment based on the probabilities for p. The steps above are repeated for every patient that enters the trial.

Below is the shiny app I made for my colleague:

<iframe src=" https://chenchong446337.shinyapps.io/minimization/" data-external="1" width="800px" height="800px">
</iframe>

## License

Released under the [MIT](https://github.com/wowchemy/wowchemy-hugo-themes/blob/master/LICENSE.md) license.
