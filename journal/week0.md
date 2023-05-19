# Week 0 - Billing and Architecture

# Prerequisite

Befor creating an `IAM user` from the `root account` refer this https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_billing.html?icmpid=docs_iam_console#tutorial-billing-step2  link

# Create a IAM User and generate and access keys:

1. Use the official link to create IAM user https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html#id_users_create_console and search for `Creating IAM users (console)`

# Note:

  Make sure to give console access to the user and the custom password, and save the credentials to a secure location / download `.csv` file

2. Create a Group in IAM and add the created user in the group `(admin)`.

3. After creating user and adding to the admin group, add permissions `AdministratorAccess` to the group.

4. Create a unique alias to make it easy for login credentials as a IAM user.

5. Login as IAM user, using IAM credentials and generate a new password in account in `security credentials` of the IAM user.

6. Now as you are loged in, create access keys for `Command Line Interface (CLI)`, After creation download `.csv` of `Access Key ID and Secret Access Key` and store it in secure 
   location.

# Configure authentication using VS Code in Gitpod:

1. Open `AWS CloudShell` in your AWS management console and follow the instructions below:

# Note:

  Use CLI Auto-promt to auto fill the cli command by pressing `TAB`, to configure auto-prompt execute below aws cli command in your preferred terminal you want to use aws cli command:

   ``` aws --cli-auto-prompt ```

2. Execute below command as describe in the below code:
 
   ``` aws sts get-caller-identity ```

   This command gives you the UserID, Account_ID, and Arn of your Account.

# Note:

  To find more info about cli command please refer `https://docs.aws.amazon.com/cli/latest/index.html`, if you have any doubt's  regarding cli commands.

# Note:

  We could use aws cli commands in AWS CloudShell because it was already installed, but it is not installed in the Gitpod

3. Open your Git repo and click on Gitpod button.

4. Open `.gitpod.yml` file, if you don't have the `.gitpod.yml` file create a file and paste the below code:
 
```yml
vscode:
  extensions:
    - 42Crunch.vscode-openap
```

# Note:

  This code is actually installing the aws cli zip folder in workspace directory(which is a folder brfore your gitpod repo), extracting the files and install the aws cli

  ```
  # Note: IMP Linux Commands

  gp open file-name - to open file in the gitpod 

  echo $PATH - to check all the paths in your linux OS

  env - to check all the environment variables

  env | grep PATH  - "|" (Pipe command means the output of first command will go to 
                               second command, "first command" | "second command" ).
                            
                   - "grep" is a way to search something linux. 
  ```
4. You won't be able to execute commands, you have to configure access keys in gitpod

5. To congiure aws credentials you have to configure aws access key credentials you have downloaded before in `step 6` of `Create a IAM User and generate and access keys:`

6. Replace the place holder with your aws access key credentials, while executing the code below:

  ```bash
  export AWS_ACCESS_KEY_ID="YOUR_ACCESS_KEY_ID"
  export AWS_SECRET_ACCESS_KEY="YOUR_SECRET_ACCESS_KEY"
  export AWS_DEFAULT_REGION="YOUR_DEFAULT_REGION"
  ```
7. Check the environment variables are set or not by using below command:

   `` env | grep AWS_ ``

8. Check if the aws cli commands execute or not.

# Configure the ``.gitpod.yml`` file to excecute a pre-build code:

1. Update the ``.gitpod.yml`` file, paste the below code:

```yml
tasks:
  - name: aws-cli
    env:
      AWS_CLI_AUTO_PROMPT: on-partial
    init: |
      cd /workspace
      curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
      unzip awscliv2.zip
      sudo ./aws/install
      cd $THEIA_WORKSPACE_ROOT
vscode:
  extensions:
    - 42Crunch.vscode-openapi
```

# Note:

  This above code install auto-prompt, download aws cli in workspace directory(Directory above your repo), extract the aws cli files, install aws cli, and $THEIA_WORKSPACE_ROOT is an environment variable whic is mapped to the repo (aws-bootcamp-cruddur-2023023)

# Note:

  Before we commit the YAML code, we have to persist the environment variables, because we have set them temporarily. To set the environment variables permanently we have to save the environment varialbes in gitpod's special credentials

2. Execute the below commands to save the evironment variables to gitpods special credentials:

  ```
  gp env AWS_ACCESS_KEY_ID="YOUR_ACCESS_KEY_ID" 
  gp env AWS_SECRET_ACCESS_KEY="YOUR_SECRET_ACCESS_KEY" 
  gp env AWS_DEFAULT_REGION="YOUR_DEFAULT_REGION" 
  ```
3. TO check the environment variables
   - Go to [gitpod](https://www.gitpod.io/)
   - Log in to your `account`
   - Click on the `profile` 
   - Select `User Setting`
   - click on `Variables`

4. You should see your environment variables, and cross check your environment vairables.

# Note:

   Before committing in gitpod, follow the instruction below:
    - Go to [gitpod](https://www.gitpod.io/)
    - Log in to your `account`
    - Click on the `profile` 
    - Select `User Setting`
    - Click on `Integration`
    - Select `Github` and `Edit Permissions`
    - Check all the boxs 
    - Then click on `Update Permissions`

5. To commit code, first type the commit message in the left hand side below the `SOURCE CONTROL` and click on `Commit`

# Note:

  If any issues eith the VS Code the refer the https://code.visualstudio.com/docs/sourcecontrol/overview link

6. Check the `GitHub` to confirmation.

7. Close the `Gitpod` tab.

8. Open it with the `GitHub` and click on `Gitpod` button

9. You will see that `Gitpod` is executing the commands of the `.gitpod.yml` file

# Create a Billing Alarm and a Budget using CLI Commands:

 1. Type the following code to check your identity:

    ``aws sts get-caller-identity``

# Note: 

  To learn how to use aws cli commands use the following https://docs.aws.amazon.com/cli/latest/index.html link

 2. From the examples of the `budget` cli commands create two file with name `budget.json` and `budget-notifications-with-subscribers.json` following are the codes of the files:
 
    `` budget.json ``

    ```
    {
    "BudgetLimit": {
        "Amount": "1",
        "Unit": "USD"
    },
    "BudgetName": "Example Tag Budget",
    "BudgetType": "COST",
    "CostFilters": {
        "TagKeyValue": [
            "user:Key$value1",
            "user:Key$value2"
        ]
    },
    "CostTypes": {
        "IncludeCredit": true,
        "IncludeDiscount": true,
        "IncludeOtherSubscription": true,
        "IncludeRecurring": true,
        "IncludeRefund": true,
        "IncludeSubscription": true,
        "IncludeSupport": true,
        "IncludeTax": true,
        "IncludeUpfront": true,
        "UseBlended": false
    },
    "TimePeriod": {
        "Start": 1477958399,
        "End": 3706473600
    },
    "TimeUnit": "MONTHLY"
    }
    ```
    `` budget-notifications-with-subscribers.json ``

    ```
    [
    {
        "Notification": {
            "ComparisonOperator": "GREATER_THAN",
            "NotificationType": "ACTUAL",
            "Threshold": 80,
            "ThresholdType": "PERCENTAGE"
        },
        "Subscribers": [
            {
                "Address": "kk502319@gmail.com",
                "SubscriptionType": "EMAIL"
            }
        ]
    }
    ]
    ```

 3. If you want to set environment variables as your AWS_ACCOUNT_ID with your account id then type command:

    ``` export ACCOUNT_ID=$(aws sts get-caller-identity --query Account --output text) ```

    ``` export AWS_ACCOUNT_ID=$(aws sts get-caller-identity --query Account --output text) ```
 
 4. To check if you have set the environment variable type command:

    ``` env | grep ACCOUNT_ ```

 4. For the `Gitpod` to remember your AWS_ACCOUNT_ID type command:

    ``` gp env AWS_ACCOUNT_ID="YOUR_ACCOUNT_ID" ```
   
 ```Note replace the place holder with your ACCOUNT_ID```

 5. To create a budget in using cli paste the following command in your `Gitpod` terminal:

    ```
    aws budgets create-budget \
    --account-id $ACCOUNT_ID \
    --budget file://aws/json/budget.json \
    --notifications-with-subscribers file://aws/json/budget-notifications-with-subscribers.json
    ```
 
 6. Check the created budget in the `AWS Management Console` in `Budget Dashboard`

 7. To create an SNS topic type command:

    ``` aws sns create-topic --name billing-alarm ```

 8. Copy the created sns topic and paste it in the place holder

 9. To create an `SNS Subscription` type command:

    ```
    aws sns subscribe \
    --topic-arn YOUR_TOPIC_ARN \
    --protocol email \
    --notification-endpoint YOUR_EMAIL_ID
    ```

 ```Note replace the place holder with your Topic arn and your Email ID```

 10. To create an `Cloudwatch Alarm` create a file `alarm-config.json` and paste the code below:

    ```
    {
    "AlarmName": "DailyEstimatedCharges",
    "AlarmDescription": "This alarm would be triggered if the daily estimated charges exceeds 50$",
    "ActionsEnabled": true,
    "AlarmActions": [
        "YOUR_SNS_TOPIC_ARN"
    ],
    "EvaluationPeriods": 1,
    "DatapointsToAlarm": 1,
    "Threshold": 1,
    "ComparisonOperator": "GreaterThanOrEqualToThreshold",
    "TreatMissingData": "breaching",
    "Metrics": [{
        "Id": "m1",
        "MetricStat": {
            "Metric": {
                "Namespace": "AWS/Billing",
                "MetricName": "EstimatedCharges",
                "Dimensions": [{
                    "Name": "Currency",
                    "Value": "USD"
                }]
            },
            "Period": 86400,
            "Stat": "Maximum"
        },
        "ReturnData": false
    },
    {
        "Id": "e1",
        "Expression": "IF(RATE(m1)>0,RATE(m1)*86400,0)",
        "Label": "DailyEstimatedCharges",
        "ReturnData": true
    }]
    }
    

       Note replace the place holder with your SNS Topic ARN```

 11. Type the following command to create cloudwatch alarm:

    ```aws cloudwatch put-metric-alarm --cli-input-json file://aws/json/alarm-config.json```  

 12. Check the created budget in the `AWS Management Console` in `CloudWatch Dashboard`

 13. Create a `tag` and push the `tag` using the following commands:

    ```
    git tag week1
    
    git push --tags
    ```