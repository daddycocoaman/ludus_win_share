# Ansible Role: ludus_win_share ([Ludus](https://ludus.cloud))

An Ansible Role that creates SMB shares on Windows hosts for Ludus. This Ludus-focused role is based on [ansible.windows.win_share](https://docs.ansible.com/ansible/latest/collections/ansible/windows/win_share_module.html).

## Requirements

- Windows 8/Windows Server 2012+

## Role Variables

This role follows the same variables as  [ansible.windows.win_share](https://docs.ansible.com/ansible/latest/collections/ansible/windows/win_share_module.html)

## Dependencies

- ansible.windows

## Example Ludus Range Config

```yaml
ludus:
  - vm_name: "{{ range_id }}-ad-dc-win2022-server-x64-1"
    hostname: "{{ range_id }}-DC01-2022"
    template: win2022-server-x64-template
    vlan: 10
    ip_last_octet: 11
    ram_gb: 6
    cpus: 4
    windows:
      sysprep: true
    domain:
      fqdn: ludus.domain
      role: primary-dc
    roles:
      - daddycocoaman.ludus_win_share
    role_vars:
      win_shares:
        - name: internal
          description: top secret share
          path: C:\shares\internal
          list: false
          full: Administrators,CEO
          read: HR-Global
          deny: HR-External
        - name: company
          description: top secret share
          path: C:\shares\company
          list: true
          full: Administrators,CEO
          read: Global

```

## License

[//]: # (If you change the License type, be sure to change the actual LICENSE file as well)
GPLv3

## Author Information

This role was created by [daddycocoaman](https://github.com/daddycocoaman), for [Ludus](https://ludus.cloud/).
