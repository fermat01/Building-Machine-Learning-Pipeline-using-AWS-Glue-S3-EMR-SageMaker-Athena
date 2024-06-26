# Machine-Learning-Pipeline-using-AWS-Glue-S3-EMR-SageMaker-Athena
 Build an end-to-end Machine Learning pipeline using AWS Glue, Amazon S3, Amazon EMR Amazon SageMaker and Amazon Athena


In this project, we embark on an exciting journey to build an end-to-end pipeline based on NASA Airfoil Self Noise  dataset.
Our cutting-edge pipeline will seamlessly integrate several state-of-the-art technologies, creating a harmonious symphony of data processing and machine learning. AWS Glue,a serverless extract-transform-load (ETL) service,will orchestrate the data flow,ensuring efficient and reliable data transformations. Amazon SageMaker based on EMR cluster will be used to train and deploy sophisticated predictive models.




## Requirements

Before Starting this guide, you will need:

- An AWS account (if you don't yet have one, please create one and [set up your environment](https://aws.amazon.com/getting-started/guides/setup-environment/))
- An IAM user that has the access and create AWS resources.
- Provided CloudFormation template
- Basic understanding of Python and apache spark 


## Use case and problem statement
A data engineer at an aeronautics consulting company. The company prides itself in being able to efficiently design airfoils for use in planes and sports cars. Data scientists in the office need to work with different algorithms and data in different formats. While they are good at Machine Learning, they count on data engineer to be able to do ETL jobs and build ML pipelines. In this project we will use the modified version of the NASA Airfoil Self Noise dataset. The dataset will be used, by dropping the duplicate rows, removing the rows with null values and building an ML pipeline to create a model that will predict the SoundLevel based on all the other columns. You will evaluate the model and towards the end you will persist the model.


Table of Contents
=================

[1. Create S3 buckets ](#create-s3-buckets)

[2. Create Glue job for extracting and storing raw data including data Catalog](#create-glue-job-for-extracting-and-storing-raw-data)

[3. Automate the data processing pipeline using Glue Workflow ](#automate-the-data-processing-pipeline-using-glue-workflowoptional)

[4. Analyze Raw Data using Athena ](#analyze-raw-data-using-athena.)

[5. Machine Learning  ](#machine-learning)


[6. Conclusion ](#conclusion)

[7. Appendix ](#appendix)


## Architecture

To implement this data pipeline, we will use a provided CloudFormation [here in us-east-1](https://signin.aws.amazon.com/oauth?response_type=code&client_id=arn%3Aaws%3Asignin%3A%3A%3Aconsole%2Fcloudformation&redirect_uri=https%3A%2F%2Fus-east-1.console.aws.amazon.com%2Fcloudformation%2Fhome%3FhashArgs%3D%2523%252Fstacks%252Fquickcreate%253FtemplateURL%253Dhttps%253A%252F%252Faws-blogs-artifacts-public.s3.amazonaws.com%252Fartifacts%252Fastra-m4-sagemaker%252Fend-to-end%252FCFN-SagemakerEMRNoAuthProductWithStudio-v3.yaml%26isauthcode%3Dtrue%26region%3Dus-east-1%26state%3DhashArgsFromTB_us-east-1_38a85d8762d46787&forceMobileLayout=0&forceMobileApp=0&code_challenge=BD80NtJoAbVeJGKadtNpkbbK23cbGz4pViZcZg4n398&code_challenge_method=SHA-256/) 
 with [Amazon SageMaker Studio](https://docs.aws.amazon.com/sagemaker/latest/dg/studio.html) which is the first fully integrated development environment (IDE) for machine learning (ML)It provides a single,web-based visual interface where we can perform all ML development steps, including preparing data,training,and deploying models.And some resources such as networking, EMR clusters. And we are going to use Aws Glue to perform ETL the input and unprocessed data  and store the result in Amazon S3 Bucket.


<img src="images/predicting-Nasa-airfoil-architure.gif" > 
