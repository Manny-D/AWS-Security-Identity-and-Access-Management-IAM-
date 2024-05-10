# AWS Identity and Access Management (IAM) Security

![AWS IAM Header Logo](https://github.com/Manny-D/AWS-Security-Identity-and-Access-Management-IAM-/assets/99146530/64c5255b-957d-4136-9356-f5427f9ce4a4)

<br>

## Description 

In this project, we are a member of the cloud security team at a financial institution that utilizes AWS for various apps. They need to provide secure access to a 3rd party auditing firm to review their financial reports stored in another AWS account. The financial institution wants to confirm that only authorized users can access sensitive financial data stored in an S3 bucket. To meet those requirements, we will be setting up IAM users, groups, roles and policies. 

<br>

## Create an Amazon Web Services Account

If you already have an AWS Account, skip to the next part. If not, expand <b>Details</b> below to see more.
<details>
<summary>Details</summary>
 
<br>  

If you do not already have an AWS account, navigate to the following page to create one [https://aws.amazon.com/free](https://aws.amazon.com/free) and click on either Complete Signup or Create a Free Account.

![AWS Sign Up](https://github.com/Manny-D/Virtual-Private-Cloud-VPC/assets/99146530/60c3c592-9e8a-44d5-a7c8-74284d8cdc30)

When on the <b>Contact Information</b> page, select <b>Personal</b> for the Account type.
 
![Account Type](https://github.com/Manny-D/Virtual-Private-Cloud-VPC/assets/99146530/feaadbb9-de42-4ebb-b6c0-6901c0337891)

<b>Note</b>: you will be prompted to enter in credit card info. This is for identity verification and the card will only be charged if you exceed the Free Tier limits.

![CC](https://github.com/Manny-D/Virtual-Private-Cloud-VPC/assets/99146530/d31dd4ae-82db-4079-bdd0-c69649451c52)

Next you will be prompted to confirm your identity via a SMS code, then will be taken to the <b>Select a support plan</b> page, leave it at <b>Basic support - Free</b> and click <b>Complete sign up</b>.

![Free Tier](https://github.com/Manny-D/Virtual-Private-Cloud-VPC/assets/99146530/81256aff-4cfc-4697-8334-2cef1eef592c)

Sign up completed! Click on <b>Go to the AWS Management Console</b>.

![Sign up congrats](https://github.com/Manny-D/Virtual-Private-Cloud-VPC/assets/99146530/d60ae22b-4e1d-4235-9b3d-f30a36ec67aa)

Login to the AWS Management Console using the (default) <b>Root user</b> option. 

![Root user](https://github.com/Manny-D/Virtual-Private-Cloud-VPC/assets/99146530/f25d606b-96dd-42d9-85b3-a845951d3244)
</details>

<br>

## AWS Multi-factor Authentication (MFA) for root and IAM users

<details>
<summary>Details</summary>

<br>

When creating a new AWS account, the intial user provsioned is the root user. It is a best practice to not use this account for daily tasks because if it gets compromised, you will likely loose access to the account, among other things! We should create another user with full admin privileges. However, for the purposes of this section of the project, we will continue using the root user and secure it with another of layer of protection by enabling AWS MFA. 

<br>

Start by clicking on your Account name (towards the top right) -> click on <b>Security credentials</b>:

![Security credentials](https://github.com/Manny-D/AWS-Security-Identity-and-Access-Management-IAM-/assets/99146530/8349a51b-6ca5-42aa-bb16-199ee1bfaf87)

Click <b>Assign MFA</b>:

![Assign MFA](https://github.com/Manny-D/AWS-Security-Identity-and-Access-Management-IAM-/assets/99146530/e52a2f1c-2f33-467f-bcbd-696b8065b4e3)

Enter a <b>Device name</b> - ex. AWSIAMProject

![Select MFA device](https://github.com/Manny-D/AWS-Security-Identity-and-Access-Management-IAM-/assets/99146530/c21095d3-a549-440c-98f2-db5c4b456049)

In the next section, <b>MFA device</b>, leave it at <b>Authenticator app</b> and click <b>Next</b>. 

![MFA Device](https://github.com/Manny-D/AWS-Security-Identity-and-Access-Management-IAM-/assets/99146530/d4967607-6ffa-4717-a20b-f023a315eee2)

On the <b>Set up device</b> page:

![Authenticator app](https://github.com/Manny-D/AWS-Security-Identity-and-Access-Management-IAM-/assets/99146530/34365c25-9891-4804-9dbf-48bd41596b1d)

- If you don't have an authenticator app, click on the [See a list of compatible applications](https://aws.amazon.com/iam/features/mfa/?audit=2019q1) link to obtain one.
- Click on <b>Show secret key</b> and scan the QR code that appears with the app you're using.
- The app provides codes one at a time. Enter the first one in the <b>MFA code 1</b> field.
- When it updates, enter the new one in the <b>MFA code 2</b> field.
- Press <b>Add MFA</b>. 

All set.

![My security credentials](https://github.com/Manny-D/AWS-Security-Identity-and-Access-Management-IAM-/assets/99146530/1db7ecc7-6574-4721-829d-9f836b4a81f4)

Now logout of your account, then log back in to test AWS MFA with your root user account. 

![MFA code login](https://github.com/Manny-D/AWS-Security-Identity-and-Access-Management-IAM-/assets/99146530/e79d5910-1968-4a3c-916c-7ba5608837ed)

</details>
 
<br>  

## Create an IAM user from the Console

<details>
<summary>Details</summary>

<br>

To align with the best security practice of least privilege, we will now create an IAM user with admin privileges to use for the remainder of the project, instead of the root user. 

<br>

From the AWS Console search bar, type IAM and click on <b>IAM</b>.

![IAM Service](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/a355e551-3137-43ee-bdd8-8437a58984a0)

This account doesn't have any users yet. So lets add one.

![IAM Dashboard](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/8392686f-a336-4dbc-9154-de2ccd759886)

On the left pane, under <b>Access management</b>, click on <b>Users</b> and on the next page, click on <b>Create user</b>.

![Create user](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/1fb7daef-a7d0-40c0-b1fc-6ab0f48be16b)

On the <b>Specify user details</b> page, under <b>User details</b>, do the following:

![Specifiy User Details ](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/5bfd13f7-82f4-432f-a5fd-5369476b891a)

- <b>User name</b>: <b>SecurityTeamAdmin</b>
- <b>Provide user access to to the AWS Management Console - optional</b>: tick the box
- <b>Are you providing console access to a person?</b>: tick the <b>I want to create an IAM user</b> radio button
- <b>Console password</b>: (create a password and take note of it)
- <b>User must create a new password at next sign-in - Recommended</b>: uncheck this box
     - this is a best practice and should be used under normal circumstances
- Click <b>Next</b>

<br>

On the <b>Set permissions</b> page, tick the <b>Attach policies directly</b> radio button.

![Set permissions](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/a5da3735-87e8-426c-82dd-00ec3fa5ab56)

Under <b>Permissions policies</b>, select the following:
- <b>AdministratorAccess</b>

![Admin Access](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/a16b9791-5a82-490b-af23-20961f516022)

- <b>AWSAccountManagementFullAccess</b> and <b>IAMUserChangePassword</b> (it's faster to search for and add them), then click <b>Next</b>.

![AWS Account Mgmt Full Access](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/d4266e98-c03f-4c23-afd8-8ccb0cb1f052)

Review your settings and click <b>Create user</b>.

![Review and create user](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/d37df096-e9a0-4a73-be7d-6016ed782fdc)

Once created, be sure to note the <b>Console sign-in URL</b>, as we'll be using this to login to the AWS Console moving forward.  

![User created](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/56f8c6a4-faab-4adf-81e5-2757d279fc83)

Test the login of the new IAM user to confirm it's working.

![IAM user test login](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/eca22b59-8c09-4e7d-81b2-4542eb625a6f)

Once logged in, you should notice the user name has changed (see top right of the AWS Console).

![IAM user closeup](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/b82791fb-fd66-48ad-a164-9b9a14acb0a9)

![New IAM user login](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/18437b17-96d6-45cb-952f-c69b83ce0c85)



<br>

</details>
 
<br>

## Create IAM user via the AWS CLI

<details>
<summary>Details</summary>

<br>

In this section we, will be using the AWS CLI via our own computer. For the purposes of this project, we will not cover the install process, but you can find instructions on Amazon's site located [here](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).

In order to utilize the AWS CLI, we need to create <b>Access keys</b> to send programmatic calls from our computer. 

<b>Note 1</b>: You can only have a maximum of 2 access keys at a time. <br>
<b>Note 2</b>: It's against best practice to create access keys via the root account. 

<br>

### Create Access Keys

From the AWS console, click on your login name (towards the top right) -> click on <b>Security credentials</b>.

![Security credentials 2](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/a708be3c-e955-45a9-a203-4d88f4594b22)

Scroll down to <b>Access keys</b> and click <b>Create access key</b>.

![Access keys](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/0abf5180-1181-4ef1-ac42-1c9848e96adc)

On the <b>Access key best practices & alternatives</b> page under <b>Use case</b>, do the following:
  
![Create access key](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/85a57373-fc5d-4702-9e87-e6b7d2e95aa9)

- Tick the <b>Command Line Interface (CLI)</b>.
- Put a check in <b>I understand the above recommendation and want to proceed to create an access key</b>.
- Click <b>Next</b>.

<br>

For <b>Set description tag - optional</b>, you can skip, or enter <b>For CLI access</b>, then click <b>Create access key</b>.

![Tag](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/f896c206-6bb4-433c-a34f-7382a4ed0a60)

Document both keys, as you will not be able to retrieve them after seeing them here. <br> 
You may want to download the .csv file for safe keeping. <br>
Once you have both keys saved somewhere, click <b>Done</b>. 

![Access key](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/8e3c80e8-06f5-4d9a-b4ae-191ca479eba5)

<br>

### Create Users

Open your computer's CLI and lets check to confirm the installed AWS CLI Version, enter:

```
aws --version
```

<b>Note</b>: I am using a Mac, so my screenshots are in iTerm2.

![AWS Version](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/1470e505-d9e0-4450-9da7-009a3249f54e)

To access the SecurityTeamAdmin account via the CLI, we need to configure it using the <b>Access keys</b> created above. 

```
aws configure
```

Grab those keys and in your CLI, do the following:

![aws configure](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/4a13f6bf-6ab1-4c19-a05d-1689de5c621f)

- <b>AWS Access Key ID</b> and <b>AWS Secret Access Key</b>: Copy / Paste the keys when prompted.
- <b>Default region name</b>: To check, via the AWS Console, click on the State to the left of your account and you'll see it listed.
   - eg. US East (N. Virginia) <b>us-east-1</b>
- <b>Default output [text]</b>: Type <b>text</b>

<br>

Now let's create some users! Enter the following to create a user:

```
aws iam create-user --user-name (enter username here)
```

Try the above for the users: Matt, Sarah and Deborah.

![Create users](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/c2f7f019-a9cc-43b1-8c42-fd3335838489)

Go back to the <b>AWS Console</b> in your browser to confirm they were created. Navigate to <b>IAM</b>, under <b>Access Management</b>, click on <b>Users</b>.

![User in AWS IAM Users](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/2b55cb05-e203-4671-8b28-77a6d4ab1316)

</details>
 
<br>


## Create IAM Groups / Add Users to those Groups

<details>
<summary>Details</summary>

<br>

Utilizing IAM groups allows easy management of users' permissions. Users assigned to an IAM group automatically inherit the permissions of the group. 

<br>

### Create IAM Group via the Console

From the IAM Dashboard, under <b>Access management</b> -> click on <b>User groups</b> -> click <b>Create group</b>.

![image](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/5a06eee5-e692-4652-ada4-761b183289c5)

Under <b>Name the group</b>, name it <b>AdminGroup</b> and add <b>Deborah</b> and <b>SecurityTeamAdmin</b>.

![Create user group](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/fb002267-c570-43d8-b366-2ad23fad61de)

Under <b>Attach permissions policies - Optional</b>: 

![Attach perm policies](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/5a1407c2-6b71-4276-90e8-67a0bd399f85)

- Search for / put a check mark next to the </b>AdministratorAccess Policy name</b>.
- Click <b>Create user group</b>.

<br>

Once created, click on <b>View group</b> or the <b>Group name</b> to view more details. 

![User group created](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/344b447c-f4bc-492c-aedc-0885d810c2ad)

![Group Summary](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/3c75772c-6cdd-4978-95c5-3cb372d0d3ea)

If you recall, we created Deborah via the AWS CLI, so she had no permissions assigned. 

Since we added her to a group, she should inherit the group's permissions. Click on her name to confirm.

![Deborah Summary](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/d3c2c31e-4836-46c5-98c0-4c7fe85e6808)

<br>

### Create IAM Group via AWS CLI

Let's create a group via the CLI that will have access to S3 buckets. 

First let's create the group using the following.

```
aws iam create-group --group-name CloudSecurityTeam
```

![CST creation in AWS CLI](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/e78eeccc-b249-4bd4-9f05-47bfc47affdc)

From the IAM Dashboard, under <b>Access management</b> -> <b>User groups</b> -> we should see <b>CloudSecurityTeam</b> but there are errors! 

![CloudSecurityTeam Group](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/4bbec405-25e3-4cf5-b11c-e796e08ace3f)

This is because we haven't assigned any Users nor Permissions as of yet. 

<br>

To take care of that, we'll add Matt and Sarah to that group via the AWS CLI using:

```
aws iam add-user-to-group --group-name CloudSecurityTeam --user-name (enter username here)
```

![CLI add users to CST group](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/d4d610e9-63e2-4283-9001-6fc8ec0d4b51)

Check the IAM Dashboard again under <b>Access management</b> -> <b>User groups</b> -> we should see <b>CloudSecurityTeam</b> now has 2 members.

![CST Members](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/bca38037-f687-4641-8e29-d79e29b7d842)

Click on <b>CloudSecurityTeam Group name</b> to confirm.

![CST Summary Members](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/c0706cc9-c3d9-4a63-8a1a-a60c682326dc)

<br>

Finally, we'll attach the S3 Full Access policy to this group. We need the policy's <b>Amazon Resource Name (ARN)</b>, which is the resource's unique identifier in AWS. 

To do this, go back to the IAM Dashboard and navigate to <b>Access management</b> -> <b>Policies</b> -> filter by / search for <b>S3FullAccess</b>. 

![S3 Policy](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/a6722d2a-913a-4933-8e56-99914c422369)

Click on <b>AmazonS3FullAccess</b> and copy the displayed <b>ARN</b>. 

![S3 ARN](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/dd732a6c-5613-4575-9641-03fe688f7ce6)

With that in mind, use the following command in your CLI:

```
aws iam attach-group-policy --group-name CloudSecurityTeam --policy-arn "arn:aws:iam::aws:policy/AmazonS3FullAccess"
```

![S3 ARN CLI](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/b16656af-ba2b-4941-94ee-71e8fe34982e)

Check the IAM Dashboard again under <b>Access management</b> -> <b>User groups</b> -> check the <b>CloudSecurityTeam User group</b>. You may need to refresh them.

![CST Permission assigned](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/f23d1b00-503d-4674-98ff-2ab8772a6b4a)

Click the <b>CloudSecurityTeam Group name</b> -> <b>Permissions</b> tab -> <b>Permissions policies</b>.

Confirm the <b>AmazonS3FullAccess Policy name</b> appears. You may need to refresh for it to appear.  

![CST Summary Perm Pol](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/cc27a5d1-aa9c-4360-bb56-d2124e06bdd6)

</details>

<br>

## Implementing IAM Policies

<details>
<summary>Details</summary>

<br>

<b>IAM Policies</b> define access permissions in AWS. For more granular control, you can create <b>Customer-managed</b> policies which are written in Java-Script Object Notation (JSON). If you are not familiar with JSON, you can create them via the visual editor. 

In this section, we'll be creating a <b>Customer-managed</b> policy that allows Read only for IAM.

<br>

In the IAM Dashboard under <b>Access management</b> -> click <b>Policies</b> -> <b>Create Policy</b>.

![Create policy](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/48ae69da-3b19-4877-acc4-187df4785475)

We'll utilize the <b>Visual</b> editor here. Under <b>Service</b> select <b>IAM</b>.

![Specify permissions - IAM](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/8f506c0c-d72c-4d84-9319-28ab89971071)

Under the <b>Actions allowed</b> section that appears, expand <b>Read</b> and add a check to <b>All read actions</b>.

![Access level](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/3fefd9bd-0746-4787-b191-7e3d369647e0)

In the <b>Resources</b> section that appears, we can be specific on which resource(s) we want to grant Read access to. 

![Resources - Specific](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/7d16e95d-2adf-4674-8ae8-f40c7fe38ebb)

If you're curious as to what the JSON code looks like, scroll back to the top and click on <b>JSON</b>.

![Resources - JSON ex](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/766fc13c-0d3d-4ca4-b1b4-14a9866acf29)

Click the <b>Visual</b> button again -> scroll back down to the <b>Resources</b> section -> tick the <b>All</b> radio button -> click <b>Next</b>.

![Resources - All](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/6c4821fe-2ab8-4988-86d1-f51ad6fc5d33)

On the <b>Review and create</b> page, under <b>Policy details</b>, do the following:  

![Policy - Review and create](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/a83d3ed5-b6b2-487e-a25a-9a87521d2451)

- <b>Policy name</b>: <b>IAMReadPolicy</b>
- <b>Description - optional</b>: <b>Read access to IAM</b>
- Scroll down and click on <b>Create policy</b> (not pictured)

<br>

Once created, on the <b>Policies</b> page -> click <b>Filter by Type</b> -> select <b>Customer managed</b>.

![Post Policy Creation - Filter by Type](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/4897fe30-b0ec-41ba-ab64-2f6d29a26fe0)

The <b>IAMReadPolicy</b> should be listed -> click radio button to the left of it -> click <b>Actions</b> and select Attach. 

![Action Attach](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/4c006da6-f729-4b51-82fb-6dab1f6892ab)

On the <b>Attach as a permissions policy</b> page, under <b>IAM Entities</b>, select <b>CloudSecurityTeam</b> -> click <b>Attach policy</b>

![Attach as a permissions policy](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/c0802646-68d1-4829-9b4b-3887fa103d63)

Let's confirm it was attached to the <b>CloudSecurityTeam</b> group. 

In the IAM Dashboard under <b>Access management</b> -> click <b>User groups</b> -> click <b>CloudSecurityTeam</b>.

![Confirm Policy Attached](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/e02ff7d0-6cbe-47b3-b45f-5e6a3f264c24)

Click on the <b>Permissions</b> tab. 

![IAMReadPolicy added](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/53cf6de3-394a-4961-85ac-17f571955879)

Now, in addition to the <b>AmazonS3FullAccess</b> policy added earlier, we should now see the <b>Customer-managed</b> policy (<b>IAMReadPolicy</b>) we just created / attached!

</details>

<br>

## Create and Upload to an S3 Bucket

<details>
<summary>Details</summary>

<br>

A Simple Storage Service (S3) bucket is a container for objects stored in Amazon. Any number of objects can be stored in a bucket and you can have up to 100 buckets in your account. 

<br>

From the AWS Console search bar, search for s3 and click on <b>S3</b>.

![Search S3](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/9490ee47-e6b2-4937-b3f7-2cfd9dd4cc28)

Click on <b>Create bucket</b>.

![Create bucket](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/546c85cd-7fc1-46bc-af86-3f27215453b7)

Under <b>General configuration</b>, do the following: 

![Bucket Name](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/506fa220-fd45-4a45-adcb-08c1e4526fe4)

- <b>Bucket name</b>: (enter a unique name)
- Leave all remaining section settings at their defaults
- Scroll down and click <b>Create bucket</b> (not pictured)

<br>

Once created, click on the bucket <b>Name</b>.

![S3 Bucket](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/c6849ad8-e284-4d7f-a19e-2b7567ede1d3)

Click up <b>Upload</b>.

![Upload](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/7b2f98e9-87fc-4ff2-968e-dbd2ec985818)

Click <b>Add files</b> -> select any files you want to test with.

![Add files](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/a082bf13-887f-4c6e-b589-2c52630cdb70)

Confirm your selected files are visible under <b>Files and folders</b> -> click <b>Upload</b>.

![Uploaded files](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/4eb8cd39-a2be-4045-ba57-7206efbf6dc9)

Great work!

![Upload successful](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/9f0c2956-4a9f-439f-adaf-a3a7a14de11f)

</details>

<br>

## Create an IAM Role for an AWS Service

<details>
<summary>Details</summary>

<br>

I AM Roles can be assigned to entities you trust. They have specific permissions and are valid for a short duration. So they are considered a best practice, as they provide temprary credentials that do not need to be rotated. 

<br>

Navigate back to the <b>IAM Dashboard</b>, under <b>Access management</b> -> click on <b>Roles</b> -> click <b>Create role</b>.

![Create role](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/298f997e-47b9-4157-bcd8-7a0ad51b76be)

<b>Note</b>: 2 default Roles already exist - <b>AWS ServiceRoleForSupport</b> and <b>AWSServiceRoleForTrustedAdvisor</b>.

<br>

Under <b>Trusted entity type</b>, leave the default <b>AWS service</b> ticked, as we'll be communicating between 2 AWS services. 

Scroll down to <b>Use case</b> -> select <b>EC2</b> -> scroll down and click <b>Next</b> (not shown). 

![trusted entity - EC2](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/e268d737-bd3b-47fe-ab5b-0ec409f05796)

On the <b>Add permission</b> page, under <b>Permission policies</b>, search for <b>AmazonS3FullAccess</b> -> select it -> click <b>Next</b>.

![Add Permission S3FullAccess](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/d7cc5e97-4e97-48ec-8d1e-c1dc579f9933)

This allows the EC2 service to communicate with the S3 service.

<br>

On the <b>Name, review, and create</b> page, under <b>Role details</b> do the following:

![Name review and create](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/d73f9254-97ac-45e2-9fad-999a8be5d060)

- <b>Role name</b>: <b>EC2toS3Role</b>
- <b>Description</b>: (leave the default entry)
- Scroll down and click <b>Create role</b> (not pictured)

<br>

The <b>EC2toS3Role</b> should now appear with the default ones. 

![EC2toS3Role created](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/9112dc3c-2d17-4a8d-9790-9a439aa04488)

<br> 

### Extra Credit: Attach Role to EC2 instance

We won't go through the process of spinning up an EC2 instance, as this is assumed knowledge and we'll only have it on for a short time.

Use the following settings when creating the EC2 Instance:
- <b>Name</b>: <b>List S3 buckets</b>
- <b>Key pair</b>: (create one if needed)
- All other section settings including OS and Instance type: (leave at their defaults)
- Click <b>Launch instance</b>

<br>

Once created, click on the <b>Instance ID</b> -> on the next page, click on it again to get to the <b>Instance summary</b> page. 

![List S3 Buckets EC2](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/0cba4ae0-51f6-4bdb-bae9-a776f0191aad)

To add the role, towards the top right, click on <b>Actions</b> -> <b>Security</b> -> <b>Modify IAM role</b>.

![Modify IAM role](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/0d5046dc-b7e1-48e7-b9cd-73fd1e327e87)

On the <b>Modify IAM role</b> page, under <b>IAM role</b>:

![IAM role](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/b384ac38-eaeb-4290-846a-8ca47aa78e81)

- Click on the dropdown and select the role created above -eg. <b>EC2toS3Role</b>
- Click <b>Update IAM role</b>

<br>

The <b>IAM Role</b> field should now be populated. 

![List S3 Buckets EC2 with Role](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/c247082c-e3a3-437b-8bd5-ff7ee1b9d1ee)

<br>

### Extra Credit 2: Configuring the EC2 Instance for Metadata Querying 

To prep for obtaining the metadata, click <b>Actions</b> -> <b>Instance settings</b> -> <b>Modify instance metadata options</b>.

![Metadata options](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/b75b0e00-6a53-4bdb-835c-0aea3f00c710)

On the <b>Modify instance metadata options</b> page, under <b>IMDSv2</b>, tick the <b>Optional Radio button</b> then click <b>Save</b>.

![Modify metadata options](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/21ff2cc4-d47c-4253-b2f2-f04cacb2bb1d)

Navigate back to the <b>Instance summary</b> page -> click <b>Connect</b>.

![Connect](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/ca87a647-6d16-49c0-8042-3008d1f9ea01)

On the <b>Connect to instance</b> page, leave the default settings and click on <b>Connect</b>.

![Connect to instance - EC2 role](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/efe6454f-65c2-4ab7-b645-ad6d735c63ef)

![Instance Connect - Role](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/2161f622-51a7-4926-b4cb-f37eb44fd17c)

<br>

### Extra Credit 3: Query EC2 Instance Metadata via <b>Instance Connect</b>

The EC2 Metadata that we will be querying is the information that can be used to manage or configure the existing running instance. 

The default IP address used to access metadata for all instances is <b>169.254.169.254</b>.

<br>

To start, let's test to see if we can acccess the S3 bucket we created earlier using:

```
aws s3 ls
```

It works, we can see the S3 Bucket created earlier!

![aws s3 ls](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/e90992b7-f3da-4eab-91ce-48f7892bd557)

<br>

Next, we'll query for the following:

EC2 instance metadata: 

```
curl http://169.254.169.254/latest/meta-data/
```

![Meta-data](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/e98a0f16-d288-49eb-bb96-3337295f4d58)

<br>

The public host name from the EC2 instance metadata:

```
curl http://169.254.169.254/latest/meta-data/public-hostname
```

![Public-hostname](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/ab55bc4f-2427-4f17-a6f4-0f53e521dc6f)

<br>

The instance type from the EC2 instance metadata:
```
curl http://169.254.169.254/latest/meta-data/instance-type
```

![Instance-type](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/7087c91f-0a47-48d8-94ea-88847856b310)

<br>

The IAM information from the EC2 instance metadata:

```
curl http://169.254.169.254/latest/meta-data/iam/info
```

![IAM-info](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/bff8027e-e532-4a92-82df-6e025ceb0b22)

<br>

The attached IAM role name from the EC2 instance metadata:

```
curl http://169.254.169.254/latest/meta-data/iam/securitycredentials/
```

![role-name](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/cf0f902f-6413-4c48-a020-1790a9d3fd06)

<br>

The STS security credentials for an IAM role from the EC2 instance metadata:

```
curl http://169.254.169.254/latest/meta-data/iam/securitycredentials/[enter Role name here]
```

![Security Credential for Role Name](https://github.com/Manny-D/Identity-and-Access-Management-IAM-Security/assets/99146530/052265b9-b3c3-41bc-9162-118fde8c154d)

</details>

<br>


## Placeholder

<details>
<summary>Details</summary>

<br>




</details>

<br>


## Placeholder

<details>
<summary>Details</summary>

<br>




</details>

<br>
