# sshw (Fork version by codeskyblue)

ssh client wrapper for automatic login.

![usage](./assets/sshw-demo.gif)

## New added feature
- add keypath support homedir ~
- support inherit parent configuration, see feature-1


**feature-1**

support

```
- name: 5L
  user: kitty
  children:
    - name: host-can-be-ignored
      host: 127.0.0.1
```

## install

use `go get`

```
go get -u github.com/codeskyblue/sshw/cmd/sshw
```

or download binary from [releases](//github.com/codeskyblue/sshw/releases).

## config

put config file in `~/.sshw` or `~/.sshw.yml` or `~/.sshw.yaml` or `./.sshw` or `./.sshw.yml` or `./.sshw.yaml`.

config example:

```yaml
- { name: dev server fully configured, user: appuser, host: 192.168.8.35, port: 22, password: 123456 }
- { name: dev server with key path, user: appuser, host: 192.168.8.35, port: 22, keypath: /root/.ssh/id_rsa }
- { name: dev server with passphrase key, user: appuser, host: 192.168.8.35, port: 22, keypath: /root/.ssh/id_rsa, passphrase: abcdefghijklmn}
- { name: dev server without port, user: appuser, host: 192.168.8.35 }
- { name: dev server without user, host: 192.168.8.35 }
- { name: dev server without password, host: 192.168.8.35 }
- { name: ⚡️ server with emoji name, host: 192.168.8.35 }
- { name: server with alias, alias: dev, host: 192.168.8.35 }
- name: server with jump
  user: appuser
  host: 192.168.8.35
  port: 22
  password: 123456
  jump:
  - user: appuser
    host: 192.168.8.36
    port: 2222


# server group 1
- name: server group 1
  password: abc123 # set default password
  port: 22 # set default port
  # user, keypath, passphrase is also support
  children:
  - { name: server 1, user: root, host: 192.168.1.2 }
  - { name: server 2, user: root, host: 192.168.1.3 }
  - { name: server 3, user: root, host: 192.168.1.4 }

# server group 2
- name: server group 2
  children:
  - { name: server 1, user: root, host: 192.168.2.2 }
  - { name: server 2, user: root, host: 192.168.3.3 }
  - { name: server 3, user: root, host: 192.168.4.4 }
```

# callback
```
- name: dev server fully configured
  user: appuser
  host: 192.168.8.35
  port: 22
  password: 123456
  callback-shells:
  - {cmd: 2}
  - {delay: 1500, cmd: 0}
  - {cmd: 'echo 1'}
 ```
