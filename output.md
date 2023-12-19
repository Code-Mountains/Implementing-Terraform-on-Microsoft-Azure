## $ az account show
```
$ az account show
{
  "environmentName": "AzureCloud",
  "homeTenantId": "84f1e4ea-8554-43e1-8709-f0b8589ea118",
  "id": "9734ed68-621d-47ed-babd-269110dbacb1",
  "isDefault": true,
  "managedByTenants": [],
  "name": "P8-Real Hands-On Labs",
  "state": "Enabled",
  "tenantId": "84f1e4ea-8554-43e1-8709-f0b8589ea118",
  "user": {
    "name": "cloud_user_p_3ba19993@realhandsonlabs.com",
    "type": "user"
  }
}

```

## $ terraform init
```
$ terraform init

Initializing the backend...
Initializing modules...
Downloading registry.terraform.io/Azure/vnet/azurerm 2.7.0 for vnet-main...
- vnet-main in .terraform/modules/vnet-main

Initializing provider plugins...
- Finding hashicorp/azurerm versions matching "~> 2.0"...
- Installing hashicorp/azurerm v2.99.0...
- Installed hashicorp/azurerm v2.99.0 (signed by HashiCorp)

Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.

```

## $ terraform plan
```
$ terraform plan -var resource_group_name=main-vnet -out vnet.tfplan

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create
 <= read (data resources)

Terraform will perform the following actions:

  # azurerm_resource_group.vnet_main will be created
  + resource "azurerm_resource_group" "vnet_main" {
      + id       = (known after apply)
      + location = "eastus"
      + name     = "main-vnet"
    }

  # module.vnet-main.data.azurerm_resource_group.vnet will be read during apply
  # (depends on a resource or a module with changes pending)
 <= data "azurerm_resource_group" "vnet" {
      + id       = (known after apply)
      + location = (known after apply)
      + name     = "main-vnet"
      + tags     = (known after apply)
    }

  # module.vnet-main.azurerm_subnet.subnet[0] will be created
  + resource "azurerm_subnet" "subnet" {
      + address_prefix                                 = (known after apply)
      + address_prefixes                               = [
          + "10.0.0.0/24",
        ]
      + enforce_private_link_endpoint_network_policies = false
      + enforce_private_link_service_network_policies  = false
      + id                                             = (known after apply)
      + name                                           = "web"
      + resource_group_name                            = "main-vnet"
      + virtual_network_name                           = "main-vnet"
    }

  # module.vnet-main.azurerm_subnet.subnet[1] will be created
  + resource "azurerm_subnet" "subnet" {
      + address_prefix                                 = (known after apply)
      + address_prefixes                               = [
          + "10.0.1.0/24",
        ]
      + enforce_private_link_endpoint_network_policies = false
      + enforce_private_link_service_network_policies  = false
      + id                                             = (known after apply)
      + name                                           = "database"
      + resource_group_name                            = "main-vnet"
      + virtual_network_name                           = "main-vnet"
    }

  # module.vnet-main.azurerm_virtual_network.vnet will be created
  + resource "azurerm_virtual_network" "vnet" {
      + address_space         = [
          + "10.0.0.0/16",
        ]
      + dns_servers           = []
      + guid                  = (known after apply)
      + id                    = (known after apply)
      + location              = (known after apply)
      + name                  = "main-vnet"
      + resource_group_name   = "main-vnet"
      + subnet                = (known after apply)
      + tags                  = {
          + "costcenter"  = "it"
          + "environment" = "dev"
        }
      + vm_protection_enabled = false
    }

Plan: 4 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + vnet_id = (known after apply)

───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

Saved the plan to: vnet.tfplan

To perform exactly these actions, run the following command to apply:
    terraform apply "vnet.tfplan"
sysadmin@rancher:~/Documents/code/terraform/Implementing-Terraform-on-Microsof
```