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

## Step 3 - Install the AWS SDK for Python (Boto3) and the AWS CLI

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

The AWS Command Line Interface (CLI) is handy to have installed too.

```python
pip install awscli
```

Reference: [AWS Command Line Interface](https://aws.amazon.com/cli/)

## Step 4 - Setup programmatic access

You've installed the SDK, but before you can use it you'll need to setup programmatic access.

[here](https://boto3.readthedocs.io/en/latest/guide/quickstart.html#configuration)

In short, in the AWS Console, navigate to the 'IAM' service. Select 'Users' on the left.
Select 'Add user' button. Set 'User name' to 'devops' and 'Access type' to 'Programmatic access'. Click next.
Select 'Create group' button. Set 'Group name' to 'admin' and check the 'AdministratorAccess' policy. Click 'Create group'. 
Make sure checkbox next to newly created group is selected and click next. Click 'Create user'. 

NOTE: In practice only give users access to the policies they need.

STAY ON THIS PAGE

Run the following AWS CLI command in your terminal and enter your 'Access key ID' and 'Secret access key' when prompted.
Set default region name to 'us-east-1' or another AWS region. 
This determines which data center your app infrastructure will live in.
Accept the default 'Default output format' of 'None' by pressing enter.

```
aws configure
```

DO save your 'Access key ID' and 'Secret access key' somewhere safe.

DO NOT commit them. They can be used to create resources that incur charges on your account.
