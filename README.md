# linux_resolvconf

This role uses the resolvconf package to manage <code>/etc/resolv.conf</code> on a Ubuntu 16.04 or Ubuntu 18.04 host. It disables management of resolv.conf by NetworkManager and dhclient on Red Hat family systems. Functionality includes ensuring nameservers, search domains, and options are present at the top of <code>/etc/resolv.conf</code>.

## Requirements

* Role uses sudo to install system packages, template system files, and manage the resolvconf, NetworkManager, and systemd services; <code>ansible_user</code> must be able to sudo to root without a password.
* Role uses apt install packages on Debian systems; apt or yum must be configured.
* Ansible magic variables are used. Facts must be available.
* This role has a molecule embedded test. Molecule must be installed in order to run the test.
## Role Variables

All over-writable variables used in this role are defined in defaults/main.yml.

The variables are grouped into sections, where the variables that are intended
to be frequently changed/overridden are defined first and variables that are 
less likely to be changed are defined last.

You can override the variables in any standard Ansible-way (e.g. group_vars,
host_vars, playbook variables, command-line, etc.).

The variables in this role inclue:

|parameter|required|default|choices|comments|
|---|---|---|---|---|
|linx_resolvconf_nameservers|false|['10.10.0.2','10.10.0.3','10.10.0.3']| |A list of strings. Each item will be added as a <code>nameserver</code> to <code>/etc/resolv.conf</code>.|
|linux_resolvconf_search|false|['domian.com', 'test.domain.com']| |A list of strings. Each item will be added to <code>search</code> in <code>/etc/resolv.conf</code>.|
|linux_resolvconf_options|false|['ndots:2', 'attempts:1', 'timeout:1', 'rotate']| |A list of strings. Each item will be added as a <code>option</code> to <code>/etc/resolv.conf</code>.|
## Dependencies


Check out the following roles to satisfy this role's requirements

|Role|Description|Source|
|---|---|---|
|ar_linux_package_sources|Sets package sources on a Linux host|https://github.com/dinohead/ar_linux_package_sources|


## Example Playbook

Apply role with role defaults
```yaml
    - hosts: servers
      roles:
         - ar_linux_resolvconf
```
Apply role and override nameservers
```yaml
    - hosts: servers
      roles:
         - { role: ar_linux_resolvconf,  
             linx_resolvconf_nameservers:{'8.8.8.8', '8.8.4.4'}
         }
```
Apply role and override all variables
```yaml
    - hosts: servers
      roles:
         - { role: ar_linux_resolvconf,  
             linx_resolvconf_nameservers:{'8.8.8.8', '8.8.4.4'},
             linx_resolvconf_search:{'mydomain.com', 'mysecretdomain.com', 'dontevergohere.com', 'dinocorn.com'},
             linx_resolvconf_options:{}
         }
```
## Author Information

|Author              |E-mail                   |
|:-------------------|:------------------------|
|Derek 'dRock' Halsey|derek.halsey@dinohead.com|

## License

MIT License

Copyright (c) 2019 Dinohead LLC

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

## Role Development Information

### Testing

### Contributing

### Git SCM
Please refer to the .gitignore file and update accordingly depending on your
development environment, etc.  The particular file was generated at 
[gitignore.io](https://www.gitignore.io/) and contains settings for the following:
  - Ansible
  - Python
  - Vim
  - Eclipse
  - IntelliJ IDEA
  - Linux
  - Windows
  
### Versioning
Please update [VERSION.md](./VERSION.md) as you release new versions of your role and try to
abide by [Semantic Versioning](http://semver.org/spec/v2.0.0.html).

### Self-contained
Please try to keep this role as self-contained as possible such that it may be
simply installed (e.g. `ansible-galaxy install`) and applied as part of a 
playbook.
