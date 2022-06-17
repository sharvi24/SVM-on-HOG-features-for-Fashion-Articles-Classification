# SVM-on-HOG-features-for-Fashion-Articles-Classification

In this project, our objective is to correctly identify Zalando’s article images (Fashion-MNIST) into one of the 10 categories.

We have experimented with multiple models, including Unsupervised learning techniques such as K-means Clustering and DBSCAN and Supervised learning methods such as SVM, Random Forests, Logistic Regression, and finally Ensemble Models (Stacking And Voting paradigm). 

The first stage of the pipeline is some standard data preprocessing. We normalized all images into the range from 0 to 1 and then applied PCA to reduce the number of dimensions. The performance of each model is evaluated by accuracy on the testing set. Confusion matrix is also leveraged to establish more detailed insights into the model’s capability of distinguishing each individual category. Cross validation is used to tune hyperparameters and our best model is able to achieve an accuracy of 91.39%. This model is a standard SVM with RBF kernel trained on HOG (Histogram of Oriented Gradients) features, a classic computer vision technique to extract features based on histograms of different gradient orientations. Since HOG computes each histogram in a local block of image, it is able to describe the structure or the shape of an object.

While we expected the ensemble models to outperform every single model, our empirical results show that a single SVM trained on the data obtained by applying PCA on HOG features outperforms the all of the ensemble models. This result is explainable in that the single models’(Random forest, logistic regression, and KNN) performance is worse than SVM even before being combined as an ensemble model. That is, it is highly plausible that they have played as noise rather than a meaningful signal.

Voting ensemble model fails to capture the meaningful signal. For every label, we can observe that a single SVM outperforms both KNN and Random Forest in F1-score. For example, in the most tricky classification case (T-shirt vs Shirt), we can observe that SVM dominates in F-1 score compared to other models. This is also true for other cases as we can see from the table. Considering voting classifier chooses the most voted class among input models, voting classifier is susceptible to noises. The same explanation could apply to the stacking classifier where we expect the ensemble model to outperform each base classifier when each model is diverse enough (i.e. they must make different mistakes). However, with the presence of one superior model, the performance of the entire ensemble could not be further improved. The final meta-classifier would be heavily biased towards the most superior model.

Since the SVM model trained on the data obtained by applying PCA on HOG features achieved the highest accuracy, we report it as our proposed model. Here, we further analyze the results of the proposed model. The proposed model predicts (8) Bag (F1 score: 98 %) and (1) Trouser (F1 score: 98 %) the most successfully while (6) Shirt (F1 score: 74 %) the least successfully. This result is understandable by the confusion matrix in that the most misclassified label of Shirt is T-Shirt. The average of overall F1 score is 91 %.
