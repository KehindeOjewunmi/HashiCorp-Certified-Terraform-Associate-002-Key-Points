# HashiCorp-Certified-Terraform-Associate-002-Key-Points

# `Directories and Modules`

Terraform treat modules as separate documents. Module calls included in the `root module` acts a link to other modules that are located either `child module` in the local directories or in external sources like the Terraform Registry.

A terraform `root module must specify required providers` in order to download required plugins to access their remote APIs

# `Dependency Lock File: .terraform.lock.hcl`

`Providers and Modules` are the external dependency that come from outside Terraform codebase.

At present, the dependency lock file `tracks only provider dependencies.` Specifying exact version constraint for module help Terraform make the same decisions again in future.

Dependency Lock File are created in the `root module of your configuration` each time you run the `terraform init` command.

You can override exisiting selected version by adding the -upgrade option when you run `terraform init -upgrade`. This will replace all of the checksum values in hashes.

Terraform uses two sources of truth: the configuration itself, and the state.

# Block Content Syntax

`image_id       = "abc123"`
`Argument name  = Argument value`
`Argument key   = Argument value`

# Nested Block Mapping

Some nested block doesn't require labels:

`lifecycle`
`timeouts`
     resource "aws_instance" "example" {
          lifecycle {
               create_before_destroy = true
          }
     }

Some nested block does require labels:

     resource "aws_instance" "example" {

          provisioner `"local-exec"` {
               command = "echo 'Hello World' >example.txt"
          }
          provisioner `"file"` {
               source      = "example.txt"
               destination = "/tmp/example.txt"
          }
          provisioner `"remote-exec"` {
               inline = ["sudo install-something -f /tmp/example.txt",]
          }
     }

# Terraform general default behavior to `configuration file` when you run `terraform apply` command

`configuration file argument supercedes state file arguments`
Create resources 
Update in-place
Destroy resources 
Destroy and re-create


# Meta-Arguments

`depends_on`

Only required when resource couldn't reference other resource from it's argument list.

`count`
It is a meta-argument for replication that accepts numerical whole number. It uses `index` as reference.

`for_each`
It is a meta-argument used to provide `distinct infrastructure object association` that accepts map or a set of strings. It uses `each.key, each.value or both as reference`.
`toset function` are used to explicitly convert a list of strings to a set ad remove duplication.

