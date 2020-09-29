# Understand Terraform's purpose (vs other IaC)

## Explain multi-cloud and provider-agnostic benefits

Terraform allows you to use the same tool, design patterns and skills on multiple cloud providers. Terraform also runs on multiple hypervisors.

`https://www.terraform.io/intro/use-cases.html#multi-cloud-deployment`

## Explain the benefits of state

Terraform statefiles (.tfstate files) is a database to map the conifugration from terraform to the provider.

`https://www.terraform.io/docs/state/purpose.html`

it allows for:

- mapping to the real world
- metadata
- performance
- syncing
