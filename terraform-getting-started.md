# Getting Started with Terraform

Build, change, and destroy Amazon Web Services (AWS) infrastructure using Terraform. Step-by-step, command-line tutorials will walk you through the Terraform basics for the first time.
## Prerequisites
To follow this tutorial, you will need:

- An AWS account
- The AWS CLI installed
- Your AWS credentials configured locally.

## Introduction to Infrastructure as Code with Terraform

Terraform is a language for defining and provisioning Infrastructure as Code (IaC) from HashiCorp. It allows you to build, change and manage infrastructure in a safe, repeatable way. Operators and Infrastructure teams can use Terraform to manage environments with a configuration language called the HashiCorp Configuration Language (HCL) for human-readable, automated deployments.

If you are new to infrastructure as code as a concept, it is the process of managing infrastructure in a file or files rather than manually configuring resources in a user interface. A resource in this instance is any piece of infrastructure in a given environment, such as a virtual machine, security group, network interface, etc.

At a high level, Terraform allows operators to use HCL to author files containing definitions of their desired resources on almost any provider (AWS, GCP, GitHub, Docker, etc.) and automates the creation of those resources at the time of apply.

## Install Terraform

To install Terraform, visit [Terraform.io](https://www.terraform.io/downloads.html) and download the applicable package for your system.

Once Terraform is installed, you can begin creating infrastructure.

## Build infrastructure

We recommend creating a new directory on your local machine and then creating the Terraform configuration code inside that directory.

### Make configuration
Create a directory terraform-demo.

```shell
$ mkdir terraform-demo
$ cd terraform-demo
```

Next, create a file for your Terraform configuration code.

```shell
$ touch main.tf
```

Paste the following lines into the file.

```hcl
provider "docker" {
    host = "unix:///var/run/docker.sock"
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.latest
  name  = "training"
  ports {
    internal = 80
    external = 80
  }
}

resource "docker_image" "nginx" {
  name = "nginx:latest"
}
```

### Initialize the directory
Initialize Terraform with the `init` command. The AWS provider will be installed. 

```shell
$ terraform init
```

### Create infrastructure
Check for any errors. If successful, provision the resource with the `apply` command.

```shell
$ terraform apply
```

The command may take a few minutes to run and when complete, will display a message indicating that the resource was created.

## Destroy infrastructure

Finally, destroy the infrastructure. This will clean up the resources you created in the previous steps.

```shell
$ terraform destroy
```

Terraform prompts for confirmation of the request. Answer `yes`. Terraform then destroys the resources it had created earlier.

## Next Steps

That concludes the getting started guide for Terraform. Hopefully, you're now able to not only see what Terraform is useful for, but you're also able to put this knowledge to use to improve building your own infrastructure.

We've covered the basics for all of these features in this guide.

As a next step, the following resources are available:

[Documentation](https://www.terraform.io/docs/index.html) - The documentation is an in-depth reference guide to all the features of Terraform, including technical details about the internals of how Terraform operates.

[Examples](https://www.terraform.io/intro/examples/index.html) - The examples have more full featured configuration files, showing some of the possibilities with Terraform.

[Modules Track](https://learn.hashicorp.com/terraform/modules/modules-overview) - Learn how to organize and re-use Terraform configuration with modules.

[Import](https://www.terraform.io/docs/import/index.html) - The import section of the documentation covers importing existing infrastructure into Terraform.

