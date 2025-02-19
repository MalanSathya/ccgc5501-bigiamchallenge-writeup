# Challenge 5: Do This First!

## Challenge Statement
Deploy the CloudFoxable environment using Terraform and retrieve the first flag from the Terraform output.

## Solution
1. **Set Up AWS Environment:**
   - Create an AWS account (non-production).
   - Create an admin user with an access key.
   - Install and configure AWS CLI.
   - Verify AWS CLI with `aws sts get-caller-identity`.

2. **Install and Configure Terraform:**
   - Install Terraform and add it to the system path.
   - Clone the CloudFoxable repository:
     ```sh
     git clone https://github.com/BishopFox/cloudfoxable
     cd cloudfoxable/aws
     ```
   - Copy and edit `terraform.tfvars` to set the AWS profile:
     ```sh
     cp terraform.tfvars.example terraform.tfvars
     ```
     Edit `terraform.tfvars`:
     ```sh
     aws_local_profile = "malan9496"
     ```
   - Initialize and apply Terraform:
     ```sh
     terraform init
     terraform apply
     ```

3. **Find the First Flag:**
   - Carefully read the Terraform output.
   - Locate the flag in the format:
     ```
     FLAG{congrats_you_are_now_a_terraform_expert_happy_hunting}
     ```
   - Submit the flag to the CTFd platform.

## Reflection
* **What was your approach?**
  - Followed the setup instructions step by step.
  - Resolved dependency issues before proceeding.

* **What was the biggest challenge?**
  - Encountered dependency issues with Terraform and AWS CLI installation.
  - Faced misconfiguration of the AWS profile in `terraform.tfvars`.

* **How did you overcome the challenges?**
  - Cleared all previous configurations and reinstalled Terraform and AWS CLI.
  - Carefully followed each step from the beginning, ensuring all dependencies were installed correctly.
  - Double-checked and corrected the AWS profile configuration in Terraform.

* **What led to the breakthrough?**
  - Realizing that the AWS profile misconfiguration was the root cause of the issue.
  - Restarting from scratch allowed for a clean setup and successful deployment.

* **Lessons Learned:**
  - Ensuring proper configuration in Terraform is crucial for smooth deployment.
  - Debugging and resolving dependency issues early helps prevent roadblocks later.
  - A step-by-step verification approach helps in identifying and fixing errors efficiently.

