# Deploy OpenSARlab

## Prerequisite

* An Amazon AWS account
* An SSL Certificate
* Domains for each maturity in the deployment


## Step 1 - Choose a Deployment Name

* Referred to as **"org"** in this doc

## Step 2 - Choose a Tag for Cost Tracking

1. Choose a tag key for cost tracking, referred to as **"cost_tag"** in this doc


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
        1. key: \<cost_tag\>
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
        1. The domain for current deployment/maturity (optional, if blank defaults to load balancer URL)
    1. OAuthPoolName
        1. osl-\<org\>-\<maturity\>-\<xxxxx\>
            1. xxxxx = 1st 5 digits of AWS Account ID (added to help assure uniqueness across AWS region)
    1. Click the "Next" button
        
    ##### Configure stack options
    1. Tags
        1. key: \<cost_tag\>
        1. value: osl-\<org\>-\<maturity\>
    1. Click the "Next" button
    
    ##### Review osl-\<org\>-container-\<maturity\>
    1. Check "I acknowledge that AWS CloudFormation might create IAM resources with custom names."
    1. Click the "Create stack" button
    
1. Monitor the osl-\<org\>-\<maturity\> stack in CloudFormation
1. Monitor the execution of osl-\<org\>-container-\<maturity\>-Pipeline in CodePipeline
1. Monitor the creation of osl-\<org\>-\<maturity\>-cluster stack in CloudFormation

## Step 9 - Create an S3 Bucket to Hold the Lambda Handler
1. Navigate to AWS S3
1. Click the "Create bucket" button

    ##### General Configuration
    1. Bucket name: Choose a name that is unique across your AWS region (consider appending your AWS ID to create a unique name)
    1. AWS Region: Select the region of the deployment
    
    ##### Clock Public Access settings for bucket
    1. Check "Block all public access"
    
    ##### Bucket Versioning
    1. Disable
    
    ##### Tags
    1. optional (costs will be negligible)
    
    ##### Default encryption
    1. Disable
    
    ##### Advanced Settings
    1. Leave on defaults
    
1. Click the "Create bucket" button

## Step 10 - Upload the Lambda Handler to the Lambda Handler S3 Bucket
1. Zip lambda_handler.py (in the osl-asf repo)
1. Upload lambda_handler.py.zip

## Step 11 - Deploy the Cognito CloudFormation Stack

1. In AWS, navigate to CloudFormation
1. Click the "Create Stack" button
    1. Select "With new resources (standard)"
    
    ##### Create stack
    1. Check "Template is ready"
    1. Check "Upload a template file"
    1. Click "Choose file"
    1. Select **cf-cognito.yaml** from the local osl-\<org\> repo
    1. Click the "Next" button
    
    ##### Specify stack details
    1. Stack name
        1. osl-\<org\>-\<maturity\>-\<xxxxx\> 
    
    ##### Configure stack options
    1. Tags
        1. key: \<cost_tag\>
        1. value: osl-\<org\>-\<maturity\>-\<xxxxx\>
    1. Click the "Next" button
    
    ##### Review osl-\<org\>-\<maturity\>-\<xxxxx\>
    1. Check "I acknowledge that AWS CloudFormation might create IAM resources with custom names."
    1. Click the "Create stack" button

## Step 12 - Update the Cognito Callback URL, Sign Out URL, and Create an Admin User

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
        
## Step 13 - Sign into OpenSARlab With the Admin Account and Add Groups

1. Sign into your deployment as the admin user
1. Click the "Control Panel" button at the top right of the screen
1. Select the "Groups" tab
1. Click the "Add New Group" button
    1. Name the group after a group in the group list (found in helm_config.yaml)
    1. Select group type: action
    1. Check "All Users?" if the group should be enabled for all users
    1. Check "Is Enabled?"
    1. repeat for all groups in group list as well as the action group "sudo"
1. Create any label groups you'd like
    1. Label groups simply group users together for easy management and carry no other effects
1. Add users to groups not marked "All Users" by checking the appropriate group boxes next to their usernames in the Groups tab

## Step 14 - Prime the Autoscaler

1. Navigate to EC2 in the AWS console
1. Select "Auto Scaling Groups" from the left sidebar menu
1. Select each auto scaling group in the deployment
    1. Click the "Edit" button in the "Group Details" section
    1. Change Desired capacity to 1
1. Login to the deployment and in turn, start up a server for each group
1. After closing each server, the desired capacity will automatically drop back down to zero, and then it will be able to scale up from zero moving forward.

## Step 15 - Activate the cost_tag

1. Wait 24 hours for the cost_tag to propagate to AWS Cost Allocation Tags
1. Navigate to AWS Billing
1. Select "Cost allocation tags" from the left sidebar menu
1. Search for your chosen cost_tag key
1. Check the tag's selection box
1. Click the "Activate" button

## Step 16 - Add the cost_tag to you Kubernetes Cluster

1. Navigate to AWS EKS
1. Select "Clusters" from the sidebar menu
1. Select your deployment's cluster
1. Select the "Tags" tab
1. CLick the "Manage tags" button
1. Click the "Add tag" button
1. Enter your cost_tag key as the tag key
1. Enter the name of the cluster as the tag value
1. Click the "Add tag"
1. Click the "Save changes" button
1. You must refresh the page to see your added tag

## Step 17 - (optional) Authorize your user to access the AWS EKS Console
This will allow access to the EKS console, which gives you much of the same information as kubectl, but in a more user friendly manner.

1. Run "kubectl edit cm aws-auth -n kube-system" from a local terminal
1. Edit the "data" section of aws-auth, adding mapUsers as a sibling of "mapRoles"
    1.     mapUsers: |
             - userarn: arn:aws:iam::<your_acct_number>:user/<your_username>
               username: <your_username>
               groups:
                 - system:masters
1. Save changes

##### Note: 
- "After you create and apply user-defined tags to your resources, it can take up to 24 hours for the tags to appear on your Cost Allocation Tags page for activation. After you select your tags for activation, it can take up to 24 hours for tags to activate."

- The costs for the first 2 days of a newly created deployment will not be tracked.
