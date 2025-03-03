# **EC2-AUTOMATION-WITH-TERRAFORM**

This README provides detailed steps on how to set up and automate the **EC2 Instance** using **Terraform**.

---

## **1. Install Terraform**

- Download Terraform from their website [Terraform Download](https://www.terraform.io/).
- Verify installation:
```bash
terraform -v
```

## **2. Configure AWS Credentials**

- Terraform needs access to AWS. Setup your credentials using:
```bash
aws configure
```

## **3. Create a Terraform Configuration File**

- Create a new directory for your Terraform project and create a file named main.tf.
```bash
mkdir terraform-ec2 && cd terraform-ec2
touch main.tf
```

## **4. Write Terraform Configuration for EC2**

- Edit main.tf and add the following configuration:
```bash
provider "aws" {
  region = "us-east-1"  # Change to your preferred region
}

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"  # Amazon Linux AMI (Check for your region)
  instance_type = "t2.micro"

  tags = {
    Name = "MyTerraformInstance"
  }
}
```

## **5. Initialize Terraform**

- Run the following command to initialize Terraform:
```bash
terraform init
```

## **6. Validate and Plan**

- heck for syntax errors and see what Terraform will create:
```bash
terraform validate
terraform plan
```

## **7. Apply the Configuration**

- To create the EC2 instance, run:
```bash
terraform apply -auto-approve
```

## **8. Verify the Instance**

- Once the instance is created, you can verify it:
```bash
aws ec2 describe-instances --query 'Reservations[*].Instances[*].[InstanceId,State.Name,PublicIpAddress]' --output table
```
- Or check in the AWS Console.

## **9. Destroy the Instance**

- If you want to delete the EC2 instance, run:
```bash
terraform destroy -auto-approve
```

## **10. Conclusion**

- You now have automated your EC2 instance using Terraform. With this you can create/destroy any instance you want to without opening the AWS console.
- For more advanced configurations, refer to the [Devstack Documentation](https://github.com/openstack/devstack)
