# terraform-google-multivpc

## Description
### Tagline
This is an auto-generated module.

### Detailed
This module was generated from [terraform-google-module-template](https://github.com/terraform-google-modules/terraform-google-module-template/), which by default generates a module that simply creates a GCS bucket. As the module develops, this README should be updated.

The resources/services/activations/deletions that this module will create/trigger are:

- Create a GCS bucket with the provided name

### PreDeploy
To deploy this blueprint you must have an active billing account and billing permissions.

## Architecture
![alt text for diagram](https://www.link-to-architecture-diagram.com)
1. Architecture description step no. 1
2. Architecture description step no. 2
3. Architecture description step no. N

## Documentation
- [Hosting a Static Website](https://cloud.google.com/storage/docs/hosting-static-website)

## Deployment Duration
Configuration: X mins
Deployment: Y mins

## Cost
[Blueprint cost details](https://cloud.google.com/products/calculator?id=02fb0c45-cc29-4567-8cc6-f72ac9024add)

## Usage

Basic usage of this module is as follows:

```hcl
module "multivpc" {
  source  = "terraform-google-modules/multivpc/google"
  version = "~> 0.1"

  project_id  = "<PROJECT ID>"
  bucket_name = "gcs-test-bucket"
}
```

Functional examples are included in the
[examples](./examples/) directory.

<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| allowed\_ssh\_ip\_ranges | A list of CIDR IP ranges from which to allow ssh access | `list(string)` | `[]` | no |
| delete\_default\_internet\_gateway\_routes | If set, ensure that all routes within the network specified whose names begin with 'default-route' and with a next hop of 'default-internet-gateway' are deleted | `bool` | `false` | no |
| deployment\_name | The name of the current deployment | `string` | n/a | yes |
| enable\_iap\_rdp\_ingress | Enable a firewall rule to allow Windows Remote Desktop Protocol access using IAP tunnels | `bool` | `false` | no |
| enable\_iap\_ssh\_ingress | Enable a firewall rule to allow SSH access using IAP tunnels | `bool` | `true` | no |
| enable\_iap\_winrm\_ingress | Enable a firewall rule to allow Windows Remote Management (WinRM) access using IAP tunnels | `bool` | `false` | no |
| enable\_internal\_traffic | Enable a firewall rule to allow all internal TCP, UDP, and ICMP traffic within the network | `bool` | `true` | no |
| extra\_iap\_ports | A list of TCP ports for which to create firewall rules that enable IAP for TCP forwarding (use dedicated enable\_iap variables for standard ports) | `list(string)` | `[]` | no |
| firewall\_rules | List of firewall rules | `any` | `[]` | no |
| ips\_per\_nat | The number of IP addresses to allocate for each regional Cloud NAT (set to 0 to disable NAT) | `number` | `2` | no |
| mtu | The network MTU (default: 8896). Recommended values: 0 (use Compute Engine default), 1460 (default outside HPC environments), 1500 (Internet default), or 8896 (for Jumbo packets). Allowed are all values in the range 1300 to 8896, inclusively. | `number` | `8896` | no |
| network\_description | An optional description of this resource (changes will trigger resource destroy/create) | `string` | `""` | no |
| network\_interface\_defaults | The template of the network settings to be used on all vpcs. | <pre>object({<br>    network            = optional(string)<br>    subnetwork         = optional(string)<br>    subnetwork_project = optional(string)<br>    network_ip         = optional(string, "")<br>    nic_type           = optional(string, "GVNIC")<br>    stack_type         = optional(string, "IPV4_ONLY")<br>    queue_count        = optional(string)<br>    access_config = optional(list(object({<br>      nat_ip                 = string<br>      network_tier           = string<br>      public_ptr_domain_name = string<br>    })), [])<br>    ipv6_access_config = optional(list(object({<br>      network_tier           = string<br>      public_ptr_domain_name = string<br>    })), [])<br>    alias_ip_range = optional(list(object({<br>      ip_cidr_range         = string<br>      subnetwork_range_name = string<br>    })), [])<br>  })</pre> | <pre>{<br>  "access_config": [],<br>  "alias_ip_range": [],<br>  "ipv6_access_config": [],<br>  "network": null,<br>  "network_ip": "",<br>  "nic_type": "GVNIC",<br>  "queue_count": null,<br>  "stack_type": "IPV4_ONLY",<br>  "subnetwork": null,<br>  "subnetwork_project": null<br>}</pre> | no |
| network\_routing\_mode | The network dynamic routing mode | `string` | `"REGIONAL"` | no |
| project\_id | Project in which the HPC deployment will be created | `string` | n/a | yes |
| region | The default region for Cloud resources | `string` | n/a | yes |

## Outputs

| Name | Description |
|------|-------------|
| additional\_networks | Network interfaces for each subnetwork created by this module |
| network\_ids | IDs of the new VPC network |
| network\_names | Names of the new VPC networks |
| network\_self\_links | Self link of the new VPC network |
| subnetwork\_addresses | IP address range of the primary subnetwork |
| subnetwork\_names | Names of the subnetwork created in each network |
| subnetwork\_self\_links | Self link of the primary subnetwork |

<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->

## Requirements

These sections describe requirements for using this module.

### Software

The following dependencies must be available:

- [Terraform][terraform] v0.13
- [Terraform Provider for GCP][terraform-provider-gcp] plugin v3.0

### Service Account

A service account with the following roles must be used to provision
the resources of this module:

- Storage Admin: `roles/storage.admin`

The [Project Factory module][project-factory-module] and the
[IAM module][iam-module] may be used in combination to provision a
service account with the necessary roles applied.

### APIs

A project with the following APIs enabled must be used to host the
resources of this module:

- Google Cloud Storage JSON API: `storage-api.googleapis.com`

The [Project Factory module][project-factory-module] can be used to
provision a project with the necessary APIs enabled.

## Contributing

Refer to the [contribution guidelines](./CONTRIBUTING.md) for
information on contributing to this module.

[iam-module]: https://registry.terraform.io/modules/terraform-google-modules/iam/google
[project-factory-module]: https://registry.terraform.io/modules/terraform-google-modules/project-factory/google
[terraform-provider-gcp]: https://www.terraform.io/docs/providers/google/index.html
[terraform]: https://www.terraform.io/downloads.html

## Security Disclosures

Please see our [security disclosure process](./SECURITY.md).
