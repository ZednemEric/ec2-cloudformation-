# ec2-cloudformation
Cloudformation template for creating an EC2


# EC2 Instance with SSH Access - AWS CloudFormation Template

This CloudFormation template provisions an Amazon EC2 instance with SSH access enabled via a security group. It requires an existing SSH key pair to connect to the instance.

---

## 📄 Template Summary

- Launches a **t3.micro** EC2 instance using Amazon Linux 2 AMI (`ami-0b5eea76982371e91`)
- Creates a security group that allows **inbound SSH (port 22)** access from any IP
- Tags the instance as **"My CF Instance"**
- Outputs the instance ID after creation

---

## 📝 Parameters

| Parameter | Description                     | Type                         | Required |
|-----------|---------------------------------|------------------------------|----------|
| `KeyName` | Name of your existing SSH key pair in AWS | `AWS::EC2::KeyPair::KeyName` | ✅ Yes    |

> 📌 **Note**: You must create a key pair in the AWS Console or import an existing one before using this template.

---

## 🚀 Deployment Instructions

You can deploy this stack using the AWS Management Console, AWS CLI, or any Infrastructure as Code tool (e.g., AWS CDK, Terraform wrapper). Below is an example using the AWS CLI:

### Prerequisites

- AWS CLI configured with your credentials
- An existing key pair (e.g., `my-key-pair`)

### CLI Deployment

```bash
aws cloudformation create-stack \
  --stack-name ec2-ssh-instance \
  --template-body file://ec2-template.yaml \
  --parameters ParameterKey=KeyName,ParameterValue=my-key-pair \
  --capabilities CAPABILITY_NAMED_IAM
🔐 Security Consideration
This template opens port 22 to the world (0.0.0.0/0). For production environments, consider limiting the CIDR range to a specific IP or IP range for better security.

📤 Outputs
Output	Description
InstanceID	The ID of the created EC2 instance

🧹 Cleanup
To delete the stack and avoid incurring charges:

bash
Copy
Edit
aws cloudformation delete-stack --stack-name ec2-ssh-instance
📎 License
This template is provided as-is for educational or prototype use. Use at your own risk.
