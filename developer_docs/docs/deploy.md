# Deploy OpenSARlab

## Prerequisite

* An Amazon AWS account
* An SSL Certificate
* Domains for each maturity in the deployment


## Step 1 - Choose a Deployment Name

* Referred to as **"org"** in this doc

## Step 2 - Add a Tag for Cost Tracking

1. TODO
1. Referred to as **"your_tag"** in this doc


## Step 3 - Import SSL Certificate into Certificate Manager

1. In AWS, navigate to Certificate Manager
1. Import your SSL Certificate


## Step 4 - Clone the ASF OpenSARlab Repositories

 1. Clone osl-asf to your dev machine
    1. git clone url_doesn't_exist_yet #TODO
 1. Clone osl-asf-container to your dev machine
     1. git clone url_doesn't_exist_yet #TODO
     

## Step 5 - Create and Populate AWS CodeCommit Repos

#### Repo 1: osl-\<org\>

1. Create a CodeCommit repo called osl-\<org\>
1. Clone osl-\<org\> to your local machine
1. Create maturity branches (at least 'prod')
    1. Referred to as **"maturity"** in this doc
    1. git checkout -b prod
1. Copy the contents of osl-asf into osl-\<org\>
1. Add, commit, and push the updates to the remote CodeCommit repo
    1 git add .
    1. git commit -m "initial commit"
    1. git push origin prod

#### Repo 2: osl-\<org\>-container

1. Create a CodeCommit repo called osl-\<org\>-container
1. Clone osl-\<org\>-container to your local machine
1. Create maturity branches (at least 'prod')
    1. Referred to as **"maturity"** in this doc
    1. git checkout -b prod
1. Copy the contents of osl-asf into osl-\<org\>-container
1. Add, commit, and push the updates to the remote CodeCommit repo
    1 git add .
    1. git commit -m "initial commit"
    1. git push origin prod


## Step 6 - Deploy the Container CloudFormation Stack

1. In AWS, navigate to CloudFormation
1. Click the "Create Stack" button
    1. Select "With new resources (standard)"

    ##### Create stack
    1. Check "Template is ready"
    1. Check "Upload a template file"
    1. Click "Choose file"
    1. Select **cf-container.yaml** from the local osl-\<org\>-container repo
    1. Click the "Next" button
    
    ##### Specify stack details
    1. Stack name
        1. osl-\<org\>-container-\<maturity\>
    1. CodeCommitSourceBranch
        1. \<maturity\>
    1. CodeCommitSourceRepo
        1. osl-\<org\>-container
    1. Click the "Next" button
        
    ##### Configure stack options
    1. Tags
        1. key: \<your_tag\>
        1. value: osl-\<org\>-container-\<maturity\>
    1. Click the "Next" button
    
    ##### Review osl-\<org\>-container-\<maturity\>
    1. Check "I acknowledge that AWS CloudFormation might create IAM resources with custom names."
    1. Click the "Create stack" button
    
1. Monitor the stack creation in CloudFormation
1. Monitor the execution of osl-\<org\>-container-\<maturity\>-Container-Pipeline in CodePipeline


## Step 7 - Edit the ECR Image Tags in osl-\<org\>/helm_config.yaml

##### Update the hub image tag
1. Navigate to AWS Elastic Container Registry (ECR)
1. Select the osl-\<org\>-container-\<maturity\>/hub repository
1. Copy the date tag for the latest push (i.e. 2021-01-26-18-04-50)
1. Open osl-\<org\>/helm_config.yaml in your local repo
    1. Navigate to hub: image: tag:
    1. Update the tag

##### Update tags for each group in each profile
1. Navigate to AWS Elastic Container Registry (ECR)
1. Select the osl-\<org\>-container-\<maturity\>/profile_name
1. Copy the date tag for the latest push (i.e. 2021-01-26-18-04-50)
1. Open osl-\<org\>/helm_config.yaml in your local repo
    1. Navigate to hub: extraConfig: myProfiles: 
    1. For each if block, if the image_url belongs to the profile whose tag you copied, update the tag
1. Repeat the above steps until the tags for all groups in all profiles have been updated

##### Push the changes
1. Add, commit, and push the updated helm_config.yaml to the remote CodeCommit repo

## Step 8 - Deploy the Kubernetes CloudFormation Stack

1. In AWS, navigate to CloudFormation
1. Click the "Create Stack" button
    1. Select "With new resources (standard)"

    ##### Create stack
    1. Check "Template is ready"
    1. Check "Upload a template file"
    1. Click "Choose file"
    1. Select **cf-pipeline.yaml** from the local osl-\<org\> repo
    1. Click the "Next" button
    
    ##### Specify stack details
    1. Stack name
        1. osl-\<org\>-\<maturity\>
    1. AdminUserName
        1. username of the main admin, which you will end up creating in Cognito
    1. CertificateArn
        1. The ARN of your SSL Certificate in Certificate Manager
    1. CodeCommitBranchName
        1. \<maturity\>
    1. CodeCommitRepoName
        1. osl-\<org\>
    1. ContainerNamespace
        1. osl-\<org\>-container-\<maturity\>
    1. JupyterHubURL
        1. The domain for current deployment/maturity
    1. OAuthPoolName
        1. osl-\<org\>-\<maturity\>-\<xxxxx\>
            1. xxxxx = 1st 5 digits of AWS Account ID (added to help assure uniqueness across AWS region)
    1. Click the "Next" button
        
    ##### Configure stack options
    1. Tags
        1. key: \<your_tag\>
        1. value: osl-\<org\>-\<maturity\>
    1. Click the "Next" button
    
    ##### Review osl-\<org\>-container-\<maturity\>
    1. Check "I acknowledge that AWS CloudFormation might create IAM resources with custom names."
    1. Click the "Create stack" button
    
1. Monitor the osl-\<org\>-\<maturity\> stack in CloudFormation
1. Monitor the execution of osl-\<org\>-container-\<maturity\>-Pipeline in CodePipeline
1. Monitor the creation of osl-\<org\>-\<maturity\>-cluster stack in CloudFormation

## Step 9 - Update the Cognito Callback URL, Sign Out URL, and Create an Admin User

1. Navigate to AWS Cognito
1. Click the "Manage User Pools" button
1. Select osl-\<org\>-\<maturity\>-\<xxxxx\>
1. Select "App client settings" from the sidebar menu
    1. Callback URL(s)
        1. https://<your_deployment/maturity_domain>/oauth_callback
    1. Sign out URL(s)
        1. https://<your_deployment/maturity_domain>
    1. Click the "Save changes" button
1. Select "Users and groups" from the sidebar menu
    1. Click the "Create User" button
        1. Fill out and submit the form, being sure to use the admin username declared when deploying the Kubernetes 
        CloudFormation Stack





