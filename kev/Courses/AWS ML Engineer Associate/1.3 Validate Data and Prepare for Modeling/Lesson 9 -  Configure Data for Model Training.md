---
tags:
  - aws
  - course
---
## **Data formatting for training**

It's important that your data is properly formatted and configured for your specific machine learning (ML) model. Different ML frameworks and platforms might have specific data format requirements. 

In this lesson, you will explore some common data formats used in model training. You will also learn about configuring your data to load into your model training resources.

![[Pasted image 20250922164043.png]]

### **Python libraries and data formatting**

Python offers several powerful libraries that can help with data formatting and cleaning. You can use the following libraries to help prepare your data for machine learning model training: **Pandas**, **NumPy**, **Scikit-learn**, **Matplotlib**, and **Seaborn**. These Python libraries can help with various **data cleansing** tasks, such as **handling missing values**, **encoding categorical features**, **scaling** and **normalizing data**, **handling outliers**, and **feature engineering**.

To learn more about use cases for these libraries, choose each of the five numbered markers.

#### Pandas
This library makes **loading**, **cleaning**, **transforming** and **analyzing** data more **straightforward**. It's helpful for tasks such as reading in data from **CSVs**, Microsoft **Excel**, and **databases**. You can also use this library for **handling missing data**, **filtering**, **aggregating**, **merging datasets**, and more.

#### NumPy
This library provides **powerful N-dimensional array** and **matrix objects** to Python. It's useful for **numeric computing** and especially helpful if you need to perform **mathematical** or **statistical operations** on Pandas dataframes. NumPy also **integrates** well **with** libraries like **SciPy** and **Scikit-learn**.

#### Scikit-learn
This machine learning library has many **preprocessing utilities** for tasks like **encoding categorical data**, **scaling** or **normalizing features**, **imputing missing values**, and more. It's designed to seamlessly work with NumPy and Pandas data structures. Scikit-learn is very useful for **preparing data before feeding into ML algorithms**.

#### Matplotlib
This plotting library helps you **visualize data**. You can use it to **create plots**, **histograms**, **heatmaps**, **scatterplots** and more. By using visualizations, you can better understand datasets, **relationships**, **distributions**, and **outliers**. This library is helpful during the exploratory data analysis phase of data preparation.

#### Seaborn
This **high-level statistical data visualization** library builds on Matplotlib. It contains **customizable themes** and **additional visualization** types, such as **violin plots**, **jointplots**, **pairplots**, and **clustering heatmaps**. Seaborn streamlines creating insightful graphs and **makes visualizations more aesthetically interesting**.

### **Formatting for Amazon SageMaker**

When using Amazon SageMaker for your ML workloads, you want to make sure you are providing data that adheres to an accepted format. The two most common formats supported by the SageMaker built-in algorithms are **CSV formatting** and **RecordIO-protobuf** formatting. 

Formatting can be a complex task. You focus more on adhering to certain formatting types during the model training and refining stage of the machine learning lifecycle. However, it is helpful to know the basic concepts and structure of these two types of formats.

#### **CSV formatting**

CSV is a widely used text-based data format for training machine learning models. CSV files **store tabular data,** where each row represents a data sample, and the columns represent the features of that sample. For SageMaker built-in algorithms, the label in the training dataset must be the first column on the left, and the features should be to the right. Many built-in algorithms in SageMaker, such as **XGBoost**, **linear learner**, and **DeepAR**, **accept CSV formatted data** as input for model training. 

#### **RecordIO-protobuf**

RecordIO-protobuf is a **binary data format** used by SageMaker for **efficient data storage** and **transfer**. This format is particularly **useful when you need to handle large datasets** or perform **automatic transformations on the data**. The RecordIO-protobuf format consists of a series of records, where **each record contains a binary-encoded protobuf message**. This format is commonly used for image data, where each record represents an image and its associated metadata.

### **AWS services for pre-training data configuration**

At this point in the ML lifecycle, you have taken the following steps to prepare your data for your ML model:  

1. **Clean and preprocess your data** as necessary, handling missing values, outliers, and any other data quality issues.
2. **Transform** and **feature engineer** your data.
3. **Consider data augmentation** and **shuffling techniques** to increase the diversity of your training data. Then, split your data into training, validation, and test sets, if applicable.

Now, you will take your clean, transformed, and fully prepared data through the configuration and ML upload process. To learn the basics about the final steps to configure your data for your machine learning model, choose the START or arrow buttons to display each of the five steps.

#### Step 1 - **Upload data to Amazon S3**

Your data is stored in a repository, like Amazon Simple Storage Service (Amazon S3). If your data is not already in Amazon S3, complete the following steps to load your data into Amazon S3:  

- Create an S3 bucket to store your data files. 
- Upload your data files to the S3 bucket, ensuring proper folder structure and file naming conventions. 
- Configure access permissions for the S3 bucket to grant read and write access to your machine learning resources.

#### Step 2 - **Mount Amazon EFS or Amazon FSx**

**Amazon Elastic File System (EFS):** Amazon Elastic File System (Amazon EFS) is a scalable file system for use with AWS Cloud services and on-premises resources. It provides a high-performance way to access and share file data. To begin using Amazon EFS for your ML workloads, create an EFS file system. Then, configure the security group and network settings to allow access from your machine learning resources.  

**Amazon FSx:** Amazon FSx provides fully managed file systems compatible with popular file system protocols, such as Windows File Server and Lustre. To begin using Amazon FSx for your ML workloads, create an Amazon FSx file system and configure the appropriate protocol. You will configure the data for either Windows or Lustre.
#### Step 3 - **Copy data from Amazon S3 to Amazon EFS or Amazon FSx**

Next, you will copy the data from storage to your configured file system. 

To copy the data, complete the following steps:  

- Use AWS data transfer utilities or custom scripts to copy your data from the S3 bucket to the mounted EFS or FSx file system. 
- Ensure that the file system has sufficient space to accommodate your data. 
- Verify data integrity by checking file sizes and checksums after the transfer is complete.
#### Step 4 - **Load the data into your ML training resource**

After your data is staged on Amazon EFS or Amazon FSx, you can use these services to load the data efficiently into your ML compute resource like Amazon SageMaker.

With **Amazon EFS**, you would create an EFS file system and mount it to your SageMaker notebook instance or training job. Copy the dataset files into the EFS file system. Then in your training script, load the data by accessing the Amazon EFS mount path. 

For **Amazon FSx**, you would create a Lustre file system and attach it to your SageMaker resource. Copy the data files to the FSx Lustre file system. In your training script, load the data by accessing the Amazon FSx mount path. 

Note that both Amazon EFS and Amazon FSx for Lustre provide shared file storage that can be accessed from multiple Amazon Elastic Compute Cloud (EC2) instances at the same time. This makes them useful options for machine learning workloads where you need a common data store that all the EC2 instances running the ML training code can access.
#### Step 5 - **Monitor, refine, scale, automate, and secure**

When your data is loaded into your resource, you will continue to monitor, refine, scale, automate, and secure your ML workloads. Monitoring, refining, scaling, automating, and securing your workloads is a complex and involved part of the ML lifecycle. You can learn more about these phases by continuing your machine learning engineer journey. For now, review the following list of considerations for monitoring, scaling, automating, and securing your ML workloads after the data processing phase:

- Implement data lifecycle management strategies, such as archiving or deleting old or unused data.
- Consider using AWS services like AWS Step Functions, AWS Lambda, Amazon Managed Workflows for Apache Airflow (Amazon MWAA), and AWS CodePipeline to automate and orchestrate your data workflows.
- Implement continuous integration and continuous deployment (CI/CD) practices to streamline the process of updating and deploying your machine learning models with new data.
- Implement appropriate security measures, such as encryption at rest and in transit, to protect your data. 
- Configure access control mechanisms, such as AWS Identity and Access Management (IAM) policies, to restrict access to your data and machine learning resources. 
- Regularly review and update security configurations to ensure compliance with organizational policies and industry best practices.


### **Test your skills****

The following questions will help you check what you’ve learned. Select the correct answer and choose SUBMIT.

A telecommunications company wants to use Amazon SageMaker to train a machine learning model on their customer data. They have the data stored in different formats.

Which data formats do most Amazon SageMaker algorithms support for training? 

- [x] CSV and RecordIO-protobuf  
- [ ] All data formats  
- [ ] No data formats  
- [ ] Custom data formats

Note: answer is `CSV and RecordIO-protobuf`