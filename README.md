# OpenVPN

| master | devel |
| -------- | -------- |
| [![Build Status](https://drone.osshelp.ru/api/badges/ansible/openvpn/status.svg)](https://drone.osshelp.ru/ansible/openvpn) | [![Build Status](https://drone.osshelp.ru/api/badges/ansible/openvpn/status.svg?ref=refs/heads/devel)](https://drone.osshelp.ru/ansible/openvpn) |

Simple role, which installs openvpn.

## Deploy example

``` yaml
    - role: openvpn
      easyrsa_params:
        - {key: 'export KEY_SIZE', value: '2048'}
      openvpn_params:
        - {key: max-clients, value: '20'}

```

Don't forget use iptables role for firewall rule setup:

``` yaml
## Setup on host
iptables -A POSTROUTING -s 10.8.0.0/24 -o eth0 -j MASQUERADE

## Setup in LXC
# On host

iptables -t nat -A PREROUTING -i eth$ -p udp -m udp --dport 61194 -m comment --comment "lxc-openvpn openvpn" -j DNAT --to-destination <cont_IP>:61194

# In container

iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source lxdbr0_IP_container

```

## FAQ

...

## Useful links

- [Official documentation](https://openvpn.net/community-resources/reference-manual-for-openvpn-2-4/)
- [Our article](https://oss.help/kb592)

## TODO

- Add bionic, focal support

## License

GPL3

## Author

OSSHelp Team, see <https://oss.help>
