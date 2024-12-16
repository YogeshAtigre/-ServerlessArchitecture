# -ServerlessArchitecture
Repository demonstrate  Serverless Architecture implementation using AWS Lambda Function , IAM Roles and Python (Boto3) 
**Question 1 )** Automated Instance Management Using AWS Lambda and Boto3
Objective: In this assignment, you will gain hands-on experience with AWS Lambda and Boto3, Amazon's SDK for Python. You will create a Lambda function that will automatically manage EC2 instances based on their   tags.
Task: You're tasked to automate the stopping and starting of EC2 instances based on tags.

Guide :-
1) Log in to the AWS Management Console and navigate to the EC2 Dashboard
2) Launch two EC2 instances with the following configuration
3) Instance Type: t2/t3.micro (Free Tier eligible) (dpendent on selected region)
4) Tag ,Instance 1: Key: Action, Value: Auto-Stop and Instance 2: Key: Action, Value: Auto-Start
5) Now go to the IAM Dashboard and create a new role
6) Select service as Lambda ,Attach policy as AmazonEC2FullAccess.
7) Name the role appropriately 
8) Navigate to the AWS Lambda Console and create a new function
9) Select Runtime as Python 3.x
10) In execution role select the IAM role created in the previous steps
11) Add the Python Boto3 code (shared in GitHub)
12) Save and deploy the Lambda function.
13) Manually invoke the function , Go to the Lambda Console, choose the function, and click Test.
14) Use a dummy test event
15) In EC2 Dashboard verify that the instance tagged Auto-Stop should transition to the stopped state and instance tagged Auto-Start should transition to the running state.
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Question 2)** Automated S3 Bucket Cleanup Using AWS Lambda and Boto3
Objective: To gain experience with AWS Lambda and Boto3 by creating a Lambda function that will automatically clean up old files in an S3 bucket.
Task: Automate the deletion of files older than 30 days in a specific S3 bucket

Guide :-
1) Login to AWS account , from AWS management console move to navigate to the S3 Dashboard.
2) Create a New S3 Bucket
3) Provide a unique bucket name and create the bucket
4) Upload Test Files , Upload multiple files to the bucket 
5) Ensure you have files older than 30 days
6) Now Create an IAM Role for Lambda
7) Go to the IAM Dashboard → Roles → Create Role
8) Choose AWS Service → Lambda
9) Attach the AmazonS3FullAccess policy , Name the role (NOTE :  In a Production scenario, use restrictive permissions)
10) Create the Lambda Function , Go to the Lambda Dashboard → Create Function → Author from Scratch
11) Provide a function name , Choose Python 3.x as the runtime
12) Assign the IAM role  createed in setps 6 to 9
13) Add the Boto3 Script (shared in Github)
14) Save the Lambda function and deploy it
15) Go to the Test tab and create a new test event
16) Trigger the function manually
17) Verify the logs in CloudWatch Logs to ensure names of the files deleted and Confirmation that only files older than 30 days were removed
18) Go back to the S3 Dashboard , Check the target bucket to ensure that Files older than 30 days are deleted and Files newer than 30 days remain intact.

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Question 4)** Automatic EBS Snapshot and Cleanup Using AWS Lambda and Boto3
Objective: To automate the backup process for your EBS volumes and ensure that backups older than a specified retention period are cleaned up to save costs.
Task: Automate the creation of snapshots for specified EBS volumes and clean up snapshots older than 30 days.

Guide :-
1) Login to AWS account , from AWS management console move to navigate to the EC2 Dashboard.
2) Identify an existing EBS volume or create a new one by navigating to Volumes under the Elastic Block Store section.
3) Note down the Volume ID (e.g., vol-0abcd1234efgh5678) of the EBS volume you wish to back up.
4) Now we need to create a IAM role for lambda funtion
5) Navigate to the IAM dashboard → Roles → Create Role.
6) Choose AWS Service and select Lambda.
7) Attach the AmazonEC2FullAccess policy for simplicity during testing. For production, create a custom policy with the least privilege principle, allowing only CreateSnapshot and DeleteSnapshot actions.
8) Provide a Name to the role and save it 
9) Create a Lambda Function , Go to the Lambda Dashboard → Create Function → Choose Author from Scratch.
10) Provide a name and select Python 3.x as the runtime.
11) Assign the IAM role created in Steps 6 to 8.
12) Write the Lambda Script : Python boto3 script (shared in github)
13) Save and Test the Function.
NOTE :- Below mentioned steps are add for further optimization and better tracking
14) Event Source (Bonus) , Create a CloudWatch Event Rule.
15) Navigate to CloudWatch Dashboard → Rules → Create Rule.
16) Select Event Source → Schedule (e.g., cron(0 12 ? * 7 *) for weekly backups)
17) Add the Lambda function as the target.
18) Verify Results , Navigate to the EC2 Dashboard → Snapshots
19) Confirm that A new snapshot for the volume is created and Older snapshots beyond the retention period are deleted

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Question 5)**Auto-Tagging EC2 Instances on Launch Using AWS Lambda and Boto3
Objective: Learn to automate the tagging of EC2 instances as soon as they are launched, ensuring better resource tracking and management.
Task: Automatically tag any newly launched EC2 instance with the current date and a custom tag.

Guide :-
1) Login to AWS account , from AWS management console move to navigate to the IAM  Dashboard.
2) Select AWS Lambda as the trusted entity
3) Attach the AmazonEC2FullAccess policy
4) Now navigate to the Lambda Dashboard → Create a new function.
5) Select Runtime as Python 3.x	
6) Select the execution role as the IAM role created in steps 1 to 3
7) Run the Python script using Boto3 (shared in github)
8) Now navigate to CloudWatch → Rules → Create Rule
9) In Event Source: Select Event Pattern , Service Name: EC2 , Event Type: EC2 Instance State-change Notification , Specific State: running
10) Add your Lambda Function as the target
11) Save the rule and ensure it is enabled
12) Launch a new EC2 instance using the AWS Console or CLI
13) Wait for a few moments for the Lambda function to execute
14) Go to the EC2 Dashboard → Select the instance → Tags tab
15) Verify the tags
