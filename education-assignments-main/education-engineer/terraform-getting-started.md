# Getting Started with Terraform

Terraform is a tool that lets you set up cloud and on premise systems using clear and readable files. You write what you want your systems to look like, and Terraform takes care of creating them.

# Prerequisites

To install Terraform, visit [Terraform.io]([https://www.terraform.io/downloads.html]) and download the Terraform file for your operating system, such as Windows, macOS, or Linux.

New online installations of Terraform install a supported version of Docker by default. Alternatively, you can install or update Docker manually by visiting [Docker]([https://docs.docker.com/engine/install/]) and download the Docker file for your operating system, such as Windows, macOS, or Linux.

# Creating a New Directory

Now that you have Terraform installed, we will create a new folder for your project and open it using the shell.

The shell is a command line tool to run Terraform commands. The shell lets you type simple commands to create folders, move between them, and tell Terraform what to do.

```shell
$ mkdir terraform-demo
$ cd terraform-demo
```

These commands create a new folder named terraform-demo and move you into it.

# Creating a New File

Now that you are inside the folder, you can use the shell to create a new file. This file will be used for your Terraform configuration.

```shell
$ touch main.tf
```
This command creates a file called main.


# Setting Up Docker with Terraform

Next we are going to paste this code into the file. The file main is now telling Terraform to use Docker and run an NGINX container. NGINX is a simple web server that can show web pages in a browser. Terraform will download NGINX, start it, and make it available on your computer.

```hcl
terraform {
  required_providers {
    docker = {
      source = "kreuzwerker/docker"
    }
  }
}
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

# Initializing Terraform

Initialize Terraform by running the ```init``` command. This command prepares your folder for Terraform and downloads the tools it needs, such as the Docker provider. You only need to run this command once for each new project folder. This command does not install Docker. Docker must already be installed and running.

```shell
$ terraform init
```

After running the command, read the output in the shell. If you see error messages, Terraform will explain what went wrong. If the command finishes without errors, you can continue by running the ```apply``` command to create the resources.

```shell
$ terraform apply
```

The command will take up to a few minutes to run and will display a message when the resource is created.

# Destroy the Resources

To remove the resources Terraform created, use the `destroy` command. This command does not delete your files. It only removes the resources created by Terraform.

```shell
$ terraform destroy
```

Look for a message are the bottom of the output asking for confirmation. Type `yes` and hit ENTER. Terraform will destroy the resources it had created earlier.

# Next steps

In this guide, you learned how to use Terraform to create and manage resources using configuration files. This approach helps teams work consistently, reduce errors, and manage changes in a controlled way. To continue learning Terraform, explore additional tutorials and documentation on the [Hashicorp Terraform]([https://developer.hashicorp.com/terraform/docs]) documentation site. These resources build on what you’ve learned here and introduce more advanced features.

We wish you the best as you continue learning and working with Terraform!
