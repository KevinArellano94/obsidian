---
tags:
  - aws
  - course
---
## **Dividing data to reduce bias**

In this course, you've learned about the value of identifying, assessing, and mitigating bias. Reducing bias in your dataset is one of the primary objectives in data preparation. With balanced data, the model can focus on meaningful patterns in the dataset rather than any inherent noise.

A common strategy to achieve a balanced and accurate dataset is to divide the data into distinct subsets for training, testing, and validation. In this lesson, you will learn about the value and basic concepts of data splitting techniques.

![[Pasted image 20250922161109.png]]

### **Train, test, validate: A tripartite approach**

The process of data preparation typically involves **partitioning your datasets into** three primary subsets: **training**, **testing**, and **validating**.

**Training dataset**

- The cornerstone of model development
- Enables the model to learn the underlying patterns and relationships within the data
- Comprises the majority of the dataset, providing ample examples for the model to glean insights from

**Testing dataset**

- Evaluates the model’s performance on unseen data to assess its generalization capabilities
- Provides a set of examples that the model has not encountered during training
- Gains valuable insights into the model's ability to make predictions on new, unseen data through test evaluation

**Validation dataset**

- Supports fine-tuning the model’s parameters without introducing bias from the test set
- Permits iterative adjustments to the model’s configurations until optimal performance is achieved

### **Data-splitting techniques**

There are several techniques for data splitting, and the practice becomes even more complex during the model training phase of the machine learning lifecycle. For now, you will learn about two common approaches: **simple hold-out** and **cross-validation**.

To learn more about data splitting techniques, choose the START or arrow buttons to display each of the techniques.

![[Pasted image 20250922161453.png]]
**Simple hold-out**

This technique involves randomly **dividing the dataset into** two subsets: one for **training** and one for **testing**. Typically, the **majority of the data is allocated to the training** set, while a **smaller portion is reserved for testing**.

**Advantages:**

- **Straight-forward** implementation
- Provides a **quick estimate** of model **performance**

**Limitations:**

- Performance estimate **might have variance** due to dependency on specific examples in the test set
- **Not suitable for small datasets** because it might **lead to overfitting** or **underfitting**

![[Pasted image 20250922161827.png]]

**Cross-validation**

This technique involves randomly **dividing the dataset into multiple subsets or folds**. **Cross-validation** provides a more **comprehensive evaluation** of model performance compared to simple hold-out.

**Advantages:**

- **Uses the entire dataset for training and testing**, maximizing data usage
- **Reduces variance in performance estimation** by **averaging results** across multiple iterations

**Limitations:**

- **Computationally more expensive**, especially for large datasets
- Might be **sensitive to class imbalances** if not stratified properly

**K-fold cross-validation**

A common technique of cross-validation is known as **K-fold cross validation**. These terms are sometimes used synonymously. **Each fold (_k_) is used for both training and testing**, with iterations **covering all possible combinations**.

In this method, the available data is **divided into equal-sized subsets _k_ times**, where _k_ represents a number. The model is then trained and evaluated _k_ times. Each division, or _fold_, serves as the test set once, while the remaining _k-1_ folds are used for training. 

For example, a training dataset might be separated into five (k=5) different subsets. The first four subsets are used as training data, and then metrics are calculated on the last test piece. This approach is applied to the remaining four models for a total of five times, or five folds. All of the training data is used and then tested on five different subsets of the test data, eventually testing all data points.

### **Dataset shuffling**

Data shuffling involves **rearranging the order of the data points in a dataset before** they are **used for training** a machine learning model. Shuffling your data **helps to verify that the training examples are presented** to the model i**n a random order** rather than in a fixed sequence.

For example, imagine a dataset of images of dogs and cats, where all the dog images are presented first, followed by all the cat images. If the model learns to classify the first half of the examples as dogs and the second half as cats, it might not generalize well to situations where the dog and cat images are intermingled. By shuffling the dataset, the model is forced to learn more robust features and patterns that can generalize to different data distributions.

**Benefits of data shuffling**

Dataset shuffling plays a crucial role in mitigating biases that might arise from the inherent structure of the data. By introducing randomness through shuffling, you can **help the model be exposed to a diverse range of examples during training**. To learn more about the benefits of data shuffling, choose each of the numbered markers.

![[Pasted image 20250922162526.png]]

**Data shuffling techniques**

Dataset shuffling plays a crucial role in mitigating biases that might arise from the inherent structure of the data. By introducing randomness through shuffling, you can expose the model to a diverse range of examples during training. The benefits of data shuffling are as follows:

![[Pasted image 20250922162748.png]]

**Random permutation**

In this technique, you shuffle the dataset by randomly swapping the positions of the data points.


![[Pasted image 20250922162755.png]]

**Epoch-based shuffling**

This technique works by dividing the dataset into _epochs_ (complete passes through the dataset) and shuffling the data points between each epoch.  


![[Pasted image 20250922162824.png]]

**Mini-batch shuffling**

In this method, you shuffle the data points within each mini-batch before presenting the batch to the model.  

---

**Randomization**

When data is shuffled randomly, the model’s exposure to different examples is varied, **preventing it from memorizing the order of samples**. Instead, the model focuses on learning meaningful patterns inherent in the data. This randomness helps **break dependencies** or correlations that might exist between adjacent examples, ensuring that the model’s learning is **not influenced by the specific arrangement of the data**. The following two tables represent a training set and a testing set. Notice how the dates are randomized, and a separate set of randomized data is used to test the model after training the model.

![[Pasted image 20250922163038.png]]

### **Data augmentation**

In the lesson discussing class imbalance (CI), you learned that dataset augmentation helps address model bias. **Data augmentation** works by **creating new**, **realistic** **training examples** that expand the model's understanding of the data distribution. Dataset augmentation involves **artificially expanding the size** and **diversity** of a dataset by applying a variety of transformations and modifications to existing data samples. These transformations **introduce variations in the data** while preserving the essential characteristics relevant to the learning task.

![[Pasted image 20250922163229.png]]

Data augmentation techniques **mitigate the risk of overfitting to the limited training data** and **improve** the model’s **ability to generalize to unseen examples**. When implementing dataset augmentation, it is common practice to **apply transformations on the fly during the training process**, rather than generating and storing the augmented data upfront. This approach **ensures efficient use of memory** and **allows for potentially infinite variations of the augmented data**. General techniques for data augmentation include **mixing** or **blending existing data samples**, **interpolating** or **extrapolating data points**, and **applying domain-specific transformations**.

To recap augmentation techniques for specific data types, choose each of the following three tabs.

- **Image-based Augmentation**
	- Image-based augmentation involves the following:
		- Flipping, rotating, scaling, or shearing images
		- Adding noise or applying color jittering
		- Mixing or blending images to create new, synthetic examples

- **Text-based Augmentation**
	- Text-based augmentation involves the following:
		- Replacing words with synonyms or antonyms
		- Randomly inserting, deleting, or swapping words
		- Paraphrasing or translating text to different languages
		- Using pre-trained language models to generate new, contextually relevant text

- **Time series Augmentation**
	- Time series augmentation involves the following:
		- Warping or scaling the time axis
		- Introducing noise or jitter to the signal
		- Mixing or concatenating different time-series segments
		- Using generative models to synthesize new time-series data

---
### **Test your skills**

The following questions will help you check what you’ve learned. Select the correct answer and choose SUBMIT.


You are building a machine learning model to predict housing prices. You have a dataset of 1,000 housing records.

Which technique would be most appropriate to evaluate the performance of your model?

- [ ] Simple hold-out  
- [ ] Removing all outliers of your dataset
- [x] K-fold cross-validation  
- [ ] No need for data splitting

Note: answer is `K-Fold cross-validation`