# Getting Started with Terraform

Terraform is the most popular language for defining and provisioning infrastructure as code (IaC). In this guide you 
will learn how to use Terraform to provision a Docker container resource from a Terraform configuration file. 

## Prerequisites 

- Terraform **version 0.12.24** or later
- [Docker Container Engine](https://docs.docker.com/install/)  

### Install Terraform 

To install Terraform, [download](https://www.terraform.io/downloads.html) the correct binary for your operating 
system and architecture. Unzip the single binary to a location in your system's PATH.

## Create Terraform configuration

In this section, you will create a Terraform configuration file and then add the configuration content. The configuration 
specifies the name of the Docker container, "training", the source image, "nginx" and other properties. 

### Create directory

Create a new directory to hold the Terraform configuration code.

```shell
$ mkdir terraform-demo
$ cd terraform-demo
```

### Create configuration file

Next, create a file named `main.tf` that will contain your Terraform configuration code.

```shell
$ touch main.tf
```

### Paste configuration 

Paste the following lines into the file and save the file.

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
## Launch the Docker resource

In the next steps, you will initialize Terraform and apply the configuration. After initialization, the `apply` command
will launch a new Docker container based on the Nginx image you specified in the configuration file. 

### terraform init

Initialize Terraform with the `init` command. The Docker Provider will be installed automatically.

```shell
$ terraform init
```

### terraform apply

After ensuring there are no errors, use the `apply` command to provision the resource. The command will take up to a few
minutes to run and will display a message indicating that the resource was created.

```shell
$ terraform apply
```

## Destroy the Docker resource

Finally, use the `destroy` command to tear down the infrastructure. When prompted for confirmation, type 
`yes` and hit ENTER for Terraform to destroy the resource. 
 
### terraform destroy

```shell
$ terraform destroy
```

## Next Steps

In this guide, you used Terraform and infrastructure as code to launch a Docker container! Using Terraform allows you 
to create reproducible and shareable configurations to provision and manage infrastructure, services or clouds. For more 
information on controlling Docker with Terraform, please see the documentation for the 
[Docker Provider](https://www.terraform.io/docs/providers/docker/index.html). Terraform offers many other providers and 
resources to deploy and manage your infrastructure. To learn more, please refer to the 
[Terraform Configuration](https://www.terraform.io/docs/configuration/index.html) documentation.
    


