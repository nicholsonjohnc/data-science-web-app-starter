# Data Science Web App Starter
Starter project for building data science web apps.

We will...

* Automate provisioning of your app's infrastructure using AWS CloudFormation (Python).
* Build out a front-end using Angular Framework (TypeScript).
* Build a highly-scalable yet low-cost back-end using AWS Lambda (Python).  

NOTE: I don't recommend cloning this repo. 
Start an empty repo for your project and copy/paste what you need 
piece-by-piece so you know what's going on.
When creating a repo don't create a README.md or .gitignore. Angular is going to create these for you.

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

```
pip install boto3
```

Reference: [AWS SDK for Python (Boto3)](https://aws.amazon.com/sdk-for-python/)

The AWS Command Line Interface (CLI) is handy to have installed too.

```
pip install awscli
```

Reference: [AWS Command Line Interface](https://aws.amazon.com/cli/)

## Step 4 - Setup programmatic access

You've installed the SDK, but before you can use it you'll need to setup programmatic access.

[here](https://boto3.readthedocs.io/en/latest/guide/quickstart.html#configuration)

In short, in the AWS Console, navigate to the 'IAM' service. Select 'Users' on the left.
Select 'Add user' button. Set 'User name' to 'devops' and 'Access type' to 'Programmatic access'. Click next.
Select 'Create group' button. Set 'Group name' to 'admin' and check the 'AdministratorAccess' policy. 
NOTE: In practice only give users access to the policies they need. Click 'Create group'. 
Make sure checkbox next to newly created group is selected and click next. Click 'Create user'. 

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

## Step 5 - Build a basic web app using Angular Framework

Before we continue provisioning our infrastructure, let's build a basic Angular web app so we have something to launch.

First, install the [Angular CLI](https://cli.angular.io/):

```
npm install -g @angular/cli
```

NOTE: [Node.js](https://nodejs.org/en/) must be installed on your system to use node package manager (npm).

Once installed, from within your empty repo, tell the Angular CLI to create a new app.

```
ng new your-app-name
```

This may take a bit as Angular installs all of the Node.js modules it depends on in 'your-app-name/node_modules'.

Once installed, I recommend moving everything in the newly created 'your-app-name' folder up a level and deleting the 'your-app-name' folder. 
I like my project structures like I like my management structures - flat. 

Now, from within your repo folder, you should be able to run your app on a local dev server that will automatically reload if you make any changes to source files.

```
ng serve
```

Once compiled, you can view your app at [http://localhost:8080/](http://localhost:8080/).
NOTE: You can specify the host and port 'ng serve' uses as follows 'ng serve --host localhost --port 8080'.

Shut down the dev server by pressing 'ctrl+c'.

Now, from within your repo folder, build a production version of your app in the 'dist' folder. This may take a sec.

```
ng build -prod
```

Once built, the contents of this folder represent our app front-end that we'll upload to an AWS S3 bucket and serve to the world using AWS CloudFront.

## Step 6 - Provision web tier (front-end) infrastructure

From within your repo folder, make directory 'cloudformation'.

```
mkdir cloudformation
```

Inside of directory 'cloudformation', make 'web-tier-stack.json' and 'web_tier_stack.py'.

```
touch cloudformation/web-tier-stack.json
touch cloudformation/web_tier_stack.py
```

[CloudFormation](https://aws.amazon.com/cloudformation/) expects a JSON template describing 
all of the infrastructure resources we want it to create, update, or delete.

We will describe any web tier infrastructure resources we want CloudFormation to manage in 'web-tier-stack.json'.
Then we'll write a Python script, 'web_tier_stack.py', to programatically create, update, or delete the stack described in 'web-tier-stack.json'. 

The template in 'web-tier-stack.json' consists of Parameters and Resources. 
Parameters are what make our template general purpose. 
For instance, 'web-tier-stack.json' takes a DomainName parameter that is used throughout 
our template to create appropriately named resources.

I recommend creating infrastructure resources by copy/pasting from the [AWS Resource Types Reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-template-resource-type-ref.html).

The resources being described in 'web-tier-stack.json' are as follows:
* WebBucket - The S3 bucket where your code will live. Name matches your domain name.   
* WebBucketPolicy - The policy for WebBucket that gives public read access to its contents.
* WebBucketWWW - An S3 bucket that simply redirects requests for the www subdomain to your domain.

## Step 7 - Provision server tier infrastructure


