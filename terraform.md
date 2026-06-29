## Terraform
Terraform is an open-source Infrastructure as Code (IaC) tool by HashiCorp that lets you define, provision, and manage cloud infrastructure using simple, declarative configuration files.
It works with multiple providers like AWS, Azure, GCP, Kubernetes, Docker, and more—allowing you to automate and version-control your entire infrastructure efficiently.

---

## Terraform Setup & Initialization

| Command | Description |
|--------|-------------|
| `terraform init` | Initialize a Terraform working directory and download required providers |
| `terraform init -upgrade` | Upgrade provider versions to the latest allowed |
| `terraform providers` | Show the providers required for the configuration |
| `terraform validate` | Validate Terraform code syntax and structure |
| `terraform fmt` | Format Terraform files |
| `terraform fmt -recursive` | Format `.tf` files in all subdirectories |

---

## Planning & Applying

| Command | Description |
|--------|-------------|
| `terraform plan` | Generate and show an execution plan |
| `terraform plan -out=tfplan` | Save plan to a file |
| `terraform apply` | Apply changes to reach the desired state |
| `terraform apply tfplan` | Apply saved plan |
| `terraform destroy` | Destroy all managed infrastructure |
| `terraform apply -destroy` | Preview what will be destroyed |

---

## State Management

| Command | Description |
|--------|-------------|
| `terraform state list` | List resources tracked in state |
| `terraform state show <resource>` | Show details of a state resource |
| `terraform state rm <resource>` | Remove resource from state |
| `terraform state mv <old> <new>` | Move or rename resources in state |
| `terraform refresh` | Refresh state with real infrastructure |
| `terraform import <resource> <id>` | Import existing infra into Terraform |

---

## Resource Targeting

| Command | Description |
|--------|-------------|
| `terraform plan -target=<resource>` | Plan changes for a specific resource |
| `terraform apply -target=<resource>` | Apply changes to a specific resource |

---

## Inspection & Debugging

| Command | Description |
|--------|-------------|
| `terraform show` | Show current state or saved plan |
| `terraform show -json` | Output state or plan in JSON |
| `terraform graph` | Generate dependency graph |
| `export TF_LOG=TRACE` | Enable verbose logs |
| `export TF_LOG_PATH=./tf.log` | Save logs to file |

---

## Workspace Management

| Command | Description |
|--------|-------------|
| `terraform workspace list` | List workspaces |
| `terraform workspace new <name>` | Create a workspace |
| `terraform workspace select <name>` | Switch workspace |
| `terraform workspace show` | Show current workspace |

---

## Output & Variables

| Command | Description |
|--------|-------------|
| `terraform output` | Show all outputs |
| `terraform output <name>` | Show specific output |
| `terraform output -json` | Output values in JSON |
| `terraform apply -var="key=value"` | Pass variables via CLI |
| `terraform apply -var-file="dev.tfvars"` | Use variables from file |

---

## Modules

| Command | Description |
|--------|-------------|
| `terraform get` | Download modules |
| `terraform get -update` | Update modules |
| `terraform init -upgrade` | Update providers + modules |

---

## Terraform Cloud / Backend

| Command | Description |
|--------|-------------|
| `terraform login` | Authenticate to Terraform Cloud |
| `terraform logout` | Log out from Terraform Cloud |
| `terraform init -migrate-state` | Migrate state to new backend |
| `terraform init -reconfigure` | Reinitialize backend configuration |

---

## Miscellaneous

| Command | Description |
|--------|-------------|
| `terraform version` | Show Terraform version |
| `terraform providers schema -json` | Print provider schema in JSON |
| `man terraform` | Open Terraform manual (Linux) |
