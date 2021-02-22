# Modules

## Introduction

Continuing to the next lesson covering modules.

## Use Case

Modules allow packaging and reusing resource configurations with Terraform. You have modules that define different resources, like a network or server. You can take these modules and plug them into a root module. This makes your code more reusable and you build configurations faster.

## Try yourself

Modules are typically stored into a folder in the root called "Modules". Each folder underneath Modules will have another folder for the specific resource module. The module name is usually formatted as "terraform-{platform}-{resource}". For example, an Azure virtual machine is "terraform-azure-server".

Like the Terraform configuration files built in previous modules, there is a main.tf file and a variables.tf file. These files define the resources being configured but are limited to a specific resource type, like a VM or network.

In the main.tf in the root folder, you then reference the module in the main.tf like so:

```
module "{module name}" {
    source = "./modules/{module folder name}"

    # Set variables, for example:
    vm_name = "vm01"
    vm_size = "Standard_B1s"

    # etc.
}
```

The variable names are defined in the module's variables.tf file.

We also looked at outputs. Outputs allow passing information between configurations. You define module outputs using a file names "outputs.tf" in the module's folder with an output block. For example, if you had a module creating network security group's (NSG), output the ID of the network security group to use in other modules. The value is the type of resource, the name of the resource block that defines it ("nsg"), and the property to output.

```
output "nsg_id" {
    description = "Network Security Group ID"
    value = azurerm_network_security_group.nsg.id
}
```

Then when referencing the NSG module, use the name of the output to reference the NSG:

```
resource "azurerm_subnet_network_security_group_association" "nsg_assoc" {
    ....
    network_security_group_id = module.nsg.nsg_id
}
```

Finally, we looked at source control for modules. Luke indicates he likes the multi-repo structure where each resource type is kept in its own repo. This way you can reference versions of that module's repo in your Terraform code.

You reference external repos in the **source** property of a module block:

```
module "storage account" {
    source = "git::https://{URL}?ref=v0.2"

    ...
}
```

The Terraform registry also has many public modules for you to use.

## Next Steps

I need to review module's a bit more as I had problem's with this module's challenge. I had to reference the solution prior to completing the challenge, and still had a few syntax things to work out. But overall a great thing to learn. The next module is covering Advanced HCL topics. This will be the last module.

[My Module 5 Challenge Solution](https://github.com/JeffBrownTech/terraform_learning/tree/main/cloudskills_terraform-on-azure/05-Modules)
