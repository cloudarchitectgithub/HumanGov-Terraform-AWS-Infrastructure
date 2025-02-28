## HumanGov: Deployment Of A Reusable Saas Multi-tenant AWS Infrastructure Using Terraform Modules Securely Storing Terraform Configuration Files On AWS Code Commit.

<p align="center">
<img src="https://i.imgur.com/xYskHeQ.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

## Project Description
The HumanGov Infrastructure project involves automating the provisioning and management of AWS resources using Terraform. The project is divided into three parts, each focusing on different aspects of Terraform configuration, remote state management, and integration with AWS CodeCommit for version control.

### Project Objectives:
1.	Automate Infrastructure Provisioning: Utilize Terraform to define and provision a set of AWS resources including EC2 instances, S3 buckets, and DynamoDB tables.
2.	Remote State Management: Configure Terraform to use a remote backend for state management to enhance collaboration and ensure consistent state tracking.
3.	Code Versioning with AWS CodeCommit: Store Terraform configurations in AWS CodeCommit, enabling version control and collaborative development practices.

## Project Solution
### Part 1: Terraform Configuration and Resource Provisioning
-	Define AWS Resources: Create Terraform configuration files (.tf files) to define the desired AWS infrastructure.
-	Initialize Terraform: Run terraform init to initialize the Terraform working directory and download necessary provider plugins.
-	Provision Resources: Execute terraform apply to provision the defined resources in AWS, such as EC2 instances, S3 buckets, and DynamoDB tables.

### Part 2: Remote State Management
-	Move State to Remote Backend: Configure Terraform to use an S3 bucket as a remote backend for storing the state file. This involves modifying the backend configuration in Terraform to point to the S3 bucket.
-	DynamoDB State Locking: Set up DynamoDB for state locking to prevent concurrent operations and ensure safe state management.
-	Initialize Remote State: Run terraform init to initialize the remote backend, migrating the local state file to the S3 bucket.

### Part 3: Integration with AWS CodeCommit
-	Setup Git Repository: Initialize a Git repository in the human-gov-infrastructure directory and add a .gitignore file to exclude sensitive information and temporary files.
-	Commit and Push to CodeCommit: Add the Terraform files to the local Git repository, commit the changes, and push them to AWS CodeCommit.
-	Capture Evidences: Provision the resources using Terraform and capture screenshots of the created resources (EC2 instances, S3 buckets, and DynamoDB tables). Then, destroy the resources to avoid incurring costs and capture the terraform destroy output as evidence.

## Part 1 - Terraform Multi-State Project  
### Step 1: Project Structure
•	Navigate to the human-gov-infrastructure folder and create a root directory for Terraform files.
<p align="center">
<img src="https://i.imgur.com/q2x99Yb.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

<p align="center">
<img src="https://i.imgur.com/ur8pgtY.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

### Step 2: Module Directory Creation
•	Inside the terraform directory, create a module directory for AWS HumanGov infrastructure.
<p align="center">
<img src="https://i.imgur.com/1znCfae.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

### Step 3: Module Files Creation
•	Inside the modules/aws_humangov_infrastructure directory, create the following files: variables.tf, main.tf, and outputs.tf
<p align="center">
<img src="https://i.imgur.com/E5S7pGE.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

 
•	variables.tf
<p align="center">
<img src="https://i.imgur.com/MqLp2Es.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />


•	main.tf
<p align="center">
<img src="https://i.imgur.com/fzBzxOz.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

 
•	outputs.tf
 <p align="center">
<img src="https://i.imgur.com/qiSTqrC.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />



### Step 4: Root Project File
•	Create a main.tf file in the root project directory to consume the AWS HumanGov infrastructure module.
<p align="center">
<img src="https://i.imgur.com/n7HlL2W.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

 

### Step 5: Variables File
•	Create a variables.tf file in the root project directory to define the list of states.
<p align="center">
<img src="https://i.imgur.com/CR0qISp.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

 

### Step 6: Outputs File
•	Create an outputs.tf file in the root project directory to define outputs for the entire infrastructure.
<p align="center">
<img src="https://i.imgur.com/AStKaUN.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

 


### Step 7: SSH Key
•	Create an SSH key named humangov-ec2-key and upload the private key humangov-ec2-key.pem to Cloud9 for future EC2 instance access.
<p align="center">
<img src="https://i.imgur.com/4cqQV8x.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

 

### Step 8: Terraform Commands
-	Initialize and apply the Terraform configuration.
-	terraform fmt
-	terraform init
-	terraform validate
-	terraform plan
-	terraform apply


## Part 2 - S3 Bucket and DynamoDB Table Creation
To achieve this, we begin by manually creating an S3 bucket using the AWS CLI. This bucket serves as the storage location for our Terraform state. Additionally, we set up a DynamoDB table, humangov-terraform-state-lock-table, which is crucial for state locking to prevent corruption in concurrent modifications.

### Step 1: S3 Bucket Creation 
•	Create a new S3 bucket to store the Terraform state remotely. Replace `your-unique-state-bucket-name` with a unique bucket name:
<p align="center">
<img src="https://i.imgur.com/fBf7cBo.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

 

### Step 2: DynamoDB Table Creation
<p align="center">
<img src="https://i.imgur.com/a3nV6gr.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

 
      
### Step 3: Backend Configuration
With the infrastructure in place, we now introduce a backend.tf file within the terraform directory of the human-gov-infrastructure project folder. This file holds the configuration details for the remote backend, utilizing the S3 bucket and DynamoDB table created in the previous steps.
•	backend.tf 
<p align="center">
<img src="https://i.imgur.com/cGcmZkS.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

 
This configuration instructs Terraform to use the specified S3 bucket for storing the state file (terraform.tfstate). Additionally, it utilizes the DynamoDB table for implementing state locking.


### Step 4: Verification and Testing
With the backend configuration set, we proceed to apply changes to the infrastructure using terraform apply. This step ensures the successful creation of resources in the AWS environment while simultaneously migrating the Terraform state to the designated S3 bucket.
-	Successful application of Terraform changes using terraform apply.
-	Verification of Terraform state migration by checking the contents of the S3 bucket in the AWS S3 console.
<p align="center">
<img src="https://i.imgur.com/QWpKkMo.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

 

To validate the effectiveness of state locking, we execute terraform destroy. Upon completion, we verify that the lock information is stored in the DynamoDB table. Subsequently, we observe the release of the lock after the destruction process concludes.
 <p align="center">
<img src="https://i.imgur.com/EpLuBup.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />



## Part 3 – Implementation

### Step 1: Switch to Git Working Directory
<p align="center">
<img src="https://i.imgur.com/seveVOM.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

 

### Step 2: Add .gitignore File
•	Create a .gitignore file to exclude unnecessary files from version control: 184.88.13.159
<p align="center">
<img src="https://i.imgur.com/QvOAl1G.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

 
•	Add the following entries to .gitignore:
<p align="center">
<img src="https://i.imgur.com/LotbXGg.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

 

### Step 3: Add Terraform Files to Git Repository
<p align="center">
<img src="https://i.imgur.com/LLbyYxP.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

 <p align="center">
<img src="https://i.imgur.com/EcpYacL.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

<p align="center">
<img src="https://i.imgur.com/mmtgQRL.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

<p align="center">
<img src="https://i.imgur.com/Cxr90Mc.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

### Step 4: AWS CodeCommit Repository:
-	Go to AWS CodeCommit.
-	Open "human-gov-infrastructure" repository.
-	Check Terraform folder with all files. 
 
<p align="center">
<img src="https://i.imgur.com/8BNGcW4.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

<p align="center">
<img src="https://i.imgur.com/UJYHWNQ.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />



## Conclusion

The HumanGov Infrastructure project successfully demonstrated the use of Terraform to automate the provisioning and management of AWS resources. The project was structured into three distinct phases, each focusing on different aspects of Terraform configuration, remote state management, and integration with AWS CodeCommit for version control. The implementation provided a robust and collaborative infrastructure management solution, ensuring consistency, security, and scalability.

### Challenges Encountered
1.	State Locking Issues: Encountering issues with DynamoDB state locking was a significant challenge. Resolving the ConditionalCheckFailedException required a thorough check of DynamoDB configuration and IAM permissions, ensuring that the Terraform user had the appropriate access to manage the state lock.
2.	Remote State Management: Migrating the Terraform state to an S3 bucket with DynamoDB for state locking introduced complexity. Ensuring that the state file was correctly migrated and that subsequent Terraform operations correctly referenced the remote state required careful configuration and validation.
3.	IAM Permissions: Configuring the necessary IAM permissions for Terraform to interact with AWS services securely was crucial. This included permissions for S3 bucket access, DynamoDB table operations, and EC2 instance management.
4.	Version Control Integration: Integrating Terraform configurations with AWS CodeCommit required attention to detail in setting up the .gitignore file to exclude sensitive and unnecessary files, ensuring that the repository contained only the relevant configuration files.

### Troubleshooting DynamoDB Locking Issue
1.	Check DynamoDB Configuration: Verify that the DynamoDB table specified for state locking is correctly configured.
2.	Review IAM Permissions: Ensure the Terraform user or role has the necessary permissions to perform PutItem operations on the DynamoDB table.
3.	Retry Terraform Destroy: After confirming the DynamoDB configuration and IAM permissions, retry the terraform destroy operation to successfully remove the infrastructure.

### Lessons Learned
1.	Importance of State Management: Proper state management is crucial for Terraform operations. Utilizing remote state storage and state locking mechanisms enhances collaboration and prevents state corruption.
2.	IAM Best Practices: Adhering to the principle of least privilege when configuring IAM roles and policies is essential for maintaining a secure infrastructure. Regularly reviewing and updating IAM policies helps mitigate security risks.
3.	Collaboration Through Version Control: Storing Terraform configurations in a version-controlled repository like AWS CodeCommit facilitates collaborative development and change tracking, making it easier to manage infrastructure changes over time.
4.	Troubleshooting and Debugging: Effective troubleshooting and debugging are critical skills in infrastructure management. Understanding error messages and knowing where to look for issues can save significant time and effort.

### Future Improvements
1.	Automation with CI/CD: Integrating the Terraform configurations with a CI/CD pipeline could further automate the provisioning and management of infrastructure, reducing manual intervention and increasing deployment speed.
2.	Enhanced Monitoring and Logging: Implementing enhanced monitoring and logging for the provisioned resources can provide better visibility into the infrastructure's health and performance, facilitating proactive maintenance.
3.	Security Enhancements: Continuously improving the security posture by regularly reviewing and updating security configurations, implementing encryption, and adhering to AWS security best practices.
