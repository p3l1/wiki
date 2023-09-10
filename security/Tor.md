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
    User user
    Port 2222
    ProxyCommand socat STDIO SOCKS4A:127.0.0.1:%h:%p,socksport=9050
```

Access your server via the TOR network with the following command:

```bash
ssh tor
```

## Access to hosts using SOCKS5 proxy

We are using the `tor` host as a jump host to reach a third server, only reachable from `tor`.

The following command accomplishes this by providing a SOCKS5 proxy.

```shell
ssh -f -N -D 1337 tor
```

The command establishes a connection to our host `tor` and opens a SOCKS proxy on `localhost:1337` on our client machine. 
Configure Firefox to use `localhost:1337` as a SOCKS5 proxy and also tunnel DNS requests.

Now all our internal hosts, which are reachable from `tor`, can be accessed from Firefox by their respective URLs and domain names.

### Increase usability

Due to the `-f` flag the `ssh` process is running in the background. To easily control the connection were adding the following options to our `~/.ssh/config` file

```config
ControlMaster auto
ControlPersist yes
ControlPath ~/.ssh/sockets/socket-%r@tor:%p
```

When an SSH connection is established to `tor` the SSH client is opening a socket at `~/.ssh/sockets/` which gives other programs the possibility to control the connection.

We can check the status...

```shell
ssh -O check tor
```

...or close the connection

```shell
ssh -O exit tor
```
