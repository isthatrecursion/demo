Step 1: Install Atom Editor
1. Open your web browser.
2. Visit the Atom Editor website mentioned in the manual: https://atom.io/
3. Download and install Atom Editor if available for your system.
4. Open the editor.
The manual uses Atom to write Terraform scripts. You can also use VS Code or Notepad.

Provision Cloud Infrastructure Using Terraform — Creating an EC2 Instance
Here is the complete step-by-step procedure for your practical, including the commands to run in Windows CMD, the Terraform code, AWS verification, and the result.
Step 1: Install the required software
Install these two tools on your Windows computer:
- Terraform: Download Terraform
- AWS CLI: Download AWS CLI for Windows
Verify the installation in Command Prompt:

terraform -version
aws --version


Step 2: Create an IAM user in AWS
1. Sign in to the AWS Management Console.
2. Search for IAM.
3. Select Users → Create user.
4. Enter a username, such as terraform-user.
5. Leave console access disabled if you only need CLI access.
6. Select Attach policies directly and choose the permissions required for your lab.
7. Create the user.
For a learning lab, AmazonEC2FullAccess is a broad permission option, but a least-privilege policy is safer.

Step 3: Generate AWS access keys
1. Select your IAM user.
2. Open Security credentials.
3. Find Access keys and click Create access key.
4. Choose Command Line Interface (CLI).
5. Follow the prompts and create the access key.
6. Securely copy the Access Key ID and Secret Access Key.
Never share your secret access key in a screenshot or chat.

Step 4: Configure AWS CLI
Open Command Prompt and run:

aws configure


Enter the following values when prompted:
Prompt	Value
AWS Access Key ID	Your IAM access key
AWS Secret Access Key	Your IAM secret key
Default region name	ap-south-1
Default output format	json

Test your credentials:

aws sts get-caller-identity --region ap-south-1


You should receive your AWS identity information. If this fails, fix the credentials or configuration before continuing.
Step 5: Create a Terraform project folder
Open CMD and run:

cd C:\Users\darsh\OneDrive\Desktop
mkdir Terraform_Script
cd Terraform_Script


If the folder already exists, don't run mkdir again. Simply enter it:

cd C:\Users\darsh\OneDrive\Desktop\Terraform_Script


Step 6: Create the Terraform configuration
1. Open Notepad:
   notepad main.tf
2. Paste this code:

provider "aws" {
  region = "ap-south-1"
}

resource "aws_instance" "myserver" {
  ami           = "ami-08e7e754b2c895da7"
  instance_type = "t2.micro"

  tags = {
    Name = "Terraform-EC2"
  }
}



3. Save the file as main.tf in the Terraform_Script folder.

Important: Confirm that ami-08e7e754b2c895da7 is a valid AMI in the Mumbai region (ap-south-1). I have not verified that specific AMI ID.
Step 7: Initialize Terraform
In CMD, make sure you are in the project folder, then run:
terraform init


Terraform downloads the AWS provider and prepares the working directory. Wait for:
Terraform has been successfully initialized!


This is the standard initialization step in the Terraform workflow. 
HashiCorp Developer+1

Step 8: Validate the configuration
Run:

terraform validate


Expected output:
Success! The configuration is valid.


If validation fails, correct the error before continuing.
Step 9: Generate the execution plan
Run:
terraform plan


Terraform previews the infrastructure changes. Review the plan and confirm that it intends to create the expected EC2 instance. 
HashiCorp Developer+1


For your current situation: Your AWS provider has been crashing with an INI parsing error. If that crash still occurs, stop here and fix your AWS configuration file before attempting to create the instance.
Step 10: Create the EC2 instance
Once terraform plan works and its output is correct, run:

terraform apply


Terraform displays the proposed changes and asks for confirmation. Type:
yes


Wait for the operation to finish. A successful run reports that the resources were added. 
HashiCorp Developer+1

Step 11: Verify the EC2 instance
1. Open the AWS EC2 Console.
2. Set the region to Asia Pacific (Mumbai) — ap-south-1.
3. Select Instances.
4. Find the instance named Terraform-EC2.
5. Check its instance ID and instance state.
The instance should appear if Terraform created it successfully.
Step 12: Destroy the instance after the experiment
When you have finished the practical, return to CMD and run:
terraform destroy


Step 14: Verify deletion in AWS
As described on page 33:
1. Open the AWS EC2 Console.
2. Navigate to Instances.
3. Refresh the instance list.
4. Check the instance created in Step 11.
5. Verify that it has been terminated or is in the process of termination.
Expected result: The EC2 instance created by Terraform is deleted.