# Tor

## Installation

```shell
brew install tor
# Copy config file in place
cp nano /opt/homebrew/etc/tor/torrc.sample /opt/homebrew/etc/tor/torrc
```
### Service

The TOR service needs to be running, as it provides a local SOCKS server for your programs to use.

```shell
brew services start tor
```

## SSH tunneling on macOS

On macOS the `ssh` binary is protected by the operating system and tools like `torsocks` cannot be used.

To use TOR with `ssh` add the following bit to you `~/.ssh/config

```config
Host tor
	HostName <address>.onion
    ProxyCommand socat STDIO SOCKS4A:127.0.0.1:%h:%p,socksport=9050
```

Access your server via the TOR network with the following command:

```bash
ssh user@tor
```
