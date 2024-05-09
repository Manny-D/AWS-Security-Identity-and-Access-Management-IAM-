# AWS Identity and Access Management (IAM) Security

![AWS IAM Header Logo](https://github.com/Manny-D/AWS-Security-Identity-and-Access-Management-IAM-/assets/99146530/64c5255b-957d-4136-9356-f5427f9ce4a4)

<br>

## Description 

In this project, we are a member of the cloud security team at a financial institution that utilizes AWS for various apps. They need to provide secure access to a 3rd party auditing form to review their financial reports stored in another AWS account. The financial institution wants to confirm that only authorized users can access sensitive financial data stored in an S3 bucket. To meet those requirements, we will be setting up IAM users, groups, roles amd policies. 

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

When creating a new AWS account, the intial user provsioned is the root user. It is a best practice to not use this account for daily tasks because if it gets compromised, you will likely loose access to the account, among other things! We should create another user with full admin privileges. However, for the purposes of this section of the project, we will be using the root user and will secure it with another of layer of protection by enabling AWS MFA. 

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

To align with the best security practive of least privilege, we'll create an IAM user with admin privileges. We will use this user account for the remainder of the project, instead of the root user. 

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



## 1

<details>
<summary>Details</summary>

<br>

</details>
 
<br>


## 2

<details>
<summary>Details</summary>

<br>

</details>
 
<br>
