# Machine-Learning-Pipeline-using-AWS-Glue-S3-EMR-SageMaker-Athena
 Build an end-to-end Machine Learning pipeline using AWS Glue, Amazon S3, Amazon EMR Amazon SageMaker and Amazon Athena


In this project, we embark on an exciting journey to build an end-to-end pipeline based on NASA Airfoil Self Noise  dataset.
Our cutting-edge pipeline will seamlessly integrate several state-of-the-art technologies, creating a harmonious symphony of data processing and machine learning. AWS Glue,a serverless extract-transform-load (ETL) service will be used to orchestrate the data flow, ensuring efficient and reliable data transformations. Amazon SageMaker based on EMR cluster will be used to train and deploy sophisticated predictive models.




## Requirements

Before Starting this guide, you will need:

- An AWS account (if you don't yet have one, please create one and [set up your environment](https://aws.amazon.com/getting-started/guides/setup-environment/))
- An IAM user that has the access and create AWS resources.
- Provided CloudFormation template
- Basic understanding of Python and apache spark 


## Use case and problem statement
A data engineer at an aeronautics consulting company need to build data pipeline for data scientist team. The company prides itself in being able to efficiently design airfoils for use in planes and sports cars. Data scientists in the office need to work with different algorithms and data in different formats. While they are good at Machine Learning, they count on data engineer to be able to do ETL jobs and build ML pipelines. 

In this project we will use the modified version of the NASA Airfoil Self Noise dataset. The dataset will be used, by dropping the duplicate rows, removing the rows with null values and building an ML pipeline to create a model that will predict the SoundLevel based on all the other columns. In the end the model will be evaluated and persisted into amazon s3 bucket for ready deployment.




Table of Contents
=================
[1. Project architecture](#project-architecture)

[2. Create S3 buckets ](#create-s3-buckets)

[3. Create sageMaker-EMR cluster ](#create-sageMaker-EMR-cluster)

[4. Create Glue job for extracting and storing raw data including data Catalog](#create-glue-job-for-extracting-and-storing-raw-data)

[5. Automate the data processing pipeline using Glue Workflow ](#automate-the-data-processing-pipeline-using-glue-workflowoptional)

[6. Analyze Raw Data using Athena ](#analyze-raw-data-using-athena.)

[7. Machine Learning  ](#machine-learning)


[8. Conclusion ](#conclusion)

[9. Appendix ](#appendix)


## 1. Architecture

To implement this data pipeline, we will use a provided CloudFormation `in us-east-1` [here ](https://us-east-1.console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/quickcreate?templateURL=https://aws-blogs-artifacts-public.s3.amazonaws.com/artifacts/astra-m4-sagemaker/end-to-end/CFN-SagemakerEMRNoAuthProductWithStudio-v3.yaml) 
 with `Amazon SageMaker Studio` which is the first fully integrated development environment (IDE) for machine learning (ML). It provides a single,web-based visual interface where we can perform all ML development steps, including preparing data,training and deploying models. And some resources such as networking, EMR clusters are included in provided template. We are going to use Aws Glue to perform ETL the input and unprocessed data  and store the result in Amazon S3 Bucket.


<img src="images/predicting-Nasa-airfoil-architure.gif" > 


## 2. Create S3 buckets*

From aws console, create bucket and give the name `ml-project01` as below and create inside the bucket 3 sub-folders named `app` , `athena-results` and `final-data`

<img src="images/create-bucket.png" > 

## 3. Create sageMaker-EMR cluster

Make sure you are in us-east-1 region in your aws management console and click on provided templated to create sageMaker-EMR cluster and other ressources such networks, service role, ...
Just give a name to the stack and create the stack as below.

<img src="images/Created-stack.png" > 