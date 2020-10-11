# Understand Terraform basics

## Handle Terraform and provider installation and versioning

### Providers

Providers are the plugins to interact with remote systems. You `must` declare a provider.

there a far more providers than the standard examples of cloud providers (aws, azure, gcp). you also have providers for things like:

- Infrastructure
  - Kubernetes
  - helm
  - docker
- networking
  - palo alto
  - cisco
  - cloudflare
- database
  - postgres
  - mysql
  - mongodb
- monitoring
  - new relic
  - data dog
  - sumo logic
  - pagerduty

### Versioning

All plugins for terraform should be versioned! Be it terraform itself, a provider, module or anything else. This gives you a consistent version being deployed and updated. Not having a version in the module or provider can result in very bad issues, with upgrades to either causing breaking changes to working code.

- example of terraform being fixed

``` c#
terraform {
  required_version = "=0.12"
}
```

- example provider using versioning

``` c#
provider "aws" {
  version = "~> 3.0"
  region  = "us-east-1"
}
```

- example module using versioning

``` c#
provider "kubernetes" {
  host                   = data.aws_eks_cluster.cluster.endpoint
  cluster_ca_certificate = base64decode(data.aws_eks_cluster.cluster.certificate_authority.0.data)
  token                  = data.aws_eks_cluster_auth.cluster.token
  load_config_file       = false
  version                = "~> 1.9"
}
```

#### version file

its possible to seperate out the providers versioning into a seperate `.tf` file. This allows you to keep the terraform code clean and easy to manage. Example below

versions.tf file

``` c#
terraform {
  required_version = ">= 0.12"

  required_providers {
    aws      = "~> 3.7.0"
    random   = "~> 2.1"
    local    = "~> 1.2"
    null     = "~> 2.1"
    template = "~> 2.1"
  }
}

```

#### Versioning Syntax

- `https://www.terraform.io/docs/configuration/version-constraints.html`

##### ~>

- ~> Allows for semver fixed upgraded at the specifc segment

``` c#
version = "~> 0.9"
```

- is equivalent to `>= 0.9, < 1.0`

``` c#
version = "~> 0.9.4"
```

- is equivalent to `>= 0.8.4, < 0.9`

##### > = < !=

- Allow from `1.20` up to `2.0.0`

``` c#
version = ">= 1.2.0, < 2.0.0"
```

### Alias

If you need to configure multiple providers. A classic example would be setting up vpc peering in aws. This needs to connect to be other requesting vpc and the accepting vpc.

example:

``` c#
provider "aws" {
  alias = "accepter"
  region = "eu-west-2"
  profile = "eks"
}

provider "aws" {
   alias = "requester"
   region = "eu-west-2"
   profile = "mgmt"
}
```

### Links

- `https://www.terraform.io/docs/configuration/providers.html`
- `https://www.terraform.io/docs/configuration/terraform.html`

## Describe plug-in based architecture

providers, modules are plugin based. for example a standard script might be something like:

- aws
  - vpc module
  - ec2 module

### Links

- `https://learn.hashicorp.com/tutorials/terraform/aws-build#initialization`

## Demonstrate using multiple providers

You can do multiple providers in terraform. Either Using the same provider with aliass (see above) or linking form diffrent providers.

### Links

- `https://learn.hashicorp.com/tutorials/terraform/aws-build#initialization`

## Describe how Terraform finds and fetches providers

- Plugins distrubuted by hasicorp are pulled down by `terraform init`
- 3rd party manual plugins can be copied into: `%APPDATA%\terraform.d\plugins` on Windows and `~/.terraform.d/plugins` on other systems.

### Links

- `https://www.terraform.io/docs/configuration/providers.html`
- `https://learn.hashicorp.com/tutorials/terraform/aws-build#initialization`

## Explain when to use and not use provisioners and when to use local-exec or remote-exec

### local-exec


### remote-exec


### Links

- `https://www.terraform.io/docs/provisioners/#provisioners-are-a-last-resort`
- `https://learn.hashicorp.com/tutorials/terraform/packer`
