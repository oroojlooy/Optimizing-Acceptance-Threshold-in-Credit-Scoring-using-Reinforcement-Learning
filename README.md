# Optimizing Acceptance Threshold in Credit Scoring using Reinforcement Learning
This is a repository for my master thesis submitted as a part of the Master of Science in Quantitative Economics degree at the University of Tartu. The research was conducted in 2017-2018 at Creditstar Group, Estonia under the supervision of Karl Märka, Head of Data Science at Creditstar Group, and Oliver Lukason, PhD at the University of Tartu.

The source code for the project can be found in the Source directory.

A complete description of the project to be added.

## Background
The problem environment considered is a trivial credit business process. It starts when the loan provider receives a loan application with the data about the application and the potential borrower. The data is then passed to a credit scoring model that outputs a credit score which reflects the risk level of the loan application. Next, if the score is too low, the lender rejects the loan application. In case the score is high enough, the lender issues the loan. Eventually, if the loan applicant doesn't repay or defaults on their loan, the lender loses the money. In case the loan applicant repays, the lender gains extra money (from interest and fees). In the end, any of those cases affect the lender's profits.
<p align = "center">
  <img width = "600" alt = "Credit business process" src = "https://raw.githubusercontent.com/MykolaGerasymovych/Optimizing-Acceptance-Threshold-in-Credit-Scoring-using-Reinforcement-Learning/master/Pics/Credit_business_process.png">
</p>

In order to make the final accept / reject decision about a loan application, its credit score is compared to an acceptance threshold or cutoff point. The latter thus regulates the acceptance rates of a credit company and resulting default rates. The problem investigated in the master thesis is the optimization of an acceptance threshold to maximize credit company's profits. The traditional approach to the problem is to simply optimize the cutoff based on the credit score distribution of an independent test dataset of loan applications. Knowing the outcomes of all the loans in the dataset each possible acceptance threshold is considered and the corresponding profits are calculated. The optimal cutoff point is the one that corresponds to the maximum profit. In case the train / test split of loan application dataset is random, the acceptance threshold optimized for the test dataset is going to be optimal for the train dataset.
<p align = "center">
  <img width = "430" alt = "Acceptance threshold optimization: traditional approach" src = "https://raw.githubusercontent.com/MykolaGerasymovych/Optimizing-Acceptance-Threshold-in-Credit-Scoring-using-Reinforcement-Learning/master/Pics/Acceptance_threshold_optimization_1.png"><img width = "430" alt = "Acceptance threshold optimization: traditional approach" src = "https://raw.githubusercontent.com/MykolaGerasymovych/Optimizing-Acceptance-Threshold-in-Credit-Scoring-using-Reinforcement-Learning/master/Pics/Acceptance_threshold_optimization_2.png">
</p>

## Problem
  The main flaw in the traditional approach is that it is static and backward looking. It fully focuses on the test dataset which consists only of historical prefiltered accepted loan applications for which the outcome is known. The actual population of loan applications that the credit scoring model is applied to consists of completely new both potentially rejeted and accepted loan applications. The inconsistency of the loan applications sample used to train the model and optimize the acceptance threshold and the general population of loan applications the model and cutoff point are applied to leads to the selection bias and population drift issues. Those distort the optimal acceptance threshold making the traditional solution incorrect.

<p align = "center">
  <img width="430" alt="Selection bias issue" src="https://raw.githubusercontent.com/MykolaGerasymovych/Optimizing-Acceptance-Threshold-in-Credit-Scoring-using-Reinforcement-Learning/master/Pics/Selection_bias.png"><img width="430" alt="Population drift issue" src="https://raw.githubusercontent.com/MykolaGerasymovych/Optimizing-Acceptance-Threshold-in-Credit-Scoring-using-Reinforcement-Learning/master/Pics/Population_drift.png">
</p>
