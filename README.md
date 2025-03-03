# **EC2-AUTOMATION-WITH-TERRAFORM**

This README provides detailed steps on how to set up and automate the **EC2 Instance** using **Terraform**.

---

## **1. Install Terraform**

- Download Terraform from their website [Terraform Download](https://www.terraform.io/).
- Verify installation:
```bash
terraform -v
```

![1](https://github.com/user-attachments/assets/d57c1e31-f555-4ed0-8aef-fcb8709ef454)

---

## **2. Configure AWS Credentials**

- Terraform needs access to AWS. Setup your credentials using:
```bash
aws configure
```

![2](https://github.com/user-attachments/assets/82263952-781f-42e1-9ea8-a2c27797248f)

---

## **3. Create a Terraform Configuration File**

- Create a new directory for your Terraform project and create a file named main.tf.
```bash
mkdir terraform-ec2 && cd terraform-ec2
touch main.tf
```

![3](https://github.com/user-attachments/assets/13ef8614-9cd0-41ab-8bf2-96ad3927e5c8)

---

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

![4](https://github.com/user-attachments/assets/67d56f09-7625-49a4-acb4-25e790e0f78e)

---

## **5. Initialize Terraform**

- Run the following command to initialize Terraform:
```bash
terraform init
```

![5](https://github.com/user-attachments/assets/d889bba6-c647-4f4e-8ce2-b1070f5e3324)

---

## **6. Validate and Plan**

- heck for syntax errors and see what Terraform will create:
```bash
terraform validate
terraform plan
```

![6](https://github.com/user-attachments/assets/320856ef-395c-4056-b4c0-0fef93fd63d1)

---

## **7. Apply the Configuration**

- To create the EC2 instance, run:
```bash
terraform apply -auto-approve
```

![7](https://github.com/user-attachments/assets/988dcda5-8ef0-4241-a2e8-b585e04170f0)
![8](https://github.com/user-attachments/assets/382bdb26-76ae-424c-8ba4-10d77f817786)

---

## **8. Verify the Instance**

- Once the instance is created, you can verify it:
```bash
aws ec2 describe-instances --query 'Reservations[*].Instances[*].[InstanceId,State.Name,PublicIpAddress]' --output table
```

![9](https://github.com/user-attachments/assets/d2497593-6c30-45c2-8761-fd6c2b2dc4fc)

- Or check in the AWS Console.

![10](https://github.com/user-attachments/assets/10f02230-fde0-4f5f-951e-92cfc2ae3c29)

---

## **9. Destroy the Instance**

- If you want to delete the EC2 instance, run:
```bash
terraform destroy -auto-approve
```

![11](https://github.com/user-attachments/assets/2497b0cf-2584-457f-aa2d-baf637e7bc7e)
![12](https://github.com/user-attachments/assets/1e670c1e-c003-47b5-a173-e62ed99381e9)

---

## **10. Conclusion**

- You now have automated your EC2 instance using Terraform. With this you can create/destroy any instance you want to without opening the AWS console.
- For more advanced configurations, refer to the [Devstack Documentation](https://github.com/openstack/devstack)
