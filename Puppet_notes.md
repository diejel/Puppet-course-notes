# Installation

## PreviousConsiderations
- Every node must point to an NTP server in order to be sync
- Set the hosts file, each record must point to the IP of the nodes
  which participates. You can use Eg:`hostnamectl set-hostname host.domain.local` 

## Master
- For CentOS based, you can use yum for adding the repository

  Eg: `$ sudo rpm -Uvh <URL>`

       `$ sudo rpm -Uvh https://yum.puppet.com/puppet7-release-el-8.noarch.rpm `

- Remember Update/Upgrade the packages on the system.

- Verify the detals of the dependencies of puppet

  Eg: `$ sudo yum list | grep -i  'puppet' `

 ```
        [osboxes@osboxes ~]$ sudo yum list | grep -i 'puppet'
        [sudo] password for osboxes: 
        puppet7-release.noarch                      7.0.0-2.el8                installed
        pdk.x86_64                                  2.2.0.0-1.el8              puppet7  
        puppet-agent.x86_64                         7.12.0-1.el8               puppet7  
        puppet-bolt.x86_64                          3.20.0-1.el8               puppet7  
        puppet-release.noarch                       1.0.0-15.el8               puppet7  
        puppetdb.noarch                             7.7.0-1.el8                puppet7  
        puppetdb-termini.noarch                     7.7.0-1.el8                puppet7  
        puppetserver.noarch                         7.4.1-1.el8                puppet7  
```
- You can now install the _agent_ and it will install other dependencies for the server.

  Eg: `$ sudo yum install puppet-agent.x86_64`
- After the step above, you can verify by doing
  
  Eg: `$ sudo rpm -qa | grep -i 'puppet' `

```
[osboxes@osboxes ~]$ sudo rpm -qa | grep -i 'puppet'
  puppet7-release-7.0.0-2.el8.noarch
  puppet-agent-7.12.0-1.el8.x86_64

```

- You can verify the installed dependencies by doing the following
  
  Eg: `$ sudo yum -qi <package_name>`

  ```
  [osboxes@osboxes ~]$ sudo rpm -qi puppet-agent 
    Name        : puppet-agent
    Version     : 7.12.0
    Release     : 1.el8
    Architecture: x86_64
    Install Date: Dom 31 Out 2021 18:58:37 EDT
    Group       : System Environment/Base
    Size        : 112870139
    License     : See components
    Signature   : RSA/SHA256, Seg 11 Out 2021 13:37:37 EDT, Key ID 4528b6cd9e61ef26
    Source RPM  : puppet-agent-7.12.0-1.el8.src.rpm
    Build Date  : Seg 11 Out 2021 13:37:08 EDT
    Build Host  : blue-disloyalty.delivery.puppetlabs.net
    Relocations : (not relocatable)
    Vendor      : Puppet Labs
    URL         : https://www.puppetlabs.com
    Summary     : The Puppet Agent package contains all of the elements needed to run puppet, including ruby, facter, and hiera.
    Description :
    The Puppet Agent package contains all of the elements needed to run puppet, including ruby, facter, and hiera.

    Contains the following components:
    cleanup
    facter 4.2.5
    hiera 3.7.0
    module-puppetlabs-augeas_core 1.1.2
    module-puppetlabs-cron_core 1.0.5
    module-puppetlabs-host_core 1.0.3
    module-puppetlabs-mount_core 1.0.4
    module-puppetlabs-scheduled_task 1.0.0
    module-puppetlabs-selinux_core 1.1.0
    module-puppetlabs-sshkeys_core 2.2.0
    module-puppetlabs-yumrepo_core 1.0.7
    module-puppetlabs-zfs_core 1.2.0
    module-puppetlabs-zone_core 1.0.3
    pl-ruby-patch
    puppet 7.12.0
    puppet-resource_api v1.8.14
    puppet-runtime 202109220
    pxp-agent 202109220
    shellpath 2015-09-18
    wrapper-script

```

## Agent