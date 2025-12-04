# Autossh on Windows

[Copssh client](https://itefix.net/copssh/client) versions 8.0.1 and higher support the autossh tool.

## Overview

autossh is a program to start a copy of ssh and monitor it, restarting it as necessary should it die or stop passing traffic. This is particularly useful for maintaining persistent SSH tunnels and connections.

## Getting Help

```bash
> autossh
```

Output:
```
usage: autossh [-V] [-M monitor_port[:echo_port]] [-f] [SSH_OPTIONS]

    -M specifies monitor port. May be overridden by environment
       variable AUTOSSH_PORT. 0 turns monitoring loop off.
       Alternatively, a port for an echo service on the remote
       machine may be specified. (Normally port 7.)
    -f run in background (autossh handles this, and does not
       pass it to ssh.)
    -V print autossh version and exit.
```

## Environment Variables

autossh uses environment variables to control its features:

### AUTOSSH_GATETIME
How long must an ssh session be established before we decide it really was established (in seconds). Default is 30 seconds; use of -f flag sets this to 0.

### AUTOSSH_LOGFILE
File to log to (default is to use the syslog facility).

### AUTOSSH_LOGLEVEL
Level of log verbosity.

### AUTOSSH_MAXLIFETIME
Set the maximum time to live (seconds).

### AUTOSSH_MAXSTART
Max times to restart (default is no limit).

### AUTOSSH_MESSAGE
Message to append to echo string (max 64 bytes).

### AUTOSSH_NTSERVICE
Tweak some things for running under cygrunsrv.

### AUTOSSH_PATH
Path to ssh if not default.

### AUTOSSH_PIDFILE
Write pid to this file.

### AUTOSSH_POLL
How often to check the connection (seconds).

### AUTOSSH_FIRST_POLL
Time before first connection check (seconds).

### AUTOSSH_PORT
Port to use for monitor connection.

### AUTOSSH_DEBUG
Turn logging to maximum verbosity and log to stderr.

## Version Information

```bash
> autossh -V
```

Output:
```
autossh 1.4f
```

## Example Usage

### Basic SSH Tunnel with Monitoring

```bash
autossh -M 20000 -f -N -L 8080:localhost:80 user@hostname
```

This creates a local port forward from port 8080 to port 80 on the remote host, with monitoring on ports 20000 and 20001.

### Using Remote Echo Service

```bash
autossh -M 20000:7 -f -N -L 8080:localhost:80 user@hostname
```

This uses the remote echo service (port 7) for monitoring instead of requiring two ports.

### Reverse Tunnel

```bash
autossh -M 20000 -f -N -R 2222:localhost:22 user@hostname
```

This creates a reverse tunnel, allowing connections from the remote host's port 2222 back to your local port 22.

### Without Monitoring (Using OpenSSH ServerAlive)

```bash
autossh -M 0 -o "ServerAliveInterval 30" -o "ServerAliveCountMax 3" -f -N -L 8080:localhost:80 user@hostname
```

This disables autossh's monitoring and relies on OpenSSH's ServerAlive options instead.

## See Also

- [autossh man page](autossh-man-page.md)
- [Copssh client homepage](https://itefix.net/copssh/client)
