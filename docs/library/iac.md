# IaC

<div class="grid" markdown>

??? abstract "Lifecycle Management"
    ??? question "terraform init"
        Initializes a working directory containing Terraform configuration files.
    ??? question "terraform plan"
        Creates an execution1 plan, showing what changes Terraform will make.
    ??? question "terraform apply"
        Executes the actions proposed in a Terraform plan.
    ??? question "terraform destroy"
        Destroys Terraform-managed infrastructure.
??? abstract "State Management"
    ??? question "terraform state list"
        Lists resources currently tracked in the Terraform state.
    ??? question "terraform state show <address>"
        Shows the attributes of a specific resource in the state.
    ??? question "terraform state mv <from-address> <to-address>"
        Moves an item in the state to a new address.
    ??? question "terraform state rm <address>"
        Removes an item from the state.
    ??? question "terraform state pull"
        Downloads the state file from the remote backend.
    ??? question "terraform state push <path>"
        Uploads a local state file to the remote backend.
??? abstract "Formatting and Validation"
    ??? question "terraform fmt"
        Reformats Terraform configuration files to a canonical style.
    ??? question "terraform validate"
        Validates the syntax of Terraform configuration files.
??? abstract "Module Management"
    ??? question "terraform get"
        Downloads and updates modules defined in the configuration.
    ??? question "terraform providers"
        Displays information about the providers used in the current configuration.
??? abstract "Workspace Management"
    ??? question "terraform workspace list"
        Lists existing Terraform workspaces.
    ??? question "terraform workspace show"
        Shows the currently selected workspace.
    ??? question "terraform workspace select <name>"
        Selects an existing workspace.
    ??? question "terraform workspace new <name>"
        Creates a new workspace.
    ??? question "terraform workspace delete <name>"
        Deletes a workspace.
??? abstract "Output and Import"
    ??? question "terraform output"
        Shows the output values from the Terraform state.
    ??? question "terraform import <address> <id>"
        Imports an existing resource into Terraform management.
??? abstract "Other Useful Commands"
    ??? question "terraform version"
        Shows the installed Terraform version.
    ??? question "terraform console"
        Opens an interactive console for evaluating Terraform expressions.
    ??? question "terraform taint <address>"
        Marks a resource as tainted, forcing its replacement on the next apply.
    ??? question "terraform untaint <address>"
        Removes the tainted status from a resource.
    ??? question "terraform debug"
        Enables debug logging.
</div>
