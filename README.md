# HashiCorp-Certified-Terraform-Associate-002-Key-Points

# `Directories and Modules`

Terraform treat modules as separate documents. Module calls included in the root module acts a link to other modules that are located either in the local directories or in external sources like the Terraform Registry.

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


