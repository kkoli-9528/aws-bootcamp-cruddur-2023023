# Week 0 - Billing and Architecture

# Create a IAM User and generate and access keys:

1. Use the official link to create IAM user 'https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html#id_users_create_console' and search for 'Creating IAM users (console)'

# Note:

Make sure to give console access to the user and the custom password, and save the credentials to a secure location / download '.csv' file

2. Create a Group in IAM and add the created user in the group '(admin)'.

3. After creating user and adding to the admin group, add permissions 'AdministratorAccess' to the group.

4. Create a unique alias to make it easy for login credentials as a IAM user.

5. Login as IAM user, using IAM credentials and generate a new password in account in 'security credentials' of the IAM user.

6. Now as you are loged in, create access keys for 'Command Line Interface (CLI)', After creation download '.csv' of "Access Key ID and Secret Access Key" and store it in secure location.

# Configure authentication using VS Code in Gitpod:

1. Open 'AWS CloudShell' in your AWS management console and follow the instructions below:

# Note:

Use CLI Auto-promt to auto fill the cli command by pressing 'TAB'
, to configure auto-prompt execute below aws cli command in your preferred terminal you want to use aws cki command:

''' aws --cli-auto-prompt '''

2. Execute below command as describe in the below code:

''' aws sts get-caller-identity '''

This command gives you the UserID, Account_ID, and Arn of your Account.

# Note:

To find more info about cli command please refer https://docs.aws.amazon.com/cli/latest/index.html, if you have any doubt's  regarding cli commands.

# Note:

We could use aws cli commands in AWS CloudShell because it was already installed, but it is not installed in the Gitpod

3. Open your Git repo and click on Gitpod button.

4. Open '.gitpod.yml' file, if you don't have the '.gitpod.yml' file create a file and paste the below code:
 
'''yml
vscode:
  extensions:
    - 42Crunch.vscode-openap
'''

# Note:

This code is actually installing the aws cli zip folder in workspace directory(which is a folder brfore your gitpod repo), extracting the files and install the aws cli

'''
# Note: IMP Linux Commands

'' gp open file-name '' to open file in the gitpod 

'' echo $PATH '' to check all the paths in your linux OS

'' env '' to check all the environment variables

'' env | grep PATH '' - ''|'' (Pipe command means the output of first command will go to 
                              second command, "first command" | "second command").
                            
                       - '' grep '' is a way to search something linux. 
'''
4. You won't be able to execute commands, you have to configure access keys in gitpod

5. To congiure aws credentials you have to configure aws access key credentials you have downloaded before in 'step 6' of 'Create a IAM User and generate and access keys:'

6. Replace the place holder with your aws access key credentials, while executing the code below:

'''
export AWS_ACCESS_KEY_ID="YOUR_ACCESS_KEY_ID"
export AWS_SECRET_ACCESS_KEY="YOUR_SECRET_ACCESS_KEY"
export AWS_DEFAULT_REGION="YOUR_DEFAULT_REGION"
'''
7. Check the environment variables are set or not by using below command:

'' env | grep AWS_ ''

8. Check if the aws cli commands execute or not.

# Configure the ''.gitpod.yml'' file to excecute a pre-build code:

1. Update the ''.gitpod.yml'' file, paste the below code:

'''yml
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
'''

# Note:

This above code install auto-prompt, download aws cli in workspace directory(Directory above your repo), extract the aws cli files, install aws cli, and $THEIA_WORKSPACE_ROOT is an environment variable whic is mapped to the repo (aws-bootcamp-cruddur-2023023)

# Note:

Before we commit the YAML code, we have to persist the environment variables, because we have set them temporarily. To set the environment variables permanently we have to save the environment varialbes in gitpod's special credentials

2. Execute the below commands to save the evironment variables to gitpods special credentials:

''' 
gp env AWS_ACCESS_KEY_ID="YOUR_ACCESS_KEY_ID" 
gp env AWS_SECRET_ACCESS_KEY="YOUR_SECRET_ACCESS_KEY" 
gp env AWS_DEFAULT_REGION="YOUR_DEFAULT_REGION" 
'''
3.  TO check the environment variables
    - Go to 'gitpod' 'https://www.gitpod.io/'
    - Log in to your 'account'
    - Click on the 'profile' 
    - Select 'User Setting'
    - click on 'Variables'

4. You should see your environment variables, and cross check your environment vairables.

# Note:

    Before committing in gitpod, follow the instruction below:
    - Go to 'gitpod' 'https://www.gitpod.io/'
    - Log in to your 'account'
    - Click on the 'profile' 
    - Select 'User Setting'
    - Click on 'Integration'
    - Select 'Github' and 'Edit Permissions'
    - Check all the boxs 
    - 'Update Permissions'

5. To commit code, first type the commit message in the left hand side below the 'SOURCE CONTROL' and click on 'Commit'

# Note:

If any issues eith the VS Code the refer the ''https://code.visualstudio.com/docs/sourcecontrol/overview'' link

6. Check the ''GitHub'' to confirmation.

7. Close the 'Gitpod' tab and Open it with the 'GitHub' and click on 'Gitpod' button  




