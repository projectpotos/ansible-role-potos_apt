
# Ansible Role - potos\_apt

This role provides the ability to:

- Add new apt gpg keys
- Add new apt repositories
- Install apt packages

but also:

- remove apt gpg keys by its GPG ID
- remove previously added apt repositories
- make sure certain apt packages are removed

## How to use

Usually you want to reference this role in your own Potos requirements.yml.j2 and define all the to-be-installed `apt keys`+ `apt repositories` + `apt packages` as variables [in your Potos specs](https://potos.dev/guide/specs-repo/structure.html#files-template-requirements-yml-j2).

Examples see below.

## Role Variable Defaults

There aren't default vars defined for this Role. Please have a look at our examples below or check out `default/main.yml` for even more details.

## Role Variables Examples

In this example, we're going to add the Microsoft + Google Repository GPG key's, add their repositories and install chrome + edge browser.

```yaml
---
# Example apt_key from Microsoft or Google
potos_apt_key:
  microsoft-packages:
    url: https://packages.microsoft.com/keys/microsoft.asc
    filename: microsoft-packages
  chrome-signing-key:
    url: https://dl.google.com/linux/linux_signing_key.pub
    filename: chrome-signing-key

# Example adding repository for MS Edge and Google Chrome
potos_apt_repository:
  edge:
    filename: microsoft-edge
    repo: deb [arch=amd64] https://packages.microsoft.com/repos/edge/ stable main
  chrome:
    filename: google-chrome
    repo: deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main

potos_apt_packages:
  - microsoft-edge-stable
  - google-chrome-stable
```

The other way around, you can also make sure certain apt keys IDs, repos or packages are removed. In this example, we're going to remove the Microsoft apt key by its ID, we remove the repository and the edge browser package.

Note: The GPG key ID consists of the last 16 characters. The full key signature be viewed with e.g. `gpg microsoft.asc` or run directly `gpg --list-packets microsoft.asc` to see the `keyid: `

```yaml
---
potos_apt_key_remove: 
  - EB3E94ADBE1229CF
  
potos_apt_repository_remove:
  edge:
    filename: microsoft-edge
    repo: deb [arch=amd64] https://packages.microsoft.com/repos/edge/ stable main

potos_apt_packages_remove:
  - microsoft-edge-stable
```

## Requirements

[ansible-role-potos_basics](https://github.com/projectpotos/ansible-role-potos_basics)

## License

See [LICENSE](./LICENSE)

## Author Information

[Project Potos](https://github.com/projectpotos)

