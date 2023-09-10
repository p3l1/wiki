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

## Access to hosts using SOCKS5 proxy

We are using the `tor` host as a jump host to reach a third server, only reachable from `tor`.

The following two commands accomplish this by providing a SOCKS5 proxy.

```shell
ssh -f -N -L 2222:<internal_host>:22 tor
sleep 5
ssh -f -N -D 1337 user@localhost -p 2222
```

The first command establishes a connection to our jump host `tor` and forwards the local port `2222` to port `22` at `<internal_host>`.

The second command uses the forwarded SSH port on our local machine and connects via the already established SSH tunnel. Also it opens on port `1337` a SOCKS proxy.

Configure Firefox to use `localhost:1337` as a SOCKS5 proxy and also tunnel DNS requests.

Now, all our internal hosts, which are reachable from `<internal_host>`, can be accessed from Firefox by their respective URLs.
