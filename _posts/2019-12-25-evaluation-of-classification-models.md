---
title: "Evaluation of Classification Models"
last_modified_at: 2019-12-25T16:20:02-05:00
categories:
  - Machine Learning

---

Classification models are widely used in varies scenarios. In this article, not only accuracy or f1 score will be discussed, but also KS and Kappa score are mentioned. 7 different evaluation methods are as follows. Let’s dive deep into them!
- Accuracy
- Precision
- Recall
- F1
- AUC-ROC
- KS
- Kappa score

### Accuracy
Accuracy is to calculate the percentage of predictions are correct. Generally speaking, it can be used in most of the cases.
However, when targets are super imbalanced, using accuracy is wrong. For instance, in fraud detection, 99.99% of transactions are good and only 0.01% is bad. If we simply assume 100% users are good, the accuracy can be 99.9%, which means accuracy is not a good indicator to evaluate the performance.

![](https://miro.medium.com/max/541/1*g3KLDZatpTquU7_yUhAMYg.png)

### Precision
Precision is also known as positive predictive value and Specificity. The way to calculate precision is as follows.
If there are 3 positives (“1”) in the prediction and 2 of them are correct (True Positive aka TP), precision is 66.6% (2/3). Here, no matter how many 0 are correct or incorrect, precision won’t be affected by them.
![](https://miro.medium.com/max/481/1*un6jCAT84LdonCOD3s9Z1A.png)


### Recall
Similarly, recall is defined as “the fraction of the relevant documents that are successfully retrieved”, and it is also known as Sensitivity.

For instance, 10 labels (ground truth) are positives(“1”) and 3 of them are predicted as positive, then the recall is 30%. The use case can be in hospitals, doctors care more about if all potential COVID-19 cases are diagnosed. Even some cases False Positive (FP) which is not that important, because there are 2nd or 3rd rounds of testing.

![](https://miro.medium.com/max/451/1*yvEMspixf9OiTDVM7T7kPw.png)

To noticed that, recall and precision are not only can be used in binary classification problems. They can also be used in multi-class modelling which will be discussed deeply in the future. You can have a quick check of how to do that in scikit-learn as well [click here].

### F1
Both recall and precision are discussed above. F-measure is a way to care about both of two metrics. The formula is the following:

![](https://miro.medium.com/max/305/1*wrgXpXTuXSjHMgKPBHRQiQ.png)

If recall and precision are equally important, F1 will used as follows.
![](https://miro.medium.com/max/230/1*v9cPoh5oD3ewGLo3irksHw.png)

![](https://miro.medium.com/max/464/1*iY_Mr0PLq2dAR3MdTqTLWg.png)


### AUC-ROC
AUC-ROC stands for “Area under the ROC Curve.” It is to measure classification models by various thresholds (the default threshold is 0.5). The range of value is from 0 to 1. In particular, the terms used in the formula are listed below.
- TN: True Negative
- TP: True Positive
- FN: False Negative
- FP: False Positive
- TPR (True Positive Rate) = Recall = TP / (TP + FN)
- FPR (False Positive Rate) = 1- Precision = FP /(FP + TN)

![](https://miro.medium.com/max/700/1*KK51NEp0VcOm_jamgPa9DA.jpeg)

![](https://miro.medium.com/max/543/1*O9LpNlBx6aZ6qZjAUXJaIA.png)



### KS
KS (Kolmogorov–Smirnov test) is a evaluation metric to compare if two samples are from the same distribution or not. Also, KS is widely used in risk management and fraud detection in banking.

![](https://miro.medium.com/max/493/1*uhMOYVP4rwq9cih5-VsGTQ.png)

In the plot, KS can be interpreted as the maximum margin of 2 classes (red and blue lines represent the cumulative probability of two classes). If the margin is huge enough, we can say the classification model can distinguish two classes pretty good.

![](https://miro.medium.com/max/580/0*535sng0P6cGKRTwL.png)


### Kappa score
Kappa score is to measure the inter-range reliability. In other words, we want to know the ‘real accuracy’ and reduce the level of uncertainty. For example, if there are 2 classes and the ratio of 2 classes are the same, there is a high probability to get the correct answer by random guess. In the same case, if there are over 10 classes, relatively it is much hard to get the correct answer by random guess.
![](https://miro.medium.com/max/272/1*OdZfzGBxl-p9VgbSKM-4NA.png)

In the formula above, Po is the observed agreement and Pe is the hypothetical probability of chance agreement. Still, no idea how it works? Let’s look at an example. Po (75%) is the same as accuracy. Then, we need to calculate how lucky we are to get Y (35/60) and N (25/60) correctly (we can also understand it as the level of difficulty).
![](https://miro.medium.com/max/700/1*HSGC_Np8mKbh5ZdfcM50VA.png)


In practice, we don’t need to manually calculate the Kappa score step by step. Instead, we can import cohen_kappa_score from sklearn directly.
![](https://miro.medium.com/max/526/1*MHJmjfetRMwohMEbECmg1Q.png)

Furthermore, the weighted kappa score can be used to evaluate ordinal multi-class classification models.


Thanks for reading. Hope those 7 evaluation metrics can give you a general idea to evaluate classification models.

# Reference
- https://en.wikipedia.org/wiki/Precision_and_recall#Recall
- https://en.wikipedia.org/wiki/Cohen%27s_kappa
- https://en.wikipedia.org/wiki/Kolmogorov%E2%80%93Smirnov_test