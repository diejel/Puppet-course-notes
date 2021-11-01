# Puppet Fast Course

## Previous Considerations
- Every node must point to an NTP server in order to be sync
- Set the _hosts_ file, each record must point to the IP of the nodes
  which participates. You can use Eg:
  ```
  [osboxes@puppetserver ~]$ cat /etc/hosts
    127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
    ::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
    192.168.56.101 puppetserver.example.com

  ```
  `$ sudo hostnamectl set-hostname puppetserver.example.com` 

## Master
- For CentOS based, you can use rpm for upgrading/installing the package

  Eg: `$ sudo rpm -Uvh <URL>`

       `$ sudo rpm -Uvh https://yum.puppet.com/puppet7-release-el-8.noarch.rpm `

- Remember Update/Upgrade the packages on the system.

- List puppet related package names from repositories

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
- You can now install the _server_ and it will install other dependencies as the agent.

  Eg: `$ sudo yum install puppetserver.noarch `

- After the step above, you can verify what was installed by doing
  
  Eg: `$ sudo rpm -qa | grep -i 'puppet' `

```
[osboxes@osboxes ~]$ sudo rpm -qa | grep -i 'puppet'
  puppet7-release-7.0.0-2.el8.noarch
  puppet-agent-7.12.0-1.el8.x86_64
  puppetserver-7.4.1-1.el8.noarch


```

- You can verify the installed information along with package version and short description by doing
  
  Eg: `$ sudo rpm -qi <package_name>`

  ```
  [osboxes@osboxes ~]$ sudo rpm -qi puppetserver-7.4.1-1.el8.noarch 
    Name        : puppetserver
    Version     : 7.4.1
    Release     : 1.el8
    Architecture: noarch
    Install Date: Dom 31 Out 2021 19:16:33 EDT
    Group       : System Environment/Daemons
    Size        : 76419622
    License     : ASL 2.0
    Signature   : RSA/SHA256, Sex 08 Out 2021 18:45:25 EDT, Key ID 4528b6cd9e61ef26
    Source RPM  : puppetserver-7.4.1-1.el8.src.rpm
    Build Date  : Sex 08 Out 2021 18:43:44 EDT
    Build Host  : k8s-jenkins-fpm-28wvz
    Relocations : / 
    Packager    : Puppet Labs <info@puppetlabs.com>
    Vendor      : Puppet Labs <info@puppetlabs.com>
    URL         : http://puppet.com
    Summary     : Puppet Labs puppetserver
    Description :
    Puppet Labs puppetserver
    Contains: Puppet Server (puppetlabs/puppetserver 7.4.1,org.clojure/clojure 1.10.1,org.bouncycastle/bcpkix-jdk15on 1.68,puppetlabs/jruby-utils 3.2.2,puppetlabs/puppetserver 7.4.1,puppetlabs/trapperkeeper-webserver-jetty9 4.2.1)


## Agent