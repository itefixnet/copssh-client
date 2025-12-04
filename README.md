# Copssh client - OpenSSH for Windows

Copssh client is a barebone distribution of OpenSSH client for Windows. It provides a self-contained environment with OpenSSH client, ssh-copy-id, autossh, and required utilities already included, offering everything you need to initiate ssh/sftp requests from your Windows computer.

If you need to serve ssh/sftp requests (run an SSH server on Windows), check out [Copssh server](https://itefix.net/copssh/server).

## Features

- **Complete OpenSSH client implementation**: Full-featured OpenSSH client for Windows
- **ssh-copy-id tool**: Easy public key distribution to remote servers (versions 8.0+)
- **autossh support**: Automatic SSH session monitoring and restart (versions 8.0.1+)
- **sftp client**: Secure file transfer protocol client for file transfers
- **ssh-keygen**: Generate and manage SSH key pairs (RSA, DSA, ECDSA, Ed25519)
- **Bash shell**: Integrated bash environment for scripting
- **Bundled dependencies**: Includes OpenSSH, Cygwin runtime, and utilities
- **Portable**: Unzip and run, no installation or system modifications required
- **Wide compatibility**: Works on Windows Vista and newer

## Requirements

- Windows Vista or later
- No external dependencies required — all components included in the package

## Download

Latest releases of Copssh client are available on GitHub:

https://github.com/itefixnet/copssh-client/releases

Each release includes:
- The complete Copssh client ZIP package (OpenSSH, bash, Cygwin runtime)
- Release notes and version history

## Basic Usage

1. Unzip the downloaded archive

2. Use OpenSSH commands directly:
   ```
   bin\ssh user@hostname
   bin\sftp user@hostname
   bin\ssh-keygen -t ed25519 -f mykey
   ```

3. For interactive bash session (optional):
   ```
   bin\bash --login
   ```

### ssh-copy-id Usage (versions 8.0+)

Transfer your public key to a remote server:

```bash
# Create a key pair
ssh-keygen -t ed25519 -f test

# Transfer the public key (dry run to test)
ssh-copy-id -n -i ./test user@hostname

# Transfer the public key
ssh-copy-id -i ./test user@hostname
```

### autossh Usage (versions 8.0.1+)

Automatically monitor and restart SSH sessions:

```bash
# Basic usage with monitoring
autossh -M 20000 -f -N -L 8080:localhost:80 user@hostname

# Check version
autossh -V
```

Copssh client is tested successfully with various SSH servers. You should test and verify that it works for your specific needs.

## Documentation

Additional guides and man pages are available in the [docs](docs/) folder:

- [ssh-copy-id Guide](docs/ssh-copy-id-guide.md) - Complete guide to using ssh-copy-id on Windows
- [ssh-copy-id Man Page](docs/ssh-copy-id-man-page.md) - Full manual page for ssh-copy-id
- [autossh Guide](docs/autossh-guide.md) - Complete guide to using autossh on Windows
- [autossh Man Page](docs/autossh-man-page.md) - Full manual page for autossh

## Links

- **Copssh client homepage**: https://itefix.net/copssh/client
- **Copssh client repository**: https://github.com/itefixnet/copssh-client
- **Copssh server** (paid solution for SSH/SFTP server on Windows): https://itefix.net/copssh/server
- **ssh-copy-id guide**: https://itefix.net/content/ssh-copy-id-tool-windows
- **autossh guide**: https://itefix.net/content/autossh-windows
- **OpenSSH homepage**: https://www.openssh.com/

## Support

Support and issue tracking are handled via GitHub Issues:

https://github.com/itefixnet/copssh-client/issues

## License

Copssh client is licensed under the BSD 2-Clause License. See LICENSE file for details.
