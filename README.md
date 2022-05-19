# Simple ansible configuration for frontend and backend instances, where some docker applications are expected to work

## Requirements

| Name | Version |
|------|---------|
| ansible | >= 2.10 |
| python | 3.9 |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| LOGNAME | Main user that will have ssh access | `string` | no | yes |
| deployuser | User that will be used for deploy purposes | `string` | deploymaster | no |
| frontend_host | Frontend server name or IP | `string` | no | yes |
| backend_host | Backend server name or IP | `string` | no | yes |

## Variable definitions

Check if `LOGNAME` environment variable has been defined.
If `LOGNAME` environment variable hadn't been defined it will be needed

> echo $LOGNAME
>
> export LOGNAME=\`whoami\`

## Description

* It configures an infrastructure for typical web application
* Roles inside would configure:

    - Hostnames and hosts file
    - SSH, NTP, File2Ban, Docker services
    - Firewall rules
    - SSH access
    - Archive delivery
    - Appropriate users, permissions and dirs
    - Additional storage for backend and make it mounted as `/database`
    - Additional Redis settings for backend

## Firewall rules

* SSH access is allowed from any ip to each instance
* Web ports(80, 443) are allowed from any ip for frontend instance
* All TCP network interactions are allowed inside the local network for these ports: `2377,7946`
* All UDP network interactions are allowed inside the local network for `4789` port