# kubectlenv

[kubectl](https://github.com/kubernetes/kubectl) version manager inspired by (aka shamelessly stolen from) [kopsenv](https://github.com/kilna/kopsenv).

## Support

Currently kubectlenv supports the following OSes, on x86-64 bit archtecture only:

- Mac OS X
- Linux
- Windows - only tested in git-bash

## Installation

### git

1. Check out kubectlenv into any path (here is `${HOME}/.kubectlenv`)

  ```sh
  $ git clone git@github.com:PatTheSilent/kubectlenv.git ~/.kubectlenv
  ```

2. Add `~/.kubectlenv/bin` to your `$PATH` any way you like

  ```sh
  $ echo 'export PATH="$HOME/.kubectlenv/bin:$PATH"' >> ~/.bash_profile
  ```

  OR you can make symlinks for `kubectlenv/bin/*` scripts into a path that is already added to your `$PATH` (e.g. `/usr/local/bin`) `OSX/Linux Only!`

  ```sh
  $ ln -s ~/.kubectlenv/bin/* /usr/local/bin
  ```
  
  On Ubuntu/Debian touching `/usr/local/bin` might require sudo access, but you can create `${HOME}/bin` or `${HOME}/.local/bin` and on next login it will get added to the session `$PATH`
  or by running `. ${HOME}/.profile` it will get added to the current shell session's `$PATH`.
  
  ```sh
  $ mkdir -p ~/.local/bin/
  $ . ~/.profile
  $ ln -s ~/.kubectlenv/bin/* ~/.local/bin
  $ which kubectlenv
  ```

## Usage

### kubectlenv install [version]

Install a specific version of kubectl. Available options for version:

- `i.j.k` exact version to install
- `latest` is a syntax to install latest version
- `latest:<regex>` is a syntax to install latest version matching regex (used by grep -e)

```sh
$ kubectlenv install 1.10.0
$ kubectlenv install latest
$ kubectlenv install latest:^1.9
$ kubectlenv install
```

#### .kubernetes-version

If you use [.kubernetes-version](#kubernetes-version), `kubectlenv install` (no argument) will install the version written in it.


### kubectlenv use &lt;version>

Switch a version to use

`latest` is a syntax to use the latest installed version

`latest:<regex>` is a syntax to use latest installed version matching regex (used by grep -e)

```sh
$ kubectlenv use 1.10.0
$ kubectlenv use latest
$ kubectlenv use latest:^1.9
```

### kubectlenv uninstall &lt;version>

Uninstall a specific version of kubectl

`latest` is a syntax to uninstall latest version
`latest:<regex>` is a syntax to uninstall latest version matching regex (used by grep -e)

```sh
$ kubectlenv uninstall 1.10.0
$ kubectlenv uninstall latest
$ kubectlenv uninstall latest:^1.9
```

### kubectlenv list

List installed versions

```sh
% kubectlenv list
* 1.10.0 (set by /opt/kubectlenv/version)
  1.9.2
  1.9.1
  1.9.0
  1.8.1
```

### kubectlenv list-remote

List installable versions

```sh
$ kubectlenv list-remote
1.10.0
1.9.2
1.9.1
1.9.0
1.8.1
1.8.0
1.7.1
1.7.0
...
```

## .kubernetes-version

If you put `.kubernetes-version` file on your project root, or in your home directory, kubectlenv detects it and use the version written in it. If the version is `latest` or `latest:<regex>`, the latest matching version currently installed will be selected.

```sh
$ cat .kubernetes-version
1.9.2

$ kubectl version client
Version 1.9.2

$ echo 1.10.0 > .kubernetes-version

$ kubectl version client
Version 1.10.0

$ echo latest:^1.8 > .kubernetes-version

$ kubectl version client
Version 1.8.1
```

## Upgrading

```sh
$ git --git-dir=~/.kubectlenv/.git pull
```

## Uninstalling

```sh
$ rm -rf /some/path/to/kubectlenv
```

## LICENSE

[kubectlenv](https://github.com/PatTheSilent/kubectlenv/blob/master/LICENSE) - derived from: [kopsenv](https://github.com/kilna/kopsenv/blob/master/LICENSE) / [rbenv](https://github.com/rbenv/rbenv/blob/master/LICENSE)

