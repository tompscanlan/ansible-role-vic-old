# ansible-role-vic

Install and manage [vSphere Integrated Containers](https://github.com/vmware/vic/)

## Requirements

Currently only runs on linux hosts, though the vic-machine binaries can support OSX and Windows

## Role Variables

### Defaults are reasonable, so no need to change any of these:

specific version of VIC to install and run'

    vic_version: "1.1.0"

Where VIC files will be installed

    vic_install_path: /opt

Generally shouldn't need to update this, any VIC version found at this version ought to be usable

    vic_download_url: "https://bintray.com/vmware/vic/download_file?file_path=vic_{{ vic_version }}.tar.gz"

Temporary storage for downloads

    vic_tmp: /tmp

Validate certs for the url we download vic from?

    vic_download_validate_certs: False


### Change these to create/delete VIC Container Hosts

List of of vic hosts create.
Each key/value pair will be passed to the vic-machine create as-is, so
any configuration supported by [vic-machine](https://github.com/vmware/vic/blob/master/doc/user/usage.md)
should be supported here

#### Example, create a vch
```yamlex
vic_controller_hosts:
  - name: test
    timeout: 5m
    target: https://vcenter.corp.local/Goddard
    user: administrator@home.local
    password: 'some_password'
    tls-cname: test1.home.local
    image-store: esx-a-ssd
    bridge-network: bridge-vic1
    compute-resource: BasementLab
    thumbprint: "29:03:72:8B:73:ED:D8:B6:D7:36:E8:EE:4F:1D:91:DE:9A:2C:3D:4A"
    bridge-network-range: 172.16.0.0/12
    management-network: Management
    management-network-gateway: 0.0.0.0/0:192.168.1.254
    management-network-ip: 192.168.1.19/24
    dns-server: 192.168.1.1
    public-network: VMNet
    organization: tscanlan
    volume-store: "esx-a-ssd/test1-volumes:default"
```

List of of vic hosts delete
each key/value pair will be passed to the vic-machine create as-is, so
any configuration supported by [vic-machine delete](https://github.com/vmware/vic/blob/master/doc/user/usage.md#deleting-a-virtual-container-host)
should be supported here

#### Example, delete two vch
```yamlex
vic_controller_hosts_delete:
  - name: test3
    timeout: 5m
    target: https://vcenter.corp.local/Goddard
    user: administrator@home.local
    password: 'some_password'
    thumbprint: "29:03:72:8B:73:ED:D8:B6:D7:36:E8:EE:4F:1D:91:DE:9A:2C:3D:4A"
  - name: test4
    timeout: 5m
    target: https://vcenter.corp.local/Goddard
    user: administrator@home.local
    password: 'some_password'
    thumbprint: "29:03:72:8B:73:ED:D8:B6:D7:36:E8:EE:4F:1D:91:DE:9A:2C:3D:4A"
```

## Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yamlex
- hosts: all
  roles:
    - role: vic
  vars:
    vic_controller_hosts:
      - name: test1
        timeout: 5m
        target: https://192.168.1.9/Goddard
        user: administrator@home.local
        password: 'some_password'
        tls-cname: test1.home.local
        image-store: esx-a-ssd
        bridge-network: bridge-vic1
        compute-resource: BasementLab
        thumbprint: "29:03:72:8B:73:ED:D8:B6:D7:36:E8:EE:4F:1D:91:DE:9A:2C:3D:4A"
        bridge-network-range: 172.16.0.0/12
        management-network: Management
        management-network-gateway: 0.0.0.0/0:192.168.1.254
        management-network-ip: 192.168.1.19/24
        dns-server: 192.168.1.1
        public-network: VMNet
        organization: tscanlan
        volume-store: "esx-a-ssd/test1-volumes:default"
       
```

## License

Copyright © 2017 VMware, Inc. All Rights Reserved.
SPDX-License-Identifier: MIT


## Author Information

Tom Scanlan
<tscanlan@vmware.com>
