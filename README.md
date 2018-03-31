# Data Science Web App Starter
Starter project for building data science web apps.

We will...

* Automate provisioning of your app's infrastructure using AWS CloudFormation (Python).
* Build out a front-end using Angular Framework (TypeScript).
* Build a simple/low-cost back-end using AWS Lambda (Python).  

NOTE: I don't recommend cloning this repo. 
Start an empty repo for your project and copy/paste what you need 
piece-by-piece so you know what's going on.  

## Step 1 - Sign up / sign in to the AWS Console 

[here](https://aws.amazon.com/)

## Step 2 - Register a domain name using Route 53

[here](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/registrar.html)

NOTE: You can purchase a domain name elsewhere, but I generally prefer to do as much as possible in AWS.
Their prices are competitive and consistent. Performance is unmatched. No gotchas. 
Also, development is easier having everything in one place.

## Step 3 - Install the AWS SDK for Python (Boto3)

As you just experienced, reading documentation and clicking around the console is slow and error prone.
A much better way is to interact with AWS programmatically.
The AWS SDK for Python allows us to do this.
From here on out we'll rely on the SDK as much as possible.
We'll spend most of our time interacting with the CloudFormation service through the SDK.
CloudFormation allows us to set up, update, and tear down an entire application stack with ease.

```python
pip install boto3
```

Reference: [AWS SDK for Python (Boto3)](https://aws.amazon.com/sdk-for-python/)
