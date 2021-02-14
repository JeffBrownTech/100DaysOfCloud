# State

## Introduction

Continue learning Terraform by following the next module in the course, this covered Terraform state and outputs.

## Review

Terraform state keeps track of the environment and how it was deployed, including resources and their dependencies. Terraform keeps this information in the Terraform state file (.tfstate). Terrform keeps track of changes made in the main.tf file and the changes it makes to the deployed environment.

You can modify the .tfstate file directly, but this is generally frowned upon. If you did, you can run ```terraform refresh``` to compare against the deployed resources. If there are discrepancies, the .tfstate file will be updated to reflect what is deployed.

If you made changes to the environment (like modifying a resource directly in the Azure portal), then running a refresh will update the .tfstate file. The refresh action also happens when you run the ```terraform plan``` command.

Terraform performs state locking, meaning it will lock the state file if it is in use. This prevents multiple people from making changes to the Terraform config file. You can store the .tfstate in a common storage location, like an Azure storage account. You define the Terraform state file location in the main.tf in the ```terraform``` block under "backend":

```
terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "2.40.0"
     }
  }
  backend "azurerm" {
    resource_group_name  = "{resource group name}"
    storage_account_name = "{storage account name}"
    container_name       = "{container name""
    key                  = "{example}.terraform.tfstate"
  }
}
```

Next was outputs, which output what has been created in a main.tf file and allows you to reference it in another file. You can add output blocks in the main.tf file or in separate output.tf files:

```
output "rg_name" {
    description = "resource group"
    value = azurerm_resource_group.{block name}.{property}
}
```

Referencing the output in another file using the backend data file:

```
resource "azurerm_subnet" "app_subnet" {
    name = "vnet-001"
    resource_group_name = data.terraform_remote_state.terraformdemo.outputs.rg_name
    etc...
}
```

Check out my answer to the [end-of-module challenge](https://github.com/JeffBrownTech/terraform_learning/tree/main/cloudskills_terraform-on-azure/03-State).

## Next Steps

Continue to next module in the course.