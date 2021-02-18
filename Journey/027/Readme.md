# Variables

## Introduction

Going through the next module in the course covering variables. Variables make a Terraform plan more resusable by allowing you to specify resource properties instead of hard-coding them into the plan.

## More About Variables

Variables in Terraform are implemented in a couple of ways. First, you write a file named variables.tf that defines the different variables and their properties. For example, create a location variable that determines resources are deployed. Define the variable type (string), description, and an optional default value.

```
variable "location" {
    type = string
    description = "Azure region to deploy resources to"
    default = "westus"
}
```

Other variable types include lists, mappings, numbers, objects, and bool (true/false).

Next, there is a terraform.tfvars file. This file contains the values of the variables for your deployment. Terraform is hard-coded to look for the .tfvars file. For example, the location variable from above:

```
location = "eastus"
```

In the main.tf file, you reference the variables using "var" and the name of the variable. For example, deploying a resource group. In the name property, I use interpolation to reference the variable inside the string. The location property is a bit simpler.

```
resource "azurerm_resource_group" "rg" {
    name = "rg-webapp-prod-${var.location}-001"
    location = var.location
}
```

You can also define variables in the command line when you execute the terraform plan. You can use multiple -var="" parameters as needed.

```
terraform apply -var="location=eastus"
```

You can define environmental variables too:

```
export TF_VAR_application=terraformdemo
```

The end of the module had another challenge to continue improving the virtual machine deployment using variables. Here is my answer to the challenge:

[JeffBrownTech GitHub | terraform_learning/cloudskills_terraform-on-azure/04-Variables](https://github.com/JeffBrownTech/terraform_learning/tree/main/cloudskills_terraform-on-azure/04-Variables)

## Next Steps

Move onto the next lesson covering Modules.