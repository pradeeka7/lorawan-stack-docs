---
title: "Installing the CLI"
description: ""
weight: 1
---

This section contains instructions for installing the command-line interface.

<!--more-->

### Package managers (recommended)

#### macOS

```bash
$ brew install TheThingsNetwork/lorawan-stack/ttn-lw-stack
```

> Note: When installing with `brew`, auto-completion is enabled automatically.

#### Linux

```bash
$ sudo snap install ttn-lw-stack
$ sudo snap alias ttn-lw-stack.ttn-lw-cli ttn-lw-cli
```

> Note: When installing with `snap`, auto-completion is enabled automatically.

### Binaries

You can download [pre-built binaries](https://github.com/TheThingsNetwork/lorawan-stack/releases) for your operating system and processor architecture.

## Configuration

The command-line needs to be configured to connect to your deployment on `thethings.example.com`. You have multiple options to make the configuration file available to the CLI:

1. Environment: `export TTN_LW_CONFIG=/path/to/ttn-lw-cli.yml`
2. Command-line flag: `-c /path/to/ttn-lw-cli.yml`
3. Save as `.ttn-lw-cli.yml` in `$XDG_CONFIG_HOME`, your home directory, or the working directory.

> NOTE: When using the snap packages, `~/.ttn-lw-cli.yml` will fail with permission errors. Choose a different path.

### Generate configuration file

For a standard deployment on `thethings.example.com`, all you need is:

```bash
$ ttn-lw-cli use thethings.example.com [--fetch-ca] [--user] [--overwrite]
```

>NOTE: On Windows, use `ttn-lw-cli.exe` instead of `ttn-lw-cli`.

This will generate and save the required CLI config file. By default, the file is saved on the current directory, use the `--user` to save it under the user config directory.

If the deployment is using a CA that is not already trusted by your system, use the `--fetch-ca` flag to also connect to the server and retrieve the CA required for establishing secure communication.

> NOTE: If the file exists already, it is not overwritten and an error is printed instead. You can use `--overwrite` to overwrite the existing configuration file.

> NOTE: You can also use the `--grpc-port` and `--oauth-server-address` flags to override the default values for the gRPC port and the OAuth server address. These are not needed for standard deployments.

### Manually creating configuration file

Alternatively, you can create a file named `.ttn-lw-cli.yml` and paste the following contents:

```yaml
oauth-server-address: 'https://thethings.example.com/oauth'

identity-server-grpc-address: 'thethings.example.com:8884'
gateway-server-grpc-address: 'thethings.example.com:8884'
network-server-grpc-address: 'thethings.example.com:8884'
application-server-grpc-address: 'thethings.example.com:8884'
join-server-grpc-address: 'thethings.example.com:8884'
device-claiming-server-grpc-address: 'thethings.example.com:8884'
device-template-converter-grpc-address: 'thethings.example.com:8884'
qr-code-generator-grpc-address: 'thethings.example.com:8884'
```

If you are using an `https` port other than `443`, you need to specify that port, e.g.:

```yaml
oauth-server-address: 'https://thethings.example:8885/oauth'
```

If your deployment uses a custom certificate authority, you'll need to add:

```yaml
ca: /path/to/ca.pem
```

For advanced options, see the [Configuration Reference]({{< ref "/reference/configuration/cli" >}}).

## Auto Completion

Use `ttn-lw-cli complete` to generate an auto-completion script for the `ttn-lw-cli` command. `bash`, `zsh`, `fish` and `powershell` shells are supported:

```bash
$ ttn-lw-cli complete --shell bash --executable ttn-lw-cli > ttn-lw-cli-autocomplete
```

Source the file to enable auto-completion:

```bash
$ . ./ttn-lw-cli-autocomplete
```

Alternatively, put in a default directory so that it is loaded automatically (This directory depends on your Operating System and your shell).

For `bash`, this directory is typically `/etc/bash_completion.d/`:

```bash
$ sudo cp ./ttn-lw-cli-autocomplete /etc/bash_completion.d/
```

Generating and sourcing an auto-completion PowerShell script on Windows is slightly modified:

```bash
$ ttn-lw-cli.exe complete --shell powershell --executable ttn-lw-cli.exe > ttn-lw-cli-autocomplete.ps1

$ . ./ttn-lw-cli-autocomplete.ps1
```
