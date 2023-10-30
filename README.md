# ddnsc

Just another simple & lightweight client to update DNS dynamically. Written in golang, but originally written in python, with easy way of supporting new service providers with REST API.


- [Introduction](#introduction)
- [Requirements](#requirements)
- [Providers](#providers)
- [Installation](#installation)
  - [Arch Linux](#arch-linux)
- [Configuration](#configuration)



Introduction
------------
ddnsc is a simple program that helps update DNS dynamically. Written in golang, but originally written in in python, and runs on GNU/Linux.



Requirements
------------
- Go lang version 1.17 or higher. If your Linux package manager version of go is too old, like Debian 11 has 1.15, then install [Go Version Manager](https://github.com/moovweb/gvm) and install 1.17 or above using that tool.



Providers
---------

ddns supports following DNS providers

|     PROVIDER     |  WEBSITE                             |
|------------------|:------------------------------------:|
| CloudFlare       |  [cloudflare.com](//cloudflare.com)  |
| DuckDNS          |  [duckdns.org](//duckdns.org)        |
| Dynu             |  [dynu.net](//dynu.net)              |
| FreeDNS          |  [freedns.afraid.org](//freedns.afraid.org)              |
| LuaDNS           |  [luadns.com](//www.luadns.com)      |

Please see the [Wiki](https://github.com/shyaminayesh/ddnsc/wiki/Providers) pages to get more information on providers.


Installation
------------

ddnsc support few major linux ditribution package managers to make it easy to install. You can always install manuallly.

### Arch Linux

You can install ddnsc on Arch Linux using [AUR](//aur.archlinux.org/packages/ddnsc) package.

  ```yay -S ddnsc```



Configuration
-------------

Multiple DNS providers, domains, and hosts/subdomains are supported. The configuration file has the following format:

```
[global]
intervel=300
use=web

[example.com]
provider=LuaDNS
email=EMAIL
key=KEY
hosts=@,blah,bazz
ttl=200

[bar.com]
provider=LuaDNS
email=EMAIL
key=KEY
hosts=@,foo
ttl=600
```

The `global` section is required, and an arbitrary number of subsequent sections after that are supported where each section title is the zone/domain to update. Hosts/subdomains to update are listed under each section. The `@` denotes updating the zone/domain itself. If the `@` were omitted from the `[example.com]` section in the example above, then only the A records for blah.example.com and bazz.example.com would be updated, and the A record for `example.com` would *not* be updated.
