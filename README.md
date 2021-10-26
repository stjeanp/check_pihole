# check_pihole
## Nagios plugin to monitor Pi-hole internals

check_pihole is a small python script that is used to monitor Pi-hole internal status. It makes it possible to use Nagios to keep an eye on the output of `pihole status` and `pihole -v`, alerting you if there's an issue with FTL not listening or if blocking is disabled, as well as if there are pending updates.

It must be run on the Pi-hole instance itself, as those are local commands. You can specify the `-s` flag to tell it to use sudo, provided you have set your sudoers file up correctly.

## Usage

```
usage: check_pihole [-h] [-s]

Check Pi-hole

optional arguments:
  -h, --help  show this help message and exit
  -s          Use sudo to run commands
```

## Installation

1. Copy the file to your Nagios plugins directory
2. Set the ownership and permissions appropriately
3. Configure nrpe (or whatever remote execution daemon you're using) to run it.
4. Test remote execution from your Nagios server
5. Update the Pi-hole host definition to check it.

### Example Nagios service definition

```
define service {
    use                     local-service
    host_name               pihole
    service_description     Pi-hole status
    check_command           check_nrpe!check_pihole
}
```

### Example nrpe config

```
command[check_pihole]=/usr/lib/nagios/plugins/check_pihole
```
