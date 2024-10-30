---
title: "Classification Metrics part 1"
date: 2024-10-30T17:55:28+08:00
description: "Guide to use classification metrics part 1."
tags: ["Machine learning","metrics"]
type: post
weight: 10
showTableOfContents: true
---

When it comes to evaluating machine learning models, accuracy is often the first metric that comes to mind. However, relying on accuracy alone can be confusing, especially when dealing with different products. In this article, we’ll explore why accuracy may not be the best metric and discuss other metrics that provide a more accurate measure of model performance.

## The Problem with Accuracy

Accuracy is simply the proportion of correct predictions out of the total number of predictions. While this seems straightforward, it can fail to give an accurate picture when the data is imbalanced.

**Consider this scenario:**
- Suppose you have 100 data points, with 90 belonging to class 1 and 10 to class 0.
- If a model predicts every data point as class 1, it will achieve an accuracy of 90%.

At first glance, this might seem impressive. However, this high accuracy is misleading because the model completely fails to identify any of the instances of class 0. This is a common pitfall in imbalanced datasets, where one class significantly outnumbers the other.

## A Better Alternative: The Confusion Matrix

To better evaluate model performance, especially in cases of imbalanced data, the confusion matrix is a powerful tool. It provides a detailed breakdown of a model’s predictions, helping us understand the types of errors it is making.

A confusion matrix categorizes predictions into four scenarios:
- **True Positive (TP):** The model predicts True, and the actual value is True.
- **False Positive (FP):** The model predicts True, but the actual value is False. This is also known as Type 1 Error.
- **True Negative (TN):** The model predicts False, and the actual value is False.
- **False Negative (FN):** The model predicts False, but the actual value is True. This is also known as Type 2 Error.

### Evaluating Model Performance Using the Confusion Matrix

High accuracy alone doesn’t necessarily indicate a good model. A model is considered good if:
- Both TP (True Positives) and TN (True Negatives) are high.
- Both FP (False Positives) and FN (False Negatives) are low.

Given the confusion matrix, we can calculate the total actual positives as:
- **Total Actual Positives (P) = TP + FN**

Similarly, the total actual negatives can be calculated as:
- **Total Actual Negatives (N) = FP + TN**

### Calculating Accuracy from the Confusion Matrix

Accuracy can be derived directly from the confusion matrix using the formula:

$$
\text{Accuracy} = \frac{\text{Correct Predictions}}{\text{Total Number of Predictions}} = \frac{TP + TN}{TP + TN + FN + FP}
$$

## Precision: When False Positives Are Critical

When we cannot afford any false positives, **precision** is the metric to focus on. Precision tells us, out of all points predicted to be positive, how many are actually positive.

$$
\text{Precision} = \frac{TP}{TP + FP}
$$

**Example:**
- Misclassifying a spam email as not spam (FN) is somewhat acceptable.
- However, classifying an important email as spam (FP) can lead to major consequences.

In scenarios where reducing false positives (FP) is crucial, precision becomes the primary metric.

**Range of Precision Values:** 0 to 1.

## Recall: When False Negatives Are Critical

When we cannot afford any false negatives, **recall** (also known as sensitivity or hit rate) becomes the key metric. Recall tells us, out of all the actually positive points, how many were predicted to be positive.

$$
\text{Recall} = \frac{TP}{TP + FN}
$$

**Example:**
- Classifying a healthy person as having cancer (FP) and conducting further tests is acceptable.
- However, missing out on diagnosing a person with cancer (FN) can be a life-or-death situation.

In such cases, minimizing false negatives (FN) is essential, and recall is the metric to focus on.

**Range of Recall Values:** 0 to 1.

## Additional Metrics to Consider

- **True Negative Rate (TNR):** Also known as specificity or selectivity, TNR tells us out of all the actual negative points, how many were correctly predicted as negative.

$$
\text{TNR} = \frac{TN}{FP + TN}
$$

- **False Positive Rate (FPR):** FPR indicates how many of the actual negative points were incorrectly classified as positive.

$$
\text{FPR} = \frac{FP}{FP + TN}
$$

- **False Negative Rate (FNR):** FNR indicates how many of the actual positive points were incorrectly classified as negative.

$$
\text{FNR} = \frac{FN}{FN + TP}
$$

## The F1 Score: Balancing Precision and Recall

When both precision and recall are equally important, the **F1 score** is the metric of choice. The F1 score is the harmonic mean of precision and recall, making it a balanced measure of a model’s performance.

$$
\text{F1 Score} = \frac{2 \times \text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}
$$

**Example:**
In a fintech company, both false positives (giving loans to people unable to repay) and false negatives (missing out on good borrowers) can have significant consequences. In such cases, balancing precision and recall is crucial, and the F1 score becomes an essential metric.

**Note:**
- The F1 score is particularly useful when dealing with imbalanced data.
- **Range:** 0 to 1.

### Why Use the Harmonic Mean in the F1 Score?

The harmonic mean penalizes lower values of precision or recall more than the arithmetic mean, ensuring that both metrics must be reasonably high for a good F1 score.

### Adjusting the F1 Score with Beta

If you need to give more importance to either precision or recall, you can adjust the F1 score using a beta parameter.

$$
F_{\beta} = (1 + \beta^2) \times \frac{\text{Precision} \times \text{Recall}}{\beta^2 \times \text{Precision} + \text{Recall}}
$$

- **Beta = 2** when recall is more important than precision.
- **Beta = 0.5** when precision is more important than recall.

