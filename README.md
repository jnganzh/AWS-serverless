# AWS-serverless

Forked from https://github.com/noahgift/awslambda

## Introduction

This repository aims to guide you through building a Serverless Data Engineering Pipeline. It will consist of setting up AWS Lambda functions, AWS Cloud9, AWS SQS, AWS DynamoDB, CloudWatch, AWS Comprehend and AWS S3.

## Diagram

![Overview](https://camo.githubusercontent.com/bb29cd924f9eb66730bbf7b0ed069a6ae03d2f1a/68747470733a2f2f757365722d696d616765732e67697468756275736572636f6e74656e742e636f6d2f35383739322f35353335343438332d62616537616638302d353437612d313165392d393930392d6135363231323531303635622e706e67)

## AWS Lambda Functions

For the purpose of this tutorial, we will be creating two lambda functions (1. Producer, 2. Consumer) using Cloud9. The files can be found in the src directory.

### Producer function

1. Proceed to the Cloud9 service, on the left side of the screen you should see AWS. Click on it, next to AWS Explorer, there should be a window-looking button click on it, a dropdown box will appear, select "Create Lambda Sam Application".

2. A few prompts will come out for the first one, select Python 3.7. 
3. For the second prompt, choose "AWS Sam Hello World".
4. Fill in the rest of the prompts by choosing appropriate names for the project.
5. A named folder will appear in your environment, cd into the folder. There will a folder called hello_world. In this folder, there is an app.py file. Replace the content of this .py file with either producer.py.
6. In the command line enter the following commands.
```
sam build --use-container
sam deploy --guided
```
Fill up all the relevant naming conventions

7. Set up IAM access by navigating to IAM services -> Roles -> Check Allow Lambda Functions -> Check Administrator Access (for permissions). Note this is important for the lambda function to have the right access to call other AWS services.
8. Navigate to AWS Lambda, the function created through cloud9 will be deployed there. Select it -> Configuration -> Permissions -> Edit Execution Role -> Select the role created in step 7.
9. Now we will add a trigger. Create a CloudWatch Trigger (Event Bridge) with a new rule, name it appropriately, under "Schedule Expression" type rate(1 minute). Deploy this trigger.

img1 

### Consumer Function

Create DynamoDB, SQS and S3 Bucket before proceeding with this step.

1. Repeat steps 1-8
2. Add a trigger, this time instead of CloudWatch, the trigger will be SQS, select the 'producer' queue.

## DynamoDB

1. Navigate to DynamoDB
2. Create a table named "fang". The table needs to be named this way unless you change the variables in the consumer.py file.
3. Primary Key has to be named "name" for a similar reason as before.
4. Add some company names as entries into the database.

## SQS

1. Navigate to SQS.
2. Create a queue called "producer" with all the default settings.

## S3 Bucket

1. Navitage to S3.
2. Create a bucket called "fangsentiment-jaryl" with all the default settings. You probably should change the code in consumer.py by giving the bucket a new name 
as bucket names have to be unique in the region.

## Results

If you followed all the steps without encountering any errors that this repo did not address, you will be able to see the results if you navigate into the s3 bucket. You will see it being populated periodically as new entries are added to DynamoDB.

img2

There is an extension of entity extraction available in the code to deploy.
