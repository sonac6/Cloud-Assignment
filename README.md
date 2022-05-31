# Cloud-Assignment
I linked my aws credentials with terraform using the aws credentials through the .aws file in terraform folder that I created on my desktop.
I created main.tf and variable.tf to create a variable file for ec2 instance.
variable "instance_name" {
  description = "Value of the Name tag for the EC2 instance"
  type        = string
  default     = "ExampleAppServerInstance2"
}

I ran the terraform innit code followed by terraform plan and terraform apply.

provider "aws" {
  region = "us-west-2"
}

resource "aws_s3_bucket" "main_s3_bucket" {
  bucket = "shrishti-assignment-cloud"
  tags = {
    Name        = "shrishti-assignment-cloud"
    Environment = "Dev"
  }
}
resource "aws_instance" "app_server" {
  ami           = "ami-08d70e59c07c61a3a"
  instance_type = "t2.micro"
  tags = {
    Name = var.instance_name
  }
}
After creating the s3 bucket, the task was to delete the local state file to use S3 as a backend.
terraform {

    backend "s3"{

        bucket = "shrishti-assignment-cloud"

        key = "terraform-state.state"

        region ="us-west-2"

    }

}
This uploaded the file in S3.
